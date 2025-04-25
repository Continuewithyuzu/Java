# 92、验证二叉搜索树

我的思路，是判断节点然后递归，但是由于搜索二叉树的条件是：

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

我的代码有一部分的测试样例没有通过

```java
class Solution {
    public boolean isValidBST(TreeNode root) {
        if (root == null) return true;
        TreeNode curr = root;
        if(curr.left != null && curr.left.val >= curr.val ){
            return false;
        }
        if(curr.right != null && curr.right.val <= curr.val ){
            return false;
        }
        isValidBST(curr.left);
        isValidBST(curr.right);
        return true;
    }
}
```

## 题解：

```java
class Solution {
    public boolean isValidBST(TreeNode root) {
        return isValidBST(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    private boolean isValidBST(TreeNode node, long left, long right) {
        if (node == null) {
            return true;
        }
        long x = node.val;
        return left < x && x < right &&
               isValidBST(node.left, left, x) &&
               isValidBST(node.right, x, right);
    }
}
```
