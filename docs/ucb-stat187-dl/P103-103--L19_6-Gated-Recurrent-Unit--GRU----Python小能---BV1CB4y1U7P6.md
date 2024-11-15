# P103：103. L19_6 Gated Recurrent Unit (GRU) - Python小能 - BV1CB4y1U7P6

 are ready to talk about the GRU。 So this is the first non-trivial recurrent system that we're going to encounter。

![](img/07142cc248762e68020f8b751b38953f_1.png)

 And effectively， this is the intuition of it。 And actually， it happened a lot later than the LSTM。 But the motivation was waiting to see whether you can get most of the benefits of an LSTM。 but with less computation。 So the point is a little bit that if you have a sequence。 then not all observations are equally relevant。 So for instance， if I scratch my head。

 that's not very relevant。 What I'm talking about hopefully will be more relevant。 So therefore。 you may very well decide to forget the fact that I scratch my head。 or it will never even really enter your memory because， well， what does it matter， what Alex does。 what matters is what's on the slides。 But so therefore， you need two mechanisms。

 You need one mechanism to decide when to pay attention。 So basically when to update your state。 And you need another mechanism to decide when to forget。 So this is like， this is a reset gate。 And only by having those two pieces can you then start to manipulate your state in a meaningful way。 So for instance， if I have a mechanism which prevents me from paying attention for ten steps。

 then my gradient of the hidden state with regard to the output will just go straight through those ten steps。 and not be affected by anything， right？ Because I've basically kept the variable constant。 At the same time， if I decide to forget， that's like running detach but using math for it， right？

 So detaching the gradient just， well， forgetting the hidden state does the same thing as the detaching。 Okay， it sounds a little bit abstract， but is the basic functionality of why you might want to have an attention in the forget gate clear？

 Everybody cool with this？ Good。 So， let's see。

![](img/07142cc248762e68020f8b751b38953f_3.png)

 Let's actually look at， let's fill this up directly as we go along。 So I have some hidden state。 ht minus one， and have some input xt。 And I go and take those two things and now I send them to a yet to define。 to be defined reset gate and an update gate。 And those two things are essentially going to be just a linear function of the inputs。 then some nonlinearity。 So this nonlinearity sigma。

 I will conveniently choose it in such a way that its values are between zero and one， such that。 you know， I can essentially switch those gates on and off， right？ So， for instance， you know。 something like a tangent might do something， well， not quite， but if I shift it， it will。 So that's the reset and the update gate。 Okay。 Everybody cool with that？ Okay， yes？

 Is using a reset and update mechanism similar to the gradient shift correction adapting to time？

 I'm not sure I see that connection right now between comparative correction and reset and update gate。 Maybe， maybe we can talk about that another time。 I'm really not seeing that connection。 Yes？

 Are they always like straight forward， fully connected？ Very good question。 In the basic units， yes。 Now， the obvious question is， you know， what would you do if you had something else like an image？

 You would almost certainly want to do something smart in terms of convolutions， right？

 And I think there are one or two papers which did this and it helps。 If there's any data type for which this hasn't been done yet， you should totally write that paper。 It's a very， very profound insight。 It's good。 So the question is basically。 do we always have something fully connected？ And the answer would have to be， well， no。

 if you can avoid it or not。 For instance， if you want to pay attention to parts in an image， right。 then you could essentially have that， let's say， you have a frame of images。 then I would basically have a convolution here。 So， okay， so we have our gating。



![](img/07142cc248762e68020f8b751b38953f_5.png)

 The next thing that we need is we need to have some candidate-hidden state。 Okay。 and so in this candidate-hidden state， what I'm doing is I'm basically computing， you know， some。 you know， x times w。 So that's basically input times some linear function。 It's a matrix。 so it's some linear function of the input。 And I have a bias because here everybody likes biases。

 right？ And then， well， I need to take the previous-in state。 But what I'm now doing is I'm using the reset gate to decide by how much I'm actually going to incorporate the previous-in state。 So if that reset gate is zero， then I'm just going to use as my candidate-hidden state stuff that only depends on my current x_t and the bias。 right？ So in other words， if my reset gate is zero， I'm resetting my， you know。

 recurrent neural network。 If the reset gate is one， I mean。 incorporating it as I would have done before otherwise。 So remember in our RNN we had exactly linear function of x and w， and h gives us， you know。 h_t plus one。 Now， the only thing is this is a candidate-hidden state。 Candidate because， well。

 besides the reset gate， we need to decide whether we are even going to bother updating。 And so that's the last part。

