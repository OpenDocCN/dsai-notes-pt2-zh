# P12：Lecture 12 - Fast Reinforcement Learning II - 大佬的迷弟的粉丝 - BV1Cc411h7QQ

 All right， we're going to go ahead and get started and then consistent with this theme。



![](img/dd3d90b32ca727decf2aefee2351f66e_1.png)

 of this section， we're going to be optimistic under uncertainty and hope that this will work。



![](img/dd3d90b32ca727decf2aefee2351f66e_3.png)

 but we will see。 Before we get into the content， I wanted to ask if anybody has any questions about logistics。

 or any other aspects of the general course。 Yeah。 Just want to double-check the people we're doing with default project are okay。

 either， not submitting or just submitting another thing from the milestone that says to the default。

 Yeah， sorry。 So the question was asking about whether or not people who are doing the default project。

 if they need to do anything in particular for the milestone， no， you don't。 Any other questions？

 Okay， so just as a reminder， where we are sort of in the class right now is last time。

 we started talking about bandits and regret and we'll do a brief recap of that today。

 And we're going to continue to talk about fast learning and we're going to go from。

 Bayesian bandits towards Markov decision processes today。 And then on Wednesday。

 we're going to talk some more about fast learning and then we're。

 going to try to talk about through fast learning and exploration。

 And just to remind us all about like why we're doing this， the idea was that if we want。

 to move reinforcement learning into real world applications， we need to think about carefully。

 taking the data that we have and how do we gather it and how do we best use it so that。

 we don't need to collect a lot of data in order for our agents to learn to make good， decisions。

 One of my original interests in this whole topic was to think sort of formally about。

 what does it mean for an agent to learn to make good decisions and what are the sort。

 of information theoretic limits of how much information would an agent need in order to。

 be able to make a provably optimal decision。 So we've been thinking about sort of a couple different main things here。

 We're talking about a couple of settings。 Last time we talked about bandits。

 Today we'll also talk about bandits and Markov decision processes。

 We're talking about frameworks which are ways for us to formally assess how good an， algorithm is。

 You know， these could be the framework of empirical success。

 We talked last time about the mathematical framework of regret and we'll talk today about。

 some other frameworks for evaluating in general how good a reinforcement learning algorithm， is。

 And then we're also talking about styles of approaches that tend to allow us to achieve。

 these different frameworks。 And last time what we started to do is to talk about optimism under uncertainty。

 So just a quick recap from bandits。 So bandit was basically a simplified version of Markov decision process where in the most。

 simple setting there's no state， there's a set of actions and now we're going to think。

 specifically about the fact that the reward is sort of some stochastic distribution。

 There's some unknown probability distribution over rewards。

 And each time step you get to select an action and see a reward。

 And then your goal is to select actions in a way that is going to optimize your rewards， over time。

 And the reason this was different than a supervised learning problem is that you only get to observe。

 the reward for the action that you sample。 So it's what's known as sensor data。

 You don't get to see what would have happened if you went to Harvard。

 So we get to see sensor data and we have to use that sensor data to make good decisions。

 And when we discussed here talking about regret what we mean in a formal mathematical。

 sense is that we were comparing the expected reward from the action we took to the expected。

 reward of the optimal action。 Now notice that all of these things are stochastic。

 So it doesn't have to have a particular parametric distribution。

 But imagine that we're thinking about Gaussians。 Let's say we had two Gaussians。

 So this is action two and this is action one。 Okay。 So here the mean of action one。

 So Q of A1 is greater than QA2。 So action one has the better expected reward。

 But notice that on any particular trial you might sometimes get it， you could imagine。

 getting your result where the actual reward you get from a suboptimal arm is better than。

 the expected reward of the optimal arm。 I just want to highlight that。

 So imagine that you'd sampled from action A2 and you got here。 This is a particular sample。

 So you could have a particular sample be better than the expected reward of the optimal arm。

 But because we're imagining doing this many， many times， we're again just looking at expectations。

 So we're saying on average， which is the best arm and on average， how much do we lose。

 from selecting a suboptimal arm？ And the goal was to minimize our total regret。

 which is equivalent to maximizing our cumulative， reward over time。

 So we then introduced this idea of optimism under uncertainty。

 And the idea was to estimate an upper confidence bound on the potential expected reward of each。

 of the arms。 So this was to say we want to be able to say for each of the arms， what do we think is。

 an upper bound of their expected value？ And then when we act。

 we're going to pick whichever arm has the highest upper confidence， bound。

 And this was going to lead to one of two outcomes。 So this could-- two things could happen。

 So either A t is equal to a star。 And in that case， what's our regret？ Zero。

 So if we select the optimal action， then we have a regret of zero。 So that's good。

 And then we have a regret of zero， like a per time step， or it's not。 And if it's not， on average。

 what happens to that upper confidence bound？ Yeah。 Yes。 Yes。 So what is it is correct？

 So we lower it。 So if we get-- if we select an arm， which is not optimal。

 then it means its real mean， is lower。 Then the upper confidence bound we're averaging。

 at least with high probability。 And so then in general， our U t of A t will decrease。

 So we're going to gain information about what the real mean is of that arm。 And we'll reduce it。

 And if we reduce it enough， over time we should find that the optimal arms upper confidence。

 bound is higher。 So I'll ask you to tell me about what might happen if we do lower bounds。

 But that's one of the reasons why upper bounds is really good。

 And I mentioned that these ideas have really been around for a long time， at least around。

 like 20-- 25 to 30 years。 So I think the first one was 1993， Kelvin， by Leslie Kelvin。 She's an MIT。

 Do you remember if it was her PhD thesis or it was just after that？

 But she talked about this idea of interval estimation， of estimating the potential rewards。

 She didn't do formal proofs of this being a good idea。 But she did it for Markov decision processes。

 And they found that it was a very good idea in terms of empirical performance。

 And then a lot of people went around and did the theoretical analysis and showed that。

 provably this is a good thing。 And I think it's interesting often about which area ends up being more advanced。

 whether， it's the empirical side or the theoretical side。 OK， so optimism under uncertainty。

 the bandit case just involves keeping track of the rewards， we've seen。

 And we saw that we could use things like huffing and equality to compute these upper confidence。

 bounds。 Because remember， each of our samples from the arms is IID。

 Because they're all coming from the same parametric distribution， which is unknown。

 And we're giving these samples。 So what we found last time is that if we use the upper confidence bound algorithm。

 I did， a proof on the board to show that with high probability we had logarithmic regret。

 Why was this important？ Because we looked at greedy algorithms and showed that they could have linear regret。

 And what is it linear in？ So this is in the number of time steps。 Number of time steps we act。

 So why is linear regret bad？ Well， if it's linear。

 it means that essentially you could be making the worst decision on every， single time point。

 And that's pretty bad。 So we'd like to have things that are growing slower。

 which means that our algorithm is， essentially learning to make good decisions。

 Now notice that in this case， this is a little bit different statement of a result than what。

 we saw before。 It's related。 This involves the gaps。 This is the gaps。

 Delta A is equal to Q of A star minus Q of A。 It's how much worse it is to take a particular。

 action than to take the optimal action。 And this is related to the bound from last time。

 Last time we proved a bound that was independent of the gaps。

 So it didn't matter what the gaps were in the problem。 This is a bound that depends on the gaps。

 Now of course you don't know what the gaps are in practice。 If you did know the gaps。

 then you would know the optimal arm to prove。 But the nice thing about this is that it's always important to know whether or not this。

 sort of knowledge appears in the analysis or in the algorithm。

 This is saying you don't need to know what the gaps are， but if you use this algorithm。

 how your regret grows depends on a property of the domain。

 You don't have to know the property of that domain， but that's what your regret will depend， on。

 And so this is saying that for upper confidence bounds， if you have different sizes of gaps。

 you're going to get different regrets。 But your algorithm is just going to proceed by following upper confidence bounds。

 It doesn't need to know about these gaps， but you're going to get better or worse performance。

 depending on what the gaps are。 And in general we'd really like these。

 We'd like our algorithms to be able to adapt to the problem so that this is known as a。

 problem dependent bound。 Right here。 And you would like those。

 You'd like to have algorithms that are agnostic that sort of provide problem dependent。

 bounds so they work better if the problem is easier。 All right。 So let's go to our toy example。

 which we were talking about as a way to see how these different， algorithms work。

 And we were looking at fake ways to treat broken toes， and where we were looking at surgery。

 buddy taping or doing nothing。 And we were imagining that we had a Bernoulli variable that determined whether or not these。

 treatments worked。 So surgery on in expectation was the most effective thing with 0。95 success。

 Buddy taping was 0。9 and doing nothing was 0。1。 So how would something like upper confidence bound algorithms work？

 Well， the beginning won't have any data， so let's sample all the arms once。

 That's going to involve sampling from a Bernoulli distribution。 So in this case。

 let's imagine that we got a1， a2， and a3 here。 And note that this is our empirical estimate where we just average over all the all the。

 rewards we've seen from a particular arm。 So we pulled each arm once。

 which is the aim is taking each action once。 We got 1， 1， 0。

 And now what we have to do is compute the upper confidence bounds for each of those arms before。

 we know what to do next。 Okay， so in this case， we're going to define upper confidence bounds by being the empirical。

 average plus the square root of 2 log t。 t is the number of times we pulled arms and nt of a is the number of times we sampled a。

 particular arm。 This is total arm pulls。 This is particular arm。 Okay。

 so what is that going to be in this case？ Let's just define it for each of them。

 So ucb of a1 is going to be equal to 1 because that's what we've got so far plus square root。

 2 log of 3 because we've pulled 3 arms so far divided by 1。

 ucb of a2 is going to be the same because we've also pulled that arm once and it got。

 the same outcome。 And then ucb of a3 is going to be different because its current reward is。

 or current expected， value is 0 so it's just going to be equal to 2 log 3 by 1。

 That's how we could instantiate each of the bounds and now we've defined the upper confidence。

 bounds for each of the arms。 So in this case after we've done that we're going to pull one of these arms。

 Let's say that we break ties randomly so the upper confidence bound of a1 and a2 is identical。

 so with 50% probability we select 1， with 50% probability we can select the other。

 And let's just compare that for a second。 So if we're using ucb I said that。

 so I'll just redefine this here so people can remember， is equal to ucb of a2。 This is。

 ucb stands for upper confidence bound。 It's equal to 1 plus square root 2 log 3 divided by 1 and ucb of a3 is equal to square root。

 2 log 3 divided by 1。 Okay so why don't we just take a second and define what would be the probability of。

 selecting each arm if you're using e greedy with epsilon equal 0。1 and what about if you're。

 using ucb。 It's always feel free to talk to anybody nearby。 Alright so let's vote。

 I'm going to ask you to vote if two arms have nonzero probability or three arms have nonzero。

 probability。 So if you're using ucb do two arms have nonzero probability？

 So three arms have nonzero probability。 Somebody who thought with ucb you only have two arms with nonzero probability when I explain。

 why。 Yeah。 Because since you're picking the maximum action and you're only going to pick a1 or a2。

 That's right。 Yeah so if we're picking the maximum action here we're only going to pick action a1 or。

 a2 we have zero probability on the third arm。 Okay let's do a quick vote for e greedy。

 For e greedy do we have nonzero probability on two arms？ On three arms？ That's right。

 What's the probability of selecting a3？ Okay。 I'm 0。1。 And we also add？ Yeah。 0。03。 Yes or 0。33？

 Yes。 Okay。 Okay。 So in the point one in this case just remember we normally define that by uniformly splitting。

 Yeah。 So we're going to just have 0。1 divided by the number of arms。 So here why do I bring this up？

 So I bring this up to indicate that while ucb is still splitting it's attention among。

 all the arms that look good it's not putting any weight right now on the arms that it doesn't。

 think could be good which in this case is arm three。

 Whereas an e greedy approach is going to put uniform probability across anything it doesn't。

 think is best。 So this is one of the insights for why these algorithms might be better is because there。

 be more strategic in how they're weighing what arms to pull compared to what an epsilon。

 greedy which is just doing uniform。 Okay。 So let's look at sort of what the regret would be in this case。

 So the actions we pulled is a 1a 2a 3a 1a 2。 So why would we pull a 2 again？

 Let's just go through that briefly。 So let's say， so first let's say we're going to pull a 1。

 So imagine that's which one we picked。 Okay。 So we pulled a 1。

 So let me just go through one more step of what the upper confidence bounds would be in， this case。

 So let's say we pull a 1。 Okay。 So now we need to redefine the upper confidence bounds。

 We actually need to redefine them for all the arms because in the denominator of that。

 upper confidence bound it depends on t which is the total number of pools or the total。

 number of pools so far if we're using that form。 So now we're going to have the UCB。

 Let's say we pulled action a 1 and let's say it got a 1。 Okay。

 So UCB of a 1 is going to have the same mean which is 1 plus square root 2 log 4 because。

 we've now pulled things four times。 But now we pulled this arm twice。

 So we're going to divide this by 2。 UCB of a 2 is going to have the mean as before because we didn't pull it。

 And then it's going to also have the 2 log 4 but we've only pulled it once。

 And UCB of a 3 is still has the mean of 0 and it's also going to have 2 log 4 divided， by 1。 Okay。

 So in this case what we're going to find is that we sort of are going to have this trading， off。

 We still have the same empirical mean for a 1 and a 2 but now we haven't pulled a 2 as。

 much as a 1 so we're going to flip and we're going to pick a 2 now。

 So that's why if we imagine that we got well actually as a quick check your understanding。

 this result would happen whether we picked one whether we got a 1 or 0 for a 1 when we。

 last pulled it。 So that's a good thing to check is an interesting but even if we got a 1 for a 1 we'd still select。

 a 2 on the next round because the upper confidence bound of it would drop even if its mean was。

 the same。 So if we look at this then so we're going to compare it to what would be the optimal。

 action if we take a map the whole time which is a 1。 So what is our regret？

 Our regret is going to be 0 and then here it's going to be 0。05 which is just equal to， 0。

