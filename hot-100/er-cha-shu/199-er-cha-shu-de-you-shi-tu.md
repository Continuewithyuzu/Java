# 199、二叉树的右视图

我的代码：

```java
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        if( root == null){
            return new ArrayList<Integer>();
        }
        List<Integer> res = new ArrayList<Integer>();
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        TreeNode curr = root;
        while(curr != null || q.size() > 0){
            q.add(curr);
            curr = q.remove();
            res.add(curr.val);
            if(curr.right != null){
                curr = curr.right;
            }
            else{
                curr = curr.left;
            }
        }
        return res;
    }
}
```

在遇到这个测试样例的时候没有通过：

<figure><img src="../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

解决办法是加一个深度depth参数，统计该深度是否初次遇到

```java
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        dfs(root, 0, ans);
        return ans;
    }

    private void dfs(TreeNode root, int depth, List<Integer> ans) {
        if (root == null) {
            return;
        }
        if (depth == ans.size()) { // 这个深度首次遇到
            ans.add(root.val);
        }
        dfs(root.right, depth + 1, ans); // 先递归右子树，保证首次遇到的一定是最右边的节点
        dfs(root.left, depth + 1, ans);
    }
}
```
