# 19：Python异常处理 🐛

![](img/174a462c3d0a84dc54709a59c8e3a1f5_0.png)

![](img/174a462c3d0a84dc54709a59c8e3a1f5_1.png)

![](img/174a462c3d0a84dc54709a59c8e3a1f5_3.png)

在本节课中，我们将要学习Python中的异常处理。异常是程序运行时发生的错误，理解如何捕获、处理和创建异常对于编写健壮的代码至关重要。我们将从认识常见的异常类型开始，逐步学习如何使用`try`和`except`来优雅地处理错误，以及如何创建自定义异常来满足特定需求。

## 认识Python异常

在编程过程中，错误几乎无处不在。最常见的错误之一是语法错误，它在代码运行前就会发生，通常是由于拼写错误或格式不正确导致的。Python会明确指出这是语法错误。

然而，在程序内部，错误可能因多种原因随时发生。一个常见的情况是调用函数时传递了错误的参数，例如参数数量不对、类型不匹配（如传递数字而非字符串），或者使用了不兼容的数据结构（如向期望列表的函数传递字典）。这些情况都会引发错误或异常。

除了课程作业，在实际应用中，你可能会遇到文件不存在、网络连接中断等情况。程序需要有能力处理和响应这些异常。本节课的目标就是学习Python处理异常的底层机制。

![](img/174a462c3d0a84dc54709a59c8e3a1f5_5.png)

## 异常的类型与回溯

Python中的“错误”和“异常”通常可以互换使用。当Python无法执行某项操作时，它会抛出一个异常。例如，尝试除以零会引发`ZeroDivisionError`。

![](img/174a462c3d0a84dc54709a59c8e3a1f5_7.png)

```python
>>> 10 / 0
ZeroDivisionError: division by zero
```

异常信息通常包含两部分：一个技术性的异常名称（如`ZeroDivisionError`）和一个易于理解的描述信息（如`division by zero`）。这为我们提供了解决问题的初步线索。

![](img/174a462c3d0a84dc54709a59c8e3a1f5_9.png)

另一个例子是`AttributeError`，它表示尝试访问对象不存在的属性。

![](img/174a462c3d0a84dc54709a59c8e3a1f5_11.png)

```python
>>> num = 100
>>> num.lower()
AttributeError: 'int' object has no attribute 'lower'
```

常见的异常类型包括：
*   **`TypeError`**：数据类型不匹配。
*   **`IndexError`**：访问列表、字符串等序列时索引超出范围。
*   **`KeyError`**：访问字典中不存在的键（类似于列表的`IndexError`）。
*   **`RuntimeError`**：程序运行时发生的各种问题的统称。

当异常发生时，程序的正常执行流程会中断。理解如何从这种中断中恢复是异常处理的核心。

## 解读回溯信息

![](img/174a462c3d0a84dc54709a59c8e3a1f5_13.png)

![](img/174a462c3d0a84dc54709a59c8e3a1f5_15.png)

当在文件中运行代码并发生异常时，Python会输出一个“回溯”信息，它展示了导致错误的函数调用链。

回溯信息通常以“Traceback (most recent call last):”开头，意思是“最近一次调用在最后”。调试时，你应该**从最后一行开始向上阅读**。最后一行指出了错误最初发生的位置（文件和行号），然后向上追溯是哪些函数调用了它。

![](img/174a462c3d0a84dc54709a59c8e3a1f5_17.png)

例如，一个回溯可能显示错误发生在`module`文件的第14行，该行在`get_age_in_days`函数内，而该函数又被第20行的代码调用。通过这种方式，你可以追踪错误的完整路径。

![](img/174a462c3d0a84dc54709a59c8e3a1f5_19.png)

在不同的开发环境（如终端、Jupyter Notebook、Python Tutor）中，回溯信息的展示方式可能略有不同，但基本结构和调试原则是相同的。

## 使用 try 和 except 捕获异常

上一节我们认识了异常及其回溯。本节中，我们来看看如何主动捕获并处理异常，防止程序崩溃。这通过`try`和`except`语句实现。

`try`块包含可能引发异常的代码。如果`try`块中的代码成功执行，则跳过`except`块。如果发生异常，则立即跳转到匹配的`except`块执行处理代码。

![](img/174a462c3d0a84dc54709a59c8e3a1f5_21.png)

以下是一个基础示例，它尝试安全地进行除法运算：

![](img/174a462c3d0a84dc54709a59c8e3a1f5_23.png)

```python
def safely_divides(x, y):
    try:
        return x / y
    except:
        print("An error occurred")
        return False
```

![](img/174a462c3d0a84dc54709a59c8e3a1f5_25.png)

在这个例子中，如果除法成功（如`safely_divides(10, 5)`），函数返回结果`2.0`。如果发生任何异常（如除以零`safely_divides(10, 0)`），程序会打印信息并返回`False`，而不会崩溃。这使得我们可以继续执行后续代码，例如将结果赋值给变量。

## 捕获特定异常

![](img/174a462c3d0a84dc54709a59c8e3a1f5_27.png)

![](img/174a462c3d0a84dc54709a59c8e3a1f5_29.png)

![](img/174a462c3d0a84dc54709a59c8e3a1f5_31.png)

使用通用的`except:`会捕获所有类型的异常，但这有时可能掩盖了其他意料之外的问题。更好的做法是指定要捕获的异常类型。

我们可以修改代码，只捕获`ZeroDivisionError`：

![](img/174a462c3d0a84dc54709a59c8e3a1f5_33.png)

