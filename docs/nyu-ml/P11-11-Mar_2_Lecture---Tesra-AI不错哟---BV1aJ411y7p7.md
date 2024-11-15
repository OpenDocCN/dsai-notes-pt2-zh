# P11：11.Mar_2_Lecture - Tesra-AI不错哟 - BV1aJ411y7p7

 All right， let's get started。

![](img/87d31aa83b168b3b70a725b27b58fb7a_1.png)



![](img/87d31aa83b168b3b70a725b27b58fb7a_2.png)

 So last Thursday， I guess most of you were here， we started talking about trees， which。 are our first truly nonlinear--is there feedback or is this okay？ And there's feedback。 Okay。 Anyway， so we talked about regression trees last week。 I want to finish up the trees unit by talking about classification trees。 It will take， I think。

 at most the first half， probably less。 And then we can talk about questions you guys might have for the short test tomorrow。 Some people posted on Piazza and then we can see if you guys have questions that you， want to ask。 I think at this stage of the game， I might focus--if you haven't already reviewed the。 lecture slides， I would probably go back over the slides at this point and maybe the。

 statements of the problems from the homework just to refresh。 If you haven't already done that。 that's probably what I would do in a limited amount of remaining， time。 All right。 classification trees。 So quick review on what a tree looks like。 We have--we're dealing with binary trees where at each node we pick one feature。

 We're dealing with continuous features right now or ordered features and we choose a split。 point and we go left to right depending on what side of the split that features on。 And as we go down the tree， we eventually reach leaf nodes and each leaf node corresponds。 to a particular rectangular or kind of--or higher dimensional the analog of a rectangle。

 a rectangular region that gets a particular prediction。 Every input--every element of the input space that falls into a particular region， parallel。 pipe and region that would correspond to a leaf node has a single prediction that's produced。 the same prediction。 And then for regression， it's going to be--we found the average of the y values in the leaf。

 nodes and then for classification， what do you think it would be for classification？ Bless you。 So in our training set， we found all of the labeled data points that fall in， say， R5。 And it's not a classification problem。 So there's going to be some of class one。 some are going to be a class two， some are， going to be class three， which class should we predict？

 >> Majority。 >> Yeah， the majority。 So when we want to predict on a new example that happens to also fall into R5。 we will， predict with whichever class showed up， the most frequently， in R5 in our training set。 Very natural， straightforward。 Any questions on that？ Set up？ All right， well， almost done。 Okay。 So the general tree building procedure is we start at the root， we look at our features。

 we choose a splitting variable， it's a particular feature， and then we split point and that splits。 our input space into two regions， R1 and R2。 So compared to the regression trees that we did last week。 we're going to need to modify， a couple things。 One is how we split the nodes and then how we prune。 but we're not going to talk about， oh， briefly mention how we're going to prune for classification trees。

 It's basically the same。 All right。 So let's see how we're going to do that。 So it's no extra cost related to consider K classes as opposed to just binary classes。 So we'll do a K-way classification tree and let's consider a D dimensional input space。 And so our splitting variable is choosing one of these D variables to split on and let's。

 continue to consider real value features。 So we're going to。 the split point will also be a real value。 And then some notation。 we had R1 and R2 for the region of the input space that's to the。 left of the split point and to the right of the split point。 All right。 All right。

 So a little bit more notation。 We're going to， so when I say a node。 what am I referring to a node of the tree？ So let's say， but I'm saying it represents a region Rm。 We're mostly， we're interested at this point in like leaf nodes where we actually care about。 the regions of the input space that are associated with that node。 All right。

 So suppose we have region Rm。 Rm is the points that fall onto the mth region or the mth leaf nodes and there's n sub。 m points in that region in the training set。 And let's define the proportion of items in the training set of class K out of all of。 them out of the， oh， another bug。 This should be， what should this be instead of m if you're following me？

 This is counting up how many items of class K we have in region Rm and we're dividing。 by something because we want to come up with a relative proportion。 Yeah， good。 And this should be n sub m instead of m。 Good。 You're following？

 So we're going to call that P hat mk。 It's the proportion of class K in node m。 Clear？ Okay。 All right。 And so our prediction is going to be looking for whichever class proportion is the highest。 Right？ Good。 Good。 So we're going to call it m sub k max over k of P hat m sub k。 So k is the class。 m is the region。 Very good。 So we want to predict， we're going to predict k of m。 We can also。

 that's when we want to predict a single class。 We can also predict the whole probability distribution。 Why not？ They're the obvious things you predict the relative proportions of each class。 So now we have almost for free， we can predict the whole distributions of our classes using。 the proportions in the node。 All right。 Cool。 All right。

 So now we've set up how we're going to do our predictions。 Let's go back to predicting a single class for a node。 How can we compute our class。 our expected misclassification rate for a particular node？ Suppose， for example。 we're predicting km because it had the highest P hat m sub k， the highest， proportion。

 Based on this training set， what would we expect the misclassification rate for an input。 element that falls into the mth region of the space or the mth node of the tree？ Yeah。 I'd say 1 minus P hat mk。 Right？ If in our leaf node 30% of the training examples were of class 2 and that was more than all。 the other ones， maybe it was like 5% class 1， 8% class 2 and there's lots of spread and。

 30% happens to be the highest。 There must be a lot of classes。 Well。 probability of error is maybe like 70%。 If 30% were of the class of predicting 70% were not。 So that would be our estimated probability of error for that prediction。 Is it clear？ Yeah。 1 minus P hat mk。 All right。 So we know how to figure out what we're predicting once we have the split。

 the partition of the， space。 So what's left is how do we partition the space？

 How do we figure out the splitting variable and how do we figure out where to split it？

 What we're going to talk about is how to evaluate how good the split is。 All right。 There's lots of ways to do that actually。 Do you guys have any ideas？ Whoa。 Okay。 So you're very good。 Entropy information gain。 Yeah。 So good inventions。 I would not have come up with that。 Very good。 So what I would have thought of off top of my head would be a misclassification rate。

 Right。 So if there's a particular split， you can estimate the probability of misclassifying a prediction。 based on that one split。 All right。 So that's one way to measure it。 And then there are fancier things which we'll end up preferring。 That's right。 All right。 So we call these measures of how good the split is。 This node impurity measure。

 And that's getting towards the idea that we really want to head towards leaf nodes that， have。 we want most of the training examples to be cronced， traded on one class so that。 when we prick that class， we're correct。 All right。 So that's。 that's certainly explains the leaf nodes。 But misclassification error would be okay with that too。

 And the information error is basically what I said we want to optimize。 But there's a little bit more to it。 We want to have this notion of node impurity。 So we'll look at a couple of pictures。 All right。 So we want as close to a single class in a node as possible。 And then it's just a matter of how do you measure that？ All right。 Okay。

 So this is a plot of different measures in a situation that we have binary class。 So two classes。 And the x-axis is p， which is the relative proportion of say class one in the training， data。 And what we want， so the worst， what's the worst possible relative proportion of the， best class？

 Yeah。 For two classes， point five。 That's like complete uncertainty。 You're。 that's the worst possible error you can get for two class。 Right。 And the best would be zero or one。 And so if we look at this， you think of these as losses or impurities， things we want to， minimize。 then the best is at the extreme， zero and one。 So we want， we want to。

 we certainly want to encourage totally pure nodes。 And 50/50 is the worst。 And then there's different penalties in between。 All right。 Okay。 So these are。 these are the actual formula， giving those curves in two dimensions here。 They're generalized into。 for two classes here， they're generalized to k classes。

 I think you'll have some opportunity to kind of get used to these things and get a feel。 for them in the homework， in the next homework。 The first one is simply misclassification error。 This one is called the genie index。 It looks a little bit familiar。 It feels a little bit like the measure of variance of a boronary variable。

 It's kind of like a variance type thing。 This on the other hand is kind of like an entropy。 Well。 this is the entropy。 This is the entropy of a， they're quite cross entropy for various reasons。 But I brought entropy because this is the entropy of the distribution represented by。 the relative proportions of each of the classes。 Okay。 All right。 So here's a picture。

 So on the left we have our data comes from four classes。 And on the right is the relative proportions of the four classes overall。 Even splits， right？

 All right。 So now let's test out one particular split。 Let's start with one on the top。 So we're splitting right down the middle from left to right。 So we have the top half and the bottom half。 This little histogram here is the relative proportions of red。 blue and yellow as are in， the top half。 Can you see this？ There's no green up。

 There's no green anywhere。 All right。 I have to refine my color descriptions because green is not coming out on the projector。 So these were green if you're looking on your computer。 But on the screen we'll call them yellow and these are orange。 Aren't they？ Darker yellow。 Darker yellow。 Golden。 All right。 So we have mustard color here but no yellow。

 And here we have yellow but no mustard。 All right。 Fine。 Now let's compare to the one on the bottom。 So on the bottom we have only two classes。 Pretty evenly split。 And on the right we have two classes evenly split。 Intuitively roughly maybe the bottom one's better because we have fewer classes。

 We've at least gotten rid of two classes from each。 Well， the measure itself。 here we've written information gain which is actually directly， related to entropy。 But big information gain is small entropy。 There's a little formula for it。 So this has larger information gain so small entropy。

 So this would be the preferred split over this one according to the entropy measure。 Okay。 I mean I can give a quick better example of why you might prefer something with higher， entropy。 Suppose we had， let's use the same number of classes， four classes。 And suppose we had a split that gave us， let's just look at one half of the split。

 So two classes that are almost exactly equal。 Maybe this one's a little bit higher。 Verse another one which was this is exactly the same。 Let's say this is 0。51， this is 0。49， oh boy。 48 and 52。 And then this one is also 0。52。 And then suppose this split had the same weight spread equally over two classes。 And each of these are 0。24。 Okay。 All right。 So what's the probability of misclassification for each of these situations？

 So again， it's the same。 It's 0。48 whether it's this or this。 Which one do you think you would prefer？ I think this one because we've already gotten rid of one class entirely。 All right。 So that's intuitive。 And then， okay， mathematically under entropy。 which of these distributions has higher entropy？ This bottom one， why？ Okay。 Well。

 you have to know for starters that entropy is maximized over a distribution over a finite。 set of elements has maximal entropy when it's a uniform distribution spread evenly among。 all of them。 So this you have to know to reason about this example。 Okay。 given that kind of conditional that we're in these two classes， splitting the way equally。

 between these two classes has far more entropy than splitting the weight unequally with all。 the weight on just one of the classes。 So condition on， we have 0。4 probability on these two classes。 The maximum entropy is to split it evenly。 Okay。 So if we minimize entropy， we're more like this。 And this kind of tells you why you want maybe to do something better or more than just misclassification。

 rates。 Any questions on that？ Okay。 Well， that's the idea。 So then all that's left is how do you find the split？ Now that we know， well。 we know roughly how to evaluate it。 There's some details I didn't tell you about how to evaluate this split。 right？ Let's hope that that's in the next slide。 All right。

 So we have our splits RL and RR for left and right and the number of points RL， let Q of。 RL and Q of RR be the node impurity measures for the two splits。 So it's either going to be the entropy or it's going to be misclassification rate or it's。 going to be the genie。 And so each split gives us two scores。

 one for the left side and one for the right side。 So the question is how do you combine them？ Yeah。 you could just add them。 The issue potentially is that what if one side of the split has far more points than the。 other one？ Yeah。 So what we do is we take a weighted average。 weighted by the number of points in each。 Exactly。 So we look for us。

 so here's the weighted average。 So the number of points on the left side times the impurity measure of the left plus the number。 of points on the right times the impurity measure of the right。 And we search for a split that maximizes or minimizes this。 Minimizes this because it's impurity。 Right。 We want to minimize the entropy， minimize the misclassification rate。

 So we're going to minimize this over all splitting variables and all splitting points。 Okay。 So do you have， do you， we know how to do this。 We talked about roughly how to do this last time。 And I guess the question is does the insight we made last time apply to today？ So first。 how do we decide to do it last time？ So let's suppose we pick a particular variable to split on。

 The question is what points do we use for the split？

 And the insight was that you don't have to check every real value in the range。 You only have to check the split points that are aligned with the actual values attained。 by the input points on that feature。 Because if you have two points here and here that are adjacent。 there's no other points， between these two， then it doesn't matter where between those two you split it。

 They all give the same split。 So you only have to check the possible split points that align with a value of a training。 point。 Okay。 So does the same approach work here when this is what we're optimizing？ Yes？

 >> Does it take a bit to try the middle value between actual values？ >> Okay。 That's interesting。 So the question is does it make sense to put the split right in the middle of the two adjacent。 values？ I like that question。 Yeah。 So， all right。 So the intuition would be okay。 It doesn't make any difference on the training set。

 But maybe if you're maximally distant between those two points， it might actually perform。 better on the test set。 That's interesting。 I buy the intuition。 You'd have to try it out and see if it matters。 Anyone else have a thought on that？ Good。 Okay。 All right。 So as we kind of mentioned， genie and entropy are the preferred methods for growing the tree。

 because they tend to get more pure nodes。 All right。 Remember last time there was a second step。 So we build the tree out and we have some stopping criteria for when we stop splitting， nodes。 And that was for example when a node has fewer than a fixed number of training examples。 we stop splitting it。 So 5， 10， something like that。 But then that potentially over fits。

 We want to control the complexity。 So then the second stage， this is the method of cart。 The second stage is to prune back these nodes。 And when we prune， we can either。 if you remember last time， what we were doing is we， are。 the first step of pruning was to find the node to prune， a single node to prune that。

 would reduce the risk by as little as possible。 Remember that？

 And then we found the next one to prune that reduced the risk by as little as possible。 Reduce the risk。 Increase the risk。 Increase the risk by as little as possible。 Increase the training error by as little as possible。 So that was for square loss。 So that was very clear。 Here what should we do？ We can find the node to prune that would increase the impurity by as little as possible。

 We could do that。 If we build it with Gini， should we prune with Gini？ And if we build it with NGP。 should we prune it by looking at NGP2？ Feels like intuitively to me， once you're already built out。 we use these other impurity， measures because they made the splits have properties that were appealing。 like they， were pure。 But once we've already built the tree and now at the pruning stage。

 the splits are already， set。 Now we should focus our site on what we're actually trying to optimize。 which is not actually， the impurity measure。 It's the training error。 It's the classification。 it's a misclassification error。 We're going to minimize the misclassification rate。 So when you prune， it makes a lot of sense to prune using the misclassification rate as。

 your criteria instead of the impurity measure。 You guys buy that？ That's pretty reasonable。 So that's all I had to say about classification trees specifically。 I had one additional comment on trees in general that I don't think I made last time。 So it's that trees make no use of geometry。 So what do we mean？ For linear methods。

 all the methods and all the methods we talked about that were kernelizable。 it's basically we're making use of an inner product in the input space where we have this， W。 the weight vector， and we have an input example X and we take the inner product between。 them and we come up with a number and maybe we add a bias。 And if you can visualize。

 so the inner product represents the geometry of the space。 It tells you about angles and it can tell you about lengths。 And it's a way to directly， well。 I'll leave it at that。 In trees， there's nothing like that at all。 There's no structure of the space that you're using except one thing。

 What's the one thing we're assuming about the input space for trees as we've presented， it？

 What does the input space need to have？ What characteristics？ Say R。 So again？ Yeah， so yeah。 We built it up in R or so it's called R D because we've been using D。 Okay。 Could we relax it from R？ So there's reels。 Can we -- what if it's just replaced reels by any set that has an order to it？

 Does that work？ Do we need a -- a measure？ Why -- where does a measure come in？

 That's a measure not on X but on Y。 Misclostification rate is a measure -- is about Y。 So what -- do we need any structure on the feature space？ Yeah？ [ Inaudible ]， Yes。 We need an ordering to the elements of the set。 So when we pick a particular element of the set。 we can split on that element and say， are you less than or equal to it or greater than it？

 So we need -- each feature has to be in -- so let's say the if feature has to be in a set。 S of I or S of I has a nice little relationship less than or equal to。 Is there anything we would need for this S I， this space for the if feature to have besides。 an inequality？ But I don't think we use a distance。 Do we use a distance anywhere？ So no。

 That's what's so neat about trees。 That this is all you need。 So if you can put an order on it。 you're set。 Even without order， what happens if you have a set S I with no order？

 You can't use some of the tricks we discussed。 You no longer choose a split point that no longer makes sense without an order。 In this case， you have to actually choose the whole partition。 You can do that。 you can say I will choose a subset of S I to be left and the rest will。 be right and they're not really related by a relation but you can still build a tree， in that way。

 That is how you handle categorical variables as opposed to real variables。 The algorithms for that are -- they are efficient when there's only two values to the categorical。 variable and it gets more complicated when you have lots of values for the categorical。 Okay。 Yes？

 >> [inaudible]， >> I would -- just on validation。 I don't have an intuition on when one is more useful than the other。 Which is fine。 It's fine to not know what's better。 You just use the computer time to try both。 Let the computer do your work。 I mean it's nice to have intuition but you don't need it to move on。 Yeah。 Okay。 So no geometry， no inner products， no distances。 It's called a non-metric method。

 Metric is distance between two things。 Here's the very important thing。 Feature scale is completely irrelevant。 There's no measure of the size of a feature。 So in particular， things like centering and scaling your variables or normalizing or whitening。 completely irrelevant for features as long as you're doing it with one feature at a time。

 Complete irrelevant for trees because it doesn't care。 It only cares about the ordering。 And this is important when trees become -- you won't necessarily use trees -- you only use。 trees from time to time but you'll especially use them for things like random forest and。 boosting as constituent elements。 And all these properties of trees carry on to ensembles of trees。

 So if you're doing random forest， which we'll talk about next week， you don't have to be。 scale your variables or center them or anything like that。 And here's the last thing which is -- this is relevant to the regression trees。 The predictions are -- they're not smooth。 They are piecewise constant。

 So this may or may not be desirable in your context。 That's all I had to say about trees。 So rest of the time is yours to see how to best prepare you for the test tomorrow。 >> May I ask a last question about trees？ >> Yeah， please。 >> We want to talk about the binary trees。 >> Wait， not yours to like chat but like --。





