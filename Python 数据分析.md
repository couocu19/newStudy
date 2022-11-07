# Python 数据分析

## 8.28

- 环境配置

  python3.7+anaconda

  ![1661656892645](C:\Users\couco\AppData\Local\Temp\1661656892645.png)

- python简单命令

```
cmd命令框退出python
1.ctrl+Z
2.quit()
3.exit()
```

- pycharm 配置python环境

![1661658383695](D:\studyNodes\Python 数据分析.assets\1661658383695.png)

- **数据分析概述**

​     1.数据获取；

​     2.探索分析与可视化；

​     3.预处理理论；

​     4.分析与建模；

​     5.模型评估。

- **python数据分析常用集成包**

```
1.Numpy 
   定义了更高级的数据结构
2.SciPy.org
   实现了很多数据科学相关的内容
3.matpltlib
   使用python实现可视化
4.sk-learn
   实现了数据挖掘领域的很多算法
5.pandas
   实现了神经网络所需要的模型
```

### step1：数据获取手段

1.数据仓库--将所有业务数据经汇总处理，构成数据仓库（**DW**）

2.监测与抓取

3.填写、日志、埋点

4.计算

- **数据库 VS 数据仓库**

  ```
  1.数据库面向业务存储，仓库面向主题存储；
  2.数据库针对应用，仓库针对分析；
  3.数据库组织规范，仓库可能冗余，相对变化更大，数据量更大。
  ```

- **检测与抓取**----即直接解析网页、接口、文件信息

  python抓取数据常用工具：

  ```
  urllib，urllib2，requests，scrapy，PhantomJS，beautifulSoup，Xpath（lxml）
  ```

- **填写、日志、埋点**

  1.用户填写信息；

  2.APP或网页埋点

  3.操作日志

- **计算**

  通过已有数据计算生成衍生数据



### 好用的数据学习网站

1.kaggle/阿里云 TIANCHI天池---数据竞赛网站

2.IMGENTET/Open Images---数据集网站

3.各领域统计数据（统计局、政府机构、公司财报等）



### 探索分析与可视化



## 8.31

- pandas读取数据简单操作

```
设置读取表格不省略中间列：
pd.set_option('display.max_columns', None)
```



## 10.6

- 数据分析理论铺垫

```
集中趋势：数据聚拢的一种衡量  eg：均值、中位数、众数、分位数
        四分位数
```

## 10.25

### pandas

导入

```
import pandas as pd
```

pandas读取csv文件

```
time = pd.read_csv(info, skiprows=[0], nrows=1, usecols=[6], header=None)   # 遍历时间列 但一个csv只读一次
rss = pd.read_csv(info, skiprows=[0], usecols=[4], header=None)     # 跳过第0行即表名行 遍历所有csv文件的rss列

1.filepath_or_buffer ： 各种文件的路径（a str，pathlib.Path或py._path.local.LocalPath），URL（包括http，ftp和S3位置）或带有read()方法的任何对象（例如打开的文件或 StringIO）
2.skiprows=[ ] : 指定读取csv文件时忽略的行号
3.nrows = 1: 指定读取的行数为1，即只读取第一行
4.usecols= [] : 指定读取的列数的列号
5.header = None : 指定不读取原始数据的表头即列名1
```

常用方法

```
df = pd.read("HR.csv")
df.mean()  //求csv文件均值
df.median()  //求csv文件中位数
df.quantile() //求csv文件的分位数，需要设置参数，如果不设置参数默认为求中位数
df.quantile(q=0.25)  //求四分位数
df.mode()  //求众数
df.std()  //求标准差
df.var()  //求方差
df.sum()  //求和
df.skew()  //求偏态系数
df.kurt()  //求峰态系数
```

### scipy.stats

介绍：

