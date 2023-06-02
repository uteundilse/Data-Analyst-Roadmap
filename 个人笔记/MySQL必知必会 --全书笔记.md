# MySQL必知必会

### 基础

1. Database 数据库 → Schema → Table  → Column : Datatype → Row : Primary Key主键
2. SHOW
    - `SHOW COLUMNS FROM orders;` == `DESCRIBE orders;`
    显示表每一列columns的信息
    Field — Typy — Null — Key — Default — Extra
    - `SHOW GRANTS;` 显示用户安全权限
3. **不区分大小写**
4. `‘’`单引号用来限定字符串，数值不需要
5. **日期格式：yyyy-mm-dd**
6. **关系表的设计**——保证把信息分解成多个表，一类数据一个表。各表通过某些常用的值（即关系设计中的关系（relational））互相关联。

### 检索 - 排序 - 过滤 - 计算

1. `SELECT`
    - `SELECT DIDSTINCT`
2. `FROM`
3. `WHERE` — 过滤行
    - `=` | `!=` | `<` | `<=` | `>` | `>=` | `BETWEEN AND`
    - `IS NULL`
    - 逻辑操作符
        - `AND`
        - `OR`
        - `()` 计算次序
        - `IN` — **IN执行速度比OR快**
        `WHERE product_id = 1002 OR product_id = 1003`  == `WHERE product_id IN (1002, 1003)`
        - `NOT`
    - `LIKE` 通配符
        - `%` — 任何字符出现任意次数
        - `_` — 单个字符
    - `REGEXP` **正则表达式**
        - `WHERE product_id REGEXP ‘1002’`
        - `.` 匹配任意一个字符
        - `|`  == OR
        - `[]`  括起来的任一值 或 **定义范围**
            - `[123]` == `1|2|3`
            - `[0-9]`
            - `[a-z]`
        - 匹配特殊字符 `\\` 前导 — **转义**
        - **定位符**
            
            `^` 文本的开始
            `$` 文本的结尾
            `[[:<:]]` 词的开始
            `[[:>:]]` 词的结尾
            
        - 匹配字符类
            
            `[:alnum:]` 任意字母和数字（同[a-zA-Z0-9]）
            `[:alpha:]` 任意字符（同[a-zA-Z]）
            `[:blank:]` 空格和制表（同[\\t]）
            `[:cntrl:]` ASCII控制字符（ASCII 0到31和127）
            `[:digit:]` 任意数字（同[0-9]）
            `[:graph:]` 与[:print:]相同，但不包括空格
            `[:lower:]` 任意小写字母（同[a-z]）
            `[:print:]` 任意可打印字符
            `[:space:]` 包括空格在内的任意空白字符（同[\\f\\n\\r\\t\\v]）
            `[:upper:]` 任意大写字母（同[A-Z]）
            `[:xdigit:]` 任意十六进制数字（同[a-fA-F0-9]）
            
        - 匹配多个实例
            
            `*`  0个或多个匹配
            `+` 1个或多个匹配（等于{1,}）
            `?` 0个或1个匹配（等于{0,1}）
            `{n}` 指定数目的匹配
            `{n,}` 不少于指定数目的匹配
            `{n,m}` 匹配数目的范围（m不超过255）
            
        - 例子
            - `sticks?` →匹配stick和sticks
            - `[[:digit:]]{4}` → 匹配连在一起的任意4位数字
4. `ORDER BY`
    - 指定降序 **DESC，**默认升序 ASC
    - **可用非选择的列排序**
    - 多个列排序
    `ORDER BY a, b;` — 先按照a排序，多个行具有相同的a时，按b排序
        - **DESC** 只应用于直接位于前面的列名
5. `LIMIT`
6. 子句
    - SELECT
    - FROM
    - WHERE
7. 计算字段
    - 拼接 **：**`Concat()` 
    `Concat(product_name, ‘(’, product_id, ‘)’)` → `watch(1002)`
    - **去掉空格**：`RTrim()` — `LTrim()` — `Trim()`
    - `AS` 别名

### 函数 - 文本、数值、时间和日期

