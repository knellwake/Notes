---
typora-root-url: ./..\img
---

# 第四章  类型、存储和变量

## 4.4 数据成员和函数成员

- 数据成员：保存这个类对象或整个类相关的数据
- 函数成员：定义了这个类/对象的行为逻辑的实现方法细节

## 4.5 预定义类型

C#共16中预定义类型：

> 高精度小数类型 ： **decimal** 类型可以准确地表示分数，常用于货币的计算。

![image-20231026165113556](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231026165113556.png?token=APYF7FBNZXPGPSY4K2RALTDFHIUMA)

## 4.6 用户定义类型

6种：

- 类（class）
- 结构体 （struct）
- 数组 （array）
- 枚举（enum）
- 委托（delegate）
- 接口 （interface）

使用用户定义类型的步骤：先**声明**类型 -> 再**实例化**类型的对象

## 4.7 栈和堆
程序运行时，数据必须存储在内存中。
运行中的程序使用两个**内存区域**来存储数据：*栈和堆*

### 4.7.1 栈

栈是一个内存数组，LIFO（Last-In First-Out，后进先出）的数据结构。

- 数据只能从栈顶执行插入和删除
- 数据放入栈顶 ： **入栈（push）**
- 从栈顶删除：**出栈（pop）**

![image-20231026191328341](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231026191328341.png?token=APYF7FCBYMZLSMQ3T4ZCW6TFHJFBS)

### 4.7.2 堆

堆是一块内存区域，在堆中可以分配大块的内存用于存储数据，堆中能任意顺序存入和删除。

不能显式的删除堆中数据，CLR的GC（自动垃圾回收）判断堆中的某个对象不再被引用使用，就会释放对象。

![image-20231026191518995](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231026191518995.png?token=APYF7FHV363WKEENO6PP33LFHJFIM)

## 4.8 值类型和引用类型

类型决定对象在内存中的存储位置——栈和堆；

- 值类型 存储在栈中，存储实际的数据；
- 引用类型 
  - 引用（地址）存储在栈，这个地址就指向堆中的数据位置
  - 实际数据存储在堆

![image-20231026191535768](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231026191535768.png?token=APYF7FA77IBOIWWG4BL4BGDFHJFJM)

### 4.8.1 存储引用类型对象的成员

如果一个引用类型是另一个对象（类）的成员：

![image-20231027105704044](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231027105704044.png)

引用类型的任何对象，它所有数据成员都存放在堆里，无论它们是值类型还是引用类型！

### 4.8.2 C#类型的分类

![image-20231027105718422](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231027105718422.png)

## 4.9 变量

表示 程序执行时存储在内存中的数据。

4种变量：

- 局部变量        方法作用域内
- 字段                类的成员
- 参数                方法间传递的临时变量
- 数组元素        同类数据项构成有序集合的一个成员

### 4.9.1 变量声明

- 变量命名 并关联一种类型
- 让编译器分配一块内存

![image-20231027105731643](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231027105731643.png)

![image-20231027105750725](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231027105750725.png)

局部变量 无默认初始化值，需要赋值后使用。

静态类型：在编译时就确认的变量类型，运行时候不能修改。

动态类型： 变量在运行时才会确认类型，dynamic，需要确保它与变量所代表的实际类型一致，否则会抛出异常；

# 第五章 类的基本概念

运行中的程序是一组相互作用的对象的集合。

## 5.5 创建变量和类的实例

类被声明，就可以创建类的实例。

## 5.6 为数据分配内存

声明类 所分配的内存（栈空间内）是用来保存引用的，

```c#
class Test{} // 声明类

Test test; //声明引用变量
```

保存对象的实际数据（为实际数据分配内存 {堆中}），需要使用new关键字

```c#
Test test = new Test();//声明 并且 初始化
```

- new 运算符 为任意类型的实例分配 并 初始化内存。

![image-20231026164727583](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231026164727583.png?token=APYF7FFNAHWIXLGTNWX7CVDFHIT54)

## 5.7 实例成员

