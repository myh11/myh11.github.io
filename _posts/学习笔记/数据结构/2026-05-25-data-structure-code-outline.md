---
layout: post
title: "数据结构代码题大纲"
date: 2026-05-25 09:50:00 +0800
categories: 学习笔记
tags: ["数据结构", "代码题", "链表", "顺序表", "C语言"]
subject: "数据结构"
branch: "分支三"
description: "整理数据结构代码题的基本模板，重点围绕顺序表、单链表、头插法、尾插法、链表逆置、查找、插入、删除等常见代码框架。"
keywords: "数据结构, 代码题, 链表, 顺序表, C语言"
author: myh
---

> 这篇文章由大二上期末复习笔记整理而来，保留原始笔记的题型、公式和易错点，并补充了导读与阶段性总结，方便后续在博客中检索和复盘。

## 导读

- 这篇是数据结构代码题的“模板仓库”，重点不在背答案，而是在理解指针移动顺序。
- 笔记从LNode和LinkList定义开始，围绕头插、尾插、链表逆置、查找、插入等基础操作整理可直接复用的C语言框架。

## 学习总结

- 链表题最容易错在指针先后顺序，尤其是逆置时要先保存后继节点，再改变当前节点指向。
- 有头结点的链表操作要区分头结点L和第一个数据节点L->next。
- 代码题复习建议把初始化、创建、遍历、查找、插入、删除、逆置拆成固定模板反复手写。

<!--more-->

## 原始笔记正文
数据结构代码题

```c
typedef struct LNode{//
    ElemType data;
    struct LNode *next;
}LNode,*LinkList;
```

LNode *p LinkList L

头插

= 指向（不要理解成赋

逆置

```c
LNode *p;
p=L->next;

L->next=NULL;
r=p->next;//重复

p->next=L->next;//
L->next=p;//

p=r;//
r=p->next;
p->next=L->next;
L->next=p;
p=r;
r=p->next;
```

```c
LNode* function(LinkList &L){
p=L->next;
L->next=NULL;
while(p存在){
    r=p->next;
    p->next=L->next;
    L->next=p;
    p=r;
}return L;}

```

```c
#include <stdio.h>
#include <stdlib.h>

typedef int ElemType;

typedef struct LNode {
    ElemType data;
    struct LNode *next;
} LNode, *LinkList;

// 你的函数逻辑（C语言版）
LNode* function(LinkList L) {
    LNode *p = L->next;
    L->next = NULL;

    while (p != NULL) {
        LNode *r = p->next;
        p->next = L->next;
        L->next = p;
        p = r;
    }

    return L;
}

// 创建链表（头插法）
void createList(LinkList *L, int arr[], int n) {
    *L = (LinkList)malloc(sizeof(LNode));
    (*L)->next = NULL;

    for (int i = 0; i < n; i++) {
        LNode *node = (LNode*)malloc(sizeof(LNode));
        node->data = arr[i];
        node->next = (*L)->next;
        (*L)->next = node;
    }
}

// 打印链表
void printList(LinkList L) {
    LNode *p = L->next;
    while (p != NULL) {
        printf("%d ", p->data);
        p = p->next;
    }
    printf("\n");
}

int main() {
    LinkList L;
    int arr[] = {1, 2, 3, 4, 5};
    int n = sizeof(arr) / sizeof(arr[0]);

    // 创建链表
    createList(&L, arr, n);

    printf("原链表: ");
    printList(L);

    // 调用你的函数
    function(L);

    printf("逆置后: ");
    printList(L);

    return 0;
}
```

