---
layout: post
title: "概率论题型总结"
date: 2026-05-25 09:40:00 +0800
categories: 学习笔记
tags: ["概率论", "题型总结", "随机变量", "参数估计", "假设检验"]
subject: "概率论"
branch: "分支二"
description: "整理概率论常见题型，包括分布函数与密度函数、独立与不相关、全概率与贝叶斯、二维随机变量、抽样分布、参数估计、置信区间和假设检验。"
keywords: "概率论, 题型总结, 随机变量, 参数估计, 假设检验"
author: myh
---

> 这篇文章由大二上期末复习笔记整理而来，保留原始笔记的题型、公式和易错点，并补充了导读与阶段性总结，方便后续在博客中检索和复盘。

## 导读

- 这篇笔记以题型为主线，适合考前建立“看到题目先判断题型”的反应。
- 内容从F(x)与f(x)的关系、独立与不相关，到二维随机变量、抽样分布、参数估计、置信区间和假设检验，覆盖概率论期末常见大题方向。

## 学习总结

- 概率论题目要先判断对象：是分布函数、概率密度、联合分布、边缘分布，还是统计量。
- 连续型题目核心是积分区域，离散型题目核心是表格概率和边缘概率。
- 参数估计、置信区间和假设检验要分清公式适用条件，尤其是显著性水平、拒绝域和统计量分布。

<!--more-->

## 原始笔记正文
![image-20260112232844029](/assets/images/study-notes/probability-question-types/01-image-20260112232844029.jpg)

![image-20260112232923682](/assets/images/study-notes/probability-question-types/02-image-20260112232923682.jpg)

![image-20260112234057785](/assets/images/study-notes/probability-question-types/03-image-20260112234057785.jpg)

![image-20260112234126174](/assets/images/study-notes/probability-question-types/04-image-20260112234126174.jpg)

![image-20260112234215113](/assets/images/study-notes/probability-question-types/05-image-20260112234215113.jpg)

![image-20260112234230187](/assets/images/study-notes/probability-question-types/06-image-20260112234230187.jpg)

![image-20260112234324192](/assets/images/study-notes/probability-question-types/07-image-20260112234324192.jpg)

f(x)的积分（面积）=概率

