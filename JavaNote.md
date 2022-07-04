# Java学习笔记

### 1.定义对象数组并赋值(对象）：

类名 [] 数组名=new 类名 [size];

例：

```java
Student [] s1=new Student[20];

​     for(int i=0;i<s1.length;i++)
         s1[i]=new Student();
```

------

### 2.调用方法时，看清属于哪个类。

### 3.定义新对象时的内存分配

![image](https://user-images.githubusercontent.com/87485783/177168778-61b2dd0f-3a4c-497d-bd59-48790bcbca51.png)


虚拟机栈即为平时提到的栈结构，**局部变量一般存储于栈结构中**，**堆，我们将new出来的结构（比如：数组、对象）加载在堆空间中，对象的属性（非static)加载在堆空间中。**

方法区：类的加载信息、常量池、静态域。

------

### 4.对象数组的内存解析

![image](https://user-images.githubusercontent.com/87485783/177168972-951598a2-eae7-43f6-8d0d-9caf24b5d570.png)

------

### 5.匿名对象

```java
class phone{
  int num;
  int size;
  public void sendemail();
   ...
}
public static void main(String[]args){
    new phone().num;   //匿名对象调用属性
    new phone().sendemail();  //匿名对象调用方法
}
```

**常用于传参**

------

### 6.对象变量

Data是一个类

```java
Data deadline;
s=deadline.toString(); //将产生编译错误
因为deadline是一个对象变量，它并不包含对象，只能引用对象
要经过初始化：
（1）deadline=new Data(); //创造一个新对象
（2）deadline=birthday //让其引用一个已有的对象
此时才能引用函数。
```

------

### 7.UML类图

#### 1.+代表public，—表示private类型，#表示protected类型。

------

### 8.重载

 **同名不同参**

**Java的重载是可以包括父类 和子类的，即子类可以重载父类的同名不同参数的方法**

------

### 9.继承：extends，java只有公有继承。

------

### 10.javabean

**(1)类是公共的     （2）有空参构造器  （3）属性有相应的get ,set方法**

------

### 11.重写（覆盖）

**（1）子类重写的方法名和形参列表与父类被重写的方法相同；**

**（2)子类重写方法权限修饰符不小于父类被重写的；**

**（3）父类的private不能被重写；**

**（4）返回值类型：1.父类是void ，子类也要是void;**

​                                  **2.父类是基本数据类型，子类也是相同的基本数据类型**

​                                  **3.父类是A类，子类是A类或A类的子类**

**（5）子类和父类的同名同参数的方法要么都声明为static，要么都为非static;**

------

### 12.this和super

#### this:

#####        它在方法内部使用，即这个方法所属对象的引用；

#####        它在构造器内部使用，表示该构造器正在初始化的对象。

​      **当在方法内需要用到调用该方法的对象时，就用this。**

#### 注意：

   1.**可以在类的构造器中使用"this(形参列表)"的方式，调用本类中重载的其 他的构造器！** 

  2.**明确：构造器中不能通过"this(形参列表)"的方式调用自身构造器**

   3.**如果一个类中声明了n个构造器，则最多有 n - 1个构造器中使用了 "this(形参列表)"**

  4.**"this(形参列表)"必须声明在类的构造器的首行！** 

  5.**在类的一个构造器中，最多只能声明一个"this(形参列表)"**

```java
class Person{ // 定义Person类
  private String name ;
  private int age ;
  public Person(){ // 无参构造器
  System.out.println("新对象实例化") ;
  }
  public Person(String name){
  this(); // 调用本类中的无参构造器
  this.name = name ;
  }
  public Person(String name,int age){
  this(name) ; // 调用有一个参数的构造器
  this.age = age;
}
}
```

#### super:

#####     1.在子类中调用父类的方法，用super关键字。

#####      2.super构造器：子类不能访问父类私有字段时，用super构造器初始化，调用的是父类的参数。

​                                 **必须是子类构造器的第一句**

------

### 13.多态

##### 使用前提：（1）继承关系     （2）方法重写              ！只适用于方法，不支持属性 ！

**不能调用子类所特有的方法**

举例:**方法声明的形参类型为父类类型，可以使用子类的对象作为实参调用该方法**

