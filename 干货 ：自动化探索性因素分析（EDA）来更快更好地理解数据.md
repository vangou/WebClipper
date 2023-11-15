# 干货 ：自动化探索性因素分析（EDA）来更快更好地理解数据
本文****约3900字****，建议阅读****10分钟****

本文将会用常用的iris数据集来学习如何在R和Python中实现探索性因素分析的过程。

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBBQCOUl65HjQqxkRuszVecdaMKLtqlcibspoQWicykJQtzFLrmE9cIPCQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
图片来自Charlotte Karlsen, Unsplash

**什么是EDA？**

EDA是我们更好地理解数据集的重要方式之一。几乎所有的数据分析和数据科学专家都在产生新观点或者数据建模之前先做EDA。**在现实生活中，依赖于数据集的复杂度和完整性，这个过程会花费大量时间。** 当然，变量越多，我们在下一步开始前就需要探索越多才能获得结论。

这就是为什么我们会用R或者Python这些最常见的数据分析程序语言，一些包能够帮我们更快更容易地完成EDA，但不会做得更好。为什么呢？因为它只会给我们展示一个结论，我们需要深入探索我们觉得“有趣”的变量。

**“80/20规则”适用:80%的数据分析师或科学家的宝贵时间花在简单的查找、清理和组织数据上，只剩下20%的时间用于执行分析。** 

我们需要哪一个库呢？

在R中我们可以用这些库：

1. dataMaid

2. DataExplorer

3. SmartEDA

在Python中，我们可以使用这些库：

1. ydata-profiling

2. dtale

3. sweetviz

4. autoviz

让我们试用一下上面列出的每个库，看看他们长什么样子以及如何帮助我们做探索性数据分析！在本文中，我将会用常用的iris数据集来学习如何在R和Python中编码。

在R中你可以使用以下代码加载iris数据集：

```makefile
 # iris is part of R's default, no need to load any packages
df = iris
# use "head()" to show the first 6 rows
head(df)
```

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBCD6PjPoIWKaUOTqXiauKOYAC5S1XdaIAuu1XSEtzQSJIZ0O4nsVDDlQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图1。 在R中加载' iris '数据集

在Python中，你可以使用以下代码来加载iris数据集:

```python
# need to import these things first
from sklearn.datasets import load_iris
import numpy as np
import pandas as pd
# use load_iris
iris = load_iris()
# convert into a pandas data frame
df = pd.DataFrame(
  data= np.c_[iris['data'], iris['target']],
  columns= iris['feature_names'] + ['species']
)
# set manually the species column as a categorical variable
df['species'] = pd.Categorical.from_codes(iris.target, iris.target_names)
# use ".head()" to show the first 5 rows
df.head()
```

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBZLTzPqZh2S6wllmKKItnPeIEzASoZ6KuHqTc5ZbsT9La9CZPmmJuaw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图2。在Python中加载' iris '数据集

**R : dataMaid**

首先，我们需要执行以下的样例代码：

```sql
# install the dataMaid library
install.packages("dataMaid")
# load the dataMaid library
library(dataMaid)
# use makeDataReport with HTML as output
makeDataReport(df, output = "html", replace = TRUE)
```

从第一个截图(图3)中，我们已经获得了关于iris数据集的大量信息：

1\. 观测值的个数是150。

2\. 变量的个数是5。

3\. 根据每个变量的数据类型执行变量检查，例如识别错误编码的缺失值、< 6 obs的水平和异常值。

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBI7K8PezLpDOW6FNAw8XK6TcNOnQA9WUXKhCoIhWK03GKjHOGPcC7Pg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)
 图3。使用iris数据集的' dataMaid '创建的报告的第一个截图

从第二个截图(图4):

1\. 变量的汇总表包括变量类、唯一值、缺失值和检测到的任何问题。我们可以看到Sepal.Width和Petal.Length变量检测到问题。  

2\. Sepal.Length提供了中心测量，包括单变量分布直方图。

