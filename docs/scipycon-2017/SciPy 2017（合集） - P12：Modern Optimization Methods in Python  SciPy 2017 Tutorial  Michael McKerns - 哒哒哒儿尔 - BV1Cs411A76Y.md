# P12：Modern Optimization Methods in Python  SciPy 2017 Tutorial  Michael McKerns - 哒哒哒儿尔 - BV1Cs411A76Y

 Good morning everybody。 This is modern optimization methods in Python。 Welcome to the SciPy 2017。

 It should be a good conference this year。 We're going to talk the next couple hours and do some hands-on kind of exercises。

 If you care to do that， during the course of this tutorial。

 the tutorial is pointed towards a recent trend of changes to optimization methods and optimization。

 So optimization is something that's used in all across all sciences。 And surprisingly enough。

 the tools in optimization， the optimization tool stack has been -- I don't want to offend people。

 but it hasn't changed much since the computer first。

 It came about that we were still using methods from the 60s with some improvements up until a couple years ago。

 So there's been a shift towards parallel computing and nonlinearity。

 Things that allow optimization problems to handle。

 to tackle large-scale physical engineering problems， chemistry problems。

 And you don't see these methods in textbooks quite yet， except the most recent kind of textbooks。

 But when you go back to physics， textbook or quantum chemistry textbook。

 you'll still see many of the older methods from the 60s。

 So we're going to talk about some of these modern methods。

 I'll go through a couple packages that have optimization in it。

 So we'll start with an introduction to optimization。

 I'm going to assume people may have done it a few times but are not totally familiar with it。

 So we'll get the lingo down and then we'll move into some of the more recent kind of methods。

 So the package we're going to center on is Mystic， which I'm the primary developer of。

 And I hope everyone was able to get -- so this is the tutorial homepage and there's the notebook files。

 There is a Python script here that you can run to make sure you have everything installed。

 Let's see this check M。 And if that runs and doesn't complain about anything。

 then you've got everything installed。 There's a few things like SQL。

com you don't have to install but it can make the database back end stuff work a little bit better。

 Okay， so hopefully everyone has that。 And if they don't， it's not terrible to install it all。

 It installs。 And I saw on Slack there was some conversation about whether this was Python 3 compatible or not。

 Mystic is just recently Python 3 compatible so it will work。 I converted notebooks this week。

 All right， so I'm， I guess， start off。 I'm Mike， Michael Kearns。

 and the -- I basically have been an optimization physicist。

 but I've been an optimization research and somewhat for 15 plus years。

 And I mean one of the things that was interesting to me is when I was first as a graduate student trying to kind of do inverse modeling。

 or basically look at -- simulate -- I mean this is the old days when， you know。

 there was no internet and dinosaurs walked the earth， right， that kind of stuff。 You know。

 I simulated a nonlinear absorption experiment and I was running a nonlinear absorption experiment to try to determine how well a nonlinear absorber would absorb light basically to get the transmission properties of it。

 nonlinear transmission properties。 And I， you know。

 there was no internet so I had to run a floppy disk back to my office。 You know。

 we're talking about a long time ago。 And I had a simulation of the experiment and the data and I also had a little bit later started to do quantum chemistry on the material。

 And I wanted to try to extract trends and understand how the structure of the material。

 what the structure of the material looked like in -- it was suspended in liquid in order to kind of like a crystal。

 molecular crystal。 I was trying to understand what the structure looked like based on the absorption transmission spectra and the nonlinear transmission and the simulation experiment。

 And what I found was that the thing that was failing me was the ability to apply physical information to the inverse problem。

 Yes， it was a pain to hook up to， you know， a home built computer that I had in my office that was like a bay of bay of cluster。

 Yes， it was a pain to get the data around on a disk。

 But the real failure that took quite a long time was to be able to constrain things。

 Like how do you constrain -- when you know something like an average bond length。

 how do you apply that as a constraint in the optimization problem to solve the structure？

 And there was just no way to do it。 Basically， you had to leave out a lot of information。

 And it was back then I realized， wow， it's kind of an unknown thing。

 but the optimization methods we have are really kind of basic and flawed。



![](img/9a512611b7f4945c6d5160b215b8b8da_1.png)

 And that's really when I started to convert my research over even back as a graduate student to focus on optimization methods。

 So it's something that's a little bit more budding now。

 So we'll first start with -- can everybody see this okay？ You need it bigger？ Okay， great。

 So we're going to start with basic components of optimization。 Optimization -- basically。

 you'll get the lingo for it so people will call it the objective function or cost function。

 It's basically a function you're interested in。 And there's a lot of things that you're going to do。

 With optimization， you tend to try to get to the bottom of something。 So you get to a minima。

 whether it's a local minima or a global minima。 Optimization。

 you can picture as there's some surface。 The surface may be unknown。 You may have a function for it。

 You may have some information about it。 And what you're trying to do is get to the lowest point on that surface or the lowest point in some region of that surface。

 And that's simply enough all of what optimization is about。

 When you do more complicated things like， let's say， optimization is used in regression。

 Regression is fitting， right？ Fitting a line to data。 Well。

 what you're doing there is you're minimizing the distance。

 But you're minimizing the difference between the best fit line through the data and your data points。

 Okay， so that's -- you have some metric -- you have some metric which gives a measure of distance。

 You're trying to minimize the distance。 And so the optimization in regression is basically -- or fitting -- is basically a minimization over the distance between the data points and the line that you're drawing through the data points。

 And you can think of the same thing in classification。

 For those of you who've done a little bit of machine learning。

 classification is essentially just splitting up a whole bunch of points with a different label like success and failure。

 And you're trying to draw the best fit line that divides those two groups as best as you can to put all the success on one side and the failures on the other。

 And the optimization problem there is to draw the line that is the furthest away from each of the points on each side。

 So that's a maximization problem， but maximization is just take the energy surface and turn it upside down。

 And then you're doing a minimization。 So that's -- optimization is basically everywhere along all sort of tools that people are using。

 And it all boils down to understanding what the potential energy surface is or the objective function is。

 the cost function， and trying to get to either A minima or the global minima。

 So here's a standard type function we're going to define。 It's polynomial。 1。

3x squared times 4x plus 6。 And then we have some optimizer。

 And the standard optimizer is a NelderMead。 So here's SyPy Optimizes NelderMead。

 And basically what you'll see is the optimizer expects cost function or an objective function to work on。

 And then it expects a vector。 So a solution vector。 So F min or -- that's NelderMead。

 It's a local steepest -- it's a local optimizer。 So basically。

 if you have some sort of surface like this potential energy surface of the polynomial。

 you pick a point。 That point is represented by the three。

 You basically drop that line -- point on the surface somewhere。 And it rolls downhill。

 which ultimately is basically what， you know， a simplified version of what NelderMead and any optimizer is doing。

 There's a lot of local optimizers。 Just picture just having a point on the surface and it rolls down the hill。

 So you get something that looks like that。 You'd pick a point like here。

 I think pick a point like here and it would roll down and find this point at the bottom。

 It's actually much harder than you think to find the true minimum。

 Even if you have a parabola like this， you get a lot of optimizers that they'll find points that are not exactly the true minimum。

 And that can make a difference in your physical interpretation of what you have。

 You may not have the exact minimum。 Because an optimizer has built in things like termination conditions。

 which tell the optimizer when to stop。 When does the gradient stop changing on the trajectory of the point moving down the surface？

 When does it stop changing by X amount？ Then the optimizer finishes。

 So those are the kind of things that are baked into optimization algorithms that tell the optimizer。

 So typically we have something that looks like that。

 And what you'll notice also is it's a black box。