![](img/87d31aa83b168b3b70a725b27b58fb7a_4.png)

 >> [ Laughs ]， >> All right， go on。 >> In a split we'll go left or right。 >> [ Inaudible ]， >> Yes。 okay， multi-way trees。 Yeah， I -- those exist。 I don't see them being used too often but that's -- but I don't work in a world where。 trees are often used。 Okay， so for my personal needs and the textbooks that we're looking at， right。 we look -- I've， been looking at a lot of textbooks to bring things together。

 It's pretty much about binary trees。 So， yeah。 What else？ Okay。 Let me say one thing that's on my mind about the test tomorrow just so it's for you to keep。 in mind。 The test might be long for some of you。 And the problems are， you know。 some may be easy and some may be hard and they might， be interspersed。

 So you have to be flexible and if you get to a problem and you're kind of stuck， you need。 to move on and get through it and go back through it。 So don't -- maybe you'll find them all straight forward but， you know， don't feel like you。 need to go -- you can skip and that might be the best strategy， you know， depending on， you know。

 maybe some areas of the course are stronger than the others。 So do those first。 Okay。 All right。 So some of you guys posted some questions。

![](img/87d31aa83b168b3b70a725b27b58fb7a_6.png)

 All right。 All right。 So the first -- this is a test question from last year。 The question was very confusing。 I don't actually think I ended up counting it last year on the true/false。 But anyway， let's talk about it。 So true or false？ If the empirical risk function is not convex。 more training data may not help estimation， error。 It's confusing。 Let's break it up into pieces。

 So the second piece。 Training data estimation error。 What's estimation error， first of all？ Yeah。 You're all -- everyone think about it？ Okay。 This is our space of all possible functions。 F star is the Bayes' optimal。 This is our hypothesis space that we're going to choose a function from。 This point is the point that minimizes what kind of error？ Approximation error。 Right。

 So the point that's closest to the Bayes' optimal in the hypothesis space is minimizing。 the approximation error。 Does this point depend on the training set？ Right。 Doesn't depend on the training set。 It just depends on the hypothesis space that we're in。 So we can write that like F star sub H to say it's restricted to H。 All right。 Now at this point。

 what do I have in mind for this point？ It's the point in H that minimizes what kind of error with respect to F star of H。 Estimation error。 So the idea is that we want to -- we restrict to H。 Why do we restrict to H？

 Why do we introduce the hypothesis space in the first place？ What were we concerned about？

 Overfitting。 Yeah。 So if we just should try to find the best F among all functions for our training data。 we are prone to overfitting。 So we restrict to hypothesis space。 Now we'd love to find the best function in the hypothesis space， but we don't have enough。 data to really find the best。 So we find the best according to our data。

 It's minimizing the empirical risk。 And the gap between this point we find。 which is going to be F hat and F star H， the difference， in the risk for those two things。 that's the estimation error。 Okay。 And what's this thing I drew？ Why do I draw one more thing？

 Optimization error。 Exactly right。 So you have some algorithms to try to find F hat and maybe it's an approximate algorithm。 or maybe you don't run it all the way to conversions or for whatever reason it doesn't get to。 F hat。 Even though you have the data to find a F hat， you just didn't have the computing patience。 or whatever to find it。 Okay， so that's a little additional error。 Optimization error。 Okay。 Now。

 more training data and estimation error。 What's the relationship？

 More training data should reduce estimation error because you're getting closer to the。 your empirical risk estimate of the true risk is converging to the true risk。 Hopefully。 Okay。 All right。 So more training data should help estimation error。 Now how does convexity come in？

 In what of the three types of errors？ Optimization error， estimation error， approximation error。 which would convexity be most relevant， to？ Let's say optimization error because convexity is what gives you effective iterative algorithms。 to minimize the empirical risk or whatever your objective function is。 So convexity is relevant to this optimization error and is maybe accepting some very abstruse。

 ways not relevant to the estimation error。 Okay。 So I think I meant this question to be easy in the sense that the second half of the question。 the second half of the statement is about estimation error and the first half is convexity。 which I'm not going to do with it。 So there should be false， but it's rather confusing。 So anyway。 All right。 Any questions on that？ All right。 Someone else has the great question。 It's kind of an。

 and if the person's here， maybe they can clarify it if this isn't getting， to it。 So we talked about sub gradient descent methods， right？

 And there was this interesting thing we said about sub gradient， which is that it's not。 a descent method， right？ So the sub gradient， you pick a sub gradient and you look in the negative sub gradient direction。 and if you go in that direction， F may not decrease。 So we had an example on the slides of that happening， a picture。 Well， okay。

 But we proved this amazing thing， which is that even if F doesn't decrease， the distance。 between where we started and where we ended up， the distance between the point where we。 started and the true minimizer or W star gets smaller when we move to the next point。 All right。 So that was very interesting。 So the question was， how is it possible？

 How can we continually be moving closer and closer to the optimal W star， but F not decrease？

 And it's not that F never decreases when you take a step。 It's that we're not guaranteed that it will decrease in any particular step。 Is there any more to that question？ Yes？ You mean how？ It is。 Well。 that's what's interesting is that it's not the case。

 So it's possible to be moving closer to the minimum， but actually moving， having F be increasing。 It's not a local minimum。 So no， this is true for a convex。 This is。 we're talking about convex functions here。 So there's no local minima at all。 [INAUDIBLE]。 The distance between me and W star before the step and after the step， after the step。

 I'm closer to W star。 That we prove。 That's for sure。 But F of W0 and F of W1。 that may be an increase。 Yes， it may be an increase。 But if we're eventually going to get to W star。 F has to decrease eventually because， F of W star is smaller than F of W where we started。 So we might do a little bit of uphill before we go downhill。 I can load the picture。

 We had a picture of it。 Yeah？ No， because we were thinking of yesterday and we couldn't imagine how it was possible。 to find the sub-rein of Wassen-Trey or whatever。 You don't like the picture？

 The crazy was a little weird to you。 I think that you said that it must。 the function must increase if we go in the opposite direction。

