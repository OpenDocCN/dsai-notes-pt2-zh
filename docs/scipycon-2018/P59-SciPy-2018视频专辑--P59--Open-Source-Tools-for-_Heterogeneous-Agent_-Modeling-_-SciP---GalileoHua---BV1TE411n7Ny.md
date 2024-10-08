# P59：SciPy 2018视频专辑 (P59. Open Source Tools for _Heterogeneous Agent_ Modeling _ SciP - GalileoHua - BV1TE411n7Ny

 Thank you for joining us if you have just arrived in the second half here。

 So now we have a presentation on， as the title says， HARC， open source tools for heterogeneous。

 agents modeling。 Only fit to you。 Thank you everyone for coming here。

 For those of you who don't recognize me from TV， my name is Matt White。

 I'm an assistant professor of economics at the University of Delaware。

 For those of you who do recognize me from TV， bad news， your televisions is possessed or。

 otherwise malfunctioning because that shouldn't have happened。 Just by show of hands。

 so I know what kind of audience I'm speaking to， how many of you， and my hands。

 I mean plural for each person so I can see you， how many of you have a background。

 in economics at the graduate level？ So I know I've got DJ and Rick。 A few others。

 And the rest of you are social scientists。 Engineer types？ Okay， great。

 So I wrote these first bits assuming they would mostly be engineer types。 So for you economists。

 you're going to kind of understand what I'm talking about。 For you engineers。

 I'm going to try to put the beginning part in the language that you， understand。

 So to give you some background as to what it is that we're talking about here about dynamic。



![](img/9ea5c2cb03436ef757c558f33faae725_1.png)

 economic modeling in general。 So this is beyond the scope of heterogeneous agents modeling。



![](img/9ea5c2cb03436ef757c558f33faae725_3.png)

 We're effectively talking about an optimal control problem for people。



![](img/9ea5c2cb03436ef757c558f33faae725_5.png)

 People making decisions or more generally firms or agents making decisions where it。



![](img/9ea5c2cb03436ef757c558f33faae725_7.png)

 could be consumers， households， firms， banks， whatever。



![](img/9ea5c2cb03436ef757c558f33faae725_9.png)

 The elements that characterize what a dynamic model is， you've got a state space， situations。

 in which you could find yourself， you've got a control space， different actions you， could take。



![](img/9ea5c2cb03436ef757c558f33faae725_11.png)

 You face some set of constraints as to what choices you can make in what states。

 There are some risk or uncertainty that happens to you。

 There are some shocks that happens to you over time and you have some conception of those。



![](img/9ea5c2cb03436ef757c558f33faae725_13.png)

 shocks。 There are some conception of dynamics， how states， controls and shocks generate next。



![](img/9ea5c2cb03436ef757c558f33faae725_15.png)

 period state or I should say tomorrow's state。

![](img/9ea5c2cb03436ef757c558f33faae725_17.png)

 It might be the next period， discretely or the next infinitesimal fraction of time forward。

 in a continuous time model。 And in some， in traditional economics I should say。

 there's always some concept of preferences， how agents feel about sequences of events that could happen to them。

 streams of experience， that could happen to them。

![](img/9ea5c2cb03436ef757c558f33faae725_19.png)

 More broadly， agents， whether it's an a traditional economics model of optimization or in so-called。



![](img/9ea5c2cb03436ef757c558f33faae725_21.png)

 agent based modeling， they always have some model of how do agents process information。



![](img/9ea5c2cb03436ef757c558f33faae725_23.png)

 and how do they make choices。 In traditional economics， how do they make choices？



![](img/9ea5c2cb03436ef757c558f33faae725_25.png)

 The answer is they optimize on some problem。 There is some utility function that they're trying to maximize in a dynamic sense and they。



![](img/9ea5c2cb03436ef757c558f33faae725_27.png)

 try to optimize on that。 In other models， there could be other decision making frameworks。

 But broadly speaking， that is the entire world of economics。



![](img/9ea5c2cb03436ef757c558f33faae725_29.png)

 For those of you who didn't get your PhD in economics， you basically just got it。



![](img/9ea5c2cb03436ef757c558f33faae725_31.png)

 Good enough。 Classifying kinds of models just to give you some sense of the delineations we're drawing。



