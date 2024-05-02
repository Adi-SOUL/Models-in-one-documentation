# Monitor

该模块用于实验进行中的远程监控与通知功能。

导入方法：
<code-block lang="python">
from Models_in_one.utils import monitor
</code-block>

## 邮件发送类（Email）
<code>Email</code>类提供了一个向外发送电子邮件的接口，可以通过简单的设置向给定目标发送邮件。

导入方法：
<code-block lang="python">
from Models_in_one.utils.monitor import Email
</code-block>

<deflist collapsible="true">
<def title="set_subject(subject: str)">
<a anchor="set_email">设置邮件标题</a>
</def>
<def title="set_text(text_list: list[str])">
<a anchor="set_email">设置邮件文本内容</a>
</def>
<def title="set_file(file_list: list[str])">
<a anchor="set_email">设置邮件附件内容</a>
</def>
<def title="send()">
<a anchor="send_email">发送邮件</a>
</def>
</deflist>

当实例化<code>Email</code>类时，需要给定目标邮箱的地址，例如创建一个发送到地址<path>adijnnuuy@gmail.com</path>的邮件：
<code-block lang="python">
exp_email = Email(address="adijnnuuy@gmail.com")
</code-block>

### 邮件内容设置 {id="set_email"}
<code>Email</code>类型的对象可以通过如下方法设置相关邮件内容：
<code-block lang="python">
# 设置邮件标题为：A Sample Email
exp_email.set_subject("A Sample Email")
# 设置邮件文本为三个自然段，内容分别为： 这是第一段，这是第二段，这是第三段
exp_email.set_text(["这是第一段", "这是第二段", "这是第三段"])
# 设置邮件附件文件为：Sample_csv.csv, Sample_txt.txt
exp_email.set_file(["Sample_csv.csv", "Sample_txt.txt"])
</code-block>

### 发送邮件 {id="send_email"}
<code>Email</code>类型的对象可以通过如下方法发送邮件：
<code-block lang="python">
exp_email.send()
</code-block>

### 示例
你可以通过<code>Email</code>功能提示一些用时较长的实验的进度，以下是一个可能的应用场景：

```Python
from Models_in_one.utils.monitor import Email
exp_email = Email(address="adijnnuuy@gmail.com")

# 用于存放当前实验新建的文件名
file_list = []

def ep_main():
    ...

if __name__ == "__main__":
    ep_main()
    exp_email.set_subject("实验完成提醒")
    exp_email.set_text(["实验已完成"])
    exp_email.set_file(file_list)
    exp_email.send()
```


## 看门狗类（WatchDog）

<code>WatchDog</code>类提供了一个通过邮件监控实验中异常耗时的方法。

导入方法：
<code-block lang="python">
from Models_in_one.utils.monitor import WatchDog
</code-block>

当使用<code>WatchDog</code>类时，你需要设置当异常出现时，邮件的目标地址，主题，文本以及附件（可选）。<a anchor="set_email"> 每个条目的设置内容与<code>Email</code>一致 </a>。
例如：
```Python
from Models_in_one.utils.monitor import WatchDog

time_out: int = 3  # 块内运行时间超过3s报警
address: str = "adijnnuut@gmail.com"  # 发送到该邮箱
subject: str = "Sample WatchDog"  # 邮件主题
text: list[str] = ["异常耗时"]  # 邮件正文
file: list[str] = ["./log.log"]  # 邮件附件
with WatchDog(time_out, address, subject, text, file):
    ...  # 需要被计时的操作

# 从这里开始不参与计时

```
<warning>
<code>WatchDog</code>类必须使用<code>with</code>语句操作！
</warning>