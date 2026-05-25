---
layout: post
title: "信息安全数学基础复习"
date: 2026-05-25 10:20:00 +0800
categories: 学习笔记
tags: ["信息安全数学基础", "数论", "同余", "欧拉函数", "勒让德符号", "原根"]
subject: "信息安全数学基础"
branch: "分支四"
description: "整理信息安全数学基础中的数论核心内容，包括互质、整除、欧拉函数、剩余系、同余方程、二次同余、勒让德符号和原根。"
keywords: "信息安全数学基础, 数论, 同余, 欧拉函数, 勒让德符号, 原根"
author: myh
---

> 这篇文章由大二上期末复习笔记整理而来，保留原始笔记的题型、公式和易错点，并补充了导读与阶段性总结，方便后续在博客中检索和复盘。

## 导读

- 这篇笔记面向信息安全数学基础复习，核心是把数论概念和解题条件整理清楚。
- 内容覆盖互质、整除、欧拉函数、带余除法、裴蜀定理、剩余系、同余、一次同余方程、二次同余、勒让德符号和原根。

## 学习总结

- 数论题最重要的是先判断条件：是否互素、最大公约数是否整除、模数是否为奇素数。
- 一次同余方程看gcd(a,m)是否整除b，二次同余要结合平方剩余和勒让德符号判断解的个数。
- 信息安全数学基础和密码学联系紧密，欧拉函数、逆元、剩余系、原根都是后续理解加密算法的基础。

<!--more-->

## 原始笔记正文
信安数基重点：

## 互质

![image-20260111183220087](/assets/images/study-notes/infosec-math-foundations-review/01-image-20260111183220087.jpg)

![image-20260111183427824](/assets/images/study-notes/infosec-math-foundations-review/02-image-20260111183427824.jpg)

![image-20260111183231658](/assets/images/study-notes/infosec-math-foundations-review/03-image-20260111183231658.jpg)

![image-20260111183244526](/assets/images/study-notes/infosec-math-foundations-review/04-image-20260111183244526.jpg)

## 整除

#### 求欧拉函数所有方法：

![image-20260109230459103](/assets/images/study-notes/infosec-math-foundations-review/05-image-20260109230459103.jpg)

#### 素数判定

![image-20260111170031454](/assets/images/study-notes/infosec-math-foundations-review/06-image-20260111170031454.jpg)

![image-20260111170208857](/assets/images/study-notes/infosec-math-foundations-review/07-image-20260111170208857.jpg)

#### 带余除法

0<=r<b  c<r<c+b

![image-20260111164449906](/assets/images/study-notes/infosec-math-foundations-review/08-image-20260111164449906.jpg)

![image-20260111164424535](/assets/images/study-notes/infosec-math-foundations-review/09-image-20260111164424535.jpg)

![image-20260111170140770](/assets/images/study-notes/infosec-math-foundations-review/10-image-20260111170140770.jpg)

#### 裴蜀定理

前提：a,b互素

![image-20260111164524863](/assets/images/study-notes/infosec-math-foundations-review/11-image-20260111164524863.jpg)

![image-20260111165401151](/assets/images/study-notes/infosec-math-foundations-review/12-image-20260111165401151.jpg)

![image-20260111164603755](/assets/images/study-notes/infosec-math-foundations-review/13-image-20260111164603755.jpg)

a|bc+(a,b)=1 :a|c

b|a c|a+(b,c)=1:bc|a

![image-20260111170255908](/assets/images/study-notes/infosec-math-foundations-review/14-image-20260111170255908.jpg)

![image-20260111165113661](/assets/images/study-notes/infosec-math-foundations-review/15-image-20260111165113661.jpg)

![image-20260111165316087](/assets/images/study-notes/infosec-math-foundations-review/16-image-20260111165316087.jpg)

## 剩余系

模 8的完全剩余系必须包含 **8** 个元素

![image-20260111171354457](/assets/images/study-notes/infosec-math-foundations-review/17-image-20260111171354457.jpg)

![image-20260111171408714](/assets/images/study-notes/infosec-math-foundations-review/18-image-20260111171408714.jpg)

简化剩余系里面没0

简化剩余系里可以都是奇数，不能都是偶数

模 m的简化剩余系中，每个元素 a 都存在唯一的模乘逆元 a-1：根据模乘逆元存在定理，gcd(a, m)=1是逆元存在的充分必要条件

