---
title: Hexo从零搭建博客
date: 2020-01-23 23:19:52
tags: [笔记]
---

hexo版从零搭建个人博客
======================

<!--more-->

> > 从零搭建自己的博客 hexo版
> > ===================================================================================
> >
> > [B站教程](https://www.bilibili.com/video/av44544186)
> >
> > 准备：Git Node.js
> > --------------------------------------------------------------
> >
> > (以下全在DOS窗口执行)
> > ---------------------------------------------------------------------
> >
> > 安装npm：npm install -g cnpm –registry=[https://registry.npm.taobao.org](https://registry.npm.taobao.org) （安装镜像提速）
> > --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
> >
> > 安装hexo：npm install -g hexo-cli
> > ----------------------------------------------------------------------------------------------------------
> >
> > 准备博客目录blog：(出错可直接删除重新开始)
> > -------------------------------------------------------------------------------------------------------------------------------------
> >
> > > 1.初始化： hexo init 生成各种文件
> > >
> > > 2.启动： hexo s [本地访问](http://localhost:4000/)
> > >
> > > 3.写博客： hexo n “标题” 自动生成并在blog下，格式为：.md
> >
> > > > md语法：[简书](https://www.jianshu.com/p/399e5a3c7cc)
> >
> > > 4.清理： hexo clean
> > >
> > > 5.生成： hexo g
> >
> > 部署到GitHub上
> > --------------------------------------------------
> >
> > > 1.创建仓库：用户部署个人博客的github仓库的命名需符合规范：
> >
> > > > 用户名 + .github.io
> >
> > > 2.git部署插件：npm install hexo-deployer-git –save
> > >
> > > -   npm audit fix
> > > -   npm audit fix –force
> > >
> > > 3.设置 \_config.yml文件
> > >
> > > > 最后面增加配置：![img1](https://github.com/ZephXu07/IMG/raw/master/UC%E6%88%AA%E5%9B%BE20190821141914.png)
> >
> > > > -   三个冒号后面需要一个空格！！！！！！！！！
> > >
> > > 4.部署到远端： hexo d
> >
> > 更换主题（演示）[主题网站](https://hexo.io/themes/)
> > -----------------------------------------------------------------------------------------------------------
> >
> > > 1.git clone他人主题： git clone https://…… themes（主题存储文件夹）/（主题名）（链接）
> > >
> > > > git clone 慢，两种方法：
> > > >
> > > > > [第一种](https://blog.csdn.net/TeFuirnever/article/details/99110367)
> > > > >
> > > > > [第二种](https://blog.csdn.net/zhouchangyu1221/article/details/86613081)
> >
> > > 2.修改\_config.yml 配置：![img2](https://github.com/ZephXu07/IMG/raw/master/UC%E6%88%AA%E5%9B%BE20190821145114.png)
> > >
> > > 冒号后面可能也需要空格！！！！！！！！！！！！！！！！
> > >
> > > 3.后续操作：
> > >
> > > > hexo clean
> > > >
> > > > hexo g
> > > >
> > > > hexo s
> > > >
> > > > 本地停止（ctrl + c）
> > > >
> > > > hexo d

修改
--------------------

- 缺失模块。
  1、请确保node版本大于6.2
  2、在博客根目录（注意不是yilia根目录）执行以下命令：
  npm i hexo-generator-json-content –save

- 3、在根目录\_config.yml里添加配置

  ```yml
  jsonContent:
    meta: false
    pages: false
    posts:
      title: true
      date: true
      path: true
      text: false
      raw: false
      content: false
      slug: false
      updated: false
      comments: false
      link: false
      permalink: false
      excerpt: false
      categories: false
      tags: true
  ```

  

  

