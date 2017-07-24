# OpenQuant支持的订单类型

---

OpenQuant支持的订单类型很多，但是国内交易市场很多不支持。下面主要介绍几种国内市场支持的订单类型，限价单和市价单。

这里有个简单的例子描述如何开多和平多，并直接下单（开空和平空和这个类似，方向相反而已）。

```
Order openLimitOrder;
Order openMarketOrder;
private void OnBar(Instrument instrument,Bar bar)
{
            openLimitOrder = BuyLimitOrder(instrument, 1, bar.Open, "buy limit order");
            Send(openLimitOrder);//买限价单
            AddReminder(Clock.DateTime.AddMinutes(1),"cancel buy limit order");//添加定时器，下单1分钟后还未成交的话做撤单处理
            openMarketOrder = BuyOrder(instrument, 2, "buy market order");//买市价单
            Send(openMarketOrder);
 }
protected override void OnOrderFilled(Order order)
{
            if (order.Text == "buy market order")
            {
                closeLimitOrder = SellLimitOrder(order.Instrument, order.Qty, order.Price + order.Instrument.TickSize * 2);
                Send(closeLimitOrder);
            }
}
protected override void OnReminder(DateTime dateTime, object data)
{
            if (data != null && data.ToString() == "cancel buy limit order")
            {//是撤单定时器触发的
                if (!openLimitOrder.IsDone)
                {//openLimitOrder还未成交
                    Cancel(openLimitOrder);
                }
            }
}
```



