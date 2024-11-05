# 102、二叉树的层序遍历

应该有递归和迭代两种解法

迭代法：应用广度优先搜索

**Ⅰ. 按层打印：** 题目要求的二叉树的 **从上至下** 打印（即按层打印），又称为二叉树的 **广度优先搜索**（BFS）。BFS 通常借助 **队列** 的先入先出特性来实现。

**II. 每层打印到一行：** 将本层全部节点打印到一行，并将下一层全部节点加入队列，以此类推，即可分为多行打印。



#### 算法流程： <a href="#id-4" id="id-4"></a>

1. **特例处理：** 当根节点为空，则返回空列表 `[]` 。
2. **初始化：** 打印结果列表 `ret = []` ，包含根节点的队列 `queue = [root]` 。
3. **BFS 循环：** 当队列 `queue` 为空时跳出。
   1. 新建一个临时列表 `level`  ，用于存储当前层打印结果。
   2. **当前层打印循环：** 循环次数为当前层节点数（即队列 `queue` 长度）。
      1. **出队：** 队首元素出队，记为 `node`。
      2. **打印：** 将 `node.val` 添加至 `level`  尾部。
      3. **添加子节点：** 若 `node` 的左（右）子节点不为空，则将左（右）子节点加入队列 `queue` 。
   3. 将当前层结果 `level` 添加入 `ret` 。
4. **返回值：** 返回打印结果列表 `ret` 即可。

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> ret = new ArrayList<List<Integer>>();
        if (root == null) {
            return ret;
        }

        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            List<Integer> level = new ArrayList<Integer>();
            int currentLevelSize = queue.size();
            for (int i = 1; i <= currentLevelSize; ++i) {
                TreeNode node = queue.poll();
                level.add(node.val);
                if (node.left != null) {
                    queue.offer(node.left);
                }
                if (node.right != null) {
                    queue.offer(node.right);
                }
            }
            ret.add(level);
        }
        
        return ret;
    }
}
```

这道题目用递归实现比较复杂
