# SciPy 2017（合集） - P9：Anatomy of Matplotlib  SciPy 2017 Tutorial  Ben Root - 哒哒哒儿尔 - BV1Cs411A76Y

 Hello， my name is Ben Root。 I am a quote unquote core dev of Matplotlib。 Yeah。

 my commit history is in the past couple years。 It gone down， but I'm still a very active member。

 And I'll be presenting to you basically the introduction， to Matplotlib for you all today。

 So we'll get started firing up the Jupyter Notebook。

 This tutorial originally derived from something， I made back in 2013。

 And then also originally meant for my coworkers。 And so I had to even do introductions and numpy thing。

 We can skip that。 We'll go straight to part one。 All right。

 I'm hoping everything here is big enough for you guys， to see comfortably。

 I know I have terrible vision， which is very interesting， because I work on a visualization library。

 But the blind leading the blind， right？ So I'd like to make sure that you think they're nice and big。

 for everybody。 OK。 Whoop。 So I've been working on Matplotlib since 2010。

 when I finally got fed up with Matlab。 And then finally， I got involved。

 And I kept running into bugs with Matplotlib。 And eventually， John Hunter。

 who originally created the library， he got so fed up with me sending him patches。

 that he finally gave me commit rights。 This is how you get involved in open source programming。

 by the way。 You annoy the core developers enough that finally they say， you do it yourself。

 You go ahead and commit it。 This had actually directly led me to getting my job， my career， job。

 that I absolutely love right now。 And I've been in for five years now and working。

 for atmospheric environmental research， because of me sending so many emails and doing so many。

 discussions on the mailing list。 And so Matplotlib can get you a job。 Just saying。 Yeah。

 This has also led to me writing a book。 So please go to your friendly neighborhood， Amazon web page。

 And check out my thing。 This book here will cover topics that are not。

 going to be covered in the tutorial today， because they are a bit more advanced topics。

 And I'll explain exactly why they're separate。 But for those who want to learn about how。

 to do interactive plotting， this is the book for you。 There is no other book that does this。

 So Matplotlibs-- you have to go back to the context--， Matplotlibs started off back in 2001。

 John Hunter， he was getting fed up with Matlab。 How many people here are Matlab users hoping maybe one day。

 to become defectors？ Good。 Good。 I was there with you。 10 years ago， I was there with you。

 He got fed up with Matlab， and he， went to code up something himself。

 And through several iterations， it finally became Matplotlib。

 And so it was designed from the very beginning， to be a library that mimics a lot of the behavior of Matlab。

 And so that means， for those who are not familiar with Matlab， is that you just state plot and boom。

 a figure window pops up， in front of you， and you can interact with it， move it around， pan， zoom。

 You can resize that window， do anything。 And then when you're done， you hit the Save button。

 and you have yourself night publication quality figures。

 available for you to use for your papers and things like that。

 John Hunter was working on a biomedical scan imaging， and such， and he needed the figures。

 to look perfect for his papers。 And so that was the origin of it。

 And that's why Matplotlib became so popular in the Python。

 community because it mimicked an API that， was very familiar to many scientists in the community。

 and it produced pixel perfect--， we like to say pixel perfect--。

 images for you without being obtuse。 And for those of you who have worked with other plotting。

 libraries， you know exactly what I mean by being obtuse。 Then on top of that， it became even more。

 In order to achieve that goal of being an interactive plotting， library。

 it had to work on a wide variety of platforms--， so Windows， Linux， and Mac。

 It had to work on a wide variety of toolkit， GUI toolkit， so WEX， GTK， TK， QT。

 It had to work on all of them。 We even had one for Coco， Ag， and Coco， and stuff like that。

 That was all the Mac stuff。 It had to work。 And it had to produce the same result。

 across all those platforms。 Then for the big order， big tall order。

 but John Hunter managed to manage--， and others managed to get going and make that stuff work。

 Text rendering is also another very important aspect， of that， which I won't get into。

 but it was a very important aspect， because scientists need to have their text rendered perfectly。

 because these things are going into publications， such as science and nature and things like that。

 And so it needed to look right or if they'll， get rejected by the editor。

 So that's what you guys are jumping into。 This is the historical context for Matt Flatlib。

 It is one of the oldest SciPy packages out there。 It was only one of the packages I know of that's older。

 and that's in SciPy fun。 Coming onto something here that's been around for a while。

 and it is what it is。 And it does this job very well。 And unfortunately， that does mean。

 that it carries a lot of historical baggage because of that。 And so there's a lot of idiosyncrasies。

 and such that you need to--， once you understand it， it goes， oh， yeah。

 that makes perfect sense in that context。 That's where I'm hoping my tutorial。

 is going to help you with。 Also， the documentation online tries。

 to help explain a lot of the reasoning and a lot of the way。

 to think about things so that it starts to make sense。

 To people who are not just coming from MATLAB， it needs to also make sense to those who are coming from R。

 those who are coming from other graphing tools as well。

 And those who are just coming completely fresh， and hadn't come from any previous tool at all。

 we need to make sure that all of you guys can get， to learn and understand。

 So the documentation has FAQs， it has examples， it has direct API documentation。

 We have these things to help suit many different people's。

 needs and experience level so that we can help you guys， out in different ways。

 I consider it the most important at the gallery。 It ends up happening unlike in other libraries。

 that you guys have learned about in the past couple of days。 With MATLAB。

 a lot of the things you want to do， you're trying to describe images。

 You want your plot to be organized this way， and you need your titles over here。

 and you need the font to be this type。 And ask those questions in a Google search or whatever。

 That's rather difficult to do。 But the gallery lets you browse through a whole bunch。

 of pre-made canned examples that cover a wide variety of things， you can do in MATLAB。

 And when you look through those images， you can then see the pieces of things you want。 You go， oh。

 so that's how you make the background black。 Oh， that's-- I see in that one， that's。

 how I do a polar plot。 And I see in that one， that's how I can have my markers。

 in this shape or something。 You can see the pieces of it and then when you click。

 on any one of those images， it'll， take you to the source code that made it。

 And the source code for these examples， are very-- at least I hope they're very well commented。

 If you feel that they're not commented， please submit some pull requests to help us further。

 explain them more。 But they're pretty well documented。 And they're very targeted in what they do。

 So that way you're not getting lost in the gigantic。

 huge example of that do like 50 different things。 They focus on one or two different things in each image。

 so that you can see， how do I do this？ How do I do that？

 And eventually when you use the gallery more and more。

 you actually then start getting used to the gallery。

 and you keep referring back to the gallery all the time。 I remember I one time saw that image。

 and you go back to the gallery and you go find that image。 Yeah， that's how you do it。

 I do this all the time。 10 years now， I've been working on that plot。

 I still go back to the gallery to get things。 I think that I would remember seeing some image that。

 came through once or something like that。 And feel free if you feel that you've come up。

 with a nifty little graph or whatever， we love examples。

 to add to the gallery so that it makes the gallery much more， useful for everyone else。

 Some other ways to learn more map plot lib， as I mentioned， the mailing list is that is exactly how。

 I got my job。 And so the mailing list is a very useful resource。

 You can talk to the developers directly， and talk to other users like yourselves who。

 might have encountered similar problems as yourself。 We're very friendly on this mailing list。

 and no question is stupid seriously。 I've received questions and people always apologize。 No。

 don't apologize。 Just ask your question。 We love for you guys using our software to get the things done。

 because we're helping to advance your science。 So in some way it actually improved my impact factor。

 So I kind of like that。 We're also on stack overflow。

 So if you have karma points you want to boost up， you can help answer each other's questions on stack overflow。

 We also recently joined up with Gitter， which， is sort of like a chat system for GitHub projects。

 So that's another place you can go to if you have a GitHub， account。 As I mentioned。

 Matplotlib rehopes the project on GitHub， and bug reports and issues， things like that。

 One thing we have are maps。 They're matplotlib enhancement proposals。

 So let's say you're not quite ready to actually implement， a feature， but you've got yourself。

 a very well-formed idea of something， that you would like to see matplotlib。

 You can actually put together a map that describes in detail。

 what you're thinking of as an improvement to matplotlib。 And you can submit that。

 And then we can refine it and things like that。 And when things get well written out， maybe by then。

 you might be willing to try implementing it， or one of us。

 other developers may be inspired by it and go， ah， yes。 I know how I can implement that。

 And we'll go ahead and implement it。 And your map may be accepted for inclusion into Matplotlib。

 And I mean， it really， honestly， it feels really， neat to see a feature that you make being。

 used by people all around the world all the time。 It feels fantastic。

 It's much better than any of the scientific software， I wrote as an undergrad。

 So moving away from documentation， stuff like that， you're going to hear me mention backends。

 This is a crucial part of Matplotlib。 And one of the reasons why Matplotlib became so successful。

 is because it works on so many different platforms。 And so Matplotlib provides to you guys。

 a single interface you to deal with。 You don't have to worry about whether or not you're on Windows。

 or you're on Linux and you're on a Mac。 The same Matplotlib script that you write。

 a Python script that you write that you use at Matplotlib， will work on all three。

 And it doesn't matter which GUI you're using， or things like that， it will work。

 What Matplotlib does is it swaps out different backends， depending on which platform you're using。

 And so sometimes you do run into the odd little bugs， and maybe back-end dependent。

 And so sometimes when you go to the mailing list， and you're reporting a problem and something not quite right。

 one of the most common questions you'll be asked， is which back-end you're using。

 'Cause sometimes we'll find a bug that way， that there might have been a mistake made。

 in one of the backends and then no one else in the world。

 is running into it because you're the only one， using that back-end， it happens。

 But that's what we mean by back-end。 And so the way you find out which back-end you're using。

 your import Matplotlib， the other thing we always want to know is your version。

 That's how you get your version， and that's how you get your back-end。

 So right now I am running version 2。0。2， which is the latest bug fix release。

 And I'm using what's known as TKAG。 Don't worry about what the detail of what that means。 Yes。

 the name is what's important to us developers， if you're reporting a bug。

 So that's how you find out that information。 But 99。99% of the time。

 you will never need to worry about this。 Seriously， we designed Matplotlib。

 so that this is not something you have to worry about。 It's only when you run into an issue。

 that you then have to at least tell it which one it is。 So IPython。

 IPython being basically the interactive version， of Python， we have special hooks with IPython。

 so that and with Jupyter so that our plots， are interactive inside the notebook。

 And there's a few different back-ends for doing this。 The one we're gonna use for this tutorial。

 is called MBAG which was the notebookAG backend。 The reason why I chose this one is because then。

 one it demonstrates how one would explicitly state， which backend you're using。

 but then it also forces you us to use， the same sort of commands we would use。

 as if we were running a Python script。 IPython， they kind of like making things a little bit simple。

 so you don't have to actually say to show a figure。

 or something like that that it would just pop up， right away。

 I wanna make things feel more like you're writing， a Python script and so we're gonna use MBAG。

 'cause it lets me force that。 But you don't have to， there are other options。

 you can use with Jupyter。 So we're matplotlib。use， MBAG。

 that's how we'll activate this particular backend， for our tutorial。 But this use command。

 you would never use this in， you would not need this particular command， in your Python script。

 You would never say use MBAG in your regular Python script。

 You would only use this in a Jupyter notebook maybe， and just in this context。 Okay。

 You guys weren't here to hear me drown， you guys were here to see me do some plots。 So。

 just to make sure that we're all on the same vocabulary， let's piece apart what a plot is。

 All right。

![](img/e4958744496fcbb23b7c948eb7b9c702_1.png)

 So this is a figure window， call the figure。

![](img/e4958744496fcbb23b7c948eb7b9c702_3.png)

 and it's gonna contain， it's just the figure window， it looks like a regular GUI window。

 but it's the figure and on the figure， you will have a variety of different things。

 You're gonna have what's called the axes or subplot， they're mostly synonymous。

 You'll also see a toolbar sometimes up on top， sometimes it's down on bottom。

 So the axes and the subplot is this area here， you have the y axis and the x axis。

 You're gonna have ticks and labels and other sort of things， where the graph gets drawn。



![](img/e4958744496fcbb23b7c948eb7b9c702_5.png)

 These are the names of the things， that we're gonna be dealing with。

 That makes sure that we're all on the common thing。 So the figure contains the subplot or the axes。

 the axes contain the two or potentially more axis objects。

 and a figure can contain multiple subplots， or multiple axes and you'll see examples。

 of us doing that shortly。 Most of the plotting can happen in an axes， or subplot object。

 And that is the white area that you saw in the figure。

 and we'll see commands on how to create those pretty easy。 These are gonna be the typical commands。

 that we're gonna use pretty much in every single script。 You want an important NumPy。

 and you're gonna want to import mapplotlib。pyplot as PLT。 This is a common convention。

 the de facto standard。 You'll see a lot of examples on the web。

 where in which they make this assumption， that NumPy is imported as MP。

 and that the Pyplot module is imported as PLT。 All right。

 so let's just start off with the very first thing。 Let's make a figure。 (mouse clicking)。

 Nothing happened。 Why？ Because by default， mapplotlib will not show you anything。

 until it's told to do so。 Again， this is the reason why I chose the MBAG back end。

 because this behave most like your usual back end。

 when you write up a Python script with mapplotlib。 So by default， it's not interactive in the sense。

 that the very first graphing command you do automatically， forces the window to show up。

 It will just go， okay， I have a figure。 Good， nothing gonna show yet。



![](img/e4958744496fcbb23b7c948eb7b9c702_7.png)

 You need to actually say， when you're ready for this thing to show up， you need to say plot。show。

 Boom， right there。

![](img/e4958744496fcbb23b7c948eb7b9c702_9.png)

 Yeah， there's nothing on our figure here， but that is a figure。 Now， we just saw four commands。

 Importing NumPy didn't even need to do that for this， but the imported mapplotlib。

 you created a figure and you showed it。 Those three things， that is gonna work。

 on every single platform， computer platform you do， to long as it has a monitor。 It'll work。

 We even have people who have it working on Solaris。 So it's going to work。

 We have people doing it on Raspberry Pi's。 It works。



![](img/e4958744496fcbb23b7c948eb7b9c702_11.png)

 So there's a lot of work that went into making this happen， and making this thing work for you。

 So what can you do with this figure？ Well， not much。

 Especially not since it doesn't really have anything， to plot yet， but you got your toolbar here。

 the home。 So let's say you did some zooming， did some panning。

 and you want to go back to where it looked like originally， you'll hit that home button。 Back。

 we'll go back。 You made one pan motion， you hit back， you'll go back a pan motion。

 kind of like in the browser。 Go forward a particular interactive motion。 There's how you would pan。

 That's how you draw a zoom box。 And then finally， this floppy disk icon。

 which apparently I've been told no millennial knows， what this means。 You know。

 I like to think that it's the five inch one。 You can resize this plot。 You can resize this figure。

 (mumbling)， The icon， what？ (mumbling)， Yeah， yeah。 Yeah， I know。

 maybe we're a little bit behind the times， in this respect， yes， but， damn it。

 I like that stupid icon， you know。