![](img/9a512611b7f4945c6d5160b215b8b8da_3.png)

 An optimizer is one of those things。 It's a black box。

 I don't know if anybody has done optimization or machine learning。

 Essentially what you get to do is you pick an optimizer， machine learning， you pick a model。

 which has an optimizer baked into the instance。 And you say go。

 And it holds on to the process until you're done。 And it has an answer for you。

 And what happened in the meantime？ Who knows？ Are you actually at the minimum？ Also， who knows？

 Right？ So that's one of those things。 When you can draw a picture like this， you can say， well。

 yeah， that looks kind of like the minimum。 That's not that bad。



![](img/9a512611b7f4945c6d5160b215b8b8da_5.png)

 But let's say it was a 15-dimensional surface。 How can you tell from some resulting value？



![](img/9a512611b7f4945c6d5160b215b8b8da_7.png)

 You see the value comes out as X and you print the value of X is minus 1。53。

 And that looks like the minimum。 A bit in a 15-dimensional surface。

 how do you tell easily that you're at the bottom of the global minimum somewhere。

 especially if it's very expensive to plot the surface？

 If plotting each point on the surface takes 20 hours， how do you know you're at the bottom？

 So those are the kind of questions that are actually really hard questions for most optimizers。

 And they're not even built to handle that。 They just give you an answer。 They give you a point。

 So even those kind of things to be able to look at the internals of the optimizer and see what's going on and understand what path it took and what not can be improvements。

 Okay。 So here we plotted our objective and our solution。



![](img/9a512611b7f4945c6d5160b215b8b8da_9.png)

![](img/9a512611b7f4945c6d5160b215b8b8da_10.png)

![](img/9a512611b7f4945c6d5160b215b8b8da_11.png)

 So one of the things that people start to do to optimization tools provide。

 standard optimization tools provide， in order to impose physical information on the problem are called box constraints。

 And what box constraints are is essentially it says， "Hey， you have some inputs。

 but the inputs are only valid within this region， within this box。

 Don't bother searching outside that box， and that helps constrain the space of the possible solutions that the optimizer can explore。

 So most optimization algorithms are not constrained。

 and many of them can't even handle things like box constraints。

 So here's a SyPy optimize and minimize scalar， and there's a few of the methods that take bounds。

 So this one method bounded takes a box that we can work in。

 We're going to work in the region 2 to 4。 So we only look for the minimum between the region 2 and 4。



![](img/9a512611b7f4945c6d5160b215b8b8da_13.png)

 And we look at the first order Bessel function。 And so again。

 what we have is we call the optimizer on the first order Bessel function。

 and it's bounded between 2 and 4。 And this is still a one-dimensional optimization problem。

 so I can plot it very easily。 And you can see here's the result。 And then when we plot the result。

 we get the point right here。 So I was searching in the region between 2 and 4。

 And the minima is right there on the edge of the boundary。 OK。

 so that is one of the ways that this region between 4 and 7 wasn't even looked at by the optimizer。

 And so that's a box constraints。

