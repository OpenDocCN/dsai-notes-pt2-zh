# Python 版 51：岭回归与Lasso回归 I 🏔️

在本节课中，我们将要学习两种重要的线性模型正则化方法：岭回归和Lasso回归。我们将通过Python的`scikit-learn`库来实践这两种方法，理解它们如何通过惩罚系数的大小来防止过拟合，并学习如何通过交叉验证选择最优的正则化参数。

上一节我们介绍了前向逐步选择法，这是一种变量选择方法。本节中我们来看看岭回归和Lasso回归，它们同样用于处理高维数据和防止过拟合，但采用了不同的正则化策略。

![](img/e1d6772d620b01bf012c1224408abe2f_1.png)

![](img/e1d6772d620b01bf012c1224408abe2f_2.png)

![](img/e1d6772d620b01bf012c1224408abe2f_4.png)

![](img/e1d6772d620b01bf012c1224408abe2f_5.png)

## 概述与数据准备

![](img/e1d6772d620b01bf012c1224408abe2f_7.png)

![](img/e1d6772d620b01bf012c1224408abe2f_8.png)

![](img/e1d6772d620b01bf012c1224408abe2f_9.png)

![](img/e1d6772d620b01bf012c1224408abe2f_11.png)

我们将使用与之前相同的数据集。在应用岭回归和Lasso之前，通常需要对数据进行标准化，以确保每个变量在惩罚项中具有可比性。

![](img/e1d6772d620b01bf012c1224408abe2f_13.png)

![](img/e1d6772d620b01bf012c1224408abe2f_14.png)

![](img/e1d6772d620b01bf012c1224408abe2f_15.png)

以下是数据标准化的步骤：
```python
# 假设 X 是特征数据
X_scaled = (X - X.mean(axis=0)) / X.std(axis=0)
```

![](img/e1d6772d620b01bf012c1224408abe2f_17.png)

![](img/e1d6772d620b01bf012c1224408abe2f_18.png)

## 岭回归

![](img/e1d6772d620b01bf012c1224408abe2f_19.png)

![](img/e1d6772d620b01bf012c1224408abe2f_20.png)

![](img/e1d6772d620b01bf012c1224408abe2f_22.png)

![](img/e1d6772d620b01bf012c1224408abe2f_23.png)

![](img/e1d6772d620b01bf012c1224408abe2f_24.png)

岭回归通过在普通最小二乘法的损失函数中添加一个L2惩罚项（系数平方和）来约束模型系数的大小。

![](img/e1d6772d620b01bf012c1224408abe2f_26.png)

其损失函数公式为：
**Loss = RSS + λ * Σ(βj²)**
其中，RSS是残差平方和，λ是控制惩罚强度的正则化参数。

![](img/e1d6772d620b01bf012c1224408abe2f_28.png)

### 绘制岭回归路径

![](img/e1d6772d620b01bf012c1224408abe2f_30.png)

![](img/e1d6772d620b01bf012c1224408abe2f_31.png)

![](img/e1d6772d620b01bf012c1224408abe2f_32.png)

我们可以使用`scikit-learn`的`ElasticNet`路径方法，通过设置`l1_ratio=0`来获得纯粹的岭回归解路径。

![](img/e1d6772d620b01bf012c1224408abe2f_34.png)

![](img/e1d6772d620b01bf012c1224408abe2f_35.png)

![](img/e1d6772d620b01bf012c1224408abe2f_36.png)

![](img/e1d6772d620b01bf012c1224408abe2f_38.png)

以下是获取并绘制系数路径的代码：
```python
from sklearn.linear_model import enet_path
import numpy as np

![](img/e1d6772d620b01bf012c1224408abe2f_40.png)

![](img/e1d6772d620b01bf012c1224408abe2f_41.png)

![](img/e1d6772d620b01bf012c1224408abe2f_43.png)

# 定义一系列lambda值（在scikit-learn中称为alpha）
lambdas = np.logspace(10, -2, 100) * 0.5
# 计算岭回归路径（l1_ratio=0 代表纯岭回归）
alphas_enet, coefs_enet, _ = enet_path(X_scaled, y, l1_ratio=0, alphas=lambdas)
```
这段代码会生成一个19x100的矩阵，每一行代表一个特征系数随λ变化的路径。

![](img/e1d6772d620b01bf012c1224408abe2f_45.png)

![](img/e1d6772d620b01bf012c1224408abe2f_46.png)

![](img/e1d6772d620b01bf012c1224408abe2f_48.png)

![](img/e1d6772d620b01bf012c1224408abe2f_49.png)

![](img/e1d6772d620b01bf012c1224408abe2f_51.png)

![](img/e1d6772d620b01bf012c1224408abe2f_52.png)

生成的路径图显示，当λ很大时（惩罚很强），所有系数都趋近于0。随着λ减小，系数逐渐向普通最小二乘解靠近。

![](img/e1d6772d620b01bf012c1224408abe2f_54.png)

![](img/e1d6772d620b01bf012c1224408abe2f_55.png)

### 交叉验证选择最优λ

![](img/e1d6772d620b01bf012c1224408abe2f_57.png)

![](img/e1d6772d620b01bf012c1224408abe2f_59.png)

![](img/e1d6772d620b01bf012c1224408abe2f_61.png)

![](img/e1d6772d620b01bf012c1224408abe2f_62.png)

为了选择最优的λ值，我们需要评估模型在不同λ下的性能。我们可以使用管道将标准化和岭回归模型组合，并进行交叉验证。