![](img/e4958744496fcbb23b7c948eb7b9c702_13.png)

 (laughing)， I don't like the computer being too smart。 So you just saw。

 they were able to resize this figure。 Well， you could also ahead of time specify。

 what the size of that figure should be， and you'll give it a tuple of width and height。

 and the width and height is in inches。 Now， it's something someone asked a couple years ago。

 when they did this， oh no， it's not five inches， on my monitor。 That's not what we mean， all right？

 It's that many inches， you know， when you save it in that data format。

 you record how many inches it should display at， and stuff like that， yeah。 A lot of times。

 a lot of people don't know， what size to use， a good estimate size to use。

 I love this function called Big Aspect。

![](img/e4958744496fcbb23b7c948eb7b9c702_15.png)

 where you'd say I want it to be twice as tall as wide， so you've passed two into Big Aspect。

 and it will produce for you a figure size， that is reasonable， and is twice as tall as it is wide。

 Wonderful， underbar， great。 So it's a useful function to have， you know。

 if you ever want to be able to control aspect， otherwise it's just gonna be roughly square。



![](img/e4958744496fcbb23b7c948eb7b9c702_17.png)

 So by default。 All right， so。

![](img/e4958744496fcbb23b7c948eb7b9c702_19.png)

 the figure by itself is not very useful， so let's actually get into something a little more interesting。

 Let's add a subplot。 Oh， MATLAB users， you may be very happy or very， very concerned。

 seeing this wonderful little idiosyncrasy of MATLAB。 111， or 170， whatever。 Yeah， we support that。

 You don't have to， but we support it。 I'm not gonna say it was a very smart API decision。



![](img/e4958744496fcbb23b7c948eb7b9c702_21.png)

 on MATLAB， but we support it。 So now look， we got ourselves a figure。



![](img/e4958744496fcbb23b7c948eb7b9c702_23.png)

 It has a title， it has a Y-axis label， it has an X-axis label。

 and it has a default X limits and Y limits。 What more could you ask for？

 (audience member speaking off mic)， So some things you may notice， we use this thing， X。set。

 is a nifty little convenience function， so you can set multiple things all at once。

 So we can set the X limits， we can set the Y limits， set it title， we can set a label for X and Y。

 very nice and nifty。 You could also explicitly set each individual value yourself。 We have X。set。

 Y label， X。set， title， we have individual functions methods as well。

 We give you a plethora of choices。 All right。 There are times where you wanna use the individual setter。

 For example， when you're setting， let's say the Y label。

 you get back a text object that you can then mess around with。

 you can also be able to set additional properties， for that object as well in that call。

 but when you're just simply setting a label， and you don't care what the label size is。

 and you don't care about which font and what color it is， that's a very useful thing to have。 Again。

 Matplotlib tries to make things easy， but also does not try to be in your way。

 by forcing you to indicate every single mundane detail。 (， )， So， what we just saw。

 the set command up here， this is the equivalent。 You see that the very last one returned back to us。

 a text object， so each call the set X label， set Y label， each set title would have returned back。

 an object that we could have played with if we wanted to。 You'll see examples of that later。 So。

 clearly， there are times where you want to use set。

 there's times where you want to explicitly set each property。 All right。

 I bet you're really champing at the bit， for getting some plotting done here。 So。

 let's just introduce ourselves to two very simple， common plot command， plot and scatter。 So。

 here we created our figure。 We created an axes object， or a subplot object， 111。

 and we're going to plot the very simple data。 There's our X data， there's our Y data。

 and we're going to give it a color。 And there's our scatter plot， there's our X data。

 there's our Y data， and we'll give it some color。 Oh， and specify some line with。

 we'll go into more detail， about this later， but you can specify。

 these are all optional things to specify， you don't have to give them， and we'll set some X limits。

 and then show it。 All right， and there we go。 We have ourselves some triangle markers from the scatter call。

 and the plot command drew ourselves a line。

![](img/e4958744496fcbb23b7c948eb7b9c702_25.png)

 Very simple， at least I hope it's simple。 It's not complicated at all。

 it's going to do exactly what you tell us to do。 So， here you just saw me use the。

 what's called the object oriented interface， where I created the figure， and then from the figure。

 I created a subplot axis to use， and that for the axes， I called the plot for that axis。

 I called the scatter for that axis， I set the X limits for that axis， I was explicit。

 I said that I want the scatter to be in this axis， I want the plot to be in this axis。

 It is tedious， but it says exactly what you mean it to say。

 This is the preferred style of coding things up in matplotlib。



![](img/e4958744496fcbb23b7c948eb7b9c702_27.png)

 and we highly encourage it， it's called the object oriented interface， and it remove ambiguity。

 However， we recognize that not everyone uses matplotlib。

 to do operationalized 5/9 uptime battle tested type stuff。

 But sometimes you're just simply starting up iPython。

 and you just want to type away a couple things， you don't want to be typing out all this extra stuff。

 The equivalent command from what we just saw above is this， where you just take the plot， that plot。

 and it will plot it。 You do plot that scatter， and it will scatter it。

 and then you do plot that X limit， and it will set your X limits。 Why does this work？

 Because it made assumptions。 When you first call plot。plot， in fact， I'll show it， it will run。

 It's going to produce the same exact plot。 Why did this work？ Because the pie plot interface。

 it assumes that you're working on the current figure。

 and it assumes that you're working on the current axis。

 Those of you coming from matlab are very familiar with GCF and GCA。 That's what is going on here。

 is that if there is no figure already made， pie plot will create one for you。

 If there is no axis made and you're doing a plotting command， it will create one for you。

 and it will always be whatever the current one is。

 This can cause confusion if you're doing more complicated plots。

 That's where then you want to use the object-oriented interface。

 But for very simple plots like this， this is very concise。 It's nice and easy to use。

 It is perfectly fine to do。 Provided you know when not to use it。

 One justification I do have for this is PEP20。 PEP20 is the Python enhancement proposal number 20。

 and that is the， DENT of Python， which is that the 20 rules of Python of which 19 were written。

 One of them is explicit is better than implicit。 Think of pie plot as the implicit interface while the object-oriented interface is the explicit one。

 It makes it really clear what exactly you mean every single time when you do it that way。 All right。

 We've done an example where we created the figure and we added one plot to it。

 We need two plots side by side in one figure。 Well， plot that subplots。

 So before we showed you you created a figure and you added a subplot。

 That's an old interface and derived mainly from MATLAB。

 This is a somewhat newer interface that we added about a few years ago。 Plot。subplot。

s at the end where it will create the figure for you and return back for you an array of subplot objects。

 So you say that you want two rows and two columns。

 You're going to get back a figure object as if you had called plot。figure。

 And you're going to get back all four of your axes object all at once。 Rather than you add one axes。

 you do your plotting。 Add the next axes， you do your plotting。

 That's the old interface with subplot。 This is the new， you know， nice， shiny， you know。

 all the cool kids are doing it interface。 You get back a NumPy array。 And in this case。

 because it is two rows and two columns， it's going to be a 2D NumPy array。 And each element。

 and it's going to be arranged in the same way that it would appear。

 So let's just quickly show what this looks like。 Look at that。 Nice， simple defaults。

 You got yourself four perfectly valid subplots that you could work with。



![](img/e4958744496fcbb23b7c948eb7b9c702_29.png)

 What you're specifying is just one row。 You get a 1D array。 If you're specifying just one subplot。

 then you actually get back just a scalar single axes object。

 But you can index this 2D array like this。 So the subplot at zero zero， subplot is zero one。

 subplot at one。 This looks like just regular indexing with NumPy。

 I did that to set the title for each one of these。 Upper left， upper right， lower left， lower left。

 work。

![](img/e4958744496fcbb23b7c948eb7b9c702_31.png)

 Did exactly what you expected to do。

![](img/e4958744496fcbb23b7c948eb7b9c702_33.png)

 And then if you don't pass any arguments， it's as if you said one row， one column。

 So any time you see the combination figure equals plot。figure and acts equal add subplot。

 one one one。 That wonderful one one one。 You can replace that with just this one single line right here。

 And it's identical。 So if you see old code， swimming around in the internet's out there。

 you can just mentally just replace that with that。 And it's identical。

 So you'll sometimes see me go back and forth between using the two interfaces。

 That's just simply for demonstration purposes and things like that。 This is also good for regular。

 gridded layouts。 If you want more complicated layout。

 in which let's say you want a subplot to span two columns or span one or more two or more rows or something。

 There are other tools that you will need to go to use that in which you have to then create your own figure first。

 And then you start mucking about with that。 But again。

 Matplotlib tries to make the easy things easy for everybody。

 The ones that use cases that most people want。 So can you as an exercise reproduce this figure right here？



![](img/e4958744496fcbb23b7c948eb7b9c702_35.png)

 We have ourselves three subplots with a sine wave and a title for each one of these subplots。

 Also notice no ticks labels anything like that。

![](img/e4958744496fcbb23b7c948eb7b9c702_37.png)

 So let's come down to this example here。 I give you a little something to start with。

 So important NumPy important matplotlib is plot。 I even give you data。

 I even give you those title names。 Let's spend five minutes。

 Can you reproduce that figure and indicate on slack when you're done so someone can make a check box or something to repeat for people to indicate。

 So five minutes。 Let's take a look。 So the quick question was is there a title that is overarching of all titles？

 The super title if you will。 Yes， there is a function called subtitle。 It's the super title。

 So it's kept at the very， very top of the figure and it always looks absolutely squashed and terrible。

 But yes， it is called the subtitle。 Yeah， for those of you who don't know， shift enter。

 Really great way to。 All right， so let's catch up here。

 Not meaning to utterly show my sneaky way for how you guys can cheat in all the future exercises。

 but。

![](img/e4958744496fcbb23b7c948eb7b9c702_39.png)

 There you go。 Just reproduce the figure right here。 So something you're going to see here。

 you're going to see used a few times plot。style。useclassic。 So matplotlib right now is on version 2。

0。 It took us two years to go from version 1。5 to version 2。0。 And in 2。

0 we actually made practically no API changes， but we did do a massive style overhaul because people said that our。

 Plot looked old。 Yes， but you know what？ When people were complaining about it。

 I created a style called classic because it's not old。 It's classic。

 I could have also gone with retro， but I felt like not enough people would know what that meant。

 So classic， so a lot of things change with this thing。 And so from time to time。

 when you do really do want to keep the old style or you're trying to avoid certain differences in behavior。

 you can go to the classic mode and you restore some older behavior。

 And sometimes I said that this presentation would allow you to use version 1。5 or version 2。0。

 There can be some examples while I say use the classic mode。

 That's what it's for just so that way people on 2。

0 will see the same things as the people on version 1。5。

 So here we created those subplots to three rows and we're going to loop over them。 Remember。

 this is a 1D numpy array so you can just do a zip on it and then we provide the Y1， Y2。

 Y3 and also the list of names。 And so zip。 Most of you guys did your software carpentry training and stuff。

 You guys know what zip is and such useful。 So that way it will let me。

 and basically each one of these is a three element list。

 And now I'm going to zip them so that way I have each iteration of the loop acts Y a name and I can then do a plot command for a axis object at a time。

 Plot， X， Y， Color， just because I want to give it a color and set。

 And this is how this may have been the harder part for you guys。

 That's okay but you can blank out the ticks by saying X ticks equals an empty list Y ticks equals an empty list。

 I'm not going to say something。 I admit I do a lot of this in the ableist type language。

 I say oh it's just that simple。 I don't mean it。 I'm sorry。

 I know people are Berkeley and not happy with me。

![](img/e4958744496fcbb23b7c948eb7b9c702_41.png)

 Yes， it's simple once you understand it。

![](img/e4958744496fcbb23b7c948eb7b9c702_43.png)

 I was in your position one time and then there you go。 You made a wonderful figure。 All right。

 Do you guys want to take a quick break because the next section is actually rather long。

 If you want to grab coffee or something and go to the bathroom or something like that you can come back。

 If you need to just quick five minutes。 A really good question that came up that may be confusing some of you because chances are you're not perfect like me。

 You had errors。 You had an error with your code and you threw an exception or something part way through。

 And so then therefore a figure never showed but a figure was created。

 Then you go back and you fix your code and you become perfect like me and you execute that and it does create a brand new figure。

 But the other figure was still in memory and then when you call plot。

show both figures show up and you go what this other figure here。

 It came from your previous failed attempt to be perfect。

 But that's all it is and the next time you run it it will disappear and everything will be all hunky dory。

 Hopefully by this point even if even many of you who did not really get to be following along with this first notebook。



