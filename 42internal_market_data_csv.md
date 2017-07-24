# 如何导入csv或txt格式的第三方数据？

---

### 1. 数据准备

请提前准备好需要导入的数据，数据格式参考下图1：

![](/assets/42internal_market_data_csv01.png)

```
                                                   图 1 数据格式
```

1. 数据导入过程

2.1添加数据

打开OpenQuant2014，点击Data-&gt;Import-&gt;CSV or Text Files 进入到数据导入界面，如图2：

![](/assets/42internal_market_data_csv02.png)

```
                                               图 2 导入菜单入口
```

点击界面右侧的Add File，选择要添加的数据（可同时选择多个文件），然后点击Next进入到数据格式设置页面，如下图3：

![](/assets/42internal_market_data_csv03.png)

```
                                              图 3 添加文件界面
```

导入数据格式设置有五部分，如下图：

![](/assets/42internal_market_data_csv04.png)

```
                                               图 4 数据格式设置
```

第一部分：CSV部分

A.Separator 分隔符选择，共有Tab制表符/Comma 逗号/Semicolon分号/Space空格四个选项，根据导入数据的格式来选择，如下图5，分隔符为逗号，则选择Comma。

![](/assets/42internal_market_data_csv05.png)

```
                                                   图 5 分隔符示例
```

B.Header with以第几行为开头的选择，导入的第一行必须是数据，非数据行需跳过，如果导入的第一行是数据，则Header with后的选项框填0，如果导入的数据第一行为列名（如下图），则填写1，即Header with \( 1 \) line。

![](/assets/42internal_market_data_csv06.png)

                                                                图 6 表头示例

第二部分：Data 数据类型选择

类型选择分为Bar\(Time\)/Trade/Quote三种，如果数据是Bar 格式的就选择Bar（Time），可选择Bar的时间；如果是Trade 就选择Trade，策略里需用报价需再导一次Quote ，即Trade 数据和 Quote数据需分别导入。

![](/assets/42internal_market_data_csv07.png)

                                                                   图 7 数据类型选择

第三部分：Date时间索引选择

A.column，按列导入，时间索引以数据文件中的时间列为准。

B.manually，手动导入，可手动导入具体某一天的数据。应用后时间索引不包含日期信息，只包含分时信息。

第四部分：标的标签选择

类型选择分为column /file/manually三种，此部分主要是确定标的名称，如是以数据文件中的某列为标的名称，则选Column；如是以文件名为标的名称，则选file（适用于批量文件导入）；也可自定义标的名称即通过manually来设置。

第五部分：设置导入的列标签

给导入的每一列设置一个标签，点击skipped根据弹出的选项设置即可。

导入K线\(Type – Bar\)数据列设置建议有以下选项：

DataTime、Open、High、Low、Close、Volumn。

导入交易\(Type – Trade\)数据列设置建议有以下选项：

DataTime、Price\(成交价\)、Size\(成交量\)、Direction\(方向\)。

导入报价\(Type –Quote\)数据列设置建议有以下选项：

DataTime、Bid、BidSize、Ask、AskSize。

例：时间设置

点击时间列的skipped，选择Date Time，可选择列表中弹出的时间格式，也可点击Custom 自行设置时间格式。时间格式可参考时间设置页面的Format help，如下图8和图9:

图 8 时间格式设置1

图 9 时间格式设置2

也可通过Advanced进行高级设置，点击Advanced，进入设置界面，通过 Other-Create instrument 可设置导入的数据存放在哪个分类下（默认为Stock），如下图10：

图 10 高级设置

全部设置好后，可点击Template右侧的Save ,将之前的设置存为模板。之后设置同样格式的数据文件时可选择模板然后点击Apply即可使用模版。然后点击Next，进入数据导入界面。

2.2导入数据

在数据导入页面，点击左上角的绿色小三角开始导入，等待导入完成后点击Close即可，如下图11：

图 11 导入数据

1. 查看导入数据

选择View-Instruments，点击导入数据存放的文件类，找到导入的数据，右键单击，在弹出菜单选择 Data，即可看到所导入的数据。如下图12、13、14：

图 12 查看数据菜单入口

图 13 查看数据

图 14 数据显示

