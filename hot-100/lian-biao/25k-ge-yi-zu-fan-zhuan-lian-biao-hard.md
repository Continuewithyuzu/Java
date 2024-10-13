---
icon: battery-exclamation
---

# 25、K 个一组翻转链表（Hard）

我的思路：

1、写交换函数，有两个形参，一个是head，一个是k

2、将交换以后的节点首尾和原来的节点连接起来



发现思路是差不多了，但是代码实现上面，不知道怎么接节点

## 于是又看了官方题解

我们需要把链表节点按照 k 个一组分组，所以可以使用一个指针 head 依次指向每组的头节点。这个指针每次向前移动 k 步，直至链表结尾。对于每个分组，我们先判断它的长度是否大于等于 k。若是，我们就翻转这部分链表，否则不需要翻转。

接下来的问题就是如何翻转一个分组内的子链表。翻转一个链表并不难，过程可以参考「206. 反转链表」。但是对于一个子链表，除了翻转其本身之外，还需要将子链表的头部与上一个子链表连接，以及子链表的尾部与下一个子链表连接。

因此，在翻转子链表的时候，我们不仅<mark style="color:blue;">**需要子链表头节点 head，还需要有 head 的上一个节点 pre**</mark>，以便翻转完后把子链表再接回 pre。

但是对于第一个子链表，它的头节点 head 前面是没有节点 pre 的。所以，<mark style="color:blue;">**我们新建一个节点，把它接到链表的头部，让它作为 pre 的初始值，这样 head 前面就有了一个节点**</mark>，我们就可以避开链表头部的边界条件。这么做还有一个好处，下面我们会看到。

反复移动指针 head 与 pre，对 head 所指向的子链表进行翻转，直到结尾，我们就得到了答案。下面我们该返回函数值了。

有的同学可能发现这又是一件麻烦事：**链表翻转之后，链表的头节点发生了变化，那么应该返回哪个节点呢？**照理来说，前 k 个节点翻转之后，链表的头节点应该是第 k 个节点。那么要在遍历过程中记录第 k 个节点吗？但是如果链表里面没有 k 个节点，答案又还是原来的头节点。我们又多了一大堆循环和判断要写，太崩溃了！

等等！还记得<mark style="background-color:blue;">**我们创建了节点 pre 吗？这个节点一开始被连接到了头节点的前面，而无论之后链表有没有翻转，它的 next 指针都会指向正确的头节点**</mark>。那么我们只要返回它的下一个节点就好了。至此，问题解决。

```java
class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode hair = new ListNode(0);
        hair.next = head;
        ListNode pre = hair;

        while (head != null) {
            ListNode tail = pre;
            // 查看剩余部分长度是否大于等于 k
            for (int i = 0; i < k; ++i) {
                tail = tail.next;
                if (tail == null) {
                    return hair.next;
                }
            }
            ListNode nex = tail.next;
            ListNode[] reverse = myReverse(head, tail);
            head = reverse[0];
            tail = reverse[1];
            // 把子链表重新接回原链表
            pre.next = head;
            tail.next = nex;
            pre = tail;
            head = tail.next;
        }

        return hair.next;
    }

    public ListNode[] myReverse(ListNode head, ListNode tail) {
        ListNode prev = tail.next;
        ListNode p = head;
        while (prev != tail) {
            ListNode nex = p.next;
            p.next = prev;
            prev = p;
            p = nex;
        }
        return new ListNode[]{tail, head};
    }
}
```

这个思路属于比较好懂的

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

***

## 进阶思路：递归

```java
class Solution {
  public ListNode reverseKGroup(ListNode head, int k) {
      ListNode currentNode = head;
      int nodeCount = 0;
      // 计算链表长度
      while (currentNode != null) {
          nodeCount++;
          currentNode = currentNode.next;
      }
      // 剩余节点不足k个 直接返回头节点
      if (nodeCount < k) {
          return head;
      }

      ListNode pre = head;
      ListNode cur = head.next;
      for (int i = 0;i < k - 1;i++) {
          ListNode next = cur.next;
          cur.next = pre;
          pre = cur;
          cur = next;
      }

      head.next = reverseKGroup(cur, k);
      return pre;
  }
}
```

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

这个递归倒是可以理解：判断递归结束的条件是长度是否大于k，否则传入新节点继续反转
