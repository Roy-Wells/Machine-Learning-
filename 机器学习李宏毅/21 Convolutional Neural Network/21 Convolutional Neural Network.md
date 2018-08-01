# Convolutional Neural Network 卷积神经网络

[TOC]

### CNN的整个架构

首先将一张图片上传——>卷积层接受之后，处理进入到 Max Pooling【最大池化 】（可以反复多次,需要事先决定）——>Flatten——>Fully Connected Feedforward network——>得到结果

![1533025385753](D:\面试md\机器学习李宏毅\21 Convolutional Neural Network\21_CNN整个架构)

在整个观察中我们会做三个观察：

1. 识别某些模块要比整张图片小很多
2. 同样的模块可能会出现在不同的区域
3. 对像素进行二次调整将不会改变这个类型

而在这三个观察所处的架构位置如下：

![1533025700740](D:\面试md\机器学习李宏毅\21 Convolutional Neural Network\21_CNN三个观察所在流程位置)

### CNN—Convolution

假设我们有一张黑白图片，该黑白图片的格式如下为0，1组成的6*6的矩阵。而假设有多个3 * 3的filter矩阵，其中选取一个filter，对黑白图片进行匹对计算，同时filter在黑白矩阵中计算，以每次移动一个单位进行计算，最后得到一个新的4*4的image矩阵。![1533026737569](D:\面试md\机器学习李宏毅\21 Convolutional Neural Network\21_Convolution黑白)

我们可以看到在经过filter1之后的计算匹对之后，左上角与左下角的两个部分是符合filter的部分，因此这个过程中是用来判断**观察2**的。而有多少filter，就将会有多少个更新之后的image图片。

如果是彩色的图片，因为我们知道彩色图片都是RGB三种格式组成，因此我们可以分为三层矩阵。同样filter也是三层矩阵。最后再进行计算。并且这三层矩阵并不是分开计算，而是考虑到一起，合并计算。

![1533027078451](D:\面试md\机器学习李宏毅\21 Convolutional Neural Network\21_Convolution彩色)