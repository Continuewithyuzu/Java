# 19、删除链表的倒数第N个节点

思路：

~~从头节点开始计算，到第i+1=n个节点时将改变指针指向~~

看错题了，是倒数第n个节点，那就要先求链表长度，先定义一个getLength函数求链表长度，再执行操作

代码实现：

```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        int i=0;
        int len = getLength(head);
        ListNode dummyHead = new ListNode(0,head);
        ListNode curr = dummyHead;
        for (i = 1; i < len-n+1 ; i++) {
            curr = curr.next;
        }
        if (curr.next != null && curr.next.next != null) {
            curr.next = curr.next.next;
        } else {
            curr.next = null;
        }
        return dummyHead.next;
    }

    public int getLength(ListNode p){
        int length = 0;
        while (p != null) {
            length++;
            p = p.next;
        }
        return length;
    }
}
```

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>
