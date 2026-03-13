# 13：面向对象编程入门

![](img/939be759790d70cf46cdfe5c4aaa6808_0.png)

在本节课中，我们将要学习面向对象编程的基础知识。我们将探讨为什么以及如何使用类、`__init__`方法和`self`关键字来构建程序，以更清晰地模拟现实世界中的实体和关系。

上一节我们介绍了课程安排和期中考试信息，本节中我们来看看面向对象编程的核心概念。

## 🧱 什么是面向对象编程？

面向对象编程是一种主流的编程范式，旨在解决如何将现实世界中的结构映射到代码中的问题。对象本身是一种数据结构，它允许我们表示某种概念（例如汽车、银行账户），并组织与该数据相关的各种事物。

对象具有**状态**（即属性，如银行账户的余额、汽车的车轮数）和**方法**（即可以对该对象执行的操作，如汽车可以驾驶、银行账户可以存款或取款）。这些概念使我们能够以更可读、更易维护的方式构建代码，并澄清我们将要使用的各种函数之间的关系。

## 📐 类与实例

在面向对象编程中，一个核心区别是**类**和**实例**。

*   **类**：可以看作是对象的模板或蓝图。它定义了某一类事物共有的属性和方法。例如，“汽车”类定义了所有汽车共有的属性（如燃料、速度）和方法（如驾驶、停车）。
*   **实例**：是类的具体实现。一个类可以创建多个实例，每个实例都拥有自己独立的属性值。例如，根据“汽车”类，我们可以创建一辆红色迷你库珀和一辆蓝色甲壳虫，它们共享相同的方法，但颜色等属性值不同。

**公式**：`对象 = 类的实例`

## 🐍 Python 中的类：语法预览

在Python中，我们使用`class`关键字来定义类。类名通常以大写字母开头，这是一种约定俗成的规范。

以下是定义一个简单银行账户类的预览：

![](img/939be759790d70cf46cdfe5c4aaa6808_2.png)

![](img/939be759790d70cf46cdfe5c4aaa6808_4.png)

```python
class BaseAccount:
    def __init__(self, name, initial_deposit):
        self._name = name
        self._balance = initial_deposit

    def balance(self):
        return self._balance

    def withdraw(self, amount):
        self._balance -= amount
```

![](img/939be759790d70cf46cdfe5c4aaa6808_6.png)

以下是代码中三个关键元素的解释：

![](img/939be759790d70cf46cdfe5c4aaa6808_8.png)

1.  **`class`关键字**：用于声明一个新的类。
2.  **`__init__`方法**：这是一个特殊方法（以双下划线开头和结尾），称为构造方法。当你创建类的新实例时，Python会自动调用它。它用于初始化对象的属性。
3.  **`self`参数**：它代表类的当前实例。在类的方法内部，我们通过`self.属性名`来访问或修改该实例的属性。在调用方法时，我们不需要显式传递`self`参数，Python会自动处理。

![](img/939be759790d70cf46cdfe5c4aaa6808_10.png)

![](img/939be759790d70cf46cdfe5c4aaa6808_12.png)

![](img/939be759790d70cf46cdfe5c4aaa6808_13.png)

![](img/939be759790d70cf46cdfe5c4aaa6808_15.png)

## 🔧 创建和使用对象

![](img/939be759790d70cf46cdfe5c4aaa6808_17.png)

![](img/939be759790d70cf46cdfe5c4aaa6808_19.png)

让我们看看如何实际使用上面定义的`BaseAccount`类。

![](img/939be759790d70cf46cdfe5c4aaa6808_21.png)

```python
# 创建一个BaseAccount类的实例
my_account = BaseAccount("CS88", 100)

![](img/939be759790d70cf46cdfe5c4aaa6808_23.png)

![](img/939be759790d70cf46cdfe5c4aaa6808_25.png)

# 访问属性（注意：单下划线是约定，表示“内部使用”，但Python不强制）
print(my_account._name)  # 输出: CS88
print(my_account._balance) # 输出: 100

![](img/939be759790d70cf46cdfe5c4aaa6808_27.png)

![](img/939be759790d70cf46cdfe5c4aaa6808_28.png)

# 调用方法
print(my_account.balance()) # 输出: 100
my_account.withdraw(42)
print(my_account.balance()) # 输出: 58
```

![](img/939be759790d70cf46cdfe5c4aaa6808_30.png)

**重要提示**：当我们调用`my_account.balance()`时，Python在幕后将其转换为`BaseAccount.balance(my_account)`。`self`参数被自动设置为`my_account`这个实例。

