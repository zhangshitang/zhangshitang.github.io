---
title: npm浏览器代理设置
tags: npm
excerpt: '内网办公可能会需要配置浏览器代理'
date: 2022-07-22 10:23:11
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