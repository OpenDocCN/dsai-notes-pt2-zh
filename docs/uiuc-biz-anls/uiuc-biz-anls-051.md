#  051：清理数据框的字符串列 📊

![](img/08979f6f388badcb158c7bd5df434f38_0.png)

在本节课中，我们将学习如何操作和清理数据框中数据类型为“对象”（即字符串或字符型）的列。我们将介绍合并字符串、修改大小写、去除空格、提取子字符串以及使用正则表达式等核心技巧。

---

## 概述

数据清洗是数据分析的关键步骤，尤其是处理文本数据时。字符串列中常见的问题包括大小写不一致、存在多余空格、需要提取或替换特定内容等。本节将演示如何使用Pandas库中的`.str`访问器及其方法来高效地解决这些问题。

![](img/08979f6f388badcb158c7bd5df434f38_2.png)

![](img/08979f6f388badcb158c7bd5df434f38_3.png)

---

## 合并字符串

有时我们需要将不同列的数据合并，或在现有字符串后添加固定文本。

以下是合并两列字符串的方法：

```python
df['name_cat'] = df['name'] + df['category']
```

运行上述代码后，数据框中会新增一个`name_cat`列，其值为`name`列和`category`列对应值的拼接。

![](img/08979f6f388badcb158c7bd5df434f38_5.png)

![](img/08979f6f388badcb158c7bd5df434f38_6.png)

如果需要在现有列的每个值后添加固定字符串，可以这样做：

```python
df['name_owner'] = df['name'] + '_wrong'
```

![](img/08979f6f388badcb158c7bd5df434f38_8.png)

执行后，`name_owner`列的每个值都会在原始名称后加上“_wrong”。

---

## 修改字符串大小写

![](img/08979f6f388badcb158c7bd5df434f38_10.png)

处理文本数据时，统一大小写（如全部转为小写）有助于后续的分析和匹配。

![](img/08979f6f388badcb158c7bd5df434f38_12.png)

我们可以使用`.str`访问器下的`.lower()`方法来实现：

```python
df['category'] = df['category'].str.lower()
```

![](img/08979f6f388badcb158c7bd5df434f38_14.png)

运行代码后，`category`列中的所有文本都会转换为小写。`.str`访问器还提供了`.upper()`（转为大写）和`.title()`（转为标题格式）等方法。

![](img/08979f6f388badcb158c7bd5df434f38_16.png)

![](img/08979f6f388badcb158c7bd5df434f38_17.png)

---

## 去除首尾空格

![](img/08979f6f388badcb158c7bd5df434f38_19.png)

![](img/08979f6f388badcb158c7bd5df434f38_20.png)

数据中不易察觉的首尾空格可能导致字符串匹配失败。检查空格的一个方法是打印列值或使用`.loc`方法查看单个值。

检查空格示例：
```python
print(df['name'])
# 或
print(df.loc[0, 'name'])
```

要去除这些空格，可以使用`.strip()`方法。通常，我们会将大小写转换和去除空格的操作链式执行：

```python
df['name'] = df['name'].str.lower().str.strip()
```

![](img/08979f6f388badcb158c7bd5df434f38_22.png)

执行后，`name`列不仅变为小写，首尾的空格也被移除。

---

![](img/08979f6f388badcb158c7bd5df434f38_24.png)

## 提取子字符串

我们可以根据字符位置从字符串中提取特定部分。

提取前6个字符：
```python
df['name_sub'] = df['name'].str[:6]
```

从第2个字符提取到第3个字符（索引从0开始）：
```python
df['name_sub'] = df['name'].str[1:3]
```

![](img/08979f6f388badcb158c7bd5df434f38_26.png)

提取最后6个字符：
```python
df['name_sub'] = df['name'].str[-6:]
```

这些操作允许我们灵活地获取字符串的任意部分。

![](img/08979f6f388badcb158c7bd5df434f38_28.png)

![](img/08979f6f388badcb158c7bd5df434f38_29.png)

---

![](img/08979f6f388badcb158c7bd5df434f38_31.png)

## 检查与替换子字符串

![](img/08979f6f388badcb158c7bd5df434f38_33.png)

![](img/08979f6f388badcb158c7bd5df434f38_34.png)

判断字符串是否包含特定内容，可以使用`.contains()`方法。

![](img/08979f6f388badcb158c7bd5df434f38_36.png)

例如，检查`name`列是否包含“ball”：
```python
df['name_ball'] = df['name'].str.contains('ball')
```

运行后，`name_ball`列会显示布尔值，表示对应行是否包含“ball”。

![](img/08979f6f388badcb158c7bd5df434f38_38.png)

若要替换或删除特定子字符串，则使用`.replace()`方法。例如，将“ball”替换为空字符串（即删除）：

```python
df['name'] = df['name'].str.replace('ball', '')
```

![](img/08979f6f388badcb158c7bd5df434f38_40.png)

![](img/08979f6f388badcb158c7bd5df434f38_42.png)

执行后，所有包含“ball”的地方都会被移除。

![](img/08979f6f388badcb158c7bd5df434f38_44.png)

---

## 拆分字符串

![](img/08979f6f388badcb158c7bd5df434f38_46.png)

`.split()`方法可以根据指定的分隔符将字符串拆分为列表。

按空格拆分：
```python
split_result = df['name'].str.split(' ')
```

按字母“a”拆分：
```python
split_result = df['name'].str.split('a')
```

![](img/08979f6f388badcb158c7bd5df434f38_48.png)

![](img/08979f6f388badcb158c7bd5df434f38_49.png)

如果希望将拆分后的结果扩展为新的数据列，可以结合`expand=True`参数：

![](img/08979f6f388badcb158c7bd5df434f38_51.png)

```python
df[['name1', 'name2', 'name3']] = df['name'].str.split(' ', expand=True)
```

这样，原`name`列会根据空格被拆分成三列。如果某行拆分后的部分不足，对应位置会填充`None`。

![](img/08979f6f388badcb158c7bd5df434f38_53.png)

---

![](img/08979f6f388badcb158c7bd5df434f38_55.png)

## 使用正则表达式

正则表达式是用于匹配复杂文本模式的强大工具。例如，我们想替换每行字符串中最后一个空格之前的所有内容。

以下代码使用正则表达式实现该功能：
```python
df['name_reg'] = df['name'].str.replace(r'^.* ', 'new_first_word ', regex=True)
```

代码解释：
*   `r'^.* '` 是一个正则表达式模式，表示“从字符串开头(`^`)匹配任意字符(`.`)零次或多次(`*`)，直到遇到一个空格”。
*   `'new_first_word '` 是替换后的内容。
*   `regex=True` 参数表明使用正则表达式进行替换。

![](img/08979f6f388badcb158c7bd5df434f38_57.png)

执行后，对于包含空格的字符串，其最后一个空格之前的部分会被替换为“new_first_word ”。

---

## 总结

![](img/08979f6f388badcb158c7bd5df434f38_59.png)

![](img/08979f6f388badcb158c7bd5df434f38_60.png)

![](img/08979f6f388badcb158c7bd5df434f38_61.png)

本节课我们一起学习了清理数据框字符串列的核心操作。我们涵盖了合并字符串、统一大小写、去除空格、提取子字符串、检查与替换内容、拆分字符串以及使用正则表达式进行模式匹配。掌握这些`.str`访问器下的方法，能帮助你高效地准备文本数据，为后续分析打下坚实基础。记住，你无需死记所有方法，但理解其原理并在需要时查找文档至关重要。