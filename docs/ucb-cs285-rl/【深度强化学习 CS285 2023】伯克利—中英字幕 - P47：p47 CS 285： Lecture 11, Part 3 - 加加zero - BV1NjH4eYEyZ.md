# 【深度强化学习 CS285 2023】伯克利—中英字幕 - P47：p47 CS 285： Lecture 11, Part 3 - 加加zero - BV1NjH4eYEyZ

 Alright， let's talk about how we can train uncertainty aware neural network models to。

 serve as our uncertainty aware dynamics models for model-based RL。



![](img/e8d3580fc142affae6b03a765db92523_1.png)

 So how can we have uncertainty aware models？ Well one very simple idea is to use the entropy of the output distribution。

 I'll tell you right now this is a bad idea， this does not work， but I'm going to explain。

 it just to make it clear why it doesn't work。

![](img/e8d3580fc142affae6b03a765db92523_3.png)

 So let's say that you have your neural network dynamics model that takes an S and AS input。

 and it produces P of ST plus one given STAT， which could be represented by a softmax distribution。

 if you're in the discrete action setting or it could be represented by a multivariate。

 Gaussian distribution in the continuous setting。 So in the multivariate Gaussian case you output a mean and a variance in the softmax。

 case you just output the logic for every possible next state。 Why is this not enough？

 Well we talked about how the problem we're having is this erroneous extrapolation。

 So for the setting where we have limited data we might overfit and make erroneous predictions。

 and the particular kind of errors that we're especially concerned with are ones where the。

 optimizer can exploit those errors by optimizing against our model。



![](img/e8d3580fc142affae6b03a765db92523_5.png)

 When the optimizer optimizes against our model what it's really going to be doing is going。



![](img/e8d3580fc142affae6b03a765db92523_7.png)

 to be finding out of distribution actions that lead to out of distribution states that。

 then lead to more out of distribution states which means that our model is going to be。



![](img/e8d3580fc142affae6b03a765db92523_9.png)

 asked to make predictions for states and actions that it was not trained on。

 The problem is that if the model is outputting the uncertainty and it's trained with a regular。



![](img/e8d3580fc142affae6b03a765db92523_11.png)

 maximum likelihood the uncertainty itself will also not be accurate for our out of distribution。

 inputs。 So out of distribution inputs will result in erroneous predictions like an erroneous mean。



![](img/e8d3580fc142affae6b03a765db92523_13.png)

 but they'll also result in an erroneous variance for the same exact reason。

 And this is because the uncertainty of the neural net output is the wrong kind of uncertainty。



![](img/e8d3580fc142affae6b03a765db92523_15.png)

 So if you imagine this highly overfitted model you could say well what variance is this model。

 going to be predicted。 Let's say that the blue curve represents the predictions from the model。

 the model outputs， are mean and the variance are wide at every point。

 So if it looks at the training points the training means are basically exactly the same。

 as the actual values。 So the optimal variance for it to output is actually zero。

 This model will be extremely confident but of course it's completely wrong。

 And we'll see exactly the same thing from deep nets。

 We'll see very confident predictions that are very good on the training points but are。



![](img/e8d3580fc142affae6b03a765db92523_17.png)

 both incorrect and overconfident on the test points。

 And this is not something special about neural nets， it's not about neural nets being bad。

 at estimating uncertainty， it's just because this is the wrong kind of uncertainty to be。



![](img/e8d3580fc142affae6b03a765db92523_19.png)

 predicting。 This measure of entropy is not trying to predict the uncertainty about the model。

 It's trying to predict how noisy the dynamics are。

 See there are two types of uncertainty and there are a variety of names that people have。

 used for them but we can call them "aliatoric" or "statistical uncertainty" which is essentially。



![](img/e8d3580fc142affae6b03a765db92523_21.png)

![](img/e8d3580fc142affae6b03a765db92523_22.png)

 the case where you have a function that is itself noisy and then we have epistemic or。

 model uncertainty which happens not because the true function itself is noisy or not but。



![](img/e8d3580fc142affae6b03a765db92523_24.png)

 because you don't know what the right function is。

 And these are fundamentally different kinds of uncertainty。