3\. Sepal.Width列出了可能有的异常值。这就是为什么汇总表显示了检测到也有问题。

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBYbcziaP7gFfZ4nNriaqeN8dEwpbg5ggd7ddwgdN0yZYX6MeFn4LhUHaw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图4。使用iris数据集的' dataMaid '创建的报告的第二个截图

第三张截图(图5):

1\. Petal.Length可能有列示的异常值。  

2\. Petal.Width提供了中心测量，包括单变量分布直方图。

3\. 将Species作为目标变量检测为一个factor，每种类型的数据计数相等，均为50。

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBgPIAEQEqgZgsR8gOz7wsDS3ZWUbtHWUSJRjK3ich57hueIXE4Q8vO6Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图5。使用iris数据集的' dataMaid '创建的报告的第三个截图

根据上面使用R中的dataMaid创建的数据报告，我们只需要执行一行代码，就可以获得关于iris数据集的大量信息。

**R：DataExplorer**

首先，我们需要执行下面的简单代码:

```sql

install.packages("DataExplorer")

library(DataExplorer)

create_report(df)
```

从第一个到第六个截图(图6、7、8、9、10、11)，我们得到的信息与前一个包没有太大的不同。

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBRxa2j54Tb2EW6Xjocjevy7ur7webMyyxgoHsudKaLSP2y7FVDAMSQw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图6。使用iris数据集的“DataExplorer”创建的报告的第一个截图  

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBuShlSBmewxSNdSrskaGVQ6ialJ6WDibuCt5utYPwdswic9eDqjK2R8vIA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图7。使用iris数据集的“DataExplorer”创建的报告的第二个截图  

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBRq5XSNbsKQQVadClB9kiaLRhtWfNIAf0C7PhI9nibw2ZzkA7C9uKT1hQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图8。 使用iris数据集的“DataExplorer”创建的报告的第三个截图

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBBZialtO2jK70Wepkb9yxOTXwFYOicG1b2J4WbhosRbOVjibP6gsD9KBWg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图9。 使用iris数据集的“DataExplorer”创建的报告的第四个截图

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VB07uIH1pIZxoKzHhRLsp2Xb1xia9TyvFH6HKue5WyxwIsOAjdNMCicehg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图10。 使用iris数据集的“DataExplorer”创建的报告的第五个截图  

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBn7oGOEicCJuLToF6LthYPVL31LQfZzWVN0cEs4omYe6wyEd1qVlBa1w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图11。 使用iris数据集的“DataExplorer”创建的报告的第六个截图  

从第七个截图(图12)中，我们得到了iris数据集中每个数值变量的QQ图。

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBqe2Vdz5iarn14KC9GRj4pSsVGE0Wda8o5oumsQJicAxdhsibiapOC6lNYA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图12。 使用iris数据集的“DataExplorer”创建的报告的第七个截图

从第八张截图(图13)中，我们得到了iris数据集中每个变量的相关矩阵。我们可以看到一些信息，如：

1\. Petal.Width和Petal.Length具有很强的正相关(0.96)，这意味着在iris数据集中，花瓣宽度越宽，花瓣长度越长。

2\. Species_setosa和Petal.Length与鸢尾的负相关系数为-0.92，表明iris的花瓣长度越短，是山鸢尾的可能性越高。

3\. 使用上面的例子，请使用这个相关矩阵提供你的发现。

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VB5uJ6uGuPegKZf5jJZVAgZ0AiaQKRTrmFZzIjViasLuVvo8Hc3Y0Wlegg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图13。 使用iris数据集的“DataExplorer”创建的报告的第八个快照

第九张截图(图14)使用主成分分析(PCA)，提供了由主成分解释的方差的百分比，其中，标签表示解释方差的累积百分比，它显示62%，越高越好。对于PCA的解释，我想我需要另一篇文章进行说明。

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBicCLWCgibgazMyCMbXPJvrWOib8AzmT1ZbtGfveKiaFjSPgCmgUoVXMLUQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图14。使用iris数据集的“DataExplorer”创建的报告的第九个截图

