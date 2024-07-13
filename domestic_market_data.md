# 3. OpenQuant2014连接CTP柜台并获取实时数据

## <div id="3.1"></div>3.1 在OpenQuant中连接CTP柜台

OpenQuant交易通道配置完成后，在Providers窗口中，鼠标右击QuantBoxCtpse这个通道，并选择连接。

 ![](/assets/oq_providers_QuantBoxCTPse_Connect.png)

连接成功后，Output窗口应该有柜台信息的输出，此时通道连接成功。如果不成功，也可以查看Output窗口中的输出并检查问题。





## <div id="3.2"></div>3.2 通过CTP实时获取CTP交易的合约信息

在OpenQuant2014已经连接到CTP柜台后，可以从CTP交易柜台实时导入当前交易合约的信息，包括合约代码，报价单位，基础价差，合约乘数等基础信息。

点击OpenQuant2014菜单并依次选择：Data - Import - Instruments - QuantBoxCtpse ，打开在Import Instruments [QuantBoxCtpse]窗口中，筛选类型、交易所、代码等信息后，按Request按钮获取合约信息，然后按Import进行导入即可。

👽目前期货合约及期权合约数量众多，建议导入时可以按照合约代码的关键字进行过滤。







## <div id="3.3"></div>3.3 通过CTP观察合约的实时数据

在CTP正常连接，并且在连续交易的盘中时段，在OpenQuant菜单中依次点击选择：View-QuoteMonitor - QuantBoxCtpse ，在打开的QuoteMonitor窗口中， 用鼠标拖动合约窗口中的代码，拖入QuoteMonitor窗口，此时就可以看到市场这些合约的报价情况，鼠标右键这些市场中的合约代码，可以选择直接下单交易。

![](/assets/oq_providers_QuantBoxCTPse_QuoteMonitor.png)



## <div id="3.4"></div>3.4 查询CTP柜台的账户基本信息

在OpenQuant菜单中依次选择：View-Account ，即可查看自己账户的资金信息。



 







