---
description: 说到二叉树，就不得不说递归，很多同学对递归都是又熟悉又陌生，递归的代码一般很简短，但每次都是一看就会，一写就废。
---

# 二叉树

## 树

### 树是一种非线性的数据结构，它是由n个(n>=0)个有限节点组成一个具有层次关系的集合。它的形状像一颗倒挂的树，根在上，叶在下。



### 特点：

· 有一个特殊的结点称为根节点，根节点没有前驱结点

· 除根节点外，其余结点被分成M(M>0)个互不相交的集合T1,T2,.....,Tm，其中每一个集合又是一颗与树类似的字树。每棵子树的根节点有且只有一个前驱，可以没有或者多个后继

· 树是递归定义的

注意：在树形结构中，子树不能有交集，否则就不是树形结构&#x20;



### 重要概念：

一个N个节点的树有N-1条边

结点的度：一个结点含有子树的个数

树的度：<mark style="color:blue;">所有结点的度的最大值称为树的度</mark>

叶子结点或终端结点：<mark style="color:blue;">度为0的结点</mark>

双亲结点或父亲结点：若一个结点含有子节点，则这个结点为其子结点的双亲结点

孩子结点或子结点：一个结点含有的子树的根结点称为该结点的子结点

根结点：<mark style="color:blue;">树中没有双亲结点的结点</mark>

结点的层次：从根开始定义，根为第一层，根的子结点为第二层，以此类推

树的高度或深度：树中结点层次的最大值

森林：由m(m>0)棵互不相交的树组成的集合称为森林&#x20;



### 性质

* 节点数=分支数+1
* 度为k的树第i层上最多有k^（i-1）个节点
* 高度为H的K叉树最多有(k^h-1)/(k-1)个节点



### 表示形式：孩子兄弟表示法

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>孩子兄弟表示法示意图</p></figcaption></figure>

```java
class Node{
    int val;          //存储的数据
    Node firstChild;  // 第一个孩子引用,一般称之为左结点，Node left
    Node nextBrother;   //下一个兄弟引用,一般称之为右结点，Node right
}
```

***

## 二叉树

二叉树是一个有限的集合，该集合为空，或者是由一个根节点和两颗子树构成，分别为左子树和右子树，只含<mark style="color:blue;">有一个根节点的也可也称为二叉树。</mark>

* 二叉树不存在度大于2的节点
* 二叉树的子树有左右之分
* 每个子树的根节点往下都可看作一个新的二叉树
* 空树和只有一个节点的树都可以称为二叉树
* 根节点只有左树（或右树）并满足节点度不大于2的情况下，也是二叉树

### 二叉树的性质（重点，选择题常考）

性质1: 如果规定根节点的层数为1，那么一颗非空的二叉树的第 k 层上最多有 2^(k-1) 个节点 k>0。

性质2: 如果规定只有根节点的二叉树的深度为 1，则深度为 k 的二叉树的最大节点数是 2^k - 1（k >= 0）。

性质3: 对于任何一棵二叉树，如果叶子(度为0)节点的个数为 n0，度为2的非叶子节点的个数为 n2，则 n0 = n2 + 1。

性质4: 具有 n 个节点的完全二叉树的深度 k 为 log(n+1) 上取整。（以2为底）

性质5: 对于具有<mark style="color:blue;">n个节点的完全二叉树</mark>，如果从上至下，从左至右的顺序对所有的节点从 0 开始进行编号，<mark style="color:blue;">如果父节点下标为 i，左孩子节点下标为：2 \* i + 1 且 < n，右孩子下标为：2 \* i + 2 且 < n</mark>，已知孩子节点下标，求父节点：(i - 1) / 2 = 父节点下标，若 i = 0，则 i 为根节点编号。 4

***

## 满二叉树

如果一棵二叉树只有度为0的结点和度为2的结点，并且度为0的结点在同一层上，则这棵二叉树为满二叉树。**换句话说，如果一颗二叉树的层数为k，且总结点的个数是2^k-1，那么就是满二叉树.**

<figure><img src="../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

***

## 完全二叉树

在完全二叉树中，除了最底层节点可能没填满外，其余每层节点数都达到最大值，并且最下面一层的节点都集中在该层最左边的若干位置。若最底层为第 h 层（h从1开始），则该层包含 1\~ 2^(h-1) 个节点。它是一种效率很高的数据结构，完全二叉树是由满二叉树引出来的。对于深度为k，有n个结点的二叉树，当且仅当每一个结点都与深度为k的满二叉树中编号从0至n-1的结点一一对应时称之为完全二叉树，**满二叉树是一种特殊的完全二叉树。**

<figure><img src="../../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

**优先级队列其实是一个堆，堆就是一棵完全二叉树，同时保证父子节点的顺序关系。**

