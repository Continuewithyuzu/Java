# 138、随机链表的复制

## 思路一：

1、先设置虚拟头节点dummy表示新的链表，最后返回dummy.next，设置节点p 值为dummy

2、新建一个Hash map，key是val，value是random.index

代码：

```java
class Solution {
    public Node copyRandomList(Node head) {
        Node dummy = new Node(0);
        dummy.next = head;
        Node p = dummy;
        Node q = head;
//        while (q != null) {
//            p.val = q.val;
//            p.random = q.random;
//            p = p.next;
//            q = q.next;
//        }
        HashMap <Integer, Node> map = new HashMap <Integer, Node>();
        while (q != null) {
            map.put(q.val,q.random);
            p.val = q.val;
            p.random = map.get(p.val);
            p = p.next;
            q = q.next;
        }
        return dummy.next;
    }
}

```

结果和思路二一样的报错

## 思路二：迭代

新建一个虚拟头节点，一个p指向虚拟头节点

while循环迭代赋值

```java
class Solution {
    public Node copyRandomList(Node head) {
        Node dummy = new Node(0);
        dummy.next = head;
        Node p = dummy;
        Node q = head;
        while (q != null) {
            p.val = q.val;
            p.random = q.random;
            p = p.next;
            q = q.next;
        }
        return dummy.next;
    }
}
```

很显然是不可以的。报错：

`Random pointer of node with label 13 from the original list was modified`

这个错误是因为修改了原链表的随机指针 (`random pointer`)，而这不是预期的行为。特别是在一些链表复制操作中，我们希望保持原链表不变，而创建一个新的链表来复制随机指针等信息。如果你在操作过程中直接修改了原链表中的随机指针，这个错误就会出现。

***

## 解法1：Hash map

利用哈希表的**查询特点**，考虑构建 原链表节点 和 新链表对应节点 的键值对映射关系，再遍历构建新链表各节点的 next 和 random 引用指向。

算法流程： 若头节点 head 为空节点，直接返回 null 。

&#x20;初始化： 哈希表 dic ， 节点 cur 指向头节点。&#x20;

复制链表： 建立新节点，并向 dic 添加键值对 (原 cur 节点, 新 cur 节点） 。 cur 遍历至原链表下一节点。

&#x20;构建新链表的引用指向： 构建新节点的 next 和 random 引用指向。 cur 遍历至原链表下一节点。

&#x20;返回值： 新链表的头节点 dic\[cur] 。

```java
class Solution {
    public Node copyRandomList(Node head) {
        if(head == null) return null;
        Node cur = head;
        Map<Node, Node> map = new HashMap<>();
        // 3. 复制各节点，并建立 “原节点 -> 新节点” 的 Map 映射
        while(cur != null) {
            map.put(cur, new Node(cur.val));
            cur = cur.next;
        }
        cur = head;
        // 4. 构建新链表的 next 和 random 指向
        while(cur != null) {
            map.get(cur).next = map.get(cur.next);
            map.get(cur).random = map.get(cur.random);
            cur = cur.next;
        }
        // 5. 返回新链表的头节点
        return map.get(head);
    }
}
```

<figure><img src="../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

* `map.get(cur).next = map.get(cur.next)`：获取 `cur` 对应的新节点，并将其 `next` 指向原链表中 `cur.next` 的新节点。
* `map.get(cur).random = map.get(cur.random)`：类似地，设置 `random` 指针，指向原链表中 `cur.random` 的新节点。
