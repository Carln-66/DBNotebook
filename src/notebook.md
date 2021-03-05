##  一、数据库的作用
1. 持久化数据
2. 方便检索
3. 存储大量数据
4. 共享、安全
5. 通过组合分析获得新的数据

## 二、数据库的相关概念
### DBMS、DB、SQL
DB：database，存储一系列有组织数据的容器    
DBMS：Database Management System，数据库管理系统，使用DBMS管理和维护数据库   
SQL：Structure Query Language，结构化查询语言，程序员用于和DBMS通信的语言  

## 三、数据库存储数据的特点
1. 数据放在表中，表再放在库中  
2. 一个库可以有多张表，每张表都有自己的唯一标识名  
3. 一张表的设计类似于Java中类的设计  
   表中的字段的设计类似于属性的设计  
   表中的记录，类似于对象  
   表中的所有记录  
   表中的所有记录类似于对象的集合  

orm：object relation mapping 对象关系映射

## 四、初始化MySQL
### MySQL产品介绍
MySQL前身属于瑞典一家公司AB，2008年被SUN公司收购，2009年SUN被Oracle公司收购

特点：  
1. 体积小、安装比较方便  
2. 开源、免费   
3. 性能高、稳定性好  
4. 兼容性好  

## MySQL产品安装
### 基于C/S架构的DBMS，需要安装服务端和客户端
www.orcle.com  
MySQL 8.0.23
### MySQL服务的启动和停止
方式一：图形化  
win+R---services.msc---MySQL服务   

方式二：管理员身份运行DOS  
启动：net start 服务名;  
停止：net stop 服务名;  

### MySQL服务的登录和退出
方式一：通过DOS命令  
mysql -h主机名 -P端口号 -u用户名 -p密码  
如果是本机，则：-h主机名   可以省略  
如果端口号是3306，则：-P端口号  可以省略  

方式二：通过图形化界面客户端  
DBeaver输入用户名连接进入  

### MySQL常见命令和语法规范
#### 常见命令
+ SHOW databases 显示当前连接下的所有数据库
+ SHOW tables   显示当前库中所有表
+ SHOW tables FROM 库名   显示指定库中所有表
+ SHOW columns FROM 表名  显示指定表中所有列
+ USE 库名    使用/打开指定库

#### 语法规范
+ 区分大小写  
+ 每条命令结尾建议用分号';'  
+ 注释：#单行注释   
  --单行注释  
  /多行注释/  
  
## 五、DQL语言学习
DQL：Data Query Language 数据查询语言  
SELECT

### 1. 基础查询
#### 语法：
SELECT 查询列表 FROM 表名;

特点：  
1. 查询结果是一个虚拟表   
2. 查询列表可以是单个字段、多个字段、常量、表达式、函数、也可以是以上的组合  

引申1：起别名  
   SELECT 字段名　AS　"别名: FROM 表名;  
   SELECT 字段名 "别名" FROM 表名;  

引申2："+"运算   
    作用：加法运算  
    如果两个操作数都是数值型，则直接做加法运算  
+ 如果其中一个为非数值型，则将强制转换为数值型，如果转换失败，则置零
>    '12'+4---16   
>    'abc'+4---4  
+ 如果其中一个为null，则结果直接为null

引申3：去重  
关键字：DISTINCT  
> SELECT DISTINCT   
>   department_id   
> FROM   
>   employees;    

引申4：补充函数  
> SELECT version();  #获取版本号  
> SELECT database();  
> SELECT user();  
> ELECT IFNULL(字段名, 表达式);  
> SELECT CONCAT(字符1, 字符2, 字符3,...);  
> SELECT LENGTH(字符/字段);  #获取字节长度
   
### 2. 条件查询
语法：  
> SELECT  
> 查询列表   
> FROM  
> 表名  
> WHERE  
> 筛选条件;  

特点：  
筛选条件的分类：  
1. 按条件表达式筛选  
   关系运算符：>, <, >=, <=, <>, =
2. 按逻辑表达式筛选  
   逻辑运算符：AND OR NOT  
3. 模糊查询   
+ LIKE: 一般和通配符搭配使用  
   + _    任意单个字符  
   + %    任意多个字符
+ BETWEEN AND: 一般判断某字段是否在指定的区间
  + a BETWEEN 10　AND　１００
