# 9：多列分组与数据合并 📊

![](img/f532cbc584857ebf382829c6dc53f06a_0.png)

![](img/f532cbc584857ebf382829c6dc53f06a_2.png)

![](img/f532cbc584857ebf382829c6dc53f06a_3.png)

![](img/f532cbc584857ebf382829c6dc53f06a_5.png)

在本节课中，我们将学习两种更高级的数据框操作技术：基于多列进行分组以及合并不同的数据框。我们将继续使用上节课的学生名册数据，并引入新的数据集来练习这些技巧。

![](img/f532cbc584857ebf382829c6dc53f06a_7.png)

![](img/f532cbc584857ebf382829c6dc53f06a_9.png)

![](img/f532cbc584857ebf382829c6dc53f06a_11.png)

![](img/f532cbc584857ebf382829c6dc53f06a_12.png)

---

![](img/f532cbc584857ebf382829c6dc53f06a_14.png)

![](img/f532cbc584857ebf382829c6dc53f06a_16.png)

![](img/f532cbc584857ebf382829c6dc53f06a_18.png)

![](img/f532cbc584857ebf382829c6dc53f06a_20.png)

![](img/f532cbc584857ebf382829c6dc53f06a_21.png)

![](img/f532cbc584857ebf382829c6dc53f06a_23.png)

## 回顾：提取名字与单列分组

![](img/f532cbc584857ebf382829c6dc53f06a_25.png)

![](img/f532cbc584857ebf382829c6dc53f06a_27.png)

上一节我们介绍了如何从全名中提取名字，并使用`groupby`进行单列分组。让我们快速回顾一下。

我们首先定义了一个函数来提取单个全名中的名字：

![](img/f532cbc584857ebf382829c6dc53f06a_29.png)

![](img/f532cbc584857ebf382829c6dc53f06a_31.png)

![](img/f532cbc584857ebf382829c6dc53f06a_32.png)

![](img/f532cbc584857ebf382829c6dc53f06a_34.png)

![](img/f532cbc584857ebf382829c6dc53f06a_36.png)

```python
def first_name(full_name):
    return full_name.split()[0]
```

![](img/f532cbc584857ebf382829c6dc53f06a_38.png)

![](img/f532cbc584857ebf382829c6dc53f06a_39.png)

![](img/f532cbc584857ebf382829c6dc53f06a_41.png)

![](img/f532cbc584857ebf382829c6dc53f06a_43.png)

然后，我们将这个函数应用到数据框的`name`列，为每个人创建了一个新的`first`名字列：

![](img/f532cbc584857ebf382829c6dc53f06a_45.png)

![](img/f532cbc584857ebf382829c6dc53f06a_46.png)

![](img/f532cbc584857ebf382829c6dc53f06a_48.png)

```python
roster['first'] = roster.get('name').apply(first_name)
```

![](img/f532cbc584857ebf382829c6dc53f06a_50.png)

![](img/f532cbc584857ebf382829c6dc53f06a_52.png)

![](img/f532cbc584857ebf382829c6dc53f06a_54.png)

接着，我们按`first`名字列分组，并统计了每个名字出现的次数，以找出最常见的名字：

![](img/f532cbc584857ebf382829c6dc53f06a_56.png)

![](img/f532cbc584857ebf382829c6dc53f06a_58.png)

![](img/f532cbc584857ebf382829c6dc53f06a_60.png)

![](img/f532cbc584857ebf382829c6dc53f06a_62.png)

![](img/f532cbc584857ebf382829c6dc53f06a_64.png)

```python
name_counts = roster.groupby('first').count()
name_counts_sorted = name_counts.sort_values('name', ascending=False)
```

![](img/f532cbc584857ebf382829c6dc53f06a_66.png)

![](img/f532cbc584857ebf382829c6dc53f06a_68.png)

我们发现“Ryan”是最常见的名字，共有9个。如果我们想进一步了解这9个Ryan是如何分布在各个讲座部分的，我们可以先筛选出所有Ryan，然后按`section`分组计数。

![](img/f532cbc584857ebf382829c6dc53f06a_70.png)

![](img/f532cbc584857ebf382829c6dc53f06a_72.png)

---

![](img/f532cbc584857ebf382829c6dc53f06a_74.png)

![](img/f532cbc584857ebf382829c6dc53f06a_76.png)

## 多列分组 🔄

![](img/f532cbc584857ebf382829c6dc53f06a_78.png)

![](img/f532cbc584857ebf382829c6dc53f06a_80.png)

