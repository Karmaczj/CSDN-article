> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/weixin_43973189/article/details/121110520?spm=1001.2014.3001.5501)

#### 目录

*   *   *   [第 2 章 Java 概述](#_2__Java__1)
        *   [第 3 章 变量](#_3___41)
        *   [第 4 章 运算符](#_4___90)
        *   [第 5 章 程序控制结构](#_5___262)
        *   [第 6 章 数组、排序和查找](#_6___490)
        *   [第 7 章 面向对象编程 (基础部分)](#_7___734)
        *   [第 8 章 面向对象编程 (中级部分)](#_8___1212)

#### 第 2 章 Java 概述

2.1 Java 重要特点

1.  Java 语言是面向对象的 (oop)
2.  Java 语言是健壮的。Java 的强类型机制、异常处理、垃圾的自动收集等是 Java 程序健壮性的重要保证
3.  Java 语言是跨平台性的。[即: 一个编译好的. class 文件可以在多个系统下运行，这种特性称为跨平台]
4.  Java 语言是解释型的 [了解] 解释性语言：javascript,PHP, java 编译性语言: c / c++ 区别是：解释性语言，编译后的代码，不能直接被机器执行, 需要解释器来执行, 编译性语言, 编译后的代码, 可 以直接被机器执行, c /c++

2.2 什么是 JDK，JRE  
2.2.1 JDK 基本介绍

1.  JDK 的全称 (Java Development Kit Java 开发工具包)  
    JDK = JRE + java 的开发工具 [java, javac,javadoc,javap 等]
2.  JDK 是提供给 Java 开发人员使用的，其中包含了 java 的开发工具，也包括了 JRE。所以安装了 JDK，就不用在单独 安装 JRE 了。

2.2.2 JRE 基本介绍

1.  JRE(Java Runtime Environment Java 运行环境)  
    JRE = JVM + Java 的核心类库 [类]
2.  包括 Java 虚拟机 (JVM Java Virtual Machine) 和 Java 程序所需的核心类库等，如果想要运行一个开发好的 Java 程序， 计算机中只需要安装 JRE 即可。

2.2.3 JDK、JRE 和 JVM 的包含关系

1.  JDK = JRE + 开发工具集（例如 Javac,java 编译工具等)
2.  JRE = JVM + Java SE 标准类库（java 核心类库）
3.  如果只想运行开发好的 .class 文件 只需要 JRE

2.3 Java 开发注意事项和细节说明  
一个源文件中最多只能有一个 public 类。其它类的个数不限，也可以将 main 方法写在非 public 类中，然后指定运行非 public 类，这样入口方法就是非 public 的 main 方法

2.4 Java 转义字符  
2.4.1 Java 常用的转义字符  
![](https://img-blog.csdnimg.cn/3344a41a7eef45ce9e7b3252fcb0a2a5.png)  
2.5 注释 (comment)  
2.5.1 Java 中的注释类型

1.  单行注释 //
2.  多行注释 /* */
3.  文档注释 /** */

2.6 DOS 命令 (了解)  
2.6.1 相关的知识补充: **相对路径， 绝对路径**  
![](https://img-blog.csdnimg.cn/6c1b3bac8a7f4a728c9d01425a4ba4ea.png)  
2.6.2 常用的 dos 命令  
![](https://img-blog.csdnimg.cn/49b8afd932ea477689229f89ea78f67b.png)

#### 第 3 章 变量

3.5 程序中 + 号的使用  
![](https://img-blog.csdnimg.cn/f77122622835408c865359f925652a64.png)  
3.6 数据类型 每一种数据都定义了明确的数据类型，在内存中分配了不同大小的内存空间 (字节)。  
![](https://img-blog.csdnimg.cn/48a5fd7228cc4c45b897aadff1ead594.png)  
3.7 整数类型  
3.7.3 整型的类型  
![](https://img-blog.csdnimg.cn/17105792e51846c3af8ef172e79f8b6b.png)  
3.7.4 整型的使用细节  
![](https://img-blog.csdnimg.cn/bdd87b209a384eb8aef57fda6fdc4583.png)  
3.8 浮点类型  
3.8.3 浮点型的分类  
![](https://img-blog.csdnimg.cn/a8c8a0a5f1734d4a9e3722e455e82d2f.png)  
3.8.4 说明一下

1.  关于浮点数在机器中存放形式的简单说明, 浮点数 = 符号位 + 指数位 + 尾数位
2.  尾数部分可能丢失，造成精度损失 (小数都是近似值)。

3.8.5 浮点型使用细节  
![](https://img-blog.csdnimg.cn/3f31f6f27c6e4d4abc47c283300e0e4d.png)  
3.9 Java API 文档  
![](https://img-blog.csdnimg.cn/c0fa0e245dd84cd9a549e909d0724596.png)  
![](https://img-blog.csdnimg.cn/04f24fd5e93c4d1b8573bcac066806e3.png)  
3.10 字符类型 (char)  
3.10.3 字符类型使用细节  
![](https://img-blog.csdnimg.cn/a35c442923d441f89966cd4a5854caeb.png)  
![](https://img-blog.csdnimg.cn/64425f49d74848fd82b94628a277af78.png)  
3.11 ASCII 码介绍 (了解)  
![](https://img-blog.csdnimg.cn/024eb1f7e6eb4ee6bdf61b16011c937e.png)  
3.12 Unicode 编码介绍 (了解)  
![](https://img-blog.csdnimg.cn/6f3821f4620c47018c0f564f7d60a046.png)  
3.13 UTF-8 编码介绍 (了解)  
![](https://img-blog.csdnimg.cn/00049d63704a438fa2f29ebf64999b2c.png)  
3.14 布尔类型：boolean  
![](https://img-blog.csdnimg.cn/94c6a33d6aae4e9d81e13a969fde9d73.png)  
![](https://img-blog.csdnimg.cn/b3867d51d9134c9fada222cb0c6d9d5b.png)  
例如：  
![](https://img-blog.csdnimg.cn/a0da1148ccb94ba8a16acbc7c4473911.png)  
3.15 基本数据类型转换  
3.15.1 自动类型转换  
![](https://img-blog.csdnimg.cn/7b878af053fa45cfb18c53b0739e7611.png)  
3.15.2 自动类型转换注意和细节  
![](https://img-blog.csdnimg.cn/bbb89b78b3034008bf989048e92e1eba.png)  
例如：  
![](https://img-blog.csdnimg.cn/c48c990558584cde9b9f811fddf1562f.png)  
![](https://img-blog.csdnimg.cn/e6a43e73a074411498b9093fc375da85.png)  
3.17 基本数据类型和 String 类型的转换  
3.17.1 介绍和使用  
![](https://img-blog.csdnimg.cn/a597291aa37a437896c5d9de41348f18.png)  
![](https://img-blog.csdnimg.cn/793c275842ed4c2c823d1daf36bcb301.png)

#### 第 4 章 运算符

4.1 运算符介绍  
4.1.1 运算符介绍  
运算符是一种特殊的符号，用以表示数据的运算、赋值和比较等。

1.  算术运算符
2.  赋值运算符
3.  关系运算符 [比较运算符]
4.  逻辑运算符
5.  位运算符 [需要二进制基础]
6.  三元运算符

4.2 算术运算符  
4.2.3 案例演示  
![](https://img-blog.csdnimg.cn/8c4da3b4e49a4eb2b8f256ae6bb693aa.png)

```
// % 取模 ,取余 
// 在 % 的本质 看一个公式!!!! a % b = a - a / b * b 
// -10 % 3 => -10 - (-10) / 3 * 3 = -10 + 9 = -1 
// 10 % -3 = 10 - 10 / (-3) * (-3) = 10 - 9 = 1 
// -10 % -3 = (-10) - (-10) / (-3) * (-3) = -10 + 9 = -1
System.out.println(10 % 3); //1 
System.out.println(-10 % 3); // -1 
System.out.println(10 % -3); //1 
System.out.println(-10 % -3);//-1
```

4.2.5 面试题  
![](https://img-blog.csdnimg.cn/229eca9e5f814b9c8b7498136361d41b.png)

```
public class ArithmeticOperatorExercise01 { 
//编写一个 main 方法 
	public static void main(String[] args) {
	int i = 1;//i->1 
	i = i++; //规则使用临时变量: (1) temp = i; (2) i = i + 1; (3) i = temp; 
	System.out.println(i); // 1
	
	int j = 1; 
	j = ++j; //规则使用临时变量: (1) j = j + 1; (2) temp = j; (3) j = temp;
	System.out.println(j); //2
```

解析：  
![](https://img-blog.csdnimg.cn/025827c81e9941749ad2843b3c8f9197.png)  
4.3 关系运算符 (比较运算符)  
4.3.2 关系运算符一览  
![](https://img-blog.csdnimg.cn/9a6b7381507143a1aaeb18ddf29a5214.png)  
4.3.4 细节说明

1.  关系运算符组成的表达式，我们称为关系表达式。 例如：a > b

4.4 逻辑运算符  
4.4.2 逻辑运算符一览  
分为两组学习

1.  短路与 && ， 短路或 ||，取反 !
2.  逻辑与 &，逻辑或 |，^ 逻辑异或  
    ![](https://img-blog.csdnimg.cn/8a8033f8782e4986b29e8dffebbd0476.png)

4.4.5 && 和 & 使用区别

1.  && 短路与：如果第一个条件为 false，则第二个条件不会判断，最终结果为 false，效率高
2.  & 逻辑与：不管第一个条件是否为 false，第二个条件都要判断，效率低
3.  开发中， 我们使用的基本是使用短路与 &&, 效率高

4.4.8 || 和 | 使用区别

1.  || 短路或：如果第一个条件为 true，则第二个条件不会判断，最终结果为 true，效率高
2.  | 逻辑或：不管第一个条件是否为 true，第二个条件都要判断，效率低
3.  开发中，我们基本使用 ||

4.4.12 练习题 1 请写出每题的输出结果  
![](https://img-blog.csdnimg.cn/3837cebd73a74831be6706aff2c4cbad.png)  
4.4.13 练习题 2 请写输出结果  
![](https://img-blog.csdnimg.cn/78a4ef9aec934353ac9b2cac25f3cc07.png)  
4.5 赋值运算符  
4.5.2 赋值运算符的分类  
基本赋值运算符 = ，例如：int a = 10;  
复合赋值运算符 += ，-= ，*= ， /= ，%= 等

4.5.4 赋值运算符特点  
![](https://img-blog.csdnimg.cn/3d6b19bcafa44945a9783c071f9877db.png)  
![](https://img-blog.csdnimg.cn/aec07a6aac654821824375d41b2f9208.png)  
4.7 运算符优先级  
![](https://img-blog.csdnimg.cn/c7e18f4488b5484483010abde9eb9c38.png)  
4.8.2 标识符的命名规范 [更加专业]  
![](https://img-blog.csdnimg.cn/c97b21067f914274802625bfe9249052.png)  
4.10 保留字  
![](https://img-blog.csdnimg.cn/23a037c314274ea8b2c2877bd8c34753.png)  
4.11 键盘输入语句

4.11.1 介绍  
在编程中，需要接收用户输入的数据，就可以使用键盘输入语句来获取。Input.java , 需要一个 扫描器 (对象), 就是 Scanner

4.11.2 步骤 ：

1.  导入该类的所在包, java.util.*
2.  创建该类对象（声明变量）
3.  调用里面的功能

4.11.3 案例演示：  
要求：可以从控制台接收用户信息，【姓名，年龄，薪水】

```
import java.util.Scanner;//表示把 java.util 下的 Scanner 类导入 
public class Input { 
//编写一个 main 方法 
	public static void main(String[] args) { 
	//演示接受用户的输入 
	//步骤 
	//Scanner 类 表示 简单文本扫描器，在 java.util 包 
	//1. 引入/导入 Scanner 类所在的包 
	//2. 创建 Scanner 对象 , new 创建一个对象,体会 
	// myScanner 就是 Scanner 类的对象 
	Scanner myScanner = new Scanner(System.in); 
	//3. 接收用户输入了， 使用 相关的方法 
	System.out.println("请输入名字"); 

	//当程序执行到 next 方法时，会等待用户输入~~~ 
	String name = myScanner.next(); //接收用户输入字符串 
	System.out.println("请输入年龄"); 
	int age = myScanner.nextInt(); //接收用户输入 int 
	System.out.println("请输入薪水"); 
	double sal = myScanner.nextDouble(); //接收用户输入 double 
	System.out.println("人的信息如下:");
	System.out.println("名字=" + name + " 年龄=" + age + " 薪水=" + sal); 
	} 
}
```

4.12 进制  
4.12.1 进制介绍  
![](https://img-blog.csdnimg.cn/4024602381ff4839ae0d268cabf474a1.png)  
4.15 二进制转换成十进制示例  
![](https://img-blog.csdnimg.cn/36d0bece86304c1c8be3574129e858c0.png)  
4.16 八进制转换成十进制示例  
![](https://img-blog.csdnimg.cn/bad5fbe0c6f74462a06b36d0604e1cfa.png)  
4.17 十六进制转换成十进制示例  
规则：从最低位 (右边) 开始，将每个位上的数提取出来，乘以 16 的 (位数 - 1) 次方，然后求和。

4.18 十进制转换成二进制  
![](https://img-blog.csdnimg.cn/1d3f131327a346358a077a86375882a8.png)  
4.19 十进制转换成八进制  
规则：将该数不断除以 8，直到商为 0 为止，然后将每步得到的余数倒过来，就是对应的八进制。

4.20 十进制转换成十六进制  
规则：将该数不断除以 16，直到商为 0 为止，然后将每步得到的余数倒过来，就是对应的十六进制。

4.21 二进制转换成八进制  
规则：从低位开始, 将二进制数每三位一组，转成对应的八进制数即可。  
案例：请将 ob11010101 转成八进制  
ob11(3)010(2)101(5) => 0325

4.22 二进制转换成十六进制  
规则：从低位开始，将二进制数每四位一组，转成对应的十六进制数即可。

4.23 八进制转换成二进制  
规则：将八进制数每 1 位，转成对应的一个 3 位的二进制数即可。

4.24 十六进制转换成二进制  
规则：将十六进制数每 1 位，转成对应的 4 位的一个二进制数即可。

4.27 原码、反码、补码  
![](https://img-blog.csdnimg.cn/1ded32984525458f9c7808d7617b3523.png)  
例子：  
![](https://img-blog.csdnimg.cn/38d7c43ff40841869ceebbcc9c7aac85.png)  
![](https://img-blog.csdnimg.cn/34df0123cb0441118f4b70fef38c6caa.png)  
![](https://img-blog.csdnimg.cn/dee4a95118034da89bc0f84e53437cfe.png)  
4.28 位运算符

4.28.1 java 中有 7 个位运算 (&、|、^、~、>>、<< 和 >>>)

4.28.2 还有 3 个位运算符 >>、<<和>>> , 运算规则:  
![](https://img-blog.csdnimg.cn/c208523fbb2e4df0bd94420536936b8e.png)  
4.28.3 应用案例  
![](https://img-blog.csdnimg.cn/a74d627b36cb4e8cb19f80082dbfa438.png)  
4.29 本章作业  
![](https://img-blog.csdnimg.cn/4e37d418d3ad4e82991a66419465948f.png)  
![](https://img-blog.csdnimg.cn/553961c7739642e6a75b69de983663ff.png)

#### 第 5 章 程序控制结构

5.1 程序流程控制介绍  
![](https://img-blog.csdnimg.cn/694d7ca06a264012b1909e691ee14349.png)  
5.2 顺序控制  
![](https://img-blog.csdnimg.cn/ae54cafdb25c40efa6b78ac11fb871f6.png)  
5.3 分支控制 if-else  
5.3.1 分支控制 if-else 介绍  
![](https://img-blog.csdnimg.cn/7e13320467bc49e59186a225d7431301.png)  
5.3.2 单分支  
![](https://img-blog.csdnimg.cn/e1b45a9ca7ff4585bda730a4fe2dc9ff.png)  
5.4.1 双分支  
![](https://img-blog.csdnimg.cn/c753182de16d4711842da85bd71106bd.png)  
5.4.4 多分支

多分支的流程图  
![](https://img-blog.csdnimg.cn/0ab622eeeff0456f9052691b85cd9f2f.png)  
案例演示 2  
![](https://img-blog.csdnimg.cn/e11c33a95b31468e99696b6a4d1a4a38.png)  
5.6 switch 分支结构  
5.6.1 基本语法  
![](https://img-blog.csdnimg.cn/7dc892662c0c4007a0f96fa58d4f9802.png)  
5.6.2 switch 分支结构流程图  
![](https://img-blog.csdnimg.cn/06fdce31057a44049799253deb1630ce.png)

5.6.4 switch 注意事项和细节讨论  
![](https://img-blog.csdnimg.cn/8769ca5352a94b42b403d6fd17db66b3.png)  
5.6.5 switch 课堂练习

2.  对学生成绩大于 60 分的，输出 "合格"。低于 60 分的，输出 "不合格"。(注：输入的成绩不能大于 100), 提示 成绩 / 60

```
//思路分析 
//1. 这道题，可以使用 分支来完成， 但是要求使用 switch 
//2. 这里我们需要进行一个转换, 编程思路 : 
// 如果成绩在 [60,100] , (int)(成绩/60) = 1 
// 如果成绩在 [0,60) , (int)(成绩/60) = 0 

//代码实现 
double score = 1.1; 
//使用 if-else 保证输入的成绩有有效的 0-100 
if( score >= 0 && score <= 100) { 
	switch ((int)(score / 60)) { 
		case 0 : 
			System.out.println("不合格"); 
			break; 
		case 1 : 
			System.out.println("合格"); 
			break; 
	} 
} else { 
	System.out.println("输入的成绩在 0-100"); 
}
```

3.  根据用于指定月份，打印该月份所属的季节。3,4,5 春季 6,7,8 夏季 9,10,11 秋季 12, 1, 2 冬季 [课堂练习, 提示 使用穿透]

```
//思路分析 
//1. 创建 Scanner 对象， 接收用户输入 
//2. 使用 int month 接收 
//3. 使用 switch 来匹配 ,使用穿透来完成，比较简洁 

Scanner myScanner = new Scanner(System.in); 
System.out.println("输入月份"); 
int month = myScanner.nextInt(); 
switch(month) { 
	case 3: 
	case 4: 
	case 5: 
		System.out.println("这是春季"); 
		break; 
	case 6: 
	case 7:
	case 8: 
		System.out.println("这是夏季"); 
		break; 
	case 9: 
	case 10: 
	case 11: 
		System.out.println("这是秋季"); 
		break; 
	case 1: 
	case 2: 
	case 12: 
		System.out.println("这是冬季"); 
		break; 
	default : 
		System.out.println("你输入的月份不对(1-12)"); 
}
```

5.6.6 switch 和 if 的比较  
![](https://img-blog.csdnimg.cn/34f22c84adc04e5897620a0960b5d47b.png)  
5.7 for 循环控制

5.7.3 for 循环流程图  
![](https://img-blog.csdnimg.cn/34da69cd17934711abded9d278716e46.png)

5.7.5 for 循环练习题

1.  打印 1~100 之间所有是 9 的倍数的整数，统计个数 及 总和.[化繁为简, 先死后活]

```
public class ForExercise { 
	//编写一个 main 方法 
	public static void main(String[] args) { 
		//打印 1~100 之间所有是 9 的倍数的整数，统计个数 及 总和.[化繁为简,先死后活] 
		//老韩的两个编程思想(技巧) 
		//1. 化繁为简 : 即将复杂的需求，拆解成简单的需求，逐步完成 编程 = 思想 --练习-> 代码 
		//2. 先死后活 : 先考虑固定的值，然后转成可以灵活变化的值 
		
		//思路分析 
		//打印 1~100 之间所有是 9 的倍数的整数，统计个数及总和 
		//化繁为简
		//(1) 完成 输出 1-100 的值 
		//(2) 在输出的过程中，进行过滤，只输出 9 的倍数 i % 9 ==0 
		//(3) 统计个数 定义一个变量 int count = 0; 当 条件满足时 count++; 
		//(4) 总和 , 定义一个变量 int sum = 0; 当条件满足时累积 sum += i; 
		//先死后活 
		//(1) 为了适应更好的需求，把范围的开始的值和结束的值，做出变量 
		//(2) 还可以更进一步 9 倍数也做成变量 int t = 9; 
	
		int count = 0; //统计 9 的倍数个数 变量 
		int sum = 0; //总和 
		int start = 10; 
		int end = 200; 
		int t = 5; //倍数 
		for(int i = start; i <= end; i++) { 
			if( i % t == 0) { 
				System.out.println("i=" + i); 
				count++; 
				sum += i;//累积 
			} 
		}

		System.out.println("count=" + count); 
		System.out.println("sum=" + sum); 
	} 
}
```

5.8 while 循环控制

5.8.2 while 循环执行流程分析

1.  画出流程图  
    ![](https://img-blog.csdnimg.cn/b293bc75b4a3479f872436dd5fe2cf20.png)  
    5.9 do…while 循环控制

5.9.3 do…while 循环执行流程图  
![](https://img-blog.csdnimg.cn/3b9840fda1064034bbcddeb3eb8167ca.png)  
5.10.4 经典的打印金字塔  
![](https://img-blog.csdnimg.cn/89ada4182954446eb84c72f1c26d9637.png)

```
public class Stars { 
	//编写一个 main 方法 
	public static void main(String[] args) { 
		/* 
			  * 
			*  * 
		   *    * 
		  ******** 
	
		思路分析 
		化繁为简 
		1. 先打印一个矩形 
		***** 
		*****
		***** 
		***** 
		*****
		
		2. 打印半个金字塔
		* 		//第 1 层 有 1 个* 
		** 		//第 2 层 有 2 个* 
		*** 	//第 3 层 有 3 个* 
		**** 	//第 4 层 有 4 个* 
		***** 	//第 5 层 有 5 个*
		
		3. 打印整个金字塔
		    * 		//第 1 层 有 1 个* 2 * 1 -1 有 4=(总层数-1)个空格 
		   *** 		//第 2 层 有 3 个* 2 * 2 -1 有 3=(总层数-2)个空格 
		  ***** 	//第 3 层 有 5 个* 2 * 3 -1 有 2=(总层数-3)个空格 
		 ******* 	//第 4 层 有 7 个* 2 * 4 -1 有 1=(总层数-4)个空格 
		********* 	//第 5 层 有 9 个* 2 * 5 -1 有 0=(总层数-5)个空格
		
		4. 打印空心的金字塔 [最难的]
		    * 		//第 1 层 有 1 个* 当前行的第一个位置是*,最后一个位置也是* 
		   * * 		//第 2 层 有 2 个* 当前行的第一个位置是*,最后一个位置也是* 
		  *   * 	//第 3 层 有 2 个* 当前行的第一个位置是*,最后一个位置也是* 
		 *     * 	//第 4 层 有 2 个* 当前行的第一个位置是*,最后一个位置也是* 
		********* 	//第 5 层 有 9 个* 全部输出*
		
		先死后活
		5 层数做成变量 int totalLevel = 5;
		*/
		int totalLevel = 20; //层数 
		for(int i = 1; i <= totalLevel; i++) { //i 表示层数 
			//在输出*之前，还有输出 对应空格 = 总层数-当前层 
			for(int k = 1; k <= totalLevel - i; k++ ) { 
				System.out.print(" "); 
			}
			//控制打印每层的*个数 
			for(int j = 1;j <= 2 * i - 1;j++) { 
				//当前行的第一个位置是*,最后一个位置也是*, 最后一层全部 * 
				if(j == 1 || j == 2 * i - 1 || i == totalLevel) { 
					System.out.print("*"); 
				} else { //其他情况输出空格 
					System.out.print(" "); 
				} 
			}
			//每打印完一层的*后，就换行 println 本身会换行 
			System.out.println(""); 
		} 
	} 
}
```

5.11 跳转控制语句 - break

5.11.1 看下面一个需求  
![](https://img-blog.csdnimg.cn/05cf2451ff434457bec488132976a163.png)  
![](https://img-blog.csdnimg.cn/76130ab023ed4af1b56fdccf23787c48.png)  
5.11.6 注意事项和细节说明：  
![](https://img-blog.csdnimg.cn/6ce2ef5b155044dc9eac2d08e2661d6f.png)  
5.12 跳转控制语句 - continue

5.12.1 基本介绍：  
![](https://img-blog.csdnimg.cn/9020e3a4989c43e3b05feb5580dc04d9.png)  
5.13 跳转控制语句 - return  
return 使用在方法，表示跳出所在的方法，在讲解方法的时候，会详细的介绍，这里我们简单的提一下。注意：如果 return 写在 main 方法，则退出程序。

#### 第 6 章 数组、排序和查找

6.1 为什么需要数组

6.1.1 数组介绍  
![](https://img-blog.csdnimg.cn/919c15f9359941d3b2f12bb5ba16e2b2.png)  
6.1.2 数组快速入门  
可以通过 数组名. length 得到数组的大小 / 长度

6.2 数组的使用  
![](https://img-blog.csdnimg.cn/6262b173f221473abbc1896a6689c449.png)  
注意：int a[] = new int [5] 和 int[ ] a = new int [5] 是等价的。

6.2.1 使用方式 2 - 动态初始化  
![](https://img-blog.csdnimg.cn/ddde89cac23248f5adb3a22598d5bfb8.png)  
6.2.2 使用方式 3 - 静态初始化  
![](https://img-blog.csdnimg.cn/cdb8217ad4cb440c951cf9323b6e5ed9.png)  
6.3 数组使用注意事项和细节  
![](https://img-blog.csdnimg.cn/d8e84e2880f4495dab309e3f39c01140.png)  
6.5 数组赋值机制  
![](https://img-blog.csdnimg.cn/9db72c8d64da45bf8a2d649ce764981b.png)  
6.6 数组拷贝  
![](https://img-blog.csdnimg.cn/dbbfc563de0a4c74a69224ff9ef969fa.png)  
![](https://img-blog.csdnimg.cn/a0cc1f9dcb534243b10733571479630f.png)  
6.7 数组反转  
![](https://img-blog.csdnimg.cn/7e7dfc1ac51e4c0da550f32af187b866.png)  
方式 1：通过找规律反转

```
public class ArrayReverse { 
	//编写一个 main 方法 
	public static void main(String[] args) { 
		//定义数组 
		int[] arr = {11, 22, 33, 44, 55, 66}; 
		//规律 
		//1. 把 arr[0] 和 arr[5] 进行交换 {66,22,33,44,55,11}
		//2. 把 arr[1] 和 arr[4] 进行交换 {66,55,33,44,22,11} 
		//3. 把 arr[2] 和 arr[3] 进行交换 {66,55,44,33,22,11} 
		//4. 一共要交换 3 次 = arr.length / 2 
		//5. 每次交换时，对应的下标 是 arr[i] 和 arr[arr.length - 1 -i] 
		//代码 
		//优化 
		int temp = 0; 
		int len = arr.length; //计算数组的长度 
		for( int i = 0; i < len / 2; i++) { 
			temp = arr[len - 1 - i];//保存 
			arr[len - 1 - i] = arr[i]; 
			arr[i] = temp; 
		}

		System.out.println("===翻转后数组==="); 
		for(int i = 0; i < arr.length; i++) { 
			System.out.print(arr[i] + "\t");//66,55,44,33,22,11 
		} 
	} 
}
```

方式 2：使用逆序赋值方式

```
public class ArrayReverse02 { 
	//编写一个 main 方法 
	public static void main(String[] args) { 
		//定义数组 
		int[] arr = {11, 22, 33, 44, 55, 66}; 
		//使用逆序赋值方式 
		//1. 先创建一个新的数组 arr2 ,大小 arr.length 
		//2. 逆序遍历 arr ,将 每个元素拷贝到 arr2 的元素中(顺序拷贝) 
		//3. 建议增加一个循环变量 j -> 0 -> 5 
		int[] arr2 = new int[arr.length]; 
		//逆序遍历 arr 
		for(int i = arr.length - 1, j = 0; i >= 0; i--, j++) { 
			arr2[j] = arr[i]; 
		}
		//4. 当 for 循环结束，arr2 就是一个逆序的数组 {66, 55, 44,33, 22, 11} 
		//5. 让 arr 指向 arr2 数据空间, 此时 arr 原来的数据空间就没有变量引用 
		// 会被当做垃圾，销毁 
		arr = arr2; 
		System.out.println("====arr 的元素情况====="); 
		//6. 输出 arr 看看 
		for(int i = 0; i < arr.length; i++) {
			System.out.print(arr[i] + "\t"); 
		} 
	} 
}
```

6.9 排序的介绍  
![](https://img-blog.csdnimg.cn/e47345ecdb0b442390c4a3e36cfd0eb5.png)  
6.10 冒泡排序法  
冒泡排序（Bubble Sorting）的基本思想是：通过对待排序序列从后向前（从下标较大的元素开始），依次比较相邻元素 的值，若发现逆序则交换，使值较大的元素逐渐从前移向后部，就象水底下的气泡一样逐渐向上冒。  
![](https://img-blog.csdnimg.cn/02f34086d66f4ff5a4fc35af6c7eba6c.png)  
![](https://img-blog.csdnimg.cn/b1e4f465cb17479bb1a29b597813eb3b.png)

```
public class BubbleSort { 
	//编写一个 main 方法 
	public static void main(String[] args) {
	int[] arr = {24, 69, 80, 57, 13, -1, 30, 200, -110}; 
	int temp = 0; //用于辅助交换的变量 
	
	//将多轮排序使用外层循环包括起来即可 
	for( int i = 0; i < arr.length - 1; i++) {//外层循环是 4 次 
		for( int j = 0; j < arr.length - 1 - i; j++) {//4 次比较-3 次-2 次-1 次 
			//如果前面的数>后面的数，就交换 
			if(arr[j] > arr[j + 1]) { 
				temp = arr[j]; 
				arr[j] = arr[j+1]; 
				arr[j+1] = temp; 
			} 
		}
		System.out.println("\n==第"+(i+1)+"轮=="); 
		for(int j = 0; j < arr.length; j++) { 
			System.out.print(arr[j] + "\t");
		} 
	}
}
```

6.12 查找

6.12.1 介绍：  
在 java 中，我们常用的查找有两种:

1.  顺序查找
2.  二分查找

6.12.2 案例演示：  
有一个数列：白眉鹰王、金毛狮王、紫衫龙王、青翼蝠王猜数游戏：从键盘中任意输入一个名称，判断数列中是否 包含此名称【顺序查找】 要求: 如果找到了，就提示找到，并给出下标值。

```
import java.util.Scanner; 
public class SeqSearch { 
	//编写一个 main 方法 
	public static void main(String[] args) { 
		/*
		思路分析 
		1. 定义一个字符串数组 
		2. 接收用户输入, 遍历数组，逐一比较，如果有，则提示信息，并退出 
		*/
		//定义一个字符串数组 
		String[] names = {"白眉鹰王", "金毛狮王", "紫衫龙王", "青翼蝠王"}; 
		Scanner myScanner = new Scanner(System.in); 
		System.out.println("请输入名字"); 
		String findName = myScanner.next(); 
		
		//遍历数组，逐一比较，如果有，则提示信息，并退出 
		//这里老师给大家一个编程思想/技巧, 一个经典的方法 
		int index = -1; 
		for(int i = 0; i < names.length; i++) { 
			//比较 字符串比较 equals, 如果要找到名字就是当前元素 
			if(findName.equals(names[i])) { 
				System.out.println("恭喜你找到 " + findName); 
				System.out.println("下标为= " + i); 
				//把 i 保存到 index 
				index = i; 
				break;//退出 
			} 
		}
		if(index == -1) { //没有找到 
			System.out.println("sorry ,没有找到 " + findName); 
		}
	}
}
```

6.14 二维数组的使用

6.14.2 使用方式 1: 动态初始化  
![](https://img-blog.csdnimg.cn/bb2a5298e4164ee78d47609f0fd9be42.png)  
![](https://img-blog.csdnimg.cn/b0078b90b5574d889d11571bcd39661d.png)  
6.14.3 使用方式 2: 动态初始化  
![](https://img-blog.csdnimg.cn/3297225ae51547fdbce011dfd25afb43.png)  
6.14.4 使用方式 3: 动态初始化 - 列数不确定  
![](https://img-blog.csdnimg.cn/0f8ed73fd532488f8cc6383a4434b3d5.png)

```
public class TwoDimensionalArray03 {
	//编写一个 main 方法 
	public static void main(String[] args) { 
		//创建 二维数组，一个有 3 个一维数组，但是每个一维数组还没有开数据空间 
		int[][] arr = new int[3][]; 
		for(int i = 0; i < arr.length; i++) {//遍历 arr 每个一维数组 
			//给每个一维数组开空间 new 
			//如果没有给一维数组 new ,那么arr[i]就是 null 
			arr[i] = new int[i + 1]; 
			
			//遍历一维数组，并给一维数组的每个元素赋值 
			for(int j = 0; j < arr[i].length; j++) { 
				arr[i][j] = i + 1;//赋值 
			}
		}
		System.out.println("=====arr 元素====="); 
		//遍历 arr 输出 
		for(int i = 0; i < arr.length; i++) { 
			//输出 arr 的每个一维数组 
			for(int j = 0; j < arr[i].length; j++) { 
				System.out.print(arr[i][j] + " "); 
			}
			System.out.println();//换行 
		} 
	} 
}
```

6.14.5 使用方式 4: 静态初始化  
![](https://img-blog.csdnimg.cn/6e11a0d7172345769476dac41d345e13.png)  
6.15 二维数组的应用案例  
使用二维数组打印一个 10 行杨辉三角  
![](https://img-blog.csdnimg.cn/d467ab406d0144a399d788a8f2f07b0b.png)

```
public class YangHui { 
	//编写一个 main 方法 
	public static void main(String[] args) {
		/*
			规律
			1.第一行有 1 个元素, 第 n 行有 n 个元素 
			2. 每一行的第一个元素和最后一个元素都是 1 
			3. 从第三行开始, 对于非第一个元素和最后一个元素的元素的值. arr[i][j] 
			arr[i][j] = arr[i-1][j] + arr[i-1][j-1]; //必须找到这个规律 
		*/ 
		int[][] yangHui = new int[12][]; 
		for(int i = 0; i < yangHui.length; i++) {//遍历 yangHui 的每个元素 
			//给每个一维数组(行) 开空间 
			yangHui[i] = new int[i+1]; 
			//给每个一维数组(行) 赋值 
			for(int j = 0; j < yangHui[i].length; j++){ 
				//每一行的第一个元素和最后一个元素都是 1 
				if(j == 0 || j == yangHui[i].length - 1) { 
					yangHui[i][j] = 1; 
				} else {//中间的元素 
					yangHui[i][j] = yangHui[i-1][j] + yangHui[i-1][j-1]; 
				}
			} 
		}
		//输出杨辉三角 
		for(int i = 0; i < yangHui.length; i++) { 
			for(int j = 0; j < yangHui[i].length; j++) {//遍历输出该行 
				System.out.print(yangHui[i][j] + "\t"); 
			}
			System.out.println();//换行. 
		} 
	} 
}
```

6.16 二维数组使用细节和注意事项  
![](https://img-blog.csdnimg.cn/1b0ad0e0d85548199d47a5815fd03482.png)  
6.17 二维数组课堂练习  
![](https://img-blog.csdnimg.cn/19b0659705e546778597169ffb8bb144.png)

#### 第 7 章 面向对象编程 (基础部分)

7.1 类与对象

7.1.5 类与对象的关系示意图  
![](https://img-blog.csdnimg.cn/904ecda8b7c94bdfbb6e2e517d5284b6.png)  
7.1.6 类与对象的关系示意图  
![](https://img-blog.csdnimg.cn/748e3e99fef4411e9ba7dce646ef93f7.png)  
7.1.8 类和对象的区别和联系  
![](https://img-blog.csdnimg.cn/3226834b917d48fa9826ce77bf0e8f54.png)  
7.1.9 对象在内存中存在形式（重要，必须搞清楚）  
![](https://img-blog.csdnimg.cn/884bbd215e474820aca4974d760a3c3f.png)  
7.1.10 属性 / 成员变量 / 字段  
![](https://img-blog.csdnimg.cn/6342ba5663194135af434de716a5e8a1.png)  
注意事项和细节说明：  
![](https://img-blog.csdnimg.cn/d72bab95d5b3481fb850fe1eeb7c5086.png)  
7.1.13 类和对象的内存分配机制  
![](https://img-blog.csdnimg.cn/2267adf1ad084ee2a4b439390c4eeaec.png)  
![](https://img-blog.csdnimg.cn/d0184b6a651d45dcb73ae12556615d80.png)  
![](https://img-blog.csdnimg.cn/76c614a047d54ade97cb8c3a4cc648f0.png)  
看一个练习题，并分析画出内存布局图，进行分析  
![](https://img-blog.csdnimg.cn/db18deb11e7a419e9d050e2cac1b7622.png)  
最后一句会报 NullPointerException 异常。

7.2 成员方法

7.2.3 方法的调用机制原理：(重要!- 示意图!!!)  
![](https://img-blog.csdnimg.cn/e09a5253a50345ef95cf6f40f650b06b.png)  
7.2.5 成员方法的好处  
![](https://img-blog.csdnimg.cn/9d8b0aeb6eca44e6b35bf2ad853bd8be.png)  
7.2.7 注意事项和使用细节  
![](https://img-blog.csdnimg.cn/3bb822f913a541a2824d999ccf58c9f4.png)  
![](https://img-blog.csdnimg.cn/9ea74ed5a5d2454688ebbdc7975a4216.png)

```
public class MethodDetail02 { 
	//编写一个 main 方法 
	public static void main(String[] args) { 
		A a = new A(); 
		//a.sayOk(); 
		a.m1(); 
	} 
}
class A { 
	//同一个类中的方法调用：直接调用即可 
	public void print(int n) { 
		System.out.println("print()方法被调用 n=" + n);
	}
	public void sayOk() { //sayOk 调用 print(直接调用即可) 
		print(10); 
		System.out.println("继续执行 sayOK()~~~"); 
	}
	//跨类中的方法 A 类调用 B 类方法：需要通过对象名调用 
	public void m1() { 
		//创建 B 对象, 然后在调用方法即可 
		System.out.println("m1() 方法被调用"); 
		B b = new B(); 
		b.hi(); 
		System.out.println("m1() 继续执行:)"); 
	} 
}
class B { 
	public void hi() { 
		System.out.println("B 类中的 hi()被执行"); 
	} 
}
```

7.3 成员方法传参机制 (非常非常重要)  
![](https://img-blog.csdnimg.cn/458bd907d5354a9ca23a5dfebdef5177.png)

```
public class MethodParameter01 { 
	//编写一个 main 方法 
	public static void main(String[] args) { 
		int a = 10; 
		int b = 20; //创建 AA 对象 名字 obj 
		AA obj = new AA(); 
		obj.swap(a, b); //调用 swap 
		System.out.println("main 方法 a=" + a + " b=" + b);//a=10 b=20 
	} 
}
class AA { 
	public void swap(int a,int b){ 
		System.out.println("\na 和 b 交换前的值\na=" + a + "\tb=" + b);//a=10 b=20 
		//完成了 a 和 b 的交换 
		int tmp = a; 
		a = b; 
		b = tmp; 
		System.out.println("\na 和 b 交换后的值\na=" + a + "\tb=" + b);//a=20 b=10 
	} 
}
```

![](https://img-blog.csdnimg.cn/19a46928a23643719a4f03732c9810f9.png)  
7.3.2 引用数据类型的传参机制  
![](https://img-blog.csdnimg.cn/f1767d2d279849f79a5f201755fc33f4.png)  
在看一个案例，下面的方法会对原来的对象有影响吗？  
p=null 和 p = new Person(); 对应示意图  
![](https://img-blog.csdnimg.cn/3e023ecd43824dd3ad7bcbbfc8e93928.png)  
7.4 方法递归调用 (非常非常重要，比较难)

7.4.4 递归重要规则  
![](https://img-blog.csdnimg.cn/32ccf72e3cbc4146b51c541c6a1b7e1d.png)  
7.4.5 课堂练习  
![](https://img-blog.csdnimg.cn/d819bb84e28a4012b893a4a4dcc72f35.png)

```
public class RecursionExercise01 { 
	//编写一个 main 方法 
	public static void main(String[] args) { 
		T t1 = new T(); 
		int n = 7; 
		int res = t1.fibonacci(n); 
		if(res != -1) { 
			System.out.println("当 n="+ n +" 对应的斐波那契数=" + res); 
		} 
		//桃子问题 
		int day = 0; 
		int peachNum = t1.peach(day); 
		if(peachNum != -1) { 
			System.out.println("第 " + day + "天有" + peachNum + "个桃子"); 
		}
	} 
}
class T {
	/*
	请使用递归的方式求出斐波那契数 1,1,2,3,5,8,13...给你一个整数 n，求出它的值是多 
	思路分析 
	1. 当 n = 1 斐波那契数 是 1 
	2. 当 n = 2 斐波那契数 是 1
	3. 当 n >= 3 斐波那契数 是前两个数的和 
	4. 这里就是一个递归的思路 
	*/ 
	public int fibonacci(int n) { 
		if( n >= 1) { 
			if( n == 1 || n == 2) { 
				return 1; 
			} else { 
				return fibonacci(n-1) + fibonacci(n-2); 
			} 
		} else { 
			System.out.println("要求输入的 n>=1 的整数"); 
			return -1; 
		} 
	}
	/*
	猴子吃桃子问题：有一堆桃子，猴子第一天吃了其中的一半，并再多吃了一个！ 
	以后每天猴子都吃其中的一半，然后再多吃一个。当到第 10 天时， 
	想再吃时（即还没吃），发现只有 1 个桃子了。问题：最初共多少个桃子？ 
	思路分析 逆推 
	1. day = 10 时 有 1 个桃子 
	2. day = 9 时 有 (day10 + 1) * 2 = 4 
	3. day = 8 时 有 (day9 + 1) * 2 = 10 
	4. 规律就是 前一天的桃子 = (后一天的桃子 + 1) *2
	5. 递归 
	 */ 
	 public int peach(int day) { 
	 	if(day == 10) {//第 10 天，只有 1 个桃 
	 		return 1; 
	 	} else if ( day >= 1 && day <=9 ) { 
	 		return (peach(day + 1) + 1) * 2;//规则，自己要想 
	 	} else { 
	 		System.out.println("day 在 1-10"); return -1; 
	 	} 
	 } 
}
```

7.4.6 递归调用应用实例 - 迷宫问题  
![](https://img-blog.csdnimg.cn/9f1c16d29397439fbdaabc442d576bcb.png)

```
public class MiGong { 
	//编写一个 main 方法 
	public static void main(String[] args) { 
		//思路 
		//1. 先创建迷宫，用二维数组表示 int[][] map = new int[8][7]; 
		//2. 先规定 map 数组的元素值: 0 表示可以走 1 表示障碍物 
		int[][] map = new int[8][7]; 
		//3. 将最上面的一行和最下面的一行，全部设置为 1 
		for(int i = 0; i < 7; i++) { 
			map[0][i] = 1; 
			map[7][i] = 1; 
		}
		//4.将最右面的一列和最左面的一列，全部设置为 1 
		for(int i = 0; i < 8; i++) {
			map[i][0] = 1; 
			map[i][6] = 1; 
		}
		map[3][1] = 1; 
		map[3][2] = 1; 
		map[2][2] = 1; //测试回溯 

		//输出当前的地图 
		System.out.println("=====当前地图情况======"); 
		for(int i = 0; i < map.length; i++) { 
			for(int j = 0; j < map[i].length; j++) { 
				System.out.print(map[i][j] + " ");//输出一行 
			}
			System.out.println(); 
		}
		//使用 findWay 给老鼠找路 
		T t1 = new T(); 
		//下右上左 
		t1.findWay(map, 1, 1); 
		System.out.println("\n====找路的情况如下=====");
		for(int i = 0; i < map.length; i++) { 
			for(int j = 0; j < map[i].length; j++) { 
				System.out.print(map[i][j] + " ");//输出一行 
			}
			System.out.println(); 
		} 
	} 
}
class T { 
	//使用递归回溯的思想来解决老鼠出迷宫 
	//老韩解读 
	//1. findWay 方法就是专门来找出迷宫的路径 
	//2. 如果找到，就返回 true ,否则返回 false 
	//3. map 就是二维数组，即表示迷宫 
	//4. i,j 就是老鼠的位置，初始化的位置为(1,1) 
	//5. 因为我们是递归的找路，所以我先规定 map 数组的各个值的含义 
	// 0 表示可以走 1 表示障碍物 2 表示可以走 3 表示走过，但是走不通是死路 
	//6. 当 map[6][5] =2 就说明找到通路,就可以结束，否则就继续找. 
	//7. 先确定老鼠找路策略 下->右->上->左
	public boolean findWay(int[][] map , int i, int j) { 
		if(map[6][5] == 2) {//说明已经找到 
			return true; 
		} else { 
			if(map[i][j] == 0) {//当前这个位置 0,说明表示可以走 
				//我们假定可以走通 
				map[i][j] = 2; 
				//使用找路策略，来确定该位置是否真的可以走通 
				//下->右->上->左 
				if(findWay(map, i + 1, j)) {//先走下 
					return true; 
				} else if(findWay(map, i, j + 1)){//右 
					return true; 
				} else if(findWay(map, i-1, j)) {//上 
					return true; 
				} else if(findWay(map, i, j-1)){//左 
					return true; 
				} else { 
					map[i][j] = 3; 
					return false; 
				} 
			} else { //map[i][j] = 1 , 2, 3 
				return false; 
			} 
		}
	}
}
```

![](https://img-blog.csdnimg.cn/688786afdfac4cc8a3c7b58eabd7a467.png)  
![](https://img-blog.csdnimg.cn/27e36d6c5f6f46728d4abd55949a04ac.png)  
7.4.7 递归调用应用实例 - 汉诺塔  
![](https://img-blog.csdnimg.cn/d27f66e3a02d46668065c35ae9d27b20.png)  
![](https://img-blog.csdnimg.cn/ea3e6e678ca444f992b0d18b508fe9b2.png)  
HanoiTower.java

```
public class HanoiTower { 
	//编写一个 main 方法 
	public static void main(String[] args) { 
		Tower tower = new Tower(); 
		tower.move(64, 'A', 'B', 'C'); 
	} 
}
class Tower { 
	//方法 
	//num 表示要移动的个数, a, b, c 分别表示 A 塔，B 塔, C 塔 
	public void move(int num , char a, char b ,char c) { 
		//如果只有一个盘 num = 1
		if(num == 1) { 
			System.out.println(a + "->" + c); 
		} else { 
			//如果有多个盘，可以看成两个 , 最下面的和上面的所有盘(num-1) 
			//(1)先移动上面所有的盘到 b, 借助 c 
			move(num - 1 , a, c, b); 
			//(2)把最下面的这个盘，移动到 c 
			System.out.println(a + "->" + c); 
			//(3)再把 b 塔的所有盘，移动到 c ,借助 a 
			move(num - 1, b, a, c); 
		} 
	} 
}
```

7.4.8 递归调用应用实例 - 八皇后问题 [同学们先尝试做，后面老师评讲.]  
![](https://img-blog.csdnimg.cn/8b637e5bdeae49eda7e65d9e6acbe6ff.png)  
![](https://img-blog.csdnimg.cn/357c717055844ef6b5dfecd8a413dfa3.png)  
7.5 方法重载 (OverLoad)

7.5.1 基本介绍  
java 中允许同一个类中，多个同名方法的存在，但要求 形参列表不一致！  
比如：System.out.println(); 其中 out 是 PrintStream 类型

7.5.2 重载的好处

1.  减轻了起名的麻烦
2.  减轻了记名的麻烦

7.5.4 注意事项和使用细节  
![](https://img-blog.csdnimg.cn/41fb7fd71c1344b2b11e37644a36179e.png)  
7.6 可变参数

7.6.1 基本概念  
java 允许将同一个类中多个同名同功能但参数个数不同的方法，封装成一个方法。  
就可以通过可变参数实现

7.6.2 基本语法  
访问修饰符 返回类型 方法名 (数据类型… 形参名) { }

7.6.3 快速入门案例 (VarParameter01.java)  
看一个案例：类 HspMethod，方法 sum 【可以计算 2 个数的和，3 个数的和 ， 4、5， 。。】

```
public class VarParameter01 { 
	//编写一个 main 方法 
	public static void main(String[] args) { 
		HspMethod m = new HspMethod(); 
		System.out.println(m.sum(1, 5, 100)); //106 
		System.out.println(m.sum(1,19)); //20 
	} 
}
class HspMethod { 
	//可以计算 2 个数的和，3 个数的和 ， 4. 5， 。。
	//老韩解读
	//1. int... 表示接受的是可变参数，类型是 int ,即可以接收多个 int(0-多) 
	//2. 使用可变参数时，可以当做数组来使用 即 nums 可以当做数组 
	//3. 遍历 nums 求和即可 
	public int sum(int... nums) { 
		//System.out.println("接收的参数个数=" + nums.length); 
		int res = 0; 
		for(int i = 0; i < nums.length; i++) { 
			res += nums[i]; 
		}
		return res; 
	} 
}
```

7.6.4 注意事项和使用细节  
![](https://img-blog.csdnimg.cn/e01812cb8e27481f9b278f81c26de40c.png)

```
public class VarParameterDetail { 
	//编写一个 main 方法 
	public static void main(String[] args) {
		//细节: 可变参数的实参可以为数组 
		int[] arr = {1, 2, 3}; 
		T t1 = new T(); 
		t1.f1(arr); 
	} 
}
class T { 
	public void f1(int... nums) { 
		System.out.println("长度=" + nums.length); 
	}
	//细节: 可变参数可以和普通类型的参数一起放在形参列表，但必须保证可变参数在最后 
	public void f2(String str, double... nums) { 
	}
	//细节: 一个形参列表中只能出现一个可变参数 
	//下面的写法是错的. 
	// public void f3(int... nums1, double... nums2) { 
	// } 
}
```

7.7 作用域

7.7.1 基本使用  
![](https://img-blog.csdnimg.cn/2f4e64c37f8a48d6934510542d30a102.png)  
7.7.2 注意事项和细节使用  
![](https://img-blog.csdnimg.cn/26d54aff1c2e4a909abc254815fe5e00.png)  
7.8 构造方法 / 构造器

7.8.2 基本语法  
![](https://img-blog.csdnimg.cn/f578678024c1457b94f9113741d9ce42.png)  
7.8.3 基本介绍  
![](https://img-blog.csdnimg.cn/ecf7bd9cdc874d32912eab850ba26aca.png)  
7.8.5 注意事项和使用细节  
![](https://img-blog.csdnimg.cn/c6387e4fe98c4d779e8f8799687faba2.png)  
7.9 对象创建的流程分析

7.9.1 看一个案例  
![](https://img-blog.csdnimg.cn/0f39aef905fd48719b14087d6f59a030.png)  
![](https://img-blog.csdnimg.cn/f18e8d4ab4ee474794a7800da9d51d93.png)  
7.10 this 关键字

7.10.2 深入理解 this  
![](https://img-blog.csdnimg.cn/f184940568b54bbfa70a3edd3282ebf9.png)  
7.10.3 this 的注意事项和使用细节  
![](https://img-blog.csdnimg.cn/3da807b7cb9a4cd6b0912547b11bf02e.png)  
7.11 本章作业  
![](https://img-blog.csdnimg.cn/0bf5a006b06d4b2ea0b5a48ba3b2ada8.png)

```
public class Homework01 { 
	//编写一个main方法
	public static void main(String[] args) {
		A01 a01 = new A01();
		double[] arr = {1, 1.4, -1.3, 89.8, 123.8 , 66}; //;{};
		Double res = a01.max(arr);
		if(res != null) {
			System.out.println("arr的最大值=" + res);
		} else {
			System.out.println("arr的输入有误, 数组不能为null, 或者{}");
		}
	}
}
/*
编写类A01，定义方法max，实现求某个double数组的最大值，并返回

思路分析
1. 类名 A01
2. 方法名 max
3. 形参 (double[])
4. 返回值 double

先完成正常业务，然后再考虑代码健壮性
 */
class A01 {
	public Double max(double[] arr) {
		//老韩先判断arr是否为null,然后再判断 length 是否>0
		if( arr!= null && arr.length > 0 ) {
			//保证arr至少有一个元素 
			double max = arr[0];//假定第一个元素就是最大值
			for(int i = 1; i < arr.length; i++) {
				if(max < arr[i]) {
					max = arr[i];
				}
			}
			return max;//double
		} else {
			return null;
		}
	}
}
```

![](https://img-blog.csdnimg.cn/1d3bbb32116c403784c78a9fae583528.png)

```
public class Homework06 { 
	//编写一个main方法
	public static void main(String[] args) {
		Cale cale = new Cale(2, 10);
		System.out.println("和=" + cale.sum());
		System.out.println("差=" + cale.minus());
		System.out.println("乘=" + cale.mul());
		Double divRes = cale.div();
		if(divRes != null) {
			System.out.println("除=" + divRes);
		} 
	}
}
/*
 编程创建一个Cale计算类，在其中定义2个变量表示两个操作数，
 定义四个方法实现求和、差、乘、商(要求除数为0的话，要提示) 并创建两个对象，分别测试 
 */
class Cale {
	double num1;
	double num2;
	public Cale(double num1, double num2) {
		this.num1 = num1;
		this.num2 = num2;
	}
	//和
	public double sum() {
		return num1 + num2;
	}
	//差
	public double minus() {
		return num1 - num2;
	}
	//乘积
	public double mul() {
		return num1 * num2;
	}
	//除法
	public Double div() {
		//判断
		if(num2 == 0) {
			System.out.println("num2 不能为0");
			return null;
		} else {
			return num1 / num2;
		}
	}
}
```

#### 第 8 章 面向对象编程 (中级部分)

8.3.4 课堂练习  
![](https://img-blog.csdnimg.cn/6c647f70642a45ccaf3e58fbb2e99cc2.png)  
8.3.5 IDEA 常用快捷键  
![](https://img-blog.csdnimg.cn/7e7978e6d0ff496188cfb8448d6d3c15.png)  
第 11 点也可以用 alt + enter

8.3.6 模板 / 自定义模板  
![](https://img-blog.csdnimg.cn/9f435ef364064dbdaa1886067c00cb05.png)  
8.4 包

8.4.2 包的三大作用  
![](https://img-blog.csdnimg.cn/074b2b3519164f0c88a706052e03a062.png)  
8.4.3 包基本语法  
![](https://img-blog.csdnimg.cn/65b4f8f5f90a44bc857f58fb66c4ca36.png)  
8.4.4 包的本质分析 (原理)  
![](https://img-blog.csdnimg.cn/84da488a84744345a7111688eb1cf7c6.png)  
8.4.5 快速入门  
![](https://img-blog.csdnimg.cn/7b1a95fd8a2140fb88ec5040644c0916.png)  
8.4.6 包的命名  
![](https://img-blog.csdnimg.cn/f3de2e90405b46eca9b1c066132d9b36.png)  
8.4.7 常用的包  
![](https://img-blog.csdnimg.cn/122d3dc3c9784b1490ea201c69969724.png)  
8.4.8 如何引入包  
![](https://img-blog.csdnimg.cn/e7cac62f4ab54f4f871d774660bf4847.png)

```
package com.hspedu.pkg; 
import java.util.Arrays; 
//注意: 
//老韩建议：我们需要使用到哪个类，就导入哪个类即可，不建议使用 *导入 
//import java.util.Scanner; //表示只会引入 java.util 包下的 Scanner 
//import java.util.*;//表示将 java.util 包下的所有类都引入(导入) 
public class Import01 { 
	public static void main(String[] args) { 
		//使用系统提供 Arrays 完成 数组排序 
		int[] arr = {-1, 20, 2, 13, 3}; 
		//比如对其进行排序 
		//传统方法是，自己编写排序(冒泡) 
		//系统是提供了相关的类，可以方便完成 
		Arrays.sort(arr); 
		//输出排序结果 
		for (int i = 0; i < arr.length ; i++) { 
			System.out.print(arr[i] + "\t"); 
		}
	}
}
```

8.4.9 注意事项和使用细节  
![](https://img-blog.csdnimg.cn/c00da91f6bcd4ebabfa1cd13f79dcd5e.png)  
8.5 访问修饰符

8.5.1 基本介绍  
![](https://img-blog.csdnimg.cn/e2df4726f09d48a99eed02aef74ed6e3.png)  
8.5.2 种访问修饰符的访问范围  
![](https://img-blog.csdnimg.cn/f7cb6e3f52bf41e8af23ba062d0ca283.png)  
8.5.3 使用的注意事项  
![](https://img-blog.csdnimg.cn/882cc27ad9d741b2b7ebff138687dd8a.png)  
8.6 面向对象编程三大特征

8.6.1 基本介绍  
面向对象编程有三大特征：封装、继承和多态。

8.6.2 封装介绍  
![](https://img-blog.csdnimg.cn/2bc2e7a6d27a44a0894b78ebc672456a.png)  
8.6.3 封装的理解和好处  
![](https://img-blog.csdnimg.cn/75e7213ddc184769bdc479b1c7c83875.png)  
8.6.4 封装的实现步骤 (三步)  
![](https://img-blog.csdnimg.cn/8f7d8e7d8caf4edd86a612d278e94702.png)  
8.7.1 将构造器和 setXxx 结合  
看一个案例

```
//有三个属性的构造器 
public Person(String name, int age, double salary) { 
	// this.name = name; 
	// this.age = age; 
	// this.salary = salary; 
	//我们可以将 set 方法写在构造器中，这样仍然可以验证 
	setName(name); 
	setAge(age); 
	setSalary(salary); 
}
```

8.8 面向对象编程 - 继承

8.8.2 继承基本介绍和示意图  
![](https://img-blog.csdnimg.cn/d82e9f90b3e8476392995b5ac4807d12.png)  
8.8.3 继承的基本语法  
![](https://img-blog.csdnimg.cn/9c838dcc4cd746ffb646bcb8e3c8a1e1.png)  
8.8.5 继承给编程带来的便利

1.  代码的复用性提高了
2.  代码的扩展性和维护性提高了

8.8.6 继承的深入讨论 / 细节问题  
![](https://img-blog.csdnimg.cn/db8f9a611b4746c4a2d44274989ca189.png)  
![](https://img-blog.csdnimg.cn/7059987d74e144758852657fafbfa026.png)  
8.8.7 继承的本质分析 (重要)  
![](https://img-blog.csdnimg.cn/a39b8ae4c8a848118bbd76eb3e11eddb.png)

```
package com.hspedu.extend_; 
/**
 * 讲解继承的本质 
 */ 
public class ExtendsTheory { 
	public static void main(String[] args) { 
		Son son = new Son();//内存的布局 
		//?-> 这时请大家注意，要按照查找关系来返回信息 
		//(1) 首先看子类是否有该属性 
		//(2) 如果子类有这个属性，并且可以访问，则返回信息 
		//(3) 如果子类没有这个属性，就看父类有没有这个属性(如果父类有该属性，并且可以访问，就返回信息..) 
		//(4) 如果父类没有就按照(3)的规则，继续找上级父类，直到 Object...
		System.out.println(son.name);//返回就是大头儿子 
		//System.out.println(son.age);//返回的就是 39 
		//System.out.println(son.getAge());//返回的就是 39 
		System.out.println(son.hobby);//返回的就是旅游 
	} 
}
class GrandPa { //爷类 
	String name = "大头爷爷";
	String hobby = "旅游"; 
}
class Father extends GrandPa {//父类 
	String name = "大头爸爸"; 
	private int age = 39; 
	public int getAge() { 
		return age; 
	} 
}
class Son extends Father { //子类 
	String name = "大头儿子"; 
}
```

子类创建的内存布局：  
![](https://img-blog.csdnimg.cn/140d6f470b704731b321a5e125e32441.png)  
如果 Father 里的 age 是 private，即使 GrandPa 里也有 age，是 public，访问 age 的时候一样到 Father 就会停止，不会继续查看 GrandPa 里是否有 age。

8.8.8 课堂练习  
![](https://img-blog.csdnimg.cn/22328c619b3342fd96d6b79f2143334a.png)  
由于 B() 函数里调用了 this 函数，所以没有 super 函数，但 B(String name) 函数有 super()。

8.9 super 关键字

8.9.1 基本介绍  
super 代表父类的引用，用于访问父类的属性、方法、构造器。

8.9.2 基本语法  
![](https://img-blog.csdnimg.cn/6a4e2c3c1cd54aceb07e62bb8c87634d.png)  
8.9.3 super 给编程带来的便利 / 细节  
![](https://img-blog.csdnimg.cn/e957b27a74e249a5b4a98b4c799db520.png)  
8.9.4 super 和 this 的比较  
![](https://img-blog.csdnimg.cn/5e29405bfc004e689f137151020950c1.png)  
8.10 方法重写 / 覆盖 (override)

8.10.1 基本介绍  
![](https://img-blog.csdnimg.cn/a3b39fc775c04fc7b3b027fa93820603.png)  
8.10.3 注意事项和使用细节  
![](https://img-blog.csdnimg.cn/5bcea772d6ad4a53aaa39d463102e32c.png)  
8.10.4 课堂练习  
![](https://img-blog.csdnimg.cn/cb72a90d41844da7aa24e7ebecf86775.png)  
8.11 面向对象编程 - 多态

8.11.1 先看一个问题  
![](https://img-blog.csdnimg.cn/7381866075084546a3683f5874736b3e.png)  
8.11.2 多 [多种] 态[状态]基本介绍  
方法或对象具有多种形态。是面向对象的第三大特征，多态是建立在封装和继承基础之上的。

8.11.3 多态的具体体现

1.  方法的多态  
    重写和重载就体现多态
    
2.  对象的多态 (核心，困难，重点)  
    ![](https://img-blog.csdnimg.cn/85c4d46b53ac4ae29aa9139cc8598536.png)
    

```
package com.hspedu.poly_.objectpoly_; 
public class Animal { 
	public void cry() { 
		System.out.println("Animal cry() 动物在叫...."); 
	} 
}
package com.hspedu.poly_.objectpoly_; 
public class Cat extends Animal { 
	public void cry() { 
		System.out.println("Cat cry() 小猫喵喵叫..."); 
	} 
}
package com.hspedu.poly_.objectpoly_; 
public class Dog extends Animal {
	public void cry() { 
		System.out.println("Dog cry() 小狗汪汪叫..."); 
	} 
}
package com.hspedu.poly_.objectpoly_; 
public class PolyObject { 
	public static void main(String[] args) { 
		//体验对象多态特点 
		//animal 编译类型就是 Animal , 运行类型 Dog 
		Animal animal = new Dog(); 
		//因为运行时 , 执行到该行时，animal 运行类型是 Dog,所以 cry 就是 Dog 的 cry 
		animal.cry(); //小狗汪汪叫 
		//animal 编译类型 Animal,运行类型就是 Cat 
		animal = new Cat(); 
		animal.cry(); //小猫喵喵叫 
	} 
}
```

8.11.5 多态注意事项和细节讨论  
![](https://img-blog.csdnimg.cn/2cc7b649c3d74c3c9a5f934539aee150.png)

```
package com.hspedu.poly_.detail_; 
public class Animal { 
	String name = "动物"; 
	int age = 10; 
	public void sleep(){ 
		System.out.println("睡"); 
	}
	public void run(){ 
		System.out.println("跑");
	}
	public void eat(){ 
		System.out.println("吃"); 
	}
	public void show(){ 
		System.out.println("hello,你好"); 
	} 
}
package com.hspedu.poly_.detail_; 
public class Cat extends Animal { 
	public void eat(){//方法重写 
		System.out.println("猫吃鱼"); 
	}
	public void catchMouse(){//Cat 特有方法 
		System.out.println("猫抓老鼠"); 
	} 
}
package com.hspedu.poly_.detail_; 
public class Dog extends Animal {//Dog 是 Animal 的子类 
}
package com.hspedu.poly_.detail_; 
public class PolyDetail {
	public static void main(String[] args) { 
		//向上转型: 父类的引用指向了子类的对象 
		//语法：父类类型引用名 = new 子类类型(); 
		Animal animal = new Cat(); 
		Object obj = new Cat();//可以吗? 可以 Object 也是 Cat 的父类 
		//向上转型调用方法的规则如下: 
		//(1)可以调用父类中的所有成员(需遵守访问权限) 
		//(2)但是不能调用子类的特有的成员 
		//(#)因为在编译阶段，能调用哪些成员,是由编译类型来决定的 
		//animal.catchMouse();错误 
		//(4)最终运行效果看子类(运行类型)的具体实现, 即调用方法时，按照从子类(运行类型)开始查找方法 
		//，然后调用，规则我前面我们讲的方法调用规则一致。 
		animal.eat();//猫吃鱼.. 
		animal.run();//跑 
		animal.show();//hello,你好 
		animal.sleep();//睡 
		
		//老师希望，可以调用 Cat 的 catchMouse 方法 
		//多态的向下转型 
		//(1)语法：子类类型 引用名 =（子类类型）父类引用; 
		//问一个问题? cat 的编译类型 Cat,运行类型是 Cat 
		Cat cat = (Cat) animal; 
		cat.catchMouse();//猫抓老鼠 
		//(2)要求父类的引用必须指向的是当前目标类型的对象
		Dog dog = (Dog) animal; //可以吗？ 
		System.out.println("ok~~"); 
	} 
}
```

向下转型图解：  
![](https://img-blog.csdnimg.cn/a431a5d1968c4877827ed40ccd6ddb9c.png)  
animal 本来就指向 cat 对象，所以对 animal 向下转型为 cat 是没有问题的，用 cat 类型指向 cat 对象。

属性没有重写之说！属性的值看编译类型：

```
package com.hspedu.poly_.detail_; 
public class PolyDetail02 { 
	public static void main(String[] args) { 
		//属性没有重写之说！属性的值看编译类型 
		Base base = new Sub();//向上转型 
		System.out.println(base.count);// ？ 看编译类型 10 
		Sub sub = new Sub(); 
		System.out.println(sub.count);//? 20 
	} 
}
class Base { //父类 
	int count = 10;//属性 
}
class Sub extends Base {//子类 
	int count = 20;//属性 
}
```

instanceOf 比较操作符，用于判断对象的运行类型是否为 XX 类型或 XX 类型的子类型：

```
package com.hspedu.poly_.detail_; 
public class PolyDetail03 { 
	public static void main(String[] args) { 
		BB bb = new BB(); 
		System.out.println(bb instanceof BB);// true 
		System.out.println(bb instanceof AA);// true 
		//aa 编译类型 AA, 运行类型是 BB 
		//BB 是 AA 子类 
		AA aa = new BB();
		System.out.println(aa instanceof AA); 
		System.out.println(aa instanceof BB); 
		Object obj = new Object(); 
		System.out.println(obj instanceof AA);//false 
		String str = "hello"; 
		//System.out.println(str instanceof AA); 
		System.out.println(str instanceof Object);//true 
	} 
}
class AA {} //父类
class BB extends AA {}//子类
```

8.11.6 课堂练习  
![](https://img-blog.csdnimg.cn/c9458212f33246c8871ea5e3693f9e23.png)  
8.11.7 java 的动态绑定机制 (非常非常重要.)  
![](https://img-blog.csdnimg.cn/83a8caca885047e7beeb2b8e5b2bf718.png)

```
package com.hspedu.poly_.dynamic_; 
public class DynamicBinding { 
	public static void main(String[] args) { 
		//a 的编译类型 A, 运行类型 B 
		A a = new B();//向上转型 
		System.out.println(a.sum());//?40 -> 30 
		System.out.println(a.sum1());//?30-> 20 
	} 
}
class A {//父类 
	public int i = 10; 
	//动态绑定机制: 
	public int sum() {//父类 sum() 
		return getI() + 10;//20 + 10
	}
	public int sum1() {//父类 sum1() 
		return i + 10;//10 + 10 
	}
	public int getI() {//父类 getI 
		return i; 
	} 
}
class B extends A {//子类 
	public int i = 20; 
//  public int sum() { 
// 		return i + 20; 
// 	}
	public int getI() {//子类 getI() 
		return i; 
	} 
// 	public int sum1() { 
// 		return i + 10; 
// 	} 
}
```

8.11.8 多态的应用  
![](https://img-blog.csdnimg.cn/a18611e7b5a04246933bdee51fda70bd.png)

```
package com.hspedu.poly_.polyarr_; 
public class PloyArray { 
	public static void main(String[] args) { 
		//应用实例:现有一个继承结构如下：要求创建 1 个 Person 对象、 
		// 2 个 Student 对象和 2 个 Teacher 对象, 统一放在数组中，并调用每个对象 say 方法 
		Person[] persons = new Person[5]; 
		persons[0] = new Person("jack", 20); 
		persons[1] = new Student("mary", 18, 100); 
		persons[2] = new Student("smith", 19, 30.1); 
		persons[3] = new Teacher("scott", 30, 20000); 
		persons[4] = new Teacher("king", 50, 25000); 
		//循环遍历多态数组，调用 say 
		for (int i = 0; i < persons.length; i++) { 
			//老师提示: person[i] 编译类型是 Person ,运行类型是是根据实际情况由 JVM 来判断 
			System.out.println(persons[i].say());//动态绑定机制 
			//这里使用 类型判断 + 向下转型. 
			if(persons[i] instanceof Student) {//判断 person[i] 的运行类型是不是 Student 
				Student student = (Student)persons[i];//向下转型 
				student.study(); //小伙伴也可以使用一条语句 ((Student)persons[i]).study(); 
			} else if(persons[i] instanceof Teacher) { 
				Teacher teacher = (Teacher)persons[i]; 
				teacher.teach();
			} else if(persons[i] instanceof Person){ 
				//
			} else {
				System.out.println("你的类型有误, 请自己检查..."); 
			} 
		} 
	} 
}
```

8.12 Object 类详解

8.12.1 equals 方法  
![](https://img-blog.csdnimg.cn/b71d23e819434b3c9579b62b8d037d0b.png)  
查看 jdk 源码之前需要配置如下，不过系统已经默认自动帮你配置了：  
![](https://img-blog.csdnimg.cn/0bac8c11b4f445d1b47b3a2465f8b82b.png)  
8.12.2 如何重写 equals 方法  
应用实例: 判断两个 Person 对象的内容是否相等，如果两个 Person 对象的各个属性值都一样，则返回 true，反之 false。

```
package com.hspedu.object_; 
public class EqualsExercise01 { 
	public static void main(String[] args) { 
		Person person1 = new Person("jack", 10, '男'); 
		Person person2 = new Person("jack", 20, '男'); 
		System.out.println(person1.equals(person2));//假 
	} 
}
//判断两个 Person 对象的内容是否相等， 
//如果两个 Person 对象的各个属性值都一样，则返回 true，反之 false 
class Person{ //extends Object 
	private String name; 
	private int age; 
	private char gender; 
	//重写 Object 的 equals 方法 
	public boolean equals(Object obj) { 
		//判断如果比较的两个对象是同一个对象，则直接返回 true 
		if(this == obj) { 
			return true; 
		}
		//类型判断 
		if(obj instanceof Person) {//是 Person，我们才比较
		//进行 向下转型, 因为我需要得到 obj 的 各个属性 
		Person p = (Person)obj; 
		return this.name.equals(p.name) && this.age == p.age && this.gender == p.gender; }
		//如果不是 Person ，则直接返回 false 
		return false; 
	}
}
```

![](https://img-blog.csdnimg.cn/045bfa63542c4e3db06c0b8eeacca2f2.png)  
![](https://img-blog.csdnimg.cn/52c637a5c15f431e99e021250fb3826c.png)  
8.12.4 hashCode 方法  
![](https://img-blog.csdnimg.cn/80c8b212ba0c4cdf9a6e4c58fac4f815.png)  
![](https://img-blog.csdnimg.cn/82fb57c61a114591afda7d5b55c825d6.png)  
8.12.5 toString 方法  
![](https://img-blog.csdnimg.cn/f466cd8ebe2c49bab9b039a749f471dd.png)

```
package com.hspedu.object_; 
public class ToString_ { 
	public static void main(String[] args) { 
		/*
			Object 的 toString() 源码 
			(1)getClass().getName() 类的全类名(包名+类名 ) 
			(2)Integer.toHexString(hashCode()) 将对象的 hashCode 值转成 16 进制字符串 
			public String toString() { 
				return getClass().getName() + "@" + Integer.toHexString(hashCode()); 
			}
		*/ 
		Monster monster = new Monster("小妖怪", "巡山的", 1000); 
		System.out.println(monster.toString() + " hashcode=" + monster.hashCode()); 
		System.out.println("==当直接输出一个对象时，toString 方法会被默认的调用=="); 
		System.out.println(monster); //等价 monster.toString()
	} 
}
class Monster { 
	private String name; 
	private String job; 
	private double sal; 
	public Monster(String name, String job, double sal) { 
		this.name = name; 
		this.job = job; 
		this.sal = sal; 
	}
	//重写 toString 方法, 输出对象的属性 
	//使用快捷键即可 alt+insert -> toString 
	@Override 
	public String toString() { //重写后，一般是把对象的属性值输出，当然程序员也可以自己定制 
		return "Monster{" + " + name + '\'' + 
			", job='" + job + '\'' + 
			", sal=" + sal + 
			'}'; 
	}
	@Override
	protected void finalize() throws Throwable { 
		System.out.println("fin.."); 
	} 
}
```

8.12.6 finalize 方法  
![](https://img-blog.csdnimg.cn/d6743b410c0d4133901ecd7f4bb11718.png)

```
package com.hspedu.object_; 
//演示 Finalize 的用法 
public class Finalize_ { 
	public static void main(String[] args) { 
		Car bmw = new Car("宝马"); 
		//这时 car 对象就是一个垃圾,垃圾回收器就会回收(销毁)对象, 在销毁对象前，会调用该对象的 finalize 方法 
		//程序员就可以在 finalize 中，写自己的业务逻辑代码(比如释放资源：数据库连接,或者打开文件..) 
		//如果程序员不重写 finalize,那么就会调用 Object 类的 finalize, 即默认处理
		//如果程序员重写了 finalize, 就可以实现自己的逻辑 
		bmw = null; 
		System.gc();//主动调用垃圾回收器 
		System.out.println("程序退出了...."); 
	} 
}
class Car { 
	private String name; 
	//属性, 资源。。 
	public Car(String name) { 
		this.name = name; 
	}
	//重写 finalize 
	@Override 
	protected void finalize() throws Throwable { 
		System.out.println("我们销毁 汽车" + name ); 
		System.out.println("释放了某些资源..."); 
	} 
}
```

8.13 断点调试 (debug)

8.13.1 一个实际需求  
![](https://img-blog.csdnimg.cn/2fdcc580afbc4b7ca9c9554c284dcdeb.png)  
8.13.3 断点调试的快捷键  
![](https://img-blog.csdnimg.cn/0c2bb4637a7943698eca02554d25b2b0.png)  
小技巧：将光标放在某个变量上，可以看到最新的数据。  
老韩小技巧：断点可以在 debug 过程中，动态的下断点

8.15 本章作业  
![](https://img-blog.csdnimg.cn/46ce8c74f9494c7e9c9da22d5397f150.png)  
![](https://img-blog.csdnimg.cn/1b5a074d3b904e84bc3352d911a40b71.png)  
![](https://img-blog.csdnimg.cn/4cace6286d40414d88ad78cbb5b1efd6.png)  
![](https://img-blog.csdnimg.cn/11711ecb19794a338b98d479235a26d3.png)