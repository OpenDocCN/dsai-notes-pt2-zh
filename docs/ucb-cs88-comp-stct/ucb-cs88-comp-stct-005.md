# 5：列表推导式与高阶函数

![](img/1c2c50300509721c3dd5b557262d0a95_1.png)

在本节课中，我们将学习Python中的两个核心概念：列表推导式和高阶函数。列表推导式提供了一种简洁高效的方式来创建和过滤列表。高阶函数则允许我们将函数作为参数传递，或者动态地创建和返回新函数，这是实现代码抽象和复用的强大工具。

## 列表推导式

上一节我们介绍了列表的基本操作，本节中我们来看看如何用更简洁的方式创建和转换列表。

![](img/1c2c50300509721c3dd5b557262d0a95_3.png)

列表推导式是Python的一个特性，它允许我们在一行代码内构建列表。我们可以将其视为一个“倒置”的`for`循环。通常的`for`循环是“对列表中的每个元素，执行某些操作”。而在列表推导式中，我们写的是“为列表中的每个元素执行某些操作，并将结果放入一个新列表”。

列表推导式的基本语法是：
```python
[expression for item in sequence]
```
其核心思想是让数据本身来驱动控制流程。这种方式通常比传统的`for`循环更简洁。

![](img/1c2c50300509721c3dd5b557262d0a95_5.png)

![](img/1c2c50300509721c3dd5b557262d0a95_6.png)

### 基础列表推导式

以下是列表推导式的一个简单示例。我们有一个课程列表：
```python
courses = ["CS 88", "DATA 8", "POLSCI 1", "MATH 1A"]
```
如果我们想提取每门课程的院系代码（即空格前的部分），可以使用列表推导式：
```python
departments = [c.split()[0] for c in courses]
# 结果：['CS', 'DATA', 'POLSCI', 'MATH']
```
在这个例子中，`c.split()[0]`是表达式，`for c in courses`是循环部分。列表推导式会遍历`courses`中的每个元素`c`，执行`c.split()[0]`，并将所有结果收集到一个新列表`departments`中。

![](img/1c2c50300509721c3dd5b557262d0a95_8.png)

### 带过滤条件的列表推导式

![](img/1c2c50300509721c3dd5b557262d0a95_10.png)

列表推导式更强大的功能在于可以添加过滤条件。其语法扩展为：
```python
[expression for item in sequence if condition]
```
只有满足`condition`的`item`，其对应的`expression`结果才会被放入新列表。

例如，生成一个0到19之间所有偶数的列表：
```python
even_numbers = [number for number in range(20) if number % 2 == 0]
# 结果：[0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
```
我们也可以将处理和过滤结合起来。例如，获取所有课程编号小于100的课程（即低年级课程）：
```python
lower_div_courses = [course for course in courses if int(course.split()[1]) < 100]
```
**注意**：在比较字符串形式的数字“88”和整数100之前，必须使用`int()`进行类型转换。

列表推导式是一个非常有用的工具，在后续的实验中你会经常用到它。当你需要将多行`for`循环逻辑浓缩为一行时，列表推导式通常是首选方案。

![](img/1c2c50300509721c3dd5b557262d0a95_12.png)

## 高阶函数

理解了如何高效地处理数据列表后，我们接下来探讨一个更抽象但极其强大的概念：高阶函数。高阶函数是能够接受其他函数作为参数，或者将函数作为返回值的函数。

### 函数作为数据

在Python中，函数本身也是一种数据。我们可以通过省略括号来引用函数对象本身，而不是调用它。
```python
print # 这是一个函数对象，而不是函数调用
p = print # 将函数对象赋值给变量p
p("Hello") # 通过变量p调用print函数
```
这种特性使得将函数作为参数传递给另一个函数成为可能。

![](img/1c2c50300509721c3dd5b557262d0a95_14.png)

![](img/1c2c50300509721c3dd5b557262d0a95_15.png)

### 接受函数作为参数的函数

![](img/1c2c50300509721c3dd5b557262d0a95_17.png)

![](img/1c2c50300509721c3dd5b557262d0a95_19.png)

![](img/1c2c50300509721c3dd5b557262d0a95_21.png)

![](img/1c2c50300509721c3dd5b557262d0a95_23.png)

![](img/1c2c50300509721c3dd5b557262d0a95_25.png)

假设我们有三个数学求和问题：
1.  求1到n的自然数之和：`sum(k)`
2.  求1到n的立方和：`sum(k^3)`
3.  用级数逼近π值：`sum(8 / ((4k-1)(4k-3)))`

![](img/1c2c50300509721c3dd5b557262d0a95_27.png)

![](img/1c2c50300509721c3dd5b557262d0a95_29.png)

如果为每个问题都写一个独立的求和函数，代码会大量重复。高阶函数可以帮助我们抽象出共同的“求和”模式。