![](img/9a512611b7f4945c6d5160b215b8b8da_15.png)

 So I will flip over to Mystic for a second is that we're going to be working with some mystic has a bunch of nonlinear test functions that are built into it in the model sub package。

 And what they do is they so mystic models， you can pick any one of the 20 or 30 test functions。

 Rosenbrock is one of the standard simple kind of nonlinear test functions。

 And if you print the documentation， it gives you kind of what the function looks like。

 And also it tells you， hey， if you want to look at this function， here's the domain。

 you should look at it to see what the minimum is。 Here's the global minimum。 And so let's do that。

 Let's here we look at the documentation。 We see it says to use the model plotter between minus three and three and minus one and five。

 And one here still it's a 2D surface。 We're looking at 3D surface。

 We're looking at for the Rosa Brock function， which has the solutions at one everywhere。

 So model plotter， this function is cheap to evaluate so you can have a granularity that's pretty small。

 And if I had done this from the command line instead of trapped in the the IPython window。

 you can actually spin the thing around。 It's just a matplotlib plot of the surface。

 And so that's what the thing looks like。 And you can see that it's basically got two wells。 In this。

 now this is， this is in this slice of the Rosa Brock function。 3D Rosa Brock solution is one， one。

 one。 And this is cut of the surface looking at the first two dimensions and the third dimension is one。

 So Rosa Brock has a couple peaks like this。 It's a nonlinear function。

 And you can use that as a tool in any of the problems that we're looking at。

 It always helps to get a good picture of what the surface you're going to be looking at is。

 So here's kind of a standard approach to doing an optimization problem is what you'll do is you take some initial guess。

 And this is going to be a 5D 5 dimensional Rosen Brock where the answer should be one， one， one。

 and one。 And we do minimize Rose and Brock starting at X zero or initial guess and we get a result。

 We can check site by optimize gives us the number of function evaluations。

 And then we can do it again。 But this time we're going to give more information。

 Some optimization algorithms if you provide the derivative of the function。 That helps。

 Not many of not many optimization algorithms can work with the derivative， but if you can。

 And if you provide the derivative。 Here Rosen Brock derivative is derivative。 Then it may do better。

 We'll print the result again and look at the function evaluations。 And derivative evaluations。

 And then。 What you see is those are not one。 Right。 The answer should be all ones。

 And it kind of fails。 In 5D。 And again because what we're doing is optimize is just taking a point and just going descent down to the nearest well。

 And you can see in five dimensions with a whole bunch of spikes。

 It's going to trail into one of the wells and get stuck。 So how do you know？

 I mean I got the same answer essentially twice。 One with the derivative and one without。

 And if you went home and just said okay。 I got it。 You'd be wrong。 And you'd be in the wrong minima。

 So one of the things that people do is run the thing many many many times。 Right。

 And if it's a non deterministic optimizer。 Then you can just run it several times within some bounds and it will just take a different random path。

 Or if it's a deterministic optimizer one of the things you can do is break up the search space or randomize the initial value you start at。

 And just keep going until you get the best answer。 So that's what we're going to do in this case。

 We're going to do a loop where we take a bunch of random numbers。

 And we minimize the objective function with the derivative and get the result。

 And we just happen to do a lot better and get it every time in that case。

 I wouldn't expect to get it every time but just that the fall of the random die in that case is we found the minimum every time。

 And essentially all that is is basically like throwing a bunch of balls on the surface and hoping it gets close to the minima。

 And if we didn't know that that was the minima。 I ultimately what people have tended to do over the course of the years is just say。

 I've gotten this number and no better in three days of trying。 That's the answer。

 And that is actually you know you'll see that kind of language masked in publications but that's what people do。

 They just give up and say this is the best I got。 I feel confident that it's the answer。

 Okay so another one of the things I want to talk about another piece of the optimization problem is the what I would guess the what I would call the traditional mechanism for imposing information。

 constraining information into the optimization problem。 So that's called the penalty function。

 And so what a penalty function is is I have a nice equation up here and for some objective function so you can think of some surface you're going to impose a penalty add a perturbation to the surface。

 Okay and that is some multiplier times some function。

 That's a perturbation to the surface and essentially what you're doing with the penalty is saying when the penalty is violated。

 when this piece of information like the the mean of all the values are larger than four。

 If that's violated it imposes a penalty on the surface and increases essentially a barrier。

 So what you get is you get you know you're trying to go to the minimum of a surface and penalty function adds a additive barrier wherever the penalty fails whenever the penalty and whenever the constraint is not satisfied。

 So if you have something like this minimize here's a two dimensional problem。

 2x1 2x0x1 plus 2x minus x squared minus 2x1 squared subject to these constraints。

 There's two equations x1 is greater than or equal to 1 and x0 cubed minus 1 is equal to 0。

 And typically for penalty functions and constraints they're often written with all of the all of the variables on the left hand side or the right hand side and they isolate just a value usually zero。

 It's usually written so everything's on the one side and it equals zero or is greater than or less than zero。

 So so what we're going to do is we're going to make a barrier where when these conditions are violated it's an additive value that helps push it away from those away from the region or where we have bad points。

 Let's get that here's our objective objective function is looks you know thanks to NumPy it looks basically just like our function we're going to maximize right there。

 And in this case to help it along I'm going to take the derivative since it's very simple kind of analytical function I take the derivative to help it along and that can be used so minimize with the Jacobian or the derivative。

 And this method SL SQP so that's linear and quadratic programming。

 So one of the techniques in in most solvers a type of solver linear and quadratic programming solvers work only on simple functions。

 They only work on linear or quadratic functions they're going to estimate your objective to be linear quadratics。

 And if you if you can say well you know I really have a high dimensional nonlinear function but it looks like a parabola then then you get the benefit of using these things like penalty functions。

 So what if you want to apply information like subject to these constraints one of the approximations you have to live with is okay we have to treat my actual problem that I'm interested in the function I'm interested in like a parabola or a line。

 Right so to be able to use these constraints we're picking a quadratic quadratic programming however luckily enough I'm only working with something that's basically in the realm of quadratic programming so it should be just fine。

 And then we do the usual thing which is basically minimize with that quadratic programming solver and then we get a result and that's unconstrained。

 And for scipy scipy optimize the constrained optimizers take constraint functions in this kind of ugly form。

 But if you compare it to the functions here you could see here's x not cubed minus x one which is this term right here。

 And here's x one minus one here。 This is classified as an inequality and this is classified as an inequality。

 And the way they have to be entered is you put everything on the left hand side and the inequalities have to be greater than or equal to。

 So if it was less than or equal to I'd have to use negative values。

 And then to make it easier to solve we even take the drutives of those equations to serve to better help assist us solve a problem。

 And then we solve it again where what we have is constraints is cons this tuple of dictionaries as our constraints。

 And you can see the first time unconstrained it tries to solve a problem and it gets two and one which is not actually the answer。

 And the constrained optimization problem tries to solve it and it gets one and one which is the answer。

 So it does better with the constraints but it's a little bit difficult to apply and again this is okay。

 In my case I didn't have to make any approximations because my objective function here is essentially a quadratic programming problem。

 If it wasn't then I have to approximate my objective typically。

 So hopefully what that should do is start to introduce you to the standard methods and optimization where many of them are。

 And there are some most optimizers of focused on being fast。

 Simply because they didn't have the technology behind them to do anything else but be fast。

 So if all you can do is approximate to a line then the thing you're going to try to do is be faster than anyone else。

 Because who cares you're not going to get the right answer。

 That's a perfectly valid domain so I've done some contract work with some of the big six banks。

 And they don't necessarily care about predicting the stock market very well。

 They care about predicting the stock market very quickly。

 So it's linear approximations on what the stock market is going to do in the next couple minutes or seconds or whatever。

 And kind of get a good idea of where the ship is going most likely and then recalculate again。

 And you know with a whole bunch of small segments that are linear segments you can approximate any line so that's what essentially what they do and they just try to be faster than anybody else。

 So they actually don't care about solving the problem really well。

 They care about solving the problem really quickly。 And that's a big domain of optimization。

 However for scientists or people in engineering doing risk analytics it's a different story。

 So you have limited data。 Your problem takes several hours to calculate that you need information。

 Alright so I'm going to look at basically here's a breadth of kind of some of the optimization methods in SIPI optimize。

 And it kind of gives you a sense of just what the most common methods out there are。

 And these are anywhere from traditional early 60s optimization methods to more modern methods built in the last 10 or so years。

 And what you'll notice is there's the majority of them are unconstrained and the ones that are constrained tend to be linear and quadratic programming。

 So you have a balance between those two types you have all these different kind of regions there's names you probably heard of before like simulated and kneeling。

 And then constrained optimization there's not as many of them。 There's things like Coplea and SLSQP。

 And again these are you have a trade-off of using constraints versus not using constraints and getting a more nonlinear solver。

 And there are other methods that I don't have up here like differential evolution and genetic algorithms。

 But those are global solvers and they tend to take a very long time。

 Basically they work by basin hopping randomly pick points。

 You're at some point in a basin on a surface and then you randomly pick a whole bunch of other points in some constrained algorithmic way。

 And it says oh this point is better now I move over to this point you keep doing that until your termination condition ends up being something like I haven't found a better point and 400 tries I'm going to stop。

 And those don't tend to do very well unless you let them run a very very very very very long time。

 And then it's still not guaranteed that you'll end in the minima because most of the termination conditions end up being something like you haven't done any better in X amount of tries。

 So here's an example from CVX opt which is convex optimization that is again treating everything。

 Like at best a parabola。 And what convex opt does is it gives you some better tools than well it's essentially geared for linear quadratic problems。

 And it's got some better tools than cypae optimized does for applying constraints and looking into the optimization problem。

 So one of the things we see here is we're going to have this objective function and we want to subject it to a whole bunch of these constraints some a bunch of inequality constraints。

 So to constrain an optimization problem with CVX opt you built a constraints constraints matrix so you have the equation a matrix a times X is B。

 Okay， it's assuming it's going to be linear and quadratic so AX equals B and your equations here are here's a minus one that corresponds to this minus zero。

 So here's the vector of the X nots and here's the vector of the X ones。 Okay。

 so this is it's looks like a minus one minus one zero and one。

 So CVX opt looks for less than or equal to this one's greater than equal to so we would have to flip the signs on it so it's a minus one that would be a minus one X not doesn't appear here so it's zero and this is a plus one。

 So that's what we get for for those coefficients of the X nots and here we have one minus one minus one and minus two。

 Okay， so those fill out our coefficients of the a matrix B is the solution vectors so here you see one two zero and four but of course this one gets flipped so it's minus two。

 And then for our cost function。 We essentially are dealing with linear quadratic programming so we have a just a matrix we don't even give it a function we say we're minimizing this function and we just give the coefficients two and one。

 And， and then here's a linear programming solver for a X times B and you get your solution。

 That seems like a lot of work to be able to just solve a fit the values of X not and X one in this linear function。

 But the key piece is being able to get those constraints in。

 And the nice thing about CVX opt is when it runs you get some of this diagnostic information。

 So actually the diagnostic information is great。 What that allows you to see is okay it's not that I just got an answer。

 I just got an answer of X not is 0。5 and X one is one point five。

 I actually can see how well the how the optimizer moved it started out and then kind of very quickly within two steps got around the cost。

 So the cost is the energy cost it's the point on the energy surface。

 And it's basically stayed around the minimum of this energy surface at point two point five。

 So that's one of the things that people who do optimization will love to see。

 What is the solution trajectory look like？ What's the value of the energy on the energy surface？

 So the value of the function the objective function as the optimizer is moved down the surface。

 And what are the values of the variables at those points？

 Well this just actually just shows you the value of the objective function at that point。

 Okay so that's more information。 Here's a quadratic case CVX opt again。

 What it's going to do is it's going to build a it's going to build a matrix of the inequalities and a matrix of the equalities。

 And you get something that looks like like this essentially quadratic programming takes a Q which is this representation of our objective function。

 And then these guys GH and AB are the coefficients just like we had before for the inequalities and the equalities。

 And it's again treating it like a quadratic programming problem。

 You're not going to be able to do anything more than parabolas with these things。

 And you can see again nicely it converges to a solution。

 And somebody who's done optimization problems when you see a solution trajectory for most descent optimizers what you're looking for is you're looking for it to kind of glide into the solution。

 You see a glide into the solution you think okay I have confidence that that's done a good job。

 Sure。 So let's see we have two。 It's X1， X2， X1 and X2。

 These first ones are the where terms I believe。 Why is it a half？

 I have the two out front to do the multiplication from the halves。

 The thing that it is going to focus on is these are coefficients for X1 and X2 and it's got a map out to the coefficients up here。

 The first one should be 2X1 squared I believe。 And this one should be X2 squared。

 And I'm multiplying by that by 2。 I don't remember why I did that。

 Probably something to do with the let's see。 Yeah。 That's right。 That's right。 Yeah。

 Basically that's exactly what I was saying is the first part is specifying the quadratic part。

 the squared terms and the second part is the linear terms。

 And there's this cross term that we've got to deal with。

 So I forget the actual specification that CVX opt uses but that's why I had to。

 It doesn't handle the cross term but to handle the cross term I'm fudging those middle values at 0。

