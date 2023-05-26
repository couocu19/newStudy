# Linux操作记录

### linux目录结构

![在这里插入图片描述](https://img-blog.csdnimg.cn/4e49557ffb994fae83b89c05bc551aa7.png) 

其中普通用户的文件都保存在/home下，home下保存了每个用户代表的文件夹。

常用文件介绍：

### ~/，~，~/.

```
cd ~/
cd ~
cd ~/.
执行这三个命令的效果相同，都代表 /home/xx（xx代表当前登录的用户）
ps：
linux中.开头的文件夹都代表隐藏文件夹
可以通过 ls -a 查看所有文件，包括普通文件和隐藏文件
```

### 相对路径和绝对路径

```
绝对路径：
linux中是从‘/’开始开始指定文件的路径。
查看linux文件系统目录结构：
cd /
```

### 显示当前所在完整路径

```
pwd
```

### 目录操作

```
mkdir 创建文件夹
rmdir 删除当前文件夹
```

### vmware和windows共享文件夹失效的处理方法

```
sudo vmhgfs-fuse .host:/ /mnt/hgfs/ -o allow_other -o uid=1000
然后再次查看即可
```

### 防火墙设置服务器访问某个端口

```
eg：
iptables -A/I INPUT/OUTPUT -p tcp –dport (80) -j ACCEPT 

ps：必须切换成管理员用户才能使用该命令

-- --可是我的问题还是没有解决。。。。。。。。。。。。。。。。。。。。。。。。555555555555555555555555555555
```

### linux操作相关

```
1.tab补全文件名命令无效---待解决；
2.在linux上下载了 asprea方便之后下载数据；
3.解压文件 tar -zxvf (文件路径必须正确)
4.deepin下载命令  apt 
5.linux下查看fastq文件 
  zless+文件名称
  ps：zless可以用来查看被压缩的文件
```

### **Apt命令**

您可以通过以下命令来查看、安装、卸载、清理、升级等信息。

```
更新包列表	sudo apt-get update
安装/升级所有可用更新	sudo apt-get dist-upgrade
安装应用程序更新	sudo apt-get upgrade
dselect安装更新	sudo apt-get dselect-upgrade
查找软件包	sudo apt-cache search package
显示包相关信息	sudo apt-cache show package
显示系统安装统计信息	sudo apt-cache stats
显示包的相关依赖	sudo apt-cache depends package
安装软件	sudo apt-get install package
重装软件	sudo apt-get install package --reinstall
强制安装软件	sudo apt-get -f install package
卸载软件	sudo apt-get remove package
卸载软件及配置	sudo apt-get remove package --purge
清理旧版本软件缓存	sudo apt-get autoclean
清理所有软件缓存	sudo apt-get clean
清理不再使用的孤立软件	sudo apt-get autoremove
删除更新和升级的缓存软件	cd /var/cache/apt/archives && sudo rm *.deb
```

### head查看文件前k行数据

```
head -n k file_path
关于head命令
head 用来显示档案的开头至标准输出中，默认head命令打印其相应文件的开头10行。
-q 隐藏文件名,在多个文件名的情况下有效
-v 显示文件名
-c N 从头显示N字节的内容
-n N 从头显示N行
```

​     **显示文件的前10个字节**

```
head -c 10 1.txt
1
显示从文件头到倒数第N个字符的内容
N=-2 也就是除了文件末尾的两个字符不显示,其余都显示
head -c -2 1.txt

1
2
3
同时查看多个文件
//默认会显示文件名
head -n 5 1.txt 2.txt

==> 1.txt <==
vvv
ccc
123 9090
asd 123
123 444 99

==> 2.txt <==
入门小站
```

### **同时查看多个文件,不显示文件名**

> ```
> head -n 5 -q 1.txt 2.txt
> head -n 5 -q 1.txt 2.txt 
> vvv
> ccc
> 123 9090
> asd 123
> 123 444 99
> 入门小站
> ```

### **显示从文件开头到倒数第N行的内容**

```
> head -n -5 1.txt
> 1
> head输出文件M和N行之间的打印行（M>N）
> 输出文件第10(N=10)行到第20(M=20)行的内容
> head -n 20 1.txt | tail -10
> 1
> 输出当前目录下最近使用的3个文件
> ls -t | head -n 3
```

### linux修改文件名称

```
sodo mv old-file-name new-file-name
```

### linux 复制文件/文件夹

将某一个文件夹下的所有文件复制到另一个文件夹

```
cp -r /home/packageA /home/packageB
运行命令之后packageB文件夹下就有packageA文件夹了。
```

将某一个文件夹复制到另一个文件夹

```
cp -r /home/packageA/* /home/cp/packageB/
或
cp -r /home/packageA/. /home/cp/packageB/
这两种方法效果是一样的。
```



### cp命令各大参数解释

![1664358601701](D:\studyNodes\Linux操作记录.assets\1664358601701.png)

### linux查看是否存在自动杀死进程的命令

```
# 通过以下三种命令查看系统是否主动杀死程序进程
dmesg | egrep -i -B100 'killed process'

## 或:
egrep -i 'killed process' /var/log/messages
egrep -i -r 'killed process' /var/log

## 或:
journalctl -xb | egrep -i 'killed process'
```

### linux查看剩余内存

```
free -h
free -m
```

### linux清理内存/磁盘命令

https://blog.csdn.net/dark159735/article/details/122314198

```
若输入清理缓存命令后提示权限不够，则改为：
sudo sh -c "echo 1/2/3 > /proc/sys/vm/drop_caches"
活者 
echo 1|sudo /proc/...
```

### linux彻底关闭 oom自动杀死进程命令

```
1.关闭oom-killer
cat /proc/sys/vm/oom-kill
echo "0" > /proc/sys/vm/oom-kill
vi /etc/sysctl.conf
vm.oom-kill = 0
```

### 修改权限

```
chmod能改变权限，-R是目录下所有文件，777就是高权限（读、写、执行）
chmod -R 777 * 意思就是将当前目录下所有文件都给予777权限
```

### 查看某个文件的大小

```
du -h filename
```

### linux解压zip文件命令

```
unzip
```

### Linux下设置环境变量

具体：https://blog.csdn.net/an520_/article/details/125220048

```
export PATH = “/。。/。。/。。:$PATH”
"/。。/。。/。"代表的就是当前要设置的命令所在的文件夹路径
```

### nano命令退出

```
ctrl+X
nano命令介绍
nano是一个字符编辑软件，类似于vi/vim，比vi/vim简单方便快捷。
nano打开一个文件：
nano + 文件名称
```

### linux解压gz文件

```
gzip -d 压缩文件名称
```
### 查看文件的行数

```
wc 文件名称/路径
wc -l 查看当前文件有多少行内容
wc -w 查看当前文件有多少字数
wc -L 查看当前文件最长的一行有多少字数
```

### linux查看文件第n行的内容

```
sed    -n    '行数p'   文件名称

sed -n '1048576p' xaa
```
### linux输出文件指定内容的行数

```
grep -n "指定值" 文件名 | nl
其中，"-n"参数表示显示行号，"指定值"需要替换为要查找的内容，"文件名"需要替换为要查找的文件名。上述命令会输出符合条件的行的行号以及内容。
若要只输出行号，可以使用cut命令对结果进行截取，如下所示：
grep -n "指定值" 文件名 | cut -d: -f1
其中，"-d"参数表示使用冒号作为分隔符，"-f1"参数表示只保留结果的第一列，即行号。
```



### linux 按行数/大小拆分文件

```
1、以100行作为基本单位切分data.txt文件
【 split -l 100 data.txt result.txt 】
输出文件：result.txtab result.txtac…结尾以 aa ab ac…
2、结尾以数字作为切分的依据
【 split -l 100 data.txt result.txt -d 】
输出文件：result.txt00、result.txt01…
3、指定切割后的文件前缀名与后缀名
【 split -l 100 data.txt -d -a 4 data_ 】
说明：
1）-l 100：按100行切割
2）data_：指定切割后的文件前缀名
3）-d：指定切割后的文件后缀名为数字
4）-a 4：指定切割后的文件后缀名数字的长度
```

### **linux 压缩文件为zip文件**

```
压缩文件夹下的所有文件：
zip  文件夹名称 压缩后的文件名称
eg：
zip split-data/* split-data.zip
ps:
deflated 70% 代表压缩率为百分之70

压缩单个/多个文件：
zip [选项] 压缩包名 源文件或源目录列表
zip fs160.zip fs160.bed
```

### linux编写循环脚本

```
for 循环初始条件
do
	循环体
done

数字转字符串：
var1=123
var2 = “$var1”---->即转为字符串

字符串拼接
$value1=home
$value2=${value1}"="
echo $value2
把要添加的字符串变量添加{}，并且需要把$放到外面。
这样输出的结果是：home=，也就是说连接成功。
又如代码如下:

[root@localhost sh]# var1=http://www.3lian.com/etc/

[root@localhost sh]# var2=yum.repos.d/

[root@localhost sh]# var3=${var1}${var2}

[root@localhost sh]# echo $var3


```

第一次写脚本代码就成功！！！！

```shell
#!/bin/bash

tail=".bed"
for((i=1;i<=306;i=i+1))
do
   var="$i"
   var1="s"${var}
   var2="m"${var}
   var3="c"${var}
   
   fn=${var}${tail}
   sfn=${var1}${tail}
   bedtools sort -i $fn > $sfn
   
   mfn=${var2}${tail}
   bedtools merge -i $sfn > $mfn

   cfn=${var3}${tail}
   bedtools coverage -a S4257-chr.bed -b $mfn > $cfn
done
```



### linux查看当前文件夹下的文件个数

```
统计当前目录下文件的个数（不包括目录）
ls -l | grep "^-" | wc -l

统计当前目录下文件的个数（包括子目录）
ls -lR| grep "^-" | wc -l

查看某目录下文件夹(目录)的个数（包括子目录）
ls -lR | grep "^d" | wc -l
```

### linux vim定位到某一行修改

```
：n
n指的是要定位到的行数
```

### linux和windows下的文件---换行符的问题

```
windows下读取到的文件的换行符： '\r\n' (\r代表回车符)
linux/unix： '\n'
这会导致linux和windows互相读取文件的时候出现换行/数据长度的问题

```

### linux 断点续传

```
wget url 直接下载
wget url -c 断点续传

```

### linux 解压 rpm文件

```
rpm2cpio readline-devel-6.2-11.el7.aarch64.rpm | cpio -div
rpm2cpio readline-6.2-11.el7.src.rpm | cpio -div
```

### conda 下载指定版本的软件包

```
conda install scipy=0.15.0
```

#PBS -N test#PBS -q workq#PBS -l nodes=1:ppn=8#PBS -j oe

 ./configure --prefix=$HOME/biosoft/mummer-4.0.0rc1 && make && make install 

```
./configure --prefix=~/apps/mummer4
```

### linux中&符号的作用

```
在命令后加&表示将命令运行到后台去执行；

```

### linux为用户永久添加某一环境变量

```
vim ~/.bashrc
export PATH="/share/home/xiongchu/downloads/wise2.4.1/src/bin:$PATH"
source ~/.bashrc

```

### linux让命令在账号退出时也在后台运行的命令

```
$ nohup sh test.sh &  
# 直接关闭当前终端，再打开一个查看  
$ ps -few|grep test.sh 
ps -aux|grep exonerate --model protein2genome Reviewed.fasta Col-CEN_v1.2.fna --sh showtargetgff >res-handed2.gff

kill -15 40820
```

还有其它方法：（可以看这个链接）

https://blog.csdn.net/u012253351/article/details/125465975

### linux解压tar.bz2文件

```
eg：
wget -c https://github.com/bedops/bedops/releases/download/v2.4.39/bedops_linux_x86_64-v2.4.39.tar.bz2
tar jxvf bedops_linux_x86_64-v2.4.39.tar.bz2
```

### linux split命令分割文件

```
split [--help][--version][-<行数>][-b <字节>][-C <字节>][-l <行数>][要切割的文件][输出文件名]
参数说明：

-<行数> : 指定每多少行切成一个小文件
-b<字节> : 指定每多少字节切成一个小文件
--help : 在线帮助
--version : 显示版本信息
-C<字节> : 与参数"-b"相似，但是在切 割时将尽量维持每行的完整性
[输出文件名] : 设置切割后文件的前置文件名， split会自动在前置文件名后再加上编号

split -1048576 newgene-ann3.bed

```

### linux查看某个文件的创建时间

```
stat 文件名
该命令可以显示文件的所有属性，包括文件的大小、访问时间、修改时间和创建时间等。其中，文件的创建时间对应着输出结果中的“Birth”信息。

例如，要查看文件example.txt的创建时间，可以在终端输入以下命令：

```

### linux处理table型数据，提取其中的几列信息并输出为新文件

```
cut -f1,2,3 input.bed > temp.bed

cut -f1,2,3,8 newgene-ann-413.bed >newgene-ann-414.bed

```

### Linux提取文件的前n行内容到新的文件中

```
head -n 10 input.txt > output.txt
```

### linux合并多个文件

```
cat file1 file2 file3 > output_file
  例如，假设我们有两个名为 a.txt 和 b.txt 的文件，想将它们合并到一个名为 c.txt 的文件中，可以使用以下命令：
cat a.txt b.txt > c.txt
   执行上述命令后，a.txt 和 b.txt 中的内容就会被依次追加到 c.txt 文件中。需要注意的是，如果 c.txt 文件已经存在，执行该命令会将原有内容覆盖掉，因此在执行前最好备份一下目标文件。
```

### 压缩文件为gz格式

```
gzip [选项] 文件名
```

