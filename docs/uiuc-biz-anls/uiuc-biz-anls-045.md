#  045：使用可视化探索数据框 📊

![](img/281ad111663c5d8e424ed29677e30c14_1.png)

![](img/281ad111663c5d8e424ed29677e30c14_3.png)

![](img/281ad111663c5d8e424ed29677e30c14_4.png)

在本节课中，我们将学习如何使用 Pandas 的 `plot` 方法快速创建探索性数据可视化图表。探索性可视化旨在帮助我们快速理解数据分布和关系，而无需过多修饰图表细节。

数据可视化通常分为两类：探索性和解释性。探索性可视化是为了快速探索数据而创建的，通常不精修坐标轴、标签或标题等细节。解释性可视化则用于向他人总结和传达关键发现，因此会精心设计字体、配色和标题等元素。本节课我们将专注于探索性可视化。

![](img/281ad111663c5d8e424ed29677e30c14_6.png)

![](img/281ad111663c5d8e424ed29677e30c14_7.png)

![](img/281ad111663c5d8e424ed29677e30c14_8.png)

## 导入数据与准备工作

![](img/281ad111663c5d8e424ed29677e30c14_10.png)

![](img/281ad111663c5d8e424ed29677e30c14_11.png)

![](img/281ad111663c5d8e424ed29677e30c14_13.png)

![](img/281ad111663c5d8e424ed29677e30c14_15.png)

首先，我们需要导入必要的库并加载数据。以下是具体步骤。

![](img/281ad111663c5d8e424ed29677e30c14_17.png)

![](img/281ad111663c5d8e424ed29677e30c14_18.png)

![](img/281ad111663c5d8e424ed29677e30c14_19.png)

![](img/281ad111663c5d8e424ed29677e30c14_20.png)

```python
import pandas as pd

![](img/281ad111663c5d8e424ed29677e30c14_21.png)

# 读取数据
df = pd.read_pickle('salary_sur_21.xz')
# 查看前五行数据
df.head()
```

![](img/281ad111663c5d8e424ed29677e30c14_23.png)

![](img/281ad111663c5d8e424ed29677e30c14_24.png)

以上代码导入了 Pandas 库，读取了一个名为 `salary_sur_21.xz` 的 pickle 文件（这是一个关于薪资的调查数据），并将其存储在 DataFrame `df` 中。使用 `head()` 方法可以快速查看数据的前几行，了解数据结构，例如包含“年薪”、“年龄范围”、“行业”等列。

## 数值型数据的单变量分析 📈

上一节我们导入了数据，本节中我们来看看如何为数值型列创建单变量图表。我们将重点关注“年薪”这一列。

创建图表的核心是使用 DataFrame 的 `plot` 方法。例如，`df[‘annual_salary’].plot.hist()` 可以生成直方图。

以下是几种常用的单变量图表及其创建方法：

![](img/281ad111663c5d8e424ed29677e30c14_26.png)

![](img/281ad111663c5d8e424ed29677e30c14_28.png)

*   **直方图**：用于展示数值数据的分布情况，显示观测值落入特定区间的次数。
    ```python
    # 基础直方图
    df['annual_salary'].plot.hist()
    # 过滤异常值并增加箱数
    df.query('annual_salary < 1e6')['annual_salary'].plot.hist(bins=50, title='Histogram of Annual Salary')
    ```
*   **密度图**：是直方图的平滑版本，能更清晰地显示数据分布的形状。
    ```python
    df.query('annual_salary < 1e6')['annual_salary'].plot.density()
    ```
*   **箱线图**：展示数据的五数概括（最小值、第一四分位数、中位数、第三四分位数、最大值）和异常值。
    ```python
    # 整体数据的箱线图
    df['annual_salary'].plot.box()
    # 按年龄组分组的箱线图，便于比较
    df.boxplot(column='annual_salary', by='age_range')
    ```

![](img/281ad111663c5d8e424ed29677e30c14_30.png)

## 分类型数据的可视化 📊

![](img/281ad111663c5d8e424ed29677e30c14_32.png)

![](img/281ad111663c5d8e424ed29677e30c14_33.png)

![](img/281ad111663c5d8e424ed29677e30c14_34.png)

![](img/281ad111663c5d8e424ed29677e30c14_36.png)

了解完数值型数据，我们转向分类型数据，例如“年龄范围”和“行业”。对于这类数据，我们通常关心每个类别出现的频率。

创建分类数据图表前，常使用 `value_counts()` 方法进行汇总。以下是几种可视化方法：

![](img/281ad111663c5d8e424ed29677e30c14_38.png)

![](img/281ad111663c5d8e424ed29677e30c14_40.png)

*   **垂直条形图**：直观比较各类别的计数。
    ```python
    df['age_range'].value_counts().plot.bar()
    ```
*   **水平条形图**：当类别名称较长时，水平条形图能提供更好的标签显示空间。
    ```python
    df['industry'].value_counts().head(7).plot.barh()
    ```
*   **饼图**：展示各类别在总体中所占的比例。
    ```python
    df['industry'].value_counts().head(5).plot.pie()
    ```

![](img/281ad111663c5d8e424ed29677e30c14_42.png)

![](img/281ad111663c5d8e424ed29677e30c14_44.png)

![](img/281ad111663c5d8e424ed29677e30c14_45.png)

## 时间序列与关系分析 🔗

最后，我们看看如何分析数据随时间的变化趋势以及两个数值变量之间的关系。

![](img/281ad111663c5d8e424ed29677e30c14_47.png)

*   **折线图与面积图**：用于展示数据随时间变化的趋势。
    ```python
    # 折线图
    df.query('annual_salary < 1e6').plot.line(x='timestamp', y='annual_salary')
    # 面积图
    df.query('annual_salary < 1e6').plot.area(x='timestamp', y='annual_salary')
    ```
*   **散点图与六边形分箱图**：用于探索两个数值变量之间的关联。当数据点过多重叠时，六边形分箱图是更好的选择。
    ```python
    # 散点图
    df.query('annual_salary < 1e6').plot.scatter(x='annual_salary', y='bonus')
    # 六边形分箱图
    df.query('annual_salary < 2e5').plot.hexbin(x='annual_salary', y='bonus', gridsize=20)
    ```

![](img/281ad111663c5d8e424ed29677e30c14_48.png)

![](img/281ad111663c5d8e424ed29677e30c14_50.png)

## 总结

![](img/281ad111663c5d8e424ed29677e30c14_51.png)

![](img/281ad111663c5d8e424ed29677e30c14_53.png)

![](img/281ad111663c5d8e424ed29677e30c14_54.png)

本节课中，我们一起学习了使用 Pandas 快速生成探索性数据可视化的多种方法。我们涵盖了针对数值型数据的直方图、密度图和箱线图；针对分类型数据的条形图和饼图；以及用于分析趋势和关系的折线图、散点图和六边形分箱图。掌握这些快速可视化的技能，是理解数据、发现模式、指导后续深入分析的关键步骤。虽然还有其他专门的绘图库（如 Matplotlib, Seaborn）可以创建更精美的解释性图表，但 Pandas 内置的 `plot` 方法为数据探索提供了一个极其高效和便捷的起点。