![](img/e4958744496fcbb23b7c948eb7b9c702_45.png)

 Hopefully we got the rest of you up and running。 Is anybody still not actually able to produce these images the way you're expecting it to？

 If you do we still have people here who can help you。

 Because you're at a plotting tutorial and so not being able to view plots is well you be in for a very boring three hours because I guarantee you the jokes get really flat after this。

 So we're now if you go back。 So if you can go ahead now and close out that part one notebook and you come back come back to this list of the available notebooks you can then go to part two plotting methods overview。

 You click on that and a new tab opens up。 We're at the visual overview of plotting functions。

 All right are you ready？ Anyone not ready？ I'm learning something from chocolate carpentry。

 Anyone not ready？ Right。 Okay。 We've talked about how we were laying out those subplots and we haven't actually talked much about the plotting itself and what store the plot。

 We showed an example of a simple line plot and we showed an example of a simple scatter plot but we never really talked about them and I guarantee you matplotlib would not be as popular as it is today if those were the only two plotting functions it provided。

 Although it still be better than matlab。 Now we do have documentation on every single。

 I got to watch my language every single plotting function we have。

 We have a nerve a lot of them and we have the gallery it covers over most of those。

 We even have a page in our documentation that lists every single plotting function we have in all different variants and things like that。

 And it is a giant monstrosity of a page it's one of those things that just happened when you're applying one of the most popular plotting libraries out there。

 Because everyone and their mother wants to be able to plot using your library。

 I'm not going to go over all of them。 I might even provide you a link to it because it's just it'll scare you。

 But I'm going to talk about I'm going to try to break them down into categories and talk about some of the main ones。

 The things that are going to interest 99% of you。 Again。

 you see this theme a lot in matplotlibs that matplotlib satisfies the needs of 90% of you and then the remaining 10 or 1%。

 You're not trying to prevent you from doing what you're doing。

 You're not as we say stupidly unhelpful。 So this tutorial in general is going to be more to wet your taste for all this。

 It's going to wet your appetite。 This is going to get you interested in what weight。 What can it do？

 It's going to help you with that。 Hopefully you'll get you interested in coming on to the mailing list and chatting with us and finding out the more things that it can do and get you to go to the gallery and explore and discover all the other things that matplotlib can do。

 So let's go over the basics。 What most of us have？ We have 1D data。

 time series most likely or some other sort of thing。 So we have plot with and without markers。

 We have scatter。 Now something to make very， very clear and this is a misconception that happens。

 What is a plot？ What is scatter？ A lot of people will say， well。

 scatter is just plot but without the lines。 That is technically incorrect。

 But more than technically incorrect， it is just wrong。 It is just a common misconception。

 If you want to make a plot of markers just simply without lines。

 then you can use plot and just say that you don't want a line。 It will be faster。

 much more efficient and it will be much more explicit of what it is you want。

 If what you really want in a situation where you are plotting markers without lines is that you want to be able to color them based upon some other piece of data or you want to size them based on some other piece of data。

 As you will see in this example here， we have the same marker just at different sizes or the same marker but at different colors or sometimes both。

 That is what scatter does。 That is the purpose of scatter so that you can size or color your markers accordingly to some piece of data。

 If you just simply wanted to put markers down but without a line， use plot instead。 Bar graphs。

 we have many different kinds of bar graphs， we have bar graphs up the wazoo。

 You can do so many different things with bar graphs。 It is crazy。 We have the generic fill。

 So basically you specify the outline of a polygon and everything inside that is automatically colored a certain way。

 But then you can also do fill between something。 You can do a whole bunch of these special little plots。

 You can do stack plots and things like that。 They are all very pretty， very useful。

 So that is the 1D type data that most people are typically used to。

 My bread and butter dealing with images， I do a lot of image processing。

 satellite data and things like that。 So I am only viewing images。

 So we have IM Show where you can pass it some data to show it or you can pass it RGB arrays red green blue channel arrays。

 So basically it is a 3D array。 So M by M by 3。 We will go into detail later。

 Then you can display any image you want。 There is peak color which is a more generalized form of IM Show。

 You can do various things like that。 Again， we will go into more detail。

 If you click on any one of these images you will see the code that produced these。

 So you can download that and you can see how it was that we made it。

 So contour will produce just the lines at equal level intervals at level curves of your 2D data。

 So contour F will produce the polygons representing the regions in between the level curves。

 And then if you want to have outlines of those polygons you will do 2 calls。

 You will do 1 to contour and then you will do the same call to contour F and you will get that there。

 And then you can even have contour labels available。 And that is called C label as well。

 I don't get into this in this tutorial how to do that。

 But if you click on this example you will see how to use C label and do that。

 And of course that is also in the gallery。 Any hydrodynamics or meteorologists in this room that we do vector fields。

 I guarantee you about half the core devs in Matplotlib are meteorologists。

 So because we have majority vote we put in a bunch of meteorology things too。 Yay meteorologists。

 I'm a meteorologist by training。 So we like wind barbs and stream plots and things like that。

 We have arrow， quiver and stream plot。 We also literally have wind barbs。

 So any meteorologists here who are used to seeing those meteor images and you see that ground thing with the barb going on。

 We actually have some of that。 Not in Matplotlib proper but you can get a separate package and have that available for you to use。

 We have data distributions。 So we have histogram functions。 We have box plots。

 We have violent plots。 All very useful tools。 The estimator type things that are used here。

 We have some very basic estimator built in。 But we can also offload the estimators to some other package as well。

 So some people like that。 And I had just now noticed yet another bug。 Stas tick to call。

 When we move it over to Matplotlib we'll file a bug report。

 So again we'll do the common import and some of the other common setups that you just don't want to get distracted with。

 All right。 So let's take a look at bar plots。 We already did plot and scatter for the moment。

 Let's take a look at bar。 The regular bar command assumes that your bars are straight up and down。

 We also have bar H where it assumes that your bars are horizontal。

 You can also we also have a call signature for the bar function where in which you can literally just pass in list of length height width。

 And what's the B stand for？ I have no clue what maybe it meant to be death or something。

 I don't know。 Box bottom bottom。 Yes。 I didn't come up with the call signatures。

 I like the length height。 You can just pass in。 And so you can actually create like basically your view of Manhattan if you want。

 Okay。 More like Kansas。 So let's just do a very simple example。

 I'm just going to create some random data。 Create my figure and my axes just to subplots here and my big aspect。

 I'm going to make this figure two times wider than it is tall before when we did big aspect to it was twice as tall as it is high。

 Now we're going to do the other way around the inverse。

 And we're going to in each one of these we're going to do a couple of our plots。

 I'm also going to take this moment。 I'm going to show off yet another function。

 Axe H line and acts V line。 So we're going to do H line for the first sub plant and V line for the second one。

 I'll show you in a moment why that's really useful。 Let's create that。

 I just also realize I haven't actually demonstrated the interactive aspect of map plot lib。

 So I'm going to pan here。

![](img/e4958744496fcbb23b7c948eb7b9c702_47.png)

 We have ourselves these are and we have that acts the acts H line。 So the horizontal line。

 And why is that really neat？ Well， no matter how much I zoom that line is going to show up。

 It's much better than doing your own little plot from zero to five。

 Because then as you zoom around from left to right， you're not seeing the edges。

 This thing will go on for infinity。 It will always be there。

 So as a nifty little feature to have available。 We are working on a feature in which you can do an arbitrary orientation of a line。

 Some people working on that is a little trickier than we thought。

 But it will be a really neat feature。 It's very common in GG plot as those coming from R。

 I'm going to pan around here。 That vertical line again will go on for infinity。 Very useful。

 But yeah， you see the text labels move as you pan around。 Everything moves around for you。

 And that's one of the powerful features of map plot lib is that this interactivity you get for free。

 Notice that you didn't have to code up a single thing to make those tick labels move with you。

 Notice you also didn't have to code up a single thing to come up with those tick labels。

 Those tick labels were figured out for you automatically。 Now you can override them if you want。

 But again， it's not being stupidly unhelpful。 It's that map plot lib will not get in your way if you want to do something。

 But if you don't specify something， it will put in some very decent default values that are a good heuristic of what you want most of the time。

 [ Inaudible ]， Yes。 All the standard GUIs， yes。 Now there is one GUI back end， the QT back end。

 They actually have an extra button right here。 That's because when the person who gifted that back end to us like 10 or so years ago。

 he added that feature in but then never did it for the other one。

 So one day we're going to have it across all of them。

 There's somebody working on a module for map plot lib that will make it easy to create cross platform widgets and things like that。

 But we spent the past two years working on the style overhaul。

 So now we're trying to catch back up with everything。

 So we'll have that eventually soon so those things will be available to everybody。

 And to all back end。 So yes。 So you also noticed that when I called the bar method on these axes。

 sometimes you'll see me capturing the return from that and sometimes you'll see me just letting it drop。

 You don't actually need to capture it most of the time。

 The only times you need to capture that in a variable is if you want to modify the properties after the fact。

 That's sometimes useful but not capturing that。 We already are holding a reference to it inside the figures and the axes and such。

 So it's never going to actually get garbage collected until you close out that figure。

 So you don't have to worry about Python destroying those objects for you inadvertently。

 It will only destroy them once your figure is closed。 So you don't have to worry about losing that。

 But if you want to modify properties， it's perfectly fine to capture that thing。 So this time。

 so we have a situation。 This is perfectly fine for most people。

 But what if you wanted those three bars there to be a different color because they're in the negative area。

 Now we could have done two separate calls to bar and had one of them be blue and one of them be green and had one of them be red。



![](img/e4958744496fcbb23b7c948eb7b9c702_49.png)

 But let's just for the sake of demonstrating why one might capture those objects that are returned by those functions or those methods。

 Let's take a look。 I could do that bar right there and then I can zip over that thing that the bar method returns a tuple like object of bar objects。

 And I'm going to check what the height was for that one。 And if it was negative。

 I'm going to set its edge color to red and salmon because I can。 Because I like fish。

 I told you the jokes were going to get worse。 So now notice I didn't do that axes h-line。

 So now that axes h-line isn't there anymore。

![](img/e4958744496fcbb23b7c948eb7b9c702_51.png)

 So zoom around。

![](img/e4958744496fcbb23b7c948eb7b9c702_53.png)

 But here I just simply showing how to make those how to make any of those bars that were negative a different color。

 You know， it's a bit of a contrived example。 Yes， but that may be a situation why you want to retain these objects and be able to do things with them。



![](img/e4958744496fcbb23b7c948eb7b9c702_55.png)

![](img/e4958744496fcbb23b7c948eb7b9c702_56.png)

![](img/e4958744496fcbb23b7c948eb7b9c702_57.png)

 Sorry， in this case I just did the regular I just did the first one。

 So I didn't do the second subplot in this in this particular case because I was just simply demonstrating it just for this。



![](img/e4958744496fcbb23b7c948eb7b9c702_59.png)

 Yeah。

![](img/e4958744496fcbb23b7c948eb7b9c702_61.png)

 Yeah， so the you can Thomas I think we have a bug。 Yeah， the edge。



![](img/e4958744496fcbb23b7c948eb7b9c702_63.png)

 Then we run into the book Thomas or there's some sort of issue with edge colors or something in bar graphs。

 I guarantee you this did work a lot two years ago。



![](img/e4958744496fcbb23b7c948eb7b9c702_65.png)

 Yeah。 Oh， you're saying you might have broke it or the edge with。



![](img/e4958744496fcbb23b7c948eb7b9c702_67.png)

 Well， there's line with that。

![](img/e4958744496fcbb23b7c948eb7b9c702_69.png)

 Okay， let's move on。 I think I recall something that there was a bug in 2。0 where certain cases。

 the edge color wasn't being set。 Again， we're going to get into what some of these things mean in the next section anyway。

 So let's not get all hung up on that right now。 All right。

 so let's take a look at the other type of stuff filled between which is very useful。

 So if you're doing what want to plot you plotting some particular data and then you want to show what the envelope is of that data or whatever。

 Very common thing that's sciencey type people I've been told do。

 We'll get to the error one of the error envelope in a second， but this is just a very nice simple。

 You know， filled between is going to assume that you want everything to be set to a Y value of zero。

 So anything below will color upward anything above it will color downward。

 but you can actually set that Y to be anywhere you want it to be。 So you want it to be 20。

 You want it to be negative 15， whatever。 You can actually set that if you want。



![](img/e4958744496fcbb23b7c948eb7b9c702_71.png)

![](img/e4958744496fcbb23b7c948eb7b9c702_72.png)

 Now let's take a look at an example where we're also in this case。 Yeah。

 so that filled between that first one we did。 The filled between X， Y。

 We only specified one bound curve and that was the Y。 The Y being that。

 but if I want to specify another bound。 Right now it's assumed to be zero。



![](img/e4958744496fcbb23b7c948eb7b9c702_74.png)

 But so that's why it's bound there， but then if I want it to be， let's say something else。

 That's how you get an envelope。 So that was why one。 That's why to you able to then bound your。



![](img/e4958744496fcbb23b7c948eb7b9c702_76.png)

 Make an envelope like that。 You can do more general things if you wanted to。



![](img/e4958744496fcbb23b7c948eb7b9c702_78.png)

![](img/e4958744496fcbb23b7c948eb7b9c702_79.png)

 It's all available。 All right， and this is the part that Thomas really wants me to highlight for everyone here。

 The brand new feature added in 1。5 is called the data keyword argument。

 A lot of these plotting functions that we're going to specify not every single one of them。

 but a lot of them。 Now take on an extra keyword argument。 Anyone here not know a keyword？

 I'm hoping the software carpentry covered what that meant。

 So you have this pandas object and how do you access the individual stuff in there by their name？

 Well， if you were to have done those examples using let's say a pandas data frame。

 you would have done data frame， square bracket quote x， end quote， square bracket comma。

 Data frame open bracket quote y quote and bracket up。 That's just so tedious。 And again。

 we want to make things simple for you guys when you're particularly in an interactive situation。

 where you're typing things at the REPL。 Kind of like how you feel like you're doing a MATLAB。

 You want to make that simple to use。 But let's say we have this data object。

 I'm not going to create a pandas object。 I'm going to make something that is a dictionary。

 It's going to have x， y1， y2， mean。 It's going to have the things already in it。

 We're going to pretend that this is a pandas object。 I'm going to create that subplot。

 I'm going to call up that fill between。 I'm going to say fill between x， the string x， fill between。

 that's my x。 And then I'm going to say y1， y2。 Now， notice if I were to just simply have that。

 just ended it right there。 That plot lived within， you're crazy。

 But I'm passing in as a data argument。 I'm passing in the data object through the data keyword。

 So now， let's say you're at the REPL and you did one plot。 Okay， good。

 You hit back and you're back to that plot。 You can then swap out another pandas object that had the same keys in there。

 It makes it really easy to quickly reference things and just swap out different data objects and things like that。

 It makes things useful for those purposes。 Let's take a look at what that makes。



![](img/e4958744496fcbb23b7c948eb7b9c702_81.png)

 Wow， it makes the same exact plot。 It's just a slightly different semantics。

 If you like the other way， that's perfectly fine。 If you like this way， that works too。

 And so a lot of the plotting functions， so bar， plot， scatter。

 they all now support the data keyword argument you can use。



![](img/e4958744496fcbb23b7c948eb7b9c702_83.png)

 All right。 So let's do a fun little thing。

![](img/e4958744496fcbb23b7c948eb7b9c702_85.png)

 And we're going to try to use bar and fill between and make a prediction of how snarky you guys are going to get by the end of this class。



![](img/e4958744496fcbb23b7c948eb7b9c702_87.png)

![](img/e4958744496fcbb23b7c948eb7b9c702_88.png)

 So let's see if we can reproduce this figure。 So I'm going to provide you some data because I already know how snarky you'll get。

 And don't worry about so much about all this stuff here。 And now even give you guys the color。

 You can change the colors if you want。 I'd like you to try to figure out， okay。

 how am I going to make these bars， these error bars。

 and this fill between right here using the data you have。



![](img/e4958744496fcbb23b7c948eb7b9c702_90.png)

 We have five minutes to give that a whirl。 So obviously the first thing you need to do is create your figure and your axes and your one axes that we're going to make。

 And you take a look at that figure。 The first thing you want is that plot of the raw snarkiness data。



![](img/e4958744496fcbb23b7c948eb7b9c702_92.png)

 So that obviously means that you have to do a plot call。

 And then the next thing you want to do is the bar graph of the of the aggregated the cumulative。

 I guess， the statistical average of the time lag。 I'm trying to sign a sound scientific and I'm just totally not working。

 But yes， we're going to take that raw snarkiness data and we're going to。

 We did that Y average at so many intervals and we said what that with that interval was。

 And we're going to provide a color。 And in addition， we're also going to provide the error data。

 And we're also going to provide the color for some of those things。 And for those who don't know。

 E color is how you specify the color of the error bar。 Meanwhile。

 edge color is the color of the bar。 The edge of the bar is。 Yeah。

 we'll cover that in the next section in the next notebook。

 And then so that's the first two plot elements that we see up here。 We have the raw snarkiness data。

 We have the bar with the error bars。 So now the only thing left is that build region behind all of this and note it is behind it。



