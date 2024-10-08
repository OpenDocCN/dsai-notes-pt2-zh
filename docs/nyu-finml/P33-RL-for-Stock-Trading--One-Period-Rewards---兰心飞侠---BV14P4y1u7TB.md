# P33：RL for Stock Trading -One Period Rewards - 兰心飞侠 - BV14P4y1u7TB

 Next， we want to specify one period reward， or negative costs， in our model。

 An instantaneous random reward received upon taking such action is obtained by substituting the equation for its own。

 shown as the first equation here， into the equation for the portfolio change that we derived here there。

 This produces an instantaneous random reward received upon taking action you'd seen。

 given by equation 13。 Please note that because of the market impact term proportional to metric Mt。

 this equation is quadratic rather than linear in action you'd seen。

 The other thing that we can see from this equation is that rewards are risky。

 as they depend on the noise term epsilon t。 Therefore。

 we will add the certain risk penalty to compensate for this risk。

 A risk penalty is simply a negative reward received for taking risk in trades。

 We will use a very simple specification for such risk penalty。

 and we'll take it to be proportional to the variance of the instantaneous reward R0。

 conditional on the given values of Xt and ut， as shown in equation 14 on this slide。

 Here lambda is a risk aversion parameter。 This variance is easily calculated and this produces the last expression here。

 We can see that this is a quadratic function of the sum Xt plus ut。

 Because the covariance matrix of noise is non-negative definite。

 the whole expression is non-positive definite quadratic form。

 The next element we have to include in the one-step reward is a penalty for fees。

 or transaction costs。 Now transaction costs depend on a sign of ut。

 because traders buy for a bid price and sell for an ask price。

 This can be taken into account by using different proportional transaction costs。

 for positive and negative values of ut。 And to handle this we represent each component ut as a difference of two non-negative values。

 ut plus and ut minus。 Then ut becomes a difference of these two values。

 while the absolute value of ut becomes their sum。 In other words ut is equal to ut plus when it's positive。

 and it's equal to minus ut minus when it's negative。

 Now with these definitions we can specify a shown in equation 17 on this slide。

 where kappa plus and kappa minus are different transaction cost parameters to buy and sell for buy and sell orders。

 And finally we have to incorporate market input defects from trading in stocks。

 Here we will assume a proportional market input that is proportional to the total position in all stocks。

 It has a few terms。 Two terms are proportional to the size of the order。

 and we can in general have different coefficients theta plus and theta minus。

 that would describe such inputs for positive and negative values of u。

 In addition the market input can depend on signals， therefore we add a third term here。

 with a weight given by some matrix fee。 Finally we collect all these contributions together and define the total one step reward as their sum。

 as shown in equation 18。 Please note that this is a random reward as the first term here depends on the noise absolute t。

 The rest of the terms is non-random for given values of x， t and ut。

 Now when we are given the next in ut， which is equal to the difference of ut plus and ut minus。

 we can define and expect it one step reward as an expectation of the expression given by equation 18。

 This produces equation 19 for the expected reward r hat t。

 Here our zero hat is an expectation of the instantaneously reward r zero conditional on a given state and action。

 as shown in equation 20。 We can now simplify this expression and bring it to a more compact form。

 which will be shown next。 So here we use a vector notation to descend and introduce a vector at of size 2m。

 which is made by stacking together， components ut plus and ut minus。

 Then the whole expression for the one step reward can be expressed as a quadratic functional of x t and at。

 which is shown in equation 21。 We have three second order terms here and two first order terms proportional to x t and at respectively。

 There is no constant term here because there is no reward without taking an action at or having a position x t。

 Please note that matrices are a t， are x x t and are a x t depend on risk aversion lambda。

 They also depend on market input matrix m and phi coefficients theta。 If all of them are equal zero。

 then the one step reward becomes a linear functional instead of a quadratic functional。 For example。

 we have a quadratic functional and we have a quadratic functional。



![](img/18593f0523ef79a40d6fdd4d434d7210_1.png)

 We have a quadratic functional。

![](img/18593f0523ef79a40d6fdd4d434d7210_3.png)