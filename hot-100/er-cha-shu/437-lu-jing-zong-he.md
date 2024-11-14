# 437、路径总和Ⅲ

我的想法是化为小事件递归完成整个过程

```java
class Solution {
    public int pathSum(TreeNode root, int targetSum) {
        if(root==null) return 0;
        TreeNode curr = root;
        int res = 0;
        //while(curr != null){
            //while(targetSum-curr.val != 0){
                if(targetSum-curr.val<0){
                    pathSum(curr.left,targetSum);
                    pathSum(curr.right,targetSum);
                }
                else{
                    if(curr.left == null) return 0;
                    //targetSum = targetSum-curr.val;
                    pathSum(curr.left,targetSum-curr.left.val);
                    //targetSum = targetSum-curr.val;
                    if(curr.right == null) return 0;
                    pathSum(curr.right,targetSum-curr.right.val);
                }
                if(targetSum==curr.v433al){
                    res++;
                }
            //}
        //}
        return res;
    }
}
```

对于递归的理解还是不是很深刻，感觉用起来还是不太得心应手，没有通过样例

题解:

```java
class Solution {
    public int pathSum(TreeNode root, long targetSum) {
        if (root == null) {
            return 0;
        }

        int ret = rootSum(root, targetSum);
        ret += pathSum(root.left, targetSum);
        ret += pathSum(root.right, targetSum);
        return ret;
    }

    public int rootSum(TreeNode root, long targetSum) {
        int ret = 0;

        if (root == null) {
            return 0;
        }
        int val = root.val;
        if (val == targetSum) {
            ret++;
        } 

        ret += rootSum(root.left, targetSum - val);
        ret += rootSum(root.right, targetSum - val);
        return ret;
    }
}
```

双重递归