![](img/e4958744496fcbb23b7c948eb7b9c702_94.png)

 So we're going to provide the envelope data that we have a fill between call。 Yeah， there we go。

 We provide the color。 And it's going to end up magically behind everything。

 This is just simply a fluke of how matplotlib defines certain things are going to be positioned by default。

 You can override any other things for the most part。

 The order in which you specify these things will determine which is on top of which。

 But for some reason we have to fill between like always behind everything。

 I don't totally understand why， but that's what it's always done。

 So now we're going to set the title of our figure， the Y label and the X label。

 And then we're going to show it。 Execute it。 Ah， a slight oddity for those of you who are running version 2。

0。 Because of the style changes。 One of the default。

 one of the changes we made to the defaults was where the bar for bar graphs were going to be oriented by default。

 In the old style， it was the location you specified was considered the edge of the bar。

 Now by default in 2。0 and later is considered to be the center of the bar。

 But you can override this。

![](img/e4958744496fcbb23b7c948eb7b9c702_96.png)

 So if we want to reproduce what the old graph looked like up here。

 because maybe your statistical processing already took that into account and already knew all this or whatever in that you know better than matplotlib。

 you can override it。 We're not going to prevent you。 So if you go back to bar。

 we're going to add an argument here。 You know why I love being a programmer？

 Because you get to do a lot of arguments。 I love arguing。 Yes。 Align equals edge。 Oh， look at that。

 Now it looks pretty much exactly like the figure that was up above。



![](img/e4958744496fcbb23b7c948eb7b9c702_98.png)

 Everything is oriented the way we want it。 And everything is all well with the world。



![](img/e4958744496fcbb23b7c948eb7b9c702_100.png)

 And you guys now know how snarky things are going to get。 I'm sorry， which part。



![](img/e4958744496fcbb23b7c948eb7b9c702_102.png)

 Right here。 And then what's the other value it can be？ It can be center， right？ Edge or center。

 Yeah。 So in the past， the default was edge。 Now it's center。

 And if you want to be one way or the other， you can just explicitly state that。

 And that's what it will be。 All right。

![](img/e4958744496fcbb23b7c948eb7b9c702_104.png)

 Wonderful。 Now， let's。 P。 L。 D。 what？ Okay。 One person。 What？ Oh， P。 R。 E。 D。 Oh， the predicted X。

 And the predicted Y。 Yeah。 The predicted。 Yes。 I know programmers are terrible with their variable name。

 And I actually， because I am perfect， I'm going to say this was not my fault。

 And I actually have proof of this。 Someone else wrote this example for me。

 If you look at the history， someone else wrote it。 All right。 So now let's move on to some images。

 This is a very common thing that many people want。 So I am show。 P。 color， P。 color mesh。

 They do slightly different things。 One of the key things that's different。 So you can use P。

 color to do。 Like P。 color， you can use it for arbitrary grids。

 So long as they're ordered in an organized fashion， in a somewhat organized fashion。

 so that they're monotonic。 They don't have to be regular， but they still have to be monotonic。

 So with P。 color and P。 color mesh， you can do these arbitrary grids。

 So you can do these nice little fancy stuff that you can't quite do with I。 m。 show。

 But if you let's say the grid is regular and you wanted to do a P。 color or P。 color mesh。

 there is one very subtle difference between I。 m。 show and P。 color。

 And that is that the coordinates you specify for I。 m。 show refers to the center of the pixel。

 Meanwhile for P。 color， they refer to the edge of the pixels。

 If you ever talk to image processing people， you can basically split them up into two groups。

 Those people who think that your coordinates should be the centers and the other people who think that it should be at the corner。

 And it's like the crypts and the bloods。 Seriously。

 if you get the two of them together in a bar and you just throw that bomb in there and they start arguing about it。

 they'll do it for hours。 I've seen this happen。 Don't start such arguments because then you'll be that crazy guy that everyone hates。

 So， but that note that that's a difference or some time people say this thing is shifted over a little bit。

 Yes， because the P。 color refers to your corner。 Now， when you have a high resolution image。

 you're not really going to notice that tiny little shift。

 But if you have a low resolution image that you're looking at。

 you're going to notice it is shifted over by half a pixel。 Now， one thing that's nice， I。 m。 show。

 you can do image interpolation automatically。 That's really nice。 They're also very。

 very fast to render。 P。 color is extremely slow。 You can do arbitrary grits。 So， you know。

 six of one half a dozen of the other。 It's pick the graphing method that fits your situation the best。

 So， let's talk about what they have in common。 And that goes back。 Remember。

 I talked about the difference between plot and scatter。 And that scatter。

 you can size your marker or color your marker according to some piece of data。

 It's known as a scalar mapable。 So， there's some scalar value that we're given。

 And we use that to determine what some other property， whether it's a size or color。

 And for the case of P。 color and I。 m。 show， we're going to be determining the colors of the pixels。

 But for scatter， you can do it for size or for color or both， if you want。

 Let's first talk about one of the most common things you'll see with images。

 And that is the color bar。 So， let's do a very simple， I'm going to load up some data。

 And I'm going to do an I。 m。 show of that data。 That data is already a 2D array of values between such and such and such。

 I don't remember what it is。 I'm going to pick a color map。 And just because I'm weird。

 I'll just the just earth thing。 We have a whole bunch of them。 We'll cover that soon。

 What the color maps are。 And then I'm going to add a color bar to the figure。

 And I'm going to say that this color bar is going to be in reference to this scalar mapable， this I。

 m。 This image data。 So we see the image that has been made nice and pixelated。

 And there's the color map that it created。 If I didn't have that color， I'm sorry， not color map。

 the color bar。 If I didn't have that there， I'm going to comment it out。

 The image is a slightly wider。 So what happens when you call big dot color bar。

 it's going to steal some space away from the axes that are there。 And use that amount of space。

 It will shrink those things down a little bit and it will use that space to add in the color bar that they're。

 You can explicitly state which axes to steal some space from。

 It will deal about the same amount from each one。 It's a bit tricky， a large gun underneath。

 but you don't have to worry about it too much。 You just have to watch out an older。

 If you have multiple subplots in a row and then you want one color bar at the very end。

 If you call big dot color bar and use that last。 I am that last image there for that。

 It's going to steal space only from that one。 So now you have one image that looks smaller than the other two。

 That looks a little odd。 You can actually then say， hey， I want you to steal space from all three。

 It will shrink all three equally so they all look to be the same size and then give that amount of space for the color bar to be added in。



![](img/e4958744496fcbb23b7c948eb7b9c702_106.png)

![](img/e4958744496fcbb23b7c948eb7b9c702_107.png)

 Okay， also notice that up until now most of our plotting calls have been on axe。

 I am sure act dot plot acts dot scatter act dot bar。 This one big dot color bar。



![](img/e4958744496fcbb23b7c948eb7b9c702_109.png)

 Because this is not an axes method。 We're not adding a color bar to an axes。

 We're adding the color bar to the figure。 Again， this is where it's really the object oriented notation。

 the object oriented approach of specifying and saying。

 I want to do this action on this object makes it explicit。 What it is that you're intending。

 It doesn't make sense to add a color bar to an axes。 It only makes sense to add it to a figure。

 Because it's just simply another element of the figure that goes with the axes。

 But it's not a part of an axis。 It is actually an axis in of itself。



![](img/e4958744496fcbb23b7c948eb7b9c702_111.png)

 But that's an implementation detail that you don't have to worry about。 But anyway。

 there are some things you can do where you want it to be positioned and how you want it oriented。

 So here we do the same sort of example。 Let's say I want a situation。 By default。

 the color bar will always be placed outside of where the axes are。

 So it gets its own space in the figure。 That's what most people want most of the time。

 We've all seen it。 You can do that。 You can actually explicitly create your own。

 what I call a CX object。 This is one of those situations where Matt Plutlib is not going to stop you from doing what it is you want。

 But it's not going to make it totally easy either。

 You have to know exactly how to specify what these axes are or what the coordinates are going to be。

 Things like that you have to know a little bit about the underlying things about figures and axes。

 But it allows you to do it。 So you specify that and there that axis is going to be created。

 I'm going to do my IM show just like I did before。 I'm going to call big。color bar。

 pass it my IM object。 I'm going to say CX equals CX。

 I'm going to tell color bar rather than you trying to steal space from these other places。

 I already made space for you。 You， this， and you pass in what that is。

 And then here's another argument。 Orientation equals horizontal。 By default， it's vertical。

 Here you can say I want it to be a horizontal color bar。 Let's say。 And look at that。 Pretty。

 Not terrible。 Yeah， if you had done， let's say we didn't have that horizontal thing in there。

 So it's now， it's a very， very wide color bar。 With all of its labels really， really， really。

 scrunched in there。 So yeah。 We're not going to stop you from doing it， but you can do it。

 And so the shape of the color bar was completely determined by the axes that was created。 But yeah。

 it's all right there。 All right。 In the last notebook， when we get to it。

 I'm going to cover a module called Axies Grid， actually called Axies Grid 1。 It actually。

 for those who want to do much more advanced type of displaying multiple images and having a color bar。

 It has a much more advanced notation for that and very， very useful。 We'll get into that。



![](img/e4958744496fcbb23b7c948eb7b9c702_113.png)

 It's neat。 So if you feel like， oh man， I mean， I got to describe all this stuff and it's going to get tedious for me to do this for everything。



![](img/e4958744496fcbb23b7c948eb7b9c702_115.png)

 We'll image that now。

![](img/e4958744496fcbb23b7c948eb7b9c702_117.png)

 Axies Grid 1 actually provides a very useful interface for handling much more complicated layouts of images and color and their associated color bars。

 What are some other parameters that these functions share besides just the C map？

 So we went over C map， we'll cover some of the names of them later。 B min， B max。 So by default。

 when you pass in the data to these functions， it's going to assume that you want the color bar or the color map to extend over the minimum and the maximum of the data that you pass in。

 It's going to assume that。 But you can explicitly say， oh， no。

 I want the B min to be this and I want the V max to be that。 Those are the arguments。

 And then you probably won't run into this too often。

 but you can actually pass in your own normalization object。

 There's documentation online about describing it， but you can actually then say that， no。

 I want you to do a log norm or I want you to do a sim log or something。

 So we can specify other log rather than just a simple basic linear log to use to normalize the data to zero to one。

 So that way we can color map it。 That's how the color mapping stuff works and the color bar works is that we normalize the data the scalar value of the scalar map。

 We normalize that to zero to one。 We then have a color map that operates on values between zero and one。

 That's all under the hood。 You never have to deal with that most of the time。

 But if you wanted to override some aspect of that， that's how you would do it。 Okay。

 so when would you use V min and V max？ Those are the ones I tend to use a lot。

 Let's say you're looking at a series of images。 And so those series of images may。

 you don't know if the minimum and the maximum value are always going to be the same。

 You can actually explicitly state I want the minimum maximum to be this。

 That way every single time the color bar is for the same range。

 And that you're color mapping it the same way。 So the same value get the same color every single time。

 Very useful。 You know， you sometimes will see people make the mistake where they don't specify this。

 And then therefore they're looking at two different images。 And they go， oh wow。

 that's a very interesting feature。 But no， actually they were both colored incorrectly。

 They weren't colored in the same way。 And so it's actually not really a feature。

 See an example of that right here。 So let's say I have this。

 Notice I got a red to blue or blue to red color map。 But my zero is not on the white。

 It's slightly in the red。 So now my data look like a slightly biased red。 Well。

 one might make a scientific pronouncement。 Oh my gosh， the universe is biased red。 No， it's not。

 You didn't specify your B-min and B-max。 And so therefore it was not centered。

 It went to whatever the min and the max of your data was。



![](img/e4958744496fcbb23b7c948eb7b9c702_119.png)

 So how do you fix that？ So you specify B-min and B-max。

 You can say that you want B-min to be negative two and the B-max to be two。



![](img/e4958744496fcbb23b7c948eb7b9c702_121.png)

 Ah， the universe is all perfectly balanced。 Yes。 Any questions on that respect？

 This is actually a very common trip up many people run into。

 They get confused with their analysis because they didn't color it right。 Okay。

 There's an example of just a single map。 But another time that this happens when you have multiple subplots in the same figure。

 well， the color map， the color bar is only going to be done to one of those figures。

 B-min and B-max， so that it may be confusing with the other one。 So if you just explicitly remember。

 explicit is better than implicit。 So if you go ahead and you say that you want it to be negative two to two。



![](img/e4958744496fcbb23b7c948eb7b9c702_123.png)

 there will be no confusion whatsoever about what it is you're viewing。 All right。 Let's do。

 I'm not going to spend like a million minutes on this， but let's just take a look。

 I want to reproduce this figure。 I'm going to give you the data。

 I'm going to spend a lot of time on this。 Again， randomly generate the data。

 I'm going to do a classic。 One of the big things that changed between version 1。5 and 2。

0 is the color map。 And I'll talk a little bit more about that， but we went from jet to veritas。

 And so for the purposes of this example， I wanted to reproduce what the old jet color map images were。

 The color map of jet is that really， really colorful one。 It is dangerous to use。

 but you don't use it。 But with the purposes， I just wanted to make something nice and pretty。

 So going to， in the interest of time， I'm going to go ahead and get this moving along solutions。

 So have that data。 Well， don't worry so much about what tight layout is。 Tight layout。

 I'll show you an example， a really good example of it later。

 And there we have the color bar axes that we're making。 The special one that we're going to have。

 I'm going to loop over the data that I have and the axes。 So I have the list of the axes object。

 I have data 1， data 2， data 3。 I'm going to do， I am showing each one。 I have vmin=0， vmax=3。

 And I'm going to say the interpolation can be near。 So that's the other thing that changed in 1。

