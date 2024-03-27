# Basic data type
本模块提供了一个数据类型`Data`，作为本项目的基本数据类型；同时提供了用于组织、管理 `Data` 的类型`DataSet`。并在`Models_in_one.utilis.data.bulitin`中提供内建的相关数据库。

<note>
<p>本项目中的神经网络模型训练、部署、与操作系统、硬件的交互均使用<code>Data</code>类型</p>
</note>

**导入方法：**
```python 
from Models_in_one.utils import data
```

## Data类型

**导入方法：**
```python 
from Models_in_one.utils.data import Data
```

<deflist collapsible="true">
    <def title="content">
       <code>Data</code>类型对象的内容
    </def>
    <def title="type">
        <code>Data</code>类型对象的类型
    </def>
    <def title="to_tensor(device)">
        返回<code>device</code>设备上的<code>Tensor</code>对象
    </def>
    <def title="norm(**keyword_args)">
        计算范数
    </def>
</deflist>
<note>对于包含形状信息的内容（例如<code>list</code>与<code>Tensor</code>），其<code>type</code>属性包含其形状信息。</note>

你可以通过基本的赋值语句创建任何内容的`Data`变量，例如：

```python 
from Models_in_one.utils.data import Data
sample_data_int: Data = Data(1)
sample_data_list: Data = Data([1])
```

`Data`类型包含基本的加、减、乘、除法操作，例如：

```python 
from Models_in_one.utils.data import Data
sample_data_int: Data = Data(1)
sample_data_list: Data = Data([1, 3])
# 加法运算
sample_data_int_2: Data = sample_data_int + 1  # Data(2)
sample_data_int_3: Data = sample_data_int + Data(2)  # Data(3)
sample_data_list_2: Data = sample_data_list + 2  # Data([3, 5])
# 除法运算
sample_data_float: Data = sample_data_int / 1  # Data(1.)
sample_data_float_2: Data = sample_data_int / Data(2)  # Data(.5)
sample_data_list_3: Data = sample_data_list / 2  # Data([.5, 1.5])
```
<warning>当涉及到包含形状信息的内容的运算时，请仔细检查参与运算的变量形状是否有意义</warning>

`Data`类型支持与`pytorch`模块基本数据类型`Tensor`的互换，例如：

```python 
from Models_in_one.utils.data import Data
from torch import Tensor, cuda, device
# 获得设备信息
if cuda.is_available():
    device = device('cuda:0')
else:
    device = device('cpu')
tensor = Tensor(1).to(device)
data = Data(1)
tensor_from_data = data.to_tensor(device)
data_from_tensor = Data(tensor)
```

## DataSet类型
`DataSet`类型是参与神经网络训练的重要类型，它提供了关于有监督神经网络训练标签映射以及训练集组织的有关方法。

**导入方法：**
```python 
from Models_in_one.utils.data import DataSet
```

<deflist collapsible="true">
    <def title="all_sets: class variable">
        <a anchor="all_set">字典，记录所有已经创建过的<code>DataSet</code>类型变量</a>
    </def>
    <def title="mapping">
       <a anchor="dataset_mapping"><code>DataSet</code>类型对象内部的映射关系</a>
    </def>
    <def title="build_mapping(input_data, output_data)">
         <a anchor="dataset_mapping">建立<code>DataSet</code>类型对象的单一映射关系</a>
    </def>
    <def title="build_mappings(input_data_list, output_data_list)">
         <a anchor="dataset_mapping">批量建立<code>DataSet</code>类型对象的映射关系</a>
    </def>
    <def title="from_dict(input_dict, clear)">
         <a anchor="dataset_mapping">从字典建立<code>DataSet</code>类型对象的映射关系</a>
    </def>
    <def title="get_input_data()">
         <a anchor="get">返回<code>DataSet</code>类型对象的输入列表</a>
    </def>
    <def title="get_output_data()">
         <a anchor="get">返回<code>DataSet</code>类型对象的输出列表</a>
    </def>
    <def title="get(input_data, default)">
         <a anchor="get">返回<code>DataSet</code>类型对象中，<code>input_data</code>对应的输出</a>
    </def>
    <def title="get_size()">
         <a anchor="get">返回<code>DataSet</code>类型对象的映射数量</a>
    </def>
    <def title="clear()">
         <a anchor="get">清空<code>DataSet</code>类型对象</a>
    </def>
    <def title="invert(copy, new_name)">
         <a anchor="invert">调换<code>DataSet</code>类型对象的输入与输出</a>
    </def>
    <def title="generator(batch_size, _device_, shuffle)">
         <a anchor="data_generator"><code>DataSet</code>类型对象内容的生成器</a>
    </def>
    <def title="set_check_flag(check_flag): class method">
         <a anchor="data_2_2_7">修改<code>DataSet</code>类型对象类型检查状态</a>
    </def>
