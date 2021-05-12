﻿# 环境

* 语言：Python 3.6.1
* 操作系统：windows
* 模块：statsmodels 0.12.1 tqdm 4.50.2 pandas 1.0.5 numpy 1.19.5 scikit-learn 0.23.2 lightgbm 2.3.1

# 代码思路

* 对于任务一，我采用了lgb模型对时序数据进行回归建模，特征包括节假日信息，当天的日期信息，包含年月日季度等等信息， 对于AB两类不同的岗位分别训练建模，均使用2020年11月以前的全部数据进行训练，使用2020年11月的数据作为验证集；
* 对于任务二，我采用了两个不同的模型进行平均融合，首先是lgb模型，特征包括节假日信息，上一日的节假日信息等等，另外还有不同之处在于，在任务二中我采用分岗位细类分别进行预测，最后将同岗位的数据按periods加和获得最终预测结果；第二个是arima模型，我将节假日信息作为外部信息对模型进行增强，对不同periods的时间序列分别进行建模。最后将这俩模型根据任务一的预测结果进行数据缩放（因为任务一的性能较优，用任务一来指导任务二模型更加逼近真实值）。

# 复现过程

* 对于任务一，直接运行day_lgb.ipynb即可生成提交文件
* 对于任务二，先运行hour_arima.ipynb, 再运行hour_lgb.ipynb即可