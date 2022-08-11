# File 类和 IO 流
## 第一章：File 类
### 1.1 概述
>FIle 类是 java.io 包下代表和平台无关的文件和目录，换言之，如果希望在程序中操作文件和目录都可以使用 File 类来完成，File 类能新建、删除、重命名文件和目录。
>在 API 中 File 的解释是 文件和目录路径名的抽象表示形式 ，即 File 类是文件或目录的路径，而不是文件本身，因此 File 类不能直接访问文件内容本身，如果需要访问文件内容本身，就需要使用 IO 流了。
>File 类代表磁盘或网络中某个文件或目录的路径名称，例如：c:/美女.jpg。
>不能直接通过 File 对象读取和写入数据，如果要操作数据，需要 IO 流。
### 1.2 File 的构造方法
- 通过将给定的路径名称字符串转换为抽象路径名为创建新的 File 实例：
```public File(String pathname) {}```
- 通过父路径名字符串和子路径名字符串创建新的 File 实例：
```public File(String parent, String child) {}```
- 通过父路径名和子路径名字符串创建新的 File 实例：
```public File(File parent, String child) {}```
- 通过将给定的 file: URI 到一个抽象路径名创建一个新的 File 
```public File(URI uri) {}```
### 1.3 File 的常用方法
#### 1.3.1 获取文件和目录基本信息的方法
- 返回由此 File 表示的文件或目录的名称：
```public String getName() {}```
- 返回由此 File 表示的文件的长度：
```ublic long length() {}```
将此 File 转换为路径名字符串：
```public String getPath() {}```

#### 1.3.2 路径
- 将此 File 实例转换为路径名称字符串：
```public String getAbsolutePath() {}```
- 返回此 File 实例的绝对路径名字符串：
```public String getAbsolutePath() {}```
- 返回此 File 实例所对应的规范路径名：
```public String getCanonicalPath() throws IOException {}```

####1.3.3 判断功能的方法
- 判断 File 实例表示的文件或目录是否存在：
```public boolean exists() {}```
- 判断 File 实例表示的是否是文件：
```public boolean isFile() {```
- 判断 File 实例表示的是否是目录：
```public boolean isDirectory() {}```
- 判断 File 构造方法中的路径是否是绝对路径：
```public boolean isAbsolute() {}```

#### 1.3.4 创建和删除的方法
- 当且仅当具有该名称的文件尚不存在时，创建一个新的空文件：
```public boolean createNewFile() throws IOException {}```
- 删除由此 File 表示的文件或目录（只能删除空目录）：
```public boolean delete() {}```
- 创建由此 File 表示的目录：
```public boolean mkdir() {}```
- 创建由此 File 表示的目录（包含父目录）：
```public boolean mkdirs() {}```

### 1.4 递归实现多级目录操作
#### 1.4.1 相关方法
- 返回一个 String 数组，表示该 File 目录中的所有子文件或目录：
```public String[] list() {}```
- 返回一个 File 数组，表示该 File 目录中的所有的子文件或目录：
```public File[] listFiles() {}```
- 返回所有满足指定过滤器的文件和目录的 String 数组：
```public String[] list(FilenameFilter filter) {}```
- 返回所有满足指定过滤器的文件和目录的 File 数组：
```public File[] listFiles(FilenameFilter filter) {}```
#### 1.4.2 递归打印多级目录
分析：多级目录的打印。遍历之前，无从知道到底有多少级目录，所以我们可以使用递归实现。
示例：
```
  print(new File("D:\\develop\\Java\\jdk1.8.0_131"));
    }
    public static void print(File file) {
        if (null != file && file.isDirectory()) {
            File[] files = file.listFiles();
            if (null != files) {
                for (File f : files) {
                    print(f);
                }
            }
        }
        System.out.println(file);
    }
```
#### 1.4.3 递归打印某目录下（包括子目录）中所有满足条件的文件
示例：列出所有 .java 文件
```
print(new File("D:\\project\\java-core"));
    }

    public static void print(File file) {
        if (null != file && file.isDirectory()) {
            File[] files = file.listFiles(new FilenameFilter() {
                @Override
                public boolean accept(File dir, String name) {
                    return name.endsWith(".java") || new File(dir, name).isDirectory();
                }
            });
            if (null != files) {
                for (File f : files) {
                    if (f.isFile()) {
                        System.out.println(f);
                    }
                    print(f);
                }
            }
        }
```



