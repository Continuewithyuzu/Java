# 215、数组中的第K个最大元素

思路没什么难的，就是先对数组排序然后返回相应下标

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        Arrays.sort(nums);
        return nums[nums.length - k];
    }
}
```

要注意的是sort是升序排序，所以要返回的下标是`nums.length - k`

<figure><img src="../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>
