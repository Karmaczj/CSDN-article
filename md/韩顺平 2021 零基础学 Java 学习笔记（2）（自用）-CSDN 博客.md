> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/weixin_43973189/article/details/121316872?spm=1001.2014.3001.5502)

#### 目录

*   *   *   [第 10 章 面向对象编程 (高级部分)](#_10___1)
        *   [第 11 章 枚举和注解](#_11___852)
        *   [第 12 章 异常 - Exception](#_12__Exception_1164)
        *   [第 13 章 常用类](#_13___1355)

#### 第 10 章 面向对象编程 (高级部分)

10.1 类变量和类方法

10.1.4 类变量内存布局  
![](https://img-blog.csdnimg.cn/9e50c66f8c75429d902104bab5dd52d5.png)  
![](https://img-blog.csdnimg.cn/9be45e2513f740d5af83a97d9f6457ee.png)  
JDK8 以前，静态域在方法区中；到了 JDK8 以后，静态域存储于定义类型的 Class 对象，在 Class 实例的尾部，Class 对象如同堆中其他对象一样，存在于 GC 堆中。

10.1.5 什么是类变量  
![](https://img-blog.csdnimg.cn/43c0d1f2c72444fd99c4f8f0f9d964a6.png)  
10.1.6 如何定义类变量  
![](https://img-blog.csdnimg.cn/94ae1f6ff8d24b59b5816effbe8eb640.png)  
10.1.7 如何访问类变量  
![](https://img-blog.csdnimg.cn/6ee87d8edead48319385e893981f7542.png)  
10.1.8 类变量使用注意事项和细节讨论  
![](https://img-blog.csdnimg.cn/8e20e8c19ee84ddcbf8054bbcfb0712f.png)  
10.1.9 类方法基本介绍  
![](https://img-blog.csdnimg.cn/487d04ac682c4f03a8e24ecf94a5fccc.png)  
10.1.10 类方法的调用  
![](https://img-blog.csdnimg.cn/094d31fa735042d880ad4d2571a68ada.png)  
10.1.12 类方法经典的使用场景  
![](https://img-blog.csdnimg.cn/6a3a3cf459644fd6a69cab100e7ccd61.png)  
10.1.13 类方法使用注意事项和细节讨论  
![](https://img-blog.csdnimg.cn/505a147071f44f8f9fcba857155e69ec.png)  
10.2 理解 main 方法语法

10.2.1 深入理解 main 方法  
![](https://img-blog.csdnimg.cn/6ff8ff11eb0f4fbfa6d69914b0b98199.png)  
10.2.2 特别提示  
![](https://img-blog.csdnimg.cn/99f2f3036c5b4eed9b0712116f5c7750.png)  
10.2.3 动态传值  
![](https://img-blog.csdnimg.cn/1f794f33240e4cdf8de8f42f93b086ae.png)  
10.3 代码块

10.3.1 基本介绍  
![](https://img-blog.csdnimg.cn/a6068caffbe142a29708c703e86a36d7.png)  
10.3.2 基本语法  
![](https://img-blog.csdnimg.cn/e5549f3141074286a60d07de1df46a4a.png)  
10.3.3 代码块的好处和案例演示  
![](https://img-blog.csdnimg.cn/8273e19ce27d4750b5e507c5921d5d15.png)

```
package com.hspedu.codeblock_; 
public class CodeBlock01 { 
	public static void main(String[] args) { 
		Movie movie = new Movie("你好，李焕英"); 
		System.out.println("==============="); 
		Movie movie2 = new Movie("唐探 3", 100, "陈思诚"); 
	}
}
class Movie { 
	private String name; 
	private double price; 
	private String director; 
	//3 个构造器-》重载 
	//老韩解读 
	//(1) 下面的三个构造器都有相同的语句 
	//(2) 这样代码看起来比较冗余 
	//(3) 这时我们可以把相同的语句，放入到一个代码块中，即可 
	//(4) 这样当我们不管调用哪个构造器，创建对象，都会先调用代码块的内容 
	//(5) 代码块调用的顺序优先于构造器.. 
	{ 
		System.out.println("电影屏幕打开..."); 
		System.out.println("广告开始..."); 
		System.out.println("电影正式开始..."); 
	}; 
	public Movie(String name) { 
		System.out.println("Movie(String name) 被调用..."); 
		this.name = name; 
	}
	public Movie(String name, double price) {
		this.name = name; 
		this.price = price; 
	}
	public Movie(String name, double price, String director) { 
		System.out.println("Movie(String name, double price, String director) 被调用..."); 
		this.name = name; 
		this.price = price; 
		this.director = director; 
	} 
}
```

10.3.4 代码块使用注意事项和细节讨论  
![](https://img-blog.csdnimg.cn/a080190b7a9f4605afa5e3f3c8321563.png)

```
package com.hspedu.codeblock_; 
public class CodeBlockDetail01 { 
	public static void main(String[] args) { 
		//类被加载的情况举例 
		//1. 创建对象实例时(new) 
		// AA aa = new AA(); 
		//2. 创建子类对象实例，父类也会被加载, 而且，父类先被加载，子类后被加载 
		// AA aa2 = new AA(); 
		//3. 使用类的静态成员时(静态属性，静态方法) 
		// System.out.println(Cat.n1); 
		//static 代码块，是在类加载时，执行的，而且只会执行一次. 
		// DD dd = new DD(); 
		// DD dd1 = new DD(); 
		//普通的代码块，在创建对象实例时，会被隐式的调用。 
		// 被创建一次，就会调用一次。 
		// 如果只是使用类的静态成员时，普通代码块并不会执行 
		System.out.println(DD.n1);//8888, 静态模块块一定会执行 
	} 
}
class DD { 
	public static int n1 = 8888;//静态属性 
	//静态代码块 
	static {
		System.out.println("DD 的静态代码 1 被执行...");
	}
	//普通代码块, 在 new 对象时，被调用，而且是每创建一个对象，就调用一次
	//可以这样简单的，理解 普通代码块是构造器的补充 
	{ 
		System.out.println("DD 的普通代码块..."); 
	} 
}
class Animal { 
	//静态代码块 
	static {
		System.out.println("Animal 的静态代码 1 被执行...");
	} 
}
class Cat extends Animal { 
	public static int n1 = 999;//静态属性 
	//静态代码块 
	static {
		System.out.println("Cat 的静态代码 1 被执行...");
	} 
}
class BB { 
	//静态代码块 
	static {
		System.out.println("BB 的静态代码 1 被执行...");//1
	} 
}
class AA extends BB { 
	//静态代码块
	static {
		System.out.println("AA 的静态代码 1 被执行...");//2 
	} 
}
```

![](https://img-blog.csdnimg.cn/47318b41b3844b7abf41eacd2fe607a4.png)

```
package com.hspedu.codeblock_; 
public class CodeBlockDetail02 { 
	public static void main(String[] args) { 
		A a = new A();// (1) A 静态代码块 01 (2) getN1 被调用...(3)A 普通代码块 01(4)getN2 被调用...(5)A() 构造器被调用 
	} 
}
class A { 
	{ //普通代码块
		System.out.println("A 普通代码块 01"); 
	}
	private int n2 = getN2();//普通属性的初始化 
	static { //静态代码块 
		System.out.println("A 静态代码块 01"); 
	}
	//静态属性的初始化 
	private static int n1 = getN1(); 
	public static int getN1() { 
		System.out.println("getN1 被调用..."); 
		return 100; 
	}
	public int getN2() { //普通方法/非静态方法 
		System.out.println("getN2 被调用..."); 
		return 200; 
	}
	//无参构造器 
	public A() { 
		System.out.println("A() 构造器被调用"); 
	} 
}
```

![](https://img-blog.csdnimg.cn/91fa5a4339824fcfae7b562909e4549d.png)

```
package com.hspedu.codeblock_; 
public class CodeBlockDetail03 { 
	public static void main(String[] args) { 
		new BBB();//(1)AAA 的普通代码块(2)AAA() 构造器被调用(3)BBB 的普通代码块(4)BBB() 构造器被调用 
	} 
}
class AAA { //父类 Object 
	{ 
		System.out.println("AAA 的普通代码块"); 
	}
	public AAA() { 
		//(1)super() 
		//(2)调用本类的普通代码块 
		System.out.println("AAA() 构造器被调用...."); 
	}
}
class BBB extends AAA { 
	{ 
		System.out.println("BBB 的普通代码块..."); 
	}
	public BBB() { 
		//(1)super() 
		//(2)调用本类的普通代码块 
		System.out.println("BBB() 构造器被调用...."); 
	} 
}
```

![](https://img-blog.csdnimg.cn/407d575aae9741fca1fb272fefe41f8b.png)

```
package com.hspedu.codeblock_;
public class CodeBlockDetail04 { 
	public static void main(String[] args) { 
		//老师说明 
		//(1) 进行类的加载 
		//1.1 先加载 父类 A02 1.2 再加载 B02 
		//(2) 创建对象 
		//2.1 从子类的构造器开始 
		new B02();//对象 
	} 
}
class A02 { //父类 
	private static int n1 = getVal01(); 
	static {
		System.out.println("A02 的一个静态代码块..");//(2) 
	}
	{ 
		System.out.println("A02 的第一个普通代码块..");//(5) 
	}
	public int n3 = getVal02();//普通属性的初始化 
	public static int getVal01() { 
		System.out.println("getVal01");//(1) 
		return 10; 
	}
	public int getVal02() { 
		System.out.println("getVal02");//(6) 
		return 10; 
	}
	public A02() {//构造器 
		//隐藏 
		//super() 
		//普通代码和普通属性的初始化...... 
		System.out.println("A02 的构造器");//(7) 
	} 
}
class B02 extends A02 { // 
	private static int n3 = getVal03(); 
	static {
		System.out.println("B02 的一个静态代码块..");//(4) 
	}
	public int n5 = getVal04();
	{ 
		System.out.println("B02 的第一个普通代码块..");//(9)
	}
	public static int getVal03() { 
		System.out.println("getVal03");//(3) 
		return 10; 
	}
	public int getVal04() { 
		System.out.println("getVal04");//(8) 
		return 10; 
	}
	//一定要慢慢的去品.. 
	public B02() {//构造器 
		//隐藏了 
		//super() 
		//普通代码块和普通属性的初始化... 
		System.out.println("B02 的构造器");//(10) 
		// TODO Auto-generated constructor stub 
	} 
}
```

10.3.6 题 2：下面的代码输出什么？  
![](https://img-blog.csdnimg.cn/acf7aba090984f858a31abc68efd7d7f.png)  
10.4 单例设计模式

10.4.1 什么是设计模式  
![](https://img-blog.csdnimg.cn/1adc9a07da5d4687829e5464b034dac0.png)  
10.4.2 什么是单例模式  
![](https://img-blog.csdnimg.cn/68b95726e1554eeaa775e3c6bb068912.png)  
10.4.3 单例模式应用实例  
![](https://img-blog.csdnimg.cn/7e03a50af62f40248068c90677356c32.png)  
饿汉式：

```
package com.hspedu.single_; 
public class SingleTon01 {
	public static void main(String[] args) { 
		// GirlFriend xh = new GirlFriend("小红"); 
		// GirlFriend xb = new GirlFriend("小白"); 
		//通过方法可以获取对象 
		GirlFriend instance = GirlFriend.getInstance(); 
		System.out.println(instance); 
		GirlFriend instance2 = GirlFriend.getInstance(); 
		System.out.println(instance2); 
		System.out.println(instance == instance2);//T 
	} 
}
//有一个类， GirlFriend 
//只能有一个女朋友 
class GirlFriend { 
	private String name;
	//为了能够在静态方法中，返回 gf 对象，需要将其修饰为 static 
	//對象，通常是重量級的對象, 餓漢式可能造成創建了對象，但是沒有使用. 
	private static GirlFriend gf = new GirlFriend("小红红"); 
	//如何保障我们只能创建一个 GirlFriend 对象 
	//步骤[单例模式-饿汉式] 
	//1. 将构造器私有化 
	//2. 在类的内部直接创建对象(该对象是 static) 
	//3. 提供一个公共的 static 方法，返回 gf 对象 
	private GirlFriend(String name) { 
		System.out.println("構造器被調用."); 
		this.name = name; 
	}
	public static GirlFriend getInstance() { 
		return gf; 
	}
	@Override 
	public String toString() { 
		return "GirlFriend{" + 
				" + name + '\'' + 
				'}'; 
	}
}
```

懒汉式：

```
package com.hspedu.single_; 
/**
* 演示懶漢式的單例模式 
*/ 
public class SingleTon02 { 
	public static void main(String[] args) { 
		Cat instance = Cat.getInstance(); 
		System.out.println(instance); 
		//再次調用 getInstance 
		Cat instance2 = Cat.getInstance(); 
		System.out.println(instance2); 
		System.out.println(instance == instance2);//T 
	} 
}
//希望在程序運行過程中，只能創建一個 Cat 對象
//使用單例模式 
class Cat { 
	private String name; 
	public static int n1 = 999; 
	private static Cat cat ; //默認是 null 
	//步驟 
	//1.仍然構造器私有化 
	//2.定義一個 static 靜態屬性對象 
	//3.提供一個 public 的 static 方法，可以返回一個 Cat 對象 
	//4.懶漢式，只有當用戶使用 getInstance 時，才返回 cat 對象, 後面再次調用時，會返回上次創建的 cat 對象 
	// 從而保證了單例 
	private Cat(String name) { 
		System.out.println("構造器調用..."); 
		this.name = name; 
	}
	public static Cat getInstance() { 
		if(cat == null) {//如果還沒有創建 cat 對象 
			cat = new Cat("小可愛"); 
		}
		return cat; 
	}
	@Override 
	public String toString() {
		return "Cat{" + 
				" + name + '\'' + 
				'}'; 
	} 
}
```

10.4.4 饿汉式 VS 懒汉式  
![](https://img-blog.csdnimg.cn/4e7fb22c550c43098fe246d9d35bc6ae.png)  
10.5 final 关键字

10.5.1 基本介绍  
![](https://img-blog.csdnimg.cn/bd2ed94ae6f84d1b8683627ea6b83a20.png)  
10.5.2 final 使用注意事项和细节讨论  
![](https://img-blog.csdnimg.cn/c2aef6899a014ff3aafa5a2f4755da33.png)

```
package com.hspedu.final_; 
public class FinalDetail01 {
	public static void main(String[] args) { 
		CC cc = new CC(); 
	} 
}
class AA { 
	/*
	1. 定义时：如 public final double TAX_RATE=0.08; 
	2. 在构造器中 
	3. 在代码块中 
	*/ 
	public final double TAX_RATE = 0.08;//1.定义时赋值 
	public final double TAX_RATE2 ; 
	public final double TAX_RATE3 ; 
	public AA() {//构造器中赋值 
		TAX_RATE2 = 1.1; 
	}
	{//在代码块赋值 
		TAX_RATE3 = 8.8; 
	} 
}
class BB {
	/*
	如果 final 修饰的属性是静态的，则初始化的位置只能是 
	1 定义时 2 在静态代码块 不能在构造器中赋值。 
	*/ 
	public static final double TAX_RATE = 99.9; 
	public static final double TAX_RATE2 ; 
	static {
		TAX_RATE2 = 3.3; 
	} 
}
//final 类不能继承，但是可以实例化对象 
final class CC { } 
//如果类不是 final 类，但是含有 final 方法，则该方法虽然不能重写，但是可以被继承 
//即，仍然遵守继承的机制. 
class DD { 
	public final void cal() { 
		System.out.println("cal()方法"); 
	} 
}
class EE extends DD { }
```

![](https://img-blog.csdnimg.cn/6074663ab4bc42ce952c12dbddaa8e87.png)

```
package com.hspedu.final_; 
public class FinalDetail02 { 
	public static void main(String[] args) { 
		System.out.println(BBB.num); 
		//包装类,String 是 final 类，不能被继承 
	} 
}
//final 和 static 往往搭配使用，效率更高，不会导致类加载.底层编译器做了优化处理 
class BBB { 
	public final static int num = 10000; 
	static {
		System.out.println("BBB 静态代码块被执行"); 
	}
}
```

输出：

10.5.3 final 应用实例  
![](https://img-blog.csdnimg.cn/1324902620b140e6977a36994ea75f0e.png)  
10.6 抽象类

10.6.2 解决之道 - 抽象类快速入门  
![](https://img-blog.csdnimg.cn/d966074effed4e5c9251aa44c4cb02bf.png)

10.6.3 抽象类的介绍  
![](https://img-blog.csdnimg.cn/787d39306ebb42cf954ce3e67234a1ab.png)  
10.6.4 抽象类使用的注意事项和细节讨论  
![](https://img-blog.csdnimg.cn/973671d2cd7a48c09278ba452d69fe1b.png)  
![](https://img-blog.csdnimg.cn/1a7cfc91d0b1488e85c8f2f85ec96cd4.png)  
![](https://img-blog.csdnimg.cn/1cf4d2ced6184f638b5167e80b52f0cd.png)  
10.6.6 课堂练习题  
![](https://img-blog.csdnimg.cn/2fdd562b5ac247c7a2f735b1108446f7.png)  
10.7 抽象类最佳实践 - 模板设计模式

10.7.1 基本介绍  
![](https://img-blog.csdnimg.cn/1bfd3d0ed9c74228a6bb6bdc3eef91fa.png)  
10.7.2 模板设计模式能解决的问题  
![](https://img-blog.csdnimg.cn/8252850c2eb5456f99a617c1c2cd0da9.png)  
10.7.3 最佳实践  
![](https://img-blog.csdnimg.cn/59f2c835de754fc48f4eccb077b9e988.png)  
![](https://img-blog.csdnimg.cn/cecd27a5ef77481eae91ece57bd553b6.png)  
![](https://img-blog.csdnimg.cn/f8444d4e48cb49bba32a04adf35869e5.png)  
10.8 接口

10.8.1 为什么有接口  
![](https://img-blog.csdnimg.cn/066a6b26902c4e4986d14dc4c67c95d1.png)  
10.8.3 基本介绍  
![](https://img-blog.csdnimg.cn/b9d69045f44443d5934328698c558ceb.png)  
10.8.4 深入讨论  
![](https://img-blog.csdnimg.cn/3ffb4bb788ee4f7d8681fb357ff70cae.png)  
![](https://img-blog.csdnimg.cn/b680a386d25843f2b9a683123340ef09.png)

```
package com.hspedu.interface_; 
public interface DBInterface { //项目经理 
	public void connect();//连接方法 
	public void close();//关闭连接 
}
package com.hspedu.interface_; 
//A 程序 
public class MysqlDB implements DBInterface { 
	@Override 
	public void connect() { 
		System.out.println("连接 mysql");
	}
	@Override 
	public void close() { 
		System.out.println("关闭 mysql"); 
	} 
}
package com.hspedu.interface_; 
//B 程序员连接 Oracle 
public class OracleDB implements DBInterface{ 
	@Override 
	public void connect() { 
		System.out.println("连接 oracle"); 
	}
	@Override 
	public void close() { 
		System.out.println("关闭 oracle"); 
	} 
}
package com.hspedu.interface_; 
public class Interface03 { 
	public static void main(String[] args) {
		MysqlDB mysqlDB = new MysqlDB(); 
		t(mysqlDB); 
		OracleDB oracleDB = new OracleDB(); 
		t(oracleDB); 
	}
	public static void t(DBInterface db) { 
		db.connect(); 
		db.close(); 
	} 
}
```

10.8.5 注意事项和细节  
![](https://img-blog.csdnimg.cn/8b4b43acd7314f6eb448f76293ef8653.png)  
![](https://img-blog.csdnimg.cn/27d0398dcca0455cb712526c35be80d7.png)  
10.8.6 课堂练习  
![](https://img-blog.csdnimg.cn/9584491cd3984b098d312a66550d8f09.png)  
10.8.7 实现接口 vs 继承类  
![](https://img-blog.csdnimg.cn/ba560d0aa7ea431e9014038ef59b59dc.png)  
10.8.8 接口的多态特性  
![](https://img-blog.csdnimg.cn/0988fcafcbde457f9cf003f09e90e4fb.png)

```
package com.hspedu.interface_; 
public class InterfacePolyParameter { 
	public static void main(String[] args) { 
		//接口的多态体现 
		//接口类型的变量 if01 可以指向 实现了 IF 接口类的对象实例 
		IF if01 = new Monster(); 
		if01 = new Car(); 
		//继承体现的多态 
		//父类类型的变量 a 可以指向 继承 AAA 的子类的对象实例 
		AAA a = new BBB(); 
		a = new CCC(); 
	} 
}
interface IF {} 
class Monster implements IF{} 
class Car implements IF{} 
class AAA { }
class BBB extends AAA {} 
class CCC extends AAA {}
```

![](https://img-blog.csdnimg.cn/04c4fd61d2c84b70968d78f58ba23de7.png)

```
package com.hspedu.interface_; 
public class InterfacePolyArr { 
	public static void main(String[] args) { 
		//多态数组 -> 接口类型数组 
		Usb[] usbs = new Usb[2]; 
		usbs[0] = new Phone_(); 
		usbs[1] = new Camera_(); 
		/*给 Usb 数组中，存放 Phone 和 相机对象，Phone 类还有一个特有的方法 call（）， 
		请遍历 Usb 数组，如果是 Phone 对象，除了调用 Usb 接口定义的方法外， 
		还需要调用 Phone 特有方法 call */ 
		for(int i = 0; i < usbs.length; i++) {
			usbs[i].work();//动态绑定.. 
			//和前面一样，我们仍然需要进行类型的向下转型 
			if(usbs[i] instanceof Phone_) {//判断他的运行类型是 Phone_ 
				((Phone_) usbs[i]).call(); 
			} 
		} 
	} 
}
interface Usb{ 
	void work(); 
}
class Phone_ implements Usb { 
	public void call() { 
		System.out.println("手机可以打电话..."); 
	}
	@Override public void work() { 
		System.out.println("手机工作中..."); 
	} 
}
class Camera_ implements Usb { 
	@Override
	public void work() { 
		System.out.println("相机工作中..."); 
	} 
}
```

![](https://img-blog.csdnimg.cn/b2bbbc4696a7451b9993ce089b2de011.png)

```
package com.hspedu.interface_; 
public class InterfacePolyPass { 
	public static void main(String[] args) { 
		//接口类型的变量可以指向，实现了该接口的类的对象实例 
		IG ig = new Teacher(); 
		//如果 IG 继承了 IH 接口，而 Teacher 类实现了 IG 接口 
		//那么，实际上就相当于 Teacher 类也实现了 IH 接口. 
		//这就是所谓的 接口多态传递现象. 
		IH ih = new Teacher(); 
	} 
}
interface IH { 
	void hi(); 
}
interface IG extends IH{ } 
class Teacher implements IG {
	@Override 
	public void hi() { 
	} 
}
```

类的五大成员：（1）属性 （2）方法 （3）构造器 （4）代码块 （5）内部类

10.9 内部类

10.9.1 基本介绍  
![](https://img-blog.csdnimg.cn/fbe9e808317f40979d0d6ea580d12adf.png)  
10.9.2 基本语法  
![](https://img-blog.csdnimg.cn/90c40ea410de4c228bc98b4464b69084.png)  
10.9.4 内部类的分类  
![](https://img-blog.csdnimg.cn/0da78e4317b64f2092ec644392fb67fa.png)  
10.9.5 局部内部类的使用  
![](https://img-blog.csdnimg.cn/5ab9f257010440459bc7049705b3b8d8.png)

```
package com.hspedu.innerclass; 
// 演示局部内部类的使用 
public class LocalInnerClass {// 
	public static void main(String[] args) { 
		//演示一遍 
		Outer02 outer02 = new Outer02(); 
		outer02.m1(); 
		System.out.println("outer02 的 hashcode=" + outer02); 
	} 
}
class Outer02 {//外部类 
	private int n1 = 100; 
	private void m2() { 
		System.out.println("Outer02 m2()"); 
	}//私有方法 
	public void m1() {//方法 
		//1.局部内部类是定义在外部类的局部位置,通常在方法 
		//3.不能添加访问修饰符,但是可以使用 final 修饰 
		//4.作用域 : 仅仅在定义它的方法或代码块中 
		final class Inner02 {//局部内部类(本质仍然是一个类) 
			//2.可以直接访问外部类的所有成员，包含私有的
			private int n1 = 800; 
			public void f1() { 
				//5. 局部内部类可以直接访问外部类的成员，比如下面 外部类 n1 和 m2() 
				//7. 如果外部类和局部内部类的成员重名时，默认遵循就近原则，如果想访问外部类的成员， 
				// 使用 外部类名.this.成员）去访问 
				// 老韩解读 Outer02.this 本质就是外部类的对象, 即哪个对象调用了 m1, Outer02.this 就是哪个对象 
				System.out.println("n1=" + n1 + " 外部类的 n1=" + Outer02.this.n1); 
				//如果这里去掉Outer02，改成this.n1，则这个this对象指的是第6点处的inner02
				System.out.println("Outer02.this hashcode=" + Outer02.this); 
				m2(); 
			} 
		}
		//6. 外部类在方法中，可以创建 Inner02 对象，然后调用方法即可 
		Inner02 inner02 = new Inner02(); 
		inner02.f1(); 
	} 
}
```

10.9.6 匿名内部类的使用 (重要!!!)  
![](https://img-blog.csdnimg.cn/c94b6cb28d154b5f9a4cb9744ea826d9.png)  
anonymous：匿名

```
package com.hspedu.innerclass; 
/**
* 演示匿名内部类的使用 
*/ 
public class AnonymousInnerClass { 
	public static void main(String[] args) { 
		Outer04 outer04 = new Outer04(); 
		outer04.method(); 
	} 
}
class Outer04 { //外部类 
	private int n1 = 10;//属性 
	public void method() {//方法 
		//基于接口的匿名内部类 
		//老韩解读 
		//1.需求： 想使用 IA 接口,并创建对象 
		//2.传统方式，是写一个类，实现该接口，并创建对象 
		//3.老韩需求是 Tiger/Dog 类只是使用一次，后面再不使用 
		//4. 可以使用匿名内部类来简化开发 
		//5. tiger 的编译类型 ? IA 
		//6. tiger 的运行类型 ? 就是匿名内部类 Outer04$1 
		/* 
			我们看底层 会分配 类名 Outer04$1
			class Outer04$1 implements IA { 
				@Override 
				public void cry() { 
					System.out.println("老虎叫唤..."); 
				} 
			} 
		*/ 
		//7. jdk 底层在创建匿名内部类 Outer04$1,立即马上就创建了 Outer04$1 实例，并且把地址 
		// 返回给 tiger 
		//8. 匿名内部类使用一次，就不能再使用 
		IA tiger = new IA() { 
			@Override 
			public void cry() { 
				System.out.println("老虎叫唤..."); 
			} 
		}; 
		System.out.println("tiger 的运行类型=" + tiger.getClass()); 
		tiger.cry(); 
		tiger.cry(); 
		tiger.cry(); //实例用多少次都行，但匿名内部类只能使用一次
		// IA tiger = new Tiger(); 
		// tiger.cry(); 
		//演示基于类的匿名内部类 
		//分析
		//1. father 编译类型 Father 
		//2. father 运行类型 Outer04$2 
		//3. 底层会创建匿名内部类 
		/* 
			class Outer04$2 extends Father{ 
				@Override 
				public void test() { 
					System.out.println("匿名内部类重写了 test 方法"); 
				}
			}
		*/ 
		//4. 同时也直接返回了 匿名内部类 Outer04$2 的对象 
		//5. 注意("jack") 参数列表会传递给 构造器 
		Father father = new Father("jack"){ 
			@Override 
			public void test() { 
				System.out.println("匿名内部类重写了 test 方法"); 
			} 
		}; //如果把方法体去掉，则运行类型为father
		System.out.println("father 对象的运行类型=" + father.getClass());//Outer04$2 
		father.test(); 
		//基于抽象类的匿名内部类 
		Animal animal = new Animal(){ 
			@Override
			void eat() { 
				System.out.println("小狗吃骨头..."); 
			}
		}; 
		animal.eat();
	}
}
interface IA {//接口
	public void cry();
}
class Father {//类
	public Father(String name) {//构造器 
		System.out.println("接收到 name=" + name);
	}
	public void test() {//方法
	}
}
abstract class Animal { //抽象类
	abstract void eat();
}
```

![](https://img-blog.csdnimg.cn/0637d9f98d1a41f39c4faad1200b2297.png)  
10.9.8 匿名内部类课堂练习  
![](https://img-blog.csdnimg.cn/83c064aff45e4719b7452d03804e9731.png)

```
package com.hspedu.innerclass; 
public class InnerClassExercise02 { 
	public static void main(String[] args) {
		CellPhone cellPhone = new CellPhone();
		cellPhone.alarmClock(new Bell() {
			@Override
			public void ring() {
				System.out.println("懒猪起床了");
			}
		});
		cellPhone.alarmClock(new Bell() {
			@Override
			public void ring() {
				System.out.println("小伙伴上课了");
			}
		});
	}
}
interface Bell{ //接口
	void ring();//方法
}
class CellPhone{//类
	public void alarmClock(Bell bell){//形参是 Bell 接口类型
		System.out.println(bell.getClass());
		bell.ring();//动态绑定
	}
}
```

10.9.9 成员内部类的使用  
![](https://img-blog.csdnimg.cn/2fb3754d79e541398ed605a9ccbbb02e.png)  
![](https://img-blog.csdnimg.cn/b997728338914d898092b867e2009e77.png)  
![](https://img-blog.csdnimg.cn/4382af79435b4855ab7dfcd440858f6a.png)

```
package com.hspedu.innerclass;
public class MemberInnerClass01 {
	public static void main(String[] args) {
		Outer08 outer08 = new Outer08();
		outer08.t1();
		//外部其他类，使用成员内部类的三种方式
		//老韩解读
		// 第一种方式
		// outer08.new Inner08(); 相当于把 new Inner08()当做是 outer08 成员
		// 这就是一个语法，不要特别的纠结.
		Outer08.Inner08 inner08 = outer08.new Inner08();
		inner08.say();
		// 第二方式 在外部类中，编写一个方法，可以返回 Inner08 对象
		Outer08.Inner08 inner08Instance = outer08.getInner08Instance();
		inner08Instance.say();
	}
}
class Outer08 { //外部类
	private int n1 = 10;
	public String name = "张三";
	private void hi() {
		System.out.println("hi()方法...");
	}
	//1.注意: 成员内部类，是定义在外部内的成员位置上
	//2.可以添加任意访问修饰符(public、protected 、默认、private),因为它的地位就是一个成员
	public class Inner08 {//成员内部类
		private double sal = 99.8;
		private int n1 = 66;
		public void say() {
			//可以直接访问外部类的所有成员，包含私有的
			//如果成员内部类的成员和外部类的成员重名，会遵守就近原则.
			//可以通过 外部类名.this.属性 来访问外部类的成员
			System.out.println("n1 = " + n1 + " name = " + name + " 外部类的 n1=" + Outer08.this.n1);
			hi();
		}
	}
	//方法，返回一个 Inner08 实例
	public Inner08 getInner08Instance(){
		return new Inner08();
	}
	//写方法
	public void t1() {
		//使用成员内部类
		//创建成员内部类的对象，然后使用相关的方法
		Inner08 inner08 = new Inner08();
		inner08.say();
		System.out.println(inner08.sal);
	}
}
```

10.9.10 静态内部类的使用  
![](https://img-blog.csdnimg.cn/d0d803651f8846168092ee5f148dd00a.png)  
![](https://img-blog.csdnimg.cn/cb7fa1f96d2f40b88e7a12a08edac9be.png)  
![](https://img-blog.csdnimg.cn/c46f53451d264c2da852dfffc6673336.png)  
![](https://img-blog.csdnimg.cn/05dbe747a5d845e7acb42ca0ff7792e3.png)  
10.10 卖油翁和老黄牛  
![](https://img-blog.csdnimg.cn/9242fbe1d49146469e19d6d87ae46735.png)

#### 第 11 章 枚举和注解

11.3 枚举  
![](https://img-blog.csdnimg.cn/d1c49d0993ce4a07aa3541ed6eae4f9e.png)  
11.4 枚举的二种实现方式  
![](https://img-blog.csdnimg.cn/9dc8f1d6cb18402cae46faeeac97720c.png)  
11.6 自定义类实现枚举 - 小结  
![](https://img-blog.csdnimg.cn/e67b32416f344fc98739439ca9785246.png)  
11.7 enum 关键字实现枚举 - 快速入门

```
package com.hspedu.enum_;
public class Enumeration03 {
	public static void main(String[] args) {
		System.out.println(Season2.AUTUMN);
		System.out.println(Season2.SUMMER);
	}
}
//演示使用 enum 关键字来实现枚举类
enum Season2 {//类
	//如果使用了 enum 来实现枚举类
	//1. 使用关键字 enum 替代 class
	//2. public static final Season SPRING = new Season("春天", "温暖") 直接使用
	// SPRING("春天", "温暖") 解读 常量名(实参列表)
	//3. 如果有多个常量(对象)， 使用 ,号间隔即可
	//4. 如果使用 enum 来实现枚举，要求将定义常量对象，写在前面
	//5. 如果我们使用的是无参构造器，创建常量对象，则可以省略 ()
	SPRING("春天", "温暖"),
	WINTER("冬天", "寒冷"),
	AUTUMN("秋天", "凉爽"),
	SUMMER("夏天", "炎热"),
	WHAT();
	private String name;
	private String desc;//描述
	private Season2() {//无参构造器
	}
	private Season2(String name, String desc) {
		this.name = name;
		this.desc = desc;
	}
	public String getName() {
		return name;
	}
	public String getDesc() {
		return desc;
	}
	@Override public String toString() {
		return "Season{" +
				" + name + '\'' +
				", desc='" + desc + '\'' +
				'}';
	}
}
```

11.7.2 enum 关键字实现枚举注意事项  
![](https://img-blog.csdnimg.cn/aa8f3921d8e04f3d91847708cf0b7657.png)  
![](https://img-blog.csdnimg.cn/6e04dbb052ea4783a2aa4c4292bc7cc1.png)  
11.8 enum 关键字实现枚举 - 课堂练习  
![](https://img-blog.csdnimg.cn/1e4574dc716a48a6bb377d26adde46c9.png)  
11.9 enum 常用方法说明  
![](https://img-blog.csdnimg.cn/132a7476531f4e4587c8213e29b7fae9.png)  
![](https://img-blog.csdnimg.cn/2d346c02234e436692e546f7b8689044.png)  
11.10 enum 常用方法应用实例  
![](https://img-blog.csdnimg.cn/5a7289a00546457a888022bd2532e5e8.png)

```
package com.hspedu.enum_;
public class EnumMethod {
	public static void main(String[] args) {
		//使用 Season2 枚举类，来演示各种方法
		Season2 autumn = Season2.AUTUMN;
		//输出枚举对象的名字
		System.out.println(autumn.name());
		//ordinal() 输出的是该枚举对象的次序/编号，从 0 开始编号
		//AUTUMN 枚举对象是第三个，因此输出 2
		System.out.println(autumn.ordinal());
		//从反编译可以看出 values 方法，返回 Season2[
		//含有定义的所有枚举对象
		Season2[] values = Season2.values();
		System.out.println("===遍历取出枚举对象(增强 for)====");
		for (Season2 season: values) {//增强 for 循环
			System.out.println(season);
		}
		//valueOf：将字符串转换成枚举对象，要求字符串必须为已有的常量名，否则报异常
		//执行流程
		//1. 根据你输入的 "AUTUMN" 到 Season2 的枚举对象去查找
		//2. 如果找到了，就返回，如果没有找到，就报错
		Season2 autumn1 = Season2.valueOf("AUTUMN");
		System.out.println("autumn1=" + autumn1);
		System.out.println(autumn == autumn1);
		
		//compareTo：比较两个枚举常量，比较的就是编号
		//老韩解读
		//1. 就是把 Season2.AUTUMN 枚举对象的编号 和 Season2.SUMMER 枚举对象的编号比较
		//2. 看看结果
		/*
		public final int compareTo(E o) {
			return self.ordinal - other.ordinal;
		}
		Season2.AUTUMN 的编号[2] - Season2.SUMMER 的编号[3]
		*/
		System.out.println(Season2.AUTUMN.compareTo(Season2.SUMMER));
		
		//补充一个增强 for
		// int[] nums = {1, 2, 9};
		//普通的 for 循环
		// System.out.println("=====普通的 for=====");
		// for (int i = 0; i < nums.length; i++) {
		// 		System.out.println(nums[i]);
		// }
		// System.out.println("=====增强的 for=====");
		//执行流程是 依次从 nums 数组中取出数据，赋给 i, 如果取出完毕，则退出 for
		// for(int i : nums) {
		// 		System.out.println("i=" + i);
		// }
	}
}
```

![](https://img-blog.csdnimg.cn/05408ac75b5345b5ab256381daffd824.png)

```
package com.hspedu.enum_;
public class EnumExercise02 {
	public static void main(String[] args) {
		//获取到所有的枚举对象， 即数组
		Week[] weeks = Week.values();
		//遍历，使用增强 for
		System.out.println("===所有星期的信息如下===");
		for (Week week : weeks) {
			System.out.println(week);
		}
	}
}
enum Week {
	//定义 Week 的枚举对象
	MONDAY("星期一"), TUESDAY("星期二"), WEDNESDAY("星期三"), THURSDAY("星期四"),
	FRIDAY("星期五"), SATURDAY("星期六"), SUNDAY("星期日");
	private String name;
	private Week(String name) {//构造器
		this.name = name;
	}
	@Override
	public String toString() {
		return name;
	}
}
```

11.11 enum 实现接口  
![](https://img-blog.csdnimg.cn/b61c48d9acbf46a0947f2331fa5fcb21.png)  
11.12 注解的理解  
![](https://img-blog.csdnimg.cn/cbebc0c9d5144a4882a4716a797b6d62.png)  
11.13 基本的 Annotation 介绍  
![](https://img-blog.csdnimg.cn/60de6785383346a3a407cc6441888bec.png)  
11.14 基本的 Annotation 应用案例

11.14.1 @Override 注解的案例 Override_.java  
![](https://img-blog.csdnimg.cn/a9089e417a274197adab9d867759d219.png)

```
package com.hspedu.annotation_;
public class Override_ {
	public static void main(String[] args) {
	}
}
class Father{//父类
	public void fly(){
		System.out.println("Father fly...");
	}
	public void say(){}
}
class Son extends Father {//子类
	//老韩解读
	//1. @Override 注解放在 fly 方法上，表示子类的 fly 方法时重写了父类的 fly
	//2. 这里如果没有写 @Override 还是重写了父类 fly
	//3. 如果你写了@Override 注解，编译器就会去检查该方法是否真的重写了父类的
	//方法，如果的确重写了，则编译通过，如果没有构成重写，则编译错误
	//4. 看看 @Override 的定义
	//解读： 如果发现 @interface 则表示它是一个注解类
	/*
		@Target(ElementType.METHOD)
		@Retention(RetentionPolicy.SOURCE)
		public @interface Override {
		}
	*/
	@Override //说明
	public void fly() {
		System.out.println("Son fly....");
	}
	@Override
	public void say() {}
}
```

![](https://img-blog.csdnimg.cn/2fd944ba90e94cf69f4d599c657af83e.png)  
11.14.2 @Deprecated 注解的案例 Deprecated_.java  
![](https://img-blog.csdnimg.cn/693ff6fb83974a0c89f9581a72727254.png)  
![](https://img-blog.csdnimg.cn/52a32535a0a3440a8bafcf655a73e4fd.png)

```
package com.hspedu.annotation_;
public class Deprecated_ {
	public static void main(String[] args) {
		A a = new A();
		a.hi();
		System.out.println(a.n1);
	}
}
//老韩解读
//1. @Deprecated 修饰某个元素, 表示该元素已经过时
//2. 即不再推荐使用，但是仍然可以使用
//3. 查看 @Deprecated 注解类的源码
//4. 可以修饰方法，类，字段, 包, 参数 等等
//5. @Deprecated 可以做版本升级过渡使用
/*
@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target(value={CONSTRUCTOR, FIELD, LOCAL_VARIABLE, METHOD, PACKAGE, PARAMETER, TYPE})
public @interface Deprecated {
}
*/
@Deprecated
class A {
	@Deprecated
	public int n1 = 10;
	@Deprecated
	public void hi(){ }
}
```

11.14.3 @SuppressWarnings 注解的案例 SuppressWarnings_.java  
![](https://img-blog.csdnimg.cn/111e557eab8741fc862e5fde33f1b736.png)

```
package com.hspedu.annotation_;
import java.util.ArrayList;
import java.util.List;
@SuppressWarnings({"rawtypes", "unchecked", "unused"})
public class SuppressWarnings_ {
	//老韩解读
	//1. 当我们不希望看到这些警告的时候，可以使用 SuppressWarnings 注解来抑制警告信息
	//2. 在{""} 中，可以写入你希望抑制(不显示)警告信息
	//3. 关于 SuppressWarnings 作用范围是和你放置的位置相关
	// 比如 @SuppressWarnings 放置在 main 方法，那么抑制警告的范围就是 main
	// 通常我们可以放置具体的语句, 方法, 类.
	//4. 看看 @SuppressWarnings 源码
	//(1) 放置的位置就是 TYPE, FIELD, METHOD, PARAMETER, CONSTRUCTOR, LOCAL_VARIABLE
	//(2) 该注解类有数组 String[] values() 设置一个数组比如 {"rawtypes", "unchecked", "unused"}
	/*
		@Target({TYPE, FIELD, METHOD, PARAMETER, CONSTRUCTOR, LOCAL_VARIABLE})
		@Retention(RetentionPolicy.SOURCE)
		public @interface SuppressWarnings {
			String[] value();
		}
	*/
	public static void main(String[] args) {
		List list = new ArrayList();
		list.add("jack");
		list.add("tom");
		list.add("mary");
		int i;
		System.out.println(list.get(1));
	}
	public void f1() {
		// @SuppressWarnings({"rawtypes"})
		List list = new ArrayList();
		list.add("jack");
		list.add("tom");
		list.add("mary");
		// @SuppressWarnings({"unused"})
		int i;
		System.out.println(list.get(1));
	}
}
```

```
可以指定的警告类型有
all，抑制所有警告
 boxing，抑制与封装/拆装作业相关的警告
cast，抑制与强制转型作业相关的警告
dep-ann，抑制与淘汰注释相关的警告
deprecation，抑制与淘汰的相关警告
fallthrough，抑制与 switch 陈述式中遗漏 break 相关的警告
finally，抑制与未传回 finally 区块相关的警告
hiding，抑制与隐藏变数的区域变数相关的警告
incomplete-switch，抑制与 switch 陈述式(enum case)中遗漏项目相关的警告
javadoc，抑制与 javadoc 相关的警告
nls，抑制与非 nls 字串文字相关的警告
null，抑制与空值分析相关的警告
rawtypes，抑制与使用 raw 类型相关的警告
resource，抑制与使用 Closeable 类型的资源相关的警告
restriction，抑制与使用不建议或禁止参照相关的警告
serial，抑制与可序列化的类别遗漏 serialVersionUID 栏位相关的警告
static-access，抑制与静态存取不正确相关的警告
static-method，抑制与可能宣告为 static 的方法相关的警告
super，抑制与置换方法相关但不含 super 呼叫的警告
synthetic-access，抑制与内部类别的存取未最佳化相关的警告
sync-override，抑制因为置换同步方法而遗漏同步化的警告
unchecked，抑制与未检查的作业相关的警告
unqualified-field-access，抑制与栏位存取不合格相关的警告
unused，抑制与未用的程式码及停用的程式码相关的警告
```

![](https://img-blog.csdnimg.cn/7247004634eb4c51be04cd038c63f35c.png)  
11.15 JDK 的元 Annotation(元注解， 了解)

11.15.1 元注解的基本介绍  
![](https://img-blog.csdnimg.cn/a0a463cb643c43a89cf70d851598b232.png)  
11.15.2 元注解的种类 (使用不多，了解, 不用深入研究)  
![](https://img-blog.csdnimg.cn/68573a63923a4d2caec54d2cb9301966.png)  
11.15.3 @Retention 注解  
![](https://img-blog.csdnimg.cn/c175ec3f0b84453fae3db5126c22b09a.png)  
![](https://img-blog.csdnimg.cn/b1df7bf35cd649f8a631302514bbd73e.png)  
![](https://img-blog.csdnimg.cn/de4e6da3e8e447cab31af4f6ab38279f.png)  
11.15.4 @Target  
![](https://img-blog.csdnimg.cn/617946988d274e3eb02d2bd192a957f8.png)  
![](https://img-blog.csdnimg.cn/3524a37880864ebe9bd6200cc4e05801.png)  
11.15.5 @Documented  
![](https://img-blog.csdnimg.cn/4736c73814c740c4a1684e5b4463f607.png)  
![](https://img-blog.csdnimg.cn/dfe8cef847264b86aa0f18ce9e9d2cc3.png)  
11.15.6 @Inherited 注解  
![](https://img-blog.csdnimg.cn/3bb195eb7a5b4e1cb12e764a10eb5d72.png)

#### 第 12 章 异常 - Exception

12.2 异常捕获  
将该代码块 -> 选中 -> 快捷键 ctrl + alt + t -> 选中 try-catch

12.3 异常介绍  
![](https://img-blog.csdnimg.cn/ab663fb1b00c4f3b9cc474b738c3f8ce.png)  
12.4 异常体系图一览

12.4.1 异常体系图  
![](https://img-blog.csdnimg.cn/3ccd97120e6942d186e807f1cb284c60.png)  
右键 ->Show Implementations 快捷键：ctrl+alt+B 查看实现的类和接口  
![](https://img-blog.csdnimg.cn/67df3de38cf44ff09d72fbb67ab88364.png)  
![](https://img-blog.csdnimg.cn/acdd35466a3d482c9d8e52b0969715a6.png)  
12.4.2 异常体系图的小结  
![](https://img-blog.csdnimg.cn/7362003089e54fe8be841bbcdd683fbf.png)  
12.5 常见的运行时异常

12.5.1 常见的运行时异常包括  
![](https://img-blog.csdnimg.cn/3338a918ea244f53a28262cb2d060273.png)  
12.5.2 常见的运行时异常举例  
![](https://img-blog.csdnimg.cn/b87b7be0599248a7a29f7dd976645258.png)  
![](https://img-blog.csdnimg.cn/7062ae2c6d244c4da2fc2031b6e94d66.png)  
![](https://img-blog.csdnimg.cn/c9dcdebe6c684570a2f1f510b75628ab.png)  
![](https://img-blog.csdnimg.cn/ce48aca6db34481e81f5404774ccad23.png)  
![](https://img-blog.csdnimg.cn/c9b9da0cfe504f30a111da23e1f9e1c5.png)  
12.6 编译异常

12.6.1 介绍  
![](https://img-blog.csdnimg.cn/3f0bae3d79a24a35a41ba69f3738cee3.png)  
12.6.2 常见的编译异常  
![](https://img-blog.csdnimg.cn/caed0dd7bccb48b8b82579630874fbe3.png)  
12.8 异常处理

12.8.1 基本介绍  
![](https://img-blog.csdnimg.cn/037467c02728454085b6977b3c5e51c6.png)  
12.8.2 异常处理的方式  
![](https://img-blog.csdnimg.cn/a7b9c1177625408699c6c916d82fa576.png)  
12.8.3 示意图  
![](https://img-blog.csdnimg.cn/d752c3bfbe004d1cb642259c087dee2a.png)  
![](https://img-blog.csdnimg.cn/7dfccd9ddabf4ccd802e4576aba7e755.png)  
12.9 try-catch 异常处理

12.9.1 try-catch 方式处理异常说明  
![](https://img-blog.csdnimg.cn/bcc416e779d941319a7536b9b7f7eb02.png)  
12.9.3 try-catch 方式处理异常 - 注意事项  
![](https://img-blog.csdnimg.cn/40ca97b127df4830a6b1799d60375595.png)  
如果想让控制台输出窗口悬浮，点击齿轮按钮 ->View Mode->Float 选中即可  
![](https://img-blog.csdnimg.cn/e3c6ecd4471345f796cf51f2335f23ab.png)  
![](https://img-blog.csdnimg.cn/da67169539954c49ad99f3a86d3d8d7a.png)  
![](https://img-blog.csdnimg.cn/5fdb8fda72d04a5b82aa1a277bfee42c.png)  
![](https://img-blog.csdnimg.cn/1fce818e87f04244b54914d376780919.png)  
注意：是出现了异常，没有捕获，执行完 finally 后程序才会会直接退出 (崩掉)；如果没有异常，则程序继续正常执行。

12.9.4 异常处理课堂练习

1.  题 1 TryCatchExercise01.java  
    ![](https://img-blog.csdnimg.cn/e9fadaa2db5140b9b25d868de91ca5fc.png)
2.  题 2TryCatchExercise02.java  
    ![](https://img-blog.csdnimg.cn/7b5a72c11c894ca08cd58329940507c8.png)
3.  题 3TryCatchExercise03.java  
    ![](https://img-blog.csdnimg.cn/a289f69eeeab42838986fcc0971f1fe0.png)  
    12.9.5 try-catch-finally 执行顺序小结  
    ![](https://img-blog.csdnimg.cn/00959d0ba89243128bb89ffc442df883.png)  
    12.9.6 课后练习题  
    如果用户输入的不是一个整数，就提示他反复输入，直到输入一个整数为止

```
package com.hspedu.try_;
import java.util.Scanner;
public class TryCatchExercise04 {
	public static void main(String[] args) {
		//如果用户输入的不是一个整数，就提示他反复输入，直到输入一个整数为止
		//思路
		//1. 创建 Scanner 对象
		//2. 使用无限循环，去接收一个输入
		//3. 然后将该输入的值，转成一个 int
		//4. 如果在转换时，抛出异常，说明输入的内容不是一个可以转成 int 的内容
		//5. 如果没有抛出异常，则 break 该循环
		Scanner scanner = new Scanner(System.in);
		int num = 0;
		String inputStr = "";
		while (true) {
			System.out.println("请输入一个整数:"); 
			inputStr = scanner.next();
			try {
				num = Integer.parseInt(inputStr); //这里是可能抛出异常
				break;
			} catch (NumberFormatException e) {
				System.out.println("你输入的不是一个整数:");
			}
		}
		System.out.println("你输入的值是=" + num);
	}
}
```

12.10 throws 异常处理

12.10.1 基本介绍  
![](https://img-blog.csdnimg.cn/ef7209d52b1f4bbd9623aa9cf9ee443e.png)  
12.10.2 快速入门案例  
![](https://img-blog.csdnimg.cn/38c6b37a0e884b9482a9540c27a02231.png)  
12.10.3 注意事项和使用细节  
![](https://img-blog.csdnimg.cn/8c6af15af7954cc1a92507b3723fde0e.png)

```
package com.hspedu.throws_;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
public class ThrowsDetail {
	public static void main(String[] args) {
		f2();
	}
	public static void f2() /*throws ArithmeticException*/ {
		//1.对于编译异常，程序中必须处理，比如 try-catch 或者 throws
		//2.对于运行时异常，程序中如果没有处理，默认就是 throws 的方式处理
		int n1 = 10;
		int n2 = 0;
		double res = n1 / n2;
	}
	public static void f1() throws FileNotFoundException {
		//这里大家思考问题 调用 f3() 报错
		//老韩解读
		//1. 因为 f3() 方法抛出的是一个编译异常
		//2. 即这时，就要 f1() 必须处理这个编译异常
		//3. 在 f1() 中，要么 try-catch-finally ,或者继续 throws 这个编译异常
		f3(); // 抛出异常
	}
	public static void f3() throws FileNotFoundException {
		FileInputStream fis = new FileInputStream("d://aa.txt");
	}
	public static void f4() {
		//老韩解读:
		//1. 在 f4()中调用方法 f5() 是 OK
		//2. 原因是 f5() 抛出的是运行异常
		//3. 而 java 中，并不要求程序员显示处理,因为有默认处理机制
		f5();
	}
	public static void f5() throws ArithmeticException { }
}
class Father { //父类
	public void method() throws RuntimeException { }
}
class Son extends Father {//子类
	//3. 子类重写父类的方法时，对抛出异常的规定:子类重写的方法，
	//所抛出的异常类型要么和父类抛出的异常一致，要么为父类抛出的异常类型的子类型
	//4. 在 throws 过程中，如果有方法 try-catch , 就相当于处理异常，就可以不必 throws
	@Override
	public void method() throws ArithmeticException { }
}
```

运行异常可以不用处理，则默认 throws，但编译异常必须显式地处理，不会默认 throws。

12.11 自定义异常

12.11.1 基本概念  
![](https://img-blog.csdnimg.cn/84bf7ba06a344697b24942e4e87fada3.png)  
12.11.2 自定义异常的步骤  
![](https://img-blog.csdnimg.cn/e90fb2463ea1486da218db245956af44.png)  
12.11.3 自定义异常的应用实例 CustomException.java  
![](https://img-blog.csdnimg.cn/dc8a2e06a28b4a4f831628a8f3cb6b43.png)

```
package com.hspedu.customexception_;
public class CustomException {
	public static void main(String[] args) /*throws AgeException*/ {
		int age = 180;
		//要求范围在 18 – 120 之间，否则抛出一个自定义异常
		if(!(age >= 18 && age <= 120)) {
			//这里我们可以通过构造器，设置信息
			throw new AgeException("年龄需要在 18~120 之间");
		}
		System.out.println("你的年龄范围正确.");
	}
}
//自定义一个异常
//老韩解读
//1. 一般情况下，我们自定义异常是继承 RuntimeException
//2. 即把自定义异常做成 运行时异常，好处时，我们可以使用默认的处理机制
//3. 即比较方便
class AgeException extends RuntimeException {
	public AgeException(String message) {//构造器
		super(message);
	}
}
```

12.12 throw 和 throws 的区别

12.12.1 一览表  
![](https://img-blog.csdnimg.cn/f8500e9e751a446d95e1937103630e75.png)  
12.12.2 测试题 - 下面的测试输出什么 ThrowException.java  
![](https://img-blog.csdnimg.cn/f9b4e5fc63db4ef3a17865b67892b261.png)  
12.13 本章作业  
![](https://img-blog.csdnimg.cn/5247f04aa7804dd79aa3613ea2eaae9b.png)  
![](https://img-blog.csdnimg.cn/a3cc020ff7b142709a980f375c2dcc85.png)  
![](https://img-blog.csdnimg.cn/0dea9c9a44a24bf08aefd03ec0860cb4.png)

#### 第 13 章 常用类

13.1 包装类

13.1.1 包装类的分类  
![](https://img-blog.csdnimg.cn/02f0008479c74bb099be0898cd01ad97.png)  
![](https://img-blog.csdnimg.cn/7ed7f1c3ec7f48aabf32df9fb00cbc9d.png)  
![](https://img-blog.csdnimg.cn/eebafc5971944795b15f32cc420a7faa.png)  
![](https://img-blog.csdnimg.cn/18fea3ee5e85448e87c7f1dcae7e5739.png)  
13.1.2 包装类和基本数据的转换  
![](https://img-blog.csdnimg.cn/479abf2d99bd4a1e8f3c9b4de5a23a43.png)  
13.1.3 案例演示

```
package com.hspedu.wrapper;
public class Integer01 {
	public static void main(String[] args) {
		//演示 int <--> Integer 的装箱和拆箱
		//jdk5 前是手动装箱和拆箱
		//手动装箱 int->Integer
		int n1 = 100;
		Integer integer = new Integer(n1);
		Integer integer1 = Integer.valueOf(n1);
		//手动拆箱
		//Integer -> int
		int i = integer.intValue();
		//jdk5 后，就可以自动装箱和自动拆箱
		int n2 = 200;
		//自动装箱 int->Integer
		Integer integer2 = n2; //底层使用的是 Integer.valueOf(n2)
		//自动拆箱 Integer->int
		int n3 = integer2; //底层仍然使用的是 intValue()方法
	}
}
```

13.1.4 课堂测试题  
![](https://img-blog.csdnimg.cn/ae3382ac41a24b6c99886a0db1471a55.png)  
13.1.5 包装类型和 String 类型的相互转换  
![](https://img-blog.csdnimg.cn/d27526a7b93246b5b356277989abe007.png)

```
package com.hspedu.wrapper;
public class WrapperVSString {
	public static void main(String[] args) {
		//包装类(Integer)->String
		Integer i = 100;//自动装箱
		//方式 1
		String str1 = i + "";
		//方式 2
		String str2 = i.toString();
		//方式 3
		String str3 = String.valueOf(i);
		//String -> 包装类(Integer)
		String str4 = "12345";
		Integer i2 = Integer.parseInt(str4);//使用到自动装箱
		Integer i3 = new Integer(str4);//构造器
		System.out.println("ok~~");
	}
}
```

13.1.6 Integer 类和 Character 类的常用方法  
![](https://img-blog.csdnimg.cn/6c7dcbb71da14724b929fae85036ff6c.png)  
13.1.7 Integer 类面试题  
![](https://img-blog.csdnimg.cn/d772071a04724dcaaeb06a39a4eb1db6.png)  
![](https://img-blog.csdnimg.cn/169d737d875247c1998a4bf2ae9180df.png)  
![](https://img-blog.csdnimg.cn/34e7a203f3d445efb503ca269dcaaf3f.png)  
![](https://img-blog.csdnimg.cn/542c8126bf6b4740accf1b7046eab417.png)  
13.1.8 Integer 类面试题总结  
![](https://img-blog.csdnimg.cn/87f944631c6c4cccbd1df8267a270ef5.png)  
解读示例六和七：只要有基本数据类型，== 判断的就是值是否相等

13.2 String 类

13.2.1 String 类的理解和创建对象  
![](https://img-blog.csdnimg.cn/d6cf878be32b424cbed5338386cc2d46.png)  
![](https://img-blog.csdnimg.cn/4d470bcb84c548f7b5f50730d7a40640.png)

```
package com.hspedu.string_;
public class String01 {
	public static void main(String[] args) {
		//1.String 对象用于保存字符串，也就是一组字符序列
		//2. "jack" 字符串常量, 双引号括起的字符序列
		//3. 字符串的字符使用 Unicode 字符编码，一个字符(不区分字母还是汉字)占两个字节
		//4. String 类有很多构造器，构造器的重载
		//常用的有 String s1 = new String();
		//String s2 = new String(String original);
		//String s3 = new String(char[] a);
		//String s4 = new String(char[] a,int startIndex,int count)
		//String s5 = new String(byte[] b)
		//5. String 类实现了接口 Serializable【String 可以串行化:可以在网络传输】
		//					接口 Comparable [String 对象可以比较大小]
		//6. String 是 final 类，不能被其他的类继承
		//7. String 有属性 private final char value[]; 用于存放字符串内容
		//8. 一定要注意：value 是一个 final 类型， 不可以修改(需要功力)：即 value 不能指向
		// 新的地址，但是单个字符内容是可以变化
		String name = "jack";
		name = "tom";
		final char[] value = {'a','b','c'};
		char[] v2 = {'t','o','m'};
		value[0] = 'H';
		//value = v2; 不可以修改 value 地址
	}
}
```

13.2.2 创建 String 对象的两种方式  
![](https://img-blog.csdnimg.cn/d1734c61721044b699745ba1349c74eb.png)  
13.2.3 两种创建 String 对象的区别  
![](https://img-blog.csdnimg.cn/a6d806d2401240b0a43b587fb31fbeb5.png)  
![](https://img-blog.csdnimg.cn/8a83045e7c1242fc9318e7321b7b4f9c.png)  
13.2.4 课堂测试题  
![](https://img-blog.csdnimg.cn/b06e5f9b654d4d6da4a006bcabcafe8d.png)  
13.3 字符串的特性

13.3.1 说明  
![](https://img-blog.csdnimg.cn/5e1779fd19364fcdb039cf9dc15bab9c.png)  
13.3.2 面试题  
![](https://img-blog.csdnimg.cn/0c85ba1789bf4888bdc1bbcc3e2d384c.png)  
![](https://img-blog.csdnimg.cn/47a1126311034e56a674c84a2369cb62.png)

```
package com.hspedu.string_;
public class StringExercise08 {
    public static void main(String[] args) {
        String a = "hello"; //创建 a对象
        String b = "abc";//创建 b对象
        //老韩解读
        //1. 先 创建一个 StringBuilder sb = StringBuilder()
        //2. 执行  sb.append("hello");
        //3. sb.append("abc");
        //4. String c= sb.toString()
        //最后其实是 c 指向堆中的对象(String) value[] -> 池中 "helloabc"
        String c = a + b;
        String d = "helloabc";
        System.out.println(c == d);//真还是假? 是false
        String e = "hello" + "abc";//直接看池， e指向常量池
        System.out.println(d == e);//真还是假? 是true
    }
}
```

![](https://img-blog.csdnimg.cn/1d91d77d0baf454b8e08e525bdf0fe7b.png)  
![](https://img-blog.csdnimg.cn/05ca24669e01495fb978f0c2f012f66d.png)  
13.4 String 类的常见方法

13.4.1 说明  
![](https://img-blog.csdnimg.cn/f0eb7b0c09a340a1bf9206df79788ff4.png)  
13.4.2 String 类的常见方法一览  
![](https://img-blog.csdnimg.cn/48ff54ca144b4e7d8ca843d51e50867e.png)

```
package com.hspedu.string_;
public class StringMethod01 {
    public static void main(String[] args) {
        //1. equals 前面已经讲过了. 比较内容是否相同，区分大小写
        String str1 = "hello";
        String str2 = "Hello";
        System.out.println(str1.equals(str2));//
        // 2.equalsIgnoreCase 忽略大小写的判断内容是否相等
        String username = "johN";
        if ("john".equalsIgnoreCase(username)) {
            System.out.println("Success!");
        } else {
            System.out.println("Failure!");
        }
        // 3.length 获取字符的个数，字符串的长度
        System.out.println("韩顺平".length());
        // 4.indexOf 获取字符在字符串对象中第一次出现的索引，索引从0开始，如果找不到，返回-1
        String s1 = "wer@terwe@g";
        int index = s1.indexOf('@');
        System.out.println(index);// 3
        System.out.println("weIndex=" + s1.indexOf("we"));//0
        // 5.lastIndexOf 获取字符在字符串中最后一次出现的索引，索引从0开始，如果找不到，返回-1
        s1 = "wer@terwe@g@";
        index = s1.lastIndexOf('@');
        System.out.println(index);//11
        System.out.println("ter的位置=" + s1.lastIndexOf("ter"));//4
        // 6.substring 截取指定范围的子串
        String name = "hello,张三";
        //下面name.substring(6) 从索引6开始截取后面所有的内容
        System.out.println(name.substring(6));//截取后面的字符
        //name.substring(0,5)表示从索引0开始截取，截取到索引 5-1=4位置，也就是[0,5)
        System.out.println(name.substring(2,5));//llo

    }
}
```

![](https://img-blog.csdnimg.cn/7fa98bc2328948b4bbb085f5d1ce4b8c.png)

```
package com.hspedu.string_;
public class StringMethod02 {
    public static void main(String[] args) {
        // 1.toUpperCase转换成大写
        String s = "heLLo";
        System.out.println(s.toUpperCase());//HELLO
        // 2.toLowerCase
        System.out.println(s.toLowerCase());//hello
        // 3.concat拼接字符串
        String s1 = "宝玉";
        s1 = s1.concat("林黛玉").concat("薛宝钗").concat("together");
        System.out.println(s1);//宝玉林黛玉薛宝钗together
        // 4.replace 替换字符串中的字符
        s1 = "宝玉 and 林黛玉 林黛玉 林黛玉";
        //在s1中，将 所有的 林黛玉 替换成薛宝钗
        // 老韩解读: s1.replace() 方法执行后，返回的结果才是替换过的.
        // 注意对 s1没有任何影响
        String s11 = s1.replace("宝玉", "jack");
        System.out.println(s1);//宝玉 and 林黛玉 林黛玉 林黛玉
        System.out.println(s11);//jack and 林黛玉 林黛玉 林黛玉
        // 5.split 分割字符串, 对于某些分割字符，我们需要 转义比如 | \\等
        String poem = "锄禾日当午,汗滴禾下土,谁知盘中餐,粒粒皆辛苦";
        //老韩解读：
        // 1. 以 , 为标准对 poem 进行分割 , 返回一个数组
        // 2. 在对字符串进行分割时，如果有特殊字符，需要加入 转义符 \
        String[] split = poem.split(",");
        poem = "E:\\aaa\\bbb";
        split = poem.split("\\\\");
        System.out.println("==分割后内容===");
        for (int i = 0; i < split.length; i++) {
            System.out.println(split[i]);
        }
        // 6.toCharArray 转换成字符数组
        s = "happy";
        char[] chs = s.toCharArray();
        for (int i = 0; i < chs.length; i++) {
            System.out.println(chs[i]);
        }
        // 7.compareTo 比较两个字符串的大小，如果前者大，
        // 则返回正数，后者大，则返回负数，如果相等，返回0
        // 老韩解读
        // (1) 如果长度相同，并且每个字符也相同，就返回 0
        // (2) 如果比较到两个字符不相等
        //     就返回 if (c1 != c2) {
        //                return c1 - c2;
        //            }
        // (3) 如果前面的部分都相同，就返回 str1.len - str2.len
        String a = "jcck";// len = 3
        String b = "jack";// len = 4
        System.out.println(a.compareTo(b)); // 返回值是 'c' - 'a' = 2的值
		// 8.format 格式字符串
        /* 占位符有:
         * %s 字符串 %c 字符 %d 整型 %.2f 浮点型
         */
        String name = "john";
        int age = 10;
        double score = 56.857;
        char gender = '男';
        //将所有的信息都拼接在一个字符串.
        String info =
                "我的姓名是" + name + "年龄是" + age + ",成绩是" + score + "性别是" + gender + "。希望大家喜欢我！";
        System.out.println(info);
        //老韩解读
        //1. %s , %d , %.2f %c 称为占位符
        //2. 这些占位符由后面变量来替换
        //3. %s 表示后面由 字符串来替换
        //4. %d 是整数来替换
        //5. %.2f 表示使用小数来替换，替换后，只会保留小数点两位, 并且进行四舍五入的处理
        //6. %c 使用char 类型来替换
        String formatStr = "我的姓名是%s 年龄是%d，成绩是%.2f 性别是%c.希望大家喜欢我！";
        String info2 = String.format(formatStr, name, age, score, gender);
        System.out.println("info2=" + info2);
    }
}
```

13.5 StringBuffer 类

13.5.1 基本介绍  
![](https://img-blog.csdnimg.cn/ae6a8a1360804a4da615056c01c438a0.png)  
![](https://img-blog.csdnimg.cn/80974c9e14884722b370d6e89d9110b7.png)  
13.5.2 String VS StringBuffer  
![](https://img-blog.csdnimg.cn/49e0c37cd33b452081f94e2003b02bba.png)  
13.5.3 StringBuffer 的构造器  
![](https://img-blog.csdnimg.cn/cf2866b8cf07466980d8d741dbcd2bcb.png)

```
package com.hspedu.stringbuffer_;
public class StringBuffer02 {
    public static void main(String[] args) {
        //构造器的使用
        //老韩解读
        //1. 创建一个 大小为 16的 char[] ,用于存放字符内容
        StringBuffer stringBuffer = new StringBuffer();
        //2 通过构造器指定 char[] 大小
        StringBuffer stringBuffer1 = new StringBuffer(100);
        //3. 通过 给一个String 创建 StringBuffer, char[] 大小就是 str.length() + 16
        StringBuffer hello = new StringBuffer("hello");
    }
}
```

13.5.4 String 和 StringBuffer 相互转换  
![](https://img-blog.csdnimg.cn/ee7f8e024d1f407c9bc43d228b5f2faf.png)

```
package com.hspedu.stringbuffer_;
public class StringAndStringBuffer {
    public static void main(String[] args) {
        //看 String——>StringBuffer
        String str = "hello tom";
        //方式1 使用构造器
        //注意： 返回的才是StringBuffer对象，对str 本身没有影响
        StringBuffer stringBuffer = new StringBuffer(str);
        //方式2 使用的是append方法
        StringBuffer stringBuffer1 = new StringBuffer();
        stringBuffer1 = stringBuffer1.append(str);

        //看看 StringBuffer ->String
        StringBuffer stringBuffer3 = new StringBuffer("韩顺平教育");
        //方式1 使用StringBuffer提供的 toString方法
        String s = stringBuffer3.toString();
        //方式2: 使用构造器来搞定
        String s1 = new String(stringBuffer3);
    }
}
```

13.5.5 StringBuffer 类常见方法  
![](https://img-blog.csdnimg.cn/8dd5ecf845244c3ba56e54c4e3c4496c.png)

```
package com.hspedu.stringbuffer_;
public class StringBufferMethod {
    public static void main(String[] args) {
        StringBuffer s = new StringBuffer("hello");
        //增
        s.append(',');// "hello,"
        s.append("张三丰");//"hello,张三丰"
        s.append("赵敏").append(100).append(true).append(10.5);//"hello,张三丰赵敏100true10.5"
        System.out.println(s);//"hello,张三丰赵敏100true10.5"
        //删
        /*
         * 删除索引为>=start && <end 处的字符
         * 解读: 删除 11~14的字符 [11, 14)
         */
        s.delete(11, 14);
        System.out.println(s);//"hello,张三丰赵敏true10.5"
        //改
        //老韩解读，使用 周芷若 替换 索引9-11的字符 [9,11)
        s.replace(9, 11, "周芷若");
        System.out.println(s);//"hello,张三丰周芷若true10.5"
        //查找指定的子串在字符串第一次出现的索引，如果找不到返回-1
        int indexOf = s.indexOf("张三丰");
        System.out.println(indexOf);//6
        //插
        //老韩解读，在索引为9的位置插入 "赵敏",原来索引为9的内容自动后移
        s.insert(9, "赵敏");
        System.out.println(s);//"hello,张三丰赵敏周芷若true10.5"
        //长度
        System.out.println(s.length());//22
        System.out.println(s);
    }
}
```

13.5.5 StringBuffer 类课堂测试题 1  
![](https://img-blog.csdnimg.cn/1faa9edc3463490c8dd4ac3b8645450e.png)  
![](https://img-blog.csdnimg.cn/4ee14527f6c84a4891cb9b744ae87883.png)  
13.5.6 StringBuffer 类课后练习 2  
![](https://img-blog.csdnimg.cn/f3af36235c36407aac0c32967679e94b.png)

```
package com.hspedu.stringbuffer_;
import java.util.Scanner;
public class StringBufferExercise02 {
    public static void main(String[] args) {
        /*
        思路分析
        1. 定义一个Scanner 对象，接收用户输入的 价格(String)
        2. 希望使用到 StringBuffer的 insert ，需要将 String 转成 StringBuffer
        3. 然后使用相关方法进行字符串的处理
        代码实现
         */
        //new Scanner(System.in)
        String price = "8123564.59";
        StringBuffer sb = new StringBuffer(price);
        //先完成一个最简单的实现123,564.59
        //找到小数点的索引，然后在该位置的前3位，插入,即可
//        int i = sb.lastIndexOf(".");
//        sb = sb.insert(i - 3, ",");
        //上面的两步需要做一个循环处理,才是正确的
        for (int i = sb.lastIndexOf(".") - 3; i > 0; i -= 3) {
            sb = sb.insert(i, ",");
        }
        System.out.println(sb);//8,123,564.59
    }
}
```

13.6 StringBuilder 类

13.6.1 基本介绍  
![](https://img-blog.csdnimg.cn/f517ef4d6644486db3aa605545704893.png)  
![](https://img-blog.csdnimg.cn/714feed5606049e48a5d609765a9162d.png)  
13.6.2 StringBuilder 常用方法  
![](https://img-blog.csdnimg.cn/f36a093348ee4ceeb9f746e591277719.png)  
13.6.3 String、StringBuffer 和 StringBuilder 的比较  
![](https://img-blog.csdnimg.cn/a1a9d60db19142e9adfd8a603eef1da0.png)  
13.6.4 String、StringBuffer 和 StringBuilder 的效率测试  
效率 ： StringBuilder > StringBuffer > String

13.6.5 String、StringBuffer 和 StringBuilder 的选择  
![](https://img-blog.csdnimg.cn/81fcc15a39a14f8282363694552ce099.png)  
13.7 Math 类

13.7.1 基本介绍  
Math 类包含用于执行基本数学运算的方法，如初等指数、对数、平方根和三角函数。

13.7.2 方法一览 (均为静态方法)  
![](https://img-blog.csdnimg.cn/8837e2abd7ad4e61ab7786b17dad4671.png)  
13.7.3 Math 类常见方法应用案例  
![](https://img-blog.csdnimg.cn/380aa31af6ac4c5eac3ab0bcb26aac3f.png)

```
package com.hspedu.math_;
public class MathMethod {
    public static void main(String[] args) {
        //看看Math常用的方法(静态方法)
        //1.abs 绝对值
        int abs = Math.abs(-9);
        System.out.println(abs);//9
        //2.pow 求幂
        double pow = Math.pow(2, 4);//2的4次方
        System.out.println(pow);//16
        //3.ceil 向上取整,返回>=该参数的最小整数(转成double);
        double ceil = Math.ceil(3.9);
        System.out.println(ceil);//4.0
        //4.floor 向下取整，返回<=该参数的最大整数(转成double)
        double floor = Math.floor(4.001);
        System.out.println(floor);//4.0
        //5.round 四舍五入  Math.floor(该参数+0.5)
        long round = Math.round(5.51);
        System.out.println(round);//6
        //6.sqrt 求开方
        double sqrt = Math.sqrt(9.0);
        System.out.println(sqrt);//3.0
        //7.random 求随机数
        //  random 返回的是 0 <= x < 1 之间的一个随机小数
        // 思考：请写出获取 a-b之间的一个随机整数,a,b均为整数 ，比如 a = 2, b=7
        //  即返回一个数 x  2 <= x <= 7
        // 老韩解读 Math.random() * (b-a) 返回的就是 0  <= 数 <= b-a
        // (1) (int)(a) <= x <= (int)(a + Math.random() * (b-a +1) )
        // (2) 使用具体的数给小伙伴介绍 a = 2  b = 7
        //  (int)(a + Math.random() * (b-a +1) ) = (int)( 2 + Math.random()*6)
        //  Math.random()*6 返回的是 0 <= x < 6 小数
        //  2 + Math.random()*6 返回的就是 2<= x < 8 小数
        //  (int)(2 + Math.random()*6) = 2 <= x <= 7
        // (3) 公式就是  (int)(a + Math.random() * (b-a +1) )
        for(int i = 0; i < 100; i++) {
            System.out.println((int)(2 +  Math.random() * (7 - 2 + 1)));
        }
        //max , min 返回最大值和最小值
        int min = Math.min(1, 9);
        int max = Math.max(45, 90);
        System.out.println("min=" + min);
        System.out.println("max=" + max);
    }
}
```

13.8 Arrays 类

13.8.1 Arrays 类常见方法应用案例  
![](https://img-blog.csdnimg.cn/277a6c9a75ab478c95f879ed9c8dacaa.png)  
![](https://img-blog.csdnimg.cn/1c50f931acea403e997fb900cd5b677a.png)

```
package com.hspedu.arrays_;
import java.util.Arrays;
import java.util.Comparator;
public class ArraysMethod01 {
    public static void main(String[] args) {
        Integer[] integers = {1, 20, 90};
        //遍历数组
//        for(int i = 0; i < integers.length; i++) {
//            System.out.println(integers[i]);
//        }
        //直接使用Arrays.toString方法，显示数组
//        System.out.println(Arrays.toString(integers));

        //演示 sort方法的使用
        Integer arr[] = {1, -1, 7, 0, 89};
        //进行排序
        //老韩解读
        //1. 可以直接使用冒泡排序 , 也可以直接使用Arrays提供的sort方法排序
        //2. 因为数组是引用类型，所以通过sort排序后，会直接影响到 实参 arr
        //3. sort重载的，也可以通过传入一个接口 Comparator 实现定制排序
        //4. 调用 定制排序 时，传入两个参数 (1) 排序的数组 arr
        //   (2) 实现了Comparator接口的匿名内部类 , 要求实现  compare方法
        //5. 先演示效果，再解释
        //6. 这里体现了接口编程的方式 , 看看源码，就明白
        //   源码分析
        //(1) Arrays.sort(arr, new Comparator()
        //(2) 最终到 TimSort类的 private static <T> void binarySort(T[] a, int lo, int hi, int start,
        //                                       Comparator<? super T> c)()
        //(3) 执行到 binarySort方法的代码, 会根据动态绑定机制 c.compare()执行我们传入的
        //    匿名内部类的 compare ()
        //     while (left < right) {
        //                int mid = (left + right) >>> 1;
        //                if (c.compare(pivot, a[mid]) < 0)
        //                    right = mid;
        //                else
        //                    left = mid + 1;
        //            }
        //(4) new Comparator() {
        //            @Override
        //            public int compare(Object o1, Object o2) {
        //                Integer i1 = (Integer) o1;
        //                Integer i2 = (Integer) o2;
        //                return i2 - i1;
        //            }
        //        }
        //(5) public int compare(Object o1, Object o2) 返回的值>0 还是 <0
        //    会影响整个排序结果, 这就充分体现了 接口编程+动态绑定+匿名内部类的综合使用
        //    将来的底层框架和源码的使用方式，会非常常见
        //Arrays.sort(arr); // 默认排序方法
        //定制排序
        Arrays.sort(arr, new Comparator() {
            @Override
            public int compare(Object o1, Object o2) {
                Integer i1 = (Integer) o1;
                Integer i2 = (Integer) o2;
                return i2 - i1;
            }
        });
        System.out.println("===排序后===");
        System.out.println(Arrays.toString(arr));//
    }
}
```

ArraysSortCustom.java

```
package com.hspedu.arrays_;
import java.util.Arrays;
import java.util.Comparator;
public class ArraysSortCustom {
    public static void main(String[] args) {
        int[] arr = {1, -1, 8, 0, 20};
        //bubble01(arr);
        bubble02(arr, new Comparator() {
            @Override
            public int compare(Object o1, Object o2) {
                int i1 = (Integer) o1;
                int i2 = (Integer) o2;
                return i2 - i1;// return i2 - i1;
            }
        });
        System.out.println("==定制排序后的情况==");
        System.out.println(Arrays.toString(arr));
    }
    //使用冒泡完成排序
    public static void bubble01(int[] arr) {
        int temp = 0;
        for (int i = 0; i < arr.length - 1; i++) {
            for (int j = 0; j < arr.length - 1 - i; j++) {
                //从小到大
                if (arr[j] > arr[j + 1]) {
                    temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }
    }
    //结合冒泡 + 定制
    public static void bubble02(int[] arr, Comparator c) {
        int temp = 0;
        for (int i = 0; i < arr.length - 1; i++) {
            for (int j = 0; j < arr.length - 1 - i; j++) {
                //数组排序由 c.compare(arr[j], arr[j + 1])返回的值决定
                if (c.compare(arr[j], arr[j + 1]) > 0) {
                    temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }
    }
}
```

ArraysMethod02.java

```
package com.hspedu.arrays_;
import java.util.Arrays;
import java.util.List;
public class ArraysMethod02 {
    public static void main(String[] args) {
        Integer[] arr = {1, 2, 90, 123, 567};
        // binarySearch 通过二分搜索法进行查找，要求必须排好
        // 老韩解读
        //1. 使用 binarySearch 二叉查找
        //2. 要求该数组是有序的. 如果该数组是无序的，不能使用binarySearch
        //3. 如果数组中不存在该元素，就返回 return -(low + 1);  // key not found.
        int index = Arrays.binarySearch(arr, 567);
        System.out.println("index=" + index);

        //copyOf 数组元素的复制
        // 老韩解读
        //1. 从 arr 数组中，拷贝 arr.length个元素到 newArr数组中
        //2. 如果拷贝的长度 > arr.length 就在新数组的后面 增加 null
        //3. 如果拷贝长度 < 0 就抛出异常NegativeArraySizeException
        //4. 该方法的底层使用的是 System.arraycopy()
        Integer[] newArr = Arrays.copyOf(arr, arr.length);
        System.out.println("==拷贝执行完毕后==");
        System.out.println(Arrays.toString(newArr));

        //fill 数组元素的填充
        Integer[] num = new Integer[]{9,3,2};
        //老韩解读
        //1. 使用 99 去填充 num数组，可以理解成是替换原理的元素
        Arrays.fill(num, 99);
        System.out.println("==num数组填充后==");
        System.out.println(Arrays.toString(num));

        //equals 比较两个数组元素内容是否完全一致
        Integer[] arr2 = {1, 2, 90, 123};
        //老韩解读
        //1. 如果arr 和 arr2 数组的元素一样，则方法true;
        //2. 如果不是完全一样，就返回 false
        boolean equals = Arrays.equals(arr, arr2);
        System.out.println("equals=" + equals);

        //asList 将一组值，转换成list
        //老韩解读
        //1. asList方法，会将 (2,3,4,5,6,1)数据转成一个List集合
        //2. 返回的 asList 编译类型 List(接口)
        //3. asList 运行类型 java.util.Arrays#ArrayList, 是Arrays类的
        //   静态内部类 private static class ArrayList<E> extends AbstractList<E>
        //              implements RandomAccess, java.io.Serializable
        List asList = Arrays.asList(2,3,4,5,6,1);
        System.out.println("asList=" + asList);
        System.out.println("asList的运行类型" + asList.getClass());
    }
}
```

13.8.2 Arrays 类课堂练习  
![](https://img-blog.csdnimg.cn/d407cb9a0d1c43b5b9d6e643c65ecd82.png)

```
package com.hspedu.arrays_;
import java.util.Arrays;
import java.util.Comparator;
public class ArrayExercise {
    public static void main(String[] args) {
        Book[] books = new Book[4];
        books[0] = new Book("红楼梦", 100);
        books[1] = new Book("金瓶梅新", 90);
        books[2] = new Book("青年文摘20年", 5);
        books[3] = new Book("java从入门到放弃~", 300);
        //(1)price从大到小
//        Arrays.sort(books, new Comparator() {
//            //这里是对Book数组排序，因此  o1 和 o2 就是Book对象
//            @Override
//            public int compare(Object o1, Object o2) {
//                Book book1 = (Book) o1;
//                Book book2 = (Book) o2;
//                double priceVal = book2.getPrice() - book1.getPrice();
//                //这里老师进行了一个转换
//                //如果发现返回结果和我们输出的不一致，就修改一下返回的 1 和 -1
//                if(priceVal > 0) {
//                    return  1;
//                } else  if(priceVal < 0) {
//                    return -1;
//                } else {
//                    return 0;
//                }
//            }
//        });

        //(2)price从小到大
//        Arrays.sort(books, new Comparator() {
//            //这里是对Book数组排序，因此  o1 和 o2 就是Book对象
//            @Override
//            public int compare(Object o1, Object o2) {
//                Book book1 = (Book) o1;
//                Book book2 = (Book) o2;
//                double priceVal = book2.getPrice() - book1.getPrice();
//                //这里老师进行了一个转换
//                //如果发现返回结果和我们输出的不一致，就修改一下返回的 1 和 -1
//                if(priceVal > 0) {
//                    return  -1;
//                } else  if(priceVal < 0) {
//                    return 1;
//                } else {
//                    return 0;
//                }
//            }
//        });

        //(3)按照书名长度从大到小
        Arrays.sort(books, new Comparator() {
            //这里是对Book数组排序，因此  o1 和 o2 就是Book对象
            @Override
            public int compare(Object o1, Object o2) {
                Book book1 = (Book) o1;
                Book book2 = (Book) o2;
                //要求按照书名的长度来进行排序
                return book2.getName().length() - book1.getName().length();
            }
        });
        System.out.println(Arrays.toString(books));
    }
}
class Book {
    private String name;
    private double price;
    public Book(String name, double price) {
        this.name = name;
        this.price = price;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public double getPrice() {
        return price;
    }
    public void setPrice(double price) {
        this.price = price;
    }
    @Override
    public String toString() {
        return "Book{" +
                " + name + '\'' +
                ", price=" + price +
                '}';
    }
}
```

13.9 System 类

13.9.1 System 类常见方法和案例  
![](https://img-blog.csdnimg.cn/78e8ab1d63c94683a4c8ac00ffcc2bca.png)

```
package com.hspedu.system_;
import java.util.Arrays;
public class System_ {
    public static void main(String[] args) {
        //exit 退出当前程序
//        System.out.println("ok1");
//        //老韩解读
//        //1. exit(0) 表示程序退出
//        //2. 0 表示一个状态 , 正常的状态
//        System.exit(0);//
//        System.out.println("ok2");

        //arraycopy ：复制数组元素，比较适合底层调用，
        // 一般使用Arrays.copyOf完成复制数组
        int[] src={1,2,3};
        int[] dest = new int[3];// dest 当前是 {0,0,0}
        //老韩解读
        //1. 主要是搞清楚这五个参数的含义
        //2.
        //     源数组
        //     * @param      src      the source array.
        //     srcPos： 从源数组的哪个索引位置开始拷贝
        //     * @param      srcPos   starting position in the source array.
        //     dest : 目标数组，即把源数组的数据拷贝到哪个数组
        //     * @param      dest     the destination array.
        //     destPos: 把源数组的数据拷贝到 目标数组的哪个索引
        //     * @param      destPos  starting position in the destination data.
        //     length: 从源数组拷贝多少个数据到目标数组
        //     * @param      length   the number of array elements to be copied.
        System.arraycopy(src, 0, dest, 0, src.length);
        // int[] src={1,2,3};
        System.out.println("dest=" + Arrays.toString(dest));//[1, 2, 3]

        //currentTimeMillens:返回当前时间距离1970-1-1 的毫秒数
        // 老韩解读:
        System.out.println(System.currentTimeMillis());
    }
}
```

13.10 BigInteger 和 BigDecimal 类

13.10.1 BigInteger 和 BigDecimal 介绍  
![](https://img-blog.csdnimg.cn/80229b84156645c5a61f7535c2a5e858.png)  
13.10.2 BigInteger 和 BigDecimal 常见方法  
![](https://img-blog.csdnimg.cn/b9db818642644bd5a9b9aa9df5f85990.png)  
BigDecimal_.java

```
package com.hspedu.bignum;
import java.math.BigDecimal;
public class BigDecimal_ {
    public static void main(String[] args) {
        //当我们需要保存一个精度很高的数时，double 不够用
        //可以是 BigDecimal
//        double d = 1999.11111111111999999999999977788d;
//        System.out.println(d);
        BigDecimal bigDecimal = new BigDecimal("1999.11");
        BigDecimal bigDecimal2 = new BigDecimal("3");
        System.out.println(bigDecimal);
        //老韩解读
        //1. 如果对 BigDecimal进行运算，比如加减乘除，需要使用对应的方法
        //2. 创建一个需要操作的 BigDecimal 然后调用相应的方法即可
        System.out.println(bigDecimal.add(bigDecimal2));
        System.out.println(bigDecimal.subtract(bigDecimal2));
        System.out.println(bigDecimal.multiply(bigDecimal2));
        //System.out.println(bigDecimal.divide(bigDecimal2));//可能抛出异常ArithmeticException
        //在调用divide 方法时，指定精度即可. BigDecimal.ROUND_CEILING
        //如果有无限循环小数，就会保留 分子 的精度
        System.out.println(bigDecimal.divide(bigDecimal2, BigDecimal.ROUND_CEILING));
    }
}
```

BigInteger_.java

```
package com.hspedu.bignum;
import java.math.BigInteger;
public class BigInteger_ {
    public static void main(String[] args) {
        //当我们编程中，需要处理很大的整数，long 不够用
        //可以使用BigInteger的类来搞定
//        long l = 23788888899999999999999999999l;
//        System.out.println("l=" + l);
        BigInteger bigInteger = new BigInteger("23788888899999999999999999999");
        BigInteger bigInteger2 = new BigInteger("10099999999999999999999999999999999999999999999999999999999999999999999999999999999");
        System.out.println(bigInteger);
        //老韩解读
        //1. 在对 BigInteger 进行加减乘除的时候，需要使用对应的方法，不能直接进行 + - * /
        //2. 可以创建一个 要操作的 BigInteger 然后进行相应操作
        BigInteger add = bigInteger.add(bigInteger2);
        System.out.println(add);//
        BigInteger subtract = bigInteger.subtract(bigInteger2);
        System.out.println(subtract);//减
        BigInteger multiply = bigInteger.multiply(bigInteger2);
        System.out.println(multiply);//乘
        BigInteger divide = bigInteger.divide(bigInteger2);
        System.out.println(divide);//除
    }
}
```

13.11 日期类

13.11.1 第一代日期类  
![](https://img-blog.csdnimg.cn/0e08fa504c7f40a8aa907edfe43256ae.png)

```
package com.hspedu.date_;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;
public class Date01 {
    public static void main(String[] args) throws ParseException {
        //老韩解读
        //1. 获取当前系统时间
        //2. 这里的Date 类是在java.util包
        //3. 默认输出的日期格式是国外的方式, 因此通常需要对格式进行转换
        Date d1 = new Date(); //获取当前系统时间
        System.out.println("当前日期=" + d1);
        Date d2 = new Date(9234567); //通过指定毫秒数得到时间
        System.out.println("d2=" + d2); //获取某个时间对应的毫秒数

        //老韩解读
        //1. 创建 SimpleDateFormat对象，可以指定相应的格式
        //2. 这里的格式使用的字母是规定好，不能乱写
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日 hh:mm:ss E");
        String format = sdf.format(d1); // format:将日期转换成指定格式的字符串
        System.out.println("当前日期=" + format);

        //老韩解读
        //1. 可以把一个格式化的String 转成对应的 Date
        //2. 得到Date 仍然在输出时，还是按照国外的形式，如果希望指定格式输出，需要转换
        //3. 在把String -> Date ， 使用的 sdf 格式需要和你给的String的格式一样，否则会抛出转换异常
        String s = "1996年01月01日 10:20:30 星期一";
        Date parse = sdf.parse(s);
        System.out.println("parse=" + sdf.format(parse));
    }
}
```

13.11.2 第二代日期类  
![](https://img-blog.csdnimg.cn/0b44e6baf46b4c38bb4455c65305fdb7.png)  
![](https://img-blog.csdnimg.cn/8625f5a6418d4aaca3702eef6059968f.png)

```
package com.hspedu.date_;
import java.util.Calendar;
public class Calendar_ {
    public static void main(String[] args) {
        //老韩解读
        //1. Calendar是一个抽象类， 并且构造器是private
        //2. 可以通过 getInstance() 来获取实例
        //3. 提供大量的方法和字段提供给程序员
        //4. Calendar没有提供对应的格式化的类，因此需要程序员自己组合来输出(灵活)
        //5. 如果我们需要按照 24小时进制来获取时间， Calendar.HOUR ==改成=> Calendar.HOUR_OF_DAY
        Calendar c = Calendar.getInstance(); //创建日历类对象//比较简单，自由
        System.out.println("c=" + c);
        //2.获取日历对象的某个日历字段
        System.out.println("年：" + c.get(Calendar.YEAR));
        // 这里为什么要 + 1, 因为Calendar 返回月时候，是按照 0 开始编号
        System.out.println("月：" + (c.get(Calendar.MONTH) + 1));
        System.out.println("日：" + c.get(Calendar.DAY_OF_MONTH));
        System.out.println("小时：" + c.get(Calendar.HOUR));
        System.out.println("分钟：" + c.get(Calendar.MINUTE));
        System.out.println("秒：" + c.get(Calendar.SECOND));
        //Calender 没有专门的格式化方法，所以需要程序员自己来组合显示
        System.out.println(c.get(Calendar.YEAR) + "-" + (c.get(Calendar.MONTH) + 1) + "-" + c.get(Calendar.DAY_OF_MONTH) +
                " " + c.get(Calendar.HOUR_OF_DAY) + ":" + c.get(Calendar.MINUTE) + ":" + c.get(Calendar.SECOND) );
    }
}
```

13.11.3 第三代日期类  
![](https://img-blog.csdnimg.cn/ff36463c50f94200a80d1e7e4b436950.png)  
![](https://img-blog.csdnimg.cn/42f453c7cba240f5983f32936e5baf5d.png)  
![](https://img-blog.csdnimg.cn/2868c577bd1f42ee9329e048308b9204.png)  
![](https://img-blog.csdnimg.cn/9184ec46cceb41188fed980c46c5009c.png)  
![](https://img-blog.csdnimg.cn/b645555019964c1f886d278d8d2f4056.png)

```
package com.hspedu.date_;
import java.time.Instant;
import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.LocalTime;
import java.time.format.DateTimeFormatter;
import java.util.ArrayList;
import java.util.Collection;
public class LocalDate_ {
    public static void main(String[] args) {
        //第三代日期
        //老韩解读
        //1. 使用now() 返回表示当前日期时间的 对象
        LocalDateTime ldt = LocalDateTime.now(); //LocalDate.now();//LocalTime.now()
        System.out.println(ldt);
        
        //2. 使用DateTimeFormatter 对象来进行格式化
        // 创建 DateTimeFormatter对象
        DateTimeFormatter dateTimeFormatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
        String format = dateTimeFormatter.format(ldt);
        System.out.println("格式化的日期=" + format);
        System.out.println("年=" + ldt.getYear());
        System.out.println("月=" + ldt.getMonth());
        System.out.println("月=" + ldt.getMonthValue());
        System.out.println("日=" + ldt.getDayOfMonth());
        System.out.println("时=" + ldt.getHour());
        System.out.println("分=" + ldt.getMinute());
        System.out.println("秒=" + ldt.getSecond());

        LocalDate now = LocalDate.now(); //可以获取年月日
        LocalTime now2 = LocalTime.now();//获取到时分秒

        //提供 plus 和 minus方法可以对当前时间进行加或者减
        //看看890天后，是什么时候 把 年月日-时分秒
        LocalDateTime localDateTime = ldt.plusDays(890);
        System.out.println("890天后=" + dateTimeFormatter.format(localDateTime));

        //看看在 3456分钟前是什么时候，把 年月日-时分秒输出
        LocalDateTime localDateTime2 = ldt.minusMinutes(3456);
        System.out.println("3456分钟前 日期=" + dateTimeFormatter.format(localDateTime2));
    }
}
```

13.12 本章作业  
![](https://img-blog.csdnimg.cn/90d3268a446744c8a6a977cb648af92d.png)

```
package com.hspedu.homework;
public class Homework01 {
    public static void main(String[] args) {
        //测试
        String str = "abcdef";
        System.out.println("===交换前===");
        System.out.println(str);
        try {
            str = reverse(str, 1, 4);
        } catch (Exception e) {
            System.out.println(e.getMessage());
            return;
        }
        System.out.println("===交换后===");
        System.out.println(str);
    }
    /**
     * (1) 将字符串中指定部分进行反转。比如将"abcdef"反转为"aedcbf"
     * (2) 编写方法 public static String reverse(String  str, int start , int end) 搞定
     * 思路分析
     * (1) 先把方法定义确定
     * (2) 把 String 转成 char[] ，因为char[] 的元素是可以交换的
     * (3) 画出分析示意图
     * (4) 代码实现
     */
    public static String reverse(String str, int start, int end) {
        //对输入的参数做一个验证
        //老韩重要的编程技巧分享!!!
        //(1) 写出正确的情况
        //(2) 然后取反即可
        //(3) 这样写，你的思路就不乱
        if(!(str != null && start >= 0 && end > start && end < str.length())) {
            throw new RuntimeException("参数不正确");
        }
        char[] chars = str.toCharArray();
        char temp = ' '; //交换辅助变量
        for (int i = start, j = end; i < j; i++, j--) {
            temp = chars[i];
            chars[i] = chars[j];
            chars[j] = temp;
        }
        //使用chars 重新构建一个String 返回即可
        return new String(chars);
    }
}
```

![](https://img-blog.csdnimg.cn/ca22be3c700f4d879a5a940d7b1b3033.png)

```
package com.hspedu.homework;
public class Homework02 {
    public static void main(String[] args) {
        String name = "abc";
        String pwd = "123456";
        String email = "ti@i@sohu.com";
        try {
            userRegister(name,pwd,email);
            System.out.println("恭喜你，注册成功~");
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }
    }
    /**
     * 思路分析
     * (1) 先编写方法 userRegister(String name, String pwd, String email) {}
     * (2) 针对 输入的内容进行校核，如果发现有问题，就抛出异常，给出提示
     * (3) 单独的写一个方法，判断 密码是否全部是数字字符 boolean
     */
    public static void userRegister(String name, String pwd, String email) {
        //再加入一些校验
        if(!(name != null && pwd != null && email != null)) {
            throw  new RuntimeException("参数不能为null");
        }
        //过关
        //第一关
        int userLength = name.length();
        if (!(userLength >= 2 && userLength <= 4)) {
            throw new RuntimeException("用户名长度为2或3或4");
        }
        //第二关
        if (!(pwd.length() == 6 && isDigital(pwd))) {
            throw new RuntimeException("密码的长度为6，要求全是数字");
        }
        //第三关
        int i = email.indexOf('@');
        int j = email.indexOf('.');
        if (!(i > 0 && j > i)) {
            throw new RuntimeException("邮箱中包含@和.   并且@在.的前面");
        }
    }
    //单独的写一个方法，判断 密码是否全部是数字字符 boolean
    public static boolean isDigital(String str) {
        char[] chars = str.toCharArray();
        for (int i = 0; i < chars.length; i++) {
            if (chars[i] < '0' || chars[i] > '9') {
                return false;
            }
        }
        return true;
    }
}
```

![](https://img-blog.csdnimg.cn/db46a05cbc594986b08c21a078b7bc54.png)

```
package com.hspedu.homework;
public class Homework03 {
    public static void main(String[] args) {
        String name = "Willian Jefferson Clinton";
        printName(name);
    }
    /**
     * 思路分析
     * (1) 对输入的字符串进行 分割split(" ")
     * (2) 对得到的String[] 进行格式化String.format（）
     * (3) 对输入的字符串进行校验即可
     */
    public static void printName(String str) {
        if(str == null) {
            System.out.println("str 不能为空");
            return;
        }
        String[] names = str.split(" ");
        if(names.length != 3) {
            System.out.println("输入的字符串格式不对");
            return;
        }
        String format = String.format("%s,%s .%c", names[2], names[0], names[1].toUpperCase().charAt(0));
        System.out.println(format);
    }
}
```

![](https://img-blog.csdnimg.cn/d8cccf23654c43aa865d099a7a67cdae.png)  
![](https://img-blog.csdnimg.cn/7e6c9211e34d4ca19f0215794c217c08.png)