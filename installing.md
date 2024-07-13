# 2. OpenQuant软件下载与安装

---

###  2.1 最新OpenQuant软件下载

在SmartQuant的官方网站中，您可以下载到OpenQuant最新版进行全功能的限时测试，测试期为30天。下载地址为：

[http://www.smartquant.com/downloads.html ](http://www.smartquant.com/downloads.html)

也可以注册在线版本QuantWeb直接进行在线测试。



国内期货CTP插件及历史数据插件下载

http://www.quantbox.cn/openquant

###  2.2 OpenQuant软件运行环境

OpenQuant系统运行在微软Windows操作系统，最新版本的OpenQuant支持Windows7，Windows8，Windows10及Windows Server 2008，Windows Server 2012等主流的Windows 64位操作系统。安装OpenQuant软件时，OpenQuant安装程序会自动检测是否有合适的.NET Framework基础软件，如果需要安装程序会自动进行升级安装。

**在2024年**，安装OpenQuant2014软件之前的准备工作：

建议的运行平台为Windows 2022 server 或者 Windows 10，并且依次安装了如下软件

安装DotNet Framework 4.8.1

安装Visual Studio 2022 社区版

安装Git，TortoiseGit

可选安装Mysql连接程序 mysql-connector-net-8.4.0 for windows



###  2.3 OpenQuant软件的安装



将下载的OpenQuant软件包存入D:\install\OpenQuant，这些软件包括：

* OpenQuant2014  Openquant主软件
* QuantBoxCtpse  CTP插件
* QuantBoxHisData QuantBox历史数据插件

在Windows 2016 或者Windows 10 的环境依次安装OpenQuant2014，QuantBoxCtpse及QuantBoxHisData

👽 **注意**：在开始安装OpenQuant前，需要在windows系统中，安装Git与TortoiseGit工具，Git安装也会在Windows系统中安装VC runtime 库，这个也是运行OpenQuant插件的必要基础环境。





运行OpenQuant安装程序，按照默认步骤进行安装即可轻松完成安装过程。

OpenQuant 应用程序会被安装在标准的 Program Files \(x86\)\SmartQuant Ltd\OpenQuant 2014 目录中。

安装插件后，在OpenQuant主界面的Providers中可以看到Execution Provider中出现QuantBoxCtpse，在Historical Data的Providers中出现QuantBoxData ， 这样安装就完成了。

![](/assets/oq_providers.png)



系统的数据文件\(data.quant 和 instruments.quant\)可以在 AppData\Roaming SmartQuant Ltd\OpenQuant 2014\data 目录中找到。

系统的配置文件可以在 AppData\Roaming\SmartQuant Ltd\OpenQuant 2014 目录中找到。

系统的示例项目可以在 Documents\OpenQuant 2014\Solutions 目录中找到。

如果你用过早先的OpenQuant软件，你一定注意到了新版本已经不再使用 Access 数据库的 instrument.sdf 来存储合约的定义。从OpenQuant 2014 版本开始，软件系统采用了新的数据文件，允许存储多种类型的对象，比如，合约、定单、还有策略的状态。





###  2.4 OpenQuant软件的卸载

卸载软件可以通过控制面板或软件自带的 Uninstall 工具卸载。

![](/assets/Uninstall.png)

除了运行Uninstall工具进行OpenQuant.exe程序卸载 以外，还需要手动删除系统盘 Users 目录下两个路径的文件夹:

1. ...\AppData\Roaming\SmartQuant Ltd            数据和配置文件
2. ...\Documents\OpenQuant 2014                      策略的项目代码

###  2.5 OpenQuant软件的启动运行

双击OpenQuant图标，经过短暂的启动加载，

![](/assets/OpenQuantLaunching.png)

你就进入OpenQuant的集成开发环境了，这是我们熟悉的Windows软件风格，StartPage中显示最近打开的项目，第一次打开时，显示的是OpenQuant的策略示例。

![](/assets/OpenQuantMainGUI.png)



###  2.6 OpenQuant配置国内期货交易通道

国内期货的主流通道是上期技术公司的CTP，我们使用QuantBoxCtpse  CTP插件连接期货经纪商的CTP交易通道。配置过程如下：

在Providers窗口中，选择QuantBoxCtpse ，在Properties中的Configuration项中，选择“..."的按钮，然后打开QuantBoxCtpse的配置界面，进行交易通道的增加。

在增加前，你应该从开户的期货经纪商获得了CTP柜台的API连接信息，并按照国内监管要求向经纪商报备了程序化交易系统，并为OpenQuant获得了OpenQuant的软件认证码。如果有任何以为可以咨询你的开户客户经理，如果遇到技术问题，可以进入QQ群，微信群咨询。

```
CTP柜台API链接信息举例:

渤海期货 CTP仿真柜台:
接口信息为：
接入IP：
电信 180.169.116.120 
联通 211.95.26.214

端口信息：
交易 43205 
行情 43213

BrockID：4080
```



在Providers窗口中，选择QuantBoxCtpse ，在Properties中的Configuration项中，选择“..."的按钮，然后打开QuantBoxCtpse的配置界面，进行交易通道的增加：

![](/assets/oq_providers_QuantBoxCTPse.png)

配置Provider：QuantBoxCtpse

QuantBoxCtpse的配置窗口如下：

![](/assets/oq_providers_QuantBoxCTPse_Configuration_MainWindow.png)

QuantBoxCtpse配置窗口

#### 2.6.1. 添加账户信息 Users

注意密码和账户名的顺序

![](/assets/oq_providers_QuantBoxCTPse_Configuration_AddUser.png)

#### 2.6.2. 添加期货公司交易及行情服务器信息 Servers

##### 2.6.2.1 添加行情服务器

添加行情服务器时需要填写如下信息：

**客户端认证：**
目前行情服务器不需要客户端认证

**服务器信息：**
服务器地址 address，tcp://180.169.116.120:43213
经纪商ID：BrokerID，4080

**标签:**
名称：渤海仿真
服务类别：Trade, Instrument, Query
标识：渤海仿真-电信行情

**流重传方式：**
选择默认的 Resume

**行情：**
IsMulticast:  默认为False
IsUsingUdp: 默认为False

![](/assets/oq_providers_QuantBoxCTPse_Configuration_AddMD.png)



##### 2.6.2.2 添加交易服务器

添加行情服务器时需要填写如下信息：

**客户端认证：**
连接交易服务器需要客户端认证，符合看穿式监管的技术要求：
需要填写：
AuthCode：期货公司给出的客户端认证代码： XXXXXXXXXXXXXX
UserProductInfo：这个默认使用OpenQuant即可
客户端标识（看穿式监管）：向期货公司进行软件报备时上报的软件标志信息：格式一般为：软件厂商名_软件产品名_版本
例如： QuantBox_OpenQuant_2014 

【参考阅读资料】 [关于期货市场启用看穿式监管公告](https://www.gov.cn/xinwen/2018-09/14/content_5322111.htm#1)

**服务器信息：**
服务器地址 address，tcp://180.169.116.120:43205
经纪商ID：BrokerID，4080

**标签:**
名称：渤海仿真-电信交易
服务类别：MarketData
标识：渤海仿真-电信交易

**流重传方式：**
选择默认的 Resume

**行情：**
IsMulticast:  默认为False
IsUsingUdp: 默认为False

#### 2.6.2.3. 添加默认连接通道信息 Connections

配置Connections时，

##### 1） 添加行情连接，指定ApiPath

**ApiPath**
选择 C:\Users\Administrator\AppData\Roaming\SmartQuant Ltd\OpenQuant 2014\XAPI\x64\CTPSE\SfitCtpse.Quote.dll
正确选择API路径后，Infomation项目的Name和Version信息会自动显示

**Active**
选择 True

**LogPrefix**
可以填写 md， 这样在日志中，前端会显示md字串，用于区分是行情连接产生的日志，在大量显示日志时，利于阅读

**Server**
选择刚刚配置的行情服务器信息：渤海仿真-电信行情

**User**
选择对应的Users信息：渤海仿真测试

**Type的UseType**
选择MarketData，Type会自动显示MarketData

![](/assets/oq_providers_QuantBoxCTPse_Configuration_ConnMD.png)



##### 2） 添加交易连接，指定相应的ApiPath

**ApiPath**
选择C:\Users\Administrator\AppData\Roaming\SmartQuant Ltd\OpenQuant 2014\XAPI\x64\CTPSE\SfitCtpse.Trader.dll

正确选择API路径后，Infomation项目的Name和Version信息会自动显示

**Active**
选择 True

**LogPrefix**
可以填写 ts， 这样在日志中，前端会显示ts字串，用于区分是交易连接产生的日志，在大量显示日志时，利于阅读

**Server**
选择刚刚配置的交易服务器信息：渤海仿真-电信交易

**User**
选择对应的Users信息：渤海仿真测试

**Type的UseType**
选择Trade，Instrument，Query三项，Type会自动显示Trade，Instrument及Query



上述过程完成后，就已经配置好了CTP柜台插件的全部信息。现在OpenQuant 2014软件可以从CTP订阅和接收交易合约及行情信息，也可以通过交易通道的进行报单及回报的接收了。

