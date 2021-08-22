# （四）Python 序列结构

|序列|支持的操作|
|-|-|
|字符串|索引、切片、相加、数乘|
|列表|索引、切片、相加、数乘、列表推导式|
|元组|索引、切片、相加、数乘|
|字典|索引、字典推导式、字典连接运算符|
|集合|索引|

## 1. 列表

1.1 访问列表元素

通过列表索引（从 `0` 开始）访问元素。
```python
>>> l = [1, 2, 3]
>>> l[0]
1
```

1.2 创建列表

通过 `[]` 或 `list()` 创建列表。
其中 `list()` 接收的参数是序列类（字符串、列表、元组、集合、字典）。

```python
>>> l1 = [1, 2, 3]
>>> l2 = list((1, 2, 3))
>>> l2
[1, 2, 3]
```

1.3 创建空列表

```python
>>> l0 = []
>>> l1 = list()
```

1.4 修改列表元素

列表属于可变数据类型，每一项都是可以改的。使用索引 `list[i]` 访问并赋值即可修改。
```python
>>> l[0] = 10 
```
1.5 添加列表元素

+ `append(x)` 方法
  在列表末尾添加元素。
+ `insert(i，x)` 方法
  在位置 `i` 处插入 `x` 元素，后续元素的下标都会改变。

1.6 删除列表元素

+ `del list[i]`
  直接删除索引是 `i` 的元素，无法使用。
+ `list.pop(i)` 
  弹出索引是 `i` 的元素，删除并使用该元素。
  当参数时，默认删除列表最后一项元素，可看作是栈顶。
+ `list.remove(x)`
  删除指定元素 `x`，无法使用。

1.7 列表的运算

+ 加法运算符
  ```python
  >>> l = [1, 2] + [3, 4, 5]
  >>> l
  [1, 2, 3, 4, 5]
  ```
  
+ 比较运算符
  逐项比较，直至比出结果。
  ```python
  >>> [1, 6, 5] > [1, 4, 2]
  True
  ```
  

 1.8 排序

+ 使用 `sort()` 方法进行永久性排序
  排序规则：数值大小和字母顺序（默认从小到大，前到后）
  ```python
  >>> l = [2, 1, 3]
  >>> l.sort()
  [1, 2, 3]
  ```
  
+ 使用 `sorted()` 函数进行临时排序
  排序规则：数值大小和字母顺序（默认从小到大，前到后）
  加参数 `reverse = True` 则规则相反
  ```python
  >>> l1 = ['b', 'a', 'c']
  >>> sorted(l1)
  ['a', 'b', 'c']
  >>> l1
  ['b', 'a', 'c']
  ```
  
+ 使用 `reverse()` 逆转列表
  ```python
  >>> [1, 3, 2, 5, 6].reverse()
  [6, 5, 2, 3, 1]
  ```

1.9 列表长度

  ```python
  >>> len(list)
  ```

1.10 切片

  与字符串的切片类似

1.11 列表解析式

语法：

```python
l = [expression for expr1 in sequence1 if condition1
                for expr2 in sequence2 if condition2
                ...
     						for exprN in sequenceN if conditionN]
```

举例1：

```python
>>> names = [' aa', 'bbb ', 'ccc ddd ', 123]
>>> names = [i.strip() for i in name if not isinstance(i, int)]
>>> names
['aa', 'bbb', 'ccc ddd']
```
举例2：

```python
l = [[1, 2, 3], [4, 5, 6, 7], [8, 9, 10, 11, 12, 13]]
l1 = [i for j in l
         for i in j]
print(l1)
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13]
```

1.12 列表的复制

**深拷贝**：（两个列表各有独立空间）

+ 使用切片 `[:]` 方法

  ```python
  l1 = l[:]
  ```

+ 使用 `copy()` 方法

  ```python
  l1 = l.copy()
  ```

**浅拷贝：**

直接使用列表名赋值，则会将两个列表关联起来（指向同一个地址）

## 2. 元组

元组使用圆括号来标识，属于不可修改类型的数据。

1.1 定义元组

+ 创建元组的方法

```py
tup = ('a', 'b', 'c)
```

+ 创造空元组

```py
tup1 = ()
```
+ 创造1个元素的元组

