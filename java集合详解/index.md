# Java集合详解




# Java集合详解



## 架构图

![img](Java集合详解.assets/65065da428fec838d4e18bb036d70d12.png)

![img](Java集合详解.assets/06373a1175a74ae365f86da14d868d67.png)

![img](Java集合详解.assets/v2-7f402ef358817499ad276455ef470e6e_r.jpg)

![img](Java集合详解.assets/v2-dddfb8f8b30a5573fc790902b3cc8ccf_r.jpg)



## 集合的简单分类

1.collection:

- List接口：一种有序列表的集合，例如，按索引排列的Student的List；
- Set接口：一种保证没有重复元素的集合，例如，所有无重复名称的Student的Set；

2.map: 

- Map：一种通过键值（key-value）查找的映射表集合，例如，根据Student的name查找对应Student的Map。



## Collection

### List

1. ArrayList：底层数据结构是数组，查询快，增删慢，线程不安全，效率高，可以存储重复元素

2. LinkedList 底层数据结构是链表，查询慢，增删快，线程不安全，效率高，可以存储重复元素

3. Vector:底层数据结构是数组，查询快，增删慢，线程安全，效率低，可以存储重复元素

   ![img](Java集合详解.assets/v2-89cebb489a429b2e6f2fc303505ea30d_r.jpg)

### Set

Set集合的特点是：元素不可重复

1. HashSet集合

- 底层数据结构是哈希表(是一个元素为链表的数组)
- 不能保证元素的顺序。
- HashSet不是线程同步的，如果多线程操作HashSet集合，则应通过代码来保证其同步。
- 集合元素值可以是null。
- 影响哈希冲突的条件，首先看哈希值是否相等，然后判断equals是否相等（内容是否相等）

1. TreeSet集合

- A:底层数据结构是红黑树(是一个自平衡的二叉树)
- B:保证元素的排序方式（自然排序），实现Comparable接口

1. LinkedHashSet集合

- A:：底层数据结构由哈希表和链表组成。
- 原来存储是什么顺序，就是什么顺序

> 各Set实现类的性能分析

- HashSet的性能比TreeSet的性能好（特别是添加，查询元素时），因为TreeSet需要额外的红黑树算法维护元素的次序，如果需要一个保持排序的Set时才用TreeSet，否则应该使用HashSet。
- LinkedHashSet是HashSet的子类，由于需要链表维护元素的顺序，所以插入和删除操作比HashSet要慢，但遍历比HashSet快。
- EnumSet是所有Set实现类中性能最好的，但它只能 保存同一个枚举类的枚举值作为集合元素。
- 以上几个Set实现类都是线程不安全的，如果多线程访问，必须手动保证集合的同步性，这在后面的章节中会讲到。

### Queue

![img](Java集合详解.assets/v2-455e27193db059383da3601735015419_r.jpg)



![img](Java集合详解.assets/1453275-20200418230939193-1484285170.png)





### 遍历Collection方式

#### 1.普通for循环遍历（有索引的）

注意set集合是无序的不能使用普通for循环遍历，只能使用增强for或者迭代器遍历

```java
import java.util.*;

public class test{
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<String>();
        list.add("Hello");
        list.add("Java");
        list.add("World");
        for (int i = 0; i < list.size(); i++){
            String s = (String) list.get(i);
            System.out.println(s);
        }
    }
}
```

#### 2.迭代器遍历（除了Map，任何Collection集合都可以遍历，因为Iterable是Collection的顶层接口）

```java
import java.util.*;

public class test{
    public static void main(String[] args) {
        Collection<String> c = new ArrayList<String>();
        c.add("Hello");
        c.add("Java");
        c.add("World");
        //获取迭代器对象
        Iterator<String> it = c.iterator();
        //hasNext()判断是否有下一个元素，如果有就用next()获取
        while(it.hasNext()){
            //获取下一个元素
            String s = it.next();
            System.out.println(s);
        }
    }
}
```

#### 3.增强for（简化的迭代器）

