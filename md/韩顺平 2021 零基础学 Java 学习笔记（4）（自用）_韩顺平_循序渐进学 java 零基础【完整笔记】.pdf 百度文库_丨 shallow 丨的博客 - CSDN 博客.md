> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/weixin_43973189/article/details/121490360?spm=1001.2014.3001.5502)

#### 目录

*   *   *   [第 21 章 网络编程](#_21___1)
        *   [第 23 章 反射 (reflection)](#_23__reflection_448)
        *   [第 24 章 零基础学 MySQL](#_24___MySQL_1038)

#### 第 21 章 [网络编程](https://so.csdn.net/so/search?q=%E7%BD%91%E7%BB%9C%E7%BC%96%E7%A8%8B&spm=1001.2101.3001.7020)

21.1 网络的相关概念

21.1.1 网络通信  
![](https://img-blog.csdnimg.cn/21e8dd264a2d4e9eb1234abb9a3c129c.png)  
21.1.2 网络  
![](https://img-blog.csdnimg.cn/c8fa9323d4564d0988f406ab01cd907b.png)  
21.1.3 ip 地址  
![](https://img-blog.csdnimg.cn/d6dc9c812a0f47cfbd70ac2df6d66bd6.png)  
21.1.4 ipv4 地址分类  
![](https://img-blog.csdnimg.cn/dbe346089d65448fb7dd56a98392774f.png)  
21.1.5 域名  
![](https://img-blog.csdnimg.cn/15b1728464744006a72df539b8da45ce.png)  
![](https://img-blog.csdnimg.cn/0b32b3f57df84e8a8e3b6eb117a1281a.png)  
21.1.6 网络[通信协议](https://so.csdn.net/so/search?q=%E9%80%9A%E4%BF%A1%E5%8D%8F%E8%AE%AE&spm=1001.2101.3001.7020)  
![](https://img-blog.csdnimg.cn/e7b8c35932494f5faaafe449acbdf73c.png)  
![](https://img-blog.csdnimg.cn/43ac13c5fa8247afbc6363c32e390752.png)  
21.1.8 TCP 和 UDP  
![](https://img-blog.csdnimg.cn/89ef5f7a757844efa687efc3d83ad030.png)  
21.2 InetAddress 类  
![](https://img-blog.csdnimg.cn/eca7341665e7471dbe50f29d4e10bd7a.png)  
![](https://img-blog.csdnimg.cn/5bca31bb7927428498d9a079b9b469f7.png)

```
package com.hspedu.api;
import java.net.InetAddress;
import java.net.UnknownHostException;
/**
 * 演示InetAddress 类的使用
 */
public class API_ {
    public static void main(String[] args) throws UnknownHostException {
        //1. 获取本机的InetAddress 对象
        InetAddress localHost = InetAddress.getLocalHost();
        System.out.println(localHost);//DESKTOP-S4MP84S/192.168.12.1

        //2. 根据指定主机名 获取 InetAddress对象
        InetAddress host1 = InetAddress.getByName("DESKTOP-S4MP84S");
        System.out.println("host1=" + host1);//DESKTOP-S4MP84S/192.168.12.1

        //3. 根据域名返回 InetAddress对象, 比如 www.baidu.com 对应
        InetAddress host2 = InetAddress.getByName("www.baidu.com");
        System.out.println("host2=" + host2);//www.baidu.com / 110.242.68.4

        //4. 通过 InetAddress 对象，获取对应的地址
        String hostAddress = host2.getHostAddress();//IP 110.242.68.4
        System.out.println("host2 对应的ip = " + hostAddress);//110.242.68.4

        //5. 通过 InetAddress 对象，获取对应的主机名/或者是域名
        String hostName = host2.getHostName();
        System.out.println("host2对应的主机名/域名=" + hostName); // www.baidu.com
    }
}
```

![](https://img-blog.csdnimg.cn/9db3cc166c0842e584aaff54c3964d21.png)  
21.3 Socket  
![](https://img-blog.csdnimg.cn/79c1891380af47efb031b81783eba295.png)  
![](https://img-blog.csdnimg.cn/519ec0beeb9144b4bf1730301d9fc841.png)  
21.4 TCP 网络通信编程

21.4.1 基本介绍  
![](https://img-blog.csdnimg.cn/0f4c93b4dd0e46a6858cb4fe8f515eab.png)  
21.4.2 应用案例 1(使用字节流)  
![](https://img-blog.csdnimg.cn/fe8fc6eb7b474ff3beea03d4bd67bcbf.png)  
![](https://img-blog.csdnimg.cn/50db65de61614eefa9dad67e2a2a460a.png)  
SocketTCP01Server.java

```
package com.hspedu.socket;
import java.io.IOException;
import java.io.InputStream;
import java.net.ServerSocket;
import java.net.Socket;
/**
 * 服务端
 */
public class SocketTCP01Server {
    public static void main(String[] args) throws IOException {
        //思路
        //1. 在本机 的9999端口监听, 等待连接
        //   细节: 要求在本机没有其它服务在监听9999
        //   细节：这个 ServerSocket 可以通过 accept() 返回多个Socket[多个客户端连接服务器的并发]
        ServerSocket serverSocket = new ServerSocket(9999);
        System.out.println("服务端，在9999端口监听，等待连接..");
        //2. 当没有客户端连接9999端口时，程序会 阻塞, 等待连接
        //   如果有客户端连接，则会返回Socket对象，程序继续
        Socket socket = serverSocket.accept();
        System.out.println("服务端 socket =" + socket.getClass());
        //3. 通过socket.getInputStream() 读取客户端写入到数据通道的数据, 显示
        InputStream inputStream = socket.getInputStream();
        //4. IO读取
        byte[] buf = new byte[1024];
        int readLen = 0;
        while ((readLen = inputStream.read(buf)) != -1) {
            System.out.println(new String(buf, 0, readLen));//根据读取到的实际长度，显示内容.
        }
        //5.关闭流和socket
        inputStream.close();
        socket.close();
        serverSocket.close();//关闭
    }
}
```

SocketTCP01Client.java

```
package com.hspedu.socket;
import java.io.IOException;
import java.io.OutputStream;
import java.net.InetAddress;
import java.net.Socket;
import java.net.UnknownHostException;
/**
 * 客户端，发送 "hello, server" 给服务端
 */
public class SocketTCP01Client {
    public static void main(String[] args) throws IOException {
        //思路
        //1. 连接服务端 (ip , 端口）
        //解读: 连接本机的 9999端口, 如果连接成功，返回Socket对象
        Socket socket = new Socket(InetAddress.getLocalHost(), 9999);
        System.out.println("客户端 socket返回=" + socket.getClass());
        //2. 连接上后，生成Socket, 通过socket.getOutputStream()
        //   得到 和 socket对象关联的输出流对象
        OutputStream outputStream = socket.getOutputStream();
        //3. 通过输出流，写入数据到 数据通道
        outputStream.write("hello, server".getBytes());
        //4. 关闭流对象和socket, 必须关闭
        outputStream.close();
        socket.close();
        System.out.println("客户端退出.....");
    }
}
```

21.4.3 应用案例 2(使用字节流)  
![](https://img-blog.csdnimg.cn/6776bf09da6a4025a354b30657f8ef17.png)  
![](https://img-blog.csdnimg.cn/bf1abd7691f24d5b8cdda3db4cfbd496.png)  
SocketTCP02Server.java

```
package com.hspedu.socket;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.ServerSocket;
import java.net.Socket;
/**
 * 服务端
 */
@SuppressWarnings({"all"})
public class SocketTCP02Server {
    public static void main(String[] args) throws IOException {
        //思路
        //1. 在本机 的9999端口监听, 等待连接
        //   细节: 要求在本机没有其它服务在监听9999
        //   细节：这个 ServerSocket 可以通过 accept() 返回多个Socket[多个客户端连接服务器的并发]
        ServerSocket serverSocket = new ServerSocket(9999);
        System.out.println("服务端，在9999端口监听，等待连接..");
        //2. 当没有客户端连接9999端口时，程序会 阻塞, 等待连接
        //   如果有客户端连接，则会返回Socket对象，程序继续
        Socket socket = serverSocket.accept();
        System.out.println("服务端 socket =" + socket.getClass());
        //3. 通过socket.getInputStream() 读取客户端写入到数据通道的数据, 显示
        InputStream inputStream = socket.getInputStream();
        //4. IO读取
        byte[] buf = new byte[1024];
        int readLen = 0;
        while ((readLen = inputStream.read(buf)) != -1) {
            System.out.println(new String(buf, 0, readLen));//根据读取到的实际长度，显示内容.
        }
        //5. 获取socket相关联的输出流
        OutputStream outputStream = socket.getOutputStream();
        outputStream.write("hello, client".getBytes());
        //   设置结束标记
        socket.shutdownOutput();
        //6.关闭流和socket
        outputStream.close();
        inputStream.close();
        socket.close();
        serverSocket.close();//关闭
    }
}
```

SocketTCP02Client.java

```
package com.hspedu.socket;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.InetAddress;
import java.net.Socket;
/**
 * 客户端，发送 "hello, server" 给服务端
 */
@SuppressWarnings({"all"})
public class SocketTCP02Client {
    public static void main(String[] args) throws IOException {
        //思路
        //1. 连接服务端 (ip , 端口）
        //解读: 连接本机的 9999端口, 如果连接成功，返回Socket对象
        Socket socket = new Socket(InetAddress.getLocalHost(), 9999);
        System.out.println("客户端 socket返回=" + socket.getClass());
        //2. 连接上后，生成Socket, 通过socket.getOutputStream()
        //   得到 和 socket对象关联的输出流对象
        OutputStream outputStream = socket.getOutputStream();
        //3. 通过输出流，写入数据到 数据通道
        outputStream.write("hello, server".getBytes());
        //   设置结束标记
        socket.shutdownOutput();
        //4. 获取和socket关联的输入流. 读取数据(字节)，并显示
        InputStream inputStream = socket.getInputStream();
        byte[] buf = new byte[1024];
        int readLen = 0;
        while ((readLen = inputStream.read(buf)) != -1) {
            System.out.println(new String(buf, 0, readLen));
        }
        //5. 关闭流对象和socket, 必须关闭
        inputStream.close();
        outputStream.close();
        socket.close();
        System.out.println("客户端退出.....");
    }
}
```

21.4.4 应用案例 3(使用字符流)  
![](https://img-blog.csdnimg.cn/53519956d33c440da223db1155f6a5b1.png)  
![](https://img-blog.csdnimg.cn/f8f9df3a75d84eb488caff3973ba5076.png)  
SocketTCP03Server.java

```
package com.hspedu.socket;
import java.io.*;
import java.net.ServerSocket;
import java.net.Socket;
/**
 * 服务端, 使用字符流方式读写
 */
@SuppressWarnings({"all"})
public class SocketTCP03Server {
    public static void main(String[] args) throws IOException {
        //思路
        //1. 在本机 的9999端口监听, 等待连接
        //   细节: 要求在本机没有其它服务在监听9999
        //   细节：这个 ServerSocket 可以通过 accept() 返回多个Socket[多个客户端连接服务器的并发]
        ServerSocket serverSocket = new ServerSocket(9999);
        System.out.println("服务端，在9999端口监听，等待连接..");
        //2. 当没有客户端连接9999端口时，程序会 阻塞, 等待连接
        //   如果有客户端连接，则会返回Socket对象，程序继续
        Socket socket = serverSocket.accept();
        System.out.println("服务端 socket =" + socket.getClass());
        //3. 通过socket.getInputStream() 读取客户端写入到数据通道的数据, 显示
        InputStream inputStream = socket.getInputStream();
        //4. IO读取, 使用字符流, 老师使用 InputStreamReader 将 inputStream 转成字符流
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(inputStream));
        String s = bufferedReader.readLine();
        System.out.println(s);//输出
        //5. 获取socket相关联的输出流
        OutputStream outputStream = socket.getOutputStream();
       //    使用字符输出流的方式回复信息
        BufferedWriter bufferedWriter = new BufferedWriter(new OutputStreamWriter(outputStream));
        bufferedWriter.write("hello client 字符流");
        bufferedWriter.newLine();// 插入一个换行符，表示回复内容的结束
        bufferedWriter.flush();//注意需要手动的flush
        //6.关闭流和socket
        bufferedWriter.close();
        bufferedReader.close();
        socket.close();
        serverSocket.close();//关闭
    }
}
```

SocketTCP03Client.java

```
package com.hspedu.socket;
import java.io.*;
import java.net.InetAddress;
import java.net.Socket;
/**
 * 客户端，发送 "hello, server" 给服务端， 使用字符流
 */
@SuppressWarnings({"all"})
public class SocketTCP03Client {
    public static void main(String[] args) throws IOException {
        //思路
        //1. 连接服务端 (ip , 端口）
        //解读: 连接本机的 9999端口, 如果连接成功，返回Socket对象
        Socket socket = new Socket(InetAddress.getLocalHost(), 9999);
        System.out.println("客户端 socket返回=" + socket.getClass());
        //2. 连接上后，生成Socket, 通过socket.getOutputStream()
        //   得到 和 socket对象关联的输出流对象
        OutputStream outputStream = socket.getOutputStream();
        //3. 通过输出流，写入数据到 数据通道, 使用字符流
        BufferedWriter bufferedWriter = new BufferedWriter(new OutputStreamWriter(outputStream));
        bufferedWriter.write("hello, server 字符流");
        bufferedWriter.newLine();//插入一个换行符，表示写入的内容结束, 注意，要求对方使用readLine()!!!!
        bufferedWriter.flush();// 如果使用的字符流，需要手动刷新，否则数据不会写入数据通道
        //4. 获取和socket关联的输入流. 读取数据(字符)，并显示
        InputStream inputStream = socket.getInputStream();
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(inputStream));
        String s = bufferedReader.readLine();
        System.out.println(s);
        //5. 关闭流对象和socket, 必须关闭
        bufferedReader.close();//关闭外层流
        bufferedWriter.close();
        socket.close();
        System.out.println("客户端退出.....");
    }
}
```

21.4.5 应用案例 4  
![](https://img-blog.csdnimg.cn/f81f0d832320400c844315c217c287d7.png)  
![](https://img-blog.csdnimg.cn/74c6c739f5ef46119e41c280e32c9546.png)  
TCPFileUploadClient.java

```
package com.hspedu.upload;
import java.io.*;
import java.net.InetAddress;
import java.net.Socket;
/**
 * 文件上传的客户端
 */
public class TCPFileUploadClient {
    public static void main(String[] args) throws Exception {
        //客户端连接服务端 8888，得到Socket对象
        Socket socket = new Socket(InetAddress.getLocalHost(), 8888);
        //创建读取磁盘文件的输入流
        //String filePath = "e:\\qie.png";
        String filePath = "e:\\abc.mp4";
        BufferedInputStream bis  = new BufferedInputStream(new FileInputStream(filePath));
        //bytes 就是filePath对应的字节数组
        byte[] bytes = StreamUtils.streamToByteArray(bis);
        //通过socket获取到输出流, 将bytes数据发送给服务端
        BufferedOutputStream bos = new BufferedOutputStream(socket.getOutputStream());
        bos.write(bytes);//将文件对应的字节数组的内容，写入到数据通道
        bis.close();
        socket.shutdownOutput();//设置写入数据的结束标记
        
        //=====接收从服务端回复的消息=====
        InputStream inputStream = socket.getInputStream();
        //使用StreamUtils 的方法，直接将 inputStream 读取到的内容 转成字符串
        String s = StreamUtils.streamToString(inputStream);
        System.out.println(s);

        //关闭相关的流
        inputStream.close();
        bos.close();
        socket.close();
    }
}
```

TCPFileUploadServer.java

```
package com.hspedu.upload;
import java.io.*;
import java.net.ServerSocket;
import java.net.Socket;
/**
 * 文件上传的服务端
 */
public class TCPFileUploadServer {
    public static void main(String[] args) throws Exception {
        //1. 服务端在本机监听8888端口
        ServerSocket serverSocket = new ServerSocket(8888);
        System.out.println("服务端在8888端口监听....");
        //2. 等待连接
        Socket socket = serverSocket.accept();
        //3. 读取客户端发送的数据
        //   通过Socket得到输入流
        BufferedInputStream bis = new BufferedInputStream(socket.getInputStream());
        byte[] bytes = StreamUtils.streamToByteArray(bis);
        //4. 将得到 bytes 数组，写入到指定的路径，就得到一个文件了
        String destFilePath = "src\\abc.mp4";
        BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(destFilePath));
        bos.write(bytes);
        bos.close();
        // 向客户端回复 "收到图片"
        // 通过socket 获取到输出流(字符)
        BufferedWriter writer = new BufferedWriter(new OutputStreamWriter(socket.getOutputStream()));
        writer.write("收到图片");
        writer.flush();//把内容刷新到数据通道
        socket.shutdownOutput();//设置写入结束标记
        //关闭其他资源
        writer.close();
        bis.close();
        socket.close();
        serverSocket.close();
    }
}
```

StreamUtils.java

```
ackage com.hspedu.upload;
import java.io.BufferedReader;
import java.io.ByteArrayOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
/**
 * 此类用于演示关于流的读写方法
 */
public class StreamUtils {
	/**
	 * 功能：将输入流转换成byte[]
	 * @param is
	 * @return
	 * @throws Exception
	 */
	public static byte[] streamToByteArray(InputStream is) throws Exception{
		ByteArrayOutputStream bos = new ByteArrayOutputStream();//创建输出流对象
		byte[] b = new byte[1024];
		int len;
		while((len=is.read(b))!=-1){
			bos.write(b, 0, len);	
		}
		byte[] array = bos.toByteArray();
		bos.close();
		return array;
	}
	/**
	 * 功能：将InputStream转换成String
	 * @param is
	 * @return
	 * @throws Exception
	 */
	public static String streamToString(InputStream is) throws Exception{
		BufferedReader reader = new BufferedReader(new InputStreamReader(is));
		StringBuilder builder= new StringBuilder();
		String line;
		while((line=reader.readLine())!=null){ //当读取到 null时，就表示结束
			builder.append(line+"\r\n");
		}
		return builder.toString();
	}
}
```

21.4.6 netstat 指令  
![](https://img-blog.csdnimg.cn/7f17f50fc7be46dab53a12071e32ae79.png)  
21.4.7 TCP 网络通讯不为人知的秘密  
![](https://img-blog.csdnimg.cn/d40feeb2cd5e410c83c5acfcfbbd5fd9.png)  
21.5 UDP 网络通信编程

21.5.1 基本介绍  
![](https://img-blog.csdnimg.cn/5f2dbeaae1c54f359c769d3122f0edb4.png)  
21.5.2 基本流程  
![](https://img-blog.csdnimg.cn/161c8ef5b28640228b0eed4940fc45c1.png)  
![](https://img-blog.csdnimg.cn/868727800a5a4f3597c1eb22cfd11dcb.png)

#### 第 23 章 反射 (reflection)

23.1 一个需求引出反射  
![](https://img-blog.csdnimg.cn/2298c9d148574f24b81cb458d7af1ba6.png)  
Cat.java

```
package com.hspedu;
public class Cat {
    private String name = "招财猫";
    public int age = 10; //public的
    public Cat() {} //无参构造器
    public Cat(String name) {
        this.name = name;
    }
    public void hi() { //常用方法
        //System.out.println("hi " + name);
    }
    public void cry() { //常用方法
        System.out.println(name + " 喵喵叫..");
    }
}
```

re.properties

```
classfullpath=com.hspedu.Cat
method=cry
```

ReflectionQuestion.java

```
package com.hspedu.reflection.question;
import com.hspedu.Cat;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.lang.reflect.Constructor;
import java.lang.reflect.Field;
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;
import java.util.Properties;
/**
 * 反射问题的引入
 */
@SuppressWarnings({"all"})
public class ReflectionQuestion {
    public static void main(String[] args) throws IOException, ClassNotFoundException, IllegalAccessException, InstantiationException, NoSuchMethodException, InvocationTargetException, NoSuchFieldException {
        //根据配置文件 re.properties 指定信息, 创建Cat对象并调用方法hi
        //老韩回忆
        //传统的方式 new 对象 -》 调用方法
//        Cat cat = new Cat();
//        cat.hi(); ===> cat.cry() 修改源码.

        //我们尝试做一做 -> 明白反射
        //1. 使用Properties 类, 可以读写配置文件
        Properties properties = new Properties();
        properties.load(new FileInputStream("src\\re.properties"));
        String classfullpath = properties.get("classfullpath").toString();//"com.hspedu.Cat"
        String methodName = properties.get("method").toString();//"hi"
        System.out.println("classfullpath=" + classfullpath);
        System.out.println("method=" + methodName);

        //2. 创建对象 , 传统的方法，行不通 =》 反射机制
        //new classfullpath();

        //3. 使用反射机制解决
        //(1) 加载类, 返回Class类型的对象cls
        Class cls = Class.forName(classfullpath);
        //(2) 通过 cls 得到你加载的类 com.hspedu.Cat 的对象实例
        Object o = cls.newInstance();
        System.out.println("o的运行类型=" + o.getClass()); //运行类型
        //(3) 通过 cls 得到你加载的类 com.hspedu.Cat 的 methodName"hi"  的方法对象
        //    即：在反射中，可以把方法视为对象（万物皆对象）
        Method method1 = cls.getMethod(methodName);
        //(4) 通过method1 调用方法: 即通过方法对象来实现调用方法
        System.out.println("=============================");
        method1.invoke(o); //传统方法 对象.方法() , 反射机制 方法.invoke(对象)
    }
}
```

23.2 反射机制

23.2.1 Java Reflection  
![](https://img-blog.csdnimg.cn/d0db06b147af4d35af671888ba256873.png)

23.2.2 Java 反射机制原理示意图!!!  
![](https://img-blog.csdnimg.cn/3f2f52c1e29b43f6a5c9058bac495d9b.png)  
![](https://img-blog.csdnimg.cn/646b1f9ea7e5485991cc15fa6e315c6c.png)  
23.2.4 反射相关的主要类  
![](https://img-blog.csdnimg.cn/bd54241461c2468c955ec04f51e40a59.png)  
Cat.java

```
package com.hspedu;
public class Cat {
    private String name = "招财猫";
    public int age = 10; //public的
    public Cat() {} //无参构造器
    public Cat(String name) {
        this.name = name;
    }
    public void hi() { //常用方法
        //System.out.println("hi " + name);
    }
    public void cry() { //常用方法
        System.out.println(name + " 喵喵叫..");
    }
}
```

Reflection01.java

```
package com.hspedu.reflection;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.lang.reflect.Constructor;
import java.lang.reflect.Field;
import java.lang.reflect.Method;
import java.util.Properties;
public class Reflection01 {
    public static void main(String[] args) throws Exception {
        //1. 使用Properties 类, 可以读写配置文件
        Properties properties = new Properties();
        properties.load(new FileInputStream("src\\re.properties"));
        String classfullpath = properties.get("classfullpath").toString();//"com.hspedu.Cat"
        String methodName = properties.get("method").toString();//"hi"

        //2. 使用反射机制解决
        //(1) 加载类, 返回Class类型的对象cls
        Class cls = Class.forName(classfullpath);
        //(2) 通过 cls 得到你加载的类 com.hspedu.Cat 的对象实例
        Object o = cls.newInstance();
        System.out.println("o的运行类型=" + o.getClass()); //运行类型
        //(3) 通过 cls 得到你加载的类 com.hspedu.Cat 的 methodName"hi"  的方法对象
        //    即：在反射中，可以把方法视为对象（万物皆对象）
        Method method1 = cls.getMethod(methodName);
        //(4) 通过method1 调用方法: 即通过方法对象来实现调用方法
        System.out.println("=============================");
        method1.invoke(o); //传统方法 对象.方法() , 反射机制 方法.invoke(对象)

        //java.lang.reflect.Field: 代表类的成员变量, Field对象表示某个类的成员变量
        //得到name字段
        //getField不能得到私有的属性
        Field nameField = cls.getField("age"); //
        System.out.println(nameField.get(o)); // 传统写法 对象.成员变量 , 反射 :  成员变量对象.get(对象)

        //java.lang.reflect.Constructor: 代表类的构造方法, Constructor对象表示构造器
        Constructor constructor = cls.getConstructor(); //()中可以指定构造器参数类型, 返回无参构造器
        System.out.println(constructor);//Cat()

        Constructor constructor2 = cls.getConstructor(String.class); //这里老师传入的 String.class 就是String类的Class对象
        System.out.println(constructor2);//Cat(String name)
    }
}
```

23.2.5 反射优点和缺点  
![](https://img-blog.csdnimg.cn/bfcbe02b0c364bc8a312aa50de01e338.png)  
23.2.6 反射调用优化 - 关闭访问检查  
![](https://img-blog.csdnimg.cn/db23f97f46d440b689fd9e6735c2aeb1.png)  
23.3 Class 类

23.3.1 基本介绍  
![](https://img-blog.csdnimg.cn/bbf3086d27314f53806fb5b6425d4334.png)  
![](https://img-blog.csdnimg.cn/2210fe1b670640149acf202f8276ed69.png)  
![](https://img-blog.csdnimg.cn/1cb27333486845008d37e29d8b5b7193.png)

```
package com.hspedu.reflection.class_;
import com.hspedu.Cat;
import java.util.ArrayList;
/**
 * 对Class类特点的梳理
 */
public class Class01 {
    public static void main(String[] args) throws ClassNotFoundException {
        //看看Class类图
        //1. Class也是类，因此也继承Object类
        //2. Class类对象不是new出来的，而是系统创建的
        //(1) 传统new对象
        /*  ClassLoader类
            public Class<?> loadClass(String name) throws ClassNotFoundException {
                return loadClass(name, false);
            }
         */
        //Cat cat = new Cat();
        //(2) 反射方式, 刚才老师没有debug到 ClassLoader类的 loadClass, 原因是，我没有注销Cat cat = new Cat();
        /*
            ClassLoader类, 仍然是通过 ClassLoader类加载Cat类的 Class对象
            public Class<?> loadClass(String name) throws ClassNotFoundException {
                return loadClass(name, false);
            }
         */
        Class cls1 = Class.forName("com.hspedu.Cat");

        //3. 对于某个类的Class类对象，在内存中只有一份，因为类只加载一次
        Class cls2 = Class.forName("com.hspedu.Cat");
        System.out.println(cls1.hashCode());
        System.out.println(cls2.hashCode());
        Class cls3 = Class.forName("com.hspedu.Dog");
        System.out.println(cls3.hashCode());
    }
}
```

23.3.2 Class 类的常用方法  
![](https://img-blog.csdnimg.cn/d0c554801ba843e8b9f3479a3510d3b5.png)  
![](https://img-blog.csdnimg.cn/126ee5311a714a249998f539152cae72.png)  
Car.java

```
package com.hspedu;
public class Car {
    public String brand = "宝马";//品牌
    public int price = 500000;
    public String color = "白色";
    @Override
    public String toString() {
        return "Car{" +
                "brand='" + brand + '\'' +
                ", price=" + price +
                ", color='" + color + '\'' +
                '}';
    }
}
```

Class02.java

```
package com.hspedu.reflection.class_;
import com.hspedu.Car;
import java.lang.reflect.Field;
/**
 * 演示Class类的常用方法
 */
public class Class02 {
    public static void main(String[] args) throws ClassNotFoundException, IllegalAccessException, InstantiationException, NoSuchFieldException {
        String classAllPath = "com.hspedu.Car";
        //1 . 获取到Car类 对应的 Class对象
        //<?> 表示不确定的Java类型
        Class<?> cls = Class.forName(classAllPath);
        //2. 输出cls
        System.out.println(cls); //显示cls对象, 是哪个类的Class对象 com.hspedu.Car
        System.out.println(cls.getClass());//输出cls运行类型 java.lang.Class
        //3. 得到包名
        System.out.println(cls.getPackage().getName());//包名 com.hspedu
        //4. 得到全类名
        System.out.println(cls.getName());//com.hspedu.Car
        //5. 通过cls创建对象实例
        Car car = (Car) cls.newInstance();
        System.out.println(car);//car.toString()
        //6. 通过反射获取属性 brand
        Field brand = cls.getField("brand");
        System.out.println(brand.get(car));//宝马
        //7. 通过反射给属性赋值
        brand.set(car, "奔驰");
        System.out.println(brand.get(car));//奔驰
        //8 我希望大家可以得到所有的属性(字段)
        System.out.println("=======所有的字段属性====");
        Field[] fields = cls.getFields();
        for (Field f : fields) {
            System.out.println(f.getName());//名称
        }
    }
}
```

23.4 获取 Class 类对象  
![](https://img-blog.csdnimg.cn/3518c648d14b45fd9b5bd1819cabb696.png)  
![](https://img-blog.csdnimg.cn/c6e6e6f9448d4907a0f7afbd18e0b2aa.png)  
![](https://img-blog.csdnimg.cn/368a0d431d214aeda0391509f0c085e6.png)  
![](https://img-blog.csdnimg.cn/c7ed532ce17643e4a53a14d41ddb8f35.png)

```
package com.hspedu.reflection.class_;
import com.hspedu.Car;
/**
 * 演示得到Class对象的各种方式(6)
 */
public class GetClass_ {
    public static void main(String[] args) throws ClassNotFoundException {
        //1. Class.forName
        String classAllPath = "com.hspedu.Car"; //通过读取配置文件获取
        Class<?> cls1 = Class.forName(classAllPath);
        System.out.println(cls1);

        //2. 类名.class , 应用场景: 用于参数传递
        Class cls2 = Car.class;
        System.out.println(cls2);

        //3. 对象.getClass(), 应用场景，有对象实例
        Car car = new Car();
        Class cls3 = car.getClass();
        System.out.println(cls3);

        //4. 通过类加载器【4种】来获取到类的Class对象
        //(1)先得到类加载器 car
        ClassLoader classLoader = car.getClass().getClassLoader();
        //(2)通过类加载器得到Class对象
        Class cls4 = classLoader.loadClass(classAllPath);
        System.out.println(cls4);

        //cls1 , cls2 , cls3 , cls4 其实是同一个对象
        System.out.println(cls1.hashCode());
        System.out.println(cls2.hashCode());
        System.out.println(cls3.hashCode());
        System.out.println(cls4.hashCode());

        //5. 基本数据(int, char,boolean,float,double,byte,long,short) 按如下方式得到Class类对象
        Class<Integer> integerClass = int.class;
        Class<Character> characterClass = char.class;
        Class<Boolean> booleanClass = boolean.class;
        System.out.println(integerClass);//int

        //6. 基本数据类型对应的包装类，可以通过 .TYPE 得到Class类对象
        Class<Integer> type1 = Integer.TYPE;
        Class<Character> type2 = Character.TYPE; //其它包装类BOOLEAN, DOUBLE, LONG,BYTE等待
        System.out.println(type1);

        System.out.println(integerClass.hashCode());//
        System.out.println(type1.hashCode());//两者是一样的
    }
}
```

23.5 哪些类型有 Class 对象  
![](https://img-blog.csdnimg.cn/f31fa282f65c4a7193553161b0736b41.png)

```
package com.hspedu.reflection.class_;
import java.io.Serializable;
/**
 * 演示哪些类型有Class对象
 */
public class AllTypeClass {
    public static void main(String[] args) {
        Class<String> cls1 = String.class;//外部类
        Class<Serializable> cls2 = Serializable.class;//接口
        Class<Integer[]> cls3 = Integer[].class;//数组
        Class<float[][]> cls4 = float[][].class;//二维数组
        Class<Deprecated> cls5 = Deprecated.class;//注解
        //枚举
        Class<Thread.State> cls6 = Thread.State.class;
        Class<Long> cls7 = long.class;//基本数据类型
        Class<Void> cls8 = void.class;//void数据类型
        Class<Class> cls9 = Class.class;//

        System.out.println(cls1);
        System.out.println(cls2);
        System.out.println(cls3);
        System.out.println(cls4);
        System.out.println(cls5);
        System.out.println(cls6);
        System.out.println(cls7);
        System.out.println(cls8);
        System.out.println(cls9);
    }
}
```

输出：  
![](https://img-blog.csdnimg.cn/e70f915b2ede4169aea6421bef6ded13.png)  
23.6 类加载

23.6.1 基本说明和类加载时机  
![](https://img-blog.csdnimg.cn/17418a99ac9142d99101a1ebaab97f7d.png)  
![](https://img-blog.csdnimg.cn/095ad6850c6b44fcb86fda98ab99ec52.png)  
23.6.3 类加载过程图  
![](https://img-blog.csdnimg.cn/18d2710356c34b7cb2eca76d5ade24c3.png)  
23.6.4 类加载各阶段完成任务  
![](https://img-blog.csdnimg.cn/d00f039c53e44ed785bd877c9b801eec.png)  
23.6.5 加载阶段  
![](https://img-blog.csdnimg.cn/f250a80b917d4b4984289d3783928424.png)  
23.6.6 连接阶段 - 验证  
![](https://img-blog.csdnimg.cn/53f9bddeecee4781a078406673c72b53.png)  
23.6.7 连接阶段 - 准备  
![](https://img-blog.csdnimg.cn/374701357c7d449e9656faf681d973b5.png)

```
package com.hspedu.reflection.classload_;
/**
 * 我们说明一个类加载的链接阶段-准备
 */
public class ClassLoad02 {
    public static void main(String[] args) {}
}
class A {
    //属性-成员变量-字段
    //老韩分析类加载的链接阶段-准备 属性是如何处理
    //1. n1 是实例属性, 不是静态变量，因此在准备阶段，是不会分配内存
    //2. n2 是静态变量，分配内存 n2 是默认初始化 0 ,而不是20
    //3. n3 是static final 是常量, 他和静态变量不一样, 因为一旦赋值就不变 n3 = 30
    public int n1 = 10;
    public static  int n2 = 20;
    public static final  int n3 = 30;
}
```

23.6.8 连接阶段 - 解析  
![](https://img-blog.csdnimg.cn/3fdbcf0ee71048e3a00d318b4a98e748.png)  
23.6.9 Initialization（初始化)  
![](https://img-blog.csdnimg.cn/7c05720a536741c9b641bfda295c8b17.png)

```
package com.hspedu.reflection.classload_;
/**
 * 演示类加载-初始化阶段
 */
public class ClassLoad03 {
    public static void main(String[] args) throws ClassNotFoundException {
        //老韩分析
        //1. 加载B类，并生成 B的class对象
        //2. 链接 num = 0
        //3. 初始化阶段
        //    依次自动收集类中的所有静态变量的赋值动作和静态代码块中的语句,并合并
        /*
                clinit() {
                    System.out.println("B 静态代码块被执行");
                    //num = 300;
                    num = 100;
                }
                合并: num = 100

         */
        //new B();//类加载
        //System.out.println(B.num);//100, 如果直接使用类的静态属性，也会导致类的加载
        //看看加载类的时候，是有同步机制控制
        /*
        protected Class<?> loadClass(String name, boolean resolve)
        throws ClassNotFoundException
        {
            //正因为有这个机制，才能保证某个类在内存中, 只有一份Class对象
            synchronized (getClassLoadingLock(name)) {
            //....
            }
            }
         */
        B b = new B();
    }
}
class B {
    static {
        System.out.println("B 静态代码块被执行");
        num = 300;
    }
    static int num = 100;
    public B() {//构造器
        System.out.println("B() 构造器被执行");
    }
}
```

23.7 通过反射获取类的结构信息

23.7.1 第一组: java.lang.Class 类  
![](https://img-blog.csdnimg.cn/9ced9596eabe45a1ad8b3ec2c7972b2d.png)  
23.7.2 第二组: java.lang.reflect.Field 类  
![](https://img-blog.csdnimg.cn/4c1f42a8a30c4649bd876d68a5dfd83d.png)  
23.7.3 第三组: java.lang.reflect.Method 类  
![](https://img-blog.csdnimg.cn/8c7f40f20a9f49698a05439325db2737.png)  
23.7.4 第四组: java.lang.reflect.Constructor 类  
![](https://img-blog.csdnimg.cn/954b66db52b548d4981c26f119b247ab.png)

```
package com.hspedu.reflection;
import org.junit.jupiter.api.Test;
import java.lang.annotation.Annotation;
import java.lang.reflect.Constructor;
import java.lang.reflect.Field;
import java.lang.reflect.Method;
/**
 * 演示如何通过反射获取类的结构信息
 */
public class ReflectionUtils {
    public static void main(String[] args) {}
    @Test
    public void api_02() throws ClassNotFoundException, NoSuchMethodException {
        //得到Class对象
        Class<?> personCls = Class.forName("com.hspedu.reflection.Person");
        //getDeclaredFields:获取本类中所有属性
        //规定 说明: 默认修饰符 是0 ， public  是1 ，private 是 2 ，protected 是 4 , static 是 8 ，final 是 16
        Field[] declaredFields = personCls.getDeclaredFields();
        for (Field declaredField : declaredFields) {
            System.out.println("本类中所有属性=" + declaredField.getName()
                    + " 该属性的修饰符值=" + declaredField.getModifiers()
                    + " 该属性的类型=" + declaredField.getType());
        }
        
        //getDeclaredMethods:获取本类中所有方法
        Method[] declaredMethods = personCls.getDeclaredMethods();
        for (Method declaredMethod : declaredMethods) {
            System.out.println("本类中所有方法=" + declaredMethod.getName()
                    + " 该方法的访问修饰符值=" + declaredMethod.getModifiers()
                    + " 该方法返回类型" + declaredMethod.getReturnType());

            //输出当前这个方法的形参数组情况
            Class<?>[] parameterTypes = declaredMethod.getParameterTypes();
            for (Class<?> parameterType : parameterTypes) {
                System.out.println("该方法的形参类型=" + parameterType);
            }
        }

        //getDeclaredConstructors:获取本类中所有构造器
        Constructor<?>[] declaredConstructors = personCls.getDeclaredConstructors();
        for (Constructor<?> declaredConstructor : declaredConstructors) {
            System.out.println("====================");
            System.out.println("本类中所有构造器=" + declaredConstructor.getName());//这里老师只是输出名

            Class<?>[] parameterTypes = declaredConstructor.getParameterTypes();
            for (Class<?> parameterType : parameterTypes) {
                System.out.println("该构造器的形参类型=" + parameterType);
            }
        }
    }

    //第一组方法API
    @Test
    public void api_01() throws ClassNotFoundException, NoSuchMethodException {
        //得到Class对象
        Class<?> personCls = Class.forName("com.hspedu.reflection.Person");
        //getName:获取全类名
        System.out.println(personCls.getName());//com.hspedu.reflection.Person
        //getSimpleName:获取简单类名
        System.out.println(personCls.getSimpleName());//Person
        //getFields:获取所有public修饰的属性，包含本类以及父类的
        Field[] fields = personCls.getFields();
        for (Field field : fields) {//增强for
            System.out.println("本类以及父类的属性=" + field.getName());
        }
        //getDeclaredFields:获取本类中所有属性
        Field[] declaredFields = personCls.getDeclaredFields();
        for (Field declaredField : declaredFields) {
            System.out.println("本类中所有属性=" + declaredField.getName());
        }
        //getMethods:获取所有public修饰的方法，包含本类以及父类的
        Method[] methods = personCls.getMethods();
        for (Method method : methods) {
            System.out.println("本类以及父类的方法=" + method.getName());
        }
        //getDeclaredMethods:获取本类中所有方法
        Method[] declaredMethods = personCls.getDeclaredMethods();
        for (Method declaredMethod : declaredMethods) {
            System.out.println("本类中所有方法=" + declaredMethod.getName());
        }
        //getConstructors: 获取所有public修饰的构造器，包含本类
        Constructor<?>[] constructors = personCls.getConstructors();
        for (Constructor<?> constructor : constructors) {
            System.out.println("本类的构造器=" + constructor.getName());
        }
        //getDeclaredConstructors:获取本类中所有构造器
        Constructor<?>[] declaredConstructors = personCls.getDeclaredConstructors();
        for (Constructor<?> declaredConstructor : declaredConstructors) {
            System.out.println("本类中所有构造器=" + declaredConstructor.getName());//这里老师只是输出名
        }
        //getPackage:以Package形式返回 包信息
        System.out.println(personCls.getPackage());//com.hspedu.reflection
        //getSuperClass:以Class形式返回父类信息
        Class<?> superclass = personCls.getSuperclass();
        System.out.println("父类的class对象=" + superclass);//
        //getInterfaces:以Class[]形式返回接口信息
        Class<?>[] interfaces = personCls.getInterfaces();
        for (Class<?> anInterface : interfaces) {
            System.out.println("接口信息=" + anInterface);
        }
        //getAnnotations:以Annotation[] 形式返回注解信息
        Annotation[] annotations = personCls.getAnnotations();
        for (Annotation annotation : annotations) {
            System.out.println("注解信息=" + annotation);//注解
        }
    }
}
class A {
    public String hobby;
    public void hi() {}
    public A() {}
    public A(String name) {}
}
interface IA {}
interface IB {}
@Deprecated
class Person extends A implements IA, IB {
    //属性
    public String name;
    protected static int age; // 4 + 8 = 12
    String job;
    private double sal;
    //构造器
    public Person() {}
    public Person(String name) {}
    //私有的
    private Person(String name, int age) {}
    //方法
    public void m1(String name, int age, double sal) {}
    protected String m2() {
        return null;
    }
    void m3() {}
    private void m4() {}
}
```

#### 第 24 章 零基础学 MySQL

24.2 解决之道

24.2.3 使用命令行窗口连接 MYSQL 数据库  
![](https://img-blog.csdnimg.cn/6cbd52b5dee44aa8a658e5088e18d46a.png)  
24.2.4 操作示意图  
![](https://img-blog.csdnimg.cn/cad48cbb3f5b4c599488be4649bddd8f.png)  
24.5 数据库三层结构 - 破除 MySQL 神秘  
![](https://img-blog.csdnimg.cn/54258e6f779d499fabe8a2b49e1070c4.png)  
![](https://img-blog.csdnimg.cn/295a5cec78164333818d7b4d56810415.png)  
24.6 数据在数据库中的存储方式  
![](https://img-blog.csdnimg.cn/4172620e7dc2489c8b11e8b86b177e3b.png)  
24.7 SQL 语句分类  
![](https://img-blog.csdnimg.cn/ad67c2576f194226bdc76ed5782c5d0a.png)  
24.8 创建数据库  
![](https://img-blog.csdnimg.cn/e67ba121e25449aebd41f221592de4ad.png)

```
# 演示数据库的操作
#创建一个名称为hsp_db01的数据库。[图形化和指令 演示]
#使用指令创建数据库
CREATE DATABASE hsp_db01;
#删除数据库指令
DROP DATABASE hsp_db01
#创建一个使用utf8字符集的hsp_db02数据库
CREATE DATABASE hsp_db02 CHARACTER SET utf8
#创建一个使用utf8字符集，并带校对规则的hsp_db03数据库
CREATE DATABASE hsp_db03 CHARACTER SET utf8 COLLATE utf8_bin
#校对规则 utf8_bin 区分大小 默认utf8_general_ci 不区分大小写

#下面是一条查询的sql , select 查询 * 表示所有字段 FROM 从哪个表
#WHERE 从哪个字段 NAME = 'tom' 查询名字是tom
SELECT *  FROM t1 WHERE NAME = 'tom'
```

24.9 查看、删除数据库  
![](https://img-blog.csdnimg.cn/b2506c3012f046298f8669ae307fdc55.png)

```
#演示删除和查询数据库
#查看当前数据库服务器中的所有数据库
SHOW DATABASES
#查看前面创建的hsp_db01数据库的定义信息
SHOW CREATE DATABASE `hsp_db01`
#老师说明 在创建数据库,表的时候，为了规避关键字，可以使用反引号解决

#删除前面创建的hsp_db01数据库
DROP DATABASE hsp_db01
```

反引号是 esc 下面那个键

24.10 备份恢复数据库  
![](https://img-blog.csdnimg.cn/3fa0eec59ce145389aaa649f669863c9.png)

```
#练习 : database03.sql 备份hsp_db02 和 hsp_db03 库中的数据，并恢复

#备份, 要在Dos下执行mysqldump指令其实在mysql安装目录\bin
#这个备份的文件，就是对应的sql语句
mysqldump -u root -p -B hsp_db02 hsp_db03 > d:\\bak.sql

DROP DATABASE ecshop;

#恢复数据库(注意：进入Mysql命令行再执行)
source d:\\bak.sql
#第二个恢复方法， 直接将bak.sql的内容放到查询编辑器中，执行
```

24.11 备份恢复数据库的表  
![](https://img-blog.csdnimg.cn/b67854faafd748eb9bcf856eb83271c9.png)  
24.12 练习  
![](https://img-blog.csdnimg.cn/c7d8edacc8e24c788bbb1c8bedb49c4c.png)

```
#这是一个ecshop 的数据库，包括ecshop 所有的表，请导入到mysql数据库中[备份]
#进入到mysql命令行: source ecshop备份文件路径 
#再将ecshop整个数据库备份到你的 d:\\ecshop.sql到dos 下 : 
mysqldump -u root -p -B ecshop > d:\\ecshop.sql
#将mysql的ecshop数据库删除, 并通过备份的d:\\ecshop.sql恢复
#进入mysql命令行
source d:\\ecshop.sql
```

24.13 创建表  
![](https://img-blog.csdnimg.cn/b0123ede22214387b9e11da439692f2b.png)

```
#指令创建表
#注意：hsp_db02创建表时，要根据需保存的数据创建相应的列，并根据数据的类型定义相应的列类型。例：user表 (快速入门案例 create_tab01.sql )
#id        	整形               [图形化，指令]                
#name 		字符串
#password 	字符串
#birthday 	日期
CREATE TABLE `user` (
	id INT, 
	`name` VARCHAR(255),
	`password` VARCHAR(255), 
	`birthday` DATE)
	CHARACTER SET utf8 COLLATE utf8_bin ENGINE INNODB;
```

24.14 Mysql 常用数据类型 (列类型)  
![](https://img-blog.csdnimg.cn/34d126a381d74f1c8e250705521ba272.png)  
![](https://img-blog.csdnimg.cn/ee51d0fccd4c4fe2b261662752943007.png)  
![](https://img-blog.csdnimg.cn/ce0d78ed076b49049dc0e7c29c2307a5.png)

24.14.1 数值型 (整数) 的基本使用  
![](https://img-blog.csdnimg.cn/26de5e52f8f742a2b0ee175371d92cc7.png)  
![](https://img-blog.csdnimg.cn/826a3af8a6d8415a9e1b90713b7daa57.png)

```
#演示整型的使用
#老韩使用tinyint 来演示范围 有符号 -128 ~ 127  如果没有符号 0-255
#说明： 表的字符集，校验规则, 存储引擎，老师使用默认
#1. 如果没有指定 unsinged , 则TINYINT就是有符号
#2. 如果指定 unsinged , 则TINYINT就是无符号 0-255
CREATE TABLE t3 (
	id TINYINT);
CREATE TABLE t4 (
	id TINYINT UNSIGNED);
	
INSERT INTO t3 VALUES(127); #这是非常简单的添加语句
SELECT * FROM t3

INSERT INTO t4 VALUES(255);
SELECT * FROM t4;
```

24.14.3 数值型 (bit) 的使用  
![](https://img-blog.csdnimg.cn/992ae072107a4087b3675d2bec6980ab.png)

```
#演示bit类型使用
#说明
#1. bit(m) m 在 1-64
#2. 添加数据 范围 按照你给的位数来确定，比如m = 8 表示一个字节 0~255
#3. 显示按照bit 
#4. 查询时，仍然可以按照数来查询
CREATE TABLE t05 (num BIT(8));
INSERT INTO t05 VALUES(255); 
SELECT * FROM t05;
SELECT * FROM t05 WHERE num = 1;
```

24.14.4 数值型 (小数) 的基本使用  
![](https://img-blog.csdnimg.cn/52b76b808efe48b1b8266fc5aadb6f73.png)

```
#演示decimal类型、float、double使用

#创建表
CREATE TABLE t06 (
	num1 FLOAT,
	num2 DOUBLE,
	num3 DECIMAL(30,20));
#添加数据
INSERT INTO t06 VALUES(88.12345678912345, 88.12345678912345,88.12345678912345);
SELECT * FROM t06;

#decimal可以存放很大的数
CREATE TABLE t07 (
	num DECIMAL(65));
INSERT INTO t07 VALUES(8999999933338388388383838838383009338388383838383838383);
```

输出：  
![](https://img-blog.csdnimg.cn/ef01c4864ab4471c96edfb012d624157.png)  
24.14.5 字符串的基本使用  
![](https://img-blog.csdnimg.cn/81e07fa325b0470fab292cde98eaecd3.png)

```
#演示字符串类型使用char varchar
#注释的快捷键 shift+ctrl+c , 注销注释 shift+ctrl+r
-- CHAR(size)
-- 固定长度字符串 最大255 字符 
-- VARCHAR(size)    0~65535字节
-- 可变长度字符串 最大65532字节  【utf8编码最大21844字符 1-3个字节用于记录大小】
-- 如果表的编码是 utf8 varchar(size) size = (65535-3) / 3 = 21844
-- 如果表的编码是 gbk varchar(size) size = (65535-3) / 2 = 32766
CREATE TABLE t09 (
	`name` CHAR(255));

CREATE TABLE t10 (
	`name` VARCHAR(32766)) CHARSET gbk;
```

24.14.6 字符串使用细节  
![](https://img-blog.csdnimg.cn/6e2d61f5bd74404d953886d0ac34eee9.png)  
![](https://img-blog.csdnimg.cn/6c97d977e0f04e068ed80db3e3dfadb9.png)  
![](https://img-blog.csdnimg.cn/c524187ffd4b4b5d98176f8fe62b67e5.png)  
![](https://img-blog.csdnimg.cn/b418ab3ba75e418ab8c9cb0a8439ac92.png)

```
#演示字符串类型的使用细节
#char(4) 和 varchar(4) 这个4表示的是字符，而不是字节, 不区分字符是汉字还是字母
CREATE TABLE t11(
	`name` CHAR(4));
INSERT INTO t11 VALUES('韩顺平好');

SELECT * FROM t11;

CREATE TABLE t12(
	`name` VARCHAR(4));
INSERT INTO t12 VALUES('韩顺平好');
INSERT INTO t12 VALUES('ab北京');
SELECT * FROM t12;

#如果varchar 不够用，可以考试使用mediumtext 或者longtext, 
#如果想简单点，可以使用直接使用text
CREATE TABLE t13( content TEXT, content2 MEDIUMTEXT , content3 LONGTEXT);
INSERT INTO t13 VALUES('韩顺平教育', '韩顺平教育100', '韩顺平教育1000~~');
SELECT * FROM t13;
```

最后一行输出：  
![](https://img-blog.csdnimg.cn/abd9dd1a7db8437f8fd5fb735abb1056.png)  
24.14.7 日期类型的基本使用  
![](https://img-blog.csdnimg.cn/5f3bbc06e0664fd8a2d58ceb5478c55a.png)

```
#演示时间相关的类型
#创建一张表, date , datetime , timestamp
CREATE TABLE t14 (
	birthday DATE , -- 生日
	job_time DATETIME, -- 记录年月日 时分秒
	login_time TIMESTAMP 
		NOT NULL DEFAULT CURRENT_TIMESTAMP 
		ON UPDATE CURRENT_TIMESTAMP); -- 登录时间, 如果希望login_time列自动更新, 需要配置
		
SELECT * FROM t14;
INSERT INTO t14(birthday, job_time) 
	VALUES('2022-11-11','2022-11-11 10:10:10');
-- 如果我们更新 t14表的某条记录，login_time列会自动的以当前时间进行更新
```

24.16 修改表  
![](https://img-blog.csdnimg.cn/004f29eb71fe48d1aab3a0802b77c286.png)  
![](https://img-blog.csdnimg.cn/3cf70fa530374d91a9533aa998721651.png)

```
#修改表的操作练习
--  员工表emp的上增加一个image列，varchar类型(要求在resume后面)。
ALTER TABLE emp 
	ADD image VARCHAR(32) NOT NULL DEFAULT '' 
	AFTER RESUME
DESC employee -- 显示表结构，可以查看表的所有列
--  修改job列，使其长度为60。
ALTER TABLE emp 
	MODIFY job VARCHAR(60) NOT NULL DEFAULT ''
--  删除sex列。
ALTER TABLE emp
	DROP sex
--  表名改为employee。
RENAME TABLE emp TO employee
--  修改表的字符集为utf8 
ALTER TABLE employee CHARACTER SET utf8
--  列名name修改为user_name
ALTER TABLE employee 
	CHANGE `name` `user_name` VARCHAR(64) NOT NULL DEFAULT ''
DESC employee
```

24.18 数据库 C[create]R[read]U[update]D[delete] 语句  
![](https://img-blog.csdnimg.cn/65b8b50481ea4a149dd3d67e5a65a3ee.png)  
24.19 Insert 语句  
![](https://img-blog.csdnimg.cn/c396e3753feb40788b772af5ccd0065a.png)

```
#练习insert 语句
-- 创建一张商品表goods (id  int , goods_name varchar(10), price double );
-- 添加2条记录
CREATE TABLE `goods` (
	id INT ,
	goods_name VARCHAR(10), -- 长度10
	price DOUBLE NOT NULL DEFAULT 100 );
-- 添加数据
INSERT INTO `goods` (id, goods_name, price) 
	VALUES(10, '华为手机', 2000);
INSERT INTO `goods` (id, goods_name, price) 
	VALUES(20, '苹果手机', 3000);
SELECT * FROM goods;

CREATE TABLE `goods2` (
	id INT ,
	goods_name VARCHAR(10), -- 长度10
	price DOUBLE NOT NULL DEFAULT 100 );
```

24.19.3 Insert 细节说明  
![](https://img-blog.csdnimg.cn/60ce8fbfa4f44a958e9f59d35383c2cd.png)

```
#说明insert 语句的细节
-- 1.插入的数据应与字段的数据类型相同。
--       比如 把 'abc' 添加到 int 类型会错误
INSERT INTO `goods` (id, goods_name, price) 
	VALUES('韩顺平', '小米手机', 2000);
-- 2. 数据的长度应在列的规定范围内，例如：不能将一个长度为80的字符串加入到长度为40的列中。
INSERT INTO `goods` (id, goods_name, price) 
	VALUES(40, 'vovo手机vovo手机vovo手机vovo手机vovo手机', 3000);
-- 3. 在values中列出的数据位置必须与被加入的列的排列位置相对应。
INSERT INTO `goods` (id, goods_name, price)  -- 不对
	VALUES('vovo手机',40, 2000);
-- 4. 字符和日期型数据应包含在单引号中。
INSERT INTO `goods` (id, goods_name, price) 
	VALUES(40, vovo手机, 3000); -- 错误的 vovo手机 应该 'vovo手机'
-- 5. 列可以插入空值[前提是该字段允许为空]，insert into table value(null)
INSERT INTO `goods` (id, goods_name, price) 
	VALUES(40, 'vovo手机', NULL);
-- 6. insert into tab_name (列名..)  values (),(),()  形式添加多条记录
INSERT INTO `goods` (id, goods_name, price) 
	VALUES(50, '三星手机', 2300),(60, '海尔手机', 1800);
-- 7. 如果是给表中的所有字段添加数据，可以不写前面的字段名称
INSERT INTO `goods`   
	VALUES(70, 'IBM手机', 5000);
-- 8. 默认值的使用，当不给某个字段值时，如果有默认值就会添加默认值，否则报错
      -- 如果某个列 没有指定 not null ,那么当添加数据时，没有给定值，则会默认给null
      -- 如果我们希望指定某个列的默认值，可以在创建表时指定
INSERT INTO `goods` (id, goods_name)   
	VALUES(80, '格力手机');

SELECT * FROM goods;
```

24.20 update 语句  
![](https://img-blog.csdnimg.cn/5ba014100b604fcb82b62ddea0399fc6.png)

```
-- 演示update语句
-- 要求: 在上面创建的employee表中修改表中的纪录
-- 1. 将所有员工薪水修改为5000元。[如果没有带where 条件，会修改所有的记录，因此要小心]
UPDATE employee SET salary = 5000 
-- 2. 将姓名为 小妖怪 的员工薪水修改为3000元。
UPDATE employee 
	SET salary = 3000 
	WHERE user_name = '小妖怪' 
-- 3. 将 老妖怪 的薪水在原有基础上增加1000元
INSERT INTO employee 
	VALUES(200, '老妖怪', '1990-11-11', '2000-11-11 10:10:10', '捶背的', 5000, '给大王捶背', 'd:\\a.jpg');

UPDATE employee 
	SET salary = salary + 1000 
	WHERE user_name = '老妖怪' 

-- 可以修改多个列的值
UPDATE employee 
	SET salary = salary + 1000 , job = '出主意的'
	WHERE user_name = '老妖怪' 
SELECT * FROM employee;
```

![](https://img-blog.csdnimg.cn/00cee578dc044c48a248f84ddf830341.png)  
24.21 delete 语句  
![](https://img-blog.csdnimg.cn/ada4ec8d5020427884781baa2ddb4115.png)  
![](https://img-blog.csdnimg.cn/fca55396227441d684f85a2a36e1ca01.png)

```
-- delete 语句演示

--  删除表中名称为’老妖怪’的记录。
DELETE FROM employee 
	WHERE user_name = '老妖怪';
--  删除表中所有记录, 老师提醒，一定要小心
DELETE FROM employee;

-- Delete语句不能删除某一列的值（可使用update 设为 null 或者 ''）
UPDATE employee SET job = '' WHERE user_name = '老妖怪';

SELECT * FROM employee

-- 要删除这个表
DROP TABLE employee;
```

24.22 select 语句  
![](https://img-blog.csdnimg.cn/9078c5a2f7ad44f3b1e332bb8df2140c.png)  
![](https://img-blog.csdnimg.cn/40c169d2a9b24092a7632d6aab236b54.png)

```
-- select 语句【重点 难点】
CREATE TABLE student(
	id INT NOT NULL DEFAULT 1,
	NAME VARCHAR(20) NOT NULL DEFAULT '',
	chinese FLOAT NOT NULL DEFAULT 0.0,
	english FLOAT NOT NULL DEFAULT 0.0,
	math FLOAT NOT NULL DEFAULT 0.0
);

INSERT INTO student(id,NAME,chinese,english,math) VALUES(1,'韩顺平',89,78,90);
INSERT INTO student(id,NAME,chinese,english,math) VALUES(2,'张飞',67,98,56);
INSERT INTO student(id,NAME,chinese,english,math) VALUES(3,'宋江',87,78,77);
INSERT INTO student(id,NAME,chinese,english,math) VALUES(4,'关羽',88,98,90);
INSERT INTO student(id,NAME,chinese,english,math) VALUES(5,'赵云',82,84,67);
INSERT INTO student(id,NAME,chinese,english,math) VALUES(6,'欧阳锋',55,85,45);
INSERT INTO student(id,NAME,chinese,english,math) VALUES(7,'黄蓉',75,65,30);
INSERT INTO student(id,NAME,chinese,english,math) VALUES(8,'韩信',45,65,99);

SELECT * FROM student;

-- 查询表中所有学生的信息。
SELECT * FROM student;
-- 查询表中所有学生的姓名和对应的英语成绩。
SELECT `name`,english FROM student;
-- 过滤表中重复数据 distinct 。
SELECT DISTINCT english FROM student;
-- 要查询的记录，每个字段都相同，才会去重
SELECT DISTINCT `name`, english FROM student;
```

24.22.4 使用表达式对查询的列进行运算  
![](https://img-blog.csdnimg.cn/b5eaef0d29d844bbbd2c77dc890b7f29.png)  
![](https://img-blog.csdnimg.cn/03498217f67c46e7aa27604de2ae363c.png)

```
-- select 语句的使用

-- 统计每个学生的总分
SELECT `name`, (chinese+english+math) FROM student;
-- 在所有学生总分加10分的情况
SELECT `name`, (chinese + english + math + 10) FROM student;
-- 使用别名表示学生分数。
SELECT `name` AS '名字', (chinese + english + math + 10) AS total_score 
	FROM student;
```

24.22.7 在 where 子句中经常使用的运算符  
![](https://img-blog.csdnimg.cn/fd63f12f49e64e9a92a514241746a17e.png)  
![](https://img-blog.csdnimg.cn/27c824acc5ee4958b8bbbbd207dbebc9.png)  
![](https://img-blog.csdnimg.cn/3000440ecb5c406fbab220bec2e2daa8.png)

```
-- select 语句
-- 查询姓名为赵云的学生成绩
SELECT * FROM student 
	WHERE `name` = '赵云'
-- 查询英语成绩大于90分的同学
SELECT * FROM student 
	WHERE english > 90
-- 查询总分大于200分的所有同学

SELECT * FROM student 
	WHERE (chinese + english + math) > 200
	
-- 查询math大于60 并且(and) id大于4的学生成绩
SELECT * FROM student
	WHERE math >60 AND id > 4
-- 查询英语成绩大于语文成绩的同学
SELECT * FROM student
	WHERE english > chinese
-- 查询总分大于200分 并且 数学成绩小于语文成绩,的姓赵的学生.
-- 赵% 表示 名字以韩开头的就可以
SELECT * FROM student
	WHERE (chinese + english + math) > 200 AND 
		math < chinese AND `name` LIKE '赵%'
-- 查询英语分数在 80－90之间的同学。
SELECT * FROM student
	WHERE english >= 80 AND english <= 90;
SELECT * FROM student
	WHERE english BETWEEN 80 AND 90; -- between .. and .. 是 闭区间
-- 查询数学分数为89,90,91的同学。
SELECT * FROM student 
	WHERE math = 89 OR math = 90 OR math = 91;
SELECT * FROM student 
	WHERE math IN (89, 90, 91);
-- 查询所有姓李的学生成绩。
SELECT * FROM student 
	WHERE `name` LIKE '韩%'
-- 查询数学分>80，语文分>80的同学
```

24.22.10 使用 order by 子句排序查询结果  
![](https://img-blog.csdnimg.cn/1de0b4e2ae2b4dfdb7153f116361d6c8.png)

```
-- 演示order by使用
-- 对数学成绩排序后输出【升序】。
SELECT * FROM student 
	ORDER BY math;
-- 对总分按从高到低的顺序输出 [降序] -- 使用别名排序
SELECT `name` , (chinese + english + math) AS total_score FROM student 
	ORDER BY total_score DESC;
-- 对姓韩的学生成绩[总分]排序输出(升序) where + order by
SELECT `name`, (chinese + english + math) AS total_score FROM student
	WHERE `name` LIKE '韩%'
	ORDER BY total_score;
SELECT * FROM student
	WHERE `name` LIKE '韩%'
	ORDER BY (chinese + english + math);
```

最后一种查询方式也可以，结果如图所示，但建议用上一种：  
![](https://img-blog.csdnimg.cn/72d6a4b7f508492ab8247266afc6d483.png)  
24.23 合计 / 统计函数

24.23.1 count  
![](https://img-blog.csdnimg.cn/d4374dc4f02f4d1280939c85d8624444.png)

```
-- 演示mysql的统计函数的使用
-- 统计一个班级共有多少学生？
SELECT COUNT(*) FROM student;
-- 统计数学成绩大于90的学生有多少个？
SELECT COUNT(*) FROM student
	WHERE math > 90
-- 统计总分大于250的人数有多少？
SELECT COUNT(*) FROM student
	WHERE (math + english + chinese) > 250
-- count(*) 和 count(列) 的区别 
-- 解释 :count(*) 返回满足条件的记录的行数
-- count(列): 统计满足条件的某列有多少个，但是会排除 为null的情况
CREATE TABLE t15 (
	`name` VARCHAR(20));
INSERT INTO t15 VALUES('tom');
INSERT INTO t15 VALUES('jack');
INSERT INTO t15 VALUES('mary');
INSERT INTO t15 VALUES(NULL);
SELECT * FROM t15;

SELECT COUNT(*) FROM t15; -- 4
SELECT COUNT(`name`) FROM t15;-- 3
```

24.23.2 sum  
![](https://img-blog.csdnimg.cn/6615214ec66d487fb78133ffa63ea94d.png)

```
-- 演示sum函数的使用
-- 统计一个班级数学总成绩？
SELECT SUM(math) FROM student;
-- 统计一个班级语文、英语、数学各科的总成绩
SELECT SUM(math) AS math_total_score,SUM(english),SUM(chinese) FROM student;
-- 统计一个班级语文、英语、数学的成绩总和
SELECT SUM(math + english + chinese) FROM student;
-- 统计一个班级语文成绩平均分
SELECT SUM(chinese)/ COUNT(*)  FROM student;
SELECT SUM(`name`) FROM student;
```

24.23.3 avg  
![](https://img-blog.csdnimg.cn/647ac946fa024b16a358d2ee4a9800b2.png)

```
-- 演示avg的使用
-- 练习：
-- 求一个班级数学平均分？
SELECT AVG(math) FROM student;
-- 求一个班级总分平均分
SELECT AVG(math + english + chinese) FROM student;
```

24.23.4 max/min  
![](https://img-blog.csdnimg.cn/8f11371cab20454bb56687ae96e3be26.png)

```
-- 演示max 和 min的使用
-- 求班级最高分和最低分（数值范围在统计中特别有用）
SELECT MAX(math + english + chinese), MIN(math + english + chinese) 
	FROM student;

-- 求出班级数学最高分和最低分
SELECT MAX(math) AS math_high_socre, MIN(math)  AS math_low_socre
	FROM student;
```

24.23.5 使用 group by 子句对列进行分组  
![](https://img-blog.csdnimg.cn/04ef69719eb54065ac841f9bba795a59.png)

```
# 演示group by + having
GROUP by用于对查询的结果分组统计
-- having子句用于限制分组显示结果.
-- ?如何显示每个部门的平均工资和最高工资
-- 老韩分析: avg(sal) max(sal)
-- 按照部分来分组查询
SELECT AVG(sal), MAX(sal) , deptno 
	FROM  emp GROUP BY deptno; 
-- 使用数学方法，对小数点进行处理
SELECT FORMAT(AVG(sal),2), MAX(sal) , deptno 
	FROM  emp GROUP BY deptno; 

-- ?显示每个部门的每种岗位的平均工资和最低工资
-- 老师分析 1. 显示每个部门的平均工资和最低工资
--          2. 显示每个部门的每种岗位的平均工资和最低工资
SELECT AVG(sal), MIN(sal) , deptno, job 
	FROM  emp GROUP BY deptno, job; 

-- ?显示平均工资低于2000的部门号和它的平均工资 // 别名

-- 老师分析 [写sql语句的思路是化繁为简,各个击破]
-- 1. 显示各个部门的平均工资和部门号
-- 2. 在1的结果基础上，进行过滤，保留 AVG(sal) < 2000
-- 3. 使用别名进行过滤 

SELECT AVG(sal), deptno 
	FROM emp GROUP BY deptno
		HAVING AVG(sal) < 2000;
-- 使用别名		
SELECT AVG(sal) AS avg_sal, deptno 
	FROM emp GROUP BY deptno
		HAVING avg_sal < 2000;	--这个效率会更高
```

having 不可以用 where 代替，WHERE 是对表中的原始数据进行过滤。

24.24 字符串相关函数  
![](https://img-blog.csdnimg.cn/cfba38dd05414f469975e7b52ee75eec.png)

```
-- 演示字符串相关函数的使用  ， 使用emp表来演示
-- CHARSET(str)	返回字串字符集
SELECT CHARSET(ename) FROM emp;
-- CONCAT (string2  [,... ])	连接字串, 将多个列拼接成一列
SELECT CONCAT(ename, ' 工作是 ', job) FROM emp;

-- INSTR (string ,substring )	返回substring在string中出现的位置,没有返回0
-- dual 亚元表, 系统表 可以作为测试表使用
SELECT INSTR('hanshunping', 'ping') FROM DUAL; 

-- UCASE (string2 )	转换成大写
SELECT UCASE(ename) FROM emp;

-- LCASE (string2 )	转换成小写

SELECT LCASE(ename) FROM emp;
-- LEFT (string2 ,length )	从string2中的左边起取length个字符
-- RIGHT (string2 ,length )	从string2中的右边起取length个字符
SELECT LEFT(ename, 2) FROM emp;

-- LENGTH (string )	string长度[按照字节]
SELECT LENGTH(ename) FROM emp;
-- REPLACE (str ,search_str ,replace_str ) 	
-- 在str中用replace_str替换search_str
-- 如果是manager 就替换成 经理
SELECT ename, REPLACE(job,'MANAGER', '经理')  FROM emp;

-- STRCMP (string1 ,string2 )	逐字符比较两字串大小
SELECT STRCMP('hsp', 'hsp') FROM DUAL;
-- SUBSTRING (str , position  [,length ])	
-- 从str的position开始【从1开始计算】,取length个字符
-- 从ename 列的第一个位置开始取出2个字符
SELECT SUBSTRING(ename, 1, 2) FROM emp;

-- LTRIM (string2 ) RTRIM (string2 )  TRIM(string)
-- 去除前端空格或后端空格
SELECT LTRIM('  韩顺平教育') FROM DUAL;
SELECT RTRIM('韩顺平教育   ') FROM DUAL;
SELECT TRIM('    韩顺平教育   ') FROM DUAL;

-- 练习: 以首字母小写的方式显示所有员工emp表的姓名
-- 方法1 
-- 思路先取出ename 的第一个字符，转成小写的
-- 把他和后面的字符串进行拼接输出即可

SELECT CONCAT(LCASE(SUBSTRING(ename,1,1)),  SUBSTRING(ename,2)) AS new_name
	FROM emp;  

SELECT CONCAT(LCASE(LEFT(ename,1)),  SUBSTRING(ename,2)) AS new_name
	FROM emp;
```

![](https://img-blog.csdnimg.cn/b5341f7daed24495a78a4e45c58739e4.png)  
24.25 数学相关函数  
![](https://img-blog.csdnimg.cn/4db74297597641398973cfef2ea76d7c.png)

```
-- 演示数学相关函数

-- ABS(num)	绝对值
SELECT ABS(-10) FROM DUAL;
-- BIN (decimal_number )十进制转二进制
SELECT BIN(10) FROM DUAL;
-- CEILING (number2 )	向上取整, 得到比num2 大的最小整数
SELECT CEILING(-1.1) FROM DUAL;

-- CONV(number2,from_base,to_base)	进制转换
-- 下面的含义是 8 是十进制的8, 转成 2进制输出
SELECT CONV(8, 10, 2) FROM DUAL;
-- 下面的含义是 8 是16进制的8, 转成 2进制输出
SELECT CONV(16, 16, 10) FROM DUAL;

-- FLOOR (number2 )	向下取整,得到比 num2 小的最大整数
SELECT FLOOR(-1.1) FROM DUAL;

-- FORMAT (number,decimal_places )	保留小数位数(四舍五入)
SELECT FORMAT(78.125458,2) FROM DUAL;

-- HEX (DecimalNumber )	转十六进制

-- LEAST (number , number2  [,..])	求最小值
SELECT LEAST(0,1, -10, 4) FROM DUAL;
-- MOD (numerator ,denominator )	求余
SELECT MOD(10, 3) FROM DUAL;

-- RAND([seed])	RAND([seed]) 返回随机数 其范围为 0 ≤ v ≤ 1.0
-- 老韩说明
-- 1. 如果使用 rand() 每次返回不同的随机数 ，在 0 ≤ v ≤ 1.0
-- 2. 如果使用 rand(seed) 返回随机数, 范围 0 ≤ v ≤ 1.0, 如果seed不变，
--    该随机数也不变了
SELECT RAND() FROM DUAL;

SELECT CURRENT_TIMESTAMP() FROM DUAL;
```

24.26 时间日期相关函数  
![](https://img-blog.csdnimg.cn/2db92edf954546db89a48837e7997165.png)

```
-- 日期时间相关函数

-- CURRENT_DATE (  )	当前日期
SELECT CURRENT_DATE() FROM DUAL;
-- CURRENT_TIME (  )	当前时间
SELECT CURRENT_TIME()  FROM DUAL;
-- CURRENT_TIMESTAMP (  ) 当前时间戳
SELECT CURRENT_TIMESTAMP()  FROM DUAL;
```

![](https://img-blog.csdnimg.cn/2c1e8ffb48484cc2a7c7f228a2a5aa23.png)

```
-- 创建测试表 信息表
CREATE TABLE mes(
	id INT , 
	content VARCHAR(30), 
	send_time DATETIME);
	
-- 添加一条记录
INSERT INTO mes 
	VALUES(1, '北京新闻', CURRENT_TIMESTAMP()); 
INSERT INTO mes VALUES(2, '上海新闻', NOW());
INSERT INTO mes VALUES(3, '广州新闻', NOW());

SELECT * FROM mes;
SELECT NOW() FROM DUAL;
```

![](https://img-blog.csdnimg.cn/55a48da34ec04df2b96d3cdfff3822c3.png)

```
-- 上应用实例
-- 显示所有新闻信息，发布日期只显示 日期，不用显示时间.
SELECT id, content, DATE(send_time) 
	FROM mes;
-- 请查询在10分钟内发布的新闻, 思路一定要梳理一下.
SELECT * 
	FROM mes
	WHERE DATE_ADD(send_time, INTERVAL 10 MINUTE) >= NOW()

SELECT * 
	FROM mes
	WHERE send_time >= DATE_SUB(NOW(), INTERVAL 10 MINUTE) 

-- 请在mysql 的sql语句中求出 2011-11-11 和 1990-1-1 相差多少天
SELECT DATEDIFF('2011-11-11', '1990-01-01') FROM DUAL;
-- 请用mysql 的sql语句求出你活了多少天? [练习] 1986-11-11 出生
SELECT DATEDIFF(NOW(), '1986-11-11') FROM DUAL;
-- 如果你能活80岁，求出你还能活多少天.[练习] 1986-11-11 出生
-- 先求出活80岁 时, 是什么日期 X
-- 然后在使用 datediff(x, now()); 1986-11-11->datetime
```

![](https://img-blog.csdnimg.cn/af36977e26544d468d811975617c8931.png)

```
-- INTERVAL 80 YEAR ： YEAR 可以是 年月日，时分秒
-- '1986-11-11' 可以date,datetime timestamp 
SELECT DATEDIFF(DATE_ADD('1986-11-11', INTERVAL 80 YEAR), NOW()) 
	FROM DUAL;
	
SELECT TIMEDIFF('10:11:11', '06:10:10') FROM DUAL;
```

![](https://img-blog.csdnimg.cn/828afef6e8fe41218305d77dadb89efb.png)  
![](https://img-blog.csdnimg.cn/ffe5eb220e1d48aa96892b3cfa708177.png)

```
-- YEAR|Month|DAY| DATE (datetime )
SELECT YEAR(NOW()) FROM DUAL;
SELECT MONTH(NOW()) FROM DUAL;
SELECT DAY(NOW()) FROM DUAL;
SELECT MONTH('2013-11-10') FROM DUAL;
-- unix_timestamp() : 返回的是1970-1-1 到现在的秒数
SELECT UNIX_TIMESTAMP() FROM DUAL;
-- FROM_UNIXTIME() : 可以把一个unix_timestamp 秒数[时间戳]，转成指定格式的日期
-- %Y-%m-%d 格式是规定好的，表示年月日
-- 意义：在开发中，可以存放一个整数，然后表示时间，通过FROM_UNIXTIME转换
--   
SELECT FROM_UNIXTIME(1618483484, '%Y-%m-%d') FROM DUAL;
SELECT FROM_UNIXTIME(1618483100, '%Y-%m-%d %H:%i:%s') FROM DUAL;
```

24.27 加密和系统函数  
![](https://img-blog.csdnimg.cn/af8e00e97cfe43bb9da08040c31171f7.png)

```
-- 演示加密函数和系统函数

-- USER()	查询用户
-- 可以查看登录到mysql的有哪些用户，以及登录的IP
SELECT USER() FROM DUAL; -- 用户@IP地址
-- DATABASE()	查询当前使用数据库名称
SELECT DATABASE();

-- MD5(str)	为字符串算出一个 MD5 32的字符串，常用(用户密码)加密
-- root 密码是 hsp -> 加密md5 -> 在数据库中存放的是加密后的密码
SELECT MD5('hsp') FROM DUAL;
SELECT LENGTH(MD5('hsp')) FROM DUAL;

-- 演示用户表，存放密码时，是md5
CREATE TABLE hsp_user
	(id INT , 
	`name` VARCHAR(32) NOT NULL DEFAULT '', 
	pwd CHAR(32) NOT NULL DEFAULT '');
INSERT INTO hsp_user 
	VALUES(100, '韩顺平', MD5('hsp'));
SELECT * FROM hsp_user;

SELECT * FROM hsp_user
	WHERE `name`='韩顺平' AND pwd = MD5('hsp')  

-- PASSWORD(str) -- 加密函数, MySQL数据库的用户密码就是 PASSWORD函数加密

SELECT PASSWORD('hsp') FROM DUAL; -- 数据库的 *81220D972A52D4C51BB1C37518A2613706220DAC

-- select * from mysql.user \G 	从原文密码str 计算并返回密码字符串
-- 通常用于对mysql数据库的用户密码加密
-- mysql.user 表示 数据库.表 
SELECT * FROM mysql.user
```

24.28 流程控制函数  
![](https://img-blog.csdnimg.cn/23ae215d58344e49a32ad3246330a222.png)

```
# 演示流程控制语句

# IF(expr1,expr2,expr3)	如果expr1为True ,则返回 expr2 否则返回 expr3
SELECT IF(TRUE, '北京', '上海') FROM DUAL;
# IFNULL(expr1,expr2)	如果expr1不为空NULL,则返回expr1,否则返回expr2
SELECT IFNULL( NULL, '韩顺平教育') FROM DUAL;
# SELECT CASE WHEN expr1 THEN expr2 WHEN expr3 THEN expr4 ELSE expr5 END; [类似多重分支.]
# 如果expr1 为TRUE,则返回expr2,如果expr2 为t, 返回 expr4, 否则返回 expr5

SELECT CASE 
	WHEN TRUE THEN 'jack'  -- jack
	WHEN FALSE THEN 'tom' 
	ELSE 'mary' END

-- 1. 查询emp 表, 如果 comm 是null , 则显示0.0
--    老师说明，判断是否为null 要使用 is null, 判断不为空 使用 is not
SELECT ename, IF(comm IS NULL , 0.0, comm)
	FROM emp;
SELECT ename, IFNULL(comm, 0.0)
	FROM emp;
-- 2. 如果emp 表的 job 是 CLERK 则显示 职员， 如果是 MANAGER 则显示经理
--     如果是 SALESMAN 则显示 销售人员，其它正常显示

SELECT ename, (SELECT CASE 
		WHEN job = 'CLERK' THEN '职员' 
		WHEN job = 'MANAGER' THEN '经理'
		WHEN job = 'SALESMAN' THEN '销售人员' 
		ELSE job END) AS 'job'	--本质上是case语句，可以把AS 'job' 移到case后面
	FROM emp;
```

不能用 replace 函数代替，replace 是对表进行操作，会修改表，if 函数只是展示。

24.29 mysql 表查询–加强  
![](https://img-blog.csdnimg.cn/85dffac63b0a474492ffc02d8e257264.png)  
![](https://img-blog.csdnimg.cn/29e6445acdf249bd9417e17e45151588.png)

```
-- 查询加强
-- ■ 使用where子句
-- 	?如何查找1992.1.1后入职的员工
-- 老师说明： 在mysql中,日期类型可以直接比较, 需要注意格式
SELECT * FROM emp
	WHERE hiredate > '1992-01-01'
-- ■ 如何使用like操作符(模糊)
-- 	%: 表示0到多个任意字符 _: 表示单个任意字符
-- 	?如何显示首字符为S的员工姓名和工资
SELECT ename, sal FROM emp
	WHERE ename LIKE 'S%'
-- 	?如何显示第三个字符为大写O的所有员工的姓名和工资
SELECT ename, sal FROM emp
	WHERE ename LIKE '__O%'

-- ■ 如何显示没有上级的雇员的情况
SELECT * FROM emp
	WHERE mgr IS NULL;
-- ■ 查询表结构 
DESC emp 

-- 使用order by子句
--   ?如何按照工资的从低到高的顺序[升序]，显示雇员的信息
SELECT * FROM emp
	ORDER BY sal 
--   ?按照部门号升序而雇员的工资降序排列 , 显示雇员信息

SELECT * FROM emp
	ORDER BY deptno ASC , sal DESC;
```

24.29.2 分页查询  
![](https://img-blog.csdnimg.cn/6bda5237f12d4967814e39a29b96deeb.png)

```
-- 分页查询
-- 按雇员的id号升序取出， 每页显示3条记录，请分别显示 第1页，第2页，第3页

-- 第1页
SELECT * FROM emp 
	ORDER BY empno 
	LIMIT 0, 3;
-- 第2页
SELECT * FROM emp 
	ORDER BY empno 
	LIMIT 3, 3;
-- 第3页
SELECT * FROM emp 
	ORDER BY empno 
	LIMIT 6, 3;
-- 推导一个公式 
SELECT * FROM emp
	ORDER BY empno 
	LIMIT 每页显示记录数 * (第几页-1) , 每页显示记录数
	
-- 测试
SELECT job, COUNT(*) FROM emp GROUP BY  job;
-- 显示雇员总数，以及获得补助的雇员数
SELECT COUNT(*) FROM emp  WHERE mgr IS NOT NULL;
SELECT MAX(sal) - MIN(sal) FROM emp;
```

24.29.3 使用分组函数和分组子句 group by  
![](https://img-blog.csdnimg.cn/b6d22f394dbe417cb5e5dc562f484554.png)

```
-- 增强group by 的使用

-- (1) 显示每种岗位的雇员总数、平均工资。
SELECT COUNT(*), AVG(sal), job 
	FROM emp 
	GROUP BY job; 
-- (2) 显示雇员总数，以及获得补助的雇员数。
--  思路: 获得补助的雇员数 就是 comm 列为非null的个数。如果count(列)的值为null, 是不会统计, SQL 非常灵活，需要我们动脑筋.
SELECT COUNT(*), COUNT(comm)
	FROM emp 

--  老师的扩展要求：统计没有获得补助的雇员数
SELECT COUNT(*), COUNT(IF(comm IS NULL, 1, NULL))
	FROM emp 

SELECT COUNT(*), COUNT(*) - COUNT(comm)
	FROM emp 

-- (3) 显示管理者的总人数。小技巧:尝试写->修改->尝试[正确的]
SELECT COUNT(DISTINCT mgr) 
	FROM emp; 

-- (4) 显示雇员工资的最大差额。
-- 思路： max(sal) - min(sal)
SELECT MAX(sal) - MIN(sal) 
	FROM emp;
```

24.29.4 数据分组的总结  
![](https://img-blog.csdnimg.cn/35dd75651bf84d7f90902e72b42fdecc.png)

```
-- 应用案例：请统计各个部门group by 的平均工资 avg，
-- 并且是大于1000的 having，并且按照平均工资从高到低排序， order by
-- 取出前两行记录 limit 0, 2

SELECT deptno, AVG(sal) AS avg_sal
	FROM emp
	GROUP BY deptno
	HAVING  avg_sal > 1000
	ORDER BY avg_sal DESC
	LIMIT 0,2
```

24.30 mysql 多表查询  
![](https://img-blog.csdnimg.cn/876edc379bc54febaef4d2a65f0f569f.png)  
![](https://img-blog.csdnimg.cn/306153f120254370b71c5f6850b84182.png)

```
-- 多表查询
-- ?显示雇员名,雇员工资及所在部门的名字 【笛卡尔集】
/*
	老韩分析
	1. 雇员名,雇员工资 来自 emp表
	2. 部门的名字 来自 dept表
	3. 需要对 emp 和 dept查询  ename,sal,dname,deptno
	4. 当我们需要指定显示某个表的列时，需要 表.列表
*/
SELECT ename,sal,dname,emp.deptno
	FROM emp, dept 
	WHERE emp.deptno = dept.deptno
	
select * from emp;
select * from dept;
select * from salgrade;
-- 老韩小技巧：多表查询的条件不能少于 表的个数-1, 否则会出现笛卡尔集
-- ?如何显示部门号为10的部门名、员工名和工资 
SELECT ename,sal,dname,emp.deptno
	FROM emp, dept 
	WHERE emp.deptno = dept.deptno and emp.deptno = 10

-- ?显示各个员工的姓名，工资，及其工资的级别

-- 思路 姓名，工资 来自 emp 13
--      工资级别 salgrade 5
-- 写sql , 先写一个简单，然后加入过滤条件...
select ename, sal, grade 
	from emp , salgrade
	where sal between losal and hisal;
```

24.30.4 自连接  
![](https://img-blog.csdnimg.cn/9df1ad1888cd4e5a9bf6023db4f1fdb5.png)

```
-- 多表查询的 自连接

-- 思考题: 显示公司员工名字和他的上级的名字

-- 老韩分析： 员工名字 在emp, 上级的名字的名字 emp
-- 员工和上级是通过 emp表的 mgr 列关联
-- 这里老师小结：
-- 自连接的特点 1. 把同一张表当做两张表使用
--               2. 需要给表取别名 表名  表别名 
--		 3. 列名不明确，可以指定列的别名 列名 as 列的别名		
SELECT worker.ename AS '职员名' ,  boss.ename AS '上级名'
	FROM emp worker, emp boss
	WHERE worker.mgr = boss.empno;
SELECT * FROM emp;
```

24.31 mysql 表子查询  
![](https://img-blog.csdnimg.cn/fccaf9cb3ce0480ab7b597a14b365563.png)

```
-- 子查询的演示
-- 请思考：如何显示与SMITH同一部门的所有员工?
/*
	1. 先查询到 SMITH的部门号得到
	2. 把上面的select 语句当做一个子查询来使用
*/
SELECT deptno 
	FROM emp 
	WHERE ename = 'SMITH'

-- 下面的答案.	
SELECT * 
	FROM emp
	WHERE deptno = (
		SELECT deptno 
		FROM emp 
		WHERE ename = 'SMITH'
	)

-- 课堂练习:如何查询和部门10的工作相同的雇员的
-- 名字、岗位、工资、部门号, 但是不含10号部门自己的雇员.
/*
	1. 查询到10号部门有哪些工作
	2. 把上面查询的结果当做子查询使用
*/
select distinct job 
	from emp 
	where deptno = 10;
	
--  下面语句完整
select ename, job, sal, deptno
	from emp
	where job in (
		SELECT DISTINCT job 
		FROM emp 
		WHERE deptno = 10
	) and deptno <> 10 	-- != 和 <> 一样都是不等于号
```

24.31.5 子查询当做临时表使用  
![](https://img-blog.csdnimg.cn/fdbf342925304cc59ffbf40bcb7d27b4.png)

```
-- 查询ecshop中各个类别中，价格最高的商品

-- 查询 商品表
-- 先得到 各个类别中，价格最高的商品 max + group by cat_id, 当做临时表
-- 把子查询当做一张临时表可以解决很多很多复杂的查询

select cat_id , max(shop_price) 
	from ecs_goods
	group by cat_id
	
-- 这个最后答案	
select goods_id, ecs_goods.cat_id, goods_name, shop_price 
	from (
		SELECT cat_id , MAX(shop_price) as max_price
		FROM ecs_goods
		GROUP BY cat_id
	) temp , ecs_goods
	where  temp.cat_id = ecs_goods.cat_id 
	and temp.max_price = ecs_goods.shop_price
```

24.31.6 在多行子查询中使用 all 操作符  
![](https://img-blog.csdnimg.cn/ccd9e88dbce040b4a3812a963dd4161c.png)

```
-- all的使用
-- 请思考:显示工资比部门30的所有员工的工资高的员工的姓名、工资和部门号
SELECT ename, sal, deptno
	FROM emp
	WHERE sal > ALL(
		SELECT sal 
			FROM emp
			WHERE deptno = 30
		) 
-- 可以这样写
SELECT ename, sal, deptno
	FROM emp
	WHERE sal > (
		SELECT MAX(sal) 
			FROM emp
			WHERE deptno = 30
		)
```

24.31.7 在多行子查询中使用 any 操作符  
![](https://img-blog.csdnimg.cn/335763121b664d5b9a93ccd4e9a17a6b.png)

```
-- any的使用
-- 请思考:如何显示工资比部门30的其中一个员工的工资高的员工的姓名、工资和部门号
SELECT ename, sal, deptno
	FROM emp
	WHERE sal > any(
		SELECT sal 
			FROM emp
			WHERE deptno = 30
		)
 SELECT ename, sal, deptno
	FROM emp
	WHERE sal > (
		SELECT min(sal) 
			FROM emp
			WHERE deptno = 30
		)
```

24.31.8 多列子查询  
![](https://img-blog.csdnimg.cn/6e1fb8789308438080e8e4ac2f298180.png)

```
-- 多列子查询
-- 请思考如何查询与allen的部门和岗位完全相同的所有雇员(并且不含allen本人)
-- (字段1， 字段2 ...) = (select 字段 1，字段2 from 。。。。)

-- 分析: 1. 得到smith的部门和岗位
SELECT deptno , job
	FROM emp 
	WHERE ename = 'ALLEN'
	
-- 分析: 2  把上面的查询当做子查询来使用，并且使用多列子查询的语法进行匹配
SELECT * 
	FROM emp
	WHERE (deptno , job) = (
		SELECT deptno , job
		FROM emp 
		WHERE ename = 'ALLEN'
	) AND ename != 'ALLEN'

-- 请查询 和宋江数学，英语，语文   
-- 成绩 完全相同的学生
SELECT * 
	FROM student
	WHERE (math, english, chinese) = (
		SELECT math, english, chinese
		FROM student
		WHERE `name` = '宋江'
	)
```

24.31.9 子查询练习

```
-- 子查询练习
-- 请思考：查找每个部门工资高于本部门平均工资的人的资料
-- 这里要用到数据查询的小技巧，把一个子查询当作一个临时表使用
-- 1. 先得到每个部门的 部门号和 对应的平均工资

SELECT deptno, AVG(sal) AS avg_sal
	FROM emp GROUP BY deptno
	
-- 2. 把上面的结果当做子查询, 和 emp 进行多表查询
SELECT ename, sal, temp.avg_sal, emp.deptno
	FROM emp, (
		SELECT deptno, AVG(sal) AS avg_sal
		FROM emp 
		GROUP BY deptno
	) temp 
	where emp.deptno = temp.deptno and emp.sal > temp.avg_sal
	
-- 查找每个部门工资最高的人的详细资料
SELECT ename, sal, temp.max_sal, emp.deptno
	FROM emp, (
		SELECT deptno, max(sal) AS max_sal
		FROM emp 
		GROUP BY deptno
	) temp 
	WHERE emp.deptno = temp.deptno AND emp.sal = temp.max_sal
	

-- 查询每个部门的信息(包括：部门名,编号,地址)和人员数量,我们一起完成。
-- 1. 部门名,编号,地址 来自 dept表
-- 2. 各个部门的人员数量 -》 构建一个临时表
select count(*), deptno 
	from emp
	group by deptno;
	
select dname, dept.deptno, loc , tmp.per_num as '人数'
	from dept, (
		SELECT COUNT(*) as per_num, deptno 
		FROM emp
		GROUP BY deptno
	) tmp 
	where tmp.deptno = dept.deptno

-- 还有一种写法 表.* 表示将该表所有列都显示出来, 可以简化sql语句
-- 在多表查询中，当多个表的列不重复时，才可以直接写列名
SELECT tmp.* , dname, loc
	FROM dept, (
		SELECT COUNT(*) AS per_num, deptno 
		FROM emp
		GROUP BY deptno
	) tmp 
	WHERE tmp.deptno = dept.deptno
```

24.32 表复制  
![](https://img-blog.csdnimg.cn/d682285c463b4310afc71bf6fb9b1020.png)

```
-- 表的复制
-- 为了对某个sql语句进行效率测试，我们需要海量数据时，可以使用此法为表创建海量数据
CREATE TABLE my_tab01 
	( id INT,
	  `name` VARCHAR(32),
	  sal DOUBLE,
	  job VARCHAR(32),
	  deptno INT);
DESC my_tab01
SELECT * FROM my_tab01;

-- 演示如何自我复制
-- 1. 先把emp 表的记录复制到 my_tab01
INSERT INTO my_tab01 
	(id, `name`, sal, job,deptno)
	SELECT empno, ename, sal, job, deptno FROM emp;
-- 2. 自我复制
INSERT INTO my_tab01
	SELECT * FROM my_tab01;
SELECT COUNT(*) FROM my_tab01;

-- 如何删除掉一张表重复记录
-- 1. 先创建一张表 my_tab02, 
-- 2. 让 my_tab02 有重复的记录
CREATE TABLE my_tab02 LIKE emp; -- 这个语句 把emp表的结构(列)，复制到my_tab02
desc my_tab02;

insert into my_tab02
	select * from emp;
select * from my_tab02;
-- 3. 考虑去重 my_tab02的记录
/*
	思路 
	(1) 先创建一张临时表 my_tmp , 该表的结构和 my_tab02一样
	(2) 把my_tmp 的记录 通过 distinct 关键字 处理后 把记录复制到 my_tmp
	(3) 清除掉 my_tab02 记录
	(4) 把 my_tmp 表的记录复制到 my_tab02
	(5) drop 掉 临时表my_tmp
*/
-- (1) 先创建一张临时表 my_tmp , 该表的结构和 my_tab02一样
create table my_tmp like my_tab02
-- (2) 把my_tmp 的记录 通过 distinct 关键字 处理后 把记录复制到 my_tmp
insert into my_tmp 
	select distinct * from my_tab02;
-- (3) 清除掉 my_tab02 记录
delete from my_tab02;
-- (4) 把 my_tmp 表的记录复制到 my_tab02
insert into my_tab02
	select * from my_tmp;
-- (5) drop 掉 临时表my_tmp
drop table my_tmp;

select * from my_tab02;
```

24.33 合并查询  
![](https://img-blog.csdnimg.cn/2f500290a55c4ab08896434673e11a2d.png)  
![](https://img-blog.csdnimg.cn/245a07f482484c2bb62b6451469c7cda.png)

```
-- 合并查询
SELECT ename,sal,job FROM emp WHERE sal>2500 -- 5

SELECT ename,sal,job FROM emp WHERE job='MANAGER' -- 3

-- union all 就是将两个查询结果合并，不会去重
SELECT ename,sal,job FROM emp WHERE sal>2500
UNION ALL
SELECT ename,sal,job FROM emp WHERE job='MANAGER'

-- union  就是将两个查询结果合并，会去重
SELECT ename,sal,job FROM emp WHERE sal>2500
UNION 
SELECT ename,sal,job FROM emp WHERE job='MANAGER'
```

24.34 mysql 表外连接  
![](https://img-blog.csdnimg.cn/c8f4dfcbd95743eda47279edbc2cbb44.png)  
![](https://img-blog.csdnimg.cn/98cac4aa2135408f90e25c2a6d3bbcea.png)  
![](https://img-blog.csdnimg.cn/4897d497678c430ba687ffd3f74aa076.png)  
![](https://img-blog.csdnimg.cn/a41e79e3936546a7b73d485df701f1db.png)

```
-- 外连接
-- 比如：列出部门名称和这些部门的员工名称和工作，
-- 同时要求 显示出那些没有员工的部门。
-- 使用我们学习过的多表查询的SQL， 看看效果如何?
SELECT dname, ename, job 
	FROM emp, dept
	WHERE emp.deptno = dept.deptno
	ORDER BY dname
SELECT * FROM dept;
SELECT * FROM emp;

CREATE TABLE stu (
	id INT,
	`name` VARCHAR(32));
INSERT INTO stu VALUES(1, 'jack'),(2,'tom'),(3, 'kity'),(4, 'nono');
SELECT * FROM stu;

CREATE TABLE exam(
	id INT,
	grade INT);
INSERT INTO exam VALUES(1, 56),(2,76),(11, 8);
SELECT * FROM exam;

-- 使用左连接
-- （显示所有人的成绩，如果没有成绩，也要显示该人的姓名和id号,成绩显示为空）
SELECT `name`, stu.id, grade
	FROM stu, exam
	WHERE stu.id = exam.id;
	
-- 改成左外连接
SELECT `name`, stu.id, grade
	FROM stu LEFT JOIN exam
	ON stu.id = exam.id;
	
-- 使用右外连接（显示所有成绩，如果没有名字匹配，显示空)
-- 即：右边的表(exam) 和左表没有匹配的记录，也会把右表的记录显示出来
SELECT `name`, stu.id, grade
	FROM stu RIGHT JOIN exam
	ON stu.id = exam.id;

-- 列出部门名称和这些部门的员工信息(名字和工作)，
-- 同时列出那些没有员工的部门名。
-- 使用左外连接实现
SELECT dname, ename, job
	FROM dept LEFT JOIN emp
	ON dept.deptno = emp.deptno
	
-- 使用右外连接实现
SELECT dname, ename, job
	FROM emp RIGHT JOIN dept
	ON dept.deptno = emp.deptno
```

24.35 mysql 约束

24.35.1 基本介绍  
![](https://img-blog.csdnimg.cn/71ccfcde6fc14614816d25cd2ecf4414.png)  
24.35.2 primary key(主键)- 基本使用  
![](https://img-blog.csdnimg.cn/a8ae203b21294d31ada6dc32aacf5404.png)  
![](https://img-blog.csdnimg.cn/826e9f14e915465484eae428f13fcba5.png)

```
-- 主键使用
-- id	name 	email
CREATE TABLE t17
	(id INT PRIMARY KEY, -- 表示id列是主键 
	`name` VARCHAR(32),
	email VARCHAR(32));
	
-- 主键列的值是不可以重复
INSERT INTO t17
	VALUES(1, 'jack', 'jack@sohu.com');
INSERT INTO t17
	VALUES(2, 'tom', 'tom@sohu.com');
INSERT INTO t17
	VALUES(1, 'hsp', 'hsp@sohu.com');
	
SELECT * FROM t17;

-- 主键使用的细节讨论
-- primary key不能重复而且不能为 null。
INSERT INTO t17
	VALUES(NULL, 'hsp', 'hsp@sohu.com');
-- 一张表最多只能有一个主键, 但可以是复合主键(比如 id+name)
CREATE TABLE t18
	(id INT PRIMARY KEY, -- 表示id列是主键 
	`name` VARCHAR(32) PRIMARY KEY,-- 错误的
	email VARCHAR(32));
-- 演示复合主键 (id 和 name 做成复合主键)
CREATE TABLE t18
	(id INT , 
	`name` VARCHAR(32), 
	email VARCHAR(32),
	PRIMARY KEY (id, `name`) -- 这里就是复合主键
	);

INSERT INTO t18
	VALUES(1, 'tom', 'tom@sohu.com');
INSERT INTO t18
	VALUES(1, 'jack', 'jack@sohu.com');
INSERT INTO t18
	VALUES(1, 'tom', 'xx@sohu.com'); -- 这里就违反了复合主键
SELECT * FROM t18;

-- 主键的指定方式 有两种 
-- 1. 直接在字段名后指定：字段名  primakry key
-- 2. 在表定义最后写 primary key(列名); 
CREATE TABLE t19
	(id INT , 
	`name` VARCHAR(32) PRIMARY KEY, 
	email VARCHAR(32)
	);
CREATE TABLE t20
	(id INT , 
	`name` VARCHAR(32) , 
	email VARCHAR(32),
	PRIMARY KEY(`name`) -- 在表定义最后写 primary key(列名)
	);
 
-- 使用desc 表名，可以看到primary key的情况
DESC t20 -- 查看 t20表的结果，显示约束的情况
DESC t18
```

24.35.3 not null(非空) 和 unique(唯一)  
![](https://img-blog.csdnimg.cn/bbfa4c5e0752403aa2647567fd3c9937.png)

```
-- unique的使用
CREATE TABLE t21
	(id INT UNIQUE ,  -- 表示 id 列是不可以重复的.
	`name` VARCHAR(32) , 
	email VARCHAR(32)
	);
	
INSERT INTO t21
	VALUES(1, 'jack', 'jack@sohu.com');
INSERT INTO t21
	VALUES(1, 'tom', 'tom@sohu.com');
	
-- unqiue使用细节
-- 1. 如果没有指定 not null , 则 unique 字段可以有多个null
-- 如果一个列(字段)， 是 unique not null 使用效果类似 primary key
INSERT INTO t21
	VALUES(NULL, 'tom', 'tom@sohu.com');
SELECT * FROM t21;
-- 2. 一张表可以有多个unique字段
CREATE TABLE t22
	(id INT UNIQUE ,  -- 表示 id 列是不可以重复的.
	`name` VARCHAR(32) UNIQUE , -- 表示name不可以重复 
	email VARCHAR(32)
	);
DESC t22
一张表只能有一个primary key字段，即使是复合主键也只能有一个
```

24.35.5 foreign key(外键)  
![](https://img-blog.csdnimg.cn/cb0163a8b3fd4256bc091b053f512970.png)  
![](https://img-blog.csdnimg.cn/deb494dc6d7947109649187c34975c54.png)  
![](https://img-blog.csdnimg.cn/966706d162d14fadb9892a6da5c162b3.png)

```
- 外键演示
-- 创建 主表 my_class
CREATE TABLE my_class (
	id INT PRIMARY KEY , -- 班级编号
	`name` VARCHAR(32) NOT NULL DEFAULT '');

-- 创建 从表 my_stu
CREATE TABLE my_stu (
	id INT PRIMARY KEY , -- 学生编号
	`name` VARCHAR(32) NOT NULL DEFAULT '',
	class_id INT , -- 学生所在班级的编号
	-- 下面指定外键关系
	FOREIGN KEY (class_id) REFERENCES my_class(id))
-- 测试数据
INSERT INTO my_class 
	VALUES(100, 'java'), (200, 'web');
INSERT INTO my_class 
	VALUES(300, 'php');
	
SELECT * FROM my_class;
INSERT INTO my_stu 
	VALUES(1, 'tom', 100);
INSERT INTO my_stu 
	VALUES(2, 'jack', 200);
INSERT INTO my_stu 
	VALUES(3, 'hsp', 300);
INSERT INTO my_stu 
	VALUES(4, 'mary', 400); -- 这里会失败...因为400班级不存在

INSERT INTO my_stu 
	VALUES(5, 'king', NULL); -- 可以, 外键 没有写 not null
SELECT * FROM my_class;

-- 一旦建立主外键的关系，数据不能随意删除了
DELETE FROM my_class
	WHERE id = 100;
```

24.35.6 check  
![](https://img-blog.csdnimg.cn/86026eae960245ca8a59a1b5a64461a7.png)

```
-- 演示check的使用
-- mysql5.7目前还不支持check ,只做语法校验，但不会生效
-- 了解 
-- 学习 oracle, sql server, 这两个数据库是真的生效.

-- 测试
CREATE TABLE t23 (
	id INT PRIMARY KEY,
	`name` VARCHAR(32) ,
	sex VARCHAR(6) CHECK (sex IN('man','woman')),
	sal DOUBLE CHECK ( sal > 1000 AND sal < 2000)
	);
-- 添加数据
INSERT INTO t23 
	VALUES(1, 'jack', 'mid', 1);
SELECT * FROM t23;
```

24.35.7 商店售货系统表设计案例  
![](https://img-blog.csdnimg.cn/609943320c914559a8cfa59d8c176500.png)

```
CREATE DATABASE shop_db;
-- 商品goods
CREATE TABLE goods (
	goods_id INT PRIMARY KEY,
	goods_name VARCHAR(64) NOT NULL DEFAULT '',
	unitprice DECIMAL(10,2) NOT NULL DEFAULT 0 
		CHECK (unitprice >= 1.0 AND unitprice <= 9999.99),
	category INT NOT NULL DEFAULT 0,
	provider VARCHAR(64) NOT NULL DEFAULT '');
	
-- 客户customer（客户号customer_id,姓名name,住址address,电邮email性别sex,身份证card_Id);
CREATE TABLE customer(
	customer_id CHAR(8) PRIMARY KEY, -- 程序员自己决定
	`name` VARCHAR(64) NOT NULL DEFAULT '',
	address VARCHAR(64) NOT NULL DEFAULT '',
	email VARCHAR(64) UNIQUE NOT NULL,
	sex ENUM('男','女') NOT NULL ,  -- 这里老师使用的枚举类型, 是生效
	card_Id CHAR(18)); 
	
-- 购买purchase（购买订单号order_id，客户号customer_id,商品号goods_id,购买数量nums);
CREATE TABLE purchase(
	order_id INT UNSIGNED PRIMARY KEY,
	customer_id CHAR(8) NOT NULL DEFAULT '', -- 外键约束在后
	goods_id INT NOT NULL DEFAULT 0 , -- 外键约束在后
	nums INT NOT NULL DEFAULT 0,
	FOREIGN KEY (customer_id) REFERENCES customer(customer_id),
	FOREIGN KEY (goods_id) REFERENCES goods(goods_id));
```

24.36 自增长  
![](https://img-blog.csdnimg.cn/2adb62cd8bd445228aced13e519857d8.png)  
![](https://img-blog.csdnimg.cn/6f067391a4804bd58f20afd77cc59632.png)

```
-- 演示自增长的使用
-- 创建表
CREATE TABLE t24
	(id INT PRIMARY KEY AUTO_INCREMENT,
	 email VARCHAR(32)NOT NULL DEFAULT '',
	 `name` VARCHAR(32)NOT NULL DEFAULT ''); 
DESC t24
-- 测试自增长的使用
INSERT INTO t24 VALUES(NULL, 'tom@qq.com', 'tom');
INSERT INTO t24 (email, `name`) VALUES('hsp@sohu.com', 'hsp');
SELECT * FROM t24;

-- 修改默认的自增长开始值
ALTER TABLE t25 AUTO_INCREMENT = 100
CREATE TABLE t25
	(id INT PRIMARY KEY AUTO_INCREMENT,
	 email VARCHAR(32)NOT NULL DEFAULT '',
	 `name` VARCHAR(32)NOT NULL DEFAULT ''); 
INSERT INTO t25 VALUES(NULL, 'mary@qq.com', 'mary');
INSERT INTO t25 VALUES(666, 'hsp@qq.com', 'hsp');
SELECT * FROM t25;
```

24.37 mysql 索引

24.37.1 索引快速入门  
![](https://img-blog.csdnimg.cn/645e8311c749433884efae7fb1129de5.png)

```
-- 在没有创建索引时，我们的查询一条记录
SELECT * 
	FROM emp 
	WHERE empno = 1234567 
-- 使用索引来优化一下， 体验索引的牛

-- 在没有创建索引前 , emp.ibd 文件大小 是 524m
-- 创建索引后 emp.ibd 文件大小 是 655m [索引本身也会占用空间.]
-- 创建ename列索引,emp.ibd 文件大小 是 827m

-- empno_index 索引名称 
-- ON emp (empno) : 表示在 emp表的 empno列创建索引
CREATE INDEX empno_index ON emp (empno)

-- 创建索引后， 查询的速度如何
SELECT * 
	FROM emp 
	WHERE empno = 1234578 -- 0.003s 原来是4.5s

-- 创建索引后，只对创建了索引的列有效 
SELECT * 
	FROM emp 
	WHERE ename = 'PjDlwy' -- 没有在ename创建索引时，时间4.7s

CREATE INDEX ename_index ON emp (ename) -- 在ename上创建索引
```

24.37.2 索引的原理  
![](https://img-blog.csdnimg.cn/43a64d21b2df468795ca142d0204cfc5.png)  
![](https://img-blog.csdnimg.cn/f3415e4cd38a4403bbb18aa8d92e04e3.png)  
24.37.3 索引的类型  
![](https://img-blog.csdnimg.cn/8ec75fc034884b68bedf84a32a576a13.png)  
24.37.4 索引使用  
![](https://img-blog.csdnimg.cn/790aa6380cd64891bfcb48a95ab8476b.png)  
![](https://img-blog.csdnimg.cn/8f228715aa4a4a0795cd54ba314c2413.png)

```
-- 演示mysql的索引的使用
-- 创建索引
CREATE TABLE t25 (
	id INT ,
	`name` VARCHAR(32));
-- 查询表是否有索引
SHOW INDEXES FROM t25;
-- 添加索引
-- 添加唯一索引 
CREATE UNIQUE INDEX id_index ON t25 (id);
-- 添加普通索引方式1
CREATE INDEX id_index ON t25 (id);
-- 如何选择 
-- 1. 如果某列的值，是不会重复的，则优先考虑使用unique索引, 否则使用普通索引
-- 添加普通索引方式2
ALTER TABLE t25 ADD INDEX id_index (id)

-- 添加主键索引
CREATE TABLE t26 (
	id INT ,
	`name` VARCHAR(32));
ALTER TABLE t26 ADD PRIMARY KEY (id)

SHOW INDEX FROM t25

-- 删除索引
DROP INDEX id_index ON t25
-- 删除主键索引
ALTER TABLE t26 DROP PRIMARY KEY

-- 修改索引 ， 先删除，在添加新的索引
-- 查询索引
-- 1. 方式
SHOW INDEX FROM t25
-- 2. 方式
SHOW INDEXES FROM t25
-- 3. 方式
SHOW KEYS FROM t25
-- 4 方式
DESC t25
```

24.37.6 小结  
![](https://img-blog.csdnimg.cn/3d86512966bc418d815b689da8b93ef0.png)  
24.38 mysql 事务

24.38.2 事务和锁  
![](https://img-blog.csdnimg.cn/aeeaa1289ff14ed9ad106a801afd618d.png)  
![](https://img-blog.csdnimg.cn/8b9dd3fe56db4af59d426c040ce300b5.png)  
24.38.3 回退事务和提交事务  
![](https://img-blog.csdnimg.cn/8fb480f3bc69448ca96ee3e4d0c8737b.png)

```
-- 事务的一个重要的概念和具体操作
-- 看一个图[看示意图]
-- 演示
-- 1. 创建一张测试表
CREATE TABLE t27
	( id INT,
	  `name` VARCHAR(32));
-- 2. 开始事务
START TRANSACTION 
-- 3. 设置保存点
SAVEPOINT a
-- 执行dml 操作
INSERT INTO t27 VALUES(100, 'tom');
SELECT * FROM t27;

SAVEPOINT b
-- 执行dml操作
INSERT INTO t27 VALUES(200, 'jack');
-- 回退到 b
ROLLBACK TO b
-- 继续回退 a
ROLLBACK TO a
-- 如果这样, 表示直接回退到事务开始的状态.
ROLLBACK 
COMMIT
```

24.38.5 事务细节讨论  
![](https://img-blog.csdnimg.cn/fc26fd1ea42c4fabb3971b75d7bca844.png)

```
-- 讨论 事务细节
-- 1. 如果不开始事务，默认情况下，dml操作是自动提交的，不能回滚
INSERT INTO t27 VALUES(300, 'milan'); -- 自动提交 commit
SELECT * FROM t27

-- 2. 如果开始一个事务，你没有创建保存点. 你可以执行 rollback，
-- 默认就是回退到你事务开始的状态
START TRANSACTION 
INSERT INTO t27 VALUES(400, 'king');
INSERT INTO t27 VALUES(500, 'scott');
ROLLBACK -- 表示直接回退到事务开始的的状态
COMMIT;

-- 3. 你也可以在这个事务中(还没有提交时), 创建多个保存点.比如: savepoint 	aaa;    
-- 执行 dml , savepoint  bbb
-- 4. 你可以在事务没有提交前，选择回退到哪个保存点
-- 5. InnoDB 存储引擎支持事务 , MyISAM 不支持
-- 6. 开始一个事务 start  transaction,    set autocommit=off;
```

24.39 mysql 事务隔离级别

24.39.1 事务隔离级别介绍  
![](https://img-blog.csdnimg.cn/bcf3d30d0ba74f248f49881e962f2a89.png)  
24.39.2 查看事务隔离级别  
![](https://img-blog.csdnimg.cn/18764abf23f64573a90c9e20833013c6.png)  
![](https://img-blog.csdnimg.cn/f3d87c4d521047b3be2d457aa578cd96.png)  
24.39.5 设置事务隔离级别  
![](https://img-blog.csdnimg.cn/ace876da17bd4dd4abee42589a9aefa9.png)  
![](https://img-blog.csdnimg.cn/6dffc2cdca384630936c3d979488d2db.png)

```
-- 演示mysql的事务隔离级别

-- 1. 开了两个mysql的控制台
-- 2. 查看当前mysql的隔离级别
SELECT @@tx_isolation;
-- mysql> SELECT @@tx_isolation;
-- +-----------------+
-- | @@tx_isolation  |
-- +-----------------+
-- | REPEATABLE-READ |
-- +-----------------+

-- 3.把其中一个控制台的隔离级别设置 Read uncommitted
SET SESSION TRANSACTION ISOLATION LEVEL READ UNCOMMITTED

-- 4. 创建表
CREATE TABLE `account`(
	id INT,
	`name` VARCHAR(32),
	money INT);

-- 查看当前会话隔离级别 
SELECT @@tx_isolation
-- 查看系统当前隔离级别
SELECT @@global.tx_isolation
-- 设置当前会话隔离级别
SET SESSION TRANSACTION ISOLATION LEVEL READ UNCOMMITTED
-- 设置系统当前隔离级别
SET GLOBAL TRANSACTION ISOLATION LEVEL [你设置的级别]
```

24.40 mysql 事务 ACID  
![](https://img-blog.csdnimg.cn/0f76cc1e3ca349539638ff04c25a8991.png)  
24.41 mysql 表类型和存储引擎

24.41.1 基本介绍  
![](https://img-blog.csdnimg.cn/2abc951d23e64661accff70a2e3dda1e.png)  
24.41.2 主要的存储引擎 / 表类型特点  
![](https://img-blog.csdnimg.cn/c62f142068ba4b8c9486a23df0c65baa.png)  
24.41.3 细节说明  
![](https://img-blog.csdnimg.cn/81a0773c7f00428f9fcecd98c38b619f.png)  
24.41.4 三种存储引擎表使用案例  
![](https://img-blog.csdnimg.cn/204df25f9de54ab0843df36bd790b300.png)  
![](https://img-blog.csdnimg.cn/cd294595552b4a0dab2b1ab0895ab5a1.png)

```
-- 表类型和存储引擎
-- 查看所有的存储引擎
SHOW ENGINES
-- innodb 存储引擎，是前面使用过.
-- 1. 支持事务 2. 支持外键 3. 支持行级锁

-- myisam 存储引擎
CREATE TABLE t28 (
	id INT,
	`name` VARCHAR(32)) ENGINE MYISAM
-- 1. 添加速度快 2. 不支持外键和事务 3. 支持表级锁

START TRANSACTION;
SAVEPOINT t1
INSERT INTO t28 VALUES(1, 'jack');
SELECT * FROM t28;
ROLLBACK TO t1

-- memory 存储引擎
-- 1. 数据存储在内存中[关闭了Mysql服务，数据丢失, 但是表结构还在] 
-- 2. 执行速度很快(没有IO读写) 3. 默认支持索引(hash表)

CREATE TABLE t29 (
	id INT,
	`name` VARCHAR(32)) ENGINE MEMORY
DESC t29
INSERT INTO t29
	VALUES(1,'tom'), (2,'jack'), (3, 'hsp');
SELECT * FROM t29

-- 指令修改存储引擎
ALTER TABLE `t29` ENGINE = INNODB
```

24.42 视图 (view)

24.42.1 看一个需求  
![](https://img-blog.csdnimg.cn/58bb09116d7e47f6aefcbf4eef8b4762.png)  
24.42.2 基本概念  
![](https://img-blog.csdnimg.cn/d8d09f9a7b434ad898bbb83dc8cdf27c.png)  
24.42.3 视图的基本使用  
![](https://img-blog.csdnimg.cn/dbd1a79ebbb64ac99edff326ea8c9a3f.png)  
![](https://img-blog.csdnimg.cn/0a3d8ed1aea94bc29fade0ce75629bbb.png)

```
-- 视图的使用
-- 创建一个视图emp_view01，只能查询emp表的(empno、ename, job 和 deptno ) 信息

-- 创建视图
CREATE VIEW emp_view01
	AS
	SELECT empno, ename, job, deptno FROM emp; 

-- 查看视图
DESC emp_view01

SELECT * FROM emp_view01;
SELECT empno, job  FROM emp_view01;

-- 查看创建视图的指令
SHOW CREATE VIEW emp_view01
-- 删除视图
DROP VIEW emp_view01;

-- 视图的细节
-- 1. 创建视图后，到数据库去看，对应视图只有一个视图结构文件(形式: 视图名.frm) 
-- 2. 视图的数据变化会影响到基表，基表的数据变化也会影响到视图[insert update delete ]

-- 修改视图 会影响到基表
UPDATE emp_view01 
	SET job = 'MANAGER' 
	WHERE empno = 7369
	
SELECT * FROM emp; -- 查询基表
SELECT * FROM emp_view01

-- 修改基本表， 会影响到视图
UPDATE emp 
	SET job = 'SALESMAN' 
	WHERE empno = 7369

-- 3. 视图中可以再使用视图 , 比如从emp_view01 视图中，选出empno,和ename做出新视图
DESC emp_view01
CREATE VIEW emp_view02
	AS
	SELECT empno, ename FROM emp_view01
SELECT * FROM emp_view02
```

24.42.6 视图最佳实践  
![](https://img-blog.csdnimg.cn/92483b2449d142be9c219cadd13665ab.png)  
24.42.7 视图课堂练习  
![](https://img-blog.csdnimg.cn/5358be6621ec4926b29e1447a368fe8a.png)

```
-- 视图的课堂练习
-- 针对 emp ，dept , 和   salgrade 张三表.创建一个视图 emp_view03，
-- 可以显示雇员编号，雇员名，雇员部门名称和 薪水级别[即使用三张表，构建一个视图]
/*
	分析: 使用三表联合查询，得到结果
	将得到的结果，构建成视图
*/
CREATE VIEW emp_view03
	AS
	SELECT empno, ename, dname, grade
	FROM emp, dept, salgrade
	WHERE emp.deptno = dept.deptno AND 
	(sal BETWEEN losal AND hisal) 

DESC emp_view03
SELECT * FROM emp_view03
```

24.43 Mysql 管理

24.43.1 Mysql 用户  
![](https://img-blog.csdnimg.cn/d28b20158e824343a9e7484a67ea2b6b.png)  
24.43.2 创建用户和删除用户  
![](https://img-blog.csdnimg.cn/b22fbe91551544c3b7031b3aefde082d.png)  
![](https://img-blog.csdnimg.cn/d03e61546d804133bfa3af72306f663a.png)

```
-- Mysql用户的管理
-- 原因：当我们做项目开发时，可以根据不同的开发人员，赋给他相应的Mysql操作权限
-- 所以，Mysql数据库管理人员(root), 根据需要创建不同的用户，赋给相应的权限，供人员使用

-- 1. 创建新的用户
-- 解读 (1) 'hsp_edu'@'localhost' 表示用户的完整信息 'hsp_edu' 用户名 'localhost' 登录的IP
-- (2) 123456 密码, 但是注意 存放到 mysql.user表时，是password('123456') 加密后的密码
--     *6BB4837EB74329105EE4568DDA7DC67ED2CA2AD9
CREATE USER 'hsp_edu'@'localhost' IDENTIFIED BY '123456'

SELECT `host`, `user`, authentication_string  
	FROM mysql.user

-- 2. 删除用户
DROP USER 'hsp_edu'@'localhost'
```

24.43.4 用户修改密码  
![](https://img-blog.csdnimg.cn/b4797ff4ff664b2e90e5fa2d48610d8b.png)

```
--  修改自己的密码, 没问题
SET PASSWORD = PASSWORD('abcdef')

-- root 用户修改 hsp_edu@localhost 密码, 是可以成功.
SET PASSWORD FOR 'hsp_edu'@'localhost' = PASSWORD('123456')
```

24.43.5 mysql 中的权限  
![](https://img-blog.csdnimg.cn/4285b2bad384496a94b6c4eb544747e6.png)  
24.43.6 给用户授权  
![](https://img-blog.csdnimg.cn/e1fef5dc6f294aa7a6d50a2912fbaf85.png)  
24.43.7 回收用户授权 和 权限生效指令  
![](https://img-blog.csdnimg.cn/dd02c56a6253483b8ad48df5b761ad8e.png)  
24.43.9 课堂练习题  
![](https://img-blog.csdnimg.cn/47174800c46d418fbe42f6e8059916f3.png)

```
-- 演示 用户权限的管理
-- 创建用户 shunping  密码 123 , 从本地登录
CREATE USER 'shunping'@'localhost' IDENTIFIED BY '123'

-- 使用root 用户创建 testdb  ,表 news
CREATE DATABASE testdb
CREATE TABLE news (
	id INT ,
	content VARCHAR(32));
-- 添加一条测试数据
INSERT INTO news VALUES(100, '北京新闻');
SELECT * FROM news;

-- 给 shunping 分配查看 news 表和 添加news的权限
GRANT SELECT , INSERT 
	ON testdb.news
	TO 'shunping'@'localhost'
	
-- 可以增加update权限
GRANT UPDATE  
	ON testdb.news
	TO 'shunping'@'localhost'
	
-- 修改 shunping的密码为 abc
SET PASSWORD FOR 'shunping'@'localhost' = PASSWORD('abc');

-- 回收 shunping 用户在 testdb.news 表的所有权限
REVOKE SELECT , UPDATE, INSERT ON testdb.news FROM 'shunping'@'localhost'
REVOKE ALL ON testdb.news FROM 'shunping'@'localhost'

-- 删除 shunping
DROP USER 'shunping'@'localhost'
```

新创建的普通用户默认情况下只能看到一个默认的系统数据库。

24.43.10 细节说明  
![](https://img-blog.csdnimg.cn/3aa529f4b180434ca101c27bbc7ddc49.png)

```
-- 说明 用户管理的细节
-- 在创建用户的时候，如果不指定Host, 则为% , %表示表示所有IP都有连接权限 
-- create user  xxx;
CREATE USER jack
SELECT `host`, `user` FROM mysql.user

-- 你也可以这样指定 
-- create user  'xxx'@'192.168.1.%'  表示 xxx用户在 192.168.1.*的ip可以登录mysql
CREATE USER 'smith'@'192.168.1.%'

-- 在删除用户的时候，如果 host 不是 %, 需要明确指定  '用户'@'host值'
DROP USER jack -- 默认就是 DROP USER 'jack'@'%'
DROP USER 'smith'@'192.168.1.%'
```

24.44 本章作业  
![](https://img-blog.csdnimg.cn/a395c7a19d234464a3298714a5b58f5c.png)  
![](https://img-blog.csdnimg.cn/6663943f78f64f5caf47e6bdb33bb78c.png)  
双引号单引号都可以

![](https://img-blog.csdnimg.cn/cc9e6458cb924928aeb25c234fbd4e43.png)

```
-- 2. 写出 查看DEPT表和EMP表的结构 的sql语句
	DESC dept
	DESC emp
-- 3. 使用简单查询语句完成:
-- (1) 显示所有部门名称。
SELECT dname 
	FROM dept;
-- (2) 显示所有雇员名及其全年收入 13月(工资+补助),并指定列别名"年收入"
SELECT ename, (sal + IFNULL(comm,0)) * 13 AS "年收入"
	FROM emp 
SELECT * FROM emp;	--如果一个数加上NULL则结果为NULL

-- 4.限制查询数据。
-- (1) 显示工资超过2850的雇员姓名和工资。
SELECT ename, sal
	FROM emp 
	WHERE sal > 2850
-- (2) 显示工资不在1500到2850之间的所有雇员名及工资。
SELECT ename, sal
	FROM emp 
	WHERE sal < 1500 OR sal > 2850
	
SELECT ename, sal
	FROM emp 
	WHERE NOT (sal >= 1500 AND sal <= 2850)
-- (3) 显示编号为7566的雇员姓名及所在部门编号。
SELECT ename, deptno
	FROM emp 
	WHERE empno = 7566
-- (4) 显示部门10和30中工资超过1500的雇员名及工资。
SELECT ename, job
	FROM emp 
	WHERE (deptno = 10 OR deptno = 30) AND sal > 1500
-- (5) 显示无管理者的雇员名及岗位。
SELECT ename, job 
	FROM emp
	WHERE mgr IS NULL;
	
-- 5.排序数据。
-- (1) 显示在1991年2月1日到1991年5月1日之间雇用的雇员名,岗位及雇佣日期, 并以雇佣日期进行排序[默认]。
-- 思路 1. 先查询到对应结果 2. 考虑排序
SELECT ename, job, hiredate
	FROM emp
	WHERE hiredate >= '1991-02-01' AND hiredate <= '1991-05-01'
	ORDER BY hiredate

-- (2) 显示获得补助的所有雇员名,工资及补助,并以工资降序排序
SELECT ename, sal, comm
	FROM emp
	WHERE comm IS NO NULL
	ORDER BY sal DESC
```

![](https://img-blog.csdnimg.cn/00d20e8e279a4a39bebb73b9fb0ca082.png)

```
-- homework03
-- ------1.选择部门30中的所有员工.
SELECT * FROM 
	emp
	WHERE deptno = 30
-- ------2.列出所有办事员(CLERK)的姓名，编号和部门编号. 
SELECT ename, empno, deptno, job FROM 
	emp
	WHERE job = 'CLERK'
-- ------3.找出佣金高于薪金的员工.
SELECT * FROM 
	emp
	WHERE IFNULL(comm, 0) > sal
-- ------4.找出佣金高于薪金60%的员工.
SELECT * FROM 
	emp
	WHERE IFNULL(comm, 0) > sal * 0.6
-- ------5.找出部门10中所有经理(MANAGER)和部门20中所有办事员(CLERK)的详细资料.
-- 
SELECT * FROM
	emp
	WHERE (deptno = 10 AND job = 'MANAGER') 
	OR (deptno = 20 AND job = 'CLERK')
-- ------6.找出部门10中所有经理(MANAGER),部门20中所有办事员(CLERK), 
 -- 还有既不是经理又不是办事员但其薪金大于或等于2000的所有员工的详细资料.
SELECT * FROM
	emp
	WHERE (deptno = 10 AND job = 'MANAGER') 
	OR (deptno = 20 AND job = 'CLERK')
	OR (job != 'MANAGER' AND job != 'CLERK' AND sal >= 2000 )
-- ------7.找出收取佣金的员工的不同工作.
SELECT DISTINCT job
	FROM emp
	WHERE comm IS NOT NULL
-- ------8.找出不收取佣金或收取的佣金低于100的员工.
SELECT *
	FROM emp
	WHERE IFNULL(comm, 0) < 100
-- ------9.找出各月倒数第3天受雇的所有员工.
-- 老韩提示: last_day(日期)， 可以返回该日期所在月份的最后一天
-- last_day(日期) - 2 得到日期所有月份的倒数第3天
SELECT * 
	FROM emp
	WHERE LAST_DAY(hiredate) - 2  =  hiredate
-- ------10.找出早于12年前受雇的员工.（即： 入职时间超过12年）
SELECT * 
	FROM emp
	WHERE DATE_ADD(hiredate, INTERVAL 12 YEAR) < NOW() 
-- ------11.以首字母小写的方式显示所有员工的姓名.
SELECT CONCAT(LCASE(SUBSTRING(ename,1,1)), SUBSTRING(ename,2))
	FROM emp;
-- ------12.显示正好为5个字符的员工的姓名.
SELECT * 
	FROM emp
	WHERE LENGTH(ename) = 5
```

![](https://img-blog.csdnimg.cn/0afa2e667097498483e974450922908c.png)

```
-- ------13.显示不带有"R"的员工的姓名.
SELECT * 
	FROM emp
	WHERE ename NOT LIKE '%R%'
-- ------14.显示所有员工姓名的前三个字符.
SELECT LEFT(ename,3)
	FROM emp
-- ------15.显示所有员工的姓名,用a替换所有"A"
SELECT REPLACE(ename, 'A', 'a') 
	FROM emp
-- ------16.显示满10年服务年限的员工的姓名和受雇日期.
SELECT ename, hiredate
	FROM emp
	WHERE DATE_ADD(hiredate, INTERVAL 10 YEAR) <= NOW()
-- ------17.显示员工的详细资料,按姓名排序.

-- ------18.显示员工的姓名和受雇日期,根据其服务年限,将最老的员工排在最前面.
SELECT ename, hiredate
	FROM emp
	ORDER BY hiredate 
-- ------19.显示所有员工的姓名、工作和薪金,按工作降序排序,若工作相同则按薪金排序.
SELECT ename, job, sal
	FROM emp
	ORDER BY job DESC, sal 
-- ------20.显示所有员工的姓名、加入公司的年份和月份,按受雇日期所在月排序,若月份相同则将最早年份的员工排在最前面.
SELECT ename, CONCAT(YEAR(hiredate),'-', MONTH(hiredate))
	FROM emp
	ORDER BY MONTH(hiredate), YEAR(hiredate)
-- ------21.显示在一个月为30天的情况所有员工的日薪金,忽略余数.
SELECT ename, FLOOR(sal / 30), sal / 30 
	FROM emp; 
-- ------22.找出在(任何年份的)2月受聘的所有员工。
SELECT * 
	FROM emp
	WHERE MONTH(hiredate) = 2
-- ------23.对于每个员工,显示其加入公司的天数.
SELECT ename, DATEDIFF(NOW(), hiredate) 
	FROM emp
-- ------24.显示姓名字段的任何位置包含"A"的所有员工的姓名.
SELECT *
	FROM emp
	WHERE ename LIKE '%A%'
-- ------25.以年月日的方式显示所有员工的服务年限.   (大概)
-- 思路 1. 先求出 工作了多少天 
SELECT ename, FLOOR(DATEDIFF(NOW(), hiredate) / 365) AS " 工作年 ", 
	FLOOR((DATEDIFF(NOW(), hiredate) % 365) / 31) AS " 工作月 ",
	DATEDIFF(NOW(), hiredate) % 31 AS " 工作天"
	FROM emp;
```

![](https://img-blog.csdnimg.cn/a19ab34d63f245a1b65598fb7a4ea517.png)

```
-- (1)．列出至少有一个员工的所有部门
/*
	先查出各个部门有多少人
	使用 having 子句过滤
*/
SELECT COUNT(*) AS c, deptno
	FROM emp 
	GROUP BY deptno 
	HAVING c >= 1
-- (2)．列出薪金比“SMITH”多的所有员工。
/*
	先查出 smith 的 sal => 作为子查询
	然后其他员工 sal 大于 smith 即可
*/
SELECT * 
	FROM emp
	WHERE sal > (
		SELECT sal 
			FROM emp 
			WHERE ename = 'SMITH'
	)
-- (3)．列出受雇日期晚于其直接上级的所有员工。
/*
	先把 emp 表 当做两张表 worker , leader
	条件 1. worker.hiredate > leader.hiredate
	     2. worker.mgr = leader.empno
*/
SELECT worker.ename AS '员工名', worker.hiredate AS '员工入职时间',
	leader.ename  AS '上级名', leader.hiredate AS '上级入职时间' 
	FROM emp worker , emp leader
	WHERE worker.hiredate > leader.hiredate 
	AND worker.mgr = leader.empno;
-- (4)．列出部门名称和这些部门的员工信息，同时列出那些没有员工的部门。
/*
	这里因为需要显示所有部门，因此考虑使用外连接，(左外连接)
	如果没有印象了，去看看老师讲的外连接.
*/
SELECT dname, emp.*
	FROM dept 
	LEFT JOIN emp ON dept.deptno = emp.deptno 
-- (5)．列出所有“CLERK”（办事员）的姓名及其部门名称。
SELECT ename, dname , job
	FROM emp, dept
	WHERE job = 'CLERK' AND emp.deptno = dept.deptno
-- (6)．列出最低薪金大于1500的各种工作。
/*
	查询各个岗位的最低工资
	使用having 子句进行过滤
*/
SELECT MIN(sal) AS min_sal , job
	FROM emp
	GROUP BY job
	HAVING min_sal > 1500
-- (7)．列出在部门“SALES”（销售部）工作的员工的姓名。
SELECT ename, dname
	FROM emp , dept
	WHERE emp.deptno = dept.deptno AND dname = 'SALES'
-- (8)．列出薪金高于公司平均薪金的所有员工。
SELECT *
	FROM emp
	WHERE sal > (
		SELECT AVG(sal) 
			FROM emp
	)
```

![](https://img-blog.csdnimg.cn/afc2e1d6182c48d093b09b4f0944a6a8.png)

```
-- (9)．列出与“SCOTT”从事相同工作的所有员工。
SELECT * 
	FROM emp
	WHERE job = (
		SELECT job 
			FROM emp
			WHERE ename = 'SCOTT'
	) AND ename != 'SCOTT'

-- (10)．列出薪金高于在部门30工作的所有员工的薪金的员工姓名和薪金。
-- 先查询出30部门的最高工资
SELECT ename, sal 
	FROM emp 
	WHERE sal > (
		SELECT MAX(sal) 
			FROM emp
			WHERE deptno = 30
	) 
-- (11)．列出在每个部门工作的员工数量、平均工资和平均服务期限(时间单位)。
-- 老师建议 ， 写sql 也是一步一步完成的
SELECT COUNT(*) AS "部门员工数量", deptno , AVG(sal) AS "部门平均工资" , 
	FORMAT(AVG(DATEDIFF(NOW(), hiredate) / 365 ),2) AS " 平均服务期限(年)"
	FROM emp 
	GROUP BY deptno
-- (12)．列出所有员工的姓名、部门名称和工资。
-- 就是 emp 和 dept 联合查询 ，连接条件就是 emp.deptno = dept.deptno
-- (13)．列出所有部门的详细信息和部门人数。
-- 1. 先得到各个部门人数 , 把下面的结果看成临时表 和 dept表联合查询
SELECT COUNT(*) AS c , deptno 
	FROM emp
	GROUP BY deptno
-- 2. 
SELECT dept.*, tmp.c AS "部门人数"
	FROM dept, (
		SELECT COUNT(*) AS c , deptno 
		FROM emp
		GROUP BY deptno
	) tmp 
	WHERE dept.deptno = tmp.deptno
-- (14)．列出各种工作的最低工资。
SELECT MIN(sal), job
	FROM emp
	GROUP BY job
-- (15)．列出MANAGER（经理）的最低薪金。
SELECT MIN(sal), job
	FROM emp
	WHERE job = 'MANAGER'
-- (16)．列出所有员工的年工资,按年薪从低到高排序。
SELECT ename, (sal + IFNULL(comm, 0)) * 12 year_sal
	FROM emp
	ORDER BY year_sal
```