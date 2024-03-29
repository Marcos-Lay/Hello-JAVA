###什么是多态，多态有什么好处，多态的必要条件是什么、Java中多态的实现方式

多态的概念呢比较简单，就是同一操作作用于不同的对象，可以有不同的解释，产生不同的执行结果。

如果按照这个概念来定义的话，那么多态应该是一种运行期的状态。
为了实现运行期的多态，或者说是动态绑定，需要满足三个条件。

即有类继承或者接口实现、子类要重写父类的方法、父类的引用指向子类的对象。

简单来一段代码解释下：
```java
    public class Parent{
        
        public void call(){
            sout("im Parent");
        }
    }

    public class Son extends Parent{// 1.有类继承或者接口实现
        public void call(){// 2.子类要重写父类的方法
            sout("im Son");
        }
    }

    public class Daughter extends Parent{// 1.有类继承或者接口实现
        public void call(){// 2.子类要重写父类的方法
            sout("im Daughter");
        }
    }

    public class Test{
        
        public static void main(String[] args){
            Parent p = new Son(); //3.父类的引用指向子类的对象
            Parent p1 = new Daughter(); //3.父类的引用指向子类的对象
        }
    }
```
这样，就实现了多态，同样是Parent类的实例，p.call 调用的是Son类的实现、p1.call调用的是Daughter的实现。
有人说，你自己定义的时候不就已经知道p是son，p1是Daughter了么。但是，有些时候你用到的对象并不都是自己声明的啊 。
比如Spring 中的IOC出来的对象，你在使用的时候就不知道他是谁，或者说你可以不用关心他是谁。根据具体情况而定。


另外，还有一种说法，包括维基百科也说明，动态还分为动态多态和静态多态。
上面提到的那种动态绑定认为是动态多态，因为只有在运行期才能知道真正调用的是哪个类的方法。

还有一种静态多态，一般认为Java中的函数重载是一种静态多态，因为他需要在编译期决定具体调用哪个方法、

关于这个动态静态的说法，我更偏向于重载和多态其实是无关的。

但是也要看情况，普通场合，我会认为只有方法的重写算是多态，毕竟这是我的观点。但是如果在面试的时候，我“可能”会认为重载也算是多态，毕竟面试官也有他的观点。我会和面试官说：我认为，多态应该是一种运行期特性，Java中的重写是多态的体现。不过也有人提出重载是一种静态多态的想法，这个问题在StackOverflow等网站上有很多人讨论，但是并没有什么定论。我更加倾向于重载不是多态。

这样沟通，既能体现出你了解的多，又能表现出你有自己的思维，不是那种别人说什么就是什么的。