## 第二章：IO流
### 2.1 概述
>I/O 是 Input 和 Output 的缩写，IO 技术是非常实用的技术，用于 处理设备之间的数据传输 ，如：读写文件、网络通讯等。
>Java 程序中，对于数据的输入/输出操作以 流stream 的方式进行。
>java.io 包下提供了各种 流 类和接口，用于获取不同种类的数据，并通过 标准的方法 输入或输出数据。
### 2.2 Java IO 原理
1. 输入（ Input ）：读取外部数据（磁盘、U 盘等存储设备的数据）到程序（内存）中。
2. 输出（ Output ）：将程序（内存）数据输出到磁盘、U 盘等存储设备中。

### 2.3 IO 的分类
* 根据流的流向分类：
   - 输入流：将数据从 其他设备 上读取到 内存 中的流。以 InputStream 、Reader 结尾。
   - 输出流：将数据从 内存 中写出到 其他设备 上的流。以 OutputStream 和 Writer 结尾。
* 根据数据的类型分类：
   - 字节流：以字节为单位，读写数据的流。以 InputStream 和 OutputStream 结尾。
   - 字符流：以字符为单位，读写数据的流。以 Reader 和 Writer 结尾。
* 根据 IO 流的角色不同分类：
   -节点流：可以从或向一个特定的地方（节点）读取数据。如 FileReader 。
   - 处理流：对一个已经存在的流进行连接和封装，通过锁封装的流的功能实现数据读写。如：BufferReader ，处理流的构造方法总是要带一个其它的流对象做参数。一个流对象经过多次其它流的多次包装，称为流的链接。
* 常用的节点流：
1. 文件：FileInputStream 、FileOutputStream 、FileReader 、FileWriter 文件进行处理的节点流。
2. 字符串：StringReader 、StringWriter 对字符串进行处理的节点流。
3. 数组： ByteArrayInputStream 、ByteArrayOutputStream、CharArrayReader 、CharArrayWriter 对数组进行处理的节点流（对应的不再是文件，而是内存中的一个数组）。
4. 管道：PipedInputStream 、PipedOutputStream 、PipedReader 、PipedWriter 对管道进行处理的节点流。
* 常用处理流：
1. 缓冲流：BufferedInputStream 、BufferedOutputStream 、BufferedReader 、BufferedWriter ---增加缓冲功能，避免频繁读写硬盘。
2. 转换流：InputStreamReader 、OutputStreamReader --- 实现字节流和字符流之间的转换。
3. 数据流：DataInputStream 、DataOutputStream - 提供读写 Java 基础数据类型功能。
4. 对象流：ObjectInputStream 、ObjectOutputStream -- 提供直接读写 Java 对象功能。
### 2.4 四大顶级抽象流父类
|      |     **输入流**        | **输出流**           |
|------|----------------------|----------------------|
|字符流 | 字符输入流 Reader      | 字符输出流 Writer      |
|字节流 |字节输入流 InputStream  | 字节输出流 OutputStream |
### 2.5 字节流
#### 2.5.1 概述
一切文件数据（文本、图片、视频等）在存储的时候，都是以二进制的形式保存的，都是一个个的字节；同样，在传输的时候依然如此。所以，字节流可以传输任意文件数据。
在操作流的时候，我们要时刻明确，无论使用什么样的流对象，底层传输始终是二进制数据。
### 2.5.3 OutputStream
java.io.OutputStream 抽象类是表示字节输出流的所有类的超类，将指定的字节信息输出的目的地。它定义了字节输出流的基本共性的功能方法。
- 写入单个字节：
```public abstract void write(int b) throws IOException;```
- 写入字节数组：
```public void write(byte b[]) throws IOException {}```
- 写入字节数组的一部分，从 offset 开始，一共 len 个：
```public void write(byte b[], int off, int len) throws IOException {}```
- 刷新流：
```public void flush() throws IOException {}```
- 关闭流：
```public void close() throws IOException {}```
> 注意：当完成流的操作的时候，必须调用 close() 方法，释放系统资源。
#### 2.5.4 FileOutputStream
FileOutputStream 是 OutputStream 的子类，FileOutputStream 是文件输出流，用于将数据写出到文件中。
>构造方法：
- 创建文件输出流以写入由指定的 File 对象表示的文件：
```public FileOutputStream(File file) throws FileNotFoundException {}```
- 创建文件输出流以指定的名称写入文件：
```public FileOutputStream(String name) throws FileNotFoundException {}```
注意：当创建 FileOutputStream 流对象的时候，必须传入一个文件路径。该路径下，如果没有这个文件，会创建该文件；如果有这个文件，会覆盖这个文件的数据。
>数据追加：
- 创建文件输出流以写入由指定的 File 对象表示的文件：
```public FileOutputStream(String name, boolean append)
      throws FileNotFoundException
  {}
  ```