1. **文本函数**
    - `Upper()` 将串转换为大写  — `Lower()`
    - `Left()` 返回串左边的字符 — `Right()` 返回串右边的字符
    - `Length()` 返回串的长度
    - `Locate()` 找出串的一个子串
    - `LTrim()` 去掉串左边的空格 — `RTrim()` 去掉串右边的空格— `Trim()`
    - `Soundex()` 返回**发音类似的字符串**
        
        ```sql
        SELECT cust_name, cust_contact
        From customers
        WHERE Soundex(cust_contact) = Soundex('Y Lie');
        
        --> Y Lee
        ```
        
    - `SubString()` 返回子串的字符
2. **数值函数**
    - `Abs()` 返回一个数的绝对值
    - `Cos()` 返回一个角度的余弦
    - `Exp()` 返回一个数的指数值
    - `Mod()` 返回除操作的余数
    - `Pi()` 返回圆周率
    - `Rand()` 返回一个随机数
    - `Sin()` 返回一个角度的正弦
    - `Sqrt()` 返回一个数的平方根
    - `Tan()` 返回一个角度的正切
3. **日期和时间函数**
    - `AddDate()` 增加一个日期（天、周等）
    `AddTime()` 增加一个时间（时、分等）
    - `CurDate()` 返回当前日期 
    `CurTime()` 返回当前时间
    `Now()` 返回当前日期和时间
    - `Date()` 返回日期时间的日期部分
    `Time()` 返回一个日期时间的时间部分
    `Year()` 返回一个日期的年份部分
    `Month()` 返回一个日期的月份部分
    `Day()` 返回一个日期的天数部分
    `Hour()` 返回一个时间的小时部分
    `Minute()` 返回一个时间的分钟部分
    `Second()` 返回一个时间的秒部分
    - `DateDiff()` **计算两个日期之差**
    - `Date_Add()` 高度灵活的日期运算函数
    - `Date_Format()` 返回一个格式化的日期或时间串
    - `DayOfWeek()` 对于一个日期，返回对应的星期几
    
    ```sql
    SELECT cust_id, order_num
    FROM orders
    WHERE Date(order_num) = '2020-01-01'
    ```
    
4. **系统函数**

### 汇总 - 聚合

1. 聚集函数 Aggregate function
    - `AVG()` 返回某列的平均值
        - 忽略列值为NULL的行
    - `COUNT()` 返回某列的行数
        - `COUNT(*)` — **包含空值NULL**
        - `COUNT(column)` — 忽略NULL
    - `MAX()` 返回某列的最大值
    - `MIN()` 返回某列的最小值
    - `SUM()` 返回某列值之和
    - 聚集函数默认计算ALL，可以**指定DISTINCT去重**

### 分组

1. GROUP BY
    - **不能使用别名** — 如果在SELECT中使用表达式，则必须在GROUP BY子句中指定相同的表达式。
    - 除聚集计算语句外，SELECT语句中的每个列都必须在GROUP BY子句中给出
    - 如果分组列中具有NULL值，则NULL将作为一个分组返回。
    如果列中有多行NULL值，它们将分为一组
    - `WITH ROLLUP` — **得到分组及分组汇总的值**
2. HAVING — 过滤分组
3. **WHERE — HAVING 区别**
    - WHERE在数据分组前进行过滤 — HAVING在数据分组后进行过滤
    - WHERE 过滤行 — HAVING 过滤分组
    
    ```sql
    # 含有2个以上、价格大于等于10以上产品的供应商，只显示前5个
    SELECT product_id, COUNT(*) AS num_prods
    FROM Products
    WHERE product_price >= 10
    GROUP BY product_id
    HAVING COUNT(*) >=2
    ORDER BY num_prods
    LIMIT 5
    ```
    

### 子查询

1. 在SELECT语句中，子查询总是**从内向外**处理
2. 过滤
3. 计算
4. **相关子查询** correlated subquery：涉及外部查询的子查询
    - 逐渐增加子查询来建立查询

### 联结表

1. **主键**（primary key）
2. **外键**（foreign key）:
外键为某个表中的一列，它包含另一个表的主键值，定义了两个表之间的关系
3. **可伸缩性**（scale）：能够适应不断增加的工作量而不失败，可伸缩性好（scale well）
4. 完全限定列名
5. **笛卡儿积（cartesian product）**：由没有联结条件的表关系返回的结果
6. 表别名
    1. `INNER JOIN`  
        - ON
        - USING
