# 爬坑记

> 记录掉过的坑、易错点、细节。

一、用IDE写Java程序出现以下错误

```basic
Resource leak: 'input' is never closed
```

+ 原因：声明了名为input的数据输入扫描仪（Scanner），系统就会为它分配相应的内存空间，但是在程序结时却<font color=red>没有释放该内存</font>，会造成资源浪费，从而出现警告。
+ 解决：在mian()函数结束时调用<font color=red> `input.close();` </font>函数结束数据流，释放内存。

二、关于拓宽类型和缩窄类型

+ 将一个小范围的变量转换为大范围的变量称为拓宽类型
+ 将一个大范围的变量转换为小范围的变量称为缩窄类型
+ 拓宽类型可以自动完成，缩窄类型需要显式转换。

三、Unix时间戳

+ 计算机科学中，格林威治时间1970年7月1日0点称为Unix时间戳。

`System.currentTimeMillis()` 返回一个 `long` 型的距Unix时间戳的毫秒数。

四、四舍五入包留一位小数（低配版）

```java
double test = 123.456;
double result;
int left = (int)(test * 100) % 10;//获取小数点后第二位数字
if (left >= 5) {
  	result = (double)((int)(v * 10) + 1) / 10;
} else {
  	result = (double)(int)(v * 10) / 10;
}
System.out.println(result);
```

> 其他形式的类似。

五、使用 `Math.random()` 生成指定区间的整数

`[a, b]`

```java
int test = (int)(Math.random() * (b -a + 1) + a)
```

六、生成指定区间的字符

`[ch1, ch2]`

```java
char test = (char) (Math.random() * (ch2 - ch1 + 1) + ch1);
```


