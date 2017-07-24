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

*  修改Program.cs在Main入口函数中添加OpenQuantOutside.Init 函数调用。这个函数可以解决策略程序在OpenQuant安装目录外运行时遇到的问题。下载 OpenQuantOutside 类型源代码。

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