![](img/e8d3580fc142affae6b03a765db92523_26.png)

 And the authority doesn't go down necessarily as you collect more data。

 If the true function is noisy， no matter how much data you collect， you will have high。

 entropy outputs just because the true function is high entropy。 Like for example。

 if you're learning the dynamics model for a game of chance， for a game where， you roll two dice。

 the correct answer for the model that models the numerical value of some。



![](img/e8d3580fc142affae6b03a765db92523_28.png)

 of those two dice is going to be random。 It's never going to become deterministic as you collect more data。

 Seeing the dice roll more and more doesn't allow you to turn that statistic into deterministic。



![](img/e8d3580fc142affae6b03a765db92523_30.png)

 one。 That's "aliatoric" uncertainty。 That's when the world itself is actually random。

 At the "extemic" uncertainty comes from the fact that you don't know what the model is。



![](img/e8d3580fc142affae6b03a765db92523_32.png)

 So epistemic uncertainty would be like the setting we had when approaching the cliff or。



![](img/e8d3580fc142affae6b03a765db92523_34.png)

 walking around on top of the mountain。 Once you collect enough data， that uncertainty goes away。

 But in the limited data regime， you have to maintain that uncertainty because you don't。



![](img/e8d3580fc142affae6b03a765db92523_36.png)

 know what the model actually is。 This is essentially the setting where the model is certain about the data。

 but we are， not certain about the model。 And that's what we want。



![](img/e8d3580fc142affae6b03a765db92523_38.png)

 Maximum likelihood training doesn't give you this。

 So just outputting a distribution over the next state or a Gaussian distribution over with。



![](img/e8d3580fc142affae6b03a765db92523_40.png)

 a mean and variance will not give you this capability。



![](img/e8d3580fc142affae6b03a765db92523_42.png)

 So how can we get？ Well， we can try to estimate a model uncertain。

 And there are a number of different techniques for doing this。

 So this is basically the setting where the model is certain about the data， but we are。

 not certain about the model。 In order to not be certain about the model。

 we need to represent a distribution over models。

![](img/e8d3580fc142affae6b03a765db92523_44.png)

 So before we have one neural net that outputted a distribution over st plus one and it has some。

 parameters theta。 So being uncertain about the model really means being uncertain about theta。



![](img/e8d3580fc142affae6b03a765db92523_46.png)

 So usually we would estimate theta as the argmax of the log probability of theta given。



![](img/e8d3580fc142affae6b03a765db92523_48.png)

 our data set， which when we are doing maximum likelihood estimation， we take to also be the。



![](img/e8d3580fc142affae6b03a765db92523_50.png)

 argmax of the log probability of the data given theta and that presumes having a uniform， prior。

 But can we instead estimate the full distribution p theta given d？



![](img/e8d3580fc142affae6b03a765db92523_52.png)

 So instead of just finding the most likely theta， what if we actually try to estimate the full。

 distribution theta given d and then use that to get our uncertainty？

 That is the right kind of uncertainty to get in this situation。

 So the entropy of this distribution will tell us the model uncertainty and we can average。

 out the parameters and get a posterior distribution over the next state。

 So when we then have to predict， we would actually integrate out our parameters。

 So instead of taking the most likely theta and outputting the probability of st plus one。

 then st at and that most likely theta will output our parameters by integrating out theta by。

 taking the integral p of st plus one given st at comma theta times p of theta given d d， theta。

 Now of course for large high dimensional parameters， spaces of this sort that we would have with。

 neural nets performing this operation exactly is completely intractable。

 So we have to resort to a variety of different approximations and that is what we are going。



![](img/e8d3580fc142affae6b03a765db92523_54.png)

 to talk about in this lecture。 So intuitively you could imagine this is producing some distribution over next states which is。



![](img/e8d3580fc142affae6b03a765db92523_56.png)

 going to integrate out all the uncertainty in your model。



