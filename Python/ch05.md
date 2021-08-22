# （五）Python语句的格式化输出

> 格式化数据的三种方法
> 1. `%`
> 2. `format`
> 3. `f-string`（python version >= 3.6）

## 1. `%` 方法

### 1.1 整数的输出

① 整数的格式化输出

整数使用 `%d` （同样适用于八进制和十六进制）进行格式化输出。

语法：`print('%nd' % num)`

扩展：`print('%nd %-md ...' % (num1, num2 ...))`

含义：`%` 相当于占位符，`m, n` 是所占的位数， 占位符和实际数字（num1,num2）之间的 `%` 是分隔符。默认情况下数字输出的是向右边对齐，少位的自动补充。在 `m,n` 前加上 `-` 号则向左对齐。

② 整数的按照指定进制输出

+ 输出数字的十进制：`print('%d' % num1)`
+ 输出数字的八进制：`print('%o' % num1)`
+ 输出数字的十六进制：`print('%x' % num3)`
+ 输出数字的十六进制（大写）：`print('%X' % num3)`

### 1.2 浮点数输出

①  `%m.nf` 

`m` 指浮点数所占的总位数，前面不加 `-` 号则向右对齐，加了则向左对齐，不足则自动补充。`n` 是指小数点后保留的位数，按照四舍五入舍去多余位数，且默认是包留6位小数。

② `%m.ne` 

`%e` 是以科学计数法输出。`m` 是指整个科学计数法的位数，例如 `1.23e+03` 的位数为 `8`。`n` 是保留小数点的位数。

③ `%g`

`%g` 是 `%f` 和 `%e` 的简写。在保证六位有效数字的前提下，使用小数方式，否则使用科学计数法。

### 1.3 字符串输出

语法：`%m.ns`

含义：`m` 是字符串所占的位数，默认向右对齐，在 `m` 前面加上 `-` 号则向左对齐，不够则自动补齐。 `n` 是截取字符串的个数（从前往后）。

## 2. `format()` 函数

> 相对上述基本格式化输出方法，`format` 的方法虽然繁琐些，但功能更加强大。 `format()` 函数把字符串当作一个模板，通过传入的参数（可传入的参数无限制）进行格式化，使用 `{}` 和  `:` 当作占位符。

### 2.1 格式化字符串

语法：`str.format(params)` 

说明：`str` 是模板字符串，`params` 是以逗号 `,` 隔开的一个个的参数。

#### ① 位置匹配

+ 无编号位置匹配

  ```python
  print('{} {}'.format('hello', 'world')) # hello world
  ```

+ 有编号位置匹配（可打乱顺序）

  ```python
  print('{1} {1} {0}'.format('hello', 'world')) # world hello hello
  ```

+ 带关键字位置匹配

  ```python
  print('{name},{tool}'.format(name='murphy',tool='vscode')) # murphy,vscode
  ```

#### ② 通过列表（元组）索引设置参数

```python
sites = ['zhihu', 'google', 'jetbrians']
print('{0[1]} {0[0]} {0[2]}'.format(sites)) # google zhihu jetbrians
```

#### ③ 通过字典设置参数（`**` 不能少）

```python
dict = {'a': 'Alan', 'b': 'Brown'}
print('{a} and {b}'.format(**dict)) # Alan and Brown
```

#### ④ 截取和格式化字符串

语法：`str.format()`

模板字符串`str`：`<序号>:<填充字符><对齐方式><宽度><截取位数><s>`

```
print('{:*^9.3s}'.format('hello'))
# 意思是截取前3位，共占9位，截取的字符串居中，多余的位置用*填充
# output:***hell***

print('{:@>10s}'.format('world'))
# output:@@@@@world
```

### 2.2 格式化数字

语法：`str.format(params)`

说明：模板字符串 `str` 不仅包括了**参数序号**（从`0` 开始），还包括了**格式控制标记**（可选）信息。

`str` 的格式：`{<参数序号>:<格式控制标记>}`   ==  `{<参数序号>:<填充字符><对齐方向><宽度><,><.精度><数字类型>`}

具体参考如下表：（注意各项标记信息的形式，`<>` 只是为了提高可读性）

