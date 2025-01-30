# 283、移动零

第一个想法：暴力解决，双重遍历，但超时了

借鉴到的更好的办法：

直接将非0的数字左移即可，再填充剩下的格子为0

代码：

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int cur=0;
        for(int i=0; i<nums.length; i++){
            if(nums[i] != 0){
                nums[cur++] = nums[i];
            }
        }
        for(;cur< nums.length;cur++){
            nums[cur] = 0;
        }
    }
}
```

<figure><img src="../../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>
