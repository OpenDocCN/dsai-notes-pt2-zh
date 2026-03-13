#  125：使用requests模块构建API请求 📡

在本节课中，我们将学习如何使用API从外部数据源获取数据，并将其导入到本地的Python环境中进行分析。我们将重点介绍如何使用Python的`requests`模块来构建和执行API请求。

## 概述

![](img/430a2c8d7fa3b2c36f1198b571fd2e30_1.png)

API（应用程序编程接口）允许不同的软件应用之间进行通信和数据交换。通过API，我们可以直接从数据提供商的服务器请求数据，而无需手动下载文件。本节课将演示如何构建一个API请求URL，并使用`requests`模块获取芝加哥市建筑许可证数据。

![](img/430a2c8d7fa3b2c36f1198b571fd2e30_3.png)

![](img/430a2c8d7fa3b2c36f1198b571fd2e30_4.png)

![](img/430a2c8d7fa3b2c36f1198b571fd2e30_5.png)

## 构建API请求URL

上一节我们介绍了API的基本概念，本节中我们来看看如何构造一个能获取特定数据的请求URL。这是使用API过程中最具挑战性的部分，原因主要有两点：

![](img/430a2c8d7fa3b2c36f1198b571fd2e30_7.png)

![](img/430a2c8d7fa3b2c36f1198b571fd2e30_8.png)

![](img/430a2c8d7fa3b2c36f1198b571fd2e30_9.png)

1.  没有一种像关系型数据库的SQL那样，在所有API中通用的、标准化的语言来指明你需要什么数据。
2.  由于缺乏标准化，URL构造非常严格，一个缺失或多余的逗号都可能导致请求失败，且不易排查。

因此，最重要的一步是仔细阅读API的使用文档。

### 查找并理解API文档

以下是查找和理解API文档的关键步骤：

1.  **访问数据门户**：我们以芝加哥市数据门户（data.cityofchicago.org）为例，在“建筑”类别下找到“建筑许可证”数据集。
2.  **查看数据详情**：该数据集包含约80.6万行数据和115个列，并提供了详细的数据字典，这对理解数据字段非常有帮助。
3.  **定位API文档**：API文档的位置并不固定。在本例中，通过点击页面右上角的“操作”按钮，在下拉菜单中找到“API”选项。
4.  **阅读关键信息**：
    *   **数据格式**：默认为JSON，也可选择CSV。
    *   **API限制**：默认每次请求最多获取1000行数据。由于总数据量远大于此，我们需要通过参数来指定获取哪一部分数据。
    *   **API端点**：这是请求的基础URL。例如：`https://data.cityofchicago.org/resource/building-permits.json`
5.  **深入研究过滤和分页**：点击API文档链接，查看详细说明。核心要点包括：
    *   **简单过滤**：在基础URL后添加问号（`?`），然后使用类似SQL的语法进行过滤。例如：`?source=NN`。
    *   **组合过滤**：使用“与”符号（`&`）连接多个过滤条件。例如：`?source=PR&region=Virgin Islands`。
    *   **SOQL查询**：该API使用类似SQL的查询语言（SOQL）。要按日期过滤，需要使用`$where`参数。例如：`?$where=application_start_date >= '2024-01-01T00:00:00.000'`。
    *   **分页**：使用`$limit`和`$offset`参数控制获取的数据量和起始位置。`$limit=1000`表示获取1000行，`$offset=0`表示从第0行开始（即第一组1000行），`$offset=1000`则获取第二组1000行。
    *   **排序**：使用`$order`参数对结果进行排序。例如：`$order=application_start_date DESC` 表示按申请开始日期降序排列。

![](img/430a2c8d7fa3b2c36f1198b571fd2e30_11.png)

![](img/430a2c8d7fa3b2c36f1198b571fd2e30_12.png)

![](img/430a2c8d7fa3b2c36f1198b571fd2e30_13.png)

![](img/430a2c8d7fa3b2c36f1198b571fd2e30_14.png)

## 在Python中执行API请求

![](img/430a2c8d7fa3b2c36f1198b571fd2e30_16.png)

理解了如何构造URL后，我们来看看如何在Python环境中将这一切组合起来并执行。

![](img/430a2c8d7fa3b2c36f1198b571fd2e30_18.png)

### 1. 导入必要模块

![](img/430a2c8d7fa3b2c36f1198b571fd2e30_20.png)