**类**的声明相当于**蓝图**，通过这个蓝图想创建多少个类的实例都可以。

- 实例成员   类的每个实例都是不同的实体。
- 静态成员

## 5.8 访问修饰符

- private         私有 只能总声明它的类内部访问
- public            公有
- protected
- internal
- protected internal

# 第六章 方法

## 6.3 局部变量

- 从声明它的那一刻开始存在；
- 在块内完成执行时结束存在；

![image-20231027112553243](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231027112553243.png)

### 6.3.1 类型推断和var关键字

为避免代码冗余（重复代码），可以使用var关键字；

- 只能用于局部变量，不能用于字段；
- 只能在变量声明并包含初始化时使用；
- 一旦编译器推断出变量的类型，它就是固定不能更改的；

## 6.4 局部常量

- 声明时必须初始化； 初始化值必须在编译期决定。
- 声明后不能改变

```c#
const Type Identifier = Value;
```

可以是Null引用，但是不能是某对象的引用，因为对象的引用是在运行时决定的；

## 6.8 返回语句和void方法

void声明 下 可以使用返回语句 提前退出方法以简化程序逻辑；

```c#
return;
```

## 6.10 参数

- 形参
- 实参

![image-20231027112606594](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231027112606594.png)

## 6.11 值参数

值参数：是把**实参的值复制给形参**；

方法被调用时，系统执行如下：

- 在栈中为形参分配空间
- 将实参复制给形参

引用类型的参数 -> 在栈中的引用（地址）被复制，导致 实参与形参指向同一个对象；-> so: 形参的变化 会 影响 实参

值类型参数 -> 栈中的值 复制 产生一个独立的数据项 -> 形参的变换不影响 实参

![image-20231027230237651](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231027230237651.png?token=APYF7FFDH2Z6UJPA5QMSGALFHPIUY)

## 6.12 引用参数 ref

- 方法的声明和调用中都使用**ref修饰符**。
- 实参必须是变量，必须被赋值。引用类型的变量可以赋值为Null 或 一个引用；

- 不会在栈上为形参分配内存。
- 形参将变成实参变量的别名，指向相同的内存位置。

![image-20231027230315411](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231027230315411.png?token=APYF7FDKENTA4PJX7EH7RLLFHPIXE)

## 6.13 引用类型作为值参数 和 引用参数

- **将引用类型对象 作为 值参数 传递**       
  - 如果在方法内创建一个新对象并且赋值给形参，将切断形参与实参之间的关联，
    - 并且在方法调用结束后，新对象也将不复存在；

![image-20231027230055616](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231027230055616.png?token=APYF7FBTM6DIHJOHBHL2ZDLFHPIOM)

- **引用类型对象 作为 引用参数 传递**
  - 如果在方法内创建一个新对象并且赋值给形参，在方法结束后该对象依然存在，
  - 并且 是实参所引用的值；

![image-20231027230539400](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231027230539400.png?token=APYF7FBRCMDB7TA5DPLDA7DFHPJAE)

## 6.14 输出参数 out

用于从方法体内把数据传出到调用代码。

- 方法声明和调用中都使用out修饰符；
- 实参必须是变量，不能是表达式。

输出参数的形参充当实参的别名。形参与实参都是同一块内存位置。

- 在方法内部，给输出参数赋值之后才能读取它。
  - 参数的**初始值无关**，没有必要在方法调用前为实参复制。
- 方法内部，方法返回之前，代码中每条可能的路径都必须为所有输出参数赋值。
  - 因为方法内代码**在读取输出参数之前必须对其写入**，所以**不可能使用输出参数把数据传入方法**。

![image-20231028091900012](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028091900012.png)

## 6.15 参数数组 params

- 在一个参数列表中只能有一个参数数组
- 如果有，它必须是列表中的最后一个
- 所有参数必须是同类型

**声明**参数数组时：

- params修饰符

- ```c#
  void Test(params int[] inVals){}
  ```

  **数组是一组有序的同类型数据项，*引用类型*；**

