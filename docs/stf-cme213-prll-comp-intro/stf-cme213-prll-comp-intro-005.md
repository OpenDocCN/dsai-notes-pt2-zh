# 005：OpenMP 第二部分 🚀

在本节课中，我们将继续学习OpenMP，深入探讨任务（Tasks）的概念、同步机制、归约操作以及一些高级特性。我们将通过具体的代码示例来理解如何在实际问题中应用这些技术。

## 概述

上一节我们介绍了OpenMP的基本概念，特别是如何并行化`for`循环。本节中，我们将探讨当并行工作不适用于`for`循环结构时，如何使用OpenMP的“任务”模型。我们还将学习任务间的依赖关系、同步点、归约操作以及原子操作等关键概念。

## 任务（Tasks）模型

并非所有并行工作都适合用`for`循环来表达。例如，在处理树形结构遍历或链表遍历时，任务的生成是动态且递归的。OpenMP的任务模型为此类问题提供了解决方案。

### 树的前序遍历示例

以下是一个遍历二叉树并执行`visit`操作的递归函数。每个节点的访问操作是独立的，可以并发执行。

```c
void traverse(TreeNode* node) {
    if (node == nullptr) return;
    #pragma omp task
    visit(node); // 假设visit是独立操作
    traverse(node->left);
    traverse(node->right);
}
```

要使用OpenMP任务并行化此遍历，需要注意几个关键点：
1.  任务必须在一个**并行区域**内创建。
2.  通常需要结合`#pragma omp single`指令，确保生成初始任务的代码只由一个线程执行一次，避免重复生成任务。

正确的并行化代码如下：

```c
#pragma omp parallel
{
    #pragma omp single
    traverse(root);
}
```

在这个模型中，遇到`#pragma omp task`时，任务可能被立即执行，也可能被放入任务池稍后由空闲线程执行。这提供了灵活的负载均衡。

### 树的后序遍历与任务同步

后序遍历（先处理子节点，再处理父节点）引入了同步需求。父节点必须等待其子节点的任务完成后，才能进行后续操作（如累加子节点结果）。这时需要使用`taskwait`指令。

以下是计算二叉树节点总数的后序遍历示例：

```c
int post_order_traverse(TreeNode* node) {
    if (node == nullptr) return 0;
    int left_count = 0, right_count = 0;

    #pragma omp task shared(left_count)
    left_count = post_order_traverse(node->left);
    #pragma omp task shared(right_count)
    right_count = post_order_traverse(node->right);

    #pragma omp taskwait // 等待左右子节点的任务完成
    return left_count + right_count + 1;
}
```

**关于变量数据共享属性的重要区别**：
*   在普通的`parallel`区域中，外部变量默认是**共享**的。
*   在`task`构造中，外部变量默认是**firstprivate**的（即每个任务获得变量的私有副本，并以进入任务前的值初始化）。

因此，在上面的代码中，我们必须使用`shared(left_count)`显式指定`left_count`为共享变量，否则每个任务修改的将是自己的私有副本，导致计算结果错误。

### 链表遍历示例

任务模型也适用于`while`循环，例如遍历链表：

```c
void traverse_list(Node* head) {
    #pragma omp parallel
    {
        #pragma omp single
        {
            Node* current = head;
            while (current != nullptr) {
                #pragma omp task // current默认是firstprivate，符合预期
                process(current);
                current = current->next;
            }
        }
    }
}
```
这里，`current`指针在任务创建时被捕获其当前值（由于默认的`firstprivate`属性），即使主线程中的`current`随后移动，也不会影响已创建任务的操作对象。

## 任务依赖与同步

`taskwait`是一种粗粒度的同步，它等待**当前任务产生的所有子任务**完成。为了更精细地控制任务执行顺序，OpenMP引入了`depend`子句。

### 依赖子句详解

`depend`子句允许我们基于内存位置（变量）定义任务间的依赖关系。
*   `depend(in: x)`: 该任务**读取**变量`x`。它必须等待所有之前对`x`有`out`依赖的任务完成。
*   `depend(out: x)`: 该任务**写入**变量`x`。它必须等待所有之前对`x`有任何依赖（`in`或`out`）的任务完成。
*   `depend(inout: x)`: 组合了`in`和`out`的含义。
*   `depend(mutex: x)`: 任务间对`x`的操作互斥，不能同时执行，但顺序不限。

依赖关系建立了任务间的偏序关系，使得任务调度器能在满足依赖的前提下最大化并发。

### 关键路径与任务优先级

在任务图中，**关键路径**是指耗时最长的顺序执行路径，它决定了程序的最短可能运行时间。为了优化性能，应优先执行关键路径上的任务。OpenMP允许通过`priority`子句给任务提示优先级（数值越大优先级越高），但这是一个对调度器的提示，并非强制保证。

```c
#pragma omp task priority(high) // 高优先级任务
void critical_path_task() { /* ... */ }
```

## 归约操作

归约是将一组值通过一个操作（如加、乘、求最大值）合并成单个值的常见模式。OpenMP提供了高效的`reduction`子句来自动处理并行循环中的归约。

### 归约的原理与语法

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_1.png)

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_3.png)

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_5.png)

归约操作通过为每个线程创建私有变量副本，并行计算局部结果，最后在循环结束时将所有局部结果合并来实现。这避免了在共享变量上的数据竞争，并提高了缓存效率。

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_7.png)

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_8.png)

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_10.png)

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_12.png)

