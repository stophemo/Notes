## 原文链接

**[Tobebetterjavaer](https://tobebetterjavaer.com/home.html)** 



## 字符串

### 源码

```java
public final class String
    implements java.io.Serializable, Comparable<String>, CharSequence {
    @Stable
    private final byte[] value;
    private final byte coder;
    private int hash;
}
```

“第一，String 类是 final 的，意味着它不能被子类继承。”

“第二，String 类实现了 Serializable 接口，意味着它可以序列化。”

“第三，String 类实现了 Comparable 接口，意味着最好不要用‘==’来比较两个字符串是否相等，而应该用 `compareTo()` 方法去比较。”

“第四，StringBuffer、StringBuilder 和 String 一样，都实现了 CharSequence 接口，所以它们仨属于近亲。由于 String 是不可变的，所以遇到字符串拼接的时候就可以考虑一下 String 的另外两个好兄弟，StringBuffer 和 StringBuilder，它俩是可变的。”

“第五，Java 9 以前，String 是用 char 型数组实现的，之后改成了 byte 型数组实现，并增加了 coder 来表示编码。在 Latin1 字符为主的程序里，可以把 String 占用的内存减少一半。当然，天下没有免费的午餐，这个改进在节省内存的同时引入了编码检测的开销。”

“第六，每一个字符串都会有一个 hash 值，这个哈希值在很大概率是不会重复的，因此 String 很适合来作为 HashMap 的键值。”

### 字符串不可变性

- String 类被 final 关键字修饰，所以它不会有子类，这就意味着没有子类可以重写它的方法，改变它的行为。
- String 类的数据存储在 `byte[]` 数组中，而这个数组也被 final 关键字修饰了，这就表示 String 对象是没法被修改的，只要初始化一次，值就确定了。

#### 这样设计的好处

第一，可以保证 String 对象的安全性，避免被篡改，毕竟像密码这种隐私信息一般就是用字符串存储的。

第二，保证哈希值不会频繁变更。毕竟要经常作为哈希表的键值，经常变更的话，哈希表的性能就会很差劲。

第三，可以实现字符串常量池。

“由于字符串的不可变性，String 类的一些方法实现最终都返回了新的字符串对象。

不管是截取、拼接，还是替换，都不是在原有的字符串上进行的，而是重新生成了新的字符串对象。也就是说，这些操作执行过后，**原来的字符串对象并没有发生改变**。

String 对象一旦被创建后就固定不变了，对 String 对象的任何修改都不会影响到原来的字符串对象，都会生成新的字符串对象。





### 字符串常量池

```java
String s = new String("二哥");
```

“使用 new 关键字创建一个字符串对象时，Java 虚拟机会先在字符串常量池中查找有没有‘二哥’这个字符串对象，如果有，就不会在字符串常量池中创建‘二哥’这个对象了，直接在堆中创建一个‘二哥’的字符串对象，然后将堆中这个‘二哥’的对象地址返回赋值给变量 s。”

“如果没有，先在字符串常量池中创建一个‘二哥’的字符串对象，然后再在堆中创建一个‘二哥’的字符串对象，然后将堆中这个‘二哥’的字符串对象地址返回赋值给变量 s。”

由于字符串的使用频率实在是太高了，所以 Java 虚拟机为了提高性能和减少内存开销，在创建字符串对象的时候进行了一些优化，特意为字符串开辟了一个字符串常量池。

```java
String s = "三妹";
```

当执行 `String s = "三妹"` 时，Java 虚拟机会先在字符串常量池中查找有没有“三妹”这个字符串对象，如果有，则不创建任何对象，直接将字符串常量池中这个“三妹”的对象地址返回，赋给变量 s；如果没有，在字符串常量池中创建“三妹”这个对象，然后将其地址返回，赋给变量 s。



来看下面这个例子：

```java
String s = new String("二哥");
String s1 = new String("二哥");
```

按照我们之前的分析，这两行代码会创建三个对象，字符串常量池中一个，堆上两个。

再来看下面这个例子：

```java
String s = "三妹";
String s1 = "三妹";
```

这两行代码只会创建一个对象，就是字符串常量池中的那个。这样的话，性能肯定就提高了！

#### 内存位置

在 Java 8 之前，字符串常量池在永久代中。

![img](Java.assets/constant-pool-01.png)

Java 8 之后，移除了永久代，字符串常量池就移到了堆中。

![img](Java.assets/constant-pool-02.png)

- 方法区是 Java 虚拟机规范中的一个概念，就像是一个接口吧；
- 永久代是 HotSpot 虚拟机中对方法的一个实现，就像是接口的实现类；
- Java 8 的时候，移除了永久代，取而代之的是元空间，是方法区的另外一个实现。

永久代是放在运行时数据区中的，所以它的大小受到 Java 虚拟机本身大小的限制，所以 Java 8 之前，会经常遇到 `java.lang.OutOfMemoryError: PremGen Space` 的异常，PremGen Space 就是方法区的意思；而元空间是直接放在内存中的，所以只受本机可用内存的限制，虽然也会发生内存溢出，但出现的几率相对之前就小了很多。

#### intern()

猜猜这段代码输出的结果

```java
String s1 = new String("二哥三妹");
String s2 = s1.intern();
System.out.println(s1 == s2);
```

第一行代码，字符串常量池中会先创建一个“二哥三妹”的对象，然后堆中会再创建一个“二哥三妹”的对象，s1 引用的是堆中的对象。

第二行代码，对 s1 执行 `intern()` 方法，该方法会从字符串常量池中查找“二哥三妹”这个字符串是否存在，此时是存在的，所以 s2 引用的是字符串常量池中的对象。

也就意味着 s1 和 s2 的引用地址是不同的，一个来自堆，一个来自字符串常量池，所以输出的结果为 false。

![img](Java.assets/intern-01.png)

```java
String s1 = new String("二哥") + new String("三妹");
String s2 = s1.intern();
System.out.println(s1 == s2);
```

第一行代码，会在字符串常量池中创建两个对象，一个是“二哥”，一个是“三妹”，然后在堆中会创建两个匿名对象“二哥”和“三妹”（可以暂时忽略），最后还有一个“二哥三妹”的对象，s1 引用的是堆中“二哥三妹”这个对象。

第二行代码，对 s1 执行 `intern()` 方法，该方法会从字符串常量池中查找“二哥三妹”这个对象是否存在，此时不存在的，但堆中已经存在了，所以字符串常量池中保存的是堆中这个“二哥三妹”对象的引用，也就是说，s2 和 s1 的引用地址是相同的，所以输出的结果为 true。

![](Java.assets/intern-02.png)

### 字符串比较

- `==`操作符用于比较两个对象的地址是否相等。
- `.equals()` 方法用于比较两个对象的内容是否相等。

#### equals()源码

```java
public boolean equals(Object anObject) {
    if (this == anObject) {
        return true;
    }
    if (anObject instanceof String) {
        String aString = (String)anObject;
        if (coder() == aString.coder()) {
            return isLatin1() ? StringLatin1.equals(value, aString.value)
                    : StringUTF16.equals(value, aString.value);
        }
    }
    return false;
}
```

首先，如果两个字符串对象的可以“==”，那就直接返回 true 了，因为这种情况下，字符串内容是必然相等的。否则就按照字符编码进行比较，分为 UTF16 和 Latin1，差别不是很大，就拿 Latin1 的来说吧。

```java
@HotSpotIntrinsicCandidate
public static boolean equals(byte[] value, byte[] other) {
    if (value.length == other.length) {
        for (int i = 0; i < value.length; i++) {
            if (value[i] != other[i]) {
                return false;
            }
        }
        return true;
    }
    return false;
}
```

String 类使用字节数组实现的，所以比较两个字符串的内容是否相等时，可以先比较字节数组的长度是否相等，不相等就直接返回 false；否则就遍历两个字符串的字节数组，只有有一个字节不相等，就返回 false。

#### 例题

第一题：



```java
new String("小萝莉").equals("小萝莉")
```

“输出什么呢？”我问。

“`.equals()` 比较的是两个字符串对象的内容是否相等，所以结果为 true。”三妹答。

第二题：



```java
new String("小萝莉") == "小萝莉"
```

“==操作符左侧的是在堆中创建的对象，右侧是在字符串常量池中的对象，尽管内容相同，但内存地址不同，所以返回 false。”三妹答。

第三题：



```java
new String("小萝莉") == new String("小萝莉")
```

“new 出来的对象肯定是完全不同的内存地址，所以返回 false。”三妹答。

第四题：



```java
"小萝莉" == "小萝莉"
```

“字符串常量池中只会有一个相同内容的对象，所以返回 true。”三妹答。

第五题：



```java
"小萝莉" == "小" + "萝莉"
```

“由于‘小’和‘萝莉’都在字符串常量池，所以编译器在遇到‘+’操作符的时候将其自动优化为“小萝莉”，所以返回 true。”

第六题：



```java
new String("小萝莉").intern() == "小萝莉"
```

“`new String("小萝莉")` 在执行的时候，会先在字符串常量池中创建对象，然后再在堆中创建对象；执行 `intern()` 方法的时候发现字符串常量池中已经有了‘小萝莉’这个对象，所以就直接返回字符串常量池中的对象引用了，那再与字符串常量池中的‘小萝莉’比较，当然会返回 true 了。



另外还有两个方案

“如果要进行两个字符串对象的内容比较，除了 `.equals()` 方法，还有其他两个可选的方案。”

#### 1）`Objects.equals()`

`Objects.equals()` 这个静态方法的优势在于不需要在调用之前判空。



```java
public static boolean equals(Object a, Object b) {
    return (a == b) || (a != null && a.equals(b));
}
```

如果直接使用 `a.equals(b)`，则需要在调用之前对 a 进行判空，否则可能会抛出空指针 `java.lang.NullPointerException`。`Objects.equals()` 用起来就完全没有这个担心。



```java
Objects.equals("小萝莉", new String("小" + "萝莉")) // --> true
Objects.equals(null, new String("小" + "萝莉")); // --> false
Objects.equals(null, null) // --> true

String a = null;
a.equals(new String("小" + "萝莉")); // throw exception
```



#### 2）String 类的 `.contentEquals()`

`.contentEquals()` 的优势在于可以将字符串与任何的字符序列（StringBuffer、StringBuilder、String、CharSequence）进行比较。



```java
public boolean contentEquals(CharSequence cs) {
    // Argument is a StringBuffer, StringBuilder
    if (cs instanceof AbstractStringBuilder) {
        if (cs instanceof StringBuffer) {
            synchronized(cs) {
                return nonSyncContentEquals((AbstractStringBuilder)cs);
            }
        } else {
            return nonSyncContentEquals((AbstractStringBuilder)cs);
        }
    }
    // Argument is a String
    if (cs instanceof String) {
        return equals(cs);
    }
    // Argument is a generic CharSequence
    int n = cs.length();
    if (n != length()) {
        return false;
    }
    byte[] val = this.value;
    if (isLatin1()) {
        for (int i = 0; i < n; i++) {
            if ((val[i] & 0xff) != cs.charAt(i)) {
                return false;
            }
        }
    } else {
        if (!StringUTF16.contentEquals(val, cs, n)) {
            return false;
        }
    }
    return true;
}
```

从源码上可以看得出，如果 cs 是 StringBuffer，该方法还会进行同步，非常的智能化；如果是 String 的话，其实调用的还是 `equals()` 方法。当然了，这也就意味着使用该方法进行比较的时候，多出来了很多步骤，性能上有些损失。



### 字符串拼接



### 字符串分割



## 集合



![img](Java.assets/gailan-01.png)



Java 集合框架可以分为两条大的支线：

- **Collection**，主要由 List、Set、Queue 组成，List 代表有序、可重复的集合，典型代表就是封装了动态数组的 **ArrayList** 和封装了链表的 **LinkedList**；Set 代表无序、不可重复的集合，典型代表就是 **HashSet** 和 **TreeSet**；Queue 代表队列，典型代表就是双端队列 **ArrayDeque**，以及优先级队列 **PriorityQue**。
- **Map**，代表键值对的集合，典型代表就是 **HashMap**。

### 概述

#### 01、List

> List 的特点是存取有序，可以存放重复的元素，可以用下标对元素进行操作

**1）ArrayList**

- ArrayList 是由数组实现的，支持随机存取，也就是可以通过下标直接存取元素；
- 从尾部插入和删除元素会比较快捷，从中间插入和删除元素会比较低效，因为涉及到数组元素的复制和移动；
- 如果内部数组的容量不足时会自动扩容，因此当元素非常庞大的时候，效率会比较低。

**2）LinkedList**

- LinkedList 是由双向链表实现的，不支持随机存取，只能从一端开始遍历，直到找到需要的元素后返回；
- 任意位置插入和删除元素都很方便，因为只需要改变前一个节点和后一个节点的引用即可，不像 ArrayList 那样需要复制和移动数组元素；
- 因为每个元素都存储了前一个和后一个节点的引用，所以相对来说，占用的内存空间会比 ArrayList 多一些。

**3）Vector 和 Stack**

List 的实现类还有一个 Vector，是一个元老级的类，比 ArrayList 出现得更早。ArrayList 和 Vector 非常相似，只不过 Vector 是线程安全的，像 get、set、add 这些方法都加了 `synchronized` 关键字，就导致执行执行效率会比较低，所以现在已经很少用了。

更好的选择是并发包下的 CopyOnWriteArrayList。

Stack 是 Vector 的一个子类，本质上也是由动态数组实现的，只不过还实现了先进后出的功能（在 get、set、add 方法的基础上追加了 pop、peek 等方法），所以叫栈。

不过，由于 Stack 执行效率比较低（方法上同样加了 synchronized 关键字），就被双端队列 ArrayDeque 取代了。

#### 02、Set

> Set 的特点是存取无序，不可以存放重复的元素，不可以用下标对元素进行操作，和 List 有很多不同

**1）HashSet**

HashSet 其实是由 HashMap 实现的，只不过值由一个固定的 Object 对象填充，而键用于操作。



```java
public class HashSet<E>
    extends AbstractSet<E>
    implements Set<E>, Cloneable, java.io.Serializable
{
    private transient HashMap<E,Object> map;

    // Dummy value to associate with an Object in the backing Map
    private static final Object PRESENT = new Object();

    public HashSet() {
        map = new HashMap<>();
    }

    public boolean add(E e) {
        return map.put(e, PRESENT)==null;
    }

    public boolean remove(Object o) {
        return map.remove(o)==PRESENT;
    }
}
```

**2）LinkedHashSet**

LinkedHashSet 继承自 HashSet，其实是由 LinkedHashMap 实现的，LinkedHashSet 的构造方法调用了 HashSet 的一个特殊的构造方法：



```java
HashSet(int initialCapacity, float loadFactor, boolean dummy) {
   map = new LinkedHashMap<>(initialCapacity, loadFactor);
}
```

**3）TreeSet**

“二哥，不用你讲了，我能猜到，TreeSet 是由 TreeMap 实现的，只不过同样操作的键位，值由一个固定的 Object 对象填充。”



#### 03、Queue

> Queue，也就是队列，通常遵循先进先出（FIFO）的原则，新元素插入到队列的尾部，访问元素返回队列的头部。

**1）ArrayDeque**

从名字上可以看得出，ArrayDeque 是一个基于数组实现的双端队列，为了满足可以同时在数组两端插入或删除元素的需求，数组必须是循环的，也就是说数组的任何一点都可以被看作是起点或者终点。

这是一个包含了 4 个元素的双端队列，和一个包含了 5 个元素的双端队列。

![img](Java.assets/gailan-02.png)

head 指向队首的第一个有效的元素，tail 指向队尾第一个可以插入元素的空位，因为是循环数组，所以 head 不一定从是从 0 开始，tail 也不一定总是比 head 大。

**2）LinkedList**

LinkedList 一般都归在 List 下，只不过，它也实现了 Deque 接口，可以作为队列来使用。等于说，LinkedList 同时实现了 Stack、Queue、PriorityQueue 的所有功能。

**3）PriorityQueue**

PriorityQueue 是一种优先级队列，它的出队顺序与元素的优先级有关，执行 remove 或者 poll 方法，返回的总是优先级最高的元素。

要想有优先级，元素就需要实现 Comparable 接口或者 Comparator 接口。

#### 04、Map

> Map 保存的是键值对，键要求保持唯一性，值可以重复。

**1）HashMap**

HashMap 实现了 Map 接口，根据键的 HashCode 值来存储数据，具有很快的访问速度，最多允许一个 null 键。

HashMap 不论是在学习还是工作当中，使用频率都是相当高的。随着 JDK 版本的不断更新，HashMap 的底层也优化了很多次，JDK 8 的时候引入了红黑树。



```java
final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
               boolean evict) {
    HashMap.Node<K,V>[] tab; HashMap.Node<K,V> p; int n, i;
    if ((tab = table) == null || (n = tab.length) == 0)
        n = (tab = resize()).length;
    if ((p = tab[i = (n - 1) & hash]) == null)
        tab[i] = newNode(hash, key, value, null);
    else {
        HashMap.Node<K,V> e; K k;
        if (p.hash == hash &&
                ((k = p.key) == key || (key != null && key.equals(k))))
            e = p;
        else if (p instanceof HashMap.TreeNode)
            e = ((HashMap.TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
        else {
            for (int binCount = 0; ; ++binCount) {
                if ((e = p.next) == null) {
                    p.next = newNode(hash, key, value, null);
                    if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
                        treeifyBin(tab, hash);
                    break;
                }
                if (e.hash == hash &&
                        ((k = e.key) == key || (key != null && key.equals(k))))
                    break;
                p = e;
            }
        }
    return null;
}
```

一旦 HashMap 发生哈希冲突，就把相同键位的地方改成链表，如果链表的长度超过 8，就该用红黑树。

**2）LinkedHashMap**

大多数情况下，只要不涉及线程安全问题，Map基本都可以使用HashMap，不过HashMap有一个问题，就是迭代HashMap的顺序并不是HashMap放置的顺序，也就是无序。HashMap的这一缺点往往会带来困扰，因为有些场景，我们期待一个有序的Map。

大多数情况下，只要不涉及到线程安全的问题，有需要键值对的时候就会使用 HashMap，但 HashMap 有一个问题，就是 HashMap 是无序的。在某些场景下，我们需要一个有序的 Map。

于是 LinkedHashMap 就闪亮登场了。LinkedHashMap 是 HashMap 的子类，内部使用链表来记录插入/访问元素的顺序。

LinkedHashMap 可以看作是 HashMap + LinkedList 的合体，它使用了 哈希表来存储数据，又用了双向链表来维持顺序。

**3）TreeMap**

HashMap 是无序的，所以遍历的时候元素的顺序也是不可测的。TreeMap 是有序的，它在内部会对键进行排序，所以遍历的时候就可以得到预期的顺序。

为了保证顺序，TreeMap 的键必须要实现 Comparable 接口或者 Comparator 接口



### ArrayList

从名字就可以看得出来，ArrayList 实现了 List 接口，并且是基于数组实现的。

数组的大小是固定的，一旦创建的时候指定了大小，就不能再调整了。也就是说，如果数组满了，就不能再添加任何元素了。ArrayList 在数组的基础上实现了自动扩容，并且提供了比数组更丰富的预定义方法（各种增删改查），非常灵活。

**如何创建一个 ArrayList**

```java
ArrayList<String> alist = new ArrayList<String>();
```

可以通过上面的语句来创建一个字符串类型的 ArrayList（通过尖括号来限定 ArrayList 中元素的类型，如果尝试添加其他类型的元素，将会产生编译错误），更简化的写法如下：



```java
List<String> alist = new ArrayList<>();
```

由于 ArrayList 实现了 List 接口，所以 alist 变量的类型可以是 List 类型；new 关键字声明后的尖括号中可以不再指定元素的类型，因为编译器可以通过前面尖括号中的类型进行智能推断。

如果非常确定 ArrayList 中元素的个数，在创建的时候还可以指定初始大小。



```java
List<String> alist = new ArrayList<>(20);
```

这样做的好处是，可以有效地避免在添加新的元素时进行不必要的扩容。但通常情况下，我们很难确定 ArrayList 中元素的个数，因此一般不指定初始大小。

**向 ArrayList 中添加一个元素**

可以通过 `add()` 方法向 ArrayList 中添加一个元素，如果不指定下标的话，就默认添加在末尾。

```java
alist.add("沉默王二");
```

研究一下 `add()` 方法的源码（基于 JDK 8 会好一点），它在添加元素的时候会判断需不需要进行扩容，如果需要的话，会执行 `grow()` 方法进行扩容，这个也是面试官特别喜欢考察的一个重点。”我叮嘱道。

**更新 ArrayList 中的元素**

可以使用 `set()` 方法来更改 ArrayList 中的元素，需要提供下标和新元素。

```java
alist.set(0, "沉默王四");
```

假设原来 0 位置上的元素为“沉默王三”，现在可以将其更新为“沉默王四”。

**删除 ArrayList 中的元素**

`remove(int index)` 方法用于删除指定下标位置上的元素，`remove(Object o)` 方法用于删除指定值的元素。

```java
alist.remove(1);
alist.remove("沉默王四");
```

**查找 ArrayList 中的元素**

如果要正序查找一个元素，可以使用 `indexOf()` 方法；如果要倒序查找一个元素，可以使用 `lastIndexOf()` 方法。

```java
alist.indexOf("沉默王二");
alist.lastIndexOf("沉默王二");
```



### LinkeList

链表大致分为三个层次：

- 第一层叫做“**单向链表**”，我只有一个后指针，指向下一个数据；
- 第二层叫做“**双向链表**”，我有两个指针，后指针指向下一个数据，前指针指向上一个数据。
- 第三层叫做“**二叉树**”，把后指针去掉，换成左右指针。

**初始化:**

```java
LinkedList<String> list = new LinkedList();
```

**增**

可以调用 add 方法添加元素：

```java
list.add("沉默王二");
list.add("沉默王三");
list.add("沉默王四");
```

- `addFirst()` 方法将元素添加到第一位；
- `addLast()` 方法将元素添加到末尾。

**删**

- `remove()`：删除第一个节点
- `remove(int)`：删除指定位置的节点
- `remove(Object)`：删除指定元素的节点
- `removeFirst()`：删除第一个节点
- `removeLast()`：删除最后一个节点

**改**

可以调用 `set()` 方法来更新元素：

```java
list.set(0, "沉默王五");
```

**查**

- `indexOf(Object)`：查找某个元素所在的位置
- `get(int)`：查找某个位置上的元素

- `getFirst()` 方法用于获取第一个元素；
- `getLast()` 方法用于获取最后一个元素；
- `poll()` 和 `pollFirst()` 方法用于删除并返回第一个元素（两个方法尽管名字不同，但方法体是完全相同的）；
- `pollLast()` 方法用于删除并返回最后一个元素；
- `peekFirst()` 方法用于返回但不删除第一个元素。



### Iterator和Iterable

在 Java 中，我们对 List 进行遍历的时候，主要有这么三种方式。

第一种：**for 循环**。

```java
for (int i = 0; i < list.size(); i++) {
    System.out.print(list.get(i) + "，");
}
```

第二种：**迭代器**。

```java
Iterator it = list.iterator();
while (it.hasNext()) {
    System.out.print(it.next() + "，");
}
```

第三种：**for-each**。(语法糖)

```java
for (String str : list) {
    System.out.print(str + "，");
}
```

第一种我们略过，第二种用的是 Iterator，第三种看起来是 for-each，其实背后也是 Iterator



- 允许删除元素（ remove 方法）







### HashMap

```java
static final int hash(Object key) {
    int h;
    return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
}
```

- `put(key,value)`: 可以单次向HashMap中添加一个键值对。

- `putAll(hashMap)`: 可以把一个HashMap集合对象，整体加入到另外一个HashMap对象中。

- `remove(key)`:  可以单次删除一个元素。

- `get(key)`:  用来取map中存储的数据，我们根据其key值，可以取到对应的value值，没有该key对应的值则返回null。

- `clear()`: 清空map中的数据

- `containsKey(key)`: 判断map集合中是否包含某个key。

- `containsKey(value)`: 判断map集合中是否包含某个value。

- `entrySet()`：hashmap.entrySet().iterator()，entrySet()的效率比keySet()要高。key和value存储在entry对象里面，遍历的时候，拿到entry对象就可以取到value了。

- `keySet()`：hashmap.keySet().iterator()，keySet是把key放到一个set集合中，通过迭代器遍历，再用hashmap.get(key)来取到value的值。

  

## IO

### 基础

#### 传输方式划分

![img](Java.assets/shangtou-01.png)

**字节**（byte）是计算机中用来表示存储容量的一个计量单位，通常情况下，一个字节有 8 位（bit）。

**字符**（char）可以是计算机中使用的字母、数字、和符号，比如说 A 1 $ 这些。

通常来说，一个字母或者一个字符占用一个字节，一个汉字占用两个字节。

在 UTF-8 编码下，一个英文字母（不分大小写）为一个字节，一个中文汉字为三个字节

**字节流**用来处理二进制文件，比如说图片啊、MP3 啊、视频啊。

**字符流**用来处理文本文件，文本文件可以看作是一种特殊的二进制文件，只不过经过了编码，便于人们阅读。

换句话说就是，**字节流可以处理一切文件，而字符流只能处理文本**。

虽然 IO 类很多，但核心的就是 4 个抽象类：`InputStream`、`OutputStream`、`Reader`、`Writer`。

虽然 IO 类的方法也很多，但核心的也就 2 个：`read` 和 `write`。

##### **InputStream 类**

- `int read()`：读取数据
- `int read(byte b[], int off, int len)`：从第 off 位置开始读，读取 len 长度的字节，然后放入数组 b 中
- `long skip(long n)`：跳过指定个数的字节
- `int available()`：返回可读的字节数
- `void close()`：关闭流，释放资源

##### **OutputStream 类**

- `void write(int b)`： 写入一个字节，虽然参数是一个 int 类型，但只有低 8 位才会写入，高 24 位会舍弃（这块后面再讲）
- `void write(byte b[], int off, int len)`： 将数组 b 中的从 off 位置开始，长度为 len 的字节写入
- `void flush()`： 强制刷新，将缓冲区的数据写入
- `void close()`：关闭流

##### **Reader 类**

- `int read()`：读取单个字符
- `int read(char cbuf[], int off, int len)`：从第 off 位置开始读，读取 len 长度的字符，然后放入数组 b 中
- `long skip(long n)`：跳过指定个数的字符
- `int ready()`：是否可以读了
- `void close()`：关闭流，释放资源

##### **Writer 类**

- `void write(int c)`： 写入一个字符
- `void write( char cbuf[], int off, int len)`： 将数组 cbuf 中的从 off 位置开始，长度为 len 的字符写入
- `void flush()`： 强制刷新，将缓冲区的数据写入
- `void close()`：关闭流

理解了上面这些方法，基本上 IO 的灵魂也就全部掌握了





#### 操作对象划分

<img src="Java.assets/shangtou-03.png" alt="img" style="zoom: 67%;" />



所有的程序，在执行的时候，都是在内存上进行的，一旦关机，内存中的数据就没了，那如果想要**持久化**，就需要把内存中的数据输出到外部，比如说文件。

文件操作算是 IO 中最典型的操作了，也是最频繁的操作。那其实你可以换个角度来思考，比如说按照 IO 的操作对象来思考，IO 就可以分类为：文件、数组、管道、基本数据类型、缓冲、打印、对象序列化/反序列化，以及转换等。

**1）文件**

文件流也就是直接操作文件的流，可以细分为字节流（FileInputStream 和 FileOuputStream）和字符流（FileReader 和 FileWriter）。

FileInputStream 的例子：



```java
int b;
FileInputStream fis1 = new FileInputStream("fis.txt");
// 循环读取
while ((b = fis1.read())!=-1) {
    System.out.println((char)b);
}
// 关闭资源
fis1.close();
```

FileOutputStream 的例子：



```java
FileOutputStream fos = new FileOutputStream("fos.txt");
fos.write("沉默王二".getBytes());
fos.close();
```

FileReader 的例子：



```java
int b = 0;
FileReader fileReader = new FileReader("read.txt");
// 循环读取
while ((b = fileReader.read())!=-1) {
    // 自动提升类型提升为 int 类型，所以用 char 强转
    System.out.println((char)b);
}
// 关闭流
fileReader.close();
```

FileWriter 的例子：



```java
FileWriter fileWriter = new FileWriter("fw.txt");
char[] chars = "沉默王二".toCharArray();
fileWriter.write(chars, 0, chars.length);
fileWriter.close();
```

当掌握了文件的输入输出，其他的自然也就掌握了，都大差不差。



### BIO | NIO | AIO

**BIO （Blocking I/O）：同步阻塞 I/O 模式。**

**NIO （New I/O）：同步非阻塞模式。**

**AIO （Asynchronous I/O）：异步非阻塞 I/O 模型。**







## 123123

### String与integer

parseInt



装箱：Integer,valueOf()       (int => integer)

拆箱：i (integer类型).intValue()     (integer => int)

### Data与SimpleDateFormat

Data()   

Data(long date)    :自标准基准时间（1970/01/01/00:00:00）+ long data 的指定毫秒数

### 字符串方法

equal()

chatAt()

subString()

replace()

split()

![image-20220710135155659](Java.assets\image-20220710135155659.png)

![image-20220710135404101](Java.assets\image-20220710135404101.png)



### 集合

#### ArrayList

![image-20220710135909697](Java.assets\image-20220710135909697.png)

 ![image-20220710135949232](Java.assets\image-20220710135949232.png)

常用成员方法

![image-20220710140602250](Java.assets\image-20220710140602250.png)



#### Set

![image-20220710153631719](Java.assets\image-20220710153631719.png)



**set遍历**

![image-20220710153832475](Java.assets\image-20220710153832475.png)



#### TreeSet

![image-20220710154233947](Java.assets\image-20220710154233947.png)

#### 二叉树

#### 红黑树



#### Map集合

![image-20220710154626037](Java.assets\image-20220710154626037.png)









### static

![image-20220710142906204](Java.assets\image-20220710142906204.png)

注意事项

/*/![image-20220710143634243](Java.assets\image-20220710143634243.png)

### 继承

抽象类





### Stream流

![image-20220710155111425](Java.assets\image-20220710155111425.png)



### IO

> 一切文件数据(文本、图片、视频等)在存储时，都是以二进制的形式保存，传输时同样如此。所以字节流可以传输任意数据。 在操作流的时候，无论使用什么样的流对象，底层传输的始终为二进制数据。

> 根据数据的流向分为：**输入流** 和 **输出流**

- 输入流 ：硬盘 --> 内存
- 输出流 ：内存 --> 硬盘

> 根据数据的类型分为：**字节流** 和 **字符流**。 另外还有：**缓冲流**、**转换流**、**序列流**、**打印流**。

#### 字节流

#### 字符流

#### 缓冲流&转换流

#### 对象操作流











