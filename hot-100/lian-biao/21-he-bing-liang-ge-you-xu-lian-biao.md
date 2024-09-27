# 21、合并两个有序链表

有两个想法：

## 1、创建虚拟头节点，每次都比较两个有序链表的next，再加入虚拟头节点的新链表里

可行，但是要注意while循环里面的判断要尽可能少，3个判断就会超时，2个不会

代码实现;

```java
class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode dummyHead = new ListNode(0);
        ListNode p = dummyHead, a = list1, b = list2;
        while(a != null && b != null) {
            if(a.val <= b.val){
                p.next = a;
                p = p.next;
                a = a.next;
            }
            else{
                p.next = b;
                p = p.next;
                b = b.next;
            }
        }
        if(a != null){
            p.next = a;
        }
        else{
            p.next = b;
        }
        return dummyHead.next;
    }
}
```

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

***

2、链表转数组 ：<mark style="color:red;">没必要，麻烦</mark>

3、原链表该指针指向

***

## 很妙的解法:递归

```java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) {
            return l2;
        } else if (l2 == null) {
            return l1;
        } else if (l1.val < l2.val) {
            l1.next = mergeTwoLists(l1.next, l2);
            return l1;
        } else {
            l2.next = mergeTwoLists(l1, l2.next);
            return l2;
        }
    }
}
```

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>
