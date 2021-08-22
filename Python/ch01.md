# （一）初识Python

### 1. 简介

python 是全世界最热门的语言之一。截至2020年8月的TIOBE排行榜TOP10：
![tiobe](https://s1.ax1x.com/2020/08/29/dTjJ54.png)

python是一门解释型语言。解释运行的意思就是代码被解释器解释才能运行，而且是解释一条语句运行一条语句。这和C/C++/Java等编译型语言不同，编译运行是编译器先把整个代码编译为计算机能够执行的字节码等文件，然后再运行。正是python解释运行的特点使得python的运行速度比编译型语言要低得多。  

### 2. 特点

+ 语法简洁。用C/C++写的几十行的代码，用python就只需要几行代码。人生苦短，我用python；
+ 跨平台运行。同一代码，在不同的安装了解释器的系统上都能运行；
+ 通用灵活。python应用广泛，可以在网络爬虫、大数据分析、服务器等各个方面得到应用；
+ 可读性高。python的强制索引使得python的代码逻辑性高，也有利于维护；
+ 类库丰富。解释器提供众多优秀的内置类和函数库；
+ 对中文的支持度高。python解释器采用UTF-8编码，处理中文更加灵活和高效。

### 3. 缺点

+ 解释运行，运行效率慢。（但实际上用在开发中，用户是体验不到这种差异的）；
+ 粘贴代码可能运行报错，因为python要保证严格缩进；
+ 代码不能加密，发布python程序即开源了代码。

### 4. 解释器

python有多种解释器，解释器执行 `.py` 文件中的代码。常见的有CPython(C编写), IPython, Jython(Java编写)等等。


### 5. 运行模式

python有命令行交互式运行和文件式运行两种运行模式。

+ python交互式编程
  在安装python的情况下，在命令行输入python(或python3)即进入交互式模式。写一句代码运行一句，不能保存下来。在此模式下，可输入语句、算式、表达式，直接运行得出结果。
+ python文件式编程
  使用文本编辑器（VSCode, Submit text 3, Notepad++等）将代码写入 `.py` 文件，保存后运行命令 `python test.py` 。常用模式，可保存代码。

更多的是使用ide(继承开发环境)，既有交互式编程，又有文件式编程。例如 PyCharm 等。

### 6. 输入和输出

使用 `print()` 进行打印（输出）。
```py
print('hello, python')
print('hello, world', end='')
```

> ✅ pritnt() 输出内容后，默认会换行。要使其不换行，则使用 `print('test', end='')` 。事实上 `end` 可以是其他内容，会加在 `'test'` 的后面。

使用 `input()` 方法进行键盘输入。
```py
name = input('请输入你的名字：')
number = int(input('请输入你的序号：'))
```

> ✅ `input()` 方法返回的默认值类型是字符串，有需要的话，显性转化为数值或其他类型。

### 7. 注释

python 有单行注释和多行注释。

+ 单行注释 `#`
  ```py
  # 这是单行注释
  ```
+ 多行注释 `"""...""" `
  ```py
  """
  注释1
  注释2
  注释3
  """
  ```
> ✅ 养成写注释的好处，有利于后期较大项目的维护和Debug

### 8. Python 开发工具

+ IDLE
  下载安装 python 的时候自带的继承开发环境，体验不好，不推荐。

+ VSCode
  采用 “文本编辑器 + 命令行” 的模式进行开发。VSCode 是高级文本编辑器，内部自带了命令行终端。在 VSCode 的编辑区编辑好了代码后，使用快捷键 `Ctrl + ` `即可进入命令行然后运行代码。当然安装相应的 python 插件也行。 

+ Pycharm
  PyCharm 是 JetBrains 旗下的一款 python 开发神器、高级 Python IDE。有免费版的有付费版的，去 JetBrians 官网即可获得。还可以安装非常丰富的利于开发的插件、主题等等。

### 9. Python 之蝉

在 python 交互式命令行输入 `import this`，就会输出当年 python 的开发者隐藏的小彩蛋，称为 ”The Zen of Python“（python 之蝉）。这是给 python 开发者们的编程建议和告诉我们要形成良好代码风格。

```python
>>> import this
The Zen of Python, by Tim Peters

Beautiful is better than ugly.

Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!
```

翻译：

```
Python之禅 by Tim Peters

优美胜于丑陋（Python 以编写优美的代码为目标）
明了胜于晦涩（优美的代码应当是明了的，命名规范，风格相似）
简洁胜于复杂（优美的代码应当是简洁的，不要有复杂的内部实现）
复杂胜于凌乱（如果复杂不可避免，那代码间也不能有难懂的关系，要保持接口简洁）
扁平胜于嵌套（优美的代码应当是扁平的，不能有太多的嵌套）
间隔胜于紧凑（优美的代码有适当的间隔，不要奢望一行代码解决问题）
可读性很重要（优美的代码是可读的）
即便假借特例的实用性之名，也不可违背这些规则（这些规则至高无上）
不要包容所有错误，除非你确定需要这样做（精准地捕获异常，不写 except:pass 风格的代码）
当存在多种可能，不要尝试去猜测
而是尽量找一种，最好是唯一一种明显的解决方案（如果不确定，就用穷举法）
虽然这并不容易，因为你不是 Python 之父（这里的 Dutch 是指 Guido ）
做也许好过不做，但不假思索就动手还不如不做（动手之前要细思量）
如果你无法向人描述你的方案，那肯定不是一个好方案；反之亦然（方案测评标准）
命名空间是一种绝妙的理念，我们应当多加利用（倡导与号召）
```
