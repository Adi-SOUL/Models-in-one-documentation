# Simulator

## 仿真类（VisCR）
该模块提供与可视化仿真程序<path>VisCR</path>之间的交互类`QTSimulator`。仅需简单的步骤即可使用连续体机器人运动学可视化仿真。

<note>
<path>VisCR</path> 详情请见 <a href="https://github.com/Adi-SOUL/VisCR">此页面</a> 

</note>

**导入方法：**
```python 
from Models_in_one.utils.vis_cr import VisCR
```

<deflist collapsible="true">
<def title="connect()">
与VisCR程序建立连接。
</def>
<def title="set_one_step_func(func: Callable[[int], list[ndarray]])">
<a anchor="set">设置单一仿真步计算实例 </a>
</def>
<def title="run()">
运行仿真程序。
</def>
</deflist>

### 设置单一仿真步计算实例 {id="set"}
在仿真程序开始运行之前，你需要定义一个函数，该函数接受一个`int`类型的变量标识当前仿真步骤的下标，并返回一个`ndarray`列表。这个函数的物理意义是：
返回第`Step: int`运行步时， 连续体机器人从近端点开始的各个点的齐次变换矩阵。

```Python
import numpy
def sample_func(step: int) -> list[numpy.ndarray]:
	res: list[numpy.ndarray] = []
	L: float = 200/40.
	theta: float = numpy.pi/3
	phi: float = numpy.pi*2/100*step
	for i in range(100):
		res.append(get_T(theta/100*(i+1), phi, L/100*(i+1)))  # get_T是计算恒曲率齐次变换矩阵的函数。
	return res
```
然后使用`VisCR`的`set_one_step_fun`设置到仿真类中。

<warning>一定要保证设置函数的参数与返回值与要求的保持一致</warning>

<warning>由于<path>OpenGL</path>的坐标系问题，请使用本模块提供的旋转矩阵进行计算</warning>
<deflist  collapsible="true">
<def title="rotate_4x4(axis: str, angle: float)">
返回绕<code>axis</code>旋转<code>angle</code>弧度的旋转矩阵。
</def>
<def title="displacement_4x4(x: float, y: float, z: float)">
返回平移矩阵。
</def>
<def title="convert_matrix_to_OpenGL_matrix(matrix: np.ndarray)">
返回<path>OpenGL</path>下对应的右手坐标系下的齐次变换矩阵转。
</def>
<def title="tip_force_matrix(f_x: float, f_y: float, f_z: float)">
返回所需要的三维力矩阵，用于添加在序列的最末端。
</def>
<def title="default_one_step(step: int)">
简单的实例仿真步函数
</def>
</deflist>

### 运行实例

<procedure title="按照如下步骤使用模拟器：">
    <step>
        在<path>PowerShell</path>中使用如下命令启动模拟器页面：
        <code-block lang="shell">
            viscr
        </code-block>
        <note>        
            第一次运行程序时，请首先使用如下命令打开并修改设置<path>.json</path>文件的位置：
            <code-block lang="shell">
                viscr ini
            </code-block>
            或者使用如下命令修改默认设置<path>.json</path>文件：
            <code-block lang="shell">
                viscr json
            </code-block>
            未正确设置上述文件可能导致程序的意外退出。
        </note>
    </step>

<step>
编写仿真程序：

```Python
import numpy
from Models_in_one.utils.vis_cr import VisCR


def sample_func(step: int) -> list[numpy.ndarray]: 
    res: list[numpy.ndarray] = ...
    return res


my_simulator = VisCR()
my_simulator.set_one_step_func(sample_func)
my_simulator.connect()
my_simulator.run()
```

</step>

<step>
运行仿真程序，然后点击<path>VisCR</path>的<path>Link Start</path>按钮。

</step>
</procedure>

<warning>
如果<path>PowerShell</path>找不到<path>VisCR</path>， 请首先确保采用推荐方法安装了<path>1.0rc1</path>（2024.3.15发布）以上的版本，其次联系开发者寻求帮助。
</warning>
