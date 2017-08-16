# OpenQuant中FOK指令的使用方法
---

立即全部成交否则自动撤销指令(FOK指令)，指在限定价位下达指令，如果该指令下所有申报手数未能全部成交，该指令下所有申报手数自动被系统撤销。



```
protected override void OnTrade(Instrument instrument, Trade trade)
{
    if (i == 0)
    {
        Order buyOrder = BuyLimitOrder(instrument, 10, trade.Price - 30 * instrument.TickSize, "buyopen");
        buyOrder.TimeInForce = TimeInForce.FOK;
        Send(buyOrder);
        System.Console.WriteLine("OnTrade "+instrument.Symbol+" FOK order ");
    }
            
    if (i == 1)
    {
        Order buyOrder = BuyLimitOrder(instrument, 100, trade.Price - 30 * instrument.TickSize, "buyopen");
        buyOrder.TimeInForce = TimeInForce.IOC;//FAK
        buyOrder.MinQty = 50;
        Send(buyOrder);
        System.Console.WriteLine("OnTrade " + instrument.Symbol + " IOC order ");
    }

    i++;
}
```