5 to 2。0 is that the interpolation will be the nearest one。

 So that means that there won't be any interpolation that's just pixelated。

 And there we have the color bar。 And we're going to orient it horizontal。 Really。

 very similar to the other example we had。 And there we go。 Like so。 Wonderful。 Alright。

 let's take a quick five minute break and we'll move on to the next section。 Okay？

 Anybody have any questions？ I'm here to help you out。 We're now in part three。

 The part three notebook。 So in the previous two， you learned how Matplotlib organizes this plot making by figures and by axes。

 You notice I had never deviated from this。 There was no other way to do it。

 It is a very simple conceptual model。 Figures， axes， all the plotting goes on there。

 We broke down the components。 So you now know that there's x axes。 There's a y axes。 There's labels。

 Things like that。 We learned how to add multiple axes to a figure and how to use them together。

 We learned how to change some of the basic appearances of them。 Added some plotting。

 We did some color borrowing and stuff。 We did a lot of wonderful and fantastic things。

 And you guys should really be off to the races now making fantastic plots and publishing stuff in nature and boosting my impact factor。

 Why are you guys still here？ Because you don't know how to control the plot and figures。

 You don't know the vocabulary yet of Matplotlib。 You know some of the nouns or things like that。

 but you don't know the adjectives。 You don't know the adverbs of how to actually do things。

 You saw some random stuff in some of the earlier things。

 but they probably just don't quite make sense yet。 You need to learn how to speak Matplotlib。

 The very first thing， and this is the most important thing probably， are the colors。

 Which is funny because I don't really see all the colors very well， but just。 So。

 there are many different ways to specify colors in Matplotlib。



![](img/e4958744496fcbb23b7c948eb7b9c702_125.png)

 First things first， and I even provide a link to the documentation for pretty much all the ways you can do it。



![](img/e4958744496fcbb23b7c948eb7b9c702_127.png)

 The first one is you can specify a string with the name of the color。

 And you saw some of this earlier。 And we support the full， what is it。

 147 color names from the HTML CSS specification， including the fact that any one of those。



![](img/e4958744496fcbb23b7c948eb7b9c702_129.png)

 names that say gray， we also accept gray。 So， if it's light gray， you can do light gray。 Also。

 Burleigh would in church， whatever。 I don't， I didn't take French。 So， you know what？

 We do not allow that。 I think we drew the line right there。 [ Inaudible ]。

 If we allow having the U in the word colors。 No。 I think I would just reject that pull request outright just because it's。

 So， and then even some of the very basic colors， we even accept single letter representations of it。



![](img/e4958744496fcbb23b7c948eb7b9c702_131.png)

 So， instead of saying blue， you can say B。 Instead of saying green， you can say G。 Red R， fancy。

 magenta， M， yellow， Y， black， K。 You realize you couldn't use B because B was already taken by blue because blue is all stuck up and thinks it's all colorful and everything。

 So， if you get to use blue。 And then white， B and W。 So。

 those are the single letter representations that are allowed。 And then the full names are。

 that's in the HTML CSS spec are also allowed。 And also， it's not case sensitive。 So。

 you can have capitalizations if you want。 We don't care。 It's all allowed。 So。

 that's the most common way to specify colors pretty much anywhere。

 The other thing you can do is you can do a string that has the hex value。

 That is also perfectly allowed。 This is also very common among people who do HTML work and things like that。

 So， if you know what your hex value is， we accept that。 You pass it in as a string。

 And then we just recently added to version two a way that， so you have one， two， three， four， five。

 six。 Character， you can have the seven and eight character represent the alpha channel if you。

 wanted， optionally。 Some people like it。 Sure。 Not a problem。

 256 shades of gray were much better than the movie。 The。

 you can specify a gray level by providing a floating point number。 But in quotes。 Yeah， whatever。

 but， so zero would be， would be black while one would be white。 So。

 anything in between there would be different levels of gray。

 Also in some places you can't do this everywhere， but you can do this in some places。 Oh， yeah。

 that gray reputation。 You can't do that everywhere， but you can do it in most places。 RGBA tuples。

 there are fewer places you can do that at the high level interface to the functions。

 and such that you guys would call， but there are places down in the lower levels where this。

 is accepted。 And there's a few places in the higher level stuff where this is allowed where you can specify。

 tuples of RGB， red， green or blue， that would be a floating point value between zero and， one。

 not zero and 255， it's zero and one。 And so you can do that。

 And then the fourth channel being alpha is again optional， but it has to be consistent。

 So if you're passing in， let's say a list of RGB tuples， I believe they all have to be either。

 size three or all size four to be consistent because recast everything in NumPy arrays。

 And so if they're not consistent， then it doesn't work。 And so that plot and scatter。

 you can't do color， or the full color spec because it gets confusing。

 at what it is you actually mean， but you can do certain things。 So if they're in some places。

 you'll know right away if it doesn't work。 And then a brand new thing that was added in 2。0。

 I don't think we actually gave this an， official name， Tom。

 so I'm going to give it an official name now called "Cycle References。"， So because I said it first。

 I plant this flag。 "Cycle References。"， So you may notice that I haven't demonstrated this yet。

 but when you call plot multiple times， each time you call plot for a particular subplot。

 the color is different。 It's called the color cycle。

 It does it automatically if you don't specify a color。

 So we have these things called matplotlib styles that you can load up。

 There's a default style that pretty much you're going to use 90% of the time。

 You never have to worry about it。 But there's been growth in this community of people developing all sorts of styles for different things。

 It becomes needed that you need to be able to set in other parts of your code。 You may need to say。

 "I wanted this to be the same color as the first color in the style color cycle。"。

 But you don't know what that color is， or you have to go through this obtuse way of looking it up and finding out what it is。

 We made this simple in 2。0 so that you can just simply say C0 as a string， C1。

 So C0 would be the first color of that color cycle。

 C1 would be the second color of this color cycle。 Whatever the color cycle is。

 you don't know what it is。 You don't care what it is。 You just want the first color。

 the second color。 You can do the first 10 iterations。

 Most color cycles are only about 6 or 7 anyway， so it doesn't matter who the most part necessarily need to have the whole。

 be able to reference every single one of them。 So you can go all the way up to C9。

 I'll show an example of this in a second。 So here， we're going to。

 I'm not going to have you guys spend 5 minutes on this。 I'm just going to show this。

 We're just going to do a simple plot where I'm going to do just a linear， a square。

 and then a cubic thing。 And each one of them you'll notice is a different color。 Blue， red。

 and green。 I think so。 I didn't say what color they should be。 That's the default color cycle。



![](img/e4958744496fcbb23b7c948eb7b9c702_133.png)

 So， let's see something。 C1， C2， C5， just because I want to be weird。



![](img/e4958744496fcbb23b7c948eb7b9c702_135.png)

 Look at that。 They're different now。 Red， green， and。 Is that salmon？ So。

 do you see how that worked？

![](img/e4958744496fcbb23b7c948eb7b9c702_137.png)

 And let's say， let's change that to 0。4。 That's going to give me some gray color， right？



![](img/e4958744496fcbb23b7c948eb7b9c702_139.png)

 There you go。 It's gray。 Let's do over here R。

![](img/e4958744496fcbb23b7c948eb7b9c702_141.png)

![](img/e4958744496fcbb23b7c948eb7b9c702_142.png)

 That's right。 It was already going to be red， right？ Make this yellow。 Or no， no， no。

 This is light gray。 Now it's light gray and then the other light gray。 It's the same thing。

 It works。

![](img/e4958744496fcbb23b7c948eb7b9c702_144.png)

![](img/e4958744496fcbb23b7c948eb7b9c702_145.png)

 Don't worry so much about the T's。 It's just providing a quick set of data where you see three lines。



![](img/e4958744496fcbb23b7c948eb7b9c702_147.png)

 You're not from MATLAB， are you？ This is a MATLABism。 I could just easily have done this。

 That is equivalent。 The next parameter， not the last， the next parameter。

 You have to be very specific here。 And also， as you'll learn， it is actually not just color。

 It's actually something a little bit more complicated than that。 Oh， it gets fun。

 And you can blame this all on MATLAB。 This is one of the things I hate and love MATLAB for。

 As a programmer， I often hate this。 This is why we can't have nice things。



![](img/e4958744496fcbb23b7c948eb7b9c702_149.png)

 Oh， yes。 PyCharm hates us too。 PyCharm and IDE hates us because they can't introspect our function properly。

 to find out what the call signature is。 We have to do all sorts of funky stuff to this call signature in order to make things work。

 Yes， our number one rule is act a lot like MATLAB because that was the original design。

 But then on top of that， our second rule is don't break backwards compatibility。

 So all the stupid decisions that MATLAB made were stuck with。 You don't need to know this。

 This is not required。 This is just simply syntactic sugar。 You don't have to do it this way。

 You can actually， and I will show this， you can actually specify， you can say color equals。

 marker equals， line style equals。 You can say all that and you can be absolutely clear exactly what you mean。

 And that is also 100% allowed。 But this syntax that I'm going to be teaching you guys is a shorthand way of specifying this information。

 That is actually very useful at times。

![](img/e4958744496fcbb23b7c948eb7b9c702_151.png)

 And it's also good to know because you'll see other people do it when you come across their code。



![](img/e4958744496fcbb23b7c948eb7b9c702_153.png)

 And you want to understand what it is they're doing。 So that's colors。 Now。

 how do you specify markers？ We have a very robust set of things for specifying markers。

 This is actually a bit of an overkill。 For example， 4， 5， 6， 7。

 That carrot left carrot right carrot up carrot down。

 That actually really never was meant to be markers。

 They were meant to be actually something dealing with ticks and stuff like that。

 So they're just enums for us。 But since they all actually fall into that。

 you actually can use these。 So whatever。 But the ones that you typically will use are the string values。

 So a period is a point。 And that's actually different than a comma， which is a pixel。

 We actually have code that actually will differentiate and will draw a dot of a certain point size。

 But then we can actually draw a pixel。 Whatever someone added that code in， we accepted it。 Okay。

 D for diamond， but then for like the small diamond， but then a big upper case D for the big。

 you know， bigger diamond。 Makes sense。 An octagon is a string eight。 A lower case O with a circle。

 P for pentagon because why not a five？ I don't know。 Yeah。

 some of these decisions didn't quite make sense。 We have two different hexagons。

 The differences with how they're oriented。 Star gets you a star and X gets you an X plus sign gets you a plus sign。

 So all these things are available to use。 So don't have to actually understand how this particular code can run。

 but this thing actually will show you what each one of these things look like。 So。 Yes。

 These are all the。 Oh， it is cycling。 Yes。 I think you're right。 It's cycling a little bit。 I think。

 Oh， no， no， it's not。 It's not cycling。 Oh， it is。 Okay。 Yes。 It is cycling。 But yeah。

 if you wanted to change it all， I could say color equals red。 There you go。 They're all red。

 So that's what they all look like as a marker。 Nice and large。 So all useful to know。

 So let's again， you know， similar sort of an example。 Let's and again， for the interest of time。

 we'll just kind of step through this。

![](img/e4958744496fcbb23b7c948eb7b9c702_155.png)

 But you can play around with this yourself。 So now I'm going to start doing that lovely mat lab stuff。

 And I'm going to start combining marker specification and color specifications。

 So the marker comes first。 So I say star， why I'm going to get a yellow star for the linear part。

 And then for the， the squared part， I'm going to have a。



![](img/e4958744496fcbb23b7c948eb7b9c702_157.png)

 A yes， octagon magenta。 Thank you。 I try to remember the color name magenta。

 And then for the cubic line， I'm going to have a green square。 There you go。

 So green squares magenta。 Octagons。 They may look rather round because they're that small。

 but when they get bigger， they actually look more octagonish。 And all that。 Yeah。



![](img/e4958744496fcbb23b7c948eb7b9c702_159.png)

 So the first one was a yellow star。 So that's just as a asterisk， why？

 And then this one was a magenta， oxygen， that's an eight M。

 And then this one here is a green square。 So that's an SG。



![](img/e4958744496fcbb23b7c948eb7b9c702_161.png)

 Now， the last thing that you can specify for these plots are the line styles。



![](img/e4958744496fcbb23b7c948eb7b9c702_163.png)

 You can do a dash for solid two dashes for a dashed line。

 You can do a dash dot for a dash dot did line。 You can do a colon for just simply a dotted line。

 And then there are three different ways to say nothing。 Now， note this is the string none。

 The Python object none actually does not draw nothing。 It actually means the default。

 So it will refer back to whatever it would be if you didn't specify it at all。

 So if you want to say don't draw a marker at all， you actually pass in a string that is empty or a space or something like that。

 That indicates nothingness。 One note as we did into these format specifiers， I do this all the time。

 Doing a dash dot line is a dash then a dot。 It's not dot then dash because what that means is that you want a solid line of dot markers。

 So， yeah， so here we do this just this quick example。 First one is going to be a solid line。

 Next one can be a dashed line。 And the next one is going to be a dash dot。 And then heck。

 we'll do a quad do another linear one。 It would be dotted。



![](img/e4958744496fcbb23b7c948eb7b9c702_165.png)

 There you go。 There's four lines here。 Look like that。



![](img/e4958744496fcbb23b7c948eb7b9c702_167.png)

 An oddity and we fix this， but it's not in any of the current releases yet。

 That you see these names of solid dash dot dotted。

 Those names are valid names to use to specify the lines around polygons。

 so the outline of a polygon。 But you can't use those shorthand notations。

 And then wherever you can use the shorthand location， you can't use the worded ones。

 We fix it for 2。1， but 2。1 hasn't been released yet。 So， but for now。

 just remember whenever you're talking about polygons and you want to specify how the outline style should be。

 the edge line， you have to use the word。 So， yeah。 It's an oddity， but in 2。1。

 you can go back and forth between the two conventions and that's perfectly allowed。 All right。 So。

 quickly， now we're going to show off。 All right。 So， this is showing this is an example。 So。

 polygon to act that bar is a polygon that ends up being made。 You have。

 so the line style LS line style， you have to say dash。 So， it's just demonstrating that。 So。

 now you have dash lines around your bars。 In case you ever wanted it to happen， you know。

 that's a feature that you want to deepen your heart， that your bars must be dashed。 We， like I said。

 matplotlib will let you do it。 We are not the arbiters of what is ugly and what is pretty。

 You know what I say does a very pretty bar plot。

![](img/e4958744496fcbb23b7c948eb7b9c702_169.png)

 So， let's kind of do a little bit of， there's other attributes。 So， we talked about color。

 We talked about marker and we talked about the line style。

 but there are other attributes that pretty much all artists。

 And these are called artists because they can draw anything that you can view on your plot is an artist。

 And we have these things。 They also have additional properties。 I do not， this， this， this。

 this Selma has gotten misplaced， but this bringing it all together。 So， I have a red dash line。

 a blue or a blue squares and green triangles。 So， I'm combining together some of these different elements so that I can specify them in a shorthand notation。

 I can create plots like this。 So， yes， that's what comes from matlab is this monstrosity of a shorthand notation for specifying。

 I could have just easily had three plot commands in each one of them saying color equals R。

 color equal B， color equal G， and then each one of them be marker， line style equals dash dash。

 marker equals S， marker equals， you know， carrot。

![](img/e4958744496fcbb23b7c948eb7b9c702_171.png)

 I could have done that， but that would have been tedious and a lot of typing and stuff。 And。

 you know， quite honestly， I'm lazy。 And， you know， as a marker of a good programmer。

 it would be extremely lazy。 So， yes。

