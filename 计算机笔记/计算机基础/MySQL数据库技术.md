# 简介
1. MySQL是<mark style="background: #FFB86CA6;">开源、多线程的关系数据库管理系统</mark>，在1995年创建的。
# 1.基础操作
## 1.1 创建数据库和表
**1.1.1创建一个数据库**
```mysql
create database bookstore
```
**1.1.2使用数据库**
```mysql
use bookstore
```
**1.1.3创建数据表**
```mysql
create table [if not exists] books (book_id INT,
				   title_id INT,
				   title varchar(50),
				   author varchar(50));
				   
create table [if exists] table2 like table1 # 创建一个结构与table1一致的表

create table 表名( 
	字段名 类型 约束（主键，非空，唯一，默认值）， 
	字段名 类型 约束（主键，非空，唯一，默认值）， 
)编码，存储引擎；
```
表约束：

|约束键|描述|
|:-|--|
|not null|表示不能存放null值|
|unique|保证唯一值|
|primary key|NOT NULL 和 UNIQUE 的结合。确保某列（或两个列多个列的结合）有唯一标识，有助于更容易更快速地找到表中的一个特定的记录。|
|foreign key|保证一个表中的数据匹配另一个表中的值的参照完整性。|
|check|保证值符合条件|
|default|默认值|


**1.1.4查看表描述**
```mysql
describe books
```
**1.1.5修改数据表**
修改book_id列的属性，设置为KEY
change子句语法:第一个 book_id表示将要修改的现有列，该子句余下的部分用于指定一个新列。
```mysql
# 完全修改
alter table books change column book_id book_id INT AUTO_INCREMENT PRIMARY KEY;
# 仅修改属性
alter table books modify book_id TEXT;
```
**1.1.6显示数据表**
```mysql
show books
```
**1.1.7修改表名**
```mysql
alter table oldName rename newName;
```
**1.1.8添加与删除**
```mysql
# 添加字段
alter table table1 add column col1 TEXT;
# 删除字段
alter table table1 drop column col2;
```
## 1.2 插入数据
标准的 INSERT 语法要为每个插入值指定相应的列。如果想为所有的列添加值，则不需指定列名，但被添加的数据一定要按表中列的顺序排列。
```mysql
insert into books values (values...) # 全部添加
insert into books (name...) values (value...) # 指定添加
# 例: insert into books (book_id) VALUES (456)
```

## 1.3 选择数据
**1.3.1查询数据**
```mysql
select * from books
```
**1.3.2限定查询**
```mysql
select book_id from books where book_id=123
```
**1.3.3关联查询**
```mysql
select book_id from books join author where 
```
**1.3.4多表关联**
多表关联可以接多个join，限制条件时用and来做限制
```mysql
select content from comments 
join books 
join author 
WHERE comments.book_id=books.book_id 
and books.author_id=author.author_id
```
## 1.4 排序，限制与分组
**1.4.1数据排序**
当我们得到很长的一列数据时，可以把数据按指定的顺序输出。使用`ORDER BY`子句可以为数据进行排序。
```mysql
# 倒叙，ASC为正序
select * from author order by author_id DESC
```

