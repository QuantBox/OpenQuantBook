# CTP插件Ask和Bid事件无法触发的问题
---
在CTP插件的属性配置选项: Settings - MarketData

![](/assets/emit_ask_bid.png)

EmitBidAsk:
true:触发OnBid和OnAsk事件
false:不触发OnBid和OnAsk事件

EmitBidAskFirst:
true:先触发OnBid和OnAsk事件，再触发OnTrade事件
false:先触发OnTrade事件，再触发OnBid和OnAsk事件



