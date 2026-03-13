# 22：L14.1 - 逻辑语言（英语）计算 🧠➡️💻

在本节课中，我们将学习一种名为“逻辑英语”的计算机语言。它是一种基于逻辑编程的语言，但使用类似英语的语法，目标是让没有数学或逻辑背景的人也能轻松阅读和理解。我们将探讨它的基本概念、特点、应用以及与知识图谱的关系。

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_1.png)

---

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_3.png)

## 概述

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_5.png)

逻辑英语被视为一种计算机语言，本质上是逻辑程序的“语法糖”。它非常接近逻辑程序，可以轻松翻译成逻辑程序。同时，它的设计灵感很大程度上来源于法律文件的语言。逻辑英语的主要优点是，无需数学、计算或逻辑训练即可阅读。它有可能成为一种未来的通用计算机语言，让受计算机程序影响的人能够理解程序在做什么。

---

## 逻辑英语的背景与发展

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_7.png)

上一节我们介绍了逻辑英语的基本概念，本节中我们来看看它的发展背景和相关工作。

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_9.png)

逻辑英语的研究可以追溯到1982年，当时的工作涉及向儿童教授逻辑作为一种计算机语言。我们从语义网络开始，这是一种很好的知识图形表示方法，并展示了如何扩展语义网络以包含规则。

除了逻辑编程，相关的工作领域还包括“受控自然语言”。特别是，Attempto Controlled English (ACE) 等项目试图控制英语的语法。最近，许多专门建立在逻辑编程基础上的发展出现，它们使用加糖的语法，但重点不是作为通用语言，而是作为领域特定语言。

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_11.png)

最接近今天展示作品的是“Roe”，它是逻辑编程语言“应答集编程”(ASP)的语法糖。它使得常规的ASP语法变得冗余，因为可读性强的英文版本随处可得。

---

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_13.png)

## 逻辑英语的核心特点与表示

了解了背景后，本节我们深入探讨逻辑英语的核心特点及其表示知识的方式。

逻辑英语的基本形式是使用子句，就像在逻辑编程中一样，有一个单一的结论和多个条件。我们使用中缀、前缀或后缀形式来书写这些子句。

以下是逻辑英语的一些核心特点：

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_15.png)

*   **变量与类型**：在逻辑程序中，变量的量化是隐式的。逻辑英语使用不定冠词（a/an）引入变量，并使用普通名词（如“部分”、“账户”）给出变量的类型。例如：`a part X of Y`。
*   **介词表示角色**：介词（如“of”）给出了谓词的角色。例如，“part of”中的“of”就是介词。
*   **无代词**：逻辑英语中没有“他”、“她”或“它”这样的代词，这是为了避免普通语言中最大的歧义来源之一。
*   **单数与现在时**：所有名词和动词都是单数，并且使用现在时态。时间概念通过具体化时间变量来处理，这比涉及模态和可能世界语义的相关逻辑要简单得多。

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_17.png)

我们可以用逻辑英语来表示知识图谱中的关系。例如，对于“一个人参与一项研究”和“一项研究是关于一种化学物质的”这样的关系，我们可以用以下方式声明谓词：

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_19.png)

```
a person participates in a study.
a study is about a chemical.
```

---

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_21.png)

## 从语义网络到逻辑规则

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_23.png)

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_25.png)

上一节我们看到了如何表示事实，本节我们来看看如何用逻辑英语表达规则，进行推理。

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_27.png)

逻辑英语可以轻松地将语义网络中的关系扩展为规则。例如，假设我们有一个知识：“一家公司生产一种产品”和“该产品含有一种化学物质”。我们可以推导出一条规则：“该公司对该化学品有兴趣”。

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_29.png)

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_31.png)

在逻辑英语中，这条规则可以写成：
```
a company has an interest in a chemical
if the company produces a product that contains the chemical.
```
在这个规则中：
*   首次引入的变量（如“a company”、“a chemical”）使用不定冠词。
*   在同一句子中再次提及的变量使用定冠词“the”。
*   结论中的“an interest”是一个存在量词，表示“存在一种兴趣关系”。

这种表示方法使得复杂的推理链条可以用接近自然语言的方式清晰地表达出来。

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_33.png)

---

## 处理时间与存在量词

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_35.png)

逻辑英语如何表达时间这种复杂概念？变量量化又有哪些细微之处？本节我们来探讨这些技术主题。

**处理时间**：通过将时间具体化为变量，我们可以用现在时态谈论过去或未来的事件。例如，关于账户余额变化的规则可以这样写：
```
the balance in an account is an amount B at a time T2
if an amount A is transferred to the account from another account at an earlier time T1,
and T1 is before T2,
and the balance in the account is an amount B1 at the time T1,
and B is the sum of A and B1.
```
这里，时间点`T1`和`T2`是变量，使得整个规则能用现在时陈述。

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_37.png)

**存在量词**：这是一个需要特别注意的技术点。
*   在逻辑英语中，所有出现在**条件部分**的变量都是**全称量词**，其范围仅限于该句子。
*   然而，如果变量出现在**原子句子（事实）** 或**规则的结论部分**，并且**不在条件中**，那么它通常是**存在量词**，并且具有更广的范围，可以在其他句子中被引用。

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_39.png)

例如：
*   `An amount is transferred from Bob’s account to Mary’s account.`（这是一个事实，其中的“An amount”是存在量词，指某个特定的金额。）
*   `An amount is transferred from Bob’s account to Mary’s account if today is the first day of the month.`（这是一个规则，结论中的“An amount”是存在量词，它是月份的函数。我们可以另写一句：`The amount transferred is greater than or equal to ten pounds.` 来引用这个特定的金额。）

---

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_41.png)

## 复杂领域应用示例

为了展示逻辑英语处理复杂现实问题的能力，我们来看一个来自法律金融领域的挑战性例子。

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_43.png)

以下是国际掉期和衍生品协会主协议中关于“提前终止”条款的一段简化逻辑英语翻译：
```
A party has the right to designate an early termination date
if an event of default occurs with respect to the other party.
However, the party does not have the right to designate an early termination date
if automatic early termination is specified to apply in the schedule.
An early termination date occurs automatically at the time an event of default occurs
if automatic early termination is specified to apply in the schedule.
```

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_45.png)

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_47.png)

这个例子展示了逻辑英语如何清晰地表达法律条文中的逻辑结构：
*   每个句子都有结论和条件。
*   “However”这样的转折词被翻译为对前句条件的否定（`if automatic early termination is specified...`），这是逻辑编程中处理例外情况的标准方式。
*   结论中的“an early termination date”是存在量词，它是违约事件和当事方的函数。

---

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_49.png)

## 总结与展望

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_51.png)

本节课中，我们一起学习了“逻辑英语”这种独特的计算机语言。

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_53.png)

我们了解到，逻辑英语是逻辑程序的语法糖，旨在成为一种人类可读且可执行的规范语言。它的核心特点包括：使用类似英语的子句、通过冠词和名词表示变量与类型、用介词表示角色、避免代词和使用单数现在时。它能够处理时间推理和存在量化等复杂概念，并已应用于法律合同等专业领域。

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_55.png)

逻辑英语不仅是一种比许多形式逻辑更简单的逻辑体系，也是一种可以明确表达句子意图的英语形式。它未来有潜力成为一种能被广大利益相关者（而不仅仅是软件工程师）理解、辩论和解释的通用计算机语言。

---

![](img/0d5382d9e3d5ec96696a7e97556c3dfb_57.png)

**感谢鲍勃·科瓦尔斯基教授对逻辑英语的精彩概述。**