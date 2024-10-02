# P26：RL Approach - Fitted Q-Iteration - 兰心飞侠 - BV14P4y1u7TB

 So in the last video， we talked about the need to use cross-sectional information on all Monte Carlo pass。

 or historical pass of the stock simultaneously when calculating an optimal policy。

 To remind you why this is the case， it's simply because the catch policy is a function that defines the mapping。

 for any inputs to the outputs。 But each observation only gives some information about such function at one particular point。

 And updating the function using only one point can be a very long and noisy procedure。

 This means that the classical keel learning algorithm。

 even though it's guaranteed to converge asymptotically。

 need to be replaced by sounding more practical that converges faster。

 Because we're working the setting of batch model reinforcement learning。

 perhaps we could do better than the classical keel learning if we managed to do updates by looking at all realizations of portfolio dynamics。

 that happened in data in order to decide on the optimal policy。 And fortunately。

 there exist extensions of keel learning for such batch mode reinforcement learning settings。

 We will take a most popular extension of keel learning to a batch reinforcement learning setting called sheet of q iteration。

 or FQI for sure。 This method was developed around 2005 and 2006 in a series of papers by Ernst and co-workers and by Murphy。

 One noticeable point here is that Ernst and co-workers considered time stationary problems where the Q function does not depend on time。

 And also many published research in reinforcement learning literature deal with an infinite horizon keel learning where a keel function is independent of time。

 Keel learning for such stationary problems is somewhat different from keel learning that we need in our problem。

 which has a finite time horizon and therefore is time dependent。

 But the paper by Murphy presented the version of batch mode keel learning that works for problems with a finite time horizon。

 such as our problem。 Now the fitted keel iteration method works with continuous value data and therefore we can now bring the model formulation back to a general continuous state space case。

 as was the case in our Monte Carlo setting for the dynamic programming solution。

 But if we want to stick to a discrete space formulation fitted keel iteration can be used in essentially the same way。

 The only difference would be in a specification of basis functions that the method needs to use。

 So to reiterate the FQI method works by using all Monte Carlo pass or historical pass for the replication portfolio simultaneous name。

 This is very similar to how we solve the problem using dynamic programming with Monte Carlo method for the case of known dynamics。

 In this method we averaged over all scenarios at time t and t plus one simultaneously by taking an empirical mean of different pathwise Monte Carlo scenarios。

 Conditioning on the information set of t at time t was implemented as conditioning on all Monte Carlo pass up to time t。

 Now in the setting of batch mode reinforcement learning the only thing we need to change in such Monte Carlo setting is the structure of input output data。

 In the setting of dynamic programming when the model is known the inputs are simulated or real forward pass of the state variable extreme。

 And the outputs are the optimal actions and action policy and optimal Q function。

 That is the negative option price。 The optimal action a star is determined by maximization of the optimal Q function and instantaneous rewards are computed in the course of backward recursion for the optimal action and optimal Q function。

 This was the case for dynamic programming now in the setting of batch motor reinforcement learning neither transition probabilities nor the policy or reward functions unknown。

 The required output is the same as before。 That is we have to find option price and hach。

 However the input is now richer than in the previous case as now we have two more observations for each observed state vector x team。

 We know the action x at and the reward RT。 Instead of this function PT star and RT we now have only samples obtained from these functions in different states x team。

 And this is the setting of batch reinforcement learning where the state variables at both times T and T plus one and rewards received for all Monte Carlo pass are used simultaneously to find the optimal action and optimal Q function at times。

 For all states x T and all actions AT of x team。 And this amounts to learning a policy。

 With either simulated Monte Carlo data or real data batch motor reinforcement learning works the same way。

 Now let's see how fitted Q iteration works in our problem。

 The FQI method looks for the optimal Q function using an expansion in the set of basis functions。

 We can use the same set of basis functions phi N of x that we used in the dynamic programming solution。

 Now recall that the reward is a quadratic function of actions。

 Therefore the Q function will also be a quadratic function of actions and we represent the Q function here as a product of vector A。

 matrix W and vector phi as shown in this equation。

 Here AT will be a vector of size three made of unity AT and one half times AT squared。

 FET is a vector of basis functions with size M where M is the number of basis functions。

 And finally WT will be a matrix of K-efficients which will have the shape of three by M。

 This form for the Q function captures its quadratic dependence on the action。

 while parameterizing the dependence on coordinate Xt with basis functions phi N of x and K-efficients W。

 For what follows we can equivalently write the Q function in a slightly different form。

 If we join the coefficient matrix W and the vector phi into a new vector U_W。

 which is indexed by W to emphasize that this vector depends on K-efficients W。

 We can also put terminal conditions on the vector U_W。

 For example if we set the terminal action AT for capital T to zero。

 this translates into terminal conditions for components of vector U_W that are shown here。

 In this case only the first component is non-zero at maturity and two other components vanish at time capital T。

 Now we can use this representation of the Q function in two ways。

 Let's first assume that parameters of matrix WT are known。

 Then because Q function is quadratic in action AT we can find the optimal action and optimal Q function in terms of components of vector U_W。

 If you do this simple math you will find these two equations。

 They define optimal action and Q function in terms of components of vector U_W。

 But in fact our objective here is rather the opposite。

 We have to find components of matrix WT or equivalently components of vector U_W from observable actions and states。

 In this case we would rather view these equations from the right to the left。

 But then we have two equations for three unknowns。

 This is still okay because these unknowns depend on the same matrix WT and are dependent in this sense。

 But it also means that to solve our problem we have to find directly the matrix WT from data。

 And in the next video we will see how this can be done。 [ Silence ]。



![](img/9b0a84a0631923d3be6d37c28ab6e5bd_1.png)

![](img/9b0a84a0631923d3be6d37c28ab6e5bd_2.png)