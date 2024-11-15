# P20：Monte Carlo - Optimal Hedge With Monte-Carlo - 兰心飞侠 - BV14P4y1u7TB

 Now， after we introduce basis functions and saw how they can be constructed。 let's come back to our original problem of implementing the backward recursion for the optimal Q function with Monte Carlo。 We said earlier that conditioning on FT in conditional expectations that appear in our formulas for the backward recursion should be understood as conditioning on the whole set of all Monte Carlo paths。 Now， we get a great method to compute such expectations using the approach of basis functions。

 Let's assume that we defined a set of basis functions， phi n of x。 where the argument x would be the current value of the state variable。 We can and actually will choose these points that we discussed in the last video as such functions。 But we will keep the notation general so that other basis functions。

 phi n of x can be picked if needed as well。 In particular。 we could incorporate some external risk factors of stock prices into our set of basis functions。 For example， we could include the S&P 500 index price or volatility indexes such as VIX as such risk factors that describe the state of the market。 In other words， our stock hands can impact the price of a particular stock。

 We could also use some combinations of these factors with stock prices。 This could capture some interaction effects between stock prices and the factors。 In short。 there is substantial freedom in how to choose the basis functions。 so we will continue with the general formulation。 So we have two unknown functions in our problem。

 The optimal action， A* of x and the optimal Q function， Q* of x。 Now， if our set of basis functions。 phi n of x is representative enough， we can use it to approximate both functions A* of x and Q* of x。 Respectively， we represent both as expansions in the same set phi n of x。 Also。 because our problem is time dependent， we make coefficients of these expansions time dependent。

 So we have two expansions with coefficients phi n， t and omega n。 t for the optimal action and optimal Q function respectively。 Now。 the problem of option pricing and hedging amounts to finding these coefficients。 And overall。 we have two M unknown coefficients in total。 So， if we have， say， 12 basis functions。

 then it means that M is equal to 12， and in this case。 we will have 24 unknown coefficients to compute。 This reduces the original infinite dimensional function optimization for functions A* of x and Q* of x to a finite dimensional optimization with a small number of parameters。

 The backward recursion should now be reformulated as a scheme to compute coefficients phi and t and omega n。 t by going backwards in time starting from time capital T-1。 Let's start with computing coefficients phi and t of the optimal action。 To this end。 let's look again at the backward recursion formula for the Q function that we derived earlier。

 As we mentioned before， the right-hand side of this relation is a quadratic function of A*t。 Therefore， it will also be a quadratic function of K-fissian's phi and t。 And to compute these coefficients with Monte Carlo， we do several things with this relation。 First。 we plug here the expansion for A*t， then replace all expectations by Monte Carlo averages and also drop all terms that are independent of A*t。

 Then we flip the sign of the whole expression to turn the maximization problem for A*t into a minimization problem。 And this gives us the objective function gt of phi shown here。 which we should minimize to find optimal coefficients phi and t。 Now。 the good news is that because this is a quadratic function of phi and t。

 it can be minimized semi-analytically。 By setting the derivative of this expression with respect to some value of phi of m t to 0 and rearranging terms。 we get a system of linear equations for K-fissian's phi and t that is shown here。 It's defined in terms of a square matrix A of dimension m by m and a vector B of length m that are computed as shown in these two formulas。 The matrix A is positive definite or it can be made positive definite by regularization as we will discuss in a moment。

 so it has an inverse。 Therefore， the solution for K-fissian's phi and t is simply given by the product of the inverse of matrix A and vector B。 So， the whole calculation is as easy as the previous analytical formula。 but now we have a computable expression for the optimal action A* rather than a theoretical formula involving two conditional expectations。 We can in fact compare our resulting expression with the previous analytical formulas in a bit more details。

 Let's write it once again as a product of the inverse of matrix A and the vector B。 One thing that should be noted here is that because this involves a matrix inversion。 it might be a good idea to supplement this calculation by a regularization for matrix A to prevent possible numerical instabilities。 A simplest practical adjustment would be to add a unit matrix with a small regularization parameter epsilon to matrix A as shown here。

 Another point to note is that the resulting expression looks very similar to our previous analytical formula for the optimal hedge。 Indeed， both the numerator and denominator in both formulas look very similar。 the only difference being in the presence of basis functions in these expressions。 These basis functions in this formula do exactly what we want them to do。 Namely。

 they implement conditioning on the whole set of Monte Carlo parts that we needed to compute optimal hedges。 Now our formula for phi and t gives us a solution for the optimal action A* of x at time step t when substituted back to the expansion of A* in basis functions。

 Our next task therefore will be to find a way to compute coefficients omega and t that determine the optimal Q function。 Let's do it to our next video。

![](img/1ec91f7b6e8e4c9c805717f3bb5fc033_1.png)

 [BLANK_AUDIO]。

![](img/1ec91f7b6e8e4c9c805717f3bb5fc033_3.png)