# 一、**Map集合的特点**：

**Map集合的特点**：
1.Map是一个双列[集合](https://so.csdn.net/so/search?q=%E9%9B%86%E5%90%88&spm=1001.2101.3001.7020)，一个元素包含两个值（一个key，一个value）
2.Map集合中的元素，key和value的数据类型可以相同，也可以不同
3.Map中的元素，key不允许重复，value可以重复
4.Map里的key和value是一一对应的。

# **二、Map中的方法:**

1.public   V  put （K key，V value） 把指定的键和值添加到Map集合中，返回值是V
如果要存储的键值对，key不重复返回值V是null
如果要存储的键值对，key重复返回值V是被替换的value值

# 三、遍历Map集合的方式

1.通过键找值的方法；
使用了setKey方法，将Map集合中的key值，存储到Set集合，用迭代器或foreach循环遍历Set集合来获取Map集合的每一个key，并使用get（key）方法来获取value值

# （一）、HashMap

**【1】.特点**：

- 1.HashMap底是哈希表，查询速度非常快（jdk1.8之前是数组+单向链表，1.8之后是数组+单向链表/红黑树 ，链表长度超过8时，换成红黑树）
- 2. HashMap是无序的集合，存储元素和取出元素的顺序有可能不一致
- 3.集合是不同步的，也就是说是多线程的，速度快

**【2】**.HashMap存储自定义类型键值
HashMap存储自定义类型键值，Map集合保证key是唯一的：作为key的元素，必须重写hashCode方法和equals方法，以保证key唯一

#### HashMap有子类LinkedHashMap：LinkedHashMap <K,V> extends HashMap <K,V>

是Map接口的哈希表和链表的实现，具有可预知的迭代顺序（有序）
底层原理：哈希表+链表（记录元素顺序）
**特点**：1.LinkedHashMap底层是哈希表+链表（保证迭代的顺序）
2.LinkedHashMap是一个有序的集合，存储元素和取出元素的顺序一致
改进之处就是：元素存储有序了