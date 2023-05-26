# R语言学习笔记

- 设置工作路径

```
setwd('D:\\Rbio')
```

- 查看工作路径

```
getwd()
```

- CMplot绘制SNP密度图代码

```
library(CMplot)
mydata<-read.table("SNP-fm160-ftl.csv",header=TRUE,sep="\t")
CMplot(mydata,plot.type="d",bin.size=1e3,col=c("darkgreen","yellow", "red"),file="jpg",memo="snp_density",dpi=300)
```

​      数据格式准备

```csv
SNP名称 染色体名称 物理位置
SNP_1_1	ref|NC_001133|	0
SNP_1_2	ref|NC_001133|	1376
SNP_1_3	ref|NC_001133|	1924
SNP_1_4	ref|NC_001133|	2445
SNP_1_5	ref|NC_001133|	5027
SNP_1_6	ref|NC_001133|	6734
SNP_1_7	ref|NC_001133|	11877
SNP_1_8	ref|NC_001133|	12175
SNP_1_9	ref|NC_001133|	12528
SNP_1_10	ref|NC_001133|	13006
SNP_1_11	ref|NC_001133|	14011
SNP_1_12	ref|NC_001133|	21739
SNP_1_13	ref|NC_001133|	23040
SNP_1_14	ref|NC_001133|	24283
SNP_1_15	ref|NC_001133|	24519
SNP_1_16	ref|NC_001133|	24944
SNP_1_17	ref|NC_001133|	25132
SNP_1_18	ref|NC_001133|	25439
SNP_1_19	ref|NC_001133|	25692
SNP_1_20	ref|NC_001133|	27479
SNP_1_21	ref|NC_001133|	28527
SNP_1_22	ref|NC_001133|	29007
SNP_1_23	ref|NC_001133|	29758
SNP_1_24	ref|NC_001133|	65497
```

  ps：

```csv
CMplot()函数中的参数 bin.size()需要根据实际情况设置，1e6代表表示1Mb内的snp位点的个数，适用于染色体长度为几百Mb的物种，对于类似于酵母这种比较短的，染色体最长只有1Mb的，需要将参数设置小一些，可以设置为1e3.
```

- R语言绘制SNP密度图（复杂图）

```
setwd("F:\\your path")
#安装软件
BiocManager::install("gtrellis")
library(gtrellis)
library(RColorBrewer)
library("circlize")
library("ComplexHeatmap")

## 导入数据
bed1<-read.table("bwa-new-yeast-chr.txt",head=T,sep='\t')
bed2<-read.table("mf4257-new-ftl-smpl-bw.txt",head=T,sep='\t')
## gene密度大小转换
gene_density = genomicDensity(bed2,window.size = 1e5)
#
col_fun = colorRamp2(seq(0, max(gene_density[[4]]),length=11),rev(brewer.pal(11, "RdYlBu")))
cm = ColorMapping(col_fun = col_fun)
#绘制坐标
lgd = color_mapping_legend(cm, plot = TRUE, title = "",color_bar="continuous")
## 调整位置
gtrellis_layout(bed1,byrow = F,ncol = 1,xpadding = c(0.1, 0),gap = unit(2, "mm"),
                border = FALSE,asist_ticks=FALSE,track_axis = FALSE,legend=lgd)
## 绘制gene密度图
add_heatmap_track(gene_density, gene_density[[4]], fill = col_fun,track=1)

## 添加染色体名称
add_track(track = 1, clip = FALSE, panel_fun = function(gr) {
  chr = get_cell_meta_data("name")
  if(chr == "ref|NC_001224|") {
    grid.lines(get_cell_meta_data("xlim"), unit(c(0, 0), "npc"),
               default.units = "native") }
  grid.text(chr,x =0.02, y = 0.38, just = c("left", "bottom"))
})
# 调整
add_track(track = 1, clip = FALSE, panel_fun = function(gr) {
  chr = get_cell_meta_data("name")
  grid.text(chr,x =0.02, y = 0.38, just = c("left", "bottom"))
})
```

- R语言查找未知函数来自哪个包

```
library(sos)
help(package="sos")
???函数名()
eg:
library(sos)
help(package="sos")
???ColorMapping()
```

- 修改后的绘制代码

```
library(gtrellis)
library(RColorBrewer)
library("circlize")
library("ComplexHeatmap")

## 导入数据
bed1<-read.table("bwa-new-yeast-chr.txt",head=F,sep='\t')
bed2<-read.table("mf4257-new-ftl-smpl-bw.txt",head=F,sep='\t')
## gene密度大小转换
gene_density = genomicDensity(bed2,window.size = 1e5)
#
col_fun = colorRamp2(seq(0, max(gene_density[[4]]),length=11),rev(brewer.pal(11, "RdYlBu")))
cm = ColorMapping(col_fun = col_fun)
#绘制坐标
lgd = color_mapping_legend(cm, plot = TRUE, title = "",color_bar="continuous")
## 调整位置
gtrellis_layout(bed1,byrow = F,ncol = 1,xpadding = c(0.1, -0.3),gap = unit(2, "mm"),
                border = FALSE,asist_ticks=FALSE,track_axis = FALSE,legend=lgd)
## 绘制gene密度图
add_heatmap_track(gene_density, gene_density[[4]], fill = col_fun,track=1)

## 添加染色体名称
add_track(track = 1, clip = FALSE, panel_fun = function(gr) {
  chr = get_cell_meta_data("name")
  if(chr == "ref|NC_001224|") {
    grid.lines(get_cell_meta_data("xlim"), unit(c(0, 0), "npc"),
               default.units = "native") }
  grid.text(chr,x =0.02, y = 0.38, just = c("left", "bottom"))
})
# 调整
add_track(track = 1, clip = FALSE, panel_fun = function(gr) {
  chr = get_cell_meta_data("name")
  grid.text(chr,x =0.02, y = 0.38, just = c("left", "bottom"))
})
```

