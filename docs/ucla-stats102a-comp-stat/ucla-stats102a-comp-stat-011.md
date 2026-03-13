# 11：循环

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_0.png)

在本节课中，我们将要学习R语言中的循环结构。循环允许我们重复执行一段代码，每次执行时可能带有略微不同的条件或值。我们将介绍`for`循环、`while`循环和`repeat`循环，并探讨如何高效地存储循环结果。此外，我们还将学习`break`和`next`语句来控制循环流程，并讨论向量化操作作为替代循环、提升代码效率的重要方法。

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_2.png)

## 🔄 `for`循环

`for`循环是R中最简单、最常见的循环类型。它遍历一个向量（可以是原子向量或列表）中的每个元素，并对每个元素执行代码块。

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_4.png)

以下是`for`循环的基本语法示例：
```r
for (x in 1:10) {
  cat(x^2, " ")
}
```
这段代码会输出从1到10每个数字的平方，结果以空格分隔：`1 4 9 16 25 36 49 64 81 100`。

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_6.png)

`for`循环也可以遍历列表。例如：
```r
L <- list(c(1,2,3), c("a","b","c","d","e","f","g"), c(TRUE, FALSE))
for (y in L) {
  print(length(y))
}
```
这段代码会依次输出列表中每个元素的长度：`3`、`7`、`2`。

## 📝 存储循环结果

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_8.png)

在循环中存储结果时，最佳实践是预先分配好存储空间，而不是在循环过程中动态增长对象。这可以显著提升性能。

以下是三种存储策略的比较：
1.  **预先分配空间（最佳）**：如果你知道结果的数量，可以预先创建一个足够长的向量来存储。
    ```r
    n <- 1e7
    results <- rep(NA, n) # 预先分配空间
    for (x in seq_along(results)) {
      results[x] <- x^2
    }
    ```
    这种方法速度最快。

2.  **动态调整大小（尚可）**：如果你不确定结果数量，可以从一个空对象开始，在每次迭代中调整其大小。
    ```r
    results <- 0 # 从一个元素开始
    for (x in 1:1e7) {
      results[x] <- x^2 # R会自动调整向量大小
    }
    ```
    这种方法比第一种慢，但可以接受。

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_10.png)

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_12.png)

3.  **逐步追加（避免使用）**：在循环中不断使用`c()`函数合并结果。
    ```r
    results <- c() # 空向量
    for (x in 1:1e5) { # 仅10万次，而非1000万次
      results <- c(results, x^2) # 非常低效！
    }
    ```
    这种方法效率极低，应尽量避免。

## 🔁 `while`循环与`repeat`循环

上一节我们介绍了按固定次数迭代的`for`循环，本节中我们来看看基于条件迭代的循环。

`while`循环会重复执行代码块，直到其条件语句的值为`FALSE`。
```r
i <- 1
results <- numeric(10)
while (i <= 10) {
  results[i] <- i^2
  i <- i + 1
}
# 循环结束后，i的值为11
```

`repeat`循环会无限重复执行，直到遇到`break`语句。
```r
i <- 1
results <- numeric(10)
repeat {
  results[i] <- i^2
  i <- i + 1
  if (i > 10) break # 满足条件时跳出循环
}
```

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_14.png)

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_15.png)

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_16.png)

**注意**：务必确保`while`循环的条件最终会变为`FALSE`，或在`repeat`循环中设置合理的`break`条件，否则会导致无限循环。

## ⏸️ `break`与`next`语句

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_18.png)

`break`和`next`是控制循环流程的两个重要语句。

*   **`break`**：立即终止当前正在运行的最内层循环。
    ```r
    for (i in 1:10) {
      if (i %% 2 == 0) break # 当i为偶数时，终止整个循环
      cat(i, " ")
    }
    # 输出: 1
    ```

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_20.png)

*   **`next`**：跳过当前迭代中剩余的代码，直接进入循环的下一次迭代。
    ```r
    for (i in 1:10) {
      if (i %% 2 == 0) next # 当i为偶数时，跳过本次迭代
      cat(i, " ")
    }
    # 输出: 1 3 5 7 9
    ```

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_22.png)

## 🔢 `seq_along`与`seq_len`函数

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_24.png)

在创建循环索引时，`seq_along()`和`seq_len()`函数非常有用。它们能安全地生成序列，特别是在处理长度可能为0的向量时。

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_26.png)

