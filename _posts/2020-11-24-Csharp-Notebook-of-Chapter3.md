---
layout: post
title: "Csharp Notebook of Chapter3"
date: 2020-11-24
excerpt: "Examples and code for displaying Csharp."
tags: [Csharp, codes, syntax]
comments: true
---

## Chapter3 变量和表达式
### Csharp注释的两种方式
* 注释一
~~~
/* This is a comment */
/* And so...
         ...is this! */
~~~
下面的语句错误：
~~~
/* Comments ofter end with "*/" characters. */ 
~~~
注释结束符好厚的后的内容（"*/"后面的字符）会被当做C#代码，因此产生错误。
* 注释二
~~~
// This is a different sort of comment.
~~~
这类注释可用于语句的说明文档，因为他们都放在一行上:
~~~
<a statement>;      // Explanation of statement
~~~
下面的语句错误:
~~~
// So is this,
   but this bit isn't.
~~~
第二行代码会被解释为C#代码。
* 注释三
~~~
/// A special comment
~~~
### 代码大纲功能
~~~
#region Using directives
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
#endregion
~~~
---
### **_剩余细节语法自行查看官方文档_**
***[C#官方文档中文版](https://docs.microsoft.com/zh-cn/dotnet/csharp/)***<br> 
***[C#官方文档英文版](https://docs.microsoft.com/en-US/dotnet/csharp/)***

