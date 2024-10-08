# P10：SciPy 2018视频专辑 (P10. PyViz - Unifying Python Tools for In Browser Data Visualiza - GalileoHua - BV1TE411n7Ny

 >> Hello， thank you。 You might have seen PIBIS around various places during the conference， here。

 but now it's my chance to actually kind of try to convince you it's maybe a good idea。

 So PIBIS is something that didn't exist a year ago， but it's building on a lot of things。

 that have been worked on for quite some time。 So I'm kind of stealing thunder from other。

 projects by badging them all or making a badge that they're all PIBIS projects。 And I'll get。

 into what that's all about。 But everything I show here should be reachable from PIBIS。org。

 So everything's fully open source， download it all。 It's all ready to play with。 At the。

 beginning of this conference， I gave a four-hour tutorial on it。 You can look at that。 All the。

 materials for that are also at PIBIS。org。 So you can all just don't worry about it。 Just。

 remember that URL。 So now I'll hide the URLs。 Don't need them anymore。 Okay。 So the starting。



![](img/6d59443486e38d65a520b93a4dcf76ab_1.png)

![](img/6d59443486e38d65a520b93a4dcf76ab_2.png)

 point for PIBIS is the situation in Python data visualization right now。 And as you've， seen today。

 there have been a lot of people get up and say their library is great and they。

 show you amazing things with their library。 I've seen some really amazing things today。

 It's really -- wow。 But we try to take the perspective of a user who is faced with something。

 like this diagram。 And it's like， all right， there's a lot of amazing stuff going on in。

 Python data Biz。 I mean， I'll have to get my job done。 So how many people here are professional。

 data Biz？ Like that is your job。 Doing data Biz。 That's what I thought。 There are a few， people。

 That is my job。 But it's not most people's job。 Most people need to get their， work done。

 Data Biz is a tool。 Data Biz is something that helps them enable -- helps you。

 enable whatever it is you're really trying to do。 Which is normally not that。 Normally。

 it's something that lets you achieve your goals in life。 Which are about other things。 And。

 so if you're faced with a diagram like this and you're faced with some beautiful talks， today， like。

 oh， I should use that。 No， I should use that。 I'm going to use them all。 I'm going。

 to learn them all。 I'm going to -- no， you're not。 You're not going to learn them all。 You're。

 not going to use them all。 It's not going to work。 If you do， you will be fired from your。

 current job and you'll have to find somebody who will pay you to do data Biz every day。

 That's very unlikely。 So I work for a company。 It's a job。 And we have -- we help other people。

 get their jobs done。 And we said， well， we're not going to survey all these things。 We have。

 a very specific set of things that we want to help people do。 And we're going to focus。

 on those and make those things much， much， much， much， much， much easier。 That is our。



