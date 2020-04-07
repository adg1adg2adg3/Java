## 集合
    集合类的两个基本接口为java.util.Collection接口 与 java.util.Map接口。(可以先看顶层类的抽象方法，因为各个底层一定有相应的方法)
### Collection
        1、可以使用多态创建对象（因为各个底层一定有相应的方法）：Collection<数据类型> 对象名称 = new 集合类型;
        2、Collection接口中iterator方法可以返回一个iterator对象，遍历集合元素可以使用：
        *iterator对象中的hasNext与next方法。
        *foreach循环(任何实现了Iterable接口的对象都可以使用foreach循环)。
        *为iterator对象中的forEachRemaining方法中提供一个Lambda表达式。
        3、当我们希望重写Collection接口时，我们可以继承AbstractCollection这个抽象类，开发者基于Collection接口的基础上为AbstractCollection这个抽象类实现了很多功能，我们只需要实现 iterator 与 size 方法即可。
    *<LinkedList>
        4、Java SE1.4为不能进行随机访问的集合实现了RandomAccess标记接口。
        5、LinkedList类中实现了一个特有的ListIterator迭代器。
        6、对于LinkedList：add方法只依赖于迭代器的位置，而remove方法依赖于迭代器的状态。
            *当用一个刚刚由ListIterator方法返回，并且指向链表表头的迭代器调用add操作时，新添加的元素将变成列表的新表头。当迭代器越过链表的最后一个元素时（即 hasNext返回false),添加的元素将变成列表的新表尾。
            *在调用next之后，remove方法确实与BACKSPACE键一样删除了迭代器左侧的元素。但是， 如果调用previous就会将右侧的元素删除掉，并且不能连续调用两次remove。
        7、LinkedList中的get方法做了微小的优化：如果索引大于size()/2就从列表尾端开始搜索元素。
        <hashSet>
        8、在JavaSE8中，数组满时链表变为平衡二叉树。
        9、装填因子超过75%，将会创建一个哈希表长度X2的新表，把所有原先表中的元素(默认长度为16)挪进去。
        10、PriorityQueue总是使用堆排序删除删除集合中最小的元素。
        11、TreeSet使用红黑树。
        12、List接口只有ArrayLIst为多线程，set接口为多线程。
        13、Object有hashCode方法，字符串中"重地"与"通话"的哈希值一样。
        14、HashCode存放自定义元素时要重写HashCode和equals方法。因为两个同一对象有不同地址值，而HashCode和equals方法会造成不同的哈希值与不相等。
        15、java.util.Collections(工具类)。
        16、Collections类内如果要使用sort(List<T> list)方法对自定义类排序时，自定义类必须实Comparable(接口)，重写CompareTo方法。
            *CompareTo方法的排序规则：自己-参数：升序，反之降序。
        17、sort(List<T> list, Comparator<? super T> c)方法对自定义类排序时，要重写Comparator接口的compare方法。
            *compare(T o1,T o2)：o1-o2升序，反之降序。
### Map
        1、有两种实现：HashMap(无序)与TreeMap(有序，仅针对键)。
        2、要迭代处理映射的键和值时，可以在Map的foreach方法中提供一个接收键和值的lambda表达式进行处理。
        3、注意使用	getOrDefault方法、putIfAbsent方法、merge方法。
        
### 迭代器
    java.util.Iterator(接口)
    Collection类中有一个Iterator()方法可以实现此接口，即Iterator可以在Collection类中构造。
    Iterator<数据类型> 对象名 = Collection类对象名.iterator();
    迭代器默认首先指向第0个元素之前的位置。