![](img/e8d3580fc142affae6b03a765db92523_58.png)

 So one choice that we could use is something called a Bayesian neural network。

 I am not going to go into great detail about Bayesian neural networks in this lecture because。

 it requires a little bit of machinery， a little bit of variational inference machinery which。

 we are actually going to cover next week。 But I do want to explain the high level idea behind Bayesian neural nets。

 So in a standard neural net of the source shown on the left you have inputs x and outputs。

 y and every weight， every connection between the hidden units， the inputs and the outputs。

 is just a number。 So all the neural nets that you have trained so far in this class basically work on this。

 principle。 In Bayesian neural networks there is a distribution over every weight。

 In the most general case there is actually a joint distribution over all the weights。

 If you want to make a prediction what you can do is you can sample from this distribution。

 as actually sample a neural net from the distribution over neural nets and ask efforts prediction。

 And if you want to get a posterior distribution over predictions if you want to sample from。

 the posterior distribution you would sample a neural net and then sample a y given that。

 neural net and you could repeat this process multiple times if you want to get many samples。

 to get a general impression of the true posterior distribution y given x with theta having been。

 integrated out。 Now modeling full joint distributions over the parameters is very difficult because the。

 parameters are very high dimensional so there are a number of common approximations that。

 could be made。 One approximation is to estimate the parameter posterior this p of theta given d as a product。

 of independent arm， marginals。 This basically means that every weight is distributed randomly but independently of all。

 the other weights。 This is of course not a very good approximation because in reality the weights have very tightly。

 interacting effects so you know if you want to vary one weight and you vary the other。

 one in the opposite direction maybe your function doesn't change very much but if you vary them。

 independently it could change quite a lot。 So using a product of independent marginals to estimate the parameter posterior is a very。

 crude approximation but it's a very simple and tractable one and for that reason it is。

 used quite often。 A common choice for the independent marginals is to represent each marginal with a Gaussian。

 distribution and that means that for every weight instead of learning its numerical value。

 you learn its mean value and its variance so for each weight you have not one number but。

 two numbers now。 You have the expected weight value and the uncertainty about the weight and that is a。

 very nice intuitive interpretation because you've gone from learning just a single weight。

 vector to learning a mean weight vector and for every dimension you have a variance。



![](img/e8d3580fc142affae6b03a765db92523_60.png)

 For more details about these kinds of methods here are a few relatively simple papers on。



![](img/e8d3580fc142affae6b03a765db92523_62.png)

 this topic weight uncertainty in neural networks by blend all and concrete trial power by goal。

 at all although there are many more recent substantially better methods that you could。



![](img/e8d3580fc142affae6b03a765db92523_64.png)

 actually use if you want to do this in practice。 So Bayesian neural networks are actually a reasonable choice to get an uncertainty aware。

 model。 To learn more about how to train them check out these papers or hang on until we cover。



![](img/e8d3580fc142affae6b03a765db92523_66.png)

 the variational inference material next week。

![](img/e8d3580fc142affae6b03a765db92523_68.png)

 Today we're going to talk about a simpler method that from my experience actually works。

 a little bit better in model-based reinforcement learning and let's use Bootstrap Ensembles。

 Here's the basic idea behind Bootstrap Ensembles。 I'll present it first intuitively and then discuss a little bit more mathematically what。

 it's doing。 What if instead of training one neural network to give us the distribution over the next。

 state given the current state in action？

![](img/e8d3580fc142affae6b03a765db92523_70.png)

 We instead train many different neural networks and we somehow diversified them so that each。

 of those neural networks learns a slightly different function。

 Ideally they would all do similar and accurate things on the training data but they would。

 all make different mistakes outside of the training data。

 If we can train this kind of ensemble of models then we can get them to essentially。

 vote on what they think the next state will be and the dispersion in their votes will give。

 us an estimate of uncertainty。 Mathematically this amounts to estimating your parameter posterior p of theta given d。

 as a mixture of Dirac delta distributions。 You probably learned about mixtures of Gaussians。

 A mixture of rock deltas is like a mixture of Gaussians。

 Only instead of Gaussians you have very narrow spikes so each element has no variance。

 It's just a mixture of delta functions where each delta function is centered at the parameter。

 vector for the corresponding network in the ensemble。

 You can train multiple models and see if they agree as you measure uncertainty。

 Formally you get a parameter posterior p of theta given d represented as a mixture of。

 Dirac deltas which means that if you want to integrate out your parameters you simply。

 average over your models。 You can start a mixture distribution where each mixture element is the prediction of。



![](img/e8d3580fc142affae6b03a765db92523_72.png)

 the corresponding model。 Now very importantly in continuous state spaces it doesn't mean that we average together the。

 actual mean state where averaging together the probabilities which means that each of， these models。

 if each of these models is Gaussian and their means are in different places our。



![](img/e8d3580fc142affae6b03a765db92523_74.png)

 output is not one Gaussian with the average of those means it's actually multiple different。

 Gaussians。 It's actually a mixture of Gaussians。 So we're mixing the probabilities not the means。

 So when you implement this in homework 4 don't just average together the next states that。



