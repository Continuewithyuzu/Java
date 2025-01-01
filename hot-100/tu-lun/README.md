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

<figure><img src="../../.gitbook/assets/image (7).png" alt="" width="375"><figcaption></figcaption></figure>

如果有节点不能到达其他节点，则为非连通图，如图：

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

### 强连通图 <a href="#qiang-lian-tong-tu" id="qiang-lian-tong-tu"></a>

在有向图中，任何两个节点是可以相互到达的，我们称之为 强连通图。

我们来看这个有向图：

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

初步一看，好像这节点都连着呢，但这不是强连通图，节点1 可以到节点5，但节点5 不能到 节点1 。

强连通图是在有向图中**任何两个节点是可以相互到达**

下面这个有向图才是强连通图：

<figure><img src="../../.gitbook/assets/image (3) (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

***

## 连通分量 <a href="#lian-tong-fen-liang" id="lian-tong-fen-liang"></a>

在无向图中的极大连通子图称之为该图的一个连通分量。

只看概念大家可能不理解，我来画个图：

<figure><img src="../../.gitbook/assets/image (4) (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

该无向图中 节点1、节点2、节点5 构成的子图就是 该无向图中的一个连通分量，该子图所有节点都是相互可达到的。

同理，节点3、节点4、节点6 构成的子图 也是该无向图中的一个连通分量。

那么无向图中 节点3 、节点4 构成的子图 是该无向图的联通分量吗？

不是！

因为必须是极大联通子图才能是连通分量，所以 必须是节点3、节点4、节点6 构成的子图才是连通分量。

## 强连通分量 <a href="#qiang-lian-tong-fen-liang" id="qiang-lian-tong-fen-liang"></a>

在有向图中极大强连通子图称之为该图的强连通分量

<figure><img src="../../.gitbook/assets/image (5) (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

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

<figure><img src="../../.gitbook/assets/image (6) (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

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

<figure><img src="../../.gitbook/assets/image (7) (1).png" alt="" width="375"><figcaption></figcaption></figure>

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

### dfs 与 bfs 区别

提到深度优先搜索（dfs），就不得不说和广度优先搜索（bfs）有什么区别

先来了解dfs的过程，很多录友可能对dfs（深度优先搜索），bfs（广度优先搜索）分不清。

先给大家说一下两者大概的区别：

* dfs是可一个方向去搜，不到黄河不回头，直到遇到绝境了，搜不下去了，再换方向（换方向的过程就涉及到了回溯）。
* bfs是先把本节点所连接的所有节点遍历一遍，走到下一个节点的时候，再把连接节点的所有节点遍历一遍，搜索方向更像是广度，四面八方的搜索过程。

### dfs 搜索过程 <a href="#dfs-sou-suo-guo-cheng" id="dfs-sou-suo-guo-cheng"></a>

上面说道dfs是可一个方向搜，不到黄河不回头。 那么我们来举一个例子。

如图一，是一个无向图，我们要搜索从节点1到节点6的所有路径。

<figure><img src="../../.gitbook/assets/image (6).png" alt="" width="375"><figcaption></figcaption></figure>

那么dfs搜索的第一条路径是这样的： （假设第一次延默认方向，就找到了节点6），图二

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

此时我们找到了节点6，（遇到黄河了，是不是应该回头了），那么应该再去搜索其他方向了。 如图三：

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt="" width="375"><figcaption></figcaption></figure>

路径2撤销了，改变了方向，走路径3（红色线）， 接着也找到终点6。 那么撤销路径2，改为路径3，在dfs中其实就是回溯的过程（这一点很重要，很多录友不理解dfs代码中回溯是用来干什么的）

又找到了一条从节点1到节点6的路径，又到黄河了，此时再回头，下图图四中，路径4撤销（回溯的过程），改为路径5。

<figure><img src="../../.gitbook/assets/image (3) (1).png" alt="" width="375"><figcaption></figcaption></figure>



又找到了一条从节点1到节点6的路径，又到黄河了，此时再回头，下图图五，路径6撤销（回溯的过程），改为路径7，路径8 和 路径7，路径9， 结果发现死路一条，都走到了自己走过的节点

<figure><img src="../../.gitbook/assets/image (4) (1).png" alt="" width="563"><figcaption></figcaption></figure>

那么节点2所连接路径和节点3所链接的路径 都走过了，撤销路径只能向上回退，去选择撤销当初节点4的选择，也就是撤销路径5，改为路径10 。 如图图六：

<figure><img src="../../.gitbook/assets/image (5) (1).png" alt="" width="375"><figcaption></figcaption></figure>

\
上图演示中，其实我并没有把 所有的 从节点1 到节点6的dfs（深度优先搜索）的过程都画出来，那样太冗余了，但 已经把dfs 关键的地方都涉及到了，关键就两点：

