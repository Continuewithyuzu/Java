# FileReader类 和 FileWriter类

## FileReader类

Reader的子类，称为文件字符输入流。

字节流不能直接操作Unicode字符，所以Java提供了字符流（汉字在文件中占用2字符）

### 构造方法

`FileReader(String name)`

`FileReader(File file)`

```java
File file = new File("example.txt");
FileReader fr = new FileReader(file);
```

### 通过`read()`方法从输入流读出源的数据

* int read()——读取一个字符，返回一个整数（0\~65535），<mark style="color:blue;">未读出则返回-1</mark>

```java
FileReader fr = new FileReader("example.txt");
int data;
while ((data = fr.read()) != -1) {
    System.out.print((char) data); // 将读取的字符输出
}
fr.close();
```

* int read(char b\[])——从源中读取b.length()长个字符到数组b中，返回实际读取的字符数目，未达到文件末尾返回-1

```java
FileReader fr = new FileReader("example.txt");
char[] buffer = new char[100];
int charsRead;
while ((charsRead = fr.read(buffer)) != -1) {
    System.out.print(new String(buffer, 0, charsRead)); // 输出字符
}
fr.close();
```

* int read(char b\[],int off,int len)——读取len个字符并存放在数组h中，返回实际读取的字符数目，到达文件末尾返回-1，off指定该方法从字符b中的什么地方存放数据

```java
FileReader fr = new FileReader("example.txt");
char[] buffer = new char[50];
int charsRead = fr.read(buffer, 5, 20); // 从文件读取最多20个字符，存储到 buffer[5] 开始的位置
fr.close();
```

### 基本用法：

```java
import java.io.FileReader;
import java.io.IOException;

public class FileReaderExample {
    public static void main(String[] args) {
        String fileName = "example.txt"; // 文件路径

        try (FileReader fr = new FileReader(fileName)) { // 使用 try-with-resources 自动关闭流
            int data;
            while ((data = fr.read()) != -1) {
                System.out.print((char) data); // 输出字符
            }
        } catch (IOException e) {
            e.printStackTrace(); // 捕获并处理异常
        }
    }
}
```

### **注意事项**