![](img/174a462c3d0a84dc54709a59c8e3a1f5_35.png)

```python
def safely_divides(x, y):
    try:
        return x / y
    except ZeroDivisionError as e:
        print(f"An error occurred: {e}")
        return False
```

这里，`except ZeroDivisionError`表示只捕获除以零的错误。`as e`将异常对象赋值给变量`e`，方便我们打印或检查其详细信息。现在，如果发生其他类型的错误（如`NameError`），它将不会被这个`except`块捕获，从而允许更上层的处理机制或直接中断程序，这有助于我们发现代码中的其他潜在错误。

![](img/174a462c3d0a84dc54709a59c8e3a1f5_37.png)

![](img/174a462c3d0a84dc54709a59c8e3a1f5_38.png)

## 使用断言

![](img/174a462c3d0a84dc54709a59c8e3a1f5_40.png)

有时，在错误发生之前，我们希望主动检查程序状态是否满足某些条件。这时可以使用`assert`（断言）语句。

![](img/174a462c3d0a84dc54709a59c8e3a1f5_42.png)

![](img/174a462c3d0a84dc54709a59c8e3a1f5_43.png)

![](img/174a462c3d0a84dc54709a59c8e3a1f5_45.png)

`assert`接受一个表达式和可选的错误信息。如果表达式为`True`，程序继续执行；如果为`False`，则立即引发`AssertionError`。

![](img/174a462c3d0a84dc54709a59c8e3a1f5_47.png)

![](img/174a462c3d0a84dc54709a59c8e3a1f5_49.png)

```python
def divides(x, y):
    assert y != 0, “Divisor cannot be zero!”
    return x / y
```

![](img/174a462c3d0a84dc54709a59c8e3a1f5_51.png)

![](img/174a462c3d0a84dc54709a59c8e3a1f5_53.png)

![](img/174a462c3d0a84dc54709a59c8e3a1f5_55.png)

![](img/174a462c3d0a84dc54709a59c8e3a1f5_57.png)

在这个例子中，调用`divides(10, 0)`会触发断言，引发`AssertionError`并显示消息“Divisor cannot be zero!”。

![](img/174a462c3d0a84dc54709a59c8e3a1f5_59.png)

断言是调试和确保代码假设的强有力工具。例如，在处理数据时，你可以断言数据长度大于零，或某个计算结果在合理范围内。Python提供了一个特性，可以通过设置`__debug__`变量或使用`-O`（优化）标志运行脚本来全局禁用所有断言，这样你可以在开发阶段保留断言用于检查，在部署时关闭它们以提高性能。

![](img/174a462c3d0a84dc54709a59c8e3a1f5_61.png)

关于`try...except`和断言，需要注意：当`try`块中的代码（或断言）引发异常时，该块内剩余的代码将不会被执行，程序会直接跳转到对应的`except`块。

## 创建和抛出自定义异常

![](img/174a462c3d0a84dc54709a59c8e3a1f5_63.png)

除了使用内置异常，我们还可以定义自己的异常类，以更精确地表示程序中特定的错误情况。自定义异常通常继承自Python的基础`Exception`类。

定义自定义异常非常简单：

![](img/174a462c3d0a84dc54709a59c8e3a1f5_65.png)

![](img/174a462c3d0a84dc54709a59c8e3a1f5_67.png)

![](img/174a462c3d0a84dc54709a59c8e3a1f5_69.png)

```python
class CS88Error(Exception):
    pass
```

![](img/174a462c3d0a84dc54709a59c8e3a1f5_71.png)

现在，你可以在代码中使用`raise`语句抛出这个自定义异常：

```python
def get_age_in_days():
    age = float(input(“How old are you? “))
    if age < 10:
        raise CS88Error(“Are you sure you want to take CS88?“)
    print(f“You are at least {age * 365:.0f} days old.“)
    return age * 365
```

![](img/174a462c3d0a84dc54709a59c8e3a1f5_73.png)

![](img/174a462c3d0a84dc54709a59c8e3a1f5_75.png)

当调用`get_age_in_days()`且输入年龄小于10时，将抛出`CS88Error`。自定义异常使得错误类型更具语义，便于在复杂的项目中识别和处理特定问题。

你可以在更高级的异常处理逻辑中捕获并处理自定义异常，甚至可以捕获后执行一些操作，然后选择是否重新抛出（`raise`）该异常，让上层代码继续处理。

![](img/174a462c3d0a84dc54709a59c8e3a1f5_77.png)

![](img/174a462c3d0a84dc54709a59c8e3a1f5_79.png)

## 总结

![](img/174a462c3d0a84dc54709a59c8e3a1f5_81.png)

本节课中我们一起学习了Python异常处理的完整流程。

![](img/174a462c3d0a84dc54709a59c8e3a1f5_83.png)

我们首先认识了各种内置异常类型及其回溯信息，学会了如何从回溯的底部开始阅读以定位错误根源。接着，我们掌握了使用`try`和`except`结构来捕获和处理异常，确保程序在遇到预期内错误时能继续运行，并探讨了如何精确捕获特定异常。我们还学习了使用`assert`语句在代码中设置检查点，确保程序状态符合预期。最后，我们了解了如何通过继承`Exception`类来创建自定义异常，并使用`raise`语句抛出它们，从而使错误处理逻辑更加清晰和模块化。

![](img/174a462c3d0a84dc54709a59c8e3a1f5_85.png)

![](img/174a462c3d0a84dc54709a59c8e3a1f5_87.png)

通过结合这些技术，你可以编写出更健壮、更易于调试和维护的Python程序。