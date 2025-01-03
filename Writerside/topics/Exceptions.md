# Exceptions

本章叙述本项目中定义的异常类。
导入方法：

```Python
from Models_in_one.utils import errors
```

<deflist collapsible="true">
<def title="OSNotSupportError">
当使用的操作系统不支持功能时，将抛出此错误。
</def>
<def title="CanNotReceiveBufferError">
当程序无法发送数据到服务器时，将抛出此错误。
</def>
<def title="CanNotSendBufferError">
当程序无法接受来自服务器的数据时，抛出此错误。
</def>
<def title="CanNotInitializeSocketError">
当TCP/IP程序无法初始化嵌套字时，将抛出此错误。
</def>
<def title="WrongSocketVersionError">
当嵌套字版本与服务器不匹配时，将抛出此错误。
</def>
<def title="CanNotConnectToServerError">
当程序无法连接至服务器时，将抛出此错误
</def>
<def title="DataTypeError">
当对<code>Data</code>或<code>DataSet</code>执行非法的数据类型操作时，将抛出此错误。
</def>
<def title="DataNotEnoughError">
当操作的数据库大小不支持进行的操作时，将抛出此错误。
</def>
<def title="InDevError">
所调用的函数还在开发中时，将抛出此错误。
</def>
<def title="ATIInitFailedError">
当<path>ATI</path>无法被初始化时，将抛出此错误。
</def>
<def title="NDIInitFailedError">
当<path>NDI</path>无法被初始化时，将抛出此错误。
</def>
<def title="NotWithinTheOptionalRangeError">
当给定的参数不在可选参数范围内时，将抛出此错误。
</def>
</deflist>
