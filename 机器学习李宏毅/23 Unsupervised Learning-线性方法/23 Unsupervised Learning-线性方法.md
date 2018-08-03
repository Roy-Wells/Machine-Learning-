## 23 Unsupervised Learning-线性方法

[TOC]

### 无监督学习

无监督学习分为两类：

* clustering & Dimension（化繁为简）聚类（**主要**）
* Generation（无中生有）生成

#### 聚类

* k—means
* Hierarchical Agglomerative Clustering(HAC)层次聚类 





在做聚类的时候，我们有一个约束：每一个对象必须要属于一个类型。

##### 维数缩减

当为了是问题简单化，我们往往会选择通过某些特定的函数将维度降低。

![1533115719035](D:\面试md\机器学习李宏毅\23 Unsupervised Learning-线性方法\23_demension reduction)

通过特定的函数之后的z的维度将会比x的维度要更少一点。

常用的一些方法有：

* 简单根据特征选择。

* PCA

（PCA）详细解释见http://blog.codinglabs.org/articles/pca-tutorial.html

