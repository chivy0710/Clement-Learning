# Markdowm 语法
## 兼容HTML语法
不展开，会 HTML自己去看

## 标题
this is an H1 tittle
===

this is an H2 tittle
---

* etext形式的标题只能表示标题1和标题2这两阶，而atx形式的标题可以表示标题1~标题6共6阶。
* 上面#与文本之间的空格不是必需的，不加也可以，但加上是个好的习惯。
* 你可以选择性地「闭合」atx样式的标题，这纯粹只是美观用的，若是觉得这样看起来比较舒适，你就可以在行尾加上 #，而行尾的 # 数量也不用和开头一样（行首的#数量决定标题的阶数）。

## 区块引用Blockquotes

> 第一条
> 第二条

Markdown 也允许你偷懒只在整个段落的第一行最前面加上> ： 
区块引用可以嵌套（例如：引用内的引用），只要根据层次加上不同数量的 > ：

 
> 这是区块引用的第一层。
>
> > 这是嵌套引用，属于第二层，因此需要再加一个`>`，两个`>`之间的空格不是必需的。
>
> 回到区块引用的第一层。

## 列表
支持有序列表和无序列表。 
无序列表使用星号、加号或是减号作为列表标记：

*   Red
*   Green
*   Blue
等同于：
+   Red
+   Green
+   Blue
等同于：
-  Red
-  Green
-  Blue
有序列表使用一个数字接着一个英文句点：
1. red
2. green
3. blue

## 分隔符
你可以在一行中用三个以上的星号、减号、底线来建立一个分隔线，行内不能有其他东西。你也可以在星号或是减号中间插入空格。下面每种写法都可以建立分隔线：
* * *
1
***
2
*****
3
- - -

## 链接

这是一个可点击的URL：
<http://www.csdn.net/>

这是一个可点击的Email：
<address@example.com>

[百度](https://www.baidu.com/ '百度')
[链接文字](链接URL "可选的链接title")
[链接文字](链接URL (可选的链接title))

详细说明就是： 
* 一个方括号，里面输入链接文本； 
* 接着一个圆括号，里面可以包含两部分内容，中间用空格隔开； 
* 【必须】 链接的网址； 
* 【可选】 链接的title文字，只要用单引号、双引号或者括弧把title文字包起来即可，加上title之后，你用鼠标移到该链接时就会显示title文字，可以把它当作一种提示信息。

## 强调

*1个*\**左右包起来表示斜体*
**2个**\***左右包起来表示粗体**
***3个***\****左右包起来表示粗斜体***

## 反斜扛的用处

Markdown可以利用反斜杠来插入一些在语法中有其它意义的符号，从而显示出这些符号，有：
\\   反斜线
\`   反引号
\*   星号
\_   底线
\{}  花括号
\[]  方括号
\()  括弧
\#   井号
\+   加号
\-   减号
\.   英文句点
\!   惊叹号


