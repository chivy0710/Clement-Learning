# GVM神经网络

_Clement Edit, 2016.7.25_

\[TOC\]

## 神经网络

神经网络是一个映射：Y~n~=Φ（X~n~，Λ）
$X\_n表示输入，n∈IR^N$
$Y\_n表示输出，n∈IR^N$
$Λ表示参数集，Λ∈IR^M$
$\(X\_n^µ, Y\_n^µ\)表示样本数据，µ = 1,...,M$
输入通常表示的是n维的矢量，无论图像或是声音，都需要前处理变为n维的矢量，这个过程通常就就是所谓的特征提取。对于图像，可以采用像素化等其他方法，对于声音，可以采用投射到标准基以及傅里叶变换等方法。
而训练一个神经网络，通俗来讲，就是寻找合适的Λ参数，通过合适的λ参数，来实现对输入数据，按照构想的输出。

## 常用的浅层神经网络

### 常用的3层神经网络

常用的浅层神经网络通常有3种，或是说成熟的3种理论，其他一些相关的3层网络大多是3种理论的变种。3种网络有BP网络（Back Propagation）多层前馈网络，SVM（Support Vector Machine）支持向量机，以及GVM（General Vector Machine）一般向量机。三层网络理论已经趋于完善，可以给出严格的数学证明，而多层网络目前尚不完善，更多的是网络层数的堆积啊，仅通过经验来看出网络效果是否更好（显而易见的是，网络层数的增加，控制参数也更多，那么通过对参数的调节，总是可能会找到比浅层网络更好的结果，但也可能不会）。

### 神经网络要控制的风险

神经网络需要控制三种风险，经验风险、结构风险以及设计风险。
经验风险即使得误差最小，拟合得到的结果与真实结果尽可能相同，虽然结果越接近越好，但是当结果完全一致的时候，可能会存在过拟合的情况。
![](/Machine Learning/imgs/fitting.png)
结构风险取决于输入输出的敏感性，一般而言，敏感性越小，结构风险也越小。敏感性体现在各阶导数上，直观体现在数据点上的斜率。斜率相差的越小，即曲线更平滑，发生过拟合的可能性也越小。对于特殊的如僭越函数，并不能用上述方法控制结构风险。
设计风险用结果的区间来度量，进行一次训练得到一个正确率，那么多次训练得到的正确率可能是在一个范围区间，这个区间度量设计风险，如果区间很大，则说明设计风险大，反之，区间小则设计风险小。其体现的是结果的稳定性，只有设计风险比较小才能说明训练的结果比较好，即体现网络的可重复性。

### BP网络

BP网络相对比较简单，属于局域学习算法，能够保证经验风险的最小化，网络一般为三层，权值为w~ij~，v~jl~，利用梯度下降算法来寻找最优解，容易陷入局部最小化的泥潭，但是由于采用解析解，运行速度非常快，一般给出的学习网络效率高。其考虑到了经验风险，使用过程中要把握训练次数的度，训练太多容易过拟合。

### SVM网络

SVM数学推导会更复杂，网络一般也为三层，SVM属于全局算法，SVM的核心是寻找支持向量，支持向量一般从训练样本里面找，隐含层个数取决于支持向量的个数。对于支持向量，列与输入维数有关，行与支持向量个数有关。采用线性最优化理论，来构造最大间隔，即让训练样本都在最大间隔之外。当测试数据输入时，若在最大间隔外，则能很好的识别，如果在最大间隔内，也可能识别到，当然也可能识别错误，如图所示。
![](/Machine Learning/imgs/SVM-showing.png)
SVM考虑到了结构风险问题，所以网络相对来说更复杂，但是效果也更好，对于设计风险，并没有涉及。

### GVM网络

GVM同样为三层网络，基于统计学习的基础，采用的是蒙特卡罗方法，随机改变某一参数，灵活性强，考虑目前计算机的性能，效率还是可行的，在运行较长时间情况下，还是可以获得较好结果，同时，由于灵活性比较强，可以引入结构风险以及设计风险来改善程序运行效果，避免陷入局部最小化问题。相比较于SVM可以设置更多的隐藏层，即更多的向量，通常来说，隐藏层维度越高，网络中提取的信息也就越多。

## 使用GVM来进行函数拟合

对于输入为1维，输出同样为1维的函数来说。设隐藏层神经元为M个，则神经网络结构为1-M-1。如图所示：
![](/Machine Learning/imgs/GVM-1-N-1.png)
对于输入层每一个输入x，从输入层到隐藏层的计算过程，有如下计算公式：

