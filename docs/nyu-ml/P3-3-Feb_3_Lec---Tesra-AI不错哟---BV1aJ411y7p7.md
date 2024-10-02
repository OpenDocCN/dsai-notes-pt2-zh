# P3：3.Feb_3_Lec - Tesra-AI不错哟 - BV1aJ411y7p7

 So just a few logistical comments。

![](img/4e43eb5d01ffd7bcdfbbc08b055bcf2a_1.png)

![](img/4e43eb5d01ffd7bcdfbbc08b055bcf2a_2.png)

 Have you guys all who have registered for the class gotten onto Piazza？ Yeah。

 it's pretty active conversation already。 I think we've had like 50 posts。 So a lot going on。

 My only request is that why don't you students help answer questions and read the questions。

 before you ask other questions。 In case there is a repetition。 So that's my only request。

 Participate by helping others。

![](img/4e43eb5d01ffd7bcdfbbc08b055bcf2a_4.png)

 Will make life easier for the instructors。 So but lots of nice and interesting questions that I think you could benefit from reading。



![](img/4e43eb5d01ffd7bcdfbbc08b055bcf2a_6.png)

 actually。 All right。 Give you one second。

![](img/4e43eb5d01ffd7bcdfbbc08b055bcf2a_8.png)

 Okay。 So today we're going to go a little bit deeper on the kind of abstract side of things。

 This notion of the risk risk minimization hypothesis spaces。

 And then we're going to move into some algorithms L1 and L2 regularization。

 So the range regression problem which you guys have already seen in your homework。

 Lasso which may be new for some of you。 And we'll see how those fit into hypothesis spaces and regularization。

 And then we'll talk about some ways to optimize those the objective functions you get。

 And that'll be about it for today。 Tomorrow will be a bit of a continuation where we'll be thinking even more carefully about。

 some of the interesting properties of Lasso and Ridge that are actually important in practice。

 And we may begin some discussion of classification losses tomorrow。

 And the next week just giving you a heads up。 Next week may be our hardest lecture mathematically or most intense。

 It's a lot of material。 And I just wanted to let you guys know in case you had some extra time to prepare。

 I posted some notes and some slides that we had last year。 A look in them over in advance can help。

 Okay。 All right， so let's get started。 Today's topic in the first half。 Excess risk decomposition。

 All right。 So let's do a little review。 Is this okay？ Of statistical learning theory from last time。

 So remember we had our input space or output space or action space where the decision functions。

 which take an input and produce an action。 We have loss functions that once you produce your action and you see what the output actually。

 is， it gives you a score， a loss。 Small is good。 Big is bad。

 And then we had our gold standard of how we evaluate a particular decision function called。

 the risk or the expected loss where this is based on the assumption that our input and。

 output pairs come from a data generating distribution。

 And that's what the expectation is taken with respect to。

 And then finally when we have this risk we can ask well what function minimizes that， risk。

 minimizes the expected loss。 Now it's called the base optimal， the base decision function。

 And the risk that that function attains is called the base risk。

 And then of course what we pointed out is we don't know the generating distribution except。

 in kind of contrived situations that we make up。 And so what can we do instead and of course what we do is we assume we have a sample of。

 data from that data generating distribution called D， D sub M。 And then we introduce the。

 empirical risk which rather than an expected value is an empirical average， a sample average。

 with respect to a data set drawn from the distribution。

 So we have this average loss over the data set as the empirical risk。

 And we saw that little demonstration last time that shows if you try to minimize the。

 empirical risk overall functions this can lead to overfitting likely will lead to overfitting。

 So what was the answer we gave last time？ We suggested let's constrain our optimization to a hypothesis space。

 a subset of the space， of all functions rather than all functions and optimize over the hypothesis space instead。

 And we're saying how do you make the hypothesis space where you put those functions into the。

 hypothesis space that you want to end up with that have the properties that seem reasonable。

 to you from the beginning。 So those were linear functions， polynomial functions， decision trees。

 all of these were， possible hypothesis spaces that are subsets of all possible decision functions。

 Alright。 So once we restrict to hypothesis space called F， we again now we get the empirical risk。

 minimizer constraint and the risk minimizer constraint both constraint to that hypothesis， space F。

 So remember F hat N， anytime there's a hat that means something is derived from data。

 And this is a typo。 There should be no hat here。 The risk minimizer has nothing to do with data。

 So this should be just an F sub the hypothesis space。 So it'll be cleaned up on the next slide。

 Alright。 So here's an important concept coming up。 I'm going to draw it on the board。

 I'm going to roughly repeat what's on the slide。 So if you can't see what I'll draw。

 you can refer to this slide。 But I prefer to draw this on the board。 So I'm going to draw a big box。

 That's too big。 And this represents all possible functions mapping from input space to the action space。

 So alright， but F mapping X to A action space。 All possible。 Now suppose we have a loss function。

 we have a data generating distribution， then we can， talk about the Bayes decision function。

 And it's a function， decision function， so it lives somewhere in this space。

 So let's write that here。 Hold on。 F star。 Can you guys see， okay with that angle？

 Well otherwise it's up there。 Alright。 Now I've been choosing the hypothesis space。

 The hypothesis space is a subset of this whole space。 So I'll draw it。 Just a cartoon。

 The idea is to show this is not the whole space， it's a subset of the space。 Alright。

 In this hypothesis space of functions， which we'll call F， there's going to be a best function。

 in the sense of minimizing the risk。 So to show that it's like as close to the optimal as possible。

 I'm going to draw it， here。 Kind of like almost like the projection of this Bayes optimal function onto the hypothesis。

 space F， but that's informal。 And we'll write this F sub hypothesis space F。 Alright。

 Let's write down the risk of the Bayes optimal。 So let's write that as R of F star。 Okay。

 And what can we say about the comparison between the risk of the Bayes optimal and the risk。

 of this constrained optimal function？ Sure。 Great。 So this is less than or equal to this。 Great。

 Alright。 So now what's the next function we need？ Any questions？ Alright。

 What's the next function we need to introduce to this picture？ The empirical risk minimizer， right？

 Let's write that， let's give us a little more room。 Let's write it here。

 So it's still an hypothesis space F。 In general it's different from the best in this class。 Okay。

 This is the empirical risk minimizer。 This is based on minimizing the empirical risk。

 It's based on data。 How about this one？ F sub F。 Based on data？ No， it's based。

 It's an unattainable ideal。 It's the minimum of the risk over this set。

 But we don't really know the risk。 The risk depends on the data generating distribution。

 It has the expectation over the data generating distribution。

 So we can have a really fine-ness but we can discuss its existence in breaking its down， down。 Okay。

 So we introduce this thing， this hypothesis space to control overfitting。

 But there's a penalty for that。 Yeah？ No？ Okay。 There's a penalty for that。

 So the issue is that the best function isn't in the hypothesis space。

 So we lost something by constraining this F。 And this gap in how well we perform according to risk。

 that's called the approximation error。 The approximation error， we can write it out as。

 I'm going to just say， APP for approximation， error。 This is on the slide。 I could run to it。 Okay。

 So the approximation error is the risk of this function minus the risk of this function。 All right。

 What happens as we make our hypothesis space bigger？ What happens to the approximation error？

 It's smaller。 Because if the new hypothesis space is strictly bigger。

 the best in the class can only get， better in terms of the risk。 Great。 Very clear。

 Let's talk about the empirical risk minimizer， this guy。 Maybe not as obvious this time。

 What happens do you think when we make the hypothesis space bigger？ Is empirical risk minimizer？

 Well let me add one thing first。 You expect the risk of the empirical risk minimizer to be better or worse than the best。

 in the class？ Almost obvious， right？ By definition。

 So we can talk about the difference of those two things。

 The risk of the empirical risk minimizer minus the risk of the best in the class。

 This is called estimation error。 So the estimation error。

 what's the source of this estimation error？ The main thing with estimation error is that we don't know the data generating distribution。

 We're approximating the risk with the empirical risk based on the data。

 So this gap between the ERM and the best in the class is purely due to the fact that we。

 don't know the distribution， we only have a sample from it。

 This gap between the best in the class and the overall best， that has nothing to do with， sample。

 The issue there is the constraint of that hypothesis space。 So two different sources of error。

 Now as we make the hypothesis space bigger， yes， approximation error decreases。

 But the estimation error is likely to increase。 Why is that？ The idea， anyone have an idea？ Okay。

 so if we， the idea is that if this， the size of this hypothesis space gets smaller。

 we have the same amount of data。 It's easier to find something close to the best than if it's a very big space。

 Big space corresponds to lots of functions that can overfit。 Overall space is more constrained。

 less likely to overfit。 All right？ So an overfitting is a big gap between the empirical and the best in the class。

 So big estimation error is like overfitting。 If this hypothesis space is too small and every function in the space is too simple for。

 people to predict。 That's underfitting。 We don't have the capacity in our hypothesis space to fit the。

 to find the decision function， that we need。 Okay， one more question。

 So fix the size of that hypothesis space。 We increase the size of our sample。 More data。

 What changes？ Yeah， so as we get more data， the empirical risk minimizer may change because we have a。

 different data set。 The estimation error， we expect to decrease。 Typically。

 we expect estimation error to decrease as you get more data or fix a hypothesis space， size。

 And this approximation error， unchanged。 Okay， good。 All right。 Any questions？

 Pretty straightforward。 Great。 There's a notion called excess risk。

 The excess risk of an decision function is the difference in the risk between that function。

 and the phase risk， the best possible risk。 So if the base of those up star。

 you can say excess risk of F is how much worse than the， best possible did we do？

 I want to drive that towards zero。 So in particular， the excess risk of the ERM。

 What's that look like？ Turns out this can be decomposed very nicely in terms of approximation error and estimation。

 error。 So here's the excess risk of F-head M。 Let's add and subtract a term。

 The risk of the best in the hypothesis space， that got there。 So we've added and subtracted it。

 This is still equal。 And now you see the first pair of terms， the last the estimation error。

 That's the risk of the ERM minus the risk of the best in the class F。 Next pair of terms。

 that's the risk of the best in the class minus the base risk。 That's the approximation error。

 So we've decomposed the excess risk， the total disappointment， the total gap between ERM。

 and the base into an approximation error and an estimation error piece。 And all right。

 so let's drill in a little bit。 Approximation error。 First thing， it's a property of the class F。

 It's our penalty for restricting the hypothesis， space。 Great。 Bigger F。 Small approximation error。

 Clear。 All right， it's approximation error， a random or non-random variable。 Non-random。

 It involves an expectation， yes， but once you-- but the expectation is not random。

 It involves probability theory， but it's not random。 Estimation error。

 It's the performance hit for choosing F based on a finite sample instead of using the full。

 distribution。 Smaller F。 Smaller estimation error， roughly speaking， and less overfitting。

 So it's estimation error random or non-random random。

 It's random because the empirical risk minimizer depends on the data set that you sample。

 It's random。 Yes， great。 All right。 So a bit of a recap。 We get a loss function。

 We choose a hypothesis space that we think will do the trick。 We do empirical risk minimization。

 It's going to require some optimization。 And then the data scientist's job is basically the choice of F to trade off between approximation。

 error and estimation error to minimize excess risk as best you can。 That's the job。

 If you were to get more training data， what do you do？ Yeah。 If you get more training data。

 you will be justified or it will make sense to enlarge， your hypothesis space。

 which would decrease approximation error。 And hopefully。

 the increase in sample size will let you maintain your estimation error， at a reasonable level。

 So you'll notice that we write the ERM。 We're writing the argument over this hypothesis space。

 which is fine to write。 But in practice， you actually have to find the argument。

 This is what we use optimization algorithms for。 So let's think in there a bit。

 because there's something going on there。 So it is true that for nice choices of loss functions and reasonable hypothesis spaces。

 we can find， computationally， the optimum， the minimum， the ERM， as precisely as we want。

 if we're going to wait for it。 So examples are red regression that you're working on in the homework。

 If you're going to wait， you can find the empirical risk minimizer to arbitrary precision。

 Takes a lot of time。 It's worth going that far。 First question。 First point。 Second point。

 there are situations like neural networks where in fact， we have actually。

 no idea how to find the empirical risk minimizer。 Now。

 it's not a convex function and we don't know how to find the true minimum of the objective。

 for a neural network， for example。 Is it an issue？ Yeah， question。 It doesn't matter。

 We may be coming back to that later in the semester， but the actual form， I'm just pointing。

 out that there are hypothesis spaces that we do not know how to find the empirical risk。

 minimizer for。 That's the main point。 Yeah？ How do we compute the base risk？ Ooh。

 How do we compute the base risk？ Yeah。 We cannot。 We can compute the empirical risk minimizer。

 Correct。 Yes。 We can never compute the risk or the base risk or the risk minimizer unless we have the。

 data generating distribution unless we know it。 In practice， we never really know it。

 We just have a sample from that distribution。 Why not？ It's a equal to zero。 Say again。

 The base risk may not be equal to zero。 That's true。

 There may be some randomness in the system that's always there， and you can never predict。

 better than a certain level。 Like for example， if you're flipping a fair coin and you want to predict whether it's。

 heads or tails， you can't do better than 50/50。 There's no prediction function that will have low risk。

 Good questions。 Any other questions？ Yeah。 [ Inaudible ]， Okay。 So the question is。

 we've run our optimization algorithm。 We found the F hat U R M。 Is there any way to -- okay。

 We never said we could find it， but if someone gave us one， can we check whether it is the。

 actual risk minimizer？ I don't know how unless you know the data generating distribution。

 I don't know if there's any way to check that now。 Yeah。 [ Inaudible ]。

 Does larger F necessarily mean smaller approximation error？ Roger F。

 well approximation error will never increase as F gets bigger。 Right。 And when I say get bigger。

 what I'm precisely meeting in this scenario is kind of a nested。

 scenario where the next hypothesis space completely contains the previous one plus some， more。

 That's what I mean by bigger。 Yeah。 [ Inaudible ]， Okay。 So the question is。

 what if you -- we don't know the data generating distribution。

 What if we directly estimated the data generating distribution first and then computed the。

 base risk with respect to that distribution？ Yeah。 Okay。 That's a method。

 I think it's some scenarios that would correspond to the plug-in method it's called。

 The issue is that it's very difficult to estimate these distributions in the very high dimensions。

 that we work with in machine learning。 We don't have the data。

 If you want to have some slides from last year， first lecture on the cursive dimensionality。

 at a point。 Yeah。 [ Inaudible ]， Yeah。 [ Inaudible ]， Yeah。 [ Inaudible ]， Yeah。 [ Inaudible ]。

 Yeah。 [ Inaudible ]， Yeah。 [ Inaudible ]， Yeah。 [ Inaudible ]， Yeah。 [ Inaudible ]， Yeah。

 [ Inaudible ]， Yeah。 [ Inaudible ]， Yeah。 [ Inaudible ]， Yeah。 [ Inaudible ]， Yeah。 [ Inaudible ]。

 Yeah。 [ Inaudible ]， Yeah。 [ Inaudible ]， Question is how do we choose a hypothesis space？

 A lot of people use linear regression。 Why do we do something different or how do we do something different？

 In some sense that's the kind of the main question we're working with in this course。

 We're going to talk about a lot of different hypothesis spaces and when they might be beneficial。

 compared to something like linear regression。 So there's no simple answer to that。

 I mean this question is usually called the model selection problem。

 And it's a problem that doesn't have a direct answer。

 The machine learning course is the answer to the model selection problem。 Yeah。 [ Inaudible ]。

 F star may not be unique but fine。 That is true。 Thank you for asking that。

 First simplicity this year I changed all my slides to say argument instead of some more carefully written way。

 But there may not be a minimizer。 It may not be unique。

 If you see anything we do or you think that will cause a problem， give a shout。

 I don't think it'll be a big issue。 But yeah there are certainly situations that we'll talk about in fact tomorrow where the。

 empirical risk minimizer is not unique in a way that's a bit annoying。

 And we talk about how to fix that。 But for the approximation part I think it just is。

 I think that's okay。 Sure。 What is that？ What's the effect of the more data is the question？ Okay。

 No。 More data has no effect on our approximation error。

 More data we expect generally decreases estimation error。 Yes。 Right。 Okay。

 So what is the effect of the data？ The job of the data scientists is to choose the hypothesis space and one hopes to bounce the errors。

 But I suppose there are some use mediums to mean the error。

 Yeah well when I said bounce what I really mean is minimize the total error however you want to do it。

 So we expect that when it's time when the estimation error is in the job of the model to grow。

 As you change， let's discuss after an example coming up。 We can discuss after that。 Any more？ Yeah？

 You don't want to cover these two controls so we can talk about how to fix。 Yeah。

 So what is underfitting？ I mean if I had to put underfitting into this picture I would say underfitting is when the hypothesis space is so small that there's no issue with estimation error。

 So this gap is very small but this approximation error is big and the lack in our fitting is because the hypothesis space is too small or inappropriate。

 We may be， yeah， leave that。 So given a case like in a given it is one of the。

 data that we are not fitting or that we can't take some point because there is being white。

 But it is not a given by any particular point。 So I want to make these words a little bit easier。

 Okay。 First let me say this。 The question is how did I know in the example from last lecture that we are overfitting and not underfitting？

 We just say that I have not found a convincing precise definition of overfitting and underfitting per se。

 Okay。 So let's just， why don't we come back to that question？ Maybe yeah。 Okay。 So we move on。

 Good questions。 Where were we？ Optimization error。 Right。 So。

 I was saying first of all for some scenarios we can optimize to as find a precision as we like。

 In some scenarios such as neural networks and others we don't even know how to find the global minimum。

 Nevertheless we take a stab。 We write an algorithm that we hope find something like a minimum or at least has some small empirical risk。

 And we'll call it F tilde sub n。 This is the function that we actually end up with after we run our algorithm。

 All right。 It's not the empirical risk minimized necessarily。

 It's something that actually comes out of our algorithm。 It's also in that box of space。

 And we're hoping it's good enough。 Let's characterize how good it is。

 There's a notion of optimization error now。 It's the gap in the risk between the function that we get from an algorithm and the empirical risk minimizer。

 Because we're trying to find the empirical risk minimizer we probably aren't going to find it exactly。

 Not quite sure how far away we are。 The gap in the risk is called optimization error。 Questions？

 Okay。 Is optimization error greater than or equal to zero？ Yeah？

 Is it likely a little bit greater than？ Because you probably don't find the actual minimum。

 If you run my greatest descent or something， you may be fine。 Like when they're very close to it。

 Okay。 We're probably not going to find the empirical risk minimizer。 I'll grant that。

 We're not going to find it exactly。 There's always a precision perhaps that we will never reach。

 So that's true。 But with that， that implies something that's a little bit different from this。

 You know what it would imply？ So what we're minimizing is the empirical risk。

 So your comment that we're not finding the empirical risk minimizer would mean that our hat of F tilde minus our hat of F hat is greater than equal to zero。

 Is that clear？ Because we're not just fine。 It's building on the point。

 Which is that so in fact yes because。 Yes。 F hat n is the by definition the minimizer of our hat。

 So yes。 If this works out at F tilde minus our hat F hat that would always be greater than equal to zero。

 Okay。 [ Inaudible ]， We cannot estimate this。 What I was saying is that the whole reason we have F tilde that is our algorithm for getting F hat as well as we can。

 So we don't necessarily know how to find F hat exactly。 We can either get it very。

 very close or something that we just hope is close。

 One way or another that's what we're calling F tilde。 All right。

 So although F tilde certainly has worse empirical risk than F hat than the ERM。

 It doesn't actually necessarily have worse risk because， whoa， for various reasons。

 F hat is not a risk minimizer in any way。 It's just a empirical risk minimizer。

 So just you might get lucky that F tilde might actually be better than F hat in terms of actual risk。

 [ Inaudible ]， Well， estimation error。 At each step we have a goal。 Right？

 So our first biggest goal is F star。 We can't get this。 It's true for overfitting reasons。

 Then we say， okay， let's constrain。 Then the best we can do is F f is this best in the class。

 We can do that either because we don't have the infinite data set we need。

 We don't have the true risk。 What can we do？ We can minimize the empirical risk。 That's F hat。

 That's nice。 That's nice。 But actually to do that we'd have to be able to solve an optimization problem which we might not have the computing power to do。

 We might not have an algorithm to do it。 We may not actually be able to find the minimizer than empirical risk either。

 Even though we know what the empirical risk is， computationally finding the minimizer F hat may also be too difficult for us。

 So when we take another step back and we say F tilde。

 F tilde is the result of the algorithm we happen to run which whose intention is to find F hat。

 But it may not actually be exactly F hat。 This can be negative。

 But we usually think it's probably going to be positive。 Great。

 So here's this full access risk decomposition where we go all the way from the algorithm output to the base risk optimization error plus estimation error plus approximation error。

 Is this excess risk？ All right。 So we have some time before the break to go over an example where I hope this clears up some questions just by making it a little bit more concrete。

 So I'm going to give you a toy example where we completely control the we know the data generating distribution。

 We're defining the data generating distribution so kind of like in the laboratory setting we can see what would happen if we actually did know we could find the base risk and that sort of thing。

 So this is a classification problem。 Classes are blue and orange。

 Our input space is the unit square。 And the input distribution is going to be a uniform distribution on the square。

 And you can see that this you can see the distribution of the class label Y。

 Everything below this diagonal line is orange and everything above is blue。 All right。

 And the base error rate。 Oh， actually， I didn't quite say correctly。

 So the probability of it being orange below the diagonal line is 0。9。

 The probability of it being orange above is 0。1。 So I misstated before。

 So there is some error built into the distribution。

 Some thing built into the distribution that we can never get rid of。

 So the base error rate is going to be 0。1。 Even if we predict the perfect separation。

 which is the diagonal line， we're always going to have some error。 0。1。 10% error rate。

 That's the base risk for this problem。 Notice I still haven't talked about hypothesis spaces or sample data。

 So we've already figured out our base risk。 OK。 So what hypothesis space show you is I will in one slide introduce a new type of hypothesis space。

 which actually I hope a lot of you have seen before。 Trees。 Binary decision tree。

 If you don't understand every detail right now， this is fine。 It's just， well。

 hopefully we can get it。 So decision tree works like this。 And input comes in。 In this case。

 it's a pair X1， X2。 We start at the top。 This is a tree。

 Start at the top of the tree and there is a， there's this predicate， like a question。 And it says。

 is X1 less than or equal to T1？ If it is， we go to the left branch。 If it's not。

 we go to the right branch and we follow the tree down。 Next， we get here。

 Suppose it was less than or equal to T1。 Is X2 less than or equal to T2？ If yes， we go to the left。

 We end up in R1。 Otherwise we go to the right。 We end up in R2。

 Each of these things at the bottom are called leaf nodes。

 And you'll notice that they correspond to regions of the input space。

 So everything in R1 must have X1 less than or equal to T1。 And X2 less than or equal to T2。

 So we come over here and this is the region of the input space that corresponds to that terminal。

 node R1。 And every terminal node， every path down the tree， ends up corresponding to a particular。

 region of this space。 The region's partition of the space。

 And we can have a different action taken in every region。 Right？

 So how does this become a decision function？ We assign an action to every terminal node。

 In a classification problem， we could put， this could be class zero， this could be class one。

 Each region gets a class。 In a regression problem， each region gets a number。

 In a generalized regression problem we're predicting distributions， each region gets a。

 distribution。 Each region gets a prediction that we can produce in action。

 Any questions on binary trees？ Just rough。 The main takeaway is that it partitions your space into these blocks that are。

 because we， only， one thing I left off is that in this type of tree。

 the questions we ask only refer， to one coordinate at a time。 That's important。

 So that gives it this blocky structure where all the lines are vertical or horizontal。

 The depth of the tree， the depth of this tree would be three， because there's in the longest。

 path from root to leaf nodes。 That's how many decisions are made。 That's the depth of the tree。

 And you can imagine the deeper your tree is the more complicated partitions you can get。

 The more breakouts you can have。 We're going to consider the hypothesis of trees。 So， solid F。

 which is all decision trees on the unit square。 And then to consider subsets of that space， F sub D。

 which will be， F sub D will be a set， of all decision trees of depth D or smaller。 So even smaller。

 F D is even smaller than F， and we're going to consider a few of them。 F two， F three， F four， F。

 okay。 These are， these are called nested hypothesis spaces， because one is contained on the next。

 Any questions on this set up so far？ So here's what we're going to do。

 We're going to look at a few different F， a few different tree hypothesis spaces。

 And because we know the data generating distribution， we're going to be in this unique situation。

 that we actually can't figure out the best in this class。

 So we're going to be actually able to find the approximation error， exactly， which is an。

 unusual thing。 But here we own the data generating distribution so we can。

 And then we're going to run a algorithm， a tree algorithm， that is going to do its best。

 to find the empirical risk minimizer。 Yeah？ Yeah， sure。

 So I think intuitively you would agree that the best possible prediction function would be。

 one that predicts where you have to predict either an orange or a blue in every spot。

 Is that you predict orange anywhere below this diagonal line and blue anywhere above。

 Would you agree that that's the base optimal decision function？ In other words。

 it has the least chance of getting an error。 Yeah， so the issue is that even in this region。

 this is only 90% orange and it's 10% below。 That's why I wrote the 。9 and also written over here。

 The probability of orange for x1 greater than x2 is 。9。 So this will be orange 90% of the time。

 So if we predict orange， we're going to be wrong 10% of the time。 So the base error rates 10%。

 [ Inaudible ]， You almost can。 What you have to say is the base error is equal to the probability of error in your prediction。

 So you have to also include the probability， so there's two cases。

 One is that the correct answer is blue and you predict orange。

 But you have to add to that the probability that the correct answer is orange and you predict blue。

 So if you write that out， that will equal 。1。 [ Inaudible ]， All right。 So here we started with F2。

 Decision trees of depth two， MOS2。 And we've written down the theoretical best。

 This is just by math。 Basically， there's no computer involved here。

 We just see that this is the best we can possibly do。 And we compute。

 you'll see in like different regions of the space， you know。

 it's not totally orange or totally blue。 And if you predict， we're going to predict orange。

 for instance， in this block。 But you're going to be right only 83% of the time。 All right。 Yes。

 This is using math offline。 So we just measure and calculate and because everything is completely unknown。

 we can compute this。 Yeah。 Okay。 So it's kind of like assuming you had an infinite training set and an optimal algorithm that could find the best possible tree。

 But in fact， we just figured it out。 You can see there's certain symmetry。

 This is the separating decision boundary that's optimal in this case。

 Under the constraint that we're using trees of depth two。 All right。

 So what happens when we go to depth three？ Oh。 So what's the--so the risk of this boundary is 。2。

 20% error rate。 So while the best possible was the diagonal line which got us 10%。

 when we do this square line that's an output of it。

 So if we get an output of the decision tree of depth two， we get 20% error。

 So twice is twice the risk。 So the approximation error is the gap between the risk of this function and the best possible。

 So that's 。1。 Let's go to trees of depth three。 Again， we can calculate the best possible。

 We see that the risk of that is 15% 。15。 So it's a little better。

 And F4 gets a little bit more complicated。 The risk is 。125。

 You can see the approximation error keeps going down to 。1， 。05， 。025。

 So these are all theoretical bests。 Now let's see what happens when we actually estimate these things from data。

 So now I'm taking data。 I'm feeding it into my tree algorithm。 I use R。

 And seeing what it comes up with， I say only give me trees that are at depth in most three。

 Give me the best you can find。 And so for F3， you can't wait with this separating boundary。

 Not so great。 It has， we look at the error。 One thing to note is that we can always figure out this。

 the true risk of a F tilde by， I mean， we could either do it by calculation。 And yes。

 or we can just keep sampling more and more points， make a test that's， you know。

 a million large and estimate the risk empirically。 So this number should be as accurate as we want。

 But why did I write plus or minus 。04 when I wrote the risk of F tilde？ [ Inaudible ]， Okay。

 it's yes。 It's like standard deviation。 And why would there be standard deviation attached to that number？

 [ Inaudible ]， Yes， exactly。 So to compute， so we're taking different samples each time。

 To compute F tilde， we draw a training set。 And then we run our algorithm on the training set。

 Training sets random。 So F tilde is random， so its risk is a random number。

 And if we were to repeat multiple times with different training sets each time。

 we're going to get some variation in the risk of F tilde。

 And that's what's being captured by that standard error。 Yes， exactly。 Okay。 [ Inaudible ]。

 How can I compute the optimization？ I cannot。 What we can do -- all right。

 so the question is how do we compute optimization error？ We can't。

 What we can compute is the error of F tilde。 Because we get the error of F tilde。

 the risk of F tilde。 But we also know the approximation error。

 So what we can do is we know estimation error plus optimization error plus approximation error。

 is equal to the excess risk。 And so we can solve the estimation error plus the optimization error。

 Don't know how to separate the two。 That we can't do。

 What would we need to separate estimation error from approximation error？ Rather。

 estimation error from optimization error。 I think -- say again？ Yes。

 If we had an algorithm that could guarantee arbitrarily -- trees that are arbitrarily close to the。

 empirical risk minimizer， then we would know we had a -- then we would know what the actual。

 estimation error is and then what's left is the optimization error。 Exactly。 Right。 [ Inaudible ]。

 Right。 We cannot calculate the estimation error because I do not know how to find the best possible。

 tree in the class。 I don't know how to find the empirical risk minimizer。

 It's a computationally difficult problem。 Okay。 So as we get more -- all right。

 So this was for F three with a sample of size thousand， twenty-four。 This was F four。

 so a more complicated space。 You can see the -- the boundary is getting a little more interesting。

 And the error is going down。 And here's F six and it gets more complicated。

 And F eight gets much now starting to get a little bit crazy。 Okay。

 So sticking with decision trees of depth eight。 Now let's see what happens when we amp up the sample size。

 Yeah。 Right now there's one thousand， twenty-four。 There's no -- how many are there？

 We define the data generating distribution so we can generate infinitely many。

 We can generate as many as we want。 So ten， twenty-four gives this and now what you hope is as we increase the sample size。

 the estimation plus approximation error goes down。

 So we're looking at that number and we're looking at these which should look nicer。

 So we're looking at the number of data。 So we're looking at the number of data。

 And we're looking at the number of data。 And we're looking at the number of data。

 And we're looking at the number of data。 And we're looking at the number of data。

 And we're looking at the number of data。 And we're looking at the number of data。

 And we're looking at the number of data。 And these are fairly typical。 Let's break this down a bit。

 So x-axis we have tree depth。 As we increase the depth of the trees。

 things are getting more complicated。 So we have left to right。

 The Bayes risk is a constant at point one， ten percent。

 The green line is the minimum risk achievable by trees of the given depth。

 So you can see as the depth increases we can get closer and closer to the Bayes risk。

 This other line is the empirical risk minimizer。 And this has a very--this is kind of a classic shape。

 You see this a lot， a U shape， where the empirical risk minimizer with a very simple tree depth。

 very， very simple hypothesis space isn't very good。 Initially。

 as the hypothesis space gets more complicated and can predict functions with more， you know。

 subtleties in them， the risk decreases。 But at some point it starts getting worse again when the trees get too complicated because we start overfitting。

 And that's what's kind of being demonstrated here。 So what's increasing here？

 The estimation error plus the approximation error is growing more quickly than the approximation error is shrinking。

 So that is some question about the balance between the two。

 Let's look at that in terms of the error pieces。 So now I've drawn--so the excess risk is the green。

 The red is the approximation error which keeps going down。

 And then this blue is the estimation error plus the optimization error which kind of keeps going up。

 And we talked about why some F-confidence fans and some don't。 Yeah， question？

 >> If your independent variable for discrete， then you would be able to define the--。

 would you be able to find an optimum with the optimization error just by writing the writing on the tree？

 >> Sure。 If you had the time to wait， you could find the optimization error。

 You could find the empirical risk minimizer exactly as long as there's a finite set of decision functions to search over。

 >> Yeah。 >> Another question before we take a break？ Yeah。 [ Inaudible ]。

 So the question is if we can't distinguish between estimation error and optimization error。

 why did I even mention them？ And it's not that we never can。 It was a trade-off。

 So for linear regression or rigid regression， you can drive the optimization error century to zero。

 So there you know。 In this case， we couldn't， but then that hot space was interesting and we could figure out the exact minimizer。

 One question？ Yeah？ [ Inaudible ]， We can in this scenario， we can figure out the excess risk。

 we can figure out the approximation error because we know the data-gettering distribution。 Okay。

 In general， yeah？ [ Inaudible ]， Okay。 So the question is what can we do with the validation set？

 Does that enter in here， right？ [ Inaudible ]， Okay。 So another fresh data set。

 not the validation set。 How does that help us？ And let's even say it's a huge data set。

 So what a fresh， huge data set lets us do is get really good approximations to the risk。 Because if。

 remember what we said last time by law of large numbers。

 as the size of our sample increases to infinity， the imputeable risk of a particular function converges to the true risk。

 So with a big enough extra data set， a big enough test set or whatever you want to call it。

 we can get very precise estimates of the risk of any single function that we want。 However。

 that's not what we need to find the approximation error。 To find the approximation error。

 what we need to do is find the minimizer of the risk。 It's a harder problem。

 So we can get a good approximation to the risk of any particular function。

 But to get the approximation error， you're going to have to know the true risk of minimizer。

 which is another story。 Question more？ Alright， let's take a break。 And let's come back in。

 I say it's in five minutes because we're running a little late。 So around seven， ten， seven。

 thirteen。