```c
#include <stdio.h>
#include <stdlib.h>

typedef int ElemType;

typedef struct LNode {
    ElemType data;
    struct LNode *next;
} LNode, *LinkList;

// 1. 初始化链表（创建头节点）
LinkList InitList() {
    LinkList L = (LinkList)malloc(sizeof(LNode));
    if (L == NULL) {
        printf("内存分配失败！\n");
        return NULL;
    }
    L->next = NULL;
    return L;
}

// 2. 尾插法创建链表（与头插法不同）
void CreateList_Tail(LinkList L, int arr[], int n) {
    LNode *tail = L;  // 尾指针，初始指向头节点

    for (int i = 0; i < n; i++) {
        LNode *node = (LNode*)malloc(sizeof(LNode));
        if (node == NULL) {
            printf("内存分配失败！\n");
            return;
        }
        node->data = arr[i];
        node->next = NULL;     // 新节点next置为NULL

        tail->next = node;     // 尾节点的next指向新节点
        tail = node;           // 尾指针移动到新节点
    }
}

// 3. 查找节点（按值查找）
LNode* LocateElem(LinkList L, ElemType e) {
    LNode *p = L->next;
    while (p != NULL) {
        if (p->data == e) {
            return p;  // 找到返回节点地址
        }
        p = p->next;
    }
    return NULL;  // 未找到返回NULL
}

// 4. 插入节点（在第i个位置插入元素e）
int ListInsert(LinkList L, int i, ElemType e) {
    if (i < 1) {
        return 0;  // 位置无效
    }

    LNode *p = L;
    int j = 0;

    // 找到第i-1个节点
    while (p != NULL && j < i - 1) {
        p = p->next;
        j++;
    }

    if (p == NULL) {
        return 0;  // 位置超出范围
    }

    // 创建新节点
    LNode *node = (LNode*)malloc(sizeof(LNode));
    if (node == NULL) {
        printf("内存分配失败！\n");
        return 0;
    }
    node->data = e;

    // 插入节点
    node->next = p->next;
    p->next = node;

    return 1;  // 插入成功
}

// 5. 删除节点（删除第i个节点）
int ListDelete(LinkList L, int i, ElemType *e) {
    if (i < 1) {
        return 0;  // 位置无效
    }

    LNode *p = L;
    int j = 0;

    // 找到第i-1个节点
    while (p != NULL && j < i - 1) {
        p = p->next;
        j++;
    }

    if (p == NULL || p->next == NULL) {
        return 0;  // 位置超出范围
    }

    // 删除节点
    LNode *q = p->next;  // q是要删除的节点
    *e = q->data;        // 保存被删除元素的值
    p->next = q->next;   // 从链表中移除
    free(q);             // 释放内存

    return 1;  // 删除成功
}

// 6. 你的逆置函数
LinkList ReverseList(LinkList L) {
    if (L == NULL || L->next == NULL) {
        return L;
    }

    LNode *p = L->next;
    L->next = NULL;

    while (p != NULL) {
        LNode *r = p->next;
        p->next = L->next;
        L->next = p;
        p = r;
    }

    return L;
}

// 7. 打印链表
void PrintList(LinkList L) {
    LNode *p = L->next;
    while (p != NULL) {
        printf("%d ", p->data);
        p = p->next;
    }
    printf("\n");
}

// 8. 销毁链表
void DestroyList(LinkList L) {
    LNode *p = L;
    while (p != NULL) {
        LNode *temp = p;
        p = p->next;
        free(temp);
    }
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int n = sizeof(arr) / sizeof(arr[0]);

    printf("=== 链表操作演示 ===\n\n");

    // 1. 初始化链表
    printf("1. 初始化链表...\n");
    LinkList L = InitList();
    if (L == NULL) {
        return 1;
    }

    // 2. 尾插法创建链表
    printf("2. 尾插法创建链表: ");
    CreateList_Tail(L, arr, n);
    PrintList(L);
    printf("   说明：尾插法得到的链表顺序与输入一致：1 2 3 4 5\n\n");

    // 3. 查找节点
    printf("3. 查找节点:\n");
    int searchValue = 3;
    LNode *found = LocateElem(L, searchValue);
    if (found != NULL) {
        printf("   找到元素 %d 在链表中\n", searchValue);
    } else {
        printf("   未找到元素 %d\n", searchValue);
    }

    searchValue = 10;
    found = LocateElem(L, searchValue);
    if (found != NULL) {
        printf("   找到元素 %d 在链表中\n", searchValue);
    } else {
        printf("   未找到元素 %d\n", searchValue);
    }
    printf("\n");

    // 4. 插入节点
    printf("4. 插入节点:\n");
    printf("   在第3个位置插入元素99: ");
    if (ListInsert(L, 3, 99)) {
        PrintList(L);
    } else {
        printf("插入失败！\n");
    }

    printf("   在链表末尾插入元素100: ");
    // 先计算长度
    int length = 0;
    LNode *p = L->next;
    while (p != NULL) {
        length++;
        p = p->next;
    }
    if (ListInsert(L, length + 1, 100)) {
        PrintList(L);
    } else {
        printf("插入失败！\n");
    }
    printf("\n");

    // 5. 删除节点
    printf("5. 删除节点:\n");
    int deletedValue;
    printf("   删除第2个节点: ");
    if (ListDelete(L, 2, &deletedValue)) {
        printf("删除的元素值为: %d\n", deletedValue);
        PrintList(L);
    } else {
        printf("删除失败！\n");
    }
    printf("\n");

    // 6. 逆置链表
    printf("6. 逆置链表:\n");
    printf("   逆置前: ");
    PrintList(L);
    ReverseList(L);
    printf("   逆置后: ");
    PrintList(L);
    printf("\n");

    // 7. 再次插入和删除测试
    printf("7. 再次插入和删除测试:\n");
    printf("   插入元素77到头部: ");
    if (ListInsert(L, 1, 77)) {
        PrintList(L);
    }

    int temp;
    printf("   删除尾部节点: ");
    // 重新计算长度
    length = 0;
    p = L->next;
    while (p != NULL) {
        length++;
        p = p->next;
    }
   if (ListDelete(L, length, &temp)) {
        printf("删除的元素值为: %d\n", temp);
        PrintList(L);
    }
    printf("\n");

    // 8. 销毁链表
    printf("8. 销毁链表并释放内存...\n");
    DestroyList(L);

    printf("\n=== 演示结束 ===\n");

    return 0;
}
```

