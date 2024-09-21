# 沃顿商学院《AI For Business（AI用于商业：AI基础／市场营销+财务／人力／管理）》（中英字幕） - P54：20_信用风险模型准备.zh_en - GPT中英字幕课程资源 - BV1Ju4y157dK

 Okay， so we're moving towards our model training and testing。



![](img/09a88955f3c611834b896a2e110fbafd_1.png)

 So let's continue preparing for this modeling process。 And just to be clear， let's reset the stage。

 right？ The goal here is in some sense to estimate a function。 F。

 using a bunch of input variables or predictors or explanatory variables that will help classify。

 our outcome variable， y is either investment grade or speculative grade。 Right。

 so y is our outcome variable， it's one if investment grade zero otherwise， it could。

 be one and minus one， and it doesn't matter。 And all these x's here are our model inputs or predictors explanatory variables。

 And so from the last video， we are starting our sort of starting point for this exercise。

 will be all the credit risk KPIs that we discussed at the outset to sort of get an economic。

 understanding of， you know， what corporate credit risk is and how we measure it。



![](img/09a88955f3c611834b896a2e110fbafd_3.png)

 Now that said， I'm going to take a look at the correlation matrix for all of these predictors。

 and I've done so in sort of a heat map format。 So let me explain what this colorful picture shows。

 So each row and each column correspond to a different combination of variables。 Right。

 so the first row corresponds to the current ratio， the first column， the current， ratio， second row。

 quick ratio， second column， quick ratio， and so on and so on and so on。

 Each number in the matrix corresponds to the correlation between a pair of variables。

 Now you'll notice that the diagonal on the diagonal， they're nothing but ones because。

 those represent the correlation between a variable with itself。

 So the correlation between the current ratio and the current ratio is one as is the correlation。

 between the assets to equity ratio and the assets to equity ratio。

 The coloring is just there to help identify stronger or weaker correlations。

 Stronger correlations are identified and I need to be able to be careful here。

 Your positive correlations are identified by darker colors。

 Here's the scale one being the strongest。 Stronger negative correlations by lighter colors。

 We don't have anything perfectly negatively correlated but we do have some correlations。

 that are less than negative point four。 Even negative point five as we see the debt to asset ratio and interest coverage ratio。

 Now why am I showing you this？ Well， I label the slide redundancy with a question mark because when we first introduced these。

 measures we sort of bucketed them by what they weren't trying to measure。

 So that first group of liquidity measures， the current ratio， quick ratio， and cash ratio。

 they're all trying to get measures of liquidity。 Now not surprisingly。

 they're also positively correlated and from just from looking at the。

 numbers as well as the darkness of the shading， they are very strongly positively correlated。

 Likewise we also have some measures that are very strongly negatively correlated。

 When we think about the debt to capitalization ratio relative to the interest coverage ratio。

 or debt to assets to interest coverage， we've got debt in the numerator and debt in the。

 denominator。 And so there's a very strong negative correlation there。

 The point of this exercise is to suggest the idea that， well， we can throw in all of these。

 variables into the model and let it sort of parse through what works and what doesn't。

 That's not always the best strategy。 There's this notion of model parsimony or simplicity that is very important and quite useful when。

 it comes to forecasting out of sample。 And so we may want to sort of pare down what we look at in terms of the number of variables。

 and that's something we'll investigate a little bit later on， but something to be aware， of。

 Of course， anything that's perfectly correlated is just going to create all sorts of problems。

 for the model。 So that's something else we could identify from this correlation matrix。 Now。

 in the case of thousands of variables， looking at a visualizing that matrix is completely。

 infeasible， but we can， of course， comb through it through， you know， programmatically or we。

 can use data compression techniques like principal components analysis， something a little bit。



![](img/09a88955f3c611834b896a2e110fbafd_5.png)

 beyond the scope of what we're going to be discussing today。 All right。 Now。

 the next thing I want to talk about are train test splits， which should be done at。

 the very start of this process。 So I'm doing a little bit of a no-no here。

 but it sort of eases the flow of the discussion。 What we need to do is we need to take that sample of data and split it into pieces。

 A training piece on which we'll be training our model， estimating our model， trying to。

 find the best model， and then a test piece or a holdout sample that we only look at once。

 we've finalized a model。 See， what we want to avoid doing is overfitting。

 We don't want to build a model that can describe the data we have really well， because then。

 when new data comes in， it may function very poorly。 The classification accuracy may be very poor。

 So we really want to train our model on the data that we have， and only once we've settled。

 on a model， determine if it's worthwhile on the back end with the test data。

 So we're going to train test split our sample。 I'm going to do it。

 So we've got here's our full data set， 10，540 observations。 My training data has 8，432 observations。

 My test data has 2，108 observations。 And what I'm showing you here are the variable averages for all of our predictors。

 as well， as the outcome variables。 So investment grade is an indicator equal to one when the observation is investment grade。

 zero otherwise。 What I'm showing you here is that the average for each of these variables across the full。

 training and test subsamples are very similar。 In fact， if I actually。

 what I'm not showing you here are sort of our test statistics， statistically。

 testing the differences between these numbers， they're all very small。

 So they are economically and statistically indistinguishable， which is what you should expect。

 if you just randomly allocate observations to training and test。 So let me just summarize。

 We've done all of our data acquisition verification， our data preparation/model preparation。

 And what we're ready to transition to now is the actual modeling， which is what's coming。



![](img/09a88955f3c611834b896a2e110fbafd_7.png)

 up next。 [BLANK_AUDIO]。

![](img/09a88955f3c611834b896a2e110fbafd_9.png)