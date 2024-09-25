---
description: >-
  在Java中，哈希（Hash）是一个广泛应用于数据结构和算法中的概念，主要用于快速查找、存储和比较数据。哈希的核心在于哈希函数（Hash
  Function），它将输入（通常称为键，key）映射到一个固定范围的输出值，这个输出值称为哈希值（Hash
  Value）或哈希码（HashCode）。哈希的目的在于将原本复杂、不规则的数据转化为简洁的、固定长度的值，使得数据的存储和检索更加高效。
hidden: true
---

# 哈希 Hash Set and Hash Map

## Hashcode()方法

Java中的每个对象都继承自Object类，而Object类有一个hashCode()方法，这个方法被设计用来返回对象的哈希码。默认的hashCode()实现通常基于<mark style="color:blue;">**对象的内存地址**</mark>，但子类通常会重写此方法，以便根据对象的实际内容生成更有意义的哈希值，这对于使用对象作为键的哈希表操作尤为重要。

作用：

hashCode()方法返回对象的哈希码值（哈希码），是一个int类型的整数。 哈希码是<mark style="color:blue;">根据对象的内存地址或者根据对象的内容计算得到的一个唯一标识符</mark>。 在Java中，hashCode()方法通常与equals()方法一起使用，用于<mark style="color:blue;">**判断两个对象是否相等**</mark>。 默认实现：

在Object类中，hashCode()方法的默认实现是根据对象的内存地址计算得到的哈希码。 换句话说，如果两个对象在内存中的地址不同，那么它们的哈希码也会不同。 重写规则：

在自定义类中，通常需要重写hashCode()方法，以便根据对象的内容来生成哈希码，而不是依赖于默认的内存地址。 如果重写了equals()方法，就应该同时重写hashCode()方法，保证相等的对象拥有相等的哈希码。 重写hashCode()方法时，应该遵循以下规则： 相等的对象必须具有相等的哈希码。 不相等的对象尽量产生不同的哈希码，以减少哈希冲突的发生。 使用场景：

在集合类中，如<mark style="color:blue;">**HashMap、HashSet等，hashCode()方法被用于确定对象在集合中的存储位置，加快数据的查找速度。 当我们需要比较自定义类的对象是否相等时，通常会重写equals()和hashCode()**</mark>**方法**。 总之，Object类的hashCode()方法是用于获取对象的哈希码的方法，可以通过重写该方法来根据对象的内容生成哈希码，以便在集合中进行快速查找和比较。

### `String`类是一个典型重写了`hashCode()`方法的类，它根据字符串的内容计算哈希值，这意味着内容相同的字符串将拥有相同的哈希值，这有助于在哈希表中快速定位和比较字符串。



## Hash 碰撞（也叫Hash冲突） 这块晚点在学

<figure><img src="../.gitbook/assets/image (4).png" alt="" width="375"><figcaption></figcaption></figure>



## Hash Map

### 1、定义 <a href="#e2-9c-92-ef-b8-8f1.-e5-ae-9a-e4-b9-89" id="e2-9c-92-ef-b8-8f1.-e5-ae-9a-e4-b9-89"></a>

Java中的HashMap是一个实现Map接口的类，它提供了一个存储键值对（key-value pairs）的数据结构。HashMap允许使用唯一的键来映射到特定的值，并且能够高效地进行插入、删除和查找操作。键值对之间没有特定的顺序，HashMap也不是线程安全的。

### 2、基本操作

在Java中，`HashMap` 是非常常用的集合类，存储键值对（key-value）。以下是 `HashMap` 的一些基本常用操作：

1.  **创建 `HashMap`：**

    ```java
    HashMap<Integer, String> map = new HashMap<>();
    ```
2.  **添加键值对 (`put`)：**

    ```java
    map.put(1, "Apple");
    map.put(2, "Banana");
    ```
3.  **通过键获取值 (`get`)：**

    ```java
    String value = map.get(1); // 返回 "Apple"
    ```
4.  **检查是否包含某个键 (`containsKey`)：**

    ```java
    boolean hasKey = map.containsKey(1); // true
    ```
5.  **检查是否包含某个值 (`containsValue`)：**

    ```java
    boolean hasValue = map.containsValue("Apple"); // true
    ```
6.  **删除键值对 (`remove`)：**

    ```java
    map.remove(1); // 移除键为1的键值对
    ```
7.  **获取 `HashMap` 大小 (`size`)：**

    ```java
    int size = map.size(); // 返回键值对的数量
    ```