- R直接运行所有代码

```
Ctrl+Shift+Enter
```

- 最终版--ggplot将酵母数据的每条染色体按照覆盖和未覆盖区域进行分区

```
library(ggplot2)#导入ggplot2包
a<-read.table(file = "fm160-all-bw.txt", header=F,quote="",sep="\t",stringsAsFactors=F)#读入数据

g<-sprintf("%s",unique(a[,4]))#选出染色体号，同时每个号码前加上Chr前缀，以备后面用来标记x轴
a[,6]<-a[,3]-a[,2]#提取每段长度
for(i in 1:length(a[,1])){
  if(a[i,4] == "chr1"){
    a[i,7]=1
  }else if(a[i,4] == "chr2"){
    a[i,7]=2
  }else if(a[i,4] == "chr3"){
    a[i,7]=3
  }else if(a[i,4] == "chr4"){
    a[i,7]=4
  }else if(a[i,4] == "chr5"){
    a[i,7]=5
  }else if(a[i,4] == "chr6"){
    a[i,7]=6
  }else if(a[i,4] == "chr7"){
    a[i,7]=7
  }else if(a[i,4] == "chr8"){
    a[i,7]=8
  }else if(a[i,4] == "chr9"){
    a[i,7]=9
  }else if(a[i,4] == "chr10"){
    a[i,7]=10
  }else if(a[i,4] == "chr11"){
    a[i,7]=11
  }else if(a[i,4] == "chr12"){
    a[i,7]=12
  }else if(a[i,4] == "chr13"){
    a[i,7]=13
  }else if(a[i,4] == "chr14"){
    a[i,7]=14
  }else if(a[i,4] == "chr15"){
    a[i,7]=15
  }else if(a[i,4] == "chr16"){
    a[i,7]=16
  }else{
    a[i,7]=17
  }
}  #总共有两组样本，为了区别分开，所以478的样本对应x坐标为染色体号-0.2，zheng58的样本对应x坐标为染色体号+0.2
colors<-c("red","blue")#三种分段，分别标记的颜色为红蓝绿，自己可以随意选取。

p<-ggplot(a,aes(x=a[,7],y=a[,6],fill=a[,5],group=a[,4]))+geom_bar(stat = "identity")+    #x轴选的是染色体号加减0.2的数据，以样本类别分组，以分段类别来填充。
  #geom_text(aes(label = a[,6]), size = 3, hjust = 0, vjust = 0,position = "stack",angle=45)+ #每个柱子的最上面添加注释样品类别信息
  theme_bw() + theme(panel.grid.major = element_blank(),
                     legend.position = c(0.9,0.9),legend.title=element_blank())+#去背景，同时调整legend的位置，以及去除legend的title
 
   scale_fill_manual(values = colors)+#设置填充的颜色
  scale_x_continuous(breaks = c(1:17),labels = g)+labs(x="",y="")+#自己设置x轴的刻度信息
  scale_y_continuous(labels = c(0,"0.5MB","1MB","1.5MB"))#设置y轴的刻度信息。

pdf(file = "result.pdf",height = 8,width = 10)
print(p)
dev.off()
png(filename = "result.jpg",type = "cairo",height = 700,width = 1100)
svg(filename = "result.svg",height = 12,width = 20)
print(p)
dev.off() 

```

- R语言svg函数参数学习(R语言将图片保存为矢量图的两种方法)

```
eg:
svg(filename = "result.svg",height = 12,width = 20)

svg(filename = if(onefile) "Rplots.svg" else "Rplot%03d.svg",          
    width = 7, height = 7, pointsize = 12,          
    onefile = FALSE, family = "sans", bg = "white",          
    antialias = c("default", "none", "gray", "subpixel"))
 
# 部分参数解释
antialias  # 字符串；要使用的抗锯齿状类型，默认为"default"
# 其他参数和pdf()一样。

如果使用ggplot2绘制图形，也可以使用ggsave()函数保存图形。
```

- R语言颜色表

![img](https://img-blog.csdnimg.cn/56f266f95f1542d3b0b2b7bab0747b29.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAYXdrX2Jpb2luZm8=,size_20,color_FFFFFF,t_70,g_se,x_16) 



- R语言中安装R包时不同的方法

```R
1.清华大学镜像
options(repos=c(CRAN="https://mirror.tuna.tsinghua.edu.cn/CRAN/"))
install.packages("scRNAseq")
2.github
if(!require(devtools)) install.packages('devtools')
devtools::install_github("kjhealy/socviz")
#其中kjhealy是Github网站的某个作者的名称， socviz是该作者名下的一个R扩展包。
3.Bioconductor
options(repos=c(CRAN="https://mirror.tuna.tsinghua.edu.cn/CRAN/"))
if (!requireNamespace("BiocManager", quietly = TRUE)){
  install.packages("BiocManager")
  BiocManager::install()
}
options(BioC_mirror="https://mirrors.tuna.tsinghua.edu.cn/bioconductor")
BiocManager::install(c("BiocStyle"))
```

- apply函数

```R
apply(
  x # 数组或矩阵
  MARGIN #应用函数的方向，1行2列 
  FUN # 应用的函数
)
# 返回值根据数据Data的数据类型与Fun的返回值自动判断返回的数据类型
```

