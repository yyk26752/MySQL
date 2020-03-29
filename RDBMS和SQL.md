###RDBMS

关系数据库管理系统（Relational Database Management System：*RDBMS*）。它是一套程序，用它来管理关系型数据库。比如常用的MySQL就是这样一套软件。



MySQL采用的是**C/S**架构（客户端/服务端模型），即用户通过SQL语句来和MySQL数据库进行通信。





###SQL 

sql是结构化查询语言，是一种用来操作RDBMS（所有的关系型数据库）的数据库语言

####DML 和 DDL

 可以把 SQL 分为两个部分：**数据操作语言** (DML) 和 **数据定义语言** (DDL)。 

DML包括增删改查:

- *SELECT* - 从数据库表中获取数据
- *UPDATE* - 更新数据库表中的数据
- *DELETE* - 从数据库表中删除数据
- *INSERT INTO* - 向数据库表中插入数据

DDL 使我们有能力创建或删除表格。我们也可以定义索引（键），规定表之间的链接，以及施加表间的约束:

- *CREATE DATABASE* - 创建新数据库
- *ALTER DATABASE* - 修改数据库
- *CREATE TABLE* - 创建新表
- *ALTER TABLE* - 变更（改变）数据库表
- *DROP TABLE* - 删除表
- *CREATE INDEX* - 创建索引
- *DROP INDEX* - 删除索引

