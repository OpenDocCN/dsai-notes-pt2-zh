# P8：8.Feb_18_Lab - Tesra-AI不错哟 - BV1aJ411y7p7

 Okay。

![](img/6ddddef09bca9a70d5f50a90c582ca0a_1.png)

![](img/6ddddef09bca9a70d5f50a90c582ca0a_2.png)

 Just a few reminders。 Today is not March 2nd， 2015。 And I'm not David。

 So don't take this information。 Zachary。 David is out of town， so I'm covering for him today。

 So we will do a little review of what we've seen and maybe some new topics and some questions。

 and answers。 So feel free to as always ask questions。 Before we begin。

 I got a request to change my office hours to a later time。 How many of you would support that idea？

 How many of you are against the idea of changing the office hours to a later time？ I want to。 Okay。

 I haven't seen you。 It's so my office hours are on Mondays to 2pm。 Just a reminder。

 So does it sound good to switch it to a later time？ Like 4pm in 5pm。 So the problem is availability。

 classroom availability。 If I can't find a class in this building。

 I will probably have to do it in the center， for data science。

 I could do Wednesday later 4 or 5pm or I could do Thursday later。 Any preference？ Yes， sir。

 What day？ Wednesday？ Wednesday or Thursday？ So Wednesday 5pm you have another class？ Okay。

 just let me note that down。 So it has to be before Wednesday。 So Wednesday 3。30pm。

 Wednesday 4pm or options。 What about Thursday？ You have class after 3pm before this time？ What？

 Yeah。 It's after this time though。 It's at 8pm。 The graders have office hours on Tuesday。 So。

 Friday is a little bit tricky。 Yeah， last semester I tried Friday's， nobody seemed to join。

 Wednesday 4 is fine， okay。 Okay， maybe I should do a poll。 Okay。 Oops。

 So how do you tune your system while you do your homework？ It's usually by inspection。

 You try a few things。 Usually the first things you try don't work so you have to tune it again。

 right？ It's either too small or too large。 If it's too large it oscillates。

 it gives you random numbers。 If it's too small it just doesn't move。 It doesn't improve。

 And then you find a switch spot and then you zoom in。 Once you find a switch spot。

 I use a min you play around in that region to find the optimal， place。

 How do you check something is optimal？ A hyper parameter tuning is optimal。

 You check it by the improvement in the validation set。 'Cause we don't care。

 We can always make the training set have very low， low， low energies， very low， low， low cost。

 But it doesn't make sense if it doesn't correspond to an improvement in the validation， set。

 The validation set can be thought of as a generalization。 How well the mission generalizes？

 If it doesn't generalize well then it's memorizing。

 It's memorizing means it's overfitting or fitting is something that we don't want。

 So we monitor the validation set or if we have the test set available we can do that。

 Technically jargon is that you screen the validation set。

 Maybe in a trouble tuning your systems in your homeworks。 Takes time。

 What other issues have you got？ Yeah， that's an issue。

 But if you really need to go below double precision then maybe something is wrong。 Yes。

 It's possible。 I didn't actually check what's going on with the homework。 It's a separate thing。

 I can look it up if you have the definition of what exactly is going on there。

 From a general theoretical point of view。 In practice I would start with a small step size。

 I would increase it little by little until it diverges。

 So the moment before divergence is your sweet spot typically。

 It depends on how you set up the regularization。 We're going to do it in a few slides。

 If you set a really small lambda then the regularization doesn't have any effect。

 That's why you need to start from a large lambda value。

 But it again depends on your particular setup。 So most of the times but you should also be careful because if you set up too much。

 if， you increase lambda by too much then the object that you're optimizing is the right hand side。

 is the second term， is the regularizer term。 Which blocks you from dealing with the original task。

 Original task was the actual loss。 So the additional term shouldn't be too large as well。

 Should be meaningful value。 So for example if you have some cost plus some regularization let's say it's parameterized。

 with w。 Say you have something like this。 What happens if you pick a very large lambda？

 What happens？ It becomes zero。 Why does it become zero？

 Because this term is meaning this after some time。 The only contribution， the optimization。

 your parable is going to be something like this， and this little cost is maybe just a tiny bit noise around it。

 So once you optimize bum bum bum in a few steps you come to zero point。 But this is your task。

 You need to focus on this。 But what happens if this is too small？

 You just optimize this and it's not regular so you don't punish with very exploding values。

 of entries of the parameters。 So for step size I would start from a smaller number and increase it。

 For a regularization parameter I would start from a higher number if I know what the solution。

 is and then decrease it to find the balance between the two。 Did you have another question？ Yeah。

 Yeah， that sounds like it's something that fits to this intuition。

 That's something that your parable familiar with as well。

 Sometimes you want to compare two different methods and it seems like they just go down。

 and then it seems like they both make this shape so it's not the fresh。

 We don't really know what's going on。 But once you take the log scale then you realize what's happening here is actually something。

 like this with let's say stochastic gradient descent and maybe something like this with。

 the gradient descent。 So this little gap that was now existent before in this plot in the real plot it becomes visible。

 and not visible in the log plot。 Okay， some loss functions。

 So suppose we have the total loss we don't have we don't average it。

 We don't divide this expression of J omega with n with the number of samples and what， happens。

 The calculation is easy since differentiation is a linear operator we can take differentiation。

 operator into the sum which is a finite sum so we can do that right we can switch differentiation。

 with the sum。 If it were infinite sum then I would have to check whether it was converging in from the。

 old up。 But it's a finite sum so I can do that I switch to order of differentiation with respect to。

 summation then I get the second equation which gives me the gradient。

 And I can follow the path of the gradient simply enough。

 So from this expression of the gradient of J omega what is the step of stochastic gradient， descent。

 And that's the last equation last last line actually there's no recall to sign there。

 So the last line tells me that if I want to do things in the stochastic way then I would。

 have to take a step in the direction of minus 2 times W parameters times input minus the。

 output times input again。 It's going to be a vector。

 It's dot product is a number minus a number times a number multiplied with a vector。

 But how do you compare the derivative here and the derivative there if you don't have the。

 averaging。 What differentiates them？ What's different between the two？

 True but if I had one over run that would be still true。

 So I want a difference between the two that's only particular to the choice of the factor。

 one over run。 Direction。 Well it's just a scaling so I can add one over run and I get the same direction right。

 Think in terms of magnitude。 What's the difference between the gradient of the JFW？

 So what's the difference between the gradient step versus the stochastic gradient step？ The divider。

 Yes it will be larger right。 The first one will be much larger because I take gradients and I add them up。

 I add n different vectors。 So this one is addition of n different vectors。

 Maybe they rotate and come back。 I don't know that but in the end on average in the expected value in the sense of mean。

 of things it's larger because in the end I'm adding n different vectors and this is going。

 to be the total one then those are the little steps。

 But I take the average if I look at the gradient。 So if I had this one over n factor in front of this expression of minus gradient J omega。

 then I would have this vector this is the total gradient and divide it by n right。

 There's none of them so it's roughly somewhere here。 That would be the average one。

 So in terms of how big of a step you are taking in that mountainous landscape the scale of。

 the two are very different depending on whether you average them or not。

 If you average them the scales are comparable of SGD and GD。

 But if you don't average them then they are not comparable。

 The gradient step is much larger roughly and times the step of a single example times larger。

 So that's actually the next slide。 So the technical computation of this is just taking expected values。

 Why do we take expected values？ Expected values are something some operations that can be done on random variables that。

 has some sort of underlying distributions。 What's a random variable here？

 I thought we just had some examples。 I thought I had a bunch of fixed points。

 I thought I had only those x1 and xn's。 But obviously I can't take them as random variables that come from some unknown distribution。

 that's called key。 So x is distributed as DP in a sense or we can just say P。

 So there is some underlying distribution of those examples that I'm selecting my samples， from。

 And once I sample them the sampled outcomes are those N samples。

 And hence even though I don't know what P is， even though I don't know what underlying distribution。

 is， I can look at their expected values and compare them。

 Because in GD and SGD the distribution will be the same。

 So taking expected value will give me a rough idea of the magnitude of stochastic steps versus。

 gradient steps。 So let's just carry that out。 Now I'm just plugging from the previous slide the expression for the gradient。

 Take expectation。 Again， expectation is a linear operation。 And I have finite sum。

 So I can reverse the order of summation and expectation。 And I take expectation inside。

 but I have is minus N times expected value of this expression。

 which is the step of stochastic descent。 So it turns out our intuition that we did on the board was indeed true。

 In expectation， the size of a， the mean size of a gradient step is N times larger than。

 the mean size of a stochastic gradient step。 Right？

 Just a simple observation that you can back with a little basic calculation。 So what does this mean？

 If you don't average， and if you want to take a， take an SGD step， we can maybe pick an example。

 and blow it by N。 So maybe it was this and we can just blow this by N and take that step instead。

 Right。 That's a possibility。 I'm not sure if it's the smartest way to do this。

 but it's a possibility。 Yes？ [ Inaudible ]， Take you this step versus this step。

 You don't usually do this。 It's just because stochastic steps， as you see， they're a little noisy。

 If you blow them by N， they might take you to places where you don't actually want to， go。 Right。

 That's not， that doesn't give you， so ultimately， why do we do stochastic gradient descent？

 To gain time。 Because time is a big constraint。 I can't train huge networks with gradient descent。

 That would be lovely， but we don't have the computational power。 That would take ages。

 You're overshooting in weird direction。 So each time， imagine them taking this。

 It's going to be like this。 Take this step。 It's going to be like this。 Take this step。

 It's going to go like this。 So in N steps， you want to reach here， but your god knows where。

 [ Inaudible ]， Yes。 Yes。 [ Inaudible ]， [ Inaudible ]， Yes。 [ Inaudible ]， Yes。 [ Inaudible ]， Yes。

 [ Inaudible ]， Yes。 [ Inaudible ]， Yes。 [ Inaudible ]， Yes。 [ Inaudible ]， Yes。 [ Inaudible ]， Yes。

 [ Inaudible ]， Yes。 [ Inaudible ]， Yes。 [ Inaudible ]， Yes。 [ Inaudible ]， Yes。 [ Inaudible ]， Yes。

 [ Inaudible ]， Yes。 [ Inaudible ]， Yes。 [ Inaudible ]， In my experience。

 I think it doesn't matter about how far you have -- how far you are from。

 the original -- if gradient descent is costly， you typically don't use it。

 If you can't afford using gradient descent， and if you know your problem is usually nice， in comics。

 which is what we had so far， then by all means go ahead and use gradient descent。

 It's much more stable， much more consistent in all cases。 So， okay。

 let's -- let's take a look at the slide again。 So it's just rewriting this expression of minus and times gradient。

 So it tells you what happens -- you know， comparing various steps。 So， you know。

 the whole point of this detour was to get us back to the average loss。

 So if I want to optimize the same thing with the same magnitudes of steps， I could use the。

 average one。 If I have the average one， then my gradient step will be like this。

 and stochastic step will， be like this。 So they are going to be those small vectors。

 and the sizes of their vectors are going to， be comparable。 The SGD will have some noise。

 but their sizes will be comparable。 And most of the times。

 I can't think of specific examples in which the total loss is going to， be a better loss function。

 but most of the times you want to use the average one。 You want to use the average loss。

 So unless there is a specific reason that forces you to use total loss， I would suggest using。

 the average loss。 And there are various other advantages of the average loss as well。

 and we'll come to that， yes？ [inaudible]， You could。

 So you are saying I could always scale the step size by N， and I could get the same thing。

 And then if you add regularization， then the scale of regularization will be different as， well。

 But good question。 You could， there isomorphic。 So the two problems are the same。

 I can scale either the step size or， you know， hyper parameters。

 That seems like it's the same thing， so it seems total。

 Why do I play the total loss versus average loss？ Right？

 The main idea of using average loss is the following。 Suppose you have huge amount of data。

 Thousands of thousands of data。 And practically they repeat themselves。 What happens then？

 [inaudible]， You are double counting the same errors。 What happens if you use the total loss？

 Or versus average loss？ Yeah， right？ So let's say you have the same thing。 No， x minus， let's say。

 let's say it's just x squared。 Or parameter is w。 Let's say you have w squared。 And you have， okay。

 w x minus y squared。 And you have two samples。 You add this， w x two minus y two squared。

 And this is your loss。 This is your total loss。 And the average loss is one half of the same thing plus one half of the same thing because。

 you have two examples。 So if you assume that x one is x two and y one is y two， what happens？

 Your gradient step in this one will be just twice of the gradient step of this one， right？

 That's fine。 What's your stochastic step？ In this case， your stochastic case。

 so stochastic step of the average one is actually equal to， the gradient step of the average one。

 In the above example， it won't be the case。 In the above example。

 the stochastic step will be half the size of the gradient step。

 So this is like you have a parabola and you have another parabola on top of it。

 And instead of adding them up， you just average them so it's the same thing， right？

 It gives you the same thing。 So why is that important？ Because if I have data that has similarities。

 then the average， then the stochastic step， stochastic。

 gradient step will give me exactly the gradient step。

 So I will save time and they will both have the same descent directions。 So in this example， again。

 you can argue that if I scale everything by one half in this first， example。

 I'll get the same thing。 But what if you have data that comes from two different sources？

 So all the parabolas are either here or there and you add them up and you have a little variation。

 between the two。 So the data， let's say this is the data of zeros and this is the data of ones that you。

 want to classify。 And it's not perfect。 It's， let's say， handwritten zeros and months。

 So some zeros have this cost and some zeros have this cost。 And in the one case。

 the handwritten digits have some of them has this cost and some of， them has this cost。

 So they're not exactly the same。 And you have 30，000 such samples and you have a huge network to train。

 Calculating the gradient of those 30，000s， 30，000 examples will be painful。

 If you take the gradient step， if you are looking at the average cost， for the average cost。

 this problem of averaging over 30，000 samples will be almost exactly the same as just taking。

 one from this， one sample from this and one sample from that and averaging over these two。

 It exactly gives you the same decent directions。 So by just bringing a little calculation。

 you save yourself time and condition power and you have a method that's almost as powerful as a gradient descent。

 That's why in practice， yes？ Because calculating the gradient of a sum of 30。

