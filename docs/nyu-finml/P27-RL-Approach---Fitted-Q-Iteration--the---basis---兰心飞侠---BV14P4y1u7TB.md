# P27：RL Approach - Fitted Q-Iteration- the Ψ-basis - 兰心飞侠 - BV14P4y1u7TB

 So in the last video， we introduced two parameterizations for the Q function。

 One in terms of matrix W_t， and another in terms of vector U_W。

 which was given by a product of matrix W_t and the vector phi of basis functions。

 We saw that if we somehow observed optimal actions， a_t star， an optimal Q function values Q_t star。

 this would serve as two equations for three unknown components of vector U_W。 Now。

 this suggests that a right solution， that the one that would be found by the dynamic programming method。

 if the dynamics are known， should be in the space of solutions。

 parameterized by a time-dependent matrix W_t， as we did in our specification of the Q function。

 So we have to find a way to learn the matrix of K-fissions W_t。 Let's see how this can be done。

 What we need to do is to rearrange terms in our definition of the Q function。

 to convert it into a product of a parameter vector。

 and a vector that depends on both the state and the action。 So how we do this？

 We do it in several simple steps。 First， let's write explicitly the value of the Q function。

 as a trace of the matrix expression given here。 We write it as the element-wise product of elements of matrix W。

 with elements of a matrix that is formed by a direct product of vectors A and phi。

 This gives us the second line in this expression。 We have two types of multiplication here。 First。

 this symbol stands for the element-wise product of two matrices。

 This product is also known as the Adamar product of two matrices。 Second。

 this other expression has this encircled cross product sign。

 and this sign stands for a matrix given by the outer product of two vectors， A_t and phi_t。

 By definition， the element i_j of this matrix is given by a product of A_t_i and phi_t_j。

 So far so good， we converted the whole expression into a trace of a product of two matrices。

 But now we can do one more thing and represent this expression， as a scalar product of two vectors。

 What we have to do to this end is to convert both matrices entering this expression to vectors。

 We can do this by concatenating columns of matrix W。

 and the matrix given by the outer product of A_t and phi_t。

 And this will give us the third line in this equation。

 Now we can compactly write this whole expression as a dot product of vector W and vector psi。

 And here vector psi is obtained by concatenating the columns of the outer product of vectors A_t and phi_t。

 This can be viewed as a new set of basis functions that depend both on state and action。

 The dependence on the action A_t is quadratic， but the dependence on the state x_t can be arbitrary and depends on the functional form of the original basis functions phi_n。

 for the state space。 If we use for example cubic B-spines as basis functions。

 as we did in the dynamic programming solution to the model。

 then the X dependence would be locally cubic。 Now let's compare what we got with the setting of dynamic programming。

 In our current reinforcement learning setting， we reduced the expression for the。

 q function to a dot product of vector W and the new vector of state action basis function psi_t。

 Both have a number of components given by 3m， so that the number of unknown coefficients in this problem is 3m。

 As you could also easily guess just by looking at the matrix W_t， which has dimension 3 by m。

 So we have 3m unknowns here。 Now what about the number of observed variables？

 For each time step in the Betch-Mold reinforcement learning setting。

 we have 3m observables because we observed the state x_t。

 the action at and the reward r_t for all of n historical or Monte Carlo paths for the stock。

 So we have 3m observables for 3m unknowns。 And if n is larger than m。

 then our problem is well posed。 We have n divided by m observations per 1v parameter in this setting。

 Now we can compare this with the situation we had with the dynamic programming approach。

 In that case， we had to find two quantities， the optimal policy and the optimal q function。

 In our dynamic programming solution， we expanded both in m basis functions。

 so we had 2m unknown coefficients in total。 This is less than 3m unknown coefficients in the reinforcement learning setting。

 But on the other hand， the number of observations per time slice in a dynamic programming approach was also less than in the reinforcement learning approach。

 And this is because in the dynamic programming setting， we only observed the states。

 So for n Monte Carlo paths， we only had n data points per each time。

 The number of observations per parameter was therefore n divided by 2m。

 which is actually less than the ratio of n divided by m that we have for the reinforcement learning setting。

 So it appears that at least when the data for reinforcement learning is generated from the dynamic programming solution both the reinforcement learning and dynamic programming methods should perform。

 about equally well。 This setting is called on policy learning。

 and it means that actions recorded for training of the reinforcement learning cation were actually optimal actions。

 It turns out that this is indeed the case and both algorithms produce nearly identical results for such setting。

 This actually gives us a simple way to benchmark our reinforcement learning algorithms。

 Because we can solve our model when it's fully specified by means of dynamic programming。

 we can compute the optimal policy from this solution。

 Then we can just use the observed actions and the words obtained with this policy as data for fitted curation method and compute the optimal policy and q function using this method。

 Because this solution is already known from dynamic programming。

 we can use it to benchmark our reinforcement learning solution and check the speed of conversions。

 the final results and so on。 This is actually very ensuring as we now know exactly what we expect to see。

 So any problems with fitted curation would immediately show up if found there。

 If we now want to try some other reinforcement learning algorithm instead of fitted curation。

 again we have a good benchmark obtained with a dynamic programming approach。

 Therefore we can test many different reinforcement learning algorithms with our simple MDP model for option pricing。

 Let's take a short pause here and continue in the next video with the actual solution of the model with the fitted curation method。



![](img/06e2e0050b82f5416f388b1b7f6c3663_1.png)

![](img/06e2e0050b82f5416f388b1b7f6c3663_2.png)