* 搜索方向，是认准一个方向搜，直到碰壁之后再换方向
* 换方向是撤销原路径，改为节点链接的下一个路径，回溯的过程。

### 代码框架 <a href="#dai-ma-kuang-jia" id="dai-ma-kuang-jia"></a>

正是因为dfs搜索可一个方向，并需要回溯，所以用递归的方式来实现是最方便的。

很多录友对回溯很陌生，建议先看看代码随想录，[回溯算法章节](https://programmercarl.com/%E5%9B%9E%E6%BA%AF%E7%AE%97%E6%B3%95%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html)。

有递归的地方就有回溯，那么回溯在哪里呢？

就递归函数的下面，例如如下代码：

```
void dfs(参数) {
    处理节点
    dfs(图，选择的节点); // 递归
    回溯，撤销处理结果
}
```

可以看到回溯操作就在递归函数的下面，递归和回溯是相辅相成的。

在讲解[二叉树章节](https://programmercarl.com/%E4%BA%8C%E5%8F%89%E6%A0%91%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html)的时候，二叉树的递归法其实就是dfs，而二叉树的迭代法，就是bfs（广度优先搜索）

所以**dfs，bfs其实是基础搜索算法，也广泛应用与其他数据结构与算法中**。

我们在回顾一下[回溯法](https://programmercarl.com/%E5%9B%9E%E6%BA%AF%E7%AE%97%E6%B3%95%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html)的代码框架：

```java
void backtracking(参数) {
    if (终止条件) {
        存放结果;
        return;
    }
    for (选择：本层集合中元素（树中节点孩子的数量就是集合的大小）) {
        处理节点;
        backtracking(路径，选择列表); // 递归
        回溯，撤销处理结果
    }
}
```

回溯算法，其实就是dfs的过程，这里给出dfs的代码框架：

```java
void dfs(参数) {
    if (终止条件) {
        存放结果;
        return;
    }

    for (选择：本节点所连接的其他节点) {
        处理节点;
        dfs(图，选择的节点); // 递归
        回溯，撤销处理结果
    }
}
```

可以发现dfs的代码框架和回溯算法的代码框架是差不多的。

下面用 深搜三部曲，来解读 dfs的代码框架

***

### 深搜三部曲 <a href="#shen-sou-san-bu-qu" id="shen-sou-san-bu-qu"></a>

在 [二叉树递归讲解](https://programmercarl.com/%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E9%80%92%E5%BD%92%E9%81%8D%E5%8E%86.html)中，给出了递归三部曲。

[回溯算法](https://programmercarl.com/%E5%9B%9E%E6%BA%AF%E7%AE%97%E6%B3%95%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html)讲解中，给出了 回溯三部曲。

其实深搜也是一样的，深搜三部曲如下：

1. 确认递归函数，参数

```java
void dfs(参数)
```

通常我们递归的时候，我们递归搜索需要了解哪些参数，其实也可以在写递归函数的时候，发现需要什么参数，再去补充就可以。

一般情况，深搜需要 二维数组数组结构保存所有路径，需要一维数组保存单一路径，这种保存结果的数组，我们可以定义一个全局变量，避免让我们的函数参数过多。

例如这样：

```cpp
vector<vector<int>> result; // 保存符合条件的所有路径
vector<int> path; // 起点到终点的路径
void dfs (图，目前搜索的节点)  
```

但这种写法看个人习惯，不强求。

2. 确认终止条件

终止条件很重要，很多同学写dfs的时候，之所以容易死循环，栈溢出等等这些问题，都是因为终止条件没有想清楚。

```java
if (终止条件) {
    存放结果;
    return;
}
```

终止添加不仅是结束本层递归，同时也是我们收获结果的时候。

另外，其实很多dfs写法，没有写终止条件，其实终止条件写在了， 下面dfs递归的逻辑里了，也就是不符合条件，直接不会向下递归。这里如果大家不理解的话，没关系，后面会有具体题目来讲解。

3. 处理目前搜索节点出发的路径

一般这里就是一个for循环的操作，去遍历 目前搜索节点 所能到的所有节点。

```java
for (选择：本节点所连接的其他节点) {
    处理节点;
    dfs(图，选择的节点); // 递归
    回溯，撤销处理结果
}
```

不少录友疑惑的地方，都是 dfs代码框架中for循环里分明已经处理节点了，那么 dfs函数下面 为什么还要撤销的呢。

如图七所示， 路径2 已经走到了 目的地节点6，那么 路径2 是如何撤销，然后改为 路径3呢？ 其实这就是 回溯的过程，撤销路径2，走换下一个方向。

<figure><img src="../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>



## 广度优先搜索（bfs）理论基础 <a href="#guang-du-you-xian-sou-suo-li-lun-ji-chu" id="guang-du-you-xian-sou-suo-li-lun-ji-chu"></a>

广搜（bfs）是一圈一圈的搜索过程，和深搜（dfs）是一条路跑到黑然后再回溯。

### 广搜的使用场景 <a href="#guang-sou-de-shi-yong-chang-jing" id="guang-sou-de-shi-yong-chang-jing"></a>

广搜的搜索方式就适合于解决两个点之间的最短路径问题。

因为广搜是从起点出发，以起始点为中心一圈一圈进行搜索，一旦遇到终点，记录之前走过的节点就是一条最短路。

当然，也有一些问题是广搜 和 深搜都可以解决的，例如岛屿问题，**这类问题的特征就是不涉及具体的遍历方式，只要能把相邻且相同属性的节点标记上就行**。 （我们会在具体题目讲解中详细来说）

### 广搜的过程 <a href="#guang-sou-de-guo-cheng" id="guang-sou-de-guo-cheng"></a>

上面我们提过，BFS是一圈一圈的搜索过程，但具体是怎么一圈一圈来搜呢。

我们用一个方格地图，假如每次搜索的方向为 上下左右（不包含斜上方），那么给出一个start起始位置，那么BFS就是从四个方向走出第一步。

<figure><img src="../../.gitbook/assets/image (50).png" alt="" width="344"><figcaption></figcaption></figure>

如果加上一个end终止位置，那么使用BFS的搜索过程如图所示：

<figure><img src="../../.gitbook/assets/image (51).png" alt="" width="375"><figcaption></figcaption></figure>

我们从图中可以看出，从start起点开始，是一圈一圈，向外搜索，方格编号1为第一步遍历的节点，方格编号2为第二步遍历的节点，第四步的时候我们找到终止点end。

正是因为BFS一圈一圈的遍历方式，所以一旦遇到终止点，那么一定是一条最短路径。

<mark style="background-color:blue;">**只要BFS只要搜到终点一定是一条最短路径**</mark>

### 代码框架 <a href="#dai-ma-kuang-jia" id="dai-ma-kuang-jia"></a>

大家应该好奇，这一圈一圈的搜索过程是怎么做到的，是放在什么容器里，才能这样去遍历。

很多网上的资料都是直接说用队列来实现。

其实，我们**仅仅需要一个容器**，能保存我们要遍历过的元素就可以，**那么用队列，还是用栈，甚至用数组，都是可以的**。

**用队列的话，就是保证每一圈都是一个方向去转，例如统一顺时针或者逆时针**。

因为队列是先进先出，加入元素和弹出元素的顺序是没有改变的。

**如果用栈的话，就是第一圈顺时针遍历，第二圈逆时针遍历，第三圈有顺时针遍历**。

因为栈是先进后出，加入元素和弹出元素的顺序改变了。

那么广搜需要注意 转圈搜索的顺序吗？ 不需要！

所以用队列，还是用栈都是可以的，但大家都习惯用队列了，**所以下面的讲解用我也用队列来讲，只不过要给大家说清楚，并不是非要用队列，用栈也可以**。

下面给出广搜代码模板，该模板针对的就是，上面的四方格的地图： （详细注释）（C++）

```cpp
int dir[4][2] = {0, 1, 1, 0, -1, 0, 0, -1}; // 表示四个方向
// grid 是地图，也就是一个二维数组
// visited标记访问过的节点，不要重复访问
// x,y 表示开始搜索节点的下标
void bfs(vector<vector<char>>& grid, vector<vector<bool>>& visited, int x, int y) {
    queue<pair<int, int>> que; // 定义队列
    que.push({x, y}); // 起始节点加入队列
    visited[x][y] = true; // 只要加入队列，立刻标记为访问过的节点
    while(!que.empty()) { // 开始遍历队列里的元素
        pair<int ,int> cur = que.front(); que.pop(); // 从队列取元素
        int curx = cur.first;
        int cury = cur.second; // 当前节点坐标
        for (int i = 0; i < 4; i++) { // 开始想当前节点的四个方向左右上下去遍历
            int nextx = curx + dir[i][0];
            int nexty = cury + dir[i][1]; // 获取周边四个方向的坐标
            if (nextx < 0 || nextx >= grid.size() || nexty < 0 || nexty >= grid[0].size()) continue;  // 坐标越界了，直接跳过
            if (!visited[nextx][nexty]) { // 如果节点没被访问过
                que.push({nextx, nexty});  // 队列添加该节点为下一轮要遍历的节点
                visited[nextx][nexty] = true; // 只要加入队列立刻标记，避免重复访问
            }
        }
    }

}
```

