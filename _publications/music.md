---
layout: wiki
title: 基于深度学习的音乐推荐系统
categories: 
description: 应用深层神经网络来解决在含有隐性反馈的基础上进行推荐的关键问题——协同过滤，构建相应的框架并借此根据用户的评分记录来向用户推荐最有可能与其相关的音乐。
keywords: 
image: https://i.loli.net/2018/11/26/5bfb586d14bcd.jpg
---

# 基于深度学习的音乐推荐系统 #

## 背景简介 ##
音乐是较为贴近大家生活的一个领域，在如今这个互联网时代，各类的音乐网站提供了成千上万的音乐，满足不同人群对音乐的需求，但面对海量的音乐人们却需要花费更多时间和精力去寻找符合自己兴趣的音乐。而音乐推荐系统的出现能够帮助用户更快找到他们寻求的目标，这种推荐服务不仅能给庞大的用户群体带来良好的使用体验，更能提升该音乐产品的竞争力，给对应的公司带来可观的商业利益。

![图片1.png](https://i.loli.net/2018/11/26/5bfb4692ec63d.png)

当前主流的推荐算法分别为基于内容的推荐和基于协同过滤的推荐这两大类，这是国内外大多数音乐网站或电台采用的技术。这两种技术都有自己的局限性，基于内容的方法处理数据的复杂度高，而基于协同过滤的方法则存在冷启动和数据稀疏性的问题。但近年来，随着深度学习的火热兴起，这两种算法都有了新的发展。

## 数据集 ##
数据集采用从yahoo网站
（ https://webscope.sandbox.yahoo.com/catalog.php?datatype=r&guccounter=1 ）
下载的R3数据集（该网站其他类似数据集也可采用），内包含有15400个用户对1000首歌曲的近300000条评分。300000个样本每个样本的形式为：用户ID--歌曲ID--评分，评分分为1-5五个层级，5分即对某首音乐的最高评分。每个用户至少有10个评分。
![数据集.jpg](https://i.loli.net/2018/11/26/5bfb4d92c08fd.jpg)


## 实现方法 ##
此次项目仅探究深度学习下的协同过滤推荐方法,参照何向南博士的《神经协同过滤》（NCF)构造一个通用框架用两条路线来对用户和项目建模。

按照评价项目推荐性能的要求，采用leave-one-out方法进行评估。所以得预先人为对数据集进行一定的处理。从每个用户的评分音乐中随机抽出一首音乐出来，由这些抽取出来的的样本组成test集（含有15400个条目），剩下的没有被抽到的所有样本都作为train集。此外还构建了negative集，及对于每个用户随机抽取99个不与该用户有所交互的音乐，与该用户在test集中交互的音乐组成一个包含有100个项目的样本。

运用多层感知机（MLP)来学习用户和项目潜在特征之间的相互作用,最终输出输入用户和输入项目相关的可能性大小,依此可以得到对于每个用户的前十位相关的音乐并将其作为对该用户推荐的结果。如果有余力的话，也可以尝试将广义矩阵分解（GMF）和MLP结合的方法来实现推荐，看对应的优化后二类熵交叉函数是否更小。

#### NCF框架 ####
![神经协同过滤（NCF）框架.jpg](https://i.loli.net/2018/11/26/5bfb4aae374e1.jpg)

#### GMF和MLP的结合 ####
![GMF和MLP的结合.jpg](https://i.loli.net/2018/11/26/5bfb52d9f1d99.jpg)

#### 待优化二类熵交叉函数 ####
![二类熵交叉函数.jpg](https://i.loli.net/2018/11/26/5bfb5904bc684.jpg)

## 开源代码 ##
[neural_collaborative_filtering](https://github.com/hexiangnan/neural_collaborative_filtering)

## 参考文献 ##
[推荐算法综述](http://ir.sdu.edu.cn/~zhuminchen/RS/yangbo2011.pdf)

[Neural Collaborative Filtering](https://www.comp.nus.edu.sg/~xiangnan/papers/ncf.pdf)

[Fast Matrix Factorization for Online Recommendation with Implicit Feedback](https://www.comp.nus.edu.sg/~xiangnan/papers/sigir16-eals-cm.pdf)





