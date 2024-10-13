# 栈和队列

队列是先进先出，栈是先进后出

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

## 栈Stack

在 Java 中，栈（Stack）是一种后进先出（LIFO）的数据结构，用于存储元素。在栈中，只有栈顶的元素是可见的和可访问的，其他元素都被隐藏起来，直到栈顶的元素被移除或弹出。Java 中的 java.util.Stack 类实现了这种栈的数据结构，并且是线程安全的，继承自 Vector 类。

压栈：栈的插入操作叫做进栈 / 压栈 / 入栈， **入数据在栈顶** 。

出栈：栈的删除操作叫做出栈。 **出数据在栈顶** 。

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

### 基本操作

| 方法              | 功能         |
| --------------- | ---------- |
| Stack()         | 构造一个空的栈    |
| E push(E e)     | 将e入栈，并返回e  |
| E pop()         | 将栈顶元素出栈并返回 |
| E peek()        | 获取栈顶元素     |
| int size()      | 获取栈中有效元素个数 |
| boolean empty() | 检测栈是否为空    |

#### 代码示例：

```java
import java.util.Stack;
 
public class StackExample {
    public static void main(String[] args) {
        Stack<String> stack = new Stack<>();
        
        // 压栈操作
        stack.push("Java");
        stack.push("Python");
        stack.push("C++");
        
        // 弹栈操作
        String topLanguage = stack.pop();
        System.out.println("弹出栈顶元素：" + topLanguage);
        
        // 查看栈顶元素
        String currentTop = stack.peek();
        System.out.println("当前栈顶元素：" + currentTop);
        
        // 判空操作
        if (stack.isEmpty()) {
            System.out.println("栈为空");
        } else {
            System.out.println("栈不为空");
        }
    }
}
```

栈在 Java 中常用于处理需要后进先出顺序的场景，例如表达式求值、逆序输出等。

***

## 队列Queue

队列（Queue）是一种先进先出（FIFO）的数据结构，用于存储元素。队列在 java.util 包中有多种实现，如 LinkedList、ArrayDeque 和 PriorityQueue。只允许在一端进行插入数据操作，在另一端进行删除数据操作的特殊线性表，队列具有先进先出FIFO(First In First Out) 入队列：进行插入操作的一端称为队尾（Tail/Rear） 出队列：进行删除操作的一端称为队头（Head/Front）

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

### 基本操作 <a href="#f0-9f-92-bd2.-e5-9f-ba-e6-9c-ac-e6-93-8d-e4-bd-9c" id="f0-9f-92-bd2.-e5-9f-ba-e6-9c-ac-e6-93-8d-e4-bd-9c"></a>

| 方法                 | 功能          |
| ------------------ | ----------- |
| boolean offer(E e) | 入队列         |
| E poll()           | 出队列         |
| peek()             | 获取队头元素      |
| int size()         | 获取队列中有效元素个数 |
| boolean isEmpty()  | 检测队列是否为空    |

**注意**：Queue是个接口，在实例化时必须实例化LinkedList的对象，因为LinkedList实现了Queue接口。

#### 代码：

```java
public static void main(String[] args) {
    Queue<Integer> q = new LinkedList<>();
    q.offer(1);
    q.offer(2);
    q.offer(3);
    q.offer(4);
    q.offer(5); // 从队尾入队列
    System.out.println(q.size());
    System.out.println(q.peek()); // 获取队头元素
    q.poll();
    System.out.println(q.poll()); // 从队头出队列，并将删除的元素返回
    if(q.isEmpty()){
    System.out.println("队列空");
    }else{
    System.out.println(q.size());
    }
}
```