000 of the same thing is 30，000 times slower than calculating the gradient of one term。 Look。

 in this step， since you don't know exactly what xi's and yi's are。

 calculating this amounts to calculating gradient of this n times。

 If you could just get away by calculating one term only， that would save you time by n times。

 They are huge。 Weight net worth weight matrix is huge。

 so you might not even have enough memory to collect all gradients。 Yes？ [inaudible]。

 Take your gradient。 [inaudible]， [inaudible]， In the average one， okay？

 So why would you normalize the gradient？ [inaudible]， So if you make the。

 if you're on different landscapes in the total of one， then average one。

 If you make the norms of the gradient the same， then you take different steps。 Like in one example。

 you have an amplified world where a normal， an average person is like a， you know。

 like gluver's gigantic world。 You have to take gigantic steps to get to the place where you want to go。

 In the other one， you're in a tiny people world， so you have to take tiny steps。

 So you want to follow the path of the gradient。 So what matters is not whether the gradient of this is comparable to the gradient of this。

 but what matters is whether the gradient of this is comparable to the stochastic gradient of the same landscape。

 Or the gradient of this compared to the stochastic gradient of the same landscape。

 So fixing a function， loss function fixes you the landscape。

 and that inherently has its own scale of things。 You're either in the gigantic world or tiny world。

 When you're a couple of eight， the way we are getting near the beam。

 or the stochastic gradient tends to be the normal gradient tends to be the gradient。 Yes。

 In the stochastic case， it also decreases， but it's noisy。 Why it's noisy？

 Because the sum of the two parabolas here is another parabola here。

 And you want to be around here in the minimum。 And if you by chance sample a function from the first example from the first one。

 the gradient will be large and it will show you on the other side。

 And that's why in practice in large scale problems people do stochastic gradient descent with a mini-batch。

 Not with mini-batch size of one， but with mini-batch size of ten hundred， or maybe even more。

 depending on the problem。 So in this example， if I take random samples of ten inputs。

 let's say I have thirty thousand training examples， and I randomly select ten of them。

 and look at the average。 The average will be a really good estimate of the underlying function。

 Because I know I have a good chance of selecting almost equally from both classes by choosing mini-batch size of ten。

 And since they're all very close to each other， and they're all very close to each other。

 the average of the two will give me something very similar to this landscape。

 So that landscape by averaging will be just maybe a tiny bit shifted version of it。

 And the stochastic steps will be calculated by the gradients of the shifted landscape。

 and the actual gradients will give me this landscape。 So this is going to be a gradient step。

 and this is going to be a stochastic gradient step。

 But the good deal is that they are so much comparable， they are almost the same。 So in this example。

 with mini-batch size of ten， the stochastic steps will almost follow the steps of the gradient descent。

 which is a huge benefit。 That's why it works in practice。 That's why average loss is much nicer。 OK。

 so if you take two， there's a higher chance that you maybe only select from the first class。

 You can do two， too， because in the long run， if you keep selecting two all the time。

 some of them will be the average ones。 So， for example， in the digit classification problem。

 classical example where SGD works better than GD， much， much faster。 In that case。

 you can take stochastic gradient， since there are ten examples， you can take stochastic gradient。

 mini-batch size 100， or 128。 That's the standard， 128。 Well。

 the trade-off is between computation time， what you can afford。

 because you want to increase the mini-batch size， but you don't want to increase it too much to slow down computation。

 Yes？ In the case， when we're using， for example， mini-batch with ten examples。

 we have to average for more than ten。 Yes。 And then take the gradient。

 And taking gradient of ten submissions is easier than taking gradient of 30，000 submissions。

 That's the whole idea。 It's actually pretty simple。

 So the idea behind SGD is that there is redundancy in data。 Data usually comes in little clumps。

 and we select a lot of them， so we have lots of lots of lots of samples to train data。

 to train the system， train a machine。 And if there is redundancy， SGD will work well。

 because it will approximate the gradient very well。 If it doesn't， I think in the homework。

 the case you had， you know， most people had the trouble of gradient descent finding a better solution than the stochastic gradient descent。

 It's because you're doing mini-batch size 1。 So the gradient of this pulls you in a direction。

 The gradient of this pulls you in another direction， so you can't really stabilize here。

 It actually bounces back and forth here。 You have to really wait a long time for the step size to diminish the very low value to be able to see points here。

 So it seems like it's taking longer。 Because that problem is not the best showcase of SGD。

 So it shouldn't mislead you。 Yes？ [inaudible]， Yes。 [inaudible]， You always have to do that。

 Because if you。 [inaudible]， No。 You can take constant step size。 That doesn't matter much。

 [inaudible]， [inaudible]， So if you don't take anything， it's actually taking a step size of 1。

 right？ Your step size is 1， in that case。 So maybe 1 is a too large of a step size。 It will diverge。

 Or maybe 1 is too small of a step size。 It really， really depends on the problem。

 How do you put constraints on v？ What's your x's and what's your y's？ If you normalize your data。

 if you preprocess and make all the x's have expected value 0 and standard deviation 1。

 it's different than having them blown up by a factor of 10。

 So that you still need to do hyperparameter tuning is because you don't know the scale of your data。

 So it doesn't save you from hyperparameter tuning。 Clearly。

 since the two functions differ by only a factor of 1 over n， once minimized。

 their minimizers are at the same place。 So on the domain。

 it's going to be the same point on the domain。 The values are going to be different。

 The altitudes are going to be different。 But the points are going to be the same。

 What happens if you're the regularizer though？ What happens in this case？ In this case。

 they are not at the same place。 In both cases， I just added a term that regularizes。

 that punishes large values of weights。 Now， the location is going to be a little different。

 Why is that？ Okay， let's ask another question。 How can I change lambdas so that the two loss functions have their minimizers at the same point？

 Minimum zero？ What？ Big lambda？ I can make lambda zero， but then I lose regularization。

 I want to keep regularization。 Lambda times n。 So I can just modify one of the lambdas。

 So now the loss function depends on lambda。 To the first one， let's explicitly write the dependency。

 lambda plus total plus。 And the other one is total divided by n plus lambda from squared。

 So if I here， instead of plugging lambda， if I plug lambda divided by n。

 I also have lambda divided by n here。 Then the minimizers are at the same place。

 But let's take a step back。 Let's take lambda is fixed before I assign those functions。

 So I have these two。 Which one question is the last line？

 Which one of those functions once minimized have the smaller complexity？

 Smaller norm in lambda in parameters w。 Which one？ Second one？ First one？ Second one， why？

 Because we have higher organization。 Yes， because it has higher organization。

 Because we put more weight in regularizing norm of b than the emphasis we put on the actual thing we want to minimize。



