#  052：清理数据框中的日期列 📅

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_0.png)

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_2.png)

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_4.png)

在本节课中，我们将学习如何处理Pandas数据框中的日期数据。日期是数据分析中常见且重要的一类数据，但由于其记录和报告格式的不一致性，处理起来可能颇具挑战。我们将介绍如何将字符串格式的日期转换为日期时间数据类型，如何提取日期特征，以及如何处理格式不一致的日期数据。

## 从字符串到日期时间

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_6.png)

上一节我们介绍了日期处理的重要性。本节中，我们来看看如何将数据框中的字符串列转换为日期时间数据类型。Pandas提供了一个非常实用的函数 `pd.to_datetime()`。

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_8.png)

以下是一个简单的数据框示例，其中包含三个日期列，它们目前都是字符串（对象）数据类型：

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_10.png)

```python
import pandas as pd

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_11.png)

# 示例数据框
df = pd.DataFrame({
    'date1': ['2025-04-03', '2026-07-14', '2027-01-01', '2032-08-09'],
    'date2': ['2025-04-03T12:00:00', '2026-07-14T23:59:59', '2027-01-01T00:00:00', '2032-08-09T03:15:24.325'],
    'date3': ['04/03/2027', '04-03-2027', '2027.04.03', '03/04/2027']
})
```

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_13.png)

`date1` 列中的值都采用 **ISO 8601** 格式（即 `YYYY-MM-DD`），格式统一。对于这种格式统一的列，转换非常简单：

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_14.png)

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_16.png)

```python
df['date1'] = pd.to_datetime(df['date1'])
```

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_18.png)

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_20.png)

执行后，`date1` 列的数据类型会从 `object` 变为 `datetime64[ns]`。这个数据类型可以精确记录日期和时间（纳秒级）。

## 提取日期特征

成功将列转换为日期时间类型后，我们就可以轻松提取各种日期特征，例如星期几、月份等。这主要通过 `.dt` 访问器实现，其功能类似于字符串列的 `.str` 访问器。

以下是提取星期几和星期几名称的示例：

```python
# 提取星期几（数字，默认周一为0）
df['d1_dow'] = df['date1'].dt.dayofweek

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_22.png)

# 提取星期几的名称
df['d1_dow_name'] = df['date1'].dt.day_name()
```

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_24.png)

通过 `.dt` 访问器，你还可以获取年、月、日、小时等其他特征。

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_26.png)

## 处理格式不一致的日期

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_28.png)

在实际数据中，日期格式往往不一致。例如，我们的 `date2` 列虽然大体是ISO 8601格式，但有些值包含时分秒，有些甚至包含毫秒，有些则没有时间部分。

如果直接使用 `pd.to_datetime()` 转换，可能会报错。Pandas为此提供了 `format='mixed'` 参数，可以智能处理混合格式：

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_30.png)

```python
df['date2'] = pd.to_datetime(df['date2'], format='mixed')
```

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_32.png)

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_34.png)

此参数会尝试解析列中各种常见的日期时间格式，并将其统一转换。

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_36.png)

然而，有些情况 `pd.to_datetime()` 也无法自动处理。例如 `date3` 列，其意图是表示“2027年4月3日”，但前三个值是“月/日/年”或类似格式，最后一个值是“日/月/年”。由于存在根本性的歧义（月份和日期的顺序不同），自动转换无法判断用户意图，可能导致错误结果。

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_38.png)

对于这种极端情况，可能需要将数据框按不同格式拆分，分别进行转换后再合并。

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_40.png)

## 计算日期差与时间间隔

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_42.png)

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_43.png)

日期时间数据类型的一个强大之处是可以直接进行算术运算，计算时间间隔。

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_45.png)

**1. 计算两个日期列之间的差值：**

```python
df['d1_minus_d2'] = df['date1'] - df['date2']
```
结果是一个 `timedelta64[ns]` 类型的序列，表示时间差。

**2. 将时间差转换为数值（例如天数）：**

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_47.png)

`timedelta` 的底层是纳秒数。我们可以先将其转换为数值，再转换为所需单位。

```python
# 将时间差转换为天数（数值）
df['d1_minus_d2_days'] = pd.to_numeric(df['d1_minus_d2']) / (1e9 * 60 * 60 * 24)
```

**3. 计算距今的时间：**

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_49.png)

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_50.png)

使用 `pd.Timestamp.now()` 获取当前时间，可以轻松计算某个日期距离今天有多久。

```python
df['days_since_d1'] = pd.Timestamp.now() - df['date1']
df['days_since_d1_numeric'] = pd.to_numeric(df['days_since_d1']) / (1e9 * 60 * 60 * 24)
```

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_52.png)

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_54.png)

**4. 计算未来或过去的日期：**

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_56.png)

使用 `pd.Timedelta` 可以方便地对日期进行加减运算。

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_58.png)

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_60.png)

```python
# 计算 date1 之后10天的日期
df['date1_plus_10d'] = df['date1'] + pd.Timedelta(10, unit='D')
```

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_61.png)

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_63.png)

## 总结

本节课中我们一起学习了在Pandas中处理日期时间数据的关键技能：

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_65.png)

1.  **转换数据类型**：使用 `pd.to_datetime()` 函数将字符串列转换为 `datetime64[ns]` 类型。
2.  **提取特征**：通过 `.dt` 访问器提取如星期、月份等日期组成部分。
3.  **处理不一致格式**：对于混合格式的日期，使用 `format='mixed'` 参数尝试转换；对于有歧义的格式，可能需要手动处理。
4.  **进行计算**：日期时间类型支持直接相减得到时间差，也支持与 `pd.Timedelta` 相加得到新的日期。可以利用 `pd.Timestamp.now()` 计算与当前时间的间隔。

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_67.png)

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_68.png)

![](img/6aba8c7dd8b85f66e0bd34c788bec1fd_69.png)

掌握这些基本操作，你将能够应对数据分析中遇到的大部分日期处理任务。