![](img/4e43eb5d01ffd7bcdfbbc08b055bcf2a_10.png)

![](img/4e43eb5d01ffd7bcdfbbc08b055bcf2a_11.png)

 >> A group of questions last round。 Let's see what we can get through round two。

 So we're going to talk about L1 and L2 regularization。



![](img/4e43eb5d01ffd7bcdfbbc08b055bcf2a_13.png)

 These are really the work courses of data science， the Lasso and the Ridge regression。

 These are probably the --， If we had one set of algorithms to learn， this would be Ridge and Lasso。

 So， taking off an Ivanov regularization， this is the topic of this set。 Hypothesis spaces。

 we're talking about -- we've spoken vaguely about larger and smaller hypothesis spaces。

 And in practice， it's convenient to work with nested sequences of hypothesis spaces like trees of certain depth。

 like we worked on before。 And so we're going to talk about one particular way to get nested sequences。

 It involves defining a complexity measure on your decision functions。 So for trees we have one。

 right？ Depth of the tree。 That was a complexity measure。

 Last time we were talking about linear functions。 And you can kind of think how many features you have。

 the more features you have， the more complex prediction function you can get。

 That would be a measure of complexity。 Polynomials。

 the degree of the polynomial could be a measure of complexity。

 Last time I'd say stuff about smoothness。 So here's a precise way to define smoothness。

 If a thing is twice differentiable， you can integrate the second derivative of square。

 This is some kind of measure of how quickly it changes。

 So all these are ways to say more or less complicated for a single function。

 There's no ground truth of like what's really more or less complicated。

 We have different ways to define it。 So these are some options。 Okay。

 So for linear models in particular， we're moving towards sparsity with the L1。

 So we could also define like L0 complexity， which is even more direct measure。

 It's the number of non-zero coefficients。 So straight up how many non-zero coefficients are allowed to be a measure of complexity。

 The last little complexity that we're going to talk about later is if you have a linear prediction function。

 the sum of the absolute values of the coefficients。 The bigger that is， the more complex。

 the more erratic functions you can produce in a certain sense。 And there's another one。

 ridge complexity。 This is where you look at the sum of squares of the coefficients。



