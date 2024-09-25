# 2、两数相加

我的思路：

1、分别取出两个链表的每个结点的数字，恢复为三位数。相加。

2、然后%10取余再/10数位分离，分别存进最新的链表

3、返回新链表

算法实现：（对于链表的实现还不熟悉）

```java
// 两个链表相加
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    // 创建一个虚拟头节点，便于处理结果链表
    ListNode dummyHead = new ListNode(0);
    ListNode p = l1, q = l2, curr = dummyHead;
    int carry = 0; // 进位变量

    // 遍历两个链表，直到最长的链表结束
    while (p != null || q != null) {
        // 如果p或q为空，则用0替代
        int x = (p != null) ? p.val : 0;
        int y = (q != null) ? q.val : 0;

        int sum = carry + x + y; // 当前位的和加上进位
        carry = sum / 10; // 更新进位
        curr.next = new ListNode(sum % 10); // 取余作为当前位的值
        curr = curr.next; // 移动到下一个节点

        // 移动指针
        if (p != null) p = p.next;
        if (q != null) q = q.next;
    }

    // 如果最后还有进位，需要再增加一个节点
    if (carry > 0) {
        curr.next = new ListNode(carry);//创建新节点
    }

    return dummyHead.next; // 返回实际的链表头节点
}
```
