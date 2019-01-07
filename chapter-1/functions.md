## mysql提供的函数

- ### DATE_ADD()

> DATE_ADD为DATE(日期)添加指定的时间间隔.

```
// 用法
DATE_ADD(date, INTERVAL expr type)

// date: 指的是合法的日期表达式
// expr: 指定的时间间隔(数字)
// type: 时间间隔的类型
```


Type值 | 含义
---|---
YEAR  | 年
MONTH | 月
WEEK | 周
DAY | 天
HOUR | 小时
QUARTER | 刻
MINUTE | 分钟
SECONDE | 秒
MICROSECOND | 微秒
SECOND_MICROSECOND | 秒&微秒
MINUTE_MICROSECOND | 分钟&微秒
MINUTE_SECOND | 分钟&秒
HOUR_MICROSECOND | 小时&微秒
HOUR_SECOND | 小时&秒
HOUR_MINUTE | 小时&分钟
DAY_MICROSECOND | 日期&微秒
DAY_SECOND | 日期&秒
DAY_MINUTE | 日期&分钟
DAY_HOUR | 日期&小时
YEAR_MONTH | 年&月份

例子:

```
// Orders表

+------------------------------------------------
|    work_id          |        work_date         
|    1                |        2019-01-07 12:24:23
+------------------------------------------------

SQL> SELECT work_id, DATE_ADD(work_date, INTERVAL 25 DAY) AS NEXTWORKTIME FROM date_example

+------------------------------------------------
|    work_id          |        work_date         
|    1                |        2019-02-01  12:24:23
+------------------------------------------------
 
```
DATE_ADD(work_date, INTERVAL 25 DAY): 在work_date的基础上加25天整.

- ### DATE_SUB()

> DATE_SUB则是与DATE_ADD相反, 用于在日期中减去指定的时间间隔.

```
// 用法
DATE_SUB(date, INTERVAL expr type)

// date: 指的是合法的日期表达式
// expr: 指定的时间间隔(数字)
// type: 时间间隔的类型
```

Type值 | 含义
---|---
YEAR  | 年
MONTH | 月
WEEK | 周
DAY | 天
HOUR | 小时
QUARTER | 刻
MINUTE | 分钟
SECONDE | 秒
MICROSECOND | 微秒
SECOND_MICROSECOND | 秒&微秒
MINUTE_MICROSECOND | 分钟&微秒
MINUTE_SECOND | 分钟&秒
HOUR_MICROSECOND | 小时&微秒
HOUR_SECOND | 小时&秒
HOUR_MINUTE | 小时&分钟
DAY_MICROSECOND | 日期&微秒
DAY_SECOND | 日期&秒
DAY_MINUTE | 日期&分钟
DAY_HOUR | 日期&小时
YEAR_MONTH | 年&月份

例子:

```
// Orders表

+----------------------------------------------------
|    work_id          |        work_date         
|    1                |        2019-01-07 12:24:23
+----------------------------------------------------

SQL> SELECT work_id, DATE_SUB(work_date, INTERVAL 5 DAY) AS NEXTWORKTIME FROM date_example

+----------------------------------------------------
|    work_id          |        work_date         
|    1                |        2019-01-02  12:24:23
+----------------------------------------------------
 
```
DATE_SUB(work_date, INTERVAL 25 DAY): 在work_date的基础上减掉5天整.

- ### DATEDIFF()

> DATEDIFF是返回两个日期之间的天数(只有值的日期部分参与计算).

```
// 用法
DATEDIFF(date1,date2)

// date1 / date2: 指的是合法的日期或日期/时间表达式
```

例子:

```
SQL> SELECT DATEDIFF('2018-12-30','2018-12-31') AS DiffDate

+---------------------
|    DiffDate               
|    -1                
+---------------------

SQL> SELECT DATEDIFF('2018-12-30','2018-12-29') AS DiffDate

+---------------------
|    DiffDate               
|    1               
+---------------------

```
DATEDIFF('2018-12-30','2018-12-31'): 计算2018-12-30与2018-12-31之间的天数间隔.

- ### DATE_FORMAT()

> DATE_FORMAT用于按照规则的格式输出日期数据.

```
// 用法
DATE_FORMAT(date, format)
```

format格式 | 描述
---|---
%a | 缩写星期名
%b | 缩写月名
%c | 月，数值
%D | 带有英文前缀的月中的天
%d | 月的天，数值（00-31）
%e | 月的天，数值（0-31）
%f	| 微秒
%H	| 小时（00-23）
%h	| 小时（01-12）
%I	| 小时（01-12）
%i	| 分钟，数值（00-59）
%j	| 年的天（001-366）
%k	| 小时（0-23）
%l	| 小时（1-12）
%M	| 月名
%m	| 月，数值（00-12）
%p	| AM 或 PM
%r	| 时间，12-小时（hh:mm:ss AM 或 PM）
%S	| 秒（00-59）
%s	| 秒（00-59）
%T	| 时间, 24-小时（hh:mm:ss）
%U	| 周（00-53）星期日是一周的第一天
%u	| 周（00-53）星期一是一周的第一天
%V	| 周（01-53）星期日是一周的第一天，与 %X 使用
%v	| 周（01-53）星期一是一周的第一天，与 %x 使用
%W	| 星期名
%w	| 周的天（0=星期日, 6=星期六）
%X	| 年，其中的星期日是周的第一天，4 位，与 %V 使用
%x	| 年，其中的星期一是周的第一天，4 位，与 %v 使用
%Y	| 年，4 位
%y	| 年，2 位