第十张截图(图15)提供了每个变量的相对重要性，它显示了Petal.Length的重要性最高，约为0.5，其次是Petal.Width等等。

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBYVaRcbR2XfolTupRvGmxcricPFg1Sbia01H06kqgs0MR4vcs4Vw29hgw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图15。使用iris数据集的“DataExplorer”创建的报告的第10个截图

**R:SmartEDA**

首先，我们需要执行下面的简单代码：

```sql
# install the SmartEDA library
install.packages("SmartEDA")
# load the SmartEDA library
library(SmartEDA)
# use ExpReport
ExpReport(df, op_file = 'SmartEDA_df.html')
```

从图16、17、18、23和24中，我们得到的信息与之前的包没有太大的不同。

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBuVjscoic8icV4q9xLtrTdSnMAuoGYgHL3c9QUlvPnIrKCMZGYDfDo5vA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图16。使用iris数据集的“SmartEDA”创建的报告的第一个截图![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBDOQ3TLJib3fV93qGE3kibVauqZgMOEr6EbUicAHzVFcaG0GzqDJkb2KsA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图17。使用iris数据集的“SmartEDA”创建的报告的第二个截图

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBAV8EM8dx9miae40jDicibOpe2L3PWSsN3mYTVZicVrtE2CEichNcn8hQqqw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)
 图18。使用虹膜数据集的“SmartEDA”创建的报告的第三个截图

从图19中，我们看到了每个变量的密度图，包括偏度和峰度测量，这是用来告诉我们数据是否正态分布的。

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBkSnD4sg7KEsYm8twYSvFsJDxJ8vgCciaX78SuwxxrIpQWWia6ibQbQtsA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图19。使用iris数据集的“SmartEDA”创建的报告的第四个截图  

从图20、21和22中，我们看到了iris数据集中可用的数值变量之间的散点图，它直观地告诉了我们相关性，为我们提供了与数字格式相关矩阵类似的信息。

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBEdDo4Eh55g2EuYlwGpr8ZT5RYBjlGfmKWVLMd7sQsDdRCL40o452Xw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图20。 使用iris数据集的“SmartEDA”创建的报告的第五个截图  

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBtiae0B6NnOke9v4wX4GhtCA8GLRoxb6AIBicia2VbBNNMrq9meffhqaAA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图21。 使用iris数据集的“SmartEDA”创建的报告的第六个截图  

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBWQ0udZkLG48N4kfByzicgBMHG90ibbUh8kAiaqRbkJWW5iadxbLtwYC9bQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图22。使用iris数据集的“SmartEDA”创建的报告的第七个截图  

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBb5hmZqZwAxjJVqAZYk4yp8nPOfeL9rVLqicb5YOCsExU7NumSYM2yaQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图23。使用虹膜数据集的“SmartEDA”创建的报告的第九个截图

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VB376qaKemQQ7lLAicojJTkOnLWZpvQ8hgmYEA833PZmEbYem2hbibPk7g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图24。使用虹膜数据集的“SmartEDA”创建的报告的第十个截图

**R：结论**

使用上面的三个包，我们得到了很多关于iris数据集的信息。这比我们尝试手动创建它要快得多，但这还不够，正因如此，我在标题中说“…更快更容易…”，因为它只给了我们一个iris数据集的概略，但至少它给了我们哪些事情我们可以开始工作，而不是寻找起点，比如:

1\. 没有丢失的变量/没有错误编码的变量，我们可以跳过这些步骤。

2\. 在某些变量中检测到离群值，我们可以通过使用任何适当的方法来处理离群值来开始清理数据，而不是手动逐个查找哪些变量有离群值。

3\. 如果需要，我们可以开始处理非正态分布的变量。

4\. 根据相关矩阵和散点图，我们可以看到哪些变量是强相关的，哪些是弱相关的。

5. 使用主成分分析(PCA)提供了由主成分解释的方差的百分比，标签表示已解释方差的累积百分比

6. iris数据集的每个特征的相对重要性也显示在这个自动化的EDA中

**Python: ydata-profiling**

首先，我们需要执行下面的简单代码：

```properties

pip install ydata-profiling

from ydata_profiling import ProfileReport

pr_df = ProfileReport(df)

pr_df
```