[SciPy](https://so.csdn.net/so/search?q=SciPy&spm=1001.2101.3001.7020)的统计模块是`scipy.stats`，其中有一个类是**连续分布**的实现，一个类是**离散分布**的实现。此外，该模块中还有很多用于**统计检验**的函数。 

导入

```
import scipy.stats as ss
或者
from scipy import stats
```

常用的分布函数

```
正态分布
ps：这里的正态分布指的是标准正太分布，即服从 X~N(0,1)的标准正态分布
ss.norm.pdf()  
ss.norm.ppf()
ss.norm.cdf()
ss.norm.rvs(size=)
卡方分布
ss.chi2....
t分布
ss.t...
F分布
ss.f...
泊松分布
ss.poisson...

注释：
名称：备注
rvs：产生服从指定分布的随机数
pdf：概率密度函数
cdf：累计分布函数-----即它为概率密度函数的积分
sf：残存函数（1-CDF）
ppf：分位点函数（CDF的逆）--------累计分布函数的反函数
isf：逆残存函数（sf的逆）
fit：对一组随机取样进行拟合，最大似然估计方法找出最适合取样数据的概率密度函数系数。
*离散分布的简单方法大多数与连续分布很类似，但是pdf被更换为密度函数pmf。

```

## 10.28

- python颜色代码

```
colors = '''#FFB6C1 LightPink 浅粉红

#FFC0CB Pink 粉红

#DC143C Crimson 深红/猩红

#FFF0F5 LavenderBlush 淡紫红

#DB7093 PaleVioletRed 弱紫罗兰红

#FF69B4 HotPink 热情的粉红

#FF1493 DeepPink 深粉红

#C71585 MediumVioletRed 中紫罗兰红

#DA70D6 Orchid 暗紫色/兰花紫

#D8BFD8 Thistle 蓟色

#DDA0DD Plum 洋李色/李子紫

#EE82EE Violet 紫罗兰

#FF00FF Magenta 洋红/玫瑰红

#FF00FF Fuchsia 紫红/灯笼海棠

#8B008B DarkMagenta 深洋红

#800080 Purple 紫色

#BA55D3 MediumOrchid 中兰花紫

#9400D3 DarkViolet 暗紫罗兰

#9932CC DarkOrchid 暗兰花紫

#4B0082 Indigo 靛青/紫兰色

#8A2BE2 BlueViolet 蓝紫罗兰

#9370DB MediumPurple 中紫色

#7B68EE MediumSlateBlue 中暗蓝色/中板岩蓝

#6A5ACD SlateBlue 石蓝色/板岩蓝

#483D8B DarkSlateBlue 暗灰蓝色/暗板岩蓝

#E6E6FA Lavender 淡紫色/熏衣草淡紫

#F8F8FF GhostWhite 幽灵白

#0000FF Blue 纯蓝

#0000CD MediumBlue 中蓝色

#191970 MidnightBlue 午夜蓝

#00008B DarkBlue 暗蓝色

#000080 Navy 海军蓝

#4169E1 RoyalBlue 皇家蓝/宝蓝

#6495ED CornflowerBlue 矢车菊蓝

#B0C4DE LightSteelBlue 亮钢蓝

#778899 LightSlateGray 亮蓝灰/亮石板灰

#708090 SlateGray 灰石色/石板灰

#1E90FF DodgerBlue 闪兰色/道奇蓝

#F0F8FF AliceBlue 爱丽丝蓝

#4682B4 SteelBlue 钢蓝/铁青

#87CEFA LightSkyBlue 亮天蓝色

#87CEEB SkyBlue 天蓝色

#00BFFF DeepSkyBlue 深天蓝

#ADD8E6 LightBlue 亮蓝

#B0E0E6 PowderBlue 粉蓝色/火药青

#5F9EA0 CadetBlue 军兰色/军服蓝

#F0FFFF Azure 蔚蓝色

#E0FFFF LightCyan 淡青色

#AFEEEE PaleTurquoise 弱绿宝石

#00FFFF Cyan 青色

#00FFFF Aqua 浅绿色/水色

#00CED1 DarkTurquoise 暗绿宝石

#2F4F4F DarkSlateGray 暗瓦灰色/暗石板灰

#008B8B DarkCyan 暗青色

#008080 Teal 水鸭色

#48D1CC MediumTurquoise 中绿宝石

#20B2AA LightSeaGreen 浅海洋绿

#40E0D0 Turquoise 绿宝石

#7FFFD4 Aquamarine 宝石碧绿

#66CDAA MediumAquamarine 中宝石碧绿

#00FA9A MediumSpringGreen 中春绿色

#F5FFFA MintCream 薄荷奶油

#00FF7F SpringGreen 春绿色

#3CB371 MediumSeaGreen 中海洋绿

#2E8B57 SeaGreen 海洋绿

#F0FFF0 Honeydew 蜜色/蜜瓜色

#90EE90 LightGreen 淡绿色

#98FB98 PaleGreen 弱绿色

#8FBC8F DarkSeaGreen 暗海洋绿

#32CD32 LimeGreen 闪光深绿

#00FF00 Lime 闪光绿

#228B22 ForestGreen 森林绿

#008000 Green 纯绿

#006400 DarkGreen 暗绿色

#7FFF00 Chartreuse 黄绿色/查特酒绿

#7CFC00 LawnGreen 草绿色/草坪绿

#ADFF2F GreenYellow 绿黄色

#556B2F DarkOliveGreen 暗橄榄绿

#9ACD32 YellowGreen 黄绿色

#6B8E23 OliveDrab 橄榄褐色

#F5F5DC Beige 米色/灰棕色

#FAFAD2 LightGoldenrodYellow 亮菊黄

#FFFFF0 Ivory 象牙色

#FFFFE0 LightYellow 浅黄色

#FFFF00 Yellow 纯黄

#808000 Olive 橄榄

#BDB76B DarkKhaki 暗黄褐色/深卡叽布

#FFFACD LemonChiffon 柠檬绸

#EEE8AA PaleGoldenrod 灰菊黄/苍麒麟色

#F0E68C Khaki 黄褐色/卡叽布

#FFD700 Gold 金色

#FFF8DC Cornsilk 玉米丝色

#DAA520 Goldenrod 金菊黄

#B8860B DarkGoldenrod 暗金菊黄

#FFFAF0 FloralWhite 花的白色

#FDF5E6 OldLace 老花色/旧蕾丝

#F5DEB3 Wheat 浅黄色/小麦色

#FFE4B5 Moccasin 鹿皮色/鹿皮靴

#FFA500 Orange 橙色

#FFEFD5 PapayaWhip 番木色/番木瓜

#FFEBCD BlanchedAlmond 白杏色

#FFDEAD NavajoWhite 纳瓦白/土著白

#FAEBD7 AntiqueWhite 古董白

#D2B48C Tan 茶色

#DEB887 BurlyWood 硬木色

#FFE4C4 Bisque 陶坯黄

#FF8C00 DarkOrange 深橙色

#FAF0E6 Linen 亚麻布

#CD853F Peru 秘鲁色

#FFDAB9 PeachPuff 桃肉色

#F4A460 SandyBrown 沙棕色

#D2691E Chocolate 巧克力色

#8B4513 SaddleBrown 重褐色/马鞍棕色

#FFF5EE Seashell 海贝壳

#A0522D Sienna 黄土赭色

#FFA07A LightSalmon 浅鲑鱼肉色

#FF7F50 Coral 珊瑚

#FF4500 OrangeRed 橙红色

#E9967A DarkSalmon 深鲜肉/鲑鱼色

#FF6347 Tomato 番茄红

#FFE4E1 MistyRose 浅玫瑰色/薄雾玫瑰

#FA8072 Salmon 鲜肉/鲑鱼色

#FFFAFA Snow 雪白色

#F08080 LightCoral 淡珊瑚色

#BC8F8F RosyBrown 玫瑰棕色

#CD5C5C IndianRed 印度红

#FF0000 Red 纯红

#A52A2A Brown 棕色

#B22222 FireBrick 火砖色/耐火砖

#8B0000 DarkRed 深红色

#800000 Maroon 栗色

#FFFFFF White 纯白

#F5F5F5 WhiteSmoke 白烟

#DCDCDC Gainsboro 淡灰色

#D3D3D3 LightGrey 浅灰色

#C0C0C0 Silver 银灰色

#A9A9A9 DarkGray 深灰色

#808080 Gray 灰色

#696969 DimGray 暗淡灰

#000000 Black 纯黑'''
```





## 11.3

- 确定一组数据的正常值的范围

```
q_low=上四分位数
q_high=下四分位数
q_interval=q_high-q_low
k=间隔数（一般在1.5到3之间）
(q_low-k*q_interval)≤x≤(q_high+k*q_interval)
上下界之间的就是通常说的“正常值”信息

去掉当前组数据的异常数据：
les=les[les<q_high+k*q_interval][les>q_low-k*q_interval]
```

- 求数据的分布直方图 //

```
  np.histogram(les,values,bins=np.arange(0.0,1.1,0.1))
```



## 11.6

- 求一组数据中各个值的占比

  （静态结构分析）

```
假设某一组数据为nb，求nb这一列的数据各个值得分布：
nb.value_count(normalize=True) （得到占比）
4    0.290961
3    0.270297
5    0.184042
2    0.159379
6    0.078256
7    0.017064

nb.value_counts()  （得到数量）
4    4365
3    4055
5    2761
2    2391
6    1174
7     256

nb.value_counts(normalize=True).sort_index() （占比＋排序）
2    0.159379
3    0.270297
4    0.290961
5    0.184042
6    0.078256
7    0.017064
```

- 一组数据的标准差和方差反应的是什么?

```
标准差和方差反映数据的什么特征
反映的是一组数据的集中与离散程度、波动与稳定状况，一般的标准差和方差越小说明数据越集中、越稳定，反之越础散。当然还要是具体情况而定.
```

- 处理csv文件时快速查看每一组数据的属性

​       df.describe()

- 消除某组数据中的异常值

  ```
  s=data
  
  s.value_count() ----->通过结果检索异常值
  
  假设异常值为 "nme"
  
  消除异常值：
  
  s.where(s!="nme").dropna()
  ```

  

- 求某个csv数据按照某个属性分组后的某一列的极差值

```
df.loc[:,["average_monthly_hours","department"]].groupby("department")["average_monthly_hours"].apply(lambda x:x.max() - x.min())
```

- 可视化分析

todo：提上日程的事情：每天至少看3个数分的视频！！！！



## 11.7

- sns绘制柱状图

  ```
  sns.countplot(x="salary",hue="department",data=df)
  真的好方便好厉害。。优秀。。。。。。
  ```

  ![1667816868720](D:\studyNodes\Python 数据分析.assets\1667816868720.png)

- 箱线图

  sns.boxplot

  参数：saturation：设定正常值范围的分位数点，例如设置四分位数： sa=0.75

  ​           whis：就是在求异常值时设定的k值，即设定几个间隔interval

![1667824715690](D:\studyNodes\Python 数据分析.assets\1667824715690.png)

- 