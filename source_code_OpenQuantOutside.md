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


