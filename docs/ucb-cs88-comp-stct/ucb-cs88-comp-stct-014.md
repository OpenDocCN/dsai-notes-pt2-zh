# 14：面向对象编程进阶 🧩

![](img/f49e75b250880623fa487fffc43ba1ff_0.png)

![](img/f49e75b250880623fa487fffc43ba1ff_1.png)

![](img/f49e75b250880623fa487fffc43ba1ff_3.png)

![](img/f49e75b250880623fa487fffc43ba1ff_4.png)

![](img/f49e75b250880623fa487fffc43ba1ff_5.png)

在本节课中，我们将深入学习面向对象编程，重点探讨Python中的特殊方法（魔法方法）和继承的概念。这些工具能帮助我们编写更自然、更强大的代码。

---

## 特殊方法：`__repr__` 与 `__str__` 🔮

上一节我们介绍了对象的基本概念，本节中我们来看看如何更好地控制和展示我们的对象。Python提供了一些以双下划线开头和结尾的“魔法方法”，它们允许我们自定义对象的行为。

![](img/f49e75b250880623fa487fffc43ba1ff_7.png)

### `__repr__` 方法

![](img/f49e75b250880623fa487fffc43ba1ff_9.png)

`__repr__` 方法旨在提供一个对象的**明确、无歧义**的字符串表示，通常用于调试和日志记录。当我们在解释器中直接输入对象名并回车时，Python会调用此方法。

![](img/f49e75b250880623fa487fffc43ba1ff_11.png)

![](img/f49e75b250880623fa487fffc43ba1ff_13.png)

**公式/代码示例：**
```python
class Account:
    def __init__(self, name, balance):
        self.name = name
        self.balance = balance
        self.account_number = Account.account_number_seed
        Account.account_number_seed += 1

    def __repr__(self):
        return f"Account(name={self.name!r}, number={self.account_number})"
```
在这个例子中，`__repr__` 方法返回了账户名和账户号，这比Python默认的内存地址表示更有用。

### `__str__` 方法

![](img/f49e75b250880623fa487fffc43ba1ff_15.png)

`__str__` 方法旨在提供一个对象的**可读性更好**的字符串表示，通常用于给最终用户查看。当我们使用 `print()` 函数时，Python会调用此方法。

![](img/f49e75b250880623fa487fffc43ba1ff_17.png)

![](img/f49e75b250880623fa487fffc43ba1ff_19.png)

![](img/f49e75b250880623fa487fffc43ba1ff_21.png)

**公式/代码示例：**
```python
class Account:
    # ... __init__ 和其他方法 ...

    def __str__(self):
        return f"Account '{self.name}' has balance: ${self.balance}"
```
`__str__` 方法可以返回更友好、包含更多上下文信息（如余额）的字符串。

**核心区别：**
*   `__repr__` 的目标是明确性，理想情况下，`eval(repr(obj))` 应能重新创建该对象。
*   `__str__` 的目标是可读性，是 `print(obj)` 时显示的内容。
*   如果只定义了 `__repr__` 而未定义 `__str__`，则 `print()` 也会使用 `__repr__`。

![](img/f49e75b250880623fa487fffc43ba1ff_23.png)

![](img/f49e75b250880623fa487fffc43ba1ff_24.png)

![](img/f49e75b250880623fa487fffc43ba1ff_26.png)

---

![](img/f49e75b250880623fa487fffc43ba1ff_28.png)

## 运算符重载：`__sub__` 方法 ➖

![](img/f49e75b250880623fa487fffc43ba1ff_30.png)

理解了如何展示对象后，我们来看看如何让对象支持像内置类型一样的操作。Python允许我们通过魔法方法重载运算符，例如实现减法。

![](img/f49e75b250880623fa487fffc43ba1ff_32.png)

假设我们有一个 `Point` 类，代表二维空间中的点。我们希望能够直接用 `-` 运算符计算两点之差。

![](img/f49e75b250880623fa487fffc43ba1ff_34.png)

**公式/代码示例：**
```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __sub__(self, other):
        """定义减法操作：返回一个新的Point，其坐标为两点的坐标差"""
        return Point(self.x - other.x, self.y - other.y)

    def __repr__(self):
        return f"Point({self.x}, {self.y})"

![](img/f49e75b250880623fa487fffc43ba1ff_36.png)

![](img/f49e75b250880623fa487fffc43ba1ff_38.png)

# 使用
origin = Point(0, 0)
campus = Point(8, 9)
result = origin - campus  # 等价于 origin.__sub__(campus)
print(result)  # 输出：Point(-8, -9)
```
通过定义 `__sub__` 方法，我们让 `Point` 对象支持了直观的减法语法，使代码更清晰易读。Python支持许多这样的运算符重载方法（如 `__add__`, `__mul__` 等）。

![](img/f49e75b250880623fa487fffc43ba1ff_40.png)

