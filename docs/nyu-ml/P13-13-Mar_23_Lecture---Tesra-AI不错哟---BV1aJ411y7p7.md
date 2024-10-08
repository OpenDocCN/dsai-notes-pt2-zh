# P13：13.Mar_23_Lecture - Tesra-AI不错哟 - BV1aJ411y7p7

 Alright guys， let's get started。

![](img/ad312fe98e99c01ed03298543603234f_1.png)

 No protection for you guys。 I hope you had a good spring break。 Today is a full lecture on boosting。

 We're going to start with "Ada Boost" which we started talking about two weeks ago but。

 we'll review what we covered because it's been some time。

 And we're going to start by presenting "Ada Boost" as just an algorithm which is kind of how。

 perception was presented。 It was an iterative method and it was like a recipe for how to compute this prediction。

 function。 So we'll start presenting "Ada Boost" that way and we're going to kind of get a feel。

 for it， see how it's working， kind of make sure it at least intuitively makes sense， to us。

 And then we're going to present kind of a new approach to modeling called "Forward Stage。

 Wise Additive Modeling" and what we'll find is that "Ada Boost" is exactly an instance。

 of this new framework and the new framework is something more familiar to us and that we。

 can understand in terms of loss functions in terms of minimization， iterative minimization。

 algorithms。 So that's going to be nice to reframe "Ada Boost" in a more familiar setting。

 And then we're going to generalize a bit further to something called "Greedian" which will allow。

 us to move away from move to more general loss functions than the one that the "Ada Boost"。

 is minimizing。 So let's go on today。 So let's do a little bit of a review。

 We are talking about ensemble methods where we have multiple models that we combine together。

 We spoke about parallel ensembles which are like the random forests and the bagging but。

 today we're talking about sequential ensembles。 And the idea there is that you build a model。

 you see what data points it does well on and， where it does poorly and the ones that it does poorly on you increase the importance。

 of and then you make a new model that tries to do well where the previous model did poorly。

 And then you look at the combination of those two models and then you see， well where is。

 it still doing poorly and you try to repair， in each step you try to repair what's still。

 not doing well from the models you have so far。 Okay， we'll make that a little bit more clear。

 Alright， so we started with this idea of a weak classifier which is kind of a classifier。

 which we hope can do at least better than 50 percent， at least better than random guessing。

 on a classification problem。 Alright， I have some examples and so in adaboost the setting is strictly binary classification。

 Our weak hypothesis space or a weak learner produces hard classifications， negative one， and one。

 So we're not in the setting of scores at this point where our base classifiers are predicting。

 hard classes。 Alright。 So the question is， given this base hypothesis space and we have an algorithm for choosing。

 an F from this hypothesis space that does at least better than random on some training， step。

 can we combine F's chosen from this hypothesis space in some way that can do very。

 well on the training set， not just a little bit better than random。

 So an adaboost typical weak learner's typical base hypothesis space would be like decision。

 trees or even decision stumps which are trees of depth one。 Sometimes linear decision functions。

 Traditionally we do boosting with rather simple hypothesis spaces is not required but this。

 is where it seems to give the most benefit。 Okay。 So one thing that we'll need is this notion of a weighted training set。

 This is where every item of the training set has a， let's call it a non-negative real value。

 associated with it and we look to minimize a weighted empirical risk， a weighted， some。

 of the weighted loss functions。 We talked about this last time。

 So rather than just the average of the loss on the data points we have a weighted average。

 and we're going to need a， so we're going to either a need an algorithm that can choose。

 a function from our hypothesis space that minimizes the weighted empirical risk or there's。

 another possibility。 Do you guys remember the other approach to use？

 Suppose we don't have an algorithm that knows how to minimize weighted empirical risk but。

 it's a black box algorithm and we know it can minimize empirical risk。 So what was。

 we talked about this last time， do you guys remember what we can do？

 We'll try to figure that again because last time someone figured it out。

 Okay duplicate the training examples and what proportions？ Yeah， according to the weights。

 So the weights are non-negative。 We have a weight for every training example。

 If we normalize the weights so they sum to one， what does that turn into？

 This is like a probability distribution on the examples。 So if we draw our example。

 so we have a training set and then now we have a probability distribution， on the training set。

 Now imagine drawing a new training set according to this distribution。

 So and suppose you made it very large， so large that almost every data point appeared。

 multiple times。 So the number of times these data point appears is going to be proportional to this weight。

 if you draw enough examples。 So if you just add up the examples drawn up from that distribution。

 the normal empirical， risk on that resampled distribution will be very close to this weighted empirical risk。

 and you can feed those sampled examples into your black box empirical risk minimizer that。

 doesn't know anything about weights。 Is that clear？ All right。

 it's for a little slow coming off spring break but I saw some not。 That's a good start。

 That's a good start。 So we have， so now we have a way to fit a weighted empirical risk from a function in our base。

 hypothesis space and that's going to be something we will need to have。

 So here's the rough sketch of out of boost。 We have our training set。

 we start with equal weights on all the training points and now， we proceed in different rounds。

 So in each round we use our algorithm and fit our， a week classifier， something from a。

 hypothesis space to the weighted training points。 In the first round they're weighted equally so nothing special。

 So we get our week classifier and then we see what this GMX misclassified and we increase。

 the weight on the examples that were misclassified and then we repeat。

 So it's going to happen is if a point is misclassified repeatedly its weight keeps getting larger。

 and larger and every time we choose a new classifier it's going to be working harder。

 and harder to fit that one point or those points that have been misclassified before。

 because their weights keep getting driven up higher。 Yeah？ Yeah。

 so the question is it's great you're doing all this work to correct the things that。

 were wrong but are you not messing up the things that you had before？ This is。

 yeah it's a balancing act。 So the new classifier that you add may only get a little bit right than the one it was。

 working really hard to get and it made you terribly on the other ones it's true but we。

 actually combine it with all the ones we had before。

 So hopefully the ones we had before are still strong enough on the rest of the data points。

 that the new thing doesn't mess it up。 So this is the。

 this is kind of the balancing act that we'll see happening when we get into， the details。 All right。

 Okay， so kind of schematically we start the original training sample we get the first class。