5 and 0。5 and then multiplying by 2 to get the coefficients right。 And that's just what it specifies。

 I don't remember exactly the。 I can't tell you directly one to one。

 But that's what the documentation will say to do the first part is quadratic。

 second part is linear and then handle the cross terms with the multiplier。

 So even in this case you see it's hard to get some of these problems to map to the solvers。 Yeah。

 Okay。 So is nice to have this trajectory。 And I'm actually I think I think I have exercises in here but what I think I'm going to do is I'm trying to time this。

 I'm trying to time this pretty well and what I'll do is I'll hold off the exercises to the end of each section and that way people can do whichever bits they want and will break up the stuff。

 So we'll go and skip to the next bit and remember there's an exercise up there if you want it。

 So I look at now what I've shown so far basically local optimizers in general but there are a few things that are global optimizers based on the differential evolution genetic algorithms。

 Like I said they do take a long time。 And it's often very difficult for them to the larger the problem。

 the larger the optimization problem， the higher dimensional the optimization problem is the more likely that these are going to be the solvers that will work for you。

 So they do take quite a long time you look at the number of function evaluations that we had in the previous problems and they were numbers like 100。

 160 almost 150。 And then you go down and look at differential evolution and you're seeing number of function evaluations like 40。

000。 And that's typically that's typically the case。

 So here's what we have we have instead of picking an initial value you pick the range some bounds that an initial guess is going to be valid in。

 So again we're looking at the Rosenbrock function we're going to do the rosobrock function in five dimensions。

 Optimization differential evolution the Rosenbrock function but instead of giving an initial value give bounds so valid between minus 10 and 10。

 So that's the lower bound and that's the upper bound for all parameters and that gets passed in and it sits there in turns for a while and then gives you a result。

 And it turns out that the random starting values that it picked it succeeded out of the 10 times we ran it it succeeded nine times。

 And you can see that the one indicator that it failed in this particular case is the function evaluations are much less。

 And you can see what happens it hopped around and it didn't find a better solution and it stopped。

 While the ones that got to the best solution what you've got is the hops are not across the entire area。

 And part of these algorithms is once you start to get on a path it often narrows the range that it hops to or narrows the range that the solution trajectory mutates to。

 So you'll end up seeing something like these large number of function evaluations because it's found it and then it is hopping around in one of these basins quite a bit and improving just very slightly。

 And then just you get this glide behavior down to a best solution。

 So if you were to look at the solution trajectory you'd see it kind of got where it was going pretty quickly and then maybe chunk down a few times like that and then just gliding out until it eventually stopped。

 So that's one of the difficult parts about that is let's say you have an objective function that takes five hours to evaluate。

 Differential evolution is not going to be your friend or any of the global methods that have these kind of function evaluations that is longer than I want to wait for it。

 All right。 Yeah， of course。 No， it's minus 10 and 10 and what I did there is I just took the list and multiplied the list by five which means it's going to be minus 10 and 10 for each for each of the parameters。

 So it's a five dimensional optimization problem。 All right。

 So that's one of the cases and it's a difficult issue with global optimization is that they tend to take a long time。

 They're very costly。 I mean one of the obvious things that people have done is they started to parallelize these global optimization methods to try to try to speed things up a little bit。

 All right。 So there's some other cases that are worth noting and I'm just going to brush through them real quick。

 If you want an error estimate built in typically you would use least squared fitting。

 So least squared fitting is this line right there。

 It looks basically like curve fit of your function starting at some initial guess。

 And what you're trying to do is fit X to your noisy data。

 So what I've done is I've built the function here。

 And what you're trying to do with a curve fit in the in the case is fit the parameters。 A， B。

 F and phi inside of this objective。 And so it's slightly different than the other optimizers and the only reason you tend to use it is fitting the curve and getting the covariance out which is an error estimate。

 And you can do that by what the least squared fit function typically returns is it returns the estimated parameter values。

 And it returns the covariance or the error estimate values。

 Otherwise there's no need to use least squared fit unless you want to get this error estimate baked in。

 So that's covariance and with all of these guys being around zero it tells us that okay the fit was pretty good。

 And you know you can see if these were my target parameters and these are the values I found they match up pretty well。

 You can see there's not much of an issue。 So that's one of the techniques and that's pretty much contained within the least squared fitting。

 Most other optimizers don't give you most of your optimization algorithms don't give you a covariance basically。

 So that's a pretty rare diagnostic technique。 Now there's another kind of interesting case which is integer programming which is used in working over discrete sets。

 So integer programming is again a specialized， specialized solver where the solver only works on the space of integers。

 So that's used in cryptography and optimizations research and a few things like that where solver doesn't work over the state of reals。

 It works over the set of integers and you have to map your problem onto an integer problem basically。

 And they can have constrained integers so constraints tend to work in those integer programming problems。

 Just like linear and quadratic problems do。 I'm just going to note that that's there。

 There's a number of solvers like Google has a solver toolkit for that。

 It doesn't necessarily have a Python interface but we will deal with it a little bit later。

 So typical uses for optimization are minimizing a function fitting data finding roots。

 So I showed the other two above root finding will look something like that。

 You get a system of equations。 You have A， B and C which are the coefficients we're trying to find。

 And X0， X1 and X2 which are the parameter vectors。

 Then we write a system of equations where we essentially have A value on the left hand side and the right hand side is equal zero。

 The idea is you have a list of three values where that's the left hand side of the equation and the right hand side is equal to zero。

 And what you're going to try to do is minimize the summed value of the equations。

 That's typically how those work。 It will start with these coefficients， these A， B and C。

 We get initial guess of -1， -1， sorry。 Point 1。1 and -point 1。

 And then root of our system of equations from this initial guess with these coefficients。

 And the result you get is the new values of our X vector， our solution vector。

 And again what it's trying to do is it's just trying to minimize the summed value of the equations。

 So it uses some metric and the metric of distance is how those equations are summed。 Do we sum。

 you know， sum squared of all of those values when they equal zero， then we're done。

 So that's root finding and that's the typical way of doing root finding。

 Alright and parameter estimation。 So there's a poly fit and I'm just going to leave that for us。

 Look at a little bit later on your own。 Okay so what have we talked about basically a lay of the land for optimizers。

 different techniques for optimization， constrained， unconstrained， some of the just special cases。

 We've talked about global and local optimization and hopefully made you familiar a little bit with the pain points。

 And this I want to bring back as our standard diagnostic tools。 So what you'll see here。

 what you see above basically that we've just went through are really， you know。

 for the last 50 years what people have dealt with in doing optimization problems。

 And the thing I want to point out is how do you understand that you found the answer。

 The answer is these are the standard ways。 You look at it by your eye。

 Basically you plot the solution， slices of the solution。 You try to understand， yes。

 from what I can plot。 It looks like I'm at the bottom。 You run it several times。

 take the best result。 If you're lucky enough to get a log of the solution vectors or print out of the solution vectors。

 kind of trace the convergence of the solution vectors and say， yeah， that kind of feels right。

 And if you're lucky， you might get the covariance matrix。

 but I'm going to really be sure you have the results you're looking for。

 So that's one of the issues in optimization。 And it's really， in many cases because of that。

 it's more of an art form than a science。 Just like experimental science is。

 you have an instrument and you have to kind of tune the instrument。

 You get the instrument to run and you tune the instrument a little bit and you get more power and you get a better focus。

 And you kind of tune it， tune it， tune it。 And one is it good enough to get the results？

 One is it actually performing as it should？ Well， you just know it is。 Or you give up and say。

 this is the best I'm going to get。 I'm going to take my results。 I mean。

 and that's essentially most optimizers are built like that。

 They are essentially a black box instrument of theory。 And I think we can do better than that。

 All right， so that's the end of this first section。

 There's three exercises in it that if you choose to do them， you can try。

 So what I'm basically going to do is go let you work on the exercises。 People want to do exercises。

 right？ If people are universally opposed to doing exercises， we'll just skip them。

 But people want to do them or not。 Okay， that looks good。 Okay， so take 15。

 20 minutes or so and try to address these exercises。

 I'll sit here and do the same thing myself and come around。 And if you have questions， ask。

 I'm planning on you can take a break now during the exercises if you like。

 I'm also going to fit in a scheduled break for 15 minutes at 10 15 right before they take the snacks away。

 All right， so was that enough time to kind of get your feet wet on those things？ Hopefully， I mean。

 these problems are quick。 They should be able to get maybe one of them。

 I think based on the timing we're going to go through here。

 what I'll just do is I'll post the solutions for the exercise up on the website after the class。

 That way， if it's not enough time for people to get through all of them。

 they still want to work through what they can and the solutions will be right there for you。

 I can even， I have them in one form， but I can put them in several other forms。 So。

 those are questions that people have on these。 Was it actually this is this first problem with three inequality constraints？

 People use CVX opt on that。 Okay， so that's and how many people did the sci-fi optimize with the tokens？

 Yeah， so people tend to use CVX opt for these things。 It actually tends to be faster。

 It works with inequalities pretty well。 However， it's a much more limited。 Well。

 they're all fairly limited， but CVX， it's still kind of clunky to work with these。

 And that's kind of what I wanted you to get the feel of more than anything else。

 We're not going to dwell too much on these。 We're going to flip over to start using Mystic where life is a little happier。

 I tend to use it in real life。 So， let me say this。

 If you are in industry and you need to get a very fast answer， you're not going to use CVX opt。

 You are going to use GURABI， which does exactly the same thing as CVX opt does。

 but you have to pay through the nose for it。 And if you're in the position where you're trying to do linear and quadratic programming and you need a fast answer。

 you'll use that。 If you're a researcher and maybe you don't have the money to spend on GURABI。

 which is a commercial product， then people use CVX opt in real life， not in the classroom。 So。

 this is basically， you know， even for these problems。

 you start to see things that are a bit difficult。 I don't know。 These problems are also not。

 they're a bit leading to and that I've made it so they all work with coefficients。

 What happens if you have a sign？ One of your constraints has a sign in it。 What then do you do？

 Well， then you're actually forced to not use CVX opt or else you're forced to make a problem that is an approximate。

 So， in that case， if you have a sign， then， okay， you're in the realm of now possibly working with SIPI and having this form here。

 but that doesn't work terribly well either。

