# Linux操作记录

## 8.31

- linux目录结构

![在这里插入图片描述](https://img-blog.csdnimg.cn/4e49557ffb994fae83b89c05bc551aa7.png) 

其中普通用户的文件都保存在/home下，home下保存了每个用户代表的文件夹。

常用文件介绍：

```

```

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

