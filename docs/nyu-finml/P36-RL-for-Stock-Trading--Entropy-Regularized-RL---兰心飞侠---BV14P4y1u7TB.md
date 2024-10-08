# P36：RL for Stock Trading -Entropy Regularized RL - 兰心飞侠 - BV14P4y1u7TB

 Okay， now we're going to have a little more math than we had before so far。

 So please bear with me as we're going to dive into a bunch of new formulas for the next few minutes。

 And also in the next video。 And if you find yourself lost some way in the middle。

 you can always stop and rewind or look into original sources for more details。

 And then maybe watch this video again。 But hopefully you will not have to do it or at least you will not have to do it too many times。

 So let's start。 Let me start with reminding you the standard Bellman equation for the value function。

 We define an optimal value function D* as shown in equation 27 as a maximum overall policy spy of an expected sum of discounted future rewards。

 Once we discussed in our previous course， when we work with the Bellman equation for the value function。

 we normally work with two equations。 One of them is a Bellman-optimality equation for V* shown in equation 28。

 The second term in the right hand side of this equation is an expectation of a future value function conditional on a given current state and action。

 The optimal value function V* at time t is a maximum of the right hand side of this equation with respect to all actions at。

 Now a policy pie is not explicitly present in this equation。

 If you already know an optimal value function V* then computing an optimum policy takes a different optimization problem in equation 29。

 We call this step a policy improvement step in our previous course。

 Now we reformulate the Bellman-optimality equation such that the policy pie explicitly appears there。

 A tick that does it shown here is sometimes called a fensual representation。

 In this formulation everything is the same as before except that now we maximize with respect to a policy pie。

 rather than with respect to actions at。 Policy pie can be any policy from a set of valid distributions that we call P here。

 Now why is this formulation equivalent to the previous formulation？

 This is because of a simple identity shown at the bottom of this slide。

 If we have a set of numbers x1 to xn then their maximum will be the same as a maximum over a set of weights。

 that we again call pie here over a dot product of these weights and the vector of values xi。

 And this is simply by construction because the optimal set of weights will give a weight of 1 to a maximum value of xi。

 and will give zero weights to the rest of x values。

 So this trick is very simple but very useful because now the policy pie enters the problem explicitly rather than implicitly。

 Now we make a very important next step。 We introduce a notion of information costs of updating a policy from a reference policy pie zero to a given policy pie。

 This cost is given by equation 30 as a log of the ratio of policy pie to policy pie zero。

 I refer you to a paper of tissue bee and co-workers for more in-depth explanation of why this quantity is called an information cost。

 But one thing we can immediately notice is that if we take an expectation of this expression with distribution pie。

 we will get what is called the public libler or KL divergence of two distributions pie and pie zero。

 which is shown in equation 32。 We mentioned the KL divergence a few times in this specialization and talked about how it serves as a measure of similarity between two distributions。

 The KL divergence is always non-negative and is strictly equal zero only when pie equals pie zero。

 Now we can take a discounted expected sum of all such information costs for all time steps。

 And this produces the total discounted information cost for a trajectory that is shown in equation 33。

 Now we can define the so-called free energy F_t。 As the value function minus the information cost of a trajectory multiplied by a factor one over beta。

 If we put explicit expressions for both terms here， we get the second form of this equation。

 Please note that we can see the whole expression in brackets here as a reward corrected or regularized by an information cost term。

 Parameter beta controls the strength of this regularization。 If we set beta to infinity。

 then the regularization term disappears。 In the opposite limit when beta is very large， sorry。

 is very low and modified one step reward will be completely determined by the second term。

 Parameter beta is called an inverse temperature parameter because it enters formulas below in a similar way to how the inverse temperature in physics enters formulas of statistical mechanics。

 So at the end， what is the free energy function？ As you can see from this equation。

 the free energy function is just an entropy regularized value function。

 As was explained in the paper by Tichbi， such entropy regularization is very helpful when an environment is noisy。

 In this case， the regularization term provides a helping hand if a priority is reasonable to find a good and noise tolerant optimal policy and optimal value function。

 And as in finance and environment is typically either noisy or very noisy。

 such entropy regularization is very useful for financial problems。

 We can now derive a Baumann equation directly for the free energy function。

 It's shown here in the equation 35 and it can be derived from the previous formula in this standard way。

 This equation can be viewed as a solved probabilistic relaxation of the optimal of the original Baumann equation where beta serves as a regularization parameter。

 If beta is set to infinity here， it reproduces the original Baumann equation as you can easily check yourself。

 Now， similarly to how we used KL divergence to regularize the value function。

 we can also regularize an action value function， Q function。

 We will call this function a G function following Tichbi and co-workers。

 A Baumann equation for the G function is the same as for the Q function。

 except we use the F function instead of the value function in the right hand side as shown in equation 36。

 We can now regroup terms in this relation and get the second form shown here。

 So the G function is an expectation of the same modified reward as in the F function。

 but this time conditioned on the current state and action， like the Q function。 In other words。

 the relation between the G function and the F function is the same as the relation between the V function。

 We can also compare the resulting expression with the formulas for the F function。

 And this gives us an explicit relation between the G function and the F function。

 which is shown in equation 37。

![](img/c821a60e51482683694de8c0ed278903_1.png)

 [BLANK_AUDIO]。

![](img/c821a60e51482683694de8c0ed278903_3.png)