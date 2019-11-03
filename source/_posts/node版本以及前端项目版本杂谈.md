---
title: node版本以及前端项目版本杂谈
tags:
  - node
  - nvm
  - npm
categories:
  - node
copyright: false
keywords: node nvm 
description: node版本对前端项目依赖的版本有着至关重要的影响.
date: 2019-10-24 19:47:30
---

{% cq %}
    node版本以及前端项目依赖版本杂谈
{% endcq %}

<!--more-->

## node简介

服务端js,运行在谷歌v8引擎的js运行时

node主要分两个版本类别: CURRENT和LTS版本,每个版本类别还随着时间的推移有着不同的版本. 

CURRENT为当前发布版本,包含最新功能.

LTS为稳定版本,会得到长期的支持,所以一般开发使用LTS版本

npm为前端最知名包管理工具,为node内置功能.

## nvm (A node.js version management)

由于前端项目模块化进程的到来,每个项目所依赖的模块都有一个当前的版本,但是这些模块又随着时间的推移,修改bug,更新所需的依赖,会有版本的迭代,而node作为js运行时,对前端模块有着深远的影响.

你是否遇到过由于新装电脑node版本,而以前的项目安装依赖报错,而跑不起来?这时候就需要版本控制,以及前端程序员对自己项目运行的环境了如指掌.

### nvm安装

1. 安装之前,把之前安装过的node卸载干净并确保node目录也删掉,并且删除npm安装位置（例如“ C：\ Users <用户> \ AppData \ Roaming \ npm”）,
2. 根据安装环境的不同安装不同版本的nvm:[windows版nvm](https://github.com/coreybutler/nvm-windows/releases)和[mac,linux版nvm](https://github.com/nvm-sh/nvm#installation-and-update)

安装建议使用运行包,免得配置环境变量.

### nvm 使用

nvm arch [32 | 64] 切换node运行在32位还是64位

nvm list [available] 查看可安装node版本

nvm install+版本号/uninstall+版本号/use+版本号 安装指定版本/卸载指定版本/使用指定版本 

nvm on/off/version/proxy [url] 设置代理 

nvm node_mirror https://npm.taobao.org/mirrors/node/ 设置node仓库源

nvm npm_mirror https://npm.taobao.org/mirrors/npm/ 设置npm仓库源

注意:国内环境下,使用nvm install+版本号容易产生node安装成功,但是npm安装失败的情况,解决版本如下
1. 用上面的两个命令设置淘宝源,然后再安装.(家里环境直接用这步就成功了,公司用这个命令也没有成功)
2. 直接去node官网下载相应的免安装解压版本,放进nvm安装目录,解压改成v+版本号的命(例 v12.13.0),然后nvm就能读取到,直接nvm use使用就可以了.

## 项目依赖版本控制(package.json)

在七八月份的ionic4项目中,由于对node版本和package-lock.json文件没有清楚的认识.在项目进行过程中,又有删除package-lock.json文件,和使用cnpm包管理工具等操作,引发了一系列bug.

有时候用cnpm包管理工具安装依赖直接报错,或者安装成功,运行项目时候,直接提示某某模块不存在,而项目无法运行起来.顾在此郑重建议不要使用cnpm版本管理,速度是快,但是容易丢失安装文件(而且好像还没cnpm版本锁?)

还有由于删除版本锁,安装了依赖以后,由于依赖文件的小版本问题,引起部分项目内容产生bug,没有报错,最终经排查对比,确定了是由于package-lock.json文件删除的原因, package-lock.json是对当前依赖的版本进行锁定,以防止由于版本变更引起bug.

在产生bug以后查了很多资料,也了解了相关node及npm的知识,对package-lock.json问题讲解参考了[记package-lock引发的一次事故](https://www.shymean.com/article/%E8%AE%B0package-lock%E5%BC%95%E5%8F%91%E7%9A%84%E4%B8%80%E6%AC%A1%E4%BA%8B%E6%95%85)
