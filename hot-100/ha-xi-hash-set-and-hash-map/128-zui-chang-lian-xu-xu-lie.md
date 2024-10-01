# 128、最长连续序列

## 我的思路：

1、先对数组排序

2、判断：该项与下一项是否相等，if 相等：i+1，else 如果该项与下一项相减为一，count+1，否则break

### 根据我的思路写的代码：

暴力解法、时间复杂度是O(n)2，超过了题目要求的O(n)

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        if (nums.length == 0) return 0;
        Arrays.sort(nums);
        int count = 1;
        for(int i=0; i<nums.length-1; i++){
            while(nums[i]==nums[i+1]){
                i+=1;
            }
            if(nums[i]!=nums[i+1]){
                if(nums[i+1]-nums[i]==1){
                    count++;
                }
                else{
                    break;
                }
            }
        }
        return count;
    }
}
```

***

时间复杂度为O(n)的解法\
用Hash set

学习了Hash Set以后写的

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        if (nums.length == 0) return 0;
        HashSet<Integer> hashSet = new HashSet<>();
        //Arrays.sort(nums);
        for (int num : nums) {
            hashSet.add(num);
        }
        //排序后使用 HashSet 去重：由于你先对数组排序再使用 HashSet 去重，
        // 这会导致排序的结果被打乱，因为 HashSet 是无序的。
        int count = 1;
        int currentcount = 1;
        Integer[] newnums = hashSet.toArray(new Integer[hashSet.size()]);//转为数组
        Arrays.sort(newnums);
        //应该在这里排序
        for (int i = 0 ; i < newnums.length-1 ; i++) {
            if(newnums[i] + 1 == newnums[i+1]){
                currentcount++;
            }
            else{
                // 不连续时，更新最大长度，并重置当前长度
                count = Math.max(count, currentcount);
                currentcount = 1;
            }
        }
        return Math.max(count, currentcount);
    }
}
```

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

***

但其实还有更简单优雅的实现

```java
//不用Hashset 数组 from GPT
import java.util.HashSet;
import java.util.Arrays;

class Solution {
    public int longestConsecutive(int[] nums) {
        if (nums.length == 0) return 0; // 如果数组为空，返回0

        Arrays.sort(nums); // 先对数组进行排序

        int maxLength = 1; // 存储最长的连续序列长度
        int currentLength = 1; // 存储当前的连续序列长度

        for (int i = 1; i < nums.length; i++) {
            if (nums[i] == nums[i - 1]) {
                continue; // 跳过重复的元素
            }
            if (nums[i] == nums[i - 1] + 1) {
                // 如果当前元素和前一个元素是连续的，则增加当前序列长度
                currentLength++;
            } else {
                // 不连续时，更新最大长度，并重置当前长度
                maxLength = Math.max(maxLength, currentLength);
                currentLength = 1;
            }
        }
        // 最后再更新一次最大长度，处理最后一个连续序列的情况
        return Math.max(maxLength, currentLength);
    }
}
```

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

***

用HashSet的解法

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        Set<Integer> numSet = new HashSet<>();
        for (int num : nums) {
            numSet.add(num);
        }

        int longestStreak = 0;

        for (int num : numSet) {
            if (!numSet.contains(num - 1)) {
                int currentNum = num;
                int currentStreak = 1;

                while (numSet.contains(currentNum + 1)) {
                    currentNum++;
                    currentStreak++;
                }

                longestStreak = Math.max(longestStreak, currentStreak);
            }
        }
        return longestStreak;
    }
}
```

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>
