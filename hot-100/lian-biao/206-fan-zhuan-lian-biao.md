# 206、反转链表

我的思路：

1、创建虚拟头节点

2、用数组存储从链表取出的每一个节点

3、从数组的最后一项开始，依次取出数字，作为新节点，放进链表

4、返回虚拟头节点

AC代码：

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode dummyHead = new ListNode(0);
        ListNode p = head;
        ListNode q = dummyHead;
        double []arr = new double[10000];
        int i=0;
        while (p != null && i<arr.length) {
            arr[i]=p.val;
            p = p.next;
            i++;
        }
        for(int j=i-1;j>=0;j--){
            q.next = new ListNode((int)(arr[j]));
            q = q.next;
        }
        return dummyHead.next;
    }
}
```

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

From 代码随想录：

如果再定义一个新的链表，实现链表元素的反转，其实这是对内存空间的浪费。

其实只需要改变链表的next指针的指向，直接将链表反转 ，而不用重新定义一个新的链表

```java
// 双指针
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode prev = null;
        ListNode cur = head;
        ListNode temp = null;
        while (cur != null) {
            temp = cur.next;// 保存下一个节点
            cur.next = prev;
            prev = cur;
            cur = temp;
        }
        return prev;
    }
}
```

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>
