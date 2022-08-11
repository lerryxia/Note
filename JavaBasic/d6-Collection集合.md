## **Collection**

Collection集合是最上层的接口，是所有集合的父接口
![image.png](/img/JavaBasic/d6_1.png)
Collection 里还定义了很多方法，主要是用于数据的[增删改查]，也叫 CRUD:

- Create, Read, Update, and Delete.

collection中常见的 API 分为这四大类：
<table>
<tr>
<th>功能</th><th>方法</th>
</tr>
<tr><td>增  </td><td>add()/addAll()</td></tr>
<tr><td>删  </td><td>remove/removeAll</td></tr>
<tr><td>改  </td><td>无</td></tr>
<tr><td>查  </td><td>contains()/containsAll()</td></tr>
<tr><td>其他</td><td>isEmpty()/size()/toArray()</td></tr>
</table>
下面具体来看：
**增**：

- _**boolean add(E e);**_

add() 方法传入的数据类型必须是 Object，所以当写入基本数据类型的时候，会做自动装箱 auto-boxing 和自动拆箱 unboxing。
还有另外一个方法 addAll()，可以把另一个集合里的元素加到此集合中。

- _**boolean addAll(Collection<? extends E> c);**_

**删**：

- _**boolean remove(Object o);**_

remove()是删除的指定元素。
那和 addAll() 对应的，自然就有removeAll()，就是把集合 B 中的所有元素都删掉。

- _**boolean removeAll(Collection<?> c);**_

**改**：
Collection Interface 里并没有直接改元素的操作，反正删和增就可以完成改了嘛！
**查**：
查下集合中有没有某个特定的元素：

- _**boolean contains(Object o);**_

查集合 A 是否包含了集合 B：

- _**boolean containsAll(Collection<?> c);**_

**还有一些对集合整体的操作：**
判断集合是否为空：

- _**boolean isEmpty();**_

集合的大小：

- _**int size();**_

把集合转成数组：

- _**Object[] toArray();**_

以上就是 Collection 中常用的 API 了。
在接口里都定义好了，子类不要也得要。
当然子类也会做一些自己的实现，这样就有了不同的数据结构。
那我们一个个来看。

## List（特点：有序，可重复）

![image.png](/img/JavaBasic/d6_2.png)
>List 的实现方式有 LinkedList 和 ArrayList 两种，那面试时最常问的就是这两个数据结构如何选择。
- 对于这类选择问题：
一是考虑数据结构是否能完成需要的功能；
如果都能完成，二是考虑哪种更高效。
- 那具体来看这两个 classes 的 API 和它们的时间复杂度：
![image.png](/img/JavaBasic/d6_2.png)
**add(E e)** 是在尾巴上加元素，虽然 ArrayList 可能会有扩容的情况出现，但是均摊复杂度（amortized time complexity）还是 O(1) 的。
**add(int index, E e)** 是在特定的位置上加元素，LinkedList 需要先找到这个位置，再加上这个元素，虽然单纯的「加」这个动作是 O(1) 的，但是要找到这个位置还是 O(n) 的。（这个有的人就认为是 O(1)，和面试官解释清楚就行了，拒绝扛精。
**remove(int index)** 是 remove 这个 index 上的元素，所以

- ArrayList 找到这个元素的过程是 O(1)，但是 remove 之后，后续元素都要往前移动一位，所以均摊复杂度是 O(n)；
- LinkedList 也是要先找到这个 index，这个过程是 O(n) 的，所以整体也是 O(n)。

**remove(E e)** 是 remove 见到的第一个这个元素，那么

- ArrayList 要先找到这个元素，这个过程是 O(n)，然后移除后还要往前移一位，这个更是 O(n)，总的还是 O(n)；
- LinkedList 也是要先找，这个过程是 O(n)，然后移走，这个过程是 O(1)，总的是 O(n).

**那造成时间复杂度的区别的原因是什么呢？**
答：

- _**因为 ArrayList 是用数组来实现的。LinkedList是基于链表实现的。**_
- _**而数组和链表的最大区别就是数组是可以随机访问的（random access）。**_

这个特点造成了在数组里可以通过下标用 O(1) 的时间拿到任何位置的数，而链表则做不到，只能从头开始逐个遍历。
也就是说在「改查」这两个功能上，**因为数组能够随机访问，所以 ArrayList 的效率高。**
那「增删」呢？
如果不考虑找到这个元素的时间，
数组因为物理上的连续性，当要增删元素时，在尾部还好，但是其他地方就会导致后续元素都要移动，所以效率较低；而链表则可以轻松的断开和下一个元素的连接，直接插入新元素或者移除旧元素。
但是呢，实际上你不能不考虑找到元素的时间啊。。。而且如果是在尾部操作，数据量大时 ArrayList 会更快的。
所以说：