```java
import java.util.*;

public class test{
    public static void main(String[] args) {
        Collection<String> c = new HashSet<String>();
        c.add("Hello");
        c.add("Java");
        c.add("World");
        //高级for遍历集合
        for (String s : c){
            System.out.println(s);
        }

        int[] arr = {1, 2, 3, 4, 5};
        //高级for遍历数组
        for (int a : arr){
            System.out.println(a);
        }
    }
}
```



## Map

1. Map用于保存具有映射关系的数据，Map里保存着两组数据：key和value，它们都可以使任何引用类型的数据，但key不能重复。所以通过指定的key就可以取出对应的value
2. Collection中的集合，元素是孤立存在的(理解为单身)，向集合中存储元素采用一个个元素的方式存储。 Map中的集合，元素是成对存在的(理解为夫妻)。每个元素由键与值两部分组成,通过键可以找对所对应的 值。
3. Collection中的集合称为单列集合，Map 中的集合称为双列集合。需要注意的是，**Map中的集合不能包含重复的键**，**值可以重复;每个键只能对应一个值。**

### Map分类

1. HashMap 非线程安全
2. HashMap：基于哈希表实现。使用HashMap要求添加的键类明确定义了hashCode()和equals()[可以重写hashCode()和equals()]，为了优化HashMap空间的使用，您可以调优初始容量和负载因子。
3. TreeMap：非线程安全基于红黑树实现。TreeMap没有调优选项，因为该树总处于平衡状态。

### 应用场景

HashMap和HashTable:HashMap去掉了HashTable的contains方法，但是加上了containsValue()和containsKey()方法。HashTable是同步的，而HashMap是非同步的，效率上比HashTable要高。HashMap允许空键值，而HashTable不允许。HashMap：适用于Map中插入、删除和定位元素。 Treemap：适用于按自然顺序或自定义顺序遍历键(key)。

### Map主要方法

![img](Java集合详解.assets/v2-a6a84ee86170bec483c91b1e6d748e30_r.jpg)

### 遍历Map方式

#### 1.通过键找值

1. 使用keySet() ，把Map集合中的所有的key取出来，存入到一个Set集合中
2. 遍历set集合，获取到Map集合中的每一 个key
3. 通过Map集合中的V get(0bject key)， 获取到所有的Value值，输出

```java
public class MapTest02 {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<>();
        map. put( "赵丽颖", 168);
        map. put("杨颖" ,165);
        map. put("林志颖" ,155);
        Set<String> Set = map.keySet();//返回的是一个set集合
        for (String key : Set) {
            Integer value = map.get(key);
            System.out.println(key+" "+value);
        }
    }
}
```

#### 2.使用Entry对象

1. 使用Map集合中的entrySet()方法，把集合中多个Entry对象取出来，存储到一个Set 集合中
2. 遍历Set集合，获取到每一个Entry
3. 调用Entry中的getKey()和IgetValue()方法获取键和值

```java
public class MapTest03 {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<>();
        map. put( "赵丽颖", 168);
        map. put("杨颖" ,165);
        map. put("林志颖" ,155);
        //获取map中的entry对象
        Set<Map.Entry<String, Integer>> set = map.entrySet();
        //从entry中获取key，value
        for (Map.Entry<String, Integer> entry : set) {
            System.out.println(entry.getKey()+entry.getValue());
        }
    }
}
```



## 一些小结论

- 如果是集合类型，有List和Set供我们选择。List的特点是插入有序的，元素是可重复的。Set的特点是插入无序的，元素不可重复的。至于选择哪个实现类来作为我们的存储容器，我们就得看具体的应用场景。是希望可重复的就得用List，选择List下常见的子类。是希望不可重复，选择Set下常见的子类。

- 如果是Key-Value型，那我们会选择Map。如果要保持插入顺序的，我们可以选择LinkedHashMap，如果不需要则选择HashMap，如果要排序则选择TreeMap。

  

## 集合与数组的区别

- 1:长度的区别

- - 数组的长度固定
  - 集合的长度可变

- 2:内容不同

- - 数组存储的是同一种类型的元素
  - 集合可以存储不同类型的元素(但是一般我们不这样干..)

- 3:元素的数据类型

- - 数组可以存储基本数据类型,也可以存储引用类型
  - 集合只能存储引用类型(你存储的是简单的int，它会自动装箱成Integer)




