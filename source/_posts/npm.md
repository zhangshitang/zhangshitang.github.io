---
title: npm浏览器代理设置
tags: npm
categories: 前端
---
设置npm 浏览器代理
```
npm config set proxy=http:
```
取消npm 浏览器代理
```
npm config delete proxy
```
npm设置淘宝镜像 npm 
```
config set registry=https://registry.npm.taobao.org
```
npm取消淘宝镜像
```
npm config delete registry
```
查看代理信息（当前配置） 
```
npm config list
```