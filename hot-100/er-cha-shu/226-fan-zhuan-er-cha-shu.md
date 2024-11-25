# 226、翻转二叉树

思路和交换两个数字一样，终于第一次靠自己ac了一道关于二叉树的题目，有了一些递归的思想

代码：

```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        TreeNode head = root;
        if(root == null) return null;
        if(root.left == null){
            root.left = root.right;
            root.right = null;
        }
        else if(root.right == null){
            root.right = root.left;
            root.left = null;
        }
        else{
            TreeNode temp = root.left;
            root.left = root.right;
            root.right = temp;
        }
        invertTree(root.left);
        invertTree(root.right);
        return head;
    }
}
```

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

要注意的就是递归结束的条件。
