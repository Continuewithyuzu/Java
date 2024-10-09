---
description: 属于是21的进阶版了
---

# 23、合并K个升序链表

## 思路一：

遍历链表数组，用一个新的数组存储所有值，排序，然后转为新的链表

然后不出意料的又超时了

代码：

```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        int []a = new int[5000000];
        int i = 0 , j = 0;
        ListNode p = lists[j];
        int len = lists.length;
       //遍历取出链表数组元素
        for (j = 0; j < len; j++) {
            if(p.next != null){
                a[i] = p.val;
                i++;
                p = p.next;
            }
        }
        Arrays.sort(a,0,i);
        ListNode dummy = new ListNode(0);
        ListNode q = dummy;
        for(int k = 0; k < a.length; k++){
            q.next = new ListNode(a[k]);
            q = q.next;
        }
        return dummy.next;
    }
}
```

## 思路二：

~~用一个新的链表，把所有的元素按顺序遍历取出。然后依照~~[~~148~~](148-pai-xu-lian-biao.md)~~排序链表，可以数组，可以分治~~



## 题解思路：

\
结合[21](21-he-bing-liang-ge-you-xu-lian-biao.md)、然后设置空链表ans，依次遍历lists，取出两两合并

```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        ListNode ans = null;
        for (int i = 0; i < lists.length; ++i) {
            ans = mergeTwoLists(ans, lists[i]);
        }
        return ans;
    }

    public ListNode mergeTwoLists(ListNode a, ListNode b) {
        if (a == null || b == null) {
            return a != null ? a : b;
        }
        ListNode head = new ListNode(0);
        ListNode tail = head, aPtr = a, bPtr = b;
        while (aPtr != null && bPtr != null) {
            if (aPtr.val < bPtr.val) {
                tail.next = aPtr;
                aPtr = aPtr.next;
            } else {
                tail.next = bPtr;
                bPtr = bPtr.next;
            }
            tail = tail.next;
        }
        tail.next = (aPtr != null ? aPtr : bPtr);
        return head.next;
    }
}
```

感慨原来思路可以这样拓展，我的思路一实在有些复杂，然后也是超时了

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

***

## 进阶：结合[21](21-he-bing-liang-ge-you-xu-lian-biao.md)、运用分治法的合并

```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        return mergeKLists(lists, 0, lists.length);
    }

    // 合并从 lists[i] 到 lists[j-1] 的链表
    private ListNode mergeKLists(ListNode[] lists, int i, int j) {
        int m = j - i;
        if (m == 0) {
            return null; // 注意输入的 lists 可能是空的
        }
        if (m == 1) {
            return lists[i]; // 无需合并，直接返回
        }
        ListNode left = mergeKLists(lists, i, i + m / 2); // 合并左半部分
        ListNode right = mergeKLists(lists, i + m / 2, j); // 合并右半部分
        return mergeTwoLists(left, right); // 最后把左半和右半合并
    }

    // 21. 合并两个有序链表
    private ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode dummy = new ListNode(); // 用哨兵节点简化代码逻辑
        ListNode cur = dummy; // cur 指向新链表的末尾
        while (list1 != null && list2 != null) {
            if (list1.val < list2.val) {
                cur.next = list1; // 把 list1 加到新链表中
                list1 = list1.next;
            } else { // 注：相等的情况加哪个节点都是可以的
                cur.next = list2; // 把 list2 加到新链表中
                list2 = list2.next;
            }
            cur = cur.next;
        }
        cur.next = list1 != null ? list1 : list2; // 拼接剩余链表
        return dummy.next;
    }
}
```

<figure><img src="../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>
