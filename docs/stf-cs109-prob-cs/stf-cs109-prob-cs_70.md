# CS109 标志

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/examples/dart_logo/`](https://chrispiech.github.io/probabilityForComputerScientists/en/examples/dart_logo/)

***

要生成 CS109 标志，我们将向斯坦福校徽的图片投掷五十万次飞镖。我们只保留至少被一次飞镖击中的像素。每个飞镖的 x 像素和 y 像素都从高斯分布中随机选择。令 $X$ 为代表 x 像素的随机变量，$Y$ 为代表 y 像素的随机变量，$S$ 为一个常数，等于标志的大小（其宽度等于其高度）。$X \sim \mathcal{N}\left(\frac{S}{2}, \frac{S}{2}\right)$ 和 $Y \sim \mathcal{N}\left(\frac{S}{3},\frac{S}{5}\right)$

### 投掷飞镖次数：0

## 飞镖结果

`<canvas style="width:370px; height:370px;" id="imgCanvas"></canvas>`

## 飞镖概率密度

`<canvas style="width:370px; height:370px;" id="distCanvas"></canvas>`

## X 分布

## Y 分布