![](img/f532cbc584857ebf382829c6dc53f06a_82.png)

但是，如果我们想一次性了解**所有**名字在各个部分的分布情况呢？例如，对于每一个名字，有多少人在9AM部分，多少人在10AM部分？

![](img/f532cbc584857ebf382829c6dc53f06a_84.png)

![](img/f532cbc584857ebf382829c6dc53f06a_85.png)

![](img/f532cbc584857ebf382829c6dc53f06a_86.png)

![](img/f532cbc584857ebf382829c6dc53f06a_87.png)

目前的方法无法直接回答这个问题。单按`first`名字分组，会把所有同名的人放在一起，但不会区分他们来自哪个部分。单按`section`分组，则不会区分组内的名字是否相同。

![](img/f532cbc584857ebf382829c6dc53f06a_89.png)

![](img/f532cbc584857ebf382829c6dc53f06a_91.png)

![](img/f532cbc584857ebf382829c6dc53f06a_93.png)

![](img/f532cbc584857ebf382829c6dc53f06a_94.png)

解决方案是：**基于多列进行分组**。我们希望分组依据是`first`名字和`section`部分的组合。例如，所有在10AM部分的“Ryan”属于一组，所有在1PM部分的“Ryan”属于另一组。

以下是具体语法。我们向`groupby`方法传入一个**列名列表**，而不是单个列名：

![](img/f532cbc584857ebf382829c6dc53f06a_96.png)

![](img/f532cbc584857ebf382829c6dc53f06a_97.png)

![](img/f532cbc584857ebf382829c6dc53f06a_99.png)

![](img/f532cbc584857ebf382829c6dc53f06a_100.png)

![](img/f532cbc584857ebf382829c6dc53f06a_102.png)

![](img/f532cbc584857ebf382829c6dc53f06a_104.png)

![](img/f532cbc584857ebf382829c6dc53f06a_106.png)

```python
counts = roster.groupby(['section', 'first']).count()
```

![](img/f532cbc584857ebf382829c6dc53f06a_108.png)

![](img/f532cbc584857ebf382829c6dc53f06a_109.png)

![](img/f532cbc584857ebf382829c6dc53f06a_111.png)

![](img/f532cbc584857ebf382829c6dc53f06a_112.png)

这行代码的意思是：首先按`section`分组，然后在每个`section`组内，再按`first`名字进行子分组。对于每个`(section, first)`组合，它会统计有多少行数据（即多少名学生）。

![](img/f532cbc584857ebf382829c6dc53f06a_114.png)

执行后，结果数据框的索引会变成由`section`和`first`两列组成的**多重索引**。为了便于处理，我们通常使用`.reset_index()`将其恢复为普通列：

```python
counts_reset = counts.reset_index()
```

![](img/f532cbc584857ebf382829c6dc53f06a_116.png)

![](img/f532cbc584857ebf382829c6dc53f06a_118.png)

![](img/f532cbc584857ebf382829c6dc53f06a_120.png)

![](img/f532cbc584857ebf382829c6dc53f06a_121.png)

**关于分组顺序**：分组`['section', 'first']`与分组`['first', 'section']`在逻辑上是等价的，都会创建相同的分组集合（即所有`(section, first)`组合）。区别在于结果数据框中行和列的显示顺序会不同。前者先按`section`排序，后者先按`first`名字排序。

![](img/f532cbc584857ebf382829c6dc53f06a_123.png)

![](img/f532cbc584857ebf382829c6dc53f06a_125.png)

![](img/f532cbc584857ebf382829c6dc53f06a_126.png)

---

![](img/f532cbc584857ebf382829c6dc53f06a_128.png)

![](img/f532cbc584857ebf382829c6dc53f06a_130.png)

![](img/f532cbc584857ebf382829c6dc53f06a_132.png)

![](img/f532cbc584857ebf382829c6dc53f06a_134.png)

![](img/f532cbc584857ebf382829c6dc53f06a_136.png)

### 练习：找出拥有最多Kevin的部分

![](img/f532cbc584857ebf382829c6dc53f06a_138.png)

![](img/f532cbc584857ebf382829c6dc53f06a_140.png)

假设我们已经有了按`section`和`first`分组计数的数据框`counts`，目标是找出哪个讲座部分拥有最多的“Kevin”。

![](img/f532cbc584857ebf382829c6dc53f06a_142.png)

![](img/f532cbc584857ebf382829c6dc53f06a_144.png)

![](img/f532cbc584857ebf382829c6dc53f06a_146.png)

