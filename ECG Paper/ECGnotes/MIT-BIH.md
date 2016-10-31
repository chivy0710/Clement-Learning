# Physio Bank

## MIT-BIH Arrhythmia Database 心律失常数据库

数据采集从1975年开始，在Boston's Beth Israel Hospital采集。在1980年完善并且部署。

on 9-track half-inch digital tape at 800 and 1600 bpi, and on quarter-inch IRIG-format FM analog tape.
在9轨道半英尺数字胶带(应该是采样所用的记录纸等信息)

包含48个半小时双通道非固定的心电图数据摘录，即每个数据记录的是半小时的心电图数据。

23个记录从4000个24小时非固定的ECG信号随机选择，4000个数据中60%是住院病人，40%是门诊病人。剩下的25个记录也是从同一个数据集中选取的，选择的是那些在小的随机样本中不能很好表征的虽不具备明显的一般性但临床心律失常特征明显的数据。**保证数据覆盖更多的类型。**

对于每个病人的数据分为3个文件，后缀为atr的标签文件，后缀为dat的数据文件，后缀为hea的头文件。

### 头文件

[.hea]为头文件，其由一行或多行ASCII码字符组成。以100.hea为例

文件名 导连数 采样频率 采样点总数
100 2 360 650000
*第一个信号*
数据文件名 数据存储格式 信号的增益(200ADC uints/mV) 分辨率 ADC零值 第一采样点值 校验数 - 采样导连
100.dat 212 200 11 1024 995 -22131 0 MLII
*第二个信号*
数据文件名 数据存储格式 信号的增益(200ADC uints/mV) 分辨率 ADC零值 第一采样点值 校验数 - 采样导连
100.dat 212 200 11 1024 1011 20052 0 V5
*注释行*
患者年龄 性别 记录数据
\# 69 M 1085 1629 x1
患者用药情况
\# Aldomet, Inderal

### 数据文件

[.dat]为数据文件，采用特殊的二进制方式存储，可通过工具转换为txt文件。

记录被数字化，在11-bit分辨率10mv的范围上，每秒每通道有360个样本。即采样频率360Hz(标准临床心电图为50Hz)，650000个采样点，采集的是30分钟的数据。采样的ADC(数模转换)值以1024为0V，ADC值除以200得到的是以mv为单位的电压值。故对于一个ADC值，先减去1024，然后除以200即可得到其电压值。

数据有两个信号，对应的是MLII以及V5导连。

### 标签文件

Record 100 (MLII, V5; male, age 69)

Medications: Aldomet, Inderal
Beats	Before 5:00	After 5:00	Total
Normal	367	1872	2239
APC	4	29	33
PVC	-	1	1
Total	371	1902	2273
Supraventricular ectopy
33 isolated beats
Rhythm	Rate	Episodes	Duration
Normal sinus rhythm	70-89	1	30:06
Signal quality	Episodes	Duration
Both clean	1	30:06
Points of interest:

11:03 Normal sinus rhythm
25:13 PVC
26:09 APCs
27:55 Normal sinus rhythm


每个数据由两个或以上的心脏病医师独立的贴上标签，不同意见的标签被重新决定从而得到的每个记录都是计算机可读的标签(总共大约有110，000个)。


#### 注释代码

说明


|注释代码|简写|说明|中文翻译|
|--------|--------|--------|------------|
|0||No TQRS||
|1|N|Normal beat | 正常搏动|
|2|L|Left bundle branch block beat|左束支传导阻滞|
|3|R|Right bundle branch block beat|右束支传导阻滞|
|4|A|Atrial premature beat|房性早搏|
|5|a|Aberrated atrial premature beat|异常房性早搏|
|6|V|Premature ventricular contraction|室性早搏|
|7|F|Fusuion of ventricular and normal beat|心室融合心跳|
|8|J|Nodal (junctional) premature beat|交界性早搏|
|9|j|Nodal (junctional) escape beat|交界性逸搏|
|10|S|Supraventricular premature or ectopic beat|室上性早搏或异常|
|11|E|Ventricular escape beat|室性逸搏|
|12|e|Atrial escape beat||
|13|/|Paced beat|起搏心跳|
|14|Q|Unclassifiable beat|未分类心跳|
|15|B|Left or right bundle branch block||
|16|r|R-on-T premature ventricular contraction||
|17|n|Supraventricular escape beat (atrial or nodal)||
|18|f|Fusion of paced and normal beat||
|19|?|Beat not classified during learning||


**Non-beat annotations:**

    Code	Description
    [		Start of ventricular flutter/fibrillation
    !		Ventricular flutter wave
    ]		End of ventricular flutter/fibrillation
    x		Non-conducted P-wave (blocked APC)
    (		Waveform onset
    )		Waveform end
    p		Peak of P-wave
    t		Peak of T-wave
    u		Peak of U-wave
    `		PQ junction
    '		J-point
    ^		(Non-captured) pacemaker artifact
    |		Isolated QRS-like artifact [1]孤立的类QRS伪迹
    ~		Change in signal quality [1] 信号质量发生变化
    +		Rhythm change [2]
    s		ST segment change [2]
    T		T-wave change [2]
    *		Systole
    D		Diastole
    =		Measurement annotation [2]
    "		Comment annotation [2]
    @		Link to external data [3]