- 创建文件输出流以指定的名称写入文件：
```
public FileOutputStream(File file, boolean append)
      throws FileNotFoundException
  {}
```
换行写出：windows 系统中的换行符号是 \r\n 。

#### 2.5.5 IO 异常处理
示例：
JDK 7 的新特性 try-with-resources ：
没有 finally ，也不需要程序员去关闭资源对象，无论是否发生异常，都会关闭资源对象。
实现了 AutoCloseable 或 Closeable 接口的类才可以自动进行资源关闭。
示例：JDK 7 的新特性 try-with-resources
#### 2.5.6 InputStream
InputStream 抽象类是表示字节输入流的所有类的超类，可以读取字节信息到内存中。它定义了字节输入流的基本共性功能方法。
- 读取单个字节：
```
  public abstract int read() throws IOException;
```
- 读取字节数组：
```java
  public int read(byte b[]) throws IOException {}
```
- 读取字节数组，从 offset 开始，len 长度：
```java
public int read(byte b[], int off, int len) throws IOException {}
```
- 关闭流：
#### 2.5.7 FileInputStream
java.io.FileInputStream 类是文件输入流，从文件中读取字节。
构造方法：
- 通过打开与实际文件的连接来创建一个 FileInputStream ，该文件由文件系统中的 File 对象 file 命名：
```public FileInputStream(File file) throws FileNotFoundException {}```
- 通过打开与实际文件的连接来创建一个 FileInputStream ，该文件由文件系统中的路径名 name 命名：
```public FileInputStream(String name) throws FileNotFoundException {}```
- 示例：读取单个字节，读取到文件末尾，返回 -1
- 示例：读取字节数组，读取到文件末尾，返回 -1
#### 2.5.8 文件复制
文件复制的本质是字节的搬家。
文件复制.png
示例：
```
 try (InputStream is = new FileInputStream("C:\\Users\\xudaxian\\Pictures\\枪械少女.jpg");
            OutputStream os = new FileOutputStream("C:\\Users\\xudaxian\\Pictures\\枪械少女1.jpg")) {
            byte[] bytes = new byte[1024];
            int len;
            while ((len = is.read(bytes)) != -1) {
                os.write(bytes, 0, len);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
```
### 2.6 字符流
#### 2.6.1 概述
当使用字节流读取文本文件的时候，可能会有一个小问题：就是遇到中文字符的时候，可能显示不完整，那是因为一个中文字符可能占用多个字节存储。所以，Java 提供了一些字符流，以字符为单位读写数据，专门用于处理文本文件。
#### 2.6.2 Reader
java.io.Reader 抽象类是表示用于读取字符流的所有类的超类，可以读取字符信息到内存中。它定义了字符输入流的基本共性功能方法。
关闭此流并释放与此流相关联的任何系统资源：
- 读取一个字符：
```abstract public void close() throws IOException;```
- 读取字符数组：
``` public int read() throws IOException```
- 读取从 offset 索引开始，len 长度的字符数组：```abstract public int read(char cbuf[], int off, int len) throws IOException;```
#### 2.6.3 FileReader
java.io.FileReader 类是读取字符文件的类。构造的时候使用系统默认的字符编码和默认字节缓冲区。
字符编码：字节和字符的对应规范。windows 系统的中文编码默认是 GBK 。
构造方法：
- 创建一个新的 FileReader ，给定要读取的 File 对象：
```public FileReader(File file) throws FileNotFoundException {}```
- 创建一个新的 FileReader ，给定要读取的文件的名称：
```public FileReader(String fileName) throws FileNotFoundException {}```