![](img/6d59443486e38d65a520b93a4dcf76ab_4.png)

 goal。 Specifically， of all the packages that we're around， we focused on a subset of them。

 that we thought were particularly relevant for the types of things we want to do and encourage。

 our government clients， our corporate clients， our academic collaborators to do。 And I'll。

 show you in just a second why we chose this particular set。 But this is a -- if you'll， notice。

 we didn't include anything in the lower right here， which is lots of amazing， 3D stuff。

 You saw some examples today。 We're doing essentially zero of that。 So don't -- don't。

 ask us about that。 We're also not doing anything based on D3。 We're doing things that are based。

 in JavaScript。 And as I showed in a second， we do focus on the browser。 But we're focusing。

 on things that were built just for Python。 There were every bit of the functionality is。

 available in Python。 There's no hidden layer that was -- that's only available to those with。

 the magic JavaScript experience。 Background experience。 So this is kind of another wall， of text。

 But this is the -- the things that motivated why we chose those particular libraries。

 and what it is that we're trying to do。 Number one， we crossed anything off that list that。

 was focusing on a desktop GUI toolkit。 None of the people we work with are comfortable， with that。

 With tying to a specific desktop。 Everybody we work with wants to be able to。

 share things on the web more generally or just inside of the organization to be able。

 to work collaboratively。 So if it doesn't work really well in a browser， we're not interested。

 in having to be part of the -- what we're trying to solve。 We also focused on ways that we can。

 have full interactivity， particularly for linking plots because we want to show a plot。

 And everybody who sees a plot， the first thing they want to do is say， what is that？ And link。

 that to another plot and drill down and drill down and we want to make that easy。 And we're。

 focusing not on people who might have a whole team of web developers at their disposal。 That's。

 great if you do。 Go for it。 But we're assuming that you are a normal person， a Python user。

 and you're trying to get your job done and you do not want -- either you do not know about。

 deeply plumbing the internals of the web or you do not wish to do so because you have， work to do。

 So we're focusing on you using Python， sitting there in your machine and you're。

 starting with your data。 You're not starting with an idea。 I'm going to do coding。 We're。

 focusing on people who are saying， I've got a source of data。 I have a specific data set。

 I have a type of data。 I need to reveal what it is。 I need to communicate it。 I need to。

 understand it， relate it。 That sort of thing。 So you're starting with data。 You do coding。

 as a means to an end， not as your primary goal。 So if coding is your primary goal， then that's。

 a different audience than these tools are built for。 I guess they should be numbered， but number。

 5 here or 6。 We keep encountering limitations where we get used to a tool， we use it a lot。

 and then suddenly data set multiplies by 10 or 100 or 1，000， we have to switch tools and。

 we can't use it anymore。 We want to eliminate that as a problem， have infinite overhead in。

 terms of data size。 You've already seen several approaches to that， motivated by some of the。

 same goals。 The various talk to us now。 We want to be able to not solve all problems ourselves。

 for data is。 We want to say let other people solve， each of the problems that are solvable。

 independently and compose those into a solution for a final test that we're doing。 The advantage。

 there is that you can make -- that we can make use when we build visualizations and explore。

 data of all the work that you find people do in your own domain on general purpose libraries。

 that we can bring into other domains and use to solve problems。 We're trying not to reinvent。

 the wheel， trying not to have a monolithic structure where we solve everything， but a flexible。

 combination， which is why we need a program like PIBIS to coordinate between different。

 libraries and different packages。 Like I mentioned， we're focusing on 2D， it's not like 3D is。

 impossible， but we're starting with a set of things that are fundamentally from a 2D background。

 rather than a swimming through data background。 Other tools are better at that。 And finally。

 this one is a little harder to explain and it's kind of the whole point of all of the， tools。

 which is that we focus on ways that you can use tools where you don't tie your。

 data up with code that is tied to visualization that is tied to a specific desktop environment。

 that is tied to a specific way of working with your data。 These are all different things。

 Your data is independent of your code。 Your code can be independent of whether it's used。

 in a Jupyter notebook， in a server， in a batch system to generate reports in an HBC。

 system where you're running it one billion times。 We want to make sure that people who。

 know a domain can work hard on the code for their domain without tying it， therefore。

 in a particular context of how they're going to view the results。 And that's where we diverge。

 from a lot of the talks that you've seen today， which are going gung-ho into Jupyter widgets。

 We do use Jupyter widgets， but we focus on ways to use Jupyter widgets or other widget。

 libraries where those libraries are not tied into your domain-specific code。 Hopefully that。

 will make sense。 We want to make sure that when you write something today， you can run。

 in a supercomputer tomorrow whether or not it has a GUI， whether or not it supports。

 any form of web anything and keep you -- keep what you've written separate from any of these。

 other technologies。 So we use Jupyter extensively as a tool， but at any moment you can walk away。

 and you'll have bare Python， bare code that you can run in any context。 So hopefully that。

 will make sense。 If not， come back to it， read the website。 You'll see a little bit of。

 philosophy there， but it's mainly just examples。 You'll see how that works every single time。

 So like I said， we're starting with -- we're assuming you've got some data。 So let's assume。

 you've got some data。 It's an appendus data frame。 At the moment， this could be X-array。

 If you have multimensional， gridded data， it could be mesh data。 It could be all sorts。

 of different types of data formats。 We're not making assumptions about that。 So let's say。

 you've got some data frame， you can look at it。 We're trying to make it easy to get from。

 having data to having not just Viz but interactive Viz， exploring data， et cetera。 So here's some。

 data。 If you call appendus dot plot， you can get a plot。 That is a plot。 That doesn't reveal。

 anything about the data。 Maybe I can make it a little bigger here。 The underlying data， if。

 you look at it， was -- this is actually incidents of some diseases over time。 Each。

 month of a year we'll show the number of cases of measles or pertussis per 100，000 people in a。

 particular year and month。 Makes sense？ If you call appendus dot plot， you'll get a plot that。

 shows you the range of years it was collected over and a bunch of other things。 Quite meaningless。

 plot。 So ideally you would always just be able to do dot plot and you get the plot you want。

 and you move on in your life， right？ That's obviously -- anyone who is claiming that you're。

 going to have that is not true。 It's true if you've set things up perfectly。 So let's set。

 things up perfectly。 Let's aggregate our data per year and across all of the -- let's group。

 it per year and aggregate across all of the states， let's say。 And then you get a data frame。

 where that's plotable immediately， right？ You've got two columns。 If you just assume the。

 first one is your x-axis and your second one is your y-axis， you can plot it， which is。

 effectively what appendus plotting does using matplotlib。 And you go to plot。 And now your。

 numbers have turned into something meaningful。 Does anybody can look at that and see something。

 happened in 1963 roughly？ And if you look it up on Wikipedia， you'll see that in 1963。

 there was a measles vaccine and you can see， okay， that's a pretty big coincidence there。

 There's some controversy， right？ What about whether vaccines work？ Not much though。 Okay。 Well。

 we can do the same thing again per state in a second。 But anyway， something happened。

 there and having looked at that， I've captured something。 But what we have here is it's a。

 great way to reveal precisely what we just asked for。 A plot of the default thing， x against， y。

 y against x。 And we've got an image。 We've got a PNG image。 This is matplotlib in line。

 inside the Jupyter notebook。 It's great that you can get an image out of it。 You can't do。

 much with that image。 So I zoomed in， unfortunately， so my slides aren't going to fit anymore。

 All right。 So， and we were able to use Panda's operations basically to format the data into。

 something that will plot automatically。 So one thing that we want to be able to do is。

 make sure that you can do this， but now you can interact with the data and that it's not。

 difficult to do so。 So we have a new package that has a very little code in it， but it。

 builds on packages that were already out there in the PyViz ecosystem。 In fact， it didn't。

 exist when we submitted this abstract， but it does now。 It's called HP plot。 And it's。

 designed to mimic the Panda's API， but give you power rather than the Panda's plotting， API。 Sorry。

 the Panda's dot plot API。 But to give you something that's both interactive。

 and it's something that you can do things with。 So as you can see， it works similarly。

 It's not just in this trivial case， all the different options。 It's quite a faithful copy。

 of the plotting API， but it gives you back a bokeh plot。 A bokeh plot is interactive， like。

 a BQ plot。 You can hover over things。 You can drag them around and such。 So， and the first。

 thing you get basically with this approach is something for free， which is that you don't。

 when it's a static plot， if you want to change anything about it， you have to mess with it， in code。

 So you end up going back to the code and go back and forth between the static plot， and code。

 And number one， you have to be good at code to do that。 And number two， it's。

 awkwardly time consuming。 In this case， if all you wanted to do was select a certain region。

 to look at， or all you want to do is find out what the value is of this peak that much can。

 be done automatically。 That's only a， that gives you a little bit further than you could， before。

 But what's actually being returned here is something that is provided by the， Hall of Use library。

 The Hall of Use library was originally built around the matplotlib。 Nowadays。

 most of our effort is going on to the， it also has a plotly back end， but most。

 of our effort is on the bokeh back end because bokeh supports， well， number one， it supports。

 the type of inplot interactivity that we needed。 And also， it's run by the same company that， I am。

 which is very convenient， because when we need something， we can make it happen and， vice versa。

 So we have a nice relationship there。 Hall of Use itself is not tied deeply， to bokeh in that way。

 It's， as I said， it was originally developed in academia outside of， Anaconda。

 but it's been a very useful way to provide new features。 So the thing about a。

 Hall of Use object is that it's not a plot。 If you go to Hall of Use。org， you'll see it。

 stop plotting your data。 What it does is it annotates your data to make it visualizable。 This is。

 I know it sounds ridiculous and academic， but what it is is that you've got your data。

 and you've added stuff to it that allows， that it's declarative， that allows it to show， itself。

 but allows other things。 And here are some of the other things that it allows。 Let's see。

 we've got exactly what we had in the previous plot。 We did a HV plot on that。

 But now we can work with this， because this is an object that is just a thin wrapper around。

 your data。 It's just your data plus the idea that it's plotable。 And you can do things like。

 overlay other things on it。 In this case， let's actually capture the fact that in 1963 something。

 happened。 And that's something that I would never remember later。 I've given the talk a。

 couple times。 Now I remember in 1963。 But for most things that I notice in a daily life。

 if I don't capture them， they're gone。 I have kids。 But in this case， we can very easily。

 capture it。 And we can combine what we already had as the cheap plot with any Hall of Use， object。

 in this case a vertical line， in this case a bit of text。 And the result is something。

 that also displays and is also not a plot。 So if you look at the object M， it's this data。

 structure。 It's got a bunch of components。 I won't worry too much about that。 I think。

 I'll cover it later in the talk。 But basically you have something that will display as a， talk。

 It is interactive。 You can do stuff with， it took you very little trouble to get， but。

 it's not a dead end。 The picture you got from my plot live is a great picture if you want。

 to put a picture somewhere。 But it's a dead end in terms of further analysis。 You can't。

 access the data in it。 It's a dead end in terms of combining with other things。 And that's。

 what we don't want to have。 We want to have somebody who's empowered while they're working。

 with their data。 To do as much as they want to be able to do with their data without switching。

 to hardcore coding and without being stopped by some arbitrary end of the analysis。 Okay。

 I was going to get to that anyway。 So if you took M and you showed what was there。

 we already saw this。 This is a， that object M was an overlay of a curve and a vertical。

 line and some text。 And if we were to use this indexing scheme， which is confusing。

 by John Luke Stevens， he's in there somewhere， this is his project。 I'm writing PyViz。 He。

 runs Hall of use with Phillip Rüdiger。 If you use this indexing scheme， you can actually。

 get back not only the underlying curve。 So that's the curve that was in there。 You can。

 always pull it back out if it's combined with other objects。 But every object also has the。

 data in there。 So you can always get at the data as well。 So the whole idea is that you're。

 sitting there， you're working with your data， you're viewing it， you're fiddling with it。

 you're messing with it， you're changing it， you're adding stuff to it， you're embedding。

 it and you work with it some more and you're back and forth and you never lose track of， your data。

 Hall of use object is your data。 Your data is always in there。 It's only that， someone。

 one of the major families of things that are supported like XRA and PANDAS， Python。

 dictionaries and NumPy， you know， begin the original， well， at least NumPy， PANDAS and。

 XRA will stay in the original format it was。 Daskeray will stay in the original format it， was。

 So it doesn't add anything to your object， it doesn't convert it。 It just is your data。

 But it's visualizable and you can build， basically you can build up towards a figure。

 you can build up towards a presentation and so on。 And one of the main motivating things。

 that we had is that your data is always much bigger than you can ever see。 It has many dimensions。

 or many columns of data。 You can always just pick little bits to be one time and the idea。

 that Hall of use allows for your data is that if you've mapped a certain set of dimensions。

 of your data onto the screen， in this case， if we've mapped year versus state， in this， case， sorry。

 year versus measles， but the data is additional indexed by state， then what。

 Hall of use does is automatically give you a little widget to say you didn't tell me。

 which state it was。 Hall of use has the notion that there are indexing dimensions， they're。

 called key dimensions and then there are value dimensions and you need to know the entire。

 set of indexing dimensions to know what your data is， what year， what month， what state。

 In this case， we got rid of the month， we kept the year， we did a group body to get rid of。

 the month， but we still kept state。 And if you do that and you don't tell it what to do。

 at that point， you'll get state as a widget， which lets you explore that。 Without having。

 a job of I'm going to program an interface where I add a widget to explore state。 No。

 it's just state is there and you haven't told me what to do with it， so you get a widget。

 It's a very different way of looking at it。 Not one， very much better in certain circumstances。

 and completely inappropriate in others。 But we're focusing on the case where you're sitting， there。

 you've got your data and you want to explore it。 Not on the case where you're。

 trying to build the best of whizming app。 So it's about trying to have very good support。

 for certain goals。 Similarly， if you have an object and you have another object， any。

 number of the objects， it should be very simple， unlike in certain blogging libraries， to。

 just say they should be next to each other or they should be overlaid on top of each other。 You can。

 plus is layout and the star is overlaid。 So that should be straightforward。 So you。

 can easily mix and match and put things as you wish。 I won't really get into， there's。

 a whole system for being able to control the options of these things without collecting。

 your code and making it be a mess。 But we don't have time to cover that。 So the last bit is。

 just to kind of illustrate the， this is all just a notebook you can download。 But the last。