![](img/9a512611b7f4945c6d5160b215b8b8da_17.png)

![](img/9a512611b7f4945c6d5160b215b8b8da_18.png)

 because this is your equation， right？ So， there it would work with a sign。

 It would work with having a constraints equation and potentially the derivative of it。 I mean。

 that's part， like I said， I'll post the exercises after the class but exercise solutions after the class。

 but I just wanted to get you feeling a little bit of the pain of doing it。

 and that's really what it is。 If it was easy， then we would understand a lot more about the world。



![](img/9a512611b7f4945c6d5160b215b8b8da_20.png)

![](img/9a512611b7f4945c6d5160b215b8b8da_21.png)

 So， the first solution， by the way， if for those people。

 that was the only one that the numbers weren't posted for。 And it's a 10 and minus three。

 just for those of you who just for your own instant gratification， if you solved it。

 it's a 10 or minus three。

![](img/9a512611b7f4945c6d5160b215b8b8da_23.png)

 And the other ones， the solutions are the solution values are in the documentation。

 like this one down here， it's seven and two， but I will --。



![](img/9a512611b7f4945c6d5160b215b8b8da_25.png)

![](img/9a512611b7f4945c6d5160b215b8b8da_26.png)

 people have questions about working on those so that populate any questions up to you that you wanted to ask before we move on to the next section。



![](img/9a512611b7f4945c6d5160b215b8b8da_28.png)

 Okay。 So， again， I have a thing。 What happens when you go to high dimensional and high dimensional optimization nonlinear constraints？

 What does the world become for you？

![](img/9a512611b7f4945c6d5160b215b8b8da_30.png)

![](img/9a512611b7f4945c6d5160b215b8b8da_31.png)

 And， I mean， basically， this was what prompted me about 15 years ago to start working on Mystic。

 and I was one of the first people to go into this portion of the field。



![](img/9a512611b7f4945c6d5160b215b8b8da_33.png)

 And Mystic's been around a long time。 It's been around for 15 years， and 12 years。

 something like that。 It's not just my research that's gone into it。

 but it's grown and there's been other people that have contributed to it。

 And it's taken on a lot of modern optimization techniques that have blossomed into the last couple years。

 but one thing initially about Mystic was we want to be able to see inside the black box。

 We want to be able to have more tools， take optimization to an object-oriented kind of white box。

 as opposed to a black box， so we can kind of customize the optimizer。

 swap in parts that better approximate our problem and have better diagnostics。 And ultimately。

 about 10， 8 years ago， I was the first person to be able to apply these new kind of constrained optimization methods。

 But for people who've done machine learning or tried machine learning。

 essentially it's a kernel transformation。 I don't know if you know really what a kernel transformation is。

 kernel transformation is a mapping。 So how many people have a math background， basic sets。

 kind of like that， right？ And on the other side， physics， quantum mechanics。 So in machine learning。

 kernel transformation is a transformation of space， from one space to the next。 Okay。

 it's taking a space and mapping it to another space。

 That kernel transformation is transforming one space to another。

 That could be a coordinate transformation。 It could be a filtering where you reduce the space down to the regions to the directions of space that have the highest variance。

 Okay， but it's a transformation。 So in quantum mechanics or physics， you think of it as an operator。

 applying an operator to transform one space to another space。

 and you have the mapping of that space with eigenvalues and eigenvectors。

 And that's applying a piece of information。 You think of the classic Schrodinger's cat kind of thing。

 right？ Is cat dead or alive？ It's both dead and alive， and you do an observation。

 And that observation is a new piece of information， and that collapses your wave function to be。

 yes， we have a dead cat。 Okay， now with that piece of information。

 we shouldn't be trying to find solutions when we have a live cat。

 So that's what a kernel transformation does。 It's a mapping of spaces from one to the other。

 where we're applying some new piece of information and reducing the search base。

 You get eigenvalues and eigenvectors out。 That's common in a lot of types of physics quantum mechanics problems。

 And essentially， a new generation of optimization。

 And one of the probably the person who started it was to apply this kind of technique to apply information in optimization problems。

 So we were doing it with penalties and box constraints and kind of poor approximations。

 but we can do that with operators or kernel transformations。

 So we'll talk about that in this section。 So if we look at Mystic。

 a introduction to Mystic will show you that it meets the Python standard。



