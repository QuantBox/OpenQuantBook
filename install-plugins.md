# 下载、安装、使用插件

---

### 下载、安装国内期货交易插件

OpenQuant系统中可以由第三方服务商或者开发者自行进行扩展，例如行情源的接入、交易通道的接入、历史数据源的接入等等，这些扩展我们称之为插件（Plugins）。

上期技术公司的CTP系统是获取国内期货实时行情、进行交易的主要平台。各个主流期货经纪商均支持客户通过CTP柜台进行期货、期权的交易。您可以在SmartQuant中文网站\([http://www.smartquant.cn](http://www.smartquant.cn)\)下载64位的CTP插件安装程序，并以默认过程安装完成后，打开OpenQuant，就可以在Providers面板找到CTP插件。

![](/assets/A99CTP.png)

图1：OpenQuant中的插件（Provider）

CTP插件提供了合约管理、交易接口和获取实时行情的接口功能。

### 使用期货交易插件

配置插件

* #### 添加合约

当CTP插件（Provider A99CTP）与CTP交易柜台正常连接后，即可为你的OpenQuant系统添加合约信息。在菜单栏中选择Data -&gt; Import -&gt; Instruments -&gt; A99CTP ，下图所示：

![](/assets/ImportInstrument.png)  
图2：为OpenQuant添加合约



弹出如图3所示界面，点击右侧Request按钮后，会显示您所连接的CTP柜台中提供的所有合约列表。您也可以使用Filter按照合约类型、交易所、字符等过滤合约后，再点击Request。

![](/assets/ImportInstumnetsRequest.png)

获取合约列表后，选择您想要导入本地使用的合约，点击右侧Import按钮，导入完成后，OQ就会将已选的合约添加进Instruments面板（View -&gt; Instruments），如图4所示。

![](/assets/importInstrumentDone.png)