ifier in the usual way。 Then we have a reweighted example based on what things were wrong。

 Those things that were wrong have a higher weight。 We get a new classifier based on that example。

 Then we take the same sample and reweight it again， et cetera and then we get M classifiers。

 Remember these are classifiers that output negative one on one， they're hard classifiers。

 And they've all been trained on different weightings of the same data set。

 And then what do we do at the end？ We take a linear combination of them and the specific way we do that we'll talk about shortly。

 And then we'll kind of value this linear combination going to be。

 Is it going to be negative one one？ No。 It's going to be a linear combination of negative ones and ones which are not negative one on。

 one。 It could be a real number， any real number so far。

 And then so we take the sign of it to convert it back to a classification。 Okay。

 That's the big picture。 Okay。 So what are these weights？ What are the weights？

 We combine the classifiers from each stage。 So the weights are going to be not negative。

 And as someone asked a few weeks ago， do we want to weigh the classifiers that did well。

 higher than the ones that didn't do well？ And yes， to some extent， yes。

 So we're going to see that the alpha M's are going to be larger when this classifier fits。

 the weighted data well， the weighted data that it received and smaller otherwise。 Okay。 All right。

 So let's talk about round M， an arbitrary round M。

 We get this classifier GM and it gets a certain weighted error。

 So this is where we count the misclassification， this is kind of the zero one misclassification。

 rate。 Instead of just adding up or getting the percentage of errors。

 we're going to weight those errors， by the weight of the individual example in that round。

 So if we were really trying hard to get example I correct， the weight was really high。

 Why would it be high？ Because we kept getting it wrong in the earlier rounds。

 So if we were really trying to get the i'th example correct and nevertheless we got it， wrong。

 we're going to count that higher in our error。 So weighted error。 Good。 So ERM， error。

 we'll call it the error of the Mth round， error sub M， that's going to。

 characterize how well our Mth classifier did on this weighted training set。 All right。

 And you notice it's between zero and one。 Is that clear？ Why is this between zero and one？

 It's clear。 If you look at W I divided by capital W is the sum of the W I。 So W I over W。

 that's like a probability。 If you add them up in sums to one， they're all non-negative。

 So this is like taking a convex combination of things that are zero and one。

 So that's certainly between zero and one。 Yeah。 So the implementation of the fields is going to take one of the errors in the same。

 Correct。 And we initialize all the W's to be the same。 That's right。 Yes。

 How do I decide the order of the classifiers？ [INAUDIBLE]， [INAUDIBLE]， [INAUDIBLE]， [INAUDIBLE]。

 [INAUDIBLE]， [INAUDIBLE]， [INAUDIBLE]， [INAUDIBLE]， [INAUDIBLE]， Let me come back to you。

 I'll come back。 Yes？ [INAUDIBLE]， Say again？ [INAUDIBLE]， Outlowers in the data， yeah。 [INAUDIBLE]。

 It could be an issue。 So the question is what about outliers in the data？ Can we overfit？ Yeah。

 Out of boost is known to have some overfitting issues。 We'll come back to that。 Good question。 What？

 I don't call it overfitting so much as performance not being great in the case of outliers。

 Overfitting I don't know。 Well， maybe it's overfitting， yeah。 [INAUDIBLE]， That is ridiculous。

 I didn't understand your question。 I'm not going to say that。 I'm not going to say that。

 I'm not going to say that。 I'm not going to say that。 Now we have a weighted training set。

 Now we're here， weight set number two。 Now we fit to minimize the weighted loss。

 weighted empirical risk。 You got it。 We just needed a recap。 Then we get classifier number two， G2。

 Then we repeat G3。 Then at the end we take a linear combination。

 Now at this point we're saying a non-negative combination of these classifiers。

 That's going to be predicting real value numbers， scores。 Then we take the sign to get a classifier。

 We have a weighted training set。 It's just two weights because we have two。

 It's a plus-one minus one。 Are there only two weights that will be the sign of the term？

 In the first round you are correct。 In the very first round there's a symmetry。

 Every point has either been classified correctly once or incorrectly once。

 If we reweight depending on just on whether it was correct or not， then you're correct。

 Everything in the second round will have one of two weights， but not so in the third round。

 There are things that were correctly classified once or twice。

 It turns out it's not just how many times it was classified。

 but it's also related to how well the classifier did in that round。 How do you do it？

 That depends entirely on the question。 The question was how do you minimize the rate of zero and error？

 I gave -- so version one。 We reduce it to the case of minimizing regular zero-one error by this re-sampling of data proportional to the weights。

 I don't know if you were here for that part。 One version is by re-sampling proportional to the weights you reduce it to minimizing zero and error。

 You could say we don't know how to minimize zero and error， and that is true。

 You don't have to minimize -- you aim to minimize zero and error or the weight of classification error。

 but you really just need to do better than random guessing。 Adjust the weight class bar？

 Just a week class -- yes。 Just a week classifier， right？

 The exact amount that we'll be weighted by -- in every round。

 we'll see that everything that was incorrectly classified gets scaled up by the same factor depending on the round。

 The weight -- the fact that it's multiplied by the same amount。

 Why don't we look at the next coming slides where we get into that？ Yeah。 Yeah。 Sure does。

 It looks at every data point unless -- well， yes。 You never get zero weight， so yes。

 It looks at every data point in every round。 That's right。

 It may almost ignore certain data points when the weights get very， very small， which happens。 Yes？

 Would it be possible to have data points get zero weight in order to speed up your error power of those？

 So， okay， ignore it。 That's a great question。 I haven't heard of anyone doing that。

 but I like the idea。 So， maybe you could have a threshold。 Like， if the weight gets really small。

 you just set it to zero and you pray that it never stops classifying that correctly， subsequently。

 It's worth the try。 I don't know。 Okay。 It's interesting。 But it's the right idea， I think。 Okay。

 All right。 So， let's -- you guys are hungry for the actual specifics， so let's just get there。 Okay。

 All right。 So， this was， let's say， answer your question。 So。

 we want to treat the weak learner as a black box。 We can use any method we want。

 but we want to at least have kind of weighted error less than a half。 Okay？

 That's sufficient for what we're going for。 Okay。 All right。 Now， the weight of the classifier。

 how do we do the reweighting？ Here it is。 So， we reweight by this factor alpha。 Here's a formula。

 log of 1 minus the error over there。 I don't know exactly -- doesn't mean anything to me directly。

 but I plotted it so we can just look at it。 So， on the x-axis， we have the error。

 This is the overall error -- the overall weighted error of the classifier， right？

 The weighted error。 And if we have the no weighted error， alpha is very high。

 And as the weight error gets closer to a half， alpha m goes towards zero。 What's alpha m？ Yeah。

 Alpha m is the weight of the classifier when we -- so remember at the end。

 we're going to add all these classifiers together。

 And the weight that classifier enters the non-negative combination is alpha m。 So。

 alpha m big means it gets a lot of weight。 Alpha m swam means it gets very little weight。 So。

 if the classifier has really bad weighted error， then it's going to have very little weight in the final。

 Okay。 All right。 That kind of makes sense。 The shape at least is in the right direction。 So。

 now that's the weighting of the entire classifier。

 And now the other thing we need to know is how we reweight the individual examples， right？

 In each round。 Okay。 So， let's take a look。 So， let's suppose alpha m is the weight of gm。 So。

 it turns out we're going to use alpha m also to help us reweight the individual examples。 So。

 suppose w i is the weight of example i before the training。 And if gm classifies xi correctly。

 the weight is unchanged。 All right。 So， in every round any example that was correctly classified。

 we don't touch it。 Otherwise， we adjust it。 We increase it by a factor。

 All of the weights of all the incorrectly classified examples are increased by e to the alpha m。

 That's our factor。 All right。 Well， e to the alpha m that counts as the log。

 but we can look at that too。 So， this is the adjustment to the weights for the incorrectly classified ones。

 All right。 So， the shape of the say， and the only difference is that now it's on a log scale on the x-axis。

 All right。 So， interpretation。 Or let's do a little bit of a recap。 So。

 every example that's misclassified in a particular round has its weight rescaled。

 Is it increased or decreased？ Increased。 Good。 And everything is rescaled by the same amount。

 They may， they still end up at different values because they started at different values。

 But the factor you increase them all by is the same。 And the factor is， yes。 I do。

 We start everything in round one with the same weight。 Say one for everything。

 Everything that's misclassified is rescaled the same amount。 So， if it's a doubling。

 all the ones that are wrong are rescaled by the same amount。 Yes。

 Only ones that are wrong are rescaled in each round。 That's right。 So。

 if we started all at once and there's a particular example that's always classified correctly in every round。

 it stays at one。 Yeah。 So， if it's a variable， we don't want to take into account how much it was。

 No， that's correct。 There's no， so the， the question was。

 suppose we had a base classifier that didn't just output negative one on one。

 This is highly restricted to hard classifiers。 So。

 there is no score given by the functions in these hypothesis spaces。

 It's just a plus one or a minus one。 You could ask。

 suppose our hypothesis space gave classifiers of confidence。 Can we leverage that somehow？

 Is the question。 I think we can， but not out of boost。 It's not out of boost。 Yeah。 Yeah。

 [ Inaudible ]， We'll rescaling increase the error。 I'm not sure it can be a little more clear。 So。

 you're rescaling the weight on a data point。 So， the error of what？

 Our goal is to come up with a function that performs， at this point。

 our goal is to find a function that minimizes the overall training error。 That's right。

 I'm using data rescaling as a piece of the process to get to minimizing the training data。

 That's correct。 So， that the question I think is basically like， does this thing actually work？

 [ Laughter ]， politely asked。 We'll come back to that。 All right。 Okay。 [ Inaudible ]。

 Did I say there's a lower error for higher weight？ Okay。 So， if the -- okay。 So， lower error。

 higher weight， give me on what？ So， error is the weighted error for a particular classifier around M。

 say？ Okay。 I thought you were rereading the training。 We -- yes。

 We weigh the classifiers by our FEM， and that's the amount that it gets multiplied by before it's added into the sum of classifiers。

 So， there's a weighing of the individual classifiers。 That's one piece of it。

 And then there's also a re-waying of the examples in each round。

 And what's interesting is the factor by which we re-way the examples is related to the factor that we used to multiply the classifier by。

 We're using alpha M。 Alpha M is involved in both cases。 Yeah？ [ Inaudible ]， Okay。

 Can we use alpha M as a confidence score of the classifier？

 Alpha M is related to how well it does on the weighted error。 So。

 in -- it's a -- it's some measure of performance。 It may be only vaguely related to how helpful it is to the final classifier。

 But --， [ Inaudible ]， That's correct。 [ Inaudible ]， It sounds like a "why does this work？

