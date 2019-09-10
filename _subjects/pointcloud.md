---
layout: wiki
title: 基于点云数据的语义分割
categories: 
description: 自动驾驶，机器人？三维的世界快来探索吧！
keywords: 
image: https://i.loli.net/2019/09/10/39qn1hb4trwyGpV.png
---

# 基于点云数据的语义分割

#### 点云

点云是一组点的集合, 常用来表示自身维度比背景空间纬度低的数据(比如空间中的曲面等)。 由于数据较为稀疏, 直接采用密集体素的方式, 不仅数据量大, 而且数据中包含过多的冗余信息, 不利于数据特征的提取。 不仅如此， 大量的3D传感器也采用点云的方式保存数据, 数据来源非常广泛。![QQ截图20180709154302.png](https://i.loli.net/2019/09/10/WFPhOn6QyDfEkLj.png)

## 数据集

* Semantic3D  

This benchmark closes the gap and provides a large labelled 3D point cloud data set of natural scenes with over 4 billion points in total. It also covers a range of diverse urban scenes: churches, streets, railroad tracks, squares, villages, soccer fields, castles to name just a few. The point clouds we provide are scanned statically with state-of-the-art equipment and contain very fine details. Our goal is to help data-demanding methods like deep neural nets to unleash their full power and to learn richer 3D representations than it was ever possible before.[网址](<http://www.semantic3d.net/>)

* KITTI数据集
  

KITTI数据集是由德国卡尔斯鲁厄理工学院和美国丰田技术研究院联合建立,主要用于立体视觉,光流,视觉测距等视觉任务,该数据集基于自动驾驶平台Annieway开发,其中的激光扫描仪的最大测量距离是120m,在深度估计任务中,该数据集中能够提供93000对RGB图像和深度图像.[网址](<http://www.cvlibs.net/datasets/kitti/index.php>)

* SUN RGB-D数据集

 In this paper, we present an RGB-D benchmark suite for the goal of advancing the state-of-the-art in all major scene understanding tasks. Our dataset is captured by four different sensors and contains 10,000 RGB-D images, at a similar scale as PASCAL VOC. The whole dataset is densely annotated and includes 146,617 2D polygons and 58,657 3D bounding boxes with accurate object orientations, as well as a 3D room layout and category for scenes. [项目](<http://rgbd.cs.princeton.edu/>)

## 实现方法

### 例子：PointCNN

山东大学李扬彦、卜瑞、孙铭超、陈宝权研究团队研究提出的PointCNN是简单通用的点云特征学习架构，基于这一方法一组神经网络模型一举刷新了五个点云基准测试的记录。 

论文地址：https://arxiv.org/abs/1801.07791 

由山东大学提出的PointCNN是一个简单通用的点云特征学习架构。基于这一方法的一组神经网络模型一举刷新了五个点云基准测试的记录。

CNN成功的关键在于其卷积操作能够很好地从基于规则域表示的数据中提取局部信息。然而，由于点云数据的不规则和无序性，使得卷积操作由于输入数据顺序的不稳定很难直接应用到点云数据上。

为了解决这个问题，PointCNN提出了一种称为X-变换的方法。X-变换是从输入点学习到的一组权值X，这组权值可以对各点相关联的特征进行重新加权和排列。 X-变换可以实现“随机应变”，即当输入点的顺序变化时, X能够相应地变化，使加权和排列之后的特征近似不变。输入特征在经过X-变换的处理之后能够变成与输入点顺序无关同时也编码了输入点形状信息的归一化的特征。在经过X-变换之后的特征上进行卷积能够极大提高卷积核的利用率, 从而大大提高卷积操作在无序数据上提取特征的能力。

**PointCNN**

PointCNN提出了一个称为X-变换的方法来解决在点云上难以有效实现卷积的问题。

![](../img/wpsBE72.tmp.jpg)

由于卷积操作本身的有序性, 对于上图中ii, iii, iv三组点, 如果把它们以i的方式进行卷积操作, 会得到以下三个输出。

![img](../img/wpsBE83.tmp.jpg)

 

对于ii和iii, 由于四个点的空间位置不一样, 我们希望进行卷积后产生的输出也会不一样。 但实际上, 直接进行卷积操作时ii和iii都被映射到了同样的位置, 因此产生的输出也完全一样, 这是不合理的。 另一方面, 对于iii和iv, 其数据完全一致, 但由于顺序不一样, 进行卷积后结果也通常会不一样, 这也不是我们所期望的。 因此, 直接对无序的点云数据进行卷积并不高效。

由于点云的无序性特点, PointCNN期望能够得到一种变换, 使得

![img](../img/wpsBE93.tmp.jpg)

中, ii和iii不同, 且iii和iv相同。

​PointCNN采用了学习权重的方式, 这里Xs是一个4x4的矩阵, 由a, b, c, d四个点的坐标经过一个子网络F得到, 即Xs = F(a, b, c, d)。

通过学习, 我们期望得到的矩阵能够满足 ![img](../img/wpsBEA4.tmp.png), 且![img](../img/wpsBEA5.tmp.png), 其中![img](../img/wpsBEA6.tmp.png)是和(a, b, c, d)与(c, a, b, d)对应的列变换矩阵, 即, 使得![img](../img/wpsBEA7.tmp.png)。

事实上, 在实验中, 学习到的MLP并不能完全满足上面的理想情况下的要求。 尽管如此, PointCNN还是得到了良好的效果。

细节上, PointCNN采用KNN选取临近点进行卷积; 将点的坐标信息进行处理添加到特征中作为其一部分; 通过随机采样等方式降低数据空间分辨率。

**实验结果**

1.classification accuracy on ModelNet40 (91.7%)

2.classification accuracy on ScanNet (77.9%)

3.segmentation part averaged IoU on ShapeNet Parts (86.13%)

4.segmentation mean IoU on S3DIS (62.74%)

5.per voxel labelling accuracy on ScanNet (85.1%)

![img](../img/wpsBEC9.tmp.jpg)

![img](../img/wpsBECA.tmp.jpg)



![](../img/QQ截图20180709154334.png)

**特别值得一提的是，在ModelNet40的分类任务上，在只使用32个点作为输入的极端压力测试下，PointCNN仍然能够取得84.4%的准确率，这一结果大幅领先目前已知的其他方法。在这种极端压力测试下，PointCNN的计算量非常小，能够在GTX 1080GPU上以每帧0.3毫秒的速度进行点云识别。自动驾驶中获取的点云往往非常稀疏，同时对实时性要求极高。该压力测试显示PointCNN有应用于自动驾驶的巨大潜力。**



**X-变换的进一步理解**

虽然X-Conv是被设计用来进行在三维点云上进行卷积, 并且它在实验中展示了最新水准的结果, 但是我们对他它背后的理论仍然知之甚少, 尤其是当它被用于深层神经网络上时, 我们的理解还十分的有限。

PointCNN采取了最简单也是最直接的方式来学习X-Conv——用一个子网络来学习变换矩阵。 虽然一般的矩阵可以用来实现权值和顺序变换, 但是这种方法是否是实现目标的最简形式仍然是不得而知的。 相比于此前的其他方法, PointCNN的参数更少, 但还是在部分小规模的数据上表现出了过拟合的问题。 X-Conv在带来强大的表征能力的同时, 可能也携带了大量额外的自由度。找到一种比一般的矩阵更加精炼的可以学习的表达形式或许是X-Conv发展的方向。

## 开源代码

[PointNet++](<https://github.com/charlesq34/pointnet2>)

[PointCNN](<https://github.com/yangyanli/PointCNN>)

[pointSIFT](<https://github.com/MVIG-SJTU/pointSIFT>)

## 参考文献

[PointNet++: Deep Hierarchical Feature Learning on Point Sets in a Metric Space](<http://stanford.edu/~rqi/pointnet2/>)

[PointCNN: Convolution On X-Transformed Points](<https://arxiv.org/abs/1801.07791>)

[PointSIFT: A SIFT-like Network Module for 3D Point Cloud Semantic Segmentation](<https://arxiv.org/abs/1807.00652>)