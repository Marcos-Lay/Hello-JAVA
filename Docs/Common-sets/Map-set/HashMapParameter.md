# HashMap源码中的那些傻傻分不清楚的参数详解
<img src = "https://github.com/Marcos-Lay/Hello-JAVA/blob/master/Docs/Common-sets/Map-set/HashMapVariable.png">
```java
/**
* 默认初始容量，必须是2的幂
*/
static final int DEFAULT_INITIAL_CAPACITY = 1 << 4; // aka 16

/**
* 默认的最大容量，必须是2的幂
*/
static final int MAXIMUM_CAPACITY = 1 << 30;

/**
* 默认加载因子
*/
static final float DEFAULT_LOAD_FACTOR = 0.75f;

/**
* 链表转换为红黑树（查找时间复杂度为 O(logn)）的阈值
*/
static final int TREEIFY_THRESHOLD = 8;

/**
* 红黑树还原为链表的阈值
*/
static final int UNTREEIFY_THRESHOLD = 6;

/**
* hashmap的size至少大于64时才可以使链表转换为红黑树
*/
static final int MIN_TREEIFY_CAPACITY = 64;
/**
* table中存储的是HashMap中所有的元素，transient修饰符的作用是使该变量在序列化的时候不会被储存，
* 至于hashmap是如何在序列化中储存元素呢？原来是它通过重写Serializable接口中的writeObject方法和readObject方法实现的
*/
transient Node<K,V>[] table;

/**
* 
* HashMap将数据转换成set的另一种存储形式，这个变量主要用于迭代功能。
*/
transient Set<Map.Entry<K,V>> entrySet;

/**
* 记录了Map中已使用的KV对的个数.
*/
transient int size;

/**
* HashMao结构修改的次数，也可以说是扩容的次数
*/
transient int modCount;

/**
* threshold表示当HashMap的size大于threshold时会执行resize操作。 
threshold=capacity*loadFactor
*
* @serial
*/
// (The javadoc description is true upon serialization.
// Additionally, if the table array has not been allocated, this
// field holds the initial array capacity, or zero signifying
// DEFAULT_INITIAL_CAPACITY.)
int threshold;

/**
* 装载因子，用来衡量HashMap的用量程度，默认值为0.75f(static final float DEFAULT_LOAD_FACTOR = 0.75f).
*
* @serial
*/
final float loadFactor;
```