大多数情况下，它显示类似的信息。我将尝试提及一些与以前的软件包完全不同的信息：

1\. 在图26中，我们总结了哪些变量具有高相关性。

2\. 总的来说，与以前的包相比，输出更具交互性，因为我们可以单击以移动到其他选项卡，并选择要显示的特定列。

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VB6boy1GgFyUQrQ2C0pv2cgXaRZ2l2omToS9sPZazsxasibRfia9N33Qyg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图25。使用iris数据库的' ydata_profiling '创建的报告的第一个截图  

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBMbXw6HzuhyPnqANflV9xkiak0b3Vg9B4HqKzmTjcw3qwNzz6zcKh9uQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图26。使用iris数据集的' ydata_profiling '创建的报告的第二个截图  

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBEtbmZV7y7o8YyUPnHia9CQGsAJY57NDneNaFqMrV4CJVnLgog6G0syQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图27。 使用iris数据集的' ydata_profiling '创建的报告的第三个截图  

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBK2oOPD4rxibh9icQblDn96fvJp5rCMfLvKYQ24ZSynkIvAjskvwicxjHg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图28。 使用iris数据集的' ydata_profiling '创建的报告的第四个截图

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBibduMIqiaZrYvamakJUVyoLt7Wu5lXMPnS4bgvmHFNWiblbLQT0TOW5ug/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图29。使用iris数据集的' ydata_profiling '创建的报告的第五个截图  

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBTdYQAFLCb5pI3zukicsc1Ticuiad52IhTDqZI9BKApNaVh3RYicZBgs8Ig/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图30。 使用iris数据集的' ydata_profiling '创建的报告的第六个截图  

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBe8ZTBzuVk3dXJySPhqH1mEqdyK35nVQ2AvuQ9e0LAHjzqFZQ4hJVAQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图31。 使用iris数据集的' ydata_profiling '创建的报告的第七个截图  

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VB8KpRhvthKszRv2vYeA11cwxjAffV1OBbEXsST4moR8bpEribevPYsgQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图32。 使用iris数据集的' ydata_profiling '创建的报告的第八个截图  

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBPLmEr8Fs0lVS80APwer81Srv39G9iaicgSdaRaLWKlSoTNXicxzZNS8WQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图33。 使用iris数据集的' ydata_profiling '创建的报告的第九个截图

**Python: dtale**

首先，我们需要执行下面的简单代码：

```properties

pip install dtale

import dtale

dtale.show(df)
```

这个包的输出和以前的包有很大的不同，在如何使用方面，内容都很相似，但是它让我们可以更好的去探索。

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBkuBWVsyl3VGWGVWlRze44Rod27a8BBBOeTp4PykwlVia7YibcmGyM0Dw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图34。使用iris数据集的' dtale '创建的报告的第一个截图  

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBNKsBZGQcJvoKTOiao10AUcnRIvYDgDOIbpbLZnpLjrDWxn0RhJSvyNw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图35。使用iris数据集的' dtale '创建的报告的第二个截图  

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBtDgZnNsFpYr5Mzeuges6LGqF8yIEqCcsKeE0hTlSUqaqdVKUsPsFjw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图36。使用iris数据集的' dtale '创建的报告的第三个截图  

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBow8xIoGBPIIJKic7ZJdmUzDUMJJkeCTiaEKrkqCnjMtDA7a0uXqJiaAicA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图37。使用iris数据集的' dtale '创建的报告的第四个截图  

**Python: sweetviz**

首先，我们需要执行下面的简单代码：

```sql
# install the sweetviz package
pip install sweetviz
# load the sweetviz
import sweetviz
# use analyze
analyze_df = sweetviz.analyze([df, "df"], target_feat = 'species')
# then show
analyze_df.show_html('analyze.html')
```

使用这个包，UI和UX有很大的不同，请欣赏!

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBiciaCZWxKwDibICnK6PLlK0ia1npYaPa0WDrOX9AH9ckSzNbUibLLb31MUg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图38。使用iris数据集的' sweetviz '创建的报告的第一个截图

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBicMprnfnLLZcT71tEicN8xZhn8HSlHIMYyjGiaqiaiaSFICvRicqhoNgYhag/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图39。 使用iris数据集的' sweetviz '创建的报告的第二个截图