![](img/6d59443486e38d65a520b93a4dcf76ab_6.png)

 bit is just to illustrate， I was trying to do a tutorial style from the beginning。 If。

 you leap ahead and use 30 lines of code instead of 10 lines of code， you get something like。



![](img/6d59443486e38d65a520b93a4dcf76ab_8.png)

![](img/6d59443486e38d65a520b93a4dcf76ab_9.png)

 this which is trying to illustrate the idea that you can be independent of your data size。

 In this particular one， remember it was all about stitching together the existing packages。

 to solve your problems while exploiting those packages。 This is built on desk。 It's running。

 on the laptop， it's got a billion point GPS data set running in the laptop that fills up。

 my 16 gigabytes of memory。 It allows me to have， it's probably all swapped out to disk。



![](img/6d59443486e38d65a520b93a4dcf76ab_11.png)

 by now， but it allows me to have interactive， it's very similar to some techniques a second， ago。

 This is all swapped out so it's going to have to page back in because it's been a。



![](img/6d59443486e38d65a520b93a4dcf76ab_13.png)

 while。 Interactive exploration of large data sets。 In this case， a large data set that's。



![](img/6d59443486e38d65a520b93a4dcf76ab_15.png)

 on my laptop。 But because it's based on number and desk， number makes the individual computations。



