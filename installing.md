# OpenQuant**软件下载与安装**

---

### 1. 最新OpenQuant软件下载

在SmartQuant的官方网站中，您可以下载到OpenQuant最新版进行全功能的限时测试，测试期为30天。下载地址为：

[http://www.smartquant.com/downloads.html ](http://www.smartquant.com/downloads.html)

也可以注册在线版本QuantWeb直接进行在线测试。

### 2. OpenQuant软件运行环境

OpenQuant系统运行在微软Windows操作系统，最新版本的OpenQuant支持Windows7，Windows8，Windows10及Windows Server 2008，Windows Server 2012等主流的Windows 64位操作系统。安装OpenQuant软件时，OpenQuant安装程序会自动检测是否有合适的.NET Framework基础软件，如果需要安装程序会自动进行升级安装。

### 3. OpenQuant软件的安装

运行OpenQuant安装程序，按照默认步骤进行安装即可轻松完成安装过程。

OpenQuant 应用程序会被安装在标准的 Program Files \(x86\)\SmartQuant Ltd\OpenQuant 2014 目录中。

系统的数据文件\(data.quant 和 instruments.quant\)可以在 AppData\Roaming SmartQuant Ltd\OpenQuant 2014\data 目录中找到。

系统的配置文件可以在 AppData\Roaming\SmartQuant Ltd\OpenQuant 2014 目录中找到。

系统的示例项目可以在 Documents\OpenQuant 2014\Solutions 目录中找到。

如果你用过早先的OpenQuant软件，你一定注意到了新版本已经不再使用 Access 数据库的 instrument.sdf 来存储合约的定义。从OpenQuant 2014 版本开始，软件系统采用了新的数据文件，允许存储多种类型的对象，比如，合约、定单、还有策略的状态。

### 4. OpenQuant软件的卸载

卸载软件可以通过控制面板或软件自带的 Uninstall 工具卸载。

![](/assets/Uninstall.png)

除了运行Uninstall工具进行OpenQuant.exe程序卸载 以外，还需要手动删除系统盘 Users 目录下两个路径的文件夹:

1. ...\AppData\Roaming\SmartQuant Ltd            数据和配置文件
2. ...\Documents\OpenQuant 2014                      策略的项目代码

### 5. OpenQuant软件的启动运行

经过短暂的启动加载，

![](/assets/OpenQuantLaunching.png)

你就进入OpenQuant的集成开发环境了，这是我们熟悉的Windows软件风格，StartPage中显示最近打开的项目，第一次打开时，显示的是OpenQuant的策略示例。

![](/assets/OpenQuantMainGUI.png)