" question。 We'll come back to it。 Let me get through some more slides。

 and then we'll come back to these questions。 All right。 So， here's kind of the overall algorithm。

 Everything we talked about already。 So， I don't think we need to dwell on this。

 Here's a little bit of an illustration。 So， we start with -- our input space is the -- a box of size one by one。

 And we have two classes， red and blue。 And we have -- so this is our first classifier。

 After one round， what do you think our base classifier -- our set our base hypothesis。

 base is if this is -- what？ Huh？ Threshold function。 Yeah。 Okay。 Decision stumps。

 This looks like decision stump。 A stump is a tree where you only have one split。 So。

 here we've split on the x-axis at whatever point -- negative point one or something。

 And to the left we're predicting red and to the right we're predicting blue。

 The color being black and white represents how big our score is for each color。 All right。

 Let's do another round。 It'll be more clear。 All right。 So， what's going on here？

 Now the -- all the points are of different sizes。 What do the sizes represent？

 There are the weights at this particular round。 All right。 So， after three rounds。

 the weight of this red thing right in the middle of the blue zone。

 is very large because it keeps getting misclassified。 So， after three rounds。

 this point has a very large weight。 All right。 These points deepen in red zone and correctly classified are quite small。

 They're like spots。 So， okay。 We've been saying that the weights stay the same or get bigger。 So。

 this is rescaled so that they don't get too ginormous。 These are the ones that are the smallest。 So。

 in our version， that would be like -- they would still be at weight one。

 But here we've kind of rescaled to keep them proportional。 Okay。 So， this is the most confident red。

 The score is the maximum and then the spray is a middle score。

 And then this white is -- score at the other extreme。

 And the final thresholding is given by this yellow line。 Okay。 Any questions on this picture？ So。

 let's look at one more round or after 120 rounds you see this -- the decision value can get quite complicated。

 This is far more complicated than a single decision -- all right。 So。

 this is one decision stump by basically linear combination of those。

 We get this more complicated boundary。 And here we get something that's quite complicated。 Okay。

 And then you see the blue。 Now the blue ones are very large because they've been -- now these blue guys are deep in red territory and they keep getting misclassified。

 All right。 All right。 How's this picture settling with you guys？ Good。 Let's clarify some things。

 Okay。 [ Inaudible ]， Wow。 That's a great question。 So。

 I guess it hasn't -- I guess it's had enough times that it wasn't correctly class。

 but -- that's a good question。 Yeah。 [ Inaudible ]， Yes。 [ Inaudible ]， Yeah。 So。

 I think what you're -- I think what you're saying is correct is that -- let's say if you can match it up exactly。

 I don't know if I have a line that pictures well enough。 I wasn't expecting this close examination。

 but let's suppose that， indeed， see this little yellow thing， that's changing the class there。 So。

 this is -- I don't know。 Would you say this to me looks like overfitting？ All right。 Okay。 So。

 I have other ways to work on overfitting issue。 But do you have any ideas right now of how you might prevent overfitting with this type of algorithm？

 Limit -- oh， limit your number of iterations of steps of rounds。 Yeah。

 we could stop running out of this at a certain point。 Maybe use validation error to say， all right。

 that's enough。 We're getting worse。 Okay。 All right。 All right。 So。

 now we've come to the question that you guys had。 But so -- so， so far， just overall in the class。

 we've kind of seen -- the main type of thing we've done is set up things as convex optimization problems。

 Like we had L1 regularization， L2 regularization， SVM， kernelized versions of these things。 And。

 you know， there are convex。 You kind of do any reasonable optimization algorithm and you're going to get to the right place。

 In the end。 And those were -- those were quite nice。 And then we had trees。 In trees。

 we know what we wanted to do。 We just didn't know algorithmically how to do it exactly。

 So we described this kind of heuristic process of building a tree out and then trimming it back。

 which people find work pretty well。 You're choosing something from the hypothesis space of trees。

 There's no proof。 In fact， we don't know how to actually find the best tree -- the best hypothesis space。

 So -- but anyway， we have an algorithm for optimizing the trees。

 I was making a different point in that bullet， but that's okay。 So， ada-boost is something new。

 It's just an algorithm， so I mentioned earlier。 So it's kind of like the perceptron algorithm。

 So we have to ask the question， like， will this minimize the training error？ At this point。

 that's the goal。 Eventually， we want it to do well on test error。 But for starters。

 we need to have it be doing something reasonable on the training error。 So there's a theorem。

 It's not too hard， but it's too long for lecture。 And may put it in the homework as an optional problem。

 It's not too hard with some guidance。 So it is true under pretty minimal assumption。 All right。

 So here's what we need。 We need it to be an actual weak classifier。

 So we need it to have weighted error less than a half。 So we define this term called the edge。

 The edge of a classifier is describing how much better than random it is。

 So it just takes a half minus there。 So now we want a big edge。 Big edge is good。 Big error is bad。

 Big edge is good。 So it's measuring something like how much better than random GM is performing。

 So here's a theorem， which we'll kind of try to figure out what it means in a minute。

 The theorem is the empirical 0， 1 risk。 This is the original error， not the weighted error。

 This is the thing that we actually want to minimize in training。

 The empirical 0 and risk of out of whose classifier GX。 What is GX？

 It's that non-negative combination of the individual classifier。

 the weighted classifiers at each round。 So it's like alpha 1 G1 plus alpha 2 G2 up to however many rounds we ran。

 So what's on the left here？ This is the risk on the training data。

 the average number of the percentage of errors basically。 It's bounded by this product。

 So what is it？ It's in terms of gamma m。 Gamma m is the edge of the individual classifiers。

 So would you think big edge should be better， right？ Big edge is far from random。

 So this thing is big， but if this thing is big， this thing gets small， and we're multiplying。

 a bunch of small things together， so it's small。 So this， when gamma is big， this product is small。

 and that's good because we want， that's the error。 It's bounding the error on the left。

 Let's look at some examples。 Alright， suppose the weighted error is less than 0。4 for all rounds。

 just to see what it looks like。 Then the edge is 0。1， because how much better than 0。5 we are。

 And then we get that the error rate is bounded by 0。98 to the m， bounded by 0。98 to the m。 So great。

 so if m， the larger m is， the more rounds we run， that thing goes down exponentially， fast。 0。

