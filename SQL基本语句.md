### 数据库操作

**数据库操作**（数据库为class）

``` sql
-- 数据库的操作
    -- 创建数据库
    create database test charset=utf8;
    
    -- 查看创建数据库的语句
    show create database test;
    
    -- 显示所有的数据库
    show databases;

    -- 删除数据库
    drop database test;

    -- 使用数据库
    use test;

    -- 查看当前使用的数据库
    select database();
    
```



**数据表的操作**（数据表为students）

```sql 
-- 数据表的操作
	-- 显示所有的表
	show tables;
	
	-- 创建表
	create table students(
    	id int unsigned not null primary key auto_increment,
        name varchar(20),
        age tinyint,
        gender enum('男', '女', '保密') default '保密',
        cls_id int
    );
    
    create table classes(
    	id int unsigned not null primary key auto_increment,
        name varchar(20)
    );
	
	-- 查看表的结构
	desc students;
	
	-- 删除数据表
	drop table students;
	
	-- 查看创建表的语句
	show create table students; 
```



**修改表 --- alter**

```sql
-- 修改表 --- alter
	-- 添加字段--- add
	alter table students add high int;
	
	-- 修改字段--- modify，只修改表的约束和类型
	alter table students modify high decimal(5,2);
	
	-- 修改字段--- change，修改表的名称，也可以修改约束和类型
	alter table students change high higth decimal(5,2);
	
	-- 删除字段 --- drop
	alter table students drop higth;
```



**增删改查 --- CRUD --  create添加、 retrieve 读取、update 修改、delete删除 **

```sql 
-- 插入数据
	-- 因为id是自动增长，所以这项可以填0、null或者default
	insert into students value(0, '小王', 18, '男');
	
	-- 部分插入, 没有赋值的都采取默认值
    insert into students (age, gender) value(19, '女');
    
    -- 同时插入多个数据
    insert into students (name, age) value('小乔', 19), ('大乔', 20);
    



-- 修改数据
	-- 枚举类型，可用数字代替，数字从1开始
	update students set age=20,gender=2 where id=2;
	
	
	

-- 删除数据
	-- 按条件删除数据, 这是物理删除，表明从数据表中真正删除
	delect from students where id=2;
	
	-- 数据来之不易，一般不真正删除，使用逻辑删除
	-- 使用额外字段来标记是否删除，is_delete
	alter table students add is_delete bit default 0;
	-- 删除时只要把该字段标记成1即可。
	update students set is_delete=1 where id=1;
    



-- 查询数据
	-- 查询所有
	select * from students;
	
	-- 有条件查询
	select * from students where gender='男';
	
	-- 查询指定字段
	select name,age from students;
	
	-- 使用as将字段名重命名
	select name as 姓名, age as 年龄 from students;
	
```



#### 总结

- 修改表的结构时，使用alter，修改数据时，使用update
- 对数据库数据表进行删除，或者删除数据表的字段，使用drop，对数据进行删除，使用delete





###外键

外键的作用，主要是对两张表中的同一数据进行约束，尽量**少使用外键**，会极大降低更新数据的效率。

```sql
-- 添加外键
-- 为students表添加外键cls_id，它与classes表相关联
alter table students add foreign key (cls_id) references classes(id);

-- 删除外键
alter table students drop foreign key 外键名称;
```




