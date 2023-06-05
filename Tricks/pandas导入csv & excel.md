# Pandas

## read_csv

1. 基础导入 — `df = pd.read_csv('test.csv')` 
2. 指定编码 — `df = pd.read_csv('test.csv',` `encoding = "ISO-8859-1")`
    - 编码默认为UTF-8
3. 指定表头（列名）
    - 默认第一行为列名
    - 取消列名 — `df = pd.read_csv('test.csv', header=None)`
    - 指定第几行为列名 — `df = pd.read_csv('test.csv',  header=2)`
4. 指定索引
    - 默认添加一列索引，从0开始
    - 指定列为索引 — `df = pd.read_csv('test.csv', index_col='ID')`
5. 读取子集（部分读取）
    - 列限制 — 只读取特定列
    `df = pd.read_csv('test.csv',  usecols=['ID', 'name', 'gender'])`
    - 行限制 —  数据集过大，只读取前100行
    `df = pd.read_csv('test.csv', nrows=100)`
6. 处理缺失值
将空字符串''视为NaN值 — `df = pd.read_csv('test.csv', na_values=[''])`
7. 是否读取空行
    - 默认跳过空行
    - 不跳过 — `df = pd.read_csv('test.csv', skip_blank_lines=False)`
8. 不读取特定行
    - 不读取的行号作为列表 — `df = pd.read_csv('test.csv',  skiprows = [1,3,7])`

## read_excel

1. 安装：`pip install openpyxl`
2. 读取单张表
    - Excel 工作表中第一张工作表：`df = pd.read_excel('test.xlsx', sheet_name=0)`
    - 指定工作表：`df = pd.read_excel('test.xlsx', sheet_name=2)`
3. 读取多张表
    
    ```python
    # 获取多张表名
    xls_file = pd.ExcelFile('test.xlsx')
    xls_file.sheet_names
    '''
    ['TEST0', 'TEST1', 'TEST2']
    '''
    
    # 分别读取特定表
    df1 = xls_file.parse('TEST0')
    df2 = xls_file.parse('TEST1')
    ```
    
4. 选择列标签
    - 默认：Excel 文件中第一个非空白行的值
    - 不设置表头：`df = pd.read_excel('test.xlsx', sheet_name=1, header=None)`
    - 指定：`df = pd.read_excel('test.xlsx', sheet_name=1, header=3)`
5. 读取子集
    - 行子集
        - 跳过前6行：`df = pd.read_excel('test.xlsx', sheet_name=1,` `skiprows=6)`
        - 跳过后6行：`df = pd.read_excel('test.xlsx', sheet_name=1,` `ski_footer=6)`
    - 列子集
        - 读取前3列：
            
            ```python
            df = pd.read_excel('test.xlsx', sheet_name=0)  
            df = df[['col1', 'col2', 'col3']]
            ```

