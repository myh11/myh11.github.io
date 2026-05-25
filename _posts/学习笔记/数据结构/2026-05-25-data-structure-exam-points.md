---
layout: post
title: "数据结构考点总结"
date: 2026-05-25 10:10:00 +0800
categories: 学习笔记
tags: ["数据结构", "考点总结", "树", "图", "线性表", "数组"]
subject: "数据结构"
branch: "分支三"
description: "围绕数据结构考试高频考点整理，覆盖树与二叉树、图、线性表、栈队列数组、串、广义表、二叉排序树和遍历构造。"
keywords: "数据结构, 考点总结, 树, 图, 线性表, 数组"
author: myh
---

> 这篇文章由大二上期末复习笔记整理而来，保留原始笔记的题型、公式和易错点，并补充了导读与阶段性总结，方便后续在博客中检索和复盘。

## 导读

- 这篇更偏“考点清单”，把树、图、线性表、数组、栈队列、串和二叉排序树中容易考计算或判断的内容集中整理。
- 笔记中包含完全二叉树、连通图、强连通图、矩阵压缩存储、后缀表达式、二叉排序树、遍历序列构造等典型考点。

## 学习总结

- 树和图的题目通常是性质计算题，要熟悉叶子结点、度、边数、连通性、强连通性等公式。
- 数组和矩阵压缩存储题要按下标、存储顺序和地址公式一步一步算。
- 二叉排序树、遍历序列构造和线性结构操作，是概念题与代码题之间的桥。

<!--more-->

## 原始笔记正文
## 代办：

所有涉及时间、空间复杂度的总结

各种树、图的概念、性质（计算）

线性表 栈 队列还没弄

## 概念

线性

时间复杂度

#### 树

##### 性质

度为0（叶子）数=度为2点数+1

![image-20260114145919255](/assets/images/study-notes/data-structure-exam-points/01-image-20260114145919255.jpg)

![image-20260114151948773](/assets/images/study-notes/data-structure-exam-points/02-image-20260114151948773.jpg)

![image-20260114194810293](/assets/images/study-notes/data-structure-exam-points/03-image-20260114194810293.jpg)

##### 分类

![image-20260114145932694](/assets/images/study-notes/data-structure-exam-points/04-image-20260114145932694.jpg)

完全二叉树叶子节点个数：n/2

![image-20260114151150565](/assets/images/study-notes/data-structure-exam-points/05-image-20260114151150565.jpg)

![image-20260114152012393](/assets/images/study-notes/data-structure-exam-points/06-image-20260114152012393.jpg)

**二叉排序树** 左<根<右

**平衡二叉树** 任意结点左右子树深度差<=1

**有向树** 一个顶点入度为0，其他点入度为1

![](/assets/images/study-notes/data-structure-exam-points/88-image-20260114150000214.jpg)

**生成树** **子图** 包含全部顶点的**极小连通子图**（边极可能少）

连通分量：极大连通子图

eg:

###### 完全二叉树 第六层8叶子结点 树最多多少点？

叶子结点只出现在**最后两层**

前6层满 2的6次方-1=63

第7层有 2的7-1次方=64-2*8=48

63+48=111

#### 图

G=（V，E）点集V（G）不能空， 边集E（G）可以空

|V|点个数

![image-20260114200031514](/assets/images/study-notes/data-structure-exam-points/07-image-20260114200031514.jpg)

连通图：无向图+任意两点都能到 最少n-1条边

强连通图：有向图+任意两点都能来回走 最少n条边 最多n(n-1)

![image-20260114150017023](/assets/images/study-notes/data-structure-exam-points/08-image-20260114150017023.jpg)

完全图：任意两点间都有线

有向完全图 边数 n(n-1)

![image-20260114194927587](/assets/images/study-notes/data-structure-exam-points/09-image-20260114194927587.jpg)

**无向完全图          n(n-1)/2**

![image-20260114195848819](/assets/images/study-notes/data-structure-exam-points/10-image-20260114195848819.jpg)

连通分量：**无**向图中极大连通子图（尽可能包含更多的点边）

强连通分量：有

![image-20260114150024824](/assets/images/study-notes/data-structure-exam-points/11-image-20260114150024824.jpg)

## 线性表

### 顺序表

![image-20260114143224087](/assets/images/study-notes/data-structure-exam-points/12-image-20260114143224087.jpg)

![image-20260114143237506](/assets/images/study-notes/data-structure-exam-points/13-image-20260114143237506.jpg)

![image-20260114144712228](/assets/images/study-notes/data-structure-exam-points/14-image-20260114144712228.jpg)



### 链表

![image-20260114143248537](/assets/images/study-notes/data-structure-exam-points/15-image-20260114143248537.jpg)

![image-20260114143308666](/assets/images/study-notes/data-structure-exam-points/16-image-20260114143308666.jpg)

