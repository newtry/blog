# mybatis学习


> 学习


## 概述

	通常情况下，使用JDBC处理SQL语句的步骤如下：

1. 建立数据库连接
2. 创建 JDBC Statements 对象
3. 设置SQL语句的传入参数
4. 执行SQL语句并获得查询结果
5. 对查询结果进行转换处理并将处理结果返回
6. 释放相关资源（关闭Connection，关闭Statement，关闭ResultSet）


	建立连接有两种方式：
	
	1. DriverManager
	2. DataSource

学习地址
http://www.iteye.com/blogs/subjects/mybatis_internals

### type包
类型处理，包含了类型处理器接口TypeHandler，父类BaseTypeHandler,以及若干个子类。

### 配置文件
将xml配置文件中的信息都读取到Configuration对象中。
封装jdk中处理xml文件的类，涉及到parsing包和builder包
主要由以下几个类：

1. XNode
2. XPathParser
3. XMLConfigBuilder
4. XMLMapperBuilder

mybatis一次查询的过程

1. 通过SqlSessionFactoryBuilder获取SqlSessionFactory
2. 通过SqlSessionFactory获取SqlSession
3. 通过sqlSession调用select、update、insert、delete等方法
4. 在具体的增删改查方法中调用executor的方法操作
5. StatementHandler处理器获取数据库连接、对sql进行预处理、增删改查操作
6. ResultSetHandler 对查询结果进行封装、资源释放、返回结果