```java
public class Test {
public void method(Person e) {
// ……
e.getInfo();
}
public static void main(Stirng args[]) {
  Test t = new Test();
  Student m = new Student();
  t.method(m); // 子类的对象m传送给父类类型的参数e
}
}
```

------

### 14.虚方法

**子类中定义了与父类同名同参数的方法，在多态情况下，将此时父类的方法称为虚拟方法，父类根据赋给它的不同子类对象，动态调用属于子类的该方法。**

```java
Person e = new Student();
e.getInfo(); //调用Student类的getInfo()方法
```

------

### 15.向下转型（强制类型转换）

**解决父类无法调用子类特有方法的问题**

##### instanceof关键字： 

```java
a instanceof A: 判断对象a是否是类A的实例，如果是，返回true。如果不是，返回false。
```

**为了避免向下转型出现异常，用改关键字进行判断，true可用，false不可用**

举例：

```java
public class Test {
public void method(Person e) { // 设Person类中没有getschool() 方法
    // System.out.pritnln(e.getschool()); //非法,编译时错误
if (e instanceof Student) {
  Student me = (Student) e; // 将e强制转换为Student类型
  System.out.pritnln(me.getschool());
}
}
public static void main(String[] args){
  Test t = new Test();
  Student m = new Student();
  t.method(m);
}
}
```

------

### 16.Object类

##### （1） equals()方法和==运算符

##### ==可以使用在基本数据类型和引用数据类型中

**重写equal方法**

```java
public boolean equals(Object obj){
   if(this==obj){
    return true;
 }
   if(obj instanceof Customer){
    Customer cust = (Customer)obj;
    //比较两个对象的每个属性是否都相同
     if(this.age==cust.age && this.name.equals(cust.name)){
     return true;
     }
     else{
      return false;
     }
     //或
     return this.age==cust.age&&this.name.equals(cust.name);
    }
    else{
      return false;
    }
   }
```

##### (2)toString()方法

------

### 17.包装类

#####  针对八种基本数据类型定义相应的引用类型—包装类（封装类）

##### （1）基本数据类型包装成包装类的实例 ---装箱

**通过包装类的构造器实现： int i = 500; Integer t = new Integer(i);**

**还可以通过字符串参数构造包装类对象： Float f = new Float(“4.56”); Long l = new Long(“asdf”);**

##### （2）获得包装类对象中包装的基本类型变量 ---拆箱

**调用包装类的.xxxValue()方法： boolean b = bObj.booleanValue();**

##### （3）字符串转换成基本数据类型

**通过包装类的构造器实现： int i = new Integer(“12”);** 

**通过包装类的parseXxx(String s)静态方法： Float f = Float.parseFloat(“12.1”);**

**（4）基本数据类型转换成字符串**

**调用字符串重载的valueOf()方法： String fstr = String.valueOf(2.34f);** 

**更直接的方式： String intStr = 5 + “   ”;**

##### （5）注：如果在一个条件表达式中混合使用Integer和Double类型，Integer值就会拆箱，提升为double，再装箱为Double:

​           **Integer n=1;**

​           **Double x=2.0;**

​           **System.out.println(true?n:x);**  **//prints 1.0**

------

### 18.static关键字

#### 使多实例共享数据