+ in: 一般用于判断某字段是否在指定的列表
    　+ a in(10, 30, 50)
+ IS NULL: 判断NULL值
   
### 3. 排序查询
语法：  
> SELECT  
> 查询列表  
> FROM   
> 表名  
> WHERE  
> 条件  
> ORDER BY  
> 排序列表  
       
特点：  
1. 排序列表可以是单个字段、多个字段、函数、别名、表达式、列的索引以及以上的组合
2. 升序： ASC   
   降序：DESC  
   
### 4. 常见函数
说明：SQL中的函数分为单行函数和分组函数  
调用语法：SELECT 函数名(实参列表);

#### 字符函数
>CONCAT(str1, str2,...): 拼接字符  
SUBSTR(str, pos): 截取从pos开始的所有字符，起始索引从1开始  
SUBSTR(str, pos, len): 截取len个从pos开始的字符，起始索引从1开始  
LENGTH(str): 获取字节个数  
CHAR_LENGTH(str): 获取字符个数  
UPPER(str): 变大写  
LOWER(str): 变小写  
> TRIM([substr from] str): 去先后指定空格，默认去空格
> LEFT(str, len): 从左边截取指定len个数的字符  
> RIGHT(str, len): 从右边截取指定len个数的字符  
> LPAD(str, substr,len): 左填充  
> RPAD(str, substr,len): 右填充   
> STRCMP(str1, str2): 比较两字符串大小，str1大返回1；str2大返回-1，相同返回0  
> INSTR(str, substr): 获取substr在str中第一次出现的索引
#### 数学函数
> ceil(x): 向上取整  
> floor(x): 向下取整  
> round(x, d): 四舍五入  
> mod(x, y): 取模/取余  
> truncate(x, d): 截断，保留小数点后d位  
> abs(x): 求绝对值  
#### 日期函数
> now(): 获取当前时间  
> curtime(): 只获取当前时间  
> curdate(): 只获取当前日期  
> date_format(date, %Y%m%d): 格式日期字符
> str_to_date(str, 格式): 将字符转换成日期
> datediff(date1, date2): 获取两个日期之间的天数差
> year(date): 获取指定日期的年
> month(date): 获取指定日期的月
> day(date): 获取指定日期的日
> ...
#### 流程控制函数
> ① if(条件, 表达式1, 表达式2): 如果条件成立，返回表达式1，否则，返回表达式2  
> ② case 表达式  
> when 值1 then 结果1  
> when 值2 then 结果2  
> ...  
> else 结果n  
> end   
> ③  
> case  
> when 条件1 then 结果1   
> when 条件2 then 结果2  
> ...  
> else 结果n  
> end  

#### 分组函数
> sum 求和  
> avg 平均  
> max 求最大  
> min求最小  
> count 计数  

特点： 
1. 实参的字段的类型，sum和avg只支持数值型，其他三个可以支持任意类型
2. 这五个函数都忽略null值
3. count可以支持一下参数：  
   count(字段): 查询该值的个数  
   count(*): 查询结果集的行数  
   count(1): 查询结果集的行数  
4. 分组函数可以和distinct搭配使用，实现去重的统计
    SELECT count(distinct 字段) FROM 表;
   
### 5. 分组查询
语法：  
> SELECT 分组函数，分组的字段    
> FROM 表名  
> WHERE 分组前的筛选条件  
> GROUP BY 分组列表  
> HAVING 分组后的筛选条件  
> ORDER BY 排序列表;  

特点：  
1. 分组列表可以是单个字段、多个字段
2. 筛选条件分为两类：  

| |筛选的基表|使用的关键字|位置|
|:---:|:---:|:---:|:---:|
|分组前筛选|原始表|WHERE|GROUP BY前面|
|分组后筛选|分组后的结果集|HAVING|GROUP BY后面|

### 6. 连接查询
说明：当查询中涉及到了多个字段，则需要通过多表连接  
笛卡尔乘积：  
出现原因：没有有效的连接条件  
解决办法：添加有效的连接条件  

-----

---------------------------SQL92语法-----------------------------
 #### 语法：  
> SELECT 查询列表  
> FROM 表1 别名1, 表2 别名2 ...  
> WHERE 连接条件   
> AND 筛选条件  
> GROUP BY 分组列表  
> HAVING 分组后筛选  
> ORDER BY 排序列表