![](img/9a512611b7f4945c6d5160b215b8b8da_35.png)

![](img/9a512611b7f4945c6d5160b215b8b8da_36.png)

 If you like the scipy optimize one liner， you have Fmin from Mystic and all the same kind of keywords。



![](img/9a512611b7f4945c6d5160b215b8b8da_38.png)

 So if you've learned scipy optimize and you've learned scipy optimize is one liners。

 you can directly use Mystic as well。 And all Mystic will have is a couple extra keywords that allow configurability。

 Mystic has an actual object-oriented interface to it that we'll see later。 But as a start。

 if you've learned scipy optimize， then you can directly start to use Mystic as well。

 And you can see in this case it's our friend the Rosenbrock function。



![](img/9a512611b7f4945c6d5160b215b8b8da_40.png)

 We're going to go in three dimensions。

![](img/9a512611b7f4945c6d5160b215b8b8da_42.png)

 There's our initial guess。 And here Rett all is the keyword that scipy also uses， retain everything。

 retain all the solution vectors。 And what that does is instead of just returning the result。

 you return a tuple of a whole bunch of things。 The last thing being all of the solution vectors。



![](img/9a512611b7f4945c6d5160b215b8b8da_44.png)

 So what you can do is then do a plot of each of the parameters within the solution vectors。

 And you get something that looks like this。 So this is a number of iterations versus the parameter value。



![](img/9a512611b7f4945c6d5160b215b8b8da_46.png)

 You can see the optimizer started with the initial values and it kind of converged to all ones eventually。

 Which is the solution of the Rosenbrock。 So you can do exactly the same thing with scipy optimize。



![](img/9a512611b7f4945c6d5160b215b8b8da_48.png)

![](img/9a512611b7f4945c6d5160b215b8b8da_49.png)

 Mystic tries to make this easier。 So that's nice to be able to look at the solution trajectories。

 And this gives you some confidence that yes， I did at least converge and not have some weird abrupt thing just stop me。

 So you should have as an operator of an optimization package or an optimization algorithm。 You know。

 you like to see these smooth convergences and not abrupt stops。

 So that should give you some confidence it's good。

 And the only thing you'd worry about is am I converging to the right minima？

 We know the answer already。 So the answer is yes because it's 111。



![](img/9a512611b7f4945c6d5160b215b8b8da_51.png)

 But that's a nice diagnostic。

![](img/9a512611b7f4945c6d5160b215b8b8da_53.png)

 Mystic actually gives you the ability to apply callbacks。



![](img/9a512611b7f4945c6d5160b215b8b8da_55.png)

 So in this case we're going to be doing the same problem。

 And I have again not as easy to do in the notebook here。



![](img/9a512611b7f4945c6d5160b215b8b8da_57.png)

![](img/9a512611b7f4945c6d5160b215b8b8da_58.png)

 But so this is run pretty well if you do it from the command line。



![](img/9a512611b7f4945c6d5160b215b8b8da_60.png)

 But it gives you the ability to we have this plot parameters function where we're just plotting。



![](img/9a512611b7f4945c6d5160b215b8b8da_62.png)

![](img/9a512611b7f4945c6d5160b215b8b8da_63.png)

 Giving a current plot of the existing parameters。

![](img/9a512611b7f4945c6d5160b215b8b8da_65.png)

 And I do an F min and I give a call back。

![](img/9a512611b7f4945c6d5160b215b8b8da_67.png)

 And that's plot parameters。 And so what that's going to do is you wouldn't see it if you ran it in the notebook。

 But if you run it outside the notebook it'll actually do a plot of the solution at every new value。

 So you'd see a plot and this plot at the bottom is dynamically drawn where the values get etched out as long as it's tracing along。



![](img/9a512611b7f4945c6d5160b215b8b8da_69.png)

 You put whatever call back function you like in there as long as the callback follows。



![](img/9a512611b7f4945c6d5160b215b8b8da_71.png)

 This it basically takes the parameter vector as the input。

 So if it takes the parameter vector as the input you can do whatever you need as a callback function。



![](img/9a512611b7f4945c6d5160b215b8b8da_73.png)

 And so this one dynamically drawn plot I actually don't use very much。



![](img/9a512611b7f4945c6d5160b215b8b8da_75.png)

 I tend to have if I use a callback or I'll use a log or something like that。

 I want it to log to a file or I want it to do something like that where then I can go and plot from the file。

 But it's just an example。 And this handler over here handler is true。

 What that does is if you set handler to true what you get to do is stop an optimization problem。



![](img/9a512611b7f4945c6d5160b215b8b8da_77.png)

 So one of the things that's a big issue is let's say you're running an optimization problem and you know the thing might take a day。

 And you've had it run 18 hours you have zero diagnostics back from it。

 And you looks like even if you do have diagnostics from it maybe the solution looks good and you feel all right that's enough。

 I want to stop or maybe you feel like I need to shut the computer down。

 Whatever it is you need to stop and the problem is if you don't if you're not able to get the diagnostic information back you're done。

 You have to shut it down you lose everything。 Ultimately in most solvers most optimization algorithms because it's a black box it's a functor that you don't get anything back until you get the result。

 You're toast so by having a handler what that allows you to do is it allows you to do a control C to do an interrupt and then interrogate the solver a little bit。

 And that's only used if you don't plan on working interactively with the solver。

 I'll show a little bit later。 I'm going to talk about the ability to walk step by step through a solver so you can actually manually control how many steps and what not。

 But if you run into a function that's blocking until the end like most optimizers are there's nothing you can do to stop them and this gives you a handler which allows you to stop and say what's the current best value apply a callback function。

 to try to get some results interrogate it a little bit and then continue or stop。

 So while that's kind of useful it's another one of those things that I used a lot initially but with better tools have put it to the side quite a bit。



![](img/9a512611b7f4945c6d5160b215b8b8da_79.png)

 But it's often one of those things that when you don't apply the handler and you've got the thing running and you run into the case where you want to stop the thing and you haven't started it with the handler then you wish you had。

 It basically costs you nothing it just allows you to do a control C and temporarily stop。 All right。

 So here's another case where I'm applying a callback that does print parameters and you can see in print parameters what I'm going to do is just say generation blah has best fit parameters of something。



![](img/9a512611b7f4945c6d5160b215b8b8da_81.png)

 So what I have is a global iteration counter and every time the callback is called it increases the iteration counter and it prints out the current value of the parameters。

 And that way even if the optimization algorithm doesn't have。

 and this is what CV CVX opt is doing internally too。



![](img/9a512611b7f4945c6d5160b215b8b8da_83.png)

 It's just got a callback function that prints the current value of the parameters or something like that。

 So here's what you get out of it with the callback printing the current value of the parameters and you can see this way that they converge pretty well。

 I mean you start up here right at the second iteration you're almost at a good solution and by the time you're down at the seventh one halfway down。

 You're pretty good。 And so that's a little bit more diagnostic information to put that kind of callback in there。

 But Mystic provides the ability so you don't have to rely on building your own callback functions so this kind of printing the parameters。