***

## 二叉搜索树 <a href="#er-cha-sou-suo-shu" id="er-cha-sou-suo-shu"></a>

前面介绍的树，都没有数值的，而二叉搜索树是有数值的了，**二叉搜索树是一个有序树**。

* 若它的左子树不空，则左子树上所有结点的值均小于它的根结点的值；
* 若它的右子树不空，则右子树上所有结点的值均大于它的根结点的值；
* 它的左、右子树也分别为二叉排序树

<figure><img src="../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

***

## 平衡二叉搜索树 <a href="#ping-heng-er-cha-sou-suo-shu" id="ping-heng-er-cha-sou-suo-shu"></a>

平衡二叉搜索树：又被称为AVL（Adelson-Velsky and Landis）树，且具有以下性质：它是一棵空树或它的左右两个子树的高度差的绝对值不超过1，并且左右两个子树都是一棵平衡二叉树。

<figure><img src="../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

## 二叉树的存储方式 <a href="#er-cha-shu-de-cun-chu-fang-shi" id="er-cha-shu-de-cun-chu-fang-shi"></a>

### **二叉树可以链式存储，也可以顺序存储。**

那么链式存储方式就用<mark style="color:blue;">指针</mark>， 顺序存储的方式就是用<mark style="color:blue;">数组</mark>。

顾名思义就是顺序存储的元素在<mark style="color:blue;">内存是连续分布</mark>的，而链式存储则是通过指针把分布在各个地址的节点串联一起

#### 链式存储：

<figure><img src="../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

#### 顺序存储：

<figure><img src="../../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

**如果父节点的数组下标是 i，那么它的左孩子就是 i \* 2 + 1，右孩子就是 i \* 2 + 2。**

但是用链式表示的二叉树，更有利于我们理解，所以一般我们都是用链式存储二叉树。

***

## 二叉树主要有两种遍历方式：

1. 深度优先遍历：先往深走，遇到叶子节点再往回走。
2. 广度优先遍历：一层一层的去遍历。

**这两种遍历是图论中最基本的两种遍历方式**，后面在介绍图论的时候 还会介绍到。

从深度优先遍历和广度优先遍历进一步拓展，才有如下遍历方式：

* 深度优先遍历
  * 前序遍历（递归法，迭代法）NLR 每次访问<mark style="color:blue;">直接打印根节点</mark>
  * 中序遍历（递归法，迭代法）LNR <mark style="color:blue;">左子树走完返回</mark>才打印根节点
  * 后序遍历（递归法，迭代法）LRN <mark style="color:blue;">左右子树都走完</mark>返回才打印根节点
* 广度优先遍历
  * 层次遍历（迭代法）

在深度优先遍历中：有三个顺序，前中后序遍历，技巧：

<figure><img src="../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

广度优先遍历的实现一般使用队列来实现，这也是队列先进先出的特点所决定的，因为需要先进先出的结构，才能一层一层的来遍历二叉树



定义二叉树代码：

```java
public class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;

    TreeNode() {}
    TreeNode(int val) { this.val = val; }
    TreeNode(int val, TreeNode left, TreeNode right) {
        this.val = val;
        this.left = left;
        this.right = right;
    }
}
```

相比链表，多了一个指针，分别指向左右孩子。

***

## 递归法前中后序遍历

### 原理：

```java
// 前序遍历·递归·LC144_二叉树的前序遍历
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<Integer>();
        preorder(root, result);
        return result;
    }

    public void preorder(TreeNode root, List<Integer> result) {
        if (root == null) {
            return;
        }
        result.add(root.val);
        preorder(root.left, result);
        preorder(root.right, result);
    }
}
// 中序遍历·递归·LC94_二叉树的中序遍历
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        inorder(root, res);
        return res;
    }

    void inorder(TreeNode root, List<Integer> list) {
        if (root == null) {
            return;
        }
        inorder(root.left, list);
        list.add(root.val);             // 注意这一句
        inorder(root.right, list);
    }
}
// 后序遍历·递归·LC145_二叉树的后序遍历
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        postorder(root, res);
        return res;
    }

    void postorder(TreeNode root, List<Integer> list) {
        if (root == null) {
            return;
        }
        postorder(root.left, list);
        postorder(root.right, list);
        list.add(root.val);             // 注意这一句
    }
}
```

### 递归法实际应用：

