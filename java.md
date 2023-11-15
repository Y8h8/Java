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

栈内存：方法运行时所进入的内存，变量也是在这里(地址给变量，方法)

堆内存：new 出来的东西会在这块内存中开辟空间并产生地址(对象的内容，static...)

**注：栈内存中有方法区**



## static

static表示静态，是Java中的一个修饰符，可以修饰成员方法，成员变量

**注：静态变量是随着类的加载而加载的，优先于对象出现。**

在jdk8以后static存在于堆内存，jdk8以前在方法区里面的。

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



## 权限修饰符

|      修饰符       | 同一类中 | 同一包中其他类 | 不同包下的子类 | 不同包下的无关类 |
| :---------------: | :------: | :------------: | :------------: | :--------------: |
|      private      |    √     |                |                |                  |
| default(空着不写) |    √     |       √        |                |                  |
|      protect      |    √     |       √        |       √        |                  |
|      public       |    √     |       √        |       √        |        √         |

权能从小到大：private < default(空着不写) < protect < public

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



## 代码块 ：

用 { } 括起来的代码。

其中有静态代码块，构造代码块，类的构造代码块。

- 局部代码块：写在方法里面的{  }，作用：提前结束变量生命周期
- 构造代码块：就是成员代码块(优先于构造方法执行)
- 静态代码块：格式：static{}，静态代码块只执行1次，随着类的加载而加载。(用于程序刚开始的数据初始化)

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

super：

- 访问父类的变量(子类访问父类)[父类要有该变量名]。
- 直接调用父类的方法。
- 调用父类构造，必须放在子类构造方法的首行。

this：

- 访问当前文件变量。
- 调用方法先在本类找再在父类找。
- 调用本类构造，必须放在构造方法的首行。

只有成员变量：则就近访问。

**注：有参构造时，this和super不可同时出现，因为this和super在调用构造方法时都要求必须放在构造方法的首行**

### 方法的重写

在继承系中，子类与父类有一模一样的方法声明，就称子类的这个方法是重写的方法。在重写中最好加@Override注释，只有在虚方法表里有的才能重写。

## 多态

### 前提

必须要有继承，方法的重写，父类引用指向子类对象

### 特点

同类型的对象，表现出的不同形态

### 好处

使用父类作为参数，可以接收所有子类对象，体现多态的扩展性与便利。

### 弊端

不能调用子类的特有方法。

### 使用与调用

父类类型 父类对象 = 子类实例;



向上转型：(子转父)

```java
父类类型 父类对象 = 子类实例;
```

向下转型：(强转多的变少的，父转子)

```java
父类类型 父类对象 = 子类实例;
子类类型 子类对象 = (子类)父类对象;
```

变量调用：编译看左，运行看左。

方法调用：编译看左，运行看***右***。

### instanceof关键字

#### 作用

用于判断b是否是a类的实例。

***b instanceof a***

返回值为bool类型

```java
//Animal类
class Animal{
	public void shout(){
	};
}
//Dog类
class Dog extends Animal{
	public void shout(){
	System.out.println("汪汪");
	};
}

//Cat类
class Cat extends Animal{
	public void shout(){
	System.out.println("喵喵");
	};
}

public class Example{
	public static void main(String[] args){
	Animal a = new Animal();
	Dog d = new Dog();
	Cat c = new Cat();
	boolean s1 = d instanceof Animal;
	boolean s2 = c instanceof Animal;
	boolean s3 = d instanceof Cat;
	}
}
```



## final关键字

类——>不能有子类

方法——>不能被子类重写

变量——>变为常量，不可被修改(修饰基本类型：数据值不能变   ；  修饰引用类型：地址值不能变，但对象内部可以变)

常量：

- 单个单词：全部大写
- 多个单词：全部大写，单词与单词之间用下划线隔开



## 抽象

### 定义

```java
//抽象方法
abstract 返回类型 方法名(参数);
```

