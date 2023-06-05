# Python 合并多个csv为excel

```python
# 根据个人配置，可能需要下载XlsxWriter库
!pip install XlsxWriter

import pandas as pd
import glob

# 获取所有CSV文件的文件名（将所有需要合并的csv文件放在一个文件夹内）
csv_files = glob.glob('hotel/*.csv')

# 创建一个空的Excel Writer对象
excel_writer = pd.ExcelWriter('merged_hotel.xlsx', engine='xlsxwriter')

# 遍历每个 CSV 文件并将其读取为 DataFrame，然后写入 Excel 表格
for csv_file in csv_files:
    # 从 CSV 文件读取数据
    df = pd.read_csv(csv_file)
    
    # 提取有效的 sheet 名称
    sheet_name = csv_file.split('\\')[-1][:-4]
    
    # 将 DataFrame 写入 Excel 表格的指定 sheet
    df.to_excel(excel_writer, sheet_name=sheet_name, index=False)

# 保存并关闭 Excel Writer 对象
excel_writer.close()
```