![](img/87d31aa83b168b3b70a725b27b58fb7a_8.png)

 The question was if we go in the opposite direction--， But the other question was the way that--。 My statement was that--， It was just even one word that made it seem like it always happened。 I said it a louder。 It's in the slides。 OK。 Well， let's get to the bottom of that。 [INAUDIBLE]。 All right。



![](img/87d31aa83b168b3b70a725b27b58fb7a_10.png)

 What do I say to this？ Sub-gradients not at the center--， OK。 Not guaranteed to be the center direction。 [INAUDIBLE]， Yeah， but it increases the function。 But can you imagine something in the cross？ It's not easy to see that the gene is a sub-grade at that point。 What？ Why are you--， Why are you using the set of function？ Makes the function increase always。

 Or it makes--， It sounds like that anyway。 No， this is for this specific gene。 In this specific example。 Or that specific function at that specific point。 Moving in the negative G direction increases the function。 So that we can see from the--， Picture。 So negative G is moving this way， which is--， So this is the minimum of the function。

 And it increases as we cross these lines。 This is-- every line we cross that's gone up a step。 So this is moving from this contour line away from it。 which is in a direction where it's getting bigger。 Now you're just asking， how do I。 notice that the sub-gradient？ So--， Sure。 [SIDE CONVERSATION]， OK。 Suppose we are here。 All right。

 So what's the direction from this point of moving where， things increase the most quickly？

 Would it be this way？ This way？ No。 The direction that we would increase most quickly is this way。 I mean， I have to draw an extra line to be sure。 But do you agree with that？

 But we call it third dimensional， right？ The input space is two dimensional。 And then there's the value of the function。 So this is an input space of R2。 So the third dimension is represented， by the contour lines in some sense。 So should I continue to explain the sub-gradient thing？ So at this point。

 this is the gradient for this function。 And then when we get to this corner。 all these points are sub-gradients because--， Because they are bounded by the--。 So the sub-differential is going， to be this kind of convex combination of the--。 all convex combination-- the convex， hull of the gradients of these parts。

 So there's this gradient for this part， and this gradient for this part。 And the sub-differential is going， to be the convex hull of those gradients。 Anyway。 This is a bit off our track。 Like-- this is getting pretty analytical。 But I think you should understand the picture。 So my understanding of your question at this point。

 is I don't understand sub-gradient geometrically。 Yeah？ [INAUDIBLE]， Yes。 Any sub-gradient-- any g that's a sub-gradient--， if you go in the negative g direction。 you're fine。 Sorry？ [INAUDIBLE]， If you go in the direction of the gradient。 that's-- if you have a gradient， and you go in the direction of the gradient。

 that's the maximal increase in the function value。 The negative gradient is the maximum decrease。 OK， so now what we're asking？ [INAUDIBLE]， That's right。 g is not a gradient。 So we don't have that nice property that minus g， decreases the function。 [INAUDIBLE]， No。 moving in the minus g gets you closer to the minimum， but it does not decrease the function。 Yes？

 [INAUDIBLE]， [INAUDIBLE]， [INAUDIBLE]， All right， well， first of all， did you。 believe that this was the only gradient here？ I couldn't draw this， right？ OK。 So the question is-- so what exactly is the question？ Why can't I draw this here？

 But this is not a-- I mean， if I just do epsilon to the left， this is not a gradient。 Only if I go epsilon to the left of here， only this is the gradient。 [INAUDIBLE]， OK。 start it again。 So--， [INAUDIBLE]， Where it does-- at the point of the corner。 it has an incident number of sub-creatients in the correct。

 Why is there a limit to the direction they think of [INAUDIBLE]， So--， OK。 so I can get at that several ways。 First of all， if you believe our proof， which we went through--。 it was once live， which was nice--， if you move in a negative gradient direction。 we're getting closer to the minimum。 So from that perspective， the only things。

 that get us closer to the minimum are from here things， that go in this direction。 So for those to the negative gradient directions， that's the opposite of these。 So from a perspective of we know the negative sub-gradient， must move us closer to the minimum。 that's a bound already。 We can't-- if the sub-gradient were this way。

 that would have us moving this way， which is away from it。 which is proved-- we cannot do that by our theorem。 So that's one explanation。 kind of a backwards explanation。 [INAUDIBLE]， Not really？ [INAUDIBLE]， [INAUDIBLE]。 So if I go this way？ [INAUDIBLE]， [INAUDIBLE]， [INAUDIBLE]， OK。 [INAUDIBLE]， Yeah。 [INAUDIBLE]。

 [INAUDIBLE]， Yeah， I did draw the same picture here。 [INAUDIBLE]， So there's this more flat， right？

 [INAUDIBLE]， So this is the gradient here。 Well， it's not easy to tell you。 [INAUDIBLE]， All right。 Let's not get too wrapped up in the sub-gradient anymore。 We can-- I just want to make sure there's not other questions， that are more addressable。 I mean。 you have the facts， right？ You know the definition of sub-gradient？

 You know the theorem about sub-gradients that， moves you closer to the minimizer。 So these are your basic tools。 So--， [INAUDIBLE]， [INAUDIBLE]， OK。 Let me get back to you with a better explanation， than I'm giving you now。 Good question。 Yes？

 [INAUDIBLE]， [INAUDIBLE]， [INAUDIBLE]， Yeah， yeah， yeah。 It's a great question。 [INAUDIBLE]， Yeah。 yeah， yeah， right， right。 So the question is-- and we'll take a break right after this。 The question is， perception is a definitive algorithm， right？

 We go in-- and then the problem on homework three。 was show that this is a sub-gradient descent algorithm。 But when you take a sub-gradient。 you have some choice on which， sub-gradient you choose。 And in particular。 or things are not differentiable， there's some question mark。 And so for this problem， you have。

 to choose the right sub-gradient to get it， to match exactly with perception。 Now， for pegasos。 which is the SVM one， I don't remember。 Did we give you a different choice of the sub-gradient for that？

 Because it doesn't matter。 [INAUDIBLE]， OK。 So for the case of SVM， of pegasos， this is--。 pegasos is kind of like the right way， to do stochastic sub-gradient descent on an objective function。 And what's key there is that our step size is decreasing， over time。 according to a particular formula for which we， have theorems。

 And as long as we're choosing a sub-gradient at every point， it will do-- well， it will do fine。 So for pegasos， we could have chosen any sub-gradient instead， of the one we chose。 And it's all fine。 Perceptron， now。 Perceptron is a recipe， originally。 for how to adjust things at every step。 And it just-- you could say it just so happens。

 to be the sub-gradient--， a particular sub-gradient of the perceptron loss。 Well。 what happens if we took the step to be zero， whenever the sub-gradient were at a non-differentiable point？

 First of all， at what point is the perceptron not， differentiable？ Zero。 What is zero？ The what？

 [INAUDIBLE]， [INAUDIBLE]， OK。 So if our prediction for a perceptron is W transpose x。 the margin is going to be YW transpose x。 And then we have the loss function。 which is not differentiable。 So we have a loss-- a margin loss。 What's the margin loss for the perceptron？ OK。 Max of？ [INAUDIBLE]， What's the margin？ How's that？

 Does it agree with what you're saying？ OK。 Great。 So when is this not differentiable？

 At m equals zero， or this equals equal to zero。 OK。 Good。 All right。 So what happens if we choose the sub-gradient-- so zero。 is a valid sub-gradient of the perceptron at m equals zero， of the perceptron loss。 So that means when we get to a point where m is equal to zero， and we take a sub-gradient。

 and we choose zero， what's our step？ No step。 OK。 So what happens if we choose zero as our sub-gradient。 at that point？ We won't be updating w in that iteration。 An iteration corresponds to a specific point。 And what's going on with that point？

 That point is working class where they're from。 That point has margin zero。 It's not being classified at all。 Yeah。 So the prediction on that point is zero。 And the margin is zero。 So what's that mean corresponding to the predicted hyperplane， or something？

 It's on the hyperplane。 So we did terribly on that point。 We're completely indecisive。 We don't even have anything we're producing。 So it sure seems like a better idea to take a step at that。 point than to stay where we are。 OK。 So Pegasus doesn't have this issue because it's using an SVM。 loss， which is not satisfied with being on a margin。 There's a loss if your margin is zero。

 There's a loss if your margin is a half。 It's penalizing you until your points have margin one or more。 So that's why we're OK。 That's why we're OK taking any subgradient in the Pegasus， place。 Because if you get stuck on the margin for SVM， what's the margin for SVM？ On the margin is one。 The nondifferentiability in SVM is one。 Well， who cares if you're stuck at one？ That's fine。

 And then as far as your question from Piazza， are we ever going to find points on the margin？ Yes。 we will find points on the margin。 Because when something gets to the margin。 we're not going to so we're going to update it。 If we're using a subgradient zero， then we're not。 going to update it at that point。 Does that mean the data types are not linear。

 separable if they are on the hand-by-hand？ The question is if there are points on the hyperplane。 does that mean the data are not linearly separable？ Well， there's two questions。 If I just give you a hyperplane， I just give you a hyperplane。 and then points on the hyperplane-- no， it doesn't say anything about the data。

 If I say this is the best possible hyperplane， you could come up with in a certain sense。 and there's still points on the hyperplane， I would say that-- well， it depends。 what I meant by best possible。 So it's a good question why you think about it。 If I minimize the SVM loss and there's points on the hyperplane， then the data is not separable。

 That's true。 That's what I'll say about that。

