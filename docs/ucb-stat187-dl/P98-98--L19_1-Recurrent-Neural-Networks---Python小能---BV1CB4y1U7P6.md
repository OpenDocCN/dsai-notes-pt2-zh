# P98：98. L19_1 Recurrent Neural Networks - Python小能 - BV1CB4y1U7P6

 Okay， so welcome to another course on recurrent neural networks。 So last week。

 we covered kind of the basics a little bit， why you actually need recurrent models。

 What the difference is between latent variable models and， models without latent variables。

 And what we effectively saw is that latent variable models can be。

 a really convenient way of dealing with the fact that you need to。

 aggregate in some way all the past state of what you've seen so far。

 And aggregate that in some variable that helps you to make predictions of what。

 you're going to see next。 And the key distinction really was that you can either just have the past。

 k terms as an embedding or you can have a latent variable。

 And if you have to pass k terms as an embedding， this makes training really easy and we actually saw what happens。

 But then you may not have a lot of fidelity。 On the other hand， if you have a latent variable model。

 you have a little bit more freedom in terms of what you can stuff into that。

 variable and then it may potentially work better。 So in the ideal case。

 this will store the sufficient statistics of all the past observations。

 So today we're going to actually see a little bit how those models behave in， practice。

 how we engineer some of them。 And let's see how far we get， probably we'll get to at least a basic。

 latent variable model， maybe we'll get to a GRU。 Unlikely that we'll cover the STMs。

 let's see how we go。

![](img/0a9d29a230d7e01a1a4d4526a4c14de9_1.png)

 So let's just recap。 Basically， what we assume is that we have some function F。

 which compresses all the information from X1 up to Xt minus 1 into some state ht。 Of course。

 if we compute that explicitly and T ranges from 1 to 10，000， this is super expensive。

 so you don't want that。 And what we do is we basically engineer this function F to be 1 that takes。

 as its inputs the previous statistic， ht minus 1。 And the previous observation in order then to allow us to make inference p of ht。

 given ht minus 1， xt minus 1， and also p of xt， given ht， and xt minus 1。

 And so we just move forward from the left to the right in this grid。

 So really the differences between width and， without latent variables are kind of subtle。

 but the implications are quite profound。 And essentially， maybe about a decade ago。

 I would have talked to you a lot about， how to do efficient inference in such models how to scale this up using graphical。

 models tools。 There are really a lot of beautiful mathematical constructs for it。

 The reason that we are pretty much skipping this and going right into deep。

 learning is actually twofold。 First of all， those models that we would be using are probably not true anyway。

 right？ So I mean， after all， they are models， right？ In very few cases。

 do you know that you really have 10 clusters as a latent state？ You don't know that。

 It's just a modeling assumption。 Secondly， while you then may have that。

 and you can maybe even specify it， you might not be able to do inference efficiently anyway to get an exact outcome。

 And so the fact that first of all， you shouldn't trust your model anyway。 Secondly， even if you do。

 you might not get the true answer either。 You might as well decide， well。

 since I don't know the truth and， even if I knew it， I couldn't get it。 Well。

 let's just do the best thing that an engineer would do， namely。

 try to engineer the best model that we can actually get our hands on。

 And that's to some extent why deep networks are now quite popular at。

 the expense of graphical models， at least in some applications。

 There are some cases where graphical models are still superior。

 especially if you have very specific structure that you can efficiently exploit。 But short of that。

 it gives you a bit of a background of why you care。 Any questions so far？ Yes？

 >> The graphical models be combined with neural networks in a way that。

 you have some major ability that you can graph the model while still having。

 the expressive power of the deep neural number？ >> So the question was。

 can you combine both and get the best of both worlds？ And indeed you can。 So for instance。

 there's this quite famous paper from， Cabbie Murphy about using a conditional random field in combination with。

 basically lower level image pre-processing to， for， instance， perform segmentation。

 And this paper is a really cool paper。 It has a couple of thousand citations， so。

 that's actually rather remarkable， given that it's only like maybe two， three years out。

 It turns out that by now the paper is getting the citations not because。

 the conditional random field part that sits on top， but。

 because of the essentially dilating convolutions where you up sample， the feature map。

 which is something， it's kind of a side remark and， quite trivial in an engineering solution。

 And by now it's getting the citations because of that and， nobody really uses a CRF anymore。

 they just go all the way straight to a deep learning。 So only if you really， really。

 really must have interoperability， or， if you have a very narrow setting where you know that specific graphical。

 model is really true， would I recommend that you build such a hybrid approach？

 But you'll pretty much know that you have this case if you have it。 Yeah。

 so this is kind of both quite liberating， but also very sad。

 Sad because a lot of tooling is now no longer so relevant， but。

 also liberating because it makes things a lot easier。

 Before that it used to be that you have this fancy model and。

 then you basically get a PhD student and you have him spend three months on。

 working out the math both either a sample or a variational inference。

 implement it write a paper and you do that five times。

 Papers are guaranteed because the math is not trivial and then you graduate， right？

 Or maybe it takes two， three years， but， this was a very predictable way of graduating。

 Unfortunately that angle no longer works so， well because they're easier tools。



![](img/0a9d29a230d7e01a1a4d4526a4c14de9_3.png)

 Anyway， so required models with hidden state。 In the simplest case。

 you could have something like this。 I have hidden state h t which is just given by some function phi of。

 I have matrix vector w times h plus matrix vector for， w times the pass observations and some bias。

 And then for the output， again， I just take some nonlinear function of the hidden state。

 So this is about as primitive as it goes and， you can use that for a simple RNN。

 And this is essentially not much more complex than a multi layer perceptron。

 except that you walk through it one step at a time。

 And the other thing is I distinguish between output and observations。

 In many cases I might want to use the output to generate the next observation and， go through it。

 but that's not necessarily the case。 For instance。

 if I want to annotate a text sequence for named entities， my input。

 so the observations are the words。 The explanation of the hidden state is then whatever that hidden state is。

 And the output would then allow me to generate named entity annotations， right？

 So that's why it makes sense to distinguish those two pieces。



![](img/0a9d29a230d7e01a1a4d4526a4c14de9_5.png)

 Okay， and so now let's actually have a look at this in terms of code because。



![](img/0a9d29a230d7e01a1a4d4526a4c14de9_7.png)

 it's really straightforward。