![](img/6d59443486e38d65a520b93a4dcf76ab_17.png)

 very fast。 Dask allows me to be distributed across an arbitrary number of processing units。



![](img/6d59443486e38d65a520b93a4dcf76ab_19.png)

![](img/6d59443486e38d65a520b93a4dcf76ab_20.png)

 a number of nodes distributed processing and such。 Here it's all on my laptop so it's。



![](img/6d59443486e38d65a520b93a4dcf76ab_22.png)

 used to use my four cores to work with these billion points。 But this could be arbitrarily。



![](img/6d59443486e38d65a520b93a4dcf76ab_24.png)

 large。 Anything Dask could support。 The more power you throw at it， the larger your data。



![](img/6d59443486e38d65a520b93a4dcf76ab_26.png)

 structures can be。 They can all be distributed。 They're all remote。 In this case it's on my。



![](img/6d59443486e38d65a520b93a4dcf76ab_28.png)

 laptop。 But if it were remote， it would just be just like in the previous talk， rendering。

 on the other side of the wire， passing the image down。 Hopefully that makes sense。 I'm。

 trying to show you from both perspectives。 This is， well， I guess one more thing to mention。

 This is point data。 I think I already mentioned supports， meshes， raster data。 It's agnostic。

 about data type。 It is focusing on two-d visualization with underlying data。 It can be anything。 So。

 on the one hand it has very large sphere of things it could do。 From the other hand， hopefully。

 you saw how you build up to that from almost nothing。 Thank you。



