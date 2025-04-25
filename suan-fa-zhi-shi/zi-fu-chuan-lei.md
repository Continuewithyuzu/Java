# 字符串类

## **toCharArray()方法**

toCharArray()是Java中字符串类的一个方法，它将一个字符串转换为一个字符数组。该方法返回一个新的字符数组，其中包含与调用它的字符串相同的字符序列。

```java
public int length()：获取字符串长度。
```

```java
public String substring(int startpoint)：返回从第startpoint个位置开始到结束截取的字符串。
public String substring(int start,int end)：返回从start开始到end（不包括end位置）截取的字符串。
```

定义可变长字符串

```java
public class Main {
    public static void main(String[] args) {
        StringBuffer sb = new StringBuffer("Hello");
        sb.append(" World");  // 使用 append() 方法追加字符串
        System.out.println(sb.toString());  // 输出 "Hello World"
    }
}
```

返回对应索引的字符

```java
char c = s.charAt(0);
```

反转字符串

```java
StringBuilder sb = new StringBuilder("hello");
StringBuilder sb1 = sb.reverse();
System.out.println(sb1.toString());
```
