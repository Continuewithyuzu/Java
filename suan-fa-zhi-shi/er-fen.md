# 二分

## **二分法的基本原理**

二分法适用于 **单调性** 的问题，即：

* **单调递增（或者递减）**：如果一个函数或数组是单调的，可以使用二分查找高效地找到特定的值或范围。
* **范围内有解**：问题的解落在某个区间内，我们可以不断缩小区间，找到最优解。

## **二分查找的应用场景**

二分法主要用于：

1. **查找数组中的某个数**
2. **求解最大/最小值**（优化问题）
3. **求解数学函数的零点**
4. **离散问题中的最优解**

## **二分查找的关键技巧**

1. **避免死循环**
   * `while (left <= right)`，而不是 `while (left < right)`，防止 `left` 永远无法等于 `right`。
2. **防止溢出**
   * 使用 `mid = left + (right - left) / 2` 而不是 `(left + right) / 2`，避免 `left + right` 过大导致溢出。
3. **判定条件**
   * 目标值在 **左侧**：`right = mid - 1`
   * 目标值在 **右侧**：`left = mid + 1`
4. **适用于单调性问题**
   * **如果目标值变大，条件仍然满足**（如 `mid` 可行时尝试更大值），就可以使用二分查找。

***

## 例题：

> **问题描述**\
> 儿童节那天有 K 位小朋友到小明家做客。小明拿出了珍藏的巧克力招待小朋友们。\
> 小明一共有 N 块巧克力，其中第 i 块是 Hi×Wi 的方格组成的长方形。为了公平起见，\
> 小明需要从这 N 块巧克力中切出 K 块巧克力分给小朋友们。切出的巧克力需要满足：\
> 形状是正方形，边长是整数;\
> 大小相同;\
> 例如一块 6×56×5 的巧克力可以切出 66 块 2×22×2 的巧克力或者 22 块 3×33×3 的巧克力。\
> 当然小朋友们都希望得到的巧克力尽可能大，你能帮小明计算出最大的边长是多少么？\
> **输入描述**\
> 第一行包含两个整数 N,KN,K (1≤N,K≤105)。\
> 以下 N 行每行包含两个整数 Hi,Wi(1≤Hi,Wi≤105)。\
> 输入保证每位小朋友至少能获得一块 1x1 的巧克力。\
> **输出描述**\
> 输出切出的正方形巧克力最大可能的边长。\
> **输入输出样例**\
> 示例\
> 输入\
> 2 10\
> 6 5\
> 5 6\
> 输出\
> 2\
> 运行限制\
> 最大运行时间：2s\
> 最大运行内存: 256M

```java
package LQ8;

import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // 读取N和K
        int N = scanner.nextInt();
        int K = scanner.nextInt();

        int[][] chocolates = new int[N][2];
        int maxSide = 0;

        // 读取巧克力的尺寸，并找出最大的可能正方形边长
        for (int i = 0; i < N; i++) {
            chocolates[i][0] = scanner.nextInt();
            chocolates[i][1] = scanner.nextInt();
            maxSide = Math.max(maxSide, Math.min(chocolates[i][0], chocolates[i][1]));
        }

        scanner.close();

        // 采用二分查找，寻找最大的可行正方形边长
        int left = 1, right = maxSide, result = 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (canCut(chocolates, N, K, mid)) {
                result = mid; // 记录可行解
                left = mid + 1; // 尝试更大的边长
            } else {
                right = mid - 1; // 过大，缩小范围
            }
        }

        System.out.println(result);
    }

    // 判断是否可以切出至少K块边长为size的正方形巧克力
    private static boolean canCut(int[][] chocolates, int N, int K, int size) {
        int count = 0;
        for (int i = 0; i < N; i++) {
            count += (chocolates[i][0] / size) * (chocolates[i][1] / size);
            if (count >= K) return true; // 及早终止
        }
        return count >= K;
    }
}
```

## 核心思路：

* 接收变量，找到最大的边长

```java
 // 读取N和K
        int N = scanner.nextInt();
        int K = scanner.nextInt();

        int[][] chocolates = new int[N][2];
        int maxSide = 0;

        // 读取巧克力的尺寸，并找出最大的可能正方形边长
        for (int i = 0; i < N; i++) {
            chocolates[i][0] = scanner.nextInt();
            chocolates[i][1] = scanner.nextInt();
            maxSide = Math.max(maxSide, Math.min(chocolates[i][0], chocolates[i][1]));
        }
```

* 二分查找算法

```java
 // 采用二分查找，寻找最大的可行正方形边长
        int left = 1, right = maxSide, result = 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (canCut(chocolates, N, K, mid)) {
                result = mid; // 记录可行解
                left = mid + 1; // 尝试更大的边长
            } else {
                right = mid - 1; // 过大，缩小范围
            }
        }
```

* canCut判断能不能足够

```java
  // 判断是否可以切出至少K块边长为size的正方形巧克力
    private static boolean canCut(int[][] chocolates, int N, int K, int size) {
        int count = 0;
        for (int i = 0; i < N; i++) {
            count += (chocolates[i][0] / size) * (chocolates[i][1] / size);
            if (count >= K) return true; // 及早终止
        }
        return count >= K;
    }
}
```
