# Java面向对象

[TOC]



## 类的定义

类：对事物的抽象

对象：具体的事物



Java Bean类(没有主函数，定义类而且只有类)：用来描述一类事物的类

测试类(有主函数)：用来检查其他类是否书写正确

工具类：不用来描述一类事物，而用来服务。(见名知意，私有化构造方法，方法定义为静态)



## 内存分配

方法区：字节码文件加载时进入的内存

栈内存：方法运行时所进入的内存，变量也是在这里

堆内存：new 出来的东西会在这块内存中开辟空间并产生地址

**注：栈内存中有方法区**



## static

static表示静态，是Java中的一个修饰符，可以修饰成员方法，成员变量

static声明的属性是被所有对象共享的(不属于对象，属于类)。//   一个改了其他都变。

静态变量     ： static——>变量(修饰)

静态方法     ： static——>方法(修饰)

静态方法只能访问静态变量和静态方法(及只能访问静态)，不能调用实例变量(及成员变量)

非静态方法可以访问静态变量和静态方法和非静态的(及可以访问所有)

**注：静态方法中没有this关键字**

```java
static String school = "A大学";//使用static修饰静态变量

//使用static关键字修饰静态方法
public class StaticMethod {
	public static void print(){
		System.out.println("i like java");
	}
	public static void main(String[] args) {

    //通过类名调用静态方法
    	StaticMethod.print();

    //通过对象调用静态方法
    	StaticMethod objects = new StaticMethod();
    	objects.print();
	}
}

```



## 封装

### 使用private     ，  getxxx()     ,   setxxx()方法。

重载：参数类型不同，参数数量不同，都调用不同的方法，使其赋予不同的属性。

this关键字    重名使用   ，重名不带this则为形参，带this则为实参（成员变量）。不重名，都是成员名。



### 构造方法：主要是完成对象的初始化

如果没有定义构造方法，系统将给出一个默认的无参数构造方法。

#### 格式

pubilc  + 类名()  //无参构造方法

pubilc   +   类名(参数) //有参构造方法

```java
public Phone_This() {//无参构造方法
	System.out.println("调用无参构造方法!");
}
```

```java
public Phone_This(String brand,double price) {//有参构造方法
	this.brand = brand;
	this.price = price;
	System.out.println("调用有参构造方法!");
}
```



### 代码块 ：

用 { } 括起来的代码。

其中有静态代码块，构造代码块，类的构造代码块。

静态代码块只执行1次，构造代码块定义几个成员就执行几次。



## 继承

好处：1.把子类中重复的代码提取在父类中，减少代码的冗余，提高代码复用性。2.可以让类与类之间产生父子关系。

### 子类(派生类)     父类(基类)

特点：类与类之间有共有的属性的类型和方法，Java只支持单继承，不支持多继承，但支持多层继承。(每一个类都直接或间接继承object类)

*使用extends 来使用父类*

```java
//继承的使用
class 父类 {
....
}
class 子类 extends 父类{
....
}
```

| 子类能否继承 | 非私有       | private(私有)    |
| ------------ | ------------ | ---------------- |
| 构造方法     | 不能         | 不能             |
| 成员变量     | 能           | 能(不可直接访问) |
| 成员方法     | 能(虚方法表) | 不能             |

#### 子类继承父类有那些？

父类的构造方法不能被子类继承

虚方法表(在方法区中加载)：非private、非static、非final       只有父类中的虚方法才能被子类继承。

### super和this的区别(多数重名使用)：

super：访问父类的变量(子类访问父类)[父类要有该变量名]。直接调用父类的方法。调用父类构造，必须放在子类构造方法的首行。

this：访问当前文件变量。调用方法先在本类找再在父类找。调用本类构造，必须放在构造方法的首行。

只有成员变量：则就近访问。

### 方法的重写

在继承系中，子类与父类有一模一样的方法声明，就称子类的这个方法是重写的方法。在重写中最好加@Override注释，只有在虚方法表里有的才能重写。

## 字符串

### new构造方法

使用：

1. 空参构造
2. 传递一个字符串
3. 传递一个字符数组 char[] chs
4. 传递一个字节数组 byte[] chs={98,...}===char[] chs={'a',...}

### 函数

#### 比较函数

equals()要完全一样

equalsIgnoreCase()忽略大小写

#### add()函数

add() 方法将元素插入到指定位置的动态数组中。

#### 自动添加间隔符号

1.

```java
public StringJoiner(间隔符号);
```

2.

```java
public StringJoiner(间隔符号,开始符号,结束符号);
```



#### 截取字符函数：

1.

```java
String substring(int beginIndex,int endIndex);
```

包左不包右  eg:

```java
String b = substring(3,5);
```

结果为：b=(3,4)

2.

```java
String substring(int beginIndex);
```

一直截取到末尾

#### 字符转数字

```java
char ch = '3';
int b = '3'-48;//'3'的ASCII为51
```

b的结果为3。

#### 替换

replace()函数



```java
String talk = "你好,CNM,...";
String result = talk.replace("CNM","***");
```

result的结果：   你好，***。



#### String的常用函数

reverse()反转(可以用于回文判断)                     length()获取长度                                  容量：最多装多少   capacity()                长度：已经装了多少   lenngth()

**个例：**toString()  把StringBuilder变回String

### 链式编程

当我们在调用一个方法时，不需要使用变量接收它的结果，可以继续使用其他方法。

### 区别String、StringBuilder、StringBuffer

- String：是一个不可变类(改变时则是创建新对象)
- StringBuilder：可变类(修改字符串时使用)，不要求线程安全，常用于字符串的拼接、反转。
- StringBuffer：可变类(修改字符串时使用)，要求线程安全。

### 拼接的区别

1.没有变量：拼接的时候没有变量，都是字符串，则触发字符串的优化机制。即在编译的时候已经为最终结果。(复用串池的字符串)

2.有变量：拼接的时候有变量，每次都产生一个新的字符串，浪费内存。

注：如果拼接的内容往StringBuilder中放，则不会创建很多无用的空间，节约内存。



### StringBuilder容量

默认容量：16

默认扩容：34(老容量*2+2)

超出默认扩容则以实际容量为准

