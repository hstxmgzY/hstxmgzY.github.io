# SQL语句复习

## SQL概述

+ SQL（Structured Query Language）
	+ 结构化查询语言，是关系数据库的标准语言
+ SQL是一个通用的、功能极强的关系数据库语言

### SQL的特点

#### 综合统一

+ 集**数据定义语言（DDL）**，**数据操纵语言（DML）**，**数据控制语言（DCL）**功能于一体。
+ 可以独立完成数据库生命周期中的全部活动：
	+ 定义和修改、删除关系模式，定义和删除视图，插入数据，建立数据库;
	+ 对数据库中的数据进行查询和更新;
	+ 数据库重构和维护
	+ 数据库安全性、完整性控制，以及事务控制
	+ 嵌入式SQL和动态SQL定义
+ 用户数据库投入运行后，可根据需要随时逐步修改模式，不影响数据库的运行。
+ 数据操作符统一

#### 高度非过程化

+ 非关系数据模型的数据操纵语言“面向过程”，必须指定存取路径。
+ SQL只要提出“做什么”，无须了解存取路径。
+ 存取路径的选择以及SQL的操作过程由系统自动完成。

#### 面向集合的操作方式

+ 非关系数据模型采用面向记录的操作方式，操作对象是一条记录
+ SQL采用集合操作方式
	+ 操作对象、查找结果可以是元组的集合
	+ 一次插入、删除、更新操作的对象可以是元组的集合

#### 以同一种语法结构提供多种使用方式

+ SQL是独立的语言
	+ 能够独立地用于联机交互的使用方式
+ SQL又是嵌入式语言
	+ SQL能够嵌入到高级语言（例如C，C++，Java）程序中，供程序员设计程序时使用

#### 语言简洁，易学易用

SQL功能极强，完成核心功能只用了9个动词。

|   SQL 功   能    |          动词          |
| :--------------: | :--------------------: |
|   数 据 查 询    |         SELECT         |
| 数 据 定 义(DDL) |  CREATE，DROP，ALTER   |
| 数 据 操 纵(DML) | INSERT，UPDATE，DELETE |
| 数 据 控 制(DCL) |     GRANT，REVOKE      |

### SQL基本概念

SQL支持关系数据库三级模式结构

![image-20240330141956615](SQL%E9%A2%98%E5%8D%95.assets/image-20240330141956615.png)

#### 基本表

+ 本身独立存在的表
+ SQL中一个关系就对应一个基本表
+ 一个（或多个）基本表对应一个存储文件
+ 一个表可以带若干索引

#### 存储文件

+ 逻辑结构组成了关系数据库的内模式
+ 物理结构对用户是隐蔽的

#### 视图

+ 从一个或几个基本表导出的表
+ 数据库中只存放视图的定义而不存放视图对应的数据
+ 视图是一个虚表
+ **用户可以在视图上再定义视图**

## 数据更新

### 插入数据

+ 两种插入数据方式
  + 插入元组
  + 插入子查询结果
    + 可以一次插入多个元组 

#### 插入元组

+ **语句格式**
	```sql
    INSERT
    INTO <表名> [(<属性列1>[,<属性列2 >…)]
    VALUES (<常量1> [,<常量2>]… );
	```

+ **功能**

	+ 将新元组插入指定表中

+ **INTO子句**

	+ 指定要插入数据的表名及属性列
	+ 属性列的顺序可与表定义中的顺序不一致
	+ 没有指定属性列：表示要插入的是一条完整的元组，且属性列属性与表定义中的顺序一致
	+ 指定部分属性列：插入的元组在其余属性列上取空值

+ VALUES子句

	+ 提供的值必须与INTO子句匹配
  	+ 值的个数
  	+ 值的类型

#### 插入子查询结果(这个重要 因为我不知道)

+ **语句格式**
	
	```sql
	INSERT
    INTO <表名> [(<属性列1> [,<属性列2>… )]
    子查询;
	```
	
+ INTO子句