![](img/e1d6772d620b01bf012c1224408abe2f_64.png)

![](img/e1d6772d620b01bf012c1224408abe2f_66.png)

![](img/e1d6772d620b01bf012c1224408abe2f_68.png)

以下是构建管道和进行网格搜索交叉验证的步骤：
```python
from sklearn.pipeline import Pipeline
from sklearn.linear_model import Ridge
from sklearn.preprocessing import StandardScaler
from sklearn.model_selection import GridSearchCV

![](img/e1d6772d620b01bf012c1224408abe2f_69.png)

![](img/e1d6772d620b01bf012c1224408abe2f_71.png)

![](img/e1d6772d620b01bf012c1224408abe2f_72.png)

![](img/e1d6772d620b01bf012c1224408abe2f_73.png)

![](img/e1d6772d620b01bf012c1224408abe2f_75.png)

# 创建管道：先标准化，再岭回归
pipe = Pipeline([('scaler', StandardScaler()), ('ridge', Ridge())])
# 定义要搜索的参数网格
param_grid = {'ridge__alpha': lambdas}
# 设置交叉验证方法（这里使用验证集方法）
cv_method = ShuffleSplit(n_splits=1, test_size=0.5, random_state=0)
# 执行网格搜索
grid = GridSearchCV(pipe, param_grid, cv=cv_method, scoring='neg_mean_squared_error')
grid.fit(X, y)
```
通过交叉验证，我们可以找到使均方误差最小的最优λ值，并得到对应的最佳模型。

![](img/e1d6772d620b01bf012c1224408abe2f_76.png)

![](img/e1d6772d620b01bf012c1224408abe2f_78.png)

![](img/e1d6772d620b01bf012c1224408abe2f_79.png)

## Lasso回归

![](img/e1d6772d620b01bf012c1224408abe2f_81.png)

Lasso回归与岭回归类似，但它使用的是L1惩罚项（系数绝对值之和）。L1惩罚的一个重要特性是能够将某些系数精确地压缩为零，从而实现变量选择。

![](img/e1d6772d620b01bf012c1224408abe2f_83.png)

![](img/e1d6772d620b01bf012c1224408abe2f_84.png)

![](img/e1d6772d620b01bf012c1224408abe2f_86.png)

![](img/e1d6772d620b01bf012c1224408abe2f_88.png)

![](img/e1d6772d620b01bf012c1224408abe2f_90.png)

其损失函数公式为：
**Loss = RSS + λ * Σ|βj|**

![](img/e1d6772d620b01bf012c1224408abe2f_92.png)

![](img/e1d6772d620b01bf012c1224408abe2f_94.png)

![](img/e1d6772d620b01bf012c1224408abe2f_96.png)

![](img/e1d6772d620b01bf012c1224408abe2f_97.png)

### 绘制Lasso路径

![](img/e1d6772d620b01bf012c1224408abe2f_99.png)

![](img/e1d6772d620b01bf012c1224408abe2f_101.png)

将`enet_path`函数中的`l1_ratio`参数设置为1，即可计算Lasso的解路径。

![](img/e1d6772d620b01bf012c1224408abe2f_103.png)

![](img/e1d6772d620b01bf012c1224408abe2f_105.png)

以下是相关代码：
```python
# 计算Lasso路径（l1_ratio=1 代表纯Lasso回归）
alphas_enet, coefs_enet, _ = enet_path(X_scaled, y, l1_ratio=1, alphas=lambdas)
```
与岭回归平滑的路径不同，Lasso的路径是分段线性的。对于较大的λ值，许多系数恰好为零。随着λ减小，系数逐个被“激活”为非零值，有时系数也可能重新变为零。

![](img/e1d6772d620b01bf012c1224408abe2f_107.png)

![](img/e1d6772d620b01bf012c1224408abe2f_109.png)

![](img/e1d6772d620b01bf012c1224408abe2f_110.png)

![](img/e1d6772d620b01bf012c1224408abe2f_112.png)

### 比较与总结

![](img/e1d6772d620b01bf012c1224408abe2f_114.png)

![](img/e1d6772d620b01bf012c1224408abe2f_116.png)

在本节课中我们一起学习了岭回归和Lasso回归的核心概念与实现。

![](img/e1d6772d620b01bf012c1224408abe2f_118.png)

*   **岭回归**：通过L2惩罚收缩系数，所有系数始终非零，模型更稳定。
*   **Lasso回归**：通过L1惩罚进行变量选择，可以产生稀疏模型（即部分系数为零）。

![](img/e1d6772d620b01bf012c1224408abe2f_120.png)

![](img/e1d6772d620b01bf012c1224408abe2f_121.png)

两种方法都需要通过交叉验证来选择恰当的正则化强度λ。在实践中，对于同一数据集，岭回归和Lasso回归的预测误差可能非常接近，但Lasso提供了可解释性更强的稀疏模型。

![](img/e1d6772d620b01bf012c1224408abe2f_123.png)

![](img/e1d6772d620b01bf012c1224408abe2f_125.png)

![](img/e1d6772d620b01bf012c1224408abe2f_127.png)

![](img/e1d6772d620b01bf012c1224408abe2f_128.png)

![](img/e1d6772d620b01bf012c1224408abe2f_129.png)

![](img/e1d6772d620b01bf012c1224408abe2f_130.png)

通过`scikit-learn`的管道和网格搜索工具，我们可以高效地完成数据预处理、模型训练和超参数调优的整个流程。