![](img/e4958744496fcbb23b7c948eb7b9c702_173.png)

 Don't let anyone tell you that a programmer is a good programmer is hard working。 You need not。



![](img/e4958744496fcbb23b7c948eb7b9c702_175.png)

 All right。 There's a whole bunch of other properties that can be set。 So， color or C。

 so you'll see some of these properties have shorthand names that are also available。

 The alpha takes a floating point value from zero to one to indicate how transparent is it。

 Don't worry so much about dash and the dash cap down， jet joint style。

 but if you ever really wanted to deal with that stuff is available。 You can actually。

 so those dashes that we specified， the dotted and those are actually the pre-made ones that are available。



![](img/e4958744496fcbb23b7c948eb7b9c702_177.png)

 You can， if you really wanted to， come up with your own dash specifications。

 And so it is a sequence of those documentation on it。 I've never actually done it myself。

 but you can actually specify exactly how you want those things to be。 There's draw style。



![](img/e4958744496fcbb23b7c948eb7b9c702_179.png)

 So， by default， the draw of a line will go shortest path between two vertices。

 But you can do different draw styles so that， let's say。

 it will take a Manhattan path approach to getting to two vertices or something like that。

 Or whether， let's say， it will go up， then over or over， then up or over part way， then up。

 then over。 Those are different draw styles that are available。 So that's the step， step， pre， step。

 mid， step， post。 It all came from people doing finance type work。

 So you know that the value is going to be the same for a particular quanta and then move on。 And。

 yeah。 Line style， we went over some of those， line width。 So how wide is it going to be？

 The marker style。 The edge color of the marker or MEC， the marker edge width。

 how wide the outline is。

![](img/e4958744496fcbb23b7c948eb7b9c702_181.png)

 Yeah。 It's complicated。 So， Mu， MFC， MS， the marker size。 Again。

 cap styles and joint styles for lines themselves， whether or not visible。

 And the Z-order Z-order is actually very important。 And something you may come across oftentimes。

 So before I made a comment about that， the build between always showed up behind everything。

 What if you didn't want us to show up behind things？ What if you wanted it to be up front？

 You can set a Z-order of that particular object and say。

 I want you to be a Z-order of five or twenty or something。 The larger the value。

 the more in front it will be。 And so that way you can actually control how these artists of these complicated plots are composed。

 There's a default values that are there and usually it matters by just simply what order you call them in。

 There's a couple of them have special values， but that's usually it。

 But you can also specify your own Z-order value any time you want。 All right。 Let's do this。

 Let's make this a real quick example， but I want you guys to actually try this out。

 I want you to make a plot that has a dotted red line。 Large yellow diamond markers。

 Those diamond markers have green edges。 All right。

 Take five minutes for that and we'll then move on to the next one。

 So I'm hearing a lot of chatter and I'm not quite sure if that means you guys are all bored with me now or that you're really excited and really finally。

 you know， really figuring is out and you're cracking it and all。 I see a lot of light bulb。

 but I'm not entirely certain that are they all lit up or something？ Not。 Okay。

 So we'll take a look at the solution here。 It involves just the plot itself is very simple to a just a question of what are they going to be colored and what the styling is done。

 So again， we could have explicitly stated that the color was red and say that the line style equals colon and that the marker equal D。

 We could have done that， but let's use the shorthand notation here。 R colon D。 Red。

 It's going to be red color。 Note that it's the red color is one of those weird things。

 So you have color， you have line color and you have marker colors color。

 Just simply take care of both line color and marker color edge colors all the， you know。

 if you don't specify those other things， it assumes whatever the color is。 But then if you say。

 but then you can override that in a moment， you'll see。

 So I want red dotted line with diamond markers。 All right。

 but remember I said I wanted yellow diamond markers。

 So you're going to have to say that the marker base color。 Because you could say marker color。

 but remember I said I wanted to have green edges。 So the face of the marker is going to be yellow。

 And that the edge color of the marker is going to be green。

 Did that make sense to anybody or that just completely utterly obtuse。

 It's okay to say this obtuse because I blame mat lab。 I mean。

 even the shorthand notation of MFC and MEC at the all came from mat lab。

 We can totally blame them on this， but it is a shorthand notation and it is a consistent one。

 And indeed you get a red line， a red dotted line with yellow markers with green outlines。



![](img/e4958744496fcbb23b7c948eb7b9c702_183.png)

![](img/e4958744496fcbb23b7c948eb7b9c702_184.png)

![](img/e4958744496fcbb23b7c948eb7b9c702_185.png)

 All right。 Let's move on from that 1D data stuff and let's come on over to the area that I love。

 Images and in particular the color maps。 And this is a very。

 very important topic in scientific visualization。 Is that you， when you plot a map。 An image。

 You could， you could just make it black and white。 It's just a great scale thing。

 And just call it done。 But you know， oddly enough the human brain hates that。

 And so we like to make them colorful to help convey a little bit of extra information。

 Things like this。 And that's what， but then it's important to select a color map that is useful and not misleading to the eye。

 And we don't see patterns there that aren't intended to be there。

 That was the problem with the old color map jet。 And jet， I can't even blame this on mat lab。

 The jet actually predates mat lab。 Sure， sure。 Mat lab probably popularized it。

 but it did exist before mat lab。 Yeah， there were other packages that were using jet or if it wasn't jet it would look very。

 very similar to jet。 Jet goes from blue to red， but it goes through greens and yellows and oranges and stuff。

 But basically， you know that comic family circus where they do that comic series where they show the kid running around the neighborhood and take all this weird path and going back。

 That's jet。 All right， don't use jet because it will actually cause you to see patterns in your data that actually aren't there。

 There was a fantastic presentation done a couple years ago， a stip high 2015， I think。

 I have a link right here by Nathaniel Smith and Stefan Banderwell who developed what are called perceptually Uniform Color Maps。

 And so basically you don't see gradients。 It is uniformly varying in color spaces。

 It's a complicated thing。 It's a very accessible， easy to understand presentation。

 It makes it oh so obvious。 Why the heck have we been doing this the wrong way for so long？

 Even mat lab actually learned the error of its ways and a few years ago they switched over their default color map from jet。

 to parula。 And they said， hey， look， this is a perceptually uniform color map。

 Everyone should use this。 Let's get all on the bandwagon。 Nathaniel Smith and Stefan Banderwell。

 they actually did an analysis。 We actually originally asked mat lab if we， the math work people。

 if we would be allowed to include parula into matplotlib， a package in matplotlib make it available。

 We weren't deciding that we wanted to be default but we wanted to make it available。

 Mat work said you're not using our intellectual property and stuff。

 This stuff is a really awesome sauce and all this other thing。

 Nathaniel Smith actually did an analysis of parula。 It is not perceptually uniform。

 It's only uniform if you consider it strictly in RGB space。 It's a very weird。

 complicated color space and such。 And so you actually do see gradients in parula that aren't actually there。

 Verritus is a lot closer to what the human eye actually sees and it makes things look much more correct。

 And that is now the new default in version 2。0 of matplotlib。 And you know what mat lab？

 They actually， people have actually added a package to mat lab so that you can load up verritus but nobody bothered to make a package to load up parula。

 That too。 But there are people who don't care about the lawyers and they still don't care enough to get parula into matplotlib。

 So just saying， just how awesome verritus is。 There's also plasma， magma， a few others。

 We'll show them in a second。 So this command， this cell that I just ran。

 it generates all the ones that are built into matplotlib by default。

 You can actually create additional ones if you wanted to。 But verritus here is the very first one。

 Very pretty。 Plasma， plasma was the runner up in ferno and magma or the other two。

 They're all perceptually uniform and they're all very nice in their own way。

 We just like verritus because it's green。 Turns out verritus。

 is it Greek or Latin for green or something like that？ Yeah。 Yeah。

 Anybody who likes obscure Star Trek references， it's green。



![](img/e4958744496fcbb23b7c948eb7b9c702_187.png)

 So sequential color maps。

![](img/e4958744496fcbb23b7c948eb7b9c702_189.png)

 These are all very nice。 These are the gray。 This is actually one of the places where you can't do gray with an E and gray with an A。

 Sorry， I didn't bother implementing that。 But very nice and simple。

 but these go from light to dark in a particular color。 In a bunch of different ways。

 The naming is a little bit complicated。 Blue to copper or something like that。 I don't know。

 And then there's another set of sequential color maps。

 These are just basically things that go from typically 0 to 1 or 0 to 100 or just things that are just very simple one-sided distribution type data。

 Things that are diverging， the things that are typically like errors。

 So are you over under a particular value？ They typically go red to green or red to blue。

 That's one of the other things that we were watching out for when we created this new color map。

 Is that we were very keenly aware of people with colorblindness。

 So we avoided color maps that had reds and greens together in them。

 So we would get up for blues instead or didn't quite go into the reds or things like that if we had to green。

 So we try to be fair to that。 It also makes things a little bit better for just simply making a gray scale image of a particular color map that makes it look a little bit more normal。

 But these are all different color maps are all available。



![](img/e4958744496fcbb23b7c948eb7b9c702_191.png)

 Qualitative ones， these are the ones I don't like to name qualitative。 I like categorical better。

 So if you have， let's say， land cover data， things like that， it's not so much。

 You're not worried about green。 You're not worried about what the value is in between。

 They're just simply quantized values and you want them to be discolored。

 This color is colored and you want them to be distinct from each other。

 There's a bunch of color maps that are available。 And again， remember。

 you can make a whole bunch of color maps for yourself as well。



![](img/e4958744496fcbb23b7c948eb7b9c702_193.png)

 You don't have to use the ones that are here。 And then there's a bunch of miscellaneous ones。 Flag。

 This one I do blame MATLAB for。 So if you're French， you're Russian， you're American。

 flag works great for you just depending on where in the cycle you're in。 [laughter]， Prism。

 it's just bastardization of JET， really。 Ocean， oddly enough， looks very much kind of sort of like。

 Parula， but it's not， it's really weird。 Again， these are just miscellaneous and not necessarily bad or anything like that。

 The GIS to NCAR， that's the one that we use for radar images。 So for the meteorologist among us。

 typically the one that used for radar images， it's a terrible， utterly horrible color map。

 So I keep it down here at the very bottom。 Like you'll see like it's dark and then it gets like light there and then also dark again。

 And then it's light and then dark and then it's like it's some stupid color map。

 But you want to know where it came from？ The FAA。 I blame FAA on this one because where you can fly。

 it was marked green。 Where you had to watch out for and flying your plane was where marked yellow。

 And then where you shouldn't put your plane ever was where marked red。

 And then they decided to make a color map out of that。 So I blame the FAA on that。

 So you can specify the color map by string name。 And so it's just to take the same data here。

 just again random data。 And I'm going to display them as an image doing the gray and doing cool。

 warm。 That gray was an A。 I guess we do accept both forms of gray。 Oh no， no， no， right there。 Yeah。

 I never remember which one。 Okay， so we have gray with an S。 I just now noticed this。



![](img/e4958744496fcbb23b7c948eb7b9c702_195.png)

 We have a gray with an S。 But it had an E there and then we have gray without an S。 But it's an A。

 Okay， I got to talk to somebody about that。 So let's -- Tom， I think we have a bug。 All right， so。

 you know， it's the same data， but with two different color maps applied to it。 That's all。

 And so it just makes everything look different based on which color map you're using。

 And so that's why it's important to pick a good color map and more importantly to not pick a bad one。

 Because it can impact the results。 And one of the things you'll see in that presentation by Nathaniel Smith is that it will point out that there was actually a study done where medical images。

 brain scan images -- I think it was brain scan images or something like that。

 When done in jet color map， the lab technician had an increased rate of misdiagnosis than if it was just simply gray scale。

 And so the conclusion is jet color map can kill you。



![](img/e4958744496fcbb23b7c948eb7b9c702_197.png)

 All right。 Oh， latex users or those who like to call it LaTeX。

 I honestly don't care which way you call it。 But so， matplotlib， again。

 being a library used by scientists and scientists loves using latex because it's better than using Microsoft Word。

 I'm seriously。 I'm really excited to be able to do this。 And so。

 you can actually have matplotlib call out to LaTeX to generate any text objects and then bring it back and automatically embed it。

 You don't have to worry about it。 All you have to do is have LaTeX installed。

 And just simply want the really， really basic things that LaTeX provides。

 you can do what we call math text， which is our own built-in home version of the most common things that we find people doing in LaTeX。

 In particular， the math type operations， so the fractions and the subscripts and superscripts and the Greek letters and things like that。

 That way you don't need to actually have LaTeX installed on your computer。

 We can actually manage to， for the most part， make things look like if it was done using LaTeX。

 We're not perfect。 We don't have ligatures and stuff like that， but it looks pretty decent。 So。

 how we do this？ Basically， if you have basically anything inside a set of dollar signs。

 if you specify that as a math text string， which， actually enough， that's what you do in LaTeX。

 right？ You have the dollar signs， so you have that inline mode of the math text。 You read them。

 parse that out， and interpret that。 So， here we have backslash sigma underscore i equals 15。 So。

 this should be the sigma， the Greek character sigma， with an i as a subscript， and then equal 15。

 And that's going to be in the title。 Look at that。 You didn't have to call LaTeX。

 You didn't have to do any of this stuff。 I didn't have to have LaTeX installed。

 I do have it installed on my machine because I am a good little scientist。

 but it didn't need to call anything out。 We can if we wanted to， but we don't have to。

 But then that will work just fine。 Notice the use of an R right here。 What this means in Python。

 I don't know if they went over this in the software carpentry。

 What that means is treat this as a raw string。 And so， you guys know the backslash n。

 the backslash r， the backslash。 These are the escape characters to mean new line and return。

 These are the special characters and stuff。 In Python， when you make a string with that。

 it will automatically interpret that to mean a new line and things like that。

 But not if you do an R。 So， if you do an R， it will treat everything as the raw string。

 And therefore， it will not turn。 Let's say you're doing the Greek letter new。

 and you have a backslash n， u。 If you didn't have the R there。

 you would have a text that would be just a u that seems to be a little bit lower than it should be。

 And actually， I think in 3。6， they now disallow unknown escape character sequences now。



![](img/e4958744496fcbb23b7c948eb7b9c702_199.png)

 So， backslash。

![](img/e4958744496fcbb23b7c948eb7b9c702_201.png)

 Oh， just warning at this point。 Yeah， so in the future， what's going to happen？ So。

 backslash s isn't a， I don't think that's a real escape sequence。 It used to be in Python。

 They were just silently just allowed that。 It didn't escape anything。 It was just there。 In future。

 Python's like 3。7 or 8 or whatever， they're going to actually make that an error because that's just not valid sequence at all。

 So， it used to doing the R and you won't have that issue at all。 How do you make it what？