执行顺序  
1. FROM  
2. WHERE  
3. AND  
4. GROUP BY  
5. HAVING  
6. SELECT  
7. ORDER BY  

-----

---------------------------SQL99语法-----------------------------
#### 内连接语法：  
> SELECT 查询列表  
> FROM 表1 别名1  
> [INNER] JOIN 表2 别名2 ON 连接条件  
> [INNER] JOIN 表3 别名3 ON 连接条件    
> WHERE 筛选条件  
> GROUP BY 分组列表  
> HAVING 分组后筛选  
> ORDER BY 排序列表
> LIMIT 子句;

#### 特点
1. 表的顺序可以调换  
2. 内连接的结果=夺标的交集  
3. n表连接至少需要n-1个连接条件

##### 分类  
1. 等值连接   
2. 非等值连接  
3. 自连接  
   
#### 外连接语法
> SELECT 查询列表  
> FROM 表1 别名1  
> LEFT | RIGHT [OUTER] JOIN 表2 别名2 ON 连接条件  
> LEFT | RIGHT [OUTER] JOIN 表3 别名3 ON 连接条件    
> WHERE 筛选条件  
> GROUP BY 分组列表  
> HAVING 分组后筛选  
> ORDER BY 排序列表
> LIMIT 子句;

##### 特点
1. 查询的结果=主表中所有的行，其中从表和它匹配的将显示匹配行，如果从表没有匹配项则显示null  
2. LEFT JOIN左边的是主表；RIGHT JOIN右边的就是主表；FULL JOIN两边都是主表
3. 一般用于查询除了交集部分剩余的不匹配的行

### 交叉连接
> SELECT 查询列表
> FROM 表1 别名1
> CROSS JOIN 表2 别名2;
   
#### 特点：
类似于笛卡尔乘积

-----

### 7. 子查询
#### 含义
嵌套在其他语句内部的SELECT语句称为子查询或内查询  
外面的语句可以是INSERT、UPDATE、DELETE、**SELECT**等，一般SELECT作为外部语句较多  
外部如果为SELECT语句，则此语句称为外查询或主查询
#### 分类
按出现位置：  
+ SELECT 后面：仅仅支持标量子查询  
+ FROM 后面： 表子查询
+ **WHERE 或 HAVING**：**标量子查询**、**列子查询**、行子查询
+ EXISTS 后面：标量子查询、列子查询、行子查询、表子查询

按结果集的行列
+ **标量子查询(单行子查询)：结果集为一行一列**
+ **列子查询(多行子查询)：结果集为多行一列**
+ 行子查询：结果集为多行多列
+ 表子查询(嵌套子查询)：结果集为多行多列

#### 示例
WHERE或HAVING后面
1. 标量子查询
案例：查询最低工资的员工姓名和工资
````
# 最低工资
SELECT min(salary) 
FROM employees;

# 查询员工的姓名和工资，要求工资等于最低工资
SELECT last_name, salary
FROM employees
WHERE salary = (
SELECT min(salary) 
FROM employees
);  
````

2. 列子查询
案例：查询所有是领导的员工姓名
````
# 查询所有员工的manager_id
SELECT manager_id
FROM employees;

# 查询姓名，employee_id属于上列表的一个
SELECT first_name
FROM employees
WHERE employee_id IN (
SELECT manager_id
FROM employees;
)
````

### 8. 分页查询
#### 应用场景
当要查询的条目数太多，一页显示不全
#### 语法
> SELECT 查询列表
> FROM 表
> LIMIT [offset,] size;

#### 注意：
+ offset代表的是其实的条目索引，默认从0开始
+ size代表的是显示的条目数

#### 公式
加入要显示的页数为page，每一页条目数为size
> SELECT 查询列表
> FROM 表
> LIMIT (page-1)*size, size

### 9. 联合查询
#### 含义
UNION：合并、联合，将多次查询结果合并为一个结果
#### 语法
> 查询语句1  
> UNION[all]  
> 查询语句2  
> UNION [all]  
> . . . 

#### 意义
1. 将一条比较复杂的语句拆分成多条语句
2. 使用于查询多个表的时候，查询的列基本一致