![](img/9ea5c2cb03436ef757c558f33faae725_33.png)

 here。 We could be talking about infinite horizon versus finite horizon。

 Do agents think that they could live forever even with an infinitesimally small possibility？

 Or do they know that there is some definite end of their problem beyond which they cannot。



![](img/9ea5c2cb03436ef757c558f33faae725_35.png)

 live？ Do the classification time based is simply， are we talking about discrete moments in time？



![](img/9ea5c2cb03436ef757c558f33faae725_37.png)

 Like I'm moving from 2017 to 2018 or Q1 2017 to Q2 2017 or we're talking about a continuous。

 flow of time。 There are very， very different types of models。

 And so we're all going to be talking about discrete time models today。



![](img/9ea5c2cb03436ef757c558f33faae725_39.png)

 And for the non-economists in the room， it will shock you to know that many economic。



![](img/9ea5c2cb03436ef757c558f33faae725_41.png)

 models， particularly in matter， solely in macroeconomics， abstract away from any sense。



![](img/9ea5c2cb03436ef757c558f33faae725_43.png)

 of humans being different from each other。

![](img/9ea5c2cb03436ef757c558f33faae725_45.png)

 They say， well， we， with some fundamental results and some less than judicious assumptions。

 we find that individual level risk does not matter so we can lump all consumers together。



![](img/9ea5c2cb03436ef757c558f33faae725_47.png)

 as the representative consumer。 And all firms together as the representative firm that hires the representative consumer。

 to produce the representative output。 As normal humans。

 it will not surprise you to learn that the assumptions that led to。



![](img/9ea5c2cb03436ef757c558f33faae725_49.png)

 this were probably one of the background factors in what led to the Great Recession， as Jani。



![](img/9ea5c2cb03436ef757c558f33faae725_51.png)

 Yellen and other smart people have since come to realize。



![](img/9ea5c2cb03436ef757c558f33faae725_53.png)

 In the class of models that we're talking about here， we're talking about models with。

 heterogeneity。 People are different from each other。

 both in the ex-ante sense that they might have different。

 preferences or they might be different types of agents entirely。



![](img/9ea5c2cb03436ef757c558f33faae725_55.png)

 One agent is a firm， another type is a consumer。

![](img/9ea5c2cb03436ef757c558f33faae725_57.png)

 But also ex post heterogeneity， different streams of random shocks happen to them along the way。



![](img/9ea5c2cb03436ef757c558f33faae725_59.png)

 So there's a whole distribution of outcomes and the distribution of states that people。



![](img/9ea5c2cb03436ef757c558f33faae725_61.png)

 find themselves in matters。 And in some models， what differentiates this from what engineers might think of as an optimal。

 control problem is that some of the things that individual agents take as exogenous to。

 them about dynamics are in fact endogenous to the entire system。

 That the actions and states collectively of all agents is what generates those dynamics。



![](img/9ea5c2cb03436ef757c558f33faae725_63.png)

 that I can treat personally as me as exogenous。 And so you need to find。

 have some sort of rule for how agents form their beliefs about。

 those dynamics and an equilibrium means that there is a consistency between how agents。

 form their beliefs and the reality that comes out of when agents act on those beliefs。



![](img/9ea5c2cb03436ef757c558f33faae725_65.png)

 So background。

![](img/9ea5c2cb03436ef757c558f33faae725_67.png)

 So suppose you wanted to get started in heterogeneous agents macroeconomics and imposing equilibrium。



![](img/9ea5c2cb03436ef757c558f33faae725_69.png)

 conditions on how agents make their optimal choices on a micro level， how those combine。



![](img/9ea5c2cb03436ef757c558f33faae725_71.png)

 to macro dynamics and how that feeds back into micro level beliefs。

 You can do this in 10 easy years。 It's really， really great。 All you need to do is go to your PhD。

 learn the history of economic modeling and where， the frontier is。

 Also along the way have picked up some software development and basic programming skills to。

 understand computer programming， maybe at the undergraduate level， maybe because you'd。

 like it for fun。 You need to learn numeric methods， root finding， optimization， interpolation。

 random number， generation。 It's sort of the basic building blocks of how you would do these things independent of whether。

 you're doing economic modeling or something else。 Things you learn specifically at the economic level or dynamic economic level。

 how we execute， specific solution methodology。 And then on top of that。

 there's a whole layer of secret sauce or trade secrets or I。

 sometimes think of it as a cult knowledge that is not really ever conveyed to you。



