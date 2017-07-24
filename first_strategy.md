# 开始第一个策略

---

Solution：解决方案

Project：项目

一个解决方案下可以有多个项目，但是只有一个启动项

双击cs文件可以打开编辑代码

### **1. 新建策略**

在菜单栏File-&gt;New-&gt;Solution，新建一个解决方案

![](/assets/first-strategy01.png)

![](/assets/first-strategy02.png)

选择新建SmartQuant Instrument Strategy Solution模式的解决方案

Name是解决方案的名称

Location 是解决方案（代码）保存的位置

单击OK按钮即新建完成，在解决方案资源管理器我们看到新建好的解决方案，而且也可以在相应的目录下找到代码文件

![](/assets/first-strategy03.png)

![](/assets/first-strategy04.png)

### **2 . 编写Hello OpenQuant策略**

OpenQaunt代码编辑器支持语法高亮、格式化、自动完成，如下所示（自动完成）

![](/assets/first-strategy05.png)

### 2.1 编写场景

在解决方案资源管理器中，可以看到Backtest项目名称是黑体加粗（右键项目名称-&gt;Set as StartUP Project可以设置启动项，每个解决方案只有一个启动项），这表示Backtest项目为启动项，而Backtest项目又以Program.cs中的Main函数为入口。

Program.cs-&gt;Main函数：

```
static void Main(string[] args)

{

 Scenario scenario = new MyScenario(Framework.Current);

 scenario.Run();

}
```

上面代码可以看出，Main函数会调用MyScenario.cs里面的Run函数。

打开Backtest项目中MyScenario.cs（场景文件），找到Run函数，添加订阅合约的代码，

我们以订阅IF1705为例。场景文件主要目的就是订阅合约、设置Bar周期等作用。

```
 public override void Run()

        {

          //这里的合约是需要在Instruments中存在的合约

          Instrument instrument = InstrumentManager.Instruments["IF1705"];

          strategy = new MyStrategy(framework, "Backtest");

          //订阅合约

          strategy.AddInstrument(instrument);

          Initialize();

          StartStrategy();

        }
```

strategy = new MyStrategy\(framework, "Backtest"\);这行代码就代表了我们的策略代码是MyStartegy.cs文件中的MyStrategy类

### 2.2 编写策略代码

在已经编写好的场景文件中，可以看到Run函数new了MyStrategy实例，并且调用了StartStrategy\(\)函数，这就表示开始启动MyStrategy策略了。OpenQuant的策略执行机制是事件机制，即触发了某事件则会调用相应的处理函数，具体各个事件和相应的处理函数后面会详细介绍，在编写实际交易策略时，这些事件和处理函数是必须了解的。

打开MyStrategy.cs，可以看到如下代码：

```
using System;

using SmartQuant; 

namespace OpenQuant

{

    public class MyStrategy : InstrumentStrategy

    {

        public MyStrategy(Framework framework, string name)

            : base(framework, name)

        {

        }

        protected override void OnStrategyStart()

        {

            System.Console.WriteLine("Hello OpenQuant");

        }

        protected override void OnBar(Instrument instrument, Bar bar)

        {

        }

    }

}
```

我们在OnStrategyStart\(\)函数中，添加System.Console.WriteLine\("Hello OpenQuant"\)，至此我们第一个策略完成，运行策略可以看到结果。

![](/assets/first-strategy06.png)

