# 感知机(preceptron)

*Clément édite à 13.10.2016, vient de "统计学习方法,李航"*

感知机是二分类的线性分类模型，输入为实例的特征向量，输出为实例的类别，取+1 和 —1 二值。
感知机学习旨在求出将训练数据进行线性划分的分离超平面，属于判别模型。

	感知机是最简单的机器学习网络模型，我们常用的BP网络严格来说是使用了“BP算法”进行训练的“多层感知机模型”。多层感知器（MLP，Multilayer Perceptron）是一种前馈人工神经网络模型，其将输入的多个数据集映射到单一的输出的数据集上，可以解决任何线性不可分问题。

## 描述
导入基于误分类的损失函数，利用梯度下降法对损失函数进行极小化，求得感知机模型。是神经网络与支持向量机的基础。

## 感知机模型
假设输入空间(特征空间)是${\cal X} \subseteq R^n$,输出空间是${\cal Y} = \{+1，-1\}$.输入$x \in {\cal X}$表示实例的特征向量，对应于输入空间(特征空间)的点;输出$y \in {\cal Y}$表示实例的类别。由输入空间到输出空间的如下函数
$$f(x)= sign(w \cdot x + b)$$
称为感知机。其中，w和b为感知机模型参数，$w \in R^n$叫做权值(weight)或权值向量(weight vector), $b \in R$叫做偏置(bias)，$w \cdot x$表示w和x的内积。sign是符号函数，即
$$
 sign(x) = \left\{\begin{array}
 +1, \qquad x\geq0 \\
 -1, \qquad x< 0 \\
 \end{array}\right.
$$
感知机是一种线性分类模型，属于判别类别。线性方程：
$$w \cdot x + b = 0$$
对应于特征空间R^n^中的一个超平面S，其中w是超平面的法向量，b是超平面的截距。超平面S称为分离超平面(separating hyperplane).
![perceptron](\imgs\perceptron-model.png)
训练数据集(实例的特征向量及类别)：$T=\{(x_1,y_1),(x_2,y_2),\cdots,(x_N,y_N)\}$
其中$x_i \in {\cal X} = R^n, y_i \in {\cal Y} = \{+1,-1\},i=1,2,\cdots,N$

## 感知机学习策略

### 数据集的线性可分性
首先，要求数据集必须线性可分，即存在一个超平面S能够将数据集的正实例点和负实例点完全正确地划分到超平面的两侧。

### 损失函数
损失函数的选择是误分类点到超平面S的总距离，输入空间R^n^中任意一点x~0~到超平面S的距离：
$$\frac1{||w||}|w\cdot x_0+b|$$
这里，||w||是w的L~2~范数。
误分类点x~i~到超平面S的距离是：
$$-\frac1{||w||}y_i(w\cdot x_0+b)$$
假设超平面S的误分类点集合为M，那么所有误分类点到超平面S的总距离为
$$-\frac1{||w||}\sum_{x_i \in M}y_i(w\cdot x_0+b)$$
可令$\frac1{||w||}=1$,就得到感知机学习的损失函数。

给定训练集数据集
$$T=\{(x_1,y_1),(x_2,y_2),\cdots,(x_N,y_N)\}$$
其中$x_i \in {\cal X} = R^n, y_i \in {\cal Y} = \{+1,-1\},i=1,2,\cdots,N$. 感知机sign(wx+b）学习的损失函数定义为：
$$L(w,b)=-\sum_{x_i \in M}y_i(w\cdot x_0+b)$$
M为误分类点的集合，这个损失函数就是感知机学习的经验风险函数。因此，给定训练数据集T，损失函数L(w,b)是w,b的连续可导函数。

## 感知机学习算法
感知机学习问题转化为求解损失函数式最优化的问题，最优化的方法是随机梯度下降法。

### 感知机学习算法的原始形式
给定训练集数据集
$$T=\{(x_1,y_1),(x_2,y_2),\cdots,(x_N,y_N)\}$$
其中$x_i \in {\cal X} = R^n, y_i \in {\cal Y} = \{+1,-1\},i=1,2,\cdots,N$,求参数w,b,使其为以下损失函数极小化问题的解
$$\min_{w,b}L(w,b)=-\sum_{x_i \in M}y_i(w\cdot x_0+b)$$
感知机学习算法是误分类驱动的，具体采用随机梯度下降法(stochastic gradient descent).首先任意选取一个超平面$w_0,b_0$,然后用梯度下降算法不断地极小化目标函数。过程中是随机选取一个误分类点使其梯度下降。
假设误分类点集合M是固定的，那么损失函数L(w,b)的梯度由
$$\nabla_wL(w,b) = -\sum_{x_i \in M}y_ix_i $$
$$\nabla_bL(w,b) = -\sum_{x_i \in M}y_i $$
随机选取一个误分类点$(x_i,y_i),对w,b进行更新：$
$$w \leftarrow w+\eta y_i x_i$$
$$b \leftarrow b+\eta y_i$$
$\eta(0<\eta \leq1)$是步长，在统计学习中又称为学习率(learning rate).

### 算法
输入：$训练集数据集T=\{(x_1,y_1),(x_2,y_2),\cdots,(x_N,y_N)\}，其中x_i \in {\cal X} = R^n, y_i \in {\cal Y} = \{+1,-1\},i=1,2,\cdots,N$.
输出：w,b;感知机模型f(x)=sign(wx+b).
1.	选取初值$w_0,b_0$
2.	在训练集中选取数据$(x_i,y_i)$
3.	如果$y_i(w \cdot x_i + b)\leq 0$
$$w \leftarrow w+\eta y_i x_i$$
$$b \leftarrow b+\eta y_i$$
4.	转至2，直至训练集中没有误分类点。

### 算法的收敛性
为了便于叙述与推导，将偏置b并入权重向量w，记作$\hat{w}=(w^T,b)^T,将输入向量加以扩充，加进常数1，记作\hat{x}=(x^T,1)^T,这样,\hat{x} \in R^{n+1}, \hat{w} \in R^{n+1}。显然，\hat{w} \cdot \hat{x} = w \cdot x + b.$

**定理(Novikoff)** $设训练集数据集T=\{(x_1,y_1),(x_2,y_2),\cdots,(x_N,y_N)\}，其中x_i \in {\cal X} = R^n, y_i \in {\cal Y} = \{+1,-1\},i=1,2,\cdots,N,则$
(1)$存在满足条件||\hat{w}_{opt}||=1的超平面\hat{w}_{opt} \cdot \hat{x} = w_{opt} \cdot x +b_{opt} = 0将训练数据集完全正确分开;且存在\gamma>0,对所有i=1,2,\cdots,N$
$$y_i(\hat{w}_{opt} \cdot \hat{x} ）=y_i( w_{opt} \cdot x +b_{opt} )\geq \gamma$$
(2)$令R= \max_{1 \leq i \leq N}||\hat{x_i}||$,则感知机算法在训练数据集上的误分类次数k满足不等式
$$l \leq \left(\frac R{\gamma} \right)^2$$

### 感知机学习算法的对偶形式
对偶形式的基本想法是，将w和b表示为实例x~i~和标记y~i~的线性组合的形式，通过求解其系数而求得w和b。不是一般性，假设初始值$w_0,b_0$均为0.对误分类点(x_i,y_i)通过
$$w \leftarrow w+\eta y_i x_i$$
$$b \leftarrow b+\eta y_i$$
逐步修改w,b,设修改n次，则w，b关于$(x_i,y_i)$的增量分别是$\alpha_i y_i x_i和\alpha_i y_i$，这里$\alpha_i = n_i \eta$,最后学习到的w，b可以分别表示为
$$w=\sum_{i=1}^N\alpha_i y_i x_i$$
$$b=\sum_{i=1}^N\alpha_i y_i$$

这里，$\alpha_i\geq 0,i=1,2, \cdots,N, 当\eta = 1时，$表示第i个实例点由于误分而进行更新的次数。实例点更新次数越多，意味着它距离分离超平面越近，也就越难正确分类。

### 对偶形式算法
输入：$训练集数据集T=\{(x_1,y_1),(x_2,y_2),\cdots,(x_N,y_N)\}，其中x_i \in {\cal X} = R^n, y_i \in {\cal Y} = \{+1,-1\},i=1,2,\cdots,N.学习率\eta(0<\eta\leq1);$
$输出：\alpha,b;感知机模型f(x)=sign(\sum_{j=1}^N \alpha_j y_j x_j+b).$
$其中\alpha = (\alpha_1, \alpha_2,\cdots,\alpha_N)^T.$
1.	$\alpha \leftarrow 0,b \leftarrow 0$
2.	在训练集中选取数据$(x_i,y_i)$
3.	如果$y_i(\sum_{j=1}^N \alpha_j y_j x_j \cdot x_i + b)\leq 0$
$$\alpha_i \leftarrow \alpha_i + \eta$$
$$b \leftarrow b+\eta y_i$$
4.	转至2，直至训练集中没有误分类点。
对偶形式中训练实例仅以内积的形式出现。为了方便，可以预先将训练集中实例间的内积计算出来并以矩阵的形式存储，这个矩阵就是所谓的Gram矩阵(Gram matrix)
$G = [x_i \cdot x_j]_{N \times N}$

