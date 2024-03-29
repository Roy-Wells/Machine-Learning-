[TOC]

#### 逻辑回归第一步：函数设置

根据上一章可知我们需要确定样本的是它的几率
$$
P_{w,b}(C_1|x),\\
如果P_{w,b}(C_1|x)\geqslant0.5，那么输出C_1\\
否则，输出C_2\\
假如我们使用的是高斯分布来确定几率的话，那么有\\
P_{w,b}(C_1|x)=\sigma(z)\\
其中\sigma (z)=\frac1{1+exp(-z)}\\
z=w*x+b=\sum w_ix_i+b
因此，我们的函数为\\
f_{w,b}(x)=P_{w,b}(C_1|x)
$$
如果我们用图像来表示模型流程的话，如下所示

![](D:\面试md\机器学习李宏毅\11 logistic regression\11_设置函数流程.png)



#### 逻辑回归第二步：函数的优劣比较

在第一步已经确立模型之后，假设已经有了训练集

![](D:\面试md\机器学习李宏毅\11 logistic regression\11_训练数据.png)

假设这组训练集的结果是由
$$
f_{w,b}=P_{w,b}(C_1|x)产生的，\\
那么给定一个w,b就决定了这个模型函数，而生成如上整组训练集的结果的概率为\\
L(w,b)=f_{w,b}(x^1)f_{w,b}(x^2)(1-f_{w,b}(x^1))…f_{w,b}(x^N)\\
而能够让L(w,b)最大化的w,b两个参数，我们取为w^*,b^*\\
则有w^*,b^*=argmax_{w,b}L(w,b)
$$
已知
$$
L(w,b)=f_{w,b}(x^1)f_{w,b}(x^2)(1-f_{w,b}(x^1))…f_{w,b}(x^N)\\
w^*,b^*=argmax_{w,b}L(w,b)
$$
我们可以通过转换，将公式转化为
$$
w^*,b^*=argmin_{w,b}-lnL(w,b)
$$
因为函数取对数并不改变函数的性质。而转换后的函数更容易计算。

而假设C1类型标为1，C2类型标记为0.通过计算可以知道函数变化如下：

![1530676835568](D:\面试md\机器学习李宏毅\11 logistic regression\11_公式变化)

通过简化之后则有
$$
-lnL(w,b)=lnf_{w,b}(x^1)lnf_{w,b}(x^2)ln(1-f_{w,b}(x^1))…\\
=\sum_n-[y^nlnf_{w,b}(x^n)+(1-y^n)ln(1-f_{w,b}(x^1))]
$$

#### 逻辑回归第三步：寻找最优函数

已知损失函数为：
$$
-lnL(w,b)=\sum_n-[y^nlnf_{w,b}(x^n)+(1-y^n)ln(1-f_{w,b}(x^1))]
$$
那么可以使用梯度下降来进行求解，即对w,b进行偏微分梯度下降更迭。前面已知
$$
f_{w,b}(x)=P_{w,b}(C_1|x)=\sigma(z)=\frac1{1+exp(-z)}\\
其中z=w*x+b=\sum_i w_ix_i+b
$$
因此我们对w，b求偏微分，可以等价视为

函数左边的偏微分：

![1530677940227](D:\面试md\机器学习李宏毅\11 logistic regression\11_w的偏微分)

函数右边的偏微分：

![1530690410141](D:\面试md\机器学习李宏毅\11 logistic regression\11_w的偏微分2)

经过整理之后，我们得到的对w进行梯度下降的偏微分，结果如下：

![1530691061020](D:\面试md\机器学习李宏毅\11 logistic regression\11_w的偏微分总)



#### 逻辑回归于线性回归的区别

![1530691132652](D:\面试md\机器学习李宏毅\11 logistic regression\11_逻辑回归和线性回归的区别)

#### 交叉熵VS平方差

##### 交叉熵

###### 1.信息量

交叉熵（cross entropy）是常用的一个概念，一般用来求目标与预测值之间的差距。 交叉熵是信息论中的一个概念，要想了解交叉熵的本质，需要先从最基本的概念讲起。 

首先是信息量。假设我们听到了两件事，分别如下：  

事件A：巴西队进入了2018世界杯决赛圈。  

事件B：中国队进入了2018世界杯决赛圈。  

仅凭直觉来说，显而易见事件B的信息量比事件A的信息量要大。究其原因，是因为事件A发生的概率很大，事件B发生的概率很小。所以当越不可能的事件发生了，我们获取到的信息量就越大。越可能发生的事件发生了，我们获取到的信息量就越小。 

![1530776267024](D:\面试md\机器学习李宏毅\11 logistic regression\11_信息量)

###### 2.熵

![1530776384797](D:\面试md\机器学习李宏毅\11 logistic regression\11_熵.png)

###### 3.相对熵

相对熵又称KL散度,如果我们对于同一个随机变量 x 有两个单独的概率分布 P(x) 和 Q(x)，我们可以使用 KL 散度（Kullback-Leibler (KL) divergence）来衡量这两个分布的差异 。

在机器学习中，P往往用来表示样本的真实分布，比如[1,0,0]表示当前样本属于第一类。Q用来表示模型所预测的分布，比如[0.7,0.2,0.1]  直观的理解就是如果用P来描述样本，那么就非常完美。而用Q来描述样本，虽然可以大致描述，但是不是那么的完美，信息量不足，需要额外的一些“信息增量”才能达到和P一样完美的描述。如果我们的Q通过反复训练，也能完美的描述样本，那么就不再需要额外的“信息增量”，Q等价于P。 

