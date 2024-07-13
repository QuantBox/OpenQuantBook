

# 4. 导入历史数据

在进行策略开发、数据研究及策略回测的时候，需要使用大量的历史数据。OpenQuant支持从数据中心或本地文件中导入历史数据。



## 4.1 通过QuantBox数据中心获取数据

### 4.1.1 连接QuantBox数据中心

在OpenQuant中，打开View菜单栏，显示Providers面板，展开Historical Data菜单，找到**QuantBoxData**并鼠标右键点击Connect。如果连接成功，QuantBoxData前面的信号灯图标会由红色变为绿色。

特别需要注意的是，QuantBoxData属性面板（View -&gt; Properties）中的DataCenterHost字段，应该确保填写的是[http://data.quantbox.com](http://data.quantbox.com)

### 4.1.2 获取历史合约信息

QuantBoxData连接成功后，在菜单栏选择Data -&gt; Import -&gt; Instruments -&gt; QuantBoxData，会弹出“Import Instruments [QuantBoxData]”窗口，点击右侧Request按钮后，会显示QuantBoxData提供的所有合约列表。

👽建议使用Filter按照合约类型、交易所、字符等过滤合约后，再点击Request，以高效获取数据。

获取合约列表后，选择您想要导入本地使用的合约，点击右侧Import按钮，导入完成后，OpenQuant就会将已选的合约添加进Instruments面板（View -&gt; Instruments）。

### 4.1.3 获取期货行情的历史数据

目前QuantBoxData提供的期货合约数据是自2012年8月至今的Trade和Quote类型的Tick数据，提供的股票合约数据是已经前复权处理过的股市开盘至今的Bar Time类型并且Bar Size设置为86400的日线数据。

获取方法为：在成功获取合约信息后，便可以开始导入历史数据。在菜单栏选择Data -&gt; Import -&gt; Historical -&gt; QuantBoxData，会弹出“Import Historical Data[QuantBoxData]”界面。将左侧Instruments面板栏中的合约拖至导入列表框中，此时合约状态为Pending等待状态，设置数据类型和时间段。



设置完成后，再点击导入界面的绿色箭头按钮，开始导入。导入过程中，合约状态为Processing，导入成功后，合约的状态会变为Completed，此时，双击Instruments栏中的该合约，即可查看导入的历史数据列表详细信息。







