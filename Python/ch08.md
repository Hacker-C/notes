# （八）Python 标准库和扩展库（第三方库）

> 在 Python 中，库或模块是指一个包含函数定义、类定义、或常量的 Python 程序文件。python 安装包中自带的库称为标准库，需要另外安装的库是扩展库（第三方库）。Python 有成千上万的扩展库，而且每天都在增长。

## 1. 扩展库的安装工具 `pip`

`pip` 是 python 的一个非常好用的包管理工具，可以用来很方便地安装和管理各种三方库。一般 python3.4+ 版本都自带 `pip` 工具。

### 1.1 检查安装

查看版本，判断是否安装
```bash
pip3 --version
pip --version
```

对于 Windows 系统，到 [python官网](https://www.python.org/) 下载符合自己系统的最新版本，安装的时候勾选 `安装pip` 即可。

对于 ubuntu/wsl(ubuntu)，使用以下命令安装
```bash
sudo apt install python3-pip
```

### 1.2 `pip` 常用命令

命令帮助
```bash
pip --help
```

查看版本
```bash
pip --version
```

升级 pip
Windows
```bash  
python -m pip install -U pip   # python2.x
python -m pip3 install -U pip    # python3.x
```

linux/wsl
```bash
pip install --upgrade pip    # python2.x
pip3 install --upgrade pip   # python3.x
```

若升级遇见问题，则使用
```bash
sudo easy_install --upgrade pip
```

查看已经通过pip安装的包
```bash
pip list
pip freeze
```

下载安装库
```bash
pip install SomePackage        # 最新版本
pip install SomePackage==1.4   # 指定版本
```

升级包
```bash
pip install --upgrade SomePackage
```

卸载包
```bash
pip uninstall SomePackage
```

搜索包
```bash
pip search SomePackage
```

显示包详情
```bash
pip show SomePackage
```

查看可升级的包
```bash
pip list -o
```

pip 清华大学开源软件镜像站
临时使用
```bash
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple SomePackage
```

如果 Python2 和 Python3 同时有 pip，则使用方法如下
Python2：
```bash
python2 -m pip install XXX
```
Python2：
```bash
python3 -m pip install XXX
```

## 2. 标准库与扩展库的导入和使用

+ `import 模块名 (as 别名)`
+ `from 模块名 import 对象名 (as 别名)`
+ `from 模块名 import *`

### 2.1 import 模块名 (as 别名)

使用此方法导入库后，使用对象的方式是 `模块名.对象名`。若还使用了 `as 别名`，则方式是 `别名.对象名`。

### 2.2 from 模块名 import 对象名 (as 别名)

使用此方法可减少查询次数，提高访问速度。同时使用了 `as 别名` 则可减少代码量，提高开发效率。
```python
from numpy import array as arr
```

### 2.3 form 模块名 import *

一次性引入指定模块中的所有对象，方便许多，但不推荐。
```python
form math import *
```