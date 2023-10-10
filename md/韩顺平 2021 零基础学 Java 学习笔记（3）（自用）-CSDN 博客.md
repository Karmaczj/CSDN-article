> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/weixin_43973189/article/details/121380152?spm=1001.2014.3001.5502)

#### 目录

*   *   *   [第 14 章 集合](#_14___1)
        *   [第 15 章 泛型](#_15___1471)
        *   [第 16 章 坦克大战](#_16___2110)
        *   [第 17 章 多线程基础](#_17___2117)
        *   [第 19 章 IO 流](#_19__IO__2659)

#### 第 14 章 集合

14.1 集合的理解和好处  
![](https://img-blog.csdnimg.cn/b350fa70129d469ebd98f972e3036dbd.png)  
![](https://img-blog.csdnimg.cn/69d613391408420da7d28eaa1475d2c9.png)  
14.2 集合的框架体系  
Java 的集合类很多，主要分为两大类，如图 ：  
![](https://img-blog.csdnimg.cn/156965ee8a8840acb37865270266d287.png)  
![](https://img-blog.csdnimg.cn/97d77dc1223b49d4bcd31183772202c9.png)  
![](https://img-blog.csdnimg.cn/54f8ac7ab3744f078e5cb438abf20b42.png)  
14.3 Collection 接口和常用方法

14.3.1 Collection 接口实现类的特点  
![](https://img-blog.csdnimg.cn/0922d83af11b445ab3762f5e73e376a1.png)  
![](https://img-blog.csdnimg.cn/0ca684aeafb14041827e525f3cf77ed2.png)

```
package com.hspedu.collection_;
import java.util.ArrayList;
import java.util.List;
public class CollectionMethod {
    @SuppressWarnings({"all"})
    public static void main(String[] args) {
        List list = new ArrayList();
//        add:添加单个元素
        list.add("jack");
        list.add(10);//list.add(new Integer(10))
        list.add(true);
        System.out.println("list=" + list);
//        remove:删除指定元素
        //list.remove(0);//删除第一个元素
        list.remove(true);//指定删除某个元素
        System.out.println("list=" + list);
//        contains:查找元素是否存在
        System.out.println(list.contains("jack"));//T
//        size:获取元素个数
        System.out.println(list.size());//2
//        isEmpty:判断是否为空
        System.out.println(list.isEmpty());//F
//        clear:清空
        list.clear();
        System.out.println("list=" + list);
//        addAll:添加多个元素
        ArrayList list2 = new ArrayList();
        list2.add("红楼梦");
        list2.add("三国演义");
        list.addAll(list2);
        System.out.println("list=" + list);
//        containsAll:查找多个元素是否都存在
        System.out.println(list.containsAll(list2));//T
//        removeAll：删除多个元素
        list.add("聊斋");
        list.removeAll(list2);
        System.out.println("list=" + list);//[聊斋]
//        说明：以ArrayList实现类来演示.
    }
}
```

14.3.2 Collection 接口遍历元素方式 1 - 使用 Iterator(迭代器)  
![](https://img-blog.csdnimg.cn/85603ce934f746b88bd7b778762011e1.png)  
![](https://img-blog.csdnimg.cn/78b175ea42074abf84fd28cc57836fa0.png)  
![](https://img-blog.csdnimg.cn/e362eab0085d4badad308e3821377ef7.png)

```
package com.hspedu.collection_;
import java.util.ArrayList;
import java.util.Collection;
import java.util.Iterator;
public class CollectionIterator {
    @SuppressWarnings({"all"})
    public static void main(String[] args) {
        Collection col = new ArrayList();
        col.add(new Book("三国演义", "罗贯中", 10.1));
        col.add(new Book("小李飞刀", "古龙", 5.1));
        col.add(new Book("红楼梦", "曹雪芹", 34.6));
        //System.out.println("col=" + col);
        //现在老师希望能够遍历 col集合
        //1. 先得到 col 对应的 迭代器
        Iterator iterator = col.iterator();
        //2. 使用while循环遍历
//        while (iterator.hasNext()) {//判断是否还有数据
//            //返回下一个元素，类型是Object
//            Object obj = iterator.next();
//            System.out.println("obj=" + obj);
//        }
        //老师教大家一个快捷键，快速生成 while => itit
        //显示所有的快捷键的的快捷键 ctrl + j
        //即Ctrl +J  显示  所有 liveTemplate快捷输入列表
        while (iterator.hasNext()) {
            Object obj = iterator.next();
            System.out.println("obj=" + obj);
        }
        //3. 当退出while循环后 , 这时iterator迭代器，指向最后的元素
        //   iterator.next();//NoSuchElementException
        //4. 如果希望再次遍历，需要重置我们的迭代器
        iterator = col.iterator();
        System.out.println("===第二次遍历===");
        while (iterator.hasNext()) {
            Object obj = iterator.next();
            System.out.println("obj=" + obj);
        }
    }
}
class Book {
    private String name;
    private String author;
    private double price;
    public Book(String name, String author, double price) {
        this.name = name;
        this.author = author;
        this.price = price;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public String getAuthor() {
        return author;
    }
    public void setAuthor(String author) {
        this.author = author;
    }
    public double getPrice() {
        return price;
    }
    public void setPrice(double price) {
        this.price = price;
    }
    @Override
    public String toString() {
        return "Book{" +
                " + name + '\'' +
                ", author='" + author + '\'' +
                ", price=" + price +
                '}';
    }
}
```

14.3.3 Collection 接口遍历对象方式 2-for 循环增强  
![](https://img-blog.csdnimg.cn/a5c39bfd9f8849c38991ae5aac05251d.png)

```
package com.hspedu.collection_;
import java.util.ArrayList;
import java.util.Collection;
public class CollectionFor {
    @SuppressWarnings({"all"})
    public static void main(String[] args) {
        Collection col = new ArrayList();
        col.add(new Book("三国演义", "罗贯中", 10.1));
        col.add(new Book("小李飞刀", "古龙", 5.1));
        col.add(new Book("红楼梦", "曹雪芹", 34.6));
        //老韩解读
        //1. 使用增强for, 在Collection集合
        //2. 增强for， 底层仍然是迭代器
        //3. 增强for可以理解成就是简化版本的 迭代器遍历
        //4. 快捷键方式 I
//        for (Object book : col) {
//            System.out.println("book=" + book);
//        }
        for (Object o : col) {
            System.out.println("book=" + o);
        }
        //增强for，也可以直接在数组使用
//        int[] nums = {1, 8, 10, 90};
//        for (int i : nums) {
//            System.out.println("i=" + i);
//        }
    }
}
```

> iter 和 col.for 都是生成增强 for 的快捷键

14.4 List 接口和常用方法

14.4.1 List 接口基本介绍  
![](https://img-blog.csdnimg.cn/6a7f8bc6448a4de68b5db0c9ad2b632f.png)  
14.4.2 List 接口的常用方法  
![](https://img-blog.csdnimg.cn/8d6577f814d449aca14ac353071ae36e.png)

```
package com.hspedu.list_;
import java.util.ArrayList;
import java.util.List;
public class ListMethod {
    @SuppressWarnings({"all"})
    public static void main(String[] args) {
        List list = new ArrayList();
        list.add("张三丰");
        list.add("贾宝玉");
//        void add(int index, Object ele):在index位置插入ele元素
        //在index = 1的位置插入一个对象
        list.add(1, "韩顺平");
        System.out.println("list=" + list);
//        boolean addAll(int index, Collection eles):从index位置开始将eles中的所有元素添加进来
        List list2 = new ArrayList();
        list2.add("jack");
        list2.add("tom");
        list.addAll(1, list2);
        System.out.println("list=" + list);
//        Object get(int index):获取指定index位置的元素
        //说过不再讲
//        int indexOf(Object obj):返回obj在集合中首次出现的位置
        System.out.println(list.indexOf("tom"));//2
//        int lastIndexOf(Object obj):返回obj在当前集合中末次出现的位置
        list.add("韩顺平");
        System.out.println("list=" + list);
        System.out.println(list.lastIndexOf("韩顺平"));
//        Object remove(int index):移除指定index位置的元素，并返回此元素
        list.remove(0);
        System.out.println("list=" + list);
//        Object set(int index, Object ele):设置指定index位置的元素为ele , 相当于是替换.
        list.set(1, "玛丽");
        System.out.println("list=" + list);
//        List subList(int fromIndex, int toIndex):返回从fromIndex到toIndex位置的子集合
        // 注意返回的子集合 fromIndex <= subList < toIndex
        List returnlist = list.subList(0, 2);
        System.out.println("returnlist=" + returnlist);
    }
}
```

subList 方法用的时候小心，对它返回的子集合操作或对原集合操作，两个集合会互相影响，还容易出异常，谨慎使用。

14.4.4 List 的三种遍历方式 [ArrayList, LinkedList,Vector]  
![](https://img-blog.csdnimg.cn/cddad2948d2c445fae8d26bb4cdcc803.png)  
14.5 ArrayList 底层结构和源码分析

14.5.1 ArrayList 的注意事项  
![](https://img-blog.csdnimg.cn/4e11ccf69fca459999ebf2b383891c3a.png)  
14.5.2 ArrayList 的底层操作机制源码分析 (重点，难点.)  
![](https://img-blog.csdnimg.cn/63c58f0731154266af967f1914a4d595.png)

```
package com.hspedu.list_;
import java.util.ArrayList;
@SuppressWarnings({"all"})
public class ArrayListSource {
    public static void main(String[] args) {
        //老韩解读源码
        //注意，注意，注意，Idea 默认情况下，Debug 显示的数据是简化后的，如果希望看到完整的数据
        //需要做设置.
        //使用无参构造器创建ArrayList对象
        //ArrayList list = new ArrayList();
        ArrayList list = new ArrayList(8);
        //使用for给list集合添加 1-10数据
        for (int i = 1; i <= 10; i++) {
            list.add(i);
        }
        //使用for给list集合添加 11-15数据
        for (int i = 11; i <= 15; i++) {
            list.add(i);
        }
        list.add(100);
        list.add(200);
        list.add(null);
    }
}
```

![](https://img-blog.csdnimg.cn/da701867a4b74f098697673fc2202e80.png)  
![](https://img-blog.csdnimg.cn/58c9ba09587b4a65a01c772d6c56cad7.png)  
Idea 默认情况下，Debug 显示的数据是简化后的，如果希望看到完整的数据需要做设置：  
![](https://img-blog.csdnimg.cn/73032cbe65744dd1b3794c3d309204ea.png)  
debug 进不去源码的话把 Debugger 下的 Stepping 中的 Do not step into the classes 选项的对钩去掉。

14.6 Vector 底层结构和源码剖析

14.6.1 Vector 的基本介绍  
![](https://img-blog.csdnimg.cn/57089a1713f745ea8235a48992ab587e.png)  
14.6.2 Vector 和 ArrayList 的比较

```
package com.hspedu.list_;
import java.util.Vector;
@SuppressWarnings({"all"})
public class Vector_ {
    public static void main(String[] args) {
        //无参构造器
        //有参数的构造
        Vector vector = new Vector(8);
        for (int i = 0; i < 10; i++) {
            vector.add(i);
        }
        vector.add(100);
        System.out.println("vector=" + vector);
        //老韩解读源码
        //1. new Vector() 底层
        /*
            public Vector() {
                this(10);
            }
         补充：如果是  Vector vector = new Vector(8);
            走的方法:
            public Vector(int initialCapacity) {
                this(initialCapacity, 0);
            }
         2. vector.add(i)
         2.1  //下面这个方法就添加数据到vector集合
            public synchronized boolean add(E e) {
                modCount++;
                ensureCapacityHelper(elementCount + 1);
                elementData[elementCount++] = e;
                return true;
            }
          2.2  //确定是否需要扩容 条件 ： minCapacity - elementData.length>0
            private void ensureCapacityHelper(int minCapacity) {
                // overflow-conscious code
                if (minCapacity - elementData.length > 0)
                    grow(minCapacity);
            }
          2.3 //如果 需要的数组大小 不够用，就扩容 , 扩容的算法
              //newCapacity = oldCapacity + ((capacityIncrement > 0) ?
              //                             capacityIncrement : oldCapacity);
              //就是扩容两倍.
            private void grow(int minCapacity) {
                // overflow-conscious code
                int oldCapacity = elementData.length;
                int newCapacity = oldCapacity + ((capacityIncrement > 0) ?
                                                 capacityIncrement : oldCapacity);
                if (newCapacity - minCapacity < 0)
                    newCapacity = minCapacity;
                if (newCapacity - MAX_ARRAY_SIZE > 0)
                    newCapacity = hugeCapacity(minCapacity);
                elementData = Arrays.copyOf(elementData, newCapacity);
            }
         */
    }
}
```

![](https://img-blog.csdnimg.cn/6974802a47d7445ab478d144a1878b2b.png)  
14.7 LinkedList 底层结构

14.7.1 LinkedList 的全面说明  
![](https://img-blog.csdnimg.cn/93107d55cb1c4f9b99cc328921bce606.png)  
14.7.2 LinkedList 的底层操作机制  
![](https://img-blog.csdnimg.cn/d8338018fb21462d980591522aa1c0be.png)  
14.7.3 LinkedList 的增删改查案例

```
package com.hspedu.list_;
import java.util.Iterator;
import java.util.LinkedList;
@SuppressWarnings({"all"})
public class LinkedListCRUD {
    public static void main(String[] args) {
        LinkedList linkedList = new LinkedList();
        linkedList.add(1);
        linkedList.add(2);
        linkedList.add(3);
        System.out.println("linkedList=" + linkedList);

        //演示一个删除结点的
        linkedList.remove(); // 这里默认删除的是第一个结点
        //linkedList.remove(2);
        System.out.println("linkedList=" + linkedList);

        //修改某个结点对象
        linkedList.set(1, 999);
        System.out.println("linkedList=" + linkedList);

        //得到某个结点对象
        //get(1) 是得到双向链表的第二个对象
        Object o = linkedList.get(1);
        System.out.println(o);//999

        //因为LinkedList 是 实现了List接口, 遍历方式
        System.out.println("===LinkeList遍历迭代器====");
        Iterator iterator = linkedList.iterator();
        while (iterator.hasNext()) {
            Object next =  iterator.next();
            System.out.println("next=" + next);
        }
        System.out.println("===LinkeList遍历增强for====");
        for (Object o1 : linkedList) {
            System.out.println("o1=" + o1);
        }
        System.out.println("===LinkeList遍历普通for====");
        for (int i = 0; i < linkedList.size(); i++) {
            System.out.println(linkedList.get(i));
        }
        //老韩源码阅读.
        /* 1. LinkedList linkedList = new LinkedList();
              public LinkedList() {}
           2. 这时 linkeList 的属性 first = null  last = null
           3. 执行 添加
               public boolean add(E e) {
                    linkLast(e);
                    return true;
                }
            4.将新的结点，加入到双向链表的最后
             void linkLast(E e) {
                final Node<E> l = last;
                final Node<E> newNode = new Node<>(l, e, null);
                last = newNode;
                if (l == null)
                    first = newNode;
                else
                    l.next = newNode;
                size++;
                modCount++;
            }
         */
        /*
          老韩读源码 linkedList.remove(); // 这里默认删除的是第一个结点
          1. 执行 removeFirst
            public E remove() {
                return removeFirst();
            }
         2. 执行
            public E removeFirst() {
                final Node<E> f = first;
                if (f == null)
                    throw new NoSuchElementException();
                return unlinkFirst(f);
            }
          3. 执行 unlinkFirst, 将 f 指向的双向链表的第一个结点拿掉
            private E unlinkFirst(Node<E> f) {
                // assert f == first && f != null;
                final E element = f.item;
                final Node<E> next = f.next;
                f.item = null;
                f.next = null; // help GC
                first = next;
                if (next == null)
                    last = null;
                else
                    next.prev = null;
                size--;
                modCount++;
                return element;
            }
         */
    }
}
```

![](https://img-blog.csdnimg.cn/ecdc4508d93344a58f30d13d8075ca62.png)  
左边为 remove 操作，右边为 add 操作。

14.8 ArrayList 和 LinkedList 比较  
![](https://img-blog.csdnimg.cn/1056c70af6e84242b74b95996e010df0.png)  
14.9 Set 接口和常用方法

14.9.1 Set 接口基本介绍  
![](https://img-blog.csdnimg.cn/6b10be4f3bfe475ea04ed7892954311b.png)  
因为是无序的所以不能重复也无索引。

14.9.2 Set 接口的常用方法和遍历方式  
![](https://img-blog.csdnimg.cn/66d7e45451144f3aae39a61969970204.png)  
14.9.4 Set 接口的常用方法举例  
![](https://img-blog.csdnimg.cn/abc58366a66f43228a35f609f8eb31bd.png)

```
package com.hspedu.set_;
import java.util.HashSet;
import java.util.Iterator;
import java.util.Set;
@SuppressWarnings({"all"})
public class SetMethod {
    public static void main(String[] args) {
        //老韩解读
        //1. 以Set 接口的实现类 HashSet 来讲解Set 接口的方法
        //2. set 接口的实现类的对象(Set接口对象，即实现了Set接口的类的对象), 不能存放重复的元素, 可以添加一个null
        //3. set 接口对象存放数据是无序(即添加的顺序和取出的顺序不一致)
        //4. 注意：取出的顺序的顺序虽然不是添加的顺序，但它也是固定的顺序.
        Set set = new HashSet();
        set.add("john");
        set.add("lucy");
        set.add("john");//重复
        set.add("jack");
        set.add("hsp");
        set.add("mary");
        set.add(null);//
        set.add(null);//再次添加null
        for(int i = 0; i <10;i ++) {
            System.out.println("set=" + set);
        }
        //遍历
        //方式1： 使用迭代器
        System.out.println("=====使用迭代器====");
        Iterator iterator = set.iterator();
        while (iterator.hasNext()) {
            Object obj =  iterator.next();
            System.out.println("obj=" + obj);
        }
        set.remove(null);
        //方式2: 增强for
        System.out.println("=====增强for====");
        for (Object o : set) {
            System.out.println("o=" + o);
        }
        //set 接口对象，不能通过索引来获取
    }
}
```

14.10 Set 接口实现类 - HashSet

14.10.1 HashSet 的全面说明  
![](https://img-blog.csdnimg.cn/9d12afbe530b49a6a5efa36291e0810d.png)  
14.10.2 HashSet 案例说明  
![](https://img-blog.csdnimg.cn/9c74494da1e4454e985c1ffea7767bc9.png)

```
package com.hspedu.set_;
import java.util.HashSet;
@SuppressWarnings({"all"})
public class HashSet01 {
    public static void main(String[] args) {
        HashSet set = new HashSet();
        //说明
        //1. 在执行add方法后，会返回一个boolean值
        //2. 如果添加成功，返回 true, 否则返回false
        //3. 可以通过 remove 指定删除哪个对象
        System.out.println(set.add("john"));//T
        System.out.println(set.add("lucy"));//T
        System.out.println(set.add("john"));//F
        System.out.println(set.add("jack"));//T
        System.out.println(set.add("Rose"));//T

        set.remove("john");
        System.out.println("set=" + set);//3个
        
        set  = new HashSet();
        System.out.println("set=" + set);//0
        //4 Hashset 不能添加相同的元素/数据?
        set.add("lucy");//添加成功
        set.add("lucy");//加入不了
        set.add(new Dog("tom"));//OK
        set.add(new Dog("tom"));//Ok
        System.out.println("set=" + set);

        //再加深一下. 非常经典的面试题.
        //看源码，做分析， 先给小伙伴留一个坑，以后讲完源码，你就了然
        //去看他的源码，即 add 到底发生了什么?=> 底层机制.
        set.add(new String("hsp"));//ok
        set.add(new String("hsp"));//加入不了.即不会有两个hsp
        System.out.println("set=" + set);
    }
}
class Dog { //定义了Dog类
    private String name;
    public Dog(String name) {
        this.name = name;
    }
    @Override
    public String toString() {
        return "Dog{" +
                " + name + '\'' +
                '}';
    }
}
```

输出：  
![](https://img-blog.csdnimg.cn/207206a8f2c44b1187f217a19250635b.png)  
14.10.3 HashSet 底层机制说明  
![](https://img-blog.csdnimg.cn/a501432cd93147148dfe3b29d6c3a274.png)  
![](https://img-blog.csdnimg.cn/870c485612584207b047957ba3276262.png)

```
package com.hspedu.set_;
import java.util.HashSet;
@SuppressWarnings({"all"})
public class HashSetSource {
    public static void main(String[] args) {
        HashSet hashSet = new HashSet();
        hashSet.add("java");//到此位置，第1次add分析完毕.
        hashSet.add("php");//到此位置，第2次add分析完毕
        hashSet.add("java");
        System.out.println("set=" + hashSet);
        /*
        老韩对HashSet 的源码解读
        1. 执行 HashSet()
            public HashSet() {
                map = new HashMap<>();
            }
        2. 执行 add()
           public boolean add(E e) {//e = "java"
                return map.put(e, PRESENT)==null;//(static) PRESENT = new Object();
           }
         3.执行 put() , 该方法会执行 hash(key) 得到key对应的hash值 算法h = key.hashCode()) ^ (h >>> 16)
             public V put(K key, V value) {//key = "java" value = PRESENT 共享
                return putVal(hash(key), key, value, false, true);
            }
         4.执行 putVal
         final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
                   boolean evict) {
                Node<K,V>[] tab; Node<K,V> p; int n, i; //定义了辅助变量
                //table 就是 HashMap 的一个数组，类型是 Node[]
                //if 语句表示如果当前table 是null, 或者 大小=0
                //就是第一次扩容，到16个空间.
                if ((tab = table) == null || (n = tab.length) == 0)
                    n = (tab = resize()).length;

                //(1)根据key，得到hash 去计算该key应该存放到table表的哪个索引位置
                //并把这个位置的对象，赋给 p
                //(2)判断p 是否为null
                //(2.1) 如果p 为null, 表示还没有存放元素, 就创建一个Node (key="java",value=PRESENT)
                //(2.2) 就放在该位置 tab[i] = newNode(hash, key, value, null)

                if ((p = tab[i = (n - 1) & hash]) == null)
                    tab[i] = newNode(hash, key, value, null);
                else {
                    //一个开发技巧提示： 在需要局部变量(辅助变量)时候，在创建
                    Node<K,V> e; K k; //
                    //如果当前索引位置对应的链表的第一个元素和准备添加的key的hash值一样
                    //并且满足 下面两个条件之一:
                    //(1) 准备加入的key 和 p 指向的Node 结点的 key 是同一个对象
                    //(2)  p 指向的Node 结点的 key 的equals() 和准备加入的key比较后相同
                    //就不能加入
                    if (p.hash == hash &&
                        ((k = p.key) == key || (key != null && key.equals(k))))
                        e = p;
                    //再判断 p 是不是一颗红黑树,
                    //如果是一颗红黑树，就调用 putTreeVal , 来进行添加
                    else if (p instanceof TreeNode)
                        e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
                    else {//如果table对应索引位置，已经是一个链表, 就使用for循环比较
                          //(1) 依次和该链表的每一个元素比较后，都不相同, 则加入到该链表的最后
                          //    注意在把元素添加到链表后，立即判断 该链表是否已经达到8个结点
                          //    , 就调用 treeifyBin() 对当前这个链表进行树化(转成红黑树)
                          //    注意，在转成红黑树时，要进行判断, 判断条件
                          //    if (tab == null || (n = tab.length) < MIN_TREEIFY_CAPACITY(64))
                          //            resize();
                          //    如果上面条件成立，先table扩容.
                          //    只有上面条件不成立时，才进行转成红黑树
                          //(2) 依次和该链表的每一个元素比较过程中，如果有相同情况,就直接break

                        for (int binCount = 0; ; ++binCount) {
                            if ((e = p.next) == null) {
                                p.next = newNode(hash, key, value, null);
                                if (binCount >= TREEIFY_THRESHOLD(8) - 1) // -1 for 1st
                                    treeifyBin(tab, hash);
                                break;
                            }
                            if (e.hash == hash &&
                                ((k = e.key) == key || (key != null && key.equals(k))))
                                break;
                            p = e;
                        }
                    }
                    if (e != null) { // existing mapping for key
                        V oldValue = e.value;
                        if (!onlyIfAbsent || oldValue == null)
                            e.value = value;
                        afterNodeAccess(e);
                        return oldValue;
                    }
                }
                ++modCount;
                //size 就是我们每加入一个结点Node(k,v,h,next), size++
                if (++size > threshold)
                    resize();//扩容
                afterNodeInsertion(evict);
                return null;
            }
         */
    }
}
```

![](https://img-blog.csdnimg.cn/6294799ac3204adabb525a07f855d5fd.png)  
扩容分两种情况，第一种情况是在长度大于等于 8 的链表后面加结点，如果数组大小没到 64，则继续扩容，并且将此结点添加到链表尾（单条链表没有数量限制，别认为 hashset 一条链表限制 8 个元素）；第二种情况是看临界值扩容，当我们向 hashset 增加一个元素，-> Node -> 加入 table , 就算是增加了一个 size++，当到了临界值 12，再添加一个元素到 13 的时候，就会触发扩容机制，而不是看 table 数组有没有用了 12 个不同的索引。

14.10.4 HashSet 课堂练习 1  
![](https://img-blog.csdnimg.cn/64d63aa3e74b40c4b2a4d57c68bc154e.png)

```
package com.hspedu.set_;
import java.util.HashSet;
import java.util.LinkedHashSet;
import java.util.Objects;
import java.util.Set;
@SuppressWarnings({"all"})
public class HashSetExercise {
    public static void main(String[] args) {
        HashSet hashSet = new HashSet();
        hashSet.add(new Employee("milan", 18));//ok
        hashSet.add(new Employee("smith", 28));//ok
        hashSet.add(new Employee("milan", 18));//加入不成功.
        //回答,加入了几个? 3个
        System.out.println("hashSet=" + hashSet);
    }
}
//创建Employee
class Employee {
    private String name;
    private int age;
    public Employee(String name, int age) {
        this.name = name;
        this.age = age;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public int getAge() {
        return age;
    }
    @Override
    public String toString() {
        return "Employee{" +
                " + name + '\'' +
                ", age=" + age +
                '}';
    }
    public void setAge(int age) {
        this.age = age;
    }
    //如果name 和 age 值相同，则返回相同的hash值
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Employee employee = (Employee) o;
        return age == employee.age &&
                Objects.equals(name, employee.name);
    }
    @Override
    public int hashCode() {
        return Objects.hash(name, age);
    }
}
```

14.11 Set 接口实现类 - LinkedHashSet

14.11.1 LinkedHashSet 的全面说明  
![](https://img-blog.csdnimg.cn/4d7b1cb042244958b8ed41441d4429b4.png)  
![](https://img-blog.csdnimg.cn/a88b9df5f17145d58de11f913d87ba23.png)

```
package com.hspedu.set_;
import java.util.LinkedHashSet;
import java.util.Set;
@SuppressWarnings({"all"})
public class LinkedHashSetSource {
    public static void main(String[] args) {
        //分析一下LinkedHashSet的底层机制
        Set set = new LinkedHashSet();
        set.add(new String("AA"));
        set.add(456);
        set.add(456);
        set.add(new Customer("刘", 1001));
        set.add(123);
        set.add("HSP");
        System.out.println("set=" + set);
        //老韩解读
        //1. LinkedHashSet 加入顺序和取出元素/数据的顺序一致
        //2. LinkedHashSet 底层维护的是一个LinkedHashMap(是HashMap的子类)
        //3. LinkedHashSet 底层结构 (数组table+双向链表)
        //4. 添加第一次时，直接将 数组table 扩容到 16 ,存放的结点类型是 LinkedHashMap$Entry
        //5. 数组是 HashMap$Node[] 存放的元素/数据是 LinkedHashMap$Entry类型
        /*
                //继承关系是在内部类完成.
                static class Entry<K,V> extends HashMap.Node<K,V> {
                    Entry<K,V> before, after;
                    Entry(int hash, K key, V value, Node<K,V> next) {
                        super(hash, key, value, next);
                    }
                }
         */
    }
}
class Customer {
    private String name;
    private int no;
    public Customer(String name, int no) {
        this.name = name;
        this.no = no;
    }
}
```

14.12 Map 接口和常用方法

14.12.1 Map 接口实现类的特点 [很实用]  
![](https://img-blog.csdnimg.cn/6110ccaac67f4a5b853b216c0e1eab30.png)

```
package com.hspedu.map_;
import java.util.HashMap;
import java.util.Map;
@SuppressWarnings({"all"})
public class Map_ {
    public static void main(String[] args) {
        //老韩解读Map 接口实现类的特点, 使用实现类HashMap
        //1. Map与Collection并列存在。用于保存具有映射关系的数据:Key-Value(双列元素)
        //2. Map 中的 key 和  value 可以是任何引用类型的数据，会封装到HashMap$Node 对象中
        //3. Map 中的 key 不允许重复，原因和HashSet 一样，前面分析过源码.
        //4. Map 中的 value 可以重复
        //5. Map 的key 可以为 null, value 也可以为null ，注意 key 为null,
        //   只能有一个，value 为null ,可以多个
        //6. 常用String类作为Map的 key
        //7. key 和 value 之间存在单向一对一关系，即通过指定的 key 总能找到对应的 value
        Map map = new HashMap();
        map.put("no1", "韩顺平");//k-v
        map.put("no2", "张无忌");//k-v
        map.put("no1", "张三丰");//当有相同的k , 就等价于替换.
        map.put("no3", "张三丰");//k-v
        map.put(null, null); //k-v
        map.put(null, "abc"); //等价替换
        map.put("no4", null); //k-v
        map.put("no5", null); //k-v
        map.put(1, "赵敏");//k-v
        map.put(new Object(), "金毛狮王");//k-v
        // 通过get 方法，传入 key ,会返回对应的value
        System.out.println(map.get("no2"));//张无忌
        System.out.println("map=" + map);
    }
}
```

![](https://img-blog.csdnimg.cn/86c251694cac439e9a7275a86d0ba5db.png)

```
package com.hspedu.map_;
import java.util.Collection;
import java.util.HashMap;
import java.util.Map;
import java.util.Set;
@SuppressWarnings({"all"})
public class MapSource_ {
    public static void main(String[] args) {
        Map map = new HashMap();
        map.put("no1", "韩顺平");//k-v
        map.put("no2", "张无忌");//k-v
        map.put(new Car(), new Person());//k-v
        //老韩解读
        //1. k-v 最后是 HashMap$Node node = newNode(hash, key, value, null)
        //2. k-v 为了方便程序员的遍历，还会 创建 EntrySet 集合 ，该集合存放的元素的类型 Entry, 而一个Entry
        //   对象就有k,v EntrySet<Entry<K,V>> 即： transient Set<Map.Entry<K,V>> entrySet;
        //3. entrySet 中， 定义的类型是 Map.Entry ，但是实际上存放的还是 HashMap$Node
        //   这时因为 static class Node<K,V> implements Map.Entry<K,V>
        //4. 当把 HashMap$Node 对象 存放到 entrySet 就方便我们的遍历, 因为 Map.Entry 提供了重要方法
        //   K getKey(); V getValue();
        
        Set set = map.entrySet();
        System.out.println(set.getClass());// HashMap$EntrySet
        for (Object obj : set) {
            //System.out.println(obj.getClass()); //HashMap$Node
            //为了从 HashMap$Node 取出k-v
            //1. 先做一个向下转型
            Map.Entry entry = (Map.Entry) obj;
            System.out.println(entry.getKey() + "-" + entry.getValue() );
        }
        Set set1 = map.keySet();
        System.out.println(set1.getClass());//class java.util.HashMap$KeySet
        Collection values = map.values();
        System.out.println(values.getClass());//class java.util.HashMap$Values
    }
}
class Car {}
class Person{}
```

输出：

```
class java.util.HashMap$EntrySet
no2-张无忌
no1-韩顺平
Car@2f4d3709-Person@b1bc7ed
class java.util.HashMap$KeySet
class java.util.HashMap$Values
```

14.12.2 Map 接口常用方法  
![](https://img-blog.csdnimg.cn/948c03e8cf4f492181e627f1e99633b3.png)

```
package com.hspedu.map_;
import java.util.HashMap;
import java.util.Map;
@SuppressWarnings({"all"})
public class MapMethod {
    public static void main(String[] args) {
        //演示map接口常用方法
        Map map = new HashMap();
        map.put("邓超", new Book("", 100));//OK
        map.put("邓超", "孙俪");//替换-> 一会分析源码
        map.put("王宝强", "马蓉");//OK
        map.put("宋喆", "马蓉");//OK
        map.put("刘令博", null);//OK
        map.put(null, "刘亦菲");//OK
        map.put("鹿晗", "关晓彤");//OK
        map.put("hsp", "hsp的老婆");
        System.out.println("map=" + map);

//        remove:根据键删除映射关系
        map.remove(null);
        System.out.println("map=" + map);
//        get：根据键获取值
        Object val = map.get("鹿晗");
        System.out.println("val=" + val);
//        size:获取元素个数
        System.out.println("k-v=" + map.size());
//        isEmpty:判断个数是否为0
        System.out.println(map.isEmpty());//F
//        clear:清除k-v
        //map.clear();
        System.out.println("map=" + map);
//        containsKey:查找键是否存在
        System.out.println("结果=" + map.containsKey("hsp"));//T
    }
}
class Book {
    private String name;
    private int num;
    public Book(String name, int num) {
        this.name = name;
        this.num = num;
    }
}
```

14.12.3 Map 接口遍历方法  
![](https://img-blog.csdnimg.cn/016beb67b2f540949361ac8ed84c455d.png)

```
package com.hspedu.map_;
import java.util.*;
@SuppressWarnings({"all"})
public class MapFor {
    public static void main(String[] args) {
        Map map = new HashMap();
        map.put("邓超", "孙俪");
        map.put("王宝强", "马蓉");
        map.put("宋喆", "马蓉");
        map.put("刘令博", null);
        map.put(null, "刘亦菲");
        map.put("鹿晗", "关晓彤");
        //第一组: 先取出 所有的Key , 通过Key 取出对应的Value
        Set keyset = map.keySet();
        //(1) 增强for
        System.out.println("-----第一种方式-------");
        for (Object key : keyset) {
            System.out.println(key + "-" + map.get(key));
        }
        //(2) 迭代器
        System.out.println("----第二种方式--------");
        Iterator iterator = keyset.iterator();
        while (iterator.hasNext()) {
            Object key =  iterator.next();
            System.out.println(key + "-" + map.get(key));
        }

        //第二组: 把所有的values取出
        Collection values = map.values();
        //这里可以使用所有的Collections使用的遍历方法
        //(1) 增强for
        System.out.println("---取出所有的value 增强for----");
        for (Object value : values) {
            System.out.println(value);
        }
        //(2) 迭代器
        System.out.println("---取出所有的value 迭代器----");
        Iterator iterator2 = values.iterator();
        while (iterator2.hasNext()) {
            Object value =  iterator2.next();
            System.out.println(value);
        }

        //第三组: 通过EntrySet 来获取 k-v
        Set entrySet = map.entrySet();// EntrySet<Map.Entry<K,V>>
        //(1) 增强for
        System.out.println("----使用EntrySet 的 for增强(第3种)----");
        for (Object entry : entrySet) {
            //将entry 转成 Map.Entry
            Map.Entry m = (Map.Entry) entry;
            System.out.println(m.getKey() + "-" + m.getValue());
        }
        //(2) 迭代器
        System.out.println("----使用EntrySet 的 迭代器(第4种)----");
        Iterator iterator3 = entrySet.iterator();
        while (iterator3.hasNext()) {
            Object entry =  iterator3.next();
            //System.out.println(next.getClass());//HashMap$Node -实现-> Map.Entry (getKey,getValue)
            //向下转型 Map.Entry
            Map.Entry m = (Map.Entry) entry;
            System.out.println(m.getKey() + "-" + m.getValue());
        }
    }
}
```

14.12.4 Map 接口课堂练习  
![](https://img-blog.csdnimg.cn/be3c49abe22646298405ce11312de495.png)

```
package com.hspedu.map_;
import java.util.HashMap;
import java.util.Iterator;
import java.util.Map;
import java.util.Set;
@SuppressWarnings({"all"})
public class MapExercise {
    public static void main(String[] args) {
        //完成代码
        Map hashMap = new HashMap();
        //添加对象
        hashMap.put(1, new Emp("jack", 300000, 1));
        hashMap.put(2, new Emp("tom", 21000, 2));
        hashMap.put(3, new Emp("milan", 12000, 3));

        //遍历2种方式
        //并遍历显示工资>18000的员工(遍历方式最少两种)
        //1. 使用keySet  -> 增强for
        Set keySet = hashMap.keySet();
        System.out.println("====第一种遍历方式====");
        for (Object key : keySet) {
            //先获取value
            Emp emp = (Emp) hashMap.get(key);
            if(emp.getSal() >18000) {
                System.out.println(emp);
            }
        }
        //2. 使用EntrySet -> 迭代器
        //   体现比较难的知识点
        //   慢慢品，越品越有味道.
        Set entrySet = hashMap.entrySet();
        System.out.println("======迭代器======");
        Iterator iterator = entrySet.iterator();
        while (iterator.hasNext()) {
            Map.Entry entry =  (Map.Entry)iterator.next();
            System.out.println(entry.getClass());//class java.util.HashMap$Node 仔细想想这里为什么是HashMap$Node
            //通过entry 取得key 和 value
            Emp emp = (Emp) entry.getValue();
            if(emp.getSal() > 18000) {
                System.out.println(emp);
            }
        }
    }
}
class Emp {
    private String name;
    private double sal;
    private int id;
    public Emp(String name, double sal, int id) {
        this.name = name;
        this.sal = sal;
        this.id = id;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public double getSal() {
        return sal;
    }
    public void setSal(double sal) {
        this.sal = sal;
    }
    public int getId() {
        return id;
    }
    public void setId(int id) {
        this.id = id;
    }
    @Override
    public String toString() {
        return "Emp{" +
                " + name + '\'' +
                ", sal=" + sal +
                ", id=" + id +
                '}';
    }
}
```

14.13 Map 接口实现类 - HashMap

14.13.1 HashMap 小结  
![](https://img-blog.csdnimg.cn/7e1322eadc1a484fb4a8a9b6197bd4af.png)  
14.13.2 HashMap 底层机制及源码剖析  
![](https://img-blog.csdnimg.cn/a5de1667b4094be4bd080d445252af46.png)  
![](https://img-blog.csdnimg.cn/7a1a278723c34547b40168e45affeb09.png)

```
package com.hspedu.map_;
import java.util.HashMap;
@SuppressWarnings({"all"})
public class HashMapSource1 {
    public static void main(String[] args) {
        HashMap map = new HashMap();
        map.put("java", 10);//ok
        map.put("php", 10);//ok
        map.put("java", 20);//替换value
        System.out.println("map=" + map);//

        /*老韩解读HashMap的源码+图解
        1. 执行构造器 new HashMap()
           初始化加载因子 loadfactor = 0.75
           HashMap$Node[] table = null
        2. 执行put 调用 hash方法，计算 key的 hash值 (h = key.hashCode()) ^ (h >>> 16)
            public V put(K key, V value) {//K = "java" value = 10
                return putVal(hash(key), key, value, false, true);
            }
         3. 执行 putVal
         final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
                   boolean evict) {
                Node<K,V>[] tab; Node<K,V> p; int n, i;//辅助变量
                //如果底层的table 数组为null, 或者 length =0 , 就扩容到16
                if ((tab = table) == null || (n = tab.length) == 0)
                    n = (tab = resize()).length;
                //取出hash值对应的table的索引位置的Node, 如果为null, 就直接把加入的k-v
                //, 创建成一个 Node ,加入该位置即可
                if ((p = tab[i = (n - 1) & hash]) == null)
                    tab[i] = newNode(hash, key, value, null);
                else {
                    Node<K,V> e; K k;//辅助变量
                // 如果table的索引位置的key的hash相同和新的key的hash值相同，
                 // 并 满足(table现有的结点的key和准备添加的key是同一个对象  || equals返回真)
                 // 就认为不能加入新的k-v
                    if (p.hash == hash &&
                        ((k = p.key) == key || (key != null && key.equals(k))))
                        e = p;
                    else if (p instanceof TreeNode)//如果当前的table的已有的Node 是红黑树，就按照红黑树的方式处理
                        e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
                    else {
                        //如果找到的结点，后面是链表，就循环比较
                        for (int binCount = 0; ; ++binCount) {//死循环
                            if ((e = p.next) == null) {//如果整个链表，没有和他相同,就加到该链表的最后
                                p.next = newNode(hash, key, value, null);
                                //加入后，判断当前链表的个数，是否已经到8个，到8个，后
                                //就调用 treeifyBin 方法进行红黑树的转换
                                if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
                                    treeifyBin(tab, hash);
                                break;
                            }
                            if (e.hash == hash && //如果在循环比较过程中，发现有相同,就break,就只是替换value
                                ((k = e.key) == key || (key != null && key.equals(k))))
                                break;
                            p = e;
                        }
                    }
                    if (e != null) { // existing mapping for key
                        V oldValue = e.value;
                        if (!onlyIfAbsent || oldValue == null)
                            e.value = value; //替换，key对应value
                        afterNodeAccess(e);
                        return oldValue;
                    }
                }
                ++modCount;//每增加一个Node ,就size++
                if (++size > threshold[12-24-48])//如size > 临界值，就扩容
                    resize();
                afterNodeInsertion(evict);
                return null;
            }
              5. 关于树化(转成红黑树)
              //如果table 为null ,或者大小还没有到 64，暂时不树化，而是进行扩容.
              //否则才会真正的树化 -> 剪枝
              final void treeifyBin(Node<K,V>[] tab, int hash) {
                int n, index; Node<K,V> e;
                if (tab == null || (n = tab.length) < MIN_TREEIFY_CAPACITY)
                    resize();
            }
         */
    }
}
```

14.14 Map 接口实现类 - Hashtable

14.14.1 HashTable 的基本介绍  
![](https://img-blog.csdnimg.cn/c2c60b6e133740a1872ddb35961770d8.png)  
![](https://img-blog.csdnimg.cn/af684d71a86c42d5b96ab10d44d21d78.png)  
14.14.2 Hashtable 和 HashMap 对比  
![](https://img-blog.csdnimg.cn/24d71674083545d79efe21157d3902a1.png)  
14.15 Map 接口实现类 - Properties

14.15.1 基本介绍  
![](https://img-blog.csdnimg.cn/687f22d2ac594fd3a76de3432487bd3e.png)  
14.15.2 基本使用

```
package com.hspedu.map_;
import java.util.Properties;
@SuppressWarnings({"all"})
public class Properties_ {
    public static void main(String[] args) {
        //老韩解读
        //1. Properties 继承  Hashtable
        //2. 可以通过 k-v 存放数据，当然key 和 value 不能为 null
        //增加
        Properties properties = new Properties();
        //properties.put(null, "abc");//抛出 空指针异常
        //properties.put("abc", null); //抛出 空指针异常
        properties.put("john", 100);//k-v
        properties.put("lucy", 100);
        properties.put("lic", 100);
        properties.put("lic", 88);//如果有相同的key ， value被替换
        System.out.println("properties=" + properties);
        
        //删除
        properties.remove("lic");
        System.out.println("properties=" + properties);

        //修改
        properties.put("john", "约翰");
        System.out.println("properties=" + properties);

		//查找，通过k 获取对应值
        System.out.println(properties.get("lic"));//88
        System.out.println(properties.getProperty("lic"));//注意，getProperty如果value类型不为 String，则返回 null
    }
}
```

14.16 总结 - 开发中如何选择集合实现类 (记住)  
![](https://img-blog.csdnimg.cn/839b8e61efc344cbb581d9a043d8f839.png)  
LinkedHashSet 的底层是 LinkedHashMap，LinkedHashMap 的底层是 HashMap。

14.17 TreeSet 源码解读

```
package com.hspedu.set_;
import java.util.Comparator;
import java.util.TreeSet;
@SuppressWarnings({"all"})
public class TreeSet_ {
    public static void main(String[] args) {
        //老韩解读
        //1. 当我们使用无参构造器，创建TreeSet时，默认按照字母升序排序
        //2. 老师希望添加的元素，按照字符串大小来排序
        //3. 使用TreeSet 提供的一个构造器，可以传入一个比较器(匿名内部类)
        //   并指定排序规则
        //4. 简单看看源码
        //老韩解读
        /*
        1. 构造器把传入的比较器对象，赋给了 TreeSet的底层的 TreeMap的属性this.comparator
         public TreeMap(Comparator<? super K> comparator) {
                this.comparator = comparator;
            }
         2. 在 调用 treeSet.add("tom"), 在底层会执行到
             if (cpr != null) {//cpr 就是我们的匿名内部类(对象)
                do {
                    parent = t;
                    //动态绑定到我们的匿名内部类(对象)compare
                    cmp = cpr.compare(key, t.key);
                    if (cmp < 0)
                        t = t.left;
                    else if (cmp > 0)
                        t = t.right;
                    else //如果相等，即返回0,这个Key就没有加入，即不会替换key的值
                        return t.setValue(value);
                } while (t != null);
            }
         */
//        TreeSet treeSet = new TreeSet();
        TreeSet treeSet = new TreeSet(new Comparator() {
            @Override
            public int compare(Object o1, Object o2) {
                //下面 调用String的 compareTo方法进行字符串大小比较
                //如果老韩要求加入的元素，按照长度大小排序
                //return ((String) o2).compareTo((String) o1);
                return ((String) o1).length() - ((String) o2).length();
            }
        });
        //添加数据.
        treeSet.add("jack");
        treeSet.add("tom");//3
        treeSet.add("sp");
        treeSet.add("a");
        treeSet.add("abc");//3
        System.out.println("treeSet=" + treeSet);
    }
}
```

TreeSet 和 TreeMap 在自身没有比较器的时候只能存实现了 Comparable 接口 的类对象

14.18 TreeMap 源码解读

```
package com.hspedu.map_;
import java.util.Comparator;
import java.util.TreeMap;
@SuppressWarnings({"all"})
public class TreeMap_ {
    public static void main(String[] args) {
        //使用默认的构造器，创建TreeMap, 是无序的(也没有排序)
        /*
            老韩要求：按照传入的 k(String) 的大小进行排序
         */
//        TreeMap treeMap = new TreeMap();
        TreeMap treeMap = new TreeMap(new Comparator() {
            @Override
            public int compare(Object o1, Object o2) {
                //按照传入的 k(String) 的大小进行排序
                //按照K(String) 的长度大小排序
                //return ((String) o2).compareTo((String) o1);
                return ((String) o2).length() - ((String) o1).length();
            }
        });
        treeMap.put("jack", "杰克");
        treeMap.put("tom", "汤姆");
        treeMap.put("kristina", "克瑞斯提诺");
        treeMap.put("smith", "斯密斯");
        treeMap.put("hsp", "韩顺平");//加入不了
        System.out.println("treemap=" + treeMap);
        /*
            老韩解读源码：
            1. 构造器. 把传入的实现了 Comparator接口的匿名内部类(对象)，传给给TreeMap的comparator
             public TreeMap(Comparator<? super K> comparator) {
                this.comparator = comparator;
            }
            2. 调用put方法
            2.1 第一次添加, 把k-v 封装到 Entry对象，放入root
            Entry<K,V> t = root;
            if (t == null) {
                compare(key, key); // type (and possibly null) check

                root = new Entry<>(key, value, null);
                size = 1;
                modCount++;
                return null;
            }
            2.2 以后添加
            Comparator<? super K> cpr = comparator;
            if (cpr != null) {
                do { //遍历所有的key , 给当前key找到适当位置
                    parent = t;
                    cmp = cpr.compare(key, t.key);//动态绑定到我们的匿名内部类的compare
                    if (cmp < 0)
                        t = t.left;
                    else if (cmp > 0)
                        t = t.right;
                    else  //如果遍历过程中，发现准备添加Key 和当前已有的Key 相等，就不添加，但value会被替换
                        return t.setValue(value);
                } while (t != null);
            }
         */
    }
}
```

14.19 Collections 工具类  
![](https://img-blog.csdnimg.cn/f8238849966345988b5b490a03cfae6a.png)  
![](https://img-blog.csdnimg.cn/b12f17f39c45403ba2d66c5d35443591.png)

```
package com.hspedu.collections_;
import java.util.*;
@SuppressWarnings({"all"})
public class Collections_ {
    public static void main(String[] args) {
        //创建ArrayList 集合，用于测试.
        List list = new ArrayList();
        list.add("tom");
        list.add("smith");
        list.add("king");
        list.add("milan");
        list.add("tom");
        
//        reverse(List)：反转 List 中元素的顺序
        Collections.reverse(list);
        System.out.println("list=" + list);
//        shuffle(List)：对 List 集合元素进行随机排序
//        for (int i = 0; i < 5; i++) {
//            Collections.shuffle(list);
//            System.out.println("list=" + list);
//        }

//        sort(List)：根据元素的自然顺序对指定 List 集合元素按升序排序
        Collections.sort(list);
        System.out.println("自然排序后");
        System.out.println("list=" + list);
//        sort(List，Comparator)：根据指定的 Comparator 产生的顺序对 List 集合元素进行排序
        //我们希望按照 字符串的长度大小排序
        Collections.sort(list, new Comparator() {
            @Override
            public int compare(Object o1, Object o2) {
                //可以加入校验代码.
                return ((String) o2).length() - ((String) o1).length();//List允许重复，所以能同时有两个长度相同的
            }
        });
        System.out.println("字符串长度大小排序=" + list);
//        swap(List，int， int)：将指定 list 集合中的 i 处元素和 j 处元素进行交换
        //比如
        Collections.swap(list, 0, 1);
        System.out.println("交换后的情况");
        System.out.println("list=" + list);

        //Object max(Collection)：根据元素的自然顺序，返回给定集合中的最大元素
        System.out.println("自然顺序最大元素=" + Collections.max(list));
        //Object max(Collection，Comparator)：根据 Comparator 指定的顺序，返回给定集合中的最大元素
        //比如，我们要返回长度最大的元素
        Object maxObject = Collections.max(list, new Comparator() {
            @Override
            public int compare(Object o1, Object o2) {
                return ((String)o1).length() - ((String)o2).length();
            }
        });
        System.out.println("长度最大的元素=" + maxObject);

        //Object min(Collection)
        //Object min(Collection，Comparator)
        //上面的两个方法，参考max即可

        //int frequency(Collection，Object)：返回指定集合中指定元素的出现次数
        System.out.println("tom出现的次数=" + Collections.frequency(list, "tom"));

        //void copy(List dest,List src)：将src中的内容复制到dest中
        ArrayList dest = new ArrayList();
        //为了完成一个完整拷贝，我们需要先给dest 赋值，大小和list.size()一样
        for(int i = 0; i < list.size(); i++) {
            dest.add("");
        }
        //注意：size是指元素个数，而length是数组长度，构造器是不会改变size的。不能通过初始化集合来给定大小，因为这并不会改变size，底层是用两个集合的size比较的，size 和 length 不能等同，size 表示 当前集合的元素个数， 随着元素的增加而增加。
        
        //拷贝
        Collections.copy(dest, list);
        System.out.println("dest=" + dest);

        //boolean replaceAll(List list，Object oldVal，Object newVal)：使用新值替换 List 对象的所有旧值
        //如果list中，有tom 就替换成 汤姆
        Collections.replaceAll(list, "tom", "汤姆");
        System.out.println("list替换后=" + list);
    }
}
```

拷贝函数的源码：如果 src 的元素个数 (size) 为 0，则会抛出异常  
![](https://img-blog.csdnimg.cn/36db0a2dbf1b4e3c971d8adf945bb2db.png)  
14.20 本章作业  
![](https://img-blog.csdnimg.cn/1808b9c5df8b47839860721b3cd6ca81.png)

```
package com.hspedu.homework;
import java.util.*;
@SuppressWarnings({"all"})
public class Homework03 {
    public static void main(String[] args) {
        Map m = new HashMap();
        m.put("jack", 650);//int->Integer
        m.put("tom", 1200);//int->Integer
        m.put("smith", 2900);//int->Integer
        System.out.println(m);

        m.put("jack", 2600);//替换，更新
        System.out.println(m);

        //为所有员工工资加薪100元；
        //keySet
        Set keySet = m.keySet();
        for (Object key : keySet) {
            //更新
            m.put(key, (Integer)m.get(key) + 100);
        }
        System.out.println(m);

        System.out.println("=============遍历=============");
        //遍历 EntrySet
        Set entrySet = m.entrySet();
        //迭代器
        Iterator iterator = entrySet.iterator();
        while (iterator.hasNext()) {
            Map.Entry entry =  (Map.Entry)iterator.next();
            System.out.println(entry.getKey() + "-" + entry.getValue());
        }

        System.out.println("====遍历所有的工资====");
        Collection values = m.values();
        for (Object value : values) {
            System.out.println("工资=" + value);
        }
    }
}
```

![](https://img-blog.csdnimg.cn/5c340e753b7040869eafbfe028b212d6.png)

```
package com.hspedu.homework;
import java.util.TreeSet;
@SuppressWarnings({"all"})
public class Homework05 {
   public static void main(String[] args) {
       TreeSet treeSet = new TreeSet();
       //分析源码
       //add 方法，因为 TreeSet() 构造器没有传入Comparator接口的匿名内部类
       //所以在底层 Comparable<? super K> k = (Comparable<? super K>) key;
       //即 把 Perosn转成 Comparable类型
       treeSet.add(new Person());//ClassCastException.
       treeSet.add(new Person());//ClassCastException.
       treeSet.add(new Person());//ClassCastException.
       treeSet.add(new Person());//ClassCastException.
       treeSet.add(new Person());//ClassCastException.
       System.out.println(treeSet);
   }
}
class Person implements Comparable{
   @Override
   public int compareTo(Object o) {
       return 0;
   }
}
```

![](https://img-blog.csdnimg.cn/a9136e044c49485080e41fe634a1f32a.png)  
![](https://img-blog.csdnimg.cn/4679be4a40c44d55a71d0c5f64227e3e.png)  
注意：table 里数据 Person 的位置是没有变化的，主要是 remove 方法会再次调用 hashCode 方法，由于 name 的值被更改，导致 remove 没有找到需要删除的值，所以 p1 没有被删除。

![](https://img-blog.csdnimg.cn/f596f1fe4c684471bb9a13b7a59fa59a.png)

#### 第 15 章 泛型

generic：泛型 [dʒəˈnerɪk]

15.1.2 使用传统方法的问题分析  
![](https://img-blog.csdnimg.cn/bb1f05211b914fef8c6f58a108838682.png)  
15.1.3 泛型快速体验 - 用泛型来解决前面的问题

```
package com.hspedu.generic.improve;
import java.util.ArrayList;
@SuppressWarnings({"all"})
/*
1.请编写程序，在ArrayList 中，添加3个Dog对象
2.Dog对象含有name 和 age, 并输出name 和 age (要求使用getXxx())
3.老师使用泛型来完成代码
 */
public class Generic02 {
    public static void main(String[] args) {
        //使用传统的方法来解决===> 使用泛型
        //老韩解读
        //1. 当我们 ArrayList<Dog> 表示存放到 ArrayList 集合中的元素是Dog类型 (细节后面说...)
        //2. 如果编译器发现添加的类型，不满足要求，就会报错
        //3. 在遍历的时候，可以直接取出 Dog 类型而不是 Object
        //4. public class ArrayList<E> {} E称为泛型,那么 Dog->E
        ArrayList<Dog> arrayList = new ArrayList<Dog>();
        arrayList.add(new Dog("旺财", 10));
        arrayList.add(new Dog("发财", 1));
        arrayList.add(new Dog("小黄", 5));
        //假如我们的程序员，不小心，添加了一只猫
        //arrayList.add(new Cat("招财猫", 8));
        System.out.println("===使用泛型====");
        for (Dog dog : arrayList) {
            System.out.println(dog.getName() + "-" + dog.getAge());
        }
    }
}
class Dog {
    private String name;
    private int age;
    public Dog(String name, int age) {
        this.name = name;
        this.age = age;
    }
   //省略getter、setter方法
}

class Cat { //Cat类
    private String name;
    private int age;
    public Cat(String name, int age) {
        this.name = name;
        this.age = age;
    }
	//省略getter、setter方法
}
```

15.2 泛型的理解和好处  
![](https://img-blog.csdnimg.cn/45d9a5a7968b462495035b7ee9e308e6.png)  
15.3 泛型介绍  
泛型可以理解成表示数据类型的一种数据类型。  
![](https://img-blog.csdnimg.cn/243f4d77b3164db9a700967d559ee7a2.png)

```
package com.hspedu.generic;
import java.util.List;
public class Generic03 {
    public static void main(String[] args) {
        //注意，特别强调： E具体的数据类型在定义Person对象的时候指定,即在编译期间，就确定E是什么类型
        Person<String> person = new Person<String>("韩顺平教育");
        person.show(); //String
        /*
            你可以这样理解，上面的Person类
            class Person {
                String s ;//E表示 s的数据类型, 该数据类型在定义Person对象的时候指定,即在编译期间，就确定E是什么类型
                public Person(String s) {//E也可以是参数类型
                    this.s = s;
                }
                public String f() {//返回类型使用E
                    return s;
                }
            }
         */
    }
}
//泛型的作用是：可以在类声明时通过一个标识表示类中某个属性的类型，
// 或者是某个方法的返回值的类型，或者是参数类型
class Person<E> {
    E s ;//E表示 s的数据类型, 该数据类型在定义Person对象的时候指定,即在编译期间，就确定E是什么类型
    public Person(E s) {//E也可以是参数类型
        this.s = s;
    }
    public E f() {//返回类型使用E
        return s;
    }
    public void show() {
        System.out.println(s.getClass());//显示s的运行类型
    }
}
```

15.4 泛型的语法  
![](https://img-blog.csdnimg.cn/3e2d7a5469d3488d9579b825deef26d2.png)  
![](https://img-blog.csdnimg.cn/018779902d284388bb40bfb77b571ecb.png)

```
package com.hspedu.generic;
import java.util.*;
@SuppressWarnings({"all"})
public class GenericExercise {
    public static void main(String[] args) {
        //使用泛型方式给HashSet 放入3个学生对象
        HashSet<Student> students = new HashSet<Student>();
        students.add(new Student("jack", 18));
        students.add(new Student("tom", 28));
        students.add(new Student("mary", 19));

        //遍历
        for (Student student : students) {
            System.out.println(student);
        }

        //使用泛型方式给HashMap 放入3个学生对象
        //K -> String V->Student
        HashMap<String, Student> hm = new HashMap<String, Student>();
        /*
            public class HashMap<K,V>  {}
         */
        hm.put("milan", new Student("milan", 38));
        hm.put("smith", new Student("smith", 48));
        hm.put("hsp", new Student("hsp", 28));

        //迭代器 EntrySet
        /*
        public Set<Map.Entry<K,V>> entrySet() {
            Set<Map.Entry<K,V>> es;
            return (es = entrySet) == null ? (entrySet = new EntrySet()) : es;
        }
         */
        Set<Map.Entry<String, Student>> entries = hm.entrySet();
        /*
            public final Iterator<Map.Entry<K,V>> iterator() {
                return new EntryIterator();
            }
         */
        Iterator<Map.Entry<String, Student>> iterator = entries.iterator();
        System.out.println("==============================");
        while (iterator.hasNext()) {
            Map.Entry<String, Student> next =  iterator.next();
            System.out.println(next.getKey() + "-" + next.getValue());
        }
    }
}
class Student {
    private String name;
    private int age;
    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
	//省略getter、setter、toString方法
}
```

15.4.4 泛型使用的注意事项和细节  
![](https://img-blog.csdnimg.cn/0f6feff3b819452e9f662d58a41de87b.png)

```
package com.hspedu.generic;
import java.util.ArrayList;
import java.util.List;
@SuppressWarnings({"all"})
public class GenericDetail {
    public static void main(String[] args) {
        //1.给泛型指向数据类型是，要求是引用类型，不能是基本数据类型
        List<Integer> list = new ArrayList<Integer>(); //OK
        //List<int> list2 = new ArrayList<int>();//错误

        //2. 说明
        //因为 E 指定了 A 类型, 构造器传入了 new A()
        //在给泛型指定具体类型后，可以传入该类型或者其子类类型
        Pig<A> aPig = new Pig<A>(new A());
        aPig.f();
        Pig<A> aPig2 = new Pig<A>(new B());
        aPig2.f();

        //3. 泛型的使用形式
        ArrayList<Integer> list1 = new ArrayList<Integer>();
        List<Integer> list2 = new ArrayList<Integer>();
        //在实际开发中，我们往往简写
        //编译器会进行类型推断, 老师推荐使用下面写法
        ArrayList<Integer> list3 = new ArrayList<>();
        List<Integer> list4 = new ArrayList<>();
        ArrayList<Pig> pigs = new ArrayList<>();

        //4. 如果是这样写 泛型默认是 Object
        ArrayList arrayList = new ArrayList();//等价 ArrayList<Object> arrayList = new ArrayList<Object>();
        /*
            public boolean add(Object e) {
                ensureCapacityInternal(size + 1);  // Increments modCount!!
                elementData[size++] = e;
                return true;
            }
         */
        Tiger tiger = new Tiger();
        /*
            class Tiger {//类
                Object e;
                public Tiger() {}
                public Tiger(Object e) {
                    this.e = e;
                }
            }
         */
    }
}
class Tiger<E> {//类
    E e;
    public Tiger() {}
    public Tiger(E e) {
        this.e = e;
    }
}
class A {}
class B extends A {}
class Pig<E> {//
    E e;
    public Pig(E e) {
        this.e = e;
    }
    public void f() {
        System.out.println(e.getClass()); //运行类型
    }
}
```

15.5 泛型课堂练习  
![](https://img-blog.csdnimg.cn/b62a54d3c6a344119547a1165b22f4e7.png)  
GenericExercise02.java

```
package com.hspedu.generic;
import java.util.ArrayList;
import java.util.Comparator;
@SuppressWarnings({"all"})
public class GenericExercise02 {
    public static void main(String[] args) {
        ArrayList<Employee> employees = new ArrayList<>();
        employees.add(new Employee("tom", 20000, new MyDate(1980,12,11)));
        employees.add(new Employee("jack", 12000, new MyDate(2001,12,12)));
        employees.add(new Employee("tom", 50000, new MyDate(1980,12,10)));
        System.out.println("employees=" + employees);

        employees.sort(new Comparator<Employee>() {
            @Override
            public int compare(Employee emp1, Employee emp2) {
                //先按照name排序，如果name相同，则按生日日期的先后排序。【即：定制排序】
                //先对传入的参数进行验证
                if(!(emp1 instanceof  Employee && emp2 instanceof Employee)) {
                    System.out.println("类型不正确..");
                    return 0;
                }
                //比较name
                int i = emp1.getName().compareTo(emp2.getName());
                if(i != 0) {
                    return i;
                }
                //下面是对birthday的比较，因此，我们最好把这个比较，放在MyDate类完成
                //封装后，将来可维护性和复用性，就大大增强.
                return emp1.getBirthday().compareTo(emp2.getBirthday());
            }
        });
        System.out.println("==对雇员进行排序==");
        System.out.println(employees);
    }
}
```

MyDate.java

```
package com.hspedu.generic;
public class MyDate implements Comparable<MyDate>{
    private int year;
    private int month;
    private int day;
	//省略构造器、getter、setter、toString方法
    @Override
    public int compareTo(MyDate o) { //把对year-month-day比较放在这里
        int yearMinus = year - o.getYear();
        if(yearMinus != 0) {
            return  yearMinus;
        }
        //如果year相同，就比较month
        int monthMinus = month - o.getMonth();
        if(monthMinus != 0) {
            return monthMinus;
        }
        //如果year 和 month
        return day - o.getDay();
    }
}
```

15.6 自定义泛型  
![](https://img-blog.csdnimg.cn/79739aa354b641a6a892ba244e376ded.png)  
![](https://img-blog.csdnimg.cn/08421fc03f7844778aeb4ac88629aa1b.png)

```
package com.hspedu.customgeneric;
import java.util.Arrays;
@SuppressWarnings({"all"})
public class CustomGeneric_ {
    public static void main(String[] args) {
        //T=Double, R=String, M=Integer
        Tiger<Double,String,Integer> g = new Tiger<>("john");
        g.setT(10.9); //OK
        //g.setT("yy"); //错误，类型不对
        System.out.println(g);
        Tiger g2 = new Tiger("john~~");//OK T=Object R=Object M=Object
        g2.setT("yy"); //OK ,因为 T=Object "yy"=String 是Object子类
        System.out.println("g2=" + g2);
    }
}
//老韩解读
//1. Tiger 后面泛型，所以我们把 Tiger 就称为自定义泛型类
//2, T, R, M 泛型的标识符, 一般是单个大写字母
//3. 泛型标识符可以有多个.
//4. 普通成员可以使用泛型 (属性、方法)
//5. 使用泛型的数组，不能初始化
//6. 静态方法中不能使用类的泛型
class Tiger<T, R, M> {
    String name;
    R r; //属性使用到泛型
    M m;
    T t;
    //因为数组在new 不能确定T的类型，就无法在内存开空间
    T[] ts;
    public Tiger(String name) {
        this.name = name;
    }
    public Tiger(R r, M m, T t) {//构造器使用泛型
        this.r = r;
        this.m = m;
        this.t = t;
    }
    public Tiger(String name, R r, M m, T t) {//构造器使用泛型
        this.name = name;
        this.r = r;
        this.m = m;
        this.t = t;
    }
    //因为静态是和类相关的，在类加载时，对象还没有创建
    //所以，如果静态方法和静态属性使用了泛型，JVM就无法完成初始化
//    static R r2;
//    public static void m1(M m) {
//
//    }

    //方法使用泛型
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public R getR() {
        return r;
    }
    public void setR(R r) {//方法使用到泛型
        this.r = r;
    }
    public M getM() {//返回类型可以使用泛型.
        return m;
    }
    public void setM(M m) {
        this.m = m;
    }
    public T getT() {
        return t;
    }
    public void setT(T t) {
        this.t = t;
    }
    @Override
    public String toString() {
        return "Tiger{" +
                " + name + '\'' +
                ", r=" + r +
                ", m=" + m +
                ", t=" + t +
                ", ts=" + Arrays.toString(ts) +
                '}';
    }
}
```

15.6.2 自定义泛型接口  
![](https://img-blog.csdnimg.cn/68969db87ea3482c9a8799577322831f.png)  
![](https://img-blog.csdnimg.cn/c2a261ede018452d941c0b0ad0e4c615.png)

```
package com.hspedu.customgeneric;
public class CustomInterfaceGeneric {
    public static void main(String[] args) {
    }
}
//在继承接口 指定泛型接口的类型
interface IA extends IUsb<String, Double> {
}
//当我们去实现IA接口时，因为IA在继承IUsu 接口时，指定了U 为String R为Double
//，在实现IUsu接口的方法时，使用String替换U, 是Double替换R
class AA implements IA {
    @Override
    public Double get(String s) {
        return null;
    }
    @Override
    public void hi(Double aDouble) {}
    @Override
    public void run(Double r1, Double r2, String u1, String u2) {}
}
//实现接口时，直接指定泛型接口的类型
//给U 指定Integer 给 R 指定了 Float
//所以，当我们实现IUsb方法时，会使用Integer替换U, 使用Float替换R
class BB implements IUsb<Integer, Float> {
    @Override
    public Float get(Integer integer) {
        return null;
    }
    @Override
    public void hi(Float aFloat) {}
    @Override
    public void run(Float r1, Float r2, Integer u1, Integer u2) {}
}
//没有指定类型，默认为Object
//建议直接写成 IUsb<Object,Object>
class CC implements IUsb { //等价 class CC implements IUsb<Object,Object> {
    @Override
    public Object get(Object o) {
        return null;
    }
    @Override
    public void hi(Object o) {}
    @Override
    public void run(Object r1, Object r2, Object u1, Object u2) {}
}
interface IUsb<U, R> {
    int n = 10;
    //U name; 不能这样使用
    //普通方法中，可以使用接口泛型
    R get(U u);
    void hi(R r);
    void run(R r1, R r2, U u1, U u2);
    //在jdk8 中，可以在接口中，使用默认方法, 也是可以使用泛型
    default R method(U u) {
        return null;
    }
}
```

15.6.3 自定义泛型方法  
![](https://img-blog.csdnimg.cn/75218bbb46bd4593ac28c6e28b07ff14.png)

```
package com.hspedu.customgeneric;
import java.util.ArrayList;
@SuppressWarnings({"all"})
public class CustomMethodGeneric {
    public static void main(String[] args) {
        Car car = new Car();
        car.fly("宝马", 100);//当调用方法时，传入参数，编译器，就会确定类型
        System.out.println("=======");
        car.fly(300, 100.1);//当调用方法时，传入参数，编译器，就会确定类型

        //测试
        //T->String, R-> ArrayList
        Fish<String, ArrayList> fish = new Fish<>();
        fish.hello(new ArrayList(), 11.3f);
    }
}
//泛型方法，可以定义在普通类中, 也可以定义在泛型类中
class Car {//普通类
    public void run() {//普通方法}
    //说明 泛型方法
    //1. <T,R> 就是泛型
    //2. 是提供给 fly使用的
    public <T, R> void fly(T t, R r) {//泛型方法
        System.out.println(t.getClass());//String
        System.out.println(r.getClass());//Integer
    }
}
class Fish<T, R> {//泛型类
    public void run() {//普通方法}
    public<U,M> void eat(U u, M m) {//泛型方法}
    //说明
    //1. 下面hi方法不是泛型方法
    //2. 是hi方法使用了类声明的 泛型
    public void hi(T t) {}
    //泛型方法，可以使用类声明的泛型，也可以使用自己声明泛型
    public<K> void hello(R r, K k) {
        System.out.println(r.getClass());//ArrayList
        System.out.println(k.getClass());//Float
    }
}
```

15.6.4 课堂练习  
![](https://img-blog.csdnimg.cn/be285cc7ee8f4baeb789bb29fcb21349.png)  
![](https://img-blog.csdnimg.cn/938fa40debd74e819b369821db926a03.png)  
15.7 泛型的继承和通配符  
![](https://img-blog.csdnimg.cn/dc5c38e758644cb79fd189ee94d28a91.png)

```
package com.hspedu;
import java.util.ArrayList;
import java.util.List;
public class GenericExtends {
    public static void main(String[] args) {
        Object o = new String("xx");
        //泛型没有继承性
        //List<Object> list = new ArrayList<String>();

        //举例说明下面三个方法的使用
        List<Object> list1 = new ArrayList<>();
        List<String> list2 = new ArrayList<>();
        List<AA> list3 = new ArrayList<>();
        List<BB> list4 = new ArrayList<>();
        List<CC> list5 = new ArrayList<>();

        //如果是 List<?> c ，可以接受任意的泛型类型
        printCollection1(list1);
        printCollection1(list2);
        printCollection1(list3);
        printCollection1(list4);
        printCollection1(list5);

        //List<? extends AA> c： 表示 上限，可以接受 AA或者AA子类
//        printCollection2(list1);//×
//        printCollection2(list2);//×
        printCollection2(list3);//√
        printCollection2(list4);//√
        printCollection2(list5);//√

        //List<? super AA> c: 支持AA类以及AA类的父类，不限于直接父类
        printCollection3(list1);//√
        //printCollection3(list2);//×
        printCollection3(list3);//√
        //printCollection3(list4);//×
        //printCollection3(list5);//×

        //冒泡排序

        //插入排序

        //....
    }
    // ? extends AA 表示 上限，可以接受 AA或者AA子类
    public static void printCollection2(List<? extends AA> c) {
        for (Object object : c) {
            System.out.println(object);
        }
    }

    //说明: List<?> 表示 任意的泛型类型都可以接受
    public static void printCollection1(List<?> c) {
        for (Object object : c) { // 通配符，取出时，就是Object
            System.out.println(object);
        }
    }

    // ? super 子类类名AA:支持AA类以及AA类的父类，不限于直接父类，
    //规定了泛型的下限
    public static void printCollection3(List<? super AA> c) {
        for (Object object : c) {
            System.out.println(object);
        }
    }
}
class AA {}
class BB extends AA {}
class CC extends BB {}
```

15.8 JUnit  
![](https://img-blog.csdnimg.cn/7bc2d25a34ed4f4ca0548d27d3f6b796.png)  
![](https://img-blog.csdnimg.cn/e96bfcb7db6543fc8d1f926aa0200dba.png)  
15.9 本章作业  
![](https://img-blog.csdnimg.cn/bf0893b57f64467db48a2519548b497e.png)  
User.java

```
package com.hspedu.homework;
public class User {
    private int id;
    private int age;
    private String name;
    //省略getter、setter、构造器、toString方法
}
```

DAO.java

```
package com.hspedu.homework;
import java.util.*;
public class DAO<T> {//泛型类
    private Map<String, T> map = new HashMap<>();
    public T get(String id) {
        return map.get(id);
    }
    public void update(String id,T entity) {
        map.put(id, entity);
    }
    //返回 map 中存放的所有 T 对象
    //遍历map [k-v],将map的 所有value(T entity),封装到ArrayList返回即可
    public List<T> list() {
        //创建 Arraylist
        List<T> list = new ArrayList<>();
        //遍历map
        Set<String> keySet = map.keySet();
        for (String key : keySet) {
            //map.get(key) 返回就是 User对象->ArrayList
            list.add(map.get(key));//也可以直接使用本类的 get(String id)
        }
        return list;
    }
    public void delete(String id) {
        map.remove(id);
    }
    public void save(String id,T entity) {//把entity保存到map
        map.put(id, entity);
    }
}
```

Homework01.java

```
package com.hspedu.homework;
import org.junit.jupiter.api.Test;
import java.util.List;
public class Homework01 {
    public static void main(String[] args) {}
    @Test
    public void testList() {
        //说明
        //这里我们给T 指定类型是User
        DAO<User> dao = new DAO<>();
        dao.save("001", new User(1,10,"jack"));
        dao.save("002", new User(2,18,"king"));
        dao.save("003", new User(3,38,"smith"));
        List<User> list = dao.list();
        System.out.println("list=" + list);

        dao.update("003", new User(3, 58, "milan"));
        dao.delete("001");//删除
        System.out.println("===修改后====");
        list = dao.list();
        System.out.println("list=" + list);
        System.out.println("id=003 " + dao.get("003"));//milan
    }
}
```

#### 第 16 章 坦克大战

16.2 java 绘图坐标体系

16.2.1 坐标体系 - 介绍  
![](https://img-blog.csdnimg.cn/f387f6076c4b41ef9aa803f43963418f.png)  
16.2.2 坐标体系 - 像素  
![](https://img-blog.csdnimg.cn/3901fcda50244250a730791befc1b071.png)

#### 第 17 章 多线程基础

17.1 线程相关概念

17.1.1 程序  
![](https://img-blog.csdnimg.cn/d6a2d6977e86434fb289e6b3b098ff6d.png)  
17.1.2 进程  
![](https://img-blog.csdnimg.cn/73eef64bed134ee48dbf1406e4126d8f.png)  
17.1.3 什么是线程  
![](https://img-blog.csdnimg.cn/87201c0e9a2443e6bae04eb7dfa6be08.png)  
17.1.4 其他相关概念  
![](https://img-blog.csdnimg.cn/af3872b9e0584038bad3648cca62f006.png)  
![](https://img-blog.csdnimg.cn/1a1442b7a4cb4ff8ade91c444e403281.png)  
17.2 线程基本使用

17.2.1 创建线程的两种方式  
![](https://img-blog.csdnimg.cn/bf313f8c39c840a89427cf9d8c050b8a.png)  
17.2.2 线程应用案例 1 - 继承 Thread 类  
![](https://img-blog.csdnimg.cn/09537cbbefaa4ce3a2387888bec188df.png)

```
package com.hspedu.threaduse;
public class Thread01 {
    public static void main(String[] args) throws InterruptedException {
        //创建Cat对象，可以当做线程使用
        Cat cat = new Cat();
        //老韩读源码
        /*
            (1)
            public synchronized void start() {
                start0();
            }
            (2)
            //start0() 是本地方法，是JVM调用, 底层是c/c++实现
            //真正实现多线程的效果， 是start0(), 而不是 run
            private native void start0();
         */
        cat.start();//启动线程-> 最终会执行cat的run方法

        //cat.run();//run方法就是一个普通的方法, 没有真正的启动一个线程，就会把run方法执行完毕，才向下执行
        //说明: 当main线程启动一个子线程 Thread-0, 主线程不会阻塞, 会继续执行
        //这时 主线程和子线程是交替执行..
        System.out.println("主线程继续执行" + Thread.currentThread().getName());//名字main
        for(int i = 0; i < 60; i++) {
            System.out.println("主线程 i=" + i);
            //让主线程休眠
            Thread.sleep(1000);
        }
    }
}
//老韩说明
//1. 当一个类继承了 Thread 类， 该类就可以当做线程使用
//2. 我们会重写 run方法，写上自己的业务代码
//3. run Thread 类 实现了 Runnable 接口的run方法
/*
    @Override
    public void run() {
        if (target != null) {
            target.run();
        }
    }
 */
class Cat extends Thread {
    int times = 0;
    @Override
    public void run() {//重写run方法，写上自己的业务逻辑
        while (true) {
            //该线程每隔1秒。在控制台输出 “喵喵, 我是小猫咪”
            System.out.println("喵喵, 我是小猫咪" + (++times) + " 线程名=" + Thread.currentThread().getName());
            //让该线程休眠1秒 ctrl+alt+t
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            if(times == 80) {
                break;//当times 到80, 退出while, 这时线程也就退出..
            }
        }
    }
}
```

![](https://img-blog.csdnimg.cn/abebbd1ed49a4058a2a8bf193f773afc.png)  
17.2.3 线程应用案例 2 - 实现 Runnable 接口  
![](https://img-blog.csdnimg.cn/3ef6afdc5a3c4c6caab3dd4a2b35315b.png)  
![](https://img-blog.csdnimg.cn/d17c67dd0bc940f2b8c5d1ac8706210c.png)

```
package com.hspedu.threaduse;
public class Thread02 {
    public static void main(String[] args) {
        Dog dog = new Dog();
        //dog.start(); 这里不能调用start
        //创建了Thread对象，把 dog对象(实现Runnable),放入Thread
        Thread thread = new Thread(dog);
        thread.start();
//        Tiger tiger = new Tiger();//实现了 Runnable
//        ThreadProxy threadProxy = new ThreadProxy(tiger);
//        threadProxy.start();
    }
}
class Animal {}
class Tiger extends Animal implements Runnable {
    @Override
    public void run() {
        System.out.println("老虎嗷嗷叫....");
    }
}
//线程代理类 , 模拟了一个极简的Thread类
class ThreadProxy implements Runnable {//你可以把Proxy类当做 ThreadProxy
    private Runnable target = null;//属性，类型是 Runnable
    @Override
    public void run() {
        if (target != null) {
            target.run();//动态绑定（运行类型Tiger）
        }
    }
    public ThreadProxy(Runnable target) {
        this.target = target;
    }
    public void start() {
        start0();//这个方法时真正实现多线程方法
    }
    public void start0() {
        run();
    }
}
class Dog implements Runnable { //通过实现Runnable接口，开发线程
    int count = 0;
    @Override
    public void run() { //普通方法
        while (true) {
            System.out.println("小狗汪汪叫..hi" + (++count) + Thread.currentThread().getName());
            //休眠1秒
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            if (count == 10) {
                break;
            }
        }
    }
}
```

17.3 继承 Thread vs 实现 Runnable 的区别  
![](https://img-blog.csdnimg.cn/a43c775608b74d85ad2712e5cecd4095.png)  
![](https://img-blog.csdnimg.cn/58382f80edcb4b208e29b93e527dc3e8.png)

```
package com.hspedu.ticket;
public class SellTicket {
    public static void main(String[] args) {
        //测试
//        SellTicket01 sellTicket01 = new SellTicket01();
//        SellTicket01 sellTicket02 = new SellTicket01();
//        SellTicket01 sellTicket03 = new SellTicket01();
//
//        //这里我们会出现超卖..
//        sellTicket01.start();//启动售票线程
//        sellTicket02.start();//启动售票线程
//        sellTicket03.start();//启动售票线程

        System.out.println("===使用实现接口方式来售票=====");
        SellTicket02 sellTicket02 = new SellTicket02();
        new Thread(sellTicket02).start();//第1个线程-窗口
        new Thread(sellTicket02).start();//第2个线程-窗口
        new Thread(sellTicket02).start();//第3个线程-窗口
    }
}
//使用Thread方式
class SellTicket01 extends Thread {
    private static int ticketNum = 100;//让多个线程共享 ticketNum
    @Override
    public void run() {
        while (true) {
            if (ticketNum <= 0) {
                System.out.println("售票结束...");
                break;
            }
            //休眠50毫秒, 模拟
            try {
                Thread.sleep(50);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("窗口 " + Thread.currentThread().getName() + " 售出一张票"
                    + " 剩余票数=" + (--ticketNum));
        }
    }
}
//实现接口方式
class SellTicket02 implements Runnable {
    private int ticketNum = 100;//让多个线程共享 ticketNum
    @Override
    public void run() {
        while (true) {
            if (ticketNum <= 0) {
                System.out.println("售票结束...");
                break;
            }
            //休眠50毫秒, 模拟
            try {
                Thread.sleep(50);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("窗口 " + Thread.currentThread().getName() + " 售出一张票"
                    + " 剩余票数=" + (--ticketNum));//1 - 0 - -1  - -2
        }
    }
}
```

17.4 线程终止  
![](https://img-blog.csdnimg.cn/b0f636c3db99409a99202b6b1a5de15c.png)  
![](https://img-blog.csdnimg.cn/c7ef7a75c6a648a5b5b1da61b538c3f6.png)

```
package com.hspedu.exit_;
public class ThreadExit_ {
    public static void main(String[] args) throws InterruptedException {
        T t1 = new T();
        t1.start();
        //如果希望main线程去控制t1 线程的终止, 必须可以修改 loop
        //让t1 退出run方法，从而终止 t1线程 -> 通知方式
        //让主线程休眠 10 秒，再通知 t1线程退出
        System.out.println("main线程休眠10s...");
        Thread.sleep(10 * 1000);
        t1.setLoop(false);
    }
}
class T extends Thread {
    private int count = 0;
    //设置一个控制变量
    private boolean loop = true;
    @Override
    public void run() {
        while (loop) {
            try {
                Thread.sleep(50);// 让当前线程休眠50ms
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("T 运行中...." + (++count));
        }
    }
    public void setLoop(boolean loop) {
        this.loop = loop;
    }
}
```

17.5 线程常用方法

17.5.1 常用方法第一组  
![](https://img-blog.csdnimg.cn/4431874fb1b345d995f98cc8c0b3bb00.png)  
17.5.2 注意事项和细节  
![](https://img-blog.csdnimg.cn/4ab8454fdd8d4013b6af72d146c2f7ca.png)  
17.5.3 应用案例  
![](https://img-blog.csdnimg.cn/14e95c545b164798bf2291d1aa2bf644.png)

```
package com.hspedu.method;
public class ThreadMethod01 {
    public static void main(String[] args) throws InterruptedException {
        //测试相关的方法
        T t = new T();
        t.setName("老韩");
        t.setPriority(Thread.MIN_PRIORITY);//1
        t.start();//启动子线程

        //主线程打印5 hi ,然后我就中断 子线程的休眠
        for(int i = 0; i < 5; i++) {
            Thread.sleep(1000);
            System.out.println("hi " + i);
        }
        System.out.println(t.getName() + " 线程的优先级 =" + t.getPriority());//1
        t.interrupt();//当执行到这里，就会中断 t线程的休眠.
    }
}
class T extends Thread { //自定义的线程类
    @Override
    public void run() {
        while (true) {
            for (int i = 0; i < 100; i++) {
                //Thread.currentThread().getName() 获取当前线程的名称
                System.out.println(Thread.currentThread().getName() + "  吃包子~~~~" + i);
            }
            try {
                System.out.println(Thread.currentThread().getName() + " 休眠中~~~");
                Thread.sleep(20000);//20秒
            } catch (InterruptedException e) {
                //当该线程执行到一个interrupt 方法时，就会catch 一个 异常, 可以加入自己的业务代码
                //InterruptedException 是捕获到一个中断异常.
                System.out.println(Thread.currentThread().getName() + "被 interrupt了");
            }
        }
    }
}
```

17.5.4 常用方法第二组  
![](https://img-blog.csdnimg.cn/6fd10d169eb04eb5b9d3688ae6985660.png)  
17.5.5 应用案例  
![](https://img-blog.csdnimg.cn/bf48f19f71f14b9093df5a17d37612cc.png)

```
package com.hspedu.method;
public class ThreadMethod02 {
    public static void main(String[] args) throws InterruptedException {
        T2 t2 = new T2();
        t2.start();
        for(int i = 1; i <= 20; i++) {
            Thread.sleep(1000);
            System.out.println("主线程(小弟) 吃了 " + i  + " 包子");
            if(i == 5) {
                System.out.println("主线程(小弟) 让 子线程(老大) 先吃");
                //join, 线程插队
                //t2.join();// 这里相当于让t2 线程先执行完毕
                Thread.yield();//礼让，不一定成功..
                System.out.println("线程(老大) 吃完了 主线程(小弟) 接着吃..");
            }
        }
    }
}
class T2 extends Thread {
    @Override
    public void run() {
        for (int i = 1; i <= 20; i++) {
            try {
                Thread.sleep(1000);//休眠1秒
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("子线程(老大) 吃了 " + i +  " 包子");
        }
    }
}
```

17.5.6 课堂练习  
![](https://img-blog.csdnimg.cn/371611cae1084ce0bf58b169d6cb669b.png)

```
package com.hspedu.method;
public class ThreadMethodExercise {
    public static void main(String[] args) throws InterruptedException {
        Thread t3 = new Thread(new T3());//创建子线程
        for (int i = 1; i <= 10; i++) {
            System.out.println("hi " + i);
            if(i == 5) {//说明主线程输出了5次 hi
                t3.start();//启动子线程 输出 hello...
                t3.join();//立即将t3子线程，插入到main线程，让t3先执行
            }
            Thread.sleep(1000);//输出一次 hi, 让main线程也休眠1s
        }
    }
}
class T3 implements Runnable {
    private int count = 0;
    @Override
    public void run() {
        while (true) {
            System.out.println("hello " + (++count));
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            if (count == 10) {
                break;
            }
        }
    }
}
```

17.5.7 用户线程和守护线程  
![](https://img-blog.csdnimg.cn/f78d787652e0421abe14f2a80167f35c.png)  
17.5.8 应用案例  
![](https://img-blog.csdnimg.cn/0391719669354cf2a3882c3e73233282.png)

```
package com.hspedu.method;
public class ThreadMethod03 {
    public static void main(String[] args) throws InterruptedException {
        MyDaemonThread myDaemonThread = new MyDaemonThread();
        //如果我们希望当main线程结束后，子线程自动结束
        //,只需将子线程设为守护线程即可
        myDaemonThread.setDaemon(true);
        myDaemonThread.start();
        for( int i = 1; i <= 10; i++) {//main线程
            System.out.println("宝强在辛苦的工作...");
            Thread.sleep(1000);
        }
    }
}
class MyDaemonThread extends Thread {
    public void run() {
        for (; ; ) {//无限循环
            try {
                Thread.sleep(1000);//休眠1000毫秒
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("马蓉和宋喆快乐聊天，哈哈哈~~~");
        }
    }
}
```

17.6 线程的生命周期

17.6.1 JDK 中用 Thread.State 枚举表示了线程的几种状态  
![](https://img-blog.csdnimg.cn/5c6b23b777b944bfa438b3c0ad26207c.png)  
17.6.2 线程状态转换图  
![](https://img-blog.csdnimg.cn/d9adb825ead94cb9a83861da8745b361.png)  
17.8 Synchronized

17.8.1 线程同步机制  
![](https://img-blog.csdnimg.cn/c83c0b72dad24ba4af4c6f36a53db715.png)  
17.8.2 同步具体方法 - Synchronized  
![](https://img-blog.csdnimg.cn/289f5b9494644ed4b86f657c815fea36.png)  
17.9 分析同步原理  
![](https://img-blog.csdnimg.cn/26d62ff01627467faf4cde5d8a91ad30.png)  
17.10 互斥锁

17.10.1 基本介绍  
![](https://img-blog.csdnimg.cn/2cfdc41010ef4848a2131a6a2118c475.png)  
17.10.2 使用互斥锁来解决售票问题  
![](https://img-blog.csdnimg.cn/e30f60bb2624483795605b5902f4eb64.png)

```
package com.hspedu.syn;
public class SellTicket {
    public static void main(String[] args) {
        //测试一把
        SellTicket03 sellTicket03 = new SellTicket03();
        new Thread(sellTicket03).start();//第1个线程-窗口
        new Thread(sellTicket03).start();//第2个线程-窗口
        new Thread(sellTicket03).start();//第3个线程-窗口
    }
}
//实现接口方式, 使用synchronized实现线程同步
class SellTicket03 implements Runnable {
    private int ticketNum = 100;//让多个线程共享 ticketNum
    private boolean loop = true;//控制run方法变量
    Object object = new Object();

    //同步方法（静态的）的锁为当前类本身
    //老韩解读
    //1. public synchronized static void m1() {} 锁是加在 SellTicket03.class
    //2. 如果在静态方法中，实现一个同步代码块.
    /*
        synchronized (SellTicket03.class) {
            System.out.println("m2");
        }
     */
    public synchronized static void m1() {}
    public static  void m2() {
        synchronized (SellTicket03.class) {
            System.out.println("m2");
        }
    }

    //老韩说明
    //1. public synchronized void sell() {} 就是一个同步方法
    //2. 这时锁在 this对象
    //3. 也可以在代码块上写 synchronize ,同步代码块, 互斥锁还是在this对象
    public /*synchronized*/ void sell() { //同步方法, 在同一时刻， 只能有一个线程来执行sell方法
        synchronized (/*this*/ object) {
            if (ticketNum <= 0) {
                System.out.println("售票结束...");
                loop = false;
                return;
            }
            //休眠50毫秒, 模拟
            try {
                Thread.sleep(50);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("窗口 " + Thread.currentThread().getName() + " 售出一张票"
                    + " 剩余票数=" + (--ticketNum));//1 - 0 - -1  - -2
        }
    }
    @Override
    public void run() {
        while (loop) {
            sell();//sell方法是一共同步方法
        }
    }
}
```

17.10.3 注意事项和细节  
![](https://img-blog.csdnimg.cn/9c6906ce70434044a78096874275c4b0.png)  
17.11 线程的死锁

17.11.1 基本介绍  
![](https://img-blog.csdnimg.cn/54888ee321044f7f9b2200d2ed42531f.png)  
17.11.3 应用案例  
![](https://img-blog.csdnimg.cn/a7605dd44b334b5280c706b68fae37f8.png)  
17.12 释放锁

17.12.1 下面操作会释放锁  
![](https://img-blog.csdnimg.cn/4c088fb8e5c0483b8cad771884d6af99.png)  
17.12.2 下面操作不会释放锁  
![](https://img-blog.csdnimg.cn/017703649cc140279c8510b2713ac116.png)  
17.13 本章作业  
![](https://img-blog.csdnimg.cn/72e11eea1c5c436cb246cb4e64ead4ad.png)

```
package com.hspedu.homework;
public class Homework02 {
    public static void main(String[] args) {
        T t = new T();
        Thread thread1 = new Thread(t);
        thread1.setName("t1");
        Thread thread2 = new Thread(t);
        thread2.setName("t2");
        thread1.start();
        thread2.start();
    }
}
//编程取款的线程
//1.因为这里涉及到多个线程共享资源，所以我们使用实现Runnable方式
//2. 每次取出 1000
class T implements  Runnable {
    private int money = 10000;
    @Override
    public void run() {
        while (true) {
            //解读
            //1. 这里使用 synchronized 实现了线程同步
            //2. 当多个线程执行到这里时，就会去争夺 this对象锁
            //3. 哪个线程争夺到(获取)this对象锁，就执行 synchronized 代码块, 执行完后，会释放this对象锁
            //4. 争夺不到this对象锁，就blocked ，准备继续争夺
            //5. this对象锁是非公平锁.
            synchronized (this) {//
                //判断余额是否够
                if (money < 1000) {
                    System.out.println("余额不足");
                    break;
                }
                money -= 1000;
                System.out.println(Thread.currentThread().getName() + " 取出了1000 当前余额=" + money);
            }
            //休眠1s
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

#### 第 19 章 IO 流

19.1 文件

19.1.1 什么是文件  
![](https://img-blog.csdnimg.cn/3eba757dd25944d295987ae12e969fba.png)  
19.1.2 文件流  
![](https://img-blog.csdnimg.cn/b43e68f72fb14480af9c1797c872fd4f.png)  
19.2 常用的文件操作

19.2.1 创建文件对象相关构造器和方法  
![](https://img-blog.csdnimg.cn/b0bf5b7b6e9f4795bd73713c7154ceca.png)

```
package com.hspedu.file;
import org.junit.jupiter.api.Test;
import java.io.*;
public class FileCreate {
    public static void main(String[] args) {}
    //方式1 new File(String pathname)
    @Test
    public void create01() {
        String filePath = "e:\\news1.txt";
        File file = new File(filePath);
        try {
            file.createNewFile();
            System.out.println("文件创建成功");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    //方式2 new File(File parent,String child) //根据父目录文件+子路径构建
    //e:\\news2.txt
    @Test
    public  void create02() {
        File parentFile = new File("e:\\");
        String fileName = "news2.txt";
        //这里的file对象，在java程序中，只是一个对象，创建在内存中
        //只有执行了createNewFile 方法，才会真正的，在磁盘创建该文件
        File file = new File(parentFile, fileName);
        try {
            file.createNewFile();
            System.out.println("创建成功~");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    //方式3 new File(String parent,String child) //根据父目录+子路径构建
    @Test
    public void create03() {
        String parentPath = "e:\\";
        String fileName = "news4.txt";
        File file = new File(parentPath, fileName);
        try {
            file.createNewFile();
            System.out.println("创建成功~");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

19.2.2 获取文件的相关信息  
![](https://img-blog.csdnimg.cn/58e365c9e8c8471f86aca0c93cddc4e4.png)

```
package com.hspedu.file;
import org.junit.jupiter.api.Test;
import java.io.File;
public class FileInformation {
    public static void main(String[] args) {}
    
    //获取文件的信息
    @Test
    public void info() {
        //先创建文件对象
        File file = new File("e:\\news1.txt");
        //注意，这里没有用createNewFile方法，因为这并不是在创建文件，而是创建这个已经存在的文件的一个对象，来对这个文件进行一些操作
        //调用相应的方法，得到对应信息
        System.out.println("文件名字=" + file.getName());
        //getName、getAbsolutePath、getParent、length、exists、isFile、isDirectory
        System.out.println("文件绝对路径=" + file.getAbsolutePath());
        System.out.println("文件父级目录=" + file.getParent());
        System.out.println("文件大小(字节)=" + file.length());
        System.out.println("文件是否存在=" + file.exists());//T
        System.out.println("是不是一个文件=" + file.isFile());//T
        System.out.println("是不是一个目录=" + file.isDirectory());//F
    }
}
```

19.2.4 目录的操作和文件删除  
![](https://img-blog.csdnimg.cn/518729a08e0c4ddba78e86b3ed9f3936.png)  
![](https://img-blog.csdnimg.cn/1565aa185e2b48079b1055bb5e2ac083.png)

```
package com.hspedu.file;
import org.junit.jupiter.api.Test;
import java.io.File;
import java.io.InputStream;
import java.io.OutputStream;
public class Directory_ {
    public static void main(String[] args) {}
    
    //判断 d:\\news1.txt 是否存在，如果存在就删除
    @Test
    public void m1() {
        String filePath = "e:\\news1.txt";
        File file = new File(filePath);
        if (file.exists()) {
            if (file.delete()) {
                System.out.println(filePath + "删除成功");
            } else {
                System.out.println(filePath + "删除失败");
            }
        } else {
            System.out.println("该文件不存在...");
        }

    }

    //判断 D:\\demo02 是否存在，存在就删除，否则提示不存在
    //这里我们需要体会到，在java编程中，目录也被当做文件
    @Test
    public void m2() {
        String filePath = "D:\\demo02";
        File file = new File(filePath);
        if (file.exists()) {
            if (file.delete()) {
                System.out.println(filePath + "删除成功");
            } else {
                System.out.println(filePath + "删除失败");
            }
        } else {
            System.out.println("该目录不存在...");
        }
    }

    //判断 D:\\demo\\a\\b\\c 目录是否存在，如果存在就提示已经存在，否则就创建
    @Test
    public void m3() {
        String directoryPath = "D:\\demo\\a\\b\\c";
        File file = new File(directoryPath);
        if (file.exists()) {
            System.out.println(directoryPath + "存在..");
        } else {
            if (file.mkdirs()) { //创建一级目录使用mkdir() ，创建多级目录使用mkdirs()
                System.out.println(directoryPath + "创建成功..");
            } else {
                System.out.println(directoryPath + "创建失败...");
            }
        }
    }
}
```

19.3 IO 流原理及流的分类

19.3.1 Java IO 流原理  
![](https://img-blog.csdnimg.cn/e4d3c5b83f9043e58235a8641f4809c2.png)  
![](https://img-blog.csdnimg.cn/b4a47bcec75340aead70d05d0013b62c.png)  
19.3.2 流的分类  
![](https://img-blog.csdnimg.cn/cc041fd97db145aba944c9d5fa023ca6.png)

```
下面四个都是抽象类
    InputStream
    OutputStream
    Reader //字符输入流
    Writer  //字符输出流
```

19.4 IO 流体系图 - 常用的类

19.4.1 IO 流体系图  
![](https://img-blog.csdnimg.cn/01399f5e466147a69952416b3e7cf020.png)  
19.4.2 InputStream 介绍  
![](https://img-blog.csdnimg.cn/73671968a7f74bd2ba38af1091e724aa.png)  
19.4.3 FileInputStream 介绍  
![](https://img-blog.csdnimg.cn/1d8081b8ebb9486083ba7bed60d6acad.png)  
![](https://img-blog.csdnimg.cn/bf03de95b8bb4714b8b7194d8add2f9d.png)

```
package com.hspedu.inputstream_;
import org.junit.jupiter.api.Test;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
/**
 * 演示FileInputStream的使用(字节输入流 文件--> 程序)
 */
public class FileInputStream_ {
    public static void main(String[] args) {}
    /**
     * 演示读取文件...
     * 单个字节的读取，效率比较低
     * -> 使用 read(byte[] b)
     */
    @Test
    public void readFile01() {
        String filePath = "e:\\hello.txt";
        int readData = 0;
        FileInputStream fileInputStream = null;
        try {
            //创建 FileInputStream 对象，用于读取 文件
            fileInputStream = new FileInputStream(filePath);
            //从该输入流读取一个字节的数据。 如果没有输入可用，此方法将阻止。
            //如果返回-1 , 表示读取完毕
            while ((readData = fileInputStream.read()) != -1) {
                System.out.print((char)readData);//转成char显示
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            //关闭文件流，释放资源.
            try {
                fileInputStream.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
    /**
     * 使用 read(byte[] b) 读取文件，提高效率
     */
    @Test
    public void readFile02() {
        String filePath = "e:\\hello.txt";
        //字节数组
        byte[] buf = new byte[8]; //一次读取8个字节.
        int readLen = 0;
        FileInputStream fileInputStream = null;
        try {
            //创建 FileInputStream 对象，用于读取 文件
            fileInputStream = new FileInputStream(filePath);
            //从该输入流读取最多b.length字节的数据到字节数组。 此方法将阻塞，直到某些输入可用。
            //如果返回-1 , 表示读取完毕
            //如果读取正常, 返回实际读取的字节数
            while ((readLen = fileInputStream.read(buf)) != -1) {
                System.out.print(new String(buf, 0, readLen));//显示
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            //关闭文件流，释放资源.
            try {
                fileInputStream.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```

19.4.3 FileOutputStream 介绍  
![](https://img-blog.csdnimg.cn/e2565491bd4b44808d23622ec2a8d977.png)  
![](https://img-blog.csdnimg.cn/177cfd9043654e6c8994aab45c53f10f.png)

```
package com.hspedu.outputstream_;
import org.junit.jupiter.api.Test;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
public class FileOutputStream01 {
    public static void main(String[] args) {}
    /**
     * 演示使用FileOutputStream 将数据写到文件中,
     * 如果该文件不存在，则创建该文件
     */
    @Test
    public void writeFile() {
        //创建 FileOutputStream对象
        String filePath = "e:\\a.txt";
        FileOutputStream fileOutputStream = null;
        try {
            //得到 FileOutputStream对象 对象
            //老师说明
            //1. new FileOutputStream(filePath) 创建方式，当写入内容时，会覆盖原来的内容
            //2. new FileOutputStream(filePath, true) 创建方式，当写入内容时，是追加到文件后面
            //不带 append 时：1.不论创建文件字节输出流前磁盘上是否有该文件，最终都会通过当前字节文件输出流在磁盘上创建文件 2.覆盖的不是内容，而是直接替换文件。简而言之，如果不带 append 就是在磁盘上面新创建一个文件(不论是否已存在)然后打开操作，覆盖是发生在文件层面，而不是文件里面的内容；如果 true 就是打开磁盘上已有的文件在其内容末尾进行操作
            fileOutputStream = new FileOutputStream(filePath, true);
            //写入一个字节
            //fileOutputStream.write('H');//
            //写入字符串
            String str = "hsp,world!";
            //str.getBytes() 可以把 字符串-> 字节数组
            //fileOutputStream.write(str.getBytes());
            /*
            write(byte[] b, int off, int len) 将 len字节从位于偏移量 off的指定字节数组写入此文件输出流
             */
            fileOutputStream.write(str.getBytes(), 0, 3);
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                fileOutputStream.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```

![](https://img-blog.csdnimg.cn/da9bd824b3504cedb0c5426d13abe9bb.png)

```
package com.hspedu.outputstream_;
import com.hspedu.inputstream_.FileInputStream_;
import java.io.*;
public class FileCopy {
    public static void main(String[] args) {
        //完成 文件拷贝，将 e:\\Koala.jpg 拷贝 c:\\
        //思路分析
        //1. 创建文件的输入流 , 将文件读入到程序
        //2. 创建文件的输出流， 将读取到的文件数据，写入到指定的文件.
        String srcFilePath = "e:\\Koala.jpg";
        String destFilePath = "e:\\Koala3.jpg";
        FileInputStream fileInputStream = null;
        FileOutputStream fileOutputStream = null;
        try {
            fileInputStream = new FileInputStream(srcFilePath);
            fileOutputStream = new FileOutputStream(destFilePath);
            //定义一个字节数组,提高读取效果
            byte[] buf = new byte[1024];
            int readLen = 0;
            while ((readLen = fileInputStream.read(buf)) != -1) {
                //读取到后，就写入到文件 通过 fileOutputStream
                //即，是一边读，一边写
                fileOutputStream.write(buf, 0, readLen);//一定要使用这个方法
                //这里写入并不会覆盖，因为没有关闭输出流
            }
            System.out.println("拷贝ok~");
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                //关闭输入流和输出流，释放资源
                if (fileInputStream != null) {
                    fileInputStream.close();
                }
                if (fileOutputStream != null) {
                    fileOutputStream.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```

19.4.6 FileReader 介绍和相关方法  
![](https://img-blog.csdnimg.cn/99a6ac90da8445d18c9d1654ae2d7781.png)  
![](https://img-blog.csdnimg.cn/616022355c93434f95cbdff00e375c9d.png)

```
package com.hspedu.reader_;
import org.junit.jupiter.api.Test;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
public class FileReader_ {
    public static void main(String[] args) {}
    
    /**
     * 单个字符读取文件
     */
    @Test
    public void readFile01() {
        String filePath = "e:\\story.txt";
        FileReader fileReader = null;
        int data = 0;
        //1. 创建FileReader对象
        try {
            fileReader = new FileReader(filePath);
            //循环读取 使用read, 单个字符读取
            while ((data = fileReader.read()) != -1) {
                System.out.print((char) data);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                if (fileReader != null) {
                    fileReader.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }

    /**
     * 字符数组读取文件
     */
    @Test
    public void readFile02() {
        System.out.println("~~~readFile02 ~~~");
        String filePath = "e:\\story.txt";
        FileReader fileReader = null;
        int readLen = 0;
        char[] buf = new char[8];
        //1. 创建FileReader对象
        try {
            fileReader = new FileReader(filePath);
            //循环读取 使用read(buf), 返回的是实际读取到的字符数
            //如果返回-1, 说明到文件结束
            while ((readLen = fileReader.read(buf)) != -1) {
                System.out.print(new String(buf, 0, readLen));
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                if (fileReader != null) {
                    fileReader.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```

19.4.7 FileWriter 介绍和相关方法  
![](https://img-blog.csdnimg.cn/9fa1620dadc4457994b944ac69d641e6.png)  
![](https://img-blog.csdnimg.cn/4ae78b3c73c4417a84d746e95c1526b7.png)

```
package com.hspedu.writer_;
import java.io.FileWriter;
import java.io.IOException;
public class FileWriter_ {
    public static void main(String[] args) {
        String filePath = "e:\\note.txt";
        //创建FileWriter对象
        FileWriter fileWriter = null;
        char[] chars = {'a', 'b', 'c'};
        try {
            fileWriter = new FileWriter(filePath);//默认是覆盖写入
//            3) write(int):写入单个字符
            fileWriter.write('H');
//            4) write(char[]):写入指定数组
            fileWriter.write(chars);
//            5) write(char[],off,len):写入指定数组的指定部分
            fileWriter.write("韩顺平教育".toCharArray(), 0, 3);
//            6) write（string）：写入整个字符串
            fileWriter.write(" 你好北京~");
            fileWriter.write("风雨之后，定见彩虹");
//            7) write(string,off,len):写入字符串的指定部分
            fileWriter.write("上海天津", 0, 2);
            //在数据量大的情况下，可以使用循环操作.
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            //对应FileWriter , 一定要关闭流，或者flush才能真正的把数据写入到文件
            //老韩看源码就知道原因.
            /*
                看看源码
                private void writeBytes() throws IOException {
        this.bb.flip();
        int var1 = this.bb.limit();
        int var2 = this.bb.position();
        assert var2 <= var1;
        int var3 = var2 <= var1 ? var1 - var2 : 0;
        if (var3 > 0) {
            if (this.ch != null) {
                assert this.ch.write(this.bb) == var3 : var3;
            } else {
                this.out.write(this.bb.array(), this.bb.arrayOffset() + var2, var3);
            }
        }
        this.bb.clear();
    }
             */
            try {
                //fileWriter.flush();
                //关闭文件流，等价 flush() + 关闭
                fileWriter.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
        System.out.println("程序结束...");
    }
}
```

19.5 节点流和处理流

19.5.1 基本介绍  
![](https://img-blog.csdnimg.cn/790dc67ac05244f597b65ef54b36e96c.png)  
19.5.2 节点流和处理流一览图  
![](https://img-blog.csdnimg.cn/9a6c1b8cc592494c8f02ba47ac0d9041.png)  
![](https://img-blog.csdnimg.cn/a718eecb7aca4eee9e20349c76c986d7.png)  
19.5.3 节点流和处理流的区别和联系  
![](https://img-blog.csdnimg.cn/cf47ccf1e7f640b69c50df2c1dfd56bc.png)  
19.5.4 处理流的功能主要体现在以下两个方面:  
![](https://img-blog.csdnimg.cn/53ce857e5cfd42df858ec3707d36fe3b.png)  
19.5.5 处理流 - BufferedReader 和 BufferedWriter  
![](https://img-blog.csdnimg.cn/4a3cfe800ffd4aa28afee3e5ec9a4b4d.png)  
![](https://img-blog.csdnimg.cn/b77b54f979c841678655b5a03b52758c.png)

```
package com.hspedu.reader_;
import java.io.BufferedReader;
import java.io.FileReader;
/**
 * 演示bufferedReader 使用
 */
public class BufferedReader_ {
    public static void main(String[] args) throws Exception {
        String filePath = "e:\\a.java";
        //创建bufferedReader
        BufferedReader bufferedReader = new BufferedReader(new FileReader(filePath));
        //读取
        String line; //按行读取, 效率高
        //说明
        //1. bufferedReader.readLine() 是按行读取文件
        //2. 当返回null 时，表示文件读取完毕
        while ((line = bufferedReader.readLine()) != null) {
            System.out.println(line);
        }
        //关闭流, 这里注意，只需要关闭 BufferedReader ，因为底层会自动的去关闭 节点流
        //FileReader。
        /*
            public void close() throws IOException {
                synchronized (lock) {
                    if (in == null)
                        return;
                    try {
                        in.close();//in 就是我们传入的 new FileReader(filePath), 关闭了.
                    } finally {
                        in = null;
                        cb = null;
                    }
                }
            }
         */
        bufferedReader.close();
    }
}
```

![](https://img-blog.csdnimg.cn/620aacda411143128803a746a07c50f7.png)

```
package com.hspedu.writer_;
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;
/**
 * 演示BufferedWriter的使用
 */
public class BufferedWriter_ {
    public static void main(String[] args) throws IOException {
        String filePath = "e:\\ok.txt";
        //创建BufferedWriter
        //说明:
        //1. new FileWriter(filePath, true) 表示以追加的方式写入
        //2. new FileWriter(filePath) , 表示以覆盖的方式写入
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(filePath));
        bufferedWriter.write("hello, 韩顺平教育!");
        bufferedWriter.newLine();//插入一个当前系统(windows、Linux等)对应的换行符
        bufferedWriter.write("hello2, 韩顺平教育!");
        bufferedWriter.newLine();
        bufferedWriter.write("hello3, 韩顺平教育!");
        bufferedWriter.newLine();
        //说明：关闭外层流即可 ， 传入的 new FileWriter(filePath) ,会在底层关闭
        bufferedWriter.close();
    }
}
```

![](https://img-blog.csdnimg.cn/5f13ef1ca3f74034851887ee28f12122.png)

```
package com.hspedu.writer_;
import java.io.*;
public class BufferedCopy_ {
    public static void main(String[] args) {
        //老韩说明
        //1. BufferedReader 和 BufferedWriter 是按照字符操作
        //2. 不要去操作 二进制文件[声音，视频，doc, pdf ], 可能造成文件损坏
        String srcFilePath = "e:\\a.java";
        String destFilePath = "e:\\a2.java";
//        String srcFilePath = "e:\\0245_韩顺平零基础学Java_引出this.avi";
//        String destFilePath = "e:\\a2韩顺平.avi";
        BufferedReader br = null;
        BufferedWriter bw = null;
        String line;
        try {
            br = new BufferedReader(new FileReader(srcFilePath));
            bw = new BufferedWriter(new FileWriter(destFilePath));
            //说明: readLine 读取一行内容，但是没有换行
            while ((line = br.readLine()) != null) {
                //每读取一行，就写入
                bw.write(line);
                //插入一个换行
                bw.newLine();
            }
            System.out.println("拷贝完毕...");
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            //关闭流
            try {
                if(br != null) {
                    br.close();
                }
                if(bw != null) {
                    bw.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```

19.5.6 处理流 - BufferedInputStream  
![](https://img-blog.csdnimg.cn/8ee131bdbe9f451ebe7aa632f5c559c6.png)  
![](https://img-blog.csdnimg.cn/bc63a021129848338e4895d56190dc95.png)  
19.5.7 处理流 - BufferedOutputStream  
![](https://img-blog.csdnimg.cn/64415dfb4cfb4420866be9dfc4ccd825.png)  
![](https://img-blog.csdnimg.cn/43176eca05864444abf3b35beda1e6f4.png)  
19.5.8 应用案例  
![](https://img-blog.csdnimg.cn/39f827a74734497bbfcdc344215d3ab3.png)

```
package com.hspedu.outputstream_;
import java.io.*;
/**
 * 演示使用BufferedOutputStream 和 BufferedInputStream使用
 * 使用他们，可以完成二进制文件拷贝.
 * 思考：字节流可以操作二进制文件，可以操作文本文件吗？当然可以
 */
public class BufferedCopy02 {
    public static void main(String[] args) {
//        String srcFilePath = "e:\\Koala.jpg";
//        String destFilePath = "e:\\hsp.jpg";
//        String srcFilePath = "e:\\0245_韩顺平零基础学Java_引出this.avi";
//        String destFilePath = "e:\\hsp.avi";
        String srcFilePath = "e:\\a.java";
        String destFilePath = "e:\\a3.java";

        //创建BufferedOutputStream对象BufferedInputStream对象
        BufferedInputStream bis = null;
        BufferedOutputStream bos = null;
        try {
            //因为 FileInputStream  是 InputStream 子类
            bis = new BufferedInputStream(new FileInputStream(srcFilePath));
            bos = new BufferedOutputStream(new FileOutputStream(destFilePath));
            //循环的读取文件，并写入到 destFilePath
            byte[] buff = new byte[1024];
            int readLen = 0;
            //当返回 -1 时，就表示文件读取完毕
            while ((readLen = bis.read(buff)) != -1) {
                bos.write(buff, 0, readLen);
            }
            System.out.println("文件拷贝完毕~~~");
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            //关闭流 , 关闭外层的处理流即可，底层会去关闭节点流
            try {
                if(bis != null) {
                    bis.close();
                }
                if(bos != null) {
                    bos.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```

19.5.9 对象流 - ObjectInputStream 和 ObjectOutputStream  
![](https://img-blog.csdnimg.cn/7b6ea451002b41a0a2e9705cf54f8f19.png)  
![](https://img-blog.csdnimg.cn/efc3f48a000547c6aa8539f8c5b3fdeb.png)  
![](https://img-blog.csdnimg.cn/8e0066ca067e428ca4d2b8887bfdf3da.png)  
![](https://img-blog.csdnimg.cn/1e100331a83c48959bb67a9195d33f7b.png)  
![](https://img-blog.csdnimg.cn/deb300c05d424805b4974ec9e27a5549.png)  
![](https://img-blog.csdnimg.cn/392b46be86174e8bbeb3832a4c5df487.png)  
ObjectOutStream_.java

```
package com.hspedu.outputstream_;
import java.io.FileOutputStream;
import java.io.ObjectOutputStream;
import java.io.Serializable;
/**
 * 演示ObjectOutputStream的使用, 完成数据的序列化
 */
public class ObjectOutStream_ {
    public static void main(String[] args) throws Exception {
        //序列化后，保存的文件格式，不是存文本，而是按照他的格式来保存
        String filePath = "e:\\data.dat";
        ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream(filePath));
        //序列化数据到 e:\data.dat
        oos.writeInt(100);// int -> Integer (实现了 Serializable)
        oos.writeBoolean(true);// boolean -> Boolean (实现了 Serializable)
        oos.writeChar('a');// char -> Character (实现了 Serializable)
        oos.writeDouble(9.5);// double -> Double (实现了 Serializable)
        oos.writeUTF("韩顺平教育");//String
        //保存一个dog对象
        oos.writeObject(new Dog("旺财", 10, "日本", "白色"));
        oos.close();
        System.out.println("数据保存完毕(序列化形式)");
    }
}
```

![](https://img-blog.csdnimg.cn/fa6cfab9c5ad448285100e6362ad9d33.png)  
ObjectInputStream_.java

```
package com.hspedu.inputstream_;
import com.hspedu.outputstream_.Dog;
import java.io.*;
public class ObjectInputStream_ {
    public static void main(String[] args) throws IOException, ClassNotFoundException {
        //指定反序列化的文件
        String filePath = "e:\\data.dat";
        ObjectInputStream ois = new ObjectInputStream(new FileInputStream(filePath));
        //读取
        //老师解读
        //1. 读取(反序列化)的顺序需要和你保存数据(序列化)的顺序一致
        //2. 否则会出现异常
        System.out.println(ois.readInt());
        System.out.println(ois.readBoolean());
        System.out.println(ois.readChar());
        System.out.println(ois.readDouble());
        System.out.println(ois.readUTF());
        //dog 的编译类型是 Object , dog 的运行类型是 Dog
        Object dog = ois.readObject();
        System.out.println("运行类型=" + dog.getClass());
        System.out.println("dog信息=" + dog);//底层 Object -> Dog

        //这里是特别重要的细节:
        //1. 如果我们希望调用Dog的方法, 需要向下转型
        //2. 需要我们将Dog类的定义放在可以引用的位置
        Dog dog2 = (Dog)dog;
        System.out.println(dog2.getName()); //旺财..
        //关闭流, 关闭外层流即可，底层会关闭 FileInputStream 流
        ois.close();
    }
}
```

idea 里有个插件可以进行翻译，极其好用，叫做 Translation。鼠标点到你需要翻译的单词位置或者选择需要翻译的句子用 ctrl+shift+y 就能翻译。并且在你起变量名字时，写中文使用快捷键，也可以翻译成英文，安利给你们。在 idea 里面的 file–》setting–》plhgins 搜索下载

![](https://img-blog.csdnimg.cn/d13055cf605b405388f3ea04392eed46.png)  
Dog.java

```
package com.hspedu.outputstream_;
import java.io.Serializable;
//如果需要序列化某个类的对象，实现 Serializable
public class Dog implements Serializable {
    private String name;
    private int age;
    //序列化对象时，默认将里面所有属性都进行序列化，但除了static或transient修饰的成员
    private static String nation;
    private transient String color;
    //序列化对象时，要求里面属性的类型也需要实现序列化接口
    private Master master = new Master();
    //serialVersionUID 序列化的版本号，可以提高兼容性
    private static final long serialVersionUID = 1L;
    public Dog(String name, int age, String nation, String color) {
        this.name = name;
        this.age = age;
        this.color = color;
        this.nation = nation;
    }
    @Override
    public String toString() {
        return "Dog{" +
                " + name + '\'' +
                ", age=" + age +
                ", color='" + color + '\'' +
                '}' + nation + " " +master;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public int getAge() {
        return age;
    }
    public void setAge(int age) {
        this.age = age;
    }
}
```

Master.java

```
package com.hspedu.outputstream_;
import java.io.Serializable;
public class Master implements Serializable {}
```

19.5.10 标准输入输出流  
![](https://img-blog.csdnimg.cn/2695671644944b419acbfebead74e9d7.png)  
![](https://img-blog.csdnimg.cn/be66b241b11f4d9c81d3a6afc2164554.png)

```
package com.hspedu.standard;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.Scanner;
public class InputAndOutput {
    public static void main(String[] args) {
        //System 类 的 public final static InputStream in = null;
        // System.in 编译类型   InputStream
        // System.in 运行类型   BufferedInputStream
        // 表示的是标准输入 键盘
        System.out.println(System.in.getClass());

        //老韩解读
        //1. public final static PrintStream out = null;
        //2. 编译类型 PrintStream
        //3. 运行类型 PrintStream
        //4. 表示标准输出 显示器
        System.out.println(System.out.getClass());
        System.out.println("hello, 韩顺平教育~");
        Scanner scanner = new Scanner(System.in);
        System.out.println("输入内容");
        String next = scanner.next();
        System.out.println("next=" + next);
    }
}
```

19.5.11 转换流 - InputStreamReader 和 OutputStreamWriter  
![](https://img-blog.csdnimg.cn/e228edceebc54d7ab194d85a21724d60.png)

```
package com.hspedu.transformation;
import java.io.*;
/**
 * 看一个中文乱码问题
 */
public class CodeQuestion {
    public static void main(String[] args) throws IOException {
        //读取e:\\a.txt 文件到程序
        //思路
        //1.  创建字符输入流 BufferedReader [处理流]
        //2. 使用 BufferedReader 对象读取a.txt
        //3. 默认情况下，读取文件是按照 utf-8 编码
        String filePath = "e:\\a.txt";
        BufferedReader br = new BufferedReader(new FileReader(filePath));
        String s = br.readLine();
        System.out.println("读取到的内容: " + s);
        br.close();
    }
```

a.txt 默认是 UTF-8 编码，但如果改成其它编码（例如：ANSI(国标码，在中国 windows 系统下一般是 GBK)）后，运行程序输出的数据就会乱码  
![](https://img-blog.csdnimg.cn/ba7aefab79f54304a7a7b55a65c50bb0.png)  
![](https://img-blog.csdnimg.cn/d0acfc80cd7244f493dd2425d4df9523.png)  
![](https://img-blog.csdnimg.cn/b79d7236798242498a5b3c61401e3c6f.png)  
![](https://img-blog.csdnimg.cn/5a1938678a104735b834de7b1b0cd169.png)  
![](https://img-blog.csdnimg.cn/b0b64a324e984f978a4ce980bf88942f.png)  
![](https://img-blog.csdnimg.cn/4d761882fc6245f6a8b73a2fa26213d8.png)

```
package com.hspedu.transformation;
import java.io.*;
/**
 * 演示使用 InputStreamReader 转换流解决中文乱码问题
 * 将字节流 FileInputStream 转成字符流  InputStreamReader, 指定编码 gbk/utf-8
 */
public class InputStreamReader_ {
    public static void main(String[] args) throws IOException {
        String filePath = "e:\\a.txt";
        //解读
        //1. 把 FileInputStream 转成 InputStreamReader
        //2. 指定编码 gbk
        //InputStreamReader isr = new InputStreamReader(new FileInputStream(filePath), "gbk");
        //3. 把 InputStreamReader 传入 BufferedReader
        //BufferedReader br = new BufferedReader(isr);

        //将2 和 3 合在一起
        BufferedReader br = new BufferedReader(new InputStreamReader(new FileInputStream(filePath), "gbk"));
        //4. 读取
        String s = br.readLine();
        System.out.println("读取内容=" + s);
        //5. 关闭外层流
        br.close();
    }
}
```

![](https://img-blog.csdnimg.cn/bb8a69ad44784a0a9f4671d0cb0f97d7.png)

```
package com.hspedu.transformation;
import java.io.*;
/**
 * 演示 OutputStreamWriter 使用
 * 把FileOutputStream 字节流，转成字符流 OutputStreamWriter
 * 指定处理的编码 gbk/utf-8/utf8
 */
public class OutputStreamWriter_ {
    public static void main(String[] args) throws IOException {
        String filePath = "e:\\hsp.txt";
        String charSet = "utf-8";
        OutputStreamWriter osw = new OutputStreamWriter(new FileOutputStream(filePath), charSet);
        osw.write("hi, 韩顺平教育");
        osw.close();
        System.out.println("按照 " + charSet + " 保存文件成功~");
    }
}
```

19.6 打印流 - PrintStream 和 PrintWriter  
![](https://img-blog.csdnimg.cn/ddb253ee2c724404a4c225b12a9ce250.png)  
![](https://img-blog.csdnimg.cn/209172a3dcfb4112ae7d92385fcd4ffe.png)  
![](https://img-blog.csdnimg.cn/ed4623bc06224944812f187486b4984e.png)  
PrintStream_.java

```
package com.hspedu.printstream;
import java.io.IOException;
import java.io.PrintStream;
/**
 * 演示PrintStream （字节打印流/输出流）
 */
public class PrintStream_ {
    public static void main(String[] args) throws IOException {
        PrintStream out = System.out;
        //在默认情况下，PrintStream 输出数据的位置是 标准输出，即显示器
        /*
             public void print(String s) {
                if (s == null) {
                    s = "null";
                }
                write(s);
            }
         */
        out.print("john, hello");
        //因为print底层使用的是write , 所以我们可以直接调用write进行打印/输出，本质是一样的
        out.write("韩顺平,你好".getBytes());
        out.close();

        //我们可以去修改打印流输出的位置/设备
        //1. 输出修改成到 "e:\\f1.txt"
        //2. "hello, 韩顺平教育~" 就会输出到 e:\f1.txt
        //3. public static void setOut(PrintStream out) {
        //        checkIO();
        //        setOut0(out); // native 方法，修改了out
        //   }
        System.setOut(new PrintStream("e:\\f1.txt"));
        System.out.println("hello, 韩顺平教育~");
    }
}
```

PrintWriter_.java

```
package com.hspedu.transformation;
import java.io.FileWriter;
import java.io.IOException;
import java.io.PrintWriter;
/**
 * 演示 PrintWriter 使用方式
 */
public class PrintWriter_ {
    public static void main(String[] args) throws IOException {
        //PrintWriter printWriter = new PrintWriter(System.out);
        PrintWriter printWriter = new PrintWriter(new FileWriter("e:\\f2.txt"));
        printWriter.print("hi, 北京你好~~~~");
        printWriter.close();//flush + 关闭流, 才会将数据写入到文件..
    }
}
```

19.7 Properties 类

19.7.2 基本介绍  
![](https://img-blog.csdnimg.cn/bb4e5b6ee8e145eeabffb1cdff37c079.png)  
![](https://img-blog.csdnimg.cn/ae41f8ba8f58452aa132a7b3e93f0d4a.png)  
![](https://img-blog.csdnimg.cn/f3dd3bba34354d16935500bce98aa04c.png)  
Properties02.java

```
package com.hspedu.properties_;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;
import java.util.Properties;
public class Properties02 {
    public static void main(String[] args) throws IOException {
        //使用Properties 类来读取mysql.properties 文件
        //1. 创建Properties 对象
        Properties properties = new Properties();
        //2. 加载指定配置文件
        properties.load(new FileReader("src\\mysql.properties"));
        //3. 把k-v显示控制台
        properties.list(System.out);
        //4. 根据key 获取对应的值
        String user = properties.getProperty("user");
        String pwd = properties.getProperty("pwd");
        System.out.println("用户名=" + user);
        System.out.println("密码是=" + pwd);
    }
}
```

Properties03.java

```
package com.hspedu.properties_;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.util.Properties;
public class Properties03 {
    public static void main(String[] args) throws IOException {
        //使用Properties 类来创建 配置文件, 修改配置文件内容
        Properties properties = new Properties();
        //创建
        //1.如果该文件没有key 就是创建
        //2.如果该文件有key ,就是修改
        /*
            Properties 父类是 Hashtable ， 底层就是Hashtable 核心方法
            public synchronized V put(K key, V value) {
                // Make sure the value is not null
                if (value == null) {
                    throw new NullPointerException();
                }
                // Makes sure the key is not already in the hashtable.
                Entry<?,?> tab[] = table;
                int hash = key.hashCode();
                int index = (hash & 0x7FFFFFFF) % tab.length;
                @SuppressWarnings("unchecked")
                Entry<K,V> entry = (Entry<K,V>)tab[index];
                for(; entry != null ; entry = entry.next) {
                    if ((entry.hash == hash) && entry.key.equals(key)) {
                        V old = entry.value;
                        entry.value = value;//如果key 存在，就替换
                        return old;
                    }
                }
                addEntry(hash, key, value, index);//如果是新k, 就addEntry
                return null;
            }
         */
        properties.setProperty("charset", "utf8");
        properties.setProperty("user", "汤姆");//注意保存时，是中文的 unicode码值
        properties.setProperty("pwd", "888888");

        //将k-v 存储文件中即可
        properties.store(new FileOutputStream("src\\mysql2.properties"), null);
        System.out.println("保存配置文件成功~");
    }
}
```

其中，setProperty 如果找不到 key 则会变成添加；store 如果已经有了相同文件则会变成覆盖

19.8 本章作业  
![](https://img-blog.csdnimg.cn/d60ec548c39941198f214b3bfe59c9aa.png)

```
package com.hspedu.homework;
import java.io.BufferedWriter;
import java.io.File;
import java.io.FileWriter;
import java.io.IOException;
public class Homework01 {
    public static void main(String[] args) throws IOException {
        String directoryPath = "e:\\mytemp";
        File file = new File(directoryPath);
        if(!file.exists()) {
            //创建
            if(file.mkdirs()) {
                System.out.println("创建 " + directoryPath + " 创建成功" );
            }else {
                System.out.println("创建 " + directoryPath + " 创建失败");
            }
        }
        String filePath  = directoryPath + "\\hello.txt";// e:\mytemp\hello.txt
        file = new File(filePath);
        if(!file.exists()) {
            //创建文件
            if(file.createNewFile()) {
                System.out.println(filePath + " 创建成功~");
                //如果文件存在，我们就使用BufferedWriter 字符输出流输出内容
                BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(file));
                bufferedWriter.write("hello, world~~ 韩顺平教育");
                bufferedWriter.close();
            } else {
                System.out.println(filePath + " 创建失败~");
            }
        } else {
            //如果文件已经存在，给出提示信息
            System.out.println(filePath + " 已经存在，不在重复创建...");
        }
    }
}
```

![](https://img-blog.csdnimg.cn/460fd6ed6e484a6793da87f1f51adb85.png)

```
package com.hspedu.homework;
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
public class Homework02 {
    public static void main(String[] args) {
        String filePath = "e:\\a.txt";
        BufferedReader br = null;
        String line = "";
        int lineNum = 0;
        try {
            br = new BufferedReader(new FileReader(filePath));
            while ((line = br.readLine()) != null) {//循环读取
                System.out.println(++lineNum + line);
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try {
                if(br != null) {
                    br.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```

这里的 get(key) 调用的是其父类 Hashtable 的方法，所以返回的 Object，用其本身的 getProperty 返回的就是 String。get 接收的是 k-v 的 entry 对象，直接用 getProperties 接收的是 k 对应的 v。

![](https://img-blog.csdnimg.cn/3b90a1c8c3fd444bbb5d924ea4628db5.png)

```
package com.hspedu.homework;
import org.junit.jupiter.api.Test;
import java.io.*;
import java.util.Properties;
public class Homework03 {
    public static void main(String[] args) throws IOException {
        String filePath = "src\\dog.properties";
        Properties properties = new Properties();
        properties.load(new FileReader(filePath));
        String name = properties.get("name") + ""; //Object -> String
        int age = Integer.parseInt(properties.get("age") + "");// Object -> int
        String color = properties.get("color") + "";//Object -> String

        Dog dog = new Dog(name, age, color);
        System.out.println("===dog对象信息====");
        System.out.println(dog);

        //将创建的Dog 对象 ，序列化到 文件 dog.dat 文件
        String serFilePath = "e:\\dog.dat";
        ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream(serFilePath));
        oos.writeObject(dog);

        //关闭流
        oos.close();
        System.out.println("dog对象，序列化完成...");
    }
    //再编写一个方法，反序列化dog
    @Test
    public void m1() throws IOException, ClassNotFoundException {
        String serFilePath = "e:\\dog.dat";
        ObjectInputStream ois = new ObjectInputStream(new FileInputStream(serFilePath));
        Dog dog = (Dog)ois.readObject();

        System.out.println("===反序列化后 dog====");
        System.out.println(dog);

        ois.close();
    }
}
class Dog implements  Serializable{
    private String name;
    private int age;
    private String color;
    //省略构造方法和toString方法
}
```