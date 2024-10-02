# P22：RL Approach - Week Introduction - 兰心飞侠 - BV14P4y1u7TB

 Welcome to the third week of our course on reinforcement learning and finance。



![](img/62c1f18e71db8d94877788fe39e23dd2_1.png)

![](img/62c1f18e71db8d94877788fe39e23dd2_2.png)

![](img/62c1f18e71db8d94877788fe39e23dd2_3.png)

 This week is going to be very interesting。 As in this week we will leave a model-based approach of dynamic programming and move to。

 data-driven and model-independent ways to solve our problem of optimal option pricing and hedging。

 Now I need to specify what I mean by model-independent here。

 given that we still discuss a model for， a Markov decision process。

 What is meant in this context by model-independence is that in a data-driven setting we only keep。

 the general structure of the model but we do not assume that transition probabilities and。

 reward functions are known。 The traditional paradigm of quantitative finance is that in order to optimally price and hedge。

 financial assets we first have to build and estimate a model of the world。

 But reinforcement learning paradigm is different and it allows us to focus directly on our。

 prime goal of optimal control。 Depending on the particular algorithm that we use。

 the task may or may not involve the， problem of building a model of the world first。

 Methods that we are going to discuss in this week actually let us do things in a model-independent。

 way。 We will start with a look at batch-mode reinforcement learning and then we will introduce Q-learning。

 one of the most famous algorithms of reinforcement learning。

 After presenting the basic version of the algorithm we will discuss its more practical。

 version called fit-of-cute-ration。 All these will be presented not in an abstract way but rather directly within our MGP model。

 of option pricing so we will immediately see how they work in a financial setting。

 In your homework for this week you will implement these solutions and see how they work in practice。



![](img/62c1f18e71db8d94877788fe39e23dd2_5.png)

 So let's get started。 [BLANK_AUDIO]。