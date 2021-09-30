### FIle类

File更应该叫一个路径（分绝对路径和相对路径）

![image-20210926090921425](E:\Typora图片仓库\image-20210926090921425.png)

![image-20210926090943157](E:\Typora图片仓库\image-20210926090943157.png)

File类的创建功能：

![image-20210926094646797](E:\Typora图片仓库\image-20210926094646797.png)

![image-20210926104652345](E:\Typora图片仓库\image-20210926104652345.png)

![image-20210926105227984](E:\Typora图片仓库\image-20210926105227984.png)

## IO流

### 1.概念

​	![image-20210926142326643](E:\Typora图片仓库\image-20210926142326643.png)

![image-20210926142512492](E:\Typora图片仓库\image-20210926142512492.png)

![image-20210926153707190](E:\Typora图片仓库\image-20210926153707190.png)

BufferedOutPutStream

![image-20210926160606358](E:\Typora图片仓库\image-20210926160606358.png)

### 2.字节流读写中文

- 读取问题：读写中文的时候会出现乱码（有的时候是半个中文）
- 写出问题：字节流直接操作字节，所以写出的中文必须将字符串转换成字节数组
- ![image-20210926162703401](E:\Typora图片仓库\image-20210926162703401.png)

### 3.字符流

1. #### 字符流FileReader

    - 可以直接读写字符的IO流

    - 案例：FileReader类的read()方法可以安装字符大小读取

        ```java
        package demo1;
        
        import java.io.FileReader;
        import java.io.IOException;
        
        public class demo1 {
            public static void main(String[] args) throws IOException {
                FileReader fileReader = new FileReader("G:\\TengTai-lesson\\20210927\\src\\demo1\\aa.txt");
                int len;
                while ((len=fileReader.read() )!= -1) {
                    System.out.print((char) len);
                }
                fileReader.close();
            }
        }
        ```

2. #### 字符流FileWriter

    - FileWriter类的Write方法可以把自动把字符转成字节写出

    - 案例：

        ```java
        package demo1;
        
        import java.io.File;
        import java.io.FileWriter;
        import java.io.IOException;
        
        public class demo2 {
            public static void main(String[] args) throws IOException {
                FileWriter fileWriter = new FileWriter("G:\\TengTai-lesson\\20210927\\src\\demo1\\aa.txt");
                fileWriter.write("hello123");
                fileWriter.close();
            }
        }
        ```

3. ![image-20210927094446488](E:\Typora图片仓库\image-20210927094446488.png)

4. 练习：用流统计字符数量

    ![image-20210927104054073](E:\Typora图片仓库\image-20210927104054073.png)

### 4.递归

概念：方法自己调用自己

弊端：不能调用次数过多，容易出现栈内存溢出

好处：不用知道循环多少次

注意：构造方法不能递归（没有返回值），递归是有返回值

练习：输入路径查找指定后缀名文件

```java
package demo4;

import java.io.File;
import java.util.Scanner;
public class Test2 {
    public static void printJavaFile(File file) {
        File[] files = file.listFiles();
        for (File file1 : files) {
            if (file1.isFile() && file1.getName().endsWith(".java")) {
                System.out.println(file1);
            }else if (file1.isDirectory()) {
                printJavaFile(file1);
            }
        }
    }
    public static File getDir() {
        Scanner scanner = new Scanner(System.in);
        System.out.println("请输入地址：");
        while (true) {
            String s = scanner.nextLine();
            File file = new File(s);
            if (!file.exists()) {
                System.out.println("请输入正确的路径：");
            } else if (file.isFile()) {
                System.out.println("请输入路径而不是文件");
            }else {
                return file;
            }
        }
    }
    public static void main(String[] args) {
        File dir = getDir();
        printJavaFile(dir);
    }
}
```

5.文件聚合读写

```java
package demo5;

import java.io.*;
import java.util.Enumeration;
import java.util.Vector;

public class Demo1 {
    public static void main(String[] args) throws IOException {
        FileInputStream inputStream1 = new FileInputStream("G:\\TengTai-lesson\\20210927\\src\\demo5\\x1.txt");
        FileInputStream inputStream2 = new FileInputStream("G:\\TengTai-lesson\\20210927\\src\\demo5\\x2.txt");
        SequenceInputStream sequenceInputStream = new SequenceInputStream(inputStream1, inputStream2);
        FileOutputStream fileOutputStream = new FileOutputStream("G:\\TengTai-lesson\\20210927\\src\\demo5\\x3.txt");
        int b;
        while ((b=sequenceInputStream.read())!=-1) {
            fileOutputStream.write(b);
        }
        sequenceInputStream.close();
        fileOutputStream.close();

        //整合多个文件
        /*Vector<Object> vector = new Vector<>();
        Enumeration e=vector.elements();
        new SequenceInputStream(e);*/
    }
}
```

### 练习题：

![image-20210927165352201](E:\Typora图片仓库\image-20210927165352201.png)