95 minus 0。9。 Here it's going to be 0。85 because it's 0。95 minus 0。1。

 Here it's going to be 0 and here it is going to be 0。05 again。 So that's how we sum up the regret。

 The regret。 Of course we don't actually know this。

 I mean we can know this if we're doing this in a simulated world but we can't know this。

 in reality because again if we actually knew it in reality then we wouldn't have to be， doing this。

 We would know the optimal arm。 We have any other questions about how UCB is working？

 Now just I guess one of the quick note here which is these upper confidence bounds are。

 high probability bounds。 So they can fail but it is possible that sometimes the upper confidence bound is lower。

 than the true mean。 So that's why when we did the proof last time we had to talk about these different。

 what happens if the upper confidence bounds hold and there we did a high probability， bound。

 Okay so an alternative would be to always select the arm with the highest lower bound。

 So what we're doing right now is just selecting the arm with the highest upper bound but you。

 could select the arm with the best lower bound。 So what might that look like？

 Let's imagine that we have two arms A1 and A2 and this is our estimate of the Q of A。

 Okay so let's imagine that these are our uncertainty bounds。

 So in this case A1 has a higher upper bound but A2 has a higher lower bound。

 So why don't we take a minute or two and think about why this could lead to linear regret。

 I think a two arm case is the easiest one to think about for this。

 Feel free to talk to anybody around you if you want a brainstorm。

 This is actually an important reason why it's good to be optimistic。

 At least in reinforcement learning。 Okay。 Okay。 [ Silence ]， >> So I talked to at least one person。

 the audience that need the right answer， which， is in this case， if you select A2。

 you're going to continue to get towards the mean。 The real mean is above the lower bound of A1。

 And so you're going to kind of get confirmation bias。

 Like A2 is going to continue to look good and you're never going to select A1。

 So we're never going to get information that allows us to disprove our hypothesis and we're。

 never going to learn what the true optimal mean is。 So that's why you can get linear regret。

 So one thing I just want to highlight is that upper confidence bounds are one nice way to。

 do optimism and they can change over time in terms of upper bound。

 But a simpler thing you might imagine doing is just to initialize things really to a high， value。

 So pretend， for example， that you already observed one pool of each of the arms and that it was。

 really， really good。 So just initialize all your values like a million or something like that。

 And then you just kind of average in that weird fake pool when you're doing your empirical， average。

 So you can imagine you pretend you pull each of your arms once， you got a million， you got。

 a trillion。 And then after that you just average in all your empirical rewards。

 So this actually can work fairly well in a lot of cases。

 The challenge is to figure out how optimistic you need to be for that fake pool。

 So just in terms of sort of comparing that approach to other approaches， recall that greedy。

 gives you linear total regret。 Constant e greedy can also give you linear total regret。

 If you decay e greedy， you can get actually sublinear regret if you use the right schedule。

 for decaying epsilon。 But that generally requires knowledge of the gaps which are unknown。

 So this is sort of generally impossible to actually achieve。 But if in principle， you know。

 if you sort of had an oracle， you could figure out how， to decay things。

 If you do optimistic initialization， if you initialize the values sufficiently optimistically。

 then you can achieve sublinear regret。 But again， it can be pretty subtle to figure out exactly how optimistic those need to be。

 And I'll talk later about an example where in that Markov decision process case， they。

 have to be much more optimistic than you might think they would need to be in order for this。

 to work well。 All right， so we're going to now start to talk about Bayesian bandits and Bayesian regret。

 And so far we've sort of made very little assumptions about the reward distribution。

 We've assumed that the rewards might be bounded。 So we typically assume that the rewards are going to lie in sort of 0 to 1。

 Or 0 to some， you know， 0 to R max or something like that， that we have bounded rewards that。

 you can't have infinite rewards as nice as it would be。

 But we haven't been making strong parametric assumptions over the distribution of rewards。

 Houghting requires the rewards to be bounded， but it doesn't assume， for example， if they're。

 Gaussian or Bernoulli or things like that。 So an alternative approach is to assume that we actually do have information on the parametric。

 distribution of the rewards and exploit that。 So we're going to talk about Bayesian bandits now。

 where we sort of explicitly compute a， posterior of the rewards given the history。

 So given the previous actions we， or arms we've pulled and the rewards we've observed。

 And given that poster， we can use that posteria to guide exploration。 And of course。

 if your prior knowledge is accurate， that might help you。

 There's sort of somewhat of a debate between frequentist and Bayesian views of the world。

 We're not going to get really too much into that in this class。

 But the idea is that it's also going to be a nice way to put in prior knowledge。

 If you have prior knowledge about the particular reward structure of your environment， you can。

 put this in and it can help in terms of exploration。 Okay， so in the Bayesian view now。

 we're just going to do sort of a quick review of Bayesian， inference。 A number of you guys。

 this is probably a refresher for some people that might be new。

 We're going to assume that we have a prior over the unknown parameters。 So in our case。

 the unknown parameters are going to be the parameters that determine。

 the reward probability distribution for each of the arms。

 And the idea is that given sort of observations or data about that parameter， like observing。

 rewards when you pull an arm， we're going to update our uncertainty over the unknown。

 parameters using Bayes' rule。 So let's look at that as a specific example。 So for example。

 imagine that the reward of an arm i is a probability distribution that。

 depends on some unknown parameter phi i。 So this is unknown。

 I'm going to have some initial prior over phi i， which is the probability of phi i。

 So this is before we pull that arm at all， this is sort of our uncertainty over that， parameter。

 And then we pull arm i and we observe a particular reward ri1。

 And then we can use this to update our estimate of the distribution over the parameters that。

 determine our reward probability distribution for this arm。 So we do that using Bayes' rule。

 And we say that the posterior probability of our parameters phi i， given that we've observed。

 that reward， is equal to our prior probability over those times， which are of our data evidence。

 or likelihood， divided by the probability observing that reward regardless of what your。

 parameters were。 And so this is Bayes' rule。 And the challenge or the important thing here is how do we compute all of those things？

 So that tells us how to update our posterior over the parameters。

 And the question is how do we do this？ So in general。

 doing this sort of updating can be very tricky to do， because if you don't。

 have any structure on the sort of parametric form of the prior and the data likelihood。

 so this again is the prior。 And this is the data likelihood。 If you have no structure on this。

 one of them is a deep neural network， another one of them。

 is some random other parametric distribution， then it may be impossible to have a close。

 form representation for what the posterior is。 So in general， this can be really hard。

 But it turns out that there's particular forms of the prior and the data likelihood that。

 mean that we can do this analytically。 So who here is familiar with conjugates？ Okay， some people。

 but not everybody。 So these are really cool conjugates， exponential families， for example。

 are conjugate distributions。 The idea is that if the parametric representation of the prior and the posterior is the same。

 we call the prior and the model conjugate。 So what would that mean？ So for example。

 what if this is like a Gaussian？ If this is a Gaussian and this is a Gaussian。

 then we would say that this and this are conjugate。

 whatever thing we're using for the data likelihood。

 It essentially means that we can do this posterior updating analytically or in close form， which。

 is really nice。 So we call it， this means that we sort of keep things in the same parametric family as。

 we're getting more evidence about these hidden parameters。 I'll give an example of this in a second。

 But there are a number of different parametric families which have conjugate priors， which。

 means that if you have an initial uncertainty over the parameter in that distribution， then。

 if you observe some data， you can update it in your still and the same parametric family。

 So if they're super elegant， come up in statistics a lot。 All right。

 so here's a particular example that's relevant to us， which is Bernoulli's。

 So let's think about a bandit problem where the reward of an arm is just a binary outcome。

 And that this is sampled from a Bernoulli with a parameter theta。 So this comes up a lot。

 This is things like advertisement click-through rates， patient treatment succeeds or fails。

 et cetera。 So in many， many cases， when we pull an arm or we take an action， we're going to get a。

 binary reward either zero or one。 So it turns out that the beta distribution， beta alpha beta。

 is conjugate for the Bernoulli， distribution。 So that means we can write down our prior over the Bernoulli parameter given alpha and。

 beta as follows。 It's theta to the alpha minus one。

 one minus theta to the beta minus one times a ratio of， the gammas。

 Gammas are related to the factorial distribution。 So all of this can be computed analytically。

 And one nice way， I think， to think about this is that we can think of alpha and beta。

 as essentially being the result of prior pools of the arm。

 We can use them also to encode sort of prior information about this。

 And I'll show you shortly an example of how these get updated。

 But what happens is that if you assume that the prior over theta is a beta， so if it looks。

 like this， this is the prior， then if you observe a reward that's in zero or one， because。

 that's what our reward distribution rewards are whenever we sample one， then the updated。

 posterior over theta is a really nice form。 It's just the same beta distribution with either one added to the alpha or one added to。

 the beta。 So essentially， if you observe r equal one， then you get beta of alpha plus one and beta。

 If you observe r equals zero， you instead add it to the beta term。

 So you can think of alpha as mean all the number of times that you saw a reward of one。

 and beta is just all the number of times you saw a reward of zero。

 Can you explain how the fact that beta was Bernoulli factored into this description and。

 why this isn't just like a description of a beta distribution， the main equation。

 I think why it was important to first say that beta is Bernoulli。

 I'm bringing up that great question。 So the reason I bring this up is that beta is a conjugate prior for the Bernoulli。

 So the idea is in this case， if we're thinking about an arm， which has binary outcomes， then。

 we can think of the average of that arm as being represented by a Bernoulli parameter。

 So let's say like 0。7 percent， you know， on average 0。7 times， we get a reward of one， and 0。3。

 we get a reward of zero。 So the mean of that arm is 0。7。

 So we're thinking about an arm which has a Bernoulli parameter that describes its mean。

 So we're thinking of like， you know， an arm with mean equal to theta。

 That's what the mean is for a Bernoulli distribution。

 And what I'm saying is that we want to now be Bayesian about that and we want to think。

 about what is the probability of that parameter given the data we've seen so far。

 And if we want to be able to update our estimate over theta， not over rewards over theta， then。

 we're going to write down our distribution over what theta's might be possible as a beta。

 distribution。 And then we're going to update that as we see evidence。

 And I'll show you shortly like what these betas look like。

 So we can think of sort of what is the probability distribution over theta's as we get more evidence。

 So for example， you might imagine if you see reward， which is 1， 1， 1， 1， 1， 1， 1， 1， then。

 your beta distribution is going to indicate that a theta， which is really high is more likely。

 If you get 0， 0， 0， 0， 0， 0， you're in your beta is going to have a different shifted posterior。

 which is going to say probably your theta is really low close to 0。 Cool。

 So we'll see an example of this in just a second。 So the nice thing in this case is that for Bernoulli's。

 which is a really common distribution， that we often want to think about。

 we can write down a prior over that parameter and， we can update analytically just using the counts。

 So we just keep track of how many times we've seen a 1 or how many times we have a 0 and。

 we use that to update our posterior。 Okay， so how do we evaluate performance now we're in this Bayesian setting？

 So in the frequent test regret， we didn't think about having distributions over parameters。

 We just thought of there being some parameter， like， you know， what's the mean of that arm。

 And then we defined our regret with respect to the best arm。

 Bayesian regret assumes there's this prior over parameters。 And so Bayesian regret says。

 what is my expected regret by thinking about what are the possible。

 parameters given my prior and then looking at the expected performance if I got a particular， theta。

 So it's a little bit different way of looking at the world。 Again。

 we're not going to really get into the philosophical aspects of this， but Bayesian。

 regret is saying like， well， we're not sure， you know， what the distributions are of these。

 arms and there'll be different worlds in which they'll take on different values and how will。

 do you do in those different worlds on average。 All right。

 so how do we try to make good decisions for Bayesian bandits？

 So one thing you might imagine is let's say we have a parametric distribution over the。

 rewards for each of the arms。 We could certainly have that in the Bayesian case。

 The idea of probability matching， which I think has been around since around 1929， it's。

 been around a long time， like almost 100 years， is that we want to select an action A according。

 to the probability that it's optimal。 So it seems quite intuitive for the appealing。

 Like we want to select arms that might be optimal more。

 We want to select arms that probably aren't likely to be optimal less。

 And it is optimistic in the face of uncertainty because in general， uncertain actions have。

 a higher probability of being the best。 So uncertain actions mean we don't know very much about what their rewards are。

 The problem is this sounds really nice。 We'd like to sort of select arms according to the probability that they're optimal。

 but， it's completely unclear how to compute that。 So this expression here is saying we want to sample an arm given a history。

 So the history here is prior pools and reward outcomes。

 This is the history of the arms we've pulled and whether we've got what sort of rewards。

 we've gotten。 And then we want to pull an arm according to the probability that that arm is better。

 than all the other arms。 And that history。 So that's quite intellectually appealing。

 but it's not at all clear how we would compute， that quantity。

 And so it's sort of somewhat magical that a very simple approach turns out to implement。

 probability matching。 And the idea is called Thompson sampling。 And again。

 this came out roughly in the 1920s。 And one of the really interesting aspects of it is it sort of disappeared for a long。

 time in terms of bandits， certainly in the AI community and CS community。

 And then around eight years ago， eight to nine years ago， people sort of got re interested。

 in understanding these。 In part due to a paper that a hog of mine published。

 which you'll see results of shortly， which indicated that empirically it can be really good。 Okay。

 so how does Thompson sampling work？ We're going to initialize a prior for each of the arms。

 Often we'd like this to be conjugate。 It doesn't have to be。 It's nice if it's conjugate。

 But we're going to have a probability over each of the arms。

 Now remember that this is sort of a probability over the parameters determining a distribution。

 So it could be if we have Bernoulli arms， it could be the probability of theta。

 I for I equals one to the number of arms。 So for example。

 this could be a beta distribution of one one。 It could say the probability that my ith arm has a Bernoulli parameter of theta is equal。

 to sampling from a beta one one。 Okay， so we're going to pick a particular parametric family to represent our prior distribution。

 of the reward distributions for each of the arms。 And then what we do is for each round。

 we first sample a reward distribution from that， posterior。 Again。

 we'll go through a concrete example of this in a second。

 But this is like picking a particular theta。 So it's like saying。

 I'm assuming that my mean for this arm or my Bernoulli parameter， for this arm is 0。7。

 picking a particular value for that parameter。 And then once you have that。

 you can compute the action value function by just taking the， mean of whatever that is。

 So notice that if theta， let's say we sample for arm one， let's say we sample 0。9， we just。

 happen to sample that arm one has a theta parameter 0。9。 Well。

 the Q for arm one is then going to be the expected value of a Bernoulli parameter， theta one。

 which is just 0。9， because the expected value for a Bernoulli variable is， just p， just the theta。

 So we're going to compute the action value function for each of these。 In the case of a Gaussian。

 it would just be its mean， for example。 So you just compute what the mean expected reward is for each of the arms under the particular。

 reward distribution we sampled。 And then you take whichever action looks best for those sampled parameters。

 So that's this。 And then we take that action and we observe our reward and then we update our posterior。

 using base law。 So we're just going to take our priors over the parameters。

 We're going to sample a particular set of parameters。 These are probably totally wrong。

 This is just us making up what the actual parameters are for each of the arms。

 And we act as if that world is optimal， we get some data， we repeat。

 So it's a fairly simple thing to do。 We of course have to see how we can do this sampling。

 And I'll show you an example with Bernoulli's in a second。

 But nowhere here are we trying to explicitly compute like what is the posterior probability。

 that this arm is optimal。 We're just sampling some and then we're going to be sort of greedy with respect to those。

 samples。 Okay。 So Tom's in sampling turns out to implement probability matching。

 which is super cool。 And for some of the intuition of this， so this is what probability matching is。

 Probability matching is that we want to select an action given the history according to the。

 probability that it's optimal， according to the probability that arm really is the best， arm。

 And we can think of that as being equivalent to the expected value of picking a reward given。

 the H and the arm is equal to the argmax of QA given that history。

 And that's what Thompson sampling is computing。 Okay。

 So let's see how this actually looks for the Rokentow example because I think that'll make。

 it a lot more concrete。 So again， in this case， remember that we have three different arms and they each are looking。

 at the success or failure of doing this treatment to try to make people's Bokentow better。

 And surgery is a Bernoulli parameter with 。95。 Taping is 。9 and nothing is 。1。

 So if we want to then run Thompson sampling in this environment， remember it doesn't know。

 what those actual parameters are， we're going to choose a beta 1 1 prior over the parameters。

 So that means that we're going to say the probability of a 1 is equal to a beta。 Okay。

 So what does a beta 1 1 look like？ It looks like a uniform distribution。 So this is 0 to 1。

 This is theta。 This is probability of theta。 So what this says is that if someone gives you a beta 1 1 distribution。

 it says you're， going to select a Bernoulli parameter from that。 I have no idea what its value is。

 It could be 0， it could be 1， it could be 。5。 It's sort of an uninformative prior。 Okay。

 so it says that initially I have no idea what these theta parameters might be for， each of the arms。

 So I'm just going to pretend it's， I'm going to start off in sumits flat。 I have no information。

 So this is what a beta 1 1 looks like。 But what's going to happen in Thompson sampling？

 So this is our distribution over thetas。 And what Thompson sampling is going to do is it's going to sample our parameter from。

 that distribution。 So in this case， it's just a uniform distribution between 0 and 1。

 So we're just going to select some value between 0 and 1。 So in this case， imagine what we got is。

 I'll just leave this up for a second so people， can see， 0。3， 0。5 and 0。6。

 There's no reason that arm 3 would be higher or lower than arm 1 or arm 2 or arm 3。 In reality。

 arm 1 is best， but we have no information about that so far。 And we have no reward so far。

 All we've done is we've just said， I have a uniform distribution over what my theta parameter。

 might be， I'm going to sample from it。 And so in this case。

 it's like sampling and you got this value once。 You got this value once and you got this value once。

 All right， we just sampled from that distribution， that uniform distribution。

 And these are the parameters we picked。 And now we're going to pretend that's real。

 So we're going to say， I'm going to pretend that my theta for surgery is 0。3， my theta。

 for taping is 0。5 and my theta for nothing is 0。6。 So if that was the real world we lived in。

 what arm would we select？ Third arm。 Third arm， exactly。 So in this world。

 the third arm really is best because that's a theta of 0。6。 So we're going to select theta is 0。6。

 Yeah。 We're using uninformative priors because I could have very well used a beta 2， 2 or 5， 5。

 So is that a significant advantage of using this for Thompson something？ Yeah， so。

 We makes a really good point。 She said we're currently using uninformative prior。

 Is it better or worse to do that compared to using an informative prior？

 So you could have had like a beta of like three four， etc。

 A beta of three four or anything that's not one one is going to give you is going to bias。

 to your distribution。 It's going to change the shape of how you sample things。

 If you have actually good information that can be really useful because it's essentially。

 like having fake pools and it can guide sort of your initial samples。

 The downside is that if that isn't correct， you can be misled for a while。

 So we often talk about like how robust are we to misspecified priors or to wrong priors。

 And so using an uninformative prior means that you're not getting a lot of benefit from。

 prior knowledge， but you're also not going to get a disadvantage。 Okay， so in this case。

 we're going to select the arm arm three because that's just the。

 arm that has the best expected mean under the samples that we did。 Okay。

 but arm three is actually not very good and we know that because arm three actually。

 only has a reward of point one。 And so when we sample it and we get the patient's outcome。

 we're going to get a zero in this， particular case because the real arm three is point one。

 So if you sample from a bruin really with point one， most of the time we're going to， get a zero。

 So now what we have to do is we have to update our posterior over arm three。 Okay。

 we have to up to what sort of what our probability of theta of arm three is given。

 that the reward was equal to zero。 So what we talked about is that the beta is a conjugate prior for the Bernoulli。

 And if we observe a one， we're going to update the first parameter， also we're going to update。

 the second parameter。 So we just saw zero， so our new beta is one two because we just saw zero。

 So we update。 So this is our new parameter。 So that's our new posterior over the arm three and it looks like this。

 So this is still theta。 It always has to be between zero and one because this is a bruin really parameter and this is。

 what the probability looks like now。 So noticed it shifted。 So it used to be flat and now it says。

 well， no， I just observed that we got a reward of， zero。

 And now I have a higher probability that theta is small。 So if I was going to sample from this。

 it is more likely I would get a lower value compared， to a higher value unlike before。

 So this is our new posterior。 And what does the posterior look like for the other arm？

 So this is for theta three。 And for the other two。

 they still look uniform because they're still a beta one one。 So for beta one one。

 this is for the other arms， theta one， theta two， this is probability， of theta。

 So the two are still uniform because we haven't pooled them yet。 We don't have any outcomes。

 So they still look like uniform distributions， but the probability over theta three looks。

 key towards zero。 So now in Thompson sampling， we again are just going to sample a value from each of these。

 different ones， each of those three distributions。 And now imagine we get 0。7， 0。5， and 0。3。 Yeah。

 Should I say p of q of a three， I'm curious why。 Because I'm going to say a three is one。 Yeah。

 Well done。 There's a couple of errors there。 Yep。 Thanks for catching that。 Any other questions？

 Okay。 Okay， so we updated our posterior over our arm three。

 Our posterior over arm one and arm two is the same as the prior because we didn't pull， them。 Okay。

 So now we're going to sample from those three distributions。

 What Thompson sampling would say is now given our posterior over all of the arms， let's select。

 an actual parameter for each of the arm。 And this time we're going to get 0。7， 0。5， and 0。3。

 So which arm were we going to select this time？ Arm one。 Arm one。

 So now the max is going to be arm one。 Okay。 So now we're going to have a posterior that looks like beta two one because we update our。

 beta。 And remember we can just think of this as being the number of r equals ones plus one。

 because we started with the beta one one and this is the number of r equals zeros plus， one。

 So now our new posterior for this one makes it look like this is so this is theta one。

 It's one zero probability of theta one。 Okay。 So now as we would expect we saw that arm one had a good outcome and so know our probability。

 that that Bernoulli parameter is higher than 0。5 is going up because we saw some positive， results。

 Okay。 So now we have， so what does our new distributions look like？ We have a beta two one。

 We have a beta one one because we haven't selected arm two yet and then we have a beta， one two。

 All right。 So what's going to happen next？ Louis again are going to sample a Bernoulli parameter。

 So let's imagine that we got 0。71， 0。65 and 0。1。 And so that means we're again going to select arm one and we again observe a one。

 Surgery is pretty effective。 And now our posterior is three one。 So now this again is 0 to one。

 This is our probability of theta one。 Okay。 So now it's looking even more peaked。

 So what's your guess of what's the next arm we're likely to sample？

 So remember the three distributions that we have right now is for arm two looks like this。

 For arm three looks like this。 So this is the probability of that arm。 So it's theta a two。

 theta a three， zero one， zero one。 So who thinks that theta one is again going to be sampled and look better than everything。

 else？ That's right。 Because it's got to have it has a posterior。

 it's Bernoulli parameter that is getting closer， like a sharp but more and more steep towards one。

 Theta two we've still never taken action a two but it just has a uniform。

 So it's very unlikely that we're going to sample a value for it that is better than。

 the value we sampled for arm one。 So again in this case we can imagine sampling again we get 0。75。

 0。45， 0。4。 We select action a one again and now we have a beta of four one and it's looking even more。

 sharp up。 So notice this is quite different than what UCV was doing。

 UCV was splitting its time between a one and two at the beginning because that we both。

 rely on their empirical means but then a two would have been taking less times。

 In this case we still haven't taken action a two yet and it may be hard for us to pull。

 it for a while。 Now that's not actually bad in this case because theta one is actually the best arm but there。

 can be some trade-offs。 Yes。 This is the only way we can update the beta distributions。

 Is there a rule that we should increment by one or because we have different kinds of， rewards。

 Here rewards are zero and one day。 So we have different kinds of rewards。

 How would we update our beta distributions？ Great question。 So here we've got binary rewards。

 How would we do this if things were not binary？ In that case we wouldn't use a beta in a Bernoulli。

 So if you didn't have for binary rewards Bernoulli is a really nice choice and beta is conjugate。

 If you have real valued rewards you might use a Gaussian and then you'd have a Gaussian。

 prior depending on whether you know your theta or not。

 And in general like for multi-nomials you can use Dirichlet distributions。

 It depends on what your reward distribution looks like and then you want to find a conjugate。

 prior for that distribution。 So there's a lot of different families of parametric distributions for which you can。

 do this sort of updating。 Yeah。 In the other things we were talking about being optimistic。 Yes。

 And here we used like a uniform distribution for initialization。

 Is it better to use something more optimistic？ That is a great question。

 So this question was so we talked before about the benefits of optimism。

 Here we just used a uniform prior and wouldn't we better to use one that is optimistic。

 It depends on the empirically。 So what is this doing？

 I'm just going to hold on that question for a second so we can look at sort of what these。

 look like。 So if we did optimism we sampled all the actions first and then we sort of got this interleaving。

 of a1 or a2。 In Thompson sampling we took a3 and then we took a1， a1， a1， a1， a1 and a1， a1， a1， a1。

 a1 is optimal in this case。 So by using a uniform prior here essentially as soon as you see something that looks pretty。

 good like better than 。5 you're going to tend to often sample it a lot more。

 So you're sort of exploiting faster to some extent。 You can put priors in there。

 The question is often like how much to put that in there and if it actually helps。

 So one of the cool things with Thompson sampling is it turns out in terms of sort of the Bayesian。

 regret bounds there as good as the upper confidence bounds。

 But empirically often exploiting faster is helpful。

 So you could put optimism in there but it might actually hurt performance because it's。

 going to force you to take。 Like in this case arm one actually is optimal。

 Now you could have imagined maybe we're just lucky there and instead we've got an a2。

 In that case you'd want something to help you eventually take a1。

 Now we will still take a2 likely at some point because there still will be a probability under。

 that uniform prior that you'll sample like 。999 and then you'll take a2。

 So you can still be sure to start taking other actions even using these uniform priors。

 But it's a really good question about sort of weird what information to put in there。 And my game。

 This is obvious that like you have like a pizza it becomes very hard for a different action。

 to catch up。 So that sense that chances at the start is more like important than。

 So maybe of one arm is really good then it becomes really hard for the other arm to catch， up。

 So in this case that's true because theta 1 really does have 。95。

 Just imagine a slightly different case where this was like 。7 or something like that。

 Then in that case over time it would be likely that your beta distribution is going to converge。

 to around the real distribution of the parameter。 So if you keep sampling theta 1 forever eventually you know it's going to sort of collapse towards。

 what the true value is。 And so if the true value isn't very close to 1 there will be some probability you'll sample。

 So imagine this versus a uniform that's not very close to 1 at some point there is a。

 nonzero probability that you'd sample something that's higher。

 So the beginning matters but you can outweigh it over time。

 Just like what we can with the empirical distributions。

 Okay so if we look at this and we sort of look at the incurred frequency regret which。

 is not the same as Bayesian regret because in that case we'd have to average over the， parameters。

 In this case Thompson sampling is doing a lot better。 So in this case here this would be 。