8.  **遍历 `HashMap` 键值对：**

    ```java
    for (Map.Entry<Integer, String> entry : map.entrySet()) {
        Integer key = entry.getKey();
        String value = entry.getValue();
        System.out.println(key + " = " + value);
    }
    ```
9.  **清空 `HashMap` (`clear`)：**

    ```java
    map.clear(); // 移除所有键值对
    ```
10. **检查 `HashMap` 是否为空 (`isEmpty`)：**

    ```java
    boolean isEmpty = map.isEmpty(); // true 如果是空的
    ```
11. **获取所有键 (`keySet`)：**

    ```java
    Set<Integer> keys = map.keySet();
    ```
12. **获取所有值 (`values`)：**

    ```java
    Collection<String> values = map.values();
    ```

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

这些操作涵盖了 `HashMap` 的大部分常见功能，方便用于存储和管理键值对数据。

示例代码：

```java
import java.util.HashMap;
import java.util.Map;
 
public class HashMapExample {
    public static void main(String[] args) {
        // 创建一个HashMap实例
        HashMap<String, Integer> myHashMap = new HashMap<>();
 
        // 添加键值对
        myHashMap.put("Apple", 1);
        myHashMap.put("Banana", 2);
        myHashMap.put("Cherry", 3);
        System.out.println("HashMap after adding elements: " + myHashMap);
 
        // 更新键对应的值
        myHashMap.put("Apple", 4);
        System.out.println("HashMap after updating 'Apple': " + myHashMap);
 
        // 检查键是否存在
        boolean isPresent = myHashMap.containsKey("Banana");
        System.out.println("Is 'Banana' a key in the HashMap? " + isPresent);
 
        // 删除键值对
        myHashMap.remove("Banana");
        System.out.println("HashMap after removing 'Banana': " + myHashMap);
 
        // 遍历HashMap
        System.out.println("Iterating over HashMap:");
        for (Map.Entry<String, Integer> entry : myHashMap.entrySet()) {
            System.out.println("Key: " + entry.getKey() + ", Value: " + entry.getValue());
        }
 
        // 获取特定键的值
        Integer appleValue = myHashMap.get("Apple");
        System.out.println("Value of 'Apple': " + appleValue);
 
        // 检查一个键是否存在且获取其值
        Integer orangeValue = myHashMap.getOrDefault("Orange", -1); // 如果没有找到键'Orange'，则返回-1
        System.out.println("Value of 'Orange' or default: " + orangeValue);
    }
}
```

### 3.特性

**键值关联**：HashMap存储的是键值对，其中<mark style="color:blue;">**键是唯一的，而值可以重复**</mark>。

无序性：HashMap中的元素没有特定的顺序，迭代时的顺序并不反映插入时的顺序。 允许null值和null键：HashMap是少数几个可以接受null键和null值的Java集合之一，但每个HashMap只能有一个null键。 线程不安全：HashMap不是线程安全的，多线程环境下若不采取额外的同步措施，可能导致数据不一致性

可调整大小：随着元素的增加，HashMap会自动扩容来维持其性能，通过重新哈希所有元素到更大的数组中实现

性能：平均情况下，HashMap提供O(1)的时间复杂度进行插入、删除和查找操作。&#x20;

### 4.内部实现

哈希表：HashMap的底层实现是一个哈希表，它由一个动态调整大小的数组（称为桶或bin）组成，数组的每个位置可以是一个链表或红黑树（JDK 8开始）

哈希函数：HashMap使用哈希函数将键转换成数组的索引。哈希冲突通过链地址法解决，即在同一索引位置的多个元素通过链表或红黑树链接起来。

负载因子：HashMap有一个负载因子，默认为0.75，它决定了HashMap何时进行扩容。当HashMap中的元素数量超过当前容量乘以负载因子时，HashMap会自动扩容，一般扩容为原来的两倍。

扩容机制：扩容时，HashMap会创建一个新的更大容量的数组，并将原数组中的所有元素重新哈希到新数组中，这个过程涉及到重新计算哈希值和重新分配。

### 5.应用场景

缓存：HashMap非常适合做轻量级的缓存，快速存取热点数据。

数据映射：在需要快速根据键查找相关联值的场景，如配置参数管理。

计数：可以用HashMap统计元素出现的频率，键是元素，值是出现次数。

去重：虽然HashSet更直接，但在需要存储额外信息或自定义比较逻辑时，HashMap可以用来去重。 图的邻接表表示：在图算法中，HashMap可以用来表示顶点的邻接关系，键是顶点，值是一个列表或集合，包含与该顶点相邻的所有顶点。

