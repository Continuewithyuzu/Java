---
description: >-
  BufferedReader 是 Java 中用于高效读取字符流的类，属于 java.io
  包。它提供了对字符流的缓冲功能，能够显著提高读操作的效率，尤其是在频繁的小规模读取的场景下。常与 FileReader 等基础字符流类结合使用。
---

# BufferedReader类

## **1. `BufferedReader` 的定义**

`BufferedReader` 是 `Reader` 的子类，作用是在字符输入流上添加缓冲功能。通过缓冲区来减少对磁盘 I/O 的直接访问，从而提高读取性能。

***

## **2. 使用场景**

* 需要从文件中高效地读取文本数据。
* 需要逐行读取文件内容（如配置文件、日志文件）。
* 需要对数据流中的字符进行缓冲处理，提高性能。

***

## **3. 构造方法**

`BufferedReader` 提供以下两种构造方法来实例化对象：

1. **`BufferedReader(Reader in)`**
   * 接受一个 `Reader` 对象作为输入流。
   *   示例：

       ```java
       java复制代码BufferedReader br = new BufferedReader(new FileReader("example.txt"));
       ```
2. **`BufferedReader(Reader in, int sz)`**
   * 接受一个 `Reader` 对象作为输入流，并指定缓冲区的大小（以字符为单位）。
   * 默认缓冲区大小为 8192 个字符（8 KB）。
   *   示例：

       ```java
       java复制代码BufferedReader br = new BufferedReader(new FileReader("example.txt"), 1024);
       ```

***

## **4. 常用方法**

**1. `String readLine()`**

* **作用**：从输入流中读取一行文本，并返回该行内容；如果到达流末尾，则返回 `null`。
* **特点**：逐行读取文件内容，适合读取纯文本文件。
*   **示例**：

    ```java
    java复制代码BufferedReader br = new BufferedReader(new FileReader("example.txt"));
    String line;
    while ((line = br.readLine()) != null) {
        System.out.println(line);
    }
    br.close();
    ```

**2. `int read()`**

* **作用**：从输入流中读取单个字符，返回字符的 Unicode 值（`0~65535` 范围的整数）；如果到达流末尾，返回 `-1`。
*   **示例**：

    ```java
    java复制代码BufferedReader br = new BufferedReader(new FileReader("example.txt"));
    int charValue;
    while ((charValue = br.read()) != -1) {
        System.out.print((char) charValue);
    }
    br.close();
    ```

**3. `int read(char[] cbuf, int off, int len)`**

* **作用**：将最多 `len` 个字符读入字符数组 `cbuf` 中，从 `off` 开始存储。
* **返回值**：实际读取的字符数；如果到达流末尾，返回 `-1`。
*   **示例**：

    ```java
    java复制代码BufferedReader br = new BufferedReader(new FileReader("example.txt"));
    char[] buffer = new char[1024];
    int charsRead;
    while ((charsRead = br.read(buffer, 0, buffer.length)) != -1) {
        System.out.print(new String(buffer, 0, charsRead));
    }
    br.close();
    ```

**4. `void close()`**

* **作用**：关闭流并释放与之关联的资源。
* **注意**：关闭 `BufferedReader` 会同时关闭它包装的底层流。
*   **示例**：

    ```java
    java复制代码BufferedReader br = new BufferedReader(new FileReader("example.txt"));
    // 使用流进行读取操作
    br.close(); // 关闭流
    ```

**5. `boolean ready()`**

* **作用**：判断流是否准备好被读取。如果可以无阻塞地读取字符，则返回 `true`。
*   **示例**：

    ```java
    java复制代码BufferedReader br = new BufferedReader(new FileReader("example.txt"));
    if (br.ready()) {
        System.out.println("Stream is ready for reading.");
    }
    br.close();
    ```



## 5、逐行读取文件内容

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class BufferedReaderExample {
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
