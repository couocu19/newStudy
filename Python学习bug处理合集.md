# Python学习bug处理合集

## 8.28

- python console 报错

  解决：并没有解决，但是我打开另一个项目是好的，所以我默认我解决了。。。

- Terminal有报红 找不到。。。文件

  ```
  是由于本地默认禁止执行外部脚本
  输入 get-executionpolicy 查看执行政策
  默认显示Restricted
  输入 set-executionpolicy remotesigned 改变默认
  按上面要求输入
  Set-ExecutionPolicy -Scope CurrentUser
  输入：
  remotesigned
  
  然后重启power shell 问题解决
  ```


## 8.31

- 终端下载pip

```
python -m ensurepip
测试是否下载成功：
pip list
```

- 更新pip 版本

```
python -m pip install --upgrade pip
```

- 查看当前pip版本

```
pip -V
```

- 下载matplotlib报错

![1661918138856](D:\studyNodes\Python学习bug处理合集.assets\1661918138856.png)

解决：

```
pip install --upgrade matplotlib
```