![](img/87d31aa83b168b3b70a725b27b58fb7a_12.png)

 Let's take a break。 All right， so there's an interesting problem。

![](img/87d31aa83b168b3b70a725b27b58fb7a_14.png)



![](img/87d31aa83b168b3b70a725b27b58fb7a_15.png)

 question over break。 Who asked me a question？ What was the question again？

 The first question on the recap， is it possible， to under-- is it possible to add a future？ OK。 right。 So you have an input space， a set of features， and you're doing with a linear regression。 or unregularized linear regression， on a particular set of features。 And you add a feature。 And the question is， can the empirical risk， and the training loss get worse？ OK。

 Or it will never get worse。 And the scary part is never。 Is there any exception to this never getting worse， when you add a feature？

 But it's not too scary because you， have to picture hypothesis spaces。 So you have the input space x。 And then we have some features that give us， a hypothesis space H1。 A hypothesis space is a subset of all functions， right？

 So it's a particular subset of all functions that we get。 Consider them as like functions of x。 So if we add a new feature， the space of possible functions， we can do on x cannot get smaller。 Adding a new feature can ever restrict， the amount of functions that we have access to。 Is that clear？ So if we add a new feature， it might be the same size， but in general。

 it could be bigger。 And then we're minimizing-- we're。 finding the best fitting function in these two spaces。 So if the space gets bigger。 or at least doesn't get smaller， then the best can't possibly get worse。 So it's never， never worse。 Adding a feature can make the hypothesis space larger。 Adding a feature can and hopefully does。

 make the hypothesis space larger。 Knealed it。 Is the same case if you're using row realization or not？

 Ah， regularization or not？ No way。 Regularization changes the story， and then it's hard to predict。 So if you have the same amount of data， and you add a feature， and use the same regularization。 does it fit？ And then the question is， what are we looking at？

 Because this was talking about training loss， right？ So if you add regularization， are we。 looking at training loss？ Are we talking about total regularized loss？ It's less well defined。 All right。 What else？ [INAUDIBLE]， Any new picture about the new ones that。 cannot deliver to the community have， but you still have the same amount of community。

 that probably means to make that decision， and that will be equal to--， OK， good question。 So same setup。 We have a fixed amount of training data。 We add a feature。 Then the question is。 does the estimation error increase？ OK， thoughts on that？ So only the direction seems right。 Because when you add a feature， you're potentially， growing your hypothesis space。

 If you have a fixed amount of data， then it feels like you're potentially increasing。 your estimation error。 Yeah， it's all directional at these small scale。 But yeah。 that's the right intuition。 That's the right direction。 All right。 Someone was asking about overfitting and underfitting。 [INAUDIBLE]。