首先，我们看一个普通的求和函数：
```python
def summation(n):
    total = 0
    for k in range(1, n+1):
        total += k
    return total
```
为了将其通用化，我们需要将“对k进行的操作”抽象出来。我们可以定义一个高阶函数，它接受一个函数`term`作为参数，这个`term`函数决定了如何计算每一项的值。
```python
def summation(n, term):
    total = 0
    for k in range(1, n+1):
        total += term(k) # 使用传入的term函数计算第k项的值
    return total
```
现在，我们只需要定义不同的`term`函数，就能解决上述三个问题：
```python
def identity(k):
    return k

![](img/1c2c50300509721c3dd5b557262d0a95_31.png)

def cube(k):
    return k ** 3

![](img/1c2c50300509721c3dd5b557262d0a95_33.png)

![](img/1c2c50300509721c3dd5b557262d0a95_35.png)

# 使用高阶函数求解
print(summation(5, identity)) # 计算1+2+3+4+5
print(summation(5, cube))     # 计算1^3+2^3+3^3+4^3+5^3
```
通过这种方式，我们成功地将变化的逻辑（如何计算每一项）封装在`term`函数中，而将不变的逻辑（求和循环）放在`summation`函数里，极大地提高了代码的复用性。

![](img/1c2c50300509721c3dd5b557262d0a95_37.png)

### 返回函数的函数

高阶函数的另一种形式是返回一个新函数。这意味着我们可以动态地“制造”函数。

![](img/1c2c50300509721c3dd5b557262d0a95_39.png)

![](img/1c2c50300509721c3dd5b557262d0a95_41.png)

![](img/1c2c50300509721c3dd5b557262d0a95_43.png)

![](img/1c2c50300509721c3dd5b557262d0a95_45.png)

![](img/1c2c50300509721c3dd5b557262d0a95_47.png)

![](img/1c2c50300509721c3dd5b557262d0a95_48.png)

![](img/1c2c50300509721c3dd5b557262d0a95_50.png)

![](img/1c2c50300509721c3dd5b557262d0a95_52.png)

例如，创建一个“小于等于”判断函数的生成器：
```python
def less_than_or_equal_maker(c):
    def lte(val):
        return val <= c
    return lte
```
这个函数接受一个参数`c`，然后在其内部定义了一个新函数`lte`。`lte`函数检查输入值`val`是否小于等于`c`。最后，`less_than_or_equal_maker`将`lte`函数作为结果返回。

![](img/1c2c50300509721c3dd5b557262d0a95_54.png)

![](img/1c2c50300509721c3dd5b557262d0a95_56.png)

![](img/1c2c50300509721c3dd5b557262d0a95_58.png)

我们可以这样使用它：
```python
lte_3 = less_than_or_equal_maker(3) # 得到一个判断是否<=3的函数
print(lte_3(5)) # 输出：False
print(lte_3(2)) # 输出：True
```
这里的关键在于，内部函数`lte`记住了它被创建时的环境，即参数`c`的值（在这个例子中是3）。这种“记住”外部变量的行为被称为**闭包**。

![](img/1c2c50300509721c3dd5b557262d0a95_60.png)

### 函数的组合

![](img/1c2c50300509721c3dd5b557262d0a95_62.png)

我们可以将两种高阶函数结合起来，创建更复杂的函数。例如，实现一个函数组合器，将两个加法函数组合成一个新的加法函数：
```python
def make_adder(n):
    def adder(k):
        return n + k
    return adder

def compose(f, g):
    def h(x):
        return f(g(x))
    return h

![](img/1c2c50300509721c3dd5b557262d0a95_64.png)

![](img/1c2c50300509721c3dd5b557262d0a95_66.png)

![](img/1c2c50300509721c3dd5b557262d0a95_68.png)

![](img/1c2c50300509721c3dd5b557262d0a95_70.png)

add_two = make_adder(2)
add_three = make_adder(3)
add_five = compose(add_two, add_three) # 组合成 add_two(add_three(x))

![](img/1c2c50300509721c3dd5b557262d0a95_72.png)

![](img/1c2c50300509721c3dd5b557262d0a95_74.png)

![](img/1c2c50300509721c3dd5b557262d0a95_76.png)

![](img/1c2c50300509721c3dd5b557262d0a95_78.png)

![](img/1c2c50300509721c3dd5b557262d0a95_80.png)

![](img/1c2c50300509721c3dd5b557262d0a95_81.png)

print(add_five(10)) # 输出：15 (相当于 2 + (3 + 10))
```
`compose`函数接受两个函数`f`和`g`作为参数，返回一个新函数`h`。当调用`h(x)`时，它会先计算`g(x)`，再将结果传递给`f`。这展示了高阶函数如何用于构建复杂的行为单元。

![](img/1c2c50300509721c3dd5b557262d0a95_83.png)

![](img/1c2c50300509721c3dd5b557262d0a95_85.png)

本节课中我们一起学习了列表推导式和高阶函数。列表推导式是处理列表数据的利器，能让代码更简洁。高阶函数则打开了函数式编程的大门，通过将函数视为“一等公民”，我们可以实现高度的代码抽象、复用和组合，这是构建复杂、灵活程序的基础。在接下来的课程和实验中，我们将继续探索这些概念的强大之处。