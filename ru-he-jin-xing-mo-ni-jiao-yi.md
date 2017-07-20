# 如何进行实盘交易

---

通过一个实例来说明如何在OpenQuant中进行模拟交易。

在OpenQuant 中打开SMACrossover策略项目，把Realtime工程设置成启动项。

![](/assets/set_startup.png)

打开场景文件\(Scenario.cs\),把使用的合约修改成国内上市交易的合约。

> ```java
> public override void Run()
> {
>     Instrument instrument1=InstrumentManager.Instruments["rb1710"];
>     Instrument instrument2=InstrumentManager.Instruments["cu1708"];
>     //...
>     //...    
> }
> ```

修改策略使用的行情通道\(Data Provider\)和交易通道\(ExecutionProvider\)，连接CTP交易行情通道，在Run函数最后以StartLive方式启动策略。

> ```java
> public override void Run()
> {
>   Instrument instrument1 = InstrumentManager.Instruments["rb1710"];
>   Instrument instrument2 = InstrumentManager.Instruments["cu1708"];
>   // Create SMA Crossover strategy
>   strategy = new MyStrategy(framework, "SMACrossover");
>   // Add instruments
>   strategy.AddInstrument(instrument1);
>   strategy.AddInstrument(instrument2);
>   strategy.DataProvider = ProviderManager.GetDataProvider("A99CTP");
>   strategy.ExecutionProvider = ProviderManager.GetExecutionProvider("A99CTP");
>   // Add 1 minute bars
>   BarFactory.Clear();
>   BarFactory.Add(instrument1, BarType.Time, barSize);
>   BarFactory.Add(instrument2, BarType.Time, barSize);
>   // Run the strategy
>   //StartStrategy();
>   StartLive();
> }
> ```



