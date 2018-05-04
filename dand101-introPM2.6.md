## 10mins DAND Intro
作为一个大龄、有娃的IT理工男（非开发），用了8个月时间完成了数据分析初级，高级，还参与了新Python课程的测试。如果用一句话对这段经历做总结，我想说的就是：充实。长话短说，自我突破是很痛苦的，Uda的这门课很好的特色小结如下：

1. 第一，能够用得到。要知道，学得再好，用不起来也白搭。数据分析的场景越来越多，数据集也非常多，还有各种竞赛，如果想用起来，大环境已经非常成熟了。而且在工作也确实有很多机会使用，比如之前自己用excel公式做了半自动化的报告就觉得很好了，学了课程才会了python这种更加风骚的操作。
2. 第二，学习曲线科学。不要会错意，对于初入门的小白来讲，课程还是挺难的。来听听想毕业都要会什么：Python语言、SQL语言、统计学、数据分析思维、A/B测试、Anaconda环境、Sublime IDE……。害不害怕？好了，不哭了……要知道Uda的学费没白交。Uda收了钱以后，还是做了很多增加反馈的节点的：
	1. 课程是项目制。4个项目就要交4个报告，还有非常专业（…严格的）评审老师。
	2. 微信通关群。在学习的过程中，每个项目有通关群，群里有助教老师耐心的解决问题。
	3. 论坛和1对1辅导。如果涉及代码比较复杂还可以发论坛（好多问题论坛里都有的……没忍住剧透了）。最后还有大招每周1次1对1电话辅导。
4. 第三，自我的突破。之前在知乎周刊看到一句话：。觉得会写代码又拽又神秘。也陆续买书瞎看，进展可以说…顶Uda一周的学习内容吧。在这次学习期间，不但一下入门了Python，R，JavaScript（用于数据分析的差不多了，目标明确，我是要用代码来分析数据的！）还学会了怎么应对统计分析、数据可视化、探索性数据分析、机器学习等等实际工作的实现。接下来就是自己积累了。

总结来说，除了项目导向的学习内容外，Uda也在非常努力的提供反馈，平滑了学习曲线。现在就剩自己认真的走下去，各位加油。ps：Uda的每周10小时的投入时间还是比较准的，不要想着偷懒，对于我这种大龄苦手来讲还要更多时间。‘充实’是说辛苦，但是不苦。

## 10mins Code Introduction
### 1/ Data Analyst？1m
要想学习数据分析，首先我们得明白数据分析师先明是干啥的？

>**Uda的定义：**
数据分析师就是用数据回答问题的人。（当老板提出奇怪的建议时，你又多了一支撑材料，可以让他闭嘴了……）
anaylist: someone who use data to answer questions

### 2/ Data Analysis Process 1m
数据分析过程：Data Analysis Process
1. **数据提提问阶段** Question Phase
	1. e.g. Characteristics of Students who pass projects
	2. e.g. How to stock store
4. **数据规整阶段** Wrangling Phase
	1. data acquisition
    2. data cleaning
5. **数据探索阶段** Explore Phase
	1. Build intuition
	2. 2. Find patterns
6. **得出结论阶段** Drawing Conclusions Phase (make predictions)
	1. Predict: Which movies users will like
	2. Conclude: Users are less likely to click cartain articles
	3. usually requires statistics or machine learning
7. **沟通交流阶段** Communication Phase
	1. Blog post, paper, email, power point, conversation
	2. Data visualization is almost always useful

### 3/ Interpreting 
#### 数据规整 * 2m
- [x] 数据下载
  https://www.kaggle.com/uciml/pm25-data-for-five-chinese-cities/data
- [x] 数据概览
  https://www.kaggle.com/uciml/pm25-data-for-five-chinese-cities
- [x] 包倒入
  ```python
  import pandas
  import csv
  ```
- [x] 数据读取
  ```python
  data = pd.read_csv(x.csv)
  data.head()
  data.info()
  ```
- [x] 数据清理
  ```python
  Shanghai_data['season'] = Shanghai_data['season'].map({1:'Spring', 2:'Summer', 3:'Autumn', 4: 'Winter'})
  Shanghai_data.head()
  ```
- [x] 数据生成
  ```python
  files = []
  out_columns = []
  df_all_cities = pd.DataFrame()
  for inx, val in enumerate(files):
  ```
####  数据探索阶段 ** 4m
- [x] 数据筛选函数 

  ```python
  def filter_data(data, condition):
  ```

- [x] 数据处理函数  

  ```python
  def usage_stats(data, filters = [], verbose = True):
  ```

#### 得出结论阶段 * 2m
- [x] 函数调用
  ```python
  df_test = usage_stats(df_all_cities, ["city == 'Shanghai'", "year >= 2012"])
  df1 = usage_stats(df_all_cities, ["city == 'Chengdu'", "year <= 2015"])
  ```
- [x] 图形展示
  ```python
  seaborn.boxplot(data['PM_US Post'], showfliers=False)
  plt.title('Boxplot of PM 2.5 of filtered data')
  plt.xlabel('PM_US Post (ug/m^3)')
  ```
  ```
  def univariate_plot(data, key = '', color = 'blue'):
  univariate_plot(df_test, 'month', 'grey')
  ```
- [x] 结论
  1. 从本可视化中我们可以看出在较温暖的月份（6-10月）空气中的PM 2.5含量较低，而较寒冷的月份，比如（11-1月）空气中的PM 2.5含量较高。