![](img/4e43eb5d01ffd7bcdfbbc08b055bcf2a_15.png)

![](img/4e43eb5d01ffd7bcdfbbc08b055bcf2a_16.png)

 And the larger that sum of squares is for your linear function， the more， again。

 the more bouncy or erratic types of functions you can produce。

 This is what you're using right now in your homework from ridge regression。 This is the penalty。

 It's the L2 penalty。 All right。 So given a complexity measure。

 we can define a nested sequence of hypothesis spaces in a pretty simple way。

 So we start with a particular hypothesis space F and a complexity measure that maps functions in F to some score。

 some number describing how complex they are。 And then we can define something that's like a ball。

 I'm just going to call it FR， F sub R。 Is the subset of F containing all decision functions that have complexity R or smaller。

 That's what we're going to find is FR。 And if this omega。

 this complexity measure omega were a norm on this function space。

 then this will quite literally be a ball of radius R in the space。

 When I picture these types of things， I am picturing a ball in a function space and a bigger ball in a smaller ball。

 Anyway， yes？ [ Inaudible ]， Oh， sorry。 Yeah， I haven't used this yet。

 So omega maps from F into R greater than zero。 That's my notation for real numbers that are greater than or equal to zero。

 So we can define some complexity levels。 And for each one， there's a corresponding hypothesis space。

 And as that complexity level increases， the hypothesis spaces grow in a nested fashion。

 This is how we can get a nested sequence of hypothesis spaces from a complexity measure and a series of points。

 All right。 So， let's bring this to our constrained empirical risk minimization。 So now。

 we have a complexity measure and we can talk about minimizing the empirical risk over functions F in our hypothesis space F。

 And then we say on top of that， let's restrict even more and say that the F's we're considering。

 this F's team means such that， so an additional constraint。 On top of that。

 the complexity of F should be bounded by R。 So we started with a big space F。 First。

 there's the whole space of all functions。 Then there's a space F， I have about the space。

 And then we're restricting the hypothesis space to a smaller hypothesis space F sub R of functions in F that have complexity in the most part。

 Cool。 And then we can vary R using validation data or cross validation。

 however you like to choose R and find the hypothesis space of the right size。 And， okay。

 So that's one form。 This form has a name。 It's called Ivanov regularization。

 There's going to be another form。 It's called TIKANov regularization。

 There's a little bit different， but it's the same idea。

 Here we're minimizing again over the whole space F。 But this time。

 there's no hard constraint on the complexity。 There's no bound the complexity needs to be less than R。

 Instead， what we do is we add into the objective function itself a penalty for how complex it is。

 So this is what you actually did in your homework。 This is the actual form from the homework。

 So we have the empirical risk plus lambda， some coefficient， times the complexity of F。

 And as we send lambda very large， this is going to be imposing a very aggressive complexity constraint。

 And it's going to be driving the function that we choose to have very low complexity。

 And when lambda goes to zero， this complexity penalty doesn't affect our empirical risk minimization at all。

 Is that clear？ So for very large lambda， we're penalizing the complexity heavily。

 which will make the minimizer of the entire objective function have relatively lower complexity。

 Is that clear？ Yeah？ Why do we need to constrain the hypothesis space F additionally？

 We already constrained it to get to F。 Why are we constraining it more？ Is that the question？ No。

 I'm being quite confused about the term。 Is that a problem you're just a example of？

 So in the previous example with the trees， you're asking。

 we had hypothesis spaces of varying sizes that got bigger。 And it's just a way to。

 it's kind of a way to quickly describe and try out and trade off between many different hypothesis spaces in an organized fashion。

 So at least in this， it's even more clear here。 As we change R。

 we're essentially getting different hypothesis spaces。

 They all happen to be subsets at the same space F。

 So this is a way to try out multiple different hypothesis spaces。 Remember。

 one of the jobs of the data scientists is to choose the hypothesis space。 Okay。 So， yeah？

 [ Inaudible question ]， So the question is if we fix lambda， are we， this is a little rougher now。

 If we， in this scenario， you know， we have a hypothesis space F and we have this complexity path。

 If we had this complexity penalty， are we really， does it correspond to a subset of the hypothesis space F actually？

 And what we'll claim later and you'll can prove in homework three is that there's an exact equivalent under some conditions between these two。

 Yeah？ [ Inaudible question ]， Yes。 That's right。 So， let me come to that in a second。 All right。 So。

 yes？ [ Inaudible question ]， I don't know what the question was。 Why what？ [ Inaudible question ]。

 Oh， why restrict it more？ Oh。 What， I was， so I was kind of saying that this is more a way to give us easy access to multiple hypothesis spaces。

 and try out multiple hypothesis spaces that happen to be nested in a convenient way。 So， like。

 a linear function with a very large feature space may still be too complex and may still over fit。

 even though it's a great restriction on all functions。 So we restrict it more in various ways。

 We can constrain the one norm of the coefficients or the L2 norm。

 We can constrain it very aggressively or we can constrain it lightly。

 And each of these things corresponds to a different hypothesis space that might have better trade-offs between overfitting and underfitting or approximation error and estimation error。

 So， it's all about searching for the right hypothesis space。

 It's not like you just choose one and you're done。 You have to try multiple ones。

 And this is a way to get there。 This is a very explicit way to look at trying multiple hypothesis spaces。

 Every R corresponds to a different one。 And this is a less explicit way。 Yes？

 [ Inaudible question ]， The question is， is inserting more constraints allowing us to generalize more？

 [ Inaudible question ]， So， indeed， the ultimate goal is to generalize。

 Generalization means basically risk。 Like， how do you perform on new examples？

 If you draw a random example from the data generation distribution， how do you expect to perform？

 That's risk。 That's what we mean by generalizing well。 It means having low risk。

 And that is the ultimate goal is to find a function space。

 such that when we run our optimization algorithm and pull a function from that space。

 it has low risk。 It generalizes well。 [ Inaudible question ]， Go on。 [ Inaudible question ]， Okay。

 So， you're saying that if you vary R， you're eventually just going to make R really large like the whole space F？

 [ Inaudible question ]， Yes， right。 But if we didn't have this constraint， it would be much --。

 [ Inaudible question ]， I think what you're saying is writing less than or equal to instead of equal to is in much difference。

 Is that what you're saying？ [ Inaudible question ]， Yeah， afterwards。 I'm not sure。

 [ Inaudible question ]， All right。 So， what I wanted to say in answer to the question here was。

 is there a difference between these two forms of regularization。

 the Ivanov and the Tikunov regularization？ And they're different in form。

 but in many general settings， they're actually equivalent。 What does that mean？

 It means that any F that you can get from some setting of R here。

 you can also get from some setting of lambda here。

 If you have the same loss and the same complexity of penalties and vice versa。

 If there's a particular setting of lambda that gave you a particular F。

 then there's another corresponding setting of R in this framework that would give you the same F。

 Setting all else stays the same。 And so， I think it's all I can say about that now。

 but so conceptually， you are free and right to -- if you see this。

 you can picture a ball in the space of some size， even though I'm practiced。

 This isn't constraining to a ball like the Ivanov form is。 And why might we prefer this form？

 It's because it's not a constrain's minimization。 We're constraining to F。

 but F could be a very pleasant space to work with， like all linear functions， for instance。

 And it's kind of an unconstrained optimization within F。 All right。

 So the proof of the equivalence between the two is actually a consequence of this Lagrangian duality theory that we're going to talk about next week。

 All right。 So now let's get into the last row in the ridge regression。

 So we have our linear least squares model。 Our function space is linear functions。

 parameterized by W， the coefficients， W vector。 And we'll start with empirical risk minimization where we just minimize this average square loss of the prediction over the data。

 And why isn't this enough？ Because even linear models can overfit sometimes。 So for instance。

 if your feature space is much larger than your number of samples。

 which happens in natural language processing， for instance。

 where you could have millions of features。 And even with linear prediction functions。

 you can overfit。 So we need to do something to constrain the optimization more。

 So ridge regression is， I'd say it's like the number one workhorse of data science when you have just the first thing you can try for most problems。

 And let me just break down the pieces。 There's this empirical risk piece。

 And this new piece is the complexity measure times lambda。

 The complexity measure here is the L2 norm of the coefficients。

 which is the sum of the squares of the coefficients。

 which again is exactly what you've seen from the homework。 And then the corresponding Ivanov form。

 which is the other way to phrase these types of problems。

 would be we minimize the empirical risk subject to an additional constraint that the sum of the squares of the coefficients is less than or equal to r。

 So a hard constraint on the sum of squares instead of kind of a soft penalty type of condition。

 And we can show that there's equal ones there。 So this is an interesting plot that's kind of common for these types of things。

 This is called a regularization paths。 And let me go first go back here to。

 let's talk about this bottom expression， the Ivanov form。 Now， when r is very small。

 when we choose a small value far close to 0， what you're going to end up with is a parameter vector w where all the coefficients are very close to 0 because the sum of squares has to equal something very small。

 So in that case， the coefficients are going to be very small。 And then the opposite extreme。

 if r were infinity， then what is your w going to end up at？ Yeah？ If r is infinity， right。

 which is the least square solution。 Exactly。 So this is what we're seeing here。

 On the left side of the graph， I'll tell you what the x-axis is in a moment。

 On the left side of the graph is what happens when we have regularization。

 very strong regularization， which is like the equivalent of r being very close to 0。

 And each of these lines is the value of the coefficient when we solve it for varying levels。

 varying amounts of regularization。 On the left， we have very aggressive regularization。

 so strong in fact that all the coefficients are 0。 And as we regularize less。

 the coefficients get larger than 0 and all the way to the right side of the graph。

 what we have is the ordinary least square solution where we have no regularization， no penalty。

 So what's the x-axis？ The x-axis is the ratio between the L2 norm of the coefficients and of the regularized solution and the L2 norm of the unregularized solution。

 So the highest value could be is 1， which is when we have no regularization。

 And the norm of the coefficients is the same as the norm of the least square solutions because they're the same solution。

 Whereas at the left， the norm of the coefficients。

 the sum of the squares of the coefficients is 0 because of regularizing so aggressively they all have to be 0 to respect to constraint。

 Yeah？ [ Inaudible ]， Question， is there any connection to principal component analysis？

 There actually is a subtle connection to principal component analysis。

 We can talk about that afterwards， but in principal component regression。

 which is where you run principal component analysis and first keep a certain number of principal components and represent your inputs in a space of reduced dimension and then run regression is kind of a。

 another type of regularization that's related to this。 But you can see that this is much smoother。

 We can regularize an arbitrary amount， whereas with PCA regression。

 we choose a specific number of dimensions to keep。 So you can see there is also a difference。

 All right。 Any questions about these regularization paths？ [ Inaudible ]， I'm not sure。

 So the question would be， so as the scientists， we're going to have to choose our hypothesis base。

 We have to choose one of these sets of coefficients to produce as their decision function。

 It's a good point。 And so how do we choose each of these x values corresponds to a different decision function with different coefficient values true and how do we pick which one to keep and not for that we would use a holdout validation set or something。

 I don't know in this case， which was the best。 Yeah。 [ Inaudible ]， [ Inaudible ]， [ Inaudible ]。

 So there's， well， the one I'm presenting is there's two steps。 First you choose your F。

 In this case， F shows in linear functions， all linear functions。

 And that's a space of a certain size。 And then in addition， I'm saying let's。

 we fixed our function of form， yes， true。 And I'm saying let's additionally constrain in different ways in terms of the sum of the coefficient。

 So there's additional constraint。 Yes， there's a different type of restriction in that the form is the same。

 but it's another way to take a subset， a smaller space。 All right。 So this is ridge regression。

 Great。 And now we're going to slide show a little bit。



