# 16：可变性与对象标识 🧠

![](img/cffe9490f38c67ad4584db1c5c937ad7_0.png)

![](img/cffe9490f38c67ad4584db1c5c937ad7_1.png)

![](img/cffe9490f38c67ad4584db1c5c937ad7_2.png)

![](img/cffe9490f38c67ad4584db1c5c937ad7_3.png)

![](img/cffe9490f38c67ad4584db1c5c937ad7_5.png)

![](img/cffe9490f38c67ad4584db1c5c937ad7_7.png)

![](img/cffe9490f38c67ad4584db1c5c937ad7_9.png)

在本节课中，我们将要学习Python中可变与不可变对象的核心概念，并深入探讨如何区分对象的“相等”与“同一”。理解这些概念对于编写健壮、高效的代码至关重要。

---

## 概述：可变性与不可变性

在Python中，所有数据都是对象。对象大致可分为两类：**可变对象**和**不可变对象**。可变对象（如列表和字典）的内容可以在不创建新对象的情况下被修改。而不可变对象（如字符串、整数、元组）一旦创建，其值就无法改变，任何“修改”操作实际上都会返回一个全新的对象。

上一节我们介绍了对象的基本概念，本节中我们来看看如何区分对象的修改与复制，并理解`is`与`==`操作符的差异。

---

## 可变对象 vs. 不可变对象

### 不可变对象示例：字符串

![](img/cffe9490f38c67ad4584db1c5c937ad7_11.png)

字符串是典型的不可变对象。当你尝试“修改”一个字符串时，Python实际上会创建一个新的字符串对象。

```python
course = "CS88"
# 尝试修改字符串，但实际上是创建了一个新对象
new_course = course.lower()
print(course)      # 输出: CS88 (原对象未变)
print(new_course)  # 输出: cs88 (新对象)
```

![](img/cffe9490f38c67ad4584db1c5c937ad7_13.png)

![](img/cffe9490f38c67ad4584db1c5c937ad7_15.png)

在上面的例子中，`course.lower()`并没有改变`course`本身，而是返回了一个全新的小写字符串。要改变`course`变量所指向的值，必须使用赋值语句：`course = course.lower()`。

### 可变对象示例：列表

![](img/cffe9490f38c67ad4584db1c5c937ad7_17.png)

列表是可变对象。你可以直接修改列表中的元素，而无需创建一个全新的列表。

![](img/cffe9490f38c67ad4584db1c5c937ad7_19.png)

```python
my_list = [1, 2, 3, 4]
# 直接修改列表中的元素
my_list[2] = “elephant”
print(my_list)  # 输出: [1, 2, ‘elephant’, 4]
```

![](img/cffe9490f38c67ad4584db1c5c937ad7_21.png)

在这个例子中，`my_list`这个列表对象本身没有变（它的“身份”没变），但其内部的数据被修改了。字典也表现出类似的可变行为。

---

## 对象的“相等”与“同一”

这是本节课的核心。Python提供了两个操作符来比较对象：
*   `==` (相等)：检查两个对象的值或内容是否相同。
*   `is` (同一)：检查两个变量名是否指向内存中的**同一个对象**。

![](img/cffe9490f38c67ad4584db1c5c937ad7_23.png)

![](img/cffe9490f38c67ad4584db1c5c937ad7_25.png)

![](img/cffe9490f38c67ad4584db1c5c937ad7_26.png)

### 理解 `==` 操作符

`==` 操作符比较的是对象的逻辑值。

![](img/cffe9490f38c67ad4584db1c5c937ad7_28.png)

```python
list_a = [1, 2, 3, 4]
list_b = [1, 2, 3, 4]
list_c = [1, 2, 3]

print(list_a == list_b)  # 输出: True (值相同)
print(list_a == list_c)  # 输出: False (值不同)
```

即使`list_a`和`list_b`是两个独立创建的列表，只要内容一样，`==`就会返回`True`。

### 理解 `is` 操作符

`is` 操作符比较的是对象的身份标识（在内存中的地址）。可以使用内置函数`id()`来查看对象的唯一标识。

