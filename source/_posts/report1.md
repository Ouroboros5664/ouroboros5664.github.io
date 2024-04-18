---
title: 静态网页博客总结
categories: 开源软件开发与社区治理
tags:
- 实验报告
sticky: 100 # 置顶
pic: /images/thumb/thumb_6.webp
comments: flase
toc: flase
only:
- home
- category
- tag
---
## 博客主题及其选取原因
博客主题：[Kratos-Rebirth](https://github.com/Candinya/Kratos-Rebirth/tree/master)
![博客主题演示](/images/theme-demo.png)
选取原因：
- 功能全面：包含了首页、文章列表、文章详情功能，且能根据文章所属分类和标签展示文章，“关于”页面可以仿照着自己实现
- UI清晰：整个页面功能块分布明确，UI设计符合用户的习惯和直觉，界面元素应该易于识别和操作，且具备一定的美观性
- 使用指南较为完善：项目给出了较为完整的[使用指南](https://github.com/Candinya/Kratos-Rebirth/blob/master/Kratos-Rebirth-Manual.md)，更便于上手
## 博客页面布局及其设计思路
### 首页
首页由顶部导航栏、顶部横幅、博客列表、汇总信息组成，左下角有音乐播放器，右下角有搜索功能和light/night切换等功能，下滑后还有回到顶部功能。修改后的博客页面基本保留了原有样式，在原基础上增添了“关于”页面，给出了博客作者的相关信息，删除了不需要的“好伙伴”页面和“链接”页面，除此之外对全部图片进行了替换，并且增加了一些博客来充实整体。
![当前博客首页](/images/blogpage.png)
### 博客详情页
博客详情页与首页大致相同，不同之处在于博客列表区域被替换为了博客详情页，右侧的汇总信息增加了当前博客的目录结构，目录结构也可选择不显示。
![博客详情页](/images/blogdetail.png)
## 博客功能实现及其技术选择
### 配置过程
博客选择使用hexo框架实现，在安装完所需工具后，使用如下命令安装脚手架工具：
``` bash
$ npm install -g hexo-cli
```
新建一个hexo项目，命名为myblog：
``` bash
$ hexo init myblog
```
进入myblog文件夹，安装依赖：
``` bash
$ cd myblog
$ npm install
```
### 修改过程
#### 主题配置
将选择的主题kratos-rebirth通过git clone命令拉到myblog/theme文件夹中：
``` bash
$ cd theme
$ git clone git@github.com:Candinya/Kratos-Rebirth.git
```
编辑_config.yml，修改title、language、theme等信息：
``` bash
title: MyBlog
author: Ouroboros
language: zh-CN
theme: kratos-rebirth
```
复制主题中的_config.html到myblog目录下，并重命名为_config.kratos.rebirth.yml，并修改导航栏如下，并且注释掉不需要的功能（如friends部分）：
``` bash
topMenu:
  - label: 首页
    icon: home
    url: /
  - label: 档案馆
    icon: file
    url: /archives/
  - label: 关于我
    icon: user
    url: /about/
```
#### 内容修改
##### 新建博客文章
1. 在myblog/source/_posts目录下新建md文件，作为博客文章
2. 编辑博客文章的头部信息，title为文章标题，categories为文章分类，tags为文章标签，sticky为文章权重，值越大文章排序越靠前，pic指定首页下文章对应的图片，comments为评论功能，当前已关闭，only指示了当前页面在首页、分类、标签下是否显示
``` bash
---
title: 静态网页博客总结
categories: 开源软件开发与社区治理
tags:
- 实验报告
sticky: 100 # 置顶
pic: /images/thumb/thumb_5.webp
comments: flase
toc: flase
only:
- home
- category
- tag
---
```
##### 图片替换
- images/thumb文件夹下的图片为文章对应的各个图片
- images文件夹下：
    - about.webp为右侧边栏头像上方的背景图
    - avatar.webp为头像图片
    - banner.webp为light模式下的横幅图片
    - banner_dark.webp为night模式下的横幅图片
    - bg.webp为light模式下的背景图片
    - bg_dark.webp为night模式下的背景图片
将上述图片全部替换为自己的即可
##### about页面的实现
在_config.kratos.rebirth.yml中，已经配置了about页面的url：
``` bash
topMenu:
  - label: 首页
    icon: home
    url: /
  - label: 档案馆
    icon: file
    url: /archives/
  - label: 关于我
    icon: user
    url: /about/
```
只需在source文件夹下新增about页面，并新增一个markdown文件，作为关于我的页面的实现
## 博客制作过程中遇到的问题及其解决方法
### about页面的书写
- 图片路径应该为/images/thumb/thumb_5.webp之类，而不是images/thumb/thumb_5.webp
- 一开始不太清楚关于页面如何实现，后来发现要在source文件夹下新建一个about文件夹，对应了/about/的url