## 框架

| **类型**       | **定义**      | **访问成员** | **访问数据**    |
| -------------- | ------------- | ------------ | --------------- |
| **顺序表实体** | `SqList L;`   | `L.length`   | `L.data[i]`     |
| **顺序表指针** | `SqList *L;`  | `L->length`  | `L->data[i]`    |
| **链表头指针** | `LinkList L;` | `L->next`    | `L->next->data` |

### 顺序表

```c
#include <stdio.h>
#include <stdlib.h>

// --- 【1. 地基：结构定义】 ---
#define MaxSize 100
typedef struct {
    int data[MaxSize];
    int length;
} SqList;

// --- 【2. 地基：初始化】 ---
void InitList(SqList *L) {
    L->length = 0; // 只要把长度设为0，逻辑上表就空了
}

// --- 【3. 核心功能区：看题目要求填什么】 ---
// 比如题目要求插入、删除或合并
void MajorFunction(SqList *L, int x) {
    // 1. 判断合法性 (if L->length == MaxSize 等)

    // 2. 核心循环 (移动元素)
    // 插入往后挪：for(int j=L->length; j>=i; j--)
    // 删除往前挪：for(int j=i; j<L->length; j++)

    // 3. 修改长度 (L->length++ 或 L->length--)
}

// --- 【4. 辅助区：通常用来打印检查】 ---
void PrintList(SqList L) {
    for(int i=0; i<L.length; i++)
        printf("%d ", L.data[i]);
}

int main() {
    SqList L;
    InitList(&L);
    // 调用功能函数...
    return 0;
}
```



### 单链表

```c
#include <stdio.h>
#include <stdlib.h>

// --- 【1. 地基：结构定义】 ---
typedef struct LNode {
    int data;
    struct LNode *next;
} LNode, *LinkList;

// --- 【2. 地基：初始化（带头结点）】 ---
LinkList InitList() {
    LinkList L = (LNode*)malloc(sizeof(LNode)); // 申请头结点
    if (L != NULL) L->next = NULL;
    return L;
}

// --- 【3. 核心功能区：考什么填什么】 ---
// 老师提到的：逆置、插入、查找、删除
void SolveProblem(LinkList L) {
    LNode *p = L->next; // p指向第一个有效节点

    // 情况A：如果是遍历/查找/求和
    while (p != NULL) {
        // 做具体逻辑...
        p = p->next; // 必写：指针后移
    }

    // 情况B：如果是插入/删除
    // 需要找到目标位置的前驱节点 q
    // 插入：s->next = q->next; q->next = s;
    // 删除：temp = q->next; q->next = temp->next; free(temp);
}

// --- 【4. 进阶功能：创建表（老师提到过）】 ---
// 尾插法：永远在屁股后面加，需要一个尾指针 r
void CreateListTail(LinkList L, int n) {
    LNode *r = L; // r 始终指向当前的末尾
    for(int i=0; i<n; i++) {
        LNode *s = (LNode*)malloc(sizeof(LNode));
        scanf("%d", &s->data);
        r->next = s; // 把新节点接到尾巴上
        r = s;       // r 移动到新的尾巴上
    }
    r->next = NULL; // 尾巴封死
}

int main() {
    LinkList L = InitList();
    // 调用功能函数...
    return 0;
}
```

## 功能

### 顺序表