- _**改查选择 ArrayList；**_
- _**增删在尾部的选择 ArrayList；**_
- 其他情况下，如果时间复杂度一样，推荐选择 ArrayList，因为overhead 更小，或者说内存使用更有效率。

## **拓展：**

- LinkedList是基于双向循环链表实现的，除了可以当做链表来操作外，它还可以当做栈、队列和双端队列来使用。
- LinkedList同样是非线程安全的，只在单线程下适合使用。
- LinkedList实现了Serializable接口，因此它支持序列化，能够通过序列化传输，实现了Cloneable接口，能被克隆。
  什么是链表

链表是由一系列非连续的节点组成的存储结构，简单分下类的话，链表又分为单向链表和双向链表，而单向/双向链表又可以分为循环链表和非循环链表，下面简单就这四种链表进行图解说明。
1. 单向链表
单向链表就是通过每个结点的指针指向下一个结点从而链接起来的结构，最后一个节点的next指向null。
![image.png](/img/JavaBasic/d6_4.png)
2. 单向循环链表
单向循环链表和单向列表的不同是，最后一个节点的next不是指向null，而是指向head节点，形成一个“环”。
![image.png](/img/JavaBasic/d6_5.png)
3. 双向链表
从名字就可以看出，双向链表是包含两个指针的，pre指向前一个节点，next指向后一个节点，但是第一个节点head的pre指向null，最后一个节点的tail指向null。
![image.png](/img/JavaBasic/d6_6.png)
4. 双向循环链表**_
双向循环链表和双向链表的不同在于，第一个节点的pre指向最后一个节点，最后一个节点的next指向第一个节点，也形成一个“环”。而LinkedList就是基于双向循环链表设计的。
![image.png](/img/JavaBasic/d6_7.png)
## Queue & Deque
Queue 是一端进另一端出的线性数据结构；而 Deque 是两端都可以进出的。
![image.png](/img/JavaBasic/d6_8.png)
## **Queue**

Java 中的 这个 Queue 接口稍微有点坑，一般来说队列的语义都是先进先出（FIFO）的。
但是这里有个例外，就是 PriorityQueue，也叫 heap，并不按照进去的时间顺序出来，而是按照规定的优先级出去，并且它的操作并不是 O(1) 的，时间复杂度的计算稍微有点复杂，
它有两组 API，基本功能是一样的，但是呢：

- 一组是会抛异常的；
- 另一组会返回一个特殊值。

![image.png](/img/JavaBasic/d6_10.png)
**为什么会抛异常呢？**

- 比如队列空了，那 remove() 就会抛异常，但是 poll() 就返回 null；element() 就会抛异常，而 peek()就返回 null 就好了。

**那 add(e) 怎么会抛异常呢？**
有些 Queue 它会有容量的限制，比如 BlockingQueue，那如果已经达到了它最大的容量且不会扩容的，就会抛异常；但如果 offer(e)，就会 return false.
**那怎么选择呢？：**

- 首先，要用就用同一组 API，前后要统一；
- 其次，根据需求。如果你需要它抛异常，那就是用抛异常的；不过做算法题时基本不用，所以选那组返回特殊值的就好了。

## _**Deque**_

Deque 是两端都可以进出的，那自然是有针对 First 端的操作和对 Last 端的操作，那每端都有两组，一组抛异常，一组返回特殊值：
![image.png](/img/JavaBasic/d6_11.png)
使用时同理，要用就用同一组。
Queue 和 Deque 的这些 API 都是 O(1) 的时间复杂度，准确来说是均摊时间复杂度。
实现类
它们的实现类有这三个：
![image.png](/img/JavaBasic/d6_12.png)
所以说，

- 如果想实现「普通队列 - 先进先出」的语义，就使用 LinkedList 或者 ArrayDeque 来实现；
- 如果想实现「优先队列」的语义，就使用 PriorityQueue；
- 如果想实现「栈」的语义，就使用 ArrayDeque。

我们一个个来看。
在实现普通队列时，**如何选择用 LinkedList 还是 ArrayDeque 呢？**
总结来说就是推荐使用 ArrayDeque，因为效率高，而 LinkedList 还会有其他的额外开销（overhead）。
**那 ArrayDeque 和 LinkedList 的区别有哪些呢？**
还是在刚才的同一个问题下，这是我认为总结的最好的：

- ArrayDeque 是一个可扩容的数组，LinkedList 是链表结构；
- ArrayDeque 里不可以存 null 值，但是LinkedList 可以；
- ArrayDeque 在操作头尾端的增删操作时更高效，但是 LinkedList
  只有在当要移除中间某个元素且已经找到了这个元素后的移除才是 O(1) 的；
