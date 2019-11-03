---
title: node项目升级ts笔记
tags:
  - babel
  - js
  - nodejs
  - typescript
categories:
  - js
copyright: false
keywords: babel,ts,node,
description: nodejs项目升级使用es6语法,到使用升级ts实录.
date: 2019-11-02 21:41:05
---


<!--more-->

## 为什么要升级node项目.

本人自认为,TypeScript是js的未来,也对构建大型项目比较友好,在写node,koa小项目时突然想到了一个问题,为什么不能用import引入项目依赖呢,接下来引发了一系列思考.也决定对项目进行升级.刚开始的思路是升级到es6版本.但是后来想了想,何不一步到位,直接升级到ts呢.下面是升级过程,

## 升级es6利器babel.

babel是一个js代码编译工具.js是一个不断发展的语言,有各个版本,还有不同的运行环境(浏览器环境,nodej环境),以及不同的浏览器环境(ie,firefox,chrome,等等).最新的es6代码以及ts代码等,不能直接在浏览器上运行,有的浏览器实现了es6的标准,但有些没有,所以就要通过babel来编译代码成es5的.

之前也使用过babel,但认知还停留在引入依赖,编写配置文件阶段,没有认真深入研究.今天遇到了一个问题,在写node项目时,因为node采用的是Commonjs的[模块规范](https://blog.csdn.net/Real_Bird/article/details/54869066),使用的都是require引入模块,但我发现有的项目就是使用import引入的,这时候就需要引入babel.

## node中引入babel

### babel6用法

1. 在package.json中加入依赖,npm安装()


``` base

"dependencies": {
    "babel": "^6.23.0",
    "babel-cli": "^6.24.1",
    "babel-core": "^6.24.0",
    "babel-preset-es2015": "^6.24.0",
    "babel-preset-stage-3": "^6.22.0",
    "babel-register": "^6.24.0",
},
 "devDependencies": {
    "babel-plugin-transform-async-to-generator": "^6.24.1",
    "babel-plugin-transform-es2015-classes": "^6.24.1",
    "babel-plugin-transform-es2015-modules-commonjs": "^6.24.1",
    "babel-plugin-transform-export-extensions": "^6.22.0",
  }


```

2. 添加配置文件.babelrc

``` base
{
  	"presets": ["stage-3"],
  	"plugins": [
  		"transform-async-to-generator",
        "transform-es2015-modules-commonjs",
        "transform-export-extensions"
    ]
}

```

3. 在加载node项目app.js之前先引入babel-core/register,新建index.js

``` base
require('babel-core/register');
require('./app.js');

```
4. 把原来的运行app.js,改成运行index.js


### [babel7用法](https://blog.csdn.net/weixin_34357887/article/details/91466569)

1. 安装babel7

``` base
npm install --save-dev @babel/core @babel/cli @babel/preset-env @babel/node

```

2. 新建.babelrc

``` base 
{  
"presets": ["@babel/preset-env"]
}

```
3. 更新package.json

``` base 
scripts": {    
        "start": "nodemon --exec babel-node src/server.js",    
        "build": "babel src --out-dir dist",    
        "serve": "node dist/server.js"  
     },  
    "author": "",  
    "license": "MIT",  
    "dependencies": {  },  
    "devDependencies": {    
        "@babel/cli": "7.4.3",    
        "@babel/core": "7.4.3",    
        "@babel/node": "7.2.2",    
        "@babel/preset-env": "7.4.3",    
        "nodemon": "1.18.11"  
      }}
```
[babel相关文档](https://juejin.im/post/5b87cab1e51d4538ac05dc54)

## 升级ts

[相关资料](https://www.jianshu.com/p/0b7ff3c38e0e)

1. 报错''ts-node'' 不是内部或外部命令，也不是可运行的程序

    解决办法:全局安装  
    
``` base
    npm install -g cross-env –save-dev
```
    在原来的命令前面添加package.json

``` base 
    cross-env NODE_ENV=development nodemon --watch 'app/**/*' -e ts --exec 'ts-node' app.ts
```
2. ts中nodemon无效, 

    使用ts-node-dev模块代替

3. npx 运行模块中的依赖,不依赖全局环境

## 总结

**自己水平有限,使用ts还有诸多问题.还不如直接使用js或者直接学习egg来的实在,而且直接使用ts的实践还比较少.不够成熟.故最终放弃使用ts,升级失败 (┬＿┬)**
