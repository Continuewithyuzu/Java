# 常用的线程方法

## 获取当前线程对象、获取线程对象名字、修改线程对象名字

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

#### 当线程没有设置名字的时候，默认的名字是什么？

* Thread-0
* Thread-1
* Thread-2
* Thread-3
* …

## 关于线程的sleep方法

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

* 静态方法：Thread.sleep(1000);&#x20;
* 参数是毫秒
* 作用： 让当前线程进入休眠，进入“阻塞状态”，放弃占有CPU时间片，让给其它线程使用。 这行代码出现在A线程中，A线程就会进入休眠。 这行代码出现在B线程中，B线程就会进入休眠。&#x20;
* Thread.sleep()方法，可以做到这种效果： 间隔特定的时间，去执行一段特定的代码，每隔多久执行一次。

例子：

```java
public class ThreadTest06 {
    public static void main(String[] args) {
    	//每打印一个数字睡1s
        for(int i = 0; i < 10; i++){
            System.out.println(Thread.currentThread().getName() + "--->" + i);

            // 睡眠1秒
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

## 中断睡眠

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

```java
public class ThreadTest08 {
    public static void main(String[] args) {
        Thread t = new Thread(new MyRunnable2());
        t.setName("t");
        t.start();

        // 希望5秒之后，t线程醒来（5秒之后主线程手里的活儿干完了。）
        try {
            Thread.sleep(1000 * 5);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        // 终断t线程的睡眠（这种终断睡眠的方式依靠了java的异常处理机制。）
        t.interrupt();
    }
}

class MyRunnable2 implements Runnable {
    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName() + "---> begin");
        try {
            // 睡眠1年
            Thread.sleep(1000 * 60 * 60 * 24 * 365);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        //1年之后才会执行这里
        System.out.println(Thread.currentThread().getName() + "---> end");
}
```

## 和线程调度有关系的方法

### 优先级

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

* 最低优先级1
* 默认优先级是5
* 最高优先级10

**优先级比较高的获取CPU时间片可能会多一些**。（但也不完全是，大概率是多的。）

### 让位方法

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

yield()方法不是阻塞方法。让当前线程让位，让给其它线程使用。

yield()方法的执行会让当前线程从“**运行状态**”回到“**就绪状态**”。

注意：在回到就绪之后，**有可能还会再次抢到**。

### 联合线程

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>
