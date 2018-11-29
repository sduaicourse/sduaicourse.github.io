---
layout: wiki
title: 深度跨模态哈希检索
categories: 多媒体检索
description: 基于层次化标签的深度跨模态哈希检索，充分利用多媒体数据的层次化标签信息，指导哈希算法对多媒体数据的编码，从而进一步提高其检索效率
keywords: 多媒体 跨模态 深度学习 哈希检索 层次结构
image: https://i.loli.net/2018/11/29/5bff55e7df991.png
---

__一、课题的背景及目的__  
  **1、课题背景**  
  近年来，多媒体数据的急剧增加为实现跨模态检索（如以文本搜索图片）带来全新的挑战。为此，哈希学习算法被广泛应用于跨模态检索领域。该学习算法旨在通过将多媒体数据有效地映射到汉明空间中，大大降低了检索的复杂度，提高检索准确率。    
  
  同时，随着深度学习技术在诸多研究领域取得的巨大成功，现有工作，如DCMH、DCH和SHDH，也初步探索了利用深度学习技术对多媒体数据进行哈希编码的可能。然而现有工作主要集中于非监督的哈希编码，即忽略了多媒体数据的标签信息，尤其是层次化的标签结构信息，忽略了存储在层次结构中的丰富信息。例如在服装领域的数据集中，服装图片可以被标记为上衣，T恤，下衣，短裙，牛仔裤等等。而事实上，这些标签存在着一定的层次化结构。因此，如何充分利用多媒体数据的层次化标签信息，指导哈希算法对多媒体数据的编码，从而提高其检索效率成为值得我们的深入关注。   
	
  **2、研究目的**  
  在现有的其他的跨模态检索的模型算法基础上进行创新改进，进一步提高检索的MAP（搜索平均准确率）。实际应用方面，充分利用数据集的层次化标签信息以及深度学习的技术，实现分层标签数据的跨模态哈希检索。还可以继续与分类任务结合，实现多任务训练工作。

__二、课题相关研究历程与状况__  
![pic01.png](https://i.loli.net/2018/11/29/5bff572bcca3e.png)
  **a) 图像Hash算法：**  
  对于图像检索问题，为了解决对存储空间和检索时间的高要求，以近似最近邻搜索（approximate nearest neighbor search）技术发展迅猛，因为其对空间和时间的需求大幅降低，而且能够得到不错的检索结果，因此成为了一种实用的替代方案。在这其中，哈希（hashing）作为一种代表性方法，近年来受到了广泛的关注。  
	
  **b) 图像深度哈希算法：**  
  最早的基于深度学习的哈希算法应该是2009年由Hinton研究组提出的Semantic Hashing方法。对于这个方法来说，深度模型只是提供了一定的非线性表示能力，而网络的输入仍是手工设计的特征，和现在通常意义上的深度学习算法还是有一定的区别。  
  
  2014年受到CNN强大学习能力的鼓舞，深度哈希发展迅速。同年，中山大学的潘炎老师研究组和颜水成老师合作，在美国人工智能协会年会（AAAI 2014）上发表的论文提出了一种名为CNNH（Convolutional Neural Network Hashing）的方法，把基于CNN的深度哈希算法推到了前台。  
  
  2015年，有四篇基于深度学习的哈希算法。在这四篇文章之中，其中一篇文章（使用手工设计特征作为输入之外，其余的三篇均为完全的端到端模型。  
  
  第一篇文章与上面介绍的CNNH一样，同样是来自中山大学的潘炎老师研究组和颜水成老师。因为这篇文章中使用了一个比CNNH中的网络深得多的Network in Network的网络结构，因此被简称为NINH（NIN Hashing）或DNNH（Deep Neural Network Hashing）。  
  
  第二篇文章来自中科院自动化研究所的谭铁牛老师的研究组，和DNNH相比没有在网络结构上下太大功夫，而是更多地关注了损失函数这一块。文章中使用了类似于DeepID2的网络结构，对于图像检索任务，目的是把数据库中的图像，按照和查询图像的相关性由大到小的顺序，依次返回。基于这个思想，这篇文章中提出直接让网络学习这个排序，因此该方法称为DSRH（Deep Semantic Ranking Hashing）。这种做法相当于直接对最终的评测指标进行优化，直接优化排序并不容易，因此作者使用了一个凸上界作为替代，进行优化。  
  
  第三篇文章来自台北中央研究院的陈祝嵩研究组，其中使用了一种比较直接的方法来学习二值编码，该方法名为DLBHC（Deep Learning of Binary Hash Codes）。  
  
  同年，由中山大学林倞老师、哈尔滨工业大学左旺孟老师和香港理工大学张磊老师等人合作的文章发表在当年的Transactions on Image Processing (TIP 2015)中，作者提出了一种使用加权Hamming距离代替标准Hamming距离的哈希方法DRSCH（Deep Regularized Similarity Comparison Hashing）。  
  
  总结：以上四篇文章中的框架，可以代表大多数深度哈希文章的做法，可以总结为：深度模型学习图像表示 + sigmoid/tanh函数限制输出范围 + 不同的损失函数 + （可选）有针对性的网络结构。  

  **c) 深度跨模态哈希：**  
  跨模态检索。一个最常见的例子是：在搜索引擎中输入一些关键词，找相关的图像。通常来说，关键词（文本）和图像并不在同一个空间中，因此无法直接比较。  在2016年年初，李武军老师带领的研究团队发布了一篇文章，介绍了一种跨模态深度哈希算法DCMH（Deep Cross-Modal Hashing）。这篇文章中，作者利用一个两路的深度模型将两种不同模态的数据（文章中是文本和图像）变换到一个公共空间，并要求相似的样本在这个公共空间中相互靠近。通过同时对图像和图像、图像和文本、文本和文本这几种不同类型的样本对施加这个约束，可以保证两种模态样本的对齐。如此一来，即可实现在公共空间中的跨模态检索（对于文本搜文本，深度哈希也有比较好的效果）。  
  
  基于层次化标签的深度跨模态哈希检索目前发布的相关研究不多，可以参考的有Supervised Deep Hashing for Hierarchical Labeled Data

__三、课题主要内容__  
  **1、主要创新点**  
	（1）将层次哈希应用到跨模态检索中，改善已有的模型  
	（2）在分类的时候使用层次结构，并将哈希的过程与分类的过程这两个任务一起训练

__四、主要参考文献资料__  
[1] Qing-YuanJiang, Wu-JunLi. Deep Cross-Modal Hashing. arXiv:1602.02255.  
[2] Devraj Mandal Kunal N. Chaudhury Soma Biswas. Generalized Semantic Preserving Hashing for n-Label Cross-Modal Retrieval. Indian Institute of Science, Bangalore – 560012  
[3] DCH: http://cfm.uestc.edu.cn/~fshen/pub.html/  
[4] SHDH: Supervised Deep Hashing for Hierarchical Labeled Data*  
https://www.researchgate.net/publication/315835894_Supervised_Deep_Hashing_for_Hierarchical_Labeled_Data  
DCMH参考代码：https://github.com/jiangqy/DCMHCVPR2017/tree/master/DCMH_tensorflow/DCMH_tensorflow  
DCH参考代码:http://cfm.uestc.edu.cn/~fshen/pub.html(在该网页中找到2017年对应的论文)  

