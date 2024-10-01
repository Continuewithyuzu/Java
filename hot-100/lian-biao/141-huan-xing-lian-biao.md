# 141、环形链表

我的思路：

1、快指针p遍历链表、慢指针q每次从头节点开始遍历

2、判断：2次while循环

如果p.next=q.next,return false

思路有点类似快慢指针法，但是由于两层while循环，超时了

```java
public class Solution {
    public boolean hasCycle(ListNode head) {
        ListNode p = head;
        ListNode q = head;
        while(p != null){
            q=head;
            while(q!=null){//3 2 0 4
                if(p==q.next){
                    return false;
                }
                q=q.next;
            }
            p=p.next;
        }
        return true;
    }
}
```

这样占用内存和空间很大

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

***

## 快慢指针法

思路：

假想「乌龟」和「兔子」在链表上移动，「兔子」跑得快，「乌龟」跑得慢。当「乌龟」和「兔子」从链表上的同一个节点开始移动时，如果该链表中没有环，那么「兔子」将一直处于「乌龟」的前方；如果该链表中有环，那么「兔子」会先于「乌龟」进入环，并且一直在环内移动。等到「乌龟」进入环时，由于「兔子」的速度快，它一定会在某个时刻与乌龟相遇，即套了「乌龟」若干圈。

代码实现

```java
public class Solution {
    public boolean hasCycle(ListNode head) {
        if (head == null || head.next == null) {
            return false;
        }
        ListNode slow = head;
        ListNode fast = head.next;
        while (slow != fast) {
            if (fast == null || fast.next == null) {
                return false;
            }
            slow = slow.next;
            fast = fast.next.next;
        }
        return true;
    }
}

```

while循环思路：

如果fast指针等于slow指针，说明相遇，那就是有环

如果走到了最后，那就是slow指针没追上fast，说明没有环

除此以外其他情况下都是有环

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

***

## 另外的解法：Hash

```java
public class Solution {
    public boolean hasCycle(ListNode head) {
        Set<ListNode> seen = new HashSet<ListNode>();
        while (head != null) {
            if (!seen.add(head)) {
                return true;
            }
            head = head.next;
        }
        return false;
    }
}
```

使用哈希表来存储所有已经访问过的节点。每次我们到达一个节点，<mark style="color:blue;">**如果该节点已经存在于哈希表中，则说明该链表是环形链表**</mark>，否则就将该节点加入哈希表中。重复这一过程，直到我们遍历完整个链表即可

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>