#### 特点
1. 要求多条语句的查询列数必须一致
2. 要求多条查询语句的查询各列类型、顺序最好一致
3. UNION：默认去重；UNION ALL：可以包含重复项

### 查询总结
#### 语法
> SELECT 查询列表            ⑦  
> FROM 表1 别名              ①   
> 连接类型 JOIN 表2          ②    
> ON 连接条件               ③    
> WHERE 筛选               ④  
> GROUP BY 分组列表         ⑤   
> HAVING 筛选              ⑥  
> ORDER BY  排序列表        ⑧  
> LIMIT 起始条目索引，条目数  ⑨   

## DML语言
### 1. 插入
#### 方式一
语法
> INSERT INTO 表名(字段名, ...) values(值, ...);  

特点：   
1. 要求值的类型与字段的类型要一致或兼容
2. 字段的个数和顺序不一定和原表的一致，单必须要正值和字段一一对应
3. 假如表中有可以为null的字段，注意可以通过以下两种方式插入null值  
   ① 字段和值都省略
   ② 字段写上，值使用null
4. 字段和值的个数必须一致
5. 字段名可以省略，默认所有列

#### 方式二
语法
> INSERT INTO 表名 SET 字段 = 值, 字段 = 值, ...

#### 两种方式的区别：
方式一支持一次插入多行，语法如下：
> INSERT INTO 表名[(字段名, ...)] values(值, ...), (值, ...), ...

方式一支持子查询，语法如下：
> INSERT INTO 表名  
> 查询语句;

### 修改
#### 修改单表的记录
语法：
> UPDATE 表名 SET 字段 = 值, 字段 = 值 [WHERE 筛选条件]

#### 修改多表的记录
语法：
> UPDATE 表1 别名 LEFT/RIGHT/ INNER JOIN 表2 别名   
> ON 连接条件    
> SET字段 = 值, 字段 = 值[WHERE 筛选条件] 

### 删除
#### 使用DELETE
1. 删除单表的记录
   > DELETE FROM 表名 [WHERE 筛选条件 LIMIT 条目数] 
2. 级联删除
   > DELETE 别名1, 别名2 FROM 表1 别名1 INNER/LEFT/RIGHT JOIN 表2 别名2  
   > ON 连接条件
   > [WHERE 筛选条件]
   
#### 使用TRUNCATE
> TRUNCATE TABLE 表名;

两种方式的区别
1. TRUNCATE删除后如果再插入，标识列从1开始  
    DELETE删除后如果再插入，标识列从断点开始
2. DELETE可以添加筛选条件，而TRUNCATE不能
3. TRUNCATE效率高
4. TRUNCATE无返回值，DELETE可以返回受影响的行数
5. TRUNCATE不可以回滚，DELETE可以

## DDL语言
### 库的管理
#### 创建库
> CREATE DATABASE [IF NOT EXISTS] 库名 [CHARACTER SET 字符集名];
#### 修改库
> ALTER DATABASE 库名 CHARACTER SET 字符集名;

#### 删除库
> DROP DATABASE [IF EXISTS] 库名

### 表的管理
#### 创建表
> CREATE TABLE [IF NOT EXISTS] 表名(  
>   字段名 字段类型 [约束],
>   字段名 字段类型 [约束],
>    . . . 
>   字段名 字段类型 [约束]
> )

#### 修改表
1. 添加列
> ALTER TABLE 表名 add column 列名 类型 [FIRST/AFTER 字段名];

2. 修改列的类型或约束
> ALTER TABLE 表名 MODIFY COLUMN 列名 新类型 [新约束]
   
3. 修改列名
> ALTER TABLE 表名 CHANGE COLUMN 旧列名 新列名 类型;

4. 删除列
> ALTER TABLE 表名 DROP COLUMN 列名

5. 修改表名
> ALTER TABLE 表名 RENAME [TO] 新表名

#### 删除表
DROP TABLE [IF EXISTS] 表名

#### 复制表
1. 仅仅复制表的结构
> CREATE TABLE 表名 LIKE 旧表;
   
2. 复制表的结构+数据
> CREATE TABLE 表名  
> SELECT 查询列表 FROM 旧表 [WHERE 筛选]