85 and it would be 。0000。 In this case Thompson sampling would be doing a much better job。

 Now Thompson sampling actually does achieve the line Robbins lower bound for the performance。

 of an algorithm。 So in terms of its lower bound is similar so that's one indication that this might be。

 a good algorithm。 There's a lot of bounds for optimism。

 In general the bounds for optimism are better than the bounds for Thompson sampling。

 A lot of the Thompson sampling bounds end up converting to sort of upper confidence bounds。

 A little bit like Thompson was asking。 So if you want to make Thompson sampling have frequentness like bounds often we end up sort。

 of making our sort of being more optimistic in terms of Thompson sampling。 To put those。

 But empirically Thompson sampling is often great。 Can you mix them？

 Can you mix Thompson sampling in upper confidence bounds？

 Maybe start with some form for confidence bound and use that information to update like。

 your priors on the Thompson sampling。 Um， I mentioned to say could you mix them？ You probably could。

 You could probably do it。 I don't know。 So I guess to me one of the so maybe you could start with upper confidence bounds and。

 then use Thompson sampling。 To me one of the big benefits of Thompson sampling empirically is that it is less optimistic。

 than upper confidence bounds。 Upper confidence bounds tend to be too optimistic for too long。

 It's like oh you know I ran into the door 30，000 times but maybe the 30，000 and one。

 time I won't you know like for your robot or something like that。

 So it often tends to sort of think about the extreme events。

 Whereas if you know that say the world is really galsy and like the probability that your。

 robot is going to run into a wall again is still really high even if it's only run into。

 the wall 10 times。 So maybe you should pick a different path。

 So I think often you probably would want to start with Thompson sampling but you would。

 like to be robust to your prior。 And so some work that tries to combine these ideas is known as pack Bayesian where you try。

 to get， I'll define what pack is in a second but you'll try to get bounce that are kind。

 of frequentist like but also get the best of both worlds。

 So you'd like to be like Bayesian if your prior is really good and pack if you like。

 sort of frequentist if it turns out that your prior is run。

 So one of the papers that I think sort of changed a lot of people's minds about Bayesian。

 and bandits and also Thompson sampling being a good idea was this paper by my colleague。

 Lee Huggley and also Chappelle where they looked at contextual bandits and we'll hopefully。

 get to this for a little bit on Wednesday。 But the idea in contextual bandits is that you have a state and an action so it's a little。

 bit different than the bandits we've seen so far。 Unlike in MDPs your action does not affect the next state。

 So for those of you doing the default project you're seeing examples of this where how you。

 treat the current patient doesn't impact the next patient that comes long but the patient。

 characteristics can affect which arm is best。 So contextual bandits is a very popular and powerful framework。

 And so in this case they were looking at news article recommendations and they were finding。

 Thompson sampling did much better than upper confidence bounds than a number of other algorithms。

 It also can be more robust when your outcomes are delayed。

 So this happens a lot often in real cases you could imagine you treat a patient you're。

 not going to find out whether or not that toe procedure helps for another six weeks but。

 in the meantime other people come in who's toes need to be treated and if you use upper。

 confidence bound algorithms they tend to be deterministic and so you just keep treating。

 everybody with the same thing until you get the outcome from the first。

 Whereas Thompson sampling is stochastic so you will be sort of trying out a lot of things。

 That's another good reason in practice why Thompson sampling can be helpful。

 Okay so I'm not going to go through the proof today but I'll put some pointers to that。

 The nice thing is that if you look at the Bayesian regret of Thompson sampling it's going。

 to have a similar result to what upper confidence bounds has。

 So it essentially has the same we can regret bounds as UCB。

 Essentially I've been slightly hand-waving for that。

 There's some important subtle details but roughly you can show that these also have good。

 Bayesian regret bounds if your prior is correct and so that's sort of again a nice sanity check。

 that you can get this logarithmic regret growth。 Alright another framework that I just mentioned sort of impassing just now is probably approximately。

 correct。 So these theoretical regret bounds specify how your regret grows over time and one thing。

 that's hard to know is whether you're making a lot of small mistakes or a few big mistakes。

 your regret bounds are cumulative so it doesn't allow you to distinguish between those two。

 So you can imagine the case of patient treatments this could be pretty important like are you。

 giving everybody a headache or a few patients really you know having really really bad side。

 effects。 So regret cumulative regret doesn't distinguish between those two because if a couple people。

 have really bad side effects that's the same as a lot of people having headaches when you。

 average over those。 And so one idea is to say well maybe we just want to kind of bound the number of non-small。

 errors。 So we want to bound the number of people that experience really bad side effects for example。

 So probably approximately correct comes up in supervised learning in the context of decision。

 making we often define it as follows a properly approximately correct algorithm or PAC state。

 that the algorithm will choose an action who is which is epsilon close to optimal with。

 probably at least one minus delta on all but a polynomial number of steps。

 So the probably part comes from here so it's not guaranteeing that you will do this but。

 with high confidence or probably it will do this。 It's approximately correct because we're only guaranteeing epsilon optimality and the important。

 aspect is it only does makes these sort of makes mistakes that might be bigger than epsilon。

 So the number of you know patients we might treat that have really really bad side effects。

 is going to be no more than a polynomial function where the polynomial function is a function。

 of the parameters of your domain。 So things like the number of actions you have epsilon and delta。

 And you should be able to compute this in advance too so you should be able to compute。

 how many mistakes you might make。 And one of the cool things is that you do a lot of the PAC algorithms algorithms that。

 are PAC are based on optimism or Thompson sampling。

 PAC for bandits is a much less common approach than when we go to MDPs。

 In bandits most of the time we look at regret but for when we look at Markov decision processes。

 PAC is more popular and we'll see one of the reasons for that probably later。

 Or feel free to ask me about it if we don't get to it today。

 Okay so what would PAC look like in our little example we had here before？

 So let's use O to denote optimism TS to denote Thompson sampling and within epsilon means。

 that the action that we select is within epsilon of the optimal action。

 So its value is epsilon close to the optimal action。 So I've written down the regret in this case。

 Here what we would have is that for optimism the first action that we pull is a one so it's。

 within epsilon yes because we're close to the optimal action。 A2 has a mean of 0。