注意：

实参传入的对象 是 **值类型** 还是 **引用类型**；

不传递实际的数值，而是自己创建一个数组并且初始化，进行传递，那么编译器会使用我创建的，而不是重新创建一个。

![image-20231024232545546](E:/Typora_MD/Image/image-20231024232545546.png)

# 第七章 深入理解类

## 7.4 静态字段

静态字段被所有类的实例共享，所有类实例都访问同一内存位置。

![image-20231028092518001](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028092518001.png)

## 7.6 静态函数成员

静态成员函数不能访问实例成员，但能访问其他静态成员。

![image-20231028092949166](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028092949166.png)

## 7.9 常量与静态量

常量即使没有类实例也可以使用，但与静态量不同，常量没有自己的存储位置，而是在编译时被编译器替换。

![image-20231028105923304](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028105923304.png)

## 7.10 属性

属性是函数成员；它不一定要为数据存储分配内存！

![image-20231028110033691](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028110033691.png)

![image-20231028110342903](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028110342903.png)

- 常见方式：字段private 封装 ， 属性public 来控制从类的外部对字段的访问。

![image-20231028110455313](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028110455313.png)

- 只有一条语句时候：

![image-20231028110502823](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028110502823.png)

### 7.10.6 只读和只写属性

![image-20231028110518436](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028110518436.png)

属性比公有字段更好！

### 7.10.8 计算只读属性实例

属性并非必须和字段关联！

![image-20231028110555309](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028110555309.png)

![image-20231028110605873](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028110605873.png)

### 7.10.9 自动实现属性

允许只声明属性，编译器会自动创建隐藏后备字段，并且自动挂载get与set访问器上。

- 不声明后备字段——编译器根据属性的类型分配存储。
- 不能提供访问器的方法体——声明为分号

![image-20231028110635697](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028110635697.png)

### 7.10.10 静态属性

- 不能访问类的实例成员，但能被实例成员访问
- 不管有无实例，都存在

## 7.11 实例构造函数

在创建类的每个实例时执行。

- 用于初始化类实例的状态
- 类想在外部创建实例，需要public构造

![image-20231028110740980](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028110740980.png)

### 7.11.1 带参数的构造函数

- 构造函数可以带参数。
- 可以被重载。

### 7.11.2 默认构造函数

编译器会默认提供隐式的无参构造；

当你创建类一个有参构造，这个默认无参构造会被顶掉；

## 7.12 静态构造函数

- 实例构造函数 初始化 类的每个新实例
- static构造函数初始化类级别的项 
  - 在引用任何 静态成员 之前
  - 在 创建类的任何实例 之前
- *（静态构造函 也可以用于 初始化 类的静态字段）*



静态构造与实例构的**不同**：

- 静态static 关键字 修饰
- 类只能有一个静态构造函数，而且不能带参数
- 静态构造不能有访问修饰符

`````c#
class Test
{
    static Test()
    {
        //执行所有静态初始化
    }
}
`````

- 类可以有静态构造和实例构造；
- 静态方法、静态构造都不能访问类所在的实例成员，因此也不能使用this访问器；
- 不能显式调用静态构造，系统会自动调用：
  - 在类的任何实例被创建之前；
  - 在类的任何静态成员被引用之前；

## 7.14 析构函数

执行在类的实例被销毁之前需要清理或释放非托管资源的行为

## 7.15 readonly 修饰符

与 const 类似，一旦值被设定就不能改变；

- const 字段只能在声明时初始化（编译时决定值），在内存中没有存储位置
- readonly 可以不用声明时就初始化（值可以在运行时决定）
  - 如果是static字段，初始化要在静态构造中
- readonly 可以是实例字段、也可以是静态字段
- readonly 在内存中有存储位置

```c#
class Test
{
    readonly int num; //未初始值
    readonly double PI = 3.14;
}
```

## 7.16 this 关键字

this关键字在类中使用，是对当前实例的引用。

- 实例方法
- 实例构造
- 属性和索引器的实例访问器

