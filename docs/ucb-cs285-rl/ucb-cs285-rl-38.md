# 39：带约束的策略梯度实现 🚀

![](img/d9f6aced9bfaaf8419cdefab2d169d39_1.png)

在本节课中，我们将学习如何实际实现一个带有约束的策略梯度算法。我们将从理论推导转向具体实践，探讨如何将策略更新的约束条件（特别是KL散度）整合到优化过程中，从而构建出稳定且高效的强化学习算法。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_3.png)

---

![](img/d9f6aced9bfaaf8419cdefab2d169d39_5.png)

![](img/d9f6aced9bfaaf8419cdefab2d169d39_7.png)

## 从理论到实践：约束的实例化

![](img/d9f6aced9bfaaf8419cdefab2d169d39_9.png)

上一节我们介绍了策略性能改进的理论保证，其核心在于约束新旧策略的分布差异。为了实例化该算法，我们有一个关键前提：当策略 `π_θ` 接近 `π_θ'` 时，状态分布 `p_θ(s_t)` 也接近 `p_θ'(s_t)`。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_11.png)

![](img/d9f6aced9bfaaf8419cdefab2d169d39_13.png)

这里的“接近”最初被定义为**总变分距离**。然而，对于许多策略类别，直接强制总变分距离约束在实践中相当困难。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_15.png)

因此，我们需要一个更便于处理的边界。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_17.png)

![](img/d9f6aced9bfaaf8419cdefab2d169d39_18.png)

---

![](img/d9f6aced9bfaaf8419cdefab2d169d39_20.png)

## 引入KL散度作为约束 🔗

![](img/d9f6aced9bfaaf8419cdefab2d169d39_22.png)

我们可以推导出一个更便捷的边界。利用总变分距离与**KL散度**相关的不等式，我们可以用KL散度来约束总变分距离。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_24.png)

![](img/d9f6aced9bfaaf8419cdefab2d169d39_26.png)

这意味着，如果我们能限制策略 `π_θ'` 和 `π_θ` 之间的KL散度，那么根据该不等式，我们也就限制了状态边缘分布的差异。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_28.png)

![](img/d9f6aced9bfaaf8419cdefab2d169d39_30.png)

对于不熟悉KL散度的同学，它是衡量两个概率分布差异最广泛使用的度量之一。它非常方便，因为其表达式通常可以表示为对数概率的期望值。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_32.png)

**KL散度的公式**如下：
```
KL(π_θ' || π_θ) = E_{a~π_θ'} [ log π_θ'(a|s) - log π_θ(a|s) ]
```

许多连续值分布的KL散度甚至有封闭形式的解，这使得它在实际应用中非常方便。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_34.png)

![](img/d9f6aced9bfaaf8419cdefab2d169d39_36.png)

一种理解为何KL散度比总变分距离更易管理的方法是：总变分距离涉及绝对值，通常不可微；而只要两个分布的支持集相同，KL散度就是可微的。KL散度具备的这些优良性质，使其在实际强化学习算法中更容易近似和使用。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_37.png)

因此，在实际构建带约束的策略梯度方法时，我们将约束表达为KL散度，而非总变分距离。由于KL散度能限制总变分距离，这样做是合理的，并且保留了理论保证。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_39.png)

![](img/d9f6aced9bfaaf8419cdefab2d169d39_41.png)

---

![](img/d9f6aced9bfaaf8419cdefab2d169d39_43.png)

## 构建优化问题 🎯

![](img/d9f6aced9bfaaf8419cdefab2d169d39_45.png)

于是，我们要优化的目标函数是通常的重要性采样目标，同时附加一个约束：`π_θ'` 和 `π_θ` 之间的KL散度不超过一个阈值 `ε`。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_47.png)

![](img/d9f6aced9bfaaf8419cdefab2d169d39_49.png)

**优化目标**可以形式化为：
```
最大化：J(θ') = E [ (π_θ'(a|s) / π_θ(a|s)) * A^π_θ(s, a) ]
约束条件：KL(π_θ' || π_θ) ≤ ε
```
如果 `ε` 足够小，这将确保 `J(θ') - J(θ)` 得到改进，因为误差项被限制住了。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_51.png)

那么，我们如何强制执行这个约束呢？

