---
layout: wiki
title: 使用Git编辑课程列表
categories: [cate1, cate2]
description: some word here
keywords: keyword1, keyword2
---

1. 下载安装git，不会的参见[廖雪峰git教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

2. 在指定目录右键 git bash，输入```git clone --recursive https://github.com/sduaicourse/sduaicourse.github.io.git ```

3. 打开_subject/目录下对应title的文件，需修改的内容包括
<img src="https://i.loli.net/2018/11/21/5bf45b984a7f2.png" alt="jieshi.png" title="jieshi.png" />

image项需写入URL地址，建议使用图床[sm.ms](https://sm.ms/)

4.使用markdown编写题目的详细内容，不会的参见[Markdown教程](https://www.jianshu.com/p/280e2ef4069e)
编写过程中的图片，文档，视频等都建议使用链接导入，图片可以使用[sm.ms](https://sm.ms/)，文档和视频可以使用Google Doc的链接

5.编辑完成后在git bash中输入
```
git pull origin master
git add *
git commit -m "upgrade subject lists"
git push origin master
```
然后会提示输入账号密码，账号：sduaicourse 密码：aicourse2018,即可完成对网页的修改
如果遇到 git push 报错：remote: Permission to XXXA/xxxx.git denied to XXXB，可参考[教程](https://blog.csdn.net/u012832088/article/details/78928576)解决