不能在静态函数成员中使用this关键字

使用this的目的：

- 用于区分类的成员 和 局部变量或参数；
- 作为调用方法的实参；

## 7.17 索引器

是一组get和set访问器，与属性类似；

![image-20231028112931664](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028112931664.png)

### 7.17.2 索引器和属性

- 和属性一样，索引器不用分配内存来存储。
- 索引器和属性都主要用来访问其他数据成员。
  - 属性表示单个数据成员
  - 索引器表示多个数据成员

索引器可以为类的多个数据成员提供get和set访问的属性。

索引器不能被声明为static，它总是实例成员。

![image-20231028112807551](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028112807551.png)

## 7.18 访问器的访问修饰符

![image-20231028112956823](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028112956823.png)

![image-20231028113006549](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028113006549.png)

# 第八章 类和继承

## 8.4 屏蔽基类成员 new

- 要屏蔽一个继承的**数据成员**，需要声明一个新的相同类型的成员，并使用相同的名称
- 派生类中声明新的具有相同签名的**函数成员**，可以屏蔽父类的函数成员。
  - 签名由名称和参数列表组成，不包括返回值；
- 使用**new修饰符**，让编译器知道是故意屏蔽继承的成员。
- 也可以屏蔽静态成员。

![image-20231028113032279](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028113032279.png)

## 8.5 基类访问 base

派生类要访问被隐藏的基类成员。使用base关键字

## 8.6 使用基类的引用

![image-20231028113156599](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028113156599.png)

基类引用 无法访问 派生类成员。

### 8.6.1 虚方法 virtual 和 重写方法 override 

当使用基类引用访问派生类对象时，得到的是基类成员。

而**虚方法可以使基类的引用访问“升至”派生类内；**

使用基类引用调用派生类方法，需要满足条件：

- 派生类的方法和基类的方法有相同的签名和返回类型；
- 基类方法 使用 virtual 标注
- 派生类的方法 使用 override 标注

![image-20231028131222113](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028131222113.png)

当使用基类调用派生类的同名方法时，方法调用被传递到派生类执行。

- 虚方法和重写方法 都必须有相同的访问修饰符。
- 不能重写static方法或非虚方法。
- **方法、属性和索引器、事件** 都可以被声明virtual和override。

### 8.6.2 覆写标记为override的方法

重写方法可以在继承的任何层次出现，也就是说：

​	当使用对象基类部分的引用调用一个被重写的方法时，方法的调用被沿派生层次向上溯执行，一直到标记为override的方法的最高派生版本；

![image-20231028131232108](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028131232108.png)

在类SecondDerived中，可以使用override或new声明方法Print()。

1. 情况1：使用override声明Print()

![image-20231029105031003](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231029105031003.png)

无论是通过派生类自行实例化调用 还是 通过基类调用，都会执行最高派生类中的方法。

2. 情况2：使用new声明Print()

![image-20231029111916291](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231029111916291.png)

##　８.７　构造函数的执行

![image-20231028131251302](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028131251302.png)

创建一个实例的过程：

１.　初始化对象的所有实例成员

２.　调用基类的构造函数

３.　执行该类自己的构造

![image-20231028131306844](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028131306844.png)

### 8.7.1 构造函数初始化语句

默认情况，会调用基类的无参构造。

希望调用指定构造时：

- 使用base关键字，指明使用哪个基类构造
- 使用this关键字，指明使用当前类的哪个构造

![image-20231028131325878](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028131325878.png)



![image-20231028131344314](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028131344314.png)

![image-20231028131356173](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028131356173.png)

### 8.7.2 类访问修饰符

- public
  - 可以被系统内任何程序集中的代码访问
- internal
  - 只能被自己所在的程序集内的类看到
  - 默认访问级别

![image-20231028131412497](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028131412497.png)

## 8.9 成员访问修饰符

![image-20231028131442636](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028131442636.png)

![image-20231028131457161](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028131457161.png)

![image-20231028131512777](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028131512777.png)