## 同余

负元和逆元：

1负元（加法）凑0

2逆元（乘法）凑1

有逆元的前提是a,m互素

![image-20260109225635789](/assets/images/study-notes/infosec-math-foundations-review/19-image-20260109225635789.jpg)

## 一次同余方程

### 前提

先求gcd(a,m) 看能不能整除b 再看是不是等于1

![image-20260109230820104](/assets/images/study-notes/infosec-math-foundations-review/20-image-20260109230820104.jpg)

![image-20260109230937348](/assets/images/study-notes/infosec-math-foundations-review/21-image-20260109230937348.jpg)

### 有几个解

#### 1.一次同余方程：

###### 能整除**最大公约数个解** 不能没解

gcd(a,m)|b

![image-20260109233144273](/assets/images/study-notes/infosec-math-foundations-review/22-image-20260109233144273.jpg)

#### 2.一次同余方程组

m两两互素-唯一解=

#### 3.二次同余方程：

###### 勒让德符号=**1 两个解 //-1没有// 0一个**

1 平方剩余 两个解

-1 平方非剩余 无解

0 p|a =0 1个解

![image-20260109233154709](/assets/images/study-notes/infosec-math-foundations-review/23-image-20260109233154709.jpg)

![image-20260111145016938](/assets/images/study-notes/infosec-math-foundations-review/24-image-20260111145016938.jpg)

m=pq有解-p q同时有解

![image-20260111145344515](/assets/images/study-notes/infosec-math-foundations-review/25-image-20260111145344515.jpg)

![image-20260111150158541](/assets/images/study-notes/infosec-math-foundations-review/26-image-20260111150158541.jpg)

![image-20260111150239136](/assets/images/study-notes/infosec-math-foundations-review/27-image-20260111150239136.jpg)

![image-20260111150304450](/assets/images/study-notes/infosec-math-foundations-review/28-image-20260111150304450.jpg)

若该方程只有 2 个解，则一定是因为 a 是 p 或 q的倍数：正常情况下模  有解必是 4 个。如果变成了 2 个，说明其中一个门只有 1 个解

## 二次同余(平方剩余)

#### 个数

p奇素数+简化剩余系=一半平方剩余 一半平方非剩余(p-1)/2

​              +完全剩余系=平方剩余：（p+1)/2 平方非剩余（p-1)/2

![image-20260111184919791](/assets/images/study-notes/infosec-math-foundations-review/29-image-20260111184919791.jpg)

![image-20260111184815350](/assets/images/study-notes/infosec-math-foundations-review/30-image-20260111184815350.jpg)

![image-20260111184830926](/assets/images/study-notes/infosec-math-foundations-review/31-image-20260111184830926.jpg)

#### 平方数一定是平方剩余

![image-20260111185120801](/assets/images/study-notes/infosec-math-foundations-review/32-image-20260111185120801.jpg)

![image-20260111185150477](/assets/images/study-notes/infosec-math-foundations-review/33-image-20260111185150477.jpg)

## 勒让德符号

奇数*奇数=奇数

奇数*偶数=偶数

### 性质

#### 1.周期性：去模化简

![image-20260109231143838](/assets/images/study-notes/infosec-math-foundations-review/34-image-20260109231143838.jpg)

#### 2.乘法：分子ab可以直接拆开

![image-20260109231227728](/assets/images/study-notes/infosec-math-foundations-review/35-image-20260109231227728.jpg)

#### 3.欧拉判别准则：1（有根） -1（没根） 0（整除）

数小的时候用

问法：**判断a是不是b的二次剩余/方程是否有解**

![image-20260109232258393](/assets/images/study-notes/infosec-math-foundations-review/36-image-20260109232258393.jpg)

![image-20260109232537561](/assets/images/study-notes/infosec-math-foundations-review/37-image-20260109232537561.jpg)

![image-20260109232227151](/assets/images/study-notes/infosec-math-foundations-review/38-image-20260109232227151.jpg)

## 原根

### 定义

![image-20260109193317873](/assets/images/study-notes/infosec-math-foundations-review/39-image-20260109193317873.jpg)

### 关系

![image-20260109193332631](/assets/images/study-notes/infosec-math-foundations-review/40-image-20260109193332631.jpg)

### 判断

#### 阶

定义:必须是**最小正整数**

