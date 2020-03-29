### Python使用MySQL流程

``` python
from pymysql import *

# 1. 获取连接对象
conn = connect(host='localhost', port=3306, user='root', password='123456', database='clusters' )

# 2. 获取cursor对象
cursor = conn.cursor()

# 3. 使用cursor对象执行sql语句，返回生效的行数
cursor.execute(sql)

# 4. 关闭cursor对象
cursor.close()

# 5. 关闭conn对象
conn.close()

```





###查询

`cursor`：用于访问和操作数据库的数据，可以执行sql语句，**它指向sql语句返回的数据集**。

它是一个指针，它指向当前访问到的位置（从0开始，0标记着第一个数据，但数据库中从1开始，所以指向下一条数据），当指向`fetch`方法时，通过cursor的数据集获取数据。

**cursor中查询的方法**

**cursor.fetchone()**：获得数据集中，当前cursor指向的**下一条数据**

**cursor.fetchmany()**：获得数据集中，当前cursor指向的下n条数据，可传递参数，表示查询几条数据，默认为1条

**cursor.fetchall()：**获得数据集中，当前cursor指向的**后面的全部数据**，并不是从数据库中所有数据。





### 增删改

因为这里要修改数据库里的内容，所以在执行完sql语句后，要提交一下，即 `conn.commit()`.在python中，**默认开启事务**，即只有commit之后，数据才会提交。

如果提交不成功，则使用`conn.rollback()`进行回滚。

防止sql注入，所以参数要使用列表的形式，将其传给execute方法。

```python
sql = "select * from students where name=%s"
name = '小明'

try:
    # 参数要使用列表的形式，且顺序与sql语句中的%s顺序一致
    cursor.execute(sql, [name]) 
    conn.commit()
except:
    conn.rollback()
```


