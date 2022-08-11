- Collection体系集合：可以使用默认方法stream()生成流,
- Map体系集合：先把Map转成Set集合，间接生成流。
- 数组：通过Arrays工具类的stream方法
- 同种数据类型的，通过Stream接口的静态方法of 生成流

**流的中间操作方法**

| **方法名**                               | **说明**                                                   |
| ---------------------------------------- | ---------------------------------------------------------- |
| Stream filter(Predicate predicate)       | 用于对流中的数据进行过滤                                   |
| Stream limit(long maxSize)               | 返回此流中的元素组成的流，截取前指定参数个数的数据         |
| Stream skip(long n)                      | 跳过指定参数个数的数据，返回由该流的剩余元素组成的流       |
| static Stream concat(Stream a, Stream b) | 合并a和b两个流为一个流                                     |
| Stream distinct()                        | 返回由该流的不同元素（根据Object.equals(Object) ）组成的流 |


**流的终结操作方法**

| **方法名**                    | **说明**                 |
| ----------------------------- | ------------------------ |
| void forEach(Consumer action) | 对此流的每个元素执行操作 |
| long count()                  | 返回此流中的元素数       |

**Stream收集操作**
把流中的数据收集到集合中
方法

| **方法名**                     | **说明**           |
| ------------------------------ | ------------------ |
| R collect(Collector collector) | 把结果收集到集合中 |


---

| **方法名**                                                   | **说明**               |
| ------------------------------------------------------------ | ---------------------- |
| public static Collector toList()                             | 把元素收集到List集合中 |
| public static Collector toSet()                              | 把元素收集到Set集合中  |
| public static Collector toMap(Function keyMapper,Function valueMapper) | 把元素收集到Map集合中  |