#### 2.6.4 Writer
java.io.Writer 抽象类是表示用于写出字符流的所有类的超类，将指定的字符信息写出到目的地，它定义了字符输出流的基本共性功能方法。
- 写入单个字符：
```public void write(int c) throws IOException {}```
- 写入字符数组：
```public void write(char cbuf[]) throws IOException {}```
- 写入从 offset 索引开始，len 长度的字符数组：
```abstract public void write(char cbuf[], int off, int len) throws IOException;```
- 写入字符串：
```public void write(String str) throws IOException {}```
- 写入从 offset 索引开始，len 长度的字符串：
```public void write(String str, int off, int len) throws IOException {}```
- 刷新流：
- 关闭流：
### 2.6.5 FileWriter
java.io.FileWriter 类是写出字符到文本的类。构造的时候使用系统默认的字符编码和默认字节缓冲区。
构造方法：
- 创建一个新的 FileWriter，给定要读取的 File 对象：
```public FileWriter(String fileName) throws IOException {}```
- 创建一个新的 FileWriter，给定要读取的文件的名称：
```public FileWriter(File file) throws IOException {}```
- 创建一个新的 FileWriter ，给定要读取的File对象，追加内容：
```public FileWriter(String fileName, boolean append) throws IOException {}```
- 创建一个新的 FileWriter ，给定要读取的文件的名称，追加内容：
```public FileWriter(File file, boolean append) throws IOException {}```

### 2.7 缓冲流
#### 2.7.1 概述
- 缓冲流，也叫高效流，按照数据类型分类：
- 字节缓冲流：BufferedOutputStream 、BufferedInputStream 。
- 字符缓冲流：BufferedReader 、BufferedWriter 。
- 缓冲流会在内部创建一个缓冲区数组，缺省使用 8192 个字节（8kb）的缓冲区。
- 缓冲流的基本原理：
- 当读取数据的时候，数据按块读入缓冲区，其后的读操作则直接访问缓冲区。
- 当使用 BufferedInputStream 读取字节文件时，BufferedInputStream 会一次性的从文件中读取 8192 个，存储在缓冲区中，直到缓冲区中装满了，才重新从文件中读取下一个 8192 个字节数组。
向流中写入字节的时候，不会直接写到文件中，先写到缓冲区中直到缓冲区中写满，BufferedOutputStream 才会将缓冲区中的数据一次性的写到文件里。使用 flush() 方法可以强制将缓冲区的内容全部写入输出流。
缓冲流的原理.png
>关闭流的顺序和打开流的顺序相反，只需要关闭最外层流即可，因为关闭最外层流的同时也会关闭对应的内层流。
>flush() 方法的使用：手动将 buffer 中内容写入文件。
>如果是带缓冲区的流对象的 close() 方法，不但会关闭流，还会在关闭流之前刷新缓冲区，关闭后不能再写出。
#### 2.7.2 字节缓冲流
- BufferedOutputStream 的构造方法：
```public BufferedOutputStream(OutputStream out) {}```
- BufferedInputStream 的构造方法：
```public BufferedInputStream(InputStream in) {}```
示例：
#### 2.7.3 字符缓冲流
- BufferedReader 的构造方法：
```public BufferedReader(Reader in) {}```
- BufferedReader 的特殊方法读取一行：
```public String readLine() throws IOException {}```
- BufferedWriter 的构造方法：
```public BufferedWriter(Writer out) {}```
- BufferedWriter 的特殊方法写入换行符：
```public void newLine() throws IOException {}```
示例：
### 2.8 转换流
#### 2.8.1 字符编码
> 计算机中存储的信息都是使用二进制表示的，而我们在屏幕上看到的数字、英文、标点符号、汉字等字符是二进制数转换之后的结果。
> 按照某种规则，将字符存储到计算机中，称为 编码 。
> 按照某种规则，将存储在计算机中的二进制数据解析并显示出来，称为 解码 。
例如：
按照A规则存储，同样按照A规则解析，那么就能正确的显示文本符号。
按照A规则存储，按照B规则解析，就会导致乱码现象。
字符编码（ CharacterEncoding ）：就是一套自然语言的字符和二进制数之间的对应规则。
编码表：生活中的文字和计算机中二进制的对应规则。
#### 2.8.2 字符集
字符集（ Charset ）：也称为编码表，是一个系统支持的所有字符集合，包括各个国家文字、标点符号、图形符号、数字等。
计算机要准确的存储和识别各种字符集符号，需要进行字符编码，一套字符集必然至少有一套字符编码。常见的字符集有：ASCII 字符集、GBK 字符集、 Unicode 字符集等等。
字符集.jpg
可见，当指定了编码，它所对应的字符集自然就指定了，所以编码才是我们最终要关心的。
#### 2.8.3 概述
> 转换流提供了在字节流和字符流之间的转换。
> Java API 提供了两个转换流：
> InputStreamReader ：将 InputStream 转换为 Reader 。
> OutputStreamWriter ：将 Writer转换为 OutputStream 。
> 字节流中的数据都是字符时，转换为字符流操作更加高效。
> 很多时候，我们使用转换流来处理文件乱码问题，实现编码和解码的功能。
> 转换流.jpg
#### 2.8.4 InputStreamReader
转换流 java.io.InputStreamReader 是 Reader 的子类，是从字节流到字符流的桥梁。它读取字节，并使用指定额字符集将其解码为字符。它的字符集可以有名称指定，也可以接受平台的默认字符集。
构造方法：
- 创建一个使用默认字符集的字符流：
```public InputStreamReader(InputStream in) {}```
- 创建一个指定字符集的字符流：
```public InputStreamReader(InputStream in, Charset cs) {}```
示例：
#### 2.8.5 OutputStreamWriter
转换流 java.io.OutputStreamWriter ，是 Writer 的子类，是从字符流到字节流的桥梁。使用指定的字符集将字符编码为字节。它的字符集可以由名称指定，也可以接受平台的默认字符集。
构造方法：
- 创建一个使用默认字符集的字符流：```public OutputStreamWriter(OutputStream out) {}```
- 创建一个指定字符集的字符流：```public OutputStreamWriter(OutputStream out, Charset cs) {}```
示例：
### 2.9 打印流
- 字节输出流：PrintStream 。
- 字符输出流：PrintWriter 。
- 打印流的特点：
   - ① 打印流负责输出打印，不关心数据源。
   - ② 提供了一系列重载的 print() 或 println() 方法，用于多种数据类型的输出。
   - ③ 打印流永远不会抛出 IOException 。
   - ④ 打印流具有自动刷新的功能：
