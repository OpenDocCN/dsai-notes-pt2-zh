# P40：40. L9_2 Covariate Shift - Python小能 - BV1CB4y1U7P6

 >> Qouserative correction。

![](img/3d44a4e9abffe620619bea169d4dbb38_1.png)

 Let's take our training set again， right？ So cats and dogs。 And what could possibly go wrong？ Okay。

 so we pulled our classifier。 So it tested。 Right？ And of course this doesn't work at all， right？

 Because it doesn't recognize that kind of cats。 And so you think， well， you know。

 this is like obvious。 Why would anybody do this？ You know， how could you possibly be so naive？ Well。

 here's a couple of examples。 So in web search， let's say you want to build a search engine。

 and maybe you have some page relevance data for the， search engine。 But now you decide， okay， well。

 my search engine is getting， really popular in Canada and the UK and Australia and so on as well。

 Not even talking about countries with different language， but even， all markets that speak English。

 You know， the search relevance may not be the same。 So for instance。

 you would imagine that Canadians are maybe， more polite， care more about bears in the queen。

 and maybe， then， you know， the royal mounted police， right？ So you can clearly see that， you know。

 the search results ought to be， slightly different。 Or in speech recognition。

 let's say I train this thing with a， west coast accent and then I want to deploy this and I deploy it。

 let's say， in Texas， right？ Or worse， I deploy it on people like me who don't speak native， English。

 right？ And then the speech recognizer fails。 I guess most of us probably had that problem at some point where。

 you called some hotline and they told you to say， hey， this is。

 the new voice operated system and you started getting really。

 mad at that voice operated system because it wouldn't understand， you， right？

 And that's covariate shift。 Because the reference distribution that the system was trained on。

 people like most of us here in this room。 Or even things have different names， the same thing。 So。

 you know， a soda is called a pop or a coke or other things。

 and that differs even within the same country。 So， here's a distribution of names for soft drinks。

 right？ And so different parts of the United States and it's red and， blue divide。

 That's different from the usual one that you would have seen。 Yeah。

 people call things pop and coke and soda。 All right， obviously， you know， near Atlanta。

 they call it coke， because， well， you know， coke is there， but nonetheless， there's。

 quite some variety。 So， even if you build a voice recognition system and let's。

 say you build it in California and then because you have another， research lab in Boston。

 Massachusetts。 And then your system will work very well if things call the soda， right？

 But they won't work for the rest。 So， this is kind of funny。 Well， these are not so funny things。

 So， the first one is something that actually happened。

 Let's say you're a medical startup and you want to design a。

 blood test to find out whether somebody has prostate cancer。

 It turns out it's fairly easy to get blood samples from sick old， men to。

 because they're sick and they say， hey， look， if you can， find a blood test to detect this earlier。

 well， you know， that's， really good。 So， sick people are usually very willing to donate， you know。

 their blood， right？ And then they realize， well， okay， we have this tiny issue we。

 don't have enough data from healthy men。 And that actually has some ethics quandaries because。

 you know， if you just sample blood and you find out， well， this person， might be sick。

 but you don't know whether you should try to， you， know， trust your tests。 So。

 do you call this guy up and， you know， scare the heck out of， him and say， hey， look。

 our test is set and you might have， cancer， but we're not sure。 On the other hand， well。

 do I shut up and let this guy maybe die， right？ So， it's not easy to get that data。

 Long story short， they had this brilliant idea of， because they。

 were on a university campus and students are a cheap bunch and， for， I guess， a free beer。

 They are willing to donate a small amount of blood。 So。

 they got a lot of this blood and got it analyzed。 And then they came to me and said， Alex。

 can you help us build a， classifier？ And I told him， yes， I could。

 And it would probably work really perfectly and it would be， perfectly useless because， well。

 their healthy population were， essentially men in their 20s who probably work up more and drink。

 more and our university students and stuff like that。 And the other。

 the sick distribution are old men with prostate， cancer and a classifier of old against young would work really。

 well， right？ So， this is covariate shift that， well， basically they blew their。

 last available cash on this and that was the end of that startup。 Mind you。

 it was run by a couple of university professors but not， solicitions。 Another case。

 reinforcement learning。 Let's say I train on data gathered with， you know， the。

 current policy and then， you know， my policy changes because， you， know。

 I'm getting better at playing StarCraft or slaying。

 monsters or controlling the AC system in my service center。 And so now a test time， well。

 because the environment， responds to that， well， you know， maybe my algorithms don't work。

 so well anymore。 There's a lot of interesting work about replay buffers on and of。

 policy learning and propane's discoring there。 So take a class of， I guess， Peter， Bill or Sege。

 Levine， and， you， know， you'll get a lot more of this。 And then there's things like， for instance。

 databases。 So let's say we build a self-learning database， self-tuning， database。

 And this is tuned on， you know， 2017 usage patterns and then you， deploy it and you deploy it。

 so I should have probably updated， it to 2019 but if I deploy it in 2018 then 2017 pattern might。

 still be slightly different。 So my algorithms will no longer be optimal。 Long story short。

 covariance is real and it's pretty much by， default assume that you have a problem of that kind。

 So let's look at the math。 So the training risk and right now I'm assuming I have， you know。

 infinite amounts of data so let's not worry about that。

 Rather so much but I basically minimize the integral dx to。

 dx p of x dy p of y given x of some loss。 But it tests time and I'm assuming that p of y given x so。

 you， know， what the correct label is for given data。

 That doesn't change between training and test time。 So for instance， talking about， you know。

 sick men， well， they are， sick regardless， right？ But I just have a lot more of one kind than the other。

 So it tests time。 I don't have the integral dp anymore but I have an integral， dq。

 And so what I really should have done is I should have minimized。

 an empirical risk relative to data drawn from the q distribution。

 But obviously I don't have the labels about test time。

 So what I can do is it's actually very simple dx q of x f of x。

 I can write it as dx p of x and then I have q of x over p of x， times f of x。

 So I have basically that ratio q of a p。 Now if you've taken measures theory class， you'll probably。

 hate me for putting this equation up because what you'd really。

 need is the rather nicodeum derivative dq dp。 But we are not going to worry about those details here。

 So if you are so inclined and you've done measure theory， yeah。

 there's a cleaner way of writing it but just for now let's just， look at that。

 And so the problem is now you need that density ratio。 And one way of going about it is well。

 I estimate p。 I estimate q。 Then I take that ratio and then it doesn't go well。 Right？

 Because density estimation is really， really， really hard。 Don't do that。

 Instead it turns out that getting the ratio of those two， instis is much easier to obtain。

 Now I'll show you how to do this and you'll actually do that in， your homework in detail。



![](img/3d44a4e9abffe620619bea169d4dbb38_3.png)