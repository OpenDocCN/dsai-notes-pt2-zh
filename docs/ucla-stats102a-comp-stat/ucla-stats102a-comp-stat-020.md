# 20：dplyr - select, filter, mutate 🛠️

![](img/52b5c2834ed0e35c48082d7333ad79da_1.png)

在本节课中，我们将学习 `tidyverse` 生态系统中一个非常重要的包——`dplyr`。`dplyr` 提供了强大的数据操作功能，通过一系列简洁的“动词”来帮助我们高效地处理数据。我们将重点介绍 `select`、`filter` 和 `mutate` 这三个核心函数。

## 概述

![](img/52b5c2834ed0e35c48082d7333ad79da_3.png)

`dplyr` 是 `tidyverse` 的核心包之一，它将复杂的数据操作任务简化为几个基本的“动词”。这种设计约束了选择，但有助于我们以更清晰、更模块化的方式思考数据处理流程。数据处理通常包括：确定任务、用程序描述任务、执行程序。`dplyr` 让这些步骤变得快速而简单。

![](img/52b5c2834ed0e35c48082d7333ad79da_5.png)

## 核心动词简介

`dplyr` 提供了多个用于数据操作的动词，其中最重要的几个是：
*   **`select`**: 用于选择数据框中的列（变量）。
*   **`filter`**: 用于根据条件筛选数据框中的行（观测）。
*   **`mutate`**: 用于创建新的列（变量）或修改现有列。
*   **`arrange`**: 用于改变行的排序顺序。
*   **`summarize`**: 用于计算汇总统计量，将多个值聚合成单个值（如计算均值）。

这些动词通常可以与 `group_by` 结合使用，以便对分组后的数据执行操作。

![](img/52b5c2834ed0e35c48082d7333ad79da_7.png)

![](img/52b5c2834ed0e35c48082d7333ad79da_9.png)

## 管道操作符 `%>%`

在深入学习具体函数前，我们需要了解管道操作符 `%>%`。它的作用是将左侧表达式的结果作为第一个参数传递给右侧的函数。

**代码示例**:
```r
# 传统写法
select(starwars, name, homeworld, species, films)

# 使用管道的写法
starwars %>% select(name, homeworld, species, films)
```
管道语法允许我们将多个操作步骤串联起来，使代码更易读，逻辑更清晰。R 基础版本也引入了原生管道操作符 `|>`，功能类似。

![](img/52b5c2834ed0e35c48082d7333ad79da_11.png)

![](img/52b5c2834ed0e35c48082d7333ad79da_12.png)

## 选择列：`select` 函数

`select` 函数用于从数据框中选择特定的列。

![](img/52b5c2834ed0e35c48082d7333ad79da_14.png)

### 基本选择

可以直接指定列名来选择它们。

**代码示例**:
```r
starwars %>% select(name, homeworld, species, films)
```

![](img/52b5c2834ed0e35c48082d7333ad79da_16.png)

### 排除列

在列名前加负号 `-` 可以排除这些列。

![](img/52b5c2834ed0e35c48082d7333ad79da_18.png)

![](img/52b5c2834ed0e35c48082d7333ad79da_19.png)

**代码示例**:
```r
starwars %>% select(-name, -eye_color, -birth_year) %>% head(3)
```

![](img/52b5c2834ed0e35c48082d7333ad79da_21.png)

### 选择列范围

可以使用 `:` 操作符选择连续的列。

![](img/52b5c2834ed0e35c48082d7333ad79da_23.png)

**代码示例**:
```r
starwars %>% select(name:eye_color)
```

### 使用辅助函数

`select` 提供了一些辅助函数，可以基于列名的模式进行选择。
*   `contains(“string”)`: 选择包含指定字符串的列。
*   `starts_with(“prefix”)`: 选择以指定前缀开头的列。
*   `ends_with(“suffix”)`: 选择以指定后缀结尾的列。
*   `matches(“regex”)`: 选择匹配正则表达式的列。

**代码示例**:
```r
# 选择以 “color” 结尾的列和 name 列
starwars %>% select(name, ends_with(“color”))

![](img/52b5c2834ed0e35c48082d7333ad79da_25.png)

![](img/52b5c2834ed0e35c48082d7333ad79da_26.png)

# 选择列名以 “s” 结尾的列
starwars %>% select(matches(“s$”))
```

### 使用变量选择列

![](img/52b5c2834ed0e35c48082d7333ad79da_28.png)

有时需要选择的列名存储在一个向量中，这时可以使用 `all_of()` 或 `any_of()` 函数。

**代码示例**:
```r
vars_to_select <- c(“name”, “mass”, “height”)
starwars %>% select(all_of(vars_to_select))
```

![](img/52b5c2834ed0e35c48082d7333ad79da_30.png)

## 筛选行：`filter` 函数

`filter` 函数用于根据逻辑条件筛选数据框的行。

### 基本筛选

