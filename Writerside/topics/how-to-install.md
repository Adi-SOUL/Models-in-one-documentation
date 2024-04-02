# How to install

理论上说，作者本人**已经**在实验用PC上完成了安装过程。但是为了防止诸如**重装系统**等操作的发生，本项目的安装过程仍然详细叙述于本节。

<note>
<p>注：本节内容同时可以作为安装Python与配置环境的相关指导</p>
</note>

## 使用安装脚本安装（推荐）
<procedure title="按照如下步骤安装：">
    <step>
        <p>从 <a href="https://www.anaconda.com">Anaconda官方网站</a>下载并安装Anaconda</p>
        <procedure title="">
        <p>关于如何设置conda的系统变量，请查看<a href="https://stackoverflow.com/questions/44597662/conda-command-is-not-recognized-on-windows-10"> StackOverflow页面</a></p>
        </procedure>
    </step>
    <step>
        <p>初始化Conda：</p>
        <code-block lang="shell">
        conda init
        </code-block>
    </step>
    <step>
    从conda创建环境：
    <code-block lang="shell">
    conda create -n [你的环境名称] python=[你选择的python版本（>=3.9）]
    </code-block>
    </step>
    <step>
    从 <a href="https://github.com/Adi-SOUL/Models-in-one/releases"> GitHub releases</a> 获取最新的安装文件压缩包，解压后然后使用如下命令进行安装：
    <code-block lang="shell">./install_[版本号].bat</code-block>
    或直接双击文件安装。
<note>
<p>请使用管理员模式运行</p>
</note>
    </step>
</procedure>

<note>
安装完成后，在命令行中使用如下命令查看帮助文档：
<code-block lang="shell">
python -m Models_in_one.utils.doc
</code-block>
</note>
<warning>
    <p>如果<code>pytorch</code>不能正确识别GPU设备，请检查自身<code>cuda</code>以及<code>cudnn</code>安装情况，并从<a href="https://pytorch.org/get-started/previous-versions">PyTorch 版本页面</a>查找适合的版本，然后使用如下命令重新安装<code>pytorch</code>：</p>
    <code-block lang="shell">pip install [你查询到的pytorch版本]</code-block>
</warning>

## 不使用安装脚本安装（不推荐）
将上一节的**步骤4**改为：
```Shell
conda activate [你的环境名称]
pip install -r requriements.txt
```
然后复制本项目源码至目标项目的根目录下。

<warning>
<p>
如果你想使用可视化运动学仿真程序<path>VisCR</path>，请不要使用这种安装方式。
</p>
</warning>



<seealso>
    <category ref="external">
        <a href="https://www.python.org/downloads">Python 官网地址</a>
        <a href="https://www.tutorialspoint.com/how-to-install-python-in-windows">Python 安装教程</a>
        <a href="https://docs.python.org/3/library/venv.html">使用venv创建虚拟环境</a>
    </category>
</seealso>