## Hash Set

### 1、定义

&#x20;Java中的HashSet是一个实现了Set接口的集合类，它提供了一种存储不可重复元素的高效数据结构。HashSet的实现基于HashMap，这意味着它内部使用了哈希表来管理元素，这使得HashSet能够提供快速的插入、删除和查找操作。

### 2、基本操作

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption><p>基本操作</p></figcaption></figure>

示例代码

```java
import java.util.HashSet;
 
public class HashSetExample {
    public static void main(String[] args) {
        // 创建一个HashSet实例
        HashSet<String> myHashSet = new HashSet<>();
 
        // 添加元素
        myHashSet.add("Apple");
        myHashSet.add("Banana");
        myHashSet.add("Cherry");
        System.out.println("HashSet after adding elements: " + myHashSet);
 
        // 检查元素是否存在
        boolean isPresent = myHashSet.contains("Banana");
        System.out.println("Is 'Banana' in the HashSet? " + isPresent);
 
        // 尝试添加重复元素
        myHashSet.add("Apple");
        System.out.println("HashSet after trying to add duplicate 'Apple': " + myHashSet);
        
        // 删除元素
        boolean isRemoved = myHashSet.remove("Banana");
        System.out.println("Is 'Banana' removed? " + isRemoved);
        System.out.println("HashSet after removing 'Banana': " + myHashSet);
 
        // 遍历HashSet
        System.out.println("Iterating over HashSet:");
        for (String fruit : myHashSet) {
            System.out.println(fruit);
        }
        
        // 清空HashSet
        myHashSet.clear();
        System.out.println("HashSet after clearing: " + myHashSet);
    }
}
```

### 3、特性

&#x20;**无序性**：HashSet不保证元素的插入顺序，每次遍历HashSet时，元素的顺序可能不同。这是因为HashSet在内部使用哈希表，元素的存储位置由其<mark style="color:blue;">**哈希值**</mark>决定。

**不允许重复**：HashSet中<mark style="color:blue;">不能包含重复的元素</mark>。这是通过比较元素的哈希值以及equals()方法来实现的。如果两个元素的哈希值相同，并且通过equals()方法比较也认为是相等的，则视为重复元素，后者将不会被加入集合中。

**允许null值**：HashSet允许存储一个null元素，因为HashMap允许一个键为null。

**非线程安全**：HashSet不是线程安全的。如果多个线程同时访问一个HashSet，且至少有一个线程修改了HashSet，则必须通过外部同步来保证线程安全。

### 4、内部实现

基于HashMap：HashSet实际上是一个包装器，它将每个元素作为HashMap的键，<mark style="color:blue;">**并且所有元素共享一个静态的、唯一的值对象作为映射的值**</mark>。这意味着HashSet中元素的添加、删除等操作实际上是在操作底层的HashMap。

哈希值与索引：当向HashSet添加元素时，首先调用该元素的hashCode()方法计算哈希值，然后使用哈希值来确定元素在底层数组中的索引位置。如果该位置已有元素（哈希冲突），则使用链地址法（在JDK 7及以前是单向链表，在JDK 8中引入了红黑树，当链表长度超过8时会转换为红黑树）来存储多个具有相同索引的元素。

扩容机制：当HashSet中的元素数量超过其当前容量乘以负载因子时，HashSet会自动进行扩容，以减少哈希冲突并保持高效的查找性能。扩容包括创建一个新的更大的数组，并将原数组中的所有元素重新哈希到新数组中。

重写equals()与hashCode()：为了确保HashSet能正确识别重复元素，存储在HashSet中的自定义对象必须正确重写equals()和hashCode()方法，保证相等的对象具有相同的哈希值，并且通过equals()方法判断也为相等。

### 5.应用场景&#x20;

Java中的HashSet是一个<mark style="color:blue;">**高效无序且不允许重复元素**</mark>的集合类，基于HashMap实现。

它的核心应用场景包括<mark style="color:blue;">**数据去重、集合运算、缓存实现、快速查找成员、统计唯一元素、辅助高级数据结构及游戏开发中的对象管理**</mark>等。 HashSet利用哈希机制提供快速的插入、删除和查找功能，特别适合需要高效率集合操作的场景。 HashSet是Java集合框架中一个非常实用的类，特别适用于需要快速插入、删除和查找，且不需要维护元素插入顺序的场景。理解其基于HashMap的实现以及如何利用哈希机制来管理元素，对于高效使用HashSet至关重要。
