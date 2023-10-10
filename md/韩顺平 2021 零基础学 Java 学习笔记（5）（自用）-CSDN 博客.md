> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/weixin_43973189/article/details/121701965?spm=1001.2014.3001.5502)

#### 目录

*   *   *   [第 25 章 JDBC 和数据库连接池](#_25__JDBC__1)
        *   [第 27 章 正则表达式](#_27___1331)

#### 第 25 章 JDBC 和[数据库连接池](https://so.csdn.net/so/search?q=%E6%95%B0%E6%8D%AE%E5%BA%93%E8%BF%9E%E6%8E%A5%E6%B1%A0&spm=1001.2101.3001.7020)

25.1 JDBC 概述

25.1.1 基本介绍  
![](https://img-blog.csdnimg.cn/4b4b4393ead74882be557298ffa40914.png)  
![](https://img-blog.csdnimg.cn/d7ff346e982546c49d6ac0612f7ab1bb.png)  
25.1.3 JDBC 带来的好处  
![](https://img-blog.csdnimg.cn/41777b1eb47e4b788231893c4e753769.png)  
![](https://img-blog.csdnimg.cn/0fe18b5350e541d6b01b6b8293b724fb.png)  
25.1.4 JDBC API  
![](https://img-blog.csdnimg.cn/89670793ee81496f88654f52bae6ea57.png)  
25.2 JDBC 快速入门

25.2.1 JDBC 程序编写步骤  
![](https://img-blog.csdnimg.cn/5a9051595e1242e284e64fe277fa90f7.png)  
25.2.3 JDBC 第一个程序

```
package com.hspedu.jdbc;
import com.mysql.jdbc.Driver;
import java.sql.Connection;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.Properties;
/**
 * 这是第一个Jdbc 程序，完成简单的操作
 */
public class Jdbc01 {
    public static void main(String[] args) throws SQLException {
        //前置工作： 在项目下创建一个文件夹比如 libs
        // 将 mysql.jar 拷贝到该目录下，点击 add to project ..加入到项目中
        //1. 注册驱动
        Driver driver = new Driver(); //创建driver对象
        //2. 得到连接
        // 老师解读
        //(1) jdbc:mysql:// 规定好表示协议，通过jdbc的方式连接mysql
        //(2) localhost 主机，可以是ip地址
        //(3) 3306 表示mysql监听的端口
        //(4) hsp_db02 连接到mysql dbms 的哪个数据库
        //(5) mysql的连接本质就是前面学过的socket连接
        String url = "jdbc:mysql://localhost:3306/hsp_db02";
        //将 用户名和密码放入到Properties 对象
        Properties properties = new Properties();
        //user 和 password 是规定好的，后面的值根据实际情况写
        properties.setProperty("user", "root");// 用户
        properties.setProperty("password", "hsp"); //密码
        Connection connect = driver.connect(url, properties);
        //3. 执行sql
        //String sql = "insert into actor values(null, '刘德华', '男', '1970-11-11', '110')";
        //String sql = "update actor set ;
        String sql = "delete from actor where id = 1";
        //statement 用于执行静态SQL语句并返回其生成的结果的对象
        Statement statement = connect.createStatement();
        int rows = statement.executeUpdate(sql); // 如果是 dml语句，返回的就是影响行数
        System.out.println(rows > 0 ? "成功" : "失败");
        //4. 关闭连接资源
        statement.close();
        connect.close();
    }
}
```

25.3 获取数据库连接 5 种方式

25.3.1 方式 1  
![](https://img-blog.csdnimg.cn/94abecb7487b4df0a2cbeb5d3136ba6a.png)

```
public class JdbcConn {
    //方式1
    @Test
    public void connect01() throws SQLException {
        Driver driver = new Driver(); //创建driver对象
        String url = "jdbc:mysql://localhost:3306/hsp_db02";
        //将 用户名和密码放入到Properties 对象
        Properties properties = new Properties();
        //说明 user 和 password 是规定好，后面的值根据实际情况写
        properties.setProperty("user", "root");// 用户
        properties.setProperty("password", "hsp"); //密码
        Connection connect = driver.connect(url, properties);
        System.out.println(connect);
    }
}
```

25.3.2 方式 2  
![](https://img-blog.csdnimg.cn/66d7da79212f44e18910473e9a4415ec.png)

```
public class JdbcConn {
	//方式2
    @Test
    public void connect02() throws ClassNotFoundException, IllegalAccessException, InstantiationException, SQLException {
        //使用反射加载Driver类 , 动态加载，更加的灵活，减少依赖性
        Class<?> aClass = Class.forName("com.mysql.jdbc.Driver");
        Driver driver = (Driver)aClass.newInstance();
        String url = "jdbc:mysql://localhost:3306/hsp_db02";
        //将 用户名和密码放入到Properties 对象
        Properties properties = new Properties();
        //说明 user 和 password 是规定好，后面的值根据实际情况写
        properties.setProperty("user", "root");// 用户
        properties.setProperty("password", "hsp"); //密码
        Connection connect = driver.connect(url, properties);
        System.out.println("方式2=" + connect);
    }
}
```

25.3.3 方式 3  
![](https://img-blog.csdnimg.cn/f2fb007dbace4f9487d0f2a491ea1937.png)

```
public class JdbcConn {
	//方式3 使用DriverManager 替代 driver 进行统一管理
    @Test
    public void connect03() throws IllegalAccessException, InstantiationException, ClassNotFoundException, SQLException {
        //使用反射加载Driver
        Class<?> aClass = Class.forName("com.mysql.jdbc.Driver");
        Driver driver = (Driver) aClass.newInstance();
        //创建url 和 user 和 password
        String url = "jdbc:mysql://localhost:3306/hsp_db02";
        String user = "root";
        String password = "hsp";
        DriverManager.registerDriver(driver);//注册Driver驱动
        Connection connection = DriverManager.getConnection(url, user, password);
        System.out.println("第三种方式=" + connection);
    }
}
```

25.3.4 方式 4  
![](https://img-blog.csdnimg.cn/7056679b7f8745e39c4b5d6437b3641b.png)

```
public class JdbcConn {
	//方式4: 使用Class.forName 自动完成注册驱动，简化代码
    @Test
    public void connect04() throws ClassNotFoundException, SQLException {
        //使用反射加载了 Driver类
        //在加载 Driver类时，完成注册
        /*
            源码: 1. 静态代码块，在类加载时，会执行一次.
            2. DriverManager.registerDriver(new Driver());
            3. 因此注册driver的工作已经完成
            static {
                try {
                    DriverManager.registerDriver(new Driver());
                } catch (SQLException var1) {
                    throw new RuntimeException("Can't register driver!");
                }
            }
         */
        Class.forName("com.mysql.jdbc.Driver");
        //创建url 和 user 和 password
        String url = "jdbc:mysql://localhost:3306/hsp_db02";
        String user = "root";
        String password = "hsp";
        Connection connection = DriverManager.getConnection(url, user, password);
        System.out.println("第4种方式~ " + connection);
    }
}
```

25.3.5 方式 5  
![](https://img-blog.csdnimg.cn/170e6ee808d74ae9a8a6d86d0510f920.png)

```
public class JdbcConn {
    //方式5 , 在方式4的基础上改进，增加配置文件，让连接mysql更加灵活
    //这种方式获取连接是使用的最多，开发推荐使用
    @Test
    public void connect05() throws IOException, ClassNotFoundException, SQLException {
        //通过Properties对象获取配置文件的信息
        Properties properties = new Properties();
        properties.load(new FileInputStream("src\\mysql.properties"));
        //获取相关的值
        String user = properties.getProperty("user");
        String password = properties.getProperty("password");
        String driver = properties.getProperty("driver");
        String url = properties.getProperty("url");
        Class.forName(driver);//建议写上
        Connection connection = DriverManager.getConnection(url, user, password);
        System.out.println("方式5 " + connection);
    }
}
```

mysql.properties

```
user=root
password=hsp
url=jdbc:mysql://localhost:3306/hsp_db02?rewriteBatchedStatements=true
driver=com.mysql.jdbc.Driver
```

25.4 ResultSet[结果集]

25.4.1 基本介绍  
![](https://img-blog.csdnimg.cn/958c2730dcd54eef9fe932c5c0f85ba9.png)  
![](https://img-blog.csdnimg.cn/8650f204a13042b48dcbeb94307b8152.png)

```
package com.hspedu.jdbc.resultset_;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.sql.*;
import java.util.Properties;
/**
 * 演示select 语句返回 ResultSet ,并取出结果
 */
@SuppressWarnings({"all"})
public class ResultSet_ {
    public static void main(String[] args) throws Exception {
        //通过Properties对象获取配置文件的信息
        Properties properties = new Properties();
        properties.load(new FileInputStream("src\\mysql.properties"));
        //获取相关的值
        String user = properties.getProperty("user");
        String password = properties.getProperty("password");
        String driver = properties.getProperty("driver");
        String url = properties.getProperty("url");
        //1. 注册驱动
        Class.forName(driver);//建议写上
        //2. 得到连接
        Connection connection = DriverManager.getConnection(url, user, password);
        //3. 得到Statement
        Statement statement = connection.createStatement();
        //4. 组织SqL
        String sql = "select id, name , sex, borndate from actor";
        //执行给定的SQL语句，该语句返回单个 ResultSet对象
        /*
        +----+-----------+-----+---------------------+
        | id | name      | sex | borndate            |
        +----+-----------+-----+---------------------+
        |  4 | 刘德华    | 男  | 1970-12-12 00:00:00 |
        |  5 | jack      | 男  | 1990-11-11 00:00:00 |
        +----+-----------+-----+---------------------+
         */
        /*
            老韩阅读debug 代码 resultSet 对象的结构
         */
        ResultSet resultSet = statement.executeQuery(sql);
        //5. 使用while取出数据
        while (resultSet.next()) { // 让光标向后移动，如果没有更多行，则返回false
            int id  = resultSet.getInt(1); //获取该行的第1列
            //int id1 = resultSet.getInt("id"); 通过列名来获取值, 推荐
            String name = resultSet.getString(2);//获取该行的第2列
            String sex = resultSet.getString(3);
            Date date = resultSet.getDate(4);
            System.out.println(id + "\t" + name + "\t" + sex + "\t" + date);
        }
        //6. 关闭连接
        resultSet.close();
        statement.close();
        connection.close();
    }
}
```

![](https://img-blog.csdnimg.cn/b1330473e9db4d0492a0d8933862e4d5.png)  
25.5 Statement

25.5.1 基本介绍  
![](https://img-blog.csdnimg.cn/e8426d50f8c141ae8812025a04c77f91.png)  
PreparedStatement 发送给 MySQL 的语句是编译过的，所以 MySQL 不用再编译，可以直接执行。

```
-- 演示sql 注入
-- 创建一张表
CREATE TABLE  admin ( -- 管理员表
NAME VARCHAR(32) NOT NULL UNIQUE,
pwd VARCHAR(32) NOT NULL DEFAULT '') CHARACTER SET utf8;
-- 添加数据
INSERT INTO admin VALUES('tom', '123');
-- 查找某个管理是否存在
SELECT * 
	FROM admin
	WHERE NAME = 'tom' AND pwd = '123'
-- SQL 
-- 输入用户名 为  1' or 
-- 输入万能密码 为 or '1'= '1 
SELECT * 
	FROM admin
	WHERE NAME = '1' OR' AND pwd = 'OR '1'= '1'
SELECT * FROM admin
```

25.5.2 应用实例  
![](https://img-blog.csdnimg.cn/dc088eb3672c4fcfa95d680475adea60.png)

```
package com.hspedu.jdbc.statement_;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.sql.*;
import java.util.Properties;
import java.util.Scanner;
/**
 * 演示statement 的注入问题
 */
@SuppressWarnings({"all"})
public class Statement_ {
    public static void main(String[] args) throws Exception {
        Scanner scanner = new Scanner(System.in);
        //让用户输入管理员名和密码
        System.out.print("请输入管理员的名字: ");  //next(): 当接收到 空格或者 '就是表示结束
        String admin_name = scanner.nextLine(); // 老师说明，如果希望看到SQL注入，这里需要用nextLine
        System.out.print("请输入管理员的密码: ");
        String admin_pwd = scanner.nextLine();
        //通过Properties对象获取配置文件的信息
        Properties properties = new Properties();
        properties.load(new FileInputStream("src\\mysql.properties"));
        //获取相关的值
        String user = properties.getProperty("user");
        String password = properties.getProperty("password");
        String driver = properties.getProperty("driver");
        String url = properties.getProperty("url");
        //1. 注册驱动
        Class.forName(driver);//建议写上
        //2. 得到连接
        Connection connection = DriverManager.getConnection(url, user, password);
        //3. 得到Statement
        Statement statement = connection.createStatement();
        //4. 组织SqL
        String sql = "select name , pwd  from admin where name ='"
                + admin_name + "' and pwd = '" + admin_pwd + "'";
        ResultSet resultSet = statement.executeQuery(sql);
        if (resultSet.next()) { //如果查询到一条记录，则说明该管理存在
            System.out.println("恭喜， 登录成功");
        } else {
            System.out.println("对不起，登录失败");
        }
        //关闭连接
        resultSet.close();
        statement.close();
        connection.close();
    }
}
```

25.6 PreparedStatement

25.6.1 基本介绍  
![](https://img-blog.csdnimg.cn/24c9faddff37466b9aadf3ad8754af12.png)  
25.6.2 预处理好处  
![](https://img-blog.csdnimg.cn/ba24d68642984d5c886578e5a5bea040.png)  
PreparedStatement 发送给 MySQL 的语句是编译过的，所以 MySQL 不用再编译，可以直接执行。

25.6.3 应用案例  
![](https://img-blog.csdnimg.cn/f926baed7e1b456a8726d405cadee546.png)  
PreparedStatement_.java

```
package com.hspedu.jdbc.preparedstatement_;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.sql.*;
import java.util.Properties;
import java.util.Scanner;
/**
 * 演示PreparedStatement使用
 */
@SuppressWarnings({"all"})
public class PreparedStatement_ {
    public static void main(String[] args) throws Exception {
        //看 PreparedStatement类图
        Scanner scanner = new Scanner(System.in);
        //让用户输入管理员名和密码
        System.out.print("请输入管理员的名字: ");  //next(): 当接收到 空格或者 '就是表示结束
        String admin_name = scanner.nextLine(); // 老师说明，如果希望看到SQL注入，这里需要用nextLine
        System.out.print("请输入管理员的密码: ");
        String admin_pwd = scanner.nextLine();
        //通过Properties对象获取配置文件的信息
        Properties properties = new Properties();
        properties.load(new FileInputStream("src\\mysql.properties"));
        //获取相关的值
        String user = properties.getProperty("user");
        String password = properties.getProperty("password");
        String driver = properties.getProperty("driver");
        String url = properties.getProperty("url");
        //1. 注册驱动
        Class.forName(driver);//建议写上
        //2. 得到连接
        Connection connection = DriverManager.getConnection(url, user, password);
        //3. 得到PreparedStatement
        //3.1 组织SqL , Sql 语句的 ? 就相当于占位符
        String sql = "select name , pwd  from admin where name =? and pwd = ?";
        //3.2 preparedStatement 对象实现了 PreparedStatement 接口的实现类的对象
        PreparedStatement preparedStatement = connection.prepareStatement(sql);
        //3.3 给 ? 赋值
        preparedStatement.setString(1, admin_name);
        preparedStatement.setString(2, admin_pwd);
        //4. 执行 select 语句使用  executeQuery
        //   如果执行的是 dml(update, insert ,delete) executeUpdate()
        //   这里执行 executeQuery ,不要再写 sql
        ResultSet resultSet = preparedStatement.executeQuery(sql);
        if (resultSet.next()) { //如果查询到一条记录，则说明该管理存在
            System.out.println("恭喜， 登录成功");
        } else {
            System.out.println("对不起，登录失败");
        }
        //关闭连接
        resultSet.close();
        preparedStatement.close();
        connection.close();
    }
}
```

PreparedStatementDML_.java

```
package com.hspedu.jdbc.preparedstatement_;
import java.io.FileInputStream;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.util.Properties;
import java.util.Scanner;
/**
 * 演示PreparedStatement使用 dml语句
 */
@SuppressWarnings({"all"})
public class PreparedStatementDML_ {
    public static void main(String[] args) throws Exception {
        //看 PreparedStatement类图
        Scanner scanner = new Scanner(System.in);
        //让用户输入管理员名和密码
        System.out.print("请输删除管理员的名字: ");  //next(): 当接收到 空格或者 '就是表示结束
        String admin_name = scanner.nextLine(); // 老师说明，如果希望看到SQL注入，这里需要用nextLine
//        System.out.print("请输入管理员的新密码: ");
//        String admin_pwd = scanner.nextLine();
        //通过Properties对象获取配置文件的信息
        Properties properties = new Properties();
        properties.load(new FileInputStream("src\\mysql.properties"));
        //获取相关的值
        String user = properties.getProperty("user");
        String password = properties.getProperty("password");
        String driver = properties.getProperty("driver");
        String url = properties.getProperty("url");
        //1. 注册驱动
        Class.forName(driver);//建议写上
        //2. 得到连接
        Connection connection = DriverManager.getConnection(url, user, password);
        //3. 得到PreparedStatement
        //3.1 组织SqL , Sql 语句的 ? 就相当于占位符
        //添加记录
        //String sql = "insert into admin values(?, ?)";
        //String sql = "update admin set pwd = ? where name = ?";
        String sql = "delete from  admin where name = ?";
        //3.2 preparedStatement 对象实现了 PreparedStatement 接口的实现类的对象
        PreparedStatement preparedStatement = connection.prepareStatement(sql);
        //3.3 给 ? 赋值
        preparedStatement.setString(1, admin_name);
        //preparedStatement.setString(2, admin_name);
        //4. 执行 dml 语句使用  executeUpdate
        int rows = preparedStatement.executeUpdate();
        System.out.println(rows > 0 ? "执行成功" : "执行失败");
        //关闭连接
        preparedStatement.close();
        connection.close();
    }
}
```

25.7 JDBC 的相关 API 小结  
![](https://img-blog.csdnimg.cn/3111e592f9e94165a2d1089d1c6f3686.png)  
![](https://img-blog.csdnimg.cn/09e933e356f74d129f8a9e8c27a1aab9.png)  
25.8 封装 JDBCUtils 【关闭连接, 得到连接】  
![](https://img-blog.csdnimg.cn/9808688a6b1b4d2abbf8aa0c746e5f64.png)  
![](https://img-blog.csdnimg.cn/40ccc41883c2464eaaa145de99c94c8e.png)  
JDBCUtils.java

```
package com.hspedu.jdbc.utils;
import java.io.FileInputStream;
import java.io.IOException;
import java.sql.*;
import java.util.Properties;
/**
 * 这是一个工具类，完成 mysql的连接和关闭资源
 */
public class JDBCUtils {
    //定义相关的属性(4个), 因为只需要一份，因此，我们做出static
    private static String user; //用户名
    private static String password; //密码
    private static String url; //url
    private static String driver; //驱动名
    //在static代码块去初始化
    static {
        try {
            Properties properties = new Properties();
            properties.load(new FileInputStream("src\\mysql.properties"));
            //读取相关的属性值
            user = properties.getProperty("user");
            password = properties.getProperty("password");
            url = properties.getProperty("url");
            driver = properties.getProperty("driver");
        } catch (IOException e) {
            //在实际开发中，我们可以这样处理
            //1. 将编译异常转成 运行异常
            //2. 调用者，可以选择捕获该异常，也可以选择默认处理该异常，比较方便.
            throw new RuntimeException(e);
        }
    }
    //连接数据库, 返回Connection
    public static Connection getConnection() {
        try {
            return DriverManager.getConnection(url, user, password);
        } catch (SQLException e) {
            //1. 将编译异常转成 运行异常
            //2. 调用者，可以选择捕获该异常，也可以选择默认处理该异常，比较方便.
            throw new RuntimeException(e);
        }
    }
    //关闭相关资源
    /*
        1. ResultSet 结果集
        2. Statement 或者 PreparedStatement
        3. Connection
        4. 如果需要关闭资源，就传入对象，否则传入 null
     */
    public static void close(ResultSet set, Statement statement, Connection connection) {
        //判断是否为null
        try {
            if (set != null) {
                set.close();
            }
            if (statement != null) {
                statement.close();
            }
            if (connection != null) {
                connection.close();
            }
        } catch (SQLException e) {
            //将编译异常转成运行异常抛出
            throw new RuntimeException(e);
        }
    }
}
```

JDBCUtils_Use.java

```
package com.hspedu.jdbc.utils;
import org.junit.jupiter.api.Test;
import java.sql.*;
/**
 * 该类演示如何使用JDBCUtils工具类，完成dml 和 select
 */
public class JDBCUtils_Use {
    @Test
    public void testSelect() {
        //1. 得到连接
        Connection connection = null;
        //2. 组织一个sql
        String sql = "select * from actor where id = ?";
        PreparedStatement preparedStatement = null;
        ResultSet set = null;
        //3. 创建PreparedStatement 对象
        try {
            connection = JDBCUtils.getConnection();
            System.out.println(connection.getClass()); //com.mysql.jdbc.JDBC4Connection
            preparedStatement = connection.prepareStatement(sql);
            preparedStatement.setInt(1, 5);//给?号赋值
            //执行, 得到结果集
            set = preparedStatement.executeQuery();
            //遍历该结果集
            while (set.next()) {
                int id = set.getInt("id");
                String name = set.getString("name");
                String sex = set.getString("sex");
                Date borndate = set.getDate("borndate");
                String phone = set.getString("phone");
                System.out.println(id + "\t" + name + "\t" + sex + "\t" + borndate + "\t" + phone);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            //关闭资源
            JDBCUtils.close(set, preparedStatement, connection);
        }
    }
    @Test
    public void testDML() {//insert , update, delete
        //1. 得到连接
        Connection connection = null;
        //2. 组织一个sql
        String sql = "update actor set name = ? where id = ?";
        // 测试 delete 和 insert ,自己玩.
        PreparedStatement preparedStatement = null;
        //3. 创建PreparedStatement 对象
        try {
            connection = JDBCUtils.getConnection();
            preparedStatement = connection.prepareStatement(sql);
            //给占位符赋值
            preparedStatement.setString(1, "周星驰");
            preparedStatement.setInt(2, 4);
            //执行
            preparedStatement.executeUpdate();
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            //关闭资源
            JDBCUtils.close(null, preparedStatement, connection);
        }
    }
}
```

25.9 事务

25.9.1 基本介绍  
![](https://img-blog.csdnimg.cn/9c86e74e0b0a45e5b68b77ab434fb8dc.png)  
25.9.2 应用实例  
![](https://img-blog.csdnimg.cn/3796d9ab1d8045d99afc7122791f54d4.png)

```
package com.hspedu.jdbc.transaction_;
import com.hspedu.jdbc.utils.JDBCUtils;
import org.junit.jupiter.api.Test;
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.SQLException;
/**
 * 演示jdbc 中如何使用事务
 */
public class Transaction_ {
    //没有使用事务.
    @Test
    public void noTransaction() {
        //操作转账的业务
        //1. 得到连接
        Connection connection = null;
        //2. 组织一个sql
        String sql = "update account set balance = balance - 100 where id = 1";
        String sql2 = "update account set balance = balance + 100 where id = 2";
        PreparedStatement preparedStatement = null;
        //3. 创建PreparedStatement 对象
        try {
            connection = JDBCUtils.getConnection(); // 在默认情况下，connection是默认自动提交
            preparedStatement = connection.prepareStatement(sql);
            preparedStatement.executeUpdate(); // 执行第1条sql
            int i = 1 / 0; //抛出异常
            preparedStatement = connection.prepareStatement(sql2);
            preparedStatement.executeUpdate(); // 执行第3条sql
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            //关闭资源
            JDBCUtils.close(null, preparedStatement, connection);
        }
    }
    //事务来解决
    @Test
    public void useTransaction() {
        //操作转账的业务
        //1. 得到连接
        Connection connection = null;
        //2. 组织一个sql
        String sql = "update account set balance = balance - 100 where id = 1";
        String sql2 = "update account set balance = balance + 100 where id = 2";
        PreparedStatement preparedStatement = null;
        //3. 创建PreparedStatement 对象
        try {
            connection = JDBCUtils.getConnection(); // 在默认情况下，connection是默认自动提交
            //将 connection 设置为不自动提交
            connection.setAutoCommit(false); //开启了事务
            preparedStatement = connection.prepareStatement(sql);
            preparedStatement.executeUpdate(); // 执行第1条sql
            int i = 1 / 0; //抛出异常
            preparedStatement = connection.prepareStatement(sql2);
            preparedStatement.executeUpdate(); // 执行第2条sql
            //这里提交事务
            connection.commit();
        } catch (SQLException e) {
            //这里我们可以进行回滚，即撤销执行的SQL
            //默认回滚到事务开始的状态.
            System.out.println("执行发生了异常，撤销执行的sql");
            try {
                connection.rollback();
            } catch (SQLException throwables) {
                throwables.printStackTrace();
            }
            e.printStackTrace();
        } finally {
            //关闭资源
            JDBCUtils.close(null, preparedStatement, connection);
        }
    }
}
```

25.10 批处理

25.10.1 基本介绍  
![](https://img-blog.csdnimg.cn/9c89cfd06dac4041899036ef71fc54c3.png)  
25.10.2 应用实例  
![](https://img-blog.csdnimg.cn/b1dabf5a47a04e3d96dffea1d067e677.png)

```
package com.hspedu.jdbc.batch_;
import com.hspedu.jdbc.utils.JDBCUtils;
import org.junit.jupiter.api.Test;
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.SQLException;
/**
 * 演示java的批处理
 */
public class Batch_ {
    //传统方法，添加5000条数据到admin2
    @Test
    public void noBatch() throws Exception {
        Connection connection = JDBCUtils.getConnection();
        String sql = "insert into admin2 values(null, ?, ?)";
        PreparedStatement preparedStatement = connection.prepareStatement(sql);
        System.out.println("开始执行");
        long start = System.currentTimeMillis();//开始时间
        for (int i = 0; i < 5000; i++) {//5000执行
            preparedStatement.setString(1, "jack" + i);
            preparedStatement.setString(2, "666");
            preparedStatement.executeUpdate();
        }
        long end = System.currentTimeMillis();
        System.out.println("传统的方式 耗时=" + (end - start));//传统的方式 耗时=10702
        //关闭连接
        JDBCUtils.close(null, preparedStatement, connection);
    }
    //使用批量方式添加数据
    @Test
    public void batch() throws Exception {
        Connection connection = JDBCUtils.getConnection();
        String sql = "insert into admin2 values(null, ?, ?)";
        PreparedStatement preparedStatement = connection.prepareStatement(sql);
        System.out.println("开始执行");
        long start = System.currentTimeMillis();//开始时间
        for (int i = 0; i < 5000; i++) {//5000执行
            preparedStatement.setString(1, "jack" + i);
            preparedStatement.setString(2, "666");
            //将sql 语句加入到批处理包中 -> 看源码
            /*
            //1. //第一就创建 ArrayList - elementData => Object[]
            //2. elementData => Object[] 就会存放我们预处理的sql语句
            //3. 当elementData满后,就按照1.5扩容
            //4. 当添加到指定的值后，就executeBatch
            //5. 批量处理会减少我们发送sql语句的网络开销，而且减少编译次数，因此效率提高
            public void addBatch() throws SQLException {
                synchronized(this.checkClosed().getConnectionMutex()) {
                    if (this.batchedArgs == null) {
                        this.batchedArgs = new ArrayList();
                    }
                    for(int i = 0; i < this.parameterValues.length; ++i) {
                        this.checkAllParametersSet(this.parameterValues[i], this.parameterStreams[i], i);
                    }
                    this.batchedArgs.add(new PreparedStatement.BatchParams(this.parameterValues, this.parameterStreams, this.isStream, this.streamLengths, this.isNull));
                }
            }
             */
            preparedStatement.addBatch();
            //当有1000条记录时，再批量执行
            if((i + 1) % 1000 == 0) {//满1000条sql
                preparedStatement.executeBatch();
                //清空一把
                preparedStatement.clearBatch();
            }
        }
        long end = System.currentTimeMillis();
        System.out.println("批量方式 耗时=" + (end - start));//批量方式 耗时=108
        //关闭连接
        JDBCUtils.close(null, preparedStatement, connection);
    }
}
```

![](https://img-blog.csdnimg.cn/26477f60475140b4af2d8da74809c576.png)  
25.11 数据库连接池

25.11.1 传统获取 Connection 问题分析  
![](https://img-blog.csdnimg.cn/16e3a266ca9841138172d18be60e4986.png)  
25.11.1 数据库连接池基本介绍  
![](https://img-blog.csdnimg.cn/4ff5ac3f530c4638b7f92fb2a11d5ef8.png)  
![](https://img-blog.csdnimg.cn/455582065fe949f1a504b87c371f2e1b.png)  
25.11.3 数据库连接池种类  
![](https://img-blog.csdnimg.cn/4ba50f4fc5c34c838d675765b4389e3d.png)  
25.11.4 C3P0 应用实例  
![](https://img-blog.csdnimg.cn/6c8f62abd4e64fdcbcde6822ab81953a.png)  
![](https://img-blog.csdnimg.cn/631cf81e4e3a4f8f9a41baaad7788c95.png)  
C3P0_.java

```
package com.hspedu.jdbc.datasource;
import com.mchange.v2.c3p0.ComboPooledDataSource;
import org.junit.jupiter.api.Test;
import java.io.FileInputStream;
import java.sql.Connection;
import java.sql.SQLException;
import java.util.Properties;
/**
 * 演示c3p0的使用
 */
public class C3P0_ {
    //方式1： 相关参数，在程序中指定user, url , password等
    @Test
    public void testC3P0_01() throws Exception {
        //1. 创建一个数据源对象
        ComboPooledDataSource comboPooledDataSource = new ComboPooledDataSource();
        //2. 通过配置文件mysql.properties 获取相关连接的信息
        Properties properties = new Properties();
        properties.load(new FileInputStream("src\\mysql.properties"));
        //读取相关的属性值
        String user = properties.getProperty("user");
        String password = properties.getProperty("password");
        String url = properties.getProperty("url");
        String driver = properties.getProperty("driver");
        
        //给数据源 comboPooledDataSource 设置相关的参数
        //注意：连接管理是由 comboPooledDataSource 来管理
        comboPooledDataSource.setDriverClass(driver);
        comboPooledDataSource.setJdbcUrl(url);
        comboPooledDataSource.setUser(user);
        comboPooledDataSource.setPassword(password);

        //设置初始化连接数
        comboPooledDataSource.setInitialPoolSize(10);
        //最大连接数
        comboPooledDataSource.setMaxPoolSize(50);
        //测试连接池的效率, 测试对mysql 5000次操作
        long start = System.currentTimeMillis();
        for (int i = 0; i < 5000; i++) {
            Connection connection = comboPooledDataSource.getConnection(); //这个方法就是从 DataSource 接口实现的
            //System.out.println("连接OK");
            connection.close();
            //这里不是关闭，连接池重写了关闭方法，功能是回收连接！！
        }
        long end = System.currentTimeMillis();
        //c3p0 5000连接mysql 耗时=391
        System.out.println("c3p0 5000连接mysql 耗时=" + (end - start));
    }

    //第二种方式 使用配置文件模板来完成
    //1. 将c3p0 提供的 c3p0.config.xml 拷贝到 src目录下
    //2. 该文件指定了连接数据库和连接池的相关参数
    @Test
    public void testC3P0_02() throws SQLException {
        ComboPooledDataSource comboPooledDataSource = new ComboPooledDataSource("hsp_edu");
        //测试5000次连接mysql
        long start = System.currentTimeMillis();
        System.out.println("开始执行....");
        for (int i = 0; i < 500000; i++) {
            Connection connection = comboPooledDataSource.getConnection();
            //System.out.println("连接OK~");
            connection.close();
        }
        long end = System.currentTimeMillis();
        //c3p0的第二种方式 耗时=413
        System.out.println("c3p0的第二种方式(500000) 耗时=" + (end - start));//1917
    }
}
```

c3p0-config.xml

```
<c3p0-config>
    <!-- 数据源名称代表连接池 -->
  <named-config >
<!-- 驱动类 -->
  <property >com.mysql.jdbc.Driver</property>
  <!-- url-->
  	<property >jdbc:mysql://127.0.0.1:3306/hsp_db02</property>
  <!-- 用户名 -->
  		<property >root</property>
  		<!-- 密码 -->
  	<property >hsp</property>
  	<!-- 每次增长的连接数-->
    <property >5</property>
    <!-- 初始的连接数 -->
    <property >10</property>
    <!-- 最小连接数 -->
    <property >5</property>
    <!-- 最大连接数 -->
    <property >50</property>
	<!-- 可连接的最多的命令对象数 -->
    <property >5</property> 
    <!-- 每个连接对象可连接的最多的命令对象数 -->
    <property >2</property>
  </named-config>
</c3p0-config>
```

25.11.5 Druid(德鲁伊) 应用实例  
![](https://img-blog.csdnimg.cn/a546c47801034a52a5cd0e7935678d29.png)

```
package com.hspedu.jdbc.datasource;
import com.alibaba.druid.pool.DruidDataSourceFactory;
import org.junit.jupiter.api.Test;
import javax.sql.DataSource;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.sql.Connection;
import java.util.Properties;
/**
 * 测试druid的使用
 */
public class Druid_ {
    @Test
    public void testDruid() throws Exception {
        //1. 加入 Druid jar包
        //2. 加入 配置文件 druid.properties , 将该文件拷贝项目的src目录
        //3. 创建Properties对象, 读取配置文件
        Properties properties = new Properties();
        properties.load(new FileInputStream("src\\druid.properties"));
        //4. 创建一个指定参数的数据库连接池, Druid连接池
        DataSource dataSource =
                DruidDataSourceFactory.createDataSource(properties);
        long start = System.currentTimeMillis();
        for (int i = 0; i < 500000; i++) {
            Connection connection = dataSource.getConnection();
            System.out.println(connection.getClass());
            //System.out.println("连接成功!");
            connection.close();
        }
        long end = System.currentTimeMillis();
        //druid连接池 操作5000 耗时=412
        System.out.println("druid连接池 操作500000 耗时=" + (end - start));//539
    }
}
```

25.11.6 将 JDBCUtils 工具类改成 Druid(德鲁伊) 实现  
![](https://img-blog.csdnimg.cn/ee40be10e8694422acdd07afdfa342a1.png)  
JDBCUtilsByDruid.java

```
package com.hspedu.jdbc.datasource;
import com.alibaba.druid.pool.DruidDataSourceFactory;
import javax.sql.DataSource;
import java.io.FileInputStream;
import java.io.IOException;
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.Properties;
/**
 * 基于druid数据库连接池的工具类
 */
public class JDBCUtilsByDruid {
    private static DataSource ds;
    //在静态代码块完成 ds初始化
    static {
        Properties properties = new Properties();
        try {
            properties.load(new FileInputStream("src\\druid.properties"));
            ds = DruidDataSourceFactory.createDataSource(properties);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
    //编写getConnection方法
    public static Connection getConnection() throws SQLException {
        return ds.getConnection();
    }
    //关闭连接, 老师再次强调： 在数据库连接池技术中，close 不是真的断掉连接
    //而是把使用的Connection对象放回连接池
    public static void close(ResultSet resultSet, Statement statement, Connection connection) {
        try {
            if (resultSet != null) {
                resultSet.close();
            }
            if (statement != null) {
                statement.close();
            }
            if (connection != null) {
                connection.close();
            }
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }
    }
}
```

JDBCUtilsByDruid_USE.java

```
package com.hspedu.jdbc.datasource;


import org.junit.jupiter.api.Test;
import java.sql.*;
import java.util.ArrayList;
@SuppressWarnings({"all"})
public class JDBCUtilsByDruid_USE {
    @Test
    public void testSelect() {
        System.out.println("使用 druid方式完成");
        //1. 得到连接
        Connection connection = null;
        //2. 组织一个sql
        String sql = "select * from actor where id >= ?";
        PreparedStatement preparedStatement = null;
        ResultSet set = null;
        //3. 创建PreparedStatement 对象
        try {
            connection = JDBCUtilsByDruid.getConnection();
            System.out.println(connection.getClass());//运行类型 com.alibaba.druid.pool.DruidPooledConnection
            preparedStatement = connection.prepareStatement(sql);
            preparedStatement.setInt(1, 1);//给?号赋值
            //执行, 得到结果集
            set = preparedStatement.executeQuery();
            //遍历该结果集
            while (set.next()) {
                int id = set.getInt("id");
                String name = set.getString("name");//getName()
                String sex = set.getString("sex");//getSex()
                Date borndate = set.getDate("borndate");
                String phone = set.getString("phone");
                System.out.println(id + "\t" + name + "\t" + sex + "\t" + borndate + "\t" + phone);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            //关闭资源
            JDBCUtilsByDruid.close(set, preparedStatement, connection);
        }
    }
}
```

25.12 Apache—DBUtils

25.12.1 先分析一个问题  
![](https://img-blog.csdnimg.cn/189b2c5e44244665a51133b1ed955341.png)  
![](https://img-blog.csdnimg.cn/15ed0728dc03426eba7da7a74b76234f.png)  
25.12.2 用自己的土方法来解决

```
//使用老师的土方法来解决ResultSet =封装=> Arraylist
    @Test
    public ArrayList<Actor> testSelectToArrayList() {
        System.out.println("使用 druid方式完成");
        //1. 得到连接
        Connection connection = null;
        //2. 组织一个sql
        String sql = "select * from actor where id >= ?";
        PreparedStatement preparedStatement = null;
        ResultSet set = null;
        ArrayList<Actor> list = new ArrayList<>();//创建ArrayList对象,存放actor对象
        //3. 创建PreparedStatement 对象
        try {
            connection = JDBCUtilsByDruid.getConnection();
            System.out.println(connection.getClass());//运行类型 com.alibaba.druid.pool.DruidPooledConnection
            preparedStatement = connection.prepareStatement(sql);
            preparedStatement.setInt(1, 1);//给?号赋值
            //执行, 得到结果集
            set = preparedStatement.executeQuery();
            //遍历该结果集
            while (set.next()) {
                int id = set.getInt("id");
                String name = set.getString("name");//getName()
                String sex = set.getString("sex");//getSex()
                Date borndate = set.getDate("borndate");
                String phone = set.getString("phone");
                //把得到的resultset 的记录，封装到 Actor对象，放入到list集合
                list.add(new Actor(id, name, sex, borndate, phone));
            }
            System.out.println("list集合数据=" + list);
            for(Actor actor : list) {
                System.out.println("id=" + actor.getId() + "\t" + actor.getName());
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            //关闭资源
            JDBCUtilsByDruid.close(set, preparedStatement, connection);
        }
        //因为ArrayList 和 connection 没有任何关联，所以该集合可以复用.
        return  list;
    }
```

JUnit 如果有返回值，中间的 sout 就不会输出结果。

25.12.3 基本介绍  
![](https://img-blog.csdnimg.cn/91f86ef6517a48689b2ee2b9ccc49add.png)  
25.12.4 应用实例  
![](https://img-blog.csdnimg.cn/d13584ee9a3843528374173197ec545f.png)  
![](https://img-blog.csdnimg.cn/25753a8668b8436fa8a2bee8d16fe201.png)

```
package com.hspedu.jdbc.datasource;
import org.apache.commons.dbutils.QueryRunner;
import org.apache.commons.dbutils.handlers.BeanHandler;
import org.apache.commons.dbutils.handlers.BeanListHandler;
import org.apache.commons.dbutils.handlers.ScalarHandler;
import org.junit.jupiter.api.Test;
import java.sql.*;
import java.util.ArrayList;
import java.util.List;
@SuppressWarnings({"all"})
public class DBUtils_USE {
    //使用apache-DBUtils 工具类 + druid 完成对表的crud操作
    @Test
    public void testQueryMany() throws SQLException { //返回结果是多行的情况
        //1. 得到 连接 (druid)
        Connection connection = JDBCUtilsByDruid.getConnection();
        //2. 使用 DBUtils 类和接口 , 先引入DBUtils 相关的jar , 加入到本Project
        //3. 创建 QueryRunner
        QueryRunner queryRunner = new QueryRunner();
        //4. 就可以执行相关的方法，返回ArrayList 结果集
        //String sql = "select * from actor where id >= ?";
        //   注意: sql 语句也可以查询部分列
        String sql = "select id, name from actor where id >= ?";
        // 老韩解读
        //(1) query 方法就是执行sql 语句，得到resultset ---封装到 --> ArrayList 集合中
        //(2) 返回集合
        //(3) connection: 连接
        //(4) sql : 执行的sql语句
        //(5) new BeanListHandler<>(Actor.class): 将resultset -> Actor 对象 -> 封装到 ArrayList
        //    底层使用反射机制 去获取Actor 类的属性，然后进行封装
        //(6) 1 就是给 sql 语句中的? 赋值，可以有多个值，因为是可变参数  Object... params
        //(7) 底层得到的resultset ,会在query 关闭, 同时也会关闭PreparedStatment
        /**
         * 分析 queryRunner.query方法:
         * public <T> T query(Connection conn, String sql, ResultSetHandler<T> rsh, Object... params) throws SQLException {
         *         PreparedStatement stmt = null;//定义PreparedStatement
         *         ResultSet rs = null;//接收返回的 ResultSet
         *         Object result = null;//返回ArrayList
         *         try {
         *             stmt = this.prepareStatement(conn, sql);//创建PreparedStatement
         *             this.fillStatement(stmt, params);//对sql 进行 ? 赋值
         *             rs = this.wrap(stmt.executeQuery());//执行sql,返回resultset
         *             result = rsh.handle(rs);//返回的resultset --> arrayList[result] [使用到反射，对传入class对象处理]
         *         } catch (SQLException var33) {
         *             this.rethrow(var33, sql, params);
         *         } finally {
         *             try {
         *                 this.close(rs);//关闭resultset
         *             } finally {
         *                 this.close((Statement)stmt);//关闭preparedstatement对象
         *             }
         *         }
         *         return result;
         *     }
         */
        List<Actor> list =
                queryRunner.query(connection, sql, new BeanListHandler<>(Actor.class), 1);
        System.out.println("输出集合的信息");
        for (Actor actor : list) {
            System.out.print(actor);
        }
        //释放资源
        JDBCUtilsByDruid.close(null, null, connection);
    }

    //演示 apache-dbutils + druid 完成 返回的结果是单行记录(单个对象)
    @Test
    public void testQuerySingle() throws SQLException {
        //1. 得到 连接 (druid)
        Connection connection = JDBCUtilsByDruid.getConnection();
        //2. 使用 DBUtils 类和接口 , 先引入DBUtils 相关的jar , 加入到本Project
        //3. 创建 QueryRunner
        QueryRunner queryRunner = new QueryRunner();
        //4. 就可以执行相关的方法，返回单个对象
        String sql = "select * from actor where id = ?";
        // 老韩解读
        // 因为我们返回的单行记录<--->单个对象 , 使用的Hander 是 BeanHandler
        Actor actor = queryRunner.query(connection, sql, new BeanHandler<>(Actor.class), 10);
        System.out.println(actor);
        // 释放资源
        JDBCUtilsByDruid.close(null, null, connection);
    }
    
    //演示apache-dbutils + druid 完成查询结果是单行单列-返回的就是object
    @Test
    public void testScalar() throws SQLException {	//scalar 在java中往往表示单行单列的那个值
        //1. 得到 连接 (druid)
        Connection connection = JDBCUtilsByDruid.getConnection();
        //2. 使用 DBUtils 类和接口 , 先引入DBUtils 相关的jar , 加入到本Project
        //3. 创建 QueryRunner
        QueryRunner queryRunner = new QueryRunner();
        //4. 就可以执行相关的方法，返回单行单列 , 返回的就是Object
        String sql = "select name from actor where id = ?";
        //老师解读： 因为返回的是一个对象, 使用的handler 就是 ScalarHandler
        Object obj = queryRunner.query(connection, sql, new ScalarHandler(), 4);
        System.out.println(obj);
        // 释放资源
        JDBCUtilsByDruid.close(null, null, connection);
    }

    //演示apache-dbutils + druid 完成 dml (update, insert ,delete)
    @Test
    public void testDML() throws SQLException {
        //1. 得到 连接 (druid)
        Connection connection = JDBCUtilsByDruid.getConnection();
        //2. 使用 DBUtils 类和接口 , 先引入DBUtils 相关的jar , 加入到本Project
        //3. 创建 QueryRunner
        QueryRunner queryRunner = new QueryRunner();
        //4. 这里组织sql 完成 update, insert delete
        //String sql = "update actor set name = ? where id = ?";
        //String sql = "insert into actor values(null, ?, ?, ?, ?)";
        String sql = "delete from actor where id = ?";
        //老韩解读
        //(1) 执行dml 操作是 queryRunner.update()
        //(2) 返回的值是受影响的行数 (affected: 受影响)
        //int affectedRow = queryRunner.update(connection, sql, "林青霞", "女", "1966-10-10", "116");
        int affectedRow = queryRunner.update(connection, sql, 1000 );
        System.out.println(affectedRow > 0 ? "执行成功" : "执行没有影响到表");
        // 释放资源
        JDBCUtilsByDruid.close(null, null, connection);
    }
}
```

25.12.5 表和 JavaBean 的类型映射关系  
![](https://img-blog.csdnimg.cn/7a155ae9b9d24bf1b82f049a14985549.png)

25.13 DAO 和增删改查通用方法 - BasicDao

25.13.1 先分析一个问题  
![](https://img-blog.csdnimg.cn/b719887c054c4aad9fa88d98fab932ad.png)  
![](https://img-blog.csdnimg.cn/d0e00e756bd049a9b247852fc1040165.png)  
![](https://img-blog.csdnimg.cn/1438dc6f7a2d41cf80e7670b89b054c7.png)

25.13.2 基本说明  
![](https://img-blog.csdnimg.cn/f1cca4f15fca4577919cc7d280f9b6b5.png)  
25.13.3 BasicDAO 应用实例  
![](https://img-blog.csdnimg.cn/d908f048d2b64cfd93415bb0e7e7677a.png)  
com.hspedu.dao_.dao.BasicDAO.java

```
package com.hspedu.dao_.dao;
import com.hspedu.dao_.utils.JDBCUtilsByDruid;
import org.apache.commons.dbutils.QueryRunner;
import org.apache.commons.dbutils.handlers.BeanHandler;
import org.apache.commons.dbutils.handlers.BeanListHandler;
import org.apache.commons.dbutils.handlers.ScalarHandler;
import java.sql.Connection;
import java.sql.SQLException;
import java.util.List;
/**
 * 开发BasicDAO , 是其他DAO的父类
 */
public class BasicDAO<T> { //泛型指定具体类型
    private QueryRunner qr =  new QueryRunner();
    //开发通用的dml方法, 针对任意的表
    public int update(String sql, Object... parameters) {
        Connection connection = null;
        try {
            connection = JDBCUtilsByDruid.getConnection();
            int update = qr.update(connection, sql, parameters);
            return  update;
        } catch (SQLException e) {
           throw  new RuntimeException(e); //将编译异常->运行异常 ,抛出
        } finally {
            JDBCUtilsByDruid.close(null, null, connection);
        }
    }
    //返回多个对象(即查询的结果是多行), 针对任意表
    /**
     * @param sql sql 语句，可以有 ?
     * @param clazz 传入一个类的Class对象 比如 Actor.class
     * @param parameters 传入 ? 的具体的值，可以是多个
     * @return 根据Actor.class 返回对应的 ArrayList 集合
     */
    public List<T> queryMulti(String sql, Class<T> clazz, Object... parameters) {
        Connection connection = null;
        try {
            connection = JDBCUtilsByDruid.getConnection();
            return qr.query(connection, sql, new BeanListHandler<T>(clazz), parameters);
        } catch (SQLException e) {
            throw  new RuntimeException(e); //将编译异常->运行异常 ,抛出
        } finally {
            JDBCUtilsByDruid.close(null, null, connection);
        }
    }
    //查询单行结果 的通用方法
    public T querySingle(String sql, Class<T> clazz, Object... parameters) {
        Connection connection = null;
        try {
            connection = JDBCUtilsByDruid.getConnection();
            return  qr.query(connection, sql, new BeanHandler<T>(clazz), parameters);
        } catch (SQLException e) {
            throw  new RuntimeException(e); //将编译异常->运行异常 ,抛出
        } finally {
            JDBCUtilsByDruid.close(null, null, connection);
        }
    }
    //查询单行单列的方法,即返回单值的方法
    public Object queryScalar(String sql, Object... parameters) {
        Connection connection = null;
        try {
            connection = JDBCUtilsByDruid.getConnection();
            return  qr.query(connection, sql, new ScalarHandler(), parameters);
        } catch (SQLException e) {
            throw  new RuntimeException(e); //将编译异常->运行异常 ,抛出
        } finally {
            JDBCUtilsByDruid.close(null, null, connection);
        }
    }
}
```

com.hspedu.dao_.dao.ActorDAO.java

```
package com.hspedu.dao_.dao;
import com.hspedu.dao_.domain.Actor;
public class ActorDAO extends BasicDAO<Actor> {
    //1. 就有 BasicDAO 的方法
    //2. 根据业务需求，可以编写特有的方法.
}
```

com.hspedu.dao_.test.TestDAO.java

```
package com.hspedu.dao_.test;
import com.hspedu.dao_.dao.ActorDAO;
import com.hspedu.dao_.domain.Actor;
import org.junit.jupiter.api.Test;
import java.util.List;
public class TestDAO {
    //测试ActorDAO 对actor表crud操作
    @Test
    public void testActorDAO() {
        ActorDAO actorDAO = new ActorDAO();
        //1. 查询
        List<Actor> actors = actorDAO.queryMulti("select * from actor where id >= ?", Actor.class, 1);
        System.out.println("===查询结果===");
        for (Actor actor : actors) {
            System.out.println(actor);
        }
        //2. 查询单行记录
        Actor actor = actorDAO.querySingle("select * from actor where id = ?", Actor.class, 6);
        System.out.println("====查询单行结果====");
        System.out.println(actor);
        //3. 查询单行单列
        Object o = actorDAO.queryScalar("select name from actor where id = ?", 6);
        System.out.println("====查询单行单列值===");
        System.out.println(o);
        //4. dml操作  insert ,update, delete
        int update = actorDAO.update("insert into actor values(null, ?, ?, ?, ?)", "张无忌", "男", "2000-11-11", "999");
        System.out.println(update > 0 ? "执行成功" : "执行没有影响表");
    }
}
```

#### 第 27 章 [正则表达式](https://so.csdn.net/so/search?q=%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F&spm=1001.2101.3001.7020)

27.1 为什么要学习正则表达式  
![](https://img-blog.csdnimg.cn/5173cb1601434e2493e670a1771021e8.png)

```
package com.hspedu.regexp;
import java.util.regex.Matcher;
import java.util.regex.Pattern;
/**
 * 体验正则表达式的威力，给我们文本处理带来哪些便利
 */
public class Regexp_ {
    public static void main(String[] args) {
    	 String content = "私有地址（Private address）属于非注册地址，专门为组织机构内部使用。\n" +
                "以下列出留用的内部私有地址\n" +
                "A类 10.0.0.0--10.255.255.255\n" +
                "B类 172.16.0.0--172.31.255.255\n" +
                "C类 192.168.0.0--192.168.255.255";
        
        //提取文章中所有的英文单词
        //提取文章中所有的数字
        //提取文章中所有的英文单词和数字
        //提取百度热榜 标题
        //(1). 传统方法. 使用遍历方式，代码量大，效率不高
        //(2). 正则表达式技术
        
        //1. 先创建一个Pattern对象 ， 模式对象, 可以理解成就是一个正则表达式对象
        //Pattern pattern = Pattern.compile("[a-zA-Z]+");
        //Pattern pattern = Pattern.compile("[0-9]+");
        //Pattern pattern = Pattern.compile("([0-9]+)|([a-zA-Z]+)");
        //Pattern pattern = Pattern.compile("<a target=\"_blank\" title=\"(\\S*)\"");
        Pattern pattern = Pattern.compile("\\d+\\.\\d+\\.\\d+\\.\\d+");
        //2. 创建一个匹配器对象
        //理解： 就是 matcher 匹配器按照 pattern(模式/样式), 到 content 文本中去匹配
        //找到就返回true, 否则就返回false
        int no = 0;
        Matcher matcher = pattern.matcher(content);
        //3. 可以开始循环匹配
        while (matcher.find()) {
            //匹配内容，文本，放到 m.group(0)
            System.out.println("找到: " + (++no) + " " +matcher.group(0));
        }
    }
}
```

27.2 再提出几个问题?  
![](https://img-blog.csdnimg.cn/ed925b90b27e4a628d2469e2fe9235ad.png)  
![](https://img-blog.csdnimg.cn/55e9d12380d647b4b9a9df76d6482da4.png)  
27.3 解决之道 - 正则表达式  
![](https://img-blog.csdnimg.cn/b5a3422b336d46d78994bd6e4e11ca88.png)  
27.4 正则表达式基本介绍  
![](https://img-blog.csdnimg.cn/a832897c939f49fc90fb5bc4fe328f87.png)  
27.5 正则表达式底层实现（重要）  
![](https://img-blog.csdnimg.cn/29c8d4834f834dbe96980dde8ef75363.png)

```
package com.hspedu.regexp;
import java.util.regex.Matcher;
import java.util.regex.Pattern;
/**
 * 分析java的正则表达式的底层实现(重要.)
 */
public class RegTheory {
    public static void main(String[] args) {
        String content = "1998年12月8日，第二代Java平台的企业版J2EE发布。1999年6月，Sun公司发布了" +
                "第二代Java平台（简称为Java2）的3个版本：J2ME（Java2 Micro Edition，Java2平台的微型" +
                "版），应用于移动、无线及有限资源的环境；J2SE（Java 2 Standard Edition，Java 2平台的" +
                "标准版），应用于桌面环境；J2EE（Java 2Enterprise Edition，Java 2平台的企业版），应" +
                "用3443于基于Java的应用服务器。Java 2平台的发布，是Java发展过程中最重要的一个" +
                "里程碑，标志着Java的应用开始普及9889 ";
        //目标：匹配所有四个数字
        //说明
        //1. \\d 表示一个任意的数字
        String regStr = "(\\d\\d)(\\d\\d)";
        //2. 创建模式对象[即正则表达式对象]
        Pattern pattern = Pattern.compile(regStr);
        //3. 创建匹配器
        //说明：创建匹配器matcher， 按照 正则表达式的规则 去匹配 content字符串
        Matcher matcher = pattern.matcher(content);
        //4.开始匹配
        /**
         * matcher.find() 完成的任务 （考虑分组）
         * 什么是分组，比如  (\d\d)(\d\d) ,正则表达式中有() 表示分组,第1个()表示第1组,第2个()表示第2组...
         * 1. 根据指定的规则 ,定位满足规则的子字符串(比如(19)(98))
         * 2. 找到后，将 子字符串的开始的索引记录到 matcher对象的属性 int[] groups;
         *    2.1 groups[0] = 0 , 把该子字符串的结束的索引+1的值记录到 groups[1] = 4
         *    2.2 记录1组()匹配到的字符串 groups[2] = 0  groups[3] = 2
         *    2.3 记录2组()匹配到的字符串 groups[4] = 2  groups[5] = 4
         *    2.4.如果有更多的分组.....
         * 3. 同时记录oldLast 的值为 子字符串的结束的 索引+1的值即35, 即下次执行find时，就从35开始匹配
         *
         * matcher.group(0) 分析
         * 源码:
         * public String group(int group) {
         *         if (first < 0)
         *             throw new IllegalStateException("No match found");
         *         if (group < 0 || group > groupCount())
         *             throw new IndexOutOfBoundsException("No group " + group);
         *         if ((groups[group*2] == -1) || (groups[group*2+1] == -1))
         *             return null;
         *         return getSubSequence(groups[group * 2], groups[group * 2 + 1]).toString();
         *     }
         *  1. 根据 groups[0]=31 和 groups[1]=35 的记录的位置，从content开始截取子字符串返回
         *     就是 [31,35) 包含 31 但是不包含索引为 35的位置
         *
         *  如果再次指向 find方法.仍然安上面分析来执行
         */
        while (matcher.find()) {
            //小结
            //1. 如果正则表达式有() 即分组
            //2. 取出匹配的字符串规则如下
            //3. group(0) 表示匹配到的子字符串
            //4. group(1) 表示匹配到的子字符串的第一组字串
            //5. group(2) 表示匹配到的子字符串的第2组字串
            //6. ... 但是分组的数不能越界.
            System.out.println("找到: " + matcher.group(0));
            System.out.println("第1组()匹配到的值=" + matcher.group(1));
            System.out.println("第2组()匹配到的值=" + matcher.group(2));
        }
    }
}
```

![](https://img-blog.csdnimg.cn/937aa953bee84639b8072124b3089678.png)

27.6 正则表达式语法

27.6.1 基本介绍  
![](https://img-blog.csdnimg.cn/b90a9f0960634280903d3b048ff0fef6.png)  
27.6.2 元字符 (Metacharacter)- 转义号 \  
![](https://img-blog.csdnimg.cn/dbe6f72052114a81b4bf8b811cd50f34.png)  
![](https://img-blog.csdnimg.cn/b7e97c8412ab470ea90620739afb264c.png)

```
package com.hspedu.regexp;
import java.util.regex.Matcher;
import java.util.regex.Pattern;
/**
 * 演示转义字符的使用
 */
public class RegExp02 {
    public static void main(String[] args) {
        String content = "abc$(a.bc(123( )";
        //匹配( => \\(
        //匹配. => \\.
        //String regStr = "\\.";
        //String regStr = "\\d\\d\\d";
        String regStr = "\\d{3}";
        Pattern pattern = Pattern.compile(regStr);
        Matcher matcher = pattern.matcher(content);
        while (matcher.find()) {
            System.out.println("找到 " + matcher.group(0));
        }
    }
}
```

27.6.3 元字符 - 字符匹配符  
![](https://img-blog.csdnimg.cn/30927c878c6f43d4b231a39a1ac98537.png)  
![](https://img-blog.csdnimg.cn/14d264b15a034785b2aac3f6738c86e7.png)  
![](https://img-blog.csdnimg.cn/970717ebeeb742128dc3379d0862ef75.png)  
![](https://img-blog.csdnimg.cn/475caeae80a54c418a75a86b41575240.png)  
![](https://img-blog.csdnimg.cn/cdce015ff86049e78241ac67f13ce12d.png)

```
package com.hspedu.regexp;
import java.util.regex.Matcher;
import java.util.regex.Pattern;
/**
 * 演示字符匹配符 的使用
 */
public class RegExp03 {
    public static void main(String[] args) {
        String content = "a11c8abc _ABCy @";
        //String regStr = "[a-z]";//匹配 a-z之间任意一个字符
        //String regStr = "[A-Z]";//匹配 A-Z之间任意一个字符
        //String regStr = "abc";//匹配 abc 字符串[默认区分大小写]
        //String regStr = "(?i)abc";//匹配 abc 字符串[不区分大小写]
        //String regStr = "[0-9]";//匹配 0-9 之间任意一个字符
        //String regStr = "[^a-z]";//匹配 不在 a-z之间任意一个字符
        //String regStr = "[^0-9]";//匹配 不在 0-9之间任意一个字符
        //String regStr = "[abcd]";//匹配 在 abcd中任意一个字符
        //String regStr = "\\D";//匹配 不在 0-9的任意一个字符
        //String regStr = "\\w";//匹配 大小写英文字母, 数字，下划线
        //String regStr = "\\W";//匹配 等价于 [^a-zA-Z0-9_]
        //\\s 匹配任何空白字符(空格,制表符等)
        //String regStr = "\\s";
        //\\S 匹配任何非空白字符 ,和\\s刚好相反
        //String regStr = "\\S";
        //.  匹配出 \n 之外的所有字符,如果要匹配.本身则需要使用 \\.
        String regStr = ".";
        //说明
        //1. 当创建Pattern对象时，指定 Pattern.CASE_INSENSITIVE, 表示匹配是不区分字母大小写.
        Pattern pattern = Pattern.compile(regStr/*, Pattern.CASE_INSENSITIVE*/);
        Matcher matcher = pattern.matcher(content);
        while (matcher.find()) {
            System.out.println("找到 " + matcher.group(0));
        }
    }
}
```

27.6.4 元字符 - 选择匹配符  
![](https://img-blog.csdnimg.cn/c8a261e73e894cd695cc5ddcbcc812ec.png)

```
package com.hspedu.regexp;
import java.util.regex.Matcher;
import java.util.regex.Pattern;
/**
 * 选择匹配符
 */
public class RegExp04 {
    public static void main(String[] args) {
        String content = "hanshunping 韩 寒冷";
        String regStr = "han|韩|寒";
        Pattern pattern = Pattern.compile(regStr/*, Pattern.CASE_INSENSITIVE*/);
        Matcher matcher = pattern.matcher(content);
        while (matcher.find()) {
            System.out.println("找到 " + matcher.group(0));
        }
    }
}
```

27.6.5 元字符 - 限定符  
![](https://img-blog.csdnimg.cn/163ac48acfd14680af852063e2cbd9b0.png)  
![](https://img-blog.csdnimg.cn/a387dcca68e84313872b583a7cc372b6.png)  
![](https://img-blog.csdnimg.cn/b27b5c84043343feb3dc2afc9284b646.png)  
![](https://img-blog.csdnimg.cn/c32325e837eb4c4dbda1f41f635f6164.png)  
![](https://img-blog.csdnimg.cn/98e34e0d1364406789446f8f1b878ce5.png)

```
package com.hspedu.regexp;
import java.util.regex.Matcher;
import java.util.regex.Pattern;
/**
 * 演示限定符的使用
 */
public class RegExp05 {
    public static void main(String[] args) {
        String content = "a211111aaaaaahello";
        //a{3},1{4},\\d{2}
        //String regStr = "a{3}";// 表示匹配 aaa
        //String regStr = "1{4}";// 表示匹配 1111
        //String regStr = "\\d{2}";// 表示匹配 两位的任意数字字符
        //a{3,4},1{4,5},\\d{2,5}
        //细节：java匹配默认贪婪匹配，即尽可能匹配多的
        //String regStr = "a{3,4}"; //表示匹配 aaa 或者 aaaa
        //String regStr = "1{4,5}"; //表示匹配 1111 或者 11111
        //String regStr = "\\d{2,5}"; //匹配2位数或者3,4,5
        //1+
        //String regStr = "1+"; //匹配一个1或者多个1
        //String regStr = "\\d+"; //匹配一个数字或者多个数字
        //1*
        //String regStr = "1*"; //匹配0个1或者多个1
        //演示?的使用, 遵守贪婪匹配
        String regStr = "a1?"; //匹配 a 或者 a1
        Pattern pattern = Pattern.compile(regStr/*, Pattern.CASE_INSENSITIVE*/);
        Matcher matcher = pattern.matcher(content);
        while (matcher.find()) {
            System.out.println("找到 " + matcher.group(0));
        }
    }
}
```

![](https://img-blog.csdnimg.cn/3b255cc5b5634e67b47629cc23c255b8.png)

```
package com.hspedu.regexp;
import java.util.regex.Matcher;
import java.util.regex.Pattern;
/**
 * 非贪婪匹配
 */
public class RegExp09 {
    public static void main(String[] args) {
        String content = "hello111111 ok";
        //String regStr = "\\d+"; //默认是贪婪匹配
       // String regStr = "\\d+?"; //非贪婪匹配
        String regStr = "\\d+?"; //非贪婪匹配
        Pattern pattern = Pattern.compile(regStr);
        Matcher matcher = pattern.matcher(content);
        while (matcher.find()) {
            System.out.println("找到: " + matcher.group(0));
        }
    }
}
```

27.6.6 元字符 - 定位符  
![](https://img-blog.csdnimg.cn/da9b4409033b41afa76338a070d3a2c8.png)

```
package com.hspedu.regexp;
import java.util.regex.Matcher;
import java.util.regex.Pattern;
/**
 * 演示定位符的使用
 */
public class RegExp06 {
    public static void main(String[] args) {
        String content = "hanshunping sphan nnhan";
        //String content = "123-abc";
        //以至少1个数字开头，后接任意个小写字母的字符串
        //String regStr = "^[0-9]+[a-z]*";
        /*如果content="a123abc"，则匹配不到
          如果content="123abc12"，则匹配结果为123abc
		*/

        //以至少1个数字开头, 必须以至少一个小写字母结束
        //String regStr = "^[0-9]+\\-[a-z]+$";
		//如果content="123abc12"，则匹配不到

        //表示匹配边界的han[这里的边界是指：被匹配的字符串最后,
        // 也可以是空格的子字符串的后面]
        //String regStr = "han\\b";

        //和\\b的含义刚刚相反
        String regStr = "han\\B";
        Pattern pattern = Pattern.compile(regStr);
        Matcher matcher = pattern.matcher(content);
        while (matcher.find()) {
            System.out.println("找到=" + matcher.group(0));
        }
    }
}
```

27.6.7 分组  
![](https://img-blog.csdnimg.cn/f36fdf8bb0dc490098c1020ff32a0985.png)

```
package com.hspedu.regexp;
import java.util.regex.Matcher;
import java.util.regex.Pattern;
/**
 * 分组:
 */
public class RegExp07 {
    public static void main(String[] args) {
        String content = "hanshunping s7789 nn1189han";
        //下面就是非命名分组
        //说明
        // 1. matcher.group(0) 得到匹配到的字符串
        // 2. matcher.group(1) 得到匹配到的字符串的第1个分组内容
        // 3. matcher.group(2) 得到匹配到的字符串的第2个分组内容
        //String regStr = "(\\d\\d)(\\d\\d)";//匹配4个数字的字符串
        //命名分组： 即可以给分组取名
        String regStr = "(?<g1>\\d\\d)(?<g2>\\d\\d)";//匹配4个数字的字符串
        Pattern pattern = Pattern.compile(regStr);
        Matcher matcher = pattern.matcher(content);
        while (matcher.find()) {
            System.out.println("找到=" + matcher.group(0));
            System.out.println("第1个分组内容=" + matcher.group(1));
            System.out.println("第1个分组内容[通过组名]=" + matcher.group("g1"));
            System.out.println("第2个分组内容=" + matcher.group(2));
            System.out.println("第2个分组内容[通过组名]=" + matcher.group("g2"));
        }
    }
}
```

![](https://img-blog.csdnimg.cn/68021200b9164950927929d8bed2372a.png)  
![](https://img-blog.csdnimg.cn/5eba4c7f035448988f9a2cfc7f16c5aa.png)

```
package com.hspedu.regexp;
import java.util.regex.Matcher;
import java.util.regex.Pattern;
/**
 * 演示非捕获分组, 语法比较奇怪
 */
public class RegExp08 {
    public static void main(String[] args) {
        String content = "hello韩顺平教育 jack韩顺平老师 韩顺平同学hello韩顺平学生";
//        找到 韩顺平教育 、韩顺平老师、韩顺平同学 子字符串
        //String regStr = "韩顺平教育|韩顺平老师|韩顺平同学";
        //上面的写法可以等价非捕获分组, 注意：不能 matcher.group(1)
        //String regStr = "韩顺平(?:教育|老师|同学)";

        //找到 韩顺平 这个关键字,但是要求只是查找韩顺平教育和 韩顺平老师 中包含有的韩顺平
        //下面也是非捕获分组，不能使用 matcher.group(1)
        //String regStr = "韩顺平(?=教育|老师)";

        //找到 韩顺平 这个关键字,但是要求只是查找 不是 (韩顺平教育 和 韩顺平老师) 中包含有的韩顺平
        //下面也是非捕获分组，不能使用 matcher.group(1)
        String regStr = "韩顺平(?!教育|老师)";
        Pattern pattern = Pattern.compile(regStr);
        Matcher matcher = pattern.matcher(content);
        while (matcher.find()) {
            System.out.println("找到: " + matcher.group(0));
        }
    }
}
```

27.7 应用实例  
![](https://img-blog.csdnimg.cn/96c324126a9b4cefa7defa8c1ced027e.png)  
RegExp10.java

```
package com.hspedu.regexp;
import java.util.regex.Matcher;
import java.util.regex.Pattern;
/**
 * 正则表达式的应用实例
 */
public class RegExp10 {
    public static void main(String[] args) {
        String content = "13588889999";
        // 汉字
        //String regStr = "^[\u0391-\uffe5]+$";
        // 邮政编码
        // 要求：是1-9开头的一个六位数.  比如：123890
        //String regStr = "^[1-9]\\d{5}$";
        // QQ号码
        // 要求:  是1-9开头的一个(5位数-10位数)  比如:  12389 , 1345687 , 187698765
        //String regStr = "^[1-9]\\d{4,9}$";
        // 手机号码
        // 要求: 必须以13,14,15,18 开头的11位数 , 比如 13588889999
        String regStr = "^1[3|4|5|8]\\d{9}$";
        Pattern pattern = Pattern.compile(regStr);
        Matcher matcher = pattern.matcher(content);
        if(matcher.find()) {
            System.out.println("满足格式");
        } else {
            System.out.println("不满足格式");
        }
    }
}
```

RegExp11.java

```
package com.hspedu.regexp;
import java.util.regex.Matcher;
import java.util.regex.Pattern;
/**
 * 演示正则表达式的使用
 */
public class RegExp11 {
    public static void main(String[] args) {
        //String content = "https://www.bilibili.com/video/BV1fh411y7R8?from=search&seid=1831060912083761326";
        String content = "http://edu.3dsmax.tech/yg/bilibili/my6652/pc/qg/05-51/index.html#201211-1?track_id=jMc0jn-hm-yHrNfVad37YdhOUh41XYmjlss9zocM26gspY5ArwWuxb4wYWpmh2Q7GzR7doU0wLkViEhUlO1qNtukyAgake2jG1bTd23lR57XzV83E9bAXWkStcAh4j9Dz7a87ThGlqgdCZ2zpQy33a0SVNMfmJLSNnDzJ71TU68Rc-3PKE7VA3kYzjk4RrKU";
        /**
         * 思路
         * 1. 先确定 url 的开始部分 https:// | http://
         * 2.然后通过 ([\w-]+\.)+[\w-]+ 匹配 www.bilibili.com
         * 3. /video/BV1fh411y7R8?from=sear 匹配(\/[\w-?=&/%.#]*)?
         */
        String regStr = "^((http|https)://)?([\\w-]+\\.)+[\\w-]+(\\/[\\w-?=&/%.#]*)?$";//注意：[. ? *]表示匹配就是.本身
        Pattern pattern = Pattern.compile(regStr);
        Matcher matcher = pattern.matcher(content);
        if(matcher.find()) {//这个方法是部分匹配，regStr最前面加了 ^ 和最后面加了 $ 才是整体匹配
            System.out.println("满足格式");
        } else {
            System.out.println("不满足格式");
        }
        //这里如果使用Pattern的matches 整体匹配 比较简洁
        System.out.println(Pattern.matches(regStr, content));//
    }
}
```

![](https://img-blog.csdnimg.cn/da4dc23ee6504e2ba1a16fbaf2b35d83.png)

27.8 正则表达式三个常用类  
![](https://img-blog.csdnimg.cn/cb2f87a2f83b4da18ea5c9b971d67aea.png)  
![](https://img-blog.csdnimg.cn/9333f142763c4aa098485c23e87af7b1.png)

```
package com.hspedu.regexp;
import java.util.regex.Pattern;
/**
 * 演示matches方法，用于整体匹配, 在验证输入的字符串是否满足条件使用
 */
public class PatternMethod {
    public static void main(String[] args) {
        String content = "hello abc hello, 韩顺平教育";
        //String regStr = "hello";
        String regStr = "hello.*";
        boolean matches = Pattern.matches(regStr, content);
        System.out.println("整体匹配= " + matches);
    }
}
```

![](https://img-blog.csdnimg.cn/7482f88cd97c4a21aec8db3a1a496b2b.png)  
![](https://img-blog.csdnimg.cn/ee96a7b56aad4960b302a00090c37375.png)  
![](https://img-blog.csdnimg.cn/f8a7a8fb7ad044d880d21c0f4d49075a.png)

```
package com.hspedu.regexp;
import java.util.regex.Matcher;
import java.util.regex.Pattern;
/**
 * Matcher 类的常用方法
 */
public class MatcherMethod {
    public static void main(String[] args) {
        String content = "hello edu jack hspedutom hello smith hello hspedu hspedu";
        String regStr = "hello";
        Pattern pattern = Pattern.compile(regStr);
        Matcher matcher = pattern.matcher(content);
        while (matcher.find()) {
            System.out.println("=================");
            System.out.println(matcher.start());
            System.out.println(matcher.end());
            System.out.println("找到: " + content.substring(matcher.start(), matcher.end()));
        }
        //整体匹配方法，常用于，去校验某个字符串是否满足某个规则
        System.out.println("整体匹配=" + matcher.matches());

        //完成如果content 有 hspedu 替换成 韩顺平教育
        regStr = "hspedu";
        pattern = Pattern.compile(regStr);
        matcher = pattern.matcher(content);
        //注意：返回的字符串才是替换后的字符串 原来的 content 不变化
        String newContent = matcher.replaceAll("韩顺平教育");
        System.out.println("newContent=" + newContent);
        System.out.println("content=" + content);
    }
}
```

27.9 分组、捕获、反向引用

27.9.1 提出需求  
![](https://img-blog.csdnimg.cn/4c672a883a834217bc0d845dbeb3556c.png)

27.9.2 介绍  
![](https://img-blog.csdnimg.cn/7681b1261cdc40bdb1738705ce09bf5c.png)  
27.9.3 看几个小案例  
![](https://img-blog.csdnimg.cn/ebdd647546494fc284e71287d2df581c.png)

```
package com.hspedu.regexp;
import java.util.regex.Matcher;
import java.util.regex.Pattern;
/**
 * 反向引用
 */
public class RegExp12 {
    public static void main(String[] args) {
        String content = "h1234el9876lo33333 j12324-333999111a1551ck14 tom11 jack22 yyy12345 xxx";
        //要匹配两个连续的相同数字 :  (\\d)\\1
        //String regStr = "(\\d)\\1";	\\1代表分组1号,也就是(\\d)
        //要匹配五个连续的相同数字： (\\d)\\1{4}
        //String regStr = "(\\d)\\1{4}";
        //要匹配个位与千位相同，十位与百位相同的数 5225 , 1551  (\\d)(\\d)\\2\\1
        //String regStr = "(\\d)(\\d)\\2\\1";
        /**
         * 请在字符串中检索商品编号,形式如:12321-333999111 这样的号码,
         * 要求满足前面是一个五位数,然后一个-号,然后是一个九位数,连续的每三位要相同
         */
        String regStr = "\\d{5}-(\\d)\\1{2}(\\d)\\2{2}(\\d)\\3{2}";
        Pattern pattern = Pattern.compile(regStr);
        Matcher matcher = pattern.matcher(content);
        while (matcher.find()) {
            System.out.println("找到 " + matcher.group(0));
        }
    }
}
```

27.9.4 经典的结巴程序  
![](https://img-blog.csdnimg.cn/3100b7248e324e50bd485da0fa51bf65.png)

```
package com.hspedu.regexp;
import java.util.regex.Matcher;
import java.util.regex.Pattern;
public class RegExp13 {
    public static void main(String[] args) {
        String content = "我....我要....学学学学....编程java!";
        //1. 去掉所有的.
        Pattern pattern = Pattern.compile("\\.");
        Matcher matcher = pattern.matcher(content);
        content = matcher.replaceAll("");
 //       System.out.println("content=" + content);
        //2. 去掉重复的字  我我要学学学学编程java!
        // 思路
        //(1) 使用 (.)\\1+
        //(2) 使用 反向引用$1 来替换匹配到的内容
        // 注意：因为正则表达式变化，所以需要重置 matcher
//        pattern = Pattern.compile("(.)\\1+");//分组的捕获内容记录到$1
//        matcher = pattern.matcher(content);
//        while (matcher.find()) {
//            System.out.println("找到=" + matcher.group(0));
//        }
//        //使用 反向引用$1 来替换匹配到的内容
//        content = matcher.replaceAll("$1");
//        System.out.println("content=" + content);

        //3. 使用一条语句 去掉重复的字  我我要学学学学编程java!
        content = Pattern.compile("(.)\\1+").matcher(content).replaceAll("$1");
        System.out.println("content=" + content);
    }
}
```

27.10 String 类中使用正则表达式

27.10.1 替换功能  
![](https://img-blog.csdnimg.cn/c3ab9d648d244f35a048f0ae711cab21.png)

```
String content = "2000年5月，JDK1.3、JDK1.4和J2SE1.3相继发布，几周后其" +
                "获得了Apple公司Mac OS X的工业标准的支持。2001年9月24日，J2EE1.3发" +
                "布。" +
                "2002年2月26日，J2SE1.4发布。自此Java的计算能力有了大幅提升";
//使用正则表达式方式，将 JDK1.3 和 JDK1.4 替换成JDK
content = content.replaceAll("JDK1\\.3|JDK1\\.4", "JDK");
System.out.println(content);
```

27.10.2 判断功能  
![](https://img-blog.csdnimg.cn/37485a7ccce6417cbfcfd797c988332b.png)

```
//要求 验证一个 手机号， 要求必须是以138 139 开头的
String content = "13888889999";
if (content.matches("1(38|39)\\d{8}")) {
	System.out.println("验证成功");
} else {
	System.out.println("验证失败");
}
```

27.10.3 分割功能  
![](https://img-blog.csdnimg.cn/f76b00c8447c4f1c9f995f0b203fce67.png)

```
//要求按照 # 或者 - 或者 ~ 或者 数字 来分割
String content = "hello#abc-jack12smith~北京";
String[] split = content.split("#|-|~|\\d+");
for (String s : split) {
	System.out.println(s);
}
```

27.11 本章作业  
![](https://img-blog.csdnimg.cn/70fbb1d5acf5461bad1229a9281fac0d.png)

```
package com.hspedu.regexp;
public class Homework01 {
    public static void main(String[] args) {
        //规定电子邮件规则为
        //只能有一个@
        //@前面是用户名,可以是a-z A-Z 0-9 _-字符
        //@后面是域名,并且域名只能是英文字母， 比如 sohu.com 或者 tsinghua.org.cn
        //        写出对应的正则表达式, 验证输入的字符串是否为满足规则
        String content = "hsp@tsinghua.org.cn kkk";
        String regStr = "^[\\w-]+@([a-zA-Z]+\\.)+[a-zA-Z]+$";
        //老师说明
        //1. String 的 matches 是整体匹配
        //2. 看看这个matches 底层
        /**
         * String 的 matches
         *  public boolean matches(String regex) {
         *         return Pattern.matches(regex, this);
         *     }
         *  Pattern
         *  public static boolean matches(String regex, CharSequence input) {
         *         Pattern p = Pattern.compile(regex);
         *         Matcher m = p.matcher(input);
         *         return m.matches();
         *     }
         *  Mather类 match
         *  Attempts to match the entire region against the pattern
         *  public boolean matches() {
         *         return match(from, ENDANCHOR);
         *     }
         */
        if (content.matches(regStr)) {
            System.out.println("匹配成功");
        } else {
            System.out.println("匹配失败");
        }
    }
}
```

![](https://img-blog.csdnimg.cn/8b5248c3525a45fbab7c9a65896f75c7.png)

```
package com.hspedu.regexp;
public class Homework02 {
    public static void main(String[] args) {
        //要求验证是不是整数或者小数
        //提示： 这个题要考虑正数和负数
        //比如： 123 -345 34.89 -87.9 -0.01 0.45 等
        /**
         * 老师的思路
         * 1. 先写出简单的正则表达式
         * 2. 再逐步的完善[根据各种情况来完善]
         */
        String content = "-0.89"; //
        String regStr = "^[-+]?([1-9]\\d*|0)(\\.\\d+)?$";
        if(content.matches(regStr)) {
            System.out.println("匹配成功 是整数或者小数");
        } else {
            System.out.println("匹配失败");
        }
    }
}
```

![](https://img-blog.csdnimg.cn/4fff7ebb4f2b45ebbdac03d74c036535.png)

```
package com.hspedu.regexp;
import java.util.regex.Matcher;
import java.util.regex.Pattern;
public class Homework03 {
    public static void main(String[] args) {
        String content = "http://www.sohu.com:8080/abc/xxx/yyy/inde@#$%x.htm";
        //因为正则表达式是根据要求来编写的，所以，如果需求需要的话，可以改进.
        String regStr = "^([a-zA-Z]+)://([a-zA-Z.]+):(\\d+)[\\w-/]*/([\\w.@#$%]+)$";
        Pattern pattern = Pattern.compile(regStr);
        Matcher matcher = pattern.matcher(content);
        if(matcher.matches()) {//整体匹配, 如果匹配成功，可以通过group(x), 获取对应分组的内容
            System.out.println("整体匹配=" + matcher.group(0));
            System.out.println("协议: " + matcher.group(1));
            System.out.println("域名: " + matcher.group(2));
            System.out.println("端口: " + matcher.group(3));
            System.out.println("文件: " + matcher.group(4));
        } else {
            System.out.println("没有匹配成功");
        }
    }
}
```

![](https://img-blog.csdnimg.cn/a7cbb0ce7c404cfead4473227a9b70dc.png)