7. 联结类型
    - 自联结
        
        ```sql
        # 子查询
        SELECT product_id, product_name
        FROM Products
        WHERE vend_id = (SELECT vend_id FROM Products WHERE prodcut_id = 'FB')
        
        '''结果一致'''
        
        # 联结查询
        SELECT p1.product_id, p2.product_name
        FROM Products AS p1, Products AS p2
        WHERE p1.vend_id = p2.vned_id AND p2.product_id = 'FB'
        ```
        
    - 自然联结
    - 外部联结
        - `LEFT JOIN`
        - `RIGHT JOIN`

### **组合查询**

1. **UNION**
    - 把多条查询的结果作为一条组合查询返回
    - NION中的每个查询必须包含**相同的列、表达式或聚集函数**
    - 自动去除了重复的行
    - **UNION ALL**

### 全文本搜索：**ENGINE=MyISAM**

- 不在导入数据时使用FULLTEXT
- `Match()`：被搜索的列
- `Against()`：使用的搜索表达式

```sql
# 在Productnotes表中的note_text列搜索指定词'rabbit'
SELECT note_text
FROM Productnotes
WHERE Match(note_text) Against('rabbit');

'''结果一致'''

# LIKE
SELECT note_text
FROM Productnotes
WHERE note_text lIKE '%rabbit%';
```

- 全文本搜索不区分大小写
- **对结果排序：**具有较高等级的行先返回
- **查询扩展**
- **布尔方式**
    - 即使没有FULLTEXT索引也可以使用
    - **缓慢的操作**：其性能将随着数据量的增加而降低
    - 全文本布尔操作符
        - `+` 包含，词必须存在
        - `-` 排除，词必须不出现
        - `>` 包含，而且增加等级值
        - `<` 包含，且减少等级值
        - `()` 把词组成子表达式（允许这些子表达式作为一个组被包含、排除、排列等）
        - `~` 取消一个词的排序值
        - `*` 词尾的通配符
        - `""` 定义一个短语（与单个词的列表不一样，它匹配整个短语以
        便包含或排除这个短语）
    
    ```sql
    SELECT note_text
    FROM Productnotes
    
    # 使用查询扩展
    WHERE Match(note_text) Against('rabbit' WITH QUERY EXPANSION);
    
    # 使用布尔方式
    WHERE Match(note_text) Against('rabbit' IN BOOLEAN MODE);
    
    # 匹配包含heavy但不包含任意以rope开始的词的行
    WHERE Match(note_text) Against('heavy -rope*' IN BOOLEAN MODE);
    ```
    
- 如果一个词出现在50%以上的行中，则将它作为一个非用词忽略。50%规则不用于IN BOOLEANMODE。

### 插入数据 - 更新数据

1. INSERT
    - 插入完整的行；
        - `INSERT INTO Product VALUES (…………)`
        - `INSERT INTO Product(…………) VALUES (…………)` — 明确指定列名和数据
    - 插入行的一部分；
    - 插入多行；
    - **插入某些查询的结果**
        - `INSERT SELECT`
2. UPDATE
    - 更新表中特定行
        
        ```sql
        UPDATE Customers
        SET cust_email = 'ute@fudd.com'
        WHERE cust_id = 10005
        ```
        
        - 以要更新的表的名字开始
        - SET命令将新值赋给被更新的列 `列=值`
        - WHERE过滤
    - 更新表中所有行
    - 更新为NULL，可删除值
    `SET cust_email = NULL`
    - **忽略错误** — `UPDATE IGNORE table_name ……`
3. DELETE
    - 删除表中特定行
        
        ```sql
        DELETE FROM Customers
        WHERE cust_id = 10005
        ```
        
    - 删除表中所有行
4. `TRUNCATE TABLE` — 从表中删除所有行 ：**速度更快**
5. 使用UPDATE或DELETE前
    - 保证每个表都有主键
    - 先用SELECT进行测试
    - 使用强制实施引用完整性的数据库

### 创建表 - 更改表 -删除表

1. CREATE TABLE
    
    ```sql
    CREATE TABLE customers(
    	cust_id      int       NOT NULL AUTO_INCREMENT,
    	cust_name    char(50)  NOT NULL,
    	cust_address char(50)  NULL,
    	cust_city    char(50)  NULL,
      cust_state   char(10)  NULL,
    	cust_country char(50)  NULL DEFAULT 'USA',
    	cust_contact char(50)  NULL,
    	cust_email   char(255) NULL,
    	PRIMARY KEY (cust_id)
    ) ENGINE=InnoDB;
    ```
    
    1. `CREATE TABLE IF NOT EXISTS`
    2. `PRIMARY KEY` — **指定主键**
    3. `AUTO_INCREMENT` — **自动增量**
        - 每个表只允许一个AUTO_INCREMENT列，而且它必须被索引
    4. `last_insert_id()`
        - `SELECT last_insert_id()` — 返回最后一个AUTO_INCREMENT值
    5. `DEFAULT` **指定默认值**
        - 只支持常量
