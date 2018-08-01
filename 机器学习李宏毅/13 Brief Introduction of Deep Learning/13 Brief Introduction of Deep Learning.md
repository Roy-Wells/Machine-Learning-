[TOC]

### 深度学习三步

![1530931685898](D:\面试md\机器学习李宏毅\13 Brief Introduction of Deep Learning\13_深度学习三步)

而在第一步设置的函数大部分是神经网络（Neural Network）。

### 神经网络

![1530934649866](D:\面试md\机器学习李宏毅\13 Brief Introduction of Deep Learning\13_神经网络1)

我们可以将神经网络看成，多个逻辑回归交叉转换形成的一个算法模型。单一的一个逻辑回归我们将其视为一个神经。不同的连接方法将会生成不同的神经网络结构。

**神经网络参数**：神经网络中所有的**权重（weight）**和**偏差(biases)**

#### 1.确定神经网络的连接方法

#####  前馈神经网络（Fully Connect Feedforward Network）

定义：

![1530936151946](D:\面试md\机器学习李宏毅\13 Brief Introduction of Deep Learning\13_前馈神经网络模型)

这个就是一个简单的函数模型。而一个简单的神经网络例子如下所示：

![1530935751284](D:\面试md\机器学习李宏毅\13 Brief Introduction of Deep Learning\13_前馈神经网络例子)

###### 矩阵运算(Matrix Operation)

神经网络的运算我们往往会用矩阵运算来进行操作。

![1530947776316](D:\面试md\机器学习李宏毅\13 Brief Introduction of Deep Learning\矩阵运算1)

而对于整个神经网络的计算方式，可以视为下图的计算方式

![1530948185879](D:\面试md\机器学习李宏毅\13 Brief Introduction of Deep Learning\矩阵运算2)

##### 如何神经网络结构的设计

![1530948785524](D:\面试md\机器学习李宏毅\13 Brief Introduction of Deep Learning\神经网络问题)

#### 2.判断函数的好坏

通过使用损失函数，计算预测结果与样本标签的交叉熵。从而判断函数的好坏。

![1530948987488](D:\面试md\机器学习李宏毅\13 Brief Introduction of Deep Learning\损失函数1)

这是计算一个样本的损失函数，而整个样本集的损失函数则如下图所示

![1530949039283](D:\面试md\机器学习李宏毅\13 Brief Introduction of Deep Learning\损失函数2)

#### 3.使用梯度下降

在选择确定了函数之后，则进行梯度下降来确定最优参数。

![1530949540538](D:\面试md\机器学习李宏毅\13 Brief Introduction of Deep Learning\梯度下降)