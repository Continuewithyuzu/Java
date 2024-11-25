---
description: >-
  参考https://programmercarl.com/kamacoder/%E5%9B%BE%E8%AE%BA%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html#%E8%BF%9E%E9%80%9A%E6%80%A7
---

# 图论

## 基本概念：

两点连成线，多个点连成的线就构成了图。

当然图也可以就一个节点，甚至没有节点（空图）

***

## 图的种类：

### 有向图

边有方向的图

### 无向图

边没有方向的图

### 加权有向图

图中边是有权值的

### 加权无向图

图中边无权值的

***

## 度 <a href="#du" id="du"></a>

无向图中有几条边连接该节点，该节点就有几度。

有向图有出度和入度的概念

出度：从该节点出发的边的个数。

入度：指向该节点边的个数。

***

## 连通性 <a href="#lian-tong-xing" id="lian-tong-xing"></a>

在图中表示节点的连通情况，我们称之为连通性。

### 连通图 <a href="#lian-tong-tu" id="lian-tong-tu"></a>

在无向图中，任何两个节点都是可以到达的，我们称之为连通图 ，如图：

<figure><img src="../.gitbook/assets/image.png" alt="" width="375"><figcaption></figcaption></figure>

如果有节点不能到达其他节点，则为非连通图，如图：

<figure><img src="../.gitbook/assets/image (1).png" alt="" width="375"><figcaption></figcaption></figure>

### 强连通图 <a href="#qiang-lian-tong-tu" id="qiang-lian-tong-tu"></a>

在有向图中，任何两个节点是可以相互到达的，我们称之为 强连通图。

我们来看这个有向图：

<figure><img src="../.gitbook/assets/image (2).png" alt="" width="375"><figcaption></figcaption></figure>

初步一看，好像这节点都连着呢，但这不是强连通图，节点1 可以到节点5，但节点5 不能到 节点1 。

强连通图是在有向图中**任何两个节点是可以相互到达**

下面这个有向图才是强连通图：

<figure><img src="../.gitbook/assets/image (3).png" alt="" width="375"><figcaption></figcaption></figure>

***

## 连通分量 <a href="#lian-tong-fen-liang" id="lian-tong-fen-liang"></a>

在无向图中的极大连通子图称之为该图的一个连通分量。

只看概念大家可能不理解，我来画个图：

<figure><img src="../.gitbook/assets/image (4).png" alt="" width="375"><figcaption></figcaption></figure>

该无向图中 节点1、节点2、节点5 构成的子图就是 该无向图中的一个连通分量，该子图所有节点都是相互可达到的。

同理，节点3、节点4、节点6 构成的子图 也是该无向图中的一个连通分量。

那么无向图中 节点3 、节点4 构成的子图 是该无向图的联通分量吗？

不是！

因为必须是极大联通子图才能是连通分量，所以 必须是节点3、节点4、节点6 构成的子图才是连通分量。

## 强连通分量 <a href="#qiang-lian-tong-fen-liang" id="qiang-lian-tong-fen-liang"></a>

在有向图中极大强连通子图称之为该图的强连通分量

<figure><img src="../.gitbook/assets/image (5).png" alt="" width="375"><figcaption></figcaption></figure>

节点1、节点2、节点3、节点4、节点5 构成的子图是强连通分量，因为这是强连通图，也是极大图。

节点6、节点7、节点8 构成的子图 不是强连通分量，因为这不是强连通图，节点8 不能达到节点6。

节点1、节点2、节点5 构成的子图 也不是 强连通分量，因为这不是极大图

***

## 图的构造 <a href="#tu-de-gou-zao" id="tu-de-gou-zao"></a>

我们如何用代码来表示一个图呢？

一般使用邻接表、邻接矩阵 或者用类来表示。

主要是 朴素存储、邻接表和邻接矩阵。

### 邻接矩阵 <a href="#lin-jie-ju-zhen" id="lin-jie-ju-zhen"></a>

邻接矩阵 使用 二维数组来表示图结构。 邻接矩阵是从节点的角度来表示图，有多少节点就申请多大的二维数组。

例如： grid\[2]\[5] = 6，表示 节点 2 连接 节点5 为有向图，节点2 指向 节点5，边的权值为6。

如果想表示无向图，即：grid\[2]\[5] = 6，grid\[5]\[2] = 6，表示节点2 与 节点5 相互连通，权值为6。

如图：

<figure><img src="../.gitbook/assets/image (6).png" alt="" width="375"><figcaption></figcaption></figure>

在一个 n （节点数）为8 的图中，就需要申请 8 \* 8 这么大的空间。

图中有一条双向边，即：grid\[2]\[5] = 6，grid\[5]\[2] = 6

这种表达方式（邻接矩阵） 在 边少，节点多的情况下，会导致申请过大的二维数组，造成空间浪费。

而且在寻找节点连接情况的时候，需要遍历整个矩阵，即 n \* n 的时间复杂度，同样造成时间浪费。

#### 邻接矩阵的优点：

* 表达方式简单，易于理解
* 检查任意两个顶点间是否存在边的操作非常快
* 适合稠密图，在边数接近顶点数平方的图中，邻接矩阵是一种空间效率较高的表示方法。

#### 缺点：

* 遇到稀疏图，会导致申请过大的二维数组造成空间浪费 且遍历 边 的时候需要遍历整个n \* n矩阵，造成时间浪费

### 邻接表 <a href="#lin-jie-biao" id="lin-jie-biao"></a>

邻接表 使用 数组 + 链表的方式来表示。 邻接表是从边的数量来表示图，有多少边 才会申请对应大小的链表。

邻接表的构造如图：

<figure><img src="../.gitbook/assets/image (7).png" alt="" width="375"><figcaption></figcaption></figure>

这里表达的图是：

* 节点1 指向 节点3 和 节点5
* 节点2 指向 节点4、节点3、节点5
* 节点3 指向 节点4
* 节点4指向节点1

有多少`边`，邻接表才会申请多少个对应的链表节点。

从图中可以直观看出 使用 数组 + 链表 来表达 边的连接情况 。

邻接表的优点：

* 对于稀疏图的存储，`只需要存储边`，空间利用率高
* 遍历节点连接情况相对容易

缺点：

* 检查任意两个节点间是否存在边，效率相对低，需要 O(V)时间，V表示某节点连接其他节点的数量。
* 实现相对复杂，不易理解

***

## 图的遍历方式 <a href="#tu-de-bian-li-fang-shi" id="tu-de-bian-li-fang-shi"></a>

图的遍历方式基本是两大类：

* 深度优先搜索（dfs）
* 广度优先搜索（bfs）

在讲解二叉树章节的时候，其实就已经讲过这两种遍历方式。

二叉树的递归遍历，是dfs 在二叉树上的遍历方式。

二叉树的层序遍历，是bfs 在二叉树上的遍历方式。

dfs 和 bfs 一种搜索算法，可以在不同的数据结构上进行搜索，在二叉树章节里是在二叉树这样的数据结构上搜索。

而在图论章节，则是在图（邻接表或邻接矩阵）上进行搜索。