2. **引擎**：ENGINE=InnoDB 
    - **InnoDB**是一个可靠的事务处理引擎，它不支持全文本搜索
    - **MyISAM**是一个性能极高的引擎，它支持全文本搜索，但不支持事务处；默认的存储引擎
    - **MEMORY**在功能等同于MyISAM，但由于数据存储在内存（不是磁盘）
    中，速度很快（特别适合于临时表）
    1. 外键不能跨引擎
3. **ALTER TABLE** 更新表
****改动前进行备份**
    1. 添加列
    2. 删除列
        
        ```sql
        ALTER TABLE vendors
        ADD vend_phone CHAR(20);
        
        ALTER TABLE vendors
        DROP COLUMN vend_phone;
        ```
        
    3. 定义外键
4. **DROP TABLE** 删除表
5. **RENAME TABLE** 重命名表
    
    ```sql
    DROP TABLE customer
    
    RENAME TABLE customer TO customers
    ```
    

### 视图

1. 虚拟的表：只包含使用时动态检索数据的查询；查看存储在别处的数据的一种设施
2. **视图一般用于检索**
3. 优势
    - 重用SQL语句
    - 简化复杂的SQL操作
    - 使用表的组成部分
    - 保护数据
    - 更改数据格式和表示
4. 规则
    - 唯一命名
    - 具有足够的访问权限
    - 可以嵌套
    - 如果视图检索数据SELECT中含有ORDER BY，那么该视图中的ORDER BY将被覆盖
    - 视图不能索引
5. **视图基础操作**
    - `CREATE VIEW` — 创建视图
    - `SHOW CREATE VIEW XXXX` — 查看视图代码
    - `DROP VIEW XXXX` — 删除视图
    - `CREATE OR REPLACE VIEW` — 创建或更新替换视图
6. 常见应用
    - 隐藏复杂SQL — 联结
    - 重新格式化检索出的数据
    - 过滤不想要的数据
    - 使用视图，简化计算字段
7. **视图更新限制**
    - 分组（GROUP BY 和 HAVING）
    - 联结
    - 子查询
    - 并
    - 聚集函数
    - DISTINCT
    - 导出（计算）列

### 存储过程

1. 为以后的使用而保存的一条或多条MySQL语句的集合
2. **优势：简单、安全、高性能**
    - 简化复杂的操作
    - 防止错误，保证数据的**一致性**
    - 简化对变动的管理，**安全性**
    - 提高性能；使用存储过程比使用单独的SQL语句要快
3. **编写和执行 存储过程的安全访问分开**
4. **执行存储过程**
    - CALL xxx
5. **创建存储过程**
    - CREATE PROCEDURE
    
    ```sql
    # 临时更改命令行实用程序的语句分隔符
    DELIMITER //
    
    CREATE PROCEDURE productpricing()
    BEGIN
    		SELECT Avg(product_price) AS priceaverage
    		FROM products;
    END //
    
    DELIMITER ;
    ```
    
6. **删除存储过程**
`DROP PROCEDURE xxx IF EXISTS`
7. 所有MySQL变量都必须以@开始
8. `SHOW CREATE PROCEDURE xxx;` — 显示存储过程的代码

### 游标 cursor

1. 存储在MySQL服务器上的数据库查询
2. 主要用于交互式应用，其中用户需要滚动屏幕上的数据，并对数据进行浏览或做出更改
3. MySQL游标只能用于**存储过程（和函数）**
4. 步骤
    - 定义游标
        - `DECLARE xxx`
        
        ```sql
        CREATE PROCEDURE processorders()
        BEGIN
        		DECLARE ordernumbers CURSOR
        		FOR
        		SELECT order_num FROM orders;
        END;
        ```
        
    - 打开游标
        - `OPEN xxx`
    - 检索
    - 关闭
        - `CLOSE xxx`

### 触发器