![](img/87d31aa83b168b3b70a725b27b58fb7a_17.png)



![](img/87d31aa83b168b3b70a725b27b58fb7a_18.png)

 We know it over-- yeah， I think--， I don't remember the exact question。 Anyone want to ask a question related to that again？ What's underfitting？ Say again？ [INAUDIBLE]。 OK， so underfitting， roughly speaking， is you think--， along lines of small hypothesis space， yeah。 The idea of underfitting is that there's， some complexity to the prediction function。

 the best possible prediction function， that we're trying to get to。 And there's enough data to kind of show that complexity。 But the hypothesis space isn't complex enough。 It isn't big enough to match the complexity shown by the data。 to match the function that is actually occurring。 So maybe we have tons of data， and we。

 see this really complicated regression function。 And all we have are linear functions。 So that would be underfitting。 Yeah。 If we have large error， are we underfitting？

 Large error on training or on test？ On test。 So large error on test could be overfitting。 Large error on test could be underfitting。 It could be either way。 If we have a big error on training set， that feels， well， it could be underfitting。 It could just be noise in the data。 But the direction is right。 Yeah。 Yeah。 [INAUDIBLE]， Yes。

 [INAUDIBLE]， Wait。 So three points， and they lie exactly on the line。 And I didn't say underfitting。 I don't know。 Did I？ OK。 [INAUDIBLE]， About what？ [INAUDIBLE]， Yes。 [INAUDIBLE]。 I think that I take like a sample bias， because the sample I have don't behave like a population。 So is it like a combination of the--， So if you have a small sample， then--。

 the sample-- small sample is getting towards estimation error。 The fact that your sample may not。 be a nice representative of the full distribution， that's about estimation error。 Yeah。 Yeah。 [INAUDIBLE]， Again， please？ [INAUDIBLE]， If you have small sample size。 that feels like you might be， moving towards overfitting the data。 Yeah。 Yeah。 [INAUDIBLE]。

 The question is， how do you choose--， we've been calling them regularization parameters。 That's what you mean， right？ Yes。 Yeah。 Second。 The regularization parameters do。 introduce the regularization parameter。 Yes。 So I think the question is， how do we。 choose the regularization parameter for things， like ridge regression and lasso regression？ No。

 it's about ridge regression。 [INAUDIBLE]， I don't know if I've used the term shrinkage factor。 so you have to introduce it to the class。 [INAUDIBLE]， Oh， OK。 [INAUDIBLE]， OK。 [INAUDIBLE]。 Ranges from 0 to 1。 Yes。 OK。 [INAUDIBLE]， OK。 [INAUDIBLE]， OK， go on。 So what's the question？

 [INAUDIBLE]， Yeah。 [INAUDIBLE]， OK， all right。 So there's two questions in there。 One is。 let's take care of shrinkage factor。 First， a shrinkage factor is just another way to describe regularization parameter。 rather， than talking about lambda， which who knows what the units are。 They take the ratio of-- if you have a picolamda， you get your w4 lambda， so called w sub lambda。

 That's your best for lambda。 And you can look at the norm of lambda。 And you can look at the ratio between the norm of lambda and theta。 And you look at the ratio between the norm of lambda and the norm of the unregularized， solution。 All right， here's the question for you guys to see if you're following regularization。

 I compute my solution to a regularized optimization problem， called L2， called L1。 Doesn't matter。 And I compute the norm of my solution。 This is linear regression， right？ So I get a w， a vector。 I compute the norm of w， either the L1 norm， if I'm doing L1， regularization， or L2， if I'm。 doing L2。 And I compare that norm to the norm of the solution I would get without regularization。

 How do they compare？ [INAUDIBLE]， Sure。 Regularization leads to solutions with smaller norm。 That's exactly what regularization is doing。 It's kind of penalizing a big norm of the solution。 Or there's an equivalent formulation， if you did the homework 7 practice problem， where it's。 exactly the equivalent in fact to literally constrain the norm to not be bigger than a。

 certain level。 Anyway。 Okay。 Now， so shrinkage factor is just another way to talk about regularization parameter。 And then how do you choose which one？ Same story， always。 Cross-validation， validation set。 This is how we choose the regularization parameter。 Good question。 Yeah。 [INAUDIBLE]。 So you want to see an example work down besides the SVM that we did in class？ Yeah。 Where is that？

 Which？ Well。 Sure。 Let's do a little bit。 Let's do a little bit of something。 [INAUDIBLE]。 What's the other method？ Okay。 All right。 It's a big story。 The look， crunchy。 No。 I mean it's -- so let's start off something and see where we get to。 Okay。 So what's the problem？

 [INAUDIBLE]， Oh。 What if we did the chicken off Ivanoff problem？ All right。 Good。 [LAUGHTER]， Okay。 So I'll start off with Ivanoff problem。 So let's skip my notation here。 All right。 So we have our loss functional of 5F。 And we want to minimize 5F subject to omega of F less than or equal to R。 But let's parametrize by W。 Let's consider hypothesis space instead of x mapping to W transpose x。

 All right。 So f of W。 All right。 So rongian is equal to phi of W plus lambda。 And then in our formulation， our constraints are always less than or equal to zero。 Right？

 So lambda times omega of W minus R。 Good？ All right。 So that's our Lagrangian。 Now。 there's this cool thing that we proved。 And I hope you guys can be convinced of this。 is that the solution to the original optimization， problem can be written like this。 Minimum over W。 So that's a premium over lambda greater than or equal to zero of the Lagrangian。

 But I will write it-- is there a mistake？ But I'll write it like this。 OK。 Now let's work this through。 So I'm a solution if I did-- the solution of this is the same as a solution to this。 So there's two cases。 What are the two cases that we need to consider to see this connection？

 There's the-- so let's break up the world of W into two possibilities。 There's W that satisfies the constraint and W that doesn't satisfy the constraint。 Right？

 So suppose W does not satisfy the constraint。 So what's not satisfying the constraint mean？

 Omega of W is-- yeah， greater than R。 OK。 In that case， what's going on over here？

 This is the key piece here。 What's lambda like？ Lambda is greater than or equal to zero， right？

 Lambda is greater than or equal to zero。 Now in the case of a constraint violation。 this thing is what？