![](img/52b5c2834ed0e35c48082d7333ad79da_32.png)

提供一个逻辑向量（条件），`filter` 会返回条件为 `TRUE` 的行。

![](img/52b5c2834ed0e35c48082d7333ad79da_34.png)

![](img/52b5c2834ed0e35c48082d7333ad79da_36.png)

**代码示例**:
```r
# 筛选出名为 “R2-D2” 的行
starwars %>% filter(name == “R2-D2”)
```

### 多条件筛选

可以使用逻辑运算符 `&` (AND) 和 `|` (OR) 组合多个条件。

![](img/52b5c2834ed0e35c48082d7333ad79da_38.png)

**代码示例**:
```r
# 筛选物种为 “Human” 或 “Droid” 的行
starwars %>% filter(species %in% c(“Human”, “Droid”))

![](img/52b5c2834ed0e35c48082d7333ad79da_40.png)

# 筛选身高小于 175 的行
starwars %>% filter(height < 175)
```

**注意**：判断一个值是否在一组值中时，应使用 `%in%` 运算符，而不是 `==`。

### 结合字符串检测

![](img/52b5c2834ed0e35c48082d7333ad79da_42.png)

`filter` 可以与 `stringr::str_detect()` 等函数结合，使用正则表达式进行更复杂的字符串匹配筛选。

![](img/52b5c2834ed0e35c48082d7333ad79da_44.png)

**代码示例**:
```r
# 筛选名字以大写 “F” 开头的行
starwars %>% filter(str_detect(name, “^F”))
```

### 组合 `filter` 与 `select`

可以链式使用 `filter` 和 `select` 来先筛选行，再选择列。

**代码示例**:
```r
starwars %>%
  filter(hair_color == “none” | eye_color == “black”) %>%
  select(name, species, homeworld, hair_color, eye_color)
```

## 创建新列：`mutate` 函数

![](img/52b5c2834ed0e35c48082d7333ad79da_46.png)

![](img/52b5c2834ed0e35c48082d7333ad79da_47.png)

`mutate` 函数用于创建新的列或修改现有的列。

### 基本创建

![](img/52b5c2834ed0e35c48082d7333ad79da_49.png)

新列的计算结果会自动添加到数据框的末尾。

**代码示例**:
```r
# 将身高从厘米转换为英寸
starwars %>%
  mutate(height_inches = height / 2.54) %>%
  select(name, height, height_inches) %>%
  head(1)
```

### 使用向量化函数

![](img/52b5c2834ed0e35c48082d7333ad79da_51.png)

`mutate` 中可以使用各种向量化函数。重要的是，新创建的列必须与数据框的行数相同。

**代码示例**:
```r
starwars %>%
  select(name, mass, birth_year) %>%
  mutate(
    cummin_mass = cummin(mass), # 累积最小值
    mass_ratio = mass / mean(mass, na.rm = TRUE), # 与平均值的比值
    pmin_value = pmin(mass, birth_year), # 逐元素最小值
    lag_mass = lag(mass, 2) # 将 mass 列的值向下偏移两位
  )
```

**注意**：像 `cummin`（累积最小值）、`cumsum`（累积和）这类函数在处理时间序列数据时更有意义。`lead` 和 `lag` 函数则用于获取向前或向后偏移的值。

## 其他实用函数

![](img/52b5c2834ed0e35c48082d7333ad79da_53.png)

### 排序行：`arrange`

![](img/52b5c2834ed0e35c48082d7333ad79da_55.png)

`arrange` 函数用于对数据框的行进行排序。

**代码示例**:
```r
starwars %>%
  select(name, birth_year, height, mass) %>%
  arrange(desc(birth_year), mass)
```

### 按位置选择行：`slice`

`slice` 系列函数用于按行的位置进行选择。
*   `slice(5:10)`: 选择第5到第10行。
*   `slice_sample(n = 5)`: 随机抽取5行。这在检查数据或抽样时非常有用。
*   `slice_max(mass, n = 3)`: 选择 `mass` 最大的3行。
*   `slice_min(mass, n = 3)`: 选择 `mass` 最小的3行。

**代码示例**:
```r
# 随机查看5行数据
starwars %>% slice_sample(n = 5)
```

## 总结

本节课我们一起学习了 `dplyr` 包中三个核心的数据操作函数：`select`、`filter` 和 `mutate`。
*   `select` 用于灵活地选择数据列。
*   `filter` 用于根据条件筛选数据行。
*   `mutate` 用于创建或转换数据列。

![](img/52b5c2834ed0e35c48082d7333ad79da_57.png)

我们还介绍了管道操作符 `%>%`，它可以将这些函数优雅地串联起来，形成清晰的数据处理流程。此外，我们简要了解了 `arrange` 和 `slice` 等辅助函数。掌握这些“动词”是进行高效数据整理和分析的基础。建议下载 `dplyr` 速查表以便随时查阅。