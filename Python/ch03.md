# （三）玩转 python 字符串

## 1. 转义字符

1.1 python中的字符串是用双引号 `""` 或者单引号 `''` 括起来。用反斜杠 `\` 表示转义字符

1.2 常见转移字符
|转移字符|含义|
|:-:|-|
|`\n`|换行|
|`\t`|制表|
|`\\`|转移反斜杠|
|`%%`|特殊转义符，显示 `%`|

## 2. 索引与切片

方法：前闭后开原则  
格式
![avatar](https://s1.ax1x.com/2020/09/01/dxk3mq.png)

举例
```py
str = 'hello,world'
print(str[1:])    # ell,world
print(str[:1])    # h
print(str[0:1])   # h
print(str[-1:])   # d
print(str[4:6])   # o,
```

## 3. 字符串运算

2.4 字符串的计算

当 `+` 用在在字符串之间，则表示拼接符。
使用 `*` 表示重复，格式为 `n * str`，其中 n 为整数，str 为字符串。

```py
str = 'hello'
print (str + '233' * 3)
# 输出：hello233233233
```

## 4. 字符串处理方法

|方法名|描述|举例|
|-|-|-|
|`str.title()`|将字符串中每个单词首字母大写|`murphy chen.title`结果是 `Murphy Chen`|
|`str.upper()`|全部转为大写|`'HELLO'.lower()` 结果是 `hello`|
|`str.lower()`|全部转为小写|`'world'.upper()` 结果是 `WORLD`|
|`str.split(sep, n)`|以 `sep` 为界对 `str` 进行 `n` 次切分，切分形成的子串作为列表的元素，返回该列表|`'a#bb#ccc#dddd'.split('#', 2)` 结果是 `['aa','bb','ccc#dddd']`|
|`str.count(sub)`|返回子串 `sub` 在 `str` 中出现的次数|`'a atom allow'.count('a')` 结果是 `3`|
|`str.replace(old, new[, max])`|将 `str` 中的子字符串 `old` 转换为新字符串 `new`，`max` 设置了最大转换数量|`'aaabbcc'.replace('a', '6', 2)` 结果是 `'66abbcc'`|
|`str.center(width[, fillchar])`|返回一个原字符串居中,并使用空格填充至长度 `width` 的新字符串。默认填充字符为空格。|`'python'.center(10, '*')` 结果是 `'**python**'`|
|`str.rstrip()`|去除右侧空白（`'' \n \t`）||
|`str.lstrip()`|去除左侧空白||
|`str.strip(chars)`|去除`str` 开头和结尾中在 `chars` 中列出的字符|`'  **aa**bbcc**'.strip(' *')` 结果是 `'aa**bbcc'`|
|`str.join(iter)`|在 `iter` 元素除最后一个外每个元素后增加字符 `str`|`'1234'.join(',')` 结果是 `'1,2,3,4'`|
