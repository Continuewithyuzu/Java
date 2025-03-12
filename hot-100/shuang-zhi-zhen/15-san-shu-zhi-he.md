# 15、三数之和

思路：

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

动画：

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

代码实现：

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        Arrays.sort(nums);
        if(nums.length < 3) return res;
        int i = 0;
        for( i = 0 ; i < nums.length-2 ; i++){
            if(i > 0 && nums[i] == nums[i-1]) continue; // 去重
            int R = nums.length - 1;
            int L = i + 1;
            while( L < R ) {
                int sum = nums[i] + nums[R] + nums[L];
                if (sum == 0) {
                    res.add(Arrays.asList(nums[i], nums[R], nums[L]));
                    
                    while(L < R && nums[L] == nums[L+1]){
                        L++;
                    }
                    while(L < R && nums[R] == nums[R-1]){
                        R--;
                    }
                    L++;
                    R--;
                } else if (sum < 0) {
                    L++;
                } else if (sum > 0) {
                    R--;
                }
            }
        }
        return res;
    }
}
```

这里不知道为什么不能加上`nums[0] > 0` 这个条件，可能是array排序的问题

这个问题留着以后看看

```java
if(nums.length < 3 || nums[0] > 0) return res;
```
