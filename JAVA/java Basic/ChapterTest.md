# Random 随机数

`(int)(Math.random() * (b - a + 1)) + a`



```java
Random ran = new Random();
int a = ran.nextInt(6) + 1;
```

> random [1 - 7)
>
> random[1 - 6]

```java
int a = ran.nextInt(6) ;
```

> random [0 - 6)

# / %

/ 除 （小数点后的不要）

% 取余数的值 （只要小数点后的值）

例子

> 153 % 10  取余 --> 15.3  只要这个余数 3 
>
> 153 / 10 除法 --> 15.3 只要整数部分  15



```
j *= j+1
j = j * (j + 1)
```



# 日期

`java.time.LocalDate` 中的 `until` 方法返回的是 `Period` 对象，表示年、月、日之间的差距。

![image-20231202211915640](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231202211915640.png)

获取总天数，可以使用 `ChronoUnit.DAYS.between` 方法。

![image-20231202212034936](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231202212034936.png)

# Scanner

next()方法读取到空白符就结束l；

nextLine()读取到回车结束也就是“\r”；

# 数学

## 不通过 / % 符号 做除法

100 / 2 == 50...0

100 - 2 循环50次 == 50...0

被除数 / 除数 = 商... 余数 

![image-20231204141809601](https://raw.githubusercontent.com/GavinGroves/Notes/main/img/image-20231204141809601.png)

减了多少次就是商 ， 减剩下的就是余数

```java
int dividend = 100;
int divisor = 2;
int count = 0;

while (dividend >= divisor){
    dividend -= divisor;
    count ++;
}
System.out.println(count+"..."+dividend);
```
