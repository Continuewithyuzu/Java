# 347、前K个高频元素

思路：实现不难，难在于怎么尽可能的快的精简代码

用hash表

代码：

```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        Arrays.sort(nums);
        HashSet set = new HashSet();
        int i;
        int count = 1;
        if(nums.length == 0) return nums;
        if(nums.length == 1 && (k == 1 || k == 0)){
            set.add(nums[0]);
        }
        for(i = 1 ; i < nums.length ; i++){
            if(nums[i] == nums[i-1]){
                count++;
            }
            else{
                count = 1;
            }
            if(count >= k){
                set.add(nums[i]);
            }
        }
        List<Integer> list = new ArrayList<>(set);
        int[] res = new int[list.size()];
        int j=0;
        for(int num:list){
            res[j++]=num;
        }
        return res;
    }
}
```

发现原来我看错题了，我写的代码是找到出现次数大于k，而题目要求的是前K出现频率

所以这题不能用HashSet



## 思路：

借助 `哈希表` 来建立数字和其出现次数的映射，遍历一遍数组统计元素的频率 维护一个元素数目为 k 的最小堆 每次都将新的元素与堆顶元素（堆中频率最小的元素）进行比较 如果新的元素的频率比堆顶端的元素大，则弹出堆顶端的元素，将新的元素添加进堆中&#x20;

最终，堆中的 k 个元素即为前 k 个高频元素

## GPT给出的解法：堆排序

```java
import java.util.*;

class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        // 1. 统计每个数字出现的频率
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }

        // 2. 使用最小堆来保留前 k 个频率最高的元素
        PriorityQueue<Integer> heap = new PriorityQueue<>(
            (n1, n2) -> map.get(n1) - map.get(n2)
        );

        for (int num : map.keySet()) {
            heap.add(num);
            if (heap.size() > k) {
                heap.poll(); // 如果堆的大小超过 k，则弹出频率最小的元素
            }
        }

        // 3. 输出结果
        int[] res = new int[k];
        for (int i = k - 1; i >= 0; i--) {
            res[i] = heap.poll();
        }

        return res;
    }
}
```

## 方法二：堆排序O(n)

```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        HashMap<Integer,Integer> map = new HashMap();
            for(int num : nums){
                if (map.containsKey(num)) {
                    map.put(num, map.get(num) + 1);
                } else {
                    map.put(num, 1);
                }
            }
            // 遍历map，用最小堆保存频率最大的k个元素
            PriorityQueue<Integer> pq = new PriorityQueue<>(new Comparator<Integer>() {
                @Override
                public int compare(Integer a, Integer b) {
                    return map.get(a) - map.get(b);
                }
            });
            for (Integer key : map.keySet()) {
                if (pq.size() < k) {
                    pq.add(key);
                } else if (map.get(key) > map.get(pq.peek())) {
                    pq.remove();
                    pq.add(key);
                }
            }
            // 取出最小堆中的元素
            List<Integer> res = new ArrayList<>();
            while (!pq.isEmpty()) {
                res.add(pq.remove());
            }
            int []ans = new int[res.size()];
            int j=0;
            for(int num:res){
                ans[j++]=num;
            }
            return ans;
    }
}
```

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

## 方法三：桶排序

```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        List<Integer> res = new ArrayList();
            // 使用字典，统计每个元素出现的次数，元素为键，元素出现的次数为值
            HashMap<Integer,Integer> map = new HashMap();
            for(int num : nums){
                if (map.containsKey(num)) {
                    map.put(num, map.get(num) + 1);
                } else {
                    map.put(num, 1);
                }
            }

            //桶排序
            //将频率作为数组下标，对于出现频率不同的数字集合，存入对应的数组下标
            List<Integer>[] list = new List[nums.length+1];
            for(int key : map.keySet()){
                // 获取出现的次数作为下标
                int i = map.get(key);
                if(list[i] == null){
                    list[i] = new ArrayList();
                }
                list[i].add(key);
            }

            // 倒序遍历数组获取出现顺序从大到小的排列
            for(int i = list.length - 1;i >= 0 && res.size() < k;i--){
                if(list[i] == null) continue;
                res.addAll(list[i]);
            }
            int []ans = new int[res.size()];
            int j=0;
            for(int num:res){
                ans[j++]=num;
            }
            return ans;
    }
}
```

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

这么多种方法中，桶排序的执行用时和消耗内存是最优的



ps:排序效率比较

<figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>
