## Day3 今日导学

### 前面的话

同学们，今天是我们开课的第3天。昨天我们已经开始接触Python代码的/数字和字符串/部分，也了解了项目的相关信息和项目工作区的使用方式。今天我们的一切将会围绕项目的撰写展开。请同学们务必在今天晚上的优达日活动前完成。我们将会用1个小时的时间讲解项目的内容。

### 今日目标

今天的目标分为3部分，首先是熟悉一下我们提交项目文件的工作区、再有就是对项目的5个部分进行一下了解、其中1-3会进行讲解，第4部分有些长咱们视频时再完成。

1. （看懂即可，课程3部分 - 配置jupyter notebook中的内容）配置jupyter notebook
   1. notebook界面（项目工作区是怎么用）
   2. 代码单元格（就是输入代码的框是怎么回事）
   3. Markdonw单元格（就是大家写字的框是怎么回事）

2. （之后咱们切换到-项目实战部分）项目工作区
   1. 这个区域就是上面那个任务使用的jupyter notebook了，所有操作都在此处完成，所有功能在上面菜单都可以选。
   2. 需要编辑的话双击到相应位置就可以了。**本项目空间不能重置！请只改动需要的地方！**
   3. 项目中的说明非常详细，请认真从头读到尾，跳过代码框，只读文字，并着重理解5个问题。

3. 填写项目文件（问题1：提出问题部分）：这部分可以发到群里来大家一起看看，因为涉及到后面代码的编写。

4. 填写项目文件（问题2:数据评估部分）：这部分将会出现较多的代码，但大部分都是现成的，不用完成，简要说明一下：

   - 数据文件：在这一部分我们先会看到做项目的5个数据文件。可以从名字看出来就是中国5个城市从2010年到2015年的数据。

     ```
      BeijingPM20100101_20151231.csv,
     2. ChengduPM20100101_20151231.csv,
     3. GuangzhouPM20100101_20151231.csv,
     4. ShanghaiPM20100101_20151231.csv,
     5. ShenyangPM20100101_20151231.csv
     ```

     文件的格式是csv，就是用逗号分隔存储数据的一种格式。里面每行记录了一次测量的数据（也可用excel打开，就是比较便于看的表格形式了）：

     ```
     No,year,month,day,hour,season,PM_Dongsi,PM_Dongsihuan,PM_Nongzhanguan,PM_US Post,DEWP,HUMI,PRES,TEMP,cbwd,Iws,precipitation,Iprec
     1,2010,1,1,0,4,NA,NA,NA,NA,-21,43,1021,-11,NW,1.79,0,0
     2,2010,1,1,1,4,NA,NA,NA,NA,-21,47,1020,-12,NW,4.92,0,0
     3,2010,1,1,2,4,NA,NA,NA,NA,-21,43,1019,-11,NW,6.71,0,0
     ```

   - 包倒入：那么要想使用python语言处理这些数据，我们需要将csv文件读取一下。在这之前，需要把用到的库导入进来，一共用到以下几个，我用#号做了注释，了解一下就好

     ```python
     import csv #读取csv文件的库
     import numpy as np #用于矩阵计算的库
     import pandas as pd #用于数据统计的库
     import matplotlib.pyplot as plt #用于图形化展示的库
     import seaborn #用于优化图形显示的库
     %matplotlib inline #用于让jupyter能显示图形的参数
     ```

   - 数据读取：最后我们要把刚才的csv文件导入成Python可以处理的数据

     ```python
     Shanghai_data = pd.read_csv('ShanghaiPM20100101_20151231.csv')
     #上面的代码就是设定了一个数据Shanghai_data，里面的数据都是从后面那个csv读取来的。导入的方法就是pd.read_csv()。pd是我们刚到入的库，read_csv()的意思就是把括弧里面的csv读进来。
     Shanghai_data.head()
     #在我们做好的数据后面加了.head()就会把数据的前5行显示出来，好让我们检查是不是成功了
     ```

   - （选看，不看不影响项目！）数据清理：上面的.head()输出后，我们会发现season是1到4编号，不是春夏秋冬啊，太没有感性的美了，可以使用map方法进行替换。

     ```python
      Shanghai_data['season'] = Shanghai_data['season'].map({1:'Spring', 2:'Summer', 3:'Autumn', 4: 'Winter'})
      Shanghai_data.head()
     ```

   - 去掉没有数据的值：其实数据的最大问题是有很多标记为NaN的空值，这样会对分析结果产生很大影响，那么我们再通过.info()方法查下到底缺失了多少：

     ```python
     Shanghai_data.info()
     #输出是：
     Data columns (total 17 columns):
     No               52584 non-null int64
     year             52584 non-null int64
     month            52584 non-null int64
     day              52584 non-null int64
     hour             52584 non-null int64
     season           52584 non-null int64
     PM_Jingan        24700 non-null float64
     PM_US Post       34039 non-null float64
     PM_Xuhui         25189 non-null float64
     DEWP             52571 non-null float64
     HUMI             52571 non-null float64
     PRES             52556 non-null float64
     TEMP             52571 non-null float64
     cbwd             52572 non-null object
     Iws              52572 non-null float64
     precipitation    48575 non-null float64
     Iprec            48575 non-null float64
     ```

     这里要第二列彩色的阿拉伯数字，就是有数值的记录。表示每个值的多少都不一样啊，这个怎么办！我们可以用一行代码把NaN这种没意义的值干掉：

     ```python
     Shanghai_data['PM_Jingan'].dropna()
     ```

   - （选看）数据生成：那么到了最后我们干脆把5个数据文件都按上面步骤处理一遍，并且将数据整合为一个文件中，这样下一步我们怎么分析就是这个数据，就方便了。我把用到的语句放到了下面，这几块代码不用看！理解即可！

    ```python
    files = []
    out_columns = []
    df_all_cities = pd.DataFrame()
    #df_all_cities 就是我们最后分析使用的数据
    for inx, val in enumerate(files):
    #用一个循环把5个城市的数据做标识（就是增加一列，来自beijing的写beijing，来自上海的写上海，便于后续筛选）
    ```

