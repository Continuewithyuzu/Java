# Page

我的思路是：

判断其中一个节点是否在以另一个节点为根节点的子树中，如果是则返回该节点，否则否则返回根节点

但是这个思路不对，有忽略的情况，所以不可行

题解：

若 root 是 p,q 的 **最近公共祖先** ，则只可能为以下情况之一：

1. p 和 q 在 root 的子树中，且分列 root 的 **异侧**（即分别在左、右子树中）；
2. p=root ，且 q 在 root 的左或右子树中；
3. q=root ，且 p 在 root 的左或右子树中；

代码：

```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root == null || root == p || root == q) return root;
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        if(left == null) return right;
        if(right == null) return left;
        return root;
    }
}
```