以下是它们的用法：
```r
L <- list(c(1,2,3), c("a","b","c"), c(TRUE, FALSE))
# 使用 seq_along 安全地生成索引
for (i in seq_along(L)) {
  print(length(L[[i]]))
}
```
`seq_along(x)`会生成一个从1到`length(x)`的序列。`seq_len(n)`会生成一个从1到`n`的序列。

**关键区别**在于当向量长度为0时：
```r
L <- list() # 空列表，长度为0
# 以下方法会出错
for (i in 1:length(L)) { # 相当于 1:0
  print(L[[i]]) # 尝试访问不存在的元素
}
# 以下方法是安全的，循环不会执行，也不会报错
for (i in seq_along(L)) { # 生成一个空序列
  print(L[[i]])
}
```
因此，推荐使用`seq_along()`或`seq_len()`来生成循环索引。

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_28.png)

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_29.png)

## ⚡ 向量化：循环的替代方案

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_31.png)

在R中，循环通常较慢。尽可能地将操作向量化是提升代码性能的关键。向量化意味着直接对整个向量或矩阵进行操作，而不是使用循环逐个元素处理。

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_33.png)

考虑一个分段函数：
```r
# 非向量化版本，只能处理单个值
f <- function(x) {
  if (x <= 0) {
    return(-x^3)
  } else if (x <= 1) {
    return(x^2)
  } else {
    return(sqrt(x))
  }
}
# 对向量使用此函数会报错
x <- seq(-2, 2, by=0.01)
# y <- f(x) # 错误！
```

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_35.png)

为了对向量使用这个函数，你可能会写一个循环：
```r
plot_values <- numeric(length(x))
for (i in seq_along(x)) {
  plot_values[i] <- f(x[i])
}
```

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_37.png)

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_38.png)

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_40.png)

然而，更高效的方法是使用向量化的`ifelse()`函数重写函数：
```r
f_vectorized <- function(x) {
  ifelse(x <= 0, -x^3,
         ifelse(x <= 1, x^2,
                sqrt(x)))
}
plot_values <- f_vectorized(x) # 直接对整个向量操作，无需循环
```
`ifelse(test, yes, no)`会向量化地评估`test`条件，并从`yes`或`no`中选取对应的值组成结果向量。

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_42.png)

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_44.png)

## 🚀 利用内置的向量化函数

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_46.png)

R提供了许多高度优化的向量化函数，应优先使用它们。

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_48.png)

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_49.png)

例如，计算一个大矩阵每行的平均值：
```r
set.seed(123)
X <- matrix(rnorm(1e6 * 100), nrow=1e6, ncol=100)

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_50.png)

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_52.png)

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_53.png)

# 方法1: 循环（慢）
system.time({
  row_means_loop <- numeric(nrow(X))
  for (i in 1:nrow(X)) {
    row_means_loop[i] <- mean(X[i, ])
  }
})

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_55.png)

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_57.png)

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_59.png)

# 方法2: 使用apply函数（较慢）
system.time({
  row_means_apply <- apply(X, 1, mean)
})

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_61.png)

# 方法3: 使用向量化的rowSums函数（最快！）
system.time({
  row_means_fast <- rowSums(X) / ncol(X)
})

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_63.png)

# 验证结果相同
all.equal(row_means_loop, row_means_apply, row_means_fast)
```
在这个例子中，`rowSums()`配合除法比循环或`apply()`快几个数量级。对于列操作，也有对应的`colSums()`、`rowMeans()`和`colMeans()`函数。

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_65.png)

## 📚 总结

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_67.png)

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_68.png)

本节课中我们一起学习了R语言中的循环结构。我们掌握了如何使用`for`、`while`和`repeat`循环来重复执行代码。我们了解了高效存储循环结果的策略，特别是预先分配空间的重要性。我们还学习了使用`break`和`next`来控制循环流程，以及使用`seq_along()`和`seq_len()`来安全地创建循环索引。

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_70.png)

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_72.png)

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_73.png)

![](img/c5091fb94e7f51f6cd3e9d78d1c27e9b_74.png)

最重要的是，我们认识到在R中，**向量化操作通常是比显式循环更高效的选择**。我们学习了如何利用`ifelse()`函数和内置的向量化函数（如`rowSums`）来重写代码，从而大幅提升计算性能。记住Donald Knuth的忠告：避免不成熟的优化，但在那关键的3%情况下，不要放弃利用向量化提升效率的机会。