以下是解决步骤：
1.  从`counts`中筛选出`first`名字为“Kevin”的行。
2.  按计数列（通常是`name`）降序排列。
3.  取排序后第一行的`section`值。

![](img/f532cbc584857ebf382829c6dc53f06a_148.png)

![](img/f532cbc584857ebf382829c6dc53f06a_150.png)

```python
# 步骤1：筛选
kevin_rows = counts[counts.get('first') == 'Kevin']
# 步骤2：排序
kevin_sorted = kevin_rows.sort_values('name', ascending=False)
# 步骤3：获取结果
section_with_most_kevins = kevin_sorted.get('section').iloc[0]
```

![](img/f532cbc584857ebf382829c6dc53f06a_152.png)

![](img/f532cbc584857ebf382829c6dc53f06a_154.png)

![](img/f532cbc584857ebf382829c6dc53f06a_156.png)

![](img/f532cbc584857ebf382829c6dc53f06a_157.png)

![](img/f532cbc584857ebf382829c6dc53f06a_159.png)

---

![](img/f532cbc584857ebf382829c6dc53f06a_161.png)

![](img/f532cbc584857ebf382829c6dc53f06a_162.png)

![](img/f532cbc584857ebf382829c6dc53f06a_164.png)

![](img/f532cbc584857ebf382829c6dc53f06a_166.png)

![](img/f532cbc584857ebf382829c6dc53f06a_168.png)

![](img/f532cbc584857ebf382829c6dc53f06a_170.png)

## 应用：海洋温度数据分析 🌡️

![](img/f532cbc584857ebf382829c6dc53f06a_172.png)

![](img/f532cbc584857ebf382829c6dc53f06a_174.png)

![](img/f532cbc584857ebf382829c6dc53f06a_176.png)

现在，让我们将多列分组技术应用到一个新的数据集：拉霍亚斯克里普斯码头自1916年至今的每日海面温度数据。

![](img/f532cbc584857ebf382829c6dc53f06a_178.png)

![](img/f532cbc584857ebf382829c6dc53f06a_179.png)

![](img/f532cbc584857ebf382829c6dc53f06a_181.png)

![](img/f532cbc584857ebf382829c6dc53f06a_183.png)

数据框`ct`包含以下列：`year`（年）、`month`（月）、`day`（日）、`surface_temp`（海面温度，摄氏度）。

![](img/f532cbc584857ebf382829c6dc53f06a_185.png)

![](img/f532cbc584857ebf382829c6dc53f06a_187.png)

![](img/f532cbc584857ebf382829c6dc53f06a_188.png)

**问题**：如何找出平均海面温度最高的**单个月份**（例如“1998年11月”）？

![](img/f532cbc584857ebf382829c6dc53f06a_190.png)

![](img/f532cbc584857ebf382829c6dc53f06a_191.png)

我们需要将所有属于同一年、同一月的日期数据分组，然后计算该组内`surface_temp`的平均值。因此，正确的分组依据是`['year', 'month']`。

![](img/f532cbc584857ebf382829c6dc53f06a_193.png)

![](img/f532cbc584857ebf382829c6dc53f06a_195.png)

![](img/f532cbc584857ebf382829c6dc53f06a_197.png)

```python
monthly_avg_temp = ct.groupby(['year', 'month']).mean()
```

![](img/f532cbc584857ebf382829c6dc53f06a_199.png)

![](img/f532cbc584857ebf382829c6dc53f06a_201.png)

![](img/f532cbc584857ebf382829c6dc53f06a_202.png)

分组后，`surface_temp`列的值就是每个年月组合的平均温度。我们可以据此进行排序，找到温度最高的月份。

![](img/f532cbc584857ebf382829c6dc53f06a_204.png)

![](img/f532cbc584857ebf382829c6dc53f06a_206.png)

**重要提示**：在解释此类数据时，务必注意数据的完整性。例如，如果数据集只更新到某年6月，那么该年的年平均温度仅基于上半年（较冷月份）的数据，不能代表全年情况，在分析趋势时需要谨慎。

![](img/f532cbc584857ebf382829c6dc53f06a_208.png)

![](img/f532cbc584857ebf382829c6dc53f06a_210.png)

![](img/f532cbc584857ebf382829c6dc53f06a_212.png)

---

![](img/f532cbc584857ebf382829c6dc53f06a_214.png)

![](img/f532cbc584857ebf382829c6dc53f06a_216.png)

![](img/f532cbc584857ebf382829c6dc53f06a_218.png)

