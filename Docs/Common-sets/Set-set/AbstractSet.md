# AbstractSet
- AbstractSet 是一个抽象类，它继承于AbstractCollection。AbstractCollection实现了Set中的绝大部分函数(CRUD)，为Set的实现类提供了便利。
## 类图

<div align="center">  
<img src="https://github.com/Marcos-Lay/Hello-JAVA/blob/master/Docs/Common-sets/Set-set/Set.png"> 
</div>

## AbstractSet的直接子类
- ConcurrentSkipListSet
- CopyOnWriteArraySet
- EnumSet
- HashSet
- TreeSet
## AbstractSet的构造函数
- AbstractSet只有无参构造
```java
     /**
     * Sole constructor.  (For invocation by subclass constructors, typically
     * implicit.)
     */
    protected AbstractSet() {
    }
```
## AbstractSet的具体实现
- 实现了equals供实现set接口的实现类使用
```java
public boolean equals(Object o) {
        if (o == this)
            return true;

        if (!(o instanceof Set))
            return false;
        Collection<?> c = (Collection<?>) o;
        if (c.size() != size())
            return false;
        try {
            return containsAll(c);
        } catch (ClassCastException unused)   {
            return false;
        } catch (NullPointerException unused) {
            return false;
        }
    }
```
- 实现了hashcode供实现set接口的实现类使用
```java
public int hashCode() {
        int h = 0;
        Iterator<E> i = iterator();
        while (i.hasNext()) {
            E obj = i.next();
            if (obj != null)
                h += obj.hashCode();
        }
        return h;
    }
```
- 实现了removeAll供实现set接口的实现类使用
```java
public boolean removeAll(Collection<?> c) {
        Objects.requireNonNull(c);
        boolean modified = false;

        if (size() > c.size()) {
            for (Iterator<?> i = c.iterator(); i.hasNext(); )
                modified |= remove(i.next());
        } else {
            for (Iterator<?> i = iterator(); i.hasNext(); ) {
                if (c.contains(i.next())) {
                    i.remove();
                    modified = true;
                }
            }
        }
        return modified;
    }
```