![](img/87d31aa83b168b3b70a725b27b58fb7a_20.png)

 That's positive。 That's right。

![](img/87d31aa83b168b3b70a725b27b58fb7a_22.png)

 OK。 Great。 It's strictly greater than zero。 OK。 Now look here。 We're taking the supremum of R lambda greater than or equal to zero。 This thing is greater than zero。 So this can go up to infinity。 All right。 So this implies this guy。 which is the Lagrangian， L of W lambda is equal to infinity。

 How about if it's less than or equal to R？ So if this is now negative， what's going on then？ Yeah。 So if lambda is bigger than zero， this thing is smaller than zero， which makes this thing smaller。 So if we're taking the supremum， we want this to be as big as possible， which means zero。 So the supremum of this expression is attained when lambda is zero。 If this is less than zero。

 which means the constraint is not violated。 All right。 So if the constraint is not violated。 then we get Lagrangian of W lambda， lambda star， lambda star is equal to phi of W。 All right。 So this justifies this statement that the minimum of the sum， the min of the max of the Lagrangian。 is equivalent to the original problem。 All right。 You guys got this now？ If you want it。

 It makes it in the notes， of course。 All right。 So what's the dual problem。 the dual optimization problem？ Switch the min of the max。 That's right。 It's that easy。 So I'm going to write， I'll just write max instead of soup。 So lambda。 greater than or equal to zero， min of W of the same thing。 Phi of W plus lambda。 Good。 OK。 Now。

 what's the dual function？ The dual function。 This is the dual optimization problem。 This is the dual problem。 What the solution， we often write this as D star。 So D for dual。 The value of the dual problem is D star。 We often write P star for the value of the original problem called the primal。 All right。 So this is the dual optimization problem with the dual function。 Where is lambda？

 Did I drop lambda？ The previous lambda that's generated。 Did I？ Sorry。 What do you mean where it's lambda？ It's here。 It's here。 I don't understand。 Sorry。 Lamb of star。 Yeah。 I didn't say anything about lambda。 Oh， I did write it for a second。 Yeah。 It's。 So it was just。 I just wrote it because when for the value we're talking to the supreme。 We're like。

 oh， at this， when we take the supreme， this thing is going to be zero or this will be infinity。 So I wrote lambda star for that。 And without lambda， you will get to the certain P star。 For a particular lambda star， you'll。 Yeah。 If you plug in a lambda here and then you minimize over w。 you'll get a certain value， not P star。 Unless it's lambda star， then you get P star。 Okay。

 What is lambda star？ I didn't really define it yet。 Sorry。 I didn't quite get there yet。 Sorry。 So what's the dual function？ Yeah。 Okay。 So it's the dual function is this piece。 This piece of function of what's not fixed in the part I've written？ Right。 Lambda。 That's right。 W is done because we minimized over it。 So we call this thing G of lambda。

 And that's the dual function。 Okay。 So what do we want to be able to say about the relationship between the solution to the prime。 one， the solution to the dual？ Okay。 So first， I'm going to simplify the expression of the dual problem。 D star is simply the max over lambda greater than equal to zero of G of lambda。 Okay。 You ask what is lambda star？ Lambda star is the lambda at which this maximum is attained。

 So lambda star is equal to arg max of the dual function。 One thing I want you guys to note。 every single time we're optimizing over the Lagrange multiplier， there's a constraint。 Do you see the constraint？ Greater than equal to zero。 That's important。 So whenever we optimize over W in all the problems we've dealt with so far， that's unconstrained。

 In the Lagrangian， it's unconstrained。 And the dual variable with the Lagrange multiplier for any quality constraint where optimizing。 is greater than equal to zero。 And Y， you already know Y， we've proved， we justified the Y。 In this whole argument， where we showed that this inner。 that this primal formulation is exactly equivalent。 So that。

 that you can convince yourself that this is equivalent tells you why you want super。 lambda greater than equal to zero。 Okay。 All right。 Where were we？ So we have the dual problem。 And then there is， so what do we want for the dual and the primal relation？ Yeah。 we kind of want them to be equal and what's always true？ Yes。 It's called weak duality。

 We always have D star is less than or equal to P star。 That seems like weird and abstract。 but we proved that very nicely in two lines。 If you go back to your slide， that min max inequality。 there's a piapto question on it where， we really hacked it apart and should be clear now。 All right。 but what we， in our course， what we're primarily interested in is that we want。

 D star to be equal to P star so that we can just solve the dual instead of the primal。 And then what do we， what's that call that has a name when that's the case？ Yeah， strong duality。 All right， and then can we state some conditions when strong duality holds？ Okay。 the problem must be feasible。 All right， so we started the primal problem。 We started the problem。

 See， yes？ Okay， so it's feasible。 Yeah， that's a good start。 We can do。 we have a particular condition called Slater's condition， remember？ So it's pretty general。 but what's the version of it that applied to support vector machines， or something？ So first of all。 we need a convex optimization problem。 So that's important。

 We don't need convexity for strong duality， but we need convexity for this particular theorem。 So Slater's， we have a convex optimization problem。 All right。 here's an important question for you guys。 What is a convex optimization problem？

 What do you have to check to make sure your problem is convex？ We have different pieces。 We have an objective function。 And now you have these constraint functions。 And we need， yeah。 we need phi convex and omega convex。 Okay？ Geometrically， this piece defines your constraint set。 Your constraint set better be convex for this to be convex optimization problem。 So that's good。

 If this is the set of feasible points， if that is the solution to this inequality， that's。 plausible。 If your constraint set looks like this， no way。 This is not a convex set。 The constraint set needs to be convex to have a convex optimization problem。 So your objective function has to be convex， but don't forget to check the constraint set， or this。

 I mean， if you check this， you're fine。 You check omega and you check phi， you're fine。 Geometrically， the feasible set must be convex。 Okay？

 The feasible set is the set of w that satisfy the constraints of the problem。 That's the feasible set。 Okay。 All right。 All right。 So we need a convex optimization problem。 And we need-- so this condition is very simple。 We need to find a strictly feasible point。 What's a strictly feasible point？ A strictly feasible point is a point that's on the interior of the constraint set。

 What does interior mean？ So you could divide a set into its boundary and the interior。 And it needs to be on the interior-- strictly on the interior， not on the boundary。 That's what you need for our Slater's condition。 All right。 It was a little easier for SVM because if all of our constraints are affine constraints。

 you only need feasibility。 You don't even need strict feasibility。 So even showing that there's a point on the boundary was sufficient。 So that was-- when someone said feasibility， that was in the case of affine constraints。 That's right。 Yeah？ Yep。 Strictly-- okay。 So I will give you two explanations。

 The first is algebraic。 So this is a constraint for the optimization problem。 Right？

 W is feasible if it satisfies this constraint。 It's strictly feasible if it satisfies the constraint with a less than and not any quality。 Okay？ Geometrically， it means that if this is the set of sub of W's that obey this constraint。 geometrically， the boundary， the outer most part of it is the part where phi of W is equal。 to zero and the inner part is where it's strictly a less。 So strictly feasible is here。

 Feasible is on the boundary。 Sure。 Yes？ The objective function must be defined。 Okay。 Yes。 So you're-- our objective functions are always defined everywhere。 So this is-- but you're right。 Yes。 The domain of the objective function must-- the whole problem is considered。 We look at the domains of all of the functions。 So the constraint function and the objective function and we look at the intersection and that's like--。

 that's the area we focus on。 But this is a little bit esoteric for our purposes。 Okay。 X。 there's no x。 Oh， we're way-- we're abstract here。 We're talking about W are primary primal variables。 Like， where do x's fit in here？ Like in an SVM？

 Oh， I might have had a typo。 Are you talking about the preparation notes？ You want to show me？

 That's different。 It's a W here。 It should be--， No。 It should be a--， Well。 here I changed my variable to W instead of x。 So we have only a box that's the function。 Yeah， yeah。 This is a parameter vector。 But that x in there is also-- serves the same function。 Okay。 All right。 More questions on this or shall we see what the next step is for duality？ All right。

 If we justify our strong duality， then we know that d star is equal to p star。 That's nice。 All right。 Do you guys remember complementary slackness？ What's complementary slackness？

 Someone should remember， maybe。 So there's this pairing between Lagrange multipliers and the constraints。 So here's our constraint function of making W minus R in lambda。 Comprometry slackness is that at the optimum， the product of these two is zero。 Here。 It might be enough duality。 Do you guys have some questions on any other topics？

 The complementary slackness is actually under the top。 You are particularly interested in complementary slackness。 All right。 Let's hit it。 So let's assume that our optimal is our taint。 All right。 So what do I mean？ So let's say W star--。 So， phi is our objective。 So phi of W star is equal to the minimum over W such that omega of W is less than or equal to R。

 So minimum over the constraint set。 Good？ Of phi of W。 So what I've written here is basically。 I found a particular W star that actually attains， that I could have written in the minimum。

