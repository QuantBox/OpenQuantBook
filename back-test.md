# **Back Test**

---

* ### 回测的速度

OpenQuant采用基于事件总线概念的架构体系，允许用户有效的利用多线程、缓存、负载均衡来构建分布式交易系统。除此之外，OpenQuant在执行层用可以预定义的高校简洁的执行消息代替了Fix消息，能够显著增加回测速度和减少内存消耗。得益于事件驱动机制和这些设计优点，OpenQuant拥有每秒钟处理百万数量级别事件的能力。

* ### 回测的相关菜单功能

点击菜单栏View，具体功能如下：

&lt;a&gt; Solution Explorer：解决方案资源管理器，策略的项目管理面板；

&lt;b&gt; Instruments：合约面板，导入的合约历史数据会在该面板中显示，双击后即可在主界面中展开详细数据信息；

&lt;c&gt; Account：当策略进行模拟交易或实盘交易时会显示交易的账户信息；

&lt;d&gt; Order Manager：订单管理器，包括策略中未完成、已完成、已取消、被拒绝的所有订单分类明细；

&lt;e&gt; Portfolios：投资组合管理，按照策略中交易的各个子策略分别进行权益、交易明细、权益和回撤的图形、绩效指标分析、子策略间相关性和权益比较等详细信息的展示；

&lt;f&gt; Chart：策略运行行情图，包括行情、交易时间点、交易数量、权益等；

&lt;g&gt; Chart\(Gapless\)：无间隔策略运行行情图，与&lt;f&gt;不同的是，去除了未交易的时间段展示；

&lt;h&gt; Strategy Monitor：策略监控，可以在运行策略前打开，运行策略时会显示相关信息；

&lt;i&gt; Strategy Manager：策略管理，可以管理各个子策略的监控或属性展示；

&lt;j&gt; Optimizers：优化，可以设置优化方案，包括暴力多核优化、传统多核优化、模拟退火多核优化、自适应模拟退火多核优化；

&lt;k&gt; Optimization Results：优化结果展示；

&lt;l&gt; Providers：插件面板，显示的是OQ自带的和您自行安装的第三方插件，主要用于提供交易接口、基础数据、历史数据、合约订阅、实时行情等；

&lt;m&gt; Provider Errors：插件提示错误信息，运行策略时显示；

&lt;n&gt; Quote Monitor：行情监控器；

&lt;o&gt; Output：输出界面，用于显示系统错误信息、Provider提示信息以及您的策略自定义的显示信息；

&lt;p&gt; Start Page：开始页面，每次打开OQ都会在代码编辑区显示出近期曾经使用的策略解决方案；

&lt;q&gt; Properties：属性界面，单击合约面板、插件面板或解决方案资源管理器界面等中的任一内容，都会在该面板中显示详细的属性。

* ### 回测的各项指标展示说明

OpenQuant提供了一系列的绩效指标，运行策略以后，打开View -&gt; Portfolios，选择Statistics。

![](/assets/PortfolioStatisticsDemo.png)