```c
// --- 功能1：插入元素 (在第 i 个位置插入 e) ---
// 注意：第 i 个位置对应的数组下标是 i-1
bool ListInsert(SqList *L, int i, int e) {
    if (i < 1 || i > L->length + 1) return false; // 检查位置是否合法
    if (L->length >= MaxSize) return false;      // 检查表是否已满

    // 核心逻辑：从后往前挪，腾出空间
    for (int j = L->length; j >= i; j--) {
        L->data[j] = L->data[j-1];//我站在空位上，伸手把前一个位置的数据拉过来
    }
    L->data[i-1] = e;  // 插入新元素,减掉前面的0，第 i 个位置对应的数组下标是 i-1
    L->length++;       // 长度加1
    return true;
}

// --- 功能2：删除元素 (删除第 i 个位置元素，并用 e 返回) ---
bool ListDelete(SqList *L, int i, int *e) {
    if (i < 1 || i > L->length) return false;    // 检查位置是否合法

    *e = L->data[i-1]; // 取出被删元素
    // 核心逻辑：从前往后挪，覆盖掉被删元素
    for (int j = i; j < L->length; j++) {
        L->data[j-1] = L->data[j];
    }
    L->length--;       // 长度减1
    return true;
}

// --- 功能3：按值查找 (返回对应的位置/序号) ---
int LocateElem(SqList L, int e) {
    for (int i = 0; i < L.length; i++) {
        if (L.data[i] == e) return i + 1; // 找到了，返回序号
    }
    return 0; // 没找到
}

// --- 功能4：删除重复元素 (作业题：针对有序顺序表) ---
void DeleteSame(SqList *L) {
    if (L->length == 0) return;
    int k = 0; // k 记录不重复序列的最后一位下标
    for (int i = 1; i < L->length; i++) {
        if (L->data[i] != L->data[k]) { // 发现新面孔
            k++;
            L->data[k] = L->data[i];    // 往前搬
        }
    }
    L->length = k + 1; // 更新长度
}
```



### 单链表

```c
// --- 功能1：查找 (按序号查找第 i 个节点) ---
LNode* GetElem(LinkList L, int i) {
    int j = 0;
    LNode *p = L; // 从头结点开始算第0个
    while (p != NULL && j < i) {
        p = p->next;
        j++;
    }
    return p; // 返回找到的节点指针（找不到返回NULL）
}

// --- 功能2：插入 (在第 i 个位置插入新元素 e) ---
bool ListInsert(LinkList L, int i, int e) {
    LNode *p = GetElem(L, i-1); // 1. 先找到第 i-1 个节点（前驱）
    if (p == NULL) return false;

    LNode *s = (LNode*)malloc(sizeof(LNode)); // 2. 申请新节点
    s->data = e;
    s->next = p->next; // 3. 核心：先连后手
    p->next = s;       // 4. 核心：再连前手
    return true;
}

// --- 功能3：删除 (删除第 i 个节点) ---
bool ListDelete(LinkList L, int i) {
    LNode *p = GetElem(L, i-1); // 1. 先找到前驱
    if (p == NULL || p->next == NULL) return false;

    LNode *q = p->next;    // 2. 标记被删节点
    p->next = q->next;     // 3. 核心：跨过去
    free(q);               // 4. 核心：释放内存
    return true;
}

// --- 功能4：逆置 (老师提到的重点：头插法原地逆置) ---
void ReverseList(LinkList L) {
    LNode *p = L->next;    // p指向第一个数据节点
    LNode *q;
    L->next = NULL;        // 先把头结点孤立出来

    while (p != NULL) {
        q = p->next;       // 临时保存 p 的后继
        p->next = L->next; // 将 p 头插到 L 后面
        L->next = p;
        p = q;             // 继续处理下一个节点
    }
}

// --- 功能5：创建表 (尾插法：考得比头插多) ---
void CreateListTail(LinkList L) {
    int x;
    LNode *r = L; // 尾指针
    while (scanf("%d", &x) && x != 999) { // 输入999结束
        LNode *s = (LNode*)malloc(sizeof(LNode));
        s->data = x;
        r->next = s; // 接到尾巴上
        r = s;       // 挪动尾指针
    }
    r->next = NULL;  // 别忘了最后封口
}
```

```c
void createList(LinkList *L, int arr[], int n) {
    *L = (LinkList)malloc(sizeof(LNode));
    (*L)->next = NULL;

    for (int i = 0; i < n; i++) {
        LNode *node = (LNode*)malloc(sizeof(LNode));
        node->data = arr[i];
        node->next = (*L)->next;
        (*L)->next = node;
    }
}
```

