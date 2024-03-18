# Logger

## 日志文件模块（Models_in_one.Log）

`Models_in_one`模块提供日志类`Log`，用于显示或将日志写入文件，该类不能被实例化，请使用类方法。

**导入方法：**
```python 
from Models_in_one import Log
```

<deflist collapsible="true">
<def title="init(file_name): class method">
<a anchor="init">初始化设定<code>Logger</code></a>
</def>
<def title="info(content, has_time): class method">
<a anchor="info">info级别消息</a>
</def>
<def title="warning(content, has_time): class method">
<a anchor="info">warning级别消息</a>
</def>
<def title="error(content, has_time): class method">
<a anchor="info">error级别消息</a>
</def>
<def title="speak(levels): class method">
<a anchor="output">打开相应级别的消息显示</a>
</def>
<def title="shutup(levels): class method">
<a anchor="output">关闭对应级别的消息显示</a>
</def>
</deflist>

### 指定日志文件位置 {id="init"}
你可以采用如下方法声明本程序日志将写入的位置。未调用此方法则不写入文件。
```python
Log.init(file_name = 'sample.log')
```

### 标注日志 {id="info"}
`Log`类型提供`info`， `warning`， `error`三种类方法对应不同级别的日志。当调用这些方法时，你需要提供一个包含元组的列表，具体如下：
```python
content = [('字段1', '该字段的颜色'), ('字段2', '该字段的颜色'), ...]
Log.info(content=content)
```
字段的颜色可以选择如下：

<table>
<tr><td>值</td><td>颜色名</td><td>颜色</td></tr>
<tr><td>'lw'</td><td>亮白色</td><td><format color="White">███</format></td></tr>
<tr><td>'ly'</td><td>亮黄色</td><td><format color="Yellow">███</format></td></tr>
<tr><td>'lr'</td><td>亮红色</td><td><format color="Red">███</format></td></tr>
<tr><td>'lc'</td><td>亮青色</td><td><format color="Cyan">███</format></td></tr>
<tr><td>'lb'</td><td>亮蓝色</td><td><format color="Blue">███</format></td></tr>
</table>

当字段的颜色留空时，默认为亮白色。这些颜色不会写入日志文件中。
`info`， `warning`， `error`三种类方法同时接受一个`bool`类型的变量`has_time`，用于表示是否记录产生日志的时刻。

### 屏幕显示 {id="output"}
`Log`类型提供`shutup`， `speak`两种类方法关闭与打开日志显示。这些方法接受一个列表，列表的内容可以包含`'info'`，`'warning'`，`'error'`三个值，用于表示作用的等级。不传入列表时表示作用于全部等级。这些方法不会影响日志文件的写入。
```python
Log.shutup()  # 关闭全部输出
Log.shutup(['info'])  # 关闭info等级的输出
Log.shutup(['info', 'warning'])  # 关闭info以及warning等级的输出

Log.speak()  # 打开全部输出
Log.speak(['info'])  # 打开info等级的输出
Log.speak(['info', 'warning'])  # 打开info以及warning等级的输出
```