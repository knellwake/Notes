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