- ArrayDeque 在内存使用方面更高效。
  所以，只要不是必须要存 null 值，就选择 ArrayDeque 吧！

**那如果是一个很资深的面试官问你，什么情况下你要选择用 LinkedList 呢？**
答：

- Java 6 以前。。。因为 ArrayDeque 在 Java 6 之后才有的。。
  为了版本兼容的问题，实际工作中我们不得不做一些妥协。。 那最后一个问题，就是关于 Stack 了。

## **Stack**

Stack 在语义上是 后进先出（LIFO） 的线性数据结构。
有很多高频面试题都是要用到栈的，比如接水问题，虽然最优解是用双指针，但是用栈是最直观的解法也是需要了解的，之后有机会再专门写吧。
那在 Java 中是怎么实现栈的呢？
虽然 Java 中有 Stack 这个类，但是呢，官方文档都说不让用了！
原因也很简单，因为 Vector 已经过被弃用了，而 Stack 是继承 Vector 的。
那么想实现 Stack 的语义，就用 ArrayDeque 吧：

- Deque stack = new ArrayDeque<>();

## Set（无序，不可重复）

最后一个 Set，刚才已经说过了 Set 的特定是无序，不重复的。
![image.png](/img/JavaBasic/d6_13.png)
Set 的常用实现类有三个：
**HashSet:** 采用 Hashmap 的 key 来储存元素，主要特点是无序的，基本操作都是 O(1) 的时间复杂度，很快。
**LinkedHashSet:** 这个是一个 HashSet + LinkedList 的结构，特点就是既拥有了 O(1) 的时间复杂度，又能够保留插入的顺序。
**TreeSet:** 采用红黑树结构，**_特点是可以有序_**，可以用自然排序或者自定义比较器来排序；缺点就是查询速度没有 HashSet 快。
**那每个 Set 的底层实现其实就是对应的 Map：
数值放在 map 中的 key 上，value 上放了个 PRESENT，是一个静态的 Object，相当于 place holder，每个 key 都指向这个 object。**

## 常用API

//HashSet:添加的索引无序 不重复 无索引
Collection<String> list1 = new HashSet<>();
//.add 添加元素并返回Boolean值
list1.add("java");
list1.add("html");

//.clear()清空集合元素
list1.clear();
System._out_.println(list1);

//判断集合是否为空 true
System._out_.println(list1.isEmpty());

//获取集合大小
System._out_.println(list1.size());

//判断集合是否包含某个元素
System._out_.println(list1.contains("java"));

//删除某个元素 如果重复仅删除第一个
System._out_.println(list1.remove("java"));

//集合转化为数组
Object[] c = list1.toArray();
System._out_.println(c);//地址
System._out_.println(Arrays._toString_(c));//内容

//合并集合
Collection<String> c1 = new ArrayList();
c1.add("c++");
Collection<String> c2 = new ArrayList();
c2.add("html");

c1.addAll(c2);//c2元素添加到c1
System._out_.println(c1);

## 迭代器（遍历集合）Iterator

Collection<String> list = new ArrayList();
list.add("java");
list.add("c++");
list.add("html");
list.add("python");
//迭代器对象
Iterator<String> iterator = list.iterator();
// String ele = iterator.next();

//while循环
while (iterator.hasNext()){
String ele = iterator.next();
System._out_.println(ele);
}

### 增强for循环

**增强型for循环使用起来比较方便，代码也比较简单，如果只是操作集合中元素的而不使用索引的话，建议用此方法。
对于普通for循环，如果需要使用索引进行其它操作的话，建议用这个。**
详细来说：
**1，区别：**
增强for循环必须有被[遍历](/img/JavaBasic/d6_14.png)
普通for循环遍历[数组](/img/JavaBasic/d6_15.png)
增强for循环不能获取下标，所以遍历数组时最好使用普通for循环。
**2，特点：**
书写简洁。
对集合进行遍历，只能获取集合元素，不能对集合进行操作，类似迭代器的简写形式，但是迭代器可以对元素进行remove操作（ListIterator可以进行增删改查的操作）。
3，格式：
**for(数据类型变量名 :被遍历的集合（collection）或者数组) {
执行语句
}**

### lambda遍历

```
        Collection<String> list = new ArrayList();
        list.add("java");
        list.add("c++");
        list.add("html");
        list.add("python");
        System.out.println(list);

        //lambda的Collection遍历
        list.forEach(new Consumer<String>() {
            @Override
            public void accept(String s) {
                System.out.println(s);
            }
        });
        //简化写法
        list.forEach(s -> {
            System.out.println(s);
        });
```


