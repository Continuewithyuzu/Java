# 94、二叉树的中序遍历

有两种方法：

1、递归

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        LinkedList list = new LinkedList();
        inOrder(root,list);
        return list;
    }

    // 中序遍历 -> 左子树 根 右子树
    public void inOrder(TreeNode root, List<Integer> res) {
        if (root == null) {
            return;
        }
        // 遍历左子树
        inOrder(root.left,res);
        // 将节点加入list中
        res.add(root.val);
        // 遍历右子树
        inOrder(root.right,res);
    }
}
```

* 调用 `inorderTraversal`，传入根节点 `1`，初始化 `list`，并调用 `inOrder(root, list)`。
* 进入 `inOrder`：
  * `root` 为节点 `1`，先递归遍历左子树，但 `root.left` 为 `null`，直接返回。
  * 添加 `1` 到 `list`。
  * 递归遍历右子树（节点 `2`）。
* 进入节点 `2` 的 `inOrder` 调用：
  * 遍历左子树（节点 `3`）。
* 进入节点 `3` 的 `inOrder` 调用：
  * 左子树为空，直接返回。
  * 添加 `3` 到 `list`。
  * 右子树为空，直接返回。
* 返回到节点 `2` 的 `inOrder` 调用，添加 `2` 到 `list`。
* 最终 `list` 是 `[1, 3, 2]`，即中序遍历结果。

***

2、迭代

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null){
            return result;
        }
        Stack<TreeNode> stack = new Stack<>();
        TreeNode cur = root;
        while (cur != null || !stack.isEmpty()){
           if (cur != null){
               stack.push(cur);
               cur = cur.left;
           }else{
               cur = stack.pop();
               result.add(cur.val);
               cur = cur.right;
           }
        }
        return result;
    }
}
```

执行过程如下：

1. `cur = root`（节点 `1`），不为空，将 `1` 压入 `stack`，并更新 `cur = cur.left`（为空）。
2. `cur` 为空，从栈中弹出节点 `1`，将 `1` 加入 `result`，更新 `cur = cur.right`（节点 `2`）。
3. `cur = 2`，不为空，将 `2` 压入 `stack`，并更新 `cur = cur.left`（节点 `3`）。
4. `cur = 3`，不为空，将 `3` 压入 `stack`，并更新 `cur = cur.left`（为空）。
5. `cur` 为空，从栈中弹出节点 `3`，将 `3` 加入 `result`，更新 `cur = cur.right`（为空）。
6. `cur` 为空，从栈中弹出节点 `2`，将 `2` 加入 `result`，更新 `cur = cur.right`（为空）。
7. `stack` 和 `cur` 均为空，循环结束，返回 `result = [1, 3, 2]`。
