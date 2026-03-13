# R 版 46：使用交叉验证进行模型选择 📊

![](img/7fea33d677987254ee64fc1e2ed231db_0.png)

在本节课中，我们将学习如何使用交叉验证进行模型选择。交叉验证是一种评估模型泛化能力的强大技术，尤其适用于样本量有限的情况。我们将重点介绍十折交叉验证，并通过R语言实现这一过程。

上一节我们介绍了使用验证集和内置统计量（如Cp）进行模型选择的方法。本节中，我们来看看如何利用交叉验证，特别是十折交叉验证，来更稳健地选择最佳模型。

![](img/7fea33d677987254ee64fc1e2ed231db_2.png)

![](img/7fea33d677987254ee64fc1e2ed231db_3.png)

![](img/7fea33d677987254ee64fc1e2ed231db_5.png)

## 交叉验证模型选择 🔄

![](img/7fea33d677987254ee64fc1e2ed231db_7.png)

![](img/7fea33d677987254ee64fc1e2ed231db_8.png)

我们将使用十折交叉验证。这种方法易于实现，虽然可以编写函数来完成，但了解其底层实现过程非常有价值。

![](img/7fea33d677987254ee64fc1e2ed231db_10.png)

![](img/7fea33d677987254ee64fc1e2ed231db_12.png)

首先，我们设置随机种子以确保结果可重现。这次我们使用种子 `11`。

![](img/7fea33d677987254ee64fc1e2ed231db_14.png)

![](img/7fea33d677987254ee64fc1e2ed231db_16.png)

![](img/7fea33d677987254ee64fc1e2ed231db_18.png)

```r
set.seed(11)
```

![](img/7fea33d677987254ee64fc1e2ed231db_20.png)

![](img/7fea33d677987254ee64fc1e2ed231db_21.png)

![](img/7fea33d677987254ee64fc1e2ed231db_23.png)

接下来，我们需要为数据集中的每个观测分配一个折号（从1到10）。目标是让每个折中的观测数量尽可能均衡。

![](img/7fea33d677987254ee64fc1e2ed231db_25.png)

![](img/7fea33d677987254ee64fc1e2ed231db_27.png)

以下是实现步骤：
1.  创建一个长度为数据集行数的向量，其元素为重复的1到10。
2.  使用 `sample()` 函数随机打乱这个向量，实现随机分配。

![](img/7fea33d677987254ee64fc1e2ed231db_29.png)

![](img/7fea33d677987254ee64fc1e2ed231db_31.png)

![](img/7fea33d677987254ee64fc1e2ed231db_32.png)

```r
folds <- sample(rep(1:10, length = nrow(Hitters)))
table(folds)
```

![](img/7fea33d677987254ee64fc1e2ed231db_34.png)

![](img/7fea33d677987254ee64fc1e2ed231db_36.png)

![](img/7fea33d677987254ee64fc1e2ed231db_37.png)

运行后，`table(folds)` 会显示每个折中的观测数量，它们大致相等（26或27个），这对于263个观测来说是尽可能均衡的。

![](img/7fea33d677987254ee64fc1e2ed231db_39.png)

![](img/7fea33d677987254ee64fc1e2ed231db_41.png)

![](img/7fea33d677987254ee64fc1e2ed231db_43.png)

现在，我们创建一个矩阵来存储误差。这个矩阵有10行（对应10折）和19列（对应从1到19个变量的不同子集模型）。

![](img/7fea33d677987254ee64fc1e2ed231db_45.png)

![](img/7fea33d677987254ee64fc1e2ed231db_47.png)

```r
cv.errors <- matrix(NA, 10, 19)
```

![](img/7fea33d677987254ee64fc1e2ed231db_49.png)

![](img/7fea33d677987254ee64fc1e2ed231db_50.png)

核心部分是一个双重循环。外层循环遍历每一折（k从1到10），内层循环遍历每个子集大小（i从1到19）。

![](img/7fea33d677987254ee64fc1e2ed231db_52.png)

![](img/7fea33d677987254ee64fc1e2ed231db_53.png)