![](img/87d31aa83b168b3b70a725b27b58fb7a_24.png)

 This is the point。 So when I write in a theorem， I don't know if there exists a particular solution。 But here I'm saying， there is W star attains it。 OK。 Let's do the same for the dual。 So there we're saying G of lambda star is equal to the tummy。 So， it's-- all right。 I'll do it for you。 Super over lambda。 And now I didn't write G yet。 G is that minimum thing。

 So G of lambda。 Yes？ [INAUDIBLE]， Thank you。 Good。 Great。 All right。 So--， [INAUDIBLE]， Say。 how do you--， [INAUDIBLE]， This is G of lambda star。 [INAUDIBLE]， OK。 So we're taking the supremum over all lambda of our dual。 All lambda greater than or equal to zero。 And that gives us a value， like the value of the function G。

 And I'm saying we attain the same value at lambda star。 So lambda star is the thing that maximizes G。 That's what-- we care about both。 So here I wrote it in a way that this shows that lambda star is the value of lambda。 that achieves this maximum。 That's so yeah， we want both。 That's right。 OK。 OK。

 So complementary slackness is trying to show that the product of this and this is equal to zero。 Let's expand this a bit。 Let's just write down actually-- let's do G of lambda star again。 Let's see。 All right。 So let's write down the definition。 Min of w phi of w plus lambda omega w minus r。 All right。 Lambda star。 This is good？ This is good。

 OK。 So what I want to do is bring in w star here。 So the question is-- so the primal is the minimum over w of the super over lambda。 And that's equal to the max over lambda and the min over w。 So the question is in those interoptimization problems， like super lambda greater than equal。 to zero， is that attained at lambda star？ So lambda star is the optimum for the dual function。

 W star is the optimal for the primal function。