```python
list_a = [1, 2, 3, 4]
list_b = [1, 2, 3, 4]
list_c = list_a  # list_c 指向 list_a 所指向的同一个列表对象

print(id(list_a))        # 输出一个内存地址，如 140245678945600
print(id(list_b))        # 输出另一个不同的地址
print(id(list_c))        # 输出与 list_a 相同的地址

print(list_a is list_b)  # 输出: False (是不同的对象)
print(list_a is list_c)  # 输出: True (是同一个对象)
```

**关键点**：如果 `a is b` 为 `True`，那么 `a == b` 也必定为 `True`。反之则不一定成立。

---

## 可变性带来的陷阱

![](img/cffe9490f38c67ad4584db1c5c937ad7_30.png)

![](img/cffe9490f38c67ad4584db1c5c937ad7_32.png)

![](img/cffe9490f38c67ad4584db1c5c937ad7_34.png)

当多个变量指向同一个可变对象时，通过任何一个变量修改对象，都会影响到所有指向它的变量。

```python
original_list = [1, 2, 3]
alias_list = original_list  # 不是复制，只是起了个别名

![](img/cffe9490f38c67ad4584db1c5c937ad7_36.png)

![](img/cffe9490f38c67ad4584db1c5c937ad7_38.png)

alias_list.append(4)
print(original_list)  # 输出: [1, 2, 3, 4] (原列表也被修改了!)
print(alias_list is original_list)  # 输出: True
```

这种行为有时会导致难以察觉的bug。为了避免这种情况，当你需要一份独立的副本时，应该显式地创建复制品。

![](img/cffe9490f38c67ad4584db1c5c937ad7_40.png)

以下是创建列表副本的几种方法：

```python
original = [1, 2, 3]
# 方法1: 使用 list() 构造函数
copy1 = list(original)
# 方法2: 使用切片 [:]
copy2 = original[:]
# 方法3: 使用 .copy() 方法 (Python 3.3+)
copy3 = original.copy()

# 现在修改副本不会影响原列表
copy1.append(4)
print(original)  # 输出: [1, 2, 3]
print(copy1)     # 输出: [1, 2, 3, 4]
```

![](img/cffe9490f38c67ad4584db1c5c937ad7_42.png)

![](img/cffe9490f38c67ad4584db1c5c937ad7_44.png)

---

## 嵌套结构的可变性

可变性的规则也适用于嵌套的数据结构。例如，元组本身是不可变的，但如果它内部包含一个列表，那么这个列表的内容仍然可以被修改。

![](img/cffe9490f38c67ad4584db1c5c937ad7_46.png)

```python
my_tuple = (1, [2, 3], 4)
# my_tuple[0] = 99  # 错误！不能修改元组元素
my_tuple[1].append(99)  # 正确！可以修改元组内的列表
print(my_tuple)  # 输出: (1, [2, 3, 99], 4)
```

![](img/cffe9490f38c67ad4584db1c5c937ad7_48.png)

这说明了Python的保护机制是“浅层”的，它只防止直接修改容器本身，而不限制修改容器内可变元素的内容。

![](img/cffe9490f38c67ad4584db1c5c937ad7_50.png)

---

## 总结

本节课中我们一起学习了Python中可变与不可变对象的关键区别，以及如何区分对象的“相等”与“同一”。

![](img/cffe9490f38c67ad4584db1c5c937ad7_52.png)

*   **可变对象**（如`list`, `dict`）允许直接修改其内容。
*   **不可变对象**（如`str`, `int`, `tuple`）的值无法改变，任何修改操作都会创建新对象。
*   **`==`操作符**用于比较两个对象的**值**是否相等。
*   **`is`操作符**用于检查两个变量是否指向内存中的**同一个对象**。
*   当处理可变对象时，需要特别注意**别名问题**，多个变量指向同一对象可能导致意外的修改。在需要独立副本时，务必使用`list()`、切片`[:]`或`.copy()`方法。

![](img/cffe9490f38c67ad4584db1c5c937ad7_54.png)

理解这些概念将帮助你更好地预测程序行为，避免常见的错误，并编写出更清晰、更可靠的代码。在接下来的课程中，我们将探讨程序的效率分析。