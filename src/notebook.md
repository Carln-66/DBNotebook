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

### 基础查询
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
   
### 条件查询
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
   
### 排序查询
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
   
### 常见函数
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
   
#### 分组查询
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

#### 连接查询
说明：当查询中涉及到了多个字段，则需要通过多表连接  
笛卡尔乘积：  
出现原因：没有有效的连接条件  
解决办法：添加有效的连接条件  
---------------------------SQL92语法-----------------------------
 语法：  
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

---------------------------SQL99语法-----------------------------
内连接语法：  
> SELECT 查询列表  
> FROM 表1 别名1  
> [INNER] JOIN 表2 别名2 ON 连接条件  
> [INNER] JOIN 表3 别名3 ON 连接条件    
> WHERE 筛选条件  
> GROUP BY 分组列表  
> HAVING 分组后筛选  
> ORDER BY 排序列表
   
   

    



     
