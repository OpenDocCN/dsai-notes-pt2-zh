# 21：Python迭代器与生成器 🐍

![](img/84714b289a8ac3ea6a4de6e4b84c6346_0.png)

![](img/84714b289a8ac3ea6a4de6e4b84c6346_1.png)

![](img/84714b289a8ac3ea6a4de6e4b84c6346_2.png)

![](img/84714b289a8ac3ea6a4de6e4b84c6346_3.png)

![](img/84714b289a8ac3ea6a4de6e4b84c6346_5.png)

在本节课中，我们将要学习Python中迭代器和生成器的概念。它们是处理数据流和实现惰性计算的核心工具，能帮助我们更高效地处理大量或动态生成的数据。我们将探讨它们的工作原理、如何创建，以及它们如何让`for`循环、`map`、`range`等我们熟悉的工具得以运行。

---

## 概述：序列、可迭代对象与迭代器

在深入之前，我们需要理清几个核心概念。在Python中，我们经常处理一系列数据。

**序列** 是一个特定的Python术语，指代有序的集合。典型的序列包括列表、元组、范围和字符串。序列支持以下操作：
*   切片（如 `my_list[1:4]`）
*   成员检查（如 `"CS88" in courses`）
*   拼接（如 `list1 + list2`）
*   计数（如 `my_list.count(‘x’)`）

**可迭代对象** 是一个更宽泛的概念，指任何你可以进行迭代（例如在`for`循环中使用）的对象。所有序列都是可迭代对象，但并非所有可迭代对象都是序列（例如`map`对象）。

**迭代器** 是代表特定数据流的对象。它提供了一种逐个访问元素的方式。

上一节我们介绍了基本概念，本节中我们来看看为什么`map`和`range`这样的对象行为特殊。

![](img/84714b289a8ac3ea6a4de6e4b84c6346_7.png)

---

![](img/84714b289a8ac3ea6a4de6e4b84c6346_9.png)

## 生成器与惰性求值

![](img/84714b289a8ac3ea6a4de6e4b84c6346_11.png)

当我们使用`map`函数时，会得到一个`map`对象，而不是列表。

```python
squares = map(lambda x: x*x, range(10))
print(squares)  # 输出: <map object at 0x...>
print(len(squares))  # 报错: object of type ‘map’ has no len()
print(squares[0])    # 报错: ‘map’ object is not subscriptable
```

这是因为`map`是一个**生成器**。它不会一次性计算出所有结果并存储在内存中，而是在每次需要下一个值时**按需生成**。这种特性称为**惰性求值**。

要查看所有结果，我们通常使用`list()`函数将其转换为列表：

```python
print(list(squares))  # 输出: [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

但生成器的强大之处在于，我们可以手动控制获取数据的节奏，这正是`next()`函数的作用。

---

## 使用 `next()` 函数

`next()`函数允许我们一次从迭代器中获取一个值。

![](img/84714b289a8ac3ea6a4de6e4b84c6346_13.png)

```python
squares = map(lambda x: x*x, range(5))
print(next(squares))  # 输出: 0
print(next(squares))  # 输出: 1
print(next(squares))  # 输出: 4
# ... 继续调用
```

![](img/84714b289a8ac3ea6a4de6e4b84c6346_15.png)

当数据流耗尽时，`next()`会抛出一个`StopIteration`异常，标志着迭代的结束。Python的`for`循环在内部就是通过不断调用`next()`并捕获`StopIteration`异常来实现的。

了解了如何使用迭代器后，接下来我们学习如何创建自己的生成器。

---

## 创建生成器：`yield` 关键字

我们可以使用`yield`关键字将任何函数转变为生成器函数。`yield`类似于`return`，但它会“暂停”函数执行，保存所有上下文，并在下次调用`next()`时从暂停处继续。

![](img/84714b289a8ac3ea6a4de6e4b84c6346_17.png)

![](img/84714b289a8ac3ea6a4de6e4b84c6346_19.png)

以下是一个生成平方数的生成器函数：

![](img/84714b289a8ac3ea6a4de6e4b84c6346_21.png)

![](img/84714b289a8ac3ea6a4de6e4b84c6346_23.png)

```python
def squares(n):
    for i in range(n):
        yield i * i

# 调用生成器函数会返回一个生成器对象
gen = squares(5)
print(type(gen))  # 输出: <class ‘generator’>

print(next(gen))  # 输出: 0
print(next(gen))  # 输出: 1
print(list(gen))  # 输出: [4, 9, 16] (注意：之前已经消耗了0和1)
```

`yield`让我们能够轻松创建按需产生数据的流。生成器在处理计算密集型任务或无限数据流时特别有用。

![](img/84714b289a8ac3ea6a4de6e4b84c6346_25.png)

![](img/84714b289a8ac3ea6a4de6e4b84c6346_27.png)

![](img/84714b289a8ac3ea6a4de6e4b84c6346_29.png)

---

## 构建自定义迭代器类

![](img/84714b289a8ac3ea6a4de6e4b84c6346_31.png)

除了使用`yield`，我们还可以通过实现**迭代器协议**来创建自定义迭代器类。这需要定义两个特殊方法：`__iter__()`和`__next__()`。

![](img/84714b289a8ac3ea6a4de6e4b84c6346_33.png)

以下是实现一个简易版`range`迭代器的示例：

![](img/84714b289a8ac3ea6a4de6e4b84c6346_35.png)

```python
class MyRange:
    def __init__(self, start, end):
        self.current = start
        self.end = end

    def __iter__(self):
        # __iter__ 必须返回一个迭代器对象。
        # 如果这个类本身实现了 __next__，通常返回 self 即可。
        return self

    def __next__(self):
        if self.current >= self.end:
            # 迭代结束时，抛出 StopIteration 异常
            raise StopIteration
        value = self.current
        self.current += 1
        return value

