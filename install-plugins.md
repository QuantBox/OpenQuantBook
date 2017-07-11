# 下载、安装、使用插件

---

### 下载、安装国内期货交易插件

OpenQuant系统中可以由第三方服务商或者开发者自行进行扩展，例如行情源的接入、交易通道的接入、历史数据源的接入等等，这些扩展我们称之为插件（Plugins）。

上期技术公司的CTP系统是获取国内期货实时行情、进行交易的主要平台。各个主流期货经纪商均支持客户通过CTP柜台进行期货、期权的交易。您可以在SmartQuant中文网站\([http://www.smartquant.cn](http://www.smartquant.cn)\)下载64位的CTP插件安装程序，并以默认过程安装完成后，打开OpenQuant，就可以在Providers面板找到CTP插件。

![](/assets/A99CTP.png)

图1：OpenQuant中的插件（Provider）

CTP插件提供了合约管理、交易接口和获取实时行情的接口功能。

### 使用期货交易插件

* #### 配置插件

安装CTP插件后，先需要配置交易通道的IP地址及端口号，交易者账户及密码等信息，使得CTP插件可以正常连接和工作。

鼠标右键点击Providers面板中的A99CTP插件，选择Properties属性：

![](/assets/ProviderProperties.png)



在CTP插件中，用户可以配置多套服务器及账户信息，但需要指定使用哪套账户信息（账号及密码）及指定哪套交易服务器、行情服务器，这些服务器使用哪个账户。

在Properties窗口中，选择Settings选项中的AllConfig，按照下列图片过程进行设置，即可以完成CTP插件的交易账号和相关信息的配置。

 ![](/assets/ProviderSettings01.png)

![](/assets/ProviderSetting02.png)

![](/assets/ProviderSetting03.png)

* #### 添加合约

当CTP插件（Provider A99CTP）与CTP交易柜台正常连接后，即可为你的OpenQuant系统添加合约信息。在菜单栏中选择Data -&gt; Import -&gt; Instruments -&gt; A99CTP ，下图所示：

![](/assets/ImportInstrument.png)  
图2：为OpenQuant添加合约

弹出如下图所示界面，点击右侧Request按钮后，会显示您所连接的CTP柜台中提供的所有合约列表。您也可以使用Filter按照合约类型、交易所、字符等过滤合约后，再点击Request。

![](/assets/ImportInstumnetsRequest.png)

获取合约列表后，选择您想要导入本地使用的合约，点击右侧Import按钮，导入完成后，OpenQuant就会将已选的合约添加进Instruments面板（View -&gt; Instruments），如下图所示。

![](/assets/importInstrumentDone.png)

