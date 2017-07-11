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