首先，需要导入`requests`模块来执行API请求，以及`pandas`模块来分析数据。

![](img/430a2c8d7fa3b2c36f1198b571fd2e30_22.png)

![](img/430a2c8d7fa3b2c36f1198b571fd2e30_24.png)

```python
import requests
import pandas as pd
```

![](img/430a2c8d7fa3b2c36f1198b571fd2e30_26.png)

![](img/430a2c8d7fa3b2c36f1198b571fd2e30_27.png)

> **注意**：如果你的环境中尚未安装`requests`模块，需要使用包管理器（如`pip`或`conda`）进行安装。

### 2. 构造请求URL

为了避免创建冗长且易错的字符串，我们将URL分解为多个部分进行构建。

![](img/430a2c8d7fa3b2c36f1198b571fd2e30_29.png)

![](img/430a2c8d7fa3b2c36f1198b571fd2e30_31.png)

![](img/430a2c8d7fa3b2c36f1198b571fd2e30_32.png)

```python
# 基础API端点
base_url = "https://data.cityofchicago.org/resource/building-permits.json"

![](img/430a2c8d7fa3b2c36f1198b571fd2e30_34.png)

# 设置获取的行数和起始点
limit_clause = "$limit=1000"
offset_clause = "$offset=0"

# 设置过滤条件：获取2024年1月1日之后的数据
modifiers = "$where=application_start_date >= '20240101'"

![](img/430a2c8d7fa3b2c36f1198b571fd2e30_36.png)

# 设置排序：按申请开始日期降序排列，确保获取最新数据
order_clause = "$order=application_start_date DESC"

# 使用f-string将所有部分组合成完整的URL
# 注意：第一个参数前用?，后续参数用&连接
url = f"{base_url}?{limit_clause}&{offset_clause}&{modifiers}&{order_clause}"
print(url) # 可以打印出来检查URL是否正确
```

![](img/430a2c8d7fa3b2c36f1198b571fd2e30_38.png)

### 3. 发送请求并获取响应

使用`requests.get()`函数发送构造好的请求。

```python
# 发送GET请求
my_response = requests.get(url)

# 检查请求状态码，200表示成功
print(f"状态码: {my_response.status_code}")
```

### 4. 处理响应数据

请求成功后，我们需要将返回的JSON数据转换为pandas DataFrame以便分析。

```python
# 将响应的JSON内容转换为Python字典
data_json = my_response.json()

# 将字典转换为pandas DataFrame
df = pd.DataFrame(data_json)

# 查看数据框的基本信息
print(f"获取的数据行数: {len(df)}")
print(df.head())
```

### 5. 数据后续处理与分析

现在数据已经存在于Python环境中，我们可以使用pandas进行各种分析。例如，将日期列转换为正确的格式，并按周对费用进行汇总。

```python
# 示例：将日期列转换为datetime类型，并计算每周总费用
df['application_start_date'] = pd.to_datetime(df['application_start_date'])
df['fee_paid'] = pd.to_numeric(df['fee_paid'], errors='coerce') # 将费用转换为数值类型

![](img/430a2c8d7fa3b2c36f1198b571fd2e30_40.png)

# 按周分组并求和
weekly_fees = df.set_index('application_start_date').resample('W')['fee_paid'].sum()

# 绘制图表
import matplotlib.pyplot as plt
weekly_fees.plot(kind='line', title='芝加哥建筑许可证每周总费用')
plt.xlabel('日期')
plt.ylabel('总费用（美元）')
plt.show()
```

## 总结

本节课中我们一起学习了如何使用Python的`requests`模块构建和执行API请求。关键步骤包括：
1.  **阅读API文档**：理解端点、过滤、排序和分页参数是关键。
2.  **构造请求URL**：将基础URL与各种查询参数（`$limit`， `$offset`， `$where`， `$order`）正确组合。
3.  **发送请求**：使用`requests.get(url)`函数。
4.  **处理响应**：检查状态码，并将返回的JSON数据转换为pandas DataFrame。
5.  **分析数据**：数据进入DataFrame后，即可利用pandas进行灵活的分析和可视化。

![](img/430a2c8d7fa3b2c36f1198b571fd2e30_42.png)

![](img/430a2c8d7fa3b2c36f1198b571fd2e30_44.png)

尽管构造URL初看可能复杂，但通过仔细阅读文档和分解步骤，你可以有效地从各种在线数据源获取实时数据，为你的分析项目提供强大的支持。