![](img/9ea5c2cb03436ef757c558f33faae725_73.png)

 It's not in any textbook。 You have to find the right people。

 So when we think about what's actually taught in economics， PhD programs， well it's really。

 just economic modeling and the history of it。 How we got here and what we now believe and what's on the fringe and what's next。

 If you are lucky enough to be in certain programs， you will be taught numeric methods。

 in one of your first two years courses and you'll get some exposure to dynamic solution。



![](img/9ea5c2cb03436ef757c558f33faae725_75.png)

 methodology。 There are some organizations that are working to improve， and I， Rick， yeah， okay。

 there， we go。 There are some organizations that are working to improve resources in this but mostly you。

 may be in a program that doesn't teach this at all。 Software development and the secret knowledge。

 you better hope you're at Minnesota or Johns， Hopkins or UPenn because otherwise you are just not with the right people and you're。



![](img/9ea5c2cb03436ef757c558f33faae725_77.png)

 not going to get it。

![](img/9ea5c2cb03436ef757c558f33faae725_79.png)

 So how has heterogeneous agents modeling programming done today？



![](img/9ea5c2cb03436ef757c558f33faae725_81.png)

 We economists have absolutely no sense of programming style。

 Every single thing that we do is done for today to get through the day for one particular。

 purpose and for no one else。

![](img/9ea5c2cb03436ef757c558f33faae725_83.png)

 We have no thought of the future。 At best we write for， I write for， well， until I did this project。

 I wrote for Future Matt。

![](img/9ea5c2cb03436ef757c558f33faae725_85.png)

 like two years in the Future Matt to remind myself what I did but not for anybody else。



![](img/9ea5c2cb03436ef757c558f33faae725_87.png)

 Everything is bespoke and handcrafted。

![](img/9ea5c2cb03436ef757c558f33faae725_89.png)

 We reinvent the wheel constantly。 Everybody redoes a work that's been done a hundred times。

 Documentation either isn't there， has been deleted as it's been inherited through the years。

 or is it just cryptic or apocryphal。 And this is a lot， Chris Carroll。

 the principal of this project likes to compare this to econometrics。

 in like the late 60s or early 70s where we said， "Oh， you want to run a regression？ Great。

 Go write a matrix in version algorithm and then get started。"。

 Well right now we're up until recently， we've been telling graduate students and young， PhDs。

 you know， go write your own backwards induction loops and go write your own optimization。



![](img/9ea5c2cb03436ef757c558f33faae725_91.png)

 routines because you have to start from zero unless you know the right people。



![](img/9ea5c2cb03436ef757c558f33faae725_93.png)

 So strategies for how you do this， you can get lucky and inherit a code based from your。

 advisor or now we're far enough into the future that it could be your advisor's advisor。



![](img/9ea5c2cb03436ef757c558f33faae725_95.png)

 wrote it originally in the late 80s and you don't know exactly where it came from and。



![](img/9ea5c2cb03436ef757c558f33faae725_97.png)

 also it's in 4Tran 77。 Reinvent the wheel for the hundredth time and sometimes proudly tell your advisor of this。



![](img/9ea5c2cb03436ef757c558f33faae725_99.png)

 great discovery you've made only for him or her to tell you that everybody knows that。

 It's in a footnote on a paper from 2004。 So to get to where something that was talked about yesterday by Megan Lang where you've。

 got disparate models that all add up to the ultimate model of plants and their interaction。



![](img/9ea5c2cb03436ef757c558f33faae725_101.png)

 with CO2 and the CO2 cycle and you want to put those together， if you think the economist。



![](img/9ea5c2cb03436ef757c558f33faae725_103.png)

 A and economist B their models both should be incorporated， you have to engage in a whole。

 lot duct tape coding， you know， putting those two pieces together because they were not written。



![](img/9ea5c2cb03436ef757c558f33faae725_105.png)

 with any sense of each other's existence or being used for another purpose。