$$o_j = f_j(\beta_jh_j),h_j = \sum_{j=1}^Mw_jx-b_j, j = 1,\cdots,M \qquad(1)$$

其中，
①    M表示隐藏层神经元个数，即隐藏层的维度。
②    fj表示激活函数，之所以具有下标j是因为在同一个神经网络中，对于不同数据可以采用不同的激活函数，对于不连续函数会有较好的拟合效果，而采用BP算法，激活函数必须一致，这也正体现了GVM的灵活性。

#### 常见的激活函数：

$Sigmoid函数：y=\frac1{1+e^{-x}}   函数将x投射到0到1之间的S曲线，非线性，过中心0.5。$
![](/Machine Learning/imgs/sigmoid.png)
$Gauss函数：y=e^{-x^2}$
![](/Machine Learning/imgs/gauss.png)
$Tanh函数：y =\frac{e^x-e^{-x}}{e^x+e^{-x}} 函数将x投射到-1到1之间的S曲线，非线性，过中心0。$
![](/Machine Learning/imgs/tanh.png)
多项式函数：最高阶根据具体需求来定，图为三次多项式函数.
![](/Machine Learning/imgs/polynome.png)

③    h~j~表示的是局域场。
④    w~j~表示的是输入层到隐藏层的权值。
⑤    b~j~表示的是局域场的偏置量，在x取值为0时，函数值恒为0，引入这样一个偏置量，可以避免在x为0时的不连续。
⑥    βj表示的是激活函数系数，控制局域场数据的范围，对于神经网络训练影响较大。
从隐藏层到输出层的计算过程，有如下计算公式：

$$y=h_j, h_j=\sum_{j=1}^Mv_jo_j，j=1,…,M\qquad(2)$$

其中，
①    v~j~表示隐藏层到输出层的权值。
\(2\)式构造的是线性神经元，可以通过进一步增加传输函数来构造非线性神经元。
参数取值范围：
1.w  取值范围设为C~w~ \[-1,1\]
2.b  取值范围设为C~b~ \[-2,2\] ，b的取值范围可适当大一些，对于网络影响较小。
3.β  取值范围设为C~β~ \[-1,1\]
4.v  取值范围设为C~v~ \[\|-1,1\|\]，v的取值为-1或是1。

## 使用GVM函数拟合过程

1. 参数初始化，对于参数随机在取值范围内赋值。
2. 通过上述公式来计算得到的输出值。
3. 计算的输出值与真实的输出值进行比较，引入cost函数来计算误差。
  $$e = \sqrt {\frac1M\sum_{j=1}^M(y'-y)^2}\qquad(3)$$

  其中，
  1\) y’表示计算得到的输出值。
  2\) y 表示实际的输出值。
4. 随机改变上述四个参数，计算得到新的误差，若新的误差比旧的误差小，则允许改变，否则恢复原来的参数值。
5. 多次迭代直到取得较小的误差值，从而得到较好的拟合效果。

## GVM函数拟合程序

以sin函数为例进行函数拟合，sin函数为非线性函数。采用C语言编写。
函数拟合的区间为\[-π，π\]。

### 拟合效果图

![](/Machine Learning/imgs/GVM-Fitting-Result.png)

### Code

