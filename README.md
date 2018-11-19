---
layout: wiki
title: Guide
categories: tools
description: 主页、团队、成果维护指南
keywords: Guide
---

> 终于做的差不多了

这次整理的主要是三部分 主页、团队、成果，这三部分都是用markdown维护的，只要修改对应markdown里面的内容就行

### 主页

主页的位置在 \pages\home.md, 我在主页里加了一个gallery，目前都是盗别人的图 图片的地址在 \images\slide里面，换掉就行。主页的内容有待丰满，谁有空帮忙更一下

### 团队
团队页面在\pages\team.md 里面的内容也要做适当修改

团队的主要信息是用YML维护的和markdown差不多，位置在 \_data\memebers.yml, 写法参照下面

``` html
- name: Doohee Cho
  photo: Doohee2.jpg
  info: Postdoc, started May 2017
  email: dooheecho80@gmail.com
  github: 3dincrement.github.io
  number_educ: 4
  education1: B.S. Yonsei University, Korea
  education2: PhD Yonsei University, Korea with <a href="http://web.yonsei.ac.kr/nano/%ED%95%99%EA%B3%BC%EC%86%8C%EA%B0%9C.htm">In-Whan Lyo</a>
  education3: Postdoc POSTECH with <a href="http://caldes.ibs.re.kr/html/caldes_en/">Han Woong Yeom</a>
  education4: Postdoc Rutgers with <a href="http://rcem.rutgers.edu/">Sang-Wook Cheong</a>
```

其中照片需要放在 images\teampic\ 里面, number_educ 不超过5。

Besides,为大家留了一个个人主页空间，在 \memeber\ 目录下建立和自己名字命名的markdown文件即可,附带留言功能， do whatever you want。

### 成果
成果页面在 \pages\publications.md 最好也改一下

成果目前只做了论文部分，类似于团队，成果也是用YML维护的，位置在\_data\publists.yml 里面，具体用法参考已有实例。照片最好放teaser，否则太长了。pdf、video 最好在主目录下新建file video文件夹，然后链接

### 更新内容两种方法
###	推荐方法
用自己账户fork repo [3dincrement18.github.io](https:// 3dincrement18.github.io)，修改完了之后pull request。这样做好处是不会发生版本冲突，也不会因为不适当修改崩溃

### 另一种方法
直接git clone 到本地，修改后再提交上去。

``` shell
git clone --recursive https://github.com/3dincrement/3dincrement.github.io.git
cd 3dincrement18.github.io
git config user.name "3dincrement"
git config user.email "3dincrement@gmail.com"
...
git add .
git commit - m "some thing you what"
git push origin master
```