![](img/f532cbc584857ebf382829c6dc53f06a_220.png)

## 数据合并 (Merging) 🤝

![](img/f532cbc584857ebf382829c6dc53f06a_222.png)

![](img/f532cbc584857ebf382829c6dc53f06a_224.png)

接下来，我们学习第二种关键技术：**合并**。当我们需要的信息分散在多个数据框中时，合并操作可以将它们组合起来。

![](img/f532cbc584857ebf382829c6dc53f06a_226.png)

![](img/f532cbc584857ebf382829c6dc53f06a_228.png)

![](img/f532cbc584857ebf382829c6dc53f06a_230.png)

考虑以下场景：你有一些旧衣服想要转卖。一家二手店根据衣物类型提供不同的回收价格比例。你有一个数据框`offer_pct`列出了每种`clothing_type`（衣物类型）对应的`offer_percentage`（回收比例）。你还有另一个数据框`clothes`，列出了你拥有的每件`item`（物品）及其`retail_price`（原价）。

![](img/f532cbc584857ebf382829c6dc53f06a_232.png)

![](img/f532cbc584857ebf382829c6dc53f06a_234.png)

![](img/f532cbc584857ebf382829c6dc53f06a_236.png)

**问题**：如果你卖掉所有衣服，能赚多少钱？

![](img/f532cbc584857ebf382829c6dc53f06a_238.png)

![](img/f532cbc584857ebf382829c6dc53f06a_240.png)

![](img/f532cbc584857ebf382829c6dc53f06a_242.png)

![](img/f532cbc584857ebf382829c6dc53f06a_243.png)

要回答这个问题，需要将两个数据框的信息结合起来：对于你拥有的每件衣服，找到其类型对应的回收比例，然后用原价乘以这个比例。

![](img/f532cbc584857ebf382829c6dc53f06a_244.png)

![](img/f532cbc584857ebf382829c6dc53f06a_246.png)

![](img/f532cbc584857ebf382829c6dc53f06a_248.png)

我们使用`merge`方法进行合并。基本语法是：

![](img/f532cbc584857ebf382829c6dc53f06a_250.png)

![](img/f532cbc584857ebf382829c6dc53f06a_251.png)

![](img/f532cbc584857ebf382829c6dc53f06a_253.png)

```python
merged_df = left_df.merge(right_df, left_on='left_column_name', right_on='right_column_name')
```

![](img/f532cbc584857ebf382829c6dc53f06a_255.png)

![](img/f532cbc584857ebf382829c6dc53f06a_257.png)

在我们的例子中：
- `left_df` 是 `offer_pct`
- `right_df` 是 `clothes`
- 用于匹配的列：`left_df`中的`clothing_type`和`right_df`中的`item`

```python
combined = offer_pct.merge(clothes, left_on='clothing_type', right_on='item')
```

![](img/f532cbc584857ebf382829c6dc53f06a_259.png)

![](img/f532cbc584857ebf382829c6dc53f06a_260.png)

![](img/f532cbc584857ebf382829c6dc53f06a_261.png)

合并过程如下：
1.  从左数据框(`offer_pct`)的第一行开始。
2.  查看其`clothing_type`的值（例如“shirt”）。
3.  在右数据框(`clothes`)的`item`列中寻找相同的值（“shirt”）。
4.  如果找到匹配项，就将左右两行的所有列组合成一个新行。
5.  如果左表的一行在右表找到多个匹配（例如“shoes”对应两双鞋），则会为每个匹配创建一行。
6.  如果左表的一行在右表没有匹配（例如“shorts”，但你没有短裤），则该行不会出现在结果中。

合并后，`combined`数据框包含了计算所需的所有信息：`offer_percentage`和`retail_price`在同一行。然后我们可以进行计算：

```python
# 将百分比转换为小数
earnings_series = (combined.get('offer_percentage') / 100) * combined.get('retail_price')
# 求和得到总收入
total_earnings = earnings_series.sum()
```

**关于合并顺序**：与分组类似，交换左右数据框的顺序（`clothes.merge(offer_pct, ...)`）会产生一个包含相同信息但行、列顺序可能不同的数据框。

![](img/f532cbc584857ebf382829c6dc53f06a_263.png)

![](img/f532cbc584857ebf382829c6dc53f06a_265.png)

---

![](img/f532cbc584857ebf382829c6dc53f06a_266.png)

![](img/f532cbc584857ebf382829c6dc53f06a_267.png)

![](img/f532cbc584857ebf382829c6dc53f06a_269.png)