1. 在特定事件发生时自动执行的语句
2. 只有表才支持触发器
3. 用触发器来保证数据的一致性（大小写、格式等）
4. 创建审计跟踪
5. 响应
    - DELETE
    - INSERT
    - UPDATE
6. 创建
    - 触发器名（**唯一性**）
    - 关联表
    - 响应活动 `DELETE | INSERT | UPDATE`
    - 执行时间（处理之前或之后）`AFTER / BEFORE`
7. CREATE TRIGGER
    
    ```sql
    CREATE TRIGGER newproduct AFTER INSERT ON Products
    FOR EACH ROW SELECT 'Product added'
    ```
    
8. `DROP TRIGGER xxx` — 删除触发器
9. 类型
    - INSERT 触发器
        - New的虚拟表
        - 将BEFORE用于数据验证和净化（目的是保证插入表中的数据确实是需要的数据）
        
        ```sql
        '''创建一个名为neworder的触发器，按照AFTER INSERTON orders执行。
        在插入一个新订单到orders表时，MySQL生成一个新订单号并保存到order_num中。
        触发器从NEW.order_num取得这个值并返回它'''
        CREATE TRIGGER neworder AFTER INSERT ON Orders
        FOR EACH ROW SELECT 'New.order_num'
        ```
        
    - DELETE 触发器
        - OLD的虚拟表：只读不能更新，访问被删除的行
        - 使用OLD保存将要被删除的行到一个存档表中
            
            ```sql
            CREATE TRIGGER deleteorder BEFORE DELETE ON Orders
            FOR EACH ROW 
            BEGIN
            		INSERT INTO archive_orders(order_num, order_date, cust_id)
            		VALUES(OLD.order_num, OLD.order_date, OLD.cust_id);
            END;
            ```
            
        - 使用BEGIN END块的好处是触发器能容纳多条SQL语句
    - UPDATE 触发器
        - 引用一个名为OLD的虚拟表访问以前（UPDATE语句前）的值
        引用一个名为NEW的虚拟表访问新更新的值；
        - 保证州名缩写总是大写
            
            ```sql
            CREATE TRIGGER updatevendor BEFORE UPDATE ON Vendors
            FOR EACH ROW SET NEW.vend_state = Upper(NEW.vend_state);
            ```
            

### 事务管理（transaction processing）

1. **InnoDB支持事务管理**；MyISAM不支持
2. **维护数据库的完整性**：管理必须成批执行的MySQL操作，以保证数据库不包含不完整的操作结果
3. 术语
    - 事务 transaction：一组SQL语句
    - 回退 rollback：撤销指定SQL语句的过程
    - 提交 commit：提交SQL语句
    - 保留点 savepoint：事务处理中设置的临时占位符(placeholder)
4. `START TRANSACTION`
5. 回退语句：`INSERT | UPDATE | DELETE`
6. **COMMIT 提交**
    
    ```sql
    # 从系统中完全删除订单20010;使用事务处理块来保证订单不被部分删除
    START TRANSACTION;
    DELETE FROM orderitems WHERE order_num = 20010;
    DELETE FROM orders WHERE order_num = 20010;
    COMMIT;
    ```
    
7. 创建占位符 `SAVEPOINT delete1;`
8. 回退到保留点 `ROLLBACK TO delete1;`
9. 更改默认的提交行为：`SET autocommit=0;` — 不自动提交更改

### 字符集和校对顺序

1. **字符集：**字母和符号的集合
2. **编码：**某个字符集成员的内部表示
3. **校对：**规定字符如何比较的指令
4. 查看所支持的字符集完整列表
`SHOW CHARACTER SET;` — 显示所有可用的字符集以及每个字符集的描述和默认校对。
5. 查看所支持校对的完整列表：
`SHOW COLLATION;` — 显示所有可用的校对，以及它们适用的字符集
6. 确定所用的字符集和校对：
`SHOW VARIABLES LIKE 'character%'
SHOW VARIABLES LIKE 'collation%'`

### 安全管理

1. 访问控制
2. 创建用户账号
`CREATE USER ute IDENTIFIED BY ‘passwoard’;`
3. 重命名：`RENAME USER ute TO ilse;`
4. 删除用户：`DROP USER ilse;`
5. 查看访问权限：`SHOW GRANTS FOR ilse;`
6. 授予权限：
`GRANT SELECT ON products.* TO ilse;` — 运行用户ilse在products数据库的所有表上使用SELECT
7. 撤销权限：
`REVOKE SELECT ON products.* FROM ilse;`
8. 更改口令：
`SET PASSWORD FOR ilse = Password(’xxxxxx’);`
9. 不指定用户名，更新当前登录用户口令
`SET PASSWORD = Password(’xxxxxx’);`