## 8.10 抽象成员

指设计为被重写的函数成员。

- 必须是一个函数成员。
  - 数据成员（字段、常量）不能成为抽象成员
- abstract修饰符标记
- 不能有方法体

![image-20231028131523754](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028131523754.png)

**抽象成员只能在抽象类中声明。**

- 方法
- 属性
- 事件
- 索引器

![image-20231028131533657](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028131533657.png)

## 8.11 抽象类

抽象类只能被作用其他类的基类。设计为被继承的类。

- 抽象类不能实例化
- 使用 abstract 修饰符



- 抽象类可以包括非抽象成员和抽象成员。 
- 抽象类可以继承抽象类
- 任何派生自抽象类的类都必须被 重写 所有抽象成员，除非派生类也是抽象类；

## 8.13 静态类

静态类中所有成员都是静态的。

隐式密封，所以不能继承静态类

![image-20231028131543775](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028131543775.png)

# 第九章 表达式和运算符

对于引用类型变量，字面量Null 表示变量没有指向内存中的数据；

@ 逐字字符串字面量 ： 字符串你输入什么打出来就是什么样；

## 比较操作和相等性操作

对于大多数引用类型，是比较引用；

​	引用相等指的是 它们指向内存中相同的对象，为TRUE

​    否则，就算**两个分离的对象**在其他方面完全相等也为FALSE；

浅拷贝（浅比较）

![image-20231028131553888](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028131553888.png)

string类型也是引用类型，但是比较方式不同，字符串比较它们的长度和大小（区分大小写）；

​     即时他们占用不同的内存区域，只要长度和大小（区分大小写）相同即为TRUE

深拷贝（深比较）



委托也是引用类型，并且也是深拷贝。

​	比较两个委托时 ： 

​			如果两个委托都是Null，或调用列表中有相同数目的成员，并且调用列表相匹配，-> TRUE

## 9.7 递增运算符 和 递减运算符

![image-20231028131604275](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028131604275.png)

![image-20231028131614458](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028131614458.png)

![image-20231028131622500](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028131622500.png)

## 9.8 条件逻辑运算符

![image-20231028131636192](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028131636192.png)

## 9.12 条件运算符

![image-20231028131647825](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231028131647825.png)

## 9.16 typeof运算符

返回已知类型的 System.Type 对象

![image-20231025173040498](E:/Typora_MD/Image/image-20231025173040498.png)

![image-20231025173127540](E:/Typora_MD/Image/image-20231025173127540.png)

![image-20231025173149114](E:/Typora_MD/Image/image-20231025173149114.png)

## 9.17 nameof运算符

返回用来表示变量、类型或成员的**字符串**

![image-20231025173303267](E:/Typora_MD/Image/image-20231025173303267.png)

# 第十章 语句

## 10.15 using 语句

某些类型的非托管对象有数量限制或很耗费系统资源。在代码使用完他们后，要释放这些资源；

using语句有助于简化该过程并且确保资源被适当的处置；

**资源是指实现了System.IDisposable接口的类或结构。**

​	接口是指未实现的函数成员的集合；

​	类和接口可以选择去实现他们。



using语句帮助减少意外的运行时错误带来的潜在问题，包装类资源的使用；

​	意外的运行时错误——异常

​	可能异常代码放入try，无论有无异常都执行的代码放入——finally

![image-20231025194113823](E:/Typora_MD/Image/image-20231025194113823.png)

![image-20231025194244060](E:/Typora_MD/Image/image-20231025194244060.png)

# 第十一章 结构

- 类是引用类型，结构体是值类型；
- 结构是隐式密封的，不能被继承

## 11.2 结构是值类型

- 结构体类型的变量不能为Null
- 两个结构体变量不能引用同一对象

![image-20231025200216754](E:/Typora_MD/Image/image-20231025200216754.png)

## 11.3 对结构赋值

把一个结构赋值给另一个结构，就是将一个结构的值复制给另一个结构。

类的复制只是复制引用。