![](img/f532cbc584857ebf382829c6dc53f06a_271.png)

![](img/f532cbc584857ebf382829c6dc53f06a_273.png)

![](img/f532cbc584857ebf382829c6dc53f06a_275.png)

### 练习：预测合并结果

![](img/f532cbc584857ebf382829c6dc53f06a_277.png)

![](img/f532cbc584857ebf382829c6dc53f06a_279.png)

![](img/f532cbc584857ebf382829c6dc53f06a_281.png)

理解合并操作的关键是能够预测结果的行数。这取决于两个数据框在匹配列上的值如何对应。

![](img/f532cbc584857ebf382829c6dc53f06a_283.png)

![](img/f532cbc584857ebf382829c6dc53f06a_285.png)

![](img/f532cbc584857ebf382829c6dc53f06a_287.png)

考虑两个数据框：
- `nice_weather_cities`: 包含`city`（城市）和`weather_score`（天气评分）。
- `schools`: 包含`school`（学校名）、`city`（城市）和`state`（州）。

![](img/f532cbc584857ebf382829c6dc53f06a_289.png)

![](img/f532cbc584857ebf382829c6dc53f06a_290.png)

![](img/f532cbc584857ebf382829c6dc53f06a_292.png)

![](img/f532cbc584857ebf382829c6dc53f06a_293.png)

**问题1**：如果按`city`列合并这两个数据框，结果会有多少行？
你需要检查左表的每个`city`值在右表的`city`列中出现了多少次。每次匹配都会产生一行。例如，如果左表的“San Diego”在右表出现了2次，那么它就会贡献2行。将所有城市的匹配行数相加即为总行数。

![](img/f532cbc584857ebf382829c6dc53f06a_295.png)

![](img/f532cbc584857ebf382829c6dc53f06a_297.png)

![](img/f532cbc584857ebf382829c6dc53f06a_299.png)

![](img/f532cbc584857ebf382829c6dc53f06a_300.png)

![](img/f532cbc584857ebf382829c6dc53f06a_302.png)

![](img/f532cbc584857ebf382829c6dc53f06a_304.png)

**问题2**：如果按`state`列合并呢？
原理相同，但现在是基于州进行匹配。左表的每个`state`值（如“CA”）会与右表中所有具有相同`state`值的行进行匹配并组合。

![](img/f532cbc584857ebf382829c6dc53f06a_306.png)

![](img/f532cbc584857ebf382829c6dc53f06a_307.png)

![](img/f532cbc584857ebf382829c6dc53f06a_309.png)

---

![](img/f532cbc584857ebf382829c6dc53f06a_310.png)

![](img/f532cbc584857ebf382829c6dc53f06a_311.png)

![](img/f532cbc584857ebf382829c6dc53f06a_313.png)

![](img/f532cbc584857ebf382829c6dc53f06a_314.png)

![](img/f532cbc584857ebf382829c6dc53f06a_316.png)

![](img/f532cbc584857ebf382829c6dc53f06a_318.png)

![](img/f532cbc584857ebf382829c6dc53f06a_320.png)

## 总结 📝

![](img/f532cbc584857ebf382829c6dc53f06a_322.png)

![](img/f532cbc584857ebf382829c6dc53f06a_324.png)

![](img/f532cbc584857ebf382829c6dc53f06a_326.png)

本节课我们一起学习了两个强大的数据框操作技术：

![](img/f532cbc584857ebf382829c6dc53f06a_328.png)

![](img/f532cbc584857ebf382829c6dc53f06a_330.png)

![](img/f532cbc584857ebf382829c6dc53f06a_332.png)

![](img/f532cbc584857ebf382829c6dc53f06a_334.png)

1.  **多列分组**：通过向`groupby()`传入列名列表，可以基于多个条件创建更精细的分组，从而进行更复杂的聚合分析，例如分析海面温度在不同年月的变化。
2.  **数据合并**：使用`merge()`方法，可以根据一个或多个共同列将来自不同数据框的信息连接起来，这对于组合相关数据集以进行综合分析至关重要，例如计算转卖衣物的总收益。

![](img/f532cbc584857ebf382829c6dc53f06a_336.png)

![](img/f532cbc584857ebf382829c6dc53f06a_338.png)

![](img/f532cbc584857ebf382829c6dc53f06a_339.png)

![](img/f532cbc584857ebf382829c6dc53f06a_341.png)

![](img/f532cbc584857ebf382829c6dc53f06a_342.png)

掌握这些技术将极大地增强你处理和分析复杂、多维度真实世界数据的能力。