```sql
-- 显示所有用户
USE mysql;
SELECT user, host FROM mysql.user;

-- 创建新用户
CREATE USER ute IDENTIFIED BY '1234';

-- 重命名用户
RENAME USER ute TO ilse;

-- 重置密码
SET PASSWORD FOR 'ilse'@'%' = '88888888';

-- 显示用户权限 
SHOW GRANTS FOR ilse;

-- 赋予用户特定数据库权限
GRANT SELECT, INSERT, UPDATE, DELETE, EXECUTE
ON my_project.* 
TO ute;

-- 撤销权限
REVOKE DELETE
ON my_project.* 
FROM ute;
```

| Privilege | Grant Table Column | Context |
| --- | --- | --- |
| ALL [PRIVILEGES] | 所有权限的同义词 | 服务器管理 |
| ALTER | Alter_priv | 表格 |
| ALTER ROUTINE | Alter_routine_priv | 存储过程 |
| CREATE | Create_priv | 数据库、表格或索引 |
| CREATE ROUTINE | Create_routine_priv | 存储过程 |
| CREATE TABLESPACE | Create_tablespace_priv | 服务器管理 |
| CREATE TEMPORARY TABLES | Create_tmp_table_priv | 表格 |
| CREATE USER | Create_user_priv | 服务器管理 |
| CREATE VIEW | Create_view_priv | 视图 |
| DELETE | Delete_priv | 表格 |
| DROP | Drop_priv | 数据库、表格或视图 |
| EVENT | Event_priv | 数据库 |
| EXECUTE | Execute_priv | 存储过程 |
| FILE | File_priv | 服务器主机上的文件访问 |
| GRANT OPTION | Grant_priv | 数据库、表格或存储过程 |
| INDEX | Index_priv | 表格 |
| INSERT | Insert_priv | 表格或列 |
| LOCK TABLES | Lock_tables_priv | 数据库 |
| PROCESS | Process_priv | 服务器管理 |
| PROXY | 查看 proxies_priv 表 | 服务器管理 |
| REFERENCES | References_priv | 数据库或表格 |
| RELOAD | Reload_priv | 服务器管理 |
| REPLICATION CLIENT | Repl_client_priv | 服务器管理 |
| REPLICATION SLAVE | Repl_slave_priv | 服务器管理 |
| SELECT | Select_priv | 表格或列 |
| SHOW DATABASES | Show_db_priv | 服务器管理 |
| SHOW VIEW | Show_view_priv | 视图 |
| SHUTDOWN | Shutdown_priv | 服务器管理 |
| SUPER | Super_priv | 服务器管理 |
| TRIGGER | Trigger_priv | 表格 |
| UPDATE | Update_priv | 表格或列 |
| USAGE | “没有权限”的同义词 | 服务器管理 |

### 数据库维护

1. 备份
    1. 使用命令行实用程序mysqldump转储所有数据库内容到某个外部文件
    2. 命令行实用程序mysqlhotcopy从一个数据库复制所有数据
    3. 使用MySQL的BACKUP TABLE或SELECT INTO OUTFILE转储所有数据到某个外部文件
2. 维护
    1. 检查表键是否正确：`ANALYZE TABLE xxx;`
    2. 检查问题：`CHECK TABLE xxx;`
    3. `CHANGED`检查自最后一次检查以来改动过的表
    4. `EXTENDED`执行最彻底的检查
    5. `FAST`只检查未正常关闭的表
    6. `MEDIUM`检查所有被删除的链接并进行键检验
    7. `QUICK`只进行快速扫描
    8. 如果从一个表中删除大量数据，应该使用`OPTIMIZE TABLE`来收回空间，优化表的性能
3. 查看日志文件
    1. **错误日志**：包含启动和关闭问题以及任意关键错误的细节
    通常名为hostname.err，位于data目录中
    2. **查询日志**：记录所有MySQL活动
    通常名为hostname.log，位于data目录中
    3. **二进制日志**：记录更新过数据（或者可能更新过数据）的所有语句
    通常名为hostname-bin，位于data目录内
    4. 缓慢查询日志：记录执行缓慢的任何查询
    通常名为hostname-slow.log ， 位于data 目录中
