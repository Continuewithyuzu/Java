# Java语言中实现线程的两种方式

## 方法一：继承Thread类

编写一个类，直接 **继承** **`java.lang.Thread`**，**重写** **`run方法`**

1. 怎么创建线程对象？ **new**继承线程的类。
2. 怎么启动线程呢？ 调用线程对象的 **`start()`** 方法。

### 伪代码：

```java
// 定义线程类
public class MyThread extends Thread{
	public void run(){
	
	}
}
// 创建线程对象
MyThread t = new MyThread();
// 启动线程。
t.start();
```

### 例子：

```java
public class ThreadTest02 {
    public static void main(String[] args) {
        MyThread t = new MyThread();
        // 启动线程
        //t.run(); // 不会启动线程，不会分配新的分支栈。（这种方式就是单线程。）
        t.start();
        // 这里的代码还是运行在主线程中。
        for(int i = 0; i < 1000; i++){
            System.out.println("主线程--->" + i);
        }
    }
}

class MyThread extends Thread {
    @Override
    public void run() {
        // 编写程序，这段程序运行在分支线程中（分支栈）。
        for(int i = 0; i < 1000; i++){
            System.out.println("分支线程--->" + i);
        }
    }
}
```

### 注意事项

* t.run() 不会启动线程，只是普通的调用方法而已。不会分配新的分支栈。（这种方式就是**单线程**）就相当于调用普通的类
* t.start() 方法的作用是：启动一个分支线程，在JVM中开辟一个新的栈空间，这段代码任务完成之后，瞬间就结束了。 这段代码的任务只是为了开启一个新的栈空间，只要新的栈空间开出来，start()方法就结束了。线程就启动成功了。 启动成功的线程**会自动调用run方法**，并且run方法在分支栈的栈底部（压栈）。 run方法在分支栈的栈底部，main方法在主栈的栈底部。run和main是平级的。&#x20;

## 方法二：实&#x73B0;**`Runnable接口`**

编写一个类，**实现** **`java.lang.Runnable`** 接口，**实现`run方法`**。

1. 怎么创建线程对象？ **new**线程类传入可运行的类/接口。
2. 怎么启动线程呢？ 调用线程对象的 **`start()`** 方法。

### 伪代码

```java
// 定义一个可运行的类
public class MyRunnable implements Runnable {
	public void run(){
	
	}
}
// 创建线程对象
Thread t = new Thread(new MyRunnable());
// 启动线程
t.start();
```

### 例子：

```java
public class ThreadTest03 {
    public static void main(String[] args) {
        Thread t = new Thread(new MyRunnable()); 
        // 启动线程
        t.start();
        
        for(int i = 0; i < 100; i++){
            System.out.println("主线程--->" + i);
        }
    }
}

// 这并不是一个线程类，是一个可运行的类。它还不是一个线程。
class MyRunnable implements Runnable {
    @Override
    public void run() {
        for(int i = 0; i < 100; i++){
            System.out.println("分支线程--->" + i);
        }
    }
}
```

**采用匿名内部类创建：**

```java
public class ThreadTest04 {
    public static void main(String[] args) {
        // 创建线程对象，采用匿名内部类方式。
        Thread t = new Thread(new Runnable(){
            @Override
            public void run() {
                for(int i = 0; i < 100; i++){
                    System.out.println("t线程---> " + i);
                }
            }
        });

        // 启动线程
        t.start();

        for(int i = 0; i < 100; i++){
            System.out.println("main线程---> " + i);
        }
    }
}

```

## **注意**

\
**第二种方式**实现接口比较常用，因为一个类实现了接口，它还可以去继承其它的类，更灵活。