![](img/e8d3580fc142affae6b03a765db92523_76.png)

 your models predict actually treat it as a mixture of Gaussians。

 Okay how can we train this bootstrap ensemble to actually get it to represent this parameter。

 posterior？ Well one mathematical tool we can use is something called the bootstrap。



![](img/e8d3580fc142affae6b03a765db92523_78.png)

 The main idea in the bootstrap is that we take our single training set and we generate。



![](img/e8d3580fc142affae6b03a765db92523_80.png)

 multiple independent data sets from the single training set to get independent models。

 So each model needs to be trained on a data set that is independent from the data set for。

 every other model but still comes from the same distribution。



![](img/e8d3580fc142affae6b03a765db92523_82.png)

 Now if we had a very large amount of data one very simple way we could do this is we could。

 take our training set and just chop it up into n non overlapping pieces and train a different。



![](img/e8d3580fc142affae6b03a765db92523_84.png)

 model on each piece。 But that's very wasteful because we're essentially decimating our data set and therefore we can't。



![](img/e8d3580fc142affae6b03a765db92523_86.png)

 have too many bootstraps we can't have too many models so when the bootstrap ensemble。

 each of these models is called a bootstrap。 So there's a cool trip that we can do which is going to maintain our data efficiency and。

 give us as many models as we want。 The idea is to train each theta i on a data set di which is sampled with replacement for。



![](img/e8d3580fc142affae6b03a765db92523_88.png)

 g。 So it decontains n data points di will also contain n data points but they will be resampled。

 from d with replacement which means that for every entry in di let's say you have n data。

 points in d you select an integer uniformly at random between 1 and d and pick the corresponding。



![](img/e8d3580fc142affae6b03a765db92523_90.png)

 element from d。 So you select a random integer from 1 to n pick the element from d right then over the。



![](img/e8d3580fc142affae6b03a765db92523_92.png)

 first entry of di。 For the second entry in di pick a random integer between 1 and d grab it from d put it in an。

 entry to for entry 3 random integer from 1 to n take it from d put entry 3 and so on and。



![](img/e8d3580fc142affae6b03a765db92523_94.png)

 so on and so on。 In expectation to get a data set that comes from the same distribution as d but every individual。



![](img/e8d3580fc142affae6b03a765db92523_96.png)

 di is going to look a little bit different。 Intuitively you can think of it as putting integer counts on every data point and those。



![](img/e8d3580fc142affae6b03a765db92523_98.png)

 counts can range from 0 to n although n is very unlikely。

 So every model trained on every di is going to see a slightly different data set although。

 statistically the data sets will be similar and it turns out this is enough to give you。

 a parameter posterior。

![](img/e8d3580fc142affae6b03a765db92523_100.png)

 So that's the theory。 Now in the world of deep learning it turns out that training and bootstrap ensemble is。

 actually even easier。 So the basic recipe I outlined on the previous slide essentially works。



![](img/e8d3580fc142affae6b03a765db92523_102.png)

 It's a fairly crude approximation because the number of models we would have is usually。

 small right so if the cost of training one neural net is 3 hours and we have to train。

 10 of them that will take 30 hours of compute。 Now you can parallelize it but it's still expensive so usually we'd use a smaller number。

 of models typically less than 10。 So our uncertainty will be a fairly crude approximation to the true parameter posterior。



![](img/e8d3580fc142affae6b03a765db92523_104.png)

 Usually though it appears experimentally that if you're training deep neural network models。



![](img/e8d3580fc142affae6b03a765db92523_106.png)

 resampling with replacement is actually usually unnecessary because just the fact that you。



![](img/e8d3580fc142affae6b03a765db92523_108.png)

 train your model with stochastic gradient descent and random initialization usually makes the。



![](img/e8d3580fc142affae6b03a765db92523_110.png)

 model sufficiently independent even if they are trained on exactly the same data set。

 So what implementing this in practice we can usually actually forego the resampling with。



![](img/e8d3580fc142affae6b03a765db92523_112.png)

 replacement。 So that makes things a little easier。

 It's important for theoretical results but practically you can skip it。



![](img/e8d3580fc142affae6b03a765db92523_114.png)

 Thank you。 [ pause ]。