# Hardware

本项目与硬件交互的方式主要为python与动态链接库（<path>.dll</path>）的交互。本模块提供与动态链接库（<path>.dll</path>）交互的必要类型，包括基类<code>DllBase</code>，NDI光学/电磁测量单元交互的<code>NDIReader</code>，读取光纤数据的<code>LUNA</code>与<code>CompatibleLUNA</code>类型，以及固高运动控制卡交互类型<code>MotorController</code>与<code>MotorJogMode</code>。

> 涉及`pyads`模块的操作请参阅：[pyads模块官方文档](https://pydas.readthedocs.io/en/latest/)

**导入方法：**
```python 
from Models_in_one.utils import hardware
```
<note>
如果你不清楚python如何与动态链接库交互，或是不清楚如何创建动态链接库，请参阅：
<procedure title="">
<p>Microsoft： <a href="https://learn.microsoft.com/zh-cn/cpp/build/walkthrough-creating-and-using-a-dynamic-link-library-cpp?view=msvc-170">使用C++编写自己的动态链接库</a></p>
<p>博客： <a href="https://www.cnblogs.com/FHC1994/p/11421229.html">使用python调用动态链接库</a></p>
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

## TensionSensor交互类型（TensionSensor）

**导入方法：**
```Python
from Models_in_one.utils.hardware.TensionSensor import TensionSensor
```

<deflist collapsible="true">
<def title="get_data(channel: Optional[int] = None)">
获得TensionSensor指定通道 <code>channel</code> 下的传感器度数
</def>
</deflist>

`TensionSensor`类型用于与TensionSensor力传感器交互，签名如下：
```python
Models_in_one.utils.hardware.TensionSensor.TensionSensor(
    port_name: str,   # 端口名称 
    baudrate: int,    # 波特率
    parity: int,      # 校验方式， 0：无校验，1：奇校验，2：偶校验
    databit: int,     # 1字节的位数，7 or 8
    stopbit: int      # 停止位
)
```

当使用 <code>get_data(channel)</code> 方法时，会以<code>Data</code>类型返回指定通道传感器的度数，当<code>channel</code>为<code>None</code>
或者为空时，以<code>List[Data]</code> 类型返回8个通道的度数。

## ForceSensor交互类型（ForceSensor， CompatibleForceSensor）

**导入方法：**
```python 
from Models_in_one.utils.hardware.ForceSensor import ForceSensor
```

### ForceSensor
<code>ForceSensor</code>类型提供读取<path>ATI</path>设备的接口，该方法的签名如下：

```python
Models_in_one.utils.hardware.ForceSensor.ForceSensor(
    calibration_file: str  # ATI设备的标定文件位置
)
```
<code>ForceSensor</code>类型提供<code>get_forces</code>方法，用于返回ATI设备的读数：

```Python
from Models_in_one.utils.hardware.ForceSensor import ForceSensor

calibration_file: str = ...
force_sensor = ForceSensor(calibration_file)
forces = force_sensor.get_forces()  # Data 类型对象
```

### CompatibleForceSensor
<code>CompatibleForceSensor</code>类型为<code>ForceSensor</code>类型的替代方案。该方法的签名如下：

```python
Models_in_one.utils.hardware.ForceSensor.CompatibleForceSensor(
    calibration_file: str  # ATI设备的标定文件位置
)
```

<code>CompatibleForceSensor</code>类型提供<code>get_forces</code>方法，用于返回ATI设备的读数：

```Python
from Models_in_one.utils.hardware.ForceSensor import CompatibleForceSensor

calibration_file: str = ...

with CompatibleForceSensor(calibration_file) as force_sensor:
    forces = force_sensor.get_forces()  # Data 类型对象
```

<warning><code>CompatibleForceSensor</code> 类型必须经过上下文管理语句使用！</warning>

<note>
<code>Models_in_one</code> 在目录 <path>./others/calibration</path> 下提供了一些标定过的 <path>.cal</path> 文件，请合理使用！

</note>

```python
CAL_216 = '.\others\calibration\FT43216.cal'
CAL_217 = '.\others\calibration\FT43217.cal'
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

`NDIReader`类型用于与NDI光学/电磁测量单元交互，签名如下：
```python
Models_in_one.utils.hardware.NDI.NDIReader(
    rom:  Optional[str] = None   # .rom 文件位置
    mode: str                    # in ['Auto', 'Optical', 'Aurora]
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


<warning>当同时使用多个测量单元时，请不要使用 <code>Auto</code> 模式。</warning>
<note>
<code>Models_in_one</code> 在目录 <path>./others/NDI_rom</path> 下提供了一些标定过的 <path>.rom</path> 文件，请结合实际坐标系合理使用！

当<code>mode</code> 被设置为<code>Aurora</code>时， <path>.rom</path>文件可以缺省。
</note>

```python
ROM_PATH_20220325 = './others/NDI_rom/20220325.rom'
ROM_PATH_20221121 = './others/NDI_rom/20221121.rom'
ROM_PATH_20230914 = './others/NDI_rom/20230914.rom'
```

## LUNA数据读取类型（LUNA，CompatibleLUNA）

**导入方法：**
```python 
from Models_in_one.utils.hardware.LUNA import LUNA, CompatibleLUNA
```

### LUNA 
<code>LUNA</code>类型提供读取<path>LUNA</path>光纤设备的接口，该方法的签名如下：

```python
Models_in_one.utils.hardware.LUNA.LUNA(
    address: str  # LUNA设备的IP地址
    port: int     # LUNA设备的端口
)
```
<code>LUNA</code>类型提供<code>get_data</code>方法，该方法接受一个<code>int</code>类型的参数，用于表示该方法将返回哪个通道的光线数据，留空时返回最近的一个通道的数据：

```Python
from Models_in_one.utils.hardware.LUNA import LUNA
address: str = ...
port: int = ...
channel: int = ...

luna = LUNA(address, port)
channel_number, data = luna.get_data(channel)
# 返回的通道是channel_number， 数据是data
# 此时的channel_number和channel应该相等
```

### CompatibleLUNA
<code>CompatibleLUNA</code>类型作为不在主程序中使用tcp/ip通讯的<path>LUNA</path>光纤设备的接口，当程序中有其他的模块与<code>LUNA</code>类型的读取有冲突时，应当使用该方法。该方法的签名如下：

```python
Models_in_one.utils.hardware.LUNA.CompatibleLUNA(
    address: str  # LUNA设备的IP地址
    port: int     # LUNA设备的端口
)
```

<code>CompatibleLUNA</code>类型提供<code>get_data</code>方法，该方法接受一个<code>int</code>类型的参数，用于表示该方法将返回哪个通道的光线数据，留空时返回最近的一个通道的数据：

```Python
from Models_in_one.utils.hardware.LUNA import CompatibleLUNA
address: str = ...
port: int = ...
channel: int = ...

with CompatibleLUNA(address, port) as luna:
    channel_number, data = luna.get_data(channel)
    # 返回的通道是channel_number， 数据是data
    # 此时的channel_number和channel应该相等
```

<warning><code>CompatibleLUNA</code> 类型必须经过上下文管理语句使用！</warning>

## 固高运动控制卡交互类型（MotorController, MotorJogMode）
<warning><code>MotorController</code> 与 <code>MotorJogMode</code> 不能同时实例化！</warning>

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
<def title="reset_from_last_log_file()">
<a anchor="reset">用于在意外断电后恢复电机的初始状态</a>
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

#### `reset_from_last_log_file` {id="reset"}
`reset_from_last_log_file`方法用于在意外断电后恢复电机的初始状态。

<warning>
该方法调用完成后会退出整个程序！
</warning>

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

<warning>调用 <code>move</code> 方法并不会中止之前的调用，如需停止电机，请使用
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

## EtherCAT电机交互类型（MotorWithEtherCAT）

**导入方法：**
```python 
from Models_in_one.utils.hardware.Motors import MotorWithEtherCAT
```
<deflist collapsible="true">
<def title="reset_motor()">
调用 DLL 的 resetMotor 函数以重置电机
</def>
<def title="enable_motor()">
调用 DLL 的 enableMotor 函数以启用电机
</def>
<def title="set_tension_ctrl(tension_val)">
设置张力控制值，输入为张力数组（Data 或 list）
</def>
<def title="set_length_ctrl(encoder_val=None)">
设置长度控制值，支持可选的编码器参考值（None 表示默认）
</def>
<def title="set_preload(preload_value)">
设置预加载值，输入为数组（list）
</def>
<def title="set_force_slope(slope_value)">
设置力的斜率，输入为 32 位无符号整数
</def>
<def title="set_pos_ctrl_params(max_velocity, velocity, acceleration, deceleration)">
设置位置控制参数，包括最大速度、目标速度、加速度和减速度
</def>
<def title="get_tendon_tension() -> Data">
获取张力数据，返回为 Data 对象
</def>
<def title="get_encoder() -> Data">
获取编码器数据，返回为 Data 对象
</def>
<def title="get_tendon_length(encoder_ref_val)">
根据编码器参考值获取张力长度，返回为 Data 对象
</def>
<def title="get_tendon_velocity()">
获取张力速度数据，返回为 Data 对象
</def>
<def title="ctrl_tension(target_tension)">
控制张力值，输入为目标张力数组（Data 或 list）
</def>
<def title="ctrl_length(target_length, encoder_ref_val=None)">
控制长度值，输入为目标长度数组和可选的编码器参考值
</def>
</deflist>



