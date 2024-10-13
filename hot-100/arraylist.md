# Arraylist

在集合框架中，ArrayList是一个普通的类，实现了List接口

* ArrayList是以泛型方式实现的，使用时必须要先实例化
* &#x20;ArrayList实现了RandomAccess接口，表明ArrayList支持随机访问&#x20;
* ArrayList实现了Cloneable接口，表明ArrayList是可以clone的&#x20;
* ArrayList实现了Serializable接口，表明ArrayList是支持序列化的&#x20;
* 和Vector不同，ArrayList不是线程安全的，在单线程下可以使用，在多线程中可以选择Vector或者CopyOnWriteArrayList&#x20;
* ArrayList底层是一段连续的空间，并且可以动态扩容，是一个动态类型的顺序表&#x20;

## 构造方法

```java
public static void main(String[] args) {
    // ArrayList创建，推荐写法
    // 构造一个空的列表
        List<Integer> list1 = new ArrayList<>();
    // 构造一个具有10个容量的列表
        List<Integer> list2 = new ArrayList<>(10);
        list2.add(1);
        list2.add(2);
        list2.add(3);
    // list2.add("hello"); // 编译失败，List<Integer>已经限定了，list2中只能存储整形元素
    // list3构造好之后，与list中的元素一致
        ArrayList<Integer> list3 = new ArrayList<>(list2);
    // 避免省略类型，否则：任意类型的元素都可以存放，使用时将是一场灾难
        List list4 = new ArrayList();
        list4.add("111");
        list4.add(100);
    }
```

### 常见操作

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

```java
public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("JavaSE");
        list.add("JavaWeb");
        list.add("JavaEE");
        list.add("JVM");
        list.add("测试课程");
        System.out.println(list);
        // 获取list中有效元素个数
        System.out.println(list.size());
        // 获取和设置index位置上的元素，注意index必须介于[0, size)间
        System.out.println(list.get(1));
        list.set(1, "JavaWEB");
        System.out.println(list.get(1));
        /*在list的index位置插入指定元素，
        index及后续的元素统一往后搬移一个位置*/
        list.add(1, "Java数据结构");
        System.out.println(list);
        // 删除指定元素，找到了就删除，该元素之后的元素统一往前搬移一个位置
        list.remove("JVM");
        System.out.println(list);
        /* 删除list中index位置上的元素，注意index
        不要超过list中有效元素个数,否则会抛出下标越界异常*/
        list.remove(list.size()-1);
        System.out.println(list);
}
        // 检测list中是否包含指定元素，包含返回true，否则返回false
        if(list.contains("测试课程")){
                list.add("测试课程");
        }
        // 查找指定元素第一次出现的位置：indexOf从前往后找，lastIndexOf从后往前找
        list.add("JavaSE");
        System.out.println(list.indexOf("JavaSE"));
        System.out.println(list.lastIndexOf("JavaSE"));
        /* 使用list中[0, 4)之间的元素构成一个新
        的SubList返回,但是和ArrayList共用一个elementData数组*/
        List<String> ret = list.subList(0, 4);
        System.out.println(ret);
        list.clear();
        System.out.println(list.size());
```

#### 遍历：

```java
public static void main(String[] args) {
        List<Integer> list = new ArrayList<>();
        list.add(1);
        list.add(2);
        list.add(3);
        list.add(4);
        list.add(5);
        // 使用下标+for遍历
        for (int i = 0; i < list.size(); i++) {
            System.out.print(list.get(i) + " ");
        }
        System.out.println();
        // 借助foreach遍历
        for (Integer integer : list) {
            System.out.print(integer + " ");
        }
        System.out.println();
        Iterator<Integer> it = list.listIterator();
        while(it.hasNext()){
            System.out.print(it.next() + " ");
        }
        System.out.println();
    }
```

## ArrayList的扩容机制

ArrayList是一个动态类型的顺序表，在Java中的扩容机制如下：

初始化：当创建一个ArrayList对象时，会分配一个默认大小的初始数组，通常是<mark style="color:blue;">**10个元素大小**</mark>。

添加元素：当往ArrayList中添加元素时，如果当前元素个数已经达到数组容量上限（即当前元素个数等于数组长度），则触发扩容操作。

扩容策略：一般情况下，<mark style="color:blue;">ArrayList的扩容操作会将当前数组的大小增加50%（即每次扩容后的新容量为原容量的1.5倍）</mark>，然后将原数组中的元素复制到新数组中。

数组复制：在进行扩容时，<mark style="color:blue;">**ArrayList内部会调用Arrays.copyOf()方法来创建一个新数组**</mark>，并将原数组中的元素复制到新数组中。

性能影响：由于扩容需要重新分配内存空间并进行元素复制，因此扩容操作会带来一定的性能开销。频繁进行大规模数据添加操作可能导致多次扩容，影响程序性能。

避免频繁扩容：为了避免频繁扩容，<mark style="color:blue;">可以在创建ArrayList时指定初始容量大小，以减少扩容次数</mark>。

扩容优化：在JDK 1.6及之后的版本中，ArrayList提供了ensureCapacity(int minCapacity)方法，用于手动设置ArrayList的最小容量，可以在添加大量元素前先调用该方法预估所需容量，减少扩容操作。
