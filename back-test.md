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

按照顺序列出如下：

**（1）Summary:**

Net Profit: $$ 净利润 = 毛利 - 毛损 $$

Gross Profit:$$毛利=\sum{盈利}$$

Gross Loss: $$毛损=\sum{亏损}$$

Drawdown Percent：$$期末权益回撤百分比=\frac{投资组合总权益期末值-历史最高值}{历史最高值}$$

Average Drawdown Percent: $$平均回撤百分比$$

Maximun Drawdown Percent: $$最大回撤百分比=\frac{投资组合总权益最高值产生之后出现的最低值-历史最高值}{历史最高值}$$

Profit Factor: $$盈亏比=\frac{毛利}{毛损}$$

Recovery Factor: $$恢复因子=\frac{净利润}{权益最大回撤值}$$

**（2）Trades:**

Num of Trades: $$总交易次数=\sum{交易次数}$$

Num of Winning Trades: $$总盈利交易次数=\sum{盈利次数}$$

Num of Losing Trades: $$总亏损交易次数=\sum{亏损次数}$$

Profitable Percent: $$盈利次数百分比=\frac{盈利交易次数}{总交易次数}$$

Averge Trade: $$平均收益=\frac{净利润}{总交易次数}$$

Averge Winning Trade: $$所有盈利交易的平均收益=\frac{毛利}{盈利交易次数}$$

Averge Losing Trade: $$所有亏损交易的平均收益=\frac{毛损}{亏损交易次数}$$

Payoff Ratio: $$平均盈亏比=\frac{盈利交易的平均收益值}{亏损交易的平均亏损值}$$

Average Maximun Adverse Excursion: $$多头为例：最大不利变动幅度均值=\frac{手数*(最低价-买入价)-手续费}{交易次数}$$

Average Maximun Favorable Excursion: $$多头为例：最大有利变动幅度均值=\frac{手数*(最高价-买入价)-手续费}{交易次数}$$

Average End Of Trade Drawdown: $$所有交易的回撤均值$$

Maximun Consecutive Winning Trades: $$最大连续盈利的交易次数$$

Maximun Consecutive Losing Trades: $$最大连续亏损的交易次数$$

Averge Trades Duration: $$平均持仓时间$$

**（3）Daily/Annual Returns:**

Daily Return Percent: $$日收益率$$

Averge Daily Return Percent: $$日平均收益率$$

Averge Annual Return Percent: $$年平均收益率=日平均收益率*年交易日数$$

Daily Return Percent Standard Deviation: $$日收益率标准差$$

Annual Return Percent Standard Deviation: $$年收益率标准差$$

Daily Return Percent Downside Risk: $$日化下行波动率=\sqrt{\frac{\sum{日收益率为正数的收益率^2}}{日收益率为负数的天数}}$$

Annual Return Percent Downside Risk: $$年化下行波动率=日化下行波动率*\sqrt{年交易日数}$$

Sharpe Ratio: $$夏普比率=\frac{投资组合预期收益率-无风险利率}{投资组合的标准差}$$

Sortino Ratio: $$索提诺比率=\frac{\sqrt{年交易日数}*日超额收益率均值}{年化下行波动率}$$

Compound Annual Growth Rate: $$年复合增长率=(\frac{现有价值}{基础价值})^{\frac{1}{年数}}-1$$

MAR Ratio: $$MAR比率=\frac{预期收益率}{最大回撤}$$

Value At Risk: $$VaR=总资本*(抽样分位数*收益率标准差)+收益率平均值$$

**PS：OpenQuant中年交易日数为252天**

* ### **手续费和滑点的处理**

可以通过设置ExecutionSimulator属性的CommissionProvider和SlippageProvider来设置手续费和滑点。

![](/assets/SetCommission.png)

也可以通过实现ICommissionProvider和ISlippageProvider接口来开发自己的手续费和滑点，或继承CommissionProvider和SlippageProvider类，重写GetCommission\(\)和GetPrice\(\)方法。默认的GetCommission\(\)和GetPrice\(\)方法如下。

```
public virtual double GetCommission(ExecutionReport report)
{
    double value = 0;

    switch(type)
    {
        case CommissionType.Absolute:
            value = commission;
            break;
        case CommissionType.Percent:
            value = commission * report.cumQty * report.avgPx;
            break;
        case CommissionType.PerShare:
            value = commission * report.cumQty;
            break;
        default:
            throw new NotSupportedException("Unknown commission type"+ type);        
    }

    if(value < minCommission)
        return minCommission

    return value;
}

public virtual double GetPrice(ExecutionReport report)
{
    double price = report.AvgPx;

    switch(report.side)
    {
        case OrderSide.Buy:
            price += price * slippage;
            break;
        case OrderSide.Sell:
            price -= price * slippage;
            break;    
            }
    return price;

}
```

* ### **分红派息**

Thanf提供的数据是已经过前复权预处理后的数据，前复权计算减去了相应的分红数据，这样回测会造成您在回测最开始的时间会默认已经取得所有回测时间段内的分红。建议提高手续费对冲这部分误差。

前复权后价格＝\[\(复权前价格-现金红利\)＋配\(新\)股价格×流通股份变动比例\]÷\(1＋流通股份变动比例\)

* ### **回测的成交原理**

OpenQuant的回测成交原理是下单后见价成交，成交价取决于报单价以及滑点的设置。需要注意的是，如果报单量大于交易总量，则仅部分成交。

### 