---

![](img/f49e75b250880623fa487fffc43ba1ff_42.png)

![](img/f49e75b250880623fa487fffc43ba1ff_44.png)

## 继承与 `super()` 函数 🧬

最后，我们来探讨面向对象编程中一个强大的概念：继承。它允许我们基于现有类创建新类，实现代码的复用和层次化组织。

### 继承的基本概念

继承模拟了“是一个（is-a）”的关系。例如，“支票账户”是一种“账户”。子类（派生类）继承父类（基类）的所有属性和方法，并可以添加或修改特定行为。

![](img/f49e75b250880623fa487fffc43ba1ff_46.png)

**公式/代码示例：**
```python
class Account:
    # 父类 Account 的定义...

![](img/f49e75b250880623fa487fffc43ba1ff_48.png)

class CheckingAccount(Account):  # CheckingAccount 继承自 Account
    def __init__(self, name, initial_deposit):
        # 调用父类的 __init__ 方法来初始化共有属性
        Account.__init__(self, name, initial_deposit)
        # 可以添加支票账户特有的属性
        self.minimum_balance = 100
```

![](img/f49e75b250880623fa487fffc43ba1ff_50.png)

![](img/f49e75b250880623fa487fffc43ba1ff_52.png)

### 使用 `super()` 函数

![](img/f49e75b250880623fa487fffc43ba1ff_54.png)

![](img/f49e75b250880623fa487fffc43ba1ff_56.png)

在子类中，我们经常需要调用父类的方法。`super()` 函数提供了一种更优雅、更安全的方式来引用父类，特别是在复杂的继承链中。

![](img/f49e75b250880623fa487fffc43ba1ff_58.png)

![](img/f49e75b250880623fa487fffc43ba1ff_60.png)

![](img/f49e75b250880623fa487fffc43ba1ff_61.png)

![](img/f49e75b250880623fa487fffc43ba1ff_62.png)

**公式/代码示例：**
```python
class SavingsAccount(Account):
    def __init__(self, name, initial_deposit, interest_rate=0.01):
        # 使用 super() 调用父类的 __init__ 方法
        super().__init__(name, initial_deposit)
        # 添加储蓄账户特有的属性
        self.interest_rate = interest_rate

    def __repr__(self):
        # 也可以使用 super() 调用父类的其他方法
        parent_repr = super().__repr__()
        return f"SavingsAccount({parent_repr}, interest_rate={self.interest_rate})"
```
使用 `super().__init__(...)` 代替 `Account.__init__(self, ...)` 的好处是，它自动处理了当前实例（`self`）的传递，并且在多重继承中能更准确地找到下一个要调用的父类方法。

![](img/f49e75b250880623fa487fffc43ba1ff_64.png)

![](img/f49e75b250880623fa487fffc43ba1ff_66.png)

![](img/f49e75b250880623fa487fffc43ba1ff_68.png)

![](img/f49e75b250880623fa487fffc43ba1ff_70.png)

![](img/f49e75b250880623fa487fffc43ba1ff_71.png)

**继承的优势：**
*   **代码复用**：避免重复编写公共逻辑。
*   **逻辑清晰**：通过类层次结构清晰地表达不同类型对象之间的关系。
*   **易于扩展**：添加新的子类非常方便，只需定义差异部分。

![](img/f49e75b250880623fa487fffc43ba1ff_73.png)

---

![](img/f49e75b250880623fa487fffc43ba1ff_75.png)

![](img/f49e75b250880623fa487fffc43ba1ff_77.png)

![](img/f49e75b250880623fa487fffc43ba1ff_79.png)

![](img/f49e75b250880623fa487fffc43ba1ff_81.png)

## 总结 📚

![](img/f49e75b250880623fa487fffc43ba1ff_83.png)

本节课中我们一起学习了：
1.  **特殊方法**：`__repr__` 用于提供明确的对象表示，`__str__` 用于提供可读的对象表示。
2.  **运算符重载**：通过定义像 `__sub__` 这样的魔法方法，可以让自定义对象支持内置运算符，使代码更直观。
3.  **继承**：通过创建子类来扩展现有类的功能，实现代码复用和层次化设计。
4.  **`super()` 函数**：在子类中调用父类方法的推荐方式，使代码更健壮，尤其在复杂的继承关系中。

![](img/f49e75b250880623fa487fffc43ba1ff_85.png)

![](img/f49e75b250880623fa487fffc43ba1ff_87.png)

![](img/f49e75b250880623fa487fffc43ba1ff_89.png)

![](img/f49e75b250880623fa487fffc43ba1ff_91.png)

![](img/f49e75b250880623fa487fffc43ba1ff_92.png)

这些概念是构建模块化、可维护和表达力强的面向对象程序的基础，将在后续项目（如蚂蚁模拟项目）中发挥重要作用。