5. （选看）问题3:筛选数据部分。这部分看着很吓人，两段超长的函数，其实这两段里面一个字都不用写。大家能看明白这两个函数是怎么使用的就可以了：

   第1个是数据筛选函数 ：

    ```python
   def filter_data(data, condition):
    ```
   第2个是数据处理函数：  

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

  

  ​    import pandas
      import csv

- 数据读取
      data = pd.read_csv(x.csv)
      data.head()
      data.info()

- 数据清理
      Shanghai_data['season'] = Shanghai_data['season'].map({1:'Spring', 2:'Summer', 3:'Autumn', 4: 'Winter'})
      Shanghai_data.head()

- 数据生成
      files = []
      out_columns = []
      df_all_cities = pd.DataFrame()
      for inx, val in enumerate(files):

数据探索阶段 ** 4m

- 数据筛选函数 
      def filter_data(data, condition):
- 数据处理函数  
      def usage_stats(data, filters = [], verbose = True):

得出结论阶段 * 2m

- 函数调用
      df_test = usage_stats(df_all_cities, ["city == 'Shanghai'", "year >= 2012"])
      df1 = usage_stats(df_all_cities, ["city == 'Chengdu'", "year <= 2015"])
- 图形展示
      seaborn.boxplot(data['PM_US Post'], showfliers=False)
      plt.title('Boxplot of PM 2.5 of filtered data')
      plt.xlabel('PM_US Post (ug/m^3)')
      def univariate_plot(data, key = '', color = 'blue'):
      univariate_plot(df_test, 'month', 'grey')
- 结论
  1. 从本可视化中我们可以看出在较温暖的月份（6-10月）空气中的PM 2.5含量较低，而较寒冷的月份，比如（11-1月）空气中的PM 2.5含量较高。
，
   4. **项目工作区**（重点！你编写项目的地方）
      1. 使用的是Jupyter Notebook
      2. 记得编写一段后在左上角点存盘图标
      3. 完成后点击‘File’ - ‘Download as’下载你要的文件（见上节要求）之后在最后那节提交项目
      4. 此部分点进去编辑就好了，想了解深入点（非项目要求，可以看课程第三部分‘（可选）Anaconda 和 Jupyter notebook’ 里面的讲解（**非项目完成相关**）
   5. （可选）本地环境搭建（**等项目做完了可以看，现在不用！**）
   6. 重点回顾（用到的代码重点回顾，看下就行）
   7. 项目：中国五个城市PM2.5分析
      1. 在此处右下角提交项目
      2. 提交项目时把文件打包成zip文件
      3. 文件不可以有中文字符
      4. 提交后会收到确认邮件
      5. **一般几个小时会收到反馈，可能需要修改，会有邮件通知，记得及时检查邮件！**
4. （！选学，项目不要求！）数据结构和循环
5. （！选学，项目不要求！）函数和标准库（了解下相关内容就可以了）

### 助教叨叨

第2天了，我们今天要开始看项目文件和Python代码了，没接触过的同学肯定会有一点点的头疼，放心，有我们配置你。要想今天达到目标，这几点可以帮到：

      1. 按照导学内容学习，先完成必要的，学有余力再看选学。
      2. 如果没看明白视频，再看一遍，都不是特别长。之后梳理一下自己的问题，**发到群里讨论！**为什么要群里，因为可以大家一起看看，可能有同学也遇到了相关问题，根据经验，大家都会特别热心的。另外这样回复速度也会快一些。当然如果习惯单独问的话，就私戳我就好了。
      3. 项目是在项目工作区完成，大家不用自己安装任何东西，7天时间特别紧张，本地环境在项目完成后再研究配置，在正式课里也会有老师解答的，一定要项目优先！！！
      4. 今天就看到Python代码了，其实没那么什么，马上你就会很熟悉了，最后鸡汤一句："Now I can code, and they can not. That's damn cool!"