![image-20231025200609589](E:/Typora_MD/Image/image-20231025200609589.png)



## 11.4 构造函数和析构函数

结构里可以有实例构造函数和静态构造函数，但不能有析构函数。

### 11.4.1 实例构造函数

- 每个结构提供一个无参构造，这个构造会把每个成员设置成该类型的默认值。
  - 值成员设置成它们的默认值，引用成员设置成Null；

- 每个结构体都存在预定义无参构造（隐式构造函数），不能删除或重定义。
  - 可以创建另外的有参构造。      
  - 与类不同，结构体的无参构造会一直存在，不会被有参顶掉。
- 调用结构体的构造函数 ， 需要使用new运算符。
  - 即使不从堆中分配内存。

![image-20231025205245242](E:/Typora_MD/Image/image-20231025205245242.png)

- 也可以不使用new运算符，但会有限制：
  - 需要对所有数据成员赋值之后，
    - 才能使用它们的值
    - 才能调用结构的函数成员

### 11.4.2 静态构造函数

与类相似，结构的静态构造创建并初始化静态数据成员，不能引用实例成员。

允许有不带参数的静态构造函数。

- 引用结构的静态成员
- 调用显式声明的构造函数

![image-20231025205347555](E:/Typora_MD/Image/image-20231025205347555.png)

## 11.5 属性和字段初始化语句

声明结构体时，不允许使用实例属性和字段初始化语句：

![image-20231025205915407](E:/Typora_MD/Image/image-20231025205915407.png)

结构体的静态属性和静态字段都可以在声明结构体时进行初始化，即使结构体本身不是静态的。

# 第十二章 枚举

- 枚举是值类型，直接存储数据
- 枚举只有一种类型的成员：命名的整数值常量

![image-20231025213749325](E:/Typora_MD/Image/image-20231025213749325.png)

- 每个枚举成员都有一个底层整数类型，默认int
- 默认第一个成员赋值为0

- 可以把枚举值赋值给枚举类型变量。

![image-20231025214029776](E:/Typora_MD/Image/image-20231025214029776.png)

![image-20231025214130522](E:/Typora_MD/Image/image-20231025214130522.png)

![image-20231025214136831](E:/Typora_MD/Image/image-20231025214136831.png)

枚举只有单一的成员类型： 声明的成员常量。

# 第十三章 数组

- 数组一旦创建，大小就固定。

## 13.2 数组的类型

- 一维数组可以认为是单行元素或元素向量
- 多维数组是由主向量中的位置组成的，每一个位置本身又是一个数组，称为子数组。
  - 子数组向量中的位置本身又是一个子数组。

![image-20231025222636564](E:/Typora_MD/Image/image-20231025222636564.png)‘

## 13.3 数组是对象

数组的实例从system.Array继承类型的对象。从BCL基类派生而来。

数组是引用类型。数组的元素可以说值类型或引用类型。

![image-20231025222942926](E:/Typora_MD/Image/image-20231025222942926.png)

![image-20231025223027644](E:/Typora_MD/Image/image-20231025223027644.png)

## 13.4 一维数组和矩形数组

声明一维数组或矩形数组，可以在类型和变量名之间使用一对方括号。

方括号内的逗号就是**秩说明符**；它们指定了数组的维度数。秩就是逗号数加1.

 声明：  long 一维数组：

![image-20231025223514066](E:/Typora_MD/Image/image-20231025223514066.png)

![image-20231025223543011](E:/Typora_MD/Image/image-20231025223543011.png)

## 13.5 实例化一维数组或矩形数组

![image-20231025223839985](E:/Typora_MD/Image/image-20231025223839985.png)

![image-20231025223826685](E:/Typora_MD/Image/image-20231025223826685.png)

![image-20231025223803068](E:/Typora_MD/Image/image-20231025223803068.png)

## 13.6 访问数组元素

![image-20231025224059940](E:/Typora_MD/Image/image-20231025224059940.png)

## 13.7 初始化数组

数组被创建后，每个元素自动初始化为类型的默认值。

