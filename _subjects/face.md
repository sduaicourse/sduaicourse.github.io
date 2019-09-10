---
layout: wiki
title: 人脸检测
categories: 
description: 换脸很火？你也可以试试，开始你的人脸检测任务
keywords: 
image: https://i.loli.net/2019/09/10/umklQUCe3E4ZNjI.png
---

# 人脸检测算法

* 人脸检测是机器视觉领域被深入研究的经典问题，在安防监控、人证比对、人机交互、社交等领域都有重要的应用价值。数码相机、智能手机等端上的设备已经大量使用人脸检测技术实现成像时对人脸的对焦、图集整理分类等功能，各种虚拟美颜相机也需要人脸检测技术定位人脸，然后才能根据人脸对齐的技术确定人脸皮肤、五官的范围然后进行美颜。在人脸识别的流程中，人脸检测是整个人脸识别算法的第一步。

![图片2.png](https://i.loli.net/2019/09/10/cFmLgXDRiYfQMeh.png)

## 数据集

* **LFW**

全名是Labeled Faces in the Wild.这个数据集是人脸评估一定会用到的一个数据集，包含了来自1680的13000张人脸图，数据是从网上搜索来的。基本都是正脸。这个数据集也是最简单的，基本主流算法都能跑到99%以上，貌似有6对label错了，所以最高正确率应该是99.9%左右。这个都跑不到99%的话别的数据集表现效果会更差。一般来说这个数据集是用来做人脸识别验证的。

* **CelebFaces**

总共包含10177个人的202599张图片，也是从搜索引擎上爬过来的,噪声不算多，适合作为训练集。同时这个数据对人脸有一些二元标签，比如是否微笑，是否戴帽子等。如果需要特定属性的人脸，也可以从中获取。

* **CASIA-WebFace**

该数据集是从IMBb网站上搜集来的，含10K个人的500K张图片。同时做了相似度聚类来去掉一部分噪声。CAISA-WebFace的数据集源和IMDb-Face是一样的，不过因为数据清洗的原因，会比IMDb-Face少一些图片。噪声不算特别多，适合作为训练数据。

- **VGG-Face**

来自2622个人的2百万张图片。每个人大概要2000+图片，跟MS-Celeb-1M有很多重叠的地方（因为都是从搜索引擎来的），这个数据集经常作为训练模型的数据，噪声比较小，相对来说能训练出比较好的结果。

## 实现方法

### 早期方法

早期的人脸检测算法使用了模板匹配技术，即用一个人脸模板图像与被检测图像中的各个位置进行匹配，确定这个位置处是否有人脸；此后机器学习算法被用于该问题，包括神经网络，支持向量机等。以上都是针对图像中某个区域进行人脸-非人脸二分类的判别。

## 深度学习框架

举例MTCNN

MTCNN顾名思义是多任务的一个方法，它将人脸区域检测和人脸关键点检测放在了一起，同Cascade CNN一样也是基于cascade的框架，但是整体思路更加巧妙合理，MTCNN总体来说分为三个部分：PNet、RNet和ONet，如下图所示：

![TIM截图20190910193632.png](https://i.loli.net/2019/09/10/qbsAuUWRrZFB3vw.png)

MTCNN在测试第一阶段的PNet是全卷积网络（FCN），全卷积网络的优点在于可以输入任意尺寸的图像，同时使用卷积运算代替了滑动窗口运算，大幅提高了效率。

除了增加人脸5个关键点的回归任务，另外在calibration阶段采用了直接回归真实位置坐标的偏移量的思路替代了Cascade CNN中的固定模式分类方式，整个思路更为合理。

![TIM截图20190910193640.png](https://i.loli.net/2019/09/10/VvL6WZRaXb4Ii7j.png)

MTCNN的整体设计思路很好，将人脸检测和人脸对齐集成到了一个框架中实现，另外整体的复杂度得到了很好的控制，可以在中端手机上跑20~30FPS。该方法目前在很多工业级场景中得到了应用。



## 开源代码

[Face recognition using Tensorflow](<https://github.com/davidsandberg/facenet>)

[Reproduce MTCNN using Tensorflow](<https://github.com/AITTSMD/MTCNN-Tensorflow>)

[OpenFace](<https://github.com/cmusatyalab/openface>)

## 参考文献

[Improved Selective Refinement Network for Face Detection](<https://arxiv.org/abs/1809.02693v1>)

[Joint Face Detection and Alignment Using Multitask Cascaded Convolutional Networks](<https://arxiv.org/abs/1604.02878>)

[FaceNet: A Unified Embedding for Face Recognition and Clustering](<https://arxiv.org/abs/1503.03832>)