**1.4.2限制记录条数**
1. 限制记录条数必须放在语句最后
2. 如果想取回 20 行以后的 10 个记录，我们可以修改LIMIT子句指定需要跳过的行数，以及想要取回的记录数。
```mysql
# 如果我想对显示的记录条数加以限制，则可在上面的 SQL 语句结尾处添加LIMIT子句
select * from books limit 5
select * from books order by book_id asc limit 5 
# 跳过5个取2个值
select * from books order by book_id asc limit 5,2
```
**1.4.3分组查询**
如果我们想让标题相同的一组数据只返回一行记录，一行记录就可以满足需求了，可以按照如下方式使用`GROUP BY`句完成这项工作：
分组查询筛选用`having`
```mysql
select avg(sal) aa from websites where sal is not null group by country having aa > 1500
```
## 1.5 分析和处理数据
**1.5.1统计函数**
```mysql
select count(*) as '作者为5的书数量' from books where author_id=5
```
**1.5.2相加函数**
相加函数常用于计算账目
```mysql
select sum(books.book_id) as '书本id之和' from books
```
**1.5.3日期函数**
```mysql
select date_format(orders.order_time,"%Y年%m月%d日%H时%m分%s秒") from orders
```
## 1.6 修改数据
**1.6.1更新数据**
第一个是表名称，第二个是要设置的值，第三个是限制条件
首先，我们要声明即将被更新的表名。接下来我们要在 SET 关键字后面指定将要修改的列以及相应的新值。如果想修改的列不止一列，那么应提供一个<mark style="background: #FFB86CA6;">由逗号分开的列表</mark>， 列表中每个列后跟随着等号操作符以及各自的新值。SET 只需输入一次即可。
```mysql
update books set books.book_id=9999 where books.book_id=88
```
**1.6.2替换数据**
如果我们使用 INSERT 语句，重复行会引发拒绝添加的警告信息。为防止这种情况发生，可以使用REPLACE语句，该语句向表中插入一行新数据，并可以用新数据替代已存在的数据。
REPLACE 语句与 INSERT 语句的语法是相同的。
```mysql
replace into author values(123,'Aud')
```
## 1.7 删除数据
可以使用 DELETE 语句删除指定的数据行。
```mysql
delete from author where author.author_id=123
```
## 1.8 模糊查询数据
我们也不清楚所查询列的精确完整值是什么。这种情况下，可以使用 LIKE 操作符。
```mysql
select * from books where books.title like '%Ms%'

select * from books where books.title in ('a','b','c')
```
## 1.9 子查询
子查询是嵌套在另外一个SQL语句里的SELECT语句。
子查询不一定是 SELECT，它也可以是 INSERT、DELETE、 DO、UPDATE 或 SET 语句。除非子查询位于 FROM 子句中，否则外部查询通常不能查询 或修改内部查询使用到的表中的数据。
```mysql
select * from (select col1,col2 from table1) as derived1
```
**1.9.1单字段子查询**
最基本的子查询返回一个标量或单一值。这种类型的子查询在以下二种情况中特别有用：在一个带有=操作符连接的WHERE语句中；
**1.9.2多段子查询**
有时候你可能想对多个值进行匹配。对于这些情况，需要在子查询中使用带有操作符的连接或使用如下子句：ALL、ANY、EXISTS、IN 或 SOME。
**1.9.3内连接**
```mysql
select * from table1 join table2 [left|right|cross] on table1.a=table2.b
```
连接类型：
- 左外连接：只连接左边的表和中间共有的数据。
- 内连接：只连接中间共有数据。
- 右外连接：只连接右边的表和中间共有的数据。
# 2.SQL语句和函数
## 2.1 用户管理
用户的访问权限可以是全局层级（如在服务器上使用所有的数据库），也可以是数据库层级、表层级或者列层级。
除了与安全相关的 SQL 语句之外，为了防止独占资源，可以限制用户对 MySQL 资源的使用并间接拒绝其他用户的服务。因此，你可以限定连接的数目或者每小时每位用户的 最大资源。
**2.1.1用户授权**
```mysql
# 用户授权
grant all privileges on study.* to 'breeze'@'localhost' identified by '258369'
```

```
all privileges：表示将所有权限授予给用户。也可指定具体的权限如：SELECT、CREATE、DROP等。

on：表示这些权限对哪些数据库和表生效，格式：数据库名.表名，这里写'*'表示所有数据库，所有表。如果我要指定将权限应用到test库的user表中，可以这么写：test.user

to：将权限授予哪个用户。格式：'用户名'@'登录IP或域名'。%表示没有限制，在任何主机都可以登录。比如：'yangxin'@'192.168.0.%'，表示yangxin这个用户只能在192.168.0IP段登录

identified by：指定用户的登录密码
```
**2.1.2用户管理**
```mysql
grant user # 创建新用户
grant # 创建用户账户，为新用户账户设置权限或者为现有的用户设置权限
revoke # 撤销权限
rename user # 修改用户名
set password # 修改密码
drop user # 删除用户
```
## 2.2 语句
**2.2.1创建用户**
`CREATE USER`语句用于在MySQL服务器上创建新用户账户。用户名用引号标示，后面跟@符号和用引号标示的主机IP地址或主机名。使用通配符`%`作为主机允许客户端指定用户从任意主机连接。
多个账户用逗号隔开。
```mysql
create user 'user'[@'host']
	[identified by [password]'password'][,...]
```
**2.2.2删除用户**
```mysql
drop user 'user'@'host'
```
**2.2.3撤销权限**
`ALL`选项用以确保撤销所有权限。`*.*`涵盖了所有数据库中的所有表。
```mysql
revoke all on *.* from 'user'@'host';
```
**2.2.4设置密码**
在`SET PASSWORD`语句中如果没有指定`for`字句，默认情况下为当前用户账户
```mysql
set password for 'user'@'host'=password('password')
```
## 2.3 常用函数
**2.3.1 aes_decrypt()函数**
这个函数用于解密文本，该文本采用高级加密标准算法编码，保密关键字的长度为128位。与之相反的函数是`AES_ENCRYPT()`，该函数解锁加密的字符串，使用密码作为第二个参数。
```mysql
aes_encrypt(str,pass str) # 加密
aes_decrypt(str,pass str) # 解密
```
**2.3.2 encode()函数**
该函数用二进制格式来加密给定的字符串，并用password作为密码来解密该字符 串。在mysql数据库的user表中，不能使用该函数作为password列的值，而是使用`password()`函数。
```mysql
encode(str,pass str);
decode(str,pass str);
password(str); # 类似MD5加密
md5(str); # MD5加密
sha(str) # SHA(Secure Hash Algorithm,SHA) 算法加密
```
**2.3.3字符串函数**
```mysql
ascii(char) # 获取ascii码
substr(str,idx,idx) # 截取字符串
char_length(str) # 获取字符串长度
charset(str) # 获取字符串编码
concat(str...) # 拼接字符串
replace(str,old,new) # 替换字符串
left(str,len) && right(str,len) # 该函数返回字符串的最后长度的字符。如果你想提取字符串的开始部分，请使用 LEFT()函数。
substring_index(str,delimiter,count) # 此函数返回字符串的子字符串，它使用定界符分割子字符串，并计算子字符串中用到的定界符的个数以确定返回哪个子字符串。

```
# 3.正则表达式
| 字符 | 作用 |
| :- | :-- |
| ^ | 匹配字符串开始 |
| $ | 匹配字符串结束 |
| . | 匹配任意字符，空格或换行符 |
| * | 匹配0或更多个前一个字符的值 |
| + | 匹配一个或更多前一个字符的值 |
| ? | 匹配0或一个前一个字符的值 |