![](img/939be759790d70cf46cdfe5c4aaa6808_32.png)

## 🛡️ 属性访问：公有与私有

![](img/939be759790d70cf46cdfe5c4aaa6808_34.png)

在类中，我们可以控制属性的可见性。

*   **单下划线前缀（如`_balance`）**：这是一种约定，提示其他程序员“这个属性主要供类内部使用，请勿直接修改”。但Python并不会阻止你从外部访问它。
*   **双下划线前缀（如`__value`）**：这会让Python对属性名称进行特殊处理（名称修饰），使其难以从类的外部直接访问。这用于实现更强的“私有性”，但目的主要是避免子类中的命名冲突，而非严格的安全限制。

![](img/939be759790d70cf46cdfe5c4aaa6808_36.png)

![](img/939be759790d70cf46cdfe5c4aaa6808_37.png)

![](img/939be759790d70cf46cdfe5c4aaa6808_39.png)

![](img/939be759790d70cf46cdfe5c4aaa6808_41.png)

![](img/939be759790d70cf46cdfe5c4aaa6808_43.png)

示例：
```python
class Test:
    def __init__(self):
        self.__value = 100 # 双下划线，私有属性

    def show_value(self):
        return self.__value # 在类内部可以访问

![](img/939be759790d70cf46cdfe5c4aaa6808_45.png)

![](img/939be759790d70cf46cdfe5c4aaa6808_47.png)

thing = Test()
print(thing.show_value()) # 输出: 100，通过公有方法访问
# print(thing.__value)    # 这行会报错：AttributeError
```

![](img/939be759790d70cf46cdfe5c4aaa6808_49.png)

## 🌐 类属性与实例属性

到目前为止，我们讨论的属性（如`_balance`）都属于**实例属性**，每个实例都有自己独立的一份。

有时，我们需要一些属于类本身、被所有实例共享的数据，这时就需要**类属性**。

![](img/939be759790d70cf46cdfe5c4aaa6808_51.png)

```python
class BaseAccountTwo:
    # 类属性
    account_number_seed = 1000

    def __init__(self, name):
        self._name = name
        # 使用类属性为当前实例分配一个账号，然后递增类属性
        self._account_number = BaseAccountTwo.account_number_seed
        BaseAccountTwo.account_number_seed += 1

    def account_number(self):
        return self._account_number

![](img/939be759790d70cf46cdfe5c4aaa6808_53.png)

![](img/939be759790d70cf46cdfe5c4aaa6808_55.png)

# 创建实例
acc1 = BaseAccountTwo("CS61B")
acc2 = BaseAccountTwo("Data 100")

print(acc1.account_number()) # 输出: 1000
print(acc2.account_number()) # 输出: 1001
print(BaseAccountTwo.account_number_seed) # 输出: 1002
```

![](img/939be759790d70cf46cdfe5c4aaa6808_57.png)

![](img/939be759790d70cf46cdfe5c4aaa6808_59.png)

![](img/939be759790d70cf46cdfe5c4aaa6808_61.png)

在这个例子中，`account_number_seed`是一个类属性。每次创建新账户时，我们都用它来分配一个唯一的账号，并使其递增。这个计数器由所有`BaseAccountTwo`实例共享。

![](img/939be759790d70cf46cdfe5c4aaa6808_63.png)

![](img/939be759790d70cf46cdfe5c4aaa6808_64.png)

![](img/939be759790d70cf46cdfe5c4aaa6808_65.png)

![](img/939be759790d70cf46cdfe5c4aaa6808_67.png)

## 📚 总结

![](img/939be759790d70cf46cdfe5c4aaa6808_69.png)

![](img/939be759790d70cf46cdfe5c4aaa6808_71.png)

本节课中我们一起学习了面向对象编程的基础。我们了解了**类**作为蓝图和**对象**作为具体实例的概念。我们掌握了在Python中定义类所需的三个核心语法：`class`关键字、`__init__`构造方法和`self`参数。我们还区分了**实例属性**（每个对象独有）和**类属性**（所有对象共享），并简单了解了使用单下划线和双下划线来控制属性访问的约定。

![](img/939be759790d70cf46cdfe5c4aaa6808_73.png)

![](img/939be759790d70cf46cdfe5c4aaa6808_75.png)

下一讲，我们将探讨**继承**，这是面向对象编程中让类之间建立联系、共享和扩展功能的核心机制。