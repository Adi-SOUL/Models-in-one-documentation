# File IO


该模块提供用于数据文件读写的类型`DataFile`。

**导入方法：**
```python 
from Models_in_one.utils.file_io import DataFile
```
## <span id=file_1>DataFile类型</span>

<deflist collapsible="true">
<def title="write(content, func, ending)">
    向文件写入内容
</def>
<def title="write_lines(content, func, ending)">
    向文件写入多行内容
</def>
<def title="read_lines(func)">
    从文件读取多行内容
</def>
</deflist>

标准的做法是，使用python提供的上下文管理器操作`DataFile`类型：
```python
from Models_in_one.utils.file_io import DataFile
with DataFile('sample_file.txt', 'r', 'utf-8') as sample_file:
	...  # do something here
```
当然你也可以：
```python
from Models_in_one.utils.file_io import DataFile
data_file = DataFile('sample_file.txt', 'r', 'utf-8')
sample_file = data_file.open()
...  # do something here
sample_file.close()  # 别忘了这一步
data_file.close()  # 这样写也可以
```
`DataFile`类型提供了更方便的读写方法。`write`、`write_lines`与`read_lines`方法可以接受一个函数对象`func`作为对每一个或是每一行写入对象的操作方法。
三种方法的签名如下：
<note>
当没有传入<code>func</code>时，与python默认同名用法一致。
</note>

```python
Models_in_one.utils.file_io.DataFile.write(
    content, 
    func, 
    ending: str = '\n'
) -> None

Models_in_one.utils.file_io.DataFile.write_lines(
    content: list, 
    func, 
    ending: str = '\n'
) -> None

Models_in_one.utils.file_io.DataFile.read_lines(
    func
) -> list
```
例如，你可以很方便地写入<path>.csv</path>文件：
```python
from Models_in_one.utils.file_io import DataFile
from Models_in_one.utils.data import Data

def write_csv(content: Data) -> str:
	to_file: str = ','.join([str(x) for x in content.content])
	return to_file

sample_data: Data = Data([1, 2, 3])
with DataFile('sample_csv.csv', 'w', 'utf-8') as sample_csv:
	sample_csv.write(func=write_csv, content=sample_data)
```

## <span id=file_2>模块级别函数</span>
<deflist collapsible="true">
<def title="time_for_filename()">
    返回当前时间字符串
</def>
</deflist>

<code-block lang="python">
from Models_in_one.utils.file_io import time_for_filename
string = time_for_filename()
print(string)
# 20240501_155339
</code-block>