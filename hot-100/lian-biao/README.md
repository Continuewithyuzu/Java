# 链表

## LinkList类

* 实现了List接口
* LinkedList的底层使用了双向链表
* LinkedList没有实现RandomAccess接口，因此LinkedList不支持随机访问
* LinkedList的任意位置插入和删除元素时效率比较高，时间复杂度为O(1)
* LinkedList比较适合任意位置插入的场景&#x20;

&#x20;在Java中，Java标准库中提供了`LinkedList`类，它是基于链表的一个实现，并且已经封装好了许多常用的链表操作。你不需要手动定义基本的链表操作函数，Java 的 `LinkedList` 类已经包含了以下常用的方法：

<figure><img src="../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **添加元素**：
  * `add(E e)`: 在链表末尾添加元素。
  * `addFirst(E e)`: 在链表开头添加元素。
  * `addLast(E e)`: 在链表末尾添加元素（与`add`方法相同）。
* **删除元素**：
  * `remove()`: 删除并返回链表的第一个元素。
  * `removeFirst()`: 删除并返回链表的第一个元素（与`remove`方法相同）。
  * `removeLast()`: 删除并返回链表的最后一个元素。
  * `remove(E e)`: 删除指定元素。
* **获取元素**：
  * `get(int index)`: 获取链表中指定索引位置的元素。
  * `getFirst()`: 获取链表的第一个元素。
  * `getLast()`: 获取链表的最后一个元素。
* **其他操作**：
  * `size()`: 返回链表的元素数量。
  * `isEmpty()`: 判断链表是否为空。
  * `contains(Object o)`: 判断链表中是否包含某个元素。

### 示例代码:

1、

```java
import java.util.LinkedList;
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        LinkedList<String> list = new LinkedList<>();
        List<String> list2 = new java.util.ArrayList<>();
        // 使用ArrayList构造LinkedList
        List<String> list3 = new LinkedList<>(list2);
        // 添加元素
        list.add("A");
        list.add("B");
        list.addFirst("C");
        list.addLast("D");

        // 获取元素
        System.out.println("第一个元素: " + list.getFirst());
        System.out.println("最后一个元素: " + list.getLast());

        // 删除元素
        list.removeFirst();
        list.removeLast();

        System.out.println("链表内容: " + list);
    }
}
```

2、

```java
public static void main(String[] args) {
    LinkedList<Integer> list = new LinkedList<>();
    list.add(1); // add(elem): 表示尾插
    list.add(2);
    list.add(3);
    list.add(4);
    list.add(5);
    list.add(6);
    list.add(7);
    System.out.println(list.size());
    System.out.println(list);
    // 在起始位置插入0
    list.add(0, 0); // add(index, elem): 在index位置插入元素elem
    System.out.println(list);
    list.remove(); // remove(): 删除第一个元素，内部调用的是removeFirst()
    list.removeFirst(); // removeFirst(): 删除第一个元素
    list.removeLast(); // removeLast(): 删除最后元素
    list.remove(1); // remove(index): 删除index位置的元素
    System.out.println(list);
    // contains(elem): 检测elem元素是否存在，如果存在返回true，否则返回false
    if(!list.contains(1)){
        list.add(0, 1);
}
    list.add(1);
    System.out.println(list);
    System.out.println(list.indexOf(1)); /*indexOf(elem): 从前往
    后找到第一个elem的位置*/
    System.out.println(list.lastIndexOf(1)); /*lastIndexOf(elem): 从后
    往前找第一个1的位置*/
    int elem = list.get(0); // get(index): 获取指定位置元素
    list.set(0, 100); // set(index, elem): 将index位置的元素设置为elem
    System.out.println(list);
    /*subList(from, to): 用list中[from, to)之间
    的元素构造一个新的LinkedList返回*/
    List<Integer> copy = list.subList(0, 3); 
    System.out.println(list);
    System.out.println(copy);
    list.clear(); // 将list中元素清空
    System.out.println(list.size());
}
```

***

## 遍历：

3种遍历：for、foreach、迭代器

```java
public static void main(String[] args) {
    LinkedList<Integer> list = new LinkedList<>();
    list.add(1); // add(elem): 表示尾插
    list.add(2);
    list.add(3);
    list.add(4);
    list.add(5);
    list.add(6);
    list.add(7);
    System.out.println(list.size());
    // foreach遍历
    for (int e:list) {
        System.out.print(e + " ");
    }
    System.out.println();
    // 使用迭代器遍历---正向遍历
    ListIterator<Integer> it = list.listIterator();
    while(it.hasNext()){
    System.out.print(it.next()+ " ");
    }
    System.out.println();
    // 使用反向迭代器---反向遍历
    ListIterator<Integer> rit = list.listIterator(list.size());
    while (rit.hasPrevious()){
    System.out.print(rit.previous() +" ");
    }
    System.out.println();
}
```

***

## 注意

在Java中，`ListNode` 类与 `LinkedList` 类是两个不同的概念。