![image-20260114143325077](/assets/images/study-notes/data-structure-exam-points/17-image-20260114143325077.jpg)

![ed8fa8807e6677ac4add19bd10d5d258](/assets/images/study-notes/data-structure-exam-points/18-ed8fa8807e6677ac4add19bd10d5d258.jpg)

![92c2fc019afa6d27a1894991760d9e27](/assets/images/study-notes/data-structure-exam-points/19-92c2fc019afa6d27a1894991760d9e27.jpg)

![image-20260114144548626](/assets/images/study-notes/data-structure-exam-points/20-image-20260114144548626.jpg)

## 栈、队列、数组

### 数组

#### 1.存储地址 记公式

![image-20260114124938129](/assets/images/study-notes/data-structure-exam-points/21-image-20260114124938129-1768366184162-1.jpg)

行优先存储（先存完一行，再存下一行）

公式：**行优先 地址 = 起始地址 + (行号×列数 + 列号) × 每个元素字节数**

计算过程：
A[6,6] = 100 + (6×20 + 6) × 2 = 100 + 126×2 = 100 + 252 = 352

- 前6行（0~5行），每行有20个元素，共 6×20 个元素。
- 第6行中，前6列（0~5列）有6个元素。

#### 2.对称矩阵元素下标：画图硬算

![image-20260114131954939](/assets/images/study-notes/data-structure-exam-points/22-image-20260114131954939.jpg)

![image-20260114125819089](/assets/images/study-notes/data-structure-exam-points/23-image-20260114125819089.jpg)

18：

按行，上面的5行12+11+10+9+8=50 第六行第一个+1 再-1（地址从0开始）=50

20：

等于第二行第7列 按列 前六列1+2+3+4+5+6=21 第7列2 -1 =22

#### 3.上/下三角

![image-20260114132310168](/assets/images/study-notes/data-structure-exam-points/24-image-20260114132310168.jpg)

![image-20260114131920077](/assets/images/study-notes/data-structure-exam-points/25-image-20260114131920077.jpg)

### 栈

递归调用、表达式求值、括号匹配

后缀表达式：**左右运**

![image-20260114205259976](/assets/images/study-notes/data-structure-exam-points/26-image-20260114205259976.jpg)

### 队列

缓存、图的广度优先搜索



## 串与广义表

### 串

![image-20260114135601096](/assets/images/study-notes/data-structure-exam-points/27-image-20260114135601096.jpg)

![image-20260114134434760](/assets/images/study-notes/data-structure-exam-points/28-image-20260114134434760.jpg)

![image-20260114134533190](/assets/images/study-notes/data-structure-exam-points/29-image-20260114134533190.jpg)

![image-20260114135351321](/assets/images/study-notes/data-structure-exam-points/30-image-20260114135351321.jpg)

两个字符串相等：长度相等且对应位置字符相同

1**.朴素模式匹配：最坏时间复杂度是O(mn)** ，其中 n是主串长度， m是模式串长度

2.**KMP 算法**:**在发生失配时，主串 T 的指针 i 永远不回溯.**它通过预先计算模式串 P 的自身特性（即 next 数组），知道失配后 P 应该向右“跳跃”到哪里继续比较.

![image-20260114141416197](/assets/images/study-notes/data-structure-exam-points/31-image-20260114141416197.jpg)

![image-20260114140954478](/assets/images/study-notes/data-structure-exam-points/32-image-20260114140954478.jpg)

总时间复杂度为 O(m+n)

不考

![image-20260114145052239](/assets/images/study-notes/data-structure-exam-points/33-image-20260114145052239.jpg)

建议从-1 0开始 不知道考不考nextual?

### 广义表

![image-20260114145104575](/assets/images/study-notes/data-structure-exam-points/34-image-20260114145104575.jpg)

下面这个有点没懂？

![image-20260114145120660](/assets/images/study-notes/data-structure-exam-points/35-image-20260114145120660.jpg)

## 数与二叉树

### 1.二叉排序树 左<根<右

构造、查找某元素次数、ASL（失败的）、删除

中序遍历序列永远是有序递增序列

只要关键字集相同，中序序列就唯一，但BST树可以有很多不同的

![image-20260114154459517](/assets/images/study-notes/data-structure-exam-points/36-image-20260114154459517.jpg)

#### ASL

![image-20260114152226602](/assets/images/study-notes/data-structure-exam-points/37-image-20260114152226602.jpg)

![image-20260114151308987](/assets/images/study-notes/data-structure-exam-points/38-image-20260114151308987.jpg)

![image-20260114154353650](/assets/images/study-notes/data-structure-exam-points/39-image-20260114154353650.jpg)

#### 删除

左子树最右下（最大）/右子树最左下 （最小)

![image-20260114151445936](/assets/images/study-notes/data-structure-exam-points/40-image-20260114151445936.jpg)