![](img/9a512611b7f4945c6d5160b215b8b8da_85.png)

![](img/9a512611b7f4945c6d5160b215b8b8da_86.png)

 It gives you what I call monitors and there's several different kind of monitors。

 One is a verbose logging monitor。

![](img/9a512611b7f4945c6d5160b215b8b8da_88.png)

 And what a verbose logging monitor does is it basically prints information to stand it out as well as creates a log file。

 Okay。 And we're capturing solution trajectories basically。

 So that's our internal diagnostic information into the optimizer。 How's the optimizer doing？

 You look at the information that comes from the solution trajectories。

 And the verbose logging monitor is a class。

![](img/9a512611b7f4945c6d5160b215b8b8da_90.png)

 It's a class object。 And what we have from it is the number of times we want to print the energy value。

 And we want to put the representation of what the energy is on the surface。

 So this thing should be going down to the minimum， which is zero in this case。

 So here we can monitor the kind of from a stream pictorially from this log what the value instead of the values that's trajectories。

 What the value of the kind of the point is on the surface and the energy value on that surface。

 So the initial guess started up pretty high at like 300 and it quickly drops down to about zero。



![](img/9a512611b7f4945c6d5160b215b8b8da_92.png)

 And you see that you ultimately end up at zero。 And that's hooked up by just saying I want an iteration monitor。

 So if you wanted to capture all of the function evaluations。

 you'd hook up an eval monitor and function evaluation monitor。

 But if you want to just capture the best value as the optimizer goes to the next iteration。

 you hook up an intermon。 They're the same object。 They're just capturing different things that a valve on the evaluation function evaluation monitor will grow to much bigger sizes because you end up doing more function evaluations than an iteration monitor。

 So the iteration monitors for the solution trajectories。 And this is， there's several fields here。

 So the first two fields are print the y information essentially print the surface information to the screen and to a file。

 And you can toggle those independently。

![](img/9a512611b7f4945c6d5160b215b8b8da_94.png)

 And so what you see with Mystic is one of the things that Mystic prints is not only easy to hook up the monitors to it but it has a very clear print of what the termination condition is。

 I stopped by meeting these conditions。 And we'll come back to that later because Mystic is going to give us the ability to change and customize our termination conditions。

 And what this did is it printed a log by default called log。

text but you can call it whatever you like。 And Mystic gives you a log reader。 Again。

 both Mystic log reader。py as a script or as a function Mystic log reader。

 And it gives you a plot of the solution trajectories that come out of this log file。

 And this is the cost function。 So this is the x values and that's the y value。

 And you can see this looks like a very happily converging solution。 The cost tails off。

 The parameters converge pretty well。 It's kind of a plotting in plotting using a steepest descent or a linear optimizer tends to look kind of clunky a little bit in that it only takes 14 iterations so you're not going to get smooth lines but that's basically nice。

 You get a good。 This is the standard analysis you'd see of optimization convergence both the parameters and the cost。



![](img/9a512611b7f4945c6d5160b215b8b8da_96.png)

 So that's available out of the log reader。 And here is and again I should have made this a little bit more interactive but if you do the model plotter and you give log。

text。

![](img/9a512611b7f4945c6d5160b215b8b8da_98.png)

 You can't really see it very well but if I was able to spin this around I could see that solution trajectory is printed right here the initial value started here。

 And you can kind of see it goes down the back and to the to the minima。

 So if I could spin this thing around you'd see that that was the case。



![](img/9a512611b7f4945c6d5160b215b8b8da_100.png)

 So one of the things but now that's that gives you more insight into what's going on in the in the optimizer and like I said mystic is trying to be very customizable so you can。



![](img/9a512611b7f4945c6d5160b215b8b8da_102.png)

![](img/9a512611b7f4945c6d5160b215b8b8da_103.png)

![](img/9a512611b7f4945c6d5160b215b8b8da_104.png)

![](img/9a512611b7f4945c6d5160b215b8b8da_105.png)

 Basically when an optimization algorithm is built it's built for a certain class of problems right so you you have all of the optimization algorithms were designed for a particular class of problems and things like the termination conditions。

 Which is when the optimizer should stop or that is customized to work for the majority of that class of problems。

 If you don't know what class of problems the optimizer is intended for or you don't have something that fits to that class you're essentially just applying。

 an optimization method and maybe the termination conditions aren't that great for you so you just try a bunch of different algorithms but what the mistake says is well actually don't want to have to pick an optimization algorithm and have the termination condition come along with it。

 I want to be able to customize that so we'll look at a differential evolution solver。



![](img/9a512611b7f4945c6d5160b215b8b8da_107.png)

 I typically use for global optimization and what we're going to do is look at mystics class based interface so mystic says all the different pieces of the optimization algorithms can show up as objects。



![](img/9a512611b7f4945c6d5160b215b8b8da_109.png)

 Here is the termination condition VTR which is essentially stop when you hit this point。

 There's a mutation strategy best one X so takes the best one and out of well I mean just。

 There's a lot of different strategies this is picking the best one in terms of mutation and how it goes forward。

 We'll pick a verbose monitor and then if we go down to the interface we're going to do nine dimensional Chevy chef polynomial and we're trying to fit using differential evolution with the bounds of minus 100 and 100 on each parameter。



![](img/9a512611b7f4945c6d5160b215b8b8da_111.png)

 Put in a verbose monitor where it's going to plot every 50th cost so that kind of shows you where it's at every 50 iterations。

 And here's the here's some of the things that you see from mystics interface is instead of using the I tend to I tend to actually typically use the one liner interface。

 Unless there's something I can't do out of the one liner interface and then you then you can come in to the multi line interface for more customization。

 But take the differential evolution solver on a nine dimensional nine dimensional problem and we have a population so differential evolution essentially says I'm going to try in this case 90。

 So we have potential solutions and then pick the best one of those 90 potential solutions and then go forward and then pick the best one of those 90 potential solutions and keep going forward until for after some time it doesn't find a better solution。

 So with mystics you can also do something like this which is set the initial values。

 So you can either pick the initial points or you can randomly pick the initial points within some bounds using I believe that's uniform。

 I would have to remember I'd have to look at the documentation。

 But also there's set sample initial points which basically allows you to pick from any known distribution your initial points。

 But so there's a lot of different ways that you can start with some initial values either a point。

 So I could do differential evolution and have all of them start from a single a single point which actually is not a smart thing to do。

 You might think it is but it's not a smart thing to do because they work on differential evolution works on mutation of the solution。

 So it's going to start with one solution and then copy that out to 90 times and then work off mutations of that solution to try to find the best value。

 So essentially a very contained random problem to start with what you want is a lot of randomness to start with randomly chosen values and then work from the best one or two of those。

 Alright so there I'm applying a iteration monitor。

 So this is going to again not capture the function evaluations but capture the iterations。

 I'm enabling the handler again let me turn it off and stop。 And then I do solve。

 It gets a result unless I stop it with the signal handler and then I want to get the solution out I can say give me the parameters the solution。

 Alright so。 And this thing kind of runs and here you see it prints every 50。

 50 values it gives the cost it's gotten down towards zero which is good which is a good fit to the。

 Here's the actual Chevy chef polynomial for nine coefficients and here's the value it it fit to that that's pretty decent。

 And here's the plot of the fitted versus exact result。



