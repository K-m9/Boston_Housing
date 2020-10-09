# 波士顿房价模型(Boston_Housing)

## 1 建模目标
分析三个自变量与房价估值之间的关系，建立回归模型。
- How to use NumPy to investigate the latent features of a dataset.
- How to analyze various learning performance plots for variance and bias.
- How to determine the best-guess model for predictions from unseen data.
- How to evaluate a model's performance on unseen data using previous data.

## 2 数据解释
波士顿住房数据收集于1978年，506个条目中的每一个都代表了来自马萨诸塞州波士顿不同郊区的14个住房特征的汇总数据。
- 自变量
 - RM: 每个住宅的平均房间数 (average number of rooms per dwelling)
 - LSTAT: 被认为地位较低的人口的百分比 (percentage of population considered lower status)
 - PTRATIO: 按城镇分配的学生与教师比例 (pupil-teacher ratio by town)

- 因变量
 - MEDV: 该房屋的价值的估值中值 (median value of owner-occupied homes)

## 3 模型的建立与求解
### 3.1 数据预处理
#### 3.1.1 缺失值处理
```python3
df.isnull().any()
```
结果如下：
```python3
RM         False
LSTAT      False
PTRATIO    False
MEDV       False
dtype: bool
```
说明无缺失值。

#### 3.1.2 异常值处理
用马氏距离法计算每个样品到样本均值间的距离。设![](https://latex.codecogs.com/svg.latex?x^{(1)},...,x^{(n)})（其中 ![](https://latex.codecogs.com/svg.latex?x^{(i)}=(x_{i1},...,x_{ip})%27)）
为来自分布为![](https://latex.codecogs.com/svg.latex?N_p(\overline%20x,S))的n个样品，其中![](https://latex.codecogs.com/svg.latex?{\overline%20x}=(\overline%20x_1,\overline%20x_p)).
则样品![](https://latex.codecogs.com/svg.latex?x^{(i)})到均值 ![](https://latex.codecogs.com/svg.latex?\overline%20x)的马氏距离定义为<br>
<div align=center><img width="200" height="40" src="https://latex.codecogs.com/svg.latex?D_i^2(x)=%20(x_i-\overline%20x)S^{-1}(x_i-\overline%20x)^T"/></div>
其中S取样本协方差阵的估计值。<br>

可以得出,![](https://latex.codecogs.com/svg.latex?D_i)服从卡方分布，
![](https://latex.codecogs.com/svg.latex?\chi^2_{0.05}(4)=11.14),可得出所有的![](https://latex.codecogs.com/svg.latex?D_i^2%3E11.14)的个数为0个，说明无异常值。

### 3.2 模型建立
由于模型的特征值较少，本文使用Lasso回归、弹性网回归和SVR进行建模比较，最终得出SVR模型的![](https://latex.codecogs.com/svg.latex?R^2)最大，因此取SVR模型作为最终模型。
#### 3.2.1 支持向量机回归
##### 3.2.1.1 SVR基础知识
给定训练样本![](https://latex.codecogs.com/svg.latex?D=\{(x_1,y_1),(x_2,y_2),...,(x_m,y_m)\},y_i\in{R}),希望学得一个形如![](https://latex.codecogs.com/svg.latex?f(x)=\omega^Tx+b)的回归模型，使得f(x)与y尽可能接近。假定能容忍f(x)与y之间最多有![](https://latex.codecogs.com/svg.latex?\epsilon)的偏差，
即仅当f(x)与y之间的差别绝对值大于![](https://latex.codecogs.com/svg.latex?\epsilon)时才计算损失。SVR模型可
以如下形式表示：



## 4 结论


## 5 参考文献
[1] 赵慧,甘仲惟,肖明.多变量统计数据中异常值检验方法的探讨[J].华中师范大学学报(自然科学版),2003(02):133-137.<br>
[2] 高惠璇.应用多元统计分析[M].北京,北京大学出版社,2005.54：103
