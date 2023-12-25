# Java内存分配

- 栈
- 堆
- 方法区
- 本地方法栈
- 寄存器

## 栈

方法/变量 被调用时 就会进栈 

## 堆

new 出来的东西 会在堆中开辟空间 并且产生地址

## 方法区

类运行时候就会产生字节码文件(.class) 临时存储在方法区 ，等待堆的调用

![image-20231207104640213](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231207104640213.png)

## 一个对象的内存图

`Student s = new Student();`

1. 加载class文件   ->  写了这行代码 就是会去加载这个类的 字节码文件 以此 获取里面的成员
2. 声明局部变量 --> Student  s  栈
3. 在堆中开辟空间 --> new 
4. 默认初始化
5. 显示初始化
6. 构造方法初始化
7. 将堆中地址赋值给左边的局部变量

# this的内存原理

this. ：所在方法调用者的地址值	(类对象.)

# 成员变量和局部变量

![image-20231207112801324](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231207112801324.png)

![image-20231207112914352](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231207112914352.png)

# OOP

## 封装

![image-20231218135632152](https://raw.githubusercontent.com/knellwake/Notes/main/img/image-20231218135632152.png)

对象代表什么，就封装进对应的数据，并且提供数据对应的行为

## 继承

多个类中存在相同属性和行为时，我们可以将这些内容抽取到单独一个类中

提取多个类的共有方法属性变量，到一个共同的父类。

提高代码复用性，防止重复代码 导致冗余和臃肿

## 多态

同一行为的多种表现形式（出现的效果不一样）

### 问答题

1. 什么叫做多态，条件是什么？ 

   同一行为的多种表现形式（出现的效果不一样）

2. 使用多态特性，带来了什么样的好处？ 

   当我们定义一个方法，这个方法的形参，是一个类，就可以传递这个类所有的子类对象！

3. 使用多态特性，注意什么样的弊端？   

   父类引用指向子类对象的情况，编译看左边，运行看右边，无法调用子类独有的方法

4. 关于多态的弊端我们如何解决？

   需要向下转型 也就是强制类型转换 ，父类引用强转为这个子类对象

   可以用 instanceof 进行转换安全判断，防止转换类型错误运行时报错

5. 在A包中我要同时使用B包下的Student和C包下的Student类，该如何使用？

   把完整路径写出来 com.xxx.xxxB.Student    com.xxx.xxxC.Student   

6. final修饰类，修饰方法，修饰变量的特点？ 

   是不可变的 类不能继承/方法不能重写/变量不能二次赋值

> static{} 静态代码块 随着类的加载而加载，并且只执行一次。

```java
public static void main(String[] args) {
    Person p1 = new Person("张三", 25);
    Person p2 = new Person("李四", 30);

    Dog dog = new Dog(2, "黑色");
    Cat cat = new Cat(3, "白色");

    p1.keepPet(dog, "骨头");
    p2.keepPet(cat, "小鱼干");
}
```

```java
Person::
public void keepPet(Animal a, String something) {
    if (a instanceof Dog) {//安全判定
        Dog d = (Dog) a;//强转
        System.out.println("年龄为" + age + "岁的" + name + "养了一只" + d.getColor() + "颜色的" + d.getAge() + "岁的狗");
        d.eat(something);
        d.lookHome();
    } else if (a instanceof Cat) {
        Cat c = (Cat) a;
        System.out.println("年龄为" + age + "岁的" + name + "养了一只" + c.getColor() + "颜色的" + c.getAge() + "岁的猫");
        c.eat(something);
        c.catchMouse();
    }else {
        System.out.println("无此类型！");
    }
}
```

# 抽象类和抽象方法

![image-20231218135609119](https://raw.githubusercontent.com/knellwake/Notes/main/img/image-20231218135609119.png)

# API

## 时间 包装类 

