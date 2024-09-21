# 沃顿商学院《AI For Business（AI用于商业：AI基础／市场营销+财务／人力／管理）》（中英字幕） - P19：18_常见损失函数.zh_en - GPT中英字幕课程资源 - BV1Ju4y157dK

 Let's talk about some of the more common ways to measure error in machine learning output。



![](img/ee32926febee5fe618fb5c24bb11950c_1.png)

 Perhaps the simplest one to understand is accuracy。

 So let's go back to our example where we're thinking about fraudulent and legitimate transactions。

 So in one column we might have the actual true values of whether a transaction was legitimate。

 or fraudulent。 In another column we have the predicted value。

 our machine learning output of whether a transaction， was fraudulent or legitimate。

 Accuracy simply indicates the fraction of times that we get the answer right。

 So it's basically comparing across the two columns and it's the fraction of times that。

 the one column matches the other column。 So that's accuracy。

 Classification error is the inverse of that。 So it's basically the fraction of times that the two columns don't match。

 So that's accuracy。 Another common metric is precision。

 Precision is asking what proportion of positive identifications were actually correct。

 So what's a positive identification？ So with machine learning output with a binary classifier is trying to predict whether something。

 is in one of two classes like legitimate or fraudulent。

 One of these two classes is indicated as positive。

 One is going to be a one so to speak and one is zero。

 So we might identify if fraudulent is the positive class in this case。

 What precision indicates is what proportion of the ones that we actually call fraudulent。

 are actually fraudulent。 So if we have a number of predictions that are fraudulent we're going to look at how。

 many of those， what fraction of those we got correct。

 And this in a sense ignores some other aspects of the data or the performance。

 It's basically looking at this particular piece， this particular measure of how often。

 what we called fraudulent was actually a fraudulent case。

 Sensitivity is a different way of looking at the performance of machine learning output。

 So in this case this is looking at how many relevant instances did you catch？

 So think about these two different columns here， the actual values and the predicted value。

 So if the actual values are legitimate， fraudulent， what sensitivity is asking is how many of the。

 fraudulent cases did you catch？ Did you let any of them slip through your net or were you able to get most of them？

 So sensitivity， a highly sensitive classifier is basically one that lets very few of the。

 relevant instances， the actually fraudulent transactions slipped through its net。

 So it's looking at something quite different from precision。

 Specificity is looking at the proportion of legitimate transactions in this case， the。

 negative case that were correctly identified as such。

 So of those transactions that were legitimate that were not fraudulent， how many of those。



![](img/ee32926febee5fe618fb5c24bb11950c_3.png)

 were correctly identified。 So again， specificity， precision， accuracy。

 they're all looking at different aspects of， what you're getting right and wrong in terms of your prediction。

 When you're talking about using one of these versus the other to think about evaluating。

 machine learning output， which we're implicitly doing is putting different weights on what。

 you care about， whether it's more important to make sure， for instance， that you never。

 miss a fraudulent transaction or whether it's more important， for instance， to make sure。

 that you never accidentally call a legitimate transaction fraudulent。

 These are the different trade-offs when thinking about these different measures。

 And there's a variety of ways to think about which are used when。

 There's language that's used around the different costs of using one versus the other。

 You might hear about true positives， true negatives， false positives and false negatives。

 True positives and true negatives are how many you get correct or how many of the identifications。

 you get correct。 True positive is the fraction of times that you identify something in the positive class。

 in this case fraudulent as being fraudulent。 For a true negative is the fraction of times we identify legitimate as being a legitimate。

 transaction。 So true positives and true negatives together basically indicate the number of times or the。

 fraction of times we're getting something right。 False positives and false negatives refer to the errors and these are things that often。

 come with costs。 And so false positives and false negatives are two different kinds of errors that may。

 involve two different kinds of costs。 False positives are the fraction of times that we identify。

 for instance， something as， legitimate as fraudulent。

 False negatives is a fraction of times we identify something as fraudulent as legitimate。 So again。

 depending on whether it's more costly to miss a fraudulent transaction or。

 whether it's more costly to accidentally flag something legitimate as fraudulent， these。

 map to false positives and false negatives and the different costs。

 And depending on what we care about from a business context， we may want to optimize one。



![](img/ee32926febee5fe618fb5c24bb11950c_5.png)

 versus the other。 There are a number of ways to represent these， to visualize these。

 to communicate these， to， different stakeholders。 One of these is called a confusion matrix。

 A confusion matrix is essentially a two by two matrix that lays out for a given case the。

 number of true positives， false positives， true negatives and false negatives。



![](img/ee32926febee5fe618fb5c24bb11950c_7.png)

 Another popular way to represent machine learning output is called an ROC curve or。

 receiver operating characteristic curve。 And this maps false positives against true positives in a way that indicates essentially。

 what the trade-offs are between those two metrics。



![](img/ee32926febee5fe618fb5c24bb11950c_9.png)

 These are some common loss functions。 We've defined them。 In the next video。

 let's talk about when it might be that some of them are preferable to， others。 [BLANK_AUDIO]。



![](img/ee32926febee5fe618fb5c24bb11950c_11.png)