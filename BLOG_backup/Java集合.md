---
title: Java集合
date: 2020-09-05 09:18:44
tags:
---

# 引言  
- 优质博客
  - [JavaGuide](https://github.com/Snailclimb/JavaGuide/blob/master/docs/java/collection/Java%E9%9B%86%E5%90%88%E6%A1%86%E6%9E%B6%E5%B8%B8%E8%A7%81%E9%9D%A2%E8%AF%95%E9%A2%98.md)
  - [java集合继承关系图](https://www.cnblogs.com/jing99/p/7057245.html)  
  - https://www.runoob.com/java/java-stack-class.html  

# 集合概述
- java集合框架图
  ![](https://www.runoob.com/wp-content/uploads/2014/01/2243690-9cd9c896e0d512ed.gif)  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200905155442847.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODkyNTEx,size_16,color_FFFFFF,t_70#pic_center)

# 集合涉及到的常见接口
## Iterator接口  
- 主要方法
  - boolean hasNext()
  - E next()  

## Comparable接口
- 重写compareTo方法（大于 返回正  == 返回0 小于 返回负）  

## Comparator接口
- 从写compare()方法  

# Collection 接口
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200905162053918.png#pic_center)
**集合中存储的都是对象的引用(地址)。**  
- 集合的输出
  - 四种输出方式
    - Iterator
    - ListIterator
    - Enumeration
    - foreach
  - 注意：
    - *在迭代时，不可以通过集合对象的方法操作集合中的元素，因为会发生ConcurrentModificationException异常。所以，在迭代器时，只能用迭代器的放过操作元素，可是Iterator方法是有限的，只能对元素进行判断，取出，删除的操作，如果想要其他的操作如添加，修改等，就需要使用其子接口，ListIterator。该接口只能通过List集合的listIterator方法获取。*  

## List接口  
(对付顺序的好帮手)： 存储的元素是有序的、可重复的。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200905162201254.png#pic_center)


### ArrayList类  
- Object[] 数组
- 查询快
- add(E e) O(1)
- add(int index, E element)  O(n-i)  
- 优秀参考：
  - [通过源码一步一步分析 ArrayList 扩容机制](https://github.com/Snailclimb/JavaGuide/blob/master/docs/java/collection/ArrayList-Grow.md)  
  - [ArrayList核心源码](https://github.com/Snailclimb/JavaGuide/blob/master/docs/java/collection/ArrayList.md)   

### LinkedList类  
- 双向链表实现
- 查询慢
- add(E e)  O(1)
- add(int index, E element) o(n)   

<style>
table th:first-of-type {
    width: 2cm;
}
table th:nth-of-type(2) {
    width: 300pt;
}
table th:nth-of-type(3) {
    width: 12em;
}
table th:nth-of-type(4) {
    width: 12em;
}
table th:nth-of-type(5) {
    width: 12em;
}
</style>  
操作类型|增|删除|改|查  
---|---|---|---|---
函数|add​(int index, E element)<br> add​(E e)<br> **offer​(E e)**<br> addAll​(Collection<? extends E> c)<br> **addFirst​(E e)**<br> **addLast​(E e)**<br>|clear​()<br> poll​()<br> remove​(int index)<br> remove​(Object o)<br>|set​(int index, E element)<br>|contains​(Object o)<br>  get​(int index)<br> 

- LinkedList可以实现List,Queue,Deque(双端队列)接口  

### Vector类  
- 线程安全的，效率低  

#### Stack类  
Vector类的子类
  1. boolean empty()
  判断栈是否为空
  2. E peek()
  返回栈顶对象，不移除
  3. E pop()
  返回栈顶对象，并移除
  4. E push(E item)
  压入栈顶
  5. int search(Object o)
  返回对象在栈的位置  

## Queue接口  
- Queue接口定义了如下6个方法，我们常用的LinkedList类就实现了Queue接口。 
  1. boolean add(E e)
  向队列中添加元素
  2. E element()
  返回队列的头，且不移除
  3. boolean offer(E e)
  向队列中添加元素
  4. E peek()
  返回队列的头，且不移除
  5. E poll()
  返回队列的头，且移除
  6. E remove()
  返回队列的头，且移除
  add、element、remove会在操作失败时抛出异常，而offer、peek、poll在操作失败时返回特殊值。   

- **offer()与add()的区别**
  - 超出队列界限时，add（）方法是抛出异常让你处理，而offer（）方法是直接返回false
  - 推荐使用offer()  

### PriorityQueue类  
- 概述
  实际上是一个堆（不指定Comparator时默认为最小堆）
队列既可以根据元素的自然顺序来排序，也可以根据 Comparator来设置排序规则。
队列的头是按指定排序方式的最小元素。如果多个元素都是最小值，则头是其中一个元素。
新建对象的时候可以指定一个初始容量，其容量会自动增加。
- 参考博客
  [Java学习笔记--PriorityQueue(优先队列)(堆)](https://www.cnblogs.com/gnivor/p/4841191.html)  
- 注意点
  - **插入方法（offer()、poll()、remove() 、add() 方法）时间复杂度为O(log(n))** ；
  - **remove(Object) 和 contains(Object) 时间复杂度为O(n)**；
  - 检索方法（peek、element 和 size）时间复杂度为常量。
  - 不允许使用 null 元素。
  - 不是同步的。不是线程安全的。如果多个线程中的任意线程从结构上修改了列表， 则这些线程不应同时访问 PriorityQueue实例。保证线程安全可以使用PriorityBlockingQueue 类。
  - 该队列是用数组实现，但是数组大小可以动态增加，容量无限。
  - 此类及其迭代器实现了 Collection 和 Iterator 接口的所有可选 方法。
  - 可以在构造函数中指定如何排序。`PriorityQueue(int initialCapacity, Comparator<? super E> comparator)`

优先队列主要方法： 

  Modifier and Type | 方法 |描述  
  ---|---|--- 
  boolean| add​(E e) |将指定的元素插入到此优先级队列中。  
  void| clear​() |从此优先级队列中删除所有元素。  
  Comparator<? super E>| comparator​()| 返回用于为了在这个队列中的元素，或比较null如果此队列根据所述排序natural ordering的元素。  
  boolean| contains​(Object o) | 如果此队列包含指定的元素，则返回 true 。  
  Iterator<E>| iterator​() |返回此队列中的元素的迭代器。  
  boolean| offer​(E e)| 将指定的元素插入到此优先级队列中。  
  E| peek​()| 检索但不删除此队列的头，如果此队列为空，则返回 null 。  
  E| poll​()| 检索并删除此队列的头部，如果此队列为空，则返回 null 。  
  boolean| remove​(Object o)| 从该队列中删除指定元素的单个实例（如果存在）。  
  int| size​()| 返回此集合中的元素数。  
  Spliterator<E>| spliterator​()| 在此队列中的元素上创建late-binding和故障快速 Spliterator 。  
  Object[]| toArray​()| 返回一个包含此队列中所有元素的数组。  
  <T> T[]| toArray​(T[] a)| 返回一个包含此队列中所有元素的数组; 返回的数组的运行时类型是指定数组的运行时类型。 



## Deque接口  
双端队列 ，LinkedList类和ArrayDeque类实现了该接口。可以操作两端

### ArrayDeque类   
- 与LinkedList类 相似，区别是底层为数组实现  

## Set接口    

### HashSet类  
- HashSet是如何保证元素唯一性的呢？
    >是通过元素的两个方法，hashCode和equals来完成。
    如果元素的HashCode值相同，才会判断equals是否为true。
    如果元素的hashcode值不同，不会调用equals。  
　　　
### LinkedHashSet类  
- 能够按照添加的顺序遍历  

### SortedSet接口  

#### TreeSet类  
- 底层为红黑树
- 能够按照添加元素的顺序进行遍历，排序的方式有自然排序和定制排序。

# Map接口  
<Key,Value>
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200905162910374.png#pic_center)

## HashTable 类  
- 线程安全 其内部方法基本经过`synchronized`修饰 （替代 ConcurrentHashMap）
- 效率较低，基本被淘汰  

##  HashMap  类  
- 优秀参考链接：
  - [HashMap(JDK1.8)源码 ](https://github.com/Snailclimb/JavaGuide/blob/master/docs/java/collection/HashMap.md)
- 底层数据结构： 数组 + 链表（jdk1.8后 链表长于（8）将链表转为红黑树）
- 扩容机制：
  - 当HashMap中的元素个数超过数组大小(数组总大小length,不是数组中个数size)\*loadFactor时，就会进行数组扩容，loadFactor的默认值为0.75，这是一个折中的取值。也就是说，默认情况下，数组大小为16，那么当HashMap中元素个数超过16\*0.75=12（这个值就是代码中的threshold值，也叫做临界值）的时候，就把数组的大小扩展为 2\*16=32，即扩大一倍，然后重新计算每个元素在数组中的位置。
- 初始容量大小和每次扩充容量大小：
  - HashMap 默认的初始化大小为 16。之后每次扩充，容量变为原来的 2 倍。
  -  创建时如果给定了容量初始值，那么 Hashtable 会直接使用你给定的大小，而 HashMap 会将其扩充为 2 的幂次方大小（HashMap 中的tableSizeFor()方法保证，下面给出了源代码）。也就是说 HashMap 总是使用 2 的幂作为哈希表的大小。 
  -  为什么是2的幂次？
     -  因为在计算元素该存放的位置的时候，用到的算法是将元素的hashcode与当前map长度-1进行与运算。源码：
  ```Java
          static int indexFor(int h, int length) {
              // assert Integer.bitCount(length) == 1 : "length must be a non-zero power of 2";
              return h & (length-1);
  }
  ```
  如果map长度为2的幂次，那长度-1的二进制一定为11111...这种形式，进行与运算就看元素的hashcode，但是如果map的长度不是2的幂次，比如为15，那长度-1就是14，二进制为1110，无论与谁相与最后一位一定是0，0001，0011，0101，1001，1011，0111，1101这几个位置就永远都不能存放元素了，空间浪费相当大。也增加了添加元素是发生碰撞的机会。减慢了查询效率。所以Hashmap的大小是2的幂次。
- [Java遍历HashMap并修改(remove)](https://blog.csdn.net/zmx729618/article/details/52795493)

### LinkedHashMap 类  
  - HashMap的子类，在上`HashMap`结构的基础上，增加了一条双向链表，使得上面的结构可以保持键值对的**插入顺序**。  

## SortedMap 接口  

### TreeMap类  
- 底层数据结构：红黑树
    
   
# 其他问题
## 什么是快速失败（fail-fast）  
- 快速失败(fail-fast) 是 Java 集合的一种错误检测机制。在使用迭代器对集合进行遍历的时候，我们在多线程下操作非安全失败(fail-safe)的集合类可能就会触发 fail-fast 机制，导致抛出 ConcurrentModificationException 异常。 另外，在单线程下，如果在遍历过程中对集合对象的内容进行了修改的话也会触发 fail-fast 机制。
- 实现机制： 每当迭代器使用 hashNext()/next()遍历下一个元素之前，都会检测 modCount 变量是否为 expectedModCount 值，是的话就返回遍历；否则抛出异常，终止遍历。如果我们在集合被遍历期间对其进行修改的话，就会改变 modCount 的值，进而导致 modCount != expectedModCount ，进而抛出 ConcurrentModificationException 异常。
- **通过 Iterator 的方法修改集合的话会修改到 expectedModCount 的值，所以不会抛出异常。**

## 什么是安全失败（fail-safe）  
- 采用安全失败机制的集合容器，在遍历时不是直接在集合内容上访问的，而是先复制原有集合内容，在拷贝的集合上进行遍历。所以，在遍历过程中对原集合所作的修改并不能被迭代器检测到，故不会抛 ConcurrentModificationException 异常。

## Arrays.asList()  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200908103807718.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODkyNTEx,size_16,color_FFFFFF,t_70#pic_center)

## Java可选操作 
简单说就是抽象类的的某些bai派生类实现里，或者接口的du某个实现类里面，某个方法可能zhi是无意义的，调用该方dao法会抛出一个异常。例如在collection的某些实现类里，里面的元素可能都是只读的，那么add这个接口是无意义的，调用会抛出`UnspportedOperationException`异常。
从设计的角度说，如果一个接口的方法设计为optional，表示这个方法不是为所有的实现而设定的，而只是为某一类的实现而设定的。


# 其他(草稿)
- List接口
  - ArrayList 
    - Object[] 数组
    - 查询快
    - add(E e) O(1)
    - add(int index, E element)  O(n-i)
  - LinkedList 
    - 双向链表实现
    - 查询慢
    - add(E e)  O(1)
    - add(int index, E element) o(n)



- Map接口
  - HashMap
    - 数组 + 链表（jdk1.8后 链表长于（8）将链表转为红黑树）
  - LinkedHashMap  
    - 在上面结构的基础上，增加了一条双向链表，使得上面的结构可以保持键值对的**插入顺序**。
  - TreeMap
  - LinkedTable
  - ConcurrentHashMap
    - 只锁桶
- Set
  - HashSet
    - 线程不安全 底层是HashMap 可以存储null值
  - LinkedHashSet
  - TreeSet  


- Collection接口  
  ![](https://images2015.cnblogs.com/blog/1010726/201706/1010726-20170621005616085-269540653.png)  
  
Modifier and Typ  | 方法| 描述  
--------|-----|-----
boolean| add(E e)|确保此集合包含指定的元素（可选操作）。 
boolean |addAll​(Collection<? extends E> c)| 将指定集合中的所有元素添加到此集合（可选操作）。  
void| clear​() |从此集合中删除所有元素（可选操作）。  
boolean |contains​(Object o) |如果此集合包含指定的元素，则返回 true 。  
boolean |containsAll​(Collection<?> c) |如果此集合包含指定集合中的所有元素，则返回 true 。  
boolean |equals​(Object o) |将指定的对象与此集合进行比较以获得相等性。  
int |hashCode​() |返回此集合的哈希码值。  
boolean |isEmpty​()| 如果此集合不包含元素，则返回 true 。  
Iterator<E> |iterator​()| 返回此集合中元素的迭代器。  
default Stream<E> |parallelStream​()| 返回可能并行的 Stream与此集合作为其来源。  
boolean |remove​(Object o)| 从该集合中删除指定元素的单个实例（如果存在）（可选操作）。  
boolean |removeAll​(Collection<?> c)| 删除指定集合中包含的所有此集合的元素（可选操作）。  
default |boolean removeIf​(Predicate<? super E> filter) |删除满足给定谓词的此集合的所有元素。  
boolean |retainAll​(Collection<?> c) |仅保留此集合中包含在指定集合中的元素（可选操作）。  
int |size​()| 返回此集合中的元素数。  
default |Spliterator<E> spliterator​()| 在此集合中的元素上创建一个Spliterator 。  
default |Stream<E> stream​() |返回一个序列 Stream与此集合作为其来源。  
Object[] |toArray​()| 返回一个包含此集合中所有元素的数组。  
<T> T[] |toArray​(T[] a)| 返回一个包含此集合中所有元素的数组; 返回的数组的运行时类型是指定数组的运行时类型。  