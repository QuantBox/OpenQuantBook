# 如何实现限价单和市价单的开平仓

---

OpenQuant支持的订单类型很多，但是国内交易市场很多不支持。下面主要介绍几种国内市场支持的订单类型，限价单和市价单的开平仓。
想要实现国内开平仓操作，需要下载安装64位CTP插件，并在项目中引用 QuantBox.OQ，下载地址：http://www.smartquant.cn/rjxz.html

这里有个简单的例子描述如何开多和平多，并直接下单（开空和平空和这个类似，方向相反而已）。


```
using QuantBox;

Order openLimitOrder;
Order openMarketOrder;
private Order closeLimitOrder;

private void OnBar(Instrument instrument,Bar bar)
{
    //开仓买限价单
    openLimitOrder = BuyLimitOrder(instrument, 1, bar.Open, "buy limit order");
    openLimitOrder.Open();
    Send(openLimitOrder);
    
    AddReminder(Clock.DateTime.AddMinutes(1),"cancel buy limit order");//添加定时器，下单1分钟后还未成交的话做撤单处理
    
    //开仓买市价单
    openMarketOrder = BuyOrder(instrument, 2, "buy market order");//买市价单
    openMarketOrder.Open();
    Send(openMarketOrder);
}
 
protected override void OnOrderFilled(Order order)
{
    if (order.Text == "buy market order")
    {
        //平仓卖限价单
        closeLimitOrder = SellLimitOrder(order.Instrument, order.Qty, order.Price + order.Instrument.TickSize * 2);
        closeLimitOrder.Close();
        Send(closeLimitOrder);
    }
}

protected override void OnReminder(DateTime dateTime, object data)
{
    if (data != null && data.ToString() == "cancel buy limit order")
    {   //是撤单定时器触发的
        if (!openLimitOrder.IsDone)
        {//openLimitOrder还未成交
         Cancel(openLimitOrder);
        }
    }
}
```



