---
title: MyBatis开发流程
date: 2019-02-16 16:47:12
tags: 学习经历
categories: SSM学习ing
---

通过这几天的学习，大概懂得了mybatis的开发流程还有基础的CURD操作，就想着把它写下来，接下来会写下mybatis框架的开发步骤，举例代码就用insert，其他read、update、delete大致跟insert一样。
<!-- more -->
## mybatis开发步骤
#### 一、导入相对应的jar包
如图所示：
![jar](/images/myBatisJar.jpg)

#### 二、写主配置文件myBatis-config.xml
`	<environments default="development">
		<environment id="development">
			<transactionManager type="JDBC" />
			<dataSource type="POOLED">
				<property name="driver" value="com.mysql.jdbc.Driver" />
				<property name="url" value="jdbc:mysql://localhost:3306/mybatis?useUnicode=true&amp;characterEncoding=UTF-8" />
				<property name="username" value="root" />
				<property name="password" value="root" />
			</dataSource>
		</environment>
	</environments>
	<mappers>
	<mapper resource="god/jiang/entity/DeptMapper.xml"/>
</mappers>`

#### 三、写映射文件
例如创建一个xxx.java的javebean,同时就要创建一个xxx.Mapper.xml来映射数据库的字段，还有要先写CURD的SQL语句，如图所示：
![mapper](/images/myBatisMapper.jpg)

#### 四、写Dao的接口和实现（以insert为例子）
1.先用Resources.getResourcesAsReader(myBatis-config.xml)读取主配置文件
2.构建sessionFactory
3.创建session(mybatis默认开启事务)
4.业务逻辑（insert为例子）
5.提交事务
代码如下：
![insert](/images/myBatisSave.jpg)

#### 五、test（省略）
...
...
...

### 结语
> MyBatis是一款优秀的持久层框架，它支持定制化SQL、存储过程以及高级映射。MyBatis避免了几乎所有的JDBC代码和手动设置参数以及获取结果集。MyBatis可以使用简单的 XML 或注解来配置和映射原生信息，将接口和 Java 的 POJOs(Plain Ordinary Java Object,普通的 Java对象)映射成数据库中的记录。
以上就是我对MyBatis的开发流程的理解和CURD示例。