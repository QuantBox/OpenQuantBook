# OpenQuant中FOK指令的使用方法
---

FOK指令:立即全部成交否则自动撤销指令，指在限定价位下达指令，如果该指令下所有申报手数未能全部成交，该指令下所有申报手数自动被系统撤销。在OpenQuant中可以通过设置order的TimeInForce = TimeInForce.FOK实现。   
   
FAK指令:立即成交剩余否则自动撤销指令，指在限定价位下达指令，如果该指令下部分申报手数成交，该指令下剩余申报手数自动被系统撤销。在OpenQuant中可以通过设置order的TimeInForce = TimeInForce.IOC实现。   

以下代码是在SimNow环境下测试通过的示例：

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
