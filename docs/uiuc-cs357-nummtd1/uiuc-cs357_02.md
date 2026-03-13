# Python

> 原文：[`cs357.cs.illinois.edu/textbook/notes/python.html`](https://cs357.cs.illinois.edu/textbook/notes/python.html)



查看幻灯片



如果你在这里看不到 PDF，请点击 这里 下载 PDF。

## 学习目标

+   熟悉 Python 3 语法

+   理解可变对象和不可变对象之间的区别

+   理解 NumPy 的用途，并了解 NumPy 数据类型的一些常见操作。

## 注意事项

1.  记住，学习编程语言最有效的方法是实践！

1.  Google 是任何编程语言的绝佳资源。

## 类型

就像任何其他语言一样，Python 中的变量可以存储不同类型的数据，例如 `int`、`float` 或 `str`。我们可以使用 `type()` 函数来查找表达式的类型。

### 示例

```py
a = 2
b = 3.0
c = a + b
d = 2 * a 
```

变量 `c` 和 `d` 的正确类型是什么？

$$\begin{flalign} & \text{A) } \text{c 是浮点数，d 是浮点数} \\ & \text{B) } \text{c 是浮点数，d 是整数} \\ & \text{C) } \text{c 是整数，d 是整数} \\ & \text{D) } \text{c 是整数，d 是浮点数} \\ \end{flalign}$$ 

**答案**



**B.**

在 Python 中，任何整数和浮点数之间的操作都会得到浮点数。因此，c 是浮点数。d 是整数，因为我们对两个整数进行了乘法运算。

## 名称和值

考虑以下示例：

```py
a = [1, 2, 3]
b = a 
```

在这种情况下，`a` 和 `b` 虽然是不同的变量，但它们并不是独立的实体。列表 `[1, 2, 3]` 是一个对象，变量名 a 和 b 都绑定到同一个列表上。

### 修改对象

现在让我们考虑另一个例子：

```py
a = [1, 2, 3]
b = a
b.append(4) 
```

`b.append(4)` 修改了对象列表，使得列表现在是 `[1, 2, 3, 4]`。我们知道 b 现在是 `[1, 2, 3, 4]`，但变量名 a 发生了什么变化？



**答案**

因为 a 和 b 绑定到同一个列表，一旦列表被修改，它们将具有相同的值。

### 获取对象的 "id"

让我们看看如何使用内置的 Python 函数来查看 a 和 b 是否指向同一个对象。

```py
# Since "a" and "b" are bounded to the same list object, they will have the same "id" print(id(a), id(b))

# The "is" keyword is an additional check to see if both variable names have the same "id" a is b 
```

### 内存管理

为了回顾 Python 管理内存的方式，让我们看看以下示例：

```py
# The following code will print "IS  False" and "EQUAL True" because a and b are bounded to two different list objects.
# Hence, they don't have the same id but the contents of their data are the same. 
a = [1, 2, 3]
b = [1, 2, 3]
print("IS  ", a is b)
print("EQUAL", a == b)

# The following code is the case we've seen before. 
# a and b are bounded to the same list object, and hence they'll have the same id. 
a = [1, 2, 3]
b = a 
```

### 可变和不可变对象

在 Python 中，对象分为 **可变** 和 **不可变**。可变对象在创建后可以被修改，包括列表、字典、NumPy 数组等。不可变对象一旦创建后就不能被修改，包括元组、字符串、浮点数等。

例如，

```py
# A successful attempt to replace the first entry of the list 
myList = [3, 5, 7]
myList[0] = 1

# The following two attempts will result in a TypeError: object does not suppoer item assignment 
myTuple = (3, 5, 7)
myTuple[0] = 1

myString = "357"
myString[0] = '1' 
```

#### 列表

列表是可变对象的一个例子。让我们看看它在不同情况下是如何表现的：

