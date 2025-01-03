# Using Neural Networks

该模块使用`pytorch`作为后端。该模块提供全连接神经网络（`FullyConnectedNeuralNetwork`）与循环神经网络（`RecurrentNeuralNetwork`）的简单构建方法，并支持从文件导入神经网络模型（`NeuralNetworkFromFile`），或者从`pytorch`自定义神经网络（`NeuralNetworkFromUser`）。同时在`models.bulitin`模块中内建了一系列常用神经网络模型。

> [pytorch官方文档](https://pytorch.org/docs/stable/index.html)

**导入方法：**
```python 
from Models_in_one.models import model_templates
```

## 模型基类（BaseModel）
`BaseModel`类型是本模块所有神经网络模型的基类，所有后续创建的神经网络模型严格继承于`BaseModel`类型。`BaseModel`类型提供神经网络从构建、设置到训练的全部方法。

<warning>
不建议用户继承<code>BaseModel</code>类型，如有自定义神经网络需求，请参见：<a anchor="neuralnetworkfromuser">自定义神经网络</a>。
</warning>

## 全连接神经网络（FullyConnectedNeuralNetwork）{id="FNN"}

全连接神经网络是一种十分基础的神经网络结构，其每一层的每一个节点都与上下层节点全部连接。具体的全连接神经网络介绍可见：

**导入方法：**
```python 
from Models_in_one.models.model_templates import FullyConnectedNeuralNetwork
```


> 知乎专栏： [深度学习开端|全连接神经网络](https://zhuanlan.zhihu.com/p/104576756)
>
> Wikipedia：[Artificial neural network](https://en.wikipedia.org/wiki/Artificial_neural_network)

本节中将以`FullyConnectedNeuralNetwork`类型为例说明所有神经网络模型的设置及训练方法，`FullyConnectedNeuralNetwork`类型的签名为：
```python
Models_in_one.models.model_templates.FullyConnectedNeuralNetwork(
    model_name: str,      # 模型名称
    _layer_info_: tuple,  # 全连接神经网络关键信息
    _device_=device       # 模型运行设备
)
```

<deflist collapsible="true">
<def title="history">
记录训练过程的字典，使用<code>train_loss</code>和<code>val_loss</code>记录从训练开始到结束的所有训练以及验证损失，使用<code>time</code>记录训练用时
</def>
<def title="convert_to_cpp(input_tensor)">
<a anchor="cpp">将训练后的模型转化为Torch-C++下的模型</a>
</def>
<def title="enable_tensorboard(log_dir)">
<a anchor="tb">启用Tensorboard</a>
</def>
<def title="enable_reduce_lr(lr_scheduler, **kwargs)">
<a anchor="lr">引入学习率控制方法</a>
</def>
<def title="enable_early_stopping(monitor, patience, min_delta)">
<a anchor="earlySt">设置早停规则</a>
</def>
<def title="set_loss_function(loss_function)">
<a anchor="set_loss">设置损失函数</a>
</def>
<def title="set_optimizer(optimizer)">
<a anchor="optim">设置优化器</a>
</def>
<def title="summary(**kwargs)">
<a anchor="summary">获得网络模型总览</a>
</def>
<def title="set_save_interval(save_interval)">
<a anchor="interval">设置保存模型的间隔</a>
</def>
<def title="train(train_dataset, val_dataset, shuffle, lr, epochs, batch_size, save_path, vis)">
<a anchor="train">网络训练</a>
</def>
<def title="interruptible_train(train_dataset, val_dataset, shuffle, lr, epochs, batch_size, save_path, vis)">
<a anchor="interruptible_train">可以被中断的网络训练</a>
</def>
<def title="predict(inputs, _device_, keep_tensor)">
<a anchor="output">获得模型输出</a>
</def>

</deflist>


### 设置神经网络模型结构
`FullyConnectedNeuralNetwork`类型提供了一种非常方便的构建方式，在初始化`FullyConnectedNeuralNetwork`类型的变量时，用户只需要提供包含各层关键信息的元组`_layer_info_`，即可完成一个全连接神经网络的创建，**`_layer_info_`中每一个子元组表示全连接网络的一层，子元组中第一个变量表示该层的节点数量，第二个变量表示该层采用的激活函数**，例如：
```python 
from Models_in_one.models import device
from Models_in_one.models.model_templates import FullyConnectedNeuralNetwork
# 创建拥有2个输入节点，隐藏层包含20个节点且激活函数为elu，2个输出节点且输出层激活函数为elu的三层全连接网络
_layer_info_: tuple = ((2, 'Linear'), (20, 'ELU'), (2, 'ELU'))
sample_fnn = FullyConnectedNeuralNetwork('sample_fnn', _layer_info_, device)
```
各种激活函数的信息可以参考[激活函数--pytorch 2.0 doc](https://pytorch.org/docs/stable/nn.html#non-linear-activations-weighted-sum-nonlinearity)。

### 设置损失函数 {id="set_loss"}
`FullyConnectedNeuralNetwork`类型提供`set_loss_function`方法，用于设置模型的损失函数。该方法接受一个类型为`torch.nn.Module`的损失函数，并将其设置为当前神经网络模型的损失函数。

例如设置`sample_fnn`的损失函数为平均绝对误差（MAE，`torch.nn.L1Loss`）：
```python
import torch
sample_fnn.set_loss_function(torch.nn.L1Loss)
```
<p>各种损失函数的信息可以参考<a href="https://pytorch.org/docs/stable/nn.html#loss-functions">损失函数--pytorch 2.0 doc</a>以及<a href="https://datawhalechina.github.io/thorough-pytorch/第六章/6.1%20自定义损失函数.html">如何自定义损失函数</a>。</p>

### 设置优化方式 {id="optim"}
优化方式是指如何根据损失函数的值修改神经网络的内部参数。常见的方法有随机梯度下降方法（**SGD**）、自适应时刻估计方法（**Adam**）等，更多内容可见：

> 知乎专栏：[优化方式介绍](https://zhuanlan.zhihu.com/p/27449596)

在训练一个神经网络模型时，指定优化方式是必要的。`FullyConnectedNeuralNetwork`类型提供`set_optimizer`方法，用于设置模型的优化方式。该方法接受一个类型为`torch.optim.Optimizer`的优化方式，并将其设置为当前神经网络模型的优化方式。

例如指定`sample_fnn`的优化方式为**Adam**方法（`torch.optim.Adam`）：
```python
import torch
sample_fnn.set_optimizer(torch.optim.Adam)
```
各种损失函数的信息可以参考[优化方法--pytorch 2.0 doc](https://pytorch.org/docs/stable/optim.html#algorithms)。

### 设置学习率规划 {id="lr"}
变化的学习率（**前期大，后期小**）可以使得神经网络模型更快速，稳定地到达最佳状态。`FullyConnectedNeuralNetwork`类型提供`enable_reduce_lr`方法，用于规划模型的学习率变化。该方法接受一个如下格式的列表：
```python
[
    (
        lr_scheduler  # torch.optim.lr_scheduler 对象
        start_from  # 从该epoch开始作用
        kwargs  # 字典对象，来自pytorch的设置参数
    ),  # 第一个学习率规划器
    (...),  # 第二个学习率规划器
    ...
]
```

例如指定`sample_fnn`的学习率变化方式为**一定时间内模型效果未好转自动下调学习率**（`torch.optim.lr_scheduler.ReduceLROnPlateau`）：
```python
import torch
kwargs = {"mode": "min", "factor": .2, "patience": 10, "verbose": False, "min_lr": 1e-4}
lr_list = [(torch.optim.lr_scheduler.ReduceLROnPlateau, 1, kwargs)]
sample_fnn.enable_reduce_lr(lr_list)
```
<p>具体学习率的设置规则以及相关参数可以参考<a href="https://pytorch.org/docs/stable/optim.html#how-to-adjust-learning-rate">how to adjust learning rate--pytorch 2.0 doc</a>以及<a href="https://datawhalechina.github.io/thorough-pytorch/第六章/6.2%20动态调整学习率.html#id2">自定义学习率变化规则</a>。</p>

### 设置早停规则 {id="earlySt"}
早停（EarlyStop）是一种避免神经网络过拟合的训练策略，当模型在训练时出现过拟合的迹象时，早停可以较为及时地停止模型地训练。`FullyConnectedNeuralNetwork`类型提供`enable_early_stopping`方法，设置模型训练的早停规则。该方法的签名如下：
```python
Models_in_one.models.model_templates.FullyConnectedNeuralNetwork.enable_early_stopping(
    monitor: str,   # 'train_loss'：训练集loss；'val_loss' ：验证集loss，二选一
    patience: int,  # 计次超过此，则停止训练
    min_delta: float # 当前monitor指标较历史最低增幅超过此，则计次加一
) -> None
```
例如在`sample_fnn`的训练过程中应用早停规则：
```python
sample_fnn.enable_early_stopping('train_loss', 30, .5)
```

### 设置Tensorboard {id="tb"}
Tensorboard是`Tensorflow`框架下的模型训练过程及结果可视化的工具。`pytorch`同样在`torch.utils.tensorboard`下提供了Tensorboard日志文件的写入接口。`FullyConnectedNeuralNetwork`类型提供`enable_tensorboard`方法，用于进行训练时的Tensorboard日志记录。该方法接受一个字符串类型变量`log_dir`作为日志文件存放的根目录，具体模型训练的日志文件目录则是存放在`log_dir/model_name/training_date`下。

>Github：[Tensorboard项目地址](https://github.com/tensorflow/tensorboard)

例如，为`sample_fnn`应用Tensorboard，记录于<path>./log</path>目录下：
```python
sample_fnn.enable_tensorboard('./log')
```
若在2023年7月21日18:02:01开始训练`sample_fnn`，则此次训练的Tensorboard日志会保存在目录：<path>./log/sample_fnn/20230721-180201/</path>。

在**powershell**中查看该次日志则可以使用命令：
```shell
tensorboard --logdir './log/sample_fnn/20230721-180201/' --port [你指定的端口号]
```
随后在浏览器中打开`localhost:你指定的端口号`即可。

### 获得模型结构总览 {id="summary"}
`FullyConnectedNeuralNetwork`类型提供`summary`方法，用于查看模型包括结构以及训练方式在内的具体信息。`summary`方法可以接受来自`torchinfo.summary`的所有参数。

例如查看`sample_fnn`到目前为止的设置信息：
```python
sample_fnn.summary()
```
你会得到：
<procedure title="示例结构" collapsible="true">
<code-block lang="shell">
#################################################################
Name of this neural network: 
sample_fnn
-----------------------------------------------------------------
Device: 
cuda:0
-----------------------------------------------------------------
Struct of this neural network: (from torchinfo)
=================================================================
Layer (type:depth-idx)                   Param #
=================================================================
__FullyConnectedNeuralNetwork__          --
├─Linear: 1-1                            60
├─ELU: 1-2                               --
├─Linear: 1-3                            42
├─ELU: 1-4                               --
=================================================================
Total params: 102
Trainable params: 102
Non-trainable params: 0
=================================================================
-----------------------------------------------------------------
The loss function of this neural network: 
'torch.nn.modules.loss.L1Loss'
-----------------------------------------------------------------
The optimizer of this neural network: 
'torch.optim.adam.Adam'
-----------------------------------------------------------------
This model has an early stopping plan with params:
monitor  : train_loss
patience : 30 epochs
min delta: 0.5
-----------------------------------------------------------------
The learning rate scheduler of this neural network: 
'torch.optim.lr_scheduler.ReduceLROnPlateau'
Here are its params:
mode            : min
factor          : 0.2
patience        : 10
verbose         : False
min_lr          : 0.0001
-----------------------------------------------------------------
The log file of Tensorboard is stored in 
.\log\sample_fnn\20230721-184927
#################################################################
</code-block>
</procedure>

### 设置模型保存间隔 {id="interval"}
`set_save_interval`方法接受一个 `int`类型的参数`save_interval`，表示每隔`save_interval`个`epoch`保存一次模型。

### 训练模型 {id="train"}
`FullyConnectedNeuralNetwork`类型提供`train`方法，用于对完成设置的神经网络模型进行训练。该函数会返回当前最优的模型保存位置。该方法的签名如下：
<warning>
至少需要使用<code>set_loss_function</code>方法以及<code>set_optimizer</code>方法设置完成损失函数以及优化方式，才能进行训练工作！
</warning>

```python
Models_in_one.models.model_templates.FullyConnectedNeuralNetwork.train(
    train_dataset: DataSet,
    val_dataset: Optional[Union[DataSet, float]],
    shuffle: bool,
    lr: float,
    epochs: int,
    batch_size: int,
    save_path: str,
    vis: bool = False
) -> str
```
<deflist collapsible="true">
<def title="tran_dataset">
指定模型训练使用的训练集
</def>
<def title="val_dataset">
指定模型训练使用的验证集。当该变量为<code>float</code>类型变量时，将指定验证集在训练集中的占比，并分割数据库用作训练与验证工作。
</def>
<def title="lr">
接受一个<code>float</code>类型的变量，设定模型训练时采用的学习率。如果使用<code>enable_reduce_lr</code>指定了学习率规划方式，此处设定的为初始学习率。
</def>
<def title="epochs">
指定模型训练最大轮数，此处定义不会与<code>enable_early_stopping</code>给定的早停设置冲突。
</def>
<def title="batch_size">
设置训练的batch size
</def>
<def title="save_path">
设置模型保存路径
</def>
<def title="vis">
设置是否向标准输出流回显模型训练指标。
</def>
</deflist>

例如，在内建的数据集`dataset_all`上训练`sample_fnn`，只需要：
```python
from Models_in_one.utils.data.builtin import dataset_all as dataset
saved_model_file_path = sample_fnn.train(dataset, None, False, 1e-3, 300, 64, "./save", False)
final_loss: float = sample_fnn.history["train_loss"][-1]
epochs: int = len(sample_fnn.history["train_loss"])
used_time: float = sample_fnn.history["time"]
log = f'Stopped at train loss: {final_loss}, used:{epochs} epochs in {used_time} s.'
print(log)
```

### 可以被中断的训练 {id="interruptible_train"}
<p>参数与<a anchor="train">训练模型</a>一节中相同，与<code>train</code>的区别是可以使用 <shortcut>Ctrl+C</shortcut>中断训练过程，并使用当前已有的训练结果继续后续代码。</p>

### 获得模型输出 {id="output"}
`FullyConnectedNeuralNetwork`类型提供`predict`方法，用于获得模型对于指定输入的输出。该方法接受两个变量：`Data`类型的`inputs`作为模型输入，以及来自`pytorch`的设备信息`device`。该方法的签名如下：
```python
Models_in_one.models.model_templates.FullyConnectedNeuralNetwork.predict(
    inputs: Data,
    _device_=device
) -> Data
```
例如获得`sample_fnn`的输出：
```python
from Models_in_one.models import device
from Models_in_one.utils.data import Data
input_data: Data = Data([1, 2])
output_data: Data = sample_fnn.predict(inputs=input_data, _device_=device)
```

### 在C++项目中使用pytorch模型 {id="cpp"}
<warning>
该方法需要在模型开始训练之前调用。
</warning>

`FullyConnectedNeuralNetwork`类型提供`convert_to_cpp`方法，用于将构建的模型转换为可以在C++项目中使用的模型文件。视模型的复杂程度，该方法可选地接受一个`torch.Tensor`类型的变量`input_tensor`辅助整个转换过程。文件夹<path>cpp_files/pytorch_c</path>下有对应的示例代码。
>具体见 [Pytorch Cpp API](https://pytorch.org/cppdocs/)

## 循环神经网络（RecurrentNeuralNetwork）
循环神经网络是一种使用序列数据或时序数据的人工神经网络。其中长短期记忆模型（LSTM）通过引入门控机制，解决了传统意义上的循环神经网络具有的梯度消失和梯度爆炸的问题，在长序列上拥有更好的表现。具体介绍可以参见：

**导入方法：**
```python 
from Models_in_one.models.model_templates import RecurrentNeuralNetwork
```


> Wikipedia：[Recurrent neural network](https://en.wikipedia.org/wiki/Recurrent_neural_network)
>
> 论文：[LSTM 论文原文](https://www.bioinf.jku.at/publications/older/2604.pdf)

本模块中传统循环神经网络与LSTM采用相同的签名：
```python
Models_in_one.models.model_templates.RecurrentNeuralNetwork(
    model_name: str,  # 模型名称
    output_dim,       # 输出节点个数
    lstm_mode: bool,  # 是否构建LSTM模型
    _device_,         # 模型运行设备
    **rnn_kwargs      # 具体的循环神经网络设计参数
)
```
参数rnn_kwargs的设计参见[RNN--pytorch 2.0 doc](https://pytorch.org/docs/stable/generated/torch.nn.RNN.html#rnn) 以及[LSTM--pytorch 2.0 doc](https://pytorch.org/docs/stable/generated/torch.nn.LSTM.html#lstm)。

## 从序列构建神经网络（NeuralNetworkFromSequential）{id="seq"}

**导入方法：**
```python 
from Models_in_one.models.model_templates import NeuralNetworkFromSequential
```

`NeuralNetworkFromSequential`类型允许用户从模型列表构建神经网络，该类型签名如下：
```python
Models_in_one.models.model_templates.NeuralNetworkFromSequential(
    model_name: str,  # 模型名称
    model_list: list[Union[nn.Module, BaseModel]],
    _device_         # 模型所在设备
)
```
实例化`NeuralNetworkFromSequential`类型时需要传入一个列表，**并在其中按顺序放入需要拼接的模型**。列表中的模型可以是来自`pytorch`的`nn.Module`类型模型，也可以是继承自`BaseModle`的模型，也可以是两者的混合。

<warning>
<code>NeuralNetworkFromSequential</code>类型不会继承来自列表中继承于<code>BaseModel</code>类型的模型的设置参数，但是会继承来自列表中所有模型的权重参数
</warning>

## 从文件构建神经网络（NeuralNetworkFromFile） {id="file"}

**导入方法：**
```python 
from Models_in_one.models.model_templates import NeuralNetworkFromFile
```

`NeuralNetworkFromFile`类型允许用户从保存的模型文件（<path>.pt</path>文件）重构神经网络模型，该类型的签名如下：
```python
Models_in_one.models.model_templates.NeuralNetworkFromFile(
    model_name: str,  # 模型名称
    file_name: str,   # 模型文件位置
    _device_          # 模型所在设备
)
```
有关pytorch模型保存于读取的问题可以参阅此处：[SAVING AND LOADING MODELS--pytorch 2.0 doc](https://pytorch.org/tutorials/beginner/saving_loading_models.html)；

有关`Tensorflow`框架与`pytorch`下的模型文件转换问题可以参阅此处：[how to convert a tensorflow model checkpoint to pytorch](https://saturncloud.io/blog/how-to-convert-a-tensorflow-model-checkpoint-to-pytorch/)，但是在最后不要保存`model.state_dict()`，而是整个模型。

## 自定义神经网络（NeuralNetworkFromUser）{id="user"}

**导入方法：**
```python 
from Models_in_one.models.model_templates import NeuralNetworkFromUser
```

<p><code>NeuralNetworkFromUser</code>类型允许用户从更底层的<code>torch.nn.Module</code>创建神经网络模型，该类型的签名如下：</p>

```python
Models_in_one.models.model_templates.NeuralNetworkFromUser(
    model_name: str,   # 模型名称
    _device_,          # 模型所在设备
    model              # torch.nn.Module 类型的模型
)
```
例如，使用`NeuralNetworkFromUser`类型创建一个3层全连接网络：
```python
from torch import nn
from Models_in_one.models import device
from Models_in_one.models.model_templates import NeuralNetworkFromUser


class __FNN__(nn.Module):
    def __init__(self):
        super(__FNN__, self).__init__()
        self.layer_for_input = nn.Linear(2, 10).to(device)
        self.dense = nn.Linear(10, 10).to(device)
        self.output_layer = nn.Linear(10, 2).to(device)
        self.act_1 = nn.Tanh()
        self.act_2 = nn.ELU()
    def forward(self, x):
        x = self.layer_for_input(x)
        x = self.act_1(x).to(device)
        x = self.dense(x)
        x = self.act_2(x).to(device)
        x = self.output_layer(x)
        return x


fnn_from_user = NeuralNetworkFromUser('sample_fnn_user', device, __FNN__())
```
<note>
你可以通过调用该类的<code>call</code>方法调用从更底层的<code>torch.nn.Module</code>创建的神经网络模型
</note>

## 内建神经网络模型
`Models_in_one.models.bulitin`模块内置了一系列已经定义并且完成设置的神经网络模型，现列举如下：


<note>
<p>当导入<code>builtin</code>时，默认行为是初始化全部的神经网络，如果只想创建需要的神经网络，请在导入前按照如下设置：</p>
<code-block lang="python">
import os
os.environ['load_all'] = 'False'
os.environ['load_pinn_2x2'] = 'True'  # 设置需要加载PINN_2x2
</code-block>
</note>

<tabs>
<tab title="FNN_3_2x2">
<code-block lang="shell">
##########################################################################################
Name of this neural network: 
builtin_fnn_3_2x2
------------------------------------------------------------------------------------------
Device: 
cuda:0
------------------------------------------------------------------------------------------
Struct of this neural network: (from torchinfo)
==========================================================================================
Layer (type:depth-idx)                   Output Shape              Param #
==========================================================================================
__FullyConnectedNeuralNetwork__          [1, 2]                    --
├─ELU: 1-1                               [1, 2]                    --
├─Linear: 1-2                            [1, 20]                   60
├─ELU: 1-3                               [1, 20]                   --
├─Linear: 1-4                            [1, 2]                    42
==========================================================================================
Total params: 102
Trainable params: 102
Non-trainable params: 0
Total mult-adds (M): 0.00
==========================================================================================
Input size (MB): 0.00
Forward/backward pass size (MB): 0.00
Params size (MB): 0.00
Estimated Total Size (MB): 0.00
==========================================================================================
------------------------------------------------------------------------------------------
The loss function of this neural network: 
'torch.nn.modules.loss.L1Loss'
------------------------------------------------------------------------------------------
The optimizer of this neural network: 
'torch.optim.adam.Adam'
------------------------------------------------------------------------------------------
The learning rate scheduler of this neural network: 
'torch.optim.lr_scheduler.ReduceLROnPlateau'
Here are its params:
mode            : min
factor          : 0.2
patience        : 10
verbose         : False
min_lr          : 0.0001
##########################################################################################
</code-block>
</tab>
<tab title="FNN_4_2x2">
<code-block lang="shell">
##########################################################################################
Name of this neural network: 
builtin_fnn_4_2x2
------------------------------------------------------------------------------------------
Device: 
cuda:0
------------------------------------------------------------------------------------------
Struct of this neural network: (from torchinfo)
==========================================================================================
Layer (type:depth-idx)                   Output Shape              Param #
==========================================================================================
__FullyConnectedNeuralNetwork__          [1, 2]                    --
├─ELU: 1-1                               [1, 2]                    --
├─Linear: 1-2                            [1, 20]                   60
├─ELU: 1-3                               [1, 20]                   --
├─Linear: 1-4                            [1, 20]                   420
├─ELU: 1-5                               [1, 20]                   --
├─Linear: 1-6                            [1, 2]                    42
==========================================================================================
Total params: 522
Trainable params: 522
Non-trainable params: 0
Total mult-adds (M): 0.00
==========================================================================================
Input size (MB): 0.00
Forward/backward pass size (MB): 0.00
Params size (MB): 0.00
Estimated Total Size (MB): 0.00
==========================================================================================
------------------------------------------------------------------------------------------
The loss function of this neural network: 
'Models_in_one.models.cores.MAPE'
------------------------------------------------------------------------------------------
The optimizer of this neural network: 
'torch.optim.adam.Adam'
------------------------------------------------------------------------------------------
The learning rate scheduler of this neural network: 
'torch.optim.lr_scheduler.ReduceLROnPlateau'
Here are its params:
mode            : min
factor          : 0.2
patience        : 10
verbose         : False
min_lr          : 0.0001
##########################################################################################
</code-block>
</tab>
<tab title="TINN_2x2">
<code-block lang="shell">
##########################################################################################
Name of this neural network: 
builtin_tinn_2x2
------------------------------------------------------------------------------------------
Device: 
cuda:0
------------------------------------------------------------------------------------------
Struct of this neural network: (from torchinfo)
==========================================================================================
Layer (type:depth-idx)                   Output Shape              Param #
==========================================================================================
__TimingInputNeuralNetwork__             [1, 2]                    --
├─Tanh: 1-1                              [1, 2]                    --
├─Linear: 1-2                            [1, 10]                   30
├─Tanh: 1-3                              [1, 2]                    --
├─Linear: 1-4                            [1, 10]                   30
├─Tanh: 1-5                              [1, 20]                   --
├─Linear: 1-6                            [1, 20]                   420
├─Tanh: 1-7                              [1, 20]                   --
├─Linear: 1-8                            [1, 10]                   210
├─ELU: 1-9                               [1, 10]                   --
├─Linear: 1-10                           [1, 2]                    22
==========================================================================================
Total params: 712
Trainable params: 712
Non-trainable params: 0
Total mult-adds (M): 0.00
==========================================================================================
Input size (MB): 0.00
Forward/backward pass size (MB): 0.00
Params size (MB): 0.00
Estimated Total Size (MB): 0.00
==========================================================================================
------------------------------------------------------------------------------------------
The loss function of this neural network: 
'torch.nn.modules.loss.L1Loss'
------------------------------------------------------------------------------------------
The optimizer of this neural network: 
'torch.optim.adam.Adam'
------------------------------------------------------------------------------------------
The learning rate scheduler of this neural network: 
'torch.optim.lr_scheduler.ReduceLROnPlateau'
Here are its params:
mode            : min
factor          : 0.2
patience        : 10
verbose         : False
min_lr          : 0.0001
##########################################################################################
</code-block>
</tab>
<tab title="RNN_2x20_2x2">
<code-block lang="shell">
##########################################################################################
Name of this neural network: 
builtin_rnn_2x20_2x2
------------------------------------------------------------------------------------------
Device: 
cuda:0
------------------------------------------------------------------------------------------
Struct of this neural network: (from torchinfo)
==========================================================================================
Layer (type:depth-idx)                   Output Shape              Param #
==========================================================================================
__RecurrentNeuralNetwork__               [1, 2]                    --
├─RNN: 1-1                               [1, 20, 20]               1,320
├─Linear: 1-2                            [1, 2]                    42
==========================================================================================
Total params: 1,362
Trainable params: 1,362
Non-trainable params: 0
Total mult-adds (M): 0.03
==========================================================================================
Input size (MB): 0.00
Forward/backward pass size (MB): 0.00
Params size (MB): 0.01
Estimated Total Size (MB): 0.01
==========================================================================================
------------------------------------------------------------------------------------------
The loss function of this neural network: 
'torch.nn.modules.loss.L1Loss'
------------------------------------------------------------------------------------------
The optimizer of this neural network: 
'torch.optim.adam.Adam'
------------------------------------------------------------------------------------------
The learning rate scheduler of this neural network: 
'torch.optim.lr_scheduler.ReduceLROnPlateau'
Here are its params:
mode            : min
factor          : 0.2
patience        : 10
verbose         : False
min_lr          : 0.0001
##########################################################################################
</code-block>
</tab>
<tab title="LSTM_2x20_2x2">
<code-block lang="shell">
##########################################################################################
Name of this neural network: 
builtin_lstm_2x20_2x2
------------------------------------------------------------------------------------------
Device: 
cuda:0
------------------------------------------------------------------------------------------
Struct of this neural network: (from torchinfo)
==========================================================================================
Layer (type:depth-idx)                   Output Shape              Param #
==========================================================================================
__RecurrentNeuralNetwork__               [1, 2]                    --
├─LSTM: 1-1                              [1, 20, 20]               5,280
├─Linear: 1-2                            [1, 2]                    42
==========================================================================================
Total params: 5,322
Trainable params: 5,322
Non-trainable params: 0
Total mult-adds (M): 0.11
==========================================================================================
Input size (MB): 0.00
Forward/backward pass size (MB): 0.00
Params size (MB): 0.02
Estimated Total Size (MB): 0.02
==========================================================================================
------------------------------------------------------------------------------------------
The loss function of this neural network: 
'torch.nn.modules.loss.L1Loss'
------------------------------------------------------------------------------------------
The optimizer of this neural network: 
'torch.optim.adam.Adam'
------------------------------------------------------------------------------------------
The learning rate scheduler of this neural network: 
'torch.optim.lr_scheduler.ReduceLROnPlateau'
Here are its params:
mode            : min
factor          : 0.2
patience        : 10
verbose         : False
min_lr          : 0.0001
##########################################################################################
</code-block>
</tab>
<tab title="PINN_2x2">
<code-block lang="shell">
##########################################################################################
Name of this neural network: 
builtin_pinn_2x2
------------------------------------------------------------------------------------------
Device: 
cuda:0
------------------------------------------------------------------------------------------
Struct of this neural network: (from torchinfo)
==========================================================================================
Layer (type:depth-idx)                   Output Shape              Param #
==========================================================================================
__PhysicsInformedNeuralNetwork__         [1, 2]                    --
├─Tanh: 1-1                              [1, 2]                    --
├─Linear: 1-2                            [1, 20]                   60
├─Tanh: 1-3                              [1, 20]                   --
├─Linear: 1-4                            [1, 20]                   420
├─ELU: 1-5                               [1, 20]                   --
├─Linear: 1-6                            [1, 2]                    42
├─Tanh: 1-7                              [1, 2]                    --
├─ELU: 1-8                               [1, 2]                    --
├─Linear: 1-9                            [1, 2]                    6
==========================================================================================
Total params: 528
Trainable params: 528
Non-trainable params: 0
Total mult-adds (M): 0.00
==========================================================================================
Input size (MB): 0.00
Forward/backward pass size (MB): 0.00
Params size (MB): 0.00
Estimated Total Size (MB): 0.00
==========================================================================================
------------------------------------------------------------------------------------------
The loss function of this neural network: 
'Models_in_one.models.cores.MAPE'
------------------------------------------------------------------------------------------
The optimizer of this neural network: 
'torch.optim.adam.Adam'
------------------------------------------------------------------------------------------
The learning rate scheduler of this neural network: 
'torch.optim.lr_scheduler.ReduceLROnPlateau'
Here are its params:
mode            : min
factor          : 0.2
patience        : 10
verbose         : False
min_lr          : 0.0001
##########################################################################################
</code-block>
</tab>
</tabs>