![](img/07142cc248762e68020f8b751b38953f_7.png)

 Namely， I compute my hidden state by just taking a convex combination of the past hidden state and the candidate-hidden state。 So if z_t is one， it means basically I'm not going to update， right？

 Because I'm just going to use h_t equals h_t minus one。 If z_t is zero， then， well。 I'm going to update entirely。 So the biases that are built in， if you think about it， are that。 you know， z and r are zero。 So if r is zero， then I'm just going to reset。



![](img/07142cc248762e68020f8b751b38953f_9.png)

 So my bias is not to take the past into account too much。

![](img/07142cc248762e68020f8b751b38953f_11.png)

 On the other hand， my bias there is to update whatever I have rather than just skipping the update entirely。 Okay。 So this was maybe a lot。

![](img/07142cc248762e68020f8b751b38953f_13.png)

 Let's just summarize all the math。 Okay。 Yes？ >> It seems kind of similar to， like。 the residual layers of z and that。 Like， why can't we just do something simple like that where we just --。 >> [inaudible]， >> Right。 >> [inaudible]， >> Okay。 >> [inaudible]， >> So， first of all。 the residual connections will come back because you can also use recurrent neural networks with residual states。

 You mostly use that if you stack the RNAs up multiple layers。 which we may or may not get the chance to cover today。 But that -- we'll discuss residual units。 Now， effectively， yes， so you could engineer in a slightly different bias such that， you know。 by default， it'll just not change the hidden state at all。 Right。 And to some extent。

 that would be just that by default， you know， ht minus one equals ht。 Right。 And， you know。 if I said， you know， zt equals one， that actually is what happens。 But I could have just maybe flipped that last equation to have ht minus one times one minus zt and htilde t times zt。 My guess is somebody at some point tried it out and it worked a little bit less well and that's why everybody agreed on the GRU parameterization。

 But I wouldn't be able to point out a paper that says， well， hey。 we tried out those two options and this one worked better。 There is one paper from Google Brain。 so by Softfendler， where they use essentially a genetic algorithm to search over a insane state space to come up with the perfect hidden cell。 And they come up with a hidden cell of about 40 units。 Okay。

 The fact that you haven't heard of the cell tells you probably everything that you need to know about it。 While it works ever so slightly better， it didn't work amazingly much better。 but it was amazingly much more expensive。 So the other thing is you've probably heard less of a GRU than about LSTMs。 And that's because GRU's work ever so slightly worse than LSTMs。 So you might wonder， you know。

 why the heck is Alex teaching us the stuff that doesn't work， right？ Well。 it's not that it doesn't work。 There are quite a few cases when it works just as well。 And in those cases， the GRU is much preferable because even so this story looks plenty complicated。 it's still cheaper than simply than the LSTM。 And I'll walk you through all the details for the various things as we go along。

 but this is just as a heads up of why people do one or the other。 Yes？

 >> Why do you stick like the activation？ >> Okay。 So it's a very good question。 So first of all。 those sigmas， these are essentially activation functions that map the input into an output that goes between 0 and 1。 That's just engineered in such a way that I get convex combinations， right？

 So if I want to have a convex combination， I need to have a value between 0 and 1。 I'm fairly confident people at some point tried what happens if you make the range larger and they found that the network diverges or does something else terrible。 And then they went back to this。 But this is a good question and one way to find out is simply to hack the Python code and just modify it and see whether the network works better。 Now， the tang is another one of those cases where you have to think about， you know。

 why would I bother？ Well， actually that's -- okay， so here's the reason。 So tang maps everything into the range between minus 1 and 1。 This is a very desirable property to have for a hidden state， right？

 Because you want your hidden state to be of a meaningful value and you don't want it to diverge。 You know， so tang， you know， around the origin is nice and linear， so everything just goes through。 At the saturation points at least it prevents it from exploding。 With otherwise training those networks is a royal pain。 Again。

 whether tang is the optimal function is， you know， a matter of personal taste。 at least you still get some tiny amount of gradient even for large activation values。 But is there a chance that somebody comes up with something better？ Of course。 And if you look at basically what happened with ReLU versus， you know， sigmoid activation。

 this was such a simple trick and it made all the difference。 For essentially modern deep networks。 This plus dropout is pretty much， you know， I think one of the key reasons why Joffin also got the Turing Award。 right？ I mean， and it's very simple math。 Yes？