![image-20231025224246668](E:/Typora_MD/Image/image-20231025224246668.png)

### 13.7.1 显示初始化一维数组

![image-20231025224407633](E:/Typora_MD/Image/image-20231025224407633.png)

### 13.7.2 显示初始化矩形数组

![image-20231025224434887](E:/Typora_MD/Image/image-20231025224434887.png)

### 13.7.4 快捷语法 

![image-20231025224650614](E:/Typora_MD/Image/image-20231025224650614.png)

### 13.7.5 隐式类型数组

![image-20231025224751401](E:/Typora_MD/Image/image-20231025224751401.png)

### 13.7.6 综合

![image-20231025225457736](E:/Typora_MD/Image/image-20231025225457736.png)

# 第十四章 委托

可以认为委托是持有一个或多个方法的对象。执行委托会 它调用所有“持有”的方法。

![image-20231025235110406](E:/Typora_MD/Image/image-20231025235110406.png)

委托和类一样，是一种用户自定义类型。（引用类型）

类表示数据和方法的集合。

委托则持有一个或多个方法。 

delegate看作一个包含有序方法列表的对象，方法具有相同的签名和返回类型。

![image-20231029143820656](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231029143820656.png)

- 方法的列表称为调用列表。
- 委托持有的方法可以来自任何类或结构，以下两方面匹配：
  - 委托的返回类型
  - 委托的签名（包括ref和out修饰符）

- 调用列表中的方法可以说实例方法也可以是静态方法。
- 调用委托时，会执行调用列表中的所有方法。

## 14.3 声明委托类型

```c#
delegate void MyDel(int x);
```

![image-20231029162916999](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231029162916999.png)

有返回值类型和签名，也就指定了委托接受方法的形式。

![image-20231029163117761](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231029163117761.png)

## 14.4 创建委托对象

委托是引用类型，所以 有引用和对象。  在委托类型声明后，可以声明变量并创建类型的对象。

![image-20231029163450715](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231029163450715.png)

可以传入 实例方法 or 静态方法

![image-20231029163458325](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231029163458325.png)

快捷方式 ：

![image-20231029163531407](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231029163531407.png)

```c#
delegate void MyDel(int x);//声明委托类型
MyDel delVar,dVar;//创建两个委托变量

delVar = myTypeClass.Mym1;//创建委托并且保存引用
dVar = SClass.Otherm2;//创建委托并且保存引用
```

![image-20231029163819066](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231029163819066.png)

## 14.5 给委托赋值

![image-20231029165352692](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231029165352692.png)

旧的委托对象会被垃圾回收器回收。

![image-20231029165339158](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231029165339158.png)

## 14.6 组合委托

![image-20231029165456603](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231029165456603.png)

## 14.7 为委托添加方法

使用 += 运算符，实际发生的是创建了一个新的委托。

![image-20231029165528062](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231029165528062.png)

![image-20231029165539477](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231029165539477.png)

##　14.8 从委托移除方法

为空会抛出异常，可以添加if判断Null。



![image-20231029165807322](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231029165807322.png)

## 14.9 调用委托

- 像调用方法一样调用委托
- 使用委托的invoke方法

![image-20231029170059106](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231029170059106.png)

## 14.10 委托的示例

![image-20231029193134231](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231029193134231.png)

## 14.11 调用带返回值的委托

![image-20231029193447518](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231029193447518.png)

![image-20231029193229216](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231029193229216.png)

## 14.12 调用带引用参数的委托

![image-20231029215400336](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231029215400336.png)

![image-20231029215344019](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231029215344019.png)

![image-20231029215323607](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231029215323607.png)

## 14.13 匿名方法

![image-20231029215441406](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231029215441406.png)

### 14.13.1 使用匿名方法

![image-20231030101056890](/C:/Users/Administrator/AppData/Roaming/Typora/typora-user-images/image-20231030101056890.png)

![image-20231030101109295](/C:/Users/Administrator/AppData/Roaming/Typora/typora-user-images/image-20231030101109295.png)