+ 子查询

  + SELECT子句目标列必须与INTO子句匹配
    + 值的个数
    + 值的类型

#### 题单

##### [**插入记录（二）**](https://www.nowcoder.com/practice/9681abf28745468c8adacb3b029a18ce?tpId=240&tqId=2223554&ru=%2Fpractice%2Fbfe8ad2bddc540fc911614aa648868b3&qru=%2Fta%2Fsql-advanced%2Fquestion-ranking&sourceUrl=%2Fexam%2Fcompany)

```sql
INSERT INTO exam_record_before_2021(uid,exam_id,start_time,submit_time,score)
SELECT uid,exam_id,start_time,submit_time,score FROM exam_record
WHERE submit_time < '2021-01-01 00:00:00'
```

##### [**插入记录（三）**](https://www.nowcoder.com/practice/978bcee6530a430fb0be716423d84082?tpId=240&tags=&title=&difficulty=0&judgeStatus=0&rp=0&sourceUrl=%2Fexam%2Fcompany)

如果要插入一个主键与表中原有数据一样的新内容，我们可以用以下两种方法来实现修改：

参考题解[题解 | #插入记录（三）#](https://blog.nowcoder.net/n/a1f793bcbece4c0295f16e403903c655)

###### 方法1（REPLACE INTO...VALUES)

```sql
REPLACE INTO examination_info
VALUES(NULL,9003,'SQL','hard',90,'2021-01-01 00:00:00');
```

> 关键字NULL可以用DEFAULT替代。

`replace into` 跟 `insert into`功能类似，不同点在于：`replace into` 首先尝试插入数据到表中，

1. 如果发现表中已经有此行数据（根据主键或者唯一索引判断）则先删除此行数据，然后插入新的数据；
2. 否则，直接插入新数据。

要注意的是：插入数据的表**必须有主键或者是唯一索引**！否则的话，replace into **会直接插入数据**，这将导致表中出现重复的数据。

###### 方法2（先删再插）

```sql
DELETE FROM examination_info
WHERE exam_id = 9003;

INSERT INTO examination_info
VALUES(NULL,9003, 'SQL','hard', 90, '2021-01-01 00:00:00')
```

### 修改数据

+ **语句格式**
  ```sql
  UPDATE <表名>
    SET <列名>=<表达式>[,<列名>=<表达式>]…
    [WHERE <条件>];
  ```
  
+ **功能**

  + 修改指定表中满足WHERE子句条件的元组
  + SET子句给出<表达式>的值用于取代相应的属性列
  + **如果省略WHERE子句，表示要修改表中的所有元组**

+ **批量更新**

  - 使用 `if` 不同条件更新不同内容
    - 符合`条件1`，给列赋值`值1`，不符合则赋值`值2`

  ```sql
  update 表名 
  set 
  	列名1 = if(条件1,值1,值2),
    列名2 = if(条件2,值3,值4)
  [where 条件];
  ```

  - 使用 `case when` 不同条件更新不同内容

  ```sql
  update 表名 
  set 列名1 =
      case
          when 条件1 then 值1
          when 条件2 then 值2
          ...
      end,
      列名2 =
      case
          when 条件21 then 值21
          when 条件22 then 值22
          ...
      end
  [where 条件];
  ```

#### 题单

##### [更新记录（二）](https://www.nowcoder.com/practice/0c2e81c6b62e4a0f848fa7693291defc?tpId=240&tags=&title=&difficulty=0&judgeStatus=0&rp=0&sourceUrl=%2Fexam%2Fcompany)

参考题解[题解 114 | #更新记录（二）#](https://blog.nowcoder.net/n/423d7c2589674c1eb98e616442136a34)

###### 方法1

```sql
UPDATE exam_record
SET submit_time = '2099-01-01 00:00:00', score = 0
WHERE start_time < '2021-09-01 00:00:00' and submit_time is NUll
```

> 注意 为空值不可以写 = ’None‘
>
> 另外 时间最好和下面这样写

```sql
update exam_record 
set 
    submit_time = '2099-01-01 00:00:00',
    score = 0
where date(start_time) < date('2021-09-01') and score is null
```

###### 方法2

```sql
update exam_record 
set 
    submit_time = if(date(start_time) < date('2021-09-01') and score is null,'2099-01-01 00:00:00',submit_time),
    score = if(date(start_time) < date('2021-09-01') and score is null,0,score)
```

###### 方法3

```sql
update exam_record 
set 
    submit_time = case
        when date(start_time) < date('2021-09-01') and score is null then '2099-01-01 00:00:00'
        else submit_time
    end,
    score = case
        when date(start_time) < date('2021-09-01') and score is null then 0
        else score
    end
```

### 删除数据

+ 语句格式
	```sql
    DELETE
    FROM     <表名>
    [WHERE <条件>];
  ```

+ 功能

	+ 删除指定表中满足WHERE子句条件的元组

+ WHERE子句

	+ 指定要删除的元组
	+ **缺省表示要删除表中的全部元组，表的定义仍在字典中**

#### 题单

##### [删除记录（一）](https://www.nowcoder.com/practice/d331359c5ca04a3b87f06b97da42159c?tpId=240&tags=&title=&difficulty=0&judgeStatus=0&rp=0&sourceUrl=%2Fexam%2Fcompany)

参考题解[题解 115 | #删除记录（一）#](https://blog.nowcoder.net/n/694e8541a6764d93b175db0a6cec1b58)

> 删除exam_record表中作答时间小于5分钟整且分数不及格（及格线为60分）的记录；

> 这题其实挺简单，但是有一个时间的问题需要掌握

###### 方法一 **日期减去日期得到分钟**

`timestampdiff`函数

```sql
delete from exam_record
where timestampdiff(minute, start_time, submit_time) < 5 
and score < 60
```

###### 方法二、**日期减去(加上)分钟得到日期**

`date_sub`函数

```sql
delete from exam_record
where date_sub(submit_time, interval 5 minute ) < start_time 
and score < 60
```

`date_add`函数

```sql
delete from exam_record
where date_add(start_time, interval 5 minute ) > submit_time 
and score < 60
```

##### [删除记录（二）](https://www.nowcoder.com/practice/964c9f7fffbb4ab18b507cfed4111b4a?tpId=240&tqId=2223562&ru=%2Fpractice%2F0c2e81c6b62e4a0f848fa7693291defc&qru=%2Fta%2Fsql-advanced%2Fquestion-ranking&sourceUrl=%2Fexam%2Fcompany)

> 删除exam_record表中未完成作答或作答时间小于5分钟整的记录中，开始作答时间最早的3条记录。

```sql
DELETE FROM exam_record
WHERE (
    submit_time IS NULL OR
    timestampdiff(minute, start_time, submit_time) < 5
)
ORDER BY start_time
LIMIT 3
```

[删除记录（三）](https://www.nowcoder.com/practice/3abefc6fc73e4f219dad0ab66e6b1e3f?tpId=240&tqId=2223563&ru=%2Fpractice%2F964c9f7fffbb4ab18b507cfed4111b4a&qru=%2Fta%2Fsql-advanced%2Fquestion-ranking&sourceUrl=%2Fexam%2Fcompany)

> 删除exam_record表中所有记录，并重置自增主键。

```sql
TRUNCATE exam_record
-- 或
DELETE FROM exam_record;
ALTER TABLE exam_record auto_increment=1;
```

这两种方法都用于清空数据库表中的数据，但它们在执行方式、性能、以及对数据库表的影响上有所不同。

1. **TRUNCATE TABLE:**
   - **执行方式：** TRUNCATE TABLE 是一个 DDL（数据定义语言）操作，它以原子操作的方式从表中删除所有数据，并重置表的自增长计数器（如果有的话）。
   - **性能：** 通常来说，TRUNCATE TABLE 的性能比 DELETE 更高，因为它是一个直接操作，不会逐行地删除记录，而是直接删除整个表中的数据。这意味着它更快，尤其是当表中有大量数据时。
   - **影响：** TRUNCATE TABLE 会重置自增长计数器，因此表的下一个插入操作将从 1 开始。
   - **注意事项：** TRUNCATE TABLE 无法撤销，而且在一些数据库中，执行 TRUNCATE TABLE 时可能会造成锁表，导致其他用户无法访问该表。

2. **DELETE FROM:**
   - **执行方式：** DELETE FROM 是一个 DML（数据操作语言）操作，它以逐行方式删除表中的数据。
   - **性能：** DELETE FROM 操作通常比 TRUNCATE TABLE 慢，因为它需要逐行扫描表并删除记录，而且会生成事务日志，这会增加额外的开销。
   - **影响：** DELETE FROM 不会重置自增长计数器，除非显式地使用 ALTER TABLE 语句来重置。
   - **注意事项：** DELETE FROM 是可以撤销的操作，因为它可以在事务中使用，并且可以针对每一行执行触发器和约束。但是，在大型表上执行 DELETE 操作可能会导致事务日志增长过快，甚至消耗大量系统资源。

**总结：**
- 如果你只是想删除表中的所有数据并重置自增长计数器，而且不需要考虑事务日志或触发器的影响，那么使用 TRUNCATE TABLE 通常是更好的选择，因为它更快速、更简单。
- 如果你需要逐行地删除数据，或者需要在事务中执行删除操作以便于撤销，那么使用 DELETE FROM 是更合适的选择，尽管它的性能可能比 TRUNCATE TABLE 差一些。

#### 删除拓展

参考 [酸菜鱼土豆大侠](https://blog.csdn.net/chengyj0505)

[原文链接](https://blog.csdn.net/chengyj0505/article/details/128358817)侵权立刻马上删掉qaq

![插入语句 方法分类](SQL%E9%A2%98%E5%8D%95.assets/b5d6a28c63294cdf9a1d9f78e086b668.png)

|           类型           |                          语句                          |
| :----------------------: | :----------------------------------------------------: |
|    删除全部/部分记录     |             delete from 表名 [where 条件];             |
|    删除表的结构和数据    |              drop table [if exists] 表名;              |
| 删除所有记录并重置自增ID |                 truncate [table] 表名;                 |
|         批量删除         | delete from 表名 where key in(value1,value2,…,valuen); |

!!! note "注意事项"

+ 使用`DELETE`的注意事项
  + `DELETE`是DML语句，**可回滚**；
  + 不加`WHERE`条件时，`DELETE`删除表中所有记录；
  + `DELETE` 删除的是表中的内容而不是表，删除后表结构不变；不会重置表的自增值；
  + 执行`DELETE`后**不会减少表或索引所占用的空间**；
  + **删除效率低**。所以多用于删除表中部分记录。

+ 使用`DROP`的注意事项
  + `DROP`是DDL语句，**执行后无法回滚**；
  + `DROP`删除表的结构及其所依赖的约束、索引等；
  + 执行`DROP`语句后会把**表所占用的空间全释放掉**。
+ 使用`truncate`的注意事项
  + 执行`truncate`语句需要拥有drop表的权限，DDL语句，执行后不能回滚；
  + `truncate`的作用是截断表或者清空表，并且只能作用于表；
  + `truncate`会清空表中的所有行，**但表结构及其约束、索引等保持不变**；
  + `truncate`会**重置表的自增值**；
  + 执行`truncate`后会使表和索引所占用的空间会恢复到初始大小；
  + 删除表中所有记录时`truncate`比`delect`执行速度快。
    + `truncate`类似于`delete`删除所有行的语句并重置自增值或`drop table`然后再`create table`语句的组合。
+ 执行大批量删除的时候最好使用`limit`，否则很有可能造成死锁。如果`delete`的`where`语句不在索引上，可以先找主键，然后根据主键删除数据。
+ 如果需要删除的数据远远大于不用删除的数据
	+ 先选择不需要删除的数据，并把它们存在一张相同结构的空表里；
	+ 再重命名原始表，并给新表命名为原始表的原始表名；
	+ 然后删掉原始表。

+ 如果需要删除超大批量数据
	+ 先删除表中索引；
	+ 再删除需要删除的数据；
	+ 然后重新创建索引。


## 日期函数与时间函数

参考（其实基本就是佬的内容，因为我不知道怎么改，他写的太好了555） [酸菜鱼土豆大侠](https://blog.csdn.net/chengyj0505)

[原文链接](https://blog.csdn.net/chengyj0505/article/details/128754760)侵权立刻马上删掉qaq

另外找到的一个非常nice的cookbook

[MySQL日期函数](https://www.begtut.com/sql/sql-ref-mysql.html)

### 日期和时间类型

表示时间值的日期和时间类型为DATETIME、DATE、TIMESTAMP、TIME和YEAR。

|   类型    |        格式         |           描述           |
| :-------: | :-----------------: | :----------------------: |
|   DATE    |     YYYY-MM-DD      |          日期值          |
|   TIME    |      HH:MM:SS       |     时间值或持续时间     |
|   YEAR    |        YYYY         |          年份值          |
| DATETIME  | YYYY-MM-DD hh:mm:ss |     混合日期和时间值     |
| TIMESTAMP | YYYY-MM-DD hh:mm:ss | 混合日期和时间值，时间戳 |

### 具体方法

#### 获取年、月、日、周等

|          函数           |                       描述                       |
| :---------------------: | :----------------------------------------------: |
|       year(date)        |                     返回年份                     |
|      quarter(date)      |       返回日期date是第几季节，返回 1 到 4        |
|       month(date)       |         返回日期date中的月份值，1 到 12          |
|       week(date)        | 计算日期 date 是本年的第几个星期，范围是 0 到 53 |
|        day(date)        |            返回日期值 date 的日期部分            |
|       hour(time)        |               返回 date 中的小时值               |
|      minute(time)       |               返回 date 中的分钟值               |
|      second(time)       |                返回 t 中的秒钟值                 |
|    microsecond(time)    |            返回日期参数所对应的微秒数            |
| extract(type from date) |  从日期 date 中获取指定的值，type 指定返回的值   |
|      weekday(date)      | 日期 date 是星期几，0 表示星期一，1 表示星期二…  |

`SELECT EXTRACT(MONTH FROM date_column) AS month FROM table_name;`

**type的取值：**

+ year(年)
+ quarter(季)
+ month(月)
+ week(周)
+ day(天)
+ hour(小时)
+ minute(分钟)
+ second(秒)
+ microsecond(毫秒)

#### 获取年月、年月日等

|              函数              |                            描述                            |
| :----------------------------: | :--------------------------------------------------------: |
|        year、month、day        |                   使用and连接单个返回值                    |
| date_format(event_time,’unit‘) |                        按照unit取值                        |
| substring(date, start, length) | 从字符串 str 的 start 位置开始截取长度为 length 的子字符串 |
|         date(datetime)         |                返回datetime中的日期date部分                |
|              like              |                          模糊查询                          |

 `DATE_FORMAT()` 用于将日期时间值按照指定的格式转换成字符串。它接受两个参数：日期时间值和格式字符串。

- `%Y-%m-%d`：表示年-月-日格式，例如："2024-03-30"
- `%Y/%m/%d %H:%i:%s`：表示年/月/日 小时:分钟:秒格式，例如："2024/03/30 15:25:10"
- `%d-%m-%Y %H:%i`：表示日-月-年 小时:分钟格式，例如："30-03-2024 15:25"



**`unit`的取值：**

```
%M 月名字(January……December) 
%W 星期名字(Sunday……Saturday) 
%D 有英语前缀的月份的日期(1st, 2nd, 3rd, 等等。） 
%Y 年, 数字, 4 位 
%y 年, 数字, 2 位 
%a 缩写的星期名字(Sun……Sat) 
%d 月份中的天数, 数字(00……31) 
%e 月份中的天数, 数字(0……31) 
%m 月, 数字(01……12) 
%c 月, 数字(1……12) 
%b 缩写的月份名字(Jan……Dec) 
%j 一年中的天数(001……366) 
%H 小时(00……23) 
%k 小时(0……23) 
%h 小时(01……12) 
%I 小时(01……12) 
%l 小时(1……12) 
%i 分钟, 数字(00……59) 
%r 时间,12 小时(hh:mm:ss [AP]M) 
%T 时间,24 小时(hh:mm:ss) 
%S 秒(00……59) 
%s 秒(00……59) 
%p AM或PM 
%w 一个星期中的天数(0=Sunday ……6=Saturday ） 
%U 星期(0……52), 这里星期天是星期的第一天 
%u 星期(0……52), 这里星期一是星期的第一天 
%% 一个文字“%”。 
```

#### 两个日期时间的整数差

| 函数                                            | 描述                                    |
| ----------------------------------------------- | --------------------------------------- |
| datediff(date_1,date_2)                         | 返回日期 date_1 - date_2 之间相隔的天数 |
| `TIMESTAMPDIFF(interval, time_start, time_end)` | 返回 time_end − time_start 的时间差     |
| timediff(time_1, time_2)                        | 返回time_1 - time_2 的时间差值          |

> 参数说明：
>
> + `interval`：参数确定（end-start）结果的单位，表示为整数。可以填year(年)、quarter(季)、month(月)、week(周)、day(天)、hour(小时)、minute(分钟)、second(秒)、microsecond(毫秒)。
> + 注意`TIMESTAMPDIFF(interval, time_start, time_end)`函数中前面那个时间是开始时间，后面那个是结束时间，和其他的相反！！！！！
> 	+ TIMESTAMPDIFF(interval, time_start, time_end)可计算time_start-time_end的时间差，单位以指定的interval为准.

!!! note "Q: 什么时候使用datediff？什么时候使用timestampdiff？什么时候使用timediff？"
+ 三个函数的区别主要在于对象的不同一个是日期，一个是时间，另外一个既可以是日期格式也可以是时间格式。
+ timestampdiff更加灵活，既可以对日期求整数差也可以对时间求整数差。而datediff只能求日期的天数差。"



#### 日期减去/加上天数得到日期 

|                             函数                             |                      描述                       |
| :----------------------------------------------------------: | :---------------------------------------------: |
|              date_add(date,interval expr type)               |    返回起始日期 date 加上一个时间段后的日期     |
|              date_sub(date,interval expr type)               |        返回函数从日期减去指定的时间间隔         |
| [ADDTIME(*datetime*, *addtime*)](https://www.begtut.com/sql/func-mysql-addtime.html) | 返回n 是一个时间表达式，时间 t 加上时间表达式 n |
| [SUBTIME(*datetime*, *time_interval*)](https://www.begtut.com/sql/func-mysql-subtime.html) |             时间 t 减去 n 秒的时间              |

```sql
SELECT DATE_ADD("2017-06-15 09:34:21", INTERVAL 15 MINUTE); 
```

#### 日期date是周几

|          函数          |                       描述                       |
| :--------------------: | :----------------------------------------------: |
|     weekday(date)      | 日期 date 是星期几，0 表示星期一，1 表示星期二…  |
| date_format(date,‘%W’) |   日期 date 是星期几，Monday周一,Tuesday周二…    |
|       week(date)       | 计算日期 date 是本年的第几个星期，范围是 0 到 53 |

#### 某个月的最后一天

|      函数      |               描述               |
| :------------: | :------------------------------: |
| last_day(date) | 返回给定日期的那一月份的最后一天 |

#### 返回当前日期/时间

|           函数            |        描述        |
| :-----------------------: | :----------------: |
| curdate()、current_date() |    返回当前日期    |
| curtime()、current_time() |    返回当前时间    |
|           now()           | 返回当前日期和时间 |
