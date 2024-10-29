# 739、每日温度

我的思路是暴力，但是禁不住题目压力测试。。。。

代码：

```java
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int i,j;
        ArrayList list = new ArrayList();
        for(i=0;i<temperatures.length;i++){
            int count = 0;
            for(j=i+1;j<temperatures.length;j++){
                if(temperatures[j]>temperatures[i]){
                    count=j-i;
                    list.add(count);
                    break;
                }
            }
            if(count == 0 ){
                list.add(0);
            }
        }
        int[] ans = new int[list.size()];
        for(i=0;i<list.size();i++){
            ans[i]=(int)list.get(i);
        }
        return ans;
    }
}
```

压力测试：

<figure><img src="../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

时间复杂度是O(n)2，用了两个for循环，所以应该是只能用栈实现了

好吧 ，看了别人的暴力：

```java
public int[] dailyTemperatures(int[] T) {
    int length = T.length;
    int[] result = new int[length];

    for (int i = 0; i < length; i++) {
        int current = T[i];
        if (current < 100) {
            for (int j = i + 1; j < length; j++) {
                if (T[j] > current) {
                    result[i] = j - i;
                    break;
                }
            }
        }
    }

    return result;
}
```

看了一下应该是最后转数组超时了，无论如何，暴力都不是我们想要的代码

***

方法二：

```java
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int n = temperatures.length;
        int[] res = new int[n];
        // 单调栈，从栈底到栈顶为温度减小的下标
        Deque<Integer> stack = new ArrayDeque<>();
        for (int i = 0; i < n; i++) {
            while (!stack.isEmpty() && temperatures[i] > temperatures[stack.getLast()]) {
                int prevIndex = stack.removeLast();
                res[prevIndex] = i - prevIndex;
            }
            stack.addLast(i);
        }
        while (!stack.isEmpty()) {
            int index = stack.removeLast();
            res[index] = 0;
        }
        return res;
    }
}
```



假设 `temperatures = [73, 74, 75, 71, 69, 72, 76, 73]`：

* 对于第一个温度 73，栈为空，将下标 0 入栈。
* 对于第二个温度 74，栈顶是 73（下标 0），74 大于 73，找到更高温度，计算 `1 - 0 = 1`，即 `res[0] = 1`，弹出 0，将 1 入栈。
* 依次进行上述逻辑处理，最终 `res = [1, 1, 4, 2, 1, 1, 0, 0]`。