```c
// 3. 查找节点（按值查找）
LNode* LocateElem(LinkList L, ElemType e) {
    LNode *p = L->next;
    while (p != NULL) {
        if (p->data == e) {
            return p;  // 找到返回节点地址
        }
        p = p->next;
    }
    return NULL;  // 未找到返回NULL
}

// 4. 插入节点（在第i个位置插入元素e）
int ListInsert(LinkList L, int i, ElemType e) {
    if (i < 1) {
        return 0;  // 位置无效
    }

    LNode *p = L;
    int j = 0;

    // 找到第i-1个节点
    while (p != NULL && j < i - 1) {
        p = p->next;
        j++;
    }

    if (p == NULL) {
        return 0;  // 位置超出范围
    }

    // 创建新节点
    LNode *node = (LNode*)malloc(sizeof(LNode));
    if (node == NULL) {
        printf("内存分配失败！\n");
        return 0;
    }
    node->data = e;

    // 插入节点
    node->next = p->next;
    p->next = node;

    return 1;  // 插入成功
}

// 5. 删除节点（删除第i个节点）
int ListDelete(LinkList L, int i, ElemType *e) {
    if (i < 1) {
        return 0;  // 位置无效
    }

    LNode *p = L;
    int j = 0;

    // 找到第i-1个节点
    while (p != NULL && j < i - 1) {
        p = p->next;
        j++;
    }

    if (p == NULL || p->next == NULL) {
        return 0;  // 位置超出范围
    }

    // 删除节点
    LNode *q = p->next;  // q是要删除的节点
    *e = q->data;        // 保存被删除元素的值
    p->next = q->next;   // 从链表中移除
    free(q);             // 释放内存

    return 1;  // 删除成功
}

```

理解

```c
#include<stdio.h>
#include<stdlib.h>
typedef struct LNode{
    int data;
    struct LNode *next;
}LNode,*LinkList;

LinkList InitList{
    LinkList L=(*LNode)malloc(sizeof(LNode));
    L->next=NULL;
    return L;
}

int IsEmpty(LinkList L){
    return L->next=NULL;
}
int GetLength(LinkList L){
    int len=0;
    LNode *p=L->Next;
    while(p!=NULL){
        len++;
        p=p->next;
    }return len;
}

```

真

```c
#include <stdio.h>

#define MaxSize 50

typedef struct {
    int data[MaxSize];
    int length;
} SqList;

// 插入：在第 i 个位置插入 e
bool ListInsert(SqList *L, int i, int e) {
    if (i < 1 || i > L->length + 1) return false;
    if (L->length >= MaxSize) return false;
    for (int j = L->length; j >= i; j--) {
        L->data[j] = L->data[j - 1];
    }
    L->data[i - 1] = e;
    L->length++;
    return true;
}

// 删除：删除第 i 个位置元素并返回
bool ListDelete(SqList *L, int i, int &e) {
    if (i < 1 || i > L->length) return false;
    e = L->data[i - 1];
    for (int j = i; j < L->length; j++) {
        L->data[j - 1] = L->data[j];
    }
    L->length--;
    return true;
}

int main() {
    SqList L;
    L.length = 0; // 初始化长度

    // 插入几个数测试
    ListInsert(&L, 1, 10);
    ListInsert(&L, 2, 20);
    ListInsert(&L, 3, 30); // 现在是 {10, 20, 30}

    int deletedVal;
    if (ListDelete(&L, 2, deletedVal)) {
        printf("删除了第2个元素，值是: %d\n", deletedVal);
    }

    printf("当前顺序表内容: ");
    for (int i = 0; i < L.length; i++) {
        printf("%d ", L.data[i]);
    }
    return 0;
}
```

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct LNode {
    int data;
    struct LNode *next;
} LNode, *LinkList;

// 逆置：带头结点的单链表原地逆置
void Reverse(LinkList L) {
    LNode *p = L->next;
    LNode *q;
    L->next = NULL;
    while (p != NULL) {
        q = p->next;
        p->next = L->next; // 将p插入到头结点之后
        L->next = p;
        p = q;
    }
}

// 打印链表
void PrintList(LinkList L) {
    LNode *p = L->next;
    while (p != NULL) {
        printf("%d -> ", p->data);
        p = p->next;
    }
    printf("NULL\n");
}

int main() {
    // 1. 初始化带头结点的链表
    LinkList L = (LinkList)malloc(sizeof(LNode));
    L->next = NULL;

    // 2. 插入一些测试数据 (简单的头插)
    for (int i = 1; i <= 3; i++) {
        LNode *s = (LNode *)malloc(sizeof(LNode));
        s->data = i * 10;
        s->next = L->next;
        L->next = s;
    }
    printf("初始链表: ");
    PrintList(L); // 打印结果：30 -> 20 -> 10 -> NULL

    // 3. 执行逆置
    Reverse(L);
    printf("逆置后链表: ");
    PrintList(L); // 打印结果：10 -> 20 -> 30 -> NULL

    return 0;
}
```
