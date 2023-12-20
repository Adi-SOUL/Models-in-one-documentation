# Reset after exception

<note>
如果你不需要使用电机，你没有必要使用这个修饰器
</note>

`utils`模块提供了一个函数修饰器`reset_after_exception`，当实验中运行的代码出现问题时，该修饰器可以捕捉问题。 当`exit_after_reset`为`True`时， 该方法会在捕捉到异常后回正硬件， 并结束程序， 否则仅捕捉异常。该修饰器的签名如下：
```python
Models_in_one.utils.reset_after_exception(
   motor,
   reset_content,  #依照实际情况选择复位指令，例如Data([0,0])或者'0'
   exit_after_reset: bool = True
)
```
在使用修饰器之前，你需要初始化你的电机（`Motor`）， 例如：
```python
from Models_in_one.utils import reset_after_exception
from Models_in_one.utils.hardware.Motors import MotorController
from Models_in_one.utils.data import Data
my_motor = MotorController()

@reset_after_exception(motor=my_motor, reset_content=Data([0,0]), exit_after_reset=True)
def ep_main():
   ...

ep_main()
```
执行上述代码时，若函数`ep_main`中存在异常，程序会捕捉到异常，并回正电机。