# Linux操作记录

## 8.31

- linux目录结构

![在这里插入图片描述](https://img-blog.csdnimg.cn/4e49557ffb994fae83b89c05bc551aa7.png) 

其中普通用户的文件都保存在/home下，home下保存了每个用户代表的文件夹。

常用文件介绍：

- ~/，~，~/.

```
cd ~/
cd ~
cd ~/.
执行这三个命令的效果相同，都代表 /home/xx（xx代表当前登录的用户）
ps：
linux中.开头的文件夹都代表隐藏文件夹
可以通过 ls -a 查看所有文件，包括普通文件和隐藏文件
```

- 相对路径和绝对路径

```
绝对路径：
linux中是从‘/’开始开始指定文件的路径。
查看linux文件系统目录结构：
cd /
```

- 显示当前所在完整路径

```
pwd
```

- 目录操作

```
mkdir 创建文件夹
rmdir 删除当前文件夹
```

- vmware和windows共享文件夹失效的处理方法

```
sudo vmhgfs-fuse .host:/ /mnt/hgfs/ -o allow_other -o uid=1000
然后再次查看即可
```

- 防火墙设置服务器访问某个端口

```
eg：
iptables -A/I INPUT/OUTPUT -p tcp –dport (80) -j ACCEPT 

ps：必须切换成管理员用户才能使用该命令

-- --可是我的问题还是没有解决。。。。。。。。。。。。。。。。。。。。。。。。555555555555555555555555555555
```

- linux操作相关

```
1.tab补全文件名命令无效---待解决；
2.在linux上下载了 asprea方便之后下载数据；
3.解压文件 tar -zxvf (文件路径必须正确)
4.deepin下载命令  apt 
5.linux下查看fastq文件 
  zless+文件名称
  ps：zless可以用来查看被压缩的文件
```

**Apt命令**
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

- head查看文件前k行数据

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


**同时查看多个文件,不显示文件名**
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


**显示从文件开头到倒数第N行的内容**
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

- ### linux修改文件名称

```
sodo mv old-file-name new-file-name
```

- ### linux 复制文件/文件夹

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



- ### cp命令各大参数解释

![1664358601701](D:\studyNodes\Linux操作记录.assets\1664358601701.png)