人类是视觉动物，这意味着人脑处理图像的速度是文本的6万倍，传递到大脑的信息中有90%是视觉信息。可视化信息使协作变得更容易，并产生影响组织绩效的新想法。这解释了为什么数据分析师在数据可视化上花费的时间是最多的。

**Python: autoviz**

首先，我们需要执行下面的简单代码：

```properties
# install the dtale package
pip install autoviz
# load the autoviz
from autoviz import AutoViz_Class
# set AutoViz_Class()
av = AutoViz_Class()
# produce AutoVize_Class of df
avt = av.AutoViz(
    "",
    sep = ",",
    depVar = "",
    dfte = df,
    header = 0,
    verbose = 1,
    lowess = False,
    chart_format = "server",
    max_rows_analyzed = 10000,
    max_cols_analyzed = 10,
    save_plot_dir=None
)
```

使用上面的代码，在浏览器中生成了一些选项卡。使用这个包我们可以看到的新东西：

1\. 输出在浏览器的多个选项卡中生成，以前的包将所有输出显示在一个选项卡中。

2\. 每个变量的小提琴图。它是箱线图和核密度图的混合版本。仍然显示与以前的包相似的信息。

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBIjDJO3k3zwqrhGes1gFbkicpZibLppNu22nyjaNiakjPrHkOYnmny6YDA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图40。使用虹膜数据集的“autoviz”创建的报告的第一个截图  

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBWeTibCwCicqM2FbQKgQLh3TX5UsBia5DhCEXU3GNibrsbicvzHAdFx84nwg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图41。使用iris数据集的“autoviz”创建的报告的第二个截图  

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBBjxGK9PbhSRes1yxdeV5cgCxWLwbwd3kXqtsib6BwF6wDAtMotJRHibg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图42。使用iris数据集的“autoviz”创建的报告的第三个截图  

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBAprUZnwuA4DBcQShUvxdzWhMS2byYD7msp3AB1ktlT7FI2fP783oqA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图43。使用iris数据集的“autoviz”创建的报告的第四个截图  

![](https://mmbiz.qpic.cn/mmbiz_gif/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBwIsVbXXT0KfHyjkpRpmAHm04SHNC4JjJp2npoBgXKTb94YIcRGj2oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

![](https://mmbiz.qpic.cn/mmbiz_png/heS6wRSHVMn8AFBLlNpdIgGWic8spS4VBb77ql1sXU7ubxXtib37GuEy3oEibEvs9xsfV7T1GM9RSJAfico9xukZiag/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图44。使用虹膜数据集的“autoviz”创建的报告的第五个截图  

**Python:结论**

使用上面的四个包，我们得到了很多关于iris数据集的信息，与R包相比没有太大的区别，但是有更多的透视图。一些注意事项：

1\. 与R包相比，Python包的输出大多更具交互性。

2\. 安装过程中可能会出现一些错误。对于这个dtale，常见的错误是关于jinja和escape。你可以参考这篇文章找到解决方案。

3\. 在一些包中，代码不像在R包中那么简单，但我认为它不是大问题，只要我们勤于阅读指导手册，就很好。

**结论**

我要用哪一个?哪一个是最好的?哪一个与我的数据集最兼容?

视情况而定。

我们尝试探索、解释上面的每个包并精确地使用它，其目的并不是作为主要的解决方案。毕竟，能够帮助我们有效地减少EDA时间已经是一件好事了。**在我看来，探索数据应该是数据分析的“乐趣”部分，所以不要害怕亲手做EDA的“肮脏”，有时非自动化方法仍然是最好的。** 

**感谢您的阅读!**

哇，我刚刚意识到这篇文章包含44张图片。如果您读到了这里，我很感激您想通过我的文章阅读和学习如何自动执行EDA的过程。我希望你喜欢这篇文章，并学习如何在你作为数据分析/科学专业人士的旅程中使用它。