![](img/4e43eb5d01ffd7bcdfbbc08b055bcf2a_18.png)

![](img/4e43eb5d01ffd7bcdfbbc08b055bcf2a_19.png)

 All right。 All right。 So now we talk about the last step。 You have a question？ [ Inaudible ]。

 So intuitively， so the question is why， what does the magnitude of the coefficients have to do with the complexity of the function？

 Okay。 So my short， so there's one answer is like， yes， visually in certain situations。

 they will actually， what？ It depends on the， let me just say this。

 The important part is that the size of the hypothesis spaces grow and shrink。

 Whether or not you want to agree that the functions individually are more or less complex。

 complexity is quite literally in the behind of the holder。

 There's different ways to define complexity。 So it's just a function that gives a score。

 a function that gives a score to every function， but it's also a way to describe to define this that I pop as a space。

 And a bigger hypothesis space has more， we could say has more complexity than a small hypothesis space just because it has more functions。

 Okay。 So， last little regression。 Just swaps out some of squares with some of absolute values。

 All right。 That's the， that's what's Lasso or L1 regularized regression。 And we have two forms。

 Just like before， it's taken off form with penalty and the Ivan off form with the heart constraint。

 And these are the regularization paths we get for Lasso。

 You could see that they are quite different。 And tomorrow we're going to drill in deeper to why they're different。

 But I think we'll get to that somewhat today。 What you're， what you're， what you're。

 I should see here is that on the left side where we're very aggressively regularizing。 Yes。

 they're all zero。 But what's different is that a lot of them stay zero until the regularization lightens up。

 So whereas here， here's comparing them side by side。 Whereas， ridge regression。

 as soon as we moved away from all being zero， they all got to be non zero and they grew smoothly thereafter。

 Whereas the Lasso， the regularization paths are quite different。

 A lot of them stay zero for longer and then move away from zero。 And this is。

 kind of related to what we were saying last time is that sparsity is one consequence of L1 regularization。

 And this is showing the sparsity where for certain choices of amount of regularization。

 for instance over here， there's only one coefficient that's non zero。 When we get to here。

 there's only two coefficients that are non zero。 At the dotted line。

 which in this example was what they finally chose for predicting out of sample， there are one， two。

 three non zero coefficients。 So two different ways to regularize give kind of two different types of coefficients that we would end up with。

 So let's talk a little bit about why。 So why do we care about sparsity？

 I kind of challenged you guys with that last time。 So when a coefficient is zero。

 we have a solution that's sparse。 We don't need those features。

 We don't need the features corresponding to those coefficients。 Okay， so so what？ Maybe。

 like what's the advantage of that？ There are some cases that it has advantages。

 One is a lot of times features are expensive。 You have to compute features。

 Sometimes you even buy features。 Like they're companies that produce features。

 They gather data and generate features for them。 And that has cost to it。

 If you find that you don't need that feature to do your predictions well。

 you don't have to use that feature。 Save money， save competition。

 So there's an advantage on a related note。 Sometimes you can have thousands of features。

 And if you want to run a system that's like giving predictions in real time。

 you have to store all those thousands of features in memory， perhaps。 So if you have， you know。

 50 million users and a thousand features of each user， that's a lot of features to store memory。

 Well， if you could have a sparse prediction function that only needs 15 features to do almost as well。

 that's a big advantage because you could store much， you could store your feature set in memory。

 From a more science perspective， maybe you're just interested in what features are the really important ones。

 So this is the feature selection problem。 Does it do better prediction？

 Sometimes it may actually predict better than say range regression。

 I wouldn't think that's your first reason to use it though。 And finally。

 it's quite good as a feature selection step。 The algorithms for running Lasso are quite efficient these days。

 And what you can do is use it as a way to choose maybe the most promising 50 features out of a batch of a thousand。

 for example。 Then you could take those 50 features and run just those on another more complicated nonlinear hypothesis space that requires a lot more computation to work with the finding empirical risk minimizer of。

 So you could use it as kind of a two step process。 First find your features that you like。

 then use those just those features in a more complicated machine learning algorithm。

 In terms of identifying the important features， will Lasso and ACI give us similar results？ PCA has。

 so PCA regression， oh， important features。 Okay。 Interesting question。

 PCA doesn't really find you important features very naturally。

 It finds you important linear combinations of features。

 You can then look at those linear combinations and say， oh。

 this particular feature of the linear combination has a very high coefficient。

 That must be an important one， but that's kind of a less natural thing to do with principal components。

 Yeah。 Good question。 Oh， yeah。 [inaudible]， Does that mean your kind of feature is more nonlinear or your trend or not？

 The first one is， I can't say yes， please。 [inaudible]。

 The idea here was that you buy a sample of the features， you get all the features。

 you see what you like， what works， what your Lasso selects。

 and then from then on you only use those ones。 So that's the idea。

 It's not that you have to see them at some point to assess them。 [inaudible]， All right。 Question。

 How do we figure out， this is a model selection problem。

 How do we figure out how much to regularize？ So which regularization coefficient or radius。

 whatever， is the one we use to actually get the decision function that we want to use in prediction。

 So what do you think is an answer to that question？ Anybody？ Second。 Yeah， use a validation set。

 So for every lambda that you try， you get a decision function。

 you get an estimate of its risk on it using a validation set。

 and you see which has the best validation performance， and that's what you use。

 This is the standard recipe。 Yes？ [inaudible]， Oh， great advantages to elastic net。

 but we'll talk about that tomorrow。 Great。 It's going to be an exciting topic。 Yeah。 [inaudible]。

 Can we choose a hypothesis space？ [inaudible]， Yeah。 So the question is。

 maybe you don't know initially how big to make your hypothesis space。 Let's make it extra large。

 So like we're pretty sure it's bigger than it needs to be。

 And then we go back and adjust the regularization to figure out the perfect size using lambda。

 [inaudible]， Yeah， we use regularization as a convenient way to adjust the size of hypothesis space essentially。

 Yes？ [inaudible]， Is that clear？ Good？ Okay。 Great。 Excellent。 All right。

 So we talked about why do we want sparsity。 These are all the reasons I can come up with。

 If you guys have any more reasons， I'd love to hear them and add to the slide。

 This is your easy interview question slide。 Why do we want sparsity？ That's all I got for you。

 [inaudible]， Yeah。 So if the underlying model is actually sparse。

 I would guess that you would get better prediction perhaps using L1 in that case。 [inaudible]。

 So maybe in a science-y view， you want to find what those features actually are。

 So identify the important features。 [inaudible]， All right。 So the little time left。 Let's。

 All right。 Here's what I'm hoping to do on the rest of the time。

 I'm hoping to get us understanding that picture that I showed in lecture one with the circles and the lines and the ellipses。

 I want to try to wrap that up。 Let's see if we can do it。 So let's think for graphical purposes。

 Let's take a very restricted iPod to space。 So let's take an input space that's R2。

 So we can draw on the xy plane。 So then our function space is simply based on two parameters。

 W1 and W2。 All right。 And so we can represent a function in a space by just a point in the plane。

 Right？ Bop the two coordinates， W1 and W2。 So what we have on the left is a contour of L2。 So these。

 I'm using this plane to represent functions in the hypothesis space F。

 So every point in this plane corresponds to a function。 How？ This axis is W1 and this axis is W2。

 All right。 So for instance， this point here， that's W1 is equal to 1 and W2 equals 0。 That clear？

 Correspondent to a friction function。 It's just F of x equals x1。 All right？ Okay。

 So I've convinced you that this plane represents all the functions in our hypothesis space F。

 And now let's do the Ivanov constraint version。 So within that space。

 let's look at all the functions that have L2 norm。 Less than or equal to R。 All right？

 So what I've drawn is this circle， which I claim is the。

 represent the set of functions that have L2 norm exactly equal to R。 Why did I draw a circle？

 This is the equation of the circle。 W1 square plus W2 square。 That is the norm of the L2 norm of W。

 And when that equals R， that's a circle of radius squared of R。 Okay。 Great。 Great。 Now。

 on the left， which are the points that correspond to functions that have some sparsity？ On the axis。

 great。 So what do I mean by sparsity？ Sparsity means。

 let's just for now say at least one of these coefficients is 0。 And yes。

 the coefficients are 0 on the axis。 So any point on the axis corresponds to a function with some coefficient to be 0。

 Fantastic。 What's going on on the right？ We have the L1 regularization。 And again。

 now the square is all functions that have L1 norm equal to R。 And again。

 the points in the axis would be the sparse ones。 So the question we're looking for is what is it about L1 regularization that supposedly leads to sparsity？

 So what's that mean？ Supposedly， that means that it leads to finding functions that are the coordinates on the coordinate lines。

 In the case of this kind of constraint that the norm is actually equal to R。

 we'd actually expect it to be one of these four corners to be the one selected。

 and if we're going to get sparsity。 So let's dig into that a little bit。

 See why that would be happening。 So here's the famous picture for the L1 regularization。

 So we've talked about this square boxes。 It's the set of all functions that have a norm L1 norm less than or equal to R in this case。

 Then we have this black dot w hat。 W hat is the empirical risk minimizer of the square error without constraint。

 except being an F。 No norm constraint。 So if we minimize this empirical risk over all w in R2。

 this is what we find。 Now， w hat is where we're here， which means it's L1 norm is larger than R。

 It's too big for our constraint。 So it's not the constraint empirical risk minimizer。

 We need to find something that has the smallest possible empirical risk， but it's in this blue box。

 So what we do is we say， okay， so this had risk， I don't know， it's called C。

 Let's go a little bit bigger than C。 Let's say C plus epsilon。

 And then all the functions that had risk C plus epsilon are on this red ellipse。 This first one。

 All right， we're still too big in norm。 We're still not L1 norm less than or equal to R。

 So it's taking a little bit bigger。 Then we go to the next ellipse。 And then we keep saying。

 all right， let's allow a little bit more risk， a little bit more empirical risk。 And so finally。

 we get to a level of empirical risk， which， and everyone on this red outside ellipse has the same empirical risk。

 And it just hits the constraint for the norm。 And that would be the solution that minimizes this empirical risk subject to the L1 norm constraint。

 But is that clear that that walk through？ All right， so yeah。

 There's absolutely a reason it's represented as an ellipse。 Question number one。

 Question number two。 Just because in this picture it hits the corner。

 why would it generically hit the corner？ Is there a question？ No， I agree。

 That is my intermediate question。 It's my intermediate corner。 Yeah， why would hit the corner？

 Fantastic。 Okay。 So first the ellipse。 So the answer to that is math。

 And I'm going to get a little bit of the math。 And the rest of the math is on homework two。

 So you'll get your chance to really work through the equations。 I'll take a start there。

 So these are -- so these ellipses are things with constant empirical risk。

 So what's the expression for the empirical risk？ This is another way to write it。

 This is a vectorized form。 And if we say -- okay， so I want a different。

 So this empirical risk is minimized by the ordinarily squares minimizer， right？

 When it's unconstrained。 And you know this expression。

 And the question is what does our unhat look like near W hat but away from it。

 So we can do this cool manipulation of our hat N of W。 This expression。

 And we can rewrite it in terms of W hat。 The W hat is the best possible solution。 That's the OLS。

 the ordinarily squares solution。 And we can write the empirical risk of W some other point。

 some other function in the space in terms of the risk of the best possible W hat。

 the ordinarily squares solution， plus a piece that makes it a little worse because we're not at the OLS solution。

 So this is an expression which you can -- you'll drive in the homework using this technique called Completing the Square。

 which you may remember from algebra in middle school or something。

 But this is the matrix vector version of it。 So it's a little bit fancier。

 I put a little document on the website explaining what this Completing the Square looks like in vectors and with matrices and vectors。

 I used to call it Completing the Quadratic Form as a better description but no one else calls it that。

 So Completing the Square。 All right。 So do you recognize this expression？

 Does that say a ellipse to you？ Or ellipse to it？ All right。 Well。 All right。

 Let's go a little further。 So now let's consider the set of W， the set of points in that plane。

 that have --， that exceed -- whose empirical risk exceeds the minimal possible empirical risk by C。

 by certain amounts of C， right？ So that's a set of all W where the empirical risk is equal to C plus -- that's what we have。

 That's a bug， sorry -- plus the risk minimizer。 And it has this form。

 And this you can -- some of you will recognize as the equation for an ellipseoid。 All right。

 So if that's not familiar， that's another issue and that you can review separately。

 But this is the -- this is the equation of an ellipseoid in Rd。

 And so that's how we know it's an ellipse。 So you can look up ellipseoids and see that this is what that is。

 All right。 So this is a little bit of matrix algebra to show that。 All right。

 So the second question was， why should it hit the corner？ So it's a great question。

 And I'm going to give you a picture answer， which is --， it is what it is。

 It's not a proof of anything。 I am not quite -- I mean。

 there are -- there are ways to show that things converge to sparse solutions。 And for instance。

 the situation of the true model being sparse， that's called sparse-distancy。 But this is different。

 This is saying -- this is not about convergence。 This is saying we have a fixed data set and we're ending up with sparse solutions。

 And why？ And I'll draw the picture that I find helpful。 So -- okay。 So here's our L1 ball， right？

 All right。 Let me make it a little smarter。 So here's my claim and you can verify it yourself。

 Let me draw some lines here。 And let's do the coloring。 All right。 So here's my claim。

 So to simplify it， let's suppose instead of ellipses， we had circles。

 just to make things a little bit easier。 So remember we had a W hat。

 which was the ordinary least square solution。 So what I'm going to claim is that if the W hat。

 the OLS solution， is anywhere in the yellow areas， and the ellipses --。

 and we have a circle instead of ellips， it's going to hit a corner。

 And if it's anywhere in the non-yellow areas， it's not going to hit a corner。

 So if you grow a circle around this point， it's going to hit the edge。

 But anywhere in this whole sector， it's going to hit a corner。

 So does this convince anybody that in some imprecise sense we're going to be more likely to hit a corner than an edge？

 OK。 So I might try to formalize this when we get to Bayesian statistics。

 where perhaps we could say like， if the true W is chosen kind of in a way that's symmetric and usually symmetric。

 So we're as likely to get something in this sector as its other sector and somehow how likely we are to get something in each sector is proportional to its area。

 then perhaps this can be made precise。 Yeah？ [ Inaudible ]， Will decrease？ Let's come back to this。

 Let's do two minutes。 Let me do one more slide。 Let's come back to this picture。

 This is the core of picture from lecture one。 So does this picture explain anything about lasso？

 So when I looked at this recently， I was like， I don't get this。 These are lines。 We need ellipses。

 right？ I mean， I get the idea of this line touching the corner， but we're not about lines。

 We're about ellipses。 So what's going on？ So can anyone think of any way to make sense of this picture in our context of lasso？

 Supposed someone told you that someone who wrote this wasn't -- maybe the person who wrote their core answer didn't exactly understand。

 but maybe the person who made the original diagram is like a real machine learning expert。

 Is there any way we could twist this to actually represent something meaningful for lasso？ Yeah？

 [ Inaudible ]， Maybe。 [ Inaudible ]， So it could be -- not sure。 It could be a tangent。

 but the tangent is different from the actual level set。 Yeah？ [ Inaudible ]， Okay。

 So I think another way to say what you're saying is that if you imagined that our W hat。

 our least-forged solution， we're really， really far away。

 Then when that ellipse boundary comes all the way back here。

 it's going to look like a straight line。 All right？ So， okay。

 that would be a way to make sense of it。 So suppose we were in that situation that the W hat were really far away。

 and so it looks like a straight line。 And what I see when I see a straight line is it's even more likely to hit a corner than when it's rounded。

 Right？ And so this actually kind of makes sense because when W hat is really far away。

 then when we have this hard-straint where a regularization is changing W hat a lot。

 it's pulling it in tremendously。 And so to tie it together。

 if regularization is extremely aggressive， it's having a very large effect on the change in how W hat。

 these squares W hat changes， then we're going to end up with more sparsity。

 or more likely enough with sparsity。 So that's my best way to interpret this picture in terms of lasso。

 All right。 So I don't want to keep you guys past nine as nine now。



![](img/4e43eb5d01ffd7bcdfbbc08b055bcf2a_21.png)

 You're welcome to say but we're also we can end the class and I'll see you guys tomorrow。