```java
// 前序遍历 -> 根 左子树 右子树
public void preOrder(TreeNode root) {
    if (root == null) {
        return;
    }
    // 碰到根节点就打印
    System.out.print(root.val + " ");
    // 遍历左子树
    preOrder(root.left);
    // 遍历右子树
    preOrder(root.right);
}
 
// 中序遍历 -> 左子树 根 右子树
public void inOrder(TreeNode root) {
    if (root == null) {
        return;
    }
    // 遍历左子树
    inOrder(root.left);
    // 打印根节点
    System.out.print(root.val + " ");
    // 遍历右子树
    inOrder(root.right);
}
 
// 后序遍历 -> 左子树 右子树 根
public void postOrder(TreeNode root) {
    if (root == null) {
        return;
    }
    // 遍历左子树
    postOrder(root.left);
    // 遍历右子树
    postOrder(root.right);
    // 打印根节点
    System.out.print(root.val + " ");
}
```

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

***

## 迭代遍历

**递归的实现就是：每一次递归调用都会把函数的局部变量、参数值和返回地址等压入调用栈中**，然后递归返回的时候，从栈顶弹出上一次递归的各项参数，所以这就是递归为什么可以返回上一层位置的原因。

所以用栈也可以实现二叉树的前后中序遍历

```java
// 前序遍历顺序：中-左-右，入栈顺序：中-右-左
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null){
            return result;
        }
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        while (!stack.isEmpty()){
            TreeNode node = stack.pop();
            result.add(node.val);
            if (node.right != null){
                stack.push(node.right);
            }
            if (node.left != null){
                stack.push(node.left);
            }
        }
        return result;
    }
}

// 中序遍历顺序: 左-中-右 入栈顺序： 左-右
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null){
            return result;
        }
        Stack<TreeNode> stack = new Stack<>();
        TreeNode cur = root;
        while (cur != null || !stack.isEmpty()){
           if (cur != null){
               stack.push(cur);
               cur = cur.left;
           }else{
               cur = stack.pop();
               result.add(cur.val);
               cur = cur.right;
           }
        }
        return result;
    }
}

// 后序遍历顺序 左-右-中 入栈顺序：中-左-右 出栈顺序：中-右-左， 最后翻转结果
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null){
            return result;
        }
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        while (!stack.isEmpty()){
            TreeNode node = stack.pop();
            result.add(node.val);
            if (node.left != null){
                stack.push(node.left);
            }
            if (node.right != null){
                stack.push(node.right);
            }
        }
        Collections.reverse(result);
        return result;
    }
}
```

***

## 层序遍历

采用非递归的方式：定义一个队列，先将根节点入队，**如果队列不为空，弹出一个队头元素并打印，接着再去看看它左树和右树的根节点是否为空，如果不会空都入队，**&#x91CD;复上述操作，当队列为空时，层序遍历结束。

示意图：

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

```java
//层序遍历
 public void levelOrder(TreeNode root){
        if(root==null){
            return;      //根为空直接返回
        }
        Queue<BTNode> q = new LinkedList<>();
        q.offer(root);    //先将根入队列    
        while(!q.isEmpty()){      //队列不为空时，循环
            BTNode cur = q.poll();   //根出队列
            System.out.print(cur.val+" ");
            if(cur.left!=null){     //根有左子树，将左子树的根入队列
                q.offer(cur.left);
            }
            if(cur.right!=null){    //根有右子树，将右子树的根入队列
                q.offer(cur.right);
            }
        }
        System.out.println();
    }
    
```

***

## **获取二叉树中结点的个数**

二叉树结点的个数=根的左子树结点的个数+根的右子树结点的个数+1（这个1就是根节点本身），所以直接一个<mark style="color:blue;">递归</mark>就解决问题了

```java
public int size(TreeNode root){
    if(root==null){
        return 0;
    }
    return 1+size(root.left)+size(root.right);
}
```

遍历思想：

```java
public int usedSize; 
public int size(TreeNode root){
    if (root == null) {
        return;
    }
    usedSize++;
    size(root.left);
    size(root.right);
}
```

***

## 获取二叉树中<mark style="color:blue;">叶子结点</mark>的个数

叶子结点就是该结点的左子树为空，右子树为空，所以当遇到此节点时返回1，递归返回所有该结点的总数

```java
public int getLeafNode(TreeNode root){
        if(root==null){
            return 0;
        }
        if(root.left == null && root.right == null){
            return 1;
        }
        return getLeafNode(root.left)+getLeafNode(root.right);
    }
```

***

## **获取二叉树中第k层结点的个数**

**求第k层节点的个数,我们可以用子问题的思想去求,分别去求它左右子树k-1层的节点个数即可**

```java
 public int getLevelNode(TreeNode root,int k){
        if(root==null||k<0){  //判断参数
            return 0;
        }
        if(k==1){        //如果k==1，则只有根返回1
            return 1;
        }
        //递归
        return getLevelNode(root.left,k-1) + getLevelNode(root.right,k-1);
    }
```

<figure><img src="../../.gitbook/assets/image (4) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