![image-20260114151457972](/assets/images/study-notes/data-structure-exam-points/41-image-20260114151457972.jpg)

#### 性能优化

ASLmin：构造平衡二叉树

![image-20260114154130588](/assets/images/study-notes/data-structure-exam-points/42-image-20260114154130588.jpg)

### 2.先/中/后/层序遍历

![image-20260114154846514](/assets/images/study-notes/data-structure-exam-points/43-image-20260114154846514.jpg)

### 遍历序列构造二叉树

先从前/后/层找根结点，再用根结点分中的左右

前+中 前的第一个是根

后＋中 后的最后一个是根

层＋中 层的第一个是中

![image-20260114155040307](/assets/images/study-notes/data-structure-exam-points/44-image-20260114155040307.jpg)



![image-20260114155056299](/assets/images/study-notes/data-structure-exam-points/45-image-20260114155056299.jpg)

能对

### 3.求最小生成树（计算代价）

#### 3.1 prime算法

只和点有关 适合**边稠密图** O（|v|2）

从点出发 找此点的最短边 合并成一个整体找最短边（最小代价唯一/相同）

![image-20260114171823753](/assets/images/study-notes/data-structure-exam-points/46-image-20260114171823753.jpg)

![image-20260114163237507](/assets/images/study-notes/data-structure-exam-points/47-image-20260114163237507.jpg)

![image-20260114163251232](/assets/images/study-notes/data-structure-exam-points/48-image-20260114163251232.jpg)

#### 3.2 krusakal算法不考

只和边有关 边稀疏图 O（|E|log2|E|）

选最小边 使点间联通 原本两点联通的不要 至所有点连通

![image-20260114155130999](/assets/images/study-notes/data-structure-exam-points/49-image-20260114155130999.jpg)

### 4.求一点v1到其他点的最短路径和路径长度 dijkstra算法

不能含负权值

![image-20260114195120917](/assets/images/study-notes/data-structure-exam-points/50-image-20260114195120917.jpg)

S：已确定最短路径的节点集合，初始时仅包含起点（如0号节点）。
U：未确定最短路径的节点集合，初始时包含除起点外的所有节点。
dist[]：记录起点到各节点的当前最短距离
path[]：记录各节点最短路径的前驱节点，初始时无前置节点则设为-1或起点

![image-20260114163454776](/assets/images/study-notes/data-structure-exam-points/51-image-20260114163454776.jpg)

![image-20260114163506016](/assets/images/study-notes/data-structure-exam-points/52-image-20260114163506016.jpg)

### 5.拓扑排序 kahn算法

**检测是否存在环**-如无法完成拓扑排序，则有环

Kahn算法：不断选取入度为0的节点（在把入度为0的点选完了在往下走），移除其出边并更新邻接节点入度，直到所有节点

![image-20260114163555215](/assets/images/study-notes/data-structure-exam-points/53-image-20260114163555215.jpg)

### 6.关键路径

事件最早开始时间 Ve[k] **取最大**

​            晚                Vl[k] **取最小** 从后往前

活动最早开始时间 e[i]  **找前面一个最早事件**

​            晚                 l[i] **最晚事件-权值** 从后往前

时间余量 活动最晚-最早

关键活动 时间余量为0

关键路径 有关键活动的路径（可能不止一条）

![image-20260114164755511](/assets/images/study-notes/data-structure-exam-points/54-image-20260114164755511.jpg)

![image-20260114164813128](/assets/images/study-notes/data-structure-exam-points/55-image-20260114164813128.jpg)

### 7.数、森林与二叉树相互转换

#### 1.树转二叉树

左孩右兄：B的左孩子不变，右孩子为B的兄弟

![image-20260114174656122](/assets/images/study-notes/data-structure-exam-points/56-image-20260114174656122.jpg)

#### 2.森林转二叉树

A的左孩子不变，

右孩子为A的兄弟D

![image-20260114174739563](/assets/images/study-notes/data-structure-exam-points/57-image-20260114174739563.jpg)

#### 3.二叉树转树

![image-20260114174830185](/assets/images/study-notes/data-structure-exam-points/58-image-20260114174830185.jpg)

#### 4.二叉树转森林

![image-20260114174847139](/assets/images/study-notes/data-structure-exam-points/59-image-20260114174847139.jpg)

### 8.哈夫曼树

1.构造哈夫曼树（带权长度最短二叉树）：左<中<右

![image-20260114174929588](/assets/images/study-notes/data-structure-exam-points/60-image-20260114174929588.jpg)

2.每个元素的哈夫曼编码 左0右1

3.平均编码长度WPL=概率*对比几次 的和

### 9.线索二叉树

## 图

### 1.图的深度优先遍历DFS

递归 栈实现