```java
//抽象类
abstract class 类名{
	....
}
```

抽象类不能实例化

抽象类不一定有抽象方法，但是有抽象方法一定是抽象类

可以有构造方法

抽象类的子类：

- 要么重写抽象类的所有抽象方法
- 要么是抽象类

**注：使用abstract关键字修饰的抽象方法不能使用private修饰，因为抽象方法必须被子类实现，如果用了private声明了，则子类无法实现该方法**

## 接口

什么是接口？接口就是规则 (是对行为的抽象)

### 定义

```java
public interface 接口名 {}
```

- 接口不能实例化
- 接口与类之间是实现关系，用implements关键字表示
- 接口里面抽象方法时候可以不需要public abstract，因为默认为此
- 接口里面常量可以不需要final，因为默认为此

```java
public class 类名 implements 接口名 {}
```

- 接口的子类(实现类)

  要么重写接口中的所有抽象方法

  要么是抽象类

**注：接口和类，可以单实现，可以多实现**

```java
public class 类名 implements 接口名1 , 接口名2 {}
```

**注：实现类还可以在继承一个类的同时实现多个接口**

```java
public class 类名 extends 父类 implements 接口名1 , 接口名2 {}
```

### 特点

- 成员变量

  ​		只能是常量

  ​		默认修饰符为：public static final

- 构造方法

  没有

- 成员方法

  ​			jdk7以前：只能是抽象方法，默认修饰符：public abstract

  ​			jdk8：可以定义有方法体的方法  

  ​				格式：

  - public default 返回值类型 方法名(参数列表) {} 

    ​		//默认方法不是抽象方法，故不强制重写，但是重写时要去掉default

    ​		//public可以省，default不能省略

    ​		//如果有多个接口，同时存在相同名字的默认方法，子类必须对该方法进行重写

  - public static 返回值类型 方法名(参数列表) {} 	

    ​         //只能通过接口名调用，不能实现类名调用或对象名调用

    ​         //public可以省   static不能省	

  ​			jdk9：可以定义私有方法

  ​				格式：

  - private 返回类型 方法名(参数列表){}

  ​						//给默认方法服务

  - private static 返回类型 方法名(参数列表){}

  ​						//给静态方法服务

### 接口与类的关系

- 类与类

  继承关系，只能单继承。但可以多层继承

- 类与接口

  实现关系，单多实现，可以继承一个类的同时实现多个接口

- 接口与接口

  继承关系，单多继承，最下面的子接口需要重写所有的抽象方法

## 包

定义：

- 包就是文件夹，用来管理各种不同功能的Java类。

全类名(全限定名)：包名＋类名 (包名：package 后面的一串       类名：自己定义的class的名字)

什么时候需要导包，什么时候不需要导包：

1. 使用同一个包中的类时，不需要导包
2. 使用java.lang包中的类时，不需要导包
3. 其他情况都要导包
4. 如果同时使用两个包中的同名类，需要用全类名



## 内部类

意义：b类表示a类的一部分，且b类离开了a类没有意义

类的内部定义的类  内部类

定义内部类的类就是外部类

外部类以外的就是外部其他类

![image-20231115154948955](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20231115154948955.png)

![image-20231115155135765](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20231115155135765.png)

内部类分为：成员内部类，局部内部类，静态内部类，匿名内部类

成员内部类

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20231115160841530.png" alt="image-20231115160841530" style="zoom:50%;" />

匿名内部类相当于创建对象(发生在继承或者接口中)

格式

```java
new 父类名或者接口名(){
	重写方法;
};
```



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

## 集合

### Collection接口

boolean  add(n)添加一个元素    boolean addAll(集合)将指定集合添加到该集合中

void clear()删除该集合的所有元素   boolean remove(n)删除指定元素  boolean removeAll(集合)删除指定集合所有元素

int size()获取集合元素个数(元素长度)

Object 