```java
 public int getLevelNode(TreeNode root,int k){
        if(root==null||k<0){  //判断参数
            return 0;
        }
        if(k==1){        //如果k==1，则只有根返回1
            return 1;
        }
        //递归
        return getLevelNode(root.left,k-1) + getLevelNode(root.right,k-1);
    }
```

***

## [**获取二叉树的高度**](104-qiu-er-cha-shu-de-zui-da-shen-du.md)&#x20;

**将此二叉树的左子树的高度与右子树的高度进行比较，较大的高度+1就是此二叉树的高度**

```java
 public int height(TreeNode root){
        if(root==null){
            return 0;
        }
        int leftHeight = height(root.left);
        int rightHeight = height(root.right);
        return (Math.max(leftHeight,rightHeight)+1);
    }
```

***

## **查找值为val的结点并返回**

先递归在左子树中找，再递归在右子树中找

```java
public BTNode find(TreeNode root,int val){
        if(root==null){
            return null;
        }
        if(root.val == val){
            return root;
        }
        BTNode leftTree = find(root.left,val); //递归在左子树中找
        if(leftTree != null){
            return leftTree;     //找到了返回
        }
        BTNode rightTree = find(root.right,val);   //递归在右子树中找
        if(rightTree != null) {
            return rightTree;
        }
        return null;
    }
```

***

## **判断一棵树是否为完全二叉树（重点，常考）**

利用完全二叉树的性质, 如果中间下标位置的结点有空缺, 说明不是完全二叉树

所以对这棵树进行层序遍历, 利用队列这种数据结构, 根节点入队, 当队列不为空时进入循环, 出队一次, 并让它的左右孩子结点入队(队列可以offer(null), 优先级队列不可以), 出队时遇见 null, 退出循环

退出循环后检查队列中剩余数据是否还有非空数据, 如果存在非空数据说明不是完全二叉树

<figure><img src="../../.gitbook/assets/image (5) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

```java
public boolean isCompleteTree(TreeNode root) {
    // 如果根节点为空，则返回 true，表示空树也是完全二叉树
    if (root == null) {
        return true;
    }
    
    // 创建一个队列，用于存储待处理的节点
    Queue<TreeNode> queue = new LinkedList<>();
    
    // 将根节点加入队列
    queue.offer(root);
    
    // 当队列不为空时，说明还有节点需要处理
    while (!queue.isEmpty()) {
        // 弹出队列中的一个节点
        TreeNode cur = queue.poll();
        
        // 如果当前节点不为空
        if (cur != null) {
            // 将当前节点的左孩子和右孩子加入队列
            queue.offer(cur.left);
            queue.offer(cur.right);
        } else {
            // 如果当前节点为空，说明已经遍历到了完全二叉树的边界，退出循环
            break;
        }
    }
    
    // 在遍历完所有节点后，检查队列中剩余的节点是否都为空
    while (!queue.isEmpty()) {
        // 弹出队列中的一个节点
        TreeNode tmp = queue.poll();
        
        // 如果队列中有非空节点，说明这棵树不是完全二叉树，返回 false
        if (tmp != null) {
            return false;
        }
    }
    
    // 如果队列中所有节点都为空，说明这棵树是完全二叉树，返回 true
    return true;
}
```

***

## 什么是平衡二叉搜索树?

二叉搜索树（Binary Search Tree，简称BST）是一种二叉树的数据结构，其中每个节点最多有两个子节点，分别是左子节点和右子节点。二叉搜索树具有以下性质：

1. **左子树节点小于父节点**：在任何一个节点上，左子树中的所有节点的值都小于该节点的值。
2. **右子树节点大于父节点**：在任何一个节点上，右子树中的所有节点的值都大于该节点的值。
3. **子树也是二叉搜索树**：每个节点的左、右子树也必须是二叉搜索树。

这种结构的特性使得二叉搜索树非常适合进行快速的查找、插入和删除操作。典型情况下，在平衡的二叉搜索树中，查找、插入和删除的时间复杂度为`O(logn)`。



### 如何由数组生成？

* **对数组进行排序**：首先，确保数组是有序的，因为二叉搜索树的性质要求左子树的节点小于根节点，而右子树的节点大于根节点。若数组未排序，先对其排序。
* **选择中间元素作为根节点**：递归地将中间元素作为根节点，以此保证树的平衡。将数组的中间元素选作根节点，可以让左半部分成为左子树，右半部分成为右子树。
* **递归构建子树**：对左半部分数组和右半部分数组分别重复这个过程，继续选择中间元素作为子树的根节点，直到数组为空。
* [例题](108-jiang-you-xu-shu-zu-zhuan-huan-wei-er-cha-sou-suo-shu.md)
