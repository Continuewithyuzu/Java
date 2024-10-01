# 160、相交链表

~~我的思路：~~

~~1、同时遍历两个链表~~

~~2、找到相同的项~~

~~3、对比后续项是否相等~~



~~新思路~~

~~1、获取长度~~

~~2、反向对比~~



上博客看到的思路：代码量更少、更快

1、选一条链表，遍历链表，将链表元素放入Hash表中

2、遍历第二条链表，看看hash表中是否包含每个节点

3、返回包含的节点

代码实现：

```java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if(headA == null || headB == null) return null;
        HashSet<ListNode> set = new HashSet<>();
        while(headA!=null){
            set.add(headA);
            headA=headA.next;
        }
        while(headB!=null){
            if(set.contains(headB)){
                return headB;
            }
            headB=headB.next;
        }
        return null;
    }
}
```

<figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

***

更常规一点的方法：\
遍历

```java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if (headA == null || headB == null) {
            return null;
        }
        ListNode current1 = headA;
        ListNode current2 = headB;
        int lenA = 0;
        int lenB = 0;

        // 统计链表1的长度，并且 current1 停在最后一个节点
        while (current1.next != null) {
            lenA++;
            current1 = current1.next;
        }
        // 统计链表2的长度，并且 current2 停在最后一个节点
        while (current2.next != null) {
            lenB++;
            current2 = current2.next;
        }

        // 若相交，则两条链表最后一个节点一定是一样的。若不一样，则不相交。
        if (current1 != current2) {
            return null;
        }

        // 求两条链表的长度差值
        int d = lenA - lenB;
        // 定义长、短链表指针，分别指向长链表和短链表头
        ListNode longList;
        ListNode shortList;
        // 如果d > 0则说明第一条链表是长链表，反之第二条链表是长链表
        if (d > 0) {
            longList = headA;
            shortList = headB;
        } else {
            longList = headB;
            shortList = headA;
        }

        d = Math.abs(d);

        // 长链表先走差值步
        for (int i = 0; i < d; i++) {
            longList = longList.next;
        }

        // 长短链表一起走，直到相遇时退出循环
        while (longList != shortList) {
            longList = longList.next;
            shortList = shortList.next;
        }
        // 返回相遇的节点
        return longList;
    }
}
```

<figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>