以下是循环内的操作流程：
1.  **训练模型**：使用 `regsubsets()` 在所有**不属于**第k折的观测数据上拟合模型。公式为 `Salary ~ .`，数据为 `Hitters[folds != k, ]`。
2.  **进行预测**：对于当前子集大小 `i`，使用我们之前编写的 `predict.regsubsets()` 函数，对**属于**第k折的观测数据（即测试集）进行预测。调用方式为 `predict(best.fit, Hitters[folds == k, ], id = i)`。
3.  **计算误差**：计算预测值与真实值之间的均方误差（MSE），并将其存储在 `cv.errors` 矩阵的第k行、第i列。

![](img/7fea33d677987254ee64fc1e2ed231db_55.png)

![](img/7fea33d677987254ee64fc1e2ed231db_56.png)

![](img/7fea33d677987254ee64fc1e2ed231db_57.png)

```r
for(k in 1:10) {
  best.fit <- regsubsets(Salary ~ ., data = Hitters[folds != k, ], nvmax = 19)
  for(i in 1:19) {
    pred <- predict(best.fit, Hitters[folds == k, ], id = i)
    cv.errors[k, i] <- mean((Hitters$Salary[folds == k] - pred)^2)
  }
}
```

![](img/7fea33d677987254ee64fc1e2ed231db_58.png)

![](img/7fea33d677987254ee64fc1e2ed231db_59.png)

![](img/7fea33d677987254ee64fc1e2ed231db_61.png)

![](img/7fea33d677987254ee64fc1e2ed231db_62.png)

循环执行完毕后，我们得到了一个完整的误差矩阵。

![](img/7fea33d677987254ee64fc1e2ed231db_63.png)

![](img/7fea33d677987254ee64fc1e2ed231db_65.png)

## 处理结果并绘图 📈

![](img/7fea33d677987254ee64fc1e2ed231db_67.png)

![](img/7fea33d677987254ee64fc1e2ed231db_68.png)

![](img/7fea33d677987254ee64fc1e2ed231db_70.png)

现在我们需要处理输出矩阵。我们对矩阵的**列**求均值，即计算每个子集大小（i）在所有10折上的平均均方误差。然后，对其取平方根，得到每个子集大小对应的**均方根误差（RMSE）**。

![](img/7fea33d677987254ee64fc1e2ed231db_71.png)

![](img/7fea33d677987254ee64fc1e2ed231db_73.png)

![](img/7fea33d677987254ee64fc1e2ed231db_74.png)

```r
rmse.cv <- sqrt(apply(cv.errors, 2, mean))
```

![](img/7fea33d677987254ee64fc1e2ed231db_75.png)

![](img/7fea33d677987254ee64fc1e2ed231db_77.png)

![](img/7fea33d677987254ee64fc1e2ed231db_79.png)

最后，我们可以绘制十折交叉验证的RMSE曲线。

![](img/7fea33d677987254ee64fc1e2ed231db_81.png)

![](img/7fea33d677987254ee64fc1e2ed231db_82.png)

![](img/7fea33d677987254ee64fc1e2ed231db_83.png)

```r
plot(rmse.cv, pch = 19, type = "b", xlab = "Number of Variables", ylab = "RMSE (CV)")
```

![](img/7fea33d677987254ee64fc1e2ed231db_85.png)

与之前单一的验证集误差曲线相比，这条交叉验证曲线更加平滑，因为它综合了全部训练数据的信息（尽管是分折计算后平均）。根据该曲线，包含11或12个变量的模型似乎表现最佳。

![](img/7fea33d677987254ee64fc1e2ed231db_86.png)

![](img/7fea33d677987254ee64fc1e2ed231db_88.png)

![](img/7fea33d677987254ee64fc1e2ed231db_89.png)

本节课中我们一起学习了如何使用十折交叉验证进行模型选择。我们通过手动分配折、构建双重循环来训练和测试模型，并计算平均误差，最终通过误差曲线确定了表现最佳的模型复杂度。交叉验证提供了一种比单一验证集更稳定、更可靠的模型评估方法。