| `<参数序号>`                    | `:`    | `<填充>`               | `<对齐>`                                                     | `<宽度>`         | `<,>`                                  | `<.精度>`                              | `<类型>`                                           |
| ------------------------------- | ------ | ---------------------- | ------------------------------------------------------------ | ---------------- | -------------------------------------- | -------------------------------------- | -------------------------------------------------- |
| 当`format()` 接收多个数字时使用 | 分隔符 | 用于填充多余位置的字符 | 指定了数字的对齐方向；`<` 指向左对齐，`>` 指向右对齐，`^` 居中对齐 | 输出数所占位位数 | 开启数字（整数和浮点数）的千分位分隔符 | 浮点数小数部分的精度或字串符截取的长度 | 整数类型（`d`,`b`,`o`,`x`,`X`），浮点数类型（`f`） |

#### ① 格式化整数

+ 以 `,` 分隔千分位

  ```python
  print('{:,d}'.format(10000000)) 
  # output:10,000,000
  ```

+ 以科学计数法输出（默认包留6位小数）

  ```python
  print('{:e}'.format(12345678))
  # output:1.234568e+07
  ```

+ 进制转换格式化

  + 十进制输出：`{:d}.format(n)` 
  + 二进制输出：`{:b}.format(n)`
  + 二进制输出（带前缀 `0b` ）：`{:#b}.format(n)`
  + 八进制输出：`{:o}.format(n)`
  + 八进制输出（带前缀 `0o` ）：`{:#o}.format(n)`
  + 十六进制输出：`{:x}.format(n)`
  + 十进制输出（大写）：`{:X}.format(n)`
  + 十进制输出（带前缀 `0x`）：`{:#x}.format(n)`

  > 使用 `format()` 进制转换还有另一种形式：
  >
  > `print(format(n, 'x')`
  >
  > `print(format(n, 'X'))`
  >
  > `print(format(n, '#X'))`

#### ② 格式化浮点数

+ 包留小数点后3位（四舍五入）

  ```python
  import math
  print('{:.3f}'.format(math.pi))
  # output:3.142
  ```

+ 科学计数法

  ```python
  print('{:.3e}'.format(12345.678976))
  # output:1.235e+04
  ```

+ 舍去小数部分（不循序四舍五入）

  ```python
  print('{:.0f}.format(2020.6562)')
  # output:2020
  ```

+ 百分比 `{:.2%}`

  ```python
  print('{:.2%}'.format(0.25678))
  # output:25.68%
  ```

+ 带符号包留小数点后2位

  ```python
  print('{:+.2f}.format(3.14159)')
  # output:+3.14
  ```

## 3. `f-string` 方法

`f-string`，亦称为格式化字符串常量（formatted string literals），是Python3.6新引入的一种字符串格式化方法，该方法源于[PEP 498 – Literal String Interpolation](https://python.org/dev/peps/pep-0498/)，主要目的是使格式化字符串的操作更加简便。``f-string` 在形式上是以 `f` 或 `F` 修饰符引领的字符串（`f'xxx'` 或 `F'xxx'`），以大括号 `{}` 标明被替换的字段；`f-string` 在本质上并不是字符串常量，而是一个在运行时运算求值的表达式：

> While other string literals always have a constant value, formatted strings are really expressions evaluated at run time.
> （与具有恒定值的其它字符串常量不同，格式化字符串实际上是运行时运算求值的表达式。）
>
> —— [Python Documentation](https://docs.python.org/3/reference/lexical_analysis.html#formatted-string-literals)

这部分暂未更新，具体请参考这里：[CSDN f-string](https://blog.csdn.net/sunxb10/article/details/81036693)

## 4. 关于 `print()` 函数

### 4.1 `print()` 函数配合 `%`，`format()` 进行数据格式化

> 见上文

### 4.2 `print(n, end='')`

`print()` 函数输出的时候默认换行，可加上 `end=''` 使其不换行。

```python
print('hello', end='')
```

除此之外，`end` 还可以是其他值。

```
print('hello', end=',')
```

### 4.3 `print(n1, n2, ... sep=' ')`

`sep` 指定了数据（n1,n2,...）之间的分隔符

## 5. `eval()`