![](img/9a512611b7f4945c6d5160b215b8b8da_113.png)

 So now one of the things that I'm not getting into that's not obvious here is you have a solver instance。



![](img/9a512611b7f4945c6d5160b215b8b8da_115.png)

 You have a solver instance and solver instance has a lot of things like population。

 So when you do solve when you're done you have the final population you have all of the iterations the trajectories that are available you can look at。

 There's functions that allow you to get them pulled out but they're actually contained within the solver。

 So you can go in and interrogate those and there's functions to go in and interrogate those but they're essentially attributes of the class。

 And the solver maintains its state。 So if you have one of these things that you stop this gives you the ability to restart a solver from where it stopped without any loss of information。

 So what that allows you to do is。 Do a convergence to a solution。

 Change the termination condition change some of the constraints change the solver a little bit。

 And restart so you can do a kind of a faster approximation to a point and then kind of knuckle down a little bit and work harder。

 And you don't have to be satisfied with a solution that seems close。

 You can start up and change the termination condition again。 I'll show a little bit of that。

 In this case we didn't have to。

![](img/9a512611b7f4945c6d5160b215b8b8da_117.png)

 If you look at the interface that we're given here for Mystic this is all the。



![](img/9a512611b7f4945c6d5160b215b8b8da_119.png)

 These are all the different interface attributes we have。

 So we have things like a hold of the generations and the evaluations。

 These are essentially internal monitors that Mystic is using to hold those values。

 You look at things like energy history best solution and best energy。 Those are the X and Y values。

 I used solution above to just essentially return the best solution。

 But in cases where there's optimizers that use multiple solutions like genetic algorithm has population matrix。

 There's other solutions besides the best one that you can get also。

 So there's a number of things like I was mentioning。

 Where we can set the termination condition set box constraints with strict ranges。

 And change basically things like set sampled initial points which are change the distribution。

 of how you're picking random initial points。

![](img/9a512611b7f4945c6d5160b215b8b8da_121.png)

 So things like that。 Now let's look at that gives us some flexibility in configuring our optimization algorithm。



![](img/9a512611b7f4945c6d5160b215b8b8da_123.png)

![](img/9a512611b7f4945c6d5160b215b8b8da_124.png)

 And I didn't even mention setting the penalty and setting the constraints because we'll get to those。



![](img/9a512611b7f4945c6d5160b215b8b8da_126.png)

 With termination conditions one of the things that's nice is being able to say well I want to customize the termination condition to be something that is meaningful to me。



![](img/9a512611b7f4945c6d5160b215b8b8da_128.png)

 And so you can actually write a custom termination condition that is exactly what you're looking for。

 If you have something that's a metric that matters to you you can hook it into a termination condition instance。

 A custom termination condition instance。 And then instead of monitoring the change in the gradient you monitor the change in whatever metric you're looking for。

 Now I didn't do that with these but what I did is I made a compound termination condition out of some of the existing ones。

 So there's VTR and change over generation。 Now change over generation is one of the standard ones for differential evolution or genetic algorithms which is it is going to change less than some amount over some number of iterations。

 And VTR is a standard termination condition for steepest descent value。

 When it gets past this point stop。 So the combination of both of those is to kind of chop off the tail at the end of differential evolution。

 So what you find is to make a lot of the global optimizers work really well you have to put in lots and lots and lots of points。

 So you're sure that it you know it's trying to stop and it's trying to find the next value and it takes 200 300 iterations to find the next value。

 And then it has another 500 iterations before it maybe finds the next best value after that。

 And you end up having these big big big long tails。

 But what happens is when you know you have the answer then you want to stop but you still have to go through this big long tail to get to the end where it actually doesn't do anything。

 And then eventually runs out because it hasn't changed over that generation。

 So one of the things you can do is apply another termination condition like VTR which just says if you've got this value then just stop。

 And so what I'm doing here is I'm compounding these together。

 I'm saying my termination condition is VTR at 1 e to the minus 8 or the combination of change over generation for the default number of times and VTR at zero。

 And then I just hook that up as my termination condition set the termination condition to this。

 And then when we hook that up you can see it runs and this is differential evolution again on the objective function here set the objective function to rows and it runs and eventually stops。

 It prints and tells me that the termination condition actually hit was where the tolerance was one e to the minus eight and not the other compound condition which had change over generation and zero。

 So that allows you to do something a little bit more complicated for how algorithms stop。

 Actually what you find out is what I found out is your ability to solve the problem is actually more driven by the termination conditions than it is by the optimizer itself。

 The optimizer itself the algorithm tends to give you efficiency for getting to the solution algorithm like differential evolution or genetic algorithm some other simulated kneeling。

 That's efficiency to the answer but the termination condition is actually you know you're looking for something that tells the optimizer one to stop。

 And if you have something that matches the criteria you're looking for very well then you're very likely to solve the problem。

 And if you have something that's an abstract condition like the gradient tails off to some small value then you're less likely to solve the problem。

 So it's actually I mean that was a surprise to me is termination conditions are actually stronger than anything else except constraints really and being able to solve the problem more so than the optimization。

 All right so here's an example of setting the using a distribution to set initial points in in some solver you say set sampled initial points。

 In this case you have to use a mystic distribution object which is basically built by mystic math distribution。

 And it takes things like either a random number generator or it takes a site by stats distribution object。

 And what it does is it gives a unified interface for both of those。

 It's nothing big but it just gives a unified interface for NumPy random and side by stats distribution and random number generators to be used within mystic to set distributions in many different places。

 So this is one of them where we can pick the initial values and you can see now I've set the initial values to be in a normal distribution centered on five with standard deviation of one。



![](img/9a512611b7f4945c6d5160b215b8b8da_130.png)

 And what I can do is then go in and look at the solver population that's going to be my initial points and taken in flat and out and plotted in a histogram。



![](img/9a512611b7f4945c6d5160b215b8b8da_132.png)

![](img/9a512611b7f4945c6d5160b215b8b8da_133.png)

 And you can see that for the number of values that I put in here which is about 60。

 It's roughly normal。 That's sampled values centered on five。 Okay。



![](img/9a512611b7f4945c6d5160b215b8b8da_135.png)

 So， let's now look at really where the one of the big。

 big features of mystic is to apply these constraints operators are these kernel transformations。



![](img/9a512611b7f4945c6d5160b215b8b8da_137.png)

![](img/9a512611b7f4945c6d5160b215b8b8da_138.png)

 We go back to penalty functions which we had before which are this perturbation we apply a penalty on the potential energy surface。

 This is what a kernel transformation or a constraint operation looks like。

 A train operator looks like。 You have an objective function F where we've applied some mapping of space。

 a transformation of some space。 Whether it's a dimensional reduction by applying finding the variances。

 the directions that have the strongest variances are a transformation to an easier space to operate over or an application of any kind of constraint。

 Just any kind of functional constraint it can apply to reduce that space。

 So if you had some sort of constraint like we had before with these constraint equations。

 you can apply those constraint equations as an operator and then work only over the solution where it's met those constraints。

 And what you have is you now have the objective function working over a new space。

 the space of only the valid solutions to the constraints。

 So this is what you need for working in a complex space of nonlinear constraints and problems that actually have real physical physics based or engineering based constraints。



![](img/9a512611b7f4945c6d5160b215b8b8da_140.png)

 And you get that of the， so I'm going to just go through some of the examples of it being applied before I'm able to apply。



![](img/9a512611b7f4945c6d5160b215b8b8da_142.png)

![](img/9a512611b7f4945c6d5160b215b8b8da_143.png)