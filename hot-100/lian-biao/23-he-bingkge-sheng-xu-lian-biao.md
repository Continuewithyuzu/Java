---
description: 属于是21的进阶版了
---

# 23、合并K个升序链表

思路一：

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

思路二：

用一个新的链表，把所有的元素按顺序遍历取出。然后依照[148](148-pai-xu-lian-biao.md)排序链表，可以数组，可以分治
