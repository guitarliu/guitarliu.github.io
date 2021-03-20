---
layout: post
title: "Python3 Functions"
date: 2020-07-30
excerpt: "Examples and code for displaying Python3 functions in posts."
tags: [Python3 Syntax]
comments: true
---

### 字典dict的keys()方法
~~~ 
>>> dict = {"a": 1, "b": 2}
>>> dict.keys()
dict_keys(["a", "b"])
>>> list(dict.keys())
['a', 'b']
~~~

### replace()方法把字符串中的old（旧字符串）替换成new（新字符串）
~~~
>>> str.replace(old, new[, max])
其中: 
old -- 将被替换的旧字符串
new -- 新字符串
max -- 可选字符串，替换不超过不超过 max 次
注意max这个参数，代表替换次数！
~~~

### 随机函数（random, uniform, randint, randrange, shuffle, sample）
#### random()方法：返回随机生成的一个实数，范围在[0, 1)
~~~
>>> import random
>>> print(random.random())
0.5926537041798844
~~~

#### uniform()方法
~~~
random.uniform(a, b): 用于生成一个指定范围内的随机浮点数，两个参数中;
其中一个是上限，一个是下限。如果a > b, 则生成的随机数n, 及b<=n<=a;
如果a>b, 则a<=n<=b.

>>> import random
>>> print(random.uniform(10, 20))
13.2960134544
>>> print(random.uniform(20, 10))
15.9038751838
~~~

#### randint()方法
~~~
random.randint(a, b): 用于生成一个指定范围内的整数。
其中参数a 是下限，参数b是上限，生成的随机数n: a<=n<=b

>>> import random
>>> print(random.randint(10, 20))
11
>>> print(random.randint(20, 20))
20
# print(random.randint(20, 10)) is wrong because b should bigger than a 
~~~

#### randrange()方法
~~~
random.randrange([start], stop[, step]): 从指定范围内，按指定基数递增的集合中获取一个随机数。
如: random.randrange(10, 100, 2), 结果相当于从[10,12,14,16,...,96,98]序列中获取一个随机数.
random.randrange(10,100,2)在结果上与random.choice(range(10,100,2))等效.

>>> import random
>>> print(random.randrange(10,100,2))
72
>>> print(random.choice(range(10,100,2))
28
>>> print(random.choice(range(10,100,2))
74
~~~

#### choice()方法
~~~
random.choice(sequence): 参数sequence表示一个有序类型。sequence在python不是一种特定的类型，
而是泛指一系列的类型。list, tuple, 字符串都属于sequence。

>>> import random
>>> print(random.choice("interesting")
e
>>> print(random.choice(["what", "is", "a", "pig"]))
a
>>> print(random.choice(("tuple", "list", "dict")))
~~~

#### shuffle()方法

~~~
random.shuffle(x[, random)): 用于将一个列表中的元素打乱
>>> import random
>>> p = ["what", "is", "a", "shame"]
>>> random.shuffle(p)
>>> p
["is", "a", "what", "shame"]
~~~

#### sample()方法
~~~
random.sample(sequence,k): 从指定序列中随机获取指定长度的片段，sample函数不会修改原有序列
>>> import random
>>> list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
>>> a = random.sample(list, 5) # 从list中随机获取5个元素，作为一个片段返回
>>> print(a)
[1, 6, 10, 8, 3]
>>> print(list) # 原有序列并没有改变
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
~~~

### python3中strip()、lstrip()、rstrip()用法
#### strip()
> 用来去除头尾字符、空白符(包括\n、\r、\t、 ‘ ’, 即: 换行、回车、制表符、空格)


#### lstrip()
> 用来去除开头字符、空白符(包括\n、\r、\t、' '，即: 换行、回车、制表符、空格)


#### rstrip()

> 用来去除结尾字符、空白符(包括\n、\r、\t、' '，即: 换行、回车、制表符、空格)