以下是一个计算数组和的并行循环：

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_14.png)

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_16.png)

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_18.png)

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_20.png)

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_22.png)

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_24.png)

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_26.png)

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_28.png)

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_30.png)

```c
double sum = 0.0;
#pragma omp parallel for reduction(+:sum)
for (int i = 0; i < n; ++i) {
    sum += array[i];
}
// 循环结束后，sum包含所有线程局部和的总和
```

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_32.png)

`reduction`子句的语法是：`reduction(operator: list)`
*   `operator`: 归约操作符，如`+`, `-`, `*`, `max`, `min`, `&` (位与), `|` (位或), `&&` (逻辑与), `||` (逻辑或)等。
*   `list`: 一个或多个用逗号分隔的变量名。

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_34.png)

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_36.png)

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_38.png)

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_40.png)

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_42.png)

### 归约练习：计算熵

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_44.png)

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_46.png)

假设我们有两个概率数组`p0`和`p1`，需要计算它们的熵并求和。这涉及多个循环和归约操作：
1.  归一化每个概率数组（求和）。
2.  计算每个归一化后分布的熵。
3.  对熵值进行求和。

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_48.png)

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_50.png)

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_52.png)

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_54.png)

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_56.png)

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_58.png)

以下是可能的实现框架：

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_60.png)

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_62.png)

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_64.png)

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_66.png)

```c
double entropy0 = 0.0, entropy1 = 0.0;
double sum0 = 0.0, sum1 = 0.0;
int n = /* 数组长度 */;

// 1. 计算概率和（归约）
#pragma omp parallel for reduction(+:sum0, sum1)
for (int i = 0; i < n; ++i) {
    sum0 += p0[i];
    sum1 += p1[i];
}
// 2. 归一化并计算熵（归约）
#pragma omp parallel for reduction(+:entropy0, entropy1)
for (int i = 0; i < n; ++i) {
    double norm_p0 = p0[i] / sum0;
    double norm_p1 = p1[i] / sum1;
    if (norm_p0 > 0) entropy0 -= norm_p0 * log(norm_p0);
    if (norm_p1 > 0) entropy1 -= norm_p1 * log(norm_p1);
}
double total_entropy_diff = entropy0 - entropy1;
```

**注意**：由于浮点数加法不满足结合律，使用不同线程数运行归约操作可能得到略有不同的结果，这是由舍入误差的累积顺序不同导致的。

## 原子操作与临界区

当多个线程需要更新同一个共享变量，且该操作不是简单的归约时（例如，根据条件有选择地更新），需要使用同步机制来保证正确性。

### 原子操作

`atomic`指令用于确保对特定内存地址的读-修改-写操作以原子方式执行。它比临界区开销小，但通常只支持简单的标量赋值或运算。

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_68.png)

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_70.png)

**N体问题示例**：计算所有粒子对之间的引力，并更新每个粒子的受力。
```c
#pragma omp parallel for
for (int i = 0; i < n; ++i) {
    for (int j = i+1; j < n; ++j) {
        Vec3 force = compute_force(particles[i], particles[j]);
        #pragma omp atomic
        particles[i].force.x += force.x;
        #pragma omp atomic
        particles[i].force.y += force.y;
        #pragma omp atomic
        particles[i].force.z += force.z;
        // 对 particles[j] 做相反的原子减操作
    }
}
```
原子操作适用于冲突较少的场景。如果大量线程频繁竞争同一内存地址，性能会严重下降。

### 临界区

`critical`指令定义一个临界区，确保每次只有一个线程能执行该段代码。它比`atomic`更通用，可以保护任意复杂的代码块，但开销也更大。

**查找素数示例**：并行检查一系列数是否为素数，并将素数插入一个共享的`std::set`。
```c
std::set<int> prime_set;
#pragma omp parallel for
for (int num = 2; num < limit; ++num) {
    if (is_prime(num)) {
        #pragma omp critical
        {
            prime_set.insert(num);
        }
    }
}
```

## 性能选择策略

在选择OpenMP并行化策略时，应遵循以下效率从高到低的顺序：
1.  **归约**：如果操作是标准的归约（如求和、求极值），使用`reduction`子句。
2.  **原子操作**：如果只是对单个标量变量进行简单的并发更新，使用`atomic`。
3.  **临界区**：如果需要保护复杂的代码段或非标量数据结构，使用`critical`。
4.  **手工加锁**：对于更复杂的同步需求，可以使用OpenMP的锁API，但这通常是最复杂且容易出错的方式。

## 总结

本节课我们一起深入学习了OpenMP的任务模型、同步机制和归约操作。
*   **任务模型** 为不规则并行问题（如树/图遍历、递归算法）提供了灵活的解决方案，我们学习了如何使用`task`、`taskwait`以及处理变量的数据共享属性。
*   **任务依赖** 允许我们定义精细的执行顺序，而`priority`提示有助于优化关键路径。
*   **归约操作** 是处理并行累加等模式的最高效方式，OpenMP能自动优化其实现。
*   **原子操作和临界区** 是解决非归约类数据竞争的基本工具，我们了解了它们的适用场景和性能差异。

![](img/c2a7cb4c105f1888eeaf9b3be0442a5c_72.png)

掌握这些概念后，你将能够利用OpenMP有效地并行化更广泛的应用程序。在接下来的课程中，我们将看到这些技术在实际算法和问题中的应用。