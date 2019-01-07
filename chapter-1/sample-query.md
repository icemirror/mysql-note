## 单表查询

### 1.1 查询表中所有的行与列

> desc table_name 查看表结构

```
SQL> desc  emp

Name      Type          Nullable   Default   Comments
------    --------      ---------  --------  --------
EMPNO     NUMBER(4)     Y                    编码
ENAME     VARCHAR2(10)  Y                    名称
...
```

> select * from table_name 返回目标表中所有的列

```
SQL> SELECT * FROM emp;

EMPNO    ENAME     JOB      MGR    ...
-----    -----     ----     -----
323      SMITH     CLERK    7902
455      JONES     ANALYST  9800
...
```

### 1.2 从表中检索部分行

> where 条件 查看公司多少销售人员

```
SQL> SELECT * FROM emp WHERE job = 'SALESMAN';

EMPNO    ENAME     JOB         MGR    ...
-----    -----     ----        -----
323      SMITH     SALESMAN    7902
455      JONES     SALESMAN    9800
...
```
### 1.3 查询空值

> 查询某一列为空的数据, 比如返回提成(comm)为空的数据:

```
SQL> SELECT * FROM emp WHERE comm = NULL;

no rows selected

```

==实际上, NULL是不能用“=”运算符的, 需要使用Mysql提供的运算符:==

- IS NULL
- IS NOT NULL
- <=> : 比较运算符, 当=左右两边都为NULL时, 返回true.

```
// 正确做法如下

SQL> SELECT * FROM emp WHERE comm IS NULL;

EMPNO    ENAME     JOB         comm    ...
-----    -----     ----        -----
323      SMITH     SALESMAN    
...
```

### 1.4 空值与运算

==实际上,NULL不支持加,减,乘,除,大小比较,相等比较,否则只能为空==


### 1.5 查找满足多个条件的行

> 查找组合条件, 如: 逻辑表达式(部门10的员工 OR 所有得到提成的员工 OR (工资 <= 2000 and 部门号=20)

```
SELECT *
  FROM EMP
 WHERE (DEPTNO = 10
        OR COMM IS NOT NULL
        OR (SAL <= 200 AND DEPTNO = 20));
EMPNO     ENAME   JOB       SAL     COMM    DEPTNO
-----     -----   ----      ----    ----    ------
763       JONES   SALESMAN  800     300     20
889       LILY    CLERK     2300            10
...
```

### 1.6 从表中检索部分列

> 查询表中部分列信息

```
SQL> SELECT empno, ename, hiredate FROM emp WHERE deptno = 10;

EMPNO   ENAME   HIREDATE    SAL
-----   -----   --------    ----
7790    JONES   2018-09-10  2450
8000    JAMES   2018-11-11  2000
...
```
### 1.7 为列取别名

> 使用as 或者直接在列名后跟别名

```
SQL> SELECT Host '主机名', User '用户名' FROM USER

// or

SQL> SELECT Host as '主机名', User as '用户名' FROM USER

主机名      用户名
------     ------
localhost   root
localhost   mysql
...
```

### 1.8 在WHERE子句中引用取别名的列

> 引用别名时千万别忘记嵌套一层, 因为这个别名在SELECT之后才有效

```
SQL> SELECT *
       FROM (SELECT sal AS '工资', comm AS '提成' FROM emp) x
      WHERE sal < 1000;
工资        提成
-----      --------
800         
900
...
```

### 参考内容

- [Oracle查询优化改写2.0(技巧与案例)](https://book.douban.com/subject/30253259/)
- [MySql - w3cshool](https://www.w3cschool.cn/mysql/mysql-tutorial.html)