分布函数是左侧概率（小于时）：积左边就行(积到x）

![image-20260112234924608](/assets/images/study-notes/probability-question-types/08-image-20260112234924608.jpg)

![image-20260112234942518](/assets/images/study-notes/probability-question-types/09-image-20260112234942518.jpg)错

![image-20260112234957254](/assets/images/study-notes/probability-question-types/10-image-20260112234957254.jpg)

![image-20260112235512679](/assets/images/study-notes/probability-question-types/11-image-20260112235512679.jpg)

![image-20260112235621293](/assets/images/study-notes/probability-question-types/12-image-20260112235621293.jpg)

![image-20260113013005135](/assets/images/study-notes/probability-question-types/13-image-20260113013005135.jpg)

![image-20260113013032600](/assets/images/study-notes/probability-question-types/14-image-20260113013032600.jpg)

![image-20260113013413540](/assets/images/study-notes/probability-question-types/15-image-20260113013413540.jpg)

![image-20260113013612476](/assets/images/study-notes/probability-question-types/16-image-20260113013612476.jpg)

![image-20260113013655629](/assets/images/study-notes/probability-question-types/17-image-20260113013655629.jpg)

![image-20260113014748535](/assets/images/study-notes/probability-question-types/18-image-20260113014748535.jpg)

显著性水平：现在弃真错误概率小于艾尔法

![image-20260113015035520](/assets/images/study-notes/probability-question-types/19-image-20260113015035520.jpg)

![image-20260113015407357](/assets/images/study-notes/probability-question-types/20-image-20260113015407357.jpg)

![image-20260113020319878](/assets/images/study-notes/probability-question-types/21-image-20260113020319878.jpg)

![image-20260113020626473](/assets/images/study-notes/probability-question-types/22-image-20260113020626473.jpg)

![image-20260113020907643](/assets/images/study-notes/probability-question-types/23-image-20260113020907643.jpg)

![image-20260113021402724](/assets/images/study-notes/probability-question-types/24-image-20260113021402724.jpg)

![image-20260113023038128](/assets/images/study-notes/probability-question-types/25-image-20260113023038128.jpg)

![image-20260113023333453](/assets/images/study-notes/probability-question-types/26-image-20260113023333453.jpg)

![image-20260113023423168](/assets/images/study-notes/probability-question-types/27-image-20260113023423168.jpg)

## 选择

### 1.F(x) f(x)

分布函数F(x)：累积量 负无穷到x F(x)=P(X<=x)

概率密度f(x)：积分后（面积）为这段概率

![image-20251228163706351](/assets/images/study-notes/probability-question-types/28-image-20251228163706351.jpg)

![image-20251228171840098](/assets/images/study-notes/probability-question-types/29-image-20251228171840098.jpg)

![image-20251228172248795](/assets/images/study-notes/probability-question-types/30-image-20251228172248795.jpg)

f(x):非负

![image-20251228172419248](/assets/images/study-notes/probability-question-types/31-image-20251228172419248.jpg)

积分=1

### 1.独立和不相关

![image-20251227225621604](/assets/images/study-notes/probability-question-types/32-image-20251227225621604.jpg)

![image-20251227225635639](/assets/images/study-notes/probability-question-types/33-image-20251227225635639.jpg)

1.

![image-20251227225700547](/assets/images/study-notes/probability-question-types/34-image-20251227225700547.jpg)

2.

![S](/assets/images/study-notes/probability-question-types/35-image-20251227225802807.jpg)

### 2.

##### 1.Z=min(X,Y)

![image-20251228153046550](/assets/images/study-notes/probability-question-types/36-image-20251228153046550.jpg)

![image-20251228153227483](/assets/images/study-notes/probability-question-types/37-image-20251228153227483.jpg)

![image-20251228153202829](/assets/images/study-notes/probability-question-types/38-image-20251228153202829.jpg)

![image-20251228153324968](/assets/images/study-notes/probability-question-types/39-image-20251228153324968.jpg)

##### 2.Z=max(X,Y)

![image-20251228153600149](/assets/images/study-notes/probability-question-types/40-image-20251228153600149.jpg)

### 3.

样本均值的分布

![image-20251228162301175](/assets/images/study-notes/probability-question-types/41-image-20251228162301175.jpg)

![image-20251228162333914](/assets/images/study-notes/probability-question-types/42-image-20251228162333914.jpg)

![image-20251228162635618](/assets/images/study-notes/probability-question-types/43-image-20251228162635618.jpg)

![image-20251228162751303](/assets/images/study-notes/probability-question-types/44-image-20251228162751303.jpg)

使Y均值=0 方差=1

![image-20251228162702234](/assets/images/study-notes/probability-question-types/45-image-20251228162702234.jpg)

### 4.

把大小关系转换为并集/交集

![image-20251228162727100](/assets/images/study-notes/probability-question-types/46-image-20251228162727100.jpg)

容斥原理 1并2=1+2-1交2

![image-20251228162522444](/assets/images/study-notes/probability-question-types/47-image-20251228162522444.jpg)

### 5.

## 全概率+贝叶斯

![image-20251227214929169](/assets/images/study-notes/probability-question-types/48-image-20251227214929169.jpg)

![image-20251227215123020](/assets/images/study-notes/probability-question-types/49-image-20251227215123020.jpg)

![image-20260113023056863](/assets/images/study-notes/probability-question-types/50-image-20260113023056863.jpg)

同分布·：方差、期望、概率密度函数同等

## 分布


> 图片占位：原笔记此处包含本地图片，当前未随博客同步。


## 二维离散型随机变量

![image-20251227215021996](/assets/images/study-notes/probability-question-types/51-image-20251227215021996.jpg)

## 二维连续型随机变量

![image-20251227214650360](/assets/images/study-notes/probability-question-types/52-image-20251227214650360.jpg)

## 抽样分布


> 图片占位：原笔记此处包含本地图片，当前未随博客同步。


## 参数估计


> 图片占位：原笔记此处包含本地图片，当前未随博客同步。


![image-20260101233737921](/assets/images/study-notes/probability-question-types/53-image-20260101233737921.jpg)

![image-20260101233758236](/assets/images/study-notes/probability-question-types/54-image-20260101233758236.jpg)

## 置信区间


> 图片占位：原笔记此处包含本地图片，当前未随博客同步。


![image-20251227205126511](/assets/images/study-notes/probability-question-types/55-image-20251227205126511.jpg)

## 假设检验

![image-20251227205141051](/assets/images/study-notes/probability-question-types/56-image-20251227205141051.jpg)
