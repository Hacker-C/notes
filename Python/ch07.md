# （七）Python程序流程控制

> Python有三种流程控制结构
>
> + 顺序结构（略）
> + 选择结构
> + 循环结构

## 1. 顺序结构

按照循序从上到下依次执行语句的结构就是循序结构，是最简单的流程控制结构。

## 2. 选择结构

> `condition` : 可判断 True / False 的条件表达式
>
> `statement`: 满足该条件下所要执行的语句

### 2. 1 `if` 语句

```python
if condition:
    statement
```

###  2.2 `if-else` 语句

```python
if condition:
    statement1
else:
    statement2
```

### 2.3 `if-elif-else` 语句

```python
if condition1:
    statement1
elif condition2:
    statement2
elif condition3:
    statement3
...
else:
    statementN
```

### 2.4 `if` 嵌套语句

`if`、`if-else`、`if-elif-else` 之间可以嵌套，根据开发的具体情况选择合理的嵌套方案。并严格遵守不同级别的 `if` 语句的代码缩进规范。

### 2.5 `pass` 语句

`pass` 语句是空语句，不做任何事情，用来占位，是为了保持程序结构的完整性。
在实际开发中，往往是为了搭起陈旭的整体逻辑结构，暂时不去实现那些细节，之后根据需要添加代码。
```py
pass
```

### 2.6 `assert` 语句

`assert` 语句又叫断言语句，用于判断一个表达式的值，当某个表达式为真，则程序继续向下执行，否则，报 ` AssertionError ` 错误，程序在此终止。
`assert` 的用处在于，与其让程序在晚些时候崩溃，不如在错误条件出现时，就直接让程序崩溃，这有利于我们对程序排错，提高程序的健壮性。

```python
assert expression
```

### 2.7 关于缩进

Python 以缩进来标记代码块的，缩进量相同的代码就成为同一个代码块。Python 规定了代码块必须缩进，且缩进量要相同，但未规定缩进量的大小。一般以一个 `tab` 或者 4 个空格键（大部分编辑器或IDE中，一个tab就是4个空格）为一个缩进量。

Python编程规范

+ 同一个代码块的所有语句都要缩进

+ 统一代码快的缩进量相同

+ 不要随意缩进（纯顺序结构不缩进）

### 2.8 `if` 语句的选择

`if-elif-else` 语句只执行一种情况，若要执行多种符合条件的情况则可以使用独立 `if` 语句。 

## 3. 循环结构

### 3.1 `while` 循环

```py
while condition:
    statement
```

### 3.2 `for` 循环

```python
for iterating_var in String|List|Tuple|Dict|Set：
    statement
```

示例
```python
for i in 'hello':
    print(i)
for i in [1, 2, 3]:
    print(i)
for i in (1, 2, 3):
    print(i)
for i in dict:
    print(dict[i])
for i in {'a', 'b', 'c'}:
    print(i)
```

> iterating_var:迭代变量

### 3.3 嵌套循环

`for` 和 `while` 之间（`for`和`for`、`while`和`while`、`for`和`while`之间均可进行循环）可以嵌套循环。

### 3.4 `break` 和 `continue` 语句

`break` 终止最近的这个循环；`continue` 跳过本轮循环，进行下一轮循环。

break 示例：
```python
if True:
    break
```

continue 示例：
```python
if i % 2 == 0:
    continue
```

### 3.5 `for i in range(j)` 方法

`range(j)` 函数是 python 内置的函数，依次返回 `[0, j)` 的 `j` 个整数。

`range(M,N)` 依次返回 `[M, N)` 的 `N-M` 个整数。

```python
for i in range(10):
    print(i, end=' ')
# output:0 1 2 3 4 5 6 7 8 9 
```