![](img/07142cc248762e68020f8b751b38953f_15.png)

 >> Can you go to the previous slide and contrast it？ Is like the whole slide？ >> Yep。 Okay。 so this is the candidate hidden state， right？ This is not our hidden state yet。

![](img/07142cc248762e68020f8b751b38953f_17.png)

 So it's H tilde。 And now I'm using H tilde to update the actual hidden state。 So I could have just written everything in one equation， right？





![](img/07142cc248762e68020f8b751b38953f_19.png)

 So if you look at the last two lines， I can basically inline that， right？

 I could basically write H t is z t， you know， point to right product with H t minus 1。 plus 1 minus z t， point to right product with， you know， the right-hand side expression， basically。 the tangent， everything that follows。 I could have inlined out。 You're， you know。 deep learning framework may very well do that in practice。

 But it just looks ugly and it's hard to understand， but this。 there's nothing particularly deep in there。 Yep。 Any other questions？ Yes？ >> Okay。 >> Okay。 So。 okay， so the question was basically， you know， how does network know how to remember and how to forget？

 Okay， so if you look at that， so R t， if R t is zero， right， then it completely nukes H t minus 1。 So that's the third line from the top， right？ So if that happens， then H tilde t only depends on x。 And without it forgets。 I did forget anything that it's seen in the past。 >> I mean。 if H tilde t equals， but not， if x is， if H t minus 1 is R t will be zero。 >> Okay。 So， well。

 what you can have， well， the other part is simply then to look at， well， the update function。 so z t， the update gate z t。 So if that is z to， well， c， to 1。 then I'm not going to update anything， right？ But if I'm setting it to zero。 then I'm going to use all of H tilde。 So， basically， if z is zero and R is 1。

 then I'm back to the plain vanilla R-n in equations， right？

 So that's the one that we did on Tuesday。 On the other hand， if I set H， well。 R to be zero and z to be 1， then I'm back in a model that doesn't have a hidden state。 Or it has a constant hidden state， so which makes this entire point less， right？ Yes？

 >> So you said that if R is zero， it's going to forget the Ruby state。 >> Correct。 >> But if R is zero， z has to be 1 for that to happen。 >> Yes， strictly speaking， you're right。 So。 basically， those two things are coupled。 Yes。 Very， very good observation。 Right。 So。 because otherwise， what I could simply have is R is zero， z is 1。

 and I still carry that state around。 Right？ So， that's the name is maybe ever so slightly misleading in terms of high parameterized。 >> What's the reason for having， like， this two step candidate， then， like， one move？

 >> There's no particular reason。 Besides the fact that people probably tried out 10 things in this one of our best。 why could I not do any algebraic transformation？ Of course， I can， right？ So。 as long as the math is identical， the same thing gets executed， so that's not the problem。 But I would suggest that if you have an idea of， you know， how to build a better， you know。

 R and N cell， that you actually go and build one。 As a matter of fact。 I was discussing that with Moo and a colleague of mine over lunch。 And we have some idea of something that we want to try， but we don't know yet where that will work。 But it's basically a rather weird idea of what to use。 So， yeah， I mean。

 this idea is maybe four years old。 And let's actually see a little bit how it works in code。

![](img/07142cc248762e68020f8b751b38953f_21.png)

 [BLANK_AUDIO]。