4. 在使用日志时，可用`FLUSH LOGS`语句来刷新和重新开始所有日志文件

---

### 数据类型

1. **目的**：
    - **限制**可存储在列中的数据
    - 在内部更**有效**地存储数据
    - 允许变换排序**顺序**
2. **字符串类型**
    
    
    | 类型 | 大小 | 用途 |
    | --- | --- | --- |
    | CHAR | 0-255 bytes | 定长字符串；
    CHAR(30) 可以存储 30 个字符 |
    | VARCHAR | 0-65535 bytes | 变长字符串 |
    | TINYBLOB | 0-255 bytes | 不超过 255 个字符的二进制字符串 |
    | TINYTEXT | 0-255 bytes | 短文本字符串 |
    | BLOB | 0-65 535 bytes | 二进制形式的长文本数据 |
    | TEXT | 0-65 535 bytes | 长文本数据 |
    | MEDIUMBLOB | 0-16 777 215 bytes | 二进制形式的中等长度文本数据 |
    | MEDIUMTEXT | 0-16 777 215 bytes | 中等长度文本数据 |
    | LONGBLOB | 0-4 294 967 295 bytes | 二进制形式的极大文本数据 |
    | LONGTEXT | 0-4 294 967 295 bytes | 极大文本数据 |
3. 数值类型
    
    
    | 类型 | 大小 | 范围（有符号） | 范围（无符号） | 用途 |
    | --- | --- | --- | --- | --- |
    | TINYINT | 1 Bytes | (-128，127) | (0，255) | 小整数值 |
    | SMALLINT | 2 Bytes | (-32 768，32 767) | (0，65 535) | 大整数值 |
    | MEDIUMINT | 3 Bytes | (-8 388 608，8 388 607) | (0，16 777 215) | 大整数值 |
    | INT或INTEGER | 4 Bytes | (-2 147 483 648，2 147 483 647) | (0，4 294 967 295) | 大整数值 |
    | BIGINT | 8 Bytes | (-9,223,372,036,854,775,808，9 223 372 036 854 775 807) | (0，18 446 744 073 709 551 615) | 极大整数值 |
    | FLOAT | 4 Bytes | (-3.402 823 466 E+38，-1.175 494 351 E-38)，0，(1.175 494 351 E-38，3.402 823 466 351 E+38) | 0，(1.175 494 351 E-38，3.402 823 466 E+38) | 单精度浮点数值 |
    | DOUBLE | 8 Bytes | (-1.797 693 134 862 315 7 E+308，-2.225 073 858 507 201 4 E-308)，0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 双精度浮点数值 |
    | DECIMAL | 对DECIMAL(M,D) ，如果M>D，为M+2否则为D+2 | 依赖于M和D的值 | 依赖于M和D的值 | 小数值 |
4. 货币数值类型
`一般使用DECIMAL(8, 2)`
5. 日期和时间数据类型
    
    
    | 类型 | 大小( bytes) | 范围 | 格式 | 用途 |
    | --- | --- | --- | --- | --- |
    | DATE | 3 | 1000-01-01/9999-12-31 | YYYY-MM-DD | 日期值 |
    | TIME | 3 | '-838:59:59'/'838:59:59' | HH:MM:SS | 时间值或持续时间 |
    | YEAR | 1 | 1901/2155 | YYYY | 年份值 |
    | DATETIME | 8 | '1000-01-01 00:00:00' 到 '9999-12-31 23:59:59' | YYYY-MM-DD hh:mm:ss | 混合日期和时间值 |
    | TIMESTAMP | 4 | '1970-01-01 00:00:01' UTC 到 '2038-01-19 03:14:07' UTC
    结束时间是第 2147483647 秒，北京时间 2038-1-19 11:14:07，格林尼治时间 2038年1月19日 凌晨 03:14:07 | YYYY-MM-DD hh:mm:ss | 混合日期和时间值，时间戳 |
6. 二进制数据类型
    - `BLOB`            Blob最大长度为64 KB
    - `MEDIUMBLOB`  Blob最大长度为16 MB
    - `LONGBLOB`     Blob最大长度为4 GB
    - `TINYBLOB`     Blob最大长度为255字节