```py
tup2 = ('a',)
```

> ❗ 创造1个元素的元组不能使用 `tup = ('a')`，否则就是创造了一个字符串 `'a'` ，要在后面加英文逗号 `,`。

1.2 遍历元组

```python
# 方法一
for i in tup:
  print(i)
# 方法二
for i in range(len(tup)):
  print(tup[i])
```

1.3 修改元组

元组的元素是不能修改的，但是可以给元组重新赋值。



## 3. 字典


3.1 定义

字典被花括号 `{}` 包裹，由一对对的 *键值对* `key:value` 组成。

3.2 创建字典的方法

```py
# 依次赋值
dict1['aaa'] = 'bbb'
dict1[123] = 444
# 直接赋值
dict2 = {
    'name': 'murphy',
    'code': 'python',
    'site': 'https://mphy.gitee.io'
}
# 创建空字典
dict = {}
```

3.3 引用和修改字典

```python
>>> dict_name[key] # 引用键值对
>>> dict_name[key] = value # 修改键值对
>>> del dict_name[key] # 删除键值对
```

3.4 遍历字典

方法一：
```python
for i in dict1:
    print('{0}: {1}'.format(i, dict1[i]))
```
方法二：使用字典的 `items()` 方法
```python
for k, v in dict1:
    print('{0}: {1}'.format(k, .v)
```

3.5 遍历字典的键

方法一：
```python
for k in dict1:
    print(k)
```
方法二：
```python
for k in dict1.keys():
    print(k)
```

3.6 按顺序遍历字典的键
使用 `sorted()` 函数对字典的键进行顺序遍历。
```python
for k in sorted(dict1.keys()):
    print(k)
```

3.7 遍历字典的值
使用 `values()` 方法遍历字典的值。
```python
for v in dict1.values():
    print(v)
```
筛选出重复的值，使用 `set()` 方法。
```python
for v in set(dict1.values()):
    print(v)
```

3.8 嵌套

善用列表的 `items()` 、`keys()`, `values` 方法对嵌套型数据进行遍历操作。

+ 字典列表

    在列表中存储列表，形成字典列表。
    ```python
    alien_0 = { ... }
    alien_1 = { ... }
    alien_2 = { ... }
    aliens = [ alien_0, alien_1, alien_2 ]
    ```
+ 列表字典

    在字典中存储列表，形成列表字典。
    ```python
    fruits_like = {
        'Peter': [ 'apple', 'banana' ],
        'Jerry': [ 'orrange', 'banana', 'watermelon' ],
        'Murphy': ['apple']
    }
    ```

+ 字典型字典

    在字典中存储字典，形成字典型字典
    ```python
    users = {
        'murphy': {
            'site': 'https://mphy.gitee.io',
            'location': 'leiyang',
            'time': 2020
        },
        'xpoet': {
            'site': 'https://xpoet.cn',
            'location': 'xxx',
            'time': 2018
        }
    }
    ```



## 4. 集合

### 4.1 可变集合


① 创建集合的两种方式：
- 使用 `{}` 括起来
  ```python
  colors = {'red', 'blue', 'yellow', 'green'}
  ```
- 使用 `set()` 创建
  ```python
  letters = set('python')
  ```

② 构造空集合的方法

```py
s = set()
```

③ 集合的成员测试和删除重复元素

```py
s1 = {'google', 'baidu', 'zhihu', 'douban', 'google'}
# 成员测试
if 'google' in s1:
    print('google is in', s1)
else:
    print('google is not in', s1)
# 删除重复元素
print(s1)
```

> ❗ 注意构造空集合不能使用 `s = {}` 的方法，这是在构造空字典。

④ 集合间的运算

```python
a = {'a', 'b', 'c', 'd', 'e'}
b = {'b', 'c', 'd', 'e', 'f'}
print(a - b) # 集合间的差集
print(a | b) # 集合间的并集
print(a & b) # 集合间的交集
print(a ^ b) # 集合间的不同时存在的元素的集合（对称差集）
```

### 4.2 不可变集合

`frozenset()`

## 5. 推导式

### 5.1 列表推导式

### 5.2 字典推导式

### 5.3 集合推导式

