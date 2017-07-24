##  常用的策略事件

---

 OnStrategyStart – 在策略启动时调用，在第一笔行情到达之前

 OnStrategyStop – 在策略结束时调用，在最后一笔行情之后

 OnBarOpen – 在Bar行情最前沿调用（如，在日线数据开盘时买入）

 OnBar – 在所有行情的后沿调用（如，在日线数据收盘时买入）

 OnPositionOpened – 当一个新的交易开仓确认后调用

 OnPositionChanged – 当仓位增加或减少时调用

 OnTrade – 当市场中有成交时调用

 OnAsk – 当盘口ask有变化时调用

 OnBid – 当盘口bid有变化时调用

 OnOrderCancelled– 当撤单确认后调用

 OnOrderFilled– 当报单全部成交后调用

 OnOrderPartiallyFilled– 当报单部分成交后调用

 OnFill – 当报单后有成交时调用OnStopExecuted

 OnReminder– 当到达指定时间时调用（定时器）

 OnStopExecuted– 当到达指定止损条件时调用  


 在策略代码编辑环境下输入override on...会有智能提示，可以看到更多事件处理函数

![](/assets/commonly_strategy_event01.png)

### **OnStrategyStart**

策略启动前OnStrategyStart方法被调用，整个策略运行期只会被调用一次。OnStrategyStart事件处理中可以创建新对象，并赋值给类中声明的变量。

例如为默认Bars创建SMA对象的例子

```
using System;
using SmartQuant;
using SmartQuant.Indicators;
namespace OpenQuant
{
    public class MyStrategy : InstrumentStrategy
    {
    private SMA sma1;
    private SMA sma2;
    private int Length1 = 5;
    private int Length2 = 10;
    protected override void OnStrategyStart()
    {
        sma1 = new SMA(Bars, Length1);
        sma2 = new SMA(Bars, Length2);
    }
  ｝
｝
```

### **OnBar**

     OnBar是在有新的完整bar到来后被触发的。每个行情包括过去一个时间段的OHLCV（开盘价、最高价、最低价、收盘价、成交量）数据。因此OnBar事件是在行情后延触发的。如果需要在行情到来前处理一些动作则需要使用OnBarOpen事件。

例如交易从9:00开始，5分钟bar。OnBar会在9:05、9:10...触发，如果用的是日线数据，那么不能在OnBar中报单，因为触发OnBar的时候已经收盘了。

```
protected override void OnBar(Instrument instrument, Bar bar)
{
    //把最新的bar添加到Bars序列
    Bars.Add(bar);
}
```

### **OnPositionOpened** 

 OnPositionOpened是在交易完成时有新的头寸建立时触发的。只有交易订单被执行后才会有新头寸生成。所有的持仓数据都是大于0的。当仓位减到0时（被平仓），头寸对象被销毁。剩下的只有开仓（包括尝试开仓）的交易记录以及平仓的交易记录。

这里是一个以新开仓位持仓数量、按照5个最小价格变动单位止盈下平仓单的例子。

```
protected override void OnPositionOpened(SmartQuant.Position position)
{
    if(position.Side == PositionSide.Long)
    {//持有多头仓位
        Order sellOrder = SellLimitOrder(position.Instrument,position.Qty,position.Price+position.Instrument.TickSize*5);
        Send(sellOrder);
    }
    else
    {//持有空头仓位
        Order buyOrder = BuyLimitOrder(position.Instrument,position.Qty,position.Price-position.Instrument.TickSize*5);
        Send(buyOrder );
    }
}
```

### **OnPositionChanged** 

 OnPositionChanged是在持仓发生变化时触发的。比如当有部分成交导致持仓变化时该事件会被触发。OnPositionChanged是一个需要必须跟踪部分成交后调整止损单数量的好地方。每当新的部分成交确认到来时，你可以添加未完成止损单的数量，这样，你的止损单会更准确的反映原始订单状态。

```
protected override void OnPositionChanged(SmartQuant.Position position)
{
}
```

### **OnTrade** 

   OnTrade是在市场中有成交就会触发。例如国内普通期货行情是1秒2个行情数据包，在每次接受到行情后，如果有成交数据就会触发OnTrade。

```
protected override void OnTrade(SmartQuant.Instrument instrument, SmartQuant.Trade trade)
{
    string symbol = instrument.Symbol;//成交的合约代码
    string time = trade.DateTime.ToString("yyyy-MM-dd HH:mm:ss.fff");//成交时间
    double price = trade.Price;//成交价格
    int size = trade.Size;//成交数量
}
```

### **OnAsk** 

 OnAsk是盘口ask数据发生变化就会触发。比较适用于对于需要监控盘口数据的策略。