```
SQL> SELECT  
     DATE_FORMAT(NOW(),'%b %d %Y %h:%i %p') AS 'DATE(%b %d %Y %h:%i %p)',
     DATE_FORMAT(NOW(),'%m-%d-%Y') AS 'DATE(%m-%d-%Y)',
     DATE_FORMAT(NOW(),'%Y-%m-%d') AS 'DATE(%Y-%m-%d)',
     DATE_FORMAT(NOW(),'%d %b %Y %T:%f') AS 'DATE(%d %b %Y %T:%f)'

// 结果:

+-----------------------------------------------------------------------------------------
| DATE(%b %d %Y %h:%i %p) | DATE(%m-%d-%Y) | DATE(%Y-%m-%d) | DATE(%d %b %Y %T:%f)
| Jan 07 2019 01:38 PM    | 01-07-2019     | 2019-01-07     | 07 Jan 2019 13:38:43:000000
+-----------------------------------------------------------------------------------------
```

- ### NOW() | CURDATE() | CURTIME()

> NOW() | CURDATE() | CURTIME() 分别用于返回当前的日期和时间, 日期, 时间.

```
SQL> SELECT NOW(), CURDATE(), CURTIME()

+-------------------------------------------------
| NOW()               | CURDATE()    | CURTIME() 
| 2019-01-07 13:58:40 | 2019-01-07   | 13: 58:40
+-------------------------------------------------

```

- ### DATE()

> DATE用于提取日期数据的日期部分.

```
SQL> SELECT DATE('2019-01-07 13:58:40') AS DATE()

+-------------------
| DATE()           
| 2019-01-07
+-------------------

```

- ### EXTRACT()

> EXTRACT 函数用于返回日期的单独部分, 例如年, 月, 日, 小时, 分钟等.

```
// 用法
EXTRACT(unit FROM date)
```


header 1 | header 2
---|---
row 1 col 1 | row 1 col 2
row 2 col 1 | row 2 col 2

unit值 | 含义
---|---
YEAR  | 年
MONTH | 月
WEEK | 周
DAY | 天
HOUR | 小时
QUARTER | 刻
MINUTE | 分钟
SECONDE | 秒
MICROSECOND | 微秒
SECOND_MICROSECOND | 秒&微秒
MINUTE_MICROSECOND | 分钟&微秒
MINUTE_SECOND | 分钟&秒
HOUR_MICROSECOND | 小时&微秒
HOUR_SECOND | 小时&秒
HOUR_MINUTE | 小时&分钟
DAY_MICROSECOND | 日期&微秒
DAY_SECOND | 日期&秒
DAY_MINUTE | 日期&分钟
DAY_HOUR | 日期&小时
YEAR_MONTH | 年&月份

```
SQL> SELECT EXTRACT(YEAR FROM NOW()) AS YEAR,
            EXTRACT(MONTH FROM NOW()) AS MONTH,
            EXTRACT(DAY FROM NOW()) AS DAY

+-------------------------------------------------
| YEAR               | MONTH   | DAY
| 2019               | 1       | 7
+-------------------------------------------------

```

- ### CONCAT()

> 使用字符串连接函数 CONCAT()

CONCAT(str1, str2...), 返回结果为连接参数产生的字符串.

注意:

1. 如果任意一个参数为NULL,则返回值为NULL
2. 如果所有参数均为非二进制字符串, 则结果为非二进制字符串;
3. 如果自变量中含任意二进制字符串, 则结果为一个二进制字符串;
4. 一个数字参数会被转化为二进制字符串格式, 为了避免可以使用显式类型cast

```
SQL> SELECT CONCAT('主机名: ', Host, ', 姓名: ',  User) AS '用户信息' FROM user

用户信息
----------------
主机名:localhost, 姓名: mysql.sys
主机名:localhost, 姓名: root
...

-----------------------------------------------

SQL> SELECT CONCAT('主机名: ', Host, ', 姓名: ',  User, NULL) AS '用户信息' FROM user

用户信息
-----------------
NULL
NULL
...
```

> 向某字段追加字符串

```
SQL> UPDATE table_name set field=CONCAT(field, '', str);
```
- ### CONCAT_WS()

> 使用CONCAT_WS(separator, str1, str2...)

```
SQL> SELECT CONCAT_WS('!', '主机名', Host, '姓名', NULL, User) AS '用户信息' FROM user

用户信息
-------------------
主机名!localhost!姓名!mysql.sys
主机名!localhost!姓名!root
...

// 注意, 存在NULL值时,返回值不为NULL,而是被忽略
```
- ### group_concat()

> 使用group_concat函数, 将组合中的列数据拼接

group_concat([DISTINCT] propName [ORDER BY ASC/DESC propName] [SEPARATOR '分隔符'])

```
SQL> SELECT id, group_concat(name separator ';') from aa group by id;

1 | 10;20;20
2 | 20
...

-----------------------------------
// 去重

SQL> SELECT id, group_concat(distinct name separator ';') from aa group by id;

1 | 10;20
2 | 20
...

// 去除name列的重复数据后使用;符号拼接
```

- ### repeat()

> 使用repeat()函数

repeat(str, times)

```
SQL> SELECT repeat(User, 2) from user

rootroot
mysqlmysql
...
```