从一个点出发 从临接点选一个往下走（这里导致有多种结果） 直到这条路走完了但点不全 回溯到上一个结点继续

![image-20260114195257223](/assets/images/study-notes/data-structure-exam-points/61-image-20260114195257223.jpg)

### 2.图的广度优先遍历BFS

队列实现

从一个点出发（指定） 访问所有相邻节点

![image-20260114175003740](/assets/images/study-notes/data-structure-exam-points/62-image-20260114175003740.jpg)

有很多种答案啊 写一个就行吗？

### 3.图的存储-画邻接矩阵、邻接表

![image-20260114203549234](/assets/images/study-notes/data-structure-exam-points/63-image-20260114203549234.jpg)

![image-20260114190358140](/assets/images/study-notes/data-structure-exam-points/64-image-20260114190358140.jpg)

![image-20260114190409690](/assets/images/study-notes/data-structure-exam-points/65-image-20260114190409690.jpg)

## 查找

#### 1.线性探测法建立查找表（已知散列函数）并计算ASL成功（平均查找长度)

![image-20260114192923642](/assets/images/study-notes/data-structure-exam-points/66-image-20260114192923642.jpg)

![image-20260114192730368](/assets/images/study-notes/data-structure-exam-points/67-image-20260114192730368.jpg)

不知道冲突时的规范写法

#### 2.链地址法

画图+求ASL成功

![image-20260114192748979](/assets/images/study-notes/data-structure-exam-points/68-image-20260114192748979.jpg)

![image-20260114192853677](/assets/images/study-notes/data-structure-exam-points/69-image-20260114192853677.jpg)

#### 3.查找关键字的平均查找长度（成功+不成功）

1.折半法

查找次数

从0开始

![image-20260114193451383](/assets/images/study-notes/data-structure-exam-points/70-image-20260114193451383.jpg)

2.二叉排序树

![image-20260114193536907](/assets/images/study-notes/data-structure-exam-points/71-image-20260114193536907.jpg)

#### 平衡二叉树

| **调整类型** | **插入路径**                   | **平衡因子变化** | **旋转操作**           |
| ------------ | ------------------------------ | ---------------- | ---------------------- |
| LL (左左)    | 失衡点的**左孩子**的**左子树** | BF = 2           | 针对失衡结点**右旋**   |
| RR (右右)    | 失衡点的**右孩子**的**右子树** | BF = -2          | 针对失衡结点**左旋**   |
| LR (左右)    | 失衡点的**左孩子**的**右子树** | BF = 2           | **双旋**：先左旋再右旋 |
| RL(右左)     | 失衡点的**右孩子**的**左子树** | BF = -2          | **双旋**：先右旋再左旋 |

![image-20251215223008644](/assets/images/study-notes/data-structure-exam-points/72-image-20251215223008644.jpg)

## 排序

#### 1.直接插入

有序时最快

![image-20260114200610695](/assets/images/study-notes/data-structure-exam-points/73-image-20260114200610695.jpg)

![image-20260114193812230](/assets/images/study-notes/data-structure-exam-points/74-image-20260114193812230.jpg)

![image-20260114193829643](/assets/images/study-notes/data-structure-exam-points/75-image-20260114193829643.jpg)

#### 2.希尔

![image-20260114193851104](/assets/images/study-notes/data-structure-exam-points/76-image-20260114193851104.jpg)

![image-20260114193902833](/assets/images/study-notes/data-structure-exam-points/77-image-20260114193902833.jpg)

#### 3.冒泡

![image-20260114193945843](/assets/images/study-notes/data-structure-exam-points/78-image-20260114193945843.jpg)

![image-20260114193954219](/assets/images/study-notes/data-structure-exam-points/79-image-20260114193954219.jpg)

#### 4.快速

平均最快

每一趟能保证至少有一个元素放到最终位置

![image-20260114194010768](/assets/images/study-notes/data-structure-exam-points/80-image-20260114194010768.jpg)

![image-20260114194019977](/assets/images/study-notes/data-structure-exam-points/81-image-20260114194019977.jpg)

#### 5.简单选择

与初始顺序无关

![image-20260114201626700](/assets/images/study-notes/data-structure-exam-points/82-image-20260114201626700.jpg)

![image-20260114194031634](/assets/images/study-notes/data-structure-exam-points/83-image-20260114194031634.jpg)

#### 6.堆排序

选前k个最有效

![image-20260114201523824](/assets/images/study-notes/data-structure-exam-points/84-image-20260114201523824.jpg)

![image-20260114201750663](/assets/images/study-notes/data-structure-exam-points/85-image-20260114201750663.jpg)

![image-20260114194049307](/assets/images/study-notes/data-structure-exam-points/86-image-20260114194049307.jpg)

![image-20260114194106587](/assets/images/study-notes/data-structure-exam-points/87-image-20260114194106587.jpg)