![](img/e4958744496fcbb23b7c948eb7b9c702_203.png)

 How do you use that？ There's， yeah。 So， you will say， use tech equals true。 We'll try this。

 I haven't actually ran my LaTeX in like 5 years。 So， we'll see。 Okay， it probably did not work。

 Because my LaTeX is probably ancient or just not working anymore。



![](img/e4958744496fcbb23b7c948eb7b9c702_205.png)

 And so， it's apparently silently failed。 [ Inaudible ]， Yeah， it's， yeah。 I'm sorry。

 I think we have a bug。

![](img/e4958744496fcbb23b7c948eb7b9c702_207.png)

 It didn't error out for me。 Just， yeah。 We'll have to look into that。 Okay。



![](img/e4958744496fcbb23b7c948eb7b9c702_209.png)

 Well， if you stand it out， it should just go down to right below。



![](img/e4958744496fcbb23b7c948eb7b9c702_211.png)

 Yeah。 Anyway， that's neither here nor there。 Now， the next thing。 So， when you have polygons。

 things like that， the bar graphs， the field contours， things like that。

 This is actually something that I very much care about because a lot of time I find myself doing publications and papers。

 doing papers for publications that are black and white only。 And so， therefore。

 you're very pretty colored bars， graphs and stuff are completely useless because they all look dark。

 And so， you got like three different categories and stuff and you can't distinguish them。



![](img/e4958744496fcbb23b7c948eb7b9c702_213.png)

 Hatches are to the rescue for this。 Unless you really want to do like different scales at gray。

 but I kind of like hatches。 So， these are the different ways you could specify hatches。 So。

 forward slash， back slashes。 Again， remember when you're back slashing， you're actually escaping。

 You're going to get the same size。 You're going to get the same size。

 You're going to get the same size。 You're going to get the same size。

 You're going to get the same size。 You're going to get the same size。

 You're going to get the same size。 You're going to get the same size。

 You're going to get the same size。 You're going to get the same size。

 You're going to get the same size。 You're going to get the same size。



![](img/e4958744496fcbb23b7c948eb7b9c702_215.png)

 You're going to get the same size。 You're going to get the same size。

 You're going to get the same size。 You're going to get the same size。

 You're going to get the same size。 You're going to get the same size。

 You're going to get the same size。 This came from MATLAB。

 It probably came from other software before this。 But the one thing that always bugged me was that it was only colors that you could cycle。

 And the way this cycling worked was that if you didn't specify a color。

 it would pick the next one in the cycle。 There was just an internal cycle that was just held in memory。

 It goes， "Okay， this person just did a plot command， but he didn't specify the color。"， "Okay。

 the next one's green。"， "Okay， this person just did a plot command。

 but he said it wants to be black。 I'm going to make it black and leave the cycle alone。"。

 But it wasn't extended to anything else besides that。 It was just color。

 So you couldn't cycle hatches。 You couldn't cycle line styles。 You couldn't -- line styles are very。

 very useful in black and white publications， because it's very hard to tell what color those thin lines are。

 But it's easier to see dash and dotted and tell the difference between them。

 So why not do general cycling of different kinds of properties？ And so for version 1。5。

 you're truly implemented property cycling。 Which is a generalization of color cycling。

 And so we deprecated colors just pure color cycling and we have implemented as a property cycle。

 And so the default style， still， cycles just color。

 But you can add other properties to it to cycle if you wanted to。

 You're probably still wondering what the heck I'm talking about。

 But this is really not that complicated， I hope。 So here -- we -- at different versions of map plot lip it's been released since 1。

5。0， we've made slight improvement to how the property cycle can be specified。

 and the different places you can specify it。 This is one way you can do it。

 There's a few other different ways to do it。 But what you do is you create these cycler objects and you can compose them。

 And in this case I'm just simply basically zipping them up。

 I'm just creating three properties to cycle through。

 So I want red lines that are with one that are solid。

 I want green lines that are with the four that are dash dotted。

 And I want cyan lines that are with six that are going to be dotted。

 So each -- I just added those three cyclers together and made a property cycle out of that。 Oh。

 an odd little thing -- and this is something Thomas wants me to tell you。 Thomas。

 you've been doing map plot lip now for what， seven or eight years， something like that。

 Just today Thomas learned this。 He never knew this existed。

 This just goes to show you that -- and you know， every single time I go back over to the tutorial。

 I learned something new as I make improvements and stuff during I've been doing this tutorial。

 like now for like four years now。 Map plot lip is just that awesome。

 It's just every single time you go back to it you find something new。

 So it just kind of helps keep map -- keep learning map plot lip all the time because it's just。

 that interesting and that fresh if you will。 Or you can take the negative view of it and go。

 "It's so freaking big。"， But I like to be optimistic and stuff。 It's always fresh。

 It's a new thing to learn every time。 So anyway， so we're going to add a property cycle that's going to cycle not just color。

 red， green and cyan， but it's going to cycle three different line width and cycle three different。

 line styles。 And I'm going to do -- I'm going to do the nice simple。

 easy to re-plotting command rather， than the more obtuse matlab style。

 I'm going to call plot three times and you'll see exactly what I mean。 Look at that。

 We just now cycle three different things。

![](img/e4958744496fcbb23b7c948eb7b9c702_217.png)

 And so you can choose what properties you want to cycle。 So let's say you don't want to cycle。

 color it all。 You're strictly going to be a black and white publication and so you need this thing to look。

 very distinct and just want them all dark。

![](img/e4958744496fcbb23b7c948eb7b9c702_219.png)

 That's okay。 That works。 I think that's all blue。 Okay， that's right。 We fail back to black。

 It used to be blue， but now it's black。 So， yeah。 You can do a bunch of different properties。



![](img/e4958744496fcbb23b7c948eb7b9c702_221.png)

 Now this is where I killed two birds with one stone。

 I'm going to show you guys hatching at the same time， show you guys property cycling。

 So I'm going to do fills and I'm going to cycle between red， orange， cyan， and yellow。

 And I'm going to do these four different hatch combinations。

 So here I have just x -- so I'm going to have a dense x as well as horizontal lines。



![](img/e4958744496fcbb23b7c948eb7b9c702_223.png)

 I'm going to have crosses with o's and dots。 And then I'm also going to have just star。

 And let's make some ugly ties。

![](img/e4958744496fcbb23b7c948eb7b9c702_225.png)

 They look better than what my kids gave me for Father's Day。



![](img/e4958744496fcbb23b7c948eb7b9c702_227.png)

 But yeah， you can see that star one， let's double -- let's do three stars because it's just so awesome。



![](img/e4958744496fcbb23b7c948eb7b9c702_229.png)

 It actually makes it more dense。

![](img/e4958744496fcbb23b7c948eb7b9c702_231.png)

 So that's the way how hatching is implemented。 And then the other slightly odd thing about hatching is I'm going to zoom in here。

 You can't actually zoom into hatching。 This is something that confuses a lot of people。

 And then it actually causes a lot of confusion because one of the other things we did with updating between 1。

5 and 2。0 and the style change。 We also increased the resolution of the fault resolution of images。

 Because the resolution increased and so it has some confusion there。 Sorry。 But， you know。

 that's progress for you。

![](img/e4958744496fcbb23b7c948eb7b9c702_233.png)

 All right。 Cool。 Cool。 We are on track。 All right。 So this next thing I'm going to talk about。

 Does anyone have any questions about what we've talked about so far？

 Because it's a lot of stuff to digest。 You guys want a break？ We can do a break。 Sure。 All right。

 I'm not going to demonstrate anything here about the topic of transform。

 But because most of the time， and when I say most of the time， I'm talking about 99。99。

99% of the time。 You're not going to have to worry about this。 For those who have been curious。

 you may have noticed how things have been -- it behaves -- oh， yes。

 the other fun thing with the hatches is that as you move around， the hatches don't move。

 It's a fun little thing。 You notice the ticks automatically move。

 the tick labels move as is as I pan and zoom。 And you might be curious， well， how does that work？

 And it's all through the transform system。 And so we have this transform system where we have different levels of transforms from figure all the way down to data。

 So figure axes will actually display figure axes and then data space。

 And so -- and these transforms are composable。 And you never really have to worry about it。

 but they're also separable as well。 So you may say that， okay。

 this particular thing is going to be specified in the data space for the x direction。

 but it's going to be in the figure space in the y direction or something like that。

 And so that way you can kind of pin things to particular areas。 So， for example。

 as I was doing this panning， it's moving things in the data space。 Meanwhile。

 these axes spines are not defined in data space。 They're defined in figure space。

 So I can go ahead and move this thing around all I want。

 It's never going to move those spines because they're not defined in data space。 But meanwhile。

 these tick labels， these are the ones on the x direction。

 they're defined in the data space for the x direction， but they're defined in the figure space。

 Or actually， you know， the figure space for the y direction， those separable in that sense。

 And so the transforms are all combined and come together like that all under the hood for you guys automatically。

 So this is the magic of Matplotlib that all these things all oriented that way。

 And that's how you have all this wonderful interactivity without you ever having to worry about what any of this does。

 So if you add a tick label here and a tick label there。

 they're going to be exactly where you expect them to be after all this interactivity。

 And you're moving things around and you're zooming and panning。

 And even if you set your own limits and stuff like that。

 you don't have to write up one bit of code to respond to any of that。 You just say。

 "I want the thing to be here。"， And it will work。 And that's basically what the transform system is。

 I go into a little bit more detail about it。 And there's also a fantastic documentation for those who do want to do some more advanced things。

 You can do a nifty thing where you can say， you can actually make a transform on top of an existing transform。

 where you say， "I want the thing to be offset by， let's say， seven points or， you know。

 so many inches or something like that。"， So wherever it is， I want to make a shadow behind it。

 Let's say you can do sort of effects using transforms。 It's a neat little thing to do。

 Because then that way you don't need to actually know what the coordinate values are of the thing you're making。

 You're just going to be having a copy of it slightly offset or some other thing。

 The transform system is also how we can have log scales， polar projections。

 we can do other sort of fancy tricks and such like that。

 We'll later talk about a couple of packages。 One called base map， the other one called cardipi。

 Cardipi base map is an older map plotting library。

 It did not take advantage of the transform system。 It's going to die。 I'm speaking。

 I'm saying this as the package maintainer。 I'm killing off base map because it's not using the transform system。

 Cardipi， a newer thing that also does map plotting， it does use the transform system。

 So you can do all sorts of wonderful interactions with your， with your plots and things like that。

 You can do things and things behave the way you expect it to。

 Base map doesn't behave because we didn't use the transform system。

 So if you fight against the machine， the machine will eat you。

 And that's what's going to end up happening。 And now you know where this magic coming from。

 It's coming from the transform system。 So if you want to learn more about it， it exists。

 And it's perfectly usable to use if you want to。 Other things I've been talking about。

 So you may have made， may have heard me mention time to， oh， by default。

 it uses the solid line style or by default， the color is blue or by default。 This happens。

 that happens。 The map plot lib RC file is the default system。

 And so anytime you don't specify something， it will go and check the RC file to see if there is a default value to use。

 That makes sense。 And we'll use that。 So anytime that you say none， the Python object none。

 it means go and check the RC file。 Or if you don't specify it at all。

 that's the same thing as saying none。 And so what this has allowed us to have happen are multiple styles。

 Anyone here heard of seaborn？ The seaborn package？ Okay， so seaborn。

 they provide the seaborn styles。 And so that's just simply a RC file that it loads up over on top of the defaults that map plot lib has so that it can make its plot look the way it wants。

 There's another package that exists called pretty plot lib。 But now。

 some people like things look different。 We have styles that are good for people doing black and white publications。

 And we have a bunch of different styles that are all done through the map plot lib RC file。

 So we have the default built-in style。 But then you can also specify your own。

 And so if you want to know where your own RC file is， you can run this little file。

 You can run this little thing and it will tell you where it's loading up your RC file。 So here。

 this file here， I can go and edit that if I wanted to。

 And I can make changes to what would be the default style of all my plots every single time I load things up。

 This is also the place you go if you want to specify a default back end or if you want to specify some other things that aren't really style related。

 But maybe， let's say one thing that you can do for those who are doing animations。

 you want to specify the default encoder to use for animations。

 You can go into this RC file and edit it there。 That way， that plot lib knows where to。

 where to use to generate a MPAG or whatever。 Alright， there's a few different ways to， so the file。

 and that's what gets loaded up by default。 And you can even then tell it to use another file within your own code。

 We also have a few things where you can actually edit individual values and you also have functions for reverting back to defaults。

 So we have MPL/RC defaults。 What that will do is that it will revert everything back to the built-in defaults。

 which is useful for a variety of different things。

 And then here is how you can edit some of those entries in the RC。 So for lines。line with and lines。

line style， I can set these two values like so。 These two commented out lines。

 they're equivalent to this line up here。 You see this pattern in that plot lib all the time。

 We provide old ways of doing things that may be one way。

 We also provide other more concise ways that may not be as flexible， but they're concise。

 So we provide both of them。 They're both perfectly valid to use。

 So here I want some thicker line with the usual and I want them to be dashed dotted。

 And then I'm going to make that plot。 So here's the first plot that happened because I did that plot before。



![](img/e4958744496fcbb23b7c948eb7b9c702_235.png)

 I called this and then here I'm making this call after。



![](img/e4958744496fcbb23b7c948eb7b9c702_237.png)

 So I'm going to make that plot dash dotted。

![](img/e4958744496fcbb23b7c948eb7b9c702_239.png)

 Yay。 I can do all sorts of things。 I'm not going to waste my time on this right now because we've got to move on。

 But this RC system is how you can change the defaults。

 Or you could have just also explicitly stated that you wanted line with equals two and line style equals dash dot。



![](img/e4958744496fcbb23b7c948eb7b9c702_241.png)

 So just as easily done that that is just perfectly valid。

 We provide multiple ways to do it because different ways suit different use cases。



![](img/e4958744496fcbb23b7c948eb7b9c702_243.png)

 Okay。 You can imagine a situation where you have a script where let's say your your publication wants a color version of your plots。

 but also a black and white one。 Because color one will be what goes online while black and white one is what gets in the paper hard copy。

 There you run the same script but with two different styles。

 So it's the same code running same images being generated just with two different styles applied。

 It makes things easy that way to do that。 All right。 And then yeah customizing map。

ly that's how you can talk about how you can load up different styles and how you can customize different styles and things to your liking。



![](img/e4958744496fcbb23b7c948eb7b9c702_245.png)

 All right。 Leave it。

![](img/e4958744496fcbb23b7c948eb7b9c702_247.png)

 Okay。 Section five artists。