![](img/6d59443486e38d65a520b93a4dcf76ab_30.png)

 [ Applause ]。

![](img/6d59443486e38d65a520b93a4dcf76ab_32.png)

 >> We have a few minutes for questions。 >> I'll leave that there to annoy you。

 >> I have one to start out with。 In your example， when these selection came up for states， it。

 was a drop down。 Does it automatically default to a drop down？ >> For categorical data。

 it will be a slide or for text data。 It will be a text box。 >> Cool。 Any other questions？

 >> Thank you very much。 When I look at your last plot or the last image， so initial。



![](img/6d59443486e38d65a520b93a4dcf76ab_34.png)

 -- so when you zoom through it， it starts up blurring and then suddenly I get --。



![](img/6d59443486e38d65a520b93a4dcf76ab_36.png)

![](img/6d59443486e38d65a520b93a4dcf76ab_37.png)

 >> That's right。 >> Great view。 Can you explain that？ What is happening？

 >> The data in this case is server side in the Python process。 Here I'm in the browser。



![](img/6d59443486e38d65a520b93a4dcf76ab_39.png)

 and there's a separate process。 The browser has very limited memory。 The Python process。



![](img/6d59443486e38d65a520b93a4dcf76ab_41.png)

 uses all the memory on my machine。 Python process has a gigabyte worth of data points。



