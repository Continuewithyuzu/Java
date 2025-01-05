# 路径注意问题

## 关于java中 要打出右斜杠''的问题：&#x20;

错误做法:\
这是新手很容易犯的一个错误。因为File类操作路径，而路径分隔符不是左斜线就是右斜线，但在java中，右斜杠本身有转义符的意思，因此，直接输出右斜杠会导致报错，如下：



```java
public class Test { 
   public static void main(String[] args) { 
   //这么输出直接报错! 
   //System.out.println("👴头铁，就要这么干：" + \);
   //System.out.println("👴头铁，就要这么干2：" + "\");
     /*
        Error:
            头铁一号会报非法字符的错误
            头铁二号会报未结束的字符串的错误
        Reason:
            这是因为\是转义符，\" 相当于输出一个双引号，
            但因此你字符串就烂尾了。
    */
    }
}
```

正确做法: <mark style="color:blue;">想打印出一条右斜杠，需要连续输入两个\键</mark>，如下：

```java
public class Demo { 
    public static void main(String[] args) { 
        //如何输出右斜杠？ System.out.println("给👴输出右斜杠：" + "\");
        
    } 
} 
```

为啥讲这个？ File类会操作文件路径，而文件路径的路径分隔符可以使&#x7528;_<mark style="background-color:orange;">**一条左斜线/ 或者两条右斜线\\\\**</mark>_ ，单独使用一条右斜线会报错。