![](img/e4958744496fcbb23b7c948eb7b9c702_249.png)

 This is the last big section quote unquote， but hopefully won't take too long to do this。 Well。

 better not take too long to do this because you don't have much time。 Okay。 Artists。

 So I mentioned this before anything that you're seeing in the figure anything that is visible is an artist。

 including the figure itself。 The figure is actually technically an artist or anything that can draw B drawn is an artist。

 And this is the base being object if you will， if you come from Java。

 This is our Java being if you will。 This is the common thing that gets shared and used throughout and we have this hierarchy of artists。

 So you have a figure artist， an axes artist， axis artist。

 things like that is all just a hierarchy and works together。

 We also have many different kinds of subclasses of artists for their drawings。

 We have primitives and we have containers so figures and axes and axes。 They're all container types。

 Meanwhile， circles， polygons， line markers， things like that。 Those are all primitives。

 They're the raw things that get drawn。 Let's take a look at a list of a variety of them。

 We have wedges， arrows， line 2D， rectangle， ellipse， fancy box patch， path patch。

 polygon and circle。

![](img/e4958744496fcbb23b7c948eb7b9c702_251.png)

![](img/e4958744496fcbb23b7c948eb7b9c702_252.png)

 I wouldn't be surprised if there's actually a few more than this。

 but this is probably the main ones you'll ever come across。



![](img/e4958744496fcbb23b7c948eb7b9c702_254.png)

 And they have all different kinds of parameters and stuff that you can do to parameterize them and use them and customize however you darn well feel。

 These artists， you're probably wondering why am I now talking about this result？

 All those plotting functions that we've made， those things all create what you see from these artists。

 And so you can now imagine， yeah， we have this list of all these plotting functions that are all very useful。

 but what if they're not suitable for what you want？ What is it not really plotting what you like？

 You could make your own plotting function by loading up the data， by passing in data。

 passing in a set of keyword arguments for properties and saying， okay。

 I'm going to generate these artists。 This tuple of artists or whatever。 And that's what you return。

 but you will also add these artists into the axes。

 You'll see an example then in a second of what happens。



![](img/e4958744496fcbb23b7c948eb7b9c702_256.png)

 So you'll see here， I create a patch collection， I give it some of the data。

 and I have to explicitly add that collection to the axes。

 I have to explicitly add the line to the axes。 So these are all those sort of things that you didn't have to do when you made a plotting function。

 But when you call the plotting function， but when you make a plotting function， yes。

 you're going to regenerate these artists and you're going to say， okay。

 you're going to go in those axes， you're going to go in that axes。

 You're going to have to do all this tedious bookkeeping to make sure everything's there。

 but once you add them， they all will become first class citizens， just like all your classes。

 And just like all your other plotting functions you've made， so you can interact with them。

 you can do all sorts of other fun stuff with that。

 And so we've actually been playing around with some of these artists。

 So remember when we grab the bar objects from the bar call and plot， you get a list of lines。

 we can mess around with some of the properties。 So we see， you know。

 here we set the line width of one of the lines to five and set the line width of the other to ten。

 So， and also mess around with the transparency， so you can kind of see the blue through the red and all that stuff。



![](img/e4958744496fcbb23b7c948eb7b9c702_258.png)

 So you could do these sort of things messing around with these artists objects。



![](img/e4958744496fcbb23b7c948eb7b9c702_260.png)

 So you can also find out what sort of properties are available。

 different artists have different properties that are available。

 so you can look up what the properties are。

![](img/e4958744496fcbb23b7c948eb7b9c702_262.png)

 We have a get P function and pie plot， so you can see what all the fun properties are that you can mess around with。

 Okay， collections， so there's primitive primitive and then there's primitive collections。

 so these are collections of primitives that are implemented in such a way that it takes advantage of the fact that they're all the same thing。

 They're all lines， or they're all markers， or they're all， so we can do certain optimizations。

 That's what collections are for。 So here I'm creating a line collection object。

 It's just simply three lines， but they're all going to have common features about。

 They're all going to be common in a sense。 They're all going to be handled together in one object。

 So I'm going to say that sets color to red。 So they're all going to be red。

 And I'm going to say it sets a line width to five。 They're all going to be a line width of five。

 And then if I wanted to， I could specify a list of colors to use。



![](img/e4958744496fcbb23b7c948eb7b9c702_264.png)

 I could specify a list of line width to use if I wanted to。

 That's what you can sometimes do with certain things in line collections。

 Some things you can't specify individual that for， but most things you can。

 This allows us to do optimizations， particularly with markers， could then be said， okay。

 it's the same marker just over and over and over again。

 That actually makes things a little bit more efficient in many， many places。



![](img/e4958744496fcbb23b7c948eb7b9c702_266.png)

 Okay。 Yeah， so I'm talking about some of those optimizations of markers。 Okay。

 So here's one regular poly collection。 So it's going to have five sides。 I'm giving it。

 it's going to be 20 of these things are going to be made。 They're 20， so I'm getting x。

 y value 20 times。 And here's a transform thing。 You know。

 so I'm saying I want to put these in data coordinates， trans data。

 And then I'm going to add that collection in。

![](img/e4958744496fcbb23b7c948eb7b9c702_268.png)

 Again， this is stuff that you most likely never have to deal with。

 but know that it exists so that when you do run into a situation where you need to make something really custom。

 you can do it。

![](img/e4958744496fcbb23b7c948eb7b9c702_270.png)

 So these are 20 stars or 20 pentagons that we put in here。



![](img/e4958744496fcbb23b7c948eb7b9c702_272.png)

 And again， in the interest of time， let's give yourself five gold stars。

 And you guys know how to cheat by now， right？

![](img/e4958744496fcbb23b7c948eb7b9c702_274.png)

 Solutions。 So I even give you a link to documentation for a star polygon collection。

 So you want a five pointed star。 And I provide the offsets， you know。

 the locations of where they're going to be。 And that they're going to be in that the offsets are specified in data coordinates。

 Because I could say that I want them to be in bigger coordinates or whatever。

 but I want them to be gold。 And I want them to be large， 175。 I like my stars， nice and large。

 And to make it easy to see， I'm going to give it a blackout line。 I have four gold stars。 Sorry。

 it's four or five pointed stars。 I keep getting myself mixed up on that。



![](img/e4958744496fcbb23b7c948eb7b9c702_276.png)

 So yes。 Do you ever wonder when you see that a movie was rated four stars， you go， well。

 what's the scale？ Was it out of five？ Was that eight？



![](img/e4958744496fcbb23b7c948eb7b9c702_278.png)

 You just， they don't ever say。 So， all right。 Last one。



![](img/e4958744496fcbb23b7c948eb7b9c702_280.png)

 The light is at the end of the tunnel。 You just don't know if it's a train。



![](img/e4958744496fcbb23b7c948eb7b9c702_282.png)

 All right。 So the last thing I want to talk about。

 and really actually I should make this section a little bit bigger。

 When I originally wrote this section， there weren't a lot of other packages available in that work off of Matplotlib。

 Ever since then， there's been this explosion of packages building off of Matplotlib。

 I mentioned a few。 There's seaborn。 Panda's uses Matplotlib for a lot of things。

 And X-arrays uses things。 And there's just all sorts of stuff out there。

 I can't even begin to start enumerating them。 But there were certain packages that for the longest time。

 they were developed by the Matplotlib team。 But they were not actually included in Matplotlib proper。

 And that is that they're not under the Matplotlib namespace。

 They kept them separate because of a variety of different reasons。

 And so one of it was that the feature that it provided was a useful feature。

 but it didn't quite behave like you totally expected to be。

 And they wanted to avoid confusion and make it clear that these things are useful things。

 but don't expect it to be exactly like a normal axes object or a normal figure object or things like that。

 They are separate。 They may not obey every single rule。 The other thing is that one of them。

 base map， the package that I'm trying to kill， that I am the maintainer of。 Yes。

 I'm the perfect maintainer for it because I'm the laziest maintainer。 I wanted to go away。

 To install base map， you need to download and install about 200-some-odd megabytes worth of stuff。

 And so 15 years ago， you've got to do that every single time。

 That was not reasonable to have people have that included as a regular part of the dependency for Matplotlib。

 We made it separate。 So base map is used for plotting maps。

 So for all the various people who want to do weather plotting and geographical plotting and stuff like that。

 we have base map there。 Don't use base map for new stuff。 You'll find it for old stuff。

 legacy apps and stuff like that。 I'm actually supporting base map until 2020。

 That's when the end of life of Python 2。7 comes。 When Python 2。7 just end of life。

 I'll cut one last release of base map and I'm washing my hands clean of it because base map is not written in Python 3。

 And so I can't -- and it's just basically a 10，000 line in net file。 I'm not kidding you。

 It's terrible。 But it was written 15 years ago and it solved a very important problem back in the day。

 Its replacement is cardipi。 It is not managed by Matplotlib。

 It's done by a completely separate organization and group。

 But we're working on trying to get all the features that are in base map into cardipi。

 So there'll be a sprint。 Maybe some of you guys might be interested in -- if you're interested in map plotting and stuff。

 Come on by and try it out。 Try out cardipi and such。 Try to get cardipi ready for 2020。

 So try to make any new code that's doing map plotting used cardipi。 Don't use base map。

 Only use base map if cardipi can't do the job。 And then report that as a bug to cardipi。

 So if you're interested in map plotlibs， you'll get mplot 3D。 These are fake 3D plots。

 I'm also speaking about this as the maintainer of mplot 3D。 I keep getting all the crap stuff。

 I know。 I just needed it for one semester。 And then because I touched it -- your germs。 Yeah。

 that is the danger open source programming。 When you do fix a bug。

 you become the de facto maintainer because you're the last one that looked at the code。

 So do be careful。 This is the lesson I learned 10 years ago。 I know nothing about 3D plotting。

 I just needed one pretty plot 10 years ago。 So mplot 3D does fake 3D plotting。 It is not great。

 But what is nice is that unfortunately all the real 3D plotting that's available out there don't act at all like map plotlib。

 So if you wanted to do this， this thing right here， you just saw that it was actually fairly simple。

 And this looks a lot like your other commands that you've done。 Plot。subplot。

 You got your figuring axis。 You just have to add one additional argument。

 You have to say that you're using 3D projection。 That's not an unreasonable request。

 I grabbed some data and I make a wireframe。 These look like plotting commands that you've been used to in mapplotlib。

 In other packages out there， myavi， btk， things like this， you can't do that。 This is not possible。

 You have to specify everything。 It's utterly insane。

 If you just wanted to make this one plot because you got this one little bit。

 you have to go through so much work to make that happen in the real 3D plotting stuff。

 We do fake 3D plotting here。 Don't make complex scenes and you'll be okay。

 What I mean by complex scenes is that if you have a say 3D bar graphs and then you also have lines going in and around it。

 it won't work properly because you're going to get these Escher effects where things are in front of other things。

 but they're really behind and stuff。 It looks like you're looking at an Escher painting because it just doesn't look physically real。

 That's because mapplotlib is not a real 3D rendering library。 It's a 2D rendering library。

 We just came up with a fake way of approximating it in certain ways。

 The other beautiful thing is that it is interactive。 You can rotate this thing around。

 All I'm doing is clicking and holding my mouse and moving my mouse around。 That's all I'm doing。

 And then with your right mouse， the right mouse button， yeah。 This feels like mapplotlib。

 doesn't it？ So the one thing you can't do and know this feature is not being implemented anytime soon is log scale。

 And that mapplotlib。mplot3d does not use the transform system。 It should， but it doesn't。

 That's because this stuff was written 15 years ago before the transform system existed。

 And I made an attempt to make it work。 Yeah。 And you need the transform system in order to do the log scale stuff。

 One day maybe I'll have the time to do it， but like I said。

 I only needed one pretty picture 10 years ago。 It's not my itch anymore。 Axie's grid one。

 This is a really， really neat package in MPL toolkits。

 You notice it's called MPL toolkits because you're not importing from mapplotlib。

 You're from MPL toolkits。 But this is not a separate package you install。 It comes with mapplotlib。

 So you install mapplotlib。 You get these two packages as well。 You know， buy one， get two free。



![](img/e4958744496fcbb23b7c948eb7b9c702_284.png)

 Axie's grid one is called Axie's grid one because there was actually a previous one called Axie's grid。

 And it was actually the old version of it。 Use Axie's grid one now。

 But it can do all sorts of really neat things。 I'm just going to demo one of it。

 Just a couple features right now。 So here， it's really easy to create a color bar that spans this。

 And then notice that the tick labels automatically disappeared for the interior stuff。

 That way they're not running into each other。 Things like that。



![](img/e4958744496fcbb23b7c948eb7b9c702_286.png)

 Neat。 And then this is another -- this is like one of those things。

 This is called parasite axies where here you'll see -- so you saw here this is the twinning feature that I showed off before。



![](img/e4958744496fcbb23b7c948eb7b9c702_288.png)

 Note with twinning as I pan and zoom this stuff around。 Things move nicely。

 Why do I feel like I missed something？ I don't know。 The legend here is moving around automatically。

 I feel like I missed a complete section。 I don't know。 Anyway， we don't have time to go back to it。

 Oh， well。 Yeah， I must have completely skipped the session on legend。

 Legends are generated automatically。 You just have to say that you want to turn it on。

 And then you just have to say ax。legend and it will automatically add it in there。

 And then note that it moved around to get out of your way。 See if Matlab ever does that for you。 So。

 Yeah。 No。 This is one of the reasons why this is an MPL toolkit that right now I'm moving only one of these。

 So if you had a twinning situation you would actually be moving both sides。

 So things would actually be behaving like you expected to。 But here this is the parasite access。

 That's the feature that's being shown -- showed off here。 It's this third one over here。

 If you ever wanted to have that feature available， you can do that。



![](img/e4958744496fcbb23b7c948eb7b9c702_290.png)

 And then finally this is the "Oo" and "I" moment。

![](img/e4958744496fcbb23b7c948eb7b9c702_292.png)

 Yeah。 This is the other thing that you can do with X's grid。



![](img/e4958744496fcbb23b7c948eb7b9c702_294.png)

 People like this for some reason。 I can see use in this。 And possibly this。

 I have no idea why one would ever want to do that。 But yeah。

 And it actually still works with the -- well， yeah。 It's a fake。 Yeah。 Again。

 this is why it's an MPL toolkit and not in Matlab。

ly proper because it's not actually doing a real thing。

 Because you can't actually pan and zoom this stuff as you would expect。 But， you know。

 if you just need to make something that looks like that， you don't care about all the interactivity。

 It's right there for you。 So I provide the link for the documentation for X's grid one。



![](img/e4958744496fcbb23b7c948eb7b9c702_296.png)

 You can take a look。 It has a lot of features and a lot of very useful stuff in there。

 Really useful especially when you're having to deal with many images with shared color bars or multiple color bars for multiple images and things like that。

 So all very useful。 Thank you guys so much for coming and for seeing through my terrible。

 utterly horrible jokes。 Please give yourself a round of applause。 Thank you。 [Applause]。

 [BLANK_AUDIO]。