![](img/87d31aa83b168b3b70a725b27b58fb7a_26.png)

 And the question is， are those lambda star and w star exactly what we need to solve the。 inner optimization problems of the primal problem and the dual problem？

 This is a question I want to pia to also。

![](img/87d31aa83b168b3b70a725b27b58fb7a_28.png)

 So let's just work this through。 And I think what I just said will be more clear。 So the minimum over all w of this expression is certainly less than or equal to the value。 of this function at a particular w。 That sounds right， right？ Good。 So I'm going to write less than or equal to what w am I going to choose？ W star， yeah。 Okay， good。

 Now， there's one thing I know about w star。 It's that it's a feasible point， right？

 W star must be feasible， which means what？ Or this part of the equation。 This thing must be negative， right？ Feasible means that omega w star is less than or equal to r。 So this thing is negative。 This is less than or equal to zero。 And what do I know about lambda star？

 Lambda star is greater than zero。 Yes， lambda star is greater than equal to zero because lambda。 the constraint for lambda， is， that's the non-negative。 So with this whole expression。 less than or equal to zero。 Positive times negative is less than or equal to zero。 Great。 So this is less than or equal to zero， which means this whole expression must be less than。

 or equal to the first term。 Because we have fe of w star and then we're subtracting something from it。 So this must be less than or equal to fe of w star。 Okay。 And now let's where the magic happens。 Supposedly a strong duality。 That tells us that the p star and the d star are the same。 So that's exactly g of lambda star is the value of the d star。 Right。

 So p star is the mass of our lambda of g of lambda。 Lambda star is the optimizer。 So g of lambda star is d star。 All right。 So g of lambda star is on the left。 Down here we have fe of w star。 Fe of w star is p star。 Good。 And they're equal if we have strong duality。 So strong duality， all right， s d。

 strong duality implies these are all equal。 Right。 Because if this is equal to this then everything between is equal because it was a stack of。 inequalities。 So that tells us something very interesting about this piece here。 What does it tell us about this？ It tells us this is equal to zero。 Great。

 So this thing is equal to zero。 That is complementary slackness condition。 When you have this Lagrange multiplier lambda star times this thing which is the left-hand。 side of the inequality。 That that equals zero。 That's complementary slackness。 There's one other very important thing that we can read off from here though which is that。

 we see that now we see that g of lambda star is indeed equal to this piece with w star， plugged in。 What is this piece？ This is the Lagrangian。 So let me write this out。 I'll never get it back。 So can you guys see it on here or no？ Okay。 So g of lambda star is equal to。 you guys recognize this as the Lagrangian？ WL of w star lambda star。 This is important。

 It's not so obvious。 It wasn't so obvious to me。 It wasn't so obvious to some people in Piazza。 You have to really commit yourself with some inequalities that this is the case。 What else？

 We have the -- all right。 Yes？ Strong duality。 When can we say we have strong duality？ Someone。 We have a convect optimization problem that is strictly feasible。

![](img/87d31aa83b168b3b70a725b27b58fb7a_30.png)

 Strictly feasible means there's a point that satisfies all the constraints with strict inequality。 Slater's condition。 If there's a question like this on an exam。 you could say Slater's condition says because， we have a feasible point and the problem is convex。 If the problem is convex， you could say that。 Yeah？

 If there's something -- I'm wondering what like slouch is there in one time？ Okay。 so we're over time， so I want to let our videographer piece out。 So you're going to cut it whenever you want。 And you guys can go whenever you want。 And I'll go soon too。 Yeah？ (laughter)， (laughter)。