![](img/9ea5c2cb03436ef757c558f33faae725_107.png)

 Why is it done this way？ Somewhat it's， I think it's。

 and this is speculation and this is why I asked whether， I was going to be filmed。

 I think it's a PhD program inertia that we continue to teach the things that we've taught。

 for a long time and we feel that we need to go through the elaborate hazing ritual that。

 is the first year economics PhD sequence and obviously there's limited bandwidth that。

 teaching economics is valuable and teaching numeric methods and solution methodology is。

 kind of seen as ancillary that well you'll just learn it if you need to learn it。

 But I think there's also some， there's going to be a little bit into the cynical about。

 it but I think maybe you can see some of your fields too。



![](img/9ea5c2cb03436ef757c558f33faae725_109.png)

 In some cases I think we are， the economics question is not particularly open in their。

 software because people want to keep their secrets secret。

 We know that inside their code there's three or five more good papers that it's the difference。

 between patenting something versus keeping it as a trade secret。

 If you think there's no way that anyone can catch up to you in science you keep something。

 as a trade secret。 If you think somebody will catch up to you in the next ten years you patent it。

 You make it public and you say this is mine。 People sit on their trade secrets because they don't think anyone's going to figure it out。

 I've literally had the shining lights of computational economics tell me you tell me what your system。

 is and I will send you the binary。 I'm not sending you my source。

 I think that's a pretty poisonous thing in academia personally。

 Also people know there's flaws in their code and they're really embarrassed about it。

 They don't necessarily know where the flaws are and so these are the rat droppings they。

 do or don't know about。 The interaction of these first two is probably the worst case scenario where what's in the。

 secret sauce， what gives it that flavor and tang。 The rat droppings。

 Sometimes you read a paper and you wonder how did they do this。

 I thought they would encounter problems X， Y and Z that ever else encounter how they do， it。

 The answer was they didn't realize they were encountering those problems and just plowed。

 ahead and got it published。 Then the other bit is that in the refereeing process it is we're focused on the economics。

 or on the field specific area。 She has time to dig through two to ten thousand lines of somebody else's code。

 Is that my five minutes？ Nobody else wants to dig through somebody else's code。

 Jean Paul Sartre says， "Hell is other people？"。

![](img/9ea5c2cb03436ef757c558f33faae725_111.png)

 I say， "Hell is other people's code。"， You don't really want to know where it comes from。

 What's our solution for this？ We are， well， the organization is called the Econ Arc which I'll tell you more about and。

 a little bit and who's supporting us。 But the first piece of this is the heterogeneous agents resource and toolkit。

 A modular， extensible， interoperable， open source， other adjectives toolkit for solving。



![](img/9ea5c2cb03436ef757c558f33faae725_113.png)

 discrete time heterogeneous agents models。

![](img/9ea5c2cb03436ef757c558f33faae725_115.png)

 Blowing by the distinction here， the line between what is heterogeneous agents macro and。

 what is structural microeconomics is completely non-existent。



![](img/9ea5c2cb03436ef757c558f33faae725_117.png)

 These are camps that really should be talking to each other because they're doing the same。

 thing and just putting a different label on it。 We're trying to provide a common framework。

 almost an API but I don't want to sound too， tacky and abuse that word。

 A common platform for people to frame their models in so that models are interoperable。

 with each other and that elements like dynamics， behavior， aggregation and belief formation。

 are all separable and modular from each other。 These things are easily swappable and easily combinable。

 If you want to know， well， what happens if I take your model but drop in agents who form。

 their beliefs about how the macroeconomy works a little bit differently， that's one line of。

 code because all the agents are in the same object or into a oriented framework。

 They've all descended from the same inheritance structure。

 We're trying to formulate this as a model tree that there are canonical very， very。

 very basic models at the top and everything descends down from that in class inheritance。

 both through on the agent representation level and on the solution method level that you're。

 inheriting most of the subroutines and then changing only a couple。



![](img/9ea5c2cb03436ef757c558f33faae725_119.png)

 So this intended to make it reduce the barriers to entry effectively。

 We're also trying to make it easier to teach these methods。

 So I said there were good teaching tools or there are now recently good teaching tools。

 for the basics of numeric methods that are foundational to both what we do and other fields。

 We're trying to provide lessons for getting， taking it a step further and doing the models。

 themselves。 Making it easier to compare models to each other。

 It is the worst thing in the field when two potentially no-bell winning economists present。

 or research the same topic with extensively the same model targeting the same data moments。

 and reach completely polar opposite conclusions which means at least one of them is wrong。

 and quite possibly both and it may be a long， long time before we find out。

 We want to make it easier to audit those models。 It's written to be extensible so not all of our code is written in the most absolutely。

 efficient way possible。 We've thrown every trick in the book at it。

 We have held back on that and left in things that could be written more efficiently but。

 for the fact that it was written with future extensions in mind that would break if you。

 tried to add that extension and use that trick。 Of course we're trying to write to be modular and allow all these components to swap。