```py
# Again, the case we've seen before: a and b are bounded to the same list object 
a = [1, 2, 3]
b = a

# Here, our variable a gets reassigned to a new object, but b is still bounded to the initial object 
a = a + [4]
print(b)
print(a)
a is b      # evaluates to False 

# In this case, the object list is modified, however, a and b remain bounded to the object 
a += [4]
print(b)
print(a)
a is b      # evaluates to True 
```

### 示例

以下代码片段中哪个会导致 `print(a==c) -> True`:

A:

```py
a = ['hello','goodbye']
b = 'hey'
a.append(b)
c = a + [b] 
```

B:

```py
a = ['hello','goodbye']
b = 'hey'
c = a + [b]
a += b 
```

C:

```py
a = ['hello','goodbye']
b = 'hey'
c = a + [b]
a.append(b) 
```



**答案**



**C**

A 是不正确的，因为 `c` 的列表中最终有两个 "hey" 元素。B 是不正确的，因为 `a += b` 将 "hey" 的每个字符都作为其自己的元素添加。因此，C 必须是正确的选择。

## 对象和命名

### 高级命名

让我们创建一些对象，并查看在接下来的代码片段中会发生什么：

```py
fruit = 'apple'

lunch = []
lunch.append(fruit)       # lunch = ['apple'] 
dinner = lunch            # dinner = ['apple'], lunch = ['apple'] dinner.append('fish')     # dinner = ['apple', 'fish'], lunch = ['apple', 'fish'] 
fruit = 'pear'            

meals = [fruit, lunch, dinner] 
print(meals)              # meals = ['pear', ['apple', 'fish'], ['apple', 'fish']] 
```

### 示例

以下代码片段的正确输出是什么？

```py
John = 'computer_science'
Tim = John
Tim += ', math'
Anna = ['electrical']
Julie = Anna
Julie += ['physics']
print(John, Anna) 
```

A: `computer_science, math ['electrical', 'physics']`

B: `computer_science, math ['electrical']`

C: `computer_science ['electrical', 'physics']`

D: `computer_science ['electrical']`



**答案**



**C**

在上面的代码片段中，由于 Python 中字符串是不可变的，John 和 Tim 指的是不同的对象，因此变量 John 等于`'computer_science'`。列表是可变的，所以 Julie 和 Anna 等于同一个列表：`['electrical', 'physics']`。因此，C 是正确的选择。

## 索引

索引在 Python 中通过多种方式遍历 for 循环非常重要。给定一个列表`a`，索引的格式遵循以下标准：`a[i:j:k]`。在这里，`i`是迭代的起始索引，`j`是迭代的停止索引（不包括），`k`是步长。

### 示例

```py
a = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
a[1::2][::-1] 
```

上面的命令行输出是什么？

$$\begin{flalign} & \text{A) } [1, 3, 5, 7, 9] \\ & \text{B) } [1, 3] \\ & \text{C) } [3, 1] \\ & \text{D) } [9, 7] \\ & \text{E) } [9, 7, 5, 3, 1] \\ && \end{flalign}$$ 

**答案**



$\bf E$

第一步是获取数组 a[1::2]的结果数组。在零索引数组中，起始索引是 1，步长是 1 直到数组的末尾（因为没有给出停止索引）。因此，结果数组是[1, 3, 5, 7, 9]，我们现在将其称为数组 b。

最后一步是获取数组 b[::-1]的结果数组。没有给出起始或停止索引，但步长是-1。这意味着我们只需要反转数组 b，因为负步长意味着我们从数组的末尾开始迭代，而不是从开始迭代。因此，最终的数组将是[9, 7, 5, 3, 1]，这等于答案选项 E。

## 控制流程

控制流程包括使用 for/while 循环遍历类似列表的对象，使用 if/else 块执行特定条件的逻辑，以及使用 break 和 continue 语句来控制何时退出 for 循环或移动到循环的下一个迭代。让我们看看这个简单示例：

