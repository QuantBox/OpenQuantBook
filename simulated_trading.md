# 如何进行模拟交易

---

要进行模拟交易先要理解什么是模拟交易。OpenQuant包含三种工作模式，Backtest\(回测\)、Paper\(模拟\)、Live\(实盘\)，而在系统内核里只有两种运行模式：Real-time、Simulation分别对应Live\(实盘\)和Backtest\(回测\)模式。这就出现了一个问题，既然系统内核中并不存在一种和Paper\(模拟\) 相对应的运行模式，那么当策略运行在Paper\(模拟\)模式时，系统内核到底发生了什么？

实际上当策略运行在Paper\(模拟\)模式时，系统内核的运行模式是Realtime。这就表示Live\(实盘\)和Paper\(模拟\)内核运行模式是相同的，那Live\(实盘\)和Paper\(模拟\)不同的运行效果是如何实现的呢，关键就是策略运行时指定的交易通道不同。Live\(实盘\)模式下策略都会连接真实的交易通道向交易所或代理商发送订单接收行情，而在Paper\(模拟\)模式下虽然也会连接真实的交易通道接收行情，但是报单并不发送给交易所或代理商而是使用系统自带的模拟交易引擎进行模拟撮合。

通过一个实例来说明如何在OpenQuant中进行模拟交易。

在OpenQuant 中打开SMACrossover策略项目，把Realtime工程设置成启动项。

![](/assets/simulated_trading01.png)

打开场景文件\(Scenario.cs\),把使用的合约修改成国内上市交易的合约。

```
public override void Run()
{
	Instrument instrument1=InstrumentManager.Instruments["rb1710"];
	Instrument instrument2=InstrumentManager.Instruments["cu1708"];
	...
	...
}
```

修改策略使用的行情通道 \(Data Provider\) 连接 CTP 行情通道，在Run函数最后以 StartPaper 方式启动策略。

```
public override void Run()
{
    Instrument instrument1 = InstrumentManager.Instruments["rb1710"];
    Instrument instrument2 = InstrumentManager.Instruments["cu1708"];
    // Create SMA Crossover strategy
    strategy = new MyStrategy(framework, "SMACrossover");
    // Add instruments
    strategy.AddInstrument(instrument1);
    strategy.AddInstrument(instrument2);
    strategy.DataProvider = ProviderManager.GetDataProvider("A99CTP");
    //strategy.ExecutionProvider = ProviderManager.GetExecutionProvider("A99CTP");
    // Add 1 minute bars
    BarFactory.Clear();
    BarFactory.Add(instrument1, BarType.Time, barSize);
    BarFactory.Add(instrument2, BarType.Time, barSize);
    // Run the strategy
    // StartStrategy();
    StartPaper();
}
```



