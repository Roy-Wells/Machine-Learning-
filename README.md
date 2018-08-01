# -
常见的机器学习知识以及其他面试知识汇总
[TOC]

### 举例

<font size="3">

![eg1](eg1.png)

#### 1. 模型确立
假设初始创建模型如下类的表示，则有无穷多的模型公式
![eg1](eg1_model.png)
而线性模型可以视为
$$y=b+\sum_{i=1}^n w_ix_i\\x_i:x{cp},x{hp},x{w},x{h}……
$$

#### 2. 样本确立
**符号说明：**
$$
x^i表示第i个训练样本的自变量\\

y^i 表示第i个训练样本的标签\\

x_j表示自变量的第j个元素
$$

![eg1_trainingData](eg1_trainingData.png)

#### 3. 构建损失函数
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;而在得到了训练数据集，以及确定了某些函数模型（function），就需要用损失函数（loss function）来衡量这些模型。
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;我们假设所创建的模型为
$$
y=b+w*x_{cp}
$$
​	则损失函数可以设定为
$$
L(f)=\sum{i=1}^{10} \bigr(y^n-f(x{cp}^n)\bigr)^2\\
即通过标签$y^n$与函数$f(x_{cp}^n)$ 所预测出的值进行减法处理获取差异值。\\得到所有样本的差异值的平方相加则为损失函数的值。
$$
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;而L(f) 中的f表示的是函数模型集中的
$$
y=b+w*x_{cp}\\
其中的变量有关的是w、b，因此可以将损失函数改动为L(w,b)。\\则损失函数的公式为：\\

L(f)=\sum{i=1}^{10} \bigr(y^n-(b+w*x{cp}^n)\bigr)^2
$$
其中的变量有关的是w、b ，因此可以将损失函数改动为L(w,b)。则损失函数的公式为：
$$
L(f)=\sum{i=1}^{10} \bigr(y^n-(b+w*x{cp}^n)\bigr)^2
$$


![eg1_lossfunction](eg1_lossfunction.png)

#### 4. 挑选最优函数模型
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在创建了损失函数之后，我们按照损失函数对所有的模型进行测试
并确定不同参数下损失函数的值。根据这个值来挑选最优的函数模型。<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;已知损失函数确立后，最优的函数模型的损失函数值最小。
因此我们可以创建一个函数$f^*$ 来求得使损失函数值最小化的函数模型：
$$
f^*=argmin_{f}L(f)\\
其中f表示的y=b+w*x_{cp}。
$$
因此我们可以等价替换为
$$
w^*,b^*=argmin_{(w,b)}L(w,b)
$$
即求能将损失函数最小化的$w，b$的值。
$$
w^*,b^*=argmin_{(w,b)}L(w,b)
$$

$$
\qquad\quad\qquad\quad\qquad\qquad=argmin{(w,b)}\sum{i=1}^{10} \bigr(y^n-(b+w*x_{cp}^n)\bigr)^2
$$

#### 5. 梯度下降（Gradient Descent）
梯度下降的方法步骤：<br>
（假设只有一个参数$w$）
* 随机挑选一个初值$$

* 计算
  $$
  \frac{dL}{dw}|{w=w^0\\}(对w^0设置一个初值)
  $$
  ,并且更迭 
  $$
  w^1\leftarrow w^0-\color{red}{\eta}\frac{dL}{dw}|_{w=w^0}\\
   （其中的 \eta被称作学习率）
  $$

  

* 计算
  $$
  \frac{dL}{dw}|{w=w^1},\\并且更迭 w^2\leftarrow w^1-\color{red}{\eta}\frac{dL}{dw}|{w=w^1}
  $$

* ……多次迭代

* 得到最终优化参数值

（假设有两个参数$w,b$）
* 随机挑选一个初值$w^0,b^0$

* 计算
  $$
  \frac{\partial L}{\partial w}|{w=w^0,b=b^0}\\\frac{\partial L}{\partial b}|{w=w^0,b=b^0}
  $$
  ,并且更迭<br>
  
  $$
  w^1\leftarrow w^0-\color{red}{\eta}\frac{\partial L}{\partial w}|_{w=w^0,b=b^0}\\
  b^1\leftarrow b^0-\color{red}{\eta}\frac{\partial L}{\partial b}|_{w=w^0,b=b^0}
  $$
  

  （其中的 $\eta$被称作学习率）

* 计算 
  $$
  \frac{\partial L}{\partial w}|{w=w^1,b=b^1}$, $\frac{\partial L}{\partial b}|{w=w^1,b=b^1}
  $$
  ,并且更迭<br>


  $$
  w^2\leftarrow w^1-\color{red}{\eta}\frac{\partial L}{\partial w}|_{w=w^1,b=b^1}\\
  b^2\leftarrow b^1-\color{red}{\eta}\frac{\partial L}{\partial b}|_{w=w^1,b=b^1}
  $$

* ……多次迭代
  *得到最终优化参数值<br>

根据原式：
$$
L(w,b)=\sum{i=1}^{10} \bigr(y^n-(b+w*x{cp}^n)\bigr)^2
$$
我们可以对其进行偏微分：
$$
\frac{\partial L}{\partial w}=\sum{i=1}^{10}2 \bigr(y^n-(b+w*x{cp}^n)\bigr)*(-x_{cp}^n)\\
\frac{\partial L}{\partial b}=\sum{i=1}^{10}2 \bigr(y^n-(b+w*x{cp}^n)\bigr)*(-1)
$$


而在不断地进行各种模型进行样本测试之后，可以发现如下的
![eg1_modelselectio](eg1_modelselection.png)
因此我们发现当变量幂的次数为3时，对测试数据有更好的拟合效果。

#### 5. 正则化
正则化表示如下：
$$
L=\sum_{i=1} \bigr(y^n-(b+\sum w_i*x_i)\bigr)^2+\sum (w_i)^2\\
通过 \sum (w_i)^2将L函数变得更平滑。
$$

选用正则化的原因是：因为在大多数情况下更平滑的函数更趋于正确
