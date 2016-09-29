# MARKDOWN 公式表示
######Clement整理于2016.9.21
## 环境（Windows）

　　需要使用MathJax引擎来编辑公式，公式直接以文字形式呈现，这样就不需要图片来显示公式，效果更好，修改更加方便。
　　使用的MARKDOWN的编辑器HarroPad，据说跨平台，用起来感觉还不错，也是今天才开始用。这个配置MathJax引擎非常方便。具体配置方式如下：

### HarroPad编辑器MathJax引擎配置

   按照目录打开：文件-->偏好设置，如图：
![偏好设置](\img\1.png)
选择左侧菜单项Markdowm，如图：
![偏好设置](\img\2.png)
勾选数学表达式选项的两项，如上图。即可以编辑数学公式了.

### 行内公式以及行间公式
#####行内公式

	标记方法：使用一个美元符号包围起来$数学公式$，或是最原始的$$$数学公式$$$

可是无法紧凑地显示行间公式，不知道这是个怎么情况。还是使用行间公式更方便，可能编辑器的问题，还是word用的习惯-_-。

**例子：**这是行内公式：$\Gamma(n) = (n-1)!\quad\forall n\in\mathbb N$
#####行间公式
	标记方法：两个美元符包围起来，例子：
$$ x = \dfrac{-b \pm \sqrt{b^2 - 4ac}}{2a} $$

### 上标和下标
	^表示上标，_表示下标。如果上下标的内容多于一个字符，要用{}把这些内容括起来当成一个整体。上下标是**可以嵌套的**，也可以同时使用。
例子：
$$x^{y^z}=(1+e^x)^{-2xy^w}$$

如果要在左右两边都有上下标，可以用\sideset命令,如下：
$$\sideset{^1_2}{^3_4}\bigotimes$$
### 分数表示
	方法1：\frac{分子}{分母}
	方法2：分子 \over 分母
#####方法1
$$\frac{a+b}{c+d}$$
#####方法2
$$1 \over 3$$

**注意**：对于\frac的方法，如果分子分母都是单个数，那么大括号{}可以省略，如：$\frac12$。

### 括号
	()、[]和|可以直接表示自己，而{}本来用于分组，因此需要用{}来表示自身，也可以使用\lbrace 和\rbrace来表示。
**例子：**
$$\{[z-(1+\frac23x)y]\div 4\}$$

**注意：**原始符号并不会随着公式大小缩放。有时候我们想要括号和分隔符显示的大点，比如上面例子中希望括号能把整个分数都包住，那么可以用\left和\right标记，实现自适应调整。
**例子：** 
$$\left(1+\frac23x\right)$$
**其他例子：**
方括号
$$\left[\frac12\right]$$
大括号
$$\left\{\frac12\right\}$$
尖括号
$$\left\langle\frac12\right\rangle$$
向上取整
$$\left\lceil\frac12\right\rceil$$
向下取整
$$\left\lfloor\frac12\right\rfloor$$

**注意：**\left和\right标记必须是成对出现的，但有时候我们只用到其中一个，比如只用一个|当作分割线，这时候可以通过.来表示空的那一方，即用\left.表达左边空的情况，用\right.表达右边空的情况。
**例子：**
$$\left. \frac{du}{dx} \right| _{x=0}$$

### 根号表示
根号开方使用\sqrt标记，语法格式如下：

    \sqrt[开方次数，默认为2]{开方因子}
**例子：**
$$\sqrt{x^3}　和　\sqrt[3]{\frac xy}$$

### 省略号
	数学公式中常见的省略号有两种，\ldots表示与文本底线对齐的省略号，\cdots表示与文本中线对齐的省略号。
**例子：**
$$f(x_1,x_2,\ldots,x_n) = x_1^2 + x_2^2 + \cdots + x_n^2$$

### 积分
	\int
**例子：**
$\int_0^1x^2{\rm d}x $

### 极限
	\lim