# 使用自定义迭代器
my_range = MyRange(0, 3)
print(next(my_range))  # 输出: 0
print(next(my_range))  # 输出: 1
for num in my_range:   # 现在也可以用在 for 循环中
    print(num)         # 输出: 2 (注意：迭代状态是延续的)
```

![](img/84714b289a8ac3ea6a4de6e4b84c6346_37.png)

**迭代器协议**规定：
1.  `__iter__()`方法返回迭代器对象本身（或一个新的迭代器对象）。
2.  `__next__()`方法返回序列中的下一个值，如果没有更多值，则引发`StopIteration`异常。

![](img/84714b289a8ac3ea6a4de6e4b84c6346_39.png)

---

![](img/84714b289a8ac3ea6a4de6e4b84c6346_41.png)

## 另一种方式：`__getitem__` 方法

![](img/84714b289a8ac3ea6a4de6e4b84c6346_43.png)

实现迭代器还有另一种不常用的方式：定义`__getitem__`方法。如果一个类定义了`__getitem__`方法，Python也能用它来进行迭代。

![](img/84714b289a8ac3ea6a4de6e4b84c6346_45.png)

![](img/84714b289a8ac3ea6a4de6e4b84c6346_47.png)

![](img/84714b289a8ac3ea6a4de6e4b84c6346_49.png)

![](img/84714b289a8ac3ea6a4de6e4b84c6346_51.png)

![](img/84714b289a8ac3ea6a4de6e4b84c6346_53.png)

```python
class SimpleRange:
    def __init__(self, limit):
        self.limit = limit

    def __getitem__(self, index):
        if index < self.limit:
            return index  # 对于 range(n)，第 i 个值就是 i
        else:
            raise IndexError  # 用 IndexError 代替 StopIteration

![](img/84714b289a8ac3ea6a4de6e4b84c6346_55.png)

![](img/84714b289a8ac3ea6a4de6e4b84c6346_56.png)

![](img/84714b289a8ac3ea6a4de6e4b84c6346_58.png)

![](img/84714b289a8ac3ea6a4de6e4b84c6346_60.png)

![](img/84714b289a8ac3ea6a4de6e4b84c6346_62.png)

for i in SimpleRange(3):
    print(i)  # 输出: 0, 1, 2
```

![](img/84714b289a8ac3ea6a4de6e4b84c6346_64.png)

虽然`__getitem__`更简单，但通过`__iter__`和`__next__`能提供更精细的控制，是更常见的做法。

---

## 检查可迭代性

在编写代码时，如果你需要检查一个对象是否可迭代，可以使用`collections.abc`模块。

![](img/84714b289a8ac3ea6a4de6e4b84c6346_66.png)

```python
from collections.abc import Iterable, Sequence

my_list = [1, 2, 3]
my_map = map(lambda x: x, [1,2])

![](img/84714b289a8ac3ea6a4de6e4b84c6346_68.png)

print(isinstance(my_list, Iterable))  # 输出: True
print(isinstance(my_list, Sequence))  # 输出: True (列表是序列)
print(isinstance(my_map, Iterable))   # 输出: True
print(isinstance(my_map, Sequence))   # 输出: False (map不是序列)
```

![](img/84714b289a8ac3ea6a4de6e4b84c6346_70.png)

---

![](img/84714b289a8ac3ea6a4de6e4b84c6346_72.png)

## 总结

本节课中我们一起学习了Python迭代器与生成器的核心知识：
*   **序列**是支持索引、切片等操作的有序集合（如列表、字符串）。
*   **可迭代对象**是任何可用于`for`循环的对象。
*   **迭代器**是实现了`__iter__()`和`__next__()`方法的对象，用于逐个访问数据流。
*   **生成器**是一种特殊的迭代器，通过`yield`关键字或生成器表达式创建，支持**惰性求值**，能高效处理大型或无限数据流。
*   我们掌握了使用`next()`函数手动控制迭代，以及通过实现**迭代器协议**或使用`yield`来创建自己的迭代器和生成器。

![](img/84714b289a8ac3ea6a4de6e4b84c6346_74.png)

![](img/84714b289a8ac3ea6a4de6e4b84c6346_75.png)

理解这些概念揭示了`for`循环、`map`、`filter`等工具的内部工作原理，并赋予你构建高效、内存友好的数据处理管道的能力。这是Python中一个强大而优雅的特性。