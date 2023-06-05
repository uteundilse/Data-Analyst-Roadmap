# MySQL 导入CSV

## 直接导入 LOAD DATA INFILE

```sql
-- 显示local_infile这个全局变量的值,用于确定是否允许导入本地数据文件
SHOW global variables like 'local_infile';

-- 将local_infile变量设置为1,允许导入本地数据文件
SET global local_infile=1;

SHOW variables like '%secure%';

USE my_project;

CREATE TABLE IF NOT EXISTS starbucks(
uniqueid         INT           NOT NULL PRIMARY KEY,
gender           VARCHAR(255),
age              INT,
id               VARCHAR(255),
became_member_on TEXT,
income           INT
);

LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/profile.csv' INTO TABLE starbucks
FIELDS TERMINATED BY ','
LINES TERMINATED BY '\n'
IGNORE 1 LINES
(uniqueid, gender, age, id, became_member_on, @income)
SET income = NULLIF(@income, ''); 
-- 将income字段设置为@income,除非@income为空,在这种情况下将income设置为NULL。
```

## 利用pandas导入

1. 利用python处理csv文件
    
    ![Untitled](MySQL%20%E5%AF%BC%E5%85%A5CSV%2083398c7a1d944749b9808145d2edbf2f/Untitled.png)
    
    ![Untitled](MySQL%20%E5%AF%BC%E5%85%A5CSV%2083398c7a1d944749b9808145d2edbf2f/Untitled%201.png)
    
    ![Untitled](MySQL%20%E5%AF%BC%E5%85%A5CSV%2083398c7a1d944749b9808145d2edbf2f/Untitled%202.png)
    
    ![Untitled](MySQL%20%E5%AF%BC%E5%85%A5CSV%2083398c7a1d944749b9808145d2edbf2f/Untitled%203.png)
    
    ![Untitled](MySQL%20%E5%AF%BC%E5%85%A5CSV%2083398c7a1d944749b9808145d2edbf2f/Untitled%204.png)
    
    ![Untitled](MySQL%20%E5%AF%BC%E5%85%A5CSV%2083398c7a1d944749b9808145d2edbf2f/Untitled%205.png)
    
2. MySQL创建表格并插入数据
    
    ![Untitled](MySQL%20%E5%AF%BC%E5%85%A5CSV%2083398c7a1d944749b9808145d2edbf2f/Untitled%206.png)
    
3. 直接将生成的txt文件一键复制粘贴
    
    ![Untitled](MySQL%20%E5%AF%BC%E5%85%A5CSV%2083398c7a1d944749b9808145d2edbf2f/Untitled%207.png)
    
    ![Untitled](MySQL%20%E5%AF%BC%E5%85%A5CSV%2083398c7a1d944749b9808145d2edbf2f/Untitled%208.png)
    
4. 导入成功
    
    ![Untitled](MySQL%20%E5%AF%BC%E5%85%A5CSV%2083398c7a1d944749b9808145d2edbf2f/Untitled%209.png)