# 如何在实盘模式下加载历史数据

---

用户在编写一些趋势策略时经常需要在策略启动时导入历史数据做初始化，例如，加载前20个交易日的日线数据等。要实现这个功能最直接的办法是使用“回测转实盘”的策略运行模式，所谓“回测转实盘”的策略运行模式就是策略先在回测模式下处理历史数据，等到历史数据处理完成后，再进入实盘模式下运行。这种模式可以让策略一种非常自然的模式处理数据，不用区分回测还是实盘。

下面就用实例来说明如何实现“回测转实盘”。首先要修改实盘场景的Scenario文件，在Run方法中添加需要加载的历史数据区间 \(设置DataSimulator的DataTime1和DateTime2属性\)，然后调用 StartBacktest\(\) 进入回测模式，在回测模式完成后设置实盘交易通道，调用 StartLive\(\) 进入实盘模式。这里需要注意的是，为了解决“回测转实盘”后策略的 OnTrade、OnAsk、OnBid 不能触发的问题，需要在进入实盘模式前调用 OpenQuantOutside.Resubscribe 重新设置行情订阅。

```
public override void Run()
{
    strategy = new TurtleStrategy(framework, "main");
    BarFactory.Clear();
    var inst = InstrumentManager.Instruments[“rb1710”];
    strategy.AddInstrument(inst);
    BarFactory.Add(inst, BarType.Time, 60);    
    DataSimulator.DateTime1 = new DateTime(2017, 06, 25);
    DataSimulator.DateTime2 = new DateTime(2017, 06, 27);
    StartBacktest();
    strategy.DataProvider = ProviderManager.GetDataProvider("A99CTP");
    strategy.ExecutionProvider = ProviderManager.GetExecutionProvider("A99CTP");
    OpenQuantOutside.Resubscribe(strategy);
    StartLive();
}
```

OpenQuantOutside 类的源代码见代码附录：[OpenQuantOutside](source_code_OpenQuantOutside.md)

