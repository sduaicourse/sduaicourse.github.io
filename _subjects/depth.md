---
layout: wiki
title: 基于单目图像的深度估计
categories: 
description: 此处应写对问题的简述
keywords: 
image: https://pic4.zhimg.com/v2-f9f2a9b644a96f1b06ca5a1d081759c2_1200x500.jpg
---

# 基于单目图像的深度估计

基于颜色图像估计深度图是计算机视觉的一个基本问题,传统的深度估计方法主要是基于立体视觉的原理.即通过两张立体视觉(双目)图像中对应像素的视差来进行计算,基于单张图像估计深度图在理论上是不可行的

* 实际效果

![实际效果](https://pic4.zhimg.com/v2-f9f2a9b644a96f1b06ca5a1d081759c2_1200x500.jpg "实际效果")

## 数据集

* Marked3D数据集  

Maked3D数据集由斯坦福大学的Saxena等人构建,使用包含激光扫描仪的能够同时获取RGB图像和对应深度图的移动拍摄系统,共包含了534对RGB图像和深度图.其中,所有的图像都是白天的城市风景和自然风光场景,其中400对RGB图像和深度图作为训练数据,其余134对作为测试数据,在该数据集中,深度的范围为5-81m,由激光扫描仪的最大探测距离决定.

* KITTI数据集
  
KITTI数据集是由德国卡尔斯鲁厄理工学院和美国丰田技术研究院联合建立,主要用于立体视觉,光流,视觉测距等视觉任务,该数据集基于自动驾驶平台Annieway开发,其中的激光扫描仪的最大测量距离是120m,在深度估计任务中,该数据集中能够提供93000对RGB图像和深度图像.

* NYU depth-V2数据集

该数据集由纽约大学Silberman等人创建,使用的微软的Kinect相机收集室内场景的RGB信息和深度信息,NYU depth-V2数据集包括了1449对RGB图像和深度图,在深度估计任务中,人们通常使用795对作为训练数据,654对用于测试数据,深度范围为0.5-10m

## 实现方法

### 基于传统数据驱动的方法

首先使用采集的数据建立数据库，从数据库中提取与单张图像相似度的top k图像，这里k=7，相似性度量是基于knn方法的gist和optical flow，然后将区域相似图像调整为点相似，这里的调整方法为sift flow方法，最后进行估计

### 基于全卷积残差网络的监督学习

cnn监督学习：

1. 基于已经有深度层的rgbd数据集

2. 将反卷积与残差结合起来，网络分为前面的resnet—50和后面的反卷积层和反池化层

3. 使用了小卷积代替大卷积的方式实现了上采样，可以减小棋盘效应，保留更多的边缘信息，同时具有了更快的度

4. 使用huber loss，具有更好的鲁棒性

### 基于左右一致性检测的无监督学习

cnn非监督学习：使用双目图像作为训练集，将左图利用神经网络恢复为右图，使之误差最小。我们可以将该问题视作回归问题，而该方法将回归问题变为了重建问题，即利用左图产生左视差，再利用左视差产生右视差。（视差：视差就是从有一定距离的两个点上观察同一个目标所产生的方向差异。从目标看两个点之间的夹角，叫做这两个点的视差角，两点之间的连线称作基线。只要知道视差角度和基线长度，就可以计算出目标和观测者之间的距离。）

1. 基于双目视觉图像数据集

2. 可以将深度预测问题视作回归问题，将左图恢复为右图，右图恢复为左图，进行一致性检测

3. 无需深度ground truth信息

4. 利用卷积神经网络，将监督的回归问题，转化成了非监督的重建问题，最小化重建误差。就是左边
warp到右边，右边warp到左边。然后求重建误差最小。

## 开源代码

[非参数深度估计 https://github.com/CielChen/DepthEstimation](https://github.com/CielChen/DepthEstimation)

[CNN监督学习 https://github.com/iro-cp/FCRN-DepthPrediction](https://github.com/iro-cp/FCRN-DepthPrediction)

[CNN非监督学习 https://github.com/mrharicot/monodepth](https://github.com/mrharicot/monodepth)

## 参考文献

[Depth Extraction from Video Using Non-parametric Sampling](https://www.semanticscholar.org/paper/Depth-Transfer%3A-Depth-Extraction-from-Video-Using-Karsch-Liu/3d57515445c00c635e15222767fc0430069ed200)

[Deeper Depth Prediction with Fully Convolutional Residual Networks](https://www.semanticscholar.org/paper/Deeper-Depth-Prediction-with-Fully-Convolutional-Laina-Rupprecht/7449cff9a37e1c64080d97b6971f94c29b31fd30)

[Unsupervised Monocular Depth Estimation with Left-Right Consistency](https://www.semanticscholar.org/paper/Unsupervised-Monocular-Depth-Estimation-with-Godard-Aodha/84c01c9760cd294718bd7c4b4c93596db1e5e068)