```py
# builds a list of the squares of integers below 50 divisible by 7 
mylist = []
for i in range(50):

  if i % 7 == 0:
    mylist.append(i**2)

# does this using something called list comprehension, a concise and easy way to write the code block above 
mylist = [i**2 for i in range(50) if i % 7 == 0]
print(mylist) 
```

## 函数

### 定义函数

有时定义一个函数是有用的。这是通过使用关键字"def"后跟参数列表来完成的。以下是一个函数定义的基本示例：

```py
# a function to return the area of a square def area(length):
  return length ** 2

print(area(2)) 
```

这是关于函数定义的[官方文档](https://docs.python.org/3.8/tutorial/controlflow.html#defining-functions)。

### 函数作用域

理解作用域的概念很重要。在函数内部创建的变量只能在该函数内部使用，因为它具有**局部作用域**。在 Python 代码的主体中创建的变量是全局变量，因此具有**全局作用域**。这个变量没有限制，可以在任何地方使用/访问。再次强调，通过查看示例来学习这是最好的方法：

```py
def add_minor(person):
  person.append('math')

def switch_majors(person):
  person = ['physics']      # here, the person variable has a local scope, meaning its value/update only happens within the function, and is "ignored" outside of it
  person.append('economics')

# all variables created out here have a global scope 
John = ['computer_science']
Tim = John
add_minor(Tim)
switch_majors(John)
print(John, Tim) 
```

### 示例

哪个代码片段不会修改变量？

A

```py
a = [3, 4]
b = [6, 7]

def do_stuff(a, b):
  return (a.append(5), b.append(8))

do_stuff(a, b) 
```

B

```py
a = 3
b = 5

def do_stuff(a, b):
  a += 1
  b += 2

do_stuff(a, b) 
```

C

```py
a = [3, 4]
b = [6, 7]

def do_stuff(a, b):
  a += [5]
  b += [8]

do_stuff(a, b) 
```



**答案**



**B**

B 是正确答案，因为在 Python 中`ints`是不可变的。这意味着在函数内部将`a`增加 1 和将`b`增加 2 只会为 a 和 b 创建新的对象。这些新对象将限制在函数的作用域内，因此变量不会被修改。

然而，列表是可变对象，向其中添加值并不会创建新的对象。函数只是更新已经具有全局作用域的变量，因此这些变量被修改。

## 字典

字典是 Python 中重要且有用的结构。字典由键值对组成，其中值是通过键提取的。你将在本课程中大量使用字典，尤其是在后面的章节中。以下是一些使用字典的示例：

```py
# definition of a dictionary myDict = {
    "number": 357,
    "major": "computer science",
    "credit hours": 3
}

# dictionaries are mutable, thus can be modified, either modifying an existing value or creating a new key myDict["major"] = "math"
myDict["level"] = "undergrad"

# looping through the keys or the values over the dictionary for x in myDict:
  print(x)
  print(myDict[x])

for x in myDict.values():
  print(x)

# there are multiple ways to remove an existing entry, here is one example myDict.pop("level")

# copy an existing dictionary into a new reference anotherDict = myDict.copy() 
```

这里是[官方文档](https://docs.python.org/3/tutorial/datastructures.html#dictionaries)关于字典和一些其他有用的数据结构。

## 类型注解

Python 是一种动态类型语言，这意味着变量的类型是在运行时确定的。正如你可能已经注意到的，这就是为什么我们有声明和初始化变量而不必为变量分配类型的奢侈。在 C++或 Java 这样的语言中，这是不允许的。

**类型注解**，然而，为开发者提供了一种指定变量、函数参数或函数结果类型的方法。虽然它并不真正提高性能，但它有助于开发者更好地理解他们正在处理的数据类型，无论是变量还是函数调用的输入和输出。以下是一个类型注解变量/函数定义的示例：

```py
# simple variable declaration (the type we're used to) a = 5

# type annotated variable declaration a: int = 5

# simple function definition (the type we're used to) def add_two_numbers(a, b):
  return a + b

# type annotated function definition (both inputs and output) def add_two_numbers(a: int, b: int) -> int:
  return a + b 
```

## NumPy

NumPy 是一个用于数值计算的 Python 库。它几乎完全用 C 和 C++开发，性能极高，可以轻松支持大量数据的操作。本节将简要介绍一些你将在整个课程中使用的常见 NumPy 工具。虽然本节将解释一些这些常见工具，但[NumPy 文档](https://NumPy.org/doc/)提供了更详细的说明，并且始终是当你不确定如何使用特定函数时的首选资源。

### NumPy 数组

NumPy 数组通常比列表更受欢迎，因为你可以对它们进行高度性能的操作以完成任何任务。这在数值方法这样的课程中尤为重要。以下是你可以初始化不同类型 NumPy 数组的方法：

```py
import numpy as np
# creates a 2d array of zeros (conceptually a matrix) that has shape 2 x 2 np.zeros((2, 2))

# creates a 2d array of ones (conceptually a matrix) that has shape 2 x 2 np.ones((2, 2))

# creates an array of numbers that are evenly spaced between 2 and 3 (4 numbers in this case) np.linspace(2, 3, 4)

# creates a 2d array of random numbers between 0 and 1 that has shape 2 x 2 np.random.rand(2, 2)

# creates an empty 2d array (conceptually a matrix) that has shape 2 x 2 np.empty((2, 2)) 
```

我们可以使用以下函数找到有关 NumPy 数组的更多信息，并对其进行更多操作：

```py
import numpy as np
a = np.zeros((2, 2))

# we can get the shape of our NumPy array with the following function print(a.shape)        # will return (2, 2) 
# this will give us the data type of the array elements print(a.dtype)        # returns float 
# If we want to convert each element in the array to an int instead of float, we can perform the following operation: a = a.astype(int)
print(a.dtype)        # returns int 
# this creates a deep copy of the array, so changing one won't affect the other b = a.copy() 
```

### 索引和切片

我们可以使用 NumPy 数组上的索引和切片来提取数组/矩阵中的特定信息。这将成为课程的一个固定部分，所以现在就习惯使用索引/切片会更好！注意，本节与上面的索引部分类似。NumPy 数组 a 将遵循以下标准：`a[i:j:k]`，其中`i`是迭代的起始索引，`j`是迭代的停止索引（不包括），`k`是步长。

```py
import numpy as np
a = np.array([3, 7, 9, 10, 3, 5])
b = np.array([[1, 2, 3], [4, 5, 6]])

# basic indexing for both 1d and 2d NumPy arrays (for 2d arrays we specify both the row and col) print(a[2])     # prints 9 print(b[0, 0])  # prints 1 
# slicing examples for both 1d and 2d NumPy arrays (for 2d arrays we specify both the row and col) print(a[1:3])     # prints [7, 9] print(b[0:1, 2])  # prints [3] 
# If we leave the row/col index empty or use a colon(:) then we're saying that we select the entire row/col print(b[:1])      # this assumes the starting index of the row is 0, so we select the entire first row, prints [[1, 2, 3]] 
```

### 数组操作

数组操作在后续章节中某些公式需要构建矩阵或对矩阵执行某些操作（例如，转置矩阵）时特别有用。以下是一些示例：

```py
import numpy as np
a = np.array([3, 7, 9, 10, 3, 5])
b = np.array([[1, 2, 3], [4, 5, 6]])

# we can reshape an array as long as the new shape has the same number of elements as the original shape b = np.reshape(b, (6, 1))
a = np.reshape(a, (3, 2))

# we can flatten an array so that all the elements are collapsed into one dimension a = a.flatten()

# we can get the transpose of a NumPy array via the following command a_transpose = a.T 
```

### 数组数学

NumPy 提供了一些可以在数组中的每个元素上执行数学函数。而不是遍历每个元素，这些函数将在整个数组上执行操作，因此非常方便。在数值方法中哪些数学函数可能是相关的？让我们看看：

```py
import numpy as np
a = np.array([[8, 9]])
b = np.array([[1, 2, 3], [4, 5, 6]]) 

# The most important operation you'll do is matrix multiplication, we can do this easily in 2 ways c = np.dot(a, b)
# or c = a @ b

# We can do a lot of other operations d = np.sin(a)
e = np.cos(a)
f = np.exp(a)
g = np.sum(a)
h = np.mean(a)
i = np.min(a) 
```

### 线性代数

这个课程通常会要求你在向量/矩阵上执行线性代数操作。这就是`numpy.linalg`库和它提供的以下函数将非常有用的地方：

```py
import numpy.linalg as la

# To take the matrix inverse of a matrix A: matrix_inv = la.inv(A)

# To get the eigenvalues/eigenvectors of a matrix A: eigval, eigvec = la.eig(A)

# To calculate the norm of a vector or a matrix A: vec_norm = la.norm(A)   # can specify what type of norm as an additional param 
# To solve linear equations for an equation Ax = b x = la.solve(A, b) 
```

### 随机数

随机数总是数值方法的一个基本组成部分。NumPy 提供了几个函数，使得使用随机数变得非常简单，这在蒙特卡洛等章节中将是关键。让我们深入了解 NumPy 为随机数提供了什么：

```py
import numpy as np
# Generating random numbers from 0 to 1: a = np.random.rand(3, 2)    # creates a 3 x 2 array that is populated with random nums from 0 to 1 
# Generating a random integer from 0 to 100: b = np.random.randint(100)

# Generate a random value based on an array of values: c = np.random.choice([1, 2, 3, 4])      # will randomly return one of the values within the array 
```

Python 还有一个与 NumPy 分开的随机模块，但可以用来执行与上面介绍的操作非常相似的操作。

### 广播

广播是 Python 中的一个强大技术，它允许我们在形状不同的两个数组之间执行算术运算。

假设我们有一个较小的数组**A**（形状为 1 x 5）和一个较大的数组**B**（形状为 4 x 5），我们想要将这些数组相加。

没有广播，只有 B 的第一行会被 A 修改。然而，有了广播，A 的值会被添加到 B 的每一行。因此，A 被广播到 B 上。维度大小需要像这个例子中那样协作，否则在执行这个算术运算时我们会收到一些错误。

这里有一个示例来说明这个概念：

```py
import numpy as np

A = np.array([[1, 2, 3, 4, 5]])
B = np.array([
    [10, 20, 30, 40, 50],
    [60, 70, 80, 90, 100],
    [110, 120, 130, 140, 150],
    [160, 170, 180, 190, 200]
])

# Add A to B using broadcasting C = B + A

# C = np.array([[ 11,  22,  33,  44,  55],
#        [ 61,  72,  83,  94, 105],
#        [111, 122, 133, 144, 155],
#        [161, 172, 183, 194, 205]]) 
print(C) 
```

这个结果展示了如何将数组 A 的值添加到数组 B 的每一行，这得益于广播。A 的维度（1 x 5）与 B（4 x 5）兼容，使得 A 能够“拉伸”到 B 上以执行逐元素加法。 ​​

## 外部链接

这里有一些我们将要在 CS 357 中使用其他包的文档。

+   [SciPy，一个用于解决数学问题的科学计算包](https://docs.scipy.org/doc/scipy/reference/)

+   [MatPlotLib，一个用于可视化和图形的包](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.html#module-matplotlib.pyplot)

## 更新日志

+   2024 年 3 月 17 日：Dev Singh（dsingh14）——修改了笔记内容以提高清晰度

+   2024 年 3 月 16 日：Arnav Aggarwal (arnava4) — 将笔记与幻灯片对齐并添加了额外的示例

+   

查看剩余条目



## 作者

+   CS 357 课程工作人员