![1530786014654](D:\面试md\机器学习李宏毅\11 logistic regression\11_KL散度)

![1530786557836](D:\面试md\机器学习李宏毅\11 logistic regression\相对熵与交叉熵.png)

###### 4.为什么要用交叉熵做loss函数？

见逻辑回归使用平方差。

交叉熵可在神经网络(机器学习)中作为损失函数，p表示真实标记的分布，q则为训练后的模型的预测标记分布，交叉熵损失函数可以衡量p与q的相似性。交叉熵作为损失函数还有一个好处是使用sigmoid函数在梯度下降时能避免均方误差损失函数学习速率降低的问题，因为学习速率可以被输出的误差所控制。

##### 逻辑回归使用平方差

假设我们使用平方差来计算损失函数并且进行梯度下降，将会出如下的情况

![1530758220116](D:\面试md\机器学习李宏毅\11 logistic regression\11_逻辑回归平方差)

即当使用平方差的时候，对于某一个样本的标签，无论预测结果是否准确，偏微分都将为0，对于距离很远的样本，这样的估计是不准确的。

![1530758462133](D:\面试md\机器学习李宏毅\11 logistic regression\11_交叉熵与平方差的三维图)

如果使用交叉熵，距离越远的点，将会下降的更快，而距离越近的点，下降速度减缓。而如果使用的是平方差，距离远的点下降速度将会非常缓慢。

#### 生成模型(Generative)和判别模型(Discriminative)

##### 生成模型

**生成模型**估计的是**联合概率分布**（joint probability distribution），p(y, x)=p(y|x)*p(x)，由数据学习联合概率密度分布P(X,Y)，然后求出条件概率分布P(Y|X)作为预测的模型，即生成模型：P(Y|X)= P(X,Y)/ P(X)。基本思想是首先建立样本的联合概率概率密度模型P(X,Y)，然后再得到后验概率P(Y|X)，再利用它进行分类。生成方法关心的是给定输入x产生输出y的生成关系。 

![1530806500184](D:\面试md\机器学习李宏毅\11 logistic regression\生成模型1.png)

![1530806543606](D:\面试md\机器学习李宏毅\11 logistic regression\生成模型2.png)

##### 判别模型

**判别模型**估计的是**条件概率分布**(conditional distribution)， p(y|x)，是给定观测变量x和目标变量y的条件模型。由数据直接学习决策函数y=f(X)或者条件概率分布P(y|x)作为预测的模型。判别方法关心的是对于给定的输入X，应该预测什么样的输出Y。 

例如：比如说要确定一只羊是山羊还是绵羊，**用判别模型**的方法是先从历史数据中学习到模型，然后通过提取这只羊的特征x来预测出这只羊f(X)是山羊的概率，是绵羊的概率。**用生成模型**的方法是我们可以根据山羊的特征首先学习出一个山羊模型，然后根据绵羊的特征学习出一个绵羊模型。然后从这只羊中提取特征，放到山羊模型P(w1|X)中看概率是多少，再放到绵羊模型P(w2|X)中看概率是多少，如果P(w1|X)>P(w2|X)，那么我们就认为X是属于w1类，即该羊属于山羊。 

再例如：比如说你的任务是识别一个语音属于哪种语言。例如对面一个人走过来，和你说了一句话，你需要识别出她说的到底是汉语、英语还是法语等。那么你可以有两种方法达到这个目的：**用生成模型**的方法是学习每一种语言，你花了大量精力把汉语、英语和法语等都学会了，我指的学会是你知道什么样的语音对应什么样的语言。然后再有人过来对你说话，你就可以知道他的语言对应什么语言；**用判别模型**的方法是不去学习每一种语言，你只学习这些语言模型之间的差别，然后再分类。意思是指我学会了汉语和英语等语言的发音是有差别的，我学会这种差别就好了。

![1530806390413](D:\面试md\机器学习李宏毅\11 logistic regression\判别模型.png)

![1530806330858](D:\面试md\机器学习李宏毅\11 logistic regression\判别模式与产生模式的区别.png) 

#### 多分类模型（3类为例）

![1530762143091](D:\面试md\机器学习李宏毅\11 logistic regression\11_多分类模型流程图)

对于多分类模型，按照上述的流程，对于一个测试样本x进行z1,z2,z3三个模型函数的计算，并且通过softmax方法，将计算结果转化成y1,y2,y3，并与测试样本中原有的标签进行交叉熵计算。最后根据交叉熵所计算出的结果，来判断x的分类。

##### 级联逻辑回归模型

当存在样本没办法通过一根直线直接将样本进行逻辑分类，那么这个时候可以通过级联逻辑回归模型，将样本转换之后再进行分类。

![1530763776640](D:\面试md\机器学习李宏毅\11 logistic regression\11_级联逻辑回归分类)

一个逻辑回归的输入可以来源于其他逻辑回归的输出，这个逻辑回归的输出也可以是其他逻辑回归的输入。把每个逻辑回归称为一个 **Neuron（神经元）**，把这些神经元连接起来的网络，就叫做 **Neural Network（神经网络）**。 









