# LinkedList

LinkedList是Java中提供的双向链表实现的数据结构。它实现了List接口，因此可以像操作普通的列表一样对其进行操作，同时也支持队列和栈的操作。与ArrayList相比，LinkedList在插入和删除元素时具有更好的性能，因为它不需要移动其他元素。但是在访问特定位置的元素时，LinkedList的性能较差，因为需要从头或尾开始遍历链表。总的来说，LinkedList适合频繁进行插入和删除操作的场景。&#x20;

* LinkedList实现了List接口
* LinkedList的底层使用了双向链表&#x20;
* LinkedList没有实现RandomAccess接口，因此LinkedList不支持随机访问&#x20;
* LinkedList的任意位置插入和删除元素时效率比较高，时间复杂度为O(1)&#x20;
* LinkedList比较适合任意位置插入的场景&#x20;

## 具体使用

### 构造

```java
public static void main(String[] args) {
    // 构造一个空的LinkedList
    List<Integer> list1 = new LinkedList<>();
    List<String> list2 = new java.util.ArrayList<>();
    list2.add("JavaSE");
    list2.add("JavaWeb");
    list2.add("JavaEE");
    // 使用ArrayList构造LinkedList
    List<String> list3 = new LinkedList<>(list2);
}
```

### 常见操作

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

#### 代码：

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

### 遍历：

LinkedList 可以使用三方方式遍历：for循环+下标、foreach、使用迭代器

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
