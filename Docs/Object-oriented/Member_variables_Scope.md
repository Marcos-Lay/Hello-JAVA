# 成员变量及成员方法的作用域
> 注意：是成员变量，不是类变量或局部变量
> 有关[成员变量与类变量和局部变量的区别](https://github.com/Marcos-Lay/Hello-JAVA/blob/master/Docs/Object-oriented/Class_member_local_variables.md)
### 对于成员变量和方法的作用域，public,protected,private以及不写之间的区别。
- public :表明该成员变量或者方法是对所有类或者对象都是可见的,所有类或者对象都可以直接访问 
- private:表明该成员变量或者方法是私有的,只有当前类对其具有访问权限,除此之外其他类或者对象都没有访问权限.子类也没有访问权限. 
- protected:表明成员变量或者方法对类自身,与同在一个包中的其他类可见,其他包下的类不可访问,除非是他的子类 
- default:表明该成员变量或者方法只有自己和其位于同一个包的内可见,其他包内的类不能访问,即便是它的子类