![](img/9ea5c2cb03436ef757c558f33faae725_121.png)

 I've covered most of these but one of the bits here that you'll see if you go to our， webpage。

 con-arc。org is that all the way at the top it makes reference to agents whether。

 they are optimizing or not。 That is a cryptic reference to the so-called agent based modeling community where their。

 concept of agents are what I would call automata。

![](img/9ea5c2cb03436ef757c558f33faae725_123.png)

 They are rule obeys。 They're not solving some optimization problem。



![](img/9ea5c2cb03436ef757c558f33faae725_125.png)

 They are doing a thing because they've been told to do a thing because it's in their nature。

 which allows you to have a much richer state space as to what information they can process。

 but it begs the question of why did they do that thing？ Where did that come from？

 We're trying to bridge the gap and behavioral economics is the one step to the left of full。

 rational expectations where people have cognitive biases。



![](img/9ea5c2cb03436ef757c558f33faae725_127.png)

 Just to give you a sense of， oh， here is， I realize during this conference that everybody。

 else has clever images and is snazzy and that's not what we do in economic economics。

 I put in the funniest thing I could think of which is Bill Murray and Asely Hat。

 I hope you're all entertained。 Just to give you a sense in these last few minutes of how this all works on the micro。

 side， our super class at the top is agent type。 This is our framework for representing all kinds of agents。

 decision makers。 In this case， the most baby one， a perfect foresight agent who is making a decision about。

 how much to consume and how much to save when they face no risk other than potential death。

 Just minor risk。 It's trivial。 The key method to agent type is the solve method。

 This is nothing more than a universal backward induction loop but putting it into a common。

 framework allows all these different types of agents to play nicely together and that。

 when you interact them in a so-called market subclass or macro concept， as long as everything。



![](img/9ea5c2cb03436ef757c558f33faae725_129.png)

 is descending from agent type， everything should play nicely together。

 I'll skip over the basics here because I have only three minutes left here。 Math。

 Consider a basic consumption saving problem that actually does have some risk。

 For the four people in the room， six people in the room who understand this， we've got。

 a consumption saving model with constant relative risk aversion utility， a constant interest。

 factor， geometric discounting at constant rate beta， a hard borrowing constraint on。

 your singular asset and permanent and transitory shocks to income。

 This is all written in normalized formats。 All the variables have been divided by your permanent income。



![](img/9ea5c2cb03436ef757c558f33faae725_131.png)

 Everyone， we're good。 So we could map this from the math of the model to its representation in HARC as the in shock。

 consumer type is the type of agent who has this problem and instances of this class fill。

 in specific values of those attributes。 So instances of the class are filling in what exact values those take on at this time。



![](img/9ea5c2cb03436ef757c558f33faae725_133.png)

 So this is either a CO2 accumulation figure or the consumption function。

 Was nobody at that talk yesterday？ Fine。 We're on different tracks。

 This is the consumption function that comes out of that。

 So just to give you a sense of what I mean by object oriented solvers and this sort of。



![](img/9ea5c2cb03436ef757c558f33faae725_135.png)

 thing and how we're trying to write HARC to be very easily extensible。

 So the solution methods themselves are object oriented。 That a solver。

 that the function that solves the method that solves the problem， the one。

 period problem is in fact an object itself。 And so it's each model not only specifies a subclass of agent type but a subclass of。



![](img/9ea5c2cb03436ef757c558f33faae725_137.png)

 the solver for the agent type above it in the model tree。

 And so here's a slightly outdated model tree。

![](img/9ea5c2cb03436ef757c558f33faae725_139.png)

 Let's zoom in on one little bit of this。