1.  **`ListNode` 类**：这是通常在数据结构中表示链表节点的类，通常包含节点的值（`val`）和指向下一个节点的引用（`next`）。例如：

    ```java
    class ListNode {
        int val;
        ListNode next;

        ListNode(int val) {
            this.val = val;
        }
    }
    ```
2. **`LinkedList` 类**：这是 Java 标准库中的一个类，属于 `java.util` 包，实现了 `List` 接口，是一个双向链表的实现。它已经封装了对链表操作的常用方法，如 `add()`, `remove()`, `get()` 等。

因此，**`ListNode` 类不能直接使用 `LinkedList` 类的封装函数**，因为它们属于不同的类型。`LinkedList` 类是一个完整的链表实现，而 `ListNode` 只是一个节点类。如果你想要利用 `LinkedList` 的方法，可以直接使用 `LinkedList` 类，而不是自己定义的 `ListNode` 类。

如果你想操作 `ListNode` 实现的链表，就需要自己手动编写相关操作函数，比如插入节点、删除节点等。

需要区分的是：

* 如果你需要操作 **单个节点**，那是 `ListNode` 的职责。
* 如果你需要操作 **整个链表**，可以选择自己实现链表操作，或者使用 Java 提供的 `LinkedList` 类。

***

## 基本原理介绍

链表是一种数据结构，和数组同级。比如，Java中我们使用的[ArrayList](https://so.csdn.net/so/search?q=ArrayList\&spm=1001.2101.3001.7020)，其实现原理是数组。而LinkedList的实现原理就是链表了。链表在进行循环遍历时效率不高，但是插入和删除时优势明显。

（Ps :有好多种链表：单向、双向、循环、有头、无头，排列组合一下有8种)

单向链表是一种<mark style="color:blue;">**线性表**</mark>，实际上是由节点（Node）组成的，一个链表拥有不定数量的节点。其数据在内存中存储是不连续的，它存储的数据分散在内存中，每个结点只能也只有它能知道下一个结点的存储位置。由N各节点（Node）组成单向链表，每一个Node记录本Node的数据及下一个Node。向外暴露的只有一个头节点（Head），我们对链表的所有操作，都是直接或者间接地通过其<mark style="color:blue;">**头节点**</mark>来进行的。

节点（Node）是由一个<mark style="color:blue;">**需要储存的对象及对下一个节点的引用**</mark>组成的。也就是说，节点拥有两个成员：<mark style="color:blue;">储存的对象、对下一个节点的引用</mark>。&#x20;

<figure><img src="../../.gitbook/assets/image (13).png" alt="" width="375"><figcaption></figcaption></figure>

## 单向链表的实现

<pre class="language-java"><code class="lang-java"><strong> class MyLink {
</strong>    Node head = null; // 头节点
    
    // 链表中的节点，data代表节点的值，next是指向下一个节点的引用
    class Node {
        Node next = null;// 节点的引用，指向下一个节点
        int data;// 节点的对象，即内容

        public Node(int data) {
            this.data = data;
        }
    }

    // 向链表中插入数据
    public void addNode(int d) {
        Node newNode = new Node(d);// 实例化一个节点
        if (head == null) {
            head = newNode;
            return;
        }
        Node tmp = head;
        while (tmp.next != null) {
            tmp = tmp.next;
        }
        tmp.next = newNode;
    }

    //删除第index个节点
    public boolean deleteNode(int index) {
        if (index &#x3C; 1 || index > length()) {
            return false;
        }
        if (index == 1) {
            head = head.next;
            return true;
        }
        int i = 1;
        Node preNode = head;
        Node curNode = preNode.next;
        while (curNode != null) {
            if (i == index) {
                preNode.next = curNode.next;
                return true;
            }
            preNode = curNode;
            curNode = curNode.next;
            i++;
        }
        return false;
    }

    //返回节点长度
    public int length() {
        int length = 0;
        Node tmp = head;
        while (tmp != null) {
            length++;
            tmp = tmp.next;
        }
        return length;
    }

    
 //在不知道头指针的情况下删除指定节点 
    public boolean deleteNode11(Node n) {
        if (n == null || n.next == null)
            return false;
        int tmp = n.data;
        n.data = n.next.data;
        n.next.data = tmp;
        n.next = n.next.next;
        System.out.println("删除成功！");
        return true;
    }

    public void printList() {
        Node tmp = head;
        while (tmp != null) {
            System.out.println(tmp.data);
            tmp = tmp.next;
        }
    }

    public static void main(String[] args) {
        MyLink list = new MyLink();
        list.addNode(5);
        list.addNode(3);
        list.addNode(1);
        list.addNode(2);
        list.addNode(55);
        list.addNode(36);
        System.out.println("linkLength:" + list.length());
        System.out.println("head.data:" + list.head.data);
        list.printList();
        list.deleteNode(4);
        System.out.println("After deleteNode(4):");
        list.printList();
    }
}

</code></pre>

***

## 虚拟头节点的创建和使用

用到这个知识点的例题： 2、206