![](img/6ddddef09bca9a70d5f50a90c582ca0a_4.png)

 That's the end of the review part。

![](img/6ddddef09bca9a70d5f50a90c582ca0a_6.png)

 We have 10 more minutes for little kernel methods。



![](img/6ddddef09bca9a70d5f50a90c582ca0a_8.png)

 Same remark， this is not February 18， 2015。 I'm not being any questions on the previous topics。 Yes。

 In general， let's say you have a function times， so let's just look at the first function。

 What happens if I take lambda zero？ Then there's no regularization。 Whatever w。 I find， I find。

 Why do I add regularization？ I added， because maybe by chance。

 I have a bad function here that doesn't punish large values of w。 So it blows up。

 And it memorizes everything。 I don't want it to memorize it over fits。 I want to prevent that。

 So in order to prevent that， in order to prevent this function blowing up， I add this term。

 But it does that if I minimize the whole thing， I also want to minimize this。

 So it blocks the growth of w。 It blocks the growth of parameters。

 So in the extreme where lambda is zero， this can be very large。 This can blow up。

 What is the other extreme when lambda is infinity？ Or very， very large。 Sum lambda very large。

 Omega star will be almost zero， right？ Yes， it's going to be zero。 Close to very close to zero。

 So what happens is very close to zero。 Then it has， according to the previous definition。

 it has low complexity， which means it has low norm。

 So what this means is that larger lambda lower the complexity。

 And that's how we derived this conclusion from two different functions。

 Because the second one has larger lambda。 Let's go quick。

 The current x will be the space of text and x will be an example。

 You didn't see the slides yesterday， right？ No。 So x will be an example of a text。

 And we are going to extract features。 Features can be some keywords that can be extracted from the text。

 such as Android。 That takes place twice， Google that takes place twice， IO shows up once。

 and then and so on and so on。 We'll come back to this text。 So if we have two different texts。

 examples of texts， how do we compare the two？ We want to find a notion of distance。

 We want to find a dual notion of similarity between the two texts。

 It can be identifying positive reviews from negative reviews。

 So if I find good keywords for positive reviews on Amazon。

 I can actually find a similarity notion between the two。 By just calculating a number。

 I can say this is very close to a positive review。 So it's supposed。

 the other one that has an unknown label will be a positive review。 And if the distance is too much。

 then I can assume that it's a negative review， right？ You can do things like that。

 So you want to come up with a function that takes input as two texts。

 and it will up you a real number that will determine how close they are。

 There are various ways to do that。 Let's say we have the following two texts。

 They seem to have come from similar contexts， and I can look at number of occurrences of various keywords。

 Now I have some feature vectors。 I extracted the vector of dimension seven here on one side and on the other side for both texts。

 Now I'm going to compare them。 It seems like their similarity is peaked in the first two elements。

 but how can I create a rigorous notion of comparison？ Let's say I normalize my vectors。

 What I do is I just take squares of all the elements。

 take the square root and divide every element by that， which gives me a new vector is the following。

 which is just normalization。 So they have the same size。 So they become comparable now。

 Now what I can do， now I have two vectors。 They are normalized。 I can take the dot product of them。

 I can take the inner product。 The inner product， remember。

 it gives you the angle between two vectors on a given space， on a given inner product space。

 I checked the inner product。 The inner product turns out to be 0。85。

 which kind of indicates high correlation。 The two texts that are originally started with have some similarities that's beyond random。

 It's a good indication。 It seems like inner product of features。

 remember they were extracted by a number of occurrences of certain keywords。 In this case。

 inner product seems to be a good kernel。 So a kernel is something that takes two inputs and speeds to a number that roughly compares and measures the distance between two objects。

 Okay。 It's a little reminder， some linear algebra。 And inner product。 So before we go any further。

 do you know the relationship between inner product spaces， norm spaces and metric spaces？

 So we want to create a notion of angle and distance。 And according to this equation。

 this first equation here， we have a notion of angle because we have this cosine theta there， right？

 We know that it's related to it just measures the theta has to be angle between two vectors。

 But it also has a norm。 It has norm of v and norm of x。

 So does it mean that every inner product space has a norm？ And as far as this。

 it does induce a norm。 So if I have an x in the space， and if I have an inner product defined。

 then I can define a norm induced by the inner product as x。x。

 This means that every inner product space is actually normed space。 And in turn。

 I can use the norm to define a metric space。 This means every normed space is a metric space。

 So if I look at the set of all spaces that are inner product。

 they are going to be the smallest because inner product implies norm。

 So those are going to be normed spaces。 And this implies metric， which is even larger。

 And the reverse relation is true。 Not every metric space is a normed space。

 Not every normed space is an inner product space。 So why is this important？ Yes。

 Metric space is the space where you have the notion of distance。

 The only thing you have in your hand is a notion of distance。 There are assumptions of all of them。

 We don't have to go into this。 The only thing we need to understand when it comes to separation of those spaces is that metric can be a very vague notion。

 As long as you can describe a distance pretty much， it's going to be a metric space。

 But it won't have the rigidity of norm。 Norm is a little more special。

 Norm gives you certain scaling properties， for example。 If you take a vector， multiply it by two。

 then its norm should be twice as much。 You don't have to have that in a metric space。

 So normed space is more rigid。 What extra thing do you have in an inner product？

 Let's answer this and we are done。 Normed space is a little rigid。

 It has distances that scales with the constant proportionally。 As you said。

 inner product space has the extra notion of angle。

 So now every normed space has to carry out the notion of angle。

 But an inner product space on top of being a metric has a distance and has rigidity of norm。

 On top of everything it has the notion of distance， notion of angles。

 That's why we have the first equation there。 That's why we can take two texts and look at the similarities。

 That's why inner product spaces are going to be the suitable spaces to work on kernels。

 And more on kernels will become the next class。 Thanks。



![](img/6ddddef09bca9a70d5f50a90c582ca0a_10.png)

 [BLANK_AUDIO]。