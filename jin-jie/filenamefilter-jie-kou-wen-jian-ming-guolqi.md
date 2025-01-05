---
description: 就是在文件集合中过滤出我想要的文件
---

# FilenameFilter接口——文件名过滤器

## 接口代码：

```java
public interface FilenameFilter {
        boolean accept(File dir, String name);
}
```

实现这个文件过滤的实质就是编写一个类实现该接口，同时重写accept方法

### 例子：

#### 1、匿名类实现FilenameFilter—–过滤指定类型文件

```java
package File类过滤器;

import java.io.File;
import java.io.FilenameFilter;

public class Test {
    public static void main(String[] args){
        File file=new File("D:\\练习");
        File[] files=file.listFiles();

        //过滤前所有文件信息
        for(File file2:files){
            System.out.println(file2);
        }

        //现在要求过滤.txt为后缀的文件
        //使用匿名函数写过滤器
        System.out.println();
        System.out.println("过滤后的文件遍历结果：");
        File[] files2=file.listFiles(new FilenameFilter() {
            //想要保存的文件则，return true;反之return false
            @Override
            public boolean accept(File dir, String name) {
                File[] files=dir.listFiles();
                if(name.endsWith(".txt")){
                    return false;
                }
                return true;
            }
        });
        for(File file2:files2){
            System.out.println(file2);
        }

    }
}
```

#### 2、创建过滤类

```java
package File类过滤器;

import java.io.File;
import java.io.FilenameFilter;

public class MyFilenameFilter implements FilenameFilter {

    @Override
    public boolean accept(File dir, String name) {
        //过滤文件夹
        File file=new File(dir,name);
        if(file.isDirectory()){
            return false;
        }

        return true;
    }

}
```
