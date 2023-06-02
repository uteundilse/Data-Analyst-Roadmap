# Data-Analyst-Roadmap 📊
**分享我的数据分析纯自学完整路线**

# 学习路径 ⚙️

### 第一阶段： 初识数据
  - Excel：[王佩丰Excel基础教程24讲](https://www.bilibili.com/video/BV1yJ411s7wS/?spm_id_from=333.337.search-card.all.click&vd_source=048f2d3fb232702db4d8b69ac02f4feb)
  - 统计学

### 第二阶段：数据库SQL
  - MySQL：[mosh-SQL入门到中级](https://www.bilibili.com/video/BV1UE41147KC/?spm_id_from=333.999.0.0&vd_source=048f2d3fb232702db4d8b69ac02f4feb)
  - [《MySQL必知必会》](https://github.com/uteundilse/Data-Analyst-Roadmap/blob/main/BOOKS/SQL/MySQL%E5%BF%85%E7%9F%A5%E5%BF%85%E4%BC%9A.pdf)
  - [《SQL进阶教程》](https://github.com/uteundilse/Data-Analyst-Roadmap/blob/main/BOOKS/SQL/SQL%E8%BF%9B%E9%98%B6%E6%95%99%E7%A8%8B%20(MICK)%20.pdf)

### 第三阶段：Python
  - [《Python编程：从入门到实践》](https://github.com/uteundilse/Data-Analyst-Roadmap/blob/main/BOOKS/Python/Python%E7%BC%96%E7%A8%8B%EF%BC%9A%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%AE%9E%E8%B7%B5.pdf)
  - [《Python数据科学手册》](https://github.com/uteundilse/Data-Analyst-Roadmap/blob/main/BOOKS/Python/Python%E6%95%B0%E6%8D%AE%E7%A7%91%E5%AD%A6%E6%89%8B%E5%86%8C.pdf)
  - 《利用Python进行数据分析》
  - [《数据科学入门》](https://github.com/uteundilse/Data-Analyst-Roadmap/blob/main/BOOKS/Python/%E6%95%B0%E6%8D%AE%E7%A7%91%E5%AD%A6%E5%85%A5%E9%97%A8.pdf)

### 第四阶段：可视化+数据分析方法
  - Power BI：
    - [Power BI基础入门](https://www.youtube.com/live/77jIzgvCIYY?feature=share)
    - [Power BI数据模型](https://www.youtube.com/live/MrLnibFTtbA?feature=share)
    - [Power BI DAX](https://www.youtube.com/live/QJw4HkagVWc?feature=share)
  - [Tableau public官网](https://public.tableau.com/app/discover)
  - 《数据分析之道：用数据思维指导业务实战》
  - 《数据分析思维：分析方法和业务知识》

### 第五阶段：项目+数据思维
  - Kaggle入门项目
    - **[Titanic-prediction](https://github.com/uteundilse/Data-Analyst-Practice/blob/main/Titanic_prediction.ipynb)**: 练习  
      二分类预测问题, 为Titanic891名乘客预测是否在泰坦尼克号沉船事故中活下来. 通过分析乘客的人口统计学特征,对数据进行清洗和填补缺失值,例如使用KNN回归算法模型对年龄列进行填充; 并且构建了多个组合特征,并对类别型特征进行了标签编码。构建线性回归模型,最终达到92.3%的预测精度.
      
    - **[California Housing Prices](https://github.com/uteundilse/Data-Analyst-Practice/blob/main/California%20Housing%20Prices.ipynb)**: 练习  
    通过对原始数据的探索, 数据清洗与预准备; 然后增加模型的特征列. 建立随机森林模型, 最终达到81.8%的准确度.
    
    - **[House Prices](https://github.com/uteundilse/Data-Analyst-Practice/blob/main/house_prices.ipynb)**: 练习   
    通过对原始数据的探索, 数据清洗与预准备,并增加模型的特征列. 对数值数据进行简单相关性分析，用以衡量如何填充空值;例如对于缺失过多的列使用最近邻居的回归算法. 进行特征转换,数据缩放等,选择多个模型进行训练,并最终取得名次714,名次15%.
    
  - 数据分析
    - **[Glassdoor平台数据分析招聘岗位分析](https://github.com/uteundilse/Data-Analyst-Practice/blob/main/Data%20Analyst%20Jobs.ipynb) Python**
    
      - 项目背景：利用Glassdoor平台的数据分析师招聘数据，对岗位进行深入分析，以了解行业趋势、需求和关键技能等，作为数据分析求职者得到更有针对性的建议
    
      - 数据预处理：对数据进行清洗和处理，去除重复项、处理缺失值和异常值，确保数据的准确性和一致性
    
      - 相关性分析：利用python采取过滤，相关性分析和特征重要性排序等手段，提炼多个关键指标，选择重要特征进行分析，如薪资水平与经验、学历之间的关系，通过相关性分析揭示影响薪资的因素
    
      - 结果与建议：通过对Glassdoor平台的数据分析招聘岗位进行深入分析，揭示了数据分析岗位在金融和科技行业的快速增长趋势。关键技能包括SQL、Excel、Python和数据可视化工具等
    
    - **[星巴克促销活动分析](https://github.com/uteundilse/Data-Analyst-Practice/blob/main/Starbucks.ipynb) Python**

      - 项目背景:分析星巴克活动期间不同营销活动对客户交易数据的影响,以确定不同客户群体的定位,提高客户粘性和品牌认知,从而增加总体收入。

      - 数据预处理:对数据集进行清洗,包括处理缺失值和异常值。缺失值采用平均值、众数填补;异常值采取上下四分位数法，并标准化数据,使变量可比。

      - 数据可视化:基于数据特征，提出问题并进行单变量和双变量统计分析。绘制散点图矩阵分析不同活动类型的关系；通过热力图探索变量间的相关性；通过核密度估计比较分布特征；绘   制箱线图比较五组客户消费金额。

      - 数据探索与建模:利用相关系数矩阵和回归分析发现会员收入、活动推送途径及活动类型等影响客户消费。K-means聚类将客户分五组,分析不同特征和响应。

      - 项目结果:发现影响客户消费和品牌忠诚的关键因素,为制定针对性营销计划提供决策支持。
      - 
  - 报表制作


# 数据分析项目 📊

# 时间安排



#