```1c
#ifdef _MSC_VER
#define _CRT_SECURE_NO_WARNINGS
#endif
//设置输入文件、输出文件以及结果文件的路径
#define Input_txt "D:\\project\\Deeplearning\\MCsin0\\in.txt"
#define Output_txt "D:\\project\\Deeplearning\\MCsin0\\out.txt"
#define Result_txt "D:\\project\\Deeplearning\\MCsin0\\result.dat"
//训练样本个数
#define Data 15
//输出样本个数
#define OutData 200
#define neuron 150
#define traintime 2000000
#define Pi 3.141592653

#include<math.h>
#include<stdio.h>
#include<stdlib.h>
#include<time.h>

double d_in[Data], d_out[Data];
double w[neuron], v[neuron], o[neuron],beta[neuron],b[neuron];
double OutputData;
double e, tempE, temp;
int MC,change;
double result(double test);
//产生数据源，顺序生成Data个-Pi到Pi以内的数作为输入项，通过计算sin值得到输出项
void data_source()
{
    double s_in[Data], s_out[Data];
    int i;
    double interval;
    FILE *f1, *f2;
    interval = 2 * Pi / (Data - 1);
    for (i = 0; i < Data; i++)
    {
        s_in[i] = -1* Pi+ i * interval;
        s_out[i] = sin(s_in[i]);
    }
    f1 = fopen(Input_txt, "w");
    if (f1 == NULL) printf("file open failed");
    for (i = 0; i < Data; i++)
        fprintf(f1, "%f\n", s_in[i]);
    fclose(f1);
    f2 = fopen(Output_txt, "w");
    for (i = 0; i < Data; i++)
        fprintf(f2, "%f\n", s_out[i]);
    fclose(f2);
}

//读取数据到d_in中和d_out中
void read_data()
{
    FILE *f1, *f2;
    int i;
    f1 = fopen(Input_txt, "r");
    if (f1 == NULL) printf("file open failed!");
    i = 0;
    while (!feof(f1))
    {
        fscanf(f1, "%lf", &d_in[i]);
        i++;
    }
    fclose(f1);
    f2 = fopen(Output_txt, "r");
    if (f2 == NULL) printf("file open failed!");
    i = 0;
    while (!feof(f2))
    {
        fscanf(f2, "%lf", &d_out[i]);
        i++;
    }
    fclose(f2);
}

//结果写到文件
void data_output()
{
    double out_in[OutData], out_out[OutData];
    int i;
    double interval;
    interval = 2 * Pi / (OutData - 1);
    FILE *f1;
    for (i = 0; i < OutData; i++)
    {
        out_in[i] = -1 * Pi + i * interval;
        out_out[i] = result(out_in[i]);
    }
    f1 = fopen(Result_txt, "w");
    if (f1 == NULL) printf("file open failed");
    for (i = 0; i < OutData; i++)
        fprintf(f1, "%f %f %f\n", out_in[i],out_out[i],sin(out_in[i]));
    fclose(f1);
}

//神经网络初始化，对权值进行随机数初始化
void initMCNetwork()
{
    int i;
    for (i = 0; i < neuron; i++)
    {
        //第一个权值量
        w[i] = ((rand() %10000 * 2.0) / 10000 - 1);
        //第二个权值量
        v[i] = (rand() * 2 / RAND_MAX - 1);
        if (v[i] == 0) v[i] = 1;
        //偏置量
        b[i] = (rand() % 10000 * 0.0004*Pi – 2*Pi);
        //局部量权值
        beta[i] = ((rand() % 10000 * 2.0) / 10000 - 1);
        o[i] = 0;
//        printf("%lf\n", b[i]);
    }
}

void computO(int var)
{
    int i;
    double sum;
    OutputData = 0;
    for (i = 0; i < neuron; i++)
    {
        sum = 0;
        sum += w[i] * d_in[var] + b[i];
        sum *= beta[i];
//sigmoid函数作为传输函数
        o[i] = 1 / (1 + exp(-1 * sum));
        OutputData += v[i] * o[i];
    }
}

//修改权值以实现迭代
void backUpdate()
{
    change = rand() % 4;
    MC = rand() % neuron;
    //change的值0对应w，1对应v,2对应b，3对应beta
    if (change == 0)
    {
        temp = w[MC];
        w[MC] += 0.2 * ((rand() % 10000 * 2.0) / 10000 - 1);
        if (w[MC] > 1 ) w[MC] = 0.99;
        if (w[MC] < -1) w[MC] = -0.99;
    }
    else if (change == 1)
    {
        temp = v[MC];
        v[MC] = (rand() * 2 / RAND_MAX - 1);
        if (v[MC] == 0) v[MC] = 1;
    }
    else if (change == 2)
    {
        temp = b[MC];
        b[MC] += 0.2 * (rand() % 10000 * 0.0004*Pi - 2*Pi);
        if (b[MC] > 2 * Pi ) b[MC] = 2 * Pi;
        else if (b[MC] < -2 * Pi) b[MC] = -2 * Pi;
    }
    else if (change == 3)
    {
        temp = beta[MC];
        beta[MC] += 0.2 * ((rand() % 10000 * 2.0) / 10000 - 1);
        if (beta[MC] > 1) beta[MC] = 0.99;
        if (beta[MC] < -1) beta[MC] = -0.99;
    }
}

void trainMCNetwork()
{
    int i;
    int c = 0;
    do
    {
        e = 0;
        for (i = 0; i < Data; i++)
        {
            computO(i);
            e += (OutputData - d_out[i])*(OutputData - d_out[i]);
        }
        e = sqrt(e);
        if (e > tempE)
        {
            if (change == 0)
                w[MC] = temp;
            else if (change == 1)
                v[MC] = temp;
            else if (change == 2)
                b[MC] = temp;
            else if (change == 3)
                beta[MC] = temp;
        }
        else tempE = e;
        if (c!=trainteme) backUpdate();
        c++;
        if (c % 1000 == 1) printf("%lf\n", tempE);
    } while (c < traintime);
}

double result(double value)
{
    int i;
    double sum;
    OutputData = 0;
    for (i = 0; i < neuron； i++)
    {
        sum = 0;
        sum += w[i] * value + b[i];
        sum *= beta[i];
        //sigmoid函数作为传输函数        
        o[i] = 1 / (1 + exp(-1 * sum));
        OutputData += v[i] * o[i];
    }
    return OutputData;
}
void main()
{
    tempE = 10000000;
    srand(time(0));
    change = 0;
    data_source();
    read_data();
    initMCNetwork();
    trainMCNetwork();
    data_output();
    printf("end");
    getchar();
}

```