98 is bad。 If we only run for one round， that's not a good bounded off。 But if we multiply 0。

98 against itself many times， that thing goes to 0。 So if we run for 100 rounds， the bound is 0。133。

 200 rounds， 0。018。 Okay， so the upper bound decreases exponentially quickly。 Let's go。 Yeah。 Okay。

 so I made one big assumption to make this picture， to make these numbers。

 What was my assumption that I made？ I assume that the error is always less than or equal to 0。4。

 So if I could do that， this is the result。 So you might ask， well， so your question was。

 does this work for all hypothesis spaces， right？ Okay。 Okay， no。 Suppose we have hypothesis space。

 for which we're not able to get any edge at all。 We can't do better than random guessing。 Well。

 then we won't have this error bounded away from a half， and we won't be able to get。

 exponential decrease， perhaps。 So another question would be， well， suppose， all right。

 test question。 Suppose the edge is， or suppose the error is bounded by 0。4。

 Will we always be able to get 0 error on the training set？ So， yes。 Is the proposal， and I agree。

 The bound goes down to， as long as the， if the edge is always， if the error is always bounded。

 away from a half， then we're always going to have exponential decrease on the upper bound。

 and eventually the error is going to go to 0。 And it will be exactly 0， right？

 Because on the left-hand side， this will get arbitrarily close to 0， and the smallest non-zero。

 thing， the thing on the left could be is what？ What's the smallest number？

 The thing on the left can be that's bigger than 0。 1 over n， right？ So on the right-hand side。

 we'll eventually be less than 1 over n， so that drives the left-hand， side to 0。

 So if we can always guarantee the error is less than a half， strictly less than a half， then。

 the right-hand side will always go to 0。 So this should tell you that if you have a training set without liars。

 with points that， aren't， you know， where the red and the blue are not separable by some kind of linear combination。

 of your base hypothesis space， so if your hypothesis space can't do it， if you're taking linear。

 combinations of things in your hypothesis space is not able to separate your data， then you。

 can't possibly get zero training error， which means you can't possibly have the error always。

 less than a half， the weighted error of a given round always less than a half。

 Any questions on this？ Yeah。 [ Inaudible ]， Yeah， so out of exactly。

 So the question is what we classifier can we use？ Yeah。

 out of boost basically takes a black box classifier， preferably one that can handle。

 weighted training data， but if not， you have to do your sampling trick to make use of it。 But right。

 algorithmically， you can use any classifier you want。 To get this type of theorem to work， yeah。

 question？ [ Inaudible ]， So the question is， is there any reason that people use these simple classifiers instead。

 of something more sophisticated？ Okay， I think the empirical example reason is that they tend to work well。

 People have run experiments， playing people run experiments where you fancy your classifiers。

 like SVMs and stuff， and you can get some benefit from boosting SVMs， but not so exciting。

 What types of classifiers do we have in our tool chest that we might want to use？ Right。

 we have these linear classifiers。 So that's kind of not as exciting to take linear combinations of linear kind of prediction。

 functions。 Trees are nice because they have these nice nonlinear properties。 [ Inaudible ]， Yeah。

 [ Inaudible ]， Yeah， so the point is that if there's a notion of generalization error。

 which is how well you're， going to do on your test data compared to how you did on your training data。

 and the more， complicated your base classes， you're exposed to having bigger generalization errors。

 so， bigger， you know， overfitting essentially。 So yes。

 that's a good point that as you increase the complexity of your hypothesis space， then。

 you're potentially overfitting， but really we， in any case， we're going to do early stopping。

 or something， so we're not really going to overfit， right？ It's just a different tradeoff。

 It's just --， [ Inaudible ]， Yeah。 Yes。 [ Inaudible ]， The pictures？ Sure。 [ Inaudible ]， Sure。

 [ Inaudible ]， [ Inaudible ]， [ Inaudible ]， The reason we decrease errors is because we have more --。

 [ Inaudible ]， So the question is why are things --， Okay。

 So why are we doing better after three rounds than we did after one round？

 It's one of the questions。 Okay。 So one reason that we can do better after three rounds than after one round is because by taking。

 these linear combinations of decision trees， of decision stumps， we get a more complicated。

 boundary that cannot be represented by a decision stump。

 So our effective hypothesis space after three rounds is bigger than after one round。

 So that's -- it's just a more expressive set of hypotheses by the third round。 Yeah。 [ Inaudible ]。

 So the question is， is this -- will we get the same boundary if we run a decision tree with three splits？

 [ Inaudible ]， No， no， not necessarily。 Because you may say， is it the same -- one question is。

 is it the same hypothesis space that you're， selecting from？ You can say。

 is every decision boundary that we can get from three rounds of boosting on。

 stumps the same as the set of all decision trees with， I guess， three splits or three nodes？

 [ Inaudible ]， Maybe。 I'm not sure。 But --， [ Inaudible ]， Well。

 but none of the minimization is exact， right？ For trees。

 we have a method that's an approximate method to figure out the right tree。

 Adebust is another way to end up with the hypothesis in that set。

 Even if the hypothesis spaces are the same， the way we choose them is not the same。

 So it's an interesting question whether the hypothesis spaces are the same。 But in any case。

 Adebust and just choosing a decision tree directly of that size are two entirely different trees。

 you're going to end up with。 Yeah。 [ Inaudible ]， You're definitely not going to end up with the same tree。

 The question is， is the hypothesis space -- the hypothesis space of after three rounds of boosting。

 with decision stumps the same as a certain type of decision tree that you can easily describe？

 Maybe。 Cool。 Okay。 All right。 I'll show you a few quick questions。 Okay。

 So it's a curious property of boosting， which is that people often -- this was kind of a mystery in。

 I don't know， ten years ago or something。 So as we run Adebust through many rounds。

 what you would expect to happen is that as the number of rounds increased。

 your training error would go down， down， down， maybe reach zero in this case。

 The test error would reach a minimum and then go back up。

 So what people often realize found though in practice is that it didn't actually look like that。

 What they found was that the training error may go down， but the test error kept going down。

 Just kind of interesting。 So they have some explanations of this。

 They kind of go beyond the scope of this course， but this is kind of the topic for like a fundamental machine learning class。

 I don't know if they cover the specific topic， but this is an interesting thing in the lore of machine learning that。

 boosting -- Adebust have this unusual property。 But one thing that tells you is that -- and we're going to refer back to this -- is that there's something special going on in the Adebust algorithm。

 Remember， Adebust is like a recipe。 What's coming up next in the second part of this lecture is we're going to show that Adebust is actually minimizing in some sense a particular loss function in a particular way。

 And what we know is that if you just minimize a loss function for hypothesis space。

 this is not typical behavior。 So there's something special about how Adebust is minimizing this loss function that gives us this interesting behavior。

 All right， let's take a break then。 See you in 10。 [sigh]， Yep。 [sigh]， Can you use anything？

 People usually use trees。 Yeah， you have to decide。 [sigh]， Not often。 [sigh]， [sigh]， [sigh]。

 [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]。

 [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]。

 [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]。

 [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]。

 [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]。

 [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]。

 [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]。

 [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]。

 [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]。

 [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]。

 [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]。

 [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]。

 [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]。

 [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]。

 [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]。

 [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]。

 [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]， [sigh]。



![](img/ad312fe98e99c01ed03298543603234f_3.png)

 [sigh]。

![](img/ad312fe98e99c01ed03298543603234f_5.png)

![](img/ad312fe98e99c01ed03298543603234f_6.png)