![](img/d9f6aced9bfaaf8419cdefab2d169d39_53.png)

---

![](img/d9f6aced9bfaaf8419cdefab2d169d39_55.png)

![](img/d9f6aced9bfaaf8419cdefab2d169d39_57.png)

## 实施约束：拉格朗日对偶法 ⚙️

![](img/d9f6aced9bfaaf8419cdefab2d169d39_59.png)

有多种方法可以实施这个约束。一个非常直接的方法是写出这个约束优化问题的**拉格朗日函数**。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_61.png)

![](img/d9f6aced9bfaaf8419cdefab2d169d39_63.png)

对于那些不熟悉拉格朗日乘子法的同学，其基本思想是：对于一个约束优化问题，我们可以将约束（左边减去右边）乘以一个**拉格朗日乘数**（这里称为 `λ`），并将其加入原始目标函数，从而形成一个无约束的拉格朗日函数。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_65.png)

**拉格朗日函数 L** 可以写为：
```
L(θ', λ) = J(θ') - λ * ( KL(π_θ' || π_θ) - ε )
```

![](img/d9f6aced9bfaaf8419cdefab2d169d39_67.png)

![](img/d9f6aced9bfaaf8419cdefab2d169d39_69.png)

解决此类约束优化问题的一种方法是**对偶梯度下降**。其步骤如下：

![](img/d9f6aced9bfaaf8419cdefab2d169d39_71.png)

以下是具体步骤：
1.  **固定 λ，优化 θ'**：以策略参数 `θ'` 为变量，最大化拉格朗日函数 `L`。
2.  **固定 θ'，更新 λ**：对偶变量 `λ` 执行梯度下降（或上升）步。直觉是，如果KL散度约束被违反（即 `KL > ε`），则增大 `λ` 以加强惩罚；如果约束满足得很好（即 `KL < ε`），则减小 `λ`。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_73.png)

![](img/d9f6aced9bfaaf8419cdefab2d169d39_74.png)

这个过程会交替进行，渐进地找到正确的拉格朗日乘数 `λ`，从而解决约束优化问题。我们将在后续课程中更详细地讨论对偶梯度下降。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_76.png)

这是一种理论上有原则的解决方案。你也可以想象一种更直观的解决方案：手动选择一个 `λ` 值，将KL散度项视为一种正则化。这在直觉上也很有道理，你基本上是在惩罚新策略偏离旧策略太多。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_78.png)

在实际操作中，我们可能不会完全执行最大化过程直到收敛，因为这可能非常耗时或不切实际。通常只进行几个梯度步。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_80.png)

![](img/d9f6aced9bfaaf8419cdefab2d169d39_82.png)

---

![](img/d9f6aced9bfaaf8419cdefab2d169d39_84.png)

## 算法概览与总结 📝

![](img/d9f6aced9bfaaf8419cdefab2d169d39_86.png)

![](img/d9f6aced9bfaaf8419cdefab2d169d39_88.png)

综上所述，这是一个完成策略优化并施加约束的算法框架：

![](img/d9f6aced9bfaaf8419cdefab2d169d39_90.png)

![](img/d9f6aced9bfaaf8419cdefab2d169d39_92.png)

以下是算法核心步骤：
1.  计算目标函数 `J(θ')` 的梯度，其形式与重要性采样策略梯度相似。
2.  计算新旧策略之间的KL散度及其梯度。
3.  利用上述梯度和拉格朗日乘数 `λ`，更新策略参数 `θ'`。
4.  根据KL散度约束的满足情况，更新对偶变量 `λ`。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_94.png)

这会得到一个真正执行约束的强化学习算法。实际上，许多现代算法都使用了这个想法的变体，包括**原始引导策略搜索方法**和**近端策略优化**。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_96.png)

![](img/d9f6aced9bfaaf8419cdefab2d169d39_98.png)

---

![](img/d9f6aced9bfaaf8419cdefab2d169d39_100.png)

本节课中，我们一起学习了如何将带约束的策略改进理论转化为可实现的算法。关键步骤包括：用更易处理的KL散度替代总变分距离作为约束，并通过拉格朗日对偶法将约束优化问题转化为可交替优化的无约束问题。这为构建稳定、高效的高级策略梯度算法（如PPO）奠定了坚实的基础。