```
protected override void OnAsk(SmartQuant.Instrument instrument, SmartQuant.Ask ask)
{
    double askPrice = ask.Price;//盘口卖盘价格
    int askSize = ask.Size;//卖盘挂单量
}
```

### **OnBid** 

OnBid是盘口bid数据发生变化就会触发。比较适用于对于需要监控盘口数据的策略。

```
protected override void OnBid(SmartQuant.Instrument instrument, SmartQuant.Bid bid)
{
    double bidPrice = bid.Price;//盘口买盘价格
    int bidSize = bid.Size;//盘口买盘挂单量
}
```

### **OnReminder**

OnReminder定时器，在具体的一个时间点触发。需要先通过AddReminder函数添加定时器，到指定时间则触发OnReminder函数。例如日内交易策略，想在收盘前10分钟就不再允许开新的仓位，假设9点开盘15点收盘。

```
bool allowOpenFlag = true;//是否允许开仓标志，true允许，false不允许
DateTime myCloseTime;//尾盘禁止开仓的时间
protected override void OnStrategyStart()
{
    System.Console.WriteLine("Hello OpenQuant");
    myCloseTime = new DateTime(DateTime.Now.Year,DateTime.Now.Month,DateTime.Now.Day,14,50,0);
    AddReminder(myCloseTime, "my close time");//添加第一个尾盘定时器
 }
protected override void OnReminder(DateTime dateTime, object data)
 {
        //通过时间和data参数判断是否是尾盘定时器触发
        if (dateTime == myCloseTime && data.ToString() == "my close time")
        {
                allowOpenFlag = false;//设置开仓标志为false,不允许开仓
                myCloseTime = myCloseTime.AddDays(1);//尾盘禁止开仓时间加1天,变为下个交易日的尾盘禁止交易时间
                AddReminder(myCloseTime, "my close time");//添加下个交易日尾盘定时器
        }
}
protected override void OnBarOpen(Instrument instrument, Bar bar)
 {
            if (bar.OpenDateTime.Hour == 9 && allowOpenFlag == false)
            {
                allowOpenFlag = true;//开盘设置允许开仓标志为 true
            }
 }
```

### **OnStopExecuted** 

 OnStopExecuted当达到设置的止损条件时调用，需要先通过AddStop函数设置止损条件。

使用AddStop函数，需要构造一个Stop止损对象做为参数传入，Stop止损条件对象又分两种触发模式，一是定时触发，二是根据行情触发。

 Stop\(Strategy strategy,Position position,DateTime time\) 在到达time时触发止损

 Stop\(Strategy strategy,Position position,double level,StopType type,StopMode mode\) 根据行情触发止损

 strategy：策略对象

 position：持仓对象

 time：具体时间，达到这个时间就调用OnStopExecuted

 level：具体数值结合type、mode使用

 Stoptype：止损方式，固定StopType.Fixed还是跟踪StopType.Trailing，Fixed就表示价格回撤固定的level点（百分比）就调用OnStopExecuted，Trailing就表示行情从AddStop之后的最高（低）点回落（回升）level点（百分比）就调用OnStopExecuted

 StopMode：level的取值方式（单位），StopMode.Absolute-level按照报价加减level计算止损点位，StopMode.Percent-level按照百分比计算止损点位。

 Stop\(strategy,position,10,StopType.Fixed,StopMode.Absolute\)- 从当前价位回撤10点则调用OnStopExecuted

 Stop\(strategy,position,10,StopType.Trailing,StopMode.Absolute\)- 从之后最优价位回撤10点则调用OnStopExecuted

 Stop\(strategy,position,0.02,StopType.Fixed,StopMode.Percent\)- 从当前价位回撤2%则调用OnStopExecuted

 Stop\(strategy,position,0.02,StopType.Trailing,StopMode.Percent\)- 从之后最优价位回撤2%则调用OnStopExecuted

 下面是一个跟踪止损的示例

```
protected override void OnPositionOpened(Position position)
{
        Stop s = new Stop(this, position, position.Instrument.TickSize * 10, StopType.Trailing, StopMode.Absolute);
        AddStop(s);//从AddStop之后，价格从最优回落10跳则调用OnStopExecuted
}
protected override void OnStopExecuted(Stop stop)
{
            if (stop.Side == PositionSide.Long)
            {
                Order closeOrder = SellOrder(stop.Instrument, stop.Qty, "close long position");
                Send(closeOrder);
            }
            else
            {
                Order closeOrder = BuyOrder(stop.Instrument, stop.Qty, "close short position");
                Send(closeOrder);
            }
}
```