![](img/9ea5c2cb03436ef757c558f33faae725_141.png)

 Supposed we want to add one little twist which is that you can borrow now。

 We don't have a hard borrowing constraint at zero but the interest rate on borrowing。

 is greater than the interest rate on saving。 It's like you're borrowing on a credit card。

 you're saving in like your zero percent savings。

![](img/9ea5c2cb03436ef757c558f33faae725_143.png)

 account。 In HARC this takes what I'm about counting eight lines to add by changing one or two。



![](img/9ea5c2cb03436ef757c558f33faae725_145.png)

![](img/9ea5c2cb03436ef757c558f33faae725_146.png)

 methods， one of them just the initialization method to store the two interest factors。



![](img/9ea5c2cb03436ef757c558f33faae725_148.png)

 And out pops a consumption function that is kinked where at the along that linear portion。



![](img/9ea5c2cb03436ef757c558f33faae725_150.png)

 is where you're neither saving nor borrowing。 If we want to add a different shock or a different twist maybe you've got preference shocks where。

 at a very low or high frequency and so sometimes we see people spending a lot more in one week。

 than another， well where's the conifer？ It's not coming from income shocks。

 Well maybe consumption is more valuable one week than other。



![](img/9ea5c2cb03436ef757c558f33faae725_152.png)

 Something's happened to you。 So we can throw in that twist and it takes about 20 lines to stick that in but no biggie。



![](img/9ea5c2cb03436ef757c558f33faae725_154.png)

 and outcomes here's consumption function by your current period preference shock。



![](img/9ea5c2cb03436ef757c558f33faae725_156.png)

 Here's the kicker。 Suppose you want to have both those twists。

 You want a model where people are having these short run preference shocks to their how much。

 they want to consume and it is more expensive to borrow。

 So this is useful in a model where you want to study deposit advance products or payday。

 loans for example。 I say HARC makes this pretty easy。



![](img/9ea5c2cb03436ef757c558f33faae725_158.png)

 HARC makes this trivial。 In this case here's the entire extent of the code omitting the arguments for the functions。

 This is the entirety of the solver code。 It's just multiple inheritance from both of those solvers。

 We had two solvers that split off from one。

![](img/9ea5c2cb03436ef757c558f33faae725_160.png)

 Reinherit from both and out pops this beautiful kink to figure where it kinked on the per。



![](img/9ea5c2cb03436ef757c558f33faae725_162.png)

 preference shock。 And that leads me to my final few seconds here where that's where we got our logo。



![](img/9ea5c2cb03436ef757c558f33faae725_164.png)

 When we got that to pop out we said there's our logo。



![](img/9ea5c2cb03436ef757c558f33faae725_166.png)

 We are the EconARC。 The heterogeneous agents resource and toolkit is just the first piece of this。



![](img/9ea5c2cb03436ef757c558f33faae725_168.png)

 We want to add other subfields of economics in which we are not experts。



![](img/9ea5c2cb03436ef757c558f33faae725_170.png)

 Maybe you are。 It feels a computational economics。 If you are an expert come talk to us。



![](img/9ea5c2cb03436ef757c558f33faae725_172.png)

 We would love to hear from you。 The monetary version of this is the early stages of it are in development at the IMF。



![](img/9ea5c2cb03436ef757c558f33faae725_174.png)

![](img/9ea5c2cb03436ef757c558f33faae725_175.png)

 And then I guess I need to get to this slide。 We are supported right now by a very generous grant from the Alvarie Peace Loan Foundation。



![](img/9ea5c2cb03436ef757c558f33faae725_177.png)

 It will surprise no one in this room that our fiscal sponsorship is from Numpfocus， a。

 wonderful organization。 I saw somebody， I thought Gina was here。 There you are。 Hey， Gina。

 Originally spawned by CFPB， a 21st century regulatory agency。



![](img/9ea5c2cb03436ef757c558f33faae725_179.png)

 And there is interest from various international central banks。 Time for questions。 Thank you。



![](img/9ea5c2cb03436ef757c558f33faae725_181.png)

 So if you can go up to that mic， I'll reserve this for the ones on the sides。



![](img/9ea5c2cb03436ef757c558f33faae725_183.png)

![](img/9ea5c2cb03436ef757c558f33faae725_184.png)

 Let's give a couple seconds for people to sort of process。



![](img/9ea5c2cb03436ef757c558f33faae725_186.png)

 And then any questions？ Okay， go ahead。

