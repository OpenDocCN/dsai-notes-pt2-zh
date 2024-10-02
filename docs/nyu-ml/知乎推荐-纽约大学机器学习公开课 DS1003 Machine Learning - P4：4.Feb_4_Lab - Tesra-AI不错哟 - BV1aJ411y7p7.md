# 知乎推荐-纽约大学机器学习公开课 DS1003 Machine Learning - P4：4.Feb_4_Lab - Tesra-AI不错哟 - BV1aJ411y7p7

 Alright， so I get started。

![](img/8074d5ece37ab440fb724f0e80292e6c_1.png)

![](img/8074d5ece37ab440fb724f0e80292e6c_2.png)

 Cool。 So today we're continuing with the LASO and we're going to talk first about some methods。

 to actually optimize the LASO just like we have gradient descent， stochastic gradient descent。

 applied directly to the objective function to do the ridge regression。

 Now we're going to see what can we do for LASO。 Alright， can you guys hear me？ Alright back there。

 Alright， great。 Alright， so recall this is the objective function for the last two。

 We have our average square loss plus an L1 regularization term， which is some of the。

 squares of those coefficients of the linear model。 And we can start by saying alright。

 what about gradient descent？ And we get stuck right away because this L1 norm is a differentiable。

 If you break it out， it's got absolute values in it。

 It's not differentiable what the kink and the absolute value。 So what can we do？

 So there's a common trick that we use in this sort of situation。

 It starts off as a trick and eventually you'll get used to it and it's just a tool you'll use。

 And it's called breaking numbers into their positive and negative parts。

 So let me show you some notation。 So consider any number A， just a number， real number。

 And we define the positive part of A。 We write it A with a plus and a superscript。

 So basically the either A， if A is positive， or zero if it's negative。 Or zero。

 So the positive part of 10 is 10。 The positive part of negative 10 is zero。

 It's gotten a positive part。 Similarly with the negative part。

 A minus the negative part of negative 10 is 10。 The negative part of 10 is zero。

 So the negative part of a negative number is the absolute value of the number。

 And the negative part of a positive number is zero。 So this will be nice。

 One thing that we'll get is that you can write A。 How would you write A in terms of A plus and A minus？

 A generic A。 It could be positive。 It could be negative。 Yeah， okay。

 So you can decompose A into A plus minus A minus。 Because if it's positive。

 A minus is zero and A plus is the right thing。 If it's negative， you got zero minus A minus。

 which is the right value of A。 Good。 So I'll just， well it'll show up on the next slide。 Similarly。

 what do we do for absolute value of A？ This is maybe even easier。

 How do we write absolute value of A in terms of A plus and A minus？ Yeah， A plus plus A minus。

 Because A plus and A minus are already not negative。

 So we just add them together to get the absolute value。 Great。 Alright。

 So we can apply this trick to lasso in a certain way。 So here's the last problem again。

 Now what if we wrote every component of W in terms of A plus and W plus and W minus？

 So we say W i is equal to W i plus minus W i minus。

 We basically take our vector of W's and make two new vectors。

 the positive part of W and the negative part of W。

 And then we say W equals the difference between those two。 Alright。 That's interesting。

 Let's try that。 Let's try plugging in that decomposition into this objective function。

 And what about here？ We have this L1 norm of W。 So that's easy to write。

 The L1 norm of W is like the sum of the absolute values。

 So you're going to have a sum of W plus and W minus。 Let's see how it looks。

 I'm missing a transpose。 Anyway。 So we have the W part becomes W plus minus W minus。

 And then the absolute value part。 Can you see what I've done wrong then？

 Is this a vector or a number？ Or a scalar？ This is a vector still。 So what do I have to do？

 Say again？ That would give the sum of the squares。 Yeah。

 We basically need to sum the entries of that。 So one transpose that， since that is a common true。

 So what's nice now is we've written this in terms of there's no more absolute value。 Alright。

 So now this thing is differentiable。 We got rid of the kinky absolute value。

 The absolute value of the kink。 But we in exchange have to constrain W plus and W minus to be non-negative。

 So we have a nice and smooth differential objective function。

 But now we have a constraint on W plus and W minus。

 We've also now instead of just one vector of size D， we've got two vectors。

 So we have a total of 2D variables。 Alright。 So that's the trade-off。

 We have 2D constraints and 2D variables。 But it's differentiable。

 And before it was not differentiable， we had no constraints and we had half the number of variables。

 Okay。 But we know how to attack this。 We can do for instance， we'll see on the next slide。

 So there's something called projected stochastic gradient descent。

 So in projected stochastic gradient descent， it's just like stochastic gradient descent。

 You take your point， you find your gradient of the objective with respect to that point。

 You go in the opposite direction， a certain step size。 That's the stochastic gradient descent piece。

 And then what's the projection part going to look like？

 What's the possible issue with the step I just took？ I might have violated the constraints。

 I might have stepped out of the set satisfying the constraints。 In this particular problem。

 that means I might have taken a step in a direction， that let W plus or W minus go negative。

 And that violates the constraints。 So the projected part means we project that point where we ended up back into the constraint step。

 And it's very easy in this setting。 How do we do that projection？ Yeah？

 I will dial into the other part。 Okay。 That's tricky。

 There's an even easier way to make sure we get back into it。 Yeah？

 Two of the terms that I'm getting？ Yeah， we can simply。

 if we take a step and W plus suddenly becomes negative point five， we just bring it back to zero。

 So we overshot and then we say， okay， back up。 That's the projection。

 So for last sort of stochastic projective stochastic gradient descent is as easy as stochastic gradient descent。

 plus a truncation when we cross zero。 All right。 Very good。 All right。 So that's one method。

 easy to understand， easy to explain。 Let's try another method。 Coordinate descent。

 So coordinate descent is a very general method。 It applies to many different objective functions。

 So I'm going to present it a bit in general and we'll see how it applies to Lasso。

 So let's suppose we have this function， general now， not just Lasso。

 It's a function of a D dimensional vector， W1 through WD。

 And recall that when you take a gradient step or stochastic gradient to step， we're potentially。

 updating every entry of our parameter vector。 So we go the gradient direction and if that gradient has non-negative entries in all of its dimensions。

 when we take a step， we're going to change every entry of that W。 Right？ Okay。

 So coordinate descent does something different。 In coordinate descent， in every step。

 we only update a single entry， a single one of these， W's that we're optimizing over。

 So how would that look？ We start， for instance， trying to optimize over W1。

 And what that would mean is we look -- this is the W1 direction， the coordinate direction。

 And we say， all right， I need to minimize dysfunction along this line。 Somewhere along this line。

 I want to find the minimum， holding everything else fixed。

 So I find the minimum in the W1 direction and that's one step of coordinate descent。

 Now I go to my next direction， which is W2， which is this way。 And then I minimize our longest line。

 So maybe I go all the way to here。 All right？ And now we do another coordinate。

 So maybe that's W3 direction。 That might be this way。 Okay。

 So we iterate through the coordinate directions， each time freezing all the other things that we've seen。

 and just optimizing over one of the directions。 All right。 So in math。

 we write -- so the i-th coordinate， the new i-th coordinate that we stepped to。

 is the minimum over that i-th coordinate of the objective function。

 where everything except W_i is fixed to whatever it was before， and we optimize over W_i。

 This is coordinate descent math person。 Yeah？ [ Inaudible ]， Okay。 Question。

 When does this actually work？ Great question。 We'll come back in a second。 All right。

 So in this true， though， that I kind of left out some details。

 When I say minimize long this direction， how do we do that？ Okay。 So maybe that's another iteration。

 Maybe we have to do steps to do that as well。 And that's -- think of that as a subroutine of this optimization method。

 And it turns out that this is a good one。 This coordinate descent is good。

 When that subroutine is easy， when it's easy to find this arg min for one coordinate at a time。

 If that's an easy problem， coordinate descent is a good idea。 Turns out it's very easy for lasso。

 That's why I bring it up。 All right。 So， yeah。 I wrote it here。

 So coordinate descent is great when it's easy or easier to minimize。

 with respect to one coordinate at a time。 Then to do the full gradient or the gas gradient or something。

 Yeah。 [ Inaudible ]， So you're asking how do we compute this arg min？

 Lots of different ways one can do it。 So -- but I -- no。 Your question specifically was。

 do we just take a little bit of a step in the direction。

 of the minimum along the line or do we go all the way to the minimum？ I think it's your question。

 No。 Well， wait。 Let me answer that question。 Which would have been a good question。

 Which is that in the classic coordinate descent， you do the full minimization。

 So you pick a direction and you do your full search。

 Maybe you have to go back and forth and you find the minimum in that direction。 And you're done。

 This is the minimum in that one coordinate。 And then you do your minimum -- that's -- that's the classic version。

 There's also a version where you just take one step in a coordinate direction。

 So I do maybe one gradient step in this direction。 One step in this -- not a gradient step。

 It's one step in direction -- so what would the gradient step be in one dimension？

 Which direction do I move？ What are my options for a gradient step in one direction？ Yeah。

 either go that way or I go this way。 And everything else is steps us。 So -- yeah。

 Is this about the consistent with gradient descent？ I don't know what quiet that means。

 If there's only one global minimum and they both find it， then they will find the same one。 Okay。

 Okay。 All right。 Okay。 Lots of questions。 Yes？ [ Inaudible ]。

 Is this a version of batch gradient descent？ [ Inaudible ]。

 There's nothing stochastic in this method that I presented。 So this is generic。

 This is for any objective function you're optimizing。 If we applied it to LASO。

 it would be the full objective empirical risk plus regularization。 Yeah？ [ Inaudible ]， Yeah。

 I mean， but we're not going to just do one path。 We'll cycle through。 Okay。 All right。

 So why do we bring up coordinate descent for LASO？

 What's quite surprising is that for the LASO objective function， the minimizer in。

 a coordinate direction has a closed form， an explicit expression you can just solve for。

 mathematically。 So no iterative method to find that minimum， or minimum。

 along one coordinate direction。 It's pretty surprising。 I'll show you what the form looks like。

 and then as an optional homework problem， you can derive it。 We can -- we'll walk you through that。

 So this is the whole expression。 This is -- so noted， this is the minimum over。

 single coordinate WJ of the LASO objective function。 All right。 And it has this interesting form。

 I'll just point out to -- well， I'll briefly speak， about this CJ。

 and then you can kind of study it more on your own。 So CJ， if you look in here。

 there's a W minus J transpose times xi minus J。 What is this？ This is saying。

 let's take our parameter vector W。 Let's leave out the jth entry。

 Let's take our x coordinates and leave out the jth entry。 And let's take their inner product。

 So that's like making a prediction using all of， our features except the jth one。

 So this little term is， what's the， prediction leaving out the jth feature？ And we're predicting on。

 in this case， the， i-th data point。 And we're looking at the residual when we。

 predict on the i-th data point without using the jth feature。 All right。

 And then we look at that residual and we -- see， we're taking like an inner product。

 of it with that jth feature which we had left out of the prediction。

 And so this is roughly like how correlated is that jth feature with the。

 residual when we predict things without the jth feature。 It's rough。 Okay。

 But this is what I think of when I see this。 All right。 In any case， so if that cj。

 which I'm going to think roughly as how， correlated is the jth feature with the residual。

 not using it， if that's small， so， it's not very helpful in fixing that residual。

 then that coefficient gets mapped， to zero。 And otherwise it gets mapped to something else。

 That's all I'm going to say about this。 But you'll have a chance to look at it more， carefully。

 So the takeaway is lasso seems free promising for。

 quarter descent because that minimization that we do in each quarter direction has。

 an explicit form。 We could just code up directly。 So it has a sense that it will be， very fast。

 Okay。 So the question -- one question was， one does this thing work？ It's a great question。

 So here's a first kind of the easy sufficient conditions。

 Turns out it's not enough for lasso though。 So if you're minimizing an f from rd to r。

 sufficient conditions for this method to work is that f is continuously。

 differentiable and it's strictly convex in each coordinate。

 So if you fix all the other coordinates and you look at just the -- just as a， function of wj。

 for instance， it's got to be strictly convex in that。

 We'll talk about -- we'll get into -- we'll review what convexity is maybe later or next week。

 So what's -- what's goes wrong with the lasso objective here that doesn't meet these， criteria？

 I've already mentioned it。 It's very --， obviously， it's differentiability。 Yes。

 it's not differentiable。 So criterion one is， violated。

 So this is nice and easy to use in sub-situations when it's true， but it's not， for lasso。

 So there's a more fancy theorem which does apply。 So this is an interesting， theorem。

 So it turns out if the objective function f that we're minimizing decomposes。

 in a certain way or in good shape， basically it's that it decomposes into two pieces， one。

 of which is a function which is differentiable and convex。 So g is like the nice part。

 differentiable and convex。 So an example would be aeroimpirical risk， right？ That's a sum。

 with the square loss。 The sum of the square losses， that's differentiable and it's， convex。

 And then this other piece with the sum over hj's acting on one coordinate at， a time， all right？

 And each of these hj's only have to be convex。 It doesn't have to be， convex。

 It doesn't have to be differentiable。 So how does this apply to our lasso？ Yeah？

 [ Inaudible Remark ]， Yeah。 This thing is exactly the form of the l1 penalty。

 The l1 penalty is the sum of， the absolute value of each coordinate， all right？

 So hj is an absolute value function， for the lasso in case。 And yes。

 it's only working on one coordinate。 So this is almost， perfect for the lasso scenario。

 So this justifies using lasso coordinate descent， for the lasso。 All right。 Any questions on that？

 Why does this justify the use of the lasso？ Simply that if you recall the lasso， we have this piece。

 which is differentiable and， convex。 And this piece， if you write it out。

 it's the sum of the absolute values of， wi。 And that's of this form where hj is the absolute value function。

 Okay。 All right。 So just， a side note。 Yes？ Can you repeat it？ Can you repeat it？

 [ Inaudible Remark ]， So the ridge regression。 I don't know。 That's a good question。

 If there's an advantage， I'm not sure。 It might be worth a try。 That'd be interesting。

 I think it would depend on the specifics。 What's the dimension of your space， for， example？

 So if your space is very high dimensional， you have to do a lot of -- you。

 have to go through a lot of coordinates before you finish one pass。 I don't know。 Yeah。

 It's a good question。 All right。 So what about coordinate descent when we don't。

 have this beautiful thing with the explicit closed form expression for the。

 minimizer in the coordinate direction？ Like what do we do then？ So do we really have。

 to go all the way to the minimum in the coordinate direction before we stop？ Can we。

 just kind of go a little bit in that direction and then go to the next， coordinate？

 So it turns out that for lasso regression， the answer is yes， and， there's some paper proving that。

 So that's interesting。 We can combine the two， things we've been talking about。

 So we have -- remember， this is the， differentiable version of our lasso objective。

 which we -- since it's differentiable， we can go ahead and do gradient descent or stochastic gradient descent on it with。

 the constraint。 Or we can try coordinate descent on it， but we can use a modified。

 version where we choose a coordinate and we take the gradient with respect to only。

 one coordinate at a time and do just one step in that direction and then move on。

 to the next coordinate。 I just wanted to mention this。 I don't want to go into。

 too much detail because we have some other stuff to cover， but I just wanted to put。

 this on the side。 You can take a look later ask questions if you want。 All right。

 So that wraps up the optimization -- the notes I wanted to give on， optimization for lasso。

 And then you'll have some implementation of that to do on， homework two。

 So you'll get a chance to actually dig into that。 All right。 Okay。 So now as promised。

 we're going to go a little bit deeper to， understanding lasso and ridge and how they compare understanding their properties。

 So let's start with a really simple model。 Another kind of like a thought， experiment。

 So suppose we have a single feature， x1， all right。 And we have a。

 response variable and out the variable y， both reals。 And suppose we get some data， you know。

 xy pairs， it's just two columns。 Very simple。 And we run least squares。

 regression and we find that the empirical risk minimizer is a -- because we were。

 restricting linear functions -- is simply f hat x equals four times x1。

 That's our empirically best linear predictor of y given x。 All right。 Very， simple。 All right。

 So that's nice。 And now here's the question I posed。 What happens if we introduce a new feature。

 a second column， x2， but x2 is， always exactly equal to x1。 All right。

 So I claim that we have no new， information。 x2 is exactly x1。

 So the empirical risk minimizer we had before is， still the best。

 We're still not going to be able to beat four times x1 in our。

 prediction because x2 tells us nothing。 All right。 Sure。 But what's different is we。

 actually have more options now。 Now we have two things。 And， you know， 2x1 plus 2x2。

 gives the same predictions， right？ Because 2x1 and x2 are equal， so that sums to 4x1， same thing。

 So there's lots of ways to bring -- to come up with an empirical。

 risk minimizer with the exact same predictions。 All right。 So this is true for。

 straight empirical risk minimization。 But what happens if we introduce L1。

 regularization or L2 regularization？ How does that play？ All right。 So first of all。

 anything -- and this is obvious -- anything where W1 and W2， the coefficients of x1 and。

 x2 sum to 4 is the same function， exactly the same function， when x1 and x2 are equal。 All right。

 So let's look at some different values of coefficients we can use for W1， and W2。

 And let's look at the corresponding L1 norm and L2 norm of those coefficients to get a。

 sense for what happens。 So all of these sum to 4。 And check out the L1 norm。 And this is just some。

 of the absolute values。 So you just matter adding 4 plus 2s or 2 plus 2s 4。

 Mine's 1 plus -- all right。 So here's an interesting one。

 So L1 norm is a sum of the absolute values。 So this is 1 plus 5 is 6。

 So check out that the L1 norm is the same for all of these solutions when they have the same。

 sign and starts to grow in at different signs。 All right。

 So this is -- this is the characteristic of， the L1 norm for a bunch of solutions where the coefficients have the same sum。

 All right。 So in words， what I draw -- the conclusion I would draw from this is that if we were to use an L1。

 penalty on least squares -- in least squares regression -- and we had two features that were。

 identical， L1， we didn't care which one you select as long as they're the same size。 It'll penalize。

 when they're different。 Same sign。 It'll penalize when they're different sign。 Okay。 So that's L1。

 Now let's go to L2。 So L2， you'll see it's minimized when they're equal， wait， 2 and 2。

 So is that -- is that， obvious why that would be the case？

 So you could actually show this using math again。 That if you have a bunch of numbers that sum to a fixed total and you want to minimize the sum of。

 their squares， which is the L2 norm， that happens when they're all equal。 So you can show that with。

 Leung-Rin multipliers。 We can also show it with a picture if you guys want to see that。 Okay。

 So let's have two coefficients。 Let's call them W1 and W2。

 And we want the set of all W1 and W2 that， have W1 plus W2 equal 4。 Those are all the ERMs。

 So the set of ERMs is equal to the set of W1 and W2， such that， they sum to 4。

 What's that set look like in this plane？ Yeah， I saw someone did this。 That's correct。

 So this is the set。 All right。 And what's the level set of the L2 norm look like？ It's the circle。

 right？ We talked about the S2。 Okay。 So the key point here is that the empirical risk minimizers。

 as we -- so this is the minimum loss。 This is the ERM。 And remember。

 just as we did last time with the L1 regularization and the L2 regularization， we said， well。

 the ERM is here， but it doesn't satisfy this L2 constraint。

 We need to gradually allow ourselves to have worse loss。

 which means moving away from this empirical risk。 But it's going to be parallel to this line。

 And so eventually it'll hit right at that 45 degree point， which is where W1 and W2 are equal。

 All right。 Some people bought that。 Any questions on that？ Yeah。 [ Inaudible Remark ]， Okay。

 So question。 L2 gives a split between the two， an equal split between -- and weight between W1 and W2。

 The first entry has all the weight on W1。 Question， which one do we prefer？

 You were suggesting the first one because of sparse or something， right？

 And then -- so last -- yesterday I gave a slide of all the reasons that one might prefer sparsity。

 What if none of them apply to me？ I don't like sparsity。 I'm not that into sparsity。 Baby。

 But there's a serious reason why we might actually prefer the second one。

 So we'll come to that in a little while。 All right。

 So the takeaway of the summary here is that when you put a L2 penalty and you have a lot of features that are exactly equal。

 then the L2 penalty will cause the weights to spread out exactly equally among the features that are equal。

 Now one penalty doesn't care how they get distributed as long as they have the same sum and they're all the same sign。

 All right。 So in practice， features are not exactly equal， typically。 But they're correlated。

 They can be highly correlated。 That happens。 And the point is that these same things that are for sure true when they're exactly equal are also roughly true when they're highly correlated and not exactly equal。

 Okay。 So in the practical case， suppose you have five features that are pretty correlated。

 not exactly the same。 When you do an L1 regularization。

 it may tend to select just one or a couple of those variables。 It may put something zero。

 It may kind of seemingly randomly assign different weights to each as long as they have the same sum。

 Whereas an L2 regularization on the same set of say five very correlated features will very definitively kind of spread that weight pretty evenly across five features。

 That's an important thing。 I think it's a very important thing to remember about L1 and L2。

 This is this property。 All right。 So what I'm about to show is some experimental data。

 what kind of simulated data that shows this in practice。 So I'll set up this model for you。 So here。

 the true model is that Y is a linear combination of Z1 and Z2。

 But we don't observe Z1 and Z2 directly。 Instead， we get three noisy observations of Z1 and three noisy observations of Z2。

 All right。 So the noisy observations of Z1 are all very correlated。 And they are near one thing。

 And noisy observations of Z2 are also correlated and near another value Z2。 Is that clear？

 And we're going to observe the noisy observations， not the z's。

 but the noisy observations of the z's。 And we're going to need to go back and predict Y。

 Is that setting clear？ All right。 Let's look at that in math。

 So let's suppose Z1 and Z2 are drawn from gouge distributions independently。 And then once we。

 and then we have， let's give ourselves six noise variables。

 six independent gouge noise variables to play with。

 And then we'll say Y is this nice linear combination of the Z's plus some noise。

 We don't observe the Z's， but if we did， this is the exact expression for the Y's。

 And then the X's are either each X， we'll say X goes from 1 to 6。

 Each X is either Z1 plus some noise or Z2 plus some noise。 Picture that？ Okay。 Great。

 So here's what we did。 We generated 100 samples of X and Y， of X and Y from this distribution。

 We generated Z's too， but we don't observe those。 And then just to give you a sense。

 the correlations among the X's in each of these two groups were quite high， 0。97。

 It's a typical correlation。 Alright。 So what we're going to look at is the regularization paths as we fit this data with lots of regression with different amounts of regularization。

 Okay。 So here's what we have。 Let's start all the way on the right。

 which is where we have no regularization at all。 So we have， we should have。

 we still have some regular。 That's interesting。 Okay。 So we have six variables。 Alright。

 And their values after lots of regression with no regularization have， I say， no。

 there's most of some。 So I got this from the book and I think there might be an error actually。

 I emailed the author and I thought it was close enough， but now I'm questioning。 But basically。

 what's， this is roughly correct。 So the two groups are in yellow and in blue。

 And they are totally correlated。 So you kind of would。

 you kind of want them to have equal weighting potentially， or， but in this case。

 LASO doesn't do that at all。 So it's， this is showing kind of LASO's indifference to where it puts the weight across the groups of variables that are correlated。

 Alright。 So I claim this is not a good outcome。 I claim that in a lot of situations。

 we prefer an even split of the weights across the things that are correlated。 So particular。

 what I think happened here is that the third variable， which is not even。

 we don't see two blue variables， right？ So the third one is zero all the way。 Okay。

 So the reason I'm wondering if this is incorrect is because with no regularization。

 it's very unlikely for any of those to actually be exactly zero。

 That's why I think something's a little off here。 So I'm not quite sure。 What's going on。

 but it's close enough to make the point。 Alright。 So can anyone give some thoughts on why we。

 why I'm concerned that this variable has， for instance， zero weight。

 even though it's no different than the other two in terms of what they represent informationally。

 They all have the same amount of noise of the original variable。

 Why should we ignore one of them and keep weights for the other two？ Why might this be an issue？

 Yeah。 Anyone？ As a beginner， trying to avoid overfitting is like in fact what you're trying to do here and put all the weight on one variable instead of splitting it more evenly。

 That might be to a lot of like variance of noise when it's exactly what we're trying to avoid。

 So putting all the weight on one variable， that might lead to you saying like variance and noise and you said overfitting。

 So maybe I think that's in the right direction。 Yeah。 [inaudible]， Yes。

 Our best estimator of the Z's would average all of the elements in each group。 That's right。

 That's the main point I have in mind when I say I like to spread the weight evenly。

 So let's think about that。 We really want to know Z which is the un-noise version of each of these yellow ones。

 That would be Z1 and each of these blue ones would be Z2。

 The best way to get rid of noise when you have three things that are noisy observations of the same thing is to average them。

 [inaudible]， If you have three people taking independent measurements of the same thing and would you rather just take one of them or would you rather take off three and average them？

 Certainly you want to average them。 It's a much， it's an estimate with a much lower variance。

 So in the regression setting， spreading your weight evenly across all the variables that have essentially the same information gives you a lot more robustness。

 So suppose instead you said， oh， they all have the same information。

 Let's be sparse and just put all the weight on X1。 Well。

 what happens if X1 for some reason had a lot of noise one day and your prediction would be totally off。

 Whereas if you took all three X1， X2 and X3 and gave them equal weight。

 which would do the same predictions typically on average， and then if X1 had an error。

 a particularly large noise， it would kind of be averaged in with the other two observations and it would kind of smooth that noise out。

 Yeah？ [inaudible]， Well， basically the question is does this make it difficult to find the important features？

 It depends what you mean by important features because basically what this is doing is it's。

 what I'm proposing would be nice to have done， is that if there's kind of a group of features that all show the same thing。

 then it's the group that's important。 There's no one that's more important than the others。

 So I would like to select the whole group or leave out the whole group。

 If you have other reasons to want sparsity， like， you know。

 you want to reduce memory or you want to reduce the time。

 you don't want to carry around all these features， that's kind of another motivation。

 Then you might want to keep only one of the batch。

 But if your goal is to make the best predictions possible and maintain robustness to noise and get the advantage of averaging out over multiple noisy versions of the same thing。

 then you should keep all of the ones in the same group。 Yeah？ [ Inaudible ]， Was court set not used？

 I don't see the connection。 Maybe we could talk offline。 Okay。 Yeah？ [ Inaudible ]， Okay。

 So the question， I think what you're saying is it possible that one of the variables is maybe less noisy than the others？

 Yeah。 And that when you combine it with the ones that are more noisy。

 then you're actually taking a penalty for that。 Yes。 I hear what you're saying。 And yeah。

 in some sense that is also an issue。 So in this pure setting。

 they all have the same amount of noise by definition。 So this is not an issue。 But in practice， yes。

 it's possible that some predictors are more noisy than others。

 even though they're all kind of around the same mean， for instance。 So in that case。

 it's a trade-off。 And that's okay。 We're finding methods that kind of have different properties。

 And then in practice， you try them out and you test them on validation error， validation data。

 and you choose which actually performs the best。 Yep。 Good question。 Okay。 All right。

 So the question is， how can we get the weight spread out more evenly？ So here， this is last。

 so it doesn't spread the weight out evenly。 What can we do to get it spread out more evenly？

 Any thoughts on that？ Yeah。 Okay。 So what if we use L2 regularization in addition to L1 regularization？

 So L1 doesn't care at all how we divide the weight， right？ But L2 cares。

 So if you just threw in a dash， a little bit of L2 regularization on top of the L1 regularization。

 if in the case of exactly equal features， that would already break the tide。

 And it would just put in a little L2 regularization in this setting， it would use 2/2 right away。

 It would use the one where the weight spread equally。 So that's the idea of elastic net。

 which is where we have an L1 and an L2 penalty。 And the idea here is that what you're hoping for is that groups of variables enter kind of together all at once。

 and have roughly even weights。 And then maybe the next group that's the second most useful will enter and become nonzero。

 and essentially the same time with roughly equal weights。

 So let's see what happens on our same data set with some LASO。 There's a theorem I'll come back to。

 So on the right we have elastic net curves and on the left we have pure LASO。

 So on the right is a LASO plus a little bit of L2 regularization。 And what you see is， yeah indeed。

 like all these three coefficient values in the different groups are quite tightly spaced。

 So it did manage to keep them with similar weights on the correlated variables。

 which was kind of the objective we're going for。 So the sense is that this elastic net will give you prediction functions that are more robust to little errors。

 because in a particular group， because you're at least kind of using a LASO。



![](img/8074d5ece37ab440fb724f0e80292e6c_4.png)