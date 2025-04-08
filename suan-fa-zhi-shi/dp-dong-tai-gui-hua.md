# dp动态规划

动态规划，英文：Dynamic Programming，简称DP，如果某一问题有很多重叠子问题，使用动态规划是最有效的。

所以动态规划中每一个状态一定是由上一个状态推导出来的，**这一点就区分于贪心**，贪心没有状态推导，而是从局部直接选最优的

**对于动态规划问题，我将拆解为如下五步曲，这五步都搞清楚了，才能说把动态规划真的掌握了！**

1. 确定dp数组（dp table）以及下标的含义
2. 确定递推公式
3. dp数组如何初始化
4. 确定遍历顺序
5. 举例推导dp数组

## 例题

### 509. 斐波那契数 <a href="#id-509-fei-bo-na-qi-shu" id="id-509-fei-bo-na-qi-shu"></a>

> 斐波那契数，通常用 F(n) 表示，形成的序列称为 斐波那契数列 。该数列由 0 和 1 开始，后面的每一项数字都是前面两项数字的和。也就是： F(0) = 0，F(1) = 1 F(n) = F(n - 1) + F(n - 2)，其中 n > 1 给你n ，请计算 F(n) 。
>
> 示例 1：
>
> * 输入：2
> * 输出：1
> * 解释：F(2) = F(1) + F(0) = 1 + 0 = 1
>
> 示例 2：
>
> * 输入：3
> * 输出：2
> * 解释：F(3) = F(2) + F(1) = 1 + 1 = 2
>
> 示例 3：
>
> * 输入：4
> * 输出：3
> * 解释：F(4) = F(3) + F(2) = 2 + 1 = 3
>
> 提示：
>
> * 0 <= n <= 30

我写的代码：

```java
class Solution {
    public int fib(int n) {
        int []dp = new int[n+2];
        dp[0]=0;
        dp[1]=1;
        if(n==0) return dp[0];
        if(n==1) return dp[1];
        for(int i=2;i<=n;i++){
            dp[i]= dp[i-1]+dp[i-2];
        }
        return dp[n];
    }
}
```

### 70. 爬楼梯 <a href="#id-70-pa-lou-ti" id="id-70-pa-lou-ti"></a>

> 假设你正在爬楼梯。需要 n 阶你才能到达楼顶。
>
> 每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？
>
> 注意：给定 n 是一个正整数。
>
> 示例 1：
>
> * 输入： 2
> * 输出： 2
> * 解释： 有两种方法可以爬到楼顶。
>   * 1 阶 + 1 阶
>   * 2 阶
>
> 示例 2：
>
> * 输入： 3
> * 输出： 3
> * 解释： 有三种方法可以爬到楼顶。
>   * 1 阶 + 1 阶 + 1 阶
>   * 1 阶 + 2 阶
>   * 2 阶 + 1 阶

我写的代码：

```java
class Solution {
    public int climbStairs(int n) {
        int [] dp = new int[n+2];
        dp[1] = 1;
        dp[2] = 2;
        if(n<=2) return dp[n];
        for(int i=3;i<=n;i++){
            dp[i] = dp[i-1]+dp[i-2];
        }
        return dp[n];
    }
}
```

### 746. 使用最小花费爬楼梯 <a href="#id-746-shi-yong-zui-xiao-hua-fei-pa-lou-ti" id="id-746-shi-yong-zui-xiao-hua-fei-pa-lou-ti"></a>

> 数组的每个下标作为一个阶梯，第 i 个阶梯对应着一个非负数的体力花费值 cost\[i]（下标从 0 开始）。
>
> 每当你爬上一个阶梯你都要花费对应的体力值，一旦支付了相应的体力值，你就可以选择向上爬一个阶梯或者爬两个阶梯。
>
> 请你找出达到楼层顶部的最低花费。在开始时，你可以选择从下标为 0 或 1 的元素作为初始阶梯。
>
> 示例 1：
>
> * 输入：cost = \[10, 15, 20]
> * 输出：15
> * 解释：最低花费是从 cost\[1] 开始，然后走两步即可到阶梯顶，一共花费 15 。
>
> 示例 2：
>
> * 输入：cost = \[1, 100, 1, 1, 1, 100, 1, 1, 100, 1]
> * 输出：6
> * 解释：最低花费方式是从 cost\[0] 开始，逐个经过那些 1 ，跳过 cost\[3] ，一共花费 6 。
>
> 提示：
>
> * cost 的长度范围是 \[2, 1000]。
> * cost\[i] 将会是一个整型数据，范围为 \[0, 999] 。

我写的代码：

```java
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int []dp = new int[cost.length+1];
        dp[0] = 0;
        dp[1] = 0;
        for(int i=2;i<=cost.length;i++){
            dp[i]=Math.min(dp[i-2]+cost[i-2],dp[i-1]+cost[i-1]);
        }
        return dp[cost.length];
    }
}
```

### 62.不同路径 <a href="#id-62-bu-tong-lu-jing" id="id-62-bu-tong-lu-jing"></a>

> 一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为 “Start” ）。
>
> 机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为 “Finish” ）。
>
> 问总共有多少条不同的路径？
>
> 示例 1：
>
> <img src="https://file.kamacoder.com/pics/20210110174033215.png" alt="" data-size="original">
>
> * 输入：m = 3, n = 7
> * 输出：28
>
> 示例 2：
>
> * 输入：m = 2, n = 3
> * 输出：3
>
> 解释： 从左上角开始，总共有 3 条路径可以到达右下角。
>
> 1. 向右 -> 向右 -> 向下
> 2. 向右 -> 向下 -> 向右
> 3. 向下 -> 向右 -> 向右
>
> 示例 3：
>
> * 输入：m = 7, n = 3
> * 输出：28
>
> 示例 4：
>
> * 输入：m = 3, n = 3
> * 输出：6
>
> 提示：
>
> * 1 <= m, n <= 100
> * 题目数据保证答案小于等于 2 \* 10^9

我写的代码：

```java
class Solution {
    public int uniquePaths(int m, int n) {
        int [][]dp = new int[m][n];
        for(int i=0;i<m;i++) dp[i][0] = 1;
        for(int i=0;i<n;i++) dp[0][i] = 1;
        for(int i=1;i<m;i++){
            for(int j=1;j<n;j++){
                dp[i][j] = dp[i-1][j] + dp[i][j-1];
            }
        }
        return dp[m-1][n-1];
    }
}
```

