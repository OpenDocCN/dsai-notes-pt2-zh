# 8：Lambda表达式与字典 🐍

在本节课中，我们将要学习Python中的两个重要概念：**Lambda表达式**和**字典**。Lambda表达式是一种编写高阶函数的简洁方式，而字典则是一种强大的数据结构，允许我们通过键名而非位置来组织和访问数据。掌握这两者将极大地简化我们的编程操作。

![](img/c2370f245f9b7d671cb9c568a1e386f0_1.png)

![](img/c2370f245f9b7d671cb9c568a1e386f0_3.png)

![](img/c2370f245f9b7d671cb9c568a1e386f0_5.png)

![](img/c2370f245f9b7d671cb9c568a1e386f0_6.png)

![](img/c2370f245f9b7d671cb9c568a1e386f0_8.png)

## Lambda表达式：匿名函数的简洁写法

上一节我们介绍了高阶函数。本节中我们来看看如何用更简洁的方式定义它们。

![](img/c2370f245f9b7d671cb9c568a1e386f0_10.png)

Lambda表达式是定义简单、单行匿名函数的一种方式。它省略了`def`关键字和函数名，直接返回表达式的值。其基本语法是：`lambda 参数: 表达式`。

![](img/c2370f245f9b7d671cb9c568a1e386f0_12.png)

例如，一个将数字加1的函数：
*   使用`def`定义：`def add1(v): return v + 1`
*   使用Lambda表达式：`add1 = lambda v: v + 1`

![](img/c2370f245f9b7d671cb9c568a1e386f0_14.png)

Lambda表达式最常用于需要将简单函数作为参数传递的场景，例如与`map`、`filter`、`sorted`等高阶函数配合使用。

![](img/c2370f245f9b7d671cb9c568a1e386f0_16.png)

以下是Lambda表达式的一些常见用法：

*   **与`map`函数结合**：`list(map(lambda n: n * n, range(10)))` 会生成一个0到9的平方数列表。
*   **与`sorted`函数结合**：`sorted(numbers, key=lambda n: n % 2)` 会根据数字是奇数还是偶数进行排序（奇数在前）。
*   **自定义排序键**：`sorted(data, key=lambda x: x[‘property’])` 可以根据数据中某个特定属性的值进行排序，这在处理表格或字典列表时非常有用。

**请注意**：在环境图中，Lambda函数没有固有名称，通常会统一显示为 `lambda`。

![](img/c2370f245f9b7d671cb9c568a1e386f0_18.png)

![](img/c2370f245f9b7d671cb9c568a1e386f0_20.png)

## 字典：通过键名组织数据

![](img/c2370f245f9b7d671cb9c568a1e386f0_22.png)

现在，我们转向另一个强大的工具——字典。如果说列表是通过索引（位置）来访问数据，那么字典就是通过键（key）来访问数据。

![](img/c2370f245f9b7d671cb9c568a1e386f0_24.png)

![](img/c2370f245f9b7d671cb9c568a1e386f0_26.png)

字典使用花括号 `{}` 创建，其中的元素以 `键: 值` 的形式存在。你可以将字典视为一组“变量名”和其对应值的集合。

![](img/c2370f245f9b7d671cb9c568a1e386f0_28.png)

![](img/c2370f245f9b7d671cb9c568a1e386f0_30.png)

以下是字典的基本操作：

*   **创建字典**：`course = {‘name’: ‘CS88’, ‘dept’: ‘Computer Science’, ‘units’: 3}`
*   **访问值**：使用方括号和键名，如 `course[‘name’]` 会返回 `‘CS88’`。
*   **安全访问（避免KeyError）**：使用 `.get()` 方法。`course.get(‘title’)` 若键不存在则返回 `None`，你也可以指定默认值：`course.get(‘title’, ‘Not Available’)`。
*   **遍历字典**：
    *   `for key in course:` 遍历所有键。
    *   `for value in course.values():` 遍历所有值。
    *   `for key, value in course.items():` 同时遍历键和值。

字典在数据处理中极其有用，例如在即将到来的Map项目中，它可以清晰地表示一家餐馆的各类信息（名称、评分、坐标等）。

![](img/c2370f245f9b7d671cb9c568a1e386f0_32.png)

## 字典推导式

![](img/c2370f245f9b7d671cb9c568a1e386f0_34.png)

与列表推导式类似，我们也可以使用推导式来快速创建字典。

![](img/c2370f245f9b7d671cb9c568a1e386f0_36.png)

![](img/c2370f245f9b7d671cb9c568a1e386f0_38.png)

![](img/c2370f245f9b7d671cb9c568a1e386f0_40.png)

![](img/c2370f245f9b7d671cb9c568a1e386f0_42.png)

例如，统计一句话中每个单词的长度：
```python
text = “once upon a time”
word_lengths = {word: len(word) for word in text.split()}
# 结果：{‘once’: 4, ‘upon’: 4, ‘a’: 1, ‘time’: 4}
```

## 总结

本节课中我们一起学习了：
1.  **Lambda表达式**：一种用于定义简单匿名函数的简洁语法，特别适合作为参数传递给高阶函数。
2.  **字典**：一种通过键（key）来存储和访问映射关系的数据结构，它比列表更能清晰地表达具有命名属性的数据。
3.  **字典推导式**：一种快速生成字典的方法。

![](img/c2370f245f9b7d671cb9c568a1e386f0_44.png)

Lambda和字典是Python中简化代码、提高效率的重要工具。在接下来的课程中，我们将利用字典来构建更复杂的抽象数据类型。