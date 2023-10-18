
# Done is better than perfect.

# SOLID
## 单一责任原则 Single Responsibility Principle

> 一个类应该只负责一件事。

["单一责任"](02_NamesAfterRefactorToSRP)

# 多态
变量 父类 = new 子类();

调用的是 变量后的父类方法

![img.png](E:\Typora_MD\img\img.png)

1. 判断父调用的方法是否是 Virtual 方法
   > * 是 Virtual 方法  
   > 
    > 并且子类进行了重写override 那么 调用出来的就是子类方法 
   > 
   > 子类没有重写 那么 调用的就还是父类方法内容
   > 
> * 否 不是Virtual  --》
> 
> 先判断父类是否有这个方法 ：
> 
> 没有 即编译时报错 找不到方法
> 
> 有 就执行父类里面的方法内容 ，总之 不会去执行子类独有方法 而父类没有的方法

“组合优于继承”

# 继承与构造函数
子类对象 会优先执行 父类构造 （默认会有无参构造）

当 父类添加 有参构造 时候 默认的无参构造 会被覆盖 

子类需要 :base 继承父类有参构造的参数 or 父类自建一个无参构造

# 抽象方法 与 虚方法
![img1.png](E:\Typora_MD\img\img1.png)

![img2.png](E:\Typora_MD\img\img2.png)

# 接口 与 抽象类
![img3.png](E:\Typora_MD\img\img3.png)

![img4.png](E:\Typora_MD\img\img4.png)

![img5.png](E:\Typora_MD\img\img5.png)

# 继承 与 接口 所构造的关系
![img_1.png](E:\Typora_MD\img\img_1.png)