![image](https://user-images.githubusercontent.com/87485783/177169134-edf6305e-f4c9-4013-a62e-56c60636623e.png)

##### 使用范围：属性，方法，代码块，内部类                 属性若声明为静态，与该属性相关的方法也要为静态

##### 访问权限允许时，可不创建对象，直接被类调用

##### 例：

```java
class Person { 类变量应用举例
private int id;
public static int total = 0;
...
}
public static void main(String args[]){
total=100; // 不用创建对象就可以访问静态成员
...
}
}
public class StaticDemo {
public static void main(String args[]) {
Person.total = 100; // 不用创建对象就可以访问静态成员
//访问方式：类名.类属性，类名.类方法
...
}}

```

##### 类方法：

##### （1）无对象实例，可用“类名.方法名”访问static修饰的类方法。

##### （2）static修饰的类方法內部只能访问static修饰的类属性。

##### （3）static不能修饰构造器，且static修饰的方法内部不能用this和super。

##### （4）static修饰的类方法不能被重写。

------

### *19.单例设计模式

##### 饿汉式

```java
class Singleton {
// 1.私有化构造器
private Singleton() {
}
// 2.内部提供一个当前类的实例
// 4.此实例也必须静态化
private static Singleton single = new Singleton();
// 3.提供公共的静态的方法，返回当前类的对象
public static Singleton getInstance() {
return single;
}
}
```

##### 懒汉式

```java
class Singleton {
// 1.私有化构造器
private Singleton() {
}
// 2.内部提供一个当前类的实例
// 4.此实例也必须静态化
private static Singleton single;
// 3.提供公共的静态的方法，返回当前类的对象
public static Singleton getInstance() {
if(single == null) {
single = new Singleton();
}
return single;
}
}
```

应用场景：

1. 网站的计数器，一般也是单例模式实现，否则难以同步。  
2. 应用程序的日志应用，一般都使用单例模式实现，这一般是由于共享的日志 文件一直处于打开状态，因为只能有一个实例去操作，否则内容不好追加。
3. 数据库连接池的设计一般也是采用单例模式，因为数据库连接是一种数据库 资源。  项目中，读取配置文件的类，一般也只有一个对象。没有必要每次使用配置 文件数据，都生成一个对象去读取。  
4. Application 也是单例的典型应用 
5. Windows的Task Manager (任务管理器)就是很典型的单例模式  
6. Windows的Recycle Bin (回收站)也是典型的单例应用。在整个系统运行过程 中，回收站一直维护着仅有的一个实例

------

### 20.main方法

##### main方法也是一种静态方法

![image](https://user-images.githubusercontent.com/87485783/177169212-08f5c816-eafb-4f83-9cd5-ba5acdbf095f.png)

------

### 21.代码块

##### 例：

```java
class Person {
public static int total;
static {
total = 100;//为total赋初值
}
…… //其它属性或方法声明
}
```

##### （1）静态代码块：用static 修饰的代码块 

##### 1. 可以有输出语句。 

##### 2. 可以对类的属性、类的声明进行初始化操作。

##### 3. 不可以对非静态的属性初始化。即：不可以调用非静态的属性和方法。 

##### 4. 若有多个静态的代码块，那么按照从上到下的顺序依次执行。 

##### 5. 静态代码块的执行要先于非静态代码块。

##### 6. 静态代码块随着类的加载而加载，且只执行一次。

##### （2）非静态代码块：没有static修饰的代码块

**1.可以有输出语句。** 

**2.可以对类的属性、类的声明进行初始化操作。**

**3.除了调用非静态的结构外，还可以调用静态的变量或方法。**

**4.若有多个非静态的代码块，那么按照从上到下的顺序依次执行。** 

**5.每次创建对象的时候，都会执行一次。且先于构造器执行。**

![image](https://user-images.githubusercontent.com/87485783/177169299-c2aba106-9f13-49a1-8c73-679e13d5e0c3.png)

------

### 22.final关键字

#### 类似C++中的const

- #### final标记的类不能被继承

- #### final标记的方法不能被子类重写。

- #### final标记的变量(成员变量或局部变量)即称为常量。名称大写，且只能被赋值一次。

------

### 23.抽象类

##### 将一个父类设计得非常抽象，以至于它没有具体的实例，这样的类叫做抽象类。

#####  用abstract关键字来修饰一个类，这个类叫做抽象类。

#####  用abstract来修饰一个方法，该方法叫做抽象方法。 

#####  抽象方法：只有方法的声明，没有方法的实现。以分号结束： 比如：public abstract void talk()

#### 含有抽象方法的类必须被声明为抽象类。

####     **抽象类不能被实例化。抽象类是用来被继承的，抽象类的子类必须重写父类的抽象方法，并提供方法体。若没有重写全部的抽象方法，仍为抽象类。**（==父类定义的方法，子类帮忙实现，父类的对象，子类帮助创建）==

####     *不能用abstract修饰变量、代码块、构造器、私有方法、静态方法、final的方法、final的类。*

##### 举例：

```java
abstract class A{
abstract void m1(); 抽象类举例
public void m2() {
System.out.println("A类中定义的m2方法");
   }
}
class B extends A {
void m1() {
    System.out.println("B类中定义的m1方法");
  }
}
public class Test {
public static void main(String args[]) {
  A a = new B();
   a.m1();
   a.m2();
  }
}
```

