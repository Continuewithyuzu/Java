# 148、排序链表

## 思路：

1、遍历链表，取出，用数组存储

2、数组排序

3、新建链表，并返回数组转链表

### 代码实现：

```java
class Solution {
    public ListNode sortList(ListNode head) {
        ListNode p = head;
        int a[] = new int[50000];
        int i = 0;
        while (p != null) {
            a[i] = p.val;
            i++;
            p = p.next;
        }
        Arrays.sort(a,0,i);//对范围内数组排序，避免对范围外的0起作用
        ListNode dummy = new ListNode(0);
        ListNode q = dummy;
        for( int j = 0; j < i; j++){
//            q.val = a[j];
//            j++;
            q.next = new ListNode(a[j]);
            q = q.next;
        }
        return dummy.next;
    }
}
```

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt="" width="563"><figcaption><p>整体的复杂度我感觉其实还是可以的</p></figcaption></figure>

### 中间出现了几个bug：

1、由于顾及到链表的长度，我在定义数组时的范围是50000，而数组的初始值默认为0，后续的代码中我排序时使用了sort(a)，由于默认值是0，排序收到了其他大于i的范围数的干扰，导致输出全是0，正确的做法应该为：sort(a，0，i)，表示对数组a从下标为0到i的数组元素进行排序

2、for循环我忘记了会自动++，在循环体中又写了j++



## 归并排序

基本原理就是首先通过快慢指针将整个链表一分为二，然后分别对这两部分排序然后合并两个链表，合并部分可以参考[21](21-he-bing-liang-ge-you-xu-lian-biao.md)

```java
class Solution {
    public ListNode sortList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }

        // 找到链表的中间节点
        ListNode slow = head, fast = head, prev = null;
        while (fast != null && fast.next != null) {
            prev = slow;
            slow = slow.next;
            fast = fast.next.next;
        }
        prev.next = null; // 将链表分成两部分

        // 递归排序
        ListNode left = sortList(head);
        ListNode right = sortList(slow);

        // 合并两个已排序的链表
        return merge(left, right);
    }

    private ListNode merge(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        ListNode current = dummy;

        while (l1 != null && l2 != null) {
            if (l1.val < l2.val) {
                current.next = l1;
                l1 = l1.next;
            } else {
                current.next = l2;
                l2 = l2.next;
            }
            current = current.next;
        }

        if (l1 != null) {
            current.next = l1;
        } else if (l2 != null) {
            current.next = l2;
        }

        return dummy.next;
    }
}
```

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt="" width="563"><figcaption><p>ps：没我的快，但是思路值得学</p></figcaption></figure>