# 4.数据类型
## 4.1 数值类型
|类型|大小|范围（有符号）|用途|
|---|---|---|---|
|TINYINT|1 Bytes|(-128，127)|小整数值|
|SMALLINT|2 Bytes|(-32 768，32 767)|大整数值|
|MEDIUMINT|3 Bytes|(-8 388 608，8 388 607)|大整数值|
|INT或INTEGER|4 Bytes|(-2 147 483 648，2 147 483 647)|大整数值|
|BIGINT|8 Bytes|(-9,223,372,036,854,775,808 ~ 9,223 372 036 854 775 807)|极大整数值|
|FLOAT|4 Bytes|超大值|单精度浮点数值|
|DOUBLE|8 Bytes|超大值|双精度浮点数值|
## 4.2 日期与时间
|类型|大小(bytes)|范围|格式|用途|
|---|---|---|---|---|
|DATE|3|1000-01-01/9999-12-31|YYYY-MM-DD|日期值|
|TIME|3|'-838:59:59'/'838:59:59'|HH:MM:SS|时间值或持续时间|
|YEAR|1|1901/2155|YYYY|年份值|
|DATETIME|8|'1000-01-01 00:00:00' 到 '9999-12-31 23:59:59'|YYYY-MM-DD hh:mm:ss|混合日期和时间值|
|TIMESTAMP|4|'1970-01-01 00:00:01' UTC 到 '2038-01-19 03:14:07'|YYYY-MM-DD hh:mm:ss|混合日期和时间值，时间戳|
## 4.3 字符串类型
|类型|大小|用途|
|---|---|---|
|CHAR|0-255 bytes|定长字符串|
|VARCHAR|0-65535 bytes|变长字符串|
|TINYBLOB|0-255 bytes|不超过 255 个字符的二进制字符串|
|TINYTEXT|0-255 bytes|短文本字符串|
|BLOB|0-65 535 bytes|二进制形式的长文本数据|
|TEXT|0-65 535 bytes|长文本数据|
|MEDIUMBLOB|0-16 777 215 bytes|二进制形式的中等长度文本数据|
|MEDIUMTEXT|0-16 777 215 bytes|中等长度文本数据|
|LONGBLOB|0-4 294 967 295 bytes|二进制形式的极大文本数据|
|LONGTEXT|0-4 294 967 295 bytes|极大文本数据|
# 5. 踩坑排错
## 5.1 中文乱码
- 在创建数据表时末尾添加`charset=utf8`
- 修改字符编码集:
```mysql
# 查看编码集
show variables like '%char%';
# 设置编码
set character_set_server=utf8;
```

| 变量名称 | 值 |
| :- | - |
|character_set_client|utf8mb4|
|character_set_connection|utf8mb4|
|character_set_database|utf8|
|character_set_filesystem|binary|
|character_set_results|utf8mb4|
|character_set_server|utf8|
|character_set_system|utf8|