9 so that's within 0。05 of 0。95 so this is yes。 Action A3 is 0。

1 so it's not within epsilon of the optimal action so this is no and so， forth。

 So this essentially allows the algorithm to be taking either action one or action A2 under。

 this definition of epsilon。 So as I don't care whether or not you're taking action A1 or A2 both of them are really pretty。

 good both of them within 0。05 of each other I mean that's fine but we don't want you to。

 take action three very much because it's much worse。

 And then in this case this one would say this is not within epsilon because the first action。

 we take is bad and then all the rest are good。 And what a PAC approach would do would they be counting all these counting the mistakes。

 Okay so we just talked about for bandits different sort of frameworks and criterias we talked。

 about regret Bayesian regret and PAC and we talked about two styles of approaches either。

 optimism or Thompson sampling。 And what we can see now is that Markov decision processes have many of the same sorts of ideas。

 being applicable but it also does get a lot more challenging。

 So in particular what we're going to talk about right now is we're going to talk about。

 tabular MDPs。 And it turns out that even from with tabular MDPs that things are a lot more subtle。

 So how does this work？ The regret the Bayesian regret and PAC is all going to be applicable so is optimism and。

 so is probability matching。 So let's start with thinking about optimism under uncertainty。

 First let's think about just doing optimistic initialization。

 So in this case imagine that we just initialize all over our Q state actions to some value。

 So let's imagine that we initialize them to R max divided by 1 minus gamma。

 Where R max is the highest reward you could see in any state action pair。

 So let's just take one minute。 Why is that value guaranteed to be optimistic？

 Anybody want to answer why that's guaranteed to be optimistic？ Yeah。

 It's higher than the possible total value because we've shown a couple of times that。

 R max one minus gamma would be the highest right。 I think that's one of the 10 too。 That is correct。

 We've shown that for a discounted mark-up decision process that the highest value you。

 could get is R max divided by 1 minus gamma。 At best all of your states have that or else some of them might not。

 So this is guaranteed to be an optimistic value。 So you could start off and you initialized all of your state action values to be R max。

 divided by 1 minus gamma。 And then you can do Monte Carlo， you can do Q learning， you can do SARS-F。

 And you can incrementally update using that。 And this can be very helpful。

 It can sort of encourage systematic exploration of states and actions because essentially。

 you're pretending that everything in the world is really awesome until proven otherwise。

 So on the downside unfortunately if you do this in general。

 There's no guarantees on performance even though it's often empirically better。

 So even though this really is an upper bound， this is optimistic， a key issue is how quickly。

 you're updating from those optimistic values。 So as an early result in this case。

 Ivan Darr and Mansour in 2002 proved that if you run， Q learning with learning rates。

 they should say alpha i。 So if you run Q learning with particular alpha rates。

 alpha i on each time step i。 And you initialize the value of a state， so this is the very beginning。

 to be R max divided， by 1 minus gamma times the product of those learning rates。

 And T is the number of samples you need to learn optimal Q。

 Then greedy only Q learning this pack with that initialization。

 So I just want to highlight something here which is this part。 So notice this is way， way。

 way larger than just R max over 1 minus gamma。 Because this is a product of all your learning rates。

 So this could be really enormous。 You can imagine that alpha is equal to 0。1 for all time steps。

 Then what you have here is you have 1 over 0。1 to the t。

 This is approximately which is equal to 10 to the t。

 So this is exponential in the number of time steps you're going to make decisions。

 It's incredibly optimistic。 It turns out this is sufficient to be pack， but it's also not very good。

 It's very， very extremely large。 Now this spins some really cool work by Chi Jin and some others over at Berkeley that showed。

 that if you use a less optimistic initialization that's strongly related to upper confidence。

 bounds and you are careful about your learning rates。 So you have to change your learning rates。

 But if you're careful about your learning rates， they prove that model of free Q learning。

 could also be pack。 And this was a pretty big deal recently because almost all of the work that's been going on。

 has been in the model based setting。 So this just came out in NURPs about two months ago。

 And so they， or sorry， not pack。 They showed regret bounds。 They're not optimal regret bounds。

 but they're good。 So they're not tight yet， but it shows that model free algorithms can do pretty well。

 Okay。 So what about model based approaches？ And the model based approaches for MDPs are the ones where we really have the best bounds。

 right now。 So there's a couple of main ideas or a couple of different procedures we could go with。

 What is that you could be really， really optimistic in all your estimates until you're confident。

 that your empirical estimates of your dynamics and reward model are close to the true dynamics。

 and reward model parameters。 So these sort of algorithms proceed as if they say the reward for all state action pairs。

 is amazing。 It's R maxified by one minus gamma。 And I'm going to continue to pretend that's true until I think I have enough data for that。

 state action pair that I think that if I did a MLE maximum likelihood estimate of those， parameters。

 they would be close to the true parameters。 So you can say I'm just going to be incredibly optimistic until I've got enough data and then。

 when I've got enough data， then I think I can get a good empirical estimate that is close。

 to the true estimate and then I'll use those instead。 So it's almost kind of like a switching point。

 You sort of keep a， you pretend everything's really， really great until you get enough。

 data and then you switch over to the empirical estimate。

 So these were some of the earliest ones that showed that MDPs could be， algorithms for。

 MDPs could be pack， so term 2002。 But they're also empirically not normally so good because you're pretending things are。

 really， really awesome， even though you might have quite a lot of evidence for that state。

 action pair that it's not awesome。 So another approach is to be optimistic given the information you have。

 So what do I mean by that？ I mean that as your agent walks around and gathers observations of the actions and rewards。

 it gets， it uses that to try to estimate how good the world could be given that data。

 And so one approach to this is to compute confidence sets on dynamics and rewards models。

 So we already saw this for bandits where we computed upper and lower confidence or we。

 could compute upper and lower confidence bounds for the rewards。

 Turns out we can also compute confidence sets over the dynamics model。

 Or we could just add reward bonuses that depend on the experience or data。

 And I'm going to talk at least a little bit today before we finish about this second thing。

 And the reason I'm going to talk about this particular approach is because when we start。

 to think about doing this in the function approximation setting， if the way that your。

 dynamics model is represented is by a deep neural network， then writing down uncertainties。

 over that can be really tricky。 And also a lot of the progress in deep neural networks for RL focus on model free approaches。

 And if we have reward bonuses， then we can easily extend that to the model free case。

 And empirically， these ones generally do pretty much as well as if we use explicit confidence， sets。

 So I'm just going to explain how the model based confidence model based interval estimation。

 with exploration bonus works。 So it's going to assume that we're given an epsilon delta and some constant m。

 And then what we're going to do is we're going to initialize some counts。

 So this is just going to keep track of the number of times we've seen a state action pair。

 So we're going to do this for all s and for all a。

 We're also going to keep track of the number of times we've seen an state action next state， pair。

 Zero for all s for all a for all s prime。 And we're also going to keep track of the total sum of rewards we've gotten from any。

 state and action pair。 So essentially， we're going to keep track of the times that we've been in any state。

 taken， any action， and went to any next state and what the sum of rewards are for when we've。

 done that。 And then we're going to define a beta parameter。

 And we're going to double check I get the。 All right。

 So beta is going to be a parameter that we're going to use to define our reward bonuses。

 And some one over one my is gamma to log the number of states number of actions to times。

 M and is an input parameter divided by delta。 And then。 Yeah， I think that's all I need here。

 So I'm going to say t equal to zero。 We're going to initialize our state。

 And start we can just say Q t of S a sequel to。 One divided by one my is gamma。

 And this assumes that all of our awards are bounded between zero and one。

 So they're bounded rewards。 Okay， so we start off when we initialize all our accounts to zero。

 We say we haven't observed any rewards yet and we pretend that the world is awesome and。

 that our Q value is the highest it could possibly be in every state action pair。

 Here are max is equal to one。 So our max is going to be equal to one because our rewards are bounded between zero and one。

 So what we do then is we take an action in the current state given our do till does given。

 our Q function so beginning we're just going to break ties randomly and then we're going。

 to observe the reward and observe the next state and then we just update our accounts。

 So we update our accounts for that particular state action pair。

 We update our accounts for S a S prime S a S prime。

 For the number of times we've been in that state taking that action and went to that particular。

 next state。 And then we update our rewards for that state action pair is equal to the previous rewards。

 for that state action pair plus RT。 And then what we're going to do is we're going to use those empirical accounts to define an。

 empirical transition model and empirical reward model。

 So our reward model is going to just be the Emily reward model which is just going to。

 be RC per SA divided times divided by the number of times we've been in that state action pair。

 Let's just the average reward for that state action pair。

 And then our transition model is also just going to be the number of times A S prime divided。

 by the number of times we've been in that state action pair。

 We're just going to define our empirical transition model and our empirical reward model。

 And it doesn't matter how we initialize things that we haven't seen at all but you can treat。

 them as uniform。 So we're going to do this for all SA。

 And then we're going to compute some uq functions。

 And we're going to compute some uq functions where we do this， where we take our empirical。

 models and we also add in a reward bonus term that depends on beta and the number of times。

 we've tried that state action pair。 And we can do value iteration。 That's what I'm doing here。

 But you could solve it however you'd like。 But the main idea here is that we're going to use our empirical estimates of the reward。

 model and the transition model by just averaging our counts or averaging the rewards we've。

 gotten for that state action pair。 And then we're going to add in this is a reward bonus。

 And note at the beginning this reward bonus can be really like it can be infinity so you。

 can because if we have no counts for that。 So then we can just initialize for any QSA。

 So for all SA such that n SA of SA is equal to zero you can just set this to be Q max。

 So to deal with if you haven't sampled that state action period。

 So that means anything for which that you haven't sampled yet is going to look maximally。

 awesome and anything else is going to be a combination of its empirical average parameters。

 plus a reward bonus and that reward bonus is going to get smaller as we have more data。

 So I'll put this on here where it will be neater。 So this is the reward bonus。

 And what you can see here is that over time that's going to shrink。

 So for time you're going to get closer and closer to using the empirical estimates for。

 a particular state action pair。 But for state action pairs you haven't tried very much there's going to be a large reward。

 bonus。 So the cool thing about this is that we can think about whether it's PAC。

 So I'll just take one more minute which is in an RL case an algorithm is PAC if on all。

 but end time steps the action selected is epsilon close to optimal action where n is a polynomial。

 function of these things。 The number of states， the number of actions gamma epsilon and delta。

 This is not true for all algorithms greedy is not PAC。 Greedy can be exponential。

 We might talk about that on Wednesday。 So no。 And the nice thing is that the MBIEB algorithm I just showed you is PAC。

 So what does it pack in？ It means that on all but this number of time steps or I'll just circle it。

 So this is sort of a large ugly expression but it is polynomial the number of states and， actions。

 It's also a function of the discount factor and the epsilon。

 In general if you want to be closer to optimal it's going to take you more data to ensure。

 that you're close to optimal。 So it's inversely dependent on epsilon。

 It's polynomial dependent on state and actions and this says on all but this many time steps。

 your algorithm is going to be taking actions that are close to optimal。 So this is pretty cool。

 It says like by just using these average estimates plus taking on a bonus term and then computing。

 the Q functions then you can actually act really well on all time steps except for a。

 polynomial number。 And then I put in here this empirical of that and I'll just say briefly that on some sort。

 of hard to construct simple toy domains these type of algorithms do much better even than。

 some other ones that are provably efficient。 They can do much much better than things like greedy。

 So algorithms like MBIEB， MBIE is a related one that uses confidence sets can do much。

 much better than this is sort of be optimistic until confident。

 And these ones are generally much better than greedy。

 So these types of optimistic algorithms can empirically be much better as well as being。

 provably better and on Wednesday we'll start to talk about how to combine them with generalization。

 Thanks。 [BLANK_AUDIO]。

![](img/dd3d90b32ca727decf2aefee2351f66e_5.png)

![](img/dd3d90b32ca727decf2aefee2351f66e_6.png)