</deflist>

<warning>初始化一个<code>DataSet</code>类型的变量需要一个独有的数据库名称</warning>

<warning>注意，默认情况下，<code>DataSet</code>类型的变量对其内容物是类型敏感的，也就是说，你不能创建包含多种<code>Data</code>的<code>DataSet</code>变量。有关<code>DataSet</code>类型的映射类型，详情参见 <a anchor="data_2_2_7">DataSet中的类型检查</a></warning>

`DataSet`类型共有一个字典`DataSet.all_sets`记录所有已经创建过的`DataSet`类型变量，你可以使用`DataSet`类型变量创建时确定的名称进行索引。例如 ：
{id="all_set"}

```python
from Models_in_one.utils.data import DataSet
sample_dataset: DataSet = DataSet(name='sample_dataset')
DataSet.all_sets['sample_dataset']  # sample_dataset
```
### 在DataSet中添加映射关系 {id="dataset_mapping"}

`DataSet`类型使用内建属性`mapping`记录映射关系。提供了`build_mapping`与`build_mappings`方法逐一与批量添加映射关系：
```python
from Models_in_one.utils.data import Data, DataSet
sample_dataset_1: DataSet = DataSet(name='sample_dataset_1')
sample_dataset_2: DataSet = DataSet(name='sample_dataset_2')
# 单一添加映射关系: Data(1) -> Data(2)
input_data, output_data = Data(1), Data(2)
sample_dataset_1.build_mapping(input_data=input_data, output_data=output_data)
# 批量添加映射关系: Data(1) -> Data(2)；Data(3) -> Data(4)
input_data_list = [Data(1), Data(3)]
output_data_list = [Data(2), Data(4)]
sample_dataset_2.build_mappings(
                    input_data_list=input_data_list,
                    output_data_list=output_data_list
)
```
同时你也可以在构造函数中使用字典创建映射关系，或是使用方法`from_dict`：
```python
from Models_in_one.utils.data import Data, DataSet
mapping_relationships = {
   Data(1): Data(2),
   Data(3): Data(4)
}
sample_dataset_3: DataSet = DataSet(name='sample_dataset_3', init_dict=mapping_relationships)
sample_dataset_4: DataSet = DataSet(name='sample_dataset_4')
sample_dataset_4.from_dict(mapping_relationships, clear=True)
```
其中，`clear`表示是是否在添加映射关系前清零原数据集。

### 获得DataSet中的映射信息 {id="get"}

`DataSet`类型提供了`get_input_data`，`get_output_data`，`get`，`get_size`与`clear`方法查询、管理映射关系：
```python
from Models_in_one.utils.data import Data, DataSet
sample_dataset: DataSet = DataSet(name='sample_dataset')
# 获得映射的全部输入
input_data: list[Data] = sample_dataset.get_input_data()
# 获得映射的全部输出
output_data: list[Data] = sample_dataset.get_output_data()
# 获得single_input_data对应的输出
single_output_data: Data = sample_dataset.get(single_input_data, default=None)  # 找不到输入时返回None
single_output_data: Data = sample_dataset[single_input_data]  # 找不到输入时raise KeyError
# 获得数据集大小
mapping_size: int = sample_dataset.get_size()
# 清空数据集
sample_dataset.clear()
```
### 调换DataSet的输入与输出 {id="invert"}
`DataSet`类型提供了方法`invert`,该方法可以调换`DataSet`的输入与输出。`invert`方法的签名为：
```python 
Models_in_one.utils.data.DataSet.invert(
    copy: bool,          
    new_name: Optional[str] = None
) -> Optional[DataSet]
```
`copy`表示是否返回一个新的修改后的数据集。当`copy`为`True`时，将不修改原数据集，而是返回一个新的数据集，同时需要提供新数据集的名称`new_name`；当`copy`为`False`时，将直接修改原数据集并返回`None`。
### DataSet中的generator方法 {id="data_generator"}
`DataSet`类型提供了方法`generator`作为`DataSet`内容的生成器，可用于神经网络的训练与验证。`generator`方法的签名为：
```python 
Models_in_one.utils.data.DataSet.generator(
    batch_size: int,          # 一次生成的映射对数目
    _device_=None,            # 设置张量所在设备
    shuffle: bool = True      # 是否临时打乱数据集分布
) -> tuple[torch.Tensor]  # 返回张量
```
例如在神经网络模型训练中，对于训练集`train_dataset`，可以执行如下操作：
```python
from Models_in_one.utils.data import DataSet
train_dataset: DataSet = DataSet('train_dataset')
generator_for_train_dataset = train_dataset.generator(
    batch_size=batch_size,
    _device_=device,
    shuffle=shuffle
)
for batch, (x, y) in enumerate(generator_for_train_dataset):
	...  # do something here
```
这段代码会在每次循环中，给出新的`(x, y)`。

