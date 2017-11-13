---
layout:     post
title:      "即将结束的2017怎么霍"
subtitle:   " \"Hello World, Hello Myself\""
date:       2017-11-13 13:30:00
author:     "ZJF"
header-img: "img/post-bg-2015.jpg"
catalog: false
tags:
    - 生活
---

> “Emmm.. en en en It's my check ”


## 前言

我终于下定决心并且把写博客这件事落实了，希望自己务必坚持下去。

这是我的博客   ZJF Blog

大学念书的时候也有想过写自己的技术博客，结果不了了之了。

这次的起因是因为Big Boss在猎聘网上浏览到一份前端同学的简历，然后转发给了我们。

进入这位同学的GitHub的博客之后发现....这种极简风格和之前见过的博客还真尼玛不一样诶。

后来了解了使用GitHub & Jekyll搭建个人博客之后才清楚，页面是高度定制化的。

再加上使用Git进行版本控制、Jekyll支持markdown语法的一系列原因让我觉得！

程序员就应该有自己的技术博客并且是这种具备一定技术性的博客。

<p id = "build"></p>
---

## 正文

简单聊聊GitHub & Jekyll创建个人博客的想法～ 

网上关于如何使用GitHub & Jekyll创建个人博客的教程很多并且大多数都很详细
但由于作者会潜意识把自己创建博客中比较顺利的部分讲的不那么详细，所以还真的需要多找几篇教学文档一起看，这博客创建的才能算是顺利。

* **Git**

* **Markdown** 带来的优雅写作体验
* 非常熟悉的 Git workflow ，**Git Commit 即 Blog Post**
* 利用 GitHub Pages 的域名和免费无限空间，不用自己折腾主机
	* 如果需要自定义域名，也只需要简单改改 DNS 加个 CNAME 就好了 
* Jekyll 的自定制非常容易，基本就是个模版引擎


本来觉得最大的缺点可能是 GitHub 在国内访问起来太慢，所以第二天一起床就到 GitCafe(Chinese GitHub Copy，现在被 Coding 收购了) 迁移了一个[镜像](http://huxpro.coding.me)出来，结果还是巨慢。

哥哥可是个前端好嘛！ 果断开 Chrome DevTool 查了下网络请求，原来是 **pending 在了 Google Fonts** 上，页面渲染一直被阻塞到请求超时为止，难怪这么慢。  
忍痛割爱，只好把 Web Fonts 去了（反正超时看到的也只能是 fallback ），果然一下就正常了，而且 GitHub 和 GitCafe 对比并没有感受到明显的速度差异，虽然 github 的 ping 值明显要高一些，达到了 300ms，于是用 DNSPOD 优化了一下速度。



---

配置的过程中也没遇到什么坑，基本就是 Git 的流程，相当顺手

大的 Jekyll 主题上直接 fork 了 Clean Blog（这个主题也相当有名，就不多赘述了。唯一的缺点大概就是没有标签支持，于是我给它补上了。）

本地调试环境需要 `gem install jekyll`，结果 rubygem 的源居然被墙了……后来手动改成了我大淘宝的镜像源才成功

Theme 的 CSS 是基于 Bootstrap 定制的，看得不爽的地方直接在 Less 里改就好了（平时更习惯 SCSS 些），**不过其实我一直觉得 Bootstrap 在移动端的体验做得相当一般，比我在淘宝参与的团队 CSS 框架差多了……**所以为了体验，也补了不少 CSS 进去

最后就进入了耗时反而最长的**做图、写字**阶段，也算是进入了**写博客**的正轨，因为是类似 Hack Day 的方式去搭这个站的，所以折腾折腾着大半夜就过去了。

第二天考虑中文字体的渲染，fork 了 [Type is Beautiful](http://www.typeisbeautiful.com/) 的 `font` CSS，调整了字号，适配了 Win 的渣渲染，中英文混排效果好多了。


## 后记

回顾这个博客的诞生，纯粹是出于个人兴趣。在知乎相关问题上回答并获得一定的 star 后，我决定把这个博客主题当作一个小小的开源项目来维护。

在经历 v1.0 - v1.5 的蜕变后，这个博客主题愈发完整，不但增加了诸多 UI 层的优化（opinionated）；在代码层面，更加丰富的配置项也使得这个主题拥有了更好的灵活性与可拓展性。而作为一个开源项目，我也积极的为其完善文档与解决 issue。

如果你恰好逛到了这里，希望你也能喜欢这个博客主题。

—— Hux 后记于 2015.10


