# Hardware

本项目与硬件交互的方式主要为python与动态链接库（<path>.dll</path>）的交互。本模块提供与动态链接库（<path>.dll</path>）交互的必要类型，包括基类<code>DllBase</code>，NDI光学测量单元交互的<code>NDIReader</code>，以及固高运动控制卡交互类型<code>MotorController</code>与<code>MotorJogMode</code>。

> 涉及`pyads`模块的操作请参阅：[pyads模块官方文档](https://pydas.readthedocs.io/en/latest/)

**导入方法：**
```python 
from Models_in_one.utils import hardware
```
<note>
如果你不清楚python如何与动态链接库交互，或是不清楚如何创建动态链接库，请参阅：
<procedure title="">
<p>Microsoft： <a href="https://learn.microsoft.com/zh-cn/cpp/build/walkthrough-creating-and-using-a-dynamic-link-library-cpp?view=msvc-170">使用C++编写自己的动态链接库</a></p>
<p>博客：<a href="https://www.cnblogs.com/FHC1994/p/11421229.html">使用python调用动态链接库</a></p>
<p>Python doc： <a href="https://docs.python.org/3/library/ctypes.html">ctypes</a></p>
</procedure>
</note>

<warning>由于硬件操作的特殊性，你不应该在一个项目中多次实例化同一个硬件交互类型</warning>

## 动态链接库（.dll）交互类型（DllBase）

**导入方法：**
```python 
from Models_in_one.utils.hardware import DllBase
```

`DllBase`类型的签名如下，所有硬件交互类型均应当继承自`DllBase`类型：
```python
Models_in_one.utils.dll_helper.DllBase(
    dll_path        : str
)
```

## NDI交互类型（NDIReader）

**导入方法：**
```python 
from Models_in_one.utils.hardware.NDI import NDIReader
```

<deflist collapsible="true">
<def title="get_position()">
获得NDI标记球（或磁导航标记）在坐标系中的位置
</def>
</deflist>

`NDIReader`类型用于与NDI光学测量单元交互，签名如下：
```python
Models_in_one.utils.hardware.NDI.NDIReader(
    rom:  str   # .rom 文件位置
    mode: str   # in ['Auto', 'Optical', 'Aurora]
)
```

**当创建`NDIReader`实例对象时，程序会初始化NDI设备。你不需要提供NDI接入的COM号，程序会自动扫描NDI的接入情况。**`NDIReader`类型提供`get_position`方法，
方法返回一个元组，元组的第一个值为一个`bool`类型变量，用于表示是否成功获得标记球位置，第二个值为一个`Data`类型变量，该变量的意义与所连接的设备相关：
```python
from Models_in_one.utils.hardware.NDI import NDIReader
ndi_reader = NDIReader('./sample.rom', mode='Auto')
res_flag, position = ndi_reader.get_position()
```
根据设定的mode参数，NDIReader 拥有不同的表现：

| `mode`  | 作用                                    | 对应`get_position`方法返回值            |
|---------|---------------------------------------|----------------------------------|
| Auto    | NDIReader自动识别设备为光学或电磁测量单元，优先连接电磁测量单元。 | 见下                               |
| Optical | 连接光学测量单元。                             | 返回标记球在<path>.rom</path>文件坐标系下的位置 |
| Aurora  | 连接电磁测量单元。                             | 返回各个磁导航标记的转换矩阵                   |


<warning>当同时使用多个测量单元时，请不要使用<code>Auto</code>模式。</warning>
<note>
<code>Models_in_one</code>在目录<path>./others/NDI_rom</path>下提供了一些标定过的<path>.rom</path>文件，请结合实际坐标系合理使用！
</note>

```python
ROM_PATH_20220325 = './others/NDI_rom/20220325.rom'
ROM_PATH_20221121 = './others/NDI_rom/20221121.rom'
ROM_PATH_20230914 = './others/NDI_rom/20230914.rom'
```

## 固高运动控制卡交互类型（MotorController与MotorJogMode）
<warning><code>MotorController</code>与<code>MotorJogMode</code>不能同时实例化！</warning>

### MotorController （电机运动控制类型）

**导入方法：**
```python 
from Models_in_one.utils.hardware.Motors import MotorController
```

<deflist collapsible="true">
<def title="move(displacements)">
<a anchor="move">按照指指定丝位移驱动电机</a>
</def>
<def title="tense(displacement)">
<a anchor="tense">按照指定丝位移张紧所有驱动丝</a>
</def>
<def title="slack(displacement)">
<a anchor="slack">按照指定丝位移松弛所有驱动丝</a>
</def>
<def title="open()">
<a anchor="open">打开所有电机</a>
</def>
<def title="close()">
<a anchor="close">关闭所有电机</a>
</def>
</deflist>

```python
from Models_in_one.utils.hardware.Motors import MotorController
motor = MotorController()
```
#### `move` {id="move"}

`move`方法接受一个参数用于指定电机运动的距离（**以驱动丝位移为准，mm**）。该参数可以为`list`或者`Data`类型，当为`list`类型式，其内容类型必须为`float`或是`Data[float]`，当为`Data`类型时，其内容类型必须为`list[float]`。**所有`list`类型变量长度必须为2或者4，当`list`类型变量长度为4时，分别指定各个电机运动量，当`list`类型变量长度为2时，按照拮抗方式指定电机运动量：**
```python
from Models_in_one.utils.data import Data
data_1 = Data([1., 2., 3., 4.])
list_1 = [1., 2., 3., 4.]
list_2 = [Data(1.), Data(2.), Data(3.), Data(4.)]
motor.move(data_1)  # 与motor.move(list_1), motor.move(list_2)相同
data_2 = Data([1., 2.])
motor.move(data_2)  # 与motor.move(Data([1., 2., -1., -2.]))相同
```
#### `tense` {id="tense"}

`tense`方法接受一个参数用于指定所有电机**向着驱动丝张紧方向的**运动距离（**以驱动丝位移为准，mm**）。该参数可以为`float`或者`Data[float]`类型。
```python
from Models_in_one.utils.data import Data
motor.tense(Data(5.))  # 与motor.move(Data([5., 5., 5., 5.]))相同
```
#### `slack` {id="slack"}

`slack`方法接受一个参数用于指定所有电机**向着驱动丝松弛方向的**运动距离（**以驱动丝位移为准，mm**）。该参数可以为`float`或者`Data[float]`类型。
```python
from Models_in_one.utils.data import Data
motor.slack(Data(5.))  # 与motor.move(Data([-5., -5., -5., -5.]))相同
```

#### `open` {id="open"}

该方法可以打开电机。
```python
motor.open()
```

#### `close` {id="close"}

该方法可以关闭电机。
```python
motor.close()
```


### MotorJogMode （电机运动复位类型）

**导入方法：**
```python 
from Models_in_one.utils.hardware.Motors import MotorJogMode
```

<deflist collapsible="true">
<def title="move(command)">
<a anchor="move_j">按照指令驱动电机</a>
</def>
<def title="open()">
<a anchor="open_j">打开所有电机</a>
</def>
<def title="close()">
<a anchor="close_j">关闭所有电机</a>
</def>
</deflist>

```python
from Models_in_one.utils.hardware.Motors import MotorJogMode
motor = MotorJogMode()
```
#### `move` {id="move_j"}

`move`方法接受一个字符参数指定进行运动的电机以及运动方向，可选的字符参数列举如下：
```python
command: str
motor.move(command)
```
| `command` | 作用                |
|-----------|-------------------|
| w         | #2 Up Forward     |
| s         | #3 Down Forward   |
| a         | #1 Left Forward   |
| d         | #4 Right Forward  |
| i         | #2 Up Back Off    |
| k         | #3 Down Back Off  |
| j         | #1 Left Back Off  |
| l         | #4 Right Back Off |
| q         | #5 Forward        |
| e         | #5 Back off       |
| 0         | Kill all          |

<warning>
调用<code>move</code>方法并不会中止之前的调用，如需停止电机，请使用
<code-block lang="python">
motor.move('0')
</code-block>
</warning>

#### `open` {id="open_j"}

该方法可以打开电机。
```python
motor.open()
```

#### `close` {id="close_j"}

该方法可以关闭电机。
```python
motor.close()
```