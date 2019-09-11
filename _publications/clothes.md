---
layout: wiki
title: 基于深度学习的个性化服装搭配
categories: 
description: 基于贝叶斯个性化排名（BPR）框架的个性化服装搭配
keywords: 
image: https://i.loli.net/2018/11/26/5bfb51d6de068.png
---

# 基于深度学习的个性化服装搭配
## 服装搭配问题背景

随着时尚产业的蓬勃发展，如何从琳琅满目的服装中搭配出合适的套装越来越成为一些人每天所头疼的问题。近年来，许多研究工作围绕服装搭配展开，现有的工作主要应用深度学习技术对服装的图像或文本进行特征提取，进而对互补服装之间的相容性进行建模。然而现有的研究工作主要针对服装之间的联系，忽略了服装与人之间的联系，所以服装搭配的研究工作的个性化问题亟待解决。

## 参考论文
- [NeuroStylist: Neural Compatibility Modeling for Clothing Matching](https://xuemeng.bitcron.com/mm2017_song.pdf)

- [Deep Neural Networks for YouTube Recommendations](https://storage.googleapis.com/pub-tools-public-publication-data/pdf/45530.pdf)

- [VBPR: Visual Bayesian Personalized Ranking from Implicit Feedback](https://cseweb.ucsd.edu/~jmcauley/pdfs/aaai16.pdf)

## 服装匹配

参考论文[NeuroStylist: Neural Compatibility Modeling for Clothing Matching](https://xuemeng.bitcron.com/mm2017_song.pdf)，通过对服装**图像**和**文本描述**的学习，经过一致性建模，获取服装之间的相关性(匹配程度)

## 用户推荐

参考论文[Deep Neural Networks for YouTube Recommendations](https://storage.googleapis.com/pub-tools-public-publication-data/pdf/45530.pdf)与[VBPR: Visual Bayesian Personalized Ranking from Implicit Feedback](https://cseweb.ucsd.edu/~jmcauley/pdfs/aaai16.pdf)

用户的服装描述了用户的穿衣风格与习惯，通过对多幅图像的学习，能够获得用户的服装搭配风格，将人的个性化加入服装搭配推荐中