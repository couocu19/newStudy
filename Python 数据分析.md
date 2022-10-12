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

