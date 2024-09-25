# 1、两数之和

Hash map

查找元素是否出现

value:下标

key:元素&#x20;



我的解法：两个For循环，时间复杂度O(n)2

优点是简单易懂，但是时间复杂度高，效率低

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int i,j;
        for(i=0;i<nums.length-1;i++){
            for(j=i+1;j<nums.length;j++){
                if(nums[i]+nums[j]==target){
                    return new int[]{i,j};
                }
            }
        }
        return null;
    }
}
```



更优雅的解法：

1、Hash Map  <mark style="color:blue;">键值对</mark>

value:下标

key:元素&#x20;

<mark style="color:blue;">**map.get返回指定键所映射的值**</mark>

```java
//使用哈希表
public int[] twoSum(int[] nums, int target) {
    int[] res = new int[2];
    if(nums == null || nums.length == 0){
        return res;
    }
    Map<Integer, Integer> map = new HashMap<>();//创建Hash Map
    for(int i = 0; i < nums.length; i++){
        int temp = target - nums[i];   // 遍历当前元素，并在map中寻找是否有匹配的key
        if(map.containsKey(temp)){
            res[1] = i;
            res[0] = map.get(temp); //返回下标
            break;
        }
        map.put(nums[i], i);    // 如果没找到匹配对，就把访问过的元素和下标加入到map中
    }
    return res;
}
```

2、双指针

```java
//使用双指针
public int[] twoSum(int[] nums, int target) {
    int m=0,n=0,k,board=0;
    int[] res=new int[2];
    int[] tmp1=new int[nums.length];
    //备份原本下标的nums数组
    System.arraycopy(nums,0,tmp1,0,nums.length);
    //将nums排序
    Arrays.sort(nums);
    //双指针
    for(int i=0,j=nums.length-1;i<j;){
        if(nums[i]+nums[j]<target)
            i++;
        else if(nums[i]+nums[j]>target)
            j--;
        else if(nums[i]+nums[j]==target){
            m=i;
            n=j;
            break;
        }
    }
    //找到nums[m]在tmp1数组中的下标
    for(k=0;k<nums.length;k++){
        if(tmp1[k]==nums[m]){
            res[0]=k;
            break;
        }
    }
    //找到nums[n]在tmp1数组中的下标
    for(int i=0;i<nums.length;i++){
        if(tmp1[i]==nums[n]&&i!=k)
            res[1]=i;
    }
    return res;
}
```
