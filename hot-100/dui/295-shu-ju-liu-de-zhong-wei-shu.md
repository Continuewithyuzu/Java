# 295、数据流的中位数

又是不想用相应知识点的一题

```java
class MedianFinder {
    ArrayList<Integer> list = new ArrayList<>();
    public MedianFinder() {

    }
    
    public void addNum(int num) {
        list.add(num);
    }
    
    public double findMedian() {
        list.sort(Integer::compare);
        int size = list.size();
        if (size % 2 == 0) {
            double m = list.get(size / 2);
            double n = list.get(size / 2 - 1);
            double median = (n + m) / 2;
            return median;
        }
        else{
            return list.get(size / 2);
        }
    }
}
```

用的是Arraylist，时间复杂度已经尽可能在优化了，还是有一个样例过不了，属实是压力测试了

<figure><img src="../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

可能真的得用堆吧。或者优化思路是把代码部分的排序换成堆排序。

***

## 题解思路

建立一个大顶堆用来存小的一边，小顶堆用来存大的一边

```java
class MedianFinder {
    Queue<Integer> A, B;
    public MedianFinder() {
        A = new PriorityQueue<>(); // 小顶堆，保存较大的一半
        B = new PriorityQueue<>((x, y) -> (y - x)); // 大顶堆，保存较小的一半
    }
    public void addNum(int num) {
        if (A.size() != B.size()) {
            A.add(num);
            B.add(A.poll());
        } else {
            B.add(num);
            A.add(B.poll());
        }
    }
    public double findMedian() {
        return A.size() != B.size() ? A.peek() : (A.peek() + B.peek()) / 2.0;
    }
}
```

