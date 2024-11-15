# P22：22.Lab_April_28 - Tesra-AI不错哟 - BV1aJ411y7p7

 All right。 Today we're going to talk about the e and algorithm with specific application。

![](img/362c510b7786023274101d45cf5e21b5_1.png)

 to the Gaussian mixture model。 All right。 So remember， a Gaussian mixture model we have。 components from which our data points are drawn and each component has a probability。 which we designate with pi and then each component has associated with a probability。 distribution or density in this case。 We have a different Gaussian density associated。

 with each of three components and each of these components would have a probability。 of generating a point。 So the generative model description that we're dealing with in Gaussian。 mixture models is first we draw a variable z which is the cluster assignment or component。 assignment from， have you guys heard of the categorical distribution？ It's like the blue。

 distribution is either zero or one。 Categorical distribution is one of k categories。 It's。 like picking a number from one to k。 It's related to the multinomial distribution but。 the multinomial distribution is if you chose n draws from a categorical distribution and。 you count it up how many of each type of number of one to k you got。 Okay， so certainly。

 keep a categorical and multinomial related。 So we choose a cluster assignment z from the。 categorical distribution and then we draw a point x from the density associated with， cluster z。 Okay， so that's how we generate our data points x。 Is that clear？ Questions？ Okay， good。 So that's a generative model and we can put that together into a joint distribution。

 for a pair x and z where of course x is observed but z will generally not be observed and this。 is simply definition of conditional probability。 But now let's plug in our conditional distribution。 of x given z。 That's that Gaussian and then pi z。 That's our probability of cluster z。 Okay。 so that's our joint but what we really need to work with is the marginal distribution。

 The marginal distribution for the data that we observe which is x。 We only observe x。 We。 don't observe z。 So we can get a density for x， a distribution for x simply。 What do we， do？

 It's very easy。 Yeah， right， we sum out over z which we don't observe。 That's marginalization。 like this。 Right， we take the joint， we sum out over z， we get p of x and then of course。 we could just substitute in our expression for the joint like that。 So this is our marginal。 distribution for a single x。 Great。 So one way to estimate the parameters of the Gaussian。

 mixture model is with maximum likelihood。 I mentioned yesterday that there's a method。 of moments approach also which is turning out to be very nice and you can learn about。 that in a second class。 Sontag's class I think。 Okay， but we're doing maximum likelihood， here。 So we're going to write down the likelihood of the data we observe and figure out which。

 parameters maximize that likelihood。 So here's the expression for the likelihood。 It's true。 of you now because we have the likelihood for p of x we did on the previous slide。 We have。 n data points。 X1 through Xn drawn iid。 So to get the likelihood of the whole data set， trivial。 we just multiply the likelihood to the individual points like that。 Okay。 All， right。

 in the usual way we want to look at the log likelihood。 It's， we usually think。 it's going to be easier to work with。 So we take the log of pd。 I'm calling this is going。 to be our objective function， our log likelihood objective function。 So now I'm writing it J。 and the parameters of the objective function are the parameters of the model that we want。

 to discover that we want to maximize over in maximum likelihood。 So when we take the log， of p of d。 the log moves nicely inside。 Can you guys see my hand？ Is this helpful？ All， right， good。 So we take the log of this product becomes the sum of the logs and we get sum， of the logs。 And then we wish we could have this log interacting with the Gaussian distribution。

 because the Gaussian distribution has this leading exponentiation and the log and the。 x cancel nicely。 But the sum blocks the log。 And this is what makes maximizing this a little。 bit difficult。 Okay。 So this is what we're going to maximize J using the em algorithm。 That's our motivation for em。 Okay。 Any questions on this？ This is just review。 Very good。 Okay。

 So a little more review。 Remember this thing we talked about yesterday， gamma， IC。 This is。 we're calling yesterday the responsibility of cluster C for the point xi。 I'm。 would prefer to just think of it as for xi。 What's the probability we think that it's， in cluster C？

 So that's gamma IC。 The vector of the gammas across all clusters is like a。 soft cluster assignment for data point。 And then the n sub C was， let's call this now。 the expected number of points in cluster C。 So I remember I said the probability and。 expectation were kind of interchangeable。 I just thought I'd worked that out for you。

 since got some uncertain stares last time。 So let's define n sub C as the expected number。 of points in cluster C for the data that we see。 So expectation of the sum in the。 we can put zi equal C。 So if the， if the cluster for xi， which is zi is equal to C， then this。 expression is one， otherwise it's zero。 We're adding up across all data points how many。

 zi's are equal to C。 So if we， this is a random variable， if we knew what it was， that would。 be the number of points that are actually from cluster C。 But we don't observe this， but we。 can take the expectation of that with this condition on the data that we do observe。 And。 then expectation of a sum is， solid the expectation， right？ And then expectation of an indicator。

 function is the probability of the event in the indicator exactly。 Good。 So sum by is。 the probability that zi is equal to C given xi。 And this of course is just gamma i C。 So this is how we get n sub C。 All right。 Good。 Good that everyone's nodding because you。 know then otherwise I would just do it again next time。 All right。 So EM algorithm for GMM。

 I showed you this yesterday。 It's an alternating algorithm where first we figure out the soft。 cluster assignments for each data point。 And then we have these parameter estimate step。 So very similar to maximum likelihood estimate for the regular Gaussian。 But now， for example。 for the mean， instead of just taking the， the mean of the points in cluster C， we don't。

 know which points are on cluster C。 So we take a weighted average where the weights are。 the probability that this point is in cluster C。 All right。 So this should seem plausible。 but you shouldn't necessarily see why this is actually the maximum likelihood or helping。 us get the maximum likelihood， but it should at least be impossible。 Okay。 All right。 So。

 here's an illustration。 So we'll start with randomly chosen means and variances。 This。 doesn't look random。 These variances are close to spherical。 Here are data points。 So we've。 initialized our parameters。 And then the next step would be to find the soft assignment for。 every point to the two clusters。 Right。 So for every point here， we find the probability。

 that it belongs to this cluster and the probability belongs to this cluster。 And here we color。 code based on those probabilities blue is dark blue is one dark red is this cluster two。 and things between is some kind of mixture and probabilities。 Yeah。 So the assignment。 here is based on a probability。 Sure。 That's， that's easy。 So basically， we have， we have。

 these two， so we had these two， let's go， first let's go back to the， so this is where we calculate。 that probability。 So the probability， say we're looking at the ith point xi， the probability。 that the ith point is in cluster J is we look at the weight of each cluster and we calculate。 its Gaussian likelihood and well this is the expression。 So it's， it's， it's， you can。

 explicitly calculate the probabilities。 Yeah。 Yeah， you initialize all the parameters， pi's。 mu's and sigma's。 Yeah。 Did you have something specific in mind for another way to do the。 soft assignments？ Okay。 Yeah。 So you can use other distributions besides Gaussian， you can。 have a mixture of some other distribution。 Okay。 All right。 So now we have our soft assignments。

 and now we have our parameter fitting which is using that weighted average of the mean。 and then a weighted estimate of the covariance and this gives us these adjusted means and。 covariance matrices， adjusted class specific densities for the two classes， two clusters。 All right。 And so on。 And this is the， yeah， algorithm converging to， so what do these， circles represent？

 What have I drawn here？ Yeah。 These are like the covariance ellipses。 of each of the two Gaussian distributions。 So you could think of it roughly as like maybe。 a one standard deviation contour of the Gaussian density， something like this。 Okay。 All right。 Yeah。 So there are some dots that have the colors that are not。 So the color of that。

 every dot basically represents the probability that is average。 Well， the probability of。 being in blue versus red。 So very blue is high probability of being in blue。 Very red is。 high probability of being red and purple in the middle is kind of split。 Yeah。 The question， is。 well， what is being in red？ What I mean is that it was generate in the generative， process。

 It was generated by the distribution。 That's the red color。 So yeah， it's certainly， possible。 but rare that from this distribution， we would generate a point that's all the way， over here。 So we would not assign that to the red cluster because that would be less， likely。 but it's possible to have come。 So there could be errors。 Yeah。 Yeah。 Yes。 Yeah。 Yeah。

 So you have a probability distribution over assignment to the clusters。 So there's， no relative。 It's the probability is always sum to one。 The color you could。 Yeah。 So。 if you can imagine that these colors are generated by， you know， you take， if the probability。 of being in blue is 30%， then we took 30% blue and 70% red and made the color。 Yeah。 Yeah。

 What is the expectation？ I mean， if you say you have an expectation step， I don't， know。 I didn't say anything my expectation step yet。 I mean， I did， but I didn't intend。 for it to be clear here。 No， I don't necessarily say that。 You know， if a point lands here。 it really is， it may not have a clear assignment to a cluster。 So， no。 So for a point to have。

 just like all， almost all its probability on just one cluster， you'd have to see that。 the likelihood of that point under the other clusters would have to be very， very small。 So that's what happened。 We would need these covariance matrices to be very， very， very， small。 So if the covariance is a very， very small， then yes， you will see more heart assignment。

 of every point， like either the one or the other。 And in fact， that's the lecture。 Next， slide。 So the example that you give us right now is that actually， so the self-market actually。 the result of this self-market algorithm is the same as the car parking。 No， I don't。 know about that。 So first of all， this is an interesting point that the gadget mixture。

 model approach doesn't give you in the first presentation a hard classification at all。 It gives you soft classifications。 So now you're maybe suggesting you threshold it to make。 a hard classification， a hard clustering。 I understand your question。 Is it just by coincidence。 that the graph that we see right now in next to this slide that we have fewer colors in， both sides？

 Is that coincidence？ How did it？ Oh， I understand your question。 Is it coincidence？ I'm not sure。 They are perfectly， the clusters are perfectly separate。 So the question is， I guess you're asking。 do the probabilities always converge to like zero or one？ Yeah， okay。 All right。 But so。 so EM for gadget mixture model seems a little like it means。 Seems like what you are suggesting。

 And there is a precise correspondence。 So first of all， in gadget mixture models。 we're allowed to have clusters that are shaped in ways that， are not circular。 So we can have clusters that look like this， for example。 Okay。 K。 means would never give clustering like this。 Okay。 So if we make a in the GM in the gadget。

 mixture model setting， however， if we have if we fix our covariance matrices to be spherical。 so not allowing stretched out conveyances。 And we have the variances going towards zero。 So really tight gagens。 Then the probabilities of your cluster assignments do converge to。 one on one on the closest cluster in， yeah， closest cluster in Euclidean sense and zero。

 on the others。 And then we do get a key means algorithm pretty much exactly。 Yeah。 Okay。 And that has to do with how the tails of the gagens decay。 So if you're very far from the。 gagens center or equivalently， if the variance is very small， then the likelihood for the。 cluster that you're closer to will be in some sense， exponentially larger than the one that。

 you're further away from the ratio of them will be very large when you're when when those。 variances are very small。 It's this type of thing that's very easy to try out in Python。 or something。 And you can just see that your likelihood under two gagens， two different， gagens。 different means say you're between but a little bit closer to one of them。 And。

 you look at the ratio of those likelihoods。 And then you send those variances to zero。 you'll see that the ratio goes up to gets very large。 Someone check that and post a， piazza。 Yes。 Yes。 There's no magic in optimization。 So it will be different though。 I mean， it means。 the course now that we have a nice correspondence， we can talk about the connection。 So if we。

 had a gagener mixture model approach and we restricted our models with this type of covariance。 we could still get stuck in local minimum in our attempt to find the maximum likelihood。 of the gagener mixture model。 So， okay。 So I don't have off the top of my head an example。 of gagener mixture modeling where we get stuck in a local minimum。 But it's interesting， question。

 So it is true that the likelihood function of for gagener mixture models is， not convex。 And so in general， there will be local maxima。 But I haven't thought about， it before like this。 So。 let's think about it for 20 seconds。 Anyone have an example？

 Can I think of an example where maximum likelihood gets stuck？ Okay， that's enough。 Okay。 Any more。 questions before we get into general EMR-able， and if we don't finish， we can continue next， week。 I think it's pretty interesting。 It's a little bit mathy， but it's not too bad。 I。 hope you guys will follow along。 Ready？ All right。 First， we have a few。 We have two or。

 three little lemmas to review from math。 First， you remember convex functions。 Good。 Jensen's。 inequality。 Very， very fun。 There aren't very many fundamental inequalities that come up。 so often in math。 There's triangle inequality， coach of shorts inequality， and he answers。 inequality are like the three top。 And I rarely see much beyond that。 There are， of course。

 but Jensen's is one of the top three。 David's top three。 Okay。 So， he answers inequality。 If you have a convex function， and x is a random variable， the expected value of f of。 x is greater than or equal to f of the expected value of x。 Okay。 All right。 Wikipedia has。 a nice geometric proof of this。 The way I remember it is with this example， I know that。

 e x squared， the expected value of x squared is greater than or equal to the square of。 the expected value of x。 How do I know that？ How do I always remember that？ Yeah， very， good。 So。 if I subtract e x squared， the expectation of x from e x squared， I bring this over here。 that's variance of x。 And I know variances are always greater than or equal to zero。 This。

 is how I remember the direction of Jensen's inequality。 Okay。 I see the answer is， was， there。 Okay。 So， that's Jensen's inequality。 Now， KL divergence。 Have you guys seen KL， divergence before？

 Kolbak Live Lord divergence。 It's interesting。 It's a way in some sense。 to measure how different two probability distributions are。 Okay。 So， it's not quite。 a distance metric， but it gives you a measure of how different things are。 So， here's its。 definition。 In the discrete case for discrete probability distributions， sum over the every。

 element in the support of the distribution， all possible values。 And Px， log Px over Qx。 It's a strange thing。 There's ways to understand it， but it's the best way to kind of get it。 is to look at information theory。 And I don't present it this year， but if you go to last。 year's slides， there's about 10 or 12 slides that's a very brief introduction to this field。

 called information theory， where things like Kolbak Live Lord divergence and entropy and。 mutual information all have very natural interpretations in terms of bits and coding。 up numbers and stuff like that。 Okay。 All right。 And the thing to， one thing to notice。 about KL divergence is that this is actually an expectation。 See， we're summing。 It's the。

 expectation of log of Px over Qx with respect to the distribution P where x is distributed， as P。 See how you can write， see how this is just an instance of the expectation。 Okay。 All right。 So we have this Kolbak Live Lord divergence and there's just two really important。 properties of it that we're going to use。 And this comes from what's called Gibbs inequality。

 And it simply says that the Kolbak Live divergence between any two distributions is first of。 all non-negative。 And second of all， it's equal to zero only if the distributions are， the same。 So that's at least a very nice property of something that we claim to measure the， difference。 the dis， somehow differences between distributions。 The Kolbak Live earns between。

 two distributions is zero if and only if it's the same distribution。 And that's what we're。 going to need in a few slides。 Okay。 So it's not， don't， don't compute， don't think that。 it's actually a distance metric。 It's not。 It's in fact not even symmetric。 So the Kolbak。 divergence between P and Q is not in general the same as the distance， the difference from， Q to P。

 All right。 So the proof I think will not go over it now， but it's worth walking， through。 There's only one inequality which comes from Jens' inequality。 Okay。 Okay。 Yeah。 Yeah。 Can you say it again？ You could take any distribution at all two distributions and。 if they differ in mean and variance or anything， then yeah， the KL divergence will be greater。

 than zero。 Okay。 All right。 So the E。M。 algorithm， we're going to look at it in terms of the。 general latent variable model。 So a general model in which you only observe X but not Z。 So we're going to have Z and X now， they can be more than just random variables。 They。 can be vectors of random variables， but we'll still do not them as X and Z。 Okay。 So we're。

 going to parameterize the model by some unknown parameter of theta。 So in their Gaussian。 motion model， theta would have been pi's and mu's and sigma's， but we'll just capture。 it all as theta to simplify notation a bit and to generalize it。 This is just to say that， I'm not。 this is not a Bayesian setting because we're conditioning on theta。 This is， this。

 is really just theta is just a parameter and we write it this way because it's easier to。 write this way than with the putting theta as a subscript on P or with a semicolon which。 would be more traditional ways of writing it。 All right。 So X is called our incomplete。 data set because it's what we observe but we imagine that there's also this Z out there。

 which is unobserved。 So X and Z together is called the complete data set。 X is called。 the incomplete data set。 So of course after the maximizing the likelihood of the incomplete。 data set X because that's what we observe。 All right。 So a deme of the data set and， all， right。 We want to find this marginal log likelihood。 So this is the likelihood of X， right because。

 we're summing out of our Z that gives us the P of X and this is for a single， sort of single。 element。 For the data set there should be an extra product in here。 All right。 So， so。 the key idea of the EM algorithm is that even though this is hard to maximize directly， if。 we have full data， if we only had to maximize the likelihood for the complete data X and， Z。

 if that's easy then the EM algorithm works well。 Okay。 So if we can maximize the complete。 log likelihood， then we're in good shape for EM algorithm even if the marginal log likelihood。 is difficult。 Now for Gaussian mixture model， are we in that situation where if you get， X and Z。 is it easy to find the maximum likelihood？ Again？ What's the， what would be the issue？ Okay。

 So the sigma is to marginalize out the Z。 But if we observe Z， we don't have to marginalize， it out。 Yeah。 So I think we mentioned this yesterday。 If you observe， if you know the。 cluster assignment of every point， it's really easy to get the maximum likelihood parameter。 settings， right？ We take all the points that are in cluster one， we find their mean， we。

 find their covariance。 That is the maximum likelihood estimate for that Gaussian distribution。 And so on for the other clusters。 So if we have the full data for Gaussian mixture model。 it's very easy to find the maximum likelihood estimates。 Yeah。 Okay。 So this is the case。 for Gaussian mixture model。 All right。 But of course we don't observe Z。 So the EM algorithm。

 is based on this really interesting idea， which is what if we had a probability distribution， on Z。 we came up with a probability distribution on Z。 And then we tried to maximize the expected。 complete log likelihood。 All right。 So we post， we come up with somehow， we'll come to how。 later on， but somehow we come up with a distribution on this unobserved variable Z， clock Q of， Z。

 All right。 And then we're looking for the expectation of the complete data log likelihood。 We can compute the expectation of the complete log likelihood with respect to this distribution， Q。 Finding the， okay， is that clear？ So that's what this， this expression is finding the。 expectation of the complete log likelihood。 Here's a complete log likelihood。 We don't。

 know Z's or something overall possible Z's and we're weighing it by the probability that。 Q gives to Z。 This is the expectation of complete log likelihood with respect to Q。 Questions on。 that？ Okay。 Sure。 How do we come up with a， how do you come up with Q？ Yes。 Any guesses？

 It should be distribution on Z that seems like a plausible distribution for Z given what。 we've observed about X。 There's a pretty natural one actually。 You could think of it。 All right。 You have another question？ This is over on the X's for one Z。 I only wrote one X and Z。 This。 is the only one。 Why did I only wrote one？ It's because we're collapsing all X one through。

 X and into X and Z one through Z and into Z。 That's what's happening here。 That's why， there's only。 it looks like one because it is one but it's an entire vector。 Right。 That's， the simplify。 Okay。 Any more？ Okay。 All right。 So EM also assumes that this maximization is， feasible。 All right。 So EM algorithm， we don't know exactly how to maximize the marginal likelihood。

 So what we're going to do instead is maximize， we're going to find a lower bound than the。 likelihood and maximize that instead。 So let's， let's examine this marginal likelihood。 This。 is the log likelihood。 Expand it out。 This is marginalizing out the joint。 Find that's， inequality。 Let's multiply and divide by this Q of Z。 So just write it down。 Q of Z。 We haven't。

 even said what it is yet。 Except for it's a distribution on Z。 So no change。 Right。 These， cancel。 But now notice that this is an expectation with respect to Q of Z because we're summing。 over all the S of Z with this probability of Z and some random expression。 So we have a。 log of an expectation。 So now we can use N's as inequality and swap it。 Right。 So which。

 way will the inequality go？ It's hard。 So the function is not convex。 So you have to switch。 it once and then so。 Okay。 Yes。 Greater than or equal to。 So we switch the expectation on。 the log and we get this expression and then we define this final expression to be LQ， theta。 We're going to be doing a lot of this LQ theta in the remaining slides。 This is。

 something called our variational lower bound on the marginal likelihood。 Okay。 So if in。 the future you ever study variational methods and you're like， I'm not sure what this is。 Come back to this slide because the calculations in this slide is essentially the core of variational。 methods。 E algorithm is kind of the simplest introduction to variational methods。 All right。

 So where we're headed here is the E algorithm。 Our goal is we're going to maximize LQ theta。 We're going to search over all probability distributions Q and all possible values of。 theta and we're just going to be some method to it but essentially we're just going over。 this whole space of distributions Q and parameters that is theta trying to get LQ of theta as。

 big as we can。 All right。 That's the objective of the M algorithm。 At the end when we've。 gotten LQ theta as large as we can， we're going to take whatever theta it is and we're going。 to say this is our estimate of theta。 That's going to be our best guess of the maximum likelihood。 estimate of theta。 All right。 So all of our effort is on finding a way to maximize L and。

 what we're going to show is that maximizing L does indeed help maximize this marginal likelihood。 All right。 And in fact if we find the global maximum of L that will also be the global。 maximum of the marginal likelihood。 So that's good。 That we can prove。 Yeah。 So are you maximizing LQ？ I mean easier than you don't。 Oh， well， and you'll see。 Okay。

 But I mean at the core is the fact that in here we have。 a joint we have the complete likelihood which is we know it to be easier than the marginal。 So we're not， notice we're not summing out over Z in the middle。 Okay。 Like here。 Okay。 So we're going to try to maximize LQ theta。 What we can do is take this expression and。

 we split it into two pieces by breaking the log of this ratio into the log of the numerator。 minus the log of the denominator。 And what you'll notice， which you should notice， is that。 the second term has no theta。 All right。 The first term has Q and theta。 Okay。 So that's， key。 So the other thing to notice is that this expression is the expected complete data log， like that。

 That's the thing that we assume is easy to maximize in the m algorithm。 All， right。 So if we maximize this expression over theta， we only have to look at this piece。 If we maximize it over Q， okay， both pieces are present。 All right。 So now we're going， to show。 we're going to look a little closer at how L lower bounds are marginal likelihood。 So first of all。

 I want you to think of these things。 I want you to think of LQ of theta。 for fixed Q for fixed probability distribution。 Think of it as a function of theta。 All right。 And so for every theta， this bound holds。 In fact， for any Q and every theta， this bound， holds。 So we can always write this down no matter what we plug in for Q and theta。 So here's， a picture。

 The red line is our， all right。 So x axis is theta。 We've， it's a cartoon version。 where our parameter space is just real。 So x axis is our theta。 The red plot is， that's。 the log marginal likelihood of our data for each theta， right？ For every theta， we have。 a different likelihood。 So if we knew the red line， the max， the maximum likelihood theta。

 is right here。 Can you say because it's under the highest point of the marginal likelihood？

 So we would like to find this point。 All right。 Yeah。 No。 Okay。 Now。 Yeah。 Well， red is the。 marginal likelihood。 Yes。 As I was going to say， this blue or purple line is L Q of theta。 for a fixed Q。 So Q is fixed and now it's a function of theta。 And this is the plot of。 our lower bound as a function of theta。 And yes， you're right。 The green is for a different。

 Q as a function of theta。 So these are two different lower bounds for different probability。 distributions Q。 So the method that we're aiming for here is we're going to kind of jiggle。 around Q。 And for every Q， we're going to find the maximum theta for that Q。 And then。 we're going to kind of go back and forth。 All right。 All right。 So I gave you this big。

 picture idea already。 We have this inequality for all theta and Q。 And we're going to， yes， I said。 we're going to search over theta for maximizing L and then take the corresponding。 theta as a estimate。 So this can very well be a local maximum。 This will typically， we。 hope to be a local maximum of our likelihood。 You can get much better with this type of， algorithm。

 So if you want to try to find the global， you may need to restart with different。 initial initialization points。 All right。 So the question left is， all right， how exactly。 are we going to go about changing Q and theta to try to find the maximum value of LQ theta？

 All right。 So we're going to use coordinate ascent， which we know about。 Coordinate ascent。 remember is where we first take one of our parameters and hold the other one fixed and。 maximize our function with respect to that parameter。 Then we fix that parameter and maximize。 respect to the other parameter。 And then are we done at that point？ No， we have to iterate。

 That's not enough to do one。 It's an iterative algorithm you keep repeating。 Okay。 That's。 called coordinate ascent。 All right。 So here is EM algorithm at the high level。 We start。 with an initial random point for theta。 We maximize over distributions， which is an interesting。 thing。 But we maximize over all probability distributions， LQ theta。 And then we fix that。

 Q star and maximize over theta and repeat。 So what we'll show is that the theta is give。 us monotonically increasing likelihood。 So that's interesting。 That's not necessarily。 obvious from here。 So as we get a new theta in every round， certainly the lower bound keeps。 increasing。 LQ star theta will keep increasing because all we do is keep stepping to a new， point。

 That's the maximum。 So we can only be increasing LQ theta。 What's interesting is。 that we also have increasing likelihood of theta。 So the probability of X given theta is also。 increasing。 Okay。 So here's an illustration of our algorithm。 We start at theta old。 Well。 let's let's start with a Q。 And now this okay， start with theta old apologies， start with。

 theta old。 Now we find a Q that gives the best lower bound at theta old。 Now would be， this。 So the best lower bound at a point is basically any lower bound that is equaled。 if we can find one that's equal to the actual function at that point， that would be the best。 We can have a lower bound at that's the best at this one point that's better than touching。

 the graph。 You might find another lower bound that is tangent to the graph and is better。 in other places。 But that's not the case here。 All right。 So we find our lower bound at theta， old。 Then we maximize this lower bound。 So we go from here and maximize the lower bound。 brings us to the peak of the purple curve。 And that gets us to new theta theta new。 Okay。

 Now we find a new Q that gives us a lower bound that's the best possible at this point。 And that would be this green curve which is tangent to the red line。 All right。 And repeat。 Okay。 All right。 We've got six minutes left。 So we have some time to make some progress， still。 So this is a very neat thing that happens if we examine this lower bound。 So here's a。

 definition of the lower bound。 Now we're going to split it in the log a little bit differently。 than we did before。 Okay。 So first we're going to split this joint distribution into conditional。 and marginal。 Right。 So that's just standard base rule or definition of conditional probability。 Now we're going to split it， split that log like this。 So we keep these two terms in the。

 first piece and move this to the second piece。 All right。 Now let's look at the second piece。 for our second。 Do you see how this simplifies？ Px given theta is independent of z。 Right。 So we can move that outside of the sum。 Now do you see how it simplifies？ Yeah。 The sum。 over z of Qz is one。 So this term becomes log of Px given theta。 What's log of Px given， theta？

 That's what we're trying to maximize。 That is exactly the marginal log likelihood。 the marginal log likelihood of x。 All right。 So that's interesting。 This is what we have。 the lower bound on。 And now it's somehow related to our lower bound by inequality。 So let's。 rearrange a bit。 So the marginal likelihood is exactly equal to the lower bound plus this。

 kau'd divergence piece。 So this is an explicit expression telling us the gap between a marginal。 likelihood and a lower bound on it。 It's exactly given by the kau'd divergence between Q and。 the marginal likelihood。 It's pretty interesting。 We're looking at it for a minute。 All right。 Okay。 All right。 So we can use this to figure out how to find the best Q。 Remember in our。

 maximized Q step？ We have maximized Q step and the maximized theta step。 This is going。 to help us with the maximized Q step。 So here's our lower bound again now with equality。 We。 want to maximize this over a Q。 The second expression has no Q in it。 So to maximize we。 can ignore this。 So now we're just maximizing this negative Q out divergence。 All right。 Overall。

 possible distribution is Q。 Okay。 So what's the answer to this maximization problem then？ Yeah？

 Yeah？ Yeah。 Right。 Yes。 That's right。 So the maximum， so first of all， let's remember。 that the kau'd divergence is greater than equal to zero and equals zero only if it's two。 pieces are equal。 The two distributions are equal。 All right。 This is a negative Q divergence。 which means it's always going to be negative or zero。 So if we can make this zero， that's。

 the maximum。 How can we choose Q to make this zero？ Very easy。 Take Q equal to P of Z given。 X and theta old。 This would have been what you could have guessed。 And it's pretty natural， right？

 What's our best guess for Z？ How about the conditional distribution of Z given what， we observed？ X。 It's very natural。 And here's the proof that that is the maximizer for fixed， theta old。 Okay。 So at that， so now we have this equality。 If we plug in Q star， then this， is inequality。 So is there something odd about this？ It's a lower bound。 And then I'm saying， it's equal。 Like。

 are we done？ What's the gap here？ So have we found， does this mean， we can？

 So it's just inequality at one particular theta at theta old。 It's not inequality everywhere。 It's equality at theta old。 This expression was for a fixed theta。 Okay。 This equality。 was for a fixed theta。 That's important。 All right。 Okay。 But we do have always an inequality。 for all theta。 So remember， L is always a lower bound for any Q and theta。 So we have。

 this inequality for all theta and an equality for the particular theta old。 And now this。 explains our picture。 Right？ So we have equality at theta old and inequality everywhere else。 Right？

 Or less than or equal to everywhere else。 When the lower bound touches what it's。 supposed to be a lower bound for， it's called a tight lower bound。 It's tight at this point。 All right？ Cool。 Any questions on this？ All right。 So now we have our， we could talk about。 our general EM algorithm。 We alternate between maximizing Q and maximizing theta。 The expectation。

 step was it's where we find this Q star， which is， we just set Q star equal to this conditional。 distribution。 And then we plug that Q star into our lower bound L。 So L Q star over theta。 And when we plug it in， this is an expectation。 Right？ Because it's an expectation with respect。 to Q star。 That's why it's called the expectation step。 So defining， finding this function right。

 as a function of theta， which is what we want to maximize。 It's an expectation， so kind。 of computing that function， that expectation， that's the expectation step。 All right。 So。 what's the next step？ We've maximized over Q。 That was the choice of Q star。 And now we。 maximize over theta。 Right。 With fixed Q star。 So we want to maximize L Q star theta with。

 fixed Q star。 And we just call that J theta。 So we just find the maximum of J theta over， theta。 That's the maximization step。 All right。 So there you have the EM algorithm。 And right， out of time。 But yeah。 That's a great question。 I think about that。 I want to say it's because， of the log。 but I don't want to even jump to that。 All right guys。 So I'll see you on， Wednesday。

 I'm flying back from somewhere on Wednesday。 So if anything weird happens with， the airplane。 I will try to post the piazza。 But I should be here。 Okay。

![](img/362c510b7786023274101d45cf5e21b5_3.png)

 [BLANK_AUDIO]。

![](img/362c510b7786023274101d45cf5e21b5_5.png)