虚拟头节点是实际存在的，只不过<mark style="color:blue;">它存放的元素是空，指向的下一个节点也是空</mark>。

一旦设立了虚拟头节点，整个链表中所有的节点都会有1个前驱节点，这样一来，我们在任意位置执行增、删、改、查都将变得简单且操作统一。如果没有设置虚拟头结点而是使用头指针，则须要if-else逻辑判空的操作。

### 头指针VS虚拟头节点 代码示例

```java
/**这里自定义一个链表，仅实现了添加（按照顺序插入）字符串的元素操作 */
public class LinekedList {

    private Node<String> head;/**头指针*/

    /** 按照顺序依次添加-使用头指针实现链表的元素插入*/
    public void addElement(String value) {
        Node<String> node = new Node<>(value);
        if (head == null) {
            node.next = head; // 将node插入到head的前面，完成插入。
            // 指针后移
            head = node; // 移动head指针到node上（将node作为新的非空head指针）为后续插入做准备。
        } else {
            node.next = head.next; // 将node指针指向head的后驱节点
            head.next = node; // 将head指针指向node节点，完成插入。
			// 指针后移
            head = node; // 移动head指针移动到新插入的node节点上,为后续插入做准备。
            // (即将原先指向非空head节点的指针改换指向到node节点上，将node节点作为新的非空头指针）
        }
    }


    /**虚拟头结点*/
    private Node<String> dummyHead = new Node<>(null,null);

    /** 按照顺序依次添加-使用虚拟头结点实现链表的元素插入 */
    public void fillElement(String value) {
        Node<String> node = new Node<>(value);
        node.next = dummyHead.next; // 将node指针指向dummyHead的后驱节点
        dummyHead.next = node; // 将dummyHead指针指向node节点，完成插入。
		// 指针后移
        dummyHead = node; // 移动dummyHead指针到新插入的node节点上,为后续插入做准备。
        // (即将原先指向dummyHead的指针改换指向到node节点上，将node节点作为新的虚拟头结点）
    }
	/**虚拟头结点*/
    private Node<String> dummyHeader = new Node<>(null,null);

    /**按照下标插入*/
    public void fillElement(int index, String value) {
        Node<String> dummyHeaderTemp = dummyHeader;
        while(index-- > 0) {
        	// 指针后移,移动到指定插入下标位置
            dummyHeader = dummyHeader.next; // 获取到所要添加节点位置的前驱节点
            // (其实就是移动指向虚拟头结点的指针到所要添加节点位置的前驱节点，
            // 然后将该前驱节点作为新的虚拟头结点，此时新的虚拟头结点data和next都非空)
        }

        Node<String> node = new Node<>(value);
        node.next = dummyHeader.next; // 将node指针指向dummyHeader的后驱节点
        dummyHeader.next = node; // 将dummyHeader指针指向node节点，从而完成插入。

        dummyHeader = dummyHeaderTemp; // 将dummyHeader指针指向原虚拟头结点dummyHeader
        // 目的是，再次以下标插入时仍然以虚拟头结点作为开始。
    }
    
    class Node<E> {
        private E data;
        public Node next;
        public Node(E data){
            this.data = data;
        }
        public Node(E data, Node<E> next) {
            this.data = data;
            this.next = next;
        }
    }
}

```

* **简化边界条件处理：** 在对链表进行插入、删除等操作时，头节点的位置往往需要特殊处理。使用虚拟头节点可以统一这些操作，避免对头节点进行单独的逻辑处理。
* **减少空指针异常：** 虚拟头节点的存在确保了链表始终有一个节点，`head` 不会为 `null`，从而减少了空指针异常的可能性。
* **代码更简洁：** 统一的处理方式使代码更为简洁，易于维护。

***

## 运用场景

1、删除链表中的某个节点：

```java
public ListNode removeElements(ListNode head, int val) {
    ListNode dummyHead = new ListNode(0);
    dummyHead.next = head;
    ListNode current = dummyHead;
    while (current.next != null) {
        if (current.next.val == val) {
            current.next = current.next.next;
        } else {
            current = current.next;
        }
    }
    return dummyHead.next;
}
```

2、合并两个有序链表：

```java
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    ListNode dummyHead = new ListNode(0);
    ListNode current = dummyHead;
    while (l1 != null && l2 != null) {
        if (l1.val <= l2.val) {
            current.next = l1;
            l1 = l1.next;
        } else {
            current.next = l2;
            l2 = l2.next;
        }
        current = current.next;
    }
    current.next = (l1 != null) ? l1 : l2;
    return dummyHead.next;
}
```

#### **注意事项**

* **实际头节点：** 操作完成后，<mark style="color:blue;">**链表的实际头节点是**</mark><mark style="color:blue;">** **</mark><mark style="color:blue;">**`dummyHead.next`**</mark>，而不是 `dummyHead` 本身。（返回<mark style="color:blue;">**`dummyHead.next`**</mark>)
* **空间开销：** 虚拟头节点会占用额外的空间，但相对于链表的整体，这个开销通常可以忽略不计。
