# 234、回文链表

思路：

一如既往，想到了用数组解决

1、遍历链表，依次取出链表元素，存进数组中

2、for循环双向遍历链表判断



## 代码实现：

```java
class Solution {
    public boolean isPalindrome(ListNode head) {
        int []arr = new int[100000];
        ListNode p = head;
        int i=0;
        while(p != null && i<arr.length) {
            arr[i]=p.val;
            p=p.next;
            i++;
        }
        for(int j=0;j<i+1/2;j++) {
            if(arr[j]!=arr[i-1-j]) {
                return false;
            }
        }
        return true;
    }
}
```

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

***

## 方法二：双指针法

```java
class Solution {
    public boolean isPalindrome(ListNode head) {
        List<Integer> vals = new ArrayList<Integer>();

        // 将链表的值复制到数组中
        ListNode currentNode = head;
        while (currentNode != null) {
            vals.add(currentNode.val);
            currentNode = currentNode.next;
        }

        // 使用双指针判断是否回文
        int front = 0;
        int back = vals.size() - 1;
        while (front < back) {
            if (!vals.get(front).equals(vals.get(back))) {
                return false;
            }
            front++;
            back--;
        }
        return true;
    }
}
```

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

***

## 更快的解法：反转链表、快慢指针法&#x20;

时间复杂度O(n)、空间复杂度O(1)

```java
class Solution {

    //反转链表
    public ListNode reverse(ListNode head) {
        ListNode prev = null;
        while (head != null) {
            ListNode next = head.next;
            head.next = prev;
            prev = head;
            head = next;
        }
        return prev;
    }

    public boolean isPalindrome(ListNode head) {
        ListNode fast = head, slow = head;
        //通过快慢指针找到中点
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        //如果fast不为空，说明链表的长度是奇数个
        if (fast != null) {
            slow = slow.next;
        }
        //反转后半部分链表
        slow = reverse(slow);

        fast = head;
        while (slow != null) {
            //然后比较，判断节点值是否相等
            if (fast.val != slow.val)
                return false;
            fast = fast.next;
            slow = slow.next;
        }
        return true;
    }
}
```

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

***

## 栈解法：（慢）：

```java
public boolean isPalindrome(ListNode head) {
    ListNode fast = head, slow = head;
    //通过快慢指针找到中点
    while (fast != null && fast.next != null) {
        fast = fast.next.next;
        slow = slow.next;
    }
    //如果fast不为空，说明链表的长度是奇数个
    if (fast != null) {
        slow = slow.next;
    }
    //反转后半部分链表
    slow = reverse(slow);

    fast = head;
    while (slow != null) {
        //然后比较，判断节点值是否相等
        if (fast.val != slow.val)
            return false;
        fast = fast.next;
        slow = slow.next;
    }
    return true;
}

//反转链表
public ListNode reverse(ListNode head) {
    ListNode prev = null;
    while (head != null) {
        ListNode next = head.next;
        head.next = prev;
        prev = head;
        head = next;
    }
    return prev;
}
```

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>
