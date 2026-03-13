# 17：使用 rvest 在 R 中进行基础网络爬虫 🕸️

![](img/196d94282b44318cec5f01262cabb3b0_0.png)

![](img/196d94282b44318cec5f01262cabb3b0_2.png)

![](img/196d94282b44318cec5f01262cabb3b0_3.png)

在本节课中，我们将学习如何使用 R 语言中的 `rvest` 包从网页上抓取数据。我们将介绍网络爬虫的基本概念、如何使用 `Selector Gadget` 工具识别网页元素，以及如何编写代码来提取和整理信息。

## 概述

网络爬虫是从互联网上自动收集数据的过程。`rvest` 包是 R 语言中一个强大的工具，它模仿“收获”一词，专门用于从网页上抓取数据。理解一些基础的 HTML 和 CSS 知识将有助于你更好地使用 `rvest`。

![](img/196d94282b44318cec5f01262cabb3b0_5.png)

## 网络爬虫基础与限制

![](img/196d94282b44318cec5f01262cabb3b0_7.png)

上一节我们介绍了网络爬虫的概念，本节中我们来看看 `rvest` 包的工作原理及其适用场景。

![](img/196d94282b44318cec5f01262cabb3b0_9.png)

![](img/196d94282b44318cec5f01262cabb3b0_10.png)

`rvest` 适用于结构相对**静态**、具有明确定义 HTML 标签的网页。它对于通过 JavaScript 动态生成内容的网站（例如无限滚动页面）或需要登录才能查看内容的网站（如 Facebook 或 X）效果不佳。

网页主要由 HTML 编写，并通过不同的标签和 CSS 类来定义格式。CSS 类用于保持页面样式的一致性。例如，一个简化的 HTML 片段可能如下所示：

![](img/196d94282b44318cec5f01262cabb3b0_12.png)

![](img/196d94282b44318cec5f01262cabb3b0_14.png)

```html
<ul class="flat-list buttons">
  <li class="comments">...</li>
  <li class="share-button">...</li>
  <li class="save-button">...</li>
</ul>
<a href="https://example.com">链接文本</a>
```

![](img/196d94282b44318cec5f01262cabb3b0_16.png)

![](img/196d94282b44318cec5f01262cabb3b0_18.png)

![](img/196d94282b44318cec5f01262cabb3b0_20.png)

![](img/196d94282b44318cec5f01262cabb3b0_22.png)

在上面的代码中，`href` 属性定义了超链接的目标地址。`rvest` 就是通过识别这些标签和属性来定位和提取信息的。

![](img/196d94282b44318cec5f01262cabb3b0_24.png)

![](img/196d94282b44318cec5f01262cabb3b0_26.png)

![](img/196d94282b44318cec5f01262cabb3b0_27.png)

![](img/196d94282b44318cec5f01262cabb3b0_29.png)

![](img/196d94282b44318cec5f01262cabb3b0_31.png)

## 使用 Selector Gadget 工具

![](img/196d94282b44318cec5f01262cabb3b0_33.png)

![](img/196d94282b44318cec5f01262cabb3b0_35.png)

![](img/196d94282b44318cec5f01262cabb3b0_37.png)

为了高效地选择网页上的特定元素，我们需要借助一个名为 `Selector Gadget` 的浏览器插件。它可以帮助我们直观地获取目标元素的 CSS 选择器路径。

![](img/196d94282b44318cec5f01262cabb3b0_38.png)

![](img/196d94282b44318cec5f01262cabb3b0_40.png)

![](img/196d94282b44318cec5f01262cabb3b0_42.png)

![](img/196d94282b44318cec5f01262cabb3b0_44.png)

以下是安装和使用 `Selector Gadget` 的步骤：

1.  首先，确保你的浏览器书签栏是可见的。在 Chrome 或 Edge 中，通常可以使用快捷键 `Cmd/Ctrl + Shift + B` 来显示。
2.  访问 `Selector Gadget` 的官方网站，将其链接拖拽到你的书签栏中完成安装。

![](img/196d94282b44318cec5f01262cabb3b0_46.png)

![](img/196d94282b44318cec5f01262cabb3b0_48.png)

![](img/196d94282b44318cec5f01262cabb3b0_49.png)

![](img/196d94282b44318cec5f01262cabb3b0_51.png)

安装完成后，你可以通过点击书签来激活它。当你在网页上移动光标时，它会高亮显示不同的元素区域。点击你想要抓取的元素，`Selector Gadget` 会尝试找出能唯一标识这类元素的 CSS 选择器，并用黄色高亮所有匹配项。如果选择过多，你可以点击不需要的元素（变为红色）来优化选择器。

![](img/196d94282b44318cec5f01262cabb3b0_53.png)

![](img/196d94282b44318cec5f01262cabb3b0_55.png)

## 基础爬虫代码示例

![](img/196d94282b44318cec5f01262cabb3b0_57.png)

![](img/196d94282b44318cec5f01262cabb3b0_59.png)

![](img/196d94282b44318cec5f01262cabb3b0_61.png)

了解了工具的使用后，我们来看看如何用 `rvest` 编写爬虫代码。核心函数包括读取网页、选择节点和提取内容。

![](img/196d94282b44318cec5f01262cabb3b0_63.png)

![](img/196d94282b44318cec5f01262cabb3b0_65.png)

![](img/196d94282b44318cec5f01262cabb3b0_67.png)