1. **性能问题**：
   * `FileReader` 是低效的，因为它直接从文件中读取字符。如果需要更高效的读取（如逐行读取），可以将它与 `BufferedReader` 结合使用。

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class BufferedFileReaderExample {
    public static void main(String[] args) {
        String fileName = "example.txt";

        try (BufferedReader br = new BufferedReader(new FileReader(fileName))) {
            String line;
            while ((line = br.readLine()) != null) {
                System.out.println(line); // 输出每一行
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

**2.编码问题**：

* `FileReader` 使用系统默认的字符编码。如果文件的编码格式不是系统默认的（如 UTF-8），可能导致乱码。
* 解决方案：使用 `InputStreamReader` 指定编码。

**3.资源管理**：

* 记得在读取文件后关闭 `FileReader`，否则可能会造成资源泄漏。建议使用 `try-with-resources`。

***

## FiileWriter类

### **1. `FileWriter` 的定义**

`FileWriter` 是 `Writer` 的子类，专门用于向文件中写入文本数据。它提供了方便的写操作方法，可以处理单个字符、字符数组和字符串。

### 2.构造方法

`FileWriter` 提供以下构造方法来实例化对象：

1. **`FileWriter(String fileName)`**
   * 接收文件名作为参数。
   * 如果文件不存在，会创建一个新文件；如果文件存在，会清空已有内容（覆盖写入）。
   *   示例：

       ```java
       FileWriter fw = new FileWriter("example.txt");
       ```
2. **`FileWriter(String fileName, boolean append)（课本不做要求）`**
   * 接收文件名和一个布尔值 `append`：
     * 如果 `append` 为 `true`，则追加内容到文件末尾。
     * 如果 `append` 为 `false`，则覆盖文件内容。
   *   示例：

       ```java
       FileWriter fw = new FileWriter("example.txt", true);
       ```
3. **`FileWriter(File file)`**
   * 接收一个 `File` 对象作为参数。
   *   示例：

       ```java
       File file = new File("example.txt");
       FileWriter fw = new FileWriter(file);
       ```
4. **`FileWriter(File file, boolean append)（课本不做要求）`**
   * 接收一个 `File` 对象和布尔值 `append`。
   *   示例：

       ```java
       File file = new File("example.txt");
       FileWriter fw = new FileWriter(file, true);
       ```

### **3. 常用方法（重点看前5个就好）**

`FileWriter` 继承了 `Writer` 类，并提供了一些常用的方法：

**1. `void write(int c)`**

* **作用**：将单个字符写入文件。
* **参数**：字符的 Unicode 值。
*   **示例**：

    ```java
    java复制代码FileWriter fw = new FileWriter("example.txt");
    fw.write(97); // 写入字符 'a' 的 Unicode 值
    fw.close();
    ```

**2. `void write(char[] cbuf)`**

* **作用**：将字符数组写入文件。
*   **示例**：

    ```java
    java复制代码FileWriter fw = new FileWriter("example.txt");
    char[] chars = {'H', 'e', 'l', 'l', 'o'};
    fw.write(chars);
    fw.close();
    ```

**3. `void write(char[] cbuf, int off, int len)`**

* **作用**：将字符数组的部分内容写入文件，从 `off` 开始写入 `len` 个字符。
*   **示例**：

    ```java
    java复制代码FileWriter fw = new FileWriter("example.txt");
    char[] chars = {'J', 'a', 'v', 'a', '!', '!', '!'};
    fw.write(chars, 0, 4); // 写入 "Java"
    fw.close();
    ```

**4. `void write(String str)`**

* **作用**：将字符串写入文件。
*   **示例**：

    ```java
    java复制代码FileWriter fw = new FileWriter("example.txt");
    fw.write("Hello, FileWriter!");
    fw.close();
    ```

**5. `void write(String str, int off, int len)`**

* **作用**：将字符串的部分内容写入文件，从 `off` 开始写入 `len` 个字符。
*   **示例**：

    ```java
    java复制代码FileWriter fw = new FileWriter("example.txt");
    fw.write("Programming in Java", 0, 11); // 写入 "Programming"
    fw.close();
    ```

**6. `void flush()`**

* **作用**：刷新缓冲区，将数据从内存中强制写入文件。
* **注意**：写操作完成后，建议调用 `flush()` 或者直接调用 `close()`，以确保数据写入文件。
*   **示例**：

    ```java
    java复制代码FileWriter fw = new FileWriter("example.txt");
    fw.write("Hello, flush!");
    fw.flush();
    fw.close();
    ```

**7. `void close()`**

* **作用**：关闭流并释放与之相关的系统资源。如果流未关闭，则写入操作可能无法保证完成。
*   **示例**：

    ```java
    java复制代码FileWriter fw = new FileWriter("example.txt");
    fw.write("Closing the stream!");
    fw.close();
    ```

## 4.基本写入操作代码

```java
import java.io.FileWriter;
import java.io.IOException;

public class FileWriterExample {
    public static void main(String[] args) {
        try {
            FileWriter fw = new FileWriter("example.txt");
            fw.write("This is a simple FileWriter example.");
            fw.close(); // 关闭流
            System.out.println("File written successfully.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

**搭配 `BufferedWriter` 使用**

`BufferedWriter` 可以提高写入效率，以下是示例：

```java
java复制代码import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;

public class BufferedWriterExample {
    public static void main(String[] args) {
        try (BufferedWriter bw = new BufferedWriter(new FileWriter("example.txt"))) {
            bw.write("Line 1: Hello, BufferedWriter!");
            bw.newLine(); // 写入换行符
            bw.write("Line 2: Another line.");
            System.out.println("Buffered writing completed.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

## **5. 注意事项**

1. **覆盖 vs 追加模式**：
   * 默认情况下，`FileWriter` 会覆盖文件内容。
   * 如果需要追加内容，必须显式设置 <mark style="color:blue;">`append`</mark> <mark style="color:blue;"></mark><mark style="color:blue;">参数为</mark> <mark style="color:blue;"></mark><mark style="color:blue;">`true`</mark>。
2. **缓冲问题**：
   * `FileWriter` 默认是无缓冲的，每次写入都会直接写入文件，效率较低。
   * 建议搭配 `BufferedWriter` 使用以提高写入效率。
3. **资源释放**：
   * 使用完 `FileWriter` 后，一定要调用 `close()` 释放资源，避免文件被占用。
   *   推荐使用 `try-with-resources` 语法，自动关闭流：

       ```java
       try (FileWriter fw = new FileWriter("example.txt")) {
           fw.write("Using try-with-resources.");
       } catch (IOException e) {
           e.printStackTrace();
       }
       ```
