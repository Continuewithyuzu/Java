# File类

## File

File，即文件、文件夹，一个**File对象表示**了磁盘上的某个**文件**或**文件夹**。**在java中，File类实质是以文件或者文件夹的路径来操作的**。**File 类是 java.io 包中唯一代表磁盘文件本身的对象。**

## **构造方法**

1.**`File (String pathname)`**： 需要传入String类型的文件路径。需要用File类型作接收。

2.**`File(String parent, String child)`**：和第一种构造方式大同小异。不过是将文件路径劈开了，分为父路径和子路径两部分，作为两个形参。

3.**`File(File parent, String child)`**：与前两种构造方式略有差异：将文件路径劈开后，又先将父路径封装成了File类型，然后再分别将“File类型的父路径” 和 “String类型的子路径”传上去。

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>