**例子：**
$\lim_{n\rightarrow+\infty}\frac{1}{n(n+1)}$
### 矢量表示
矢量用\vect标记实现，语法格式如下：

	\vec{矢量值}
**例子：**
$$\vec{a} \cdot \vec{b}=0$$

### 空格
为了给公式增加标号经常需要大量的空格，实现方法可以通过在ab间加入\空格或\;增加些许间隙，\quad 与 \qquad 会增加更大的间隙。
**例子：**
$a\;b$ 或 $a\quad b$ 或 $a\qquad b$

### 累加、累乘
	\sum，\prod
**例子：**
$\sum_1^n\frac{1}{x^2}$， $\prod_{i=0}^n\frac{1}{x^2}$

### 希腊字母
小写：
$\alpha \beta \gamma \delta \epsilon \zeta \eta \theta \iota \kappa \lambda \mu \nu \xi \omicron \pi \rho \sigma \tau \upsilon \phi \chi \psi \omega$

特殊记法(写法不同)：
$\varepsilon \varkappa \vartheta \varpi \varrho \varsigma \varphi$

大写：
$A B \Gamma \Delta E Z H \Theta I K \Lambda M N \Xi O \Pi R \Sigma T \Upsilon \Phi C \Psi \Omega$

### 数学符号汇总
± ：\pm 
× ：\times 
÷：\div 
∣：\mid

⋅：\cdot 
∘：\circ 
∗: \ast 
⨀：\bigodot 
⨂：\bigotimes 
⨁：\bigoplus 
≤：\leq 
≥：\geq 
≠：\neq 
≈：\approx 
≡：\equiv 
∑：\sum 
∏：\prod 
∐：\coprod
###### 集合运算符:
∅：\emptyset 
∈：\in 
∉：\notin 
⊂：\subset 
⊃ ：\supset 
⊆ ：\subseteq 
⊇ ：\supseteq 
⋂ ：\bigcap 
⋃ ：\bigcup 
⋁ ：\bigvee 
⋀ ：\bigwedge 
⨄ ：\biguplus 
⨆：\bigsqcup

###### 对数运算符：
log ：\log 
lg ：\lg 
ln ：\ln

###### 三角运算符： 
⊥：\bot 
∠：\angle 
30∘：30^\circ 
sin ：\sin 
cos ：\cos 
tan ：\tan 
cot ：\cot 
sec ：\sec 
csc ：\csc

###### 微积分运算符： 
y′x：\prime 
∫：\int 
∬ ：\iint 
∭ ：\iiint 
∬∬：\iiiint 
∮ ：\oint 
lim ：\lim 
∞ ：\infty 
∇：\nabla

###### 逻辑运算符： 
∵：\because 
∴ ：\therefore 
∀ ：\forall 
∃ ：\exists 
≠ ：\not= 
≯：\not> 
⊄：\not\subset

###### 戴帽符号： 
y^ ：\hat{y} 
\check{y} ：\check{y} 
y˘ ：\breve{y}

###### 连线符号： 
$\overline{a+b+c+d} $
$\underline{a+b+c+d}$
$\overbrace{a+\underbrace{b+c}_{1.0}+d}^{2.0}$

###### 箭头符号： 
↑：\uparrow 
↓：\downarrow 
⇑ ：\Uparrow 
⇓：\Downarrow 
→：\rightarrow 
← ：\leftarrow 
⇒ ：\Rightarrow 
⇐ ：\Leftarrow 
⟶ ：\longrightarrow 
⟵ ：\longleftarrow 
⟹：\Longrightarrow 
⟸ ：\Longleftarrow

###### 使用指定字体:
{\rm text}如： 
使用罗马字体：text ${\rm text}$ 

其他的字体还有： 
\rm　　罗马体　　　　　　　\it　　意大利体 
\bf　　黑体　　　　　　　　\cal 　花体 
\sl　　倾斜体　　　　　　　\sf　　等线体 
\mit 　数学斜体　　　　　　\tt　　打字机字体 
\sc　　小体大写字母