阶（不是d，要确定是最小正整数阶）|整除 欧拉函数

![image-20260111152525947](/assets/images/study-notes/infosec-math-foundations-review/41-image-20260111152525947.jpg)

![image-20260109194457878](/assets/images/study-notes/infosec-math-foundations-review/42-image-20260109194457878.jpg)

![image-20260111151314427](/assets/images/study-notes/infosec-math-foundations-review/43-image-20260111151314427.jpg)

#### 原根

1**必须有原根才有指数**

如果找不到一个能覆盖全场的“原根”，我们就无法为集合里所有的数建立一套统一的、完整的“指数映射表” 。因此，指数系统也就失去了意义。

**2只要有属于简化剩余系的原根（与m互素的数）：每个数都有唯一的指数**（因为这 ϕ(m) 个余数互不相同，且都落在“简化剩余系”这个范围内，所以它们刚好一个不漏、不重复地盖满了整个集合

3判定基础：首先确认**模m是否存在原根（m是否属于m=2，m=4，m=素数n次方，m=2*素数n次方 ）**![image-20260109193354400](/assets/images/study-notes/infosec-math-foundations-review/44-image-20260109193354400.jpg)

![image-20260111151334874](/assets/images/study-notes/infosec-math-foundations-review/45-image-20260111151334874.jpg)

建立联系：指出原根 g 是简化剩余系的一个生成元，它通过方幂  gx与系内元素 a 建立了一一对应的关系，这种关系即为指数（离散对数

4原根个数： ![image-20260109194412372](/assets/images/study-notes/infosec-math-foundations-review/46-image-20260109194412372.jpg)

![image-20260111155615616](/assets/images/study-notes/infosec-math-foundations-review/47-image-20260111155615616.jpg)

#### 离散对数![image-20260111152713634](/assets/images/study-notes/infosec-math-foundations-review/48-image-20260111152713634.jpg)

![image-20260111152722743](/assets/images/study-notes/infosec-math-foundations-review/49-image-20260111152722743.jpg)

p-1

#### 指数

**指数性质**![image-20260109193431075](/assets/images/study-notes/infosec-math-foundations-review/50-image-20260109193431075.jpg)

![image-20260111160912828](/assets/images/study-notes/infosec-math-foundations-review/51-image-20260111160912828.jpg)

讲解：

![image-20260111160929606](/assets/images/study-notes/infosec-math-foundations-review/52-image-20260111160929606.jpg)



![image-20260111161849252](/assets/images/study-notes/infosec-math-foundations-review/53-image-20260111161849252.jpg)

![image-20260111161903947](/assets/images/study-notes/infosec-math-foundations-review/54-image-20260111161903947.jpg)

![image-20260109193756417](/assets/images/study-notes/infosec-math-foundations-review/55-image-20260109193756417.jpg)

## 近世代数

### 群判定


> 图片占位：原笔记此处包含本地图片，当前未随博客同步。


### 环域判定


> 图片占位：原笔记此处包含本地图片，当前未随博客同步。


加法：

封闭性：任意两个数相加，结果还在集合里

结合律:模加法满足结合律

加法单位元：为0（任意数+0=不变）

加法逆元：表中的0 任意元素有加法逆元

交换律：模加法满足交换律

**交换群**

加法分配律：模加法满足分配律

乘法：

乘法封闭性+结合律：乘完还在集合里，模乘法满足乘法结合律

**环**

乘法单位元：为1（任何数*1=不变）

非零乘法逆元：表中1 任意非零元素有乘法逆元

交换律：模乘法满足交换律

**域**

![](/assets/images/study-notes/infosec-math-foundations-review/56-image-20260109212759761.jpg)

![image-20260109212826043](/assets/images/study-notes/infosec-math-foundations-review/57-image-20260109212826043.jpg)

![image-20260109212900822](/assets/images/study-notes/infosec-math-foundations-review/58-image-20260109212900822.jpg)

### 不可约多项式

1

![image-20260109205052409](/assets/images/study-notes/infosec-math-foundations-review/59-image-20260109205052409.jpg)

可约”的意思是这个多项式可以被“拆开”，

3 次多项式  是可约的，它拆开后的次数分配只有一种可能：3 次 = 1 次 *2 次

它一定会包含一个 1 次因式（即形如 x - c 的部分）

