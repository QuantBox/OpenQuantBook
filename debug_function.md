#  如何调试一个策略

---

 简单的策略调试可以在代码中使用Console.WriteLine\(\)输出调试信息。如果需要高级调试功能可以通过Visual Studio来进行， OpenQuant的策略工程是一个标准的Visual Studio解决方案，可以使用Visual Studio打开、运行、调试OpenQuant的策略。需要注意的是由于运行环境的变化，当需要在Visual Studio中开发调试策略时要对策略项目配置进行一些调整：

修改策略项目中的场景工程\(Backtest、Realtime、Optimization\)的程序集信息，需要将信息中的公司属性设置成” SmartQuant Ltd。

![](/assets/debug_function01.png)

![](/assets/debug_function02.png)

修改工程生成属性，将工程编译64位程序。注意要同时修改Debug和Release两种配置方式。

![](/assets/debug_function03.png)

在Visual Studio中运行调试策略时，默认配置下策略程序并不生成在OpenQuant的安装目录，这就带来了策略引用的模块无法找到的问题，有两种方式解决这个问题：  


* 将策略工程的输出目录改成OpenQuant的安装目录，由于OpenQuant安装在C:\Program Files\目录下，在这个目录下输出程序需要以管理员身份运行Visual Studio。

![](/assets/debug_function04.png)

*  修改Program.cs在Main入口函数中添加OpenQuantOutside.Init 函数调用。这个函数可以解决策略程序在OpenQuant安装目录外运行时遇到的问题。

```
class Program
{
    static void Main(string[] args)
    {
        OpenQuantOutside.Init();
        var scenario = new BacktestScenario(Framework.Current);
        scenario.Run();
    }
}
```
OpenQuantOutside 类的源代码如下：

```
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.IO;
using System.Reflection;
using System.Threading;
using Microsoft.Win32;
using System.Linq;

namespace SmartQuant
{
    public class OpenQuantOutside
    {
        private static readonly string SmartQuantPath;

        private static string GetSmartQuantPath()
        {
            var key = Registry.LocalMachine.OpenSubKey(@"SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\{C224DA18-4901-433D-BD94-82D28B640B2C}");
            if (key != null) {
                var names = new List<string>(key.GetSubKeyNames());
                names.Sort();
                return key.GetValue("InstallLocation").ToString();
            }
            return Directory.GetParent(Path.GetDirectoryName(Assembly.GetEntryAssembly().Location)).FullName;
        }

        private static Assembly DomainOnAssemblyResolve(object sender, ResolveEventArgs args)
        {
            var assemblyName = new AssemblyName(args.Name);
            var path = Path.Combine(SmartQuantPath, assemblyName.Name + ".dll");
            if (File.Exists(path)) {
                return Assembly.LoadFile(path);
            }
            Console.WriteLine(@"Not Found: " + assemblyName.Name);
            return null;
        }

        private static void OpenFileServer()
        {
            var file = Path.Combine(SmartQuantPath, "FileServer.exe");
            if (Process.GetProcessesByName("FileServer").Length == 0) {
                try {
                    Process.Start(new ProcessStartInfo {
                        UseShellExecute = false,
                        FileName = file,
                        WindowStyle = ProcessWindowStyle.Hidden,
                        CreateNoWindow = true,
                        Arguments = "-auto"
                    });
                    new EventWaitHandle(false, EventResetMode.AutoReset, "DataFileServerHandle").WaitOne();
                }
                catch (Exception ex) {
                    Console.WriteLine(string.Concat("Framework::Init Can not start ", file, " ", ex));
                }
            }
        }

        static OpenQuantOutside()
        {
            SmartQuantPath = GetSmartQuantPath();
            AppDomain.CurrentDomain.AssemblyResolve += DomainOnAssemblyResolve;
        }

        public static void Init()
        {
            OpenFileServer();
        }

        private static void Resubscribe(Strategy root, FieldInfo subscriptionListfield, IDataProvider provider)
        {
            foreach (var child in root.Strategies) {
                var subscriptionList = (SubscriptionList)subscriptionListfield.GetValue(child);
                if (subscriptionList != null) {
                    var items = subscriptionList.ToList();
                    foreach (var item in items) {
                        subscriptionList.Remove(item);
                        subscriptionList.Add(item.Instrument, provider);
                    }
                }
                if (child.Strategies.Count > 0) Resubscribe(child, subscriptionListfield, provider);
            }
        }

        public static void Resubscribe(Strategy root)
        {
            Resubscribe(root, null);
        }

        public static void Resubscribe(Strategy root, IDataProvider provider)
        {
            var fields = typeof(Strategy).GetFields(BindingFlags.Instance | BindingFlags.NonPublic);
            FieldInfo subscriptionListField = null;
            FieldInfo providerField = null;
            foreach (var field in fields) {
                if (field.FieldType.Name == "SubscriptionList") {
                    subscriptionListField = field;
                }
                if (field.FieldType.Name == "IDataProvider") {
                    providerField = field;
                }
            }

            if (subscriptionListField == null)
                return;
            if (provider == null && providerField == null) {
                return;
            }
            Resubscribe(root, subscriptionListField, provider ?? (IDataProvider)providerField.GetValue(root));
        }
    }
}

```