### 数据类型
#### 数值型
1. 整型：tinyint、mediumint、int/integer、bigint  
特点：  
   ① 都可以设置无符号和有符号，默认有符号，通过UNSIGNED设置无符号  
   ② 如果超出了范围，会报out of range异常，插入临界值
   ③ 长度可以不指定，默认会有一个长度。长度表示显式的最大宽度，如果不够，左边用0填充和，但需要搭配ZEROFILL，并且默认变为无符号整型。
   
2. 浮点型：  
   定点数：decimal(M, D)    4  
   浮点数：float(M, D); double(M, D)    8  
特点：  
① M代表整数部位与小数部位的个数，D代表小数部位  
② 如果超出范围，则报out of range异常，并且插入临界值  
③ M和D都可以省略，但对于定点数，M默认为10，D默认为0  
④ 如果精度要求较高，则优先考虑使用定点数

#### 字符型
char、varchar、binary、varbinary、enum、set、text、blob

char：固定长度的字符，写法为char(M)，最大长度不能超过M，其中M可以省略，默认为1  
varchar：可变长度的字符，写法为varchar(M)，最大长度不能超过M，其中M不能省略

#### 日期型
year 年  
date 日期  
time 时间  
datetime 日期+时间  
timestamp 日期+时间 受时区、语法模式、版本的影响，更能反映时区的真实事件

### 常见的约束
> CREATE TABLE 表名(  
> 字段名 字段类型 约束  
> )  

含义：一种限制，用于限制表中的数据，为了保证表中的数据的准确性和可靠性

分类：六大约束  
+ NOT NULL：非空，用于保证该字段的值不能为空。比如姓名、学号等
+ DEFAULT：默认，用于保证该字段有默认值。比如性别
+ PRIMARY KEY：主键，用于保证该字段的值具有唯一性，并且非空。比如学号、员工编号
+ UNIQUE：唯一，用于保证该字段的值具有唯一性，可以为空。比如座位号，邮箱
+ CHECK：检查约束[mysql中不支持]。比如年龄，性别
+ FOREIGN KEY：外键，用于限制两个表的关系，用于保证改字段的值必须来自主表的关联列的。在从表添加外键的约束，用于引用主表中某列的值
比如专业编号，员工表的部门编号，员工表的工种编号。

添加约束的时机： 
1. 创建表时
2. 修改表时

约束的添加分类：  
列级约束：六大约束在语法上都支持，但外键约束没有效果  
表级约束：除了非空、默认，其他都支持  

>  	 SELECT TABLE 表名(  
>		字段名 字段类型 列级约束,  
>		字段名 字段类型,  
>		表级约束  
>       )  

主键和唯一的对比：

| |保证唯一性|是否允许为空|一个表中可以有几个|
|:---:|:---:|:---:|:---:|
|主键|√|否|至多有一个|
|唯一|√|是|可以有多个|

外键：  
1. 要求在从表设置外键关系
2. 从表的外键列的类型和主表的关联列的类型要求一致或兼容
3. 主表的关联列一般是一个key（主键、唯一）
4. 插入数据时，先插入主表，再插入从表；删除数据时。先删除主表，再删除从表。


#### 1. 添加列级约束
* 语法：
* 直接在字段名和类型后追加约束类型
* 只支持：默认、非空、主键、唯一
####  2. 添加表级约束
* 语法：在各个字段的最下面
* 【CONSTRAINT 约束名】 约束类型（字段名）

| |位置|支持的约束类型|是否可以起约束名|
|:---:|:---:|:---:|:---:|
|列级约束|列的后面|语法都支持，但外键没有效果|不可以|
|表级约束|所有列的下面|默认非空都不支持，其他都支持|可以，（主键没有效果）|

## TCL语言
### 事务
#### 含义
事务：一条或多条sql语句组成一个执行单位，一组sql语句妖媚都执行，要么都不执行
#### 特点（ACID）
A: 原子性：一个事务是不可再分割的整体，要么都执行要么都不执行。  
C: 一致性：一个事务可以使数据从一个一致状态切换到另外一个一致的状态
I: 隔离性：一个事务的执行不受其他事务的干扰。
D: 持久性：一个事务一旦提交，则永久的持久化本地

#### 事务的使用步骤
了解：  
隐式(自动)事务：没有明显的开始和结束，本身就是一条事务可以自动提交，比如INSERT、UPDATE、DELETE  
显式事务事务：具有明显的开启和结束

使用显式事务

    



     