构造方法的第一个参数必须是 IO 流对象，第二个参数是 true 。
  ```
   - public PrintStream(OutputStream out, boolean autoFlush) {}
  ```
必须调用 println() 、printf() 、format() 中的其中一个，才会启用自动刷新。
⑤ System.out 返回的是 PrintStream 的实例。
示例：
### 2.10 序列化
#### 2.10.1 概述
Java 提供了一种 对象序列化 的机制。用一个字节序列可以表示一个对象，该字节序列包含该 对象的类型 和 对象中存储的属性 等信息。
字节序列写出到文件之后，相当于文件中 持久保存 了一个对象信息；反之，该字节序列还可以从文件中读取回来，重构对象，对它进行 反序列化 。
对象的数据、对象的类型和对象中存储的数据信息，都可以用来在内存中创建对象。
序列化和反系列化.jpg
#### 2.10.2 ObjectOutputStream
java.io.ObjectOutputStream 类是将 Java 对象的原始数据类型写出到文件以实现对象的持久存储。
* 构造方法：
* 序列化操作：
   - ① 类必须实现 java.io.Serializable 接口，Serializable 是一个标记接口，不实现此接口的类不会使任何状态序列化或反序列化，会抛出NotSerializableException 异常（如果类中的某个属性也是引用数据类型，那么该属性如果也要序列化，必须实现 Serializable 接口）。
   - ② 该类的所有属性必须是可序列化的。如果有一个属性不需要序列化的，则该属性必须注明是瞬时态的，使用 transient 关键字修饰。
   - ③ 静态变量的值不会序列化。
写出对象的方法：
  ```public final void writeObject(Object obj) throws IOException {}```
#### 2.10.3 ObjectInputStream
java.io.ObjectInputStream 类是将之前使用 ObjectOutputStream 序列化的原始数据恢复成对象。
构造方法：
```public ObjectInputStream(InputStream in) throws IOException {}```
读取对象的方法：
```public final Object readObject()
throws IOException, ClassNotFoundException {}```