以下是一个从 Reddit 页面抓取评论数量的基础示例：

![](img/196d94282b44318cec5f01262cabb3b0_69.png)

```r
# 加载必要的库
library(rvest)
library(stringr) # 用于后续处理文本，如正则表达式

# 1. 读取网页
reddit_page <- read_html("https://old.reddit.com")

# 2. 使用从Selector Gadget获取的选择器抓取评论节点
# 假设选择器为 “.comments”
comment_nodes <- html_nodes(reddit_page, ".comments")

![](img/196d94282b44318cec5f01262cabb3b0_71.png)

# 3. 从节点中提取文本
comment_text <- html_text(comment_nodes)

# 4. 使用正则表达式提取纯数字（例如“10 comments”中的10）
comment_counts <- as.numeric(str_extract(comment_text, "\\d+"))

# 查看结果
head(comment_counts)
```

同样地，你可以使用类似的方法抓取标题，选择器可能类似于 `.title.may-blank`。

## 使用 polite 包进行礼貌爬虫

直接快速地对一个网站发起大量请求可能导致你的 IP 被限制或封禁。因此，在进行大规模爬取时，遵守网络礼仪至关重要。`polite` 包可以帮助我们管理请求频率。

![](img/196d94282b44318cec5f01262cabb3b0_73.png)

![](img/196d94282b44318cec5f01262cabb3b0_75.png)

![](img/196d94282b44318cec5f01262cabb3b0_77.png)

`polite` 包通过创建一个“会话”来管理爬虫，它会自动在请求间添加延迟，避免对服务器造成压力。

以下是使用 `polite` 的基本工作流程：

```r
library(polite)
library(rvest)

![](img/196d94282b44318cec5f01262cabb3b0_79.png)

![](img/196d94282b44318cec5f01262cabb3b0_81.png)

# 1. 创建一个礼貌会话，并“拜访”目标网站
session <- bow("https://www.imdb.com/title/tt1490017/") # 乐高大电影页面

# 2. 抓取页面内容
page_content <- scrape(session)

![](img/196d94282b44318cec5f01262cabb3b0_83.png)

# 3. 使用rvest函数解析内容
# 例如，抓取评分
rating <- page_content %>%
  html_nodes(".cxhHyR") %>% # 从Selector Gadget获得的选择器
  html_text() %>%
  as.numeric()
```

![](img/196d94282b44318cec5f01262cabb3b0_85.png)

## 综合案例：爬取电影演员信息

![](img/196d94282b44318cec5f01262cabb3b0_87.png)

![](img/196d94282b44318cec5f01262cabb3b0_88.png)

现在，我们将前面所学的知识结合起来，完成一个综合任务：从一部电影的页面开始，爬取所有主演的名字和链接，然后依次访问每位主演的个人页面，抓取他们正在进行的项目。

这个案例演示了如何自动化地遍历多个页面并结构化存储数据。

```r
library(polite)
library(rvest)
library(stringr)

# 启动会话，从乐高大电影页面开始
session <- bow("https://www.imdb.com/title/tt1490017/")
page_content <- scrape(session)

![](img/196d94282b44318cec5f01262cabb3b0_90.png)

# 抓取演员名单和对应的个人页面链接
actor_names <- page_content %>%
  html_nodes(".gcqK-eh a") %>% # 抓取包含演员名的a标签
  html_text()

![](img/196d94282b44318cec5f01262cabb3b0_92.png)

actor_urls <- page_content %>%
  html_nodes(".gcqK-eh a") %>%
  html_attr("href") # 提取href属性，即链接

# 为链接向量加上演员名字作为名称，方便后续引用
names(actor_urls) <- actor_names

![](img/196d94282b44318cec5f01262cabb3b0_94.png)

# 初始化一个空列表，用于存储所有演员的项目信息
all_projects <- list()

# 循环处理前几位演员（例如4位）
for (actor in actor_names[1:4]) {
  # 让会话跳转到该演员的个人页面
  actor_page <- nod(session, actor_urls[actor]) %>% scrape()

  # 从演员页面抓取项目信息（假设选择器为“.ipc-metadata-list-summary-item__t”）
  projects <- actor_page %>%
    html_nodes(".ipc-metadata-list-summary-item__t") %>%
    html_text() %>%
    head(10) # 只取前10个项目

  # 将结果存入列表
  all_projects[[actor]] <- list(
    name = rep(actor, length(projects)),
    projects = projects
  )
  # polite会话会自动处理请求间隔
}

# 将列表转换为数据框，便于分析
results_df <- do.call(rbind, lapply(all_projects, as.data.frame))
print(results_df)
```

![](img/196d94282b44318cec5f01262cabb3b0_96.png)

## 其他工具与总结

除了 `rvest`，还有其他更复杂的网络爬虫工具，例如 R 或 Python 中的 `Selenium`，以及 Python 中的 `Scrapy` 和 `Beautiful Soup`。它们能处理更动态、更复杂的网页。

本节课中我们一起学习了使用 R 语言进行基础网络爬虫的核心技能。我们介绍了 `rvest` 包的基本用法，学习了如何利用 `Selector Gadget` 工具定位网页元素，编写了提取文本和属性的代码，并强调了使用 `polite` 包进行礼貌爬虫以避免被封禁的重要性。最后，通过一个综合案例，我们实践了如何自动化地遍历多个相关页面并收集结构化数据。掌握这些基础将为你在数据收集方面打开一扇新的大门。