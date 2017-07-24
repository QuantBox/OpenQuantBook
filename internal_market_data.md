# 获取国内市场数据

---

### 支持股票、基金、外汇、期权、期货吗？

OpenQuant功能上支持以上所有标的。

数据上，目前暂时已接入了中国大陆的A股、期货数据。

其他的数据，例如中国大陆的B股、基金、期权也在接入的计划中；美股、港股、外汇数据会在上述三种数据接入完成再逐步接入。

### 提供什么数据？

目前提供的数据有：

股票开盘至今的A股前复权日线数据

2012年8月至今的期货tick数据

A股、指数、期货的标的信息

### 数据每天什么时候更新？

目前的A股数据、期货数据均是在18:00 ~ 20:00 更新。

### 数据如何接入？

可以通过官方发布的Provider ThanfData下载数据。

1.Thanf数据接口的连接

打开View菜单栏，显示Providers面板，展开Historical Data菜单，找到ThanfData并右键，如下图1所示，点击Connect，如果连接成功，ThanfData前面的图标会由红色变为绿色。

特别需要注意的是，如图1右侧属性面板（View -&gt; Properties）中的DataCenterHost字段，应该确保填写的是[http://data.thanf.com/。](http://data.thanf.com/。)

![](/assets/internal_market_data01.png)

```
                                                图 1 连接Thanf数据接口
```

1. 获取Thanf合约信息

ThanfData连接成功后，在菜单栏选择Data -&gt; Import -&gt; Instruments -&gt; ThanfData，会弹出如图2所示界面，点击右侧Request按钮后，会显示Thanf提供的所有合约列表。

您也可以使用Filter按照合约类型、交易所、字符等过滤合约后，再点击Request，如图3所示。

获取合约列表后，选择您想要导入本地使用的合约，点击右侧Import按钮，导入完成后，OQ就会将已选的合约添加进Instruments面板（View -&gt; Instruments），如图4所示。

![](/assets/internal_market_data02.png)

```
                                                 图 2 导入Thanf合约初始界面
```

![](/assets/internal_market_data03.png)

```
                                                  图 3 请求订阅合约
```

![](/assets/internal_market_data04.png)

```
                                                    图 4 导入Thanf合约完成界面
```

1. 获取Thanf历史数据

成功获取合约信息后，便可以开始导入历史数据。在菜单栏选择Data -&gt; Import -&gt; Historical -&gt; ThanfData，会弹出如图5所示界面。

![](/assets/internal_market_data05.png)

```
                                                   图 5 导入Thanf合约历史数据初始界面
```

将左侧Instruments面板栏中的合约拖至导入列表框中，此时合约状态为Pending等待状态，设置数据类型和时间段，如图6所示。

目前Thanf提供的期货合约数据是自2012年8月至今的Trade和Quote类型的Tick数据，提供的股票合约数据是已经前复权处理过的股市开盘至今的Bar Time类型并且Bar Size设置为86400的日线数据。后续数据服务的更新会在官网和本文中实时公布。

设置完成后，再点击导入界面的绿色箭头按钮，开始导入。

![](/assets/internal_market_data06.png)

```
                                                图 6 开始导入合约历史数据
```

![](/assets/internal_market_data07.png)

```
                                       图 7 Thanf合约历史数据导入完成界面
```

导入过程中，合约状态为Processing，导入成功后，合约的状态会变为Completed，如图7所示。

此时，双击Instruments栏中的该合约，即可查看导入的历史数据列表详细信息，如图8所示。

![](/assets/internal_market_data08.png)

```
                                              图 8 查看合约历史数据
```

### 数据每天什么时候更新？

目前的A股数据、期货数据均是在18:00 ~ 20:00 更新。