![](img/9ea5c2cb03436ef757c558f33faae725_188.png)

 Yeah， so earlier in the talk you。 I think you have to lean into it。



![](img/9ea5c2cb03436ef757c558f33faae725_190.png)

 Okay， can you hear me now？ Yeah。 So earlier in the talk you mentioned that there is something that's not being done that。



![](img/9ea5c2cb03436ef757c558f33faae725_192.png)

 is modeling your ultimate consumer and basically you can really lump it into just one representative。



![](img/9ea5c2cb03436ef757c558f33faae725_194.png)

 So I'm curious if you said that there is a distribution。

 Has any work been done using this framework or if it's in the works about modeling your。

 consumer as some sort of distribution or not？ Oh， yeah， yes。 So the。 Well， so here's the thing。



![](img/9ea5c2cb03436ef757c558f33faae725_196.png)

 So if you truly want to do head reaching this agent's macro， if people say， oh， you want。



![](img/9ea5c2cb03436ef757c558f33faae725_198.png)

 to get away from rep agent， then each agent when they do their processing needs to think。

 about what the entire distribution of the state of everybody is。

 So when you all make your optimizing decisions， some economists think you know how rich every。

 single person is and also what their job is and how risky it is and that's absurd。



![](img/9ea5c2cb03436ef757c558f33faae725_200.png)

 And so， yes， so representationally we do this by storing the distribution as some sort of。

 finite vector of its。 As a stochastic vector sometimes it's stored as a。

 We approximate the 300 million household or 300 million people in the United States by like， 100。

000 because that's pretty close。 But yes， so we do represent the population as a distribution and usually use projection。

 methods to reduce the infinite dimensional space to like a two or three important moment。

 space for what humans are actually able to track is usually how it's done。 Yeah。

 Are there any more questions we have to talk about？



![](img/9ea5c2cb03436ef757c558f33faae725_202.png)

 Great talk。 What's the relationship with QuantEcon？ We aspire to be them。

 So I kept pointing at Rick。

![](img/9ea5c2cb03436ef757c558f33faae725_204.png)

 I don't want to sound presumptuous。

![](img/9ea5c2cb03436ef757c558f33faae725_206.png)

 I'm open to a merger either way。 So QuantEcon has been wildly successful。

 So every time that we made reference to a group that is providing tools for people to。

 learn the foundations， I was talking about QuantEcon。



![](img/9ea5c2cb03436ef757c558f33faae725_208.png)

 We would like to get our。 So the lesson style notebooks that we're currently in the process of making right now。

 we're， somewhat modeling that on the courseware that QuantEcon provides。

 We're sort of using that as a learning model for our teaching。



![](img/9ea5c2cb03436ef757c558f33faae725_210.png)

 The formal relationship is that we email John Stotryrsky whenever we want to know how。

 they did something。 And in some cases hire John Stotryrsky's brother to do our Web Dev。

 And also for friends with Rick。 We have time。 We have time for about one more question quickly。

 Does anyone have an additional question？ Yes。

![](img/9ea5c2cb03436ef757c558f33faae725_212.png)

 Have you done any work with the Ag and Applied Economics fields？



![](img/9ea5c2cb03436ef757c558f33faae725_214.png)

 Not yet。 That's one of the。 So I think about resource economics or。 Not yet。

 That's one of those things that we would be open to。 So I don't know much about Ag Economics。

 I think of it as the canonical， like the fishery and forestry problem or the first thing we're。

 taught in dynamics。 But I don't know what they do。

 But if they could have a framework like this that is the。

 There's some overarching canonical Ag Econ problem， then we would love to have the Ark， I guess。

 Or maybe it could be our long sought art of Ark， which we've been trying to back end for， a while。

 Backfill， excuse me。 Not joking， we've got a plutarch。 Papers in LaTeX using the Ark。



![](img/9ea5c2cb03436ef757c558f33faae725_216.png)

 All right。 Well， I think at this point we should let everyone sort of break lightning talks down。



![](img/9ea5c2cb03436ef757c558f33faae725_218.png)

 in the ballroom。 That's all。

![](img/9ea5c2cb03436ef757c558f33faae725_220.png)

 Thank the speakers。 [applause]， Thank the speakers。 (applause)， you。