### DataSet中的类型检查 {id="data_2_2_7"}
本节负责介绍`DataSet`类型内建的类型检查功能

默认情况下`DataSet`类型会保证其内部建立的映射对类型两两一致。当第一个映射对被建立时，`DataSet`类型的变量记录该映射对的类型关系，后续使用方法`build_mapping`与`build_mappings`时，当构成映射关系的变量数据类型不一致时，会抛出异常`DataTypeError`：
```python 
from Models_in_one.utils.data import Data, DataSet
int_data_1 = Data(1)
int_data_2 = Data(2)
str_data = Data('str')
sample_dataset = DataSet('type_check')
# 数据映射关系为：int->int
sample_dataset.build_mapping(int_data_1, int_data_2)
# 数据映射关系为：int->str
sample_dataset.build_mapping(int_data_2, str_data)  # invalid input data mapping
# expect (<class 'int'>, <class 'int'>), got (<class 'int'>, <class 'str'>)
```
通常情况不需要关心`DataSet`类型内建的类型检查功能，只需要确保你建立的映射关系都是满足`DataSet`类型内建的类型检查要求。但是，如果**你明白并且确定你在做什么**，`DataSet`类型提供了一个方法`set_check_flag`用于关闭**全局的**类型检查功能：
```python
from Models_in_one.utils.data import DataSet
DataSet.set_check_flag(False)  # 关闭所有DataSet类型的变量的类型检查功能
DataSet.set_check_flag(True)  # 启用所有DataSet类型的变量的类型检查功能
```
<warning>
    <p>需要注意的是，当类型检查功能被重新启用时，<code>DataSet</code>会重新检查<code>DataSet.all_sets</code>中记录的所有数据库的类型关系，当遇到不满足要求的数据库，会抛出异常<code>DataTypeError</code>。</p>    
</warning>

```python
from Models_in_one.utils.data import Data, DataSet
# 关闭所有DataSet类型的变量的类型检查功能
DataSet.set_check_flag(False)
int_data_1 = Data(1)
int_data_2 = Data(2)
str_data = Data('str')
sample_dataset = DataSet('type_check')
# 数据映射关系为：int->int
sample_dataset.build_mapping(int_data_1, int_data_2)
# 数据映射关系为：int->str
sample_dataset.build_mapping(int_data_2, str_data)
# 重新启用所有DataSet类型的变量的类型检查功能
DataSet.set_check_flag(True)  # DataTypeError: 'invalid data type in type_check'
```
<warning>再次强调，如果你不明白并且不确定你在做什么，请不要关闭<code>DataSet</code>提供的类型检查功能！</warning>


## 模块级别函数
<deflist collapsible="true">
    <def title="merge_dataset(dataset_list, new_dataset_name)">
        <a anchor="merge">融合两个<code>DataSet</code>类型对象</a>
    </def>
    <def title="split_dataset(dataset, ratio, new_dataset_name_1, new_dataset_name_2, shuffle)">
       <a anchor="split">分割<code>DataSet</code>类型对象</a>
    </def>
    <def title="root_mean_square_error(y_true, y_pred)">
       <a anchor="RMSE">计算均方根误差</a>
    </def>
</deflist>

### DataSet融合 {id="merge"}
对于已经构建好的数据库，`Models_in_one.utils.data`模块提供了函数`merge_dataset`创建将多个数据库混合后的混合数据库。请保证各个数据库构成映射关系的变量数据类型一致。修改参与融合的数据库并不会影响合成后的数据库。函数`merge_dataset`签名为：
```python
Models_in_one.utils.data.merge_dataset(
    dataset_list: list[DataSet], 
    new_dataset_name: str
) -> DataSet
```
### DataSet分割 {id="split"}
对于已经构建好的数据库，`Models_in_one.utils.data`模块提供了函数`split_dataset`创建将数据库分割后的子数据库。修改原始数据库并不会影响分割后的数据库。函数`split_dataset`签名为：
```python
Models_in_one.utils.data.split_dataset(
    dataset: DataSet,
    ratio: float,
    new_dataset_name_1: str,
    new_dataset_name_2: str,
    shuffle: bool = True
) -> tuple[DataSet, DataSet]
```
`ratio`指定分割后第一个子数据库在原始数据库中的占比， `shuffle`指定分割前是否打乱原始数据库，如果原始数据库数据量不足以支撑分割，将抛出`ValueError`。

### 均方根误差 {id="RMSE"}
`Models_in_one.utils.data`模块提供了函数`root_mean_square_error`与`RMSE`计算两个列表之间的均方根误差：
```Python
Models_in_one.utilis.data.root_mean_square_error(
    y_true: list[Data], 
    y_pred: list[Data]
) -> Data
```
`RMSE`是`root_mean_square_error`别名