![image-20260109205032525](/assets/images/study-notes/infosec-math-foundations-review/60-image-20260109205032525.jpg)

### 概念

#### 群

单位元**唯一**

封闭性![image-20260109222604683](/assets/images/study-notes/infosec-math-foundations-review/61-image-20260109222604683.jpg)

循环群与原根：若模m存在**原根**，则其**简化剩余系**关于模乘法构成的群是**循环群**。

运算表判定：在有限群的运算表中，**每一行和每一列中，每个群元素都出现且仅出现一次**

封闭+结合+左逆元+左单位元=群（左＋右不行：

![image-20260111190821686](/assets/images/study-notes/infosec-math-foundations-review/62-image-20260111190821686.jpg)

封闭+结合+左/右单位元=半群

![image-20260111191631156](/assets/images/study-notes/infosec-math-foundations-review/63-image-20260111191631156.jpg)

#### 循环群

##### 循环群一定是交换群

##### 循环群有几个生成元

1.欧拉函数个

![image-20260111191122207](/assets/images/study-notes/infosec-math-foundations-review/64-image-20260111191122207.jpg)

2.无限：两个

![image-20260111191139697](/assets/images/study-notes/infosec-math-foundations-review/65-image-20260111191139697.jpg)

**所有真子群是循环群，原来群不一定是循环群**

![image-20260111191802816](/assets/images/study-notes/infosec-math-foundations-review/66-image-20260111191802816.jpg)

##### 群：逆元运算(交换) 共轭 交换群：性质

![image-20260111192733978](/assets/images/study-notes/infosec-math-foundations-review/67-image-20260111192733978.jpg)

#### 环

**环和域区别：非零元素是否都有乘法逆元**（环就是因为有的元素没有乘法逆元变成不了域的）

#### 域

![image-20260109223209942](/assets/images/study-notes/infosec-math-foundations-review/68-image-20260109223209942.jpg):Z6不是域 Z5是

域中每一个**非零**元素都要有乘法逆元

![image-20260111195710207](/assets/images/study-notes/infosec-math-foundations-review/69-image-20260111195710207.jpg)

1**有理数集Q+实数集R+复数集C** 普通加法和乘法构成**域**

2整数集Z 环

3合数模剩余类Z6 环 素数模剩余类 域

4多项式集R[x] 环

5矩阵集 环

![image-20260111190201414](/assets/images/study-notes/infosec-math-foundations-review/70-image-20260111190201414.jpg)

#### 不可约多项式

多项式可约性：一个多项式在不同意义下（不同的域上）的可约性可能不同

*可不可约：*

*1 2/3次代入0和1 ！=0没根就不可约*

*2 看能不能拆成相乘*

![image-20260111192622473](/assets/images/study-notes/infosec-math-foundations-review/71-image-20260111192622473.jpg)

**2次/3次没根肯定不可约 456次不一定**



**3 次多项式判定：一个 3 次多项式在Zp上不可约的充要条件是它Zp中没有根**

![image-20260109223044358](/assets/images/study-notes/infosec-math-foundations-review/72-image-20260109223044358.jpg)

![image-20260111190615534](/assets/images/study-notes/infosec-math-foundations-review/73-image-20260111190615534.jpg)

![image-20260111192331262](/assets/images/study-notes/infosec-math-foundations-review/74-image-20260111192331262.jpg)

![image-20260111192354043](/assets/images/study-notes/infosec-math-foundations-review/75-image-20260111192354043.jpg)

1.**构造有限域**的方法就是使用**不**可约多项式

![image-20260109223938731](/assets/images/study-notes/infosec-math-foundations-review/76-image-20260109223938731.jpg)

2有限域阶的个数（阶个数）Z3 2次 3的2次方=9个

![image-20260109224048969](/assets/images/study-notes/infosec-math-foundations-review/77-image-20260109224048969.jpg)

![image-20260109224129938](/assets/images/study-notes/infosec-math-foundations-review/78-image-20260109224129938.jpg)

![image-20260111190530670](/assets/images/study-notes/infosec-math-foundations-review/79-image-20260111190530670.jpg)

![image-20260111193038374](/assets/images/study-notes/infosec-math-foundations-review/80-image-20260111193038374.jpg)

3.

![image-20260109224317417](/assets/images/study-notes/infosec-math-foundations-review/81-image-20260109224317417.jpg)
