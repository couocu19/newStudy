# Python数据分析代码记录

## 处理表格相关

- **去除表格中某一列为特定值的所有行**

可以使用pandas模块来处理表格数据，具体实现步骤如下：

1. 导入pandas模块

```python
import pandas as pd
```

2. 读取表格数据

```python
df = pd.read_excel('filename.xlsx')
```

3. 去除某一列为特定值的所有行

假设要去除第二列为0的所有行，可以使用以下代码：

```python
df = df[df.iloc[:,1] != 0]
```

其中，`iloc[:,1]`表示选取所有行的第二列数据，`!= 0`表示不等于0的数据。

4. 保存处理后的数据

```python
df.to_excel('new_filename.xlsx', index=False)
```

其中，`index=False`表示不保存索引列。