### 高效算法

高效算法采用的方法是只进行一次对全体参数进行训练，并将结果保存。再进行迭代的时候，只对改变量进行迭代，而不是对整个样本进行重新训练，这样能够使得算法快M倍，M是定义的隐藏层维度。

```1c
#ifdef _MSC_VER
#define _CRT_SECURE_NO_WARNINGS
#endif
#define Input_txt "D:\\project\\Deeplearning\\MCsin0V2\\in.txt"
#define Output_txt "D:\\project\\Deeplearning\\MCsin0V2\\out.txt"
#define Result_txt "D:\\project\\Deeplearning\\MCsin0V2\\result.dat"
//训练样本个数
#define Data 15
//输出样本个数
#define OutData 200
#define neuron 200
#define traintime 2000000
#define Pi 3.141592653

#include<math.h>
#include<stdio.h>
#include<stdlib.h>
#include<time.h>

double d_in[Data], d_out[Data];
double w[neuron], v[neuron], o[Data][neuron],beta[neuron],b[neuron];
double OutputData[Data];
double e, tempE, temp;
double temp_out[Data][2];
int MC,change;
double result(double test);

//产生数据源，顺序生成Data个-Pi到Pi以内的数作为输入项，通过计算sin值得到输出项
void data_source()
{
    double s_in[Data], s_out[Data];
    int i;
    double interval;
    FILE *f1, *f2;
    interval = 2 * Pi / (Data - 1);
    for (i = 0; i < Data; i++)
    {
        s_in[i] = -1* Pi+ i * interval;
        s_out[i] = sin(s_in[i]);
    }
    f1 = fopen(Input_txt, "w");
    if (f1 == NULL) printf("file open failed");
    for (i = 0; i < Data; i++)
        fprintf(f1, "%f\n", s_in[i]);
    fclose(f1);
    f2 = fopen(Output_txt, "w");
    for (i = 0; i < Data; i++)
        fprintf(f2, "%f\n", s_out[i]);
    fclose(f2);
}

//读取数据到d_in中和d_out中
void read_data()
{
    FILE *f1, *f2;
    int i;
    f1 = fopen(Input_txt, "r");
    if (f1 == NULL) printf("file open failed!");
    i = 0;
    while (!feof(f1))
    {
        fscanf(f1, "%lf", &d_in[i]);
        i++;
    }
    fclose(f1);
    f2 = fopen(Output_txt, "r");
    if (f2 == NULL) printf("file open failed!");
    i = 0;
    while (!feof(f2))
    {
        fscanf(f2, "%lf", &d_out[i]);
        i++;
    }
    fclose(f2);
}

//结果写到文件
void data_output()
{
    double out_in[OutData], out_out[OutData];
    int i;
    double interval;
    interval = 2 * Pi / (OutData - 1);
    FILE *f1;
    for (i = 0; i < OutData; i++)
    {
        out_in[i] = -1 * Pi + i * interval;
        out_out[i] = result(out_in[i]);
    }
    f1 = fopen(Result_txt, "w");
    if (f1 == NULL) printf("file open failed");
    for (i = 0; i < OutData; i++)
        fprintf(f1, "%f %f %f\n", out_in[i],out_out[i],sin(out_in[i]));
    fclose(f1);
}

//神经网络初始化，对权值进行随机数初始化
void initMCNetwork()
{
    int i,j;
    for (i = 0; i < neuron; i++)
    {
        //第一个权值量
        w[i] = ((rand() %10000 * 2.0) / 10000 - 1);
        //第二个权值量
        v[i] = (rand() * 2 / RAND_MAX - 1);
        if (v[i] == 0) v[i] = 1;
        //偏置量
        b[i] = (rand() % 10000 * 0.0004 * Pi - 2 * Pi);
        //局部量权值
        beta[i] = ((rand() % 10000 * 2.0) / 10000 - 1);
        for (j = 0;j < Data; j++)
            o[j][i] = 0;
//        printf("%lf\n", b[i]);
    }
}

void computO(int var)
{
    int i;
    double sum;
    OutputData[var] = 0;
    for (i = 0; i < neuron; i++)
    {
        sum = 0;
        sum += w[i] * d_in[var] + b[i];
        sum *= beta[i];
//sigmoid函数作为传输函数        
        o[var][i] = 1 / (1 + exp(-1 * sum));
//gauss函数作为传输函数
//        o[i] = exp(-1 * sum * sum);
//tanh函数作为传输函数
//        o[var][i] = (exp(sum) - exp(-1*sum)) / (exp(sum) + exp(-1*sum));
        OutputData[var] += v[i] * o[var][i];
    }
}

//修改权值以实现迭代
void backUpdate() 
{
    int i;
    double ss;
    change = rand() % 4;
    MC = rand() % neuron;
    for (i = 0; i < Data; i++)
    {
        temp_out[i][0] = OutputData[i];
        temp_out[i][1] = o[i][MC];
    }
    for (i = 0; i < Data; i++)
        OutputData[i] -= o[i][MC] * v[MC];
    //change的值0对应w，1对应v,2对应b，3对应beta
    if (change == 0)
    {
        temp = w[MC];
        w[MC] += 0.1 * ((rand() % 10000 * 2.0) / 10000 - 1);
        if (w[MC] > 1 ) w[MC] = 0.99;
        if (w[MC] < -1) w[MC] = -0.99;
    }
    else if (change == 1)
    {
        temp = v[MC];
        v[MC] = (rand() * 2 / RAND_MAX - 1);
        if (v[MC] == 0) v[MC] = 1;
    }
    else if (change == 2)
    {
        temp = b[MC];
        b[MC] += 0.1 * (rand() % 10000 * 0.0004*Pi - 2*Pi);
        if (b[MC] > 2 * Pi ) b[MC] = 2 * Pi;
        else if (b[MC] < -2 * Pi) b[MC] = -2 * Pi;
    }
    else if (change == 3)
    {
        temp = beta[MC];
        beta[MC] += 0.1 * ((rand() % 10000 * 2.0) / 10000 - 1);
        if (beta[MC] > 1) beta[MC] = 0.99;
        if (beta[MC] < -1) beta[MC] = -0.99;
    }
    for (i = 0; i < Data; i++)
    {
        ss = 0;
        ss += w[MC] * d_in[i] + b[MC];
        ss *= beta[MC];
        o[i][MC] = 1 / (1 + exp(-1 * ss));
        OutputData[i] += o[i][MC] * v[MC];
    }
}

void trainMCNetwork()
{
    int i;
    int c = 0;
    for (i = 0; i < Data; i++)
        computO(i);
    do
    {
        e = 0;
        for (i = 0; i < Data; i++)
            e += (OutputData[i] - d_out[i])*(OutputData[i] - d_out[i]);
        if (e > tempE)
        {
            for (i = 0; i < Data; i++)
            {
                OutputData[i] = temp_out[i][0];
                o[i][MC] = temp_out[i][1];
            }
            if (change == 0)
                w[MC] = temp;
            else if (change == 1)
                v[MC] = temp;
            else if (change == 2)
                b[MC] = temp;
            else if (change == 3)
                beta[MC] = temp;
        }
        else tempE = e;
        c++;
        if (c!=traintime)
            backUpdate();

        if (c == 1 || c % 1000 == 0) printf("%d  %lf\n",c,tempE);
    } while (c < traintime);
}

double result(double value)
{
    int i;
    double sum;
    OutputData[0] = 0;
    for (i = 0; i < neuron; i++)
    {
        sum = 0;
        sum += w[i] * value + b[i];
        sum *= beta[i];
//sigmoid函数作为传输函数        
        o[0][i] = 1 / (1 + exp(-1 * sum));
//gauss函数作为传输函数        
//        o[i] = exp(-1 * sum * sum);
//tanh函数作为传输函数
//        o[0][i] = (exp(sum) - exp(-1 * sum)) / (exp(sum) + exp(-1 * sum));
        OutputData[0] += v[i] * o[0][i];
    }
    return OutputData[0];
}

void main()
{
    tempE = 1000000;
    srand(time(0));
    change = 0;
    data_source();
    read_data();
    initMCNetwork();
    trainMCNetwork();
    data_output();
    printf("end");
    getchar();
}

```