![](img/6d59443486e38d65a520b93a4dcf76ab_43.png)

 It iterates through those on all four cores。 Each four does -- partitions the data set。



![](img/6d59443486e38d65a520b93a4dcf76ab_45.png)

 into four chunks。 Let's each -- each of those four chunks work independently。 It's iterating。



![](img/6d59443486e38d65a520b93a4dcf76ab_47.png)

 through all billion points。 No matter how much I've zoomed in， it iterates through a。

 billion points。 Finds out whether they fall in the viewport。 Aggregates them per pixel。

 Does that for each of the four chunks， merges the four chunks。

 Turns that over and serializes that as a binary array， passes that into the browser。 The。

 browser color map set renders it as an image and you see it。 And then you zoom in again。



![](img/6d59443486e38d65a520b93a4dcf76ab_49.png)

 The whole thing starts over again。 And so it's all -- at no point is your data ever。



![](img/6d59443486e38d65a520b93a4dcf76ab_51.png)

 present in your browser。 It's always only an image of your data。



![](img/6d59443486e38d65a520b93a4dcf76ab_53.png)

 But because -- and this is a billion points。 If this were only a million points， that's。

 a super easy case and it's immediately snapping and you can't even tell what's going on。



![](img/6d59443486e38d65a520b93a4dcf76ab_55.png)

 If it's a billion points， it's slow enough that I can explain it and you can see how it。



![](img/6d59443486e38d65a520b93a4dcf76ab_57.png)

 works。 Hopefully that makes sense。 And that's all thanks to Numba being ultra fast on the。



![](img/6d59443486e38d65a520b93a4dcf76ab_59.png)

 bottom side and Dask being able to coordinate that across an arbitrary number of processing， units。



![](img/6d59443486e38d65a520b93a4dcf76ab_61.png)

 >> Precomputing an directory of your data on the server side will that speed up the visualization。



![](img/6d59443486e38d65a520b93a4dcf76ab_63.png)

 You will be doing that。 It was entirely our plan all along。 In fact， our plan was to do。



![](img/6d59443486e38d65a520b93a4dcf76ab_65.png)

 that and also to pre-render to tiles。 But we found that it worked so fast on my laptop。



![](img/6d59443486e38d65a520b93a4dcf76ab_67.png)

 that we didn't have to do it for that project。 We have to do it for our next project which。

 is 100 times bigger。 But for this project， it was like， oh， we can get away with this。

 A billion points， that's nothing。 >> Great。 Thanks so much。

 And so now we just have the lightning talks left for today。



![](img/6d59443486e38d65a520b93a4dcf76ab_69.png)

 [APPLAUSE]， [no audio]。