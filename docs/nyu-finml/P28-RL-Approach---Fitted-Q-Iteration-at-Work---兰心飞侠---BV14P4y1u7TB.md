# P28：RL Approach - Fitted Q-Iteration at Work - 兰心飞侠 - BV14P4y1u7TB

 So in the previous video， we converted our problem to a more standard formulation。 where the unknown Q function is expanded in a new basis psi of dimension 3 times m。 where parameters w that are given by parameters of the original matrix wt are stored commonwise。 Now， our problem is to compute this key-ficient wt。 As in a dynamic programming solution。

 we compute this key-ficient recursively by going backwards in time。 starting from time capital T minus 1， then capital T minus 2。 and so on all the way to the current time t equals 0。 The way to do it is similar to what we did with the dynamic programming approach。 Again。

 we look at the Bellman-Eptimality equation shown here。 It says that the time t Q function is given by the expectation of the expression in the right-hand side of this equation。 Now， we can interpret it as regression of this expression on the unknown function Qt。 that is written as an expansion in state-action basis function psi n。

 where epsilon t would be a random noise time t would mean 0。 These two equations are clearly equivalent in expectations。 because if we take expectations of both sides of the second equation。 we recover the Bellman-Eptimality equation。 So now we have a standard regression problem for K-ficient's wt in this setting。

 Let's note that this is both similar to and also different from how we computed the optimal Q function。 with the optimal action in our dynamic programming solution in the last week。 There we had the regression problem approximation for the Bellman equation for the optimal Q function evaluated at the optimal action at star。 Respectively， we expanded this Q function in a set of basis function phi n of x。

 because the action at here was fixed to be the optimal action at star。 Rewards， rt。 were computed there as a part of the solution to the problem。 Now。 all these can be compared with the present reinforcement learning setting。 This time we compute the optimal Q function using a regression interpretation of the Bellman equation for arbitrary actions at。

 and not just for the optimal action at star， as we had for the dynamic programming solution。 The other and related difference is that now our function approximation for the Q function relies on expansion in state action basis function psi m。 rather than state dependent basis functions phi n。 as was the case with the dynamic programming solution。 And furthermore。

 while in the dynamic programming approach we computed the rewards rt in the reinforcement learning setting。 both the rewards rt and actions at are observed。 So， because we reduced the problem to regression。 we can now find the coefficients wn by minimization of the objective function shown in this equation。 Now， this relation holds for any data， including data that may be of policy。

 that is collected under a sub-optimal policy。 Before we move to this general case。 let's discuss what we should get for a simpler case of own policy learning。 when all recorded actions are optimal actions。 For this case。 we simply have to substitute at by at star in the previous equation。

 Then we have the first equation shown here。 But now we can see that it's almost identical to the objective function that is shown in the second equation here。 and this is the objective function which we had in our dynamic programming solution。 The only difference is in the last term in these two equations。 but this is exactly the term that is optimized by a choice of parameters。

 If we have infinite number of observations， then these two objective functions will have the same minimum。 because the last terms can be made conciding pointwise in this limit。 Therefore。 both methods converge asymptotically to the same solution if we deal with the own policy coloring。 But because coloring is an off-policy algorithm， and because the original optimization problem for K-efficient WTS convex。

 we are guaranteed that the off-policy method isymptotically converges to the same solution。 We can also find the explicit link between the two solutions for large but finite n。 if we impose the equality between them in the least square sense。 And this will give us this objective function in the first equation here。

 So when it for K-efficient WTS in terms of K-efficient's omega T of the DP solution。 we obtain the second equation here。 This equation gives the solution of the reinforcement learning problem for unpalice learning in terms of the dynamic programming solution。

 and this relation becomes exact in the limit when n goes to infinity。 Now let's come back to a more general case of finite n and off-policy learning that is given by our least square optimization for K-efficient's WTS。 This case is also easy to solve。 Similar to our dynamic programming solution。 we introduced Matics ST and Vector MT that are shown in these equations。

 and expressed in terms of new basis functions psi n。 Then the optimal weights WT star。 simply given by the inverse of Matics ST times Vector MT。 Once we have the K-efficient WT star。 we know the optimal Q function and also know the elements of Vector U underscore W。 that we introduced earlier。 We compute this optimal Q function for the current time step T。

 and then we move to the previous time step T minus 1 in our backward recursion。 But now。 according to the Bellman-Optimality equation， we will need the optimal Q function at the optimal action AT star。 from the next time step T to solve for K-efficient's WT minus 1 for the current time step。 How exactly we do it is very important for the algorithm， so let's discuss this next。

 Once we solve for K-efficient's WT for the current time step T。 we can compute the elements of Vector U underscore W。 that we introduced earlier and write the optimal Q function for the next time step T plus 1。 as the second order polynomial in components of this vector， as shown in this equation。

 But the critical point is that it would be completely wrong to use a point of a maximum of this expression as a function of AT plus 1 star。 as such optimal value， because this would amount to using the same data set to estimate both the optimal action and the optimal Q function。

 This would lead to a potential overestimation of a QT plus 1 star due to Jensen's inequality and convexity of the MOCs function。 The correct way to proceed is to plug there our previous analytical solution for AT plus 1 star shown here and deploy it at the previous time step。

 Due to availability of the optimal analytical action。 we do not face in our setting a potential overestimation problem。 because now we do not use the same data set to estimate two functions。 The second calculation of the optimal action is now analytical。

 And here I would like to note that a potential overestimation is a classical problem of Q learning。 that is sometimes addressed using various numerical tricks such as， for example， double Q learning。 You can read more on such methods in an additional reading for this week。 but in our framework such tricks are not needed because the analytical optimal action is available。

 This produces a numerical stable solution to the model。 So to summarize。 we saw how to make a one backwards step in a fitted Q iteration method。 Going in this way all the way back to the current time T equals zero， we get the optimal option。 hedge and price。 But this time in a completely data driven and model independent way due to the fact that fitted Q iteration is a model free and off policy algorithm。





![](img/b47add49eadad5b358d1dbc96b225e78_1.png)

 [BLANK_AUDIO]。

![](img/b47add49eadad5b358d1dbc96b225e78_3.png)