## 内建DataSets {id="built_in"}

`Models_in_one.utils.data`模块中提供了一些内建的标准`DataSet`类型数据库。这些数据库是在长度200mm，直径10mm的丝驱动单节段通用连续体机器人上采集到的末端位置信息到驱动丝长的映射。

你可以使用数据集名称在`DataSet.all_sets`中索引数据集，或者采用如下语句导入：
```python
from Models_in_one.utils.data.builtin import [Models_in_one.utils.data.builtin中对应变量名]
```
它们的名称以及内容列举如下：
<tabs>
    <tab title="单一数据库">
<table>
<tr><td><code>Models_in_one.utils.data.builtin</code>中对应变量名</td><td>数据集名称</td><td>采集轨迹</td><td>数据集大小</td></tr>
<tr><td><code>dataset_round_24</code></td><td>round_24</td><td>圆形，半径24mm</td><td>600</td></tr>
<tr><td><code>dataset_round_26</code></td><td>round_26</td><td>圆形，半径26mm</td><td>651</td></tr>
<tr><td><code>dataset_round_30</code></td><td>round_30</td><td>圆形，半径30mm</td><td>751</td></tr>
<tr><td><code>dataset_round_32</code></td><td>round_32</td><td>圆形，半径32mm</td><td>800</td></tr>
<tr><td><code>dataset_square_30</code></td><td>square_30</td><td>方形，边长60mm</td><td>751</td></tr>
<tr><td><code>dataset_square_32</code></td><td>square_32</td><td>方形，边长64mm</td><td>800</td></tr>
<tr><td><code>dataset_square_36</code></td><td>square_36</td><td>方形，边长72mm</td><td>901</td></tr>
<tr><td><code>dataset_square_40</code></td><td>square_40</td><td>方形，边长80mm</td><td>1000</td></tr>
<tr><td><code>dataset_round_24_2to1</code></td><td>round_24_2to1</td><td>圆形，半径24mm</td><td>600</td></tr>
<tr><td><code>dataset_round_26_2to1</code></td><td>round_26_2to1</td><td>圆形，半径26mm</td><td>651</td></tr>
<tr><td><code>dataset_round_30_2to1</code></td><td>round_30_2to1</td><td>圆形，半径30mm</td><td>751</td></tr>
<tr><td><code>dataset_round_32_2to1</code></td><td>round_32_2to1</td><td>圆形，半径32mm</td><td>800</td></tr>
<tr><td><code>dataset_square_30_2to1</code></td><td>square_30_2to1</td><td>方形，边长60mm</td><td>751</td></tr>
<tr><td><code>dataset_square_32_2to1</code></td><td>square_32_2to1</td><td>方形，边长64mm</td><td>800</td></tr>
<tr><td><code>dataset_square_36_2to1</code></td><td>square_36_2to1</td><td>方形，边长72mm</td><td>901</td></tr>
<tr><td><code>dataset_square_40_2to1</code></td><td>square_40_2to1</td><td>方形，边长80mm</td><td>1000</td></tr>
</table>
    </tab>
    <tab title="融合数据库">
    <table>
<tr><td><code>Models_in_one.utils.data.builtin</code>中对应变量名</td><td>数据集名称</td><td>包含单一数据库名称</td><td>数据集大小</td></tr>
<tr><td><code>dataset_round</code></td><td>round</td><td>round_24、round_26、round_30、round_32</td><td>2802</td></tr>
<tr><td><code>dataset_square</code></td><td>square</td><td>square_30、square_32、square_36、square_40</td><td>3452</td></tr>
<tr><td><code>dataset_all</code></td><td>all</td><td>round、square</td><td>6254</td></tr>
<tr><td><code>dataset_round_2to1</code></td><td>round_2to1</td><td>round_24_2to1、round_26_2to1、round_30_2to1、round_32_2to1</td><td>2802</td></tr>
<tr><td><code>dataset_square_2to1</code></td><td>square_2to1</td><td>square_30_2to1、square_32_2to1、square_36_2to1、square_40_2to1</td><td>3452</td></tr>
<tr><td><code>dataset_all_2to1</code></td><td>all_2to1</td><td>round_2to1、square_2to1</td><td>6254</td></tr>
</table>
    </tab>
</tabs>

> 名称未含有`2to1`的数据库，其类型信息为：`("<class 'list'> with (2,)", "<class 'list'> with (2,)")`；名称含有`2to1`的数据库，其类型信息为：`("<class 'torch.Tensor'> with torch.Size([2, 2])", "<class 'list'> with (2,)")`
{style="note"}

> 名称含有`2to1`的数据库，其物理意义是前后两个时刻的末端位置信息，映射到后一时刻的驱动丝长
{style="note"}