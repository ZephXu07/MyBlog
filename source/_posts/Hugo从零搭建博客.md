---
title: Hugo从零搭建博客
date: 2020-01-23 23:20:32
tags: [笔记]
---

hugo版从零搭建个人博客
======================

<!--more-->

[B站教程](https://www.bilibili.com/video/av51574688)

> 1：在[此处](https://github.com/gohugoio/hugo/releases)地址下找到Windows压缩文件下载
>
> 2:如何看hugo安装成没成功，打开cmd，输入hugo version
>
> 3：安装成功后，用Hugo来创建自己的博客，命令：hugo new site myblog
> 注：myblog为文件夹名字
>
> 4:下载设置主题，去[主题网址](https://themes.gohugo.io/)选择自己喜欢的主题进行下载
>
> 5.下载主题
> ![img](https://github.com/ZephXu07/IMG/raw/master/1033328-20190513110131643-1221757335.pn)
>
> 6.启动博客命令，输入 hugo server -t m10c –buildDrafts
>
> 7.创建文章，在根目录下创建，hugo new post/（名字）.md
>
> 8.md文档语法：
>
> [md语法](https://www.jianshu.com/p/399e5a3c7cc5)
>
> 9.部署远端：
>
> > 1.仓库：![img3](https://github.com/ZephXu07/IMG/raw/master/UC%E6%88%AA%E5%9B%BE20190822213904.png)
> >
> > 2.仓库已经有了，但是个空仓库，接下来敲命令hugo –theme=m10c
> > –baseUrl=”地址” –buildDrafts，
> >
> > 3.成功后会在根目录下生成一个public文件，把这个public传到github仓库
> >
> > > cd public/
> > >
> > > git init
> > >
> > > git add .
> > >
> > > git commit -m”相关信息”
> > >
> > > git remote add origin
> > > [https://github.com/ZephXu07/zephxu07.github.io.git](https://github.com/ZephXu07/zephxu07.github.io.git)
> > >
> > > git push -u origin master

> > 4.访问：[个人博客](https://zephxu07.github.io/)