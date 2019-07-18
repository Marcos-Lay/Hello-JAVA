# HashSet
## 类图
<div align="center">  
<img src="https://github.com/Marcos-Lay/Hello-JAVA/blob/master/Docs/Common-sets/Set-set/Set.png"> 
</div>
## 继承AbstractSet<E>
- 实现公有方法（equals，hashcode，removeAll）
## 所有已实现的接口：
- Serializable（可序列化）
- Cloneable（可复制）
- Iterable<E>（可迭代）
- Collection<E>（集合接口）
- Set<E>（Set接口）
## 直接已知子类：
- JobStateReasons
- LinkedHashSet
## HashSet的构造方法
> 无参构造
- 创建一个HashMap，并且指定默认长度为16，默认加载因子为0.75
```java
public HashSet() {
        map = new HashMap<>();
    }
```
> 有参构造（集合）
- 创建一个初始容量能够容纳输入集合大小的HashMap，默认加载因子为0.75,如果输入集合为空则抛出空指针异常（NullPointerException）
```java
public HashSet(@NotNull @Flow(sourcelsContainer=true,targetlsContainer=true)Collection<? extends E> c) {
        map = new HashMap<>(Math.max((int) (c.size()/.75f) + 1, 16));
        addAll(c);
    }
```
> 有参构造（初始容量，加载因子）
- 创建一个HashMap,初始容量与加载因子手动设定
```java
public HashSet(int initialCapacity, float loadFactor) {
        map = new HashMap<>(initialCapacity, loadFactor);
    }
```
> 有参构造（初始容量）
- 创建一个HashMap,初始容量手动设定，默认加载因子为0.75
```java
public HashSet(int initialCapacity) {
        map = new HashMap<>(initialCapacity);
    }
```
> 有参构造（初始容量，加载因子，dummp(Boolean)）
- 创建一个手动指定初始容量，加载因子的LinkHashMap,<a>Dummp网上介绍没有任何作用，有待深究</a>
```java
HashSet(int initialCapacity, float loadFactor, boolean dummy) {
        map = new LinkedHashMap<>(initialCapacity, loadFactor);
    }
```
## HashSet中实现的方法
> iterator方法
- 使用迭代器返回HashSet中的元素，返回的顺序无规律
```java
public Iterator<E> iterator() {
        return map.keySet().iterator();
    }
```
> size方法
- 返回HashSet中元素的个数
```java
public int size() {
        return map.size();
    }
```