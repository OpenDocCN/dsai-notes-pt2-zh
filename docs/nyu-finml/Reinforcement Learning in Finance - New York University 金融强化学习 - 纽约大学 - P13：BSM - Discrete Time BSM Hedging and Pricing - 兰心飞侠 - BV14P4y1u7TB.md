# Reinforcement Learning in Finance - New York University 金融强化学习 - 纽约大学 - P13：BSM - Discrete Time BSM Hedging and Pricing - 兰心飞侠 - BV14P4y1u7TB

 Now let's see how we should compute optimal hedges。 There is optimal positions in stock。



![](img/4301b24490c2d474050063d523186a7a_1.png)

 in all possible states of the world at time t。 So how can we do this？ In a previous video。

 we computed the portfolio value using a pathwise evaluation on Monte Carlo pass。 Now to compute。

 optimal hedges， you'd see we need to look at all Monte Carlo pass simultaneously。 The。

 other name for this is a cross-sectional analysis。 So we need to do a cross-sectional。

 analysis of known Monte Carlo pass to find optimal hedges。 Why is it so？ This is simply。

 because each Monte Carlo pass gives us only one value as t at time t。 But a hedging strategy。

 you'd see should apply to all states that might be encountered in the future。 Therefore。

 to compute an optimal hedge you'd see for a given time step t， we need the cross-sectional。

 information on all Monte Carlo pass at this time。 Okay， so the first point we make here。

 is that we have to look at all Monte Carlo pass at once。 The second question is in what。

 time order we should compute optimal hedges。 We will do it backwards in time， starting。

 from the final time t equal to capital T。 This is similar to the portfolio value calculation。

 that we did in a previous video。 However， because we can't know the future when we compute， a hedge。

 for each time t we should condition on the information ft that is available at， time t。

 Doin otherwise would be equivalent to picking into the future。 The information。

 set ft includes a history of individual Monte Carlo pass up to and including time t。 And。

 in addition， ft may include some market factors that can impact stock prices。 Now let's see。

 how we can compute the optimal hedges you start。 We obtained the optimal hedges you start by。

 minimization of variance of pi of t across all Monte Carlo pass at time t， conditional。

 on the information set ft。 We can also use our recursive formula for the portfolio value to。

 make the dependence on the argument ut explicit。 Now because variance of this expression is a。

 quadratic function of ut， this second form makes it clear that with you here with quadratic。

 optimization。 And therefore this can be solved semi analytically。 But before we do that， let's。

 take a look at this equation from the financial perspective。 Using two forms of this equation。

 we can interpret it in two related ways。 The first form of this equation means that all。

 uncertainty in a portfolio value pi t is due to uncertainty of the back cash account b， t。

 Therefore， an optimal hedge should minimize the cost of hedge capital at each time step。

 t that would be proportional to this uncertainty。 Now the second equation shows how this can。

 be done by using the recursive relation for pi t and choosing an optimal stock holding。

 ut according to this equation。 Now we can compute the optimal hedge by setting the derivative。

 of this equation to zero。 And this gives us the formula shown here in equation 10。 As。

 we said before， we have to compute this relation by going backwards in time starting from time。

 t minus one then t minus two and so on all the way to time zero。 The next and a bit harder。

 question is how to compute this expression。 It involves one step expectations of quantities。

 at time t plus one conditional on information or at time t。 Now how they can be computed。

 depends on whether we deal with a continuous or a discrete state space。 If the state space。

 is discrete， then such one step conditional expectations are simply finite sums involving。

 transition probabilities of MDP model。 But on the other hand， if we work in a continuous。

 state setting， these conditional expectations can be calculated with Monte Carlo by using。

 expansions in basis functions。 We will discuss how we can do it later。 But for now， let's。

 just remember that for what comes that FT will stand for cross sectional information set， at time t。

 Now let's consider how we can compute the option price in this framework。 First。

 we define a mean option price CT as a time t expected value of the hash portfolio pi， t。

 Now we can use our recursive relation for the portfolio value pi t and get the second。

 form of this relation。 And finally， we can replace the portfolio value pi sub t plus。

 one in this expression by its expectation at time t plus one。 This is because this term。

 stands here under expectation at time t。 So when we replace it by its future expectation。

 at time t plus one， we use what is called the tower law of conditional expectations。

 We then obtain what is shown in the third line of this equation。 And finally， in the last， line。

 we use again the definition of the mean price so that at the end we have a recursive。

 formula for the mean price itself。 So far so good， however， this is not all yet what we。

 need for option pricing。 The thing is that the mean option price C hat t corresponds。

 only to the mean of the portfolio of the hash portfolio， which corresponds to the mean cash。

 amount the seller should put in a bank when she sells the option。 But what about risk？ Clearly。

 there is risk that the expected value of cash amount B0 will not be sufficient to adequately。

 hedge the option in any given scenario。 Therefore， the option seller should charge a premium for。

 the option and in addition to the mean option price。 Now， one possible way to specify such。

 this premium is shown in this equation。 We simply add here discounted sum of all future。

 variances of the hash portfolio multiplied by a risk aversion parameter lambda。 Clearly。

 the smaller the future variance of the replicating portfolio， the smaller the risk premium that。

 the seller should charge。 But the absolute amount of this premium is controlled by the。

 risk aversion parameter lambda。 This is the expression that we will be working with going， forward。

 Now， the problem of the option seller is to minimize this expression by optimally。

 hedging the option because she needs to stay competitive when selling the option。 So our。

 problem is minimization。 But we can also formulate it as a maximization problem if we flip the。

 sign of the whole expression as shown here。 We will use this formulation our next lesson。

 So for now， I just ask you to take a mental note of this expression。 And on this point。

 we are ready to move to our next topic。 [BLANK_AUDIO]。



![](img/4301b24490c2d474050063d523186a7a_3.png)