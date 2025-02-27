# 42、接雨水

终于写道了传说中hard的接雨水



一开始按着自己的思路写了一个代码，但是超时了

遂看题解

<pre class="language-java"><code class="lang-java">class Solution {
<strong>    public int trap(int[] height) {
</strong>        int n = height.length;
        int res = 0;
        // 左右指针：分别指向左右两边界的列
        int left = 0, right = n - 1;
        // 左指针的左边最大高度、右指针的右边最大高度
        int leftMax = height[left], rightMax = height[right];
        // 最两边的列存不了水
        left++;
        right--;
        // 向中间靠拢
        while(left &#x3C;= right){
            leftMax = Math.max(leftMax, height[left]);
            rightMax = Math.max(rightMax, height[right]);
            if(leftMax &#x3C; rightMax){
                // 左指针的leftMax比右指针的rightMax矮
                // 说明：左指针的右边至少有一个板子 > 左指针左边所有板子
                // 根据水桶效应，保证了左指针当前列的水量决定权在左边
                // 那么可以计算左指针当前列的水量：左边最大高度-当前列高度
                res += leftMax - height[left];
                left++;
            }else{
                // 右边同理
                res += rightMax - height[right];
                right--;
            }
        }
        return res;
    }
}
</code></pre>

