# SciPy 2017（合集） - P20：Cython for Data Scientists and Data Scientists  SciPy 2017 Tutorial  Dillon Nied - 哒哒哒儿尔 - BV1Cs411A76Y

 >> Good morning， everyone。 So I apologize for the delays in getting started。

 For those of you who are not here around 8 o'clock， or are not paying attention to。

 the Sython tutorials Slack page， your instructor Kurt Smith is not me。

 He has suddenly fallen ill this morning and is unable to be here。 So we will do。

 we will do what we can to get through the pieces of this tutorial together。

 Have any of us had a dream where we show up to school and。

 realize there's a test and forgot to study？ So when I was in grad school。

 the new grad students used to get， hazed by being given someone else a slide deck。

 That they had to present， they didn't get a chance to see beforehand。 This is being filmed。

 and this is four hours long， so this is exactly my nightmare。 >> You can do it。 >> Thank you。

 Thank you for the vote of encouragement。 Hopefully this won't be too terrible。

 and you will keep coming back for the other tutorials， and keep coming back to SyPy。 Hopefully。

 Kurt will be feeling better later in the week， and you can feel free to approach him and pester him with questions。

 For the time being， if there is a tricky problem you have， or a really intricate question。

 especially a question that involves God forbid C++。

 I would like to suggest that instead of asking me。

 you direct those questions to Prabhu who is sitting right here。 So welcome to our scytheon tutorial。

 Could I see just by a show of hands very quickly， how many of us have used scytheon before？

 A little more than half of us it looks like， "Okay， good。 Have we all heard of scytheon before。

 signing it for this tutorial？"， I'm seeing a couple of hands not raised。

 so maybe our last question is， "How many of us hate raising our hands？"， [laughter]。

 I think that's the rest of them， all right？ So we're well covered。

 So scytheon is a super set of the Python programming language。

 that gives us very easy access into C and C++ level constructs。

 There are some libraries in Python these days that are being written entirely in scytheon。

 and there are people who used to write code in C that now write code in scytheon。

 principally because it is easier to read， it is more likely to be correct。

 and it's easier to onboard someone into a super set of Python， that it is to onboard someone into C。

 if you're looking for other people to help develop and maintain your code base。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_1.png)

 as you go on in time。 So scytheon is created by someone named Kurt Smith。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_3.png)

 Again， not me。 He wrote this book about scytheon。 He is the absolute expert。

 He used to work for the same company。 Oh， so I'm Dylan， by the way。

 I worked for a company called Enthot。 This is a conference we put on in the rear。

 So he used to work for us too。 He now works for a company called Homeaway。

 which also has offices here in Austin。 He， I guess， was a physicist。 I've never actually met him。

 And then a scientific software developer， and now he is a data scientist over at Homeaway。

 He uses a whole bunch of tools， a lot of which are very in vogue at the moment。

 including things like Figno， Caris。 This is not pi NCMC。 This is something a little different。

 pi NC3。 And he used to work in oil and gas finance in travel。

 I don't know if that means he traveled a lot， or he worked for the travel industry。

 If you see this video， I'm so sorry for my training in travel。

 So what we're going to be doing here today， is we're going a little bit deeper into the internals of scytheon。

 to see the good use cases for scytheon， the bad use cases for scytheon。

 We're going to motivate our discussion by putting， sort of plain vanilla Python up first。

 and we're going to compare scytheon's performance against it。

 If you look a little bit further on in the notes， you'll see a description somewhere that says scytheon code。

 will give you about 60 times speed up in your performance， for numerical applications。

 This is sort of an average maybe。 The actual performance gain you will see will vary pretty wildly。

 for very computationally intensive programs， especially ones that are recursive。

 You can see performance gains that are up to， three orders of magnitude in size。

 So if you are doing a very strong numerical computing。

 this is definitely a very good library to know。 There are。

 I haven't looked this far in the materials yet， but apparently going to be some templates。

 that you can use for your own scytheon projects later in the future。

 And of course for this particular tutorial， everything we're going to be doing is inside of these Jupyter notebooks。

 using this very， very handy sort of auto compile and run magic function。

 If Jupyter is something that you are really excited about， the Jupyter people are here too。

 This isn't on the website， but I heard they might be doing a sprint this weekend。

 so that could be available to you as well。 There are some things that we are not going to be talking about。

 We're not going to be talking about pointers in C or pointer arithmetic， much to my happiness。

 We are not going to be talking about memory allocation， or how Python counts references。

 So Python itself is of course a garbage collected language。

 And you are never actually destroying things in memory。

 It's Python's garbage collector that sort of scoots along after you。

 and scrubs away all the things that you don't need anymore。

 We're not going to be talking about the C API in Python。

 You will see it pop up a couple of times in the notebooks as we go through。

 So things like the Pi object， class of objects in C。

 If you ever start using Python to do things like， a wrap C or C++ code directly by hand。

 this is something that you might want to start thinking about。

 It is possible of course because Python is a language written in C。

 to write your own C wrapper extensions for Python without ever getting close to Python。

 And there are examples at Python。org for how you can do this。

 We are not going to be talking about taking a C or C++ code base and wrap it with Python。

 because it requires C and C++ expertise that frankly I do not have。

 And I guess he was concerned that the participants might not either。

 So this tutorial is going to be different because it is much more hands-on。

 both in the sense that there is actual code in all of these cells that you will be。

 shift-entering to run as we go through the tutorial。

 But there are also little questions and exercises that I get to pose to you and make you do。

 We are going to go through the basics of Python fairly quickly so that we can get into the more。

 exciting things and have some people who use Python in their daily work。

 teach those parts of the class instead of me。 So my name is Dylan。

 We have two people joining us here。 This is Prabhu in the blue shirt and Chris in the blue shirt。

 They will be covering the later part of this class and they will be available during the class。

 to help field questions。 And I guess later in the course I haven't looked this far into the notebooks yet。

 There is going to be data science focused exercises that we can have you work on。

 So we will go through maybe the first four or four-ish notebooks。

 Hopefully this will take us between somewhere like a half an hour and an hour。

 at which point we can have a break for coffee before they take it away at 10。30。

 Because we all know how important coffee is。 All right。

 so if you haven't already I would like you to make sure that you have。

 either the Docker image running if you are interacting with this through Docker。

 This is what I have right here。 Or you have done one of the non-docker installs and you started your Jupyter。

 notebook server and you have notebook 00 up preliminaries because we are going to start。

 executing cells together now。 So for this class we will be using a Jupyter notebook extension for Sython。

 that has the special percent sign percent sign CYTHON。 This is a Sython magic。

 So the first thing we are going to do is load that extension in。

 And then we can execute the Sython magic cell containing our Sython code。

 Now typically when you work in Sython this is sort of a。

 I was going to say a two-step maybe a three-step process。

 So you start with your Sython code which is defined inside of a 。pyx file。

 And the first thing that Sython does is it transpiles that code from Sython code into native C。

 If you have gone through this process one of the things that you will observe is that the。

 C code that is generated is much more verbose。 So simply from a typing point of view you are saving yourself quite a lot of time。

 It is fairly typical to see 100 lines of code in Sython expand to something like 500 in native C。

 It does some really clever optimizations under the hood and it will do type guessing。

 If you are not very explicit about the static types you will be using。

 After it has been transpiled into C it is going to get compiled down into native machine code。

 So that is step two and then step three is of course you can import that extension now。

 into a Python session and you are interacting with that code from inside of Python but the bulk of。

 the work is being done sort of at the C level。 So by using the Sython magic we are taking that translation and compilation step。

 and sort of having that happen magically hence the magic function behind the scenes for us so that。

 we can immediately interact inside of our Jubyter notebooks the things that we have been defining。

 So now that we have our first Sython function which is going to multiply some integer by Pi。

 we can use it and see what happens when we multiply Pi by 10。

 and we see something that looks like a very reasonable approximation of Pi times 10。

 Is there anyone who is seeing a very strange number like 1000 or a very small fraction like 0。04？

 All right so this is good I'm not seeing any hands up so either you're one of those people who。

 doesn't like raising your hand or are reasonably certain that your compiler is working。

 For those of you who haven't seen the syntax before inside of Jupyter notebooks。

 and inside of the iPython ecosystem generally we can follow some sort of command with a single。

 question mark which is going to pull up the doc string。

 and so what we see here is the doc string for the Sython magic that tells us what's happening so。

 it's creating some temporary directory called Sython where it writes out that 。poix file。

 and does that translation compilation and then re-importation step for us。

 There are lots of arguments we can include。 It looks like there is a specifier for saying which kind of Python syntax you want to use。

 so I guess you could have Python 2 syntax inside of a Python 3 notebook although it seems just like。

 a horrible idea maybe we're going to recommend against that one。 More importantly here you can。

 also link to specific libraries that you would have to have a Sython compiling against。

 so for those of you who are maybe not so familiar with C there are a whole bunch of dynamic libraries。

 on your computer that can give you sorts of different superpowers so for example if you have a particular。

 version of the like open blads that you'd like to use or a math kernel library you could specify。

 those flags here。 I think this is something that we're not going to worry about for this class。

 but it is something you should think about for the future。 It looks like we have one more one more。

 so we can execute which is going to use the special banks syntax which in Jupyter notebooks is going to。

 redirect the following command instead of going to Python it's going to go to your systems terminal。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_5.png)

 That's unfortunate。 [inaudible]， So in order to find out where this is supposed to go I'm going to have to actually look at the。

 the structure inside of the docker image so maybe we'll skip that I assume what we're。

 supposed to be looking at here is just the actual dot pyx compiled function so we can say oh this。

 actually did create some file and some directory in your docker image。

 Now I'm very curious who Javi is。 All right so this is the end of notebook 00 this might be a good time to pause and ask if there。

 are any questions before we continue。 So my guess here is that this will be in the actual so inside of you for using docker inside。

 of that docker image we'll have just its own little file system and this will be inside of the。

 local IPython configuration directory so when you install Jupyter when you install IPython in your。

 system they create these hidden directories in your home directory that contain a lot of。

 information about where IPython is to find things and it looks like the intention here was to create。

 a subdirectory inside of this location specifically for the python pre compiled and。

 post compiled files。 So for those of you who are not using the docker image you should be able to just open a terminal。

 if you do ls flag a to look at all the things in your current home directory you should see some。

 path that looks vaguely like this。 [pause]， That's probably the correct location there's not like a dot cache in the middle。

 Okay so this looks a lot better so here are the， temporary files that have been created for us by sython and we see the actual dot pyx files here。

 in here and it looks like these might be using something this isn't this isn't temp file。

 possibly just prepending something like uid to the end of this under sython under magic。

 So here it is generating our pyx here is that transpiled ccode if we are feeling particularly。

 adventurous maybe instead of doing cat will do head and so i don't print out a million lines of things。

 [pause]， So we can take a quick look here is my ccode generated for me by sython。

 The interesting stuff if you actually do pull up one of the the native c files is going to be。

 fairly far down the page so a lot of the stuff you'll see in the beginning is a lot of setup code。

 for pulling in specific parts of the the c python api。

 Type checks for the reusing version two version three not a lot of cross compatibility stuff。

 Just for just for fun。 So it's two thousand four hundred and fourteen lines from i think this is one function。

 that we defined up here somewhere。 Yeah so this is our first sython function where we're multiplying i by by some approximation of pi。

 and getting something that looks rather large。 [pause]。

 So once we have this dot c file again sython is going ahead and using our compiler。

 to generate that down into to native machine code。

 If you are on a unit system like me this is probably showing up as a dot s o a shared object。

 If you're on a window system this will be a dynamically linked library。 [pause]， Yes？ [pause]。

 [pause]， I'm sorry between the dot p y x and the dot。 [pause]， [pause]， [pause]。

 Yeah I don't know why you're getting c plus plus files and i am not。 [pause]。

 Okay now that could be and p y x itself is an extension to sort of differentiate between things。

 that are vanilla python and then actual sython files。 I think the intention might have been。

 to have dot p y c for dot p y and then the c for sython but this of course has already been。

 used by pythons byte compiler for the byte compiled versions of your modules。

 So we have these called dot p y x。 [pause]， [pause]， It's born from pyrex。 [pause]。

 Interesting so they are pyrex files like the glass。 [pause]， [pause]， [pause]， [pause]， [pause]。

 So I guess we know that sython is is heat resistant。 Are there other questions？ [pause]。

 Alright let's move on to notebook number one。 [pause]。

 Notebook number one starts with the provocative title。 Why is python so slow？

 I might raise one little flag here and say that python is not a particularly slow language。

 Python has a lot of really clever optimizations to do things quickly to do them safely and to。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_7.png)

 do them in a very small amount of memory and especially if you are someone who is fortunate。

 enough to currently be using python 3。6。 A lot of these improvements are very very nice。

 So python itself I would not call it slow but for some tasks it is slow relative to other languages。

 And in particular if we start thinking about performing mathematical operations。

 especially something simple like addition and we want to do that a whole bunch of times in a row。

 For one particular operation python is going to be just a fraction slower than something like。

 C but when you combine all of those additions on top of additions on top of additions that。

 fractional slow down really starts to add up。 And this is one of the places where we're going to。

 see a performance difference when we switch into something like sython instead of just plain vanilla。

 python。 So there are sort of two two answers to this about why python is so slow we're going to。

 go over sort of both of them as we go through the notebook。 The very first thing we're going to do。

 is we're going to look at an actual python function and what bytecode is calling through。

 its its capi。 So the first thing we're going to do is we're going to create a function that is。

 performing some sort of additions we're using that binary plus operator。

 The next thing that we're going to do is we're going to import a module out of python called， this。

 I don't know what this does is it disassembles compiled python functions so that we can look。

 inside at the instructions in the bytecode。 So we'll execute this again where they shift enter。

 So we have four things happening here。 The first thing that we're doing is we are telling the python。

 interpreter that it should be loading whatever we called a inside of our function declaration here。

 into into its memory。 So presumably this means off of the heap into something a little more local。

 We'll do the same thing for whatever object we've given in the name B。

 And we're going to add the two of them together and then finally we're going to return out of。

 that function call or whatever the outcome was。 So this might seem like it's fairly simple but。

 in each one of these steps there is quite a lot of other things going on。 So it's not as simple as。

 like oh I have two integers and I know I'm performing some kind of an integer addition。

 So what we're going to do first is we're going to look at what exactly this binary add thing is。

 So if we look at the python source code which is open source of course it's now available on。

 github so it's even easier to find。 You can find it looks like the binary add is in a file called。

 ceval。 Now the first thing we're doing is we are grabbing a couple of python objects。

 So this is the pi object here from the capi we were talking about for python。

 And we have a commented out warning not to try to micro optimize things which also just might。

 be good life advice。 And then we are following this up with a couple of checks specifically for whether this is a。

 Unicode character。 When it is not we're going to pull out this this pi number add。

 So we've gone from at the very top in the bytecode this binary add for adding two things together。

 To now we have something else to look up which is this pi number add。

 For those of you who are interested in the garbage collector which we are not talking about this。

 is a directive to the garbage collector right here telling us to decrement the number of references。

 we have to the thing on the left and then also the thing on the right。

 So now that we've seen what binary add is the next question is given that I have two。

 two numbers of some kind what is this pi number add object that we were looking at。

 Pi number add is taking two arguments both of them pi objects。

 Now we're going to call one of them v one of them w， and we're going to start off here。

 by trying to do this this binary operation one， followed by a bunch of checks so for example if one of the objects in particular has。

 a not implemented flag set on its magic add operator what we're going to try to do is reverse。

 the order of these things and then perform the operation in the opposite direction using。

 something like the R add magic。 So this was our pi number add and once again we're deferring a lot of the actual work to this binary。

 op one so let's look at binary op one。 Once again we are taking our two objects we still have that v we still have that w。

 and we are initializing a couple of things a couple of places in memory that have nothing in them。

 And it looks like if they are， both numbers we are using this this nb bin op。

 followed by some more defensive code some more type checking some more not implemented checking。

 So the next thing we have to do is we're going to go down to look at nb。bin op。

 which is looking for a particular nb method for performing this operation it's looking for a。

 particular binary function so we can keep chasing those and eventually we come to a function defined on。

 long objects and it's going to allow us to finally add these two integers together。

 We are adding these two values creating a Python integer from them so this is Python long from。

 a c long and this is what we are returning eventually back to the to the Python section so this is our。

 Python object and then once again a whole bunch of checks for size some directives sorry some directives。

 to our reference counter。 So there is something a little bit strange here which is this medium value。

 we can think about what that medium value might be。

 And this looks like some sort of check for handling the actual size that's being allocated to these。

 integer objects。 Okay so that was a lot of code that we just we just walk through。

 One thing you might be wondering is why was there so much for an operation that seems like。

 it should be very simple we're just typing that single plus into the computer and just have it。

 work and there's all this stuff going on sort of behind the scenes going on under the hood。

 What are we doing？ So the first thing here is that when we issue that plus operator this is some。

 binary add against sent to the Python interpreter and the Python interpreter has to actually figure。

 out what that's supposed to mean。 So we have this interpretation step where we have this byte。

 code we're receiving and we have to have a way of pulling up individual C process calls out of that。

 The second sort of big source of slowdown here is that of course in Python we really。

 braced this idea of strong polymorphism so we can have these binary operators like the plus。

 operator working for any kind of object that we would like。 And this is one of the amazing。

 features of Python but it also means that the Python interpreter has no way of knowing in advance。

 what it is getting when it sees that plus operator。

 And even for something that seems like it should， be similar things like adding two numbers together the actual code that's being called when you see。

 that plus operator is going to be wildly different and if these things are two integers if these。

 things are two floating point numbers if these things are two complex numbers。 So there has to。

 be a lot of lookups for what type of object is this can I perform this particular operation on it。

 and we saw that there was also a whole lot of error checking。 So in each one of these steps there's。

 a check for if I look at the method defined on this particular object in Python am I seeing that。

 not implemented flag that tells me I have to look elsewhere for where this addition operator is defined。

 And then finally there's a lot of error checking around how big is this object there's a lot of。

 memory management we are increasing reference counts we are decreasing reference counts and for。

 us the programmer this is very nice because it means that we don't have to worry about things。

 like memory leaks inside of our Python code but because we are putting all this work on the Python。

 interpreter that means that our code is not going to run as quickly and the difference is going to be。

 much larger for very small tasks like addition and it becomes noticeable。

 And then finally there's this last step where after we have done all of our stuff inside of C。

 we have to repackage it into a Python object so we can pass it back up to the user to start doing。

 things with。 So what we might want to do next is do do a little bit of timing so for those of you。

 who haven't seen it before this is maybe not my favorite feature but it's definitely in the top five。

 of things that exist inside of the iPython ecosystem this magic time it when we run it with a single。

 expression it will run it a sufficient number of times to take about a second or longer。

 and it's going to give us its best guess for how long this operation actually takes to complete。

 sort of ignoring all the other stuff that's going on in my computer like talking to the projector。

 and running the Jupyter notebook itself。 So for our foo one and two i think was just that addition。

 step so we can see that for adding these integers this is taking about 96 nanoseconds。

 and for performing string concatenation again with that binary plus operator this is taking about。

 140 nanoseconds。 Now what you see on your own hardware might be a little bit different than this。

 that's totally fine but when we start comparing the timing of Python code to the timing of。

 Python code later in the program just make sure that in your head you're making your comparison。

 between the numbers either from my first computer up here and my second run later on this computer。

 or from your own local timing tests。 All right so to summarize the first notebook we have two major。

 sources of slowdown in our code the first being that our Python interpreter has to figure out what。

 to do when it sees these bytecode instructions。 The second thing it has to do is it has to figure。

 out what kind of addition am I actually performing because on on my computer I might have an infinitely。

 large number of things that I need to to check first。 So this is the end of notebook one before。

 we move on to notebook two I would like to pause and ask if there are any questions about what we've。

 seen so far。 Yes。 So there's like a couple a couple things going on。 So I'm not 100% confident。

 about this。 My best guess is it has to be somewhat related to the fact that Python and see think about。

 integer size very differently。 So in the world of Python and integer can be arbitrarily large。

 So in Python we don't see things like integer overflow for example whereas in C of course you。

 have a limit to the size that your integers can have and this is limited by the amount of memory。

 you allocate to those integers。 So presumably this is a check for sort of that compatibility。

 later between the two。 But if my if my C experts know more。 Yeah feel free to jump in。

 How do I debug Python is yours currently not working。 Sure。

 So one of the nice things about Python is it still gives us that Python like way of interacting。

 with things。 So the error messages you get out of Python are fairly informative。 It'll show you。

 the stack trace it'll tell you what it expected to see it'll tell you what it's on instead。

 So that's going to be our sort of our first step if there's a problem。

 Our zero of the step is going to be when that Python compiler transpiles and then compiles。

 that code down to see you will get transpiler warnings saying that for example you declared。

 this object to be a floating point but you are inserting doubles into it later。 And then of course。

 you still get the the C compiler warnings as well。

 So if there is an issue when this does get compiled， from that C down into your native machine code。

 So you have like sort of three sets of warnings， you can see。

 Now the actual that dot C code still lives in your system。 So we looked at the just。

 ahead of it the first 20 lines a minute ago。 So you are at any point welcome to load that into。

 an editor of your choice。 And if you have some sort of particular CD bugger you like to use。

 to walk through a couple examples of executing code and see what happens at each level。 Yes。

 Please do。 So you can actually go from five on down to see if you're looking at the C code and try to figure。

 out what to do。 Yeah。 That's what like I'm able to go to see or see code but I'm not able to step to the site of code。

 Yeah。 That won't be。 Yeah。 You never get to step to the site of code because it's there to be。

 attributed and turned into C。 I believe this the C code that gets written is marked up at a link with。

 the lines from which the C was generated。 So you give yourself a hinting when you're looking for the code。

 But otherwise you don't walk through the site。 Are you going to cover site with -a？ Yes。

 The other questions before yes。 Just curious if you're going to turn this at some point before you。

 Are you going to look at when we should use the line versus the site on？

 I look at - you'll get some speed up to keep it going。

 What does it work the effort in the work in site？ That's a terrific question。

 I don't believe there is a description about that in the notebooks， although。

 I've only looked at the first five。 So this might show up later。

 I think I can answer that question to， some extent。

 We are of course very concerned about our time on making the best use of it。 One of the。

 things that we know is that human time is always more expensive than computational time。 So one of。

 the things we want to do is use our computers to reduce the cognitive burden on people。 So it might。

 not be worth going to the trouble of translating everything in your Python code base into Python if。

 there is a sort of an intermediate solution。 And NumPy is one of those intermediate solutions。

 So I think my answer to your question would be use NumPy if you can。 And when NumPy doesn't provide。

 you enough functionality or if it's not flexible enough， I'm at that point I would transition into。

 Python。 Now that being said， the barrier to entry in Python is fairly low for the performance that。

 you get。 I'm not sure this is something that we will see as we go through these notebooks， but。

 typically you can take some Python code that's fairly math heavy。 You change that extension from。

 dot py to dot pyx and you sprinkle in maybe a dozen static type declarations and you see an。

 immediate two order magnitude performance gain。 Now you can really tinker with it to get your code。

 to run even quicker， but the actual sort of big bang for the buck comes pretty fast。

 Is that helpful or okay？ [inaudible]， So to echo the gentleman's response。

 if you already have code that's very heavily reliant on NumPy and， using NumPy well。

 you might not see a performance gain。 I was switching that code into Python。 In general。

 maybe I can ask the videographer， is it helpful to have me repeat the questions and。

 answers from the audience？ Okay， we can start doing that。 Yes？ [inaudible]。

 So another gentleman has chimed in to say that he likes to think about it as writing code that。

 is vectorized versus code that is iterative。 If your code can easily be vectorized， NumPy is。

 a solution for you and if the solution needs to be iterative， you should be using something like。

 Python。 And if members of the audience would like to keep answering questions for the rest of the。

 tutorial。 All right， so we were going to transition into notebook number two。

 We're going to start thinking about what exactly it is that Python is doing that is going to make。

 our Python code work a lot more quickly。 So we saw that we had two major sources of slowdown。

 one of these being that interpretation step and the other one being all of these lookups on。

 dynamically defined objects to see how am I actually supposed to add this thing。

 So we're going to play around with a couple of very simple Python functions to see where。

 these performance benefits are coming from。 So because this is a new notebook， we do not share。

 Python interpreters between individual notebooks。 So we need to reload that。

 Python extension so we can have really handy access to that Python magic。

 And the first thing that we are going to do is we have a function here called SIFU。

 Now that looks very similar to the foo we had before in vanilla Python， we were adding together。

 A and B。 And the next thing that we are going to do is now that we have compiled it。

 we are going to use that handy magic time method to see how long SIFU is going to take to add。

 two integers together that one and that two。 And this is now about 82 nanoseconds。 So a little bit。

 faster， not much， but a little bit faster than the Python code we looked at a minute ago。

 The next thing that we are going to do is look at the modules of SIFU。

 I had to see that it is here in home Javi-N， iPython， SIFU。C Python。 So here is my。

 shared object built by on my computer。 This would be GCC。

 It looks like the intention for the next couple of cells is to calculate the actual。

 performance difference that we are getting。 I assume these numbers that are hard coded in。

 are coming from Kurt's computer。 You can feel free to edit these yourself with。

 the code you got from running the Python version of FU versus the time you got from running the。

 SIFU version of FU。 So we see that for Kurt。 The speed of that he got from using SIFU for the。

 integer edition was about 29。5%。 I am going to go to the notebook where we did our timing for。

 the integer 1 and 2 for me。 That was 95。7 nanoseconds。 And then for SIFU was 82。8。

 So my performance gain was maybe a little bit less than Kurt's。 For me it is about 13。5%。

 We are going to do something similar with that string concatenation example that we had from。

 our pure Python code。 So we are going to use our meta-timate function on SIFU given A and B。

 And this is currently at 121 nanoseconds。 So we can run Kurt's timings here。 And for Kurt he saw。

 a performance gain of about 16%。 And we can put in our own timings。

 And for me it is going to be a little bit less here at about 12%。

 So what we are looking at here is the same code that we had before。 All we are doing is returning。

 that A plus B we have not done anything special with static declarations which is where we are。

 really going to see the performance gains come in。 So this is just simply from using a compiled。

 versus an interpreted edition statement。 So just having that compilation step in between the。

 declaration of the code and the actual runtime operation of the code here is giving us it looks。

 like somewhere a steady between 10% and 20% performance gain。

 So this is not the big fun part of the class but this is also interesting to see that this is。

 contributing to the benefits of SIFU on here。 So if we look at， and I'm not going to execute this。

 link because I think this is still the incorrect address， but luckily Kurt has had the foresight。

 to pace the code that we would have seen underneath the cell here。 Correct。

 So I'm not sure this is a thing that we cover maybe later in the notebooks。

 but it is true that you can do multi-threading in Sython。 So because we are dropping down into。

 that C later， we have access to all of those C-like behaviors that we're used to having。

 for very performant code。 One particular example of which would be using something like OpenMP。

 to distribute tasks across the cores of a CPU。 I'm sorry。

 I'm failing at announcing the questions to the videographer。 So the question was， what about。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_9.png)

 multi-threading？ And the gentleman has pointed out that multi-threading is also going to come with。

 this communication cost and yes， of course， that's always something that comes with parallel designs。

 and programming。 So that functionality is available to you， but again。

 you want to think about whether， the trade-offs here are going to be worth it。

 So if we look at the transpiled。 Yes。 Not that I'm aware of。 The question was。

 are these pi objects being pulled in from Boost？ The answer is clearly not。 Yeah。 Thank you。

 Prabhu and Chris。 So if we look at the transpiled C code from the Sython CIFU object that we just wrote。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_11.png)

 we see again here that same pi number add entry point。 That we saw before。

 So we can conclude that converting from this is in very large font。

 from interpret it to compiled code， is giving us the speed up。

 But the real big performance gain we're going to get is by adding type declarations into our code。

 So one of the nice things about working in Python is that as a dynamically typed language。

 we are not constrained into declaring in advance what kind of an object that we're going to be。

 dealing with。 And this becomes very， very useful for having code that is very modular， very。

 composable。 But it comes with a significant downside。 And that downside， again， is the exact。

 kind of performance that we're talking about。 So if you know in advance that you're going to be。

 getting integers versus floating point numbers， you can allow a Python to optimize around those。

 cases and avoid a lot of those dynamic method lookups that we saw sprinkled all throughout。

 the actual C code from C Python。 So the next thing that we are going to do is we're going to define。

 this is not only a， factorial function， this is a recursive factorial function。

 That's going to compute the factorial， for some number n。 In the first case here。

 this is a pure Python function。 So we can declare it， with a shift， enter， we'll run shift。

 enter again for this magic time it to see how long it takes， and then immediately after it。

 and we will see what the output of the factorial is。 And the， factorial of 20 is a large number。

 Competing this took that's about three， three microseconds。

 So the next thing that we can do is we can see what this performance looks like when this code。

 is translated into into Python。 So in the very next cell， we are going to be defining two different。

 Python functions。 So this first one is going to be much like the Python function we had done before。

 where we're not adding anything special。 All we're doing is adding that one compilation step。

 Otherwise line for line， this is identical to the Python code we were looking at before。

 In the second example， you're going to see one difference。 And that difference is this word here。

 in front of the argument n。 So in the function signature for a sci-fact double， we are not just。

 pulling in some object and we are letting sci-thon know that this is going to be a double。

 So this is， a c-type double precision floating point number。

 So we can compile both of these functions。 And the next thing that we can do is we can redo that timing step first with the sci-thon。

 function with no type declarations in it。 And then secondly， the function that does include those。

 type declarations。 So in the first example， we took about three microseconds for the pure Python version。

 for the unsped up on static type declared having sci-thon version。 We've come down to about one。

 and a quarter microseconds。 So this feels pretty good。 And we're already。

 that's almost twice as fast。 Twice plus a little bit more。

 And we can run that time and again with our static type declaration。

 and we should see something rather dramatic。 There we go。 So now we are down to this is about。

 about a， microsecond。 So this one particular function call is now taking about as third of the time that it。

 used to。 And the difference again is that one word， declaring that what I'm getting in a。

 advance is that C-type double。 Now we can do something a little funkier。 There are two。

 additional things happening here。 The first is that we are declaring not just the type that is being。

 put into this function call。 So not only is it receiving a double， we're declaring what's being。

 returned out of this function。 So it receives a double and it returns a double。 And again。

 these are double precision floating point numbers。 The next thing is instead of having just the def。

 Python function keyword for declaring functions， we have CP def。 Now we'll talk in I think notebook。

 four about exactly what this is doing。 The takeaway here is it is making sort of。

 the brief version is making two different functions out of this one declaration。

 The first is a native， C function that only deals with C objects。

 And the second is a little wrapper function that knows how。

 to translate between those types and the Python types。 So we can declare this， we can transpilot。

 and then compile it and then re-import it。 And during this time session， we are now down to。

 there we go， about 80 nanoseconds。 So we are now 40 times faster than we used to be。

 And this is the point in the talk where we feel very， very good about being here。 Perfect。 Answer。

 So the short answer is yes。 The slightly longer answer is it might not be as performant as you。

 would like。 This isn't something I've ever tried to do myself though。 So I don't know if。

 there is special syntax for -- sorry， yes， thank you for reminding me。 So the question was。

 is it possible to siphonize a function that accepts an arbitrarily large number of inputs？

 So for Python syntax， of course， we have like the splat orgs and double splat orgs that allow us。

 to pass an arbitrarily large number of positional or keyword arguments into our function calls。

 And the question is， if this is possible within Python。 [ Inaudible ]。

 So the follow-up question was， if I can guarantee that all the things that I'm receiving are doubles。

 is it possible to， for example， receive an arbitrarily large number of doubles？

 And I think I'm going， to have to punt this question to the experts。

 So an audience member has tried this out in real， time。

 This is one of the nice things about giving a talk to a room full of computers。 And the answer is。

 is that for something like a C def or a Cp def， this raises an exception。

 If you have a plain def function， then you're getting compiled into something in Python。

 Then it will accept that orgs。 But again， we might not see the same kinds of performance。

 boosts that we would like。 [ Inaudible ]， So probably has chimes in to add that it might help to think about Python as a way of converting。

 or Python code into C。 And that for anything that is a C def or a Cp def， if there's not a way to。

 write that code in C， something I would accept an arbitrarily large number of arguments， it's。

 also not going to be something that's supported by Python。

 So we are close to the end of the notebook here。 We're going to try， I believe， just one more thing。

 And the one additional thing we're going to try is a loop-based version of the same factorial。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_13.png)

 calculator。 One of the things that we know about Python is that Python interpreter itself is not。

 particularly amenable to recursive solutions to problems。 This will not always be true。

 but generally， speaking， iterative solutions are going to be more performant inside of Python。

 So possibly， comparing the recursive Python to recursive C was not really fair。

 So what we can do here is define， iterative versions of the solution。

 both for pure Python and for Python， and compare their， performance。

 So we're going to start with our PyFAC looping function to calculate our， factorial n。 Once again。

 we can time it。 And I guess we're also looking at the output to make。

 sure that Python isn't lying to me about the result。

 So we should still see something to the power of， 18。 And this looks quite a lot better。

 So our recursive solution was taking about three， microseconds。 We're now down to one microsecond。

 So for those of you who were looking for a quick， performance gains for pure Python。

 this is one of them， is to stop writing so many recursive， function calls。

 We can do a similar function here， again with Python， using the most optimized， version of this。

 here we are accepting a double， sorry， we are returning a double， we are accepting， an integer。

 We are declaring the type of our return value here。 So this is that cdef double r。

 as we're declaring that return object r is going to be a double precision floating point number。

 We are initializing its value to be one。 One thing。

 if you haven't written anything in Python before， that might be a little unintuitive。

 is you actually get some pretty serious performance gains from。

 declaring the type of your looping variables。 So if you are doing something like for i in range 10。

 declaring i to be an integer is something that you should be doing。

 I think the very best performance， comes from using unsigned integers for this。

 but I don't have numbers for that on hand。 So we can do that same translation， compilation。

 re-importation step。 We can re-run that timing。

![](img/b8d9e1d8490d7c84cfc812d37b0318c6_15.png)

 function to see how long this takes。 We are at about 65 nanoseconds， and we can look at how much。

 faster we are going， and again we'll do this twice。 So we can first look at Kurt's numbers from his。

 computer。 He is getting about a 30x performance boost for our numbers here。 We went from about， 1。

1 to 0。065 and a little bit less， keeping with the things we've seen from previous examples。

 So at the end of our notebook here， we have some exercises questions。 I don't have Kurt speaking。

 notes， so I don't know if I'm supposed to make you answer these to the camera。 It'd be quite an。

 exercise to have you come to the front of the room and speak into the microphone。 The first。

 question， maybe we'll just ask you to ruminate on it， or maybe have a wander around the room。

 and then make you tell me in person， is why we are using a double precision。 So this is a floating。

 point format instead of a long， which is an integer type number。 Question number two， why are。

 pi-fact loop and sci-fact loop better from a robustness point of view？ So not from a performance。

 point of view。 And then question number three， you're supposed to rate a trivial， I assume no op。

 means。 It doesn't actually do anything。 No operation function in Python and measure with performance。

 and under the same thing in Python and compare them， and it looks like the code has already been。

 written。 So here is our declaration for our Python non-operation function， which is just the。

 keyword pass。 This is a Python keyword for don't do anything。 And here we have our。

 Python no operation function， which is just the same。 So maybe we'll take a couple of minutes。

 to have you see if you're going to answer these questions for yourself。 I'm not going to put you。

 on the spot to answer them out loud， but maybe I will come ask a couple of you in person。 And then。

 finally， you will execute these cells down here to create your Python no op， your Python no op。

 and see how their performance differs。 All right， so we had a little bit of time。

 to sit down and work through the set of questions at the end of notebook number two。 Some of you in。

 the audience had some additional questions to ask during the break。 One question that I would。

 like to answer for the class， a gentleman in the room had asked me how exactly Sigh thought。

 knows for things that are not statically declared how to translate this into C。

 And the answer to this is that in these cases， it is largely pulling functions out of Python's。

 C API itself。 So the Python interpreter is written in C。 The operations that the Python。

 interpreter performs eventually all happen in something like C。 So it is not so much work to pull。

 out that C source and to have it used directly by， by Python。 Now， when we start adding in the。

 static site declarations， and some of the seed dust that we'll spend most of the next notebook。

 talking about， what we'll see is that this compilation can sort of bypass a lot of the Python。

 C API to have this stuff directly written in native C without a lot of that Python overhead。

 So we had these three things we were working on。 The last thing was to clear a function that did。

 nothing in both Python and Python， I mean to perform a timing difference。

 What we see for my computer， up here is that the difference is between something like 75 nanoseconds in something like 43 nanoseconds。

 for the Python version。 And there's a question， what does this imply for the function call overhead。

 in Python versus Python？ And if you guessed that Python has a little bit more of a function call。

 overhead， you would have been correct。 Do we have questions about about the exercises before we move on？

 Yes。 Do you have a more specific answer for why these gates is more overhead over the。

 back of the Python？ In this particular case， so it might be possible that when Python sees a function that just has this pass attached to it。

 it returns control over the interpreter immediately back up the call stack。 I don't know if there's。

 something specific additional that's happening that we wouldn't expect， but we might believe that。

 it's a lot of the same sorts of things that we saw before that in Python we have this interpretation。

 step where we are interpreting the compiled bytecode。

 and this is not something that exists inside of， Python code。 Other questions about notebook too？

 Yes。 Oh， so why are we using a double instead of a long？ So if we use a sort of integer format。

 we don't have the same dynamic range in the number of values that we can encode， so we make it more。

 likely we'll run into something like an overflow error where we count up to some certain number。

 of integer and then start back at the negative version of that integer and start sort of counting。

 up again。 So we might not even get warned that something bad is going wrong。 We just might get。

 numbers that are very clearly incorrect。 You might compute the factorial and get like negative five。

 for example， which would be very unexpected。 By using a double precision floating point number。

 we are hopefully allocating enough space that we can encode a very large range of values。

 factorials get big very quickly， and this protects us against that。 All right。

 we're going to move on to the third notebook， the third notebook which talks about。

 the types that are available to us within Sython。 We are going to keep talking for about 15 minutes。

 and at which point we are going to take a break so that you can all get snacks and coffee before。

 the snacks and coffee are taken away。 And if it gets past 10， 15， and I'm still rambling。

 feel free to throw stuff at me。 But like nothing， nothing hard。 You can throw like wadded up paper。

 I -- please don't throw the coffee at me。 All right。

 so we mentioned at the very beginning of the talk。

 today that Sython is what we call a superset of Python。 It is a strict superset of Python。

 And what that means is that all valid Python code is also valid Sython code。 So all the things。

 that you're used to putting inside of a Python function can also go inside of a Sython function。

 all the kinds of objects you're used to having in Python you can also have within Sython。

 What Sython does is it gives you access to a lot of C-level things in addition to the Python-level。

 things that you are used to having。 And there are also some special Sython specific stuff。

 So there are some Sython helper functions for doing things like writing parallelized for loops。

 for example， which may or may not be somewhere in the notebooks。

 So to make it easier for the rest of this class where you will actually be writing Sython code。

 eventually we are going to have an overview of the types that are available to us within Sython。

 So once again， we have all of the regular Python stuff that we're used to having。

 But we also have the whole C typing system at our disposal。

 So now the first thing that we're going to do is inside of our magic Sython cell。

 We are going to create a couple of objects。 The first object is going to be the integer one。

 Our second object here is going to be the string A。 They're both being given the same name here。

 And when we call print on that object。

![](img/b8d9e1d8490d7c84cfc812d37b0318c6_17.png)

 it's referenced to always being resolved dynamically during the runtime of the program。

 So these are normal Python objects。 We can do normal Python things with them。

 But we can also have special C-type objects。 And this is what we're going to look at next。

 We're going to start with talking about integers。 So this is our integral types header。

 If you already know C， this is just going to be describing to you the kinds of types you're。

 already familiar thinking about。 If you're not someone who's worked in C before。

 this is going to be a very important notebook to keep handy。 You can of course also look up the。

 there's a link to the Wikipedia page that lists the data types that are available in C。

 And we all have descriptions about why they have certain names and how large they are， for example。

 Now the first thing that we'll talk about before we actually talk about what these。

 different types are is this C-deaf statement， C-deaf。

 This is a directive that we are giving to Sython to let it know that we are declaring types。

 to be C-type objects。 So this is a C integer， a C unsigned long， a C long long。

 Now typically the things that we declare using C-deaf are not going to be available to us from。

 inside of Python。 And the reason is it's missing the translation step from the native C data type。

 into something that the Python interpreter will understand。 We'll see later that it's very easy。

 We're going to add one additional letter and we're going to get a wrapper that will make these。

 things available to us within Python。 So there are principally two things that we're going to be。

 concerned about when we think about integer data types。 The first thing is how much space it takes。

 And the second thing is whether or not we're allowed to put a minus sign in front of it。

 So when you see things that say unsigned versus signed， what this means is a signed number is。

 allowed to be negative。 Unsigned numbers are only positive。 So the integer is starting at 0， 1， 2。

 3， 4。 A signed number can be negative 1， negative 2， negative 3， negative 4。

 Now they can both encode the same number of specific values given that the signed and the。

 unsigned version are the same size。 They're occupying the same amount of space and memory。

 But what it means is if you have a signed integer that goes from negative 126 to positive 125。

 if that integer is unsigned， its range will be shifted to the right to go from 0 to 255。 Yes。

 So the definition of what makes a number a long versus a long long is in some cases。

 architecture dependent。 So I'm not super well versed in how these rules are made。 But the。

 Dart-Kabal that controls number formats， the IEEE， has set rules for how these things are。

 allowed to be。 And typically， my understanding is that something that's designated as a long。

 is allowed to include up to a certain number of bytes， but does not have to occupy all of that。

 precision。 So if you have something that's declared to be a 128-bit number， it might only be using。

 something like 92 of those bits to actually encode the value。 Of course， I'm sorry。

 that wasn't more， helpful。 [INAUDIBLE]， Is there a shortcut to run the program？ Yes。

 So the question was， is there an easier way to run each one of these cells？

 And if you hold on the shift key and hit enter， it will evaluate the cell and then move you on to。

 the next one。 If you get to a point where I did， I don't have my power cord with me。 So my hard。

 drive shut down while I was walking around the room answering questions， and when I had to restart。

 my interpreter， there was also a shortcut to run all of the cells in a notebook。 You can go to cell。

 and then either run all of them or run all the ones above where you are。

 run all the ones below where， you are。 So for those of you who haven't used Jupyter notebooks before。

 we're not going to have， I don't， think we're going to have time in here to get into all the really nifty things they can do。

 But notebooks themselves are modal editors。 So if you're used to thinking about something like。

 command mode versus insert mode， this also exists inside of Jupyter。 And there is information about。

 that in the help documentation。 So we've seen that sign versus unsigned is telling us whether or not。

 there is a minus that's allowed to be in front of the number and then also how that range of values。

 that's covered is shifted。 The distinction between the second part of the number， so am I talking。

 about an integer？ Am I talking about a long？ Am I talking about a long， long has to do with how。

 much space is allocated to that individual number？ Is this going to be 16 bits， 32 bits and 64 bits？

 So if we are saying that things are C-def， C-defined inside of Python， these have static types in C。

 and I cannot dynamically reassign the names given to those objects to be some other data type。

 So we saw before that with Python objects， I can declare that O is an integer and then。

 overwrite it with a string later and this works just fine。 Inside of Python， I get a big pink box。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_19.png)

 So if I have something that I'm declaring in advance， I is going to be an integer。

 I'm guaranteeing this to Python and then later I try to make a keyboard designation like Quirty。

 I get this exception message that says to do， Unicode literals do not support coercion to C-types other than Pi Unicode or Pi Unicode starter。

 So the type coercion from the Unicode string here， I'm into the integer is what's failing。

 So integers are nice in that they have what we call infinite precision。 So the integer one is。

 always the integer one but the size that I'm allowed to code in my integers is very strictly。

 limited to the amount of space。 I'm going to dedicate to those integers and the other thing is。

 that given an integer number， there's no way to represent a value like 1。5。 So one of the。

 formats that we can use if we'd like to have those kinds of rational numbers or we would。

 like to have a wider dynamic range of numbers in the same amount of memory and just use something。

 called a floating point number。 So if you have been working in Python and you type your number。

 like 4。5， what you were getting was a floating point number inside of Python。 So in in Python。

 we have access to floating point numbers of different sizes。 A float should be。

 something around 32 bits in size。 Our double is going to be around 64 bits。 A long double。

 this might be the one that is closer to 92。 So once again， we can use CDAF to declare our float。

 our double and our long double， and we can print them out。 For those of you who haven't seen it。

 Python allows us to create， integer literals using scientific notation。

 If you deal with very large or very small numbers， this is a very useful thing to know。

 And just like Python gives us access to complex types of numbers。

 Python also allows us to define complex types of numbers。 Typically， these are choices large。

 as their corresponding floating points because they have to have a way of encoding both the real。

 component and also the imaginary component。 So we have our float complex which will be， 64。

 the double complex which will be 128， choices large as their corresponding types in floating point numbers。

 Now we can also have strings from within Python， with like a little asterisk here。

 So if you are working through the Python notebooks using the， Docker image。

 we are all using Python 3 where the string type is a Unicode string。 We are not。

 going to be talking about the difference between the way that Python 2， things about strings and。

 the way that Python 3， things about strings in here。 If you have questions about that。

 the best thing to do would be to wait until after the tutorial and then you and I can have a chat about。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_21.png)

 it。 Or you can see the fine manual。 And this is Kurt's documentation。 All right， so in Python 3。

 now we have two different sort of fundamental ways of thinking。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_23.png)

 about what a string is。 One of these is that it's meant to be human readable text and the other。

 is that these are just the raw bytes that I'm pulling off of my computer。

 And here we have our str_object which corresponds to that Unicode text string。

 and our bytes be object which corresponds to our bytes string。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_25.png)

![](img/b8d9e1d8490d7c84cfc812d37b0318c6_26.png)

 There is another section here about string types that are specific to the C language。 So in Python。

 we don't have this sort of idea of a single letter as a data type。 And Python， we only have strings。

 We can have strings that are of length zero， strings of length one， strings of length two。

 And a string of length one is a string of length one， that has just a letter inside of it。

 But most languages have this concept of a single character， object。

 And this is something that we have available to us now in Python through C。 So this is our。

 seedf char which is going to refer to an individual character。

 And here we're declaring that this is， a buffer of characters。

 And I'm getting an additional warning， about the risks inherent to using global Python objects from within Python。

 Which was our pop quiz。 Thank you for not throwing your coffee at me。 So it is now 10。15。

 We will break for， let's say， 15 minutes。 So you can all grab a coffee and grab a snack。

 It will reconvene at 10。30 at which， point we will finish up notebook number three。

 I hope you've all had a chance to recapinate， and to rehydrate and to re- -- I was going to say glucosinate。

 but that's not quite right。 Sugar， hopefully there was sugar involved。 Recarbohydrate。

 It's much better。 So when we left we had been going through sort of a brief tour about the types that are available。

 to us within Python。 We saw that we have all of the normal Python types still at our disposal。

 We have the additional option of doing things like declaring the size we want allocated to our。

 numeric data。 Whether we want those integers to be signed or unsigned。 And we can specifically。

 ask for this data type that does not exist from within Python。 The very last thing that we saw。

 was that when we ran the cell here， where we are creating a pointer to this character buffer。

 that we saw a warning。 And there is a pop quiz here。 When working with C-level strings。

 what must we keep in mind to maintain Python guarantees？ I'm not going to make you answer this。

 question。 Chris was helpful enough to come answer it for us。 And the reason that it's generally。

 speaking a bad idea to work with C-buffer strings inside of Python is that the Python。

 interpreter is assuming that all of our strings are immutable objects。 Particularly because we'll。

 use them for things like keys in a dictionary。 Whereas the C string characters are immutable。

 during the runtime execution of the program。 So you might create things that look like Python。

 strings and that mostly behave like Python strings。 But whose data become modified。

 Which will make bad things happen。 Guedo Bonrasum will show up at your house。

 Looking somewhat displeased。 So we have just a couple more things to talk about in C Python。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_28.png)

 Not C Python， sorry。 In Python， we also have access to an additional set of data structures。

 that you might be using。 You might be used to using from inside of Python。 We have access to。

 things from the array library。 We also have access to things like daytime objects。 So if you end up。

 dealing with dates and times inside of your Python code， you can keep your access to the same。

 kinds of Python structures。 At the beginning of this line， we're starting it with something called。

 C import as opposed to import。 The little note here says that we will cover C import later。

 I don't actually know if that's true or not。 So we will say a brief thing about it now。

 C import is the key word we use to import functionality specifically into the C layer that's being。

 generated by Python and not something that's going to be available inside of just the normal Python。

 environment。 So here we are importing specifically the daytime objects from C Python into the C code。

 that we are writing inside of our C dev statements。 It just sees all the way down。 As one bit of。

 clarification， because someone asked me about this the last time I talked about Python， you'll hear。

 me sometimes talk about the C level。 And what I mean is that at the C level of code， like the。

 letter C， not the ocean。 The last， the very last cell in this particular notebook is talking about。

 declaring and manipulating pointers。 There's a note here that says only do this if you have to。

 And since I do not have to， what I would like to do is ask if there are any questions before。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_30.png)

 we move on to the fourth notebook。 Yes。 Yes。 So the question was the C import statements。

 or I'm importing things into the C level of my code。 Are these only things from C Python？ Are。

 these things that have to be declared specifically inside of Python？ And the answer is this will be。

 I believe， anything that has a C API attached to it。 So one of the things that I do a lot， but I'm。

 not sure we'll end up in these notebooks， is importing NumPy's C level API into this Python。

 So this is just giving us sort of a， a Pythonic way of doing something like an include。 Yeah。

 other questions？ Yes。 When you do the， when you're on the slide or where you're going to see that。

 or using Python types， is it going to do anything like what does it look like on the C level with like。

 we have a dictionary like what does that look like it see？ Is it important to think about that。

 or is that just to abstract the way we should worry about it？ I believe so。

 So the question was when we do a C def and the type we're declaring is a Python。

 data type like a list or like a dictionary， what does it look like at the C level？ Is that。

 something that we should worry about？ Or is that something that's sort of taking care of for us by。

 Python？ The answer to that question is what we're getting is essentially just that Python object。

 the way that Python objects usually behave with all their good sides and all their downsides。

 What we're doing is we're declaring that it will only ever be that object and that it's not going。

 to be something else。 So if we declare something to be a Python dictionary。

 it's not going to magically， turn into a list at some point。

 This gives Python some guarantees about how it can optimize the。

 method calls for that particular object。 What it's not going to do is give us the performance。

 benefits that we get from having a C data type there instead。 All right。

 seeing no further questions， we move on to book four， which is functions。

 And when in the notebooks it said that we are going to talk about that C def versus C p def later。

 this is exactly where that's going to happen。 So at least for now for this morning， I have not。

 been lying to you。 So inside of Python， we can use that def keyword that we get from Python。

 to define Python functions that look like Python functions that behave like Python functions。

 And these are always going to be expecting some sort of Python input and are going to be returning。

 some sort of Python output。 So we can create a function in Python， which is accepting two arguments。

 and B， it's returning a plus B。 And we can print out some some of the information about this。

 function。 And so we can look at its type。 It is a function and it has a whole set of information。

 that's attached to it。 So if you haven't seen these before， these are special thunder attributes。

 that contain information necessary for the functioning of this function inside of Python。

 This is our thunder string method for coursing it into a string。 A summary here should be a closure。

 Yeah， a thunder closure。 So if your function is enclosing aspects of its environment。

 things like objects that have been named， they go in a dictionary that's attached to this object here。

 Now we can have the same， the same function， we'll call it scyfunck。 Now， the actual code。

 hasn't changed。 The difference is in this particular case。

 We are asking for it to be compiled for us。 And here is something that looks a little different。

 So instead of saying that this is a， function， we say is now a built in function or method。 Now。

 if we look at all of these special things that are attached， all those。

 dunder attributes to the pure Python function versus the compiled scython function， one of the。

 things that we see is that the attributes of the function， things like that closure attribute。

 things like the global objects we have access to inside of our function， things like the default。

 values inside of that function are no longer going to be available to us。 So this is dynamic。

 behavior that Python is supporting， but not scython。 Just for fun。

 we can make sure that Python and scythonck are returning the same values when。

 they're given the same parameters。 And so far this has worked。 Now， we also see that we can。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_32.png)

 define a class called class， which is Swedish for class。 Now， is it the cells in being compiled？ Oh。

 with the scythonck。 Okay。 So if we define our own custom class， we see that the scythonck。

 plus operator is correctly accessing the dunder add method。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_34.png)

 All right。 So that was def the Python function declaring keyword。 We can move into the c。

 function declaring keyword and this is c def。 So the c def keyword is how we're going to declare。

 not just functions， but all of the kinds of objects we want to have available only at the， c level。

 not have access to inside of Python。 Now， there are a lot of reasons why you might want。

 to have access to your objects limited to being at the c level。 The key benefit is if you can。

 push your code down to the c level and delay coming back up to Python until the last possible。

 moment， you'll not be incurring the costs of translating objects from c objects to Python。

 objects back to c objects back to Python objects， which for one particular function call is not that。

 heavy。 But again， if you're doing that same function call many， many times in a row。

 that additional computational cost is really going to add up。 So here in the cell。

 we are defining a， c function。 This will be a c native function called untyped。

 It's going to accept two arguments， and be it's going to return a plus b。 Now。

 we are going to define a typed version of that same， function。

 which is going to accept two double precision floating point numbers。 It's going to。

 add them together。 And then before returning the result， it's going to coerce it into an integer。

 And there is a commented line out here。 Now that if I call my typed function with types that it does not accept。

 So my typed addition， function was only accepting my double precision floating point numbers。

 If I give it two strings， how would I get down here is this error in compiling the Python code。

 So this is in the， transpolation step where I'm going from that Python code to that dot c file。

 Sython is telling me that in this particular case， I'm giving types to this function。

 now that the function does not accept。 So if one of the things that you really， really miss when。

 you moved into Python is not having some sort of static type checking happening during a compilation。

 step， I'm as a way of giving you some sort of hint about the accuracy of your program。

 You now have that functionality back。 And again， once I define these objects with that cdef keyword。

 they are no longer available to me， inside of Python， only inside of c。

 So here we have that cdef declaration of the untyped and the typed functions。

 When I try to call these directly from Python， we are unhappy。

 So the third type of function that we're allowed to use is something called cdef。

 So what we've done， here is we've added one additional letter is this p after the c and before the d and def。

 What， cdef is going to do is going to write two functions for us。

 So it's going to write that clevel function， that is that statically typed really fast。

 But it's additionally going to write a wrap around。

 that function that will make it available to us inside the Python level as well。

 So a really common practice is to have a cpdef function that itself is referencing cdef functions。

 elsewhere in your module。 So here we can cpedef， a cpedef function。

 it's going to accept two integers， y and z， it's going to return the integer addition of those。

 And now that I have used cpedef， this is， available to me inside of Python and not only at the level of c。

 There's one additional thing that's happened here inside of our scethon magic function。 We have。

 included the a flag where a here stands for annotate and it's going to generate an HTML output。

 That's going to give us some hints about where a particular slow points in our code might be。

 In this particular case， we are seeing yellow highlights around things that are available to。

 be interacted with from inside of Python。 So here we see that by using cpedef， there we go。

 This particular function is referenceable from inside Python。

 Now we have a pop quiz saying that given that a cpedef function is like a cdef function with the。

 constraint of using only Python convertible types in its signature， what ctypes can we not use with。

 the a cpedef function？ Once again， I'm not going to make you answer this or to put you on the spot。

 but anything that exists only inside the world of c but not inside the world of Python is not going。

 to work here since these objects eventually have to be reconverted into a Python data type。

 Now the last thing we're going to talk about here in notebook four is how we handle exceptions。

 inside of the world of Python。 So what we're going to do is do our cpedef again。 So we can have a。

 Python c function along with a Python wrapper that we get for free。

 Now we're going to call it unchecked， div。 We're going to give it two integers and we're going to get back an integer and it's going to do。

 some sort of division for us。 So we can try running this function printing out the result of dividing。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_36.png)

 one by zero。 And we see a little warning message that says the exception was ignored。

 One of the things that we know from the Zeno Python is that we should not ignore exceptions。

 unless there is an explicit line somewhere saying that we want to ignore this exception。

 So this is probably not the behavior that we want。 So what we can do。

 is we can add this special except keyword to say that if there is some kind of an error。

 we would like to have that error raised up to the Python level。

 And here is the zero division error that we are used to having inside the world of Python。

 and when I do divide something by zero。 And this is quite a long stack trace so we are going to。

 shorten you。 Now if I have some kind of a function that has a return type in c I can specify after。

 the except here some sort of sensible to be used so that scython knows how to raise that particular。

 exception。 So in this notebook we've seen that we have three ways of defining functions。

 One just for Python one just for c and one that gives us functions inside of c and inside of Python。

 Before we move on to notebook five do we have questions about what we've just seen？ Yes。

 So if you define functions within like a Cp_depth declaration inside like one。

 Python cell tested like if you move out into a regular Python cell you can't access those functions。

 but then I was playing around with it and I tried to access them into this single。

 Python cell and it didn't access them。 So like can you only work within a single cell。

 then we'll look at that right or is something going wrong？ That's a really good question。 So the。

 question was we saw that if I use cp_depth to define that function I can use Python to call it。

 whatever I want。 If I use c_depth to define a function I can only call it inside that magic scython。

 code cell at the C level and if I try to call it in a different magic scython code cell suddenly。

 it's not working there either。 And the reason for that is that scython is generating separate files。

 for each cell and it's just a virtue of the way the scython magic works。 So typically if you are。

 defining a sort of c_depth function you would either be importing it when you need it or it would。

 be called from the exact same file。 So that's just it has to do with the way the notebook is set up。

 Very good question though。 So if that happened to you too。 Yes。

 So when you have the exception you have the exception star。 You specify what exception you're。

 doing。 But you do have the exception you want it going。 You specify which exception that is。

 That's a terrific question。 I actually do not know the answer to that。

 So the question was here we are saying inside of my function after the declaration I'm saying。

 except if there is anything that goes wrong I'd like to raise it。 Am I allowed to specify that。

 I only want to catch things like arithmetic errors。 Sorry that I only want to raise things。

 that are arithmetic errors。 So our experts are hard at work answering the question。 I'll make。

 sure someone gets back to you。 Are there other questions？ Yes。

 So if you're coding outside of a notebook format how do you close the Python block？

 So the question was if I'm coding outside of a notebook how do I close the Python block？

 And the answer is that the Python block is everything inside the 。poix file。

 So if there is something， that you did not want to be compiled by Python it would need to be in just a normal 。

poix file。 So the the Python magic that we're using here is specific to to IPython。 Yes。

 So the question was will we ever see an actual outside of a notebook writing the 。poix file。

 transpiling it compiling it and then executing it。 And the answer is that at the very end if we。

 get there and if we don't get to do that today like in the morning you can always do it tonight for。

 homework。 All right。 So seeing no further questions I'd like to turn over control of the podium to。

 Prabhu。 Prabhu is the director of Enthot India。 He's going to be walking you through the rest of。

 the notebooks because frankly we are coming close to the borders of my knowledge。

 So thank you for your， attention and welcome Prabhu。 Is that big enough at the back？

 I've changed a few things on this slide， in this notebook。

 So yeah so before we begin I'm Prabhu and I'm stepping in for Kurt I'm no substitute， I know that。

 I've been using Python and I use Python regularly but I clearly don't know as much as。

 Kurt does so although he called me an expert I don't think I'm really that much of an expert on it。

 but I think I can handle these slides。 So so far what we've seen is you kind of got an exposure to。

 the basics of Python and now we're going to sort of look at profiling and performance in a little。

 greater detail。 So the way the current the fifth notebook is set up it wasn't clear to me that。

 so all of you do all know about p-run in Python how profiling execution how you profile execution。

 of a function how do you look at the output and how to make sense of that。 I'm not sure so how many。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_38.png)

 of you have done that before。 Okay so there's a significant section that doesn't so you don't。

 have to I mean type out what I've typed I'm just going to walk you through but if it if you could。

 pay attention to my slides what's seen on the board here that would help。 So I'm going to start。

 with loading the extension so the reloader doesn't matter。

 I have just taken the same exact code that。

![](img/b8d9e1d8490d7c84cfc812d37b0318c6_40.png)

 you have over here which says all of this stuff and I have just made it a pure Python set of functions。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_42.png)

![](img/b8d9e1d8490d7c84cfc812d37b0318c6_43.png)

 So what is happening here is Kurt has created some functions here that we're going to explore。

 and try to look at the performance of these functions。 So if this is pure Python it's very。

 straightforward to do this right。 So this is pure Python code we just there's a function called outer。

 which takes a single integer argument there's a function called inner and then there's a reverse。

 which basically reverses the list and the reverse is calling out so if you look here。

 it's calling out to this underscore reverse helper okay for whatever contrived reason it's doing that。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_45.png)

 Now so if I was just to say reverse of list range 10 it does what we want it does what it says。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_47.png)

 it's doing right it just reverses that list。 Now if I want to see what's slow and what's fast in this。

 in Python and especially with an iPython notebook you can do %p run。 Now if you just do %p run you。

 can only run whatever is you specify in that one line but if you do %p run it makes the entire cell。

 something that's going to be profiled for you all right。 So you can put a bunch of lines there。

 you run it and it'll actually use the Python profiler and then count how much time is being spent in。

 every single line of your code all right。 It's doing a bit of work so if you run it it will give。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_49.png)

![](img/b8d9e1d8490d7c84cfc812d37b0318c6_50.png)

 you something that looks like this it says four function calls in zero seconds it's a pretty fast。

 function so maybe I should make it a little longer let's make it okay so that's taking a bit。

 longer so yeah so four function calls in 2。118 seconds it orders it by the internal time of execution。

 so what you're going to see here is the number of so it'll basically list out each of the functions。

 that were called all right and it'll tell you how many times this function which is some Python magic。

 dot reverse which was defined here this function it says it was called once then it's saying some。

 function in string was called okay then there's a built-in method built-ins exec is being called。

 built-in method disable of ls profile so something internal to the profiling system all right。

 So what it's going to do is it's going to list out all of the functions this is not very useful in。

 this case but when we look at the inner and outer example that's going to do some computation。

 that's going to do something meaningful all right and then it basically we'll see how much time is。

 being spent in inner how much time is being spent in outer and now you have a mechanism to find out。

 what's taking more time and then you can sit and spend your time trying to optimize that function all。

 right so let's now do the same thing oops I was sorry oh I'm sorry I ran the wrong code okay so the。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_52.png)

![](img/b8d9e1d8490d7c84cfc812d37b0318c6_53.png)

![](img/b8d9e1d8490d7c84cfc812d37b0318c6_54.png)

 first one I run this I run this I then I run this p run now you see it says built-in methods exec。

 and then it also has the underscore reverse helper you see this here so it says reverse。

 it also has underscore reverse because I ran this in pure Python right but now if I were to do the。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_56.png)

 same thing with the sythan code here right I'll try that reverse you'll see that it doesn't even。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_58.png)

![](img/b8d9e1d8490d7c84cfc812d37b0318c6_59.png)

 show me underscore reverse right you see reverse but it doesn't even show you underscore reverse。

 means I couldn't trace through it the reason is the underscore reverse helper is a cdeft function。

 which means it doesn't exist in python land it's a c function that this function is calling and python。

 has no way of knowing that that function was called and it has no way of actually tracking how much。

 time was spent in that function all right so the first thing that the exercise does or rather the。

 example does is you see this comment line here it says percentage sythan colon profile equals true。

 so if you have a pyx file at the top of that file you can put certain sythan directives okay。

 you can say a profile equals true then what sythan will do is when it generates the c code。

 it will spit out additional blobs of code right that will tell python hey this function was。

 caught so keep track of that is this clear otherwise it's just a c function so it's just。

 gonna do a jump into that call it and get back there's no way for python to keep track of that。

 does this make sense so now if i were to compile this run that it works you will see。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_61.png)

![](img/b8d9e1d8490d7c84cfc812d37b0318c6_62.png)

 that it actually says it trace this as well as this i noticed that it actually has the pyx。

 line here so which means it actually tells you this function in that pyx file at this line has。

 been called so many times and you spend so much time in this does this make sense all right so。

 two things going on that we learned the first is p run p run is a pure python thing so any python。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_64.png)

 code you have you can just two percentage p run or percentage percentage p run inside a cell。

 and it will profile the execution of all of those and give you account of how much time each function。

 took all right and if you look at that maybe you look at the output a bit that's like this。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_66.png)

![](img/b8d9e1d8490d7c84cfc812d37b0318c6_67.png)

 so what it says is these are number of calls this is the total time which was spent inside this。

 function but excluding any sub functions it called auto all right the next is per call which is the。

 total time divided by the number of calls so now it's because it's rounded it off to three places。

 which is dropped off the charts the cumulative time says that's the amount of time it took for。

 the function and all of its sub functions so if you take say let's go back to the example。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_69.png)

 if you look at outer outer is calling inner right so maybe let's do the same thing with p run of。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_71.png)

 outer and then let's see what output we get all right so it made a total of thousand and six。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_73.png)

 function and function calls in four point six seconds in thousand and one times it called。

 the inner function all right and now notice that the total time in the inner is four point six。

 three seconds which means inner is doing bulk of the work all right but let's look at outer if you。

 look at outer where's outer outer is here so if you look at this line it says that the outer function。

 the total time of execution is point zero zero three which means that the time just to execute。

 the outer alone without stepping into the inner is point zero zero three the cumulative time is。

 four point six three which means it adds up whatever function calls that go inside it does this make。

 sense so when you read it you should be able to you should be comfortable reading these calls right。

 any questions yes yes huge it's huge it's huge it's a huge it's a huge hit you take so if you're。

 basically so the the place where this helps is okay so it's a really good question i repeat the。

 question the question is when you profile the execution of a python a pure python program。

 adding profile costs you maybe 10 percent or something like that but if you're going to do。

 that with sython code because python profiler is profiling it isn't that going to add an impact。

 and the answer is yes so supposing you took a function and you optimized it to sython you。

 nicely annotated it and you generated high-performance sython code and let's say the sython function is。

 like hundred times faster all of the profiling stuff is done in python which means you're going。

 to go back to your 1x in conversion you're going to be close to your old python may not be that bad。

 but you're going to get a significant penalty because you're profiling it from the python side。

 so the question is why on earth is this of any use the reason this is useful is very often。

 when you're profiling let's say you have sython code if you can't even find out how much time。

 your sython code took you can't profile it at all at any level right so what you try to do with this is。

 when you profile your functions the innermost functions when you profile they're going to kill。

 you which means your total performance is going to be bad but what you try to do is you try to。

 find out what your performance bottlenecks in terms of the functional blocks optimize those。

 and then take off profiling so you usually never run your production code with profiling。

 all right so when you're compiling out your actual code that you're going to use。

 don't use profiling but when you want to just get the numbers to find out which functions are。

 slower than which you need to actually turn on some amount of profiling does that make sense。

 all right so it's not it is not going to be performed definitely not it's not going to be。

 performed all right but without this there's no way you can even find out which function is taking。

 how much time that's the key here yes， oh no it actually includes everything that's going on。

 so in fact if you look at it it's going to say method disable of lsprof profiler objects which。

 is nothing in our code right so basically all it's doing is it's adding a bunch of hooks at python。

 level which trap execution of the function turns on timing so it's actually doing a bunch of。

 additional work so it may hit things that you didn't you know do anything about there's a possibility。

 that it'll do that all right any more questions yes i think an implication from that that。

 i want to probably tell is that it's going to affect your timing of your side。

 you know the side is not going to include the overhead yes of course yeah yeah is that。

 what your question is all right i'm sorry then yeah so no the timing of the site and function itself。

 you know is going to be timed correctly but under the provision that your is actually now being。

 exposed as a python function and you're going to make other python function call so it's going。

 to actually be a little slower it's not going to be significantly faster。

 yes so it so basically okay so maybe let's um let's turn this off。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_75.png)

 there is my code okay this font size is not， all right so let's do a percentage time it okay so this is something that i often tell people i teach。

 that i don't know all the answers the guy that knows all the answers is your python interpreter。

 and sometimes it changes from one place to the other so the best way to actually get the best answers。

 is to try it out and find out for yourself that doesn't mean i'm not going to answer the question。

 but there's a probability that i'm going to be wrong occasionally so don't hold me against it。

 okay so let's just do a time it of say outer。

![](img/b8d9e1d8490d7c84cfc812d37b0318c6_77.png)

 let's call it say thousand， and that's going to take a bit maybe i shouldn't turn thousand。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_79.png)

![](img/b8d9e1d8490d7c84cfc812d37b0318c6_80.png)

 hmm takes a while all right so it takes 4。52 seconds per loop in this case。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_82.png)

 this is without any profiling okay did i not。

![](img/b8d9e1d8490d7c84cfc812d37b0318c6_84.png)

![](img/b8d9e1d8490d7c84cfc812d37b0318c6_85.png)

 that's not good。

![](img/b8d9e1d8490d7c84cfc812d37b0318c6_87.png)

 i shouldn't do 10，000 okay 4。42 seconds so maybe i'll make it smaller so it doesn't take so long。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_89.png)

![](img/b8d9e1d8490d7c84cfc812d37b0318c6_90.png)

 all right so 44。3 milliseconds for thousand and let's now do it with profiling。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_92.png)

 that way i should re-execute this and then come back here。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_94.png)

 i'll just rerun this i ran the one with the profiling。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_96.png)

 okay not too bad so okay so let's just do it properly。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_98.png)

 i'll do it step by step so i okay we do that we do this， i don't know that okay 41。8 milliseconds。

 on that 42。3 so there is a change but it's small it's not too big。

 sometimes the hit can be much larger all right depending on what you're doing。

 because basically what happens is now this every time reverse helper is called it has to。

 check update record that all right but it does take a small hit so yes your numbers will change a。

 little bit but hopefully by not too much right but the key point is now with the profile function。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_100.png)

 with the profile variant all of these cdef functions are also in my profile which means i。

 actually know how much time that function is taking to execute all right which is nice so now i can。

 actually profile and find out which sections of my code are going to be slow and actually optimize。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_102.png)

![](img/b8d9e1d8490d7c84cfc812d37b0318c6_103.png)

 them now the second thing you can do obviously which uh illness already covered is looking at。

 the annotations so now if you do that sython minus a it does two things for us um it generates。

 this html blob which you can inspect and look at which functions are slow and which functions are。

 fast um i don't think you didn't spend too much time on the nature of the html right all right。

 so i'll spend a little time on that so the idea here is um hang on。

 it's twofold the first is you can use p-run but if you want to use p-run you need to know how to。

 how to make sure all of these functions that you're measuring are profiled so you need to turn on。

 this you need to turn on sython profile is equal to true otherwise those functions will not even。

 show up in your profile all right the second part is when you do sython minus a it does two things as。

 i said the first is it generates this html which gives you a representation of which lines it。

 things are likely to be slow which lines it things are really optimized using a comment and then it。

 also generates the extension so that you can call the function all right but if you were to do this on。

 the command prompt you can see sython something dot p-y-x if you do sython minus a it's just going。

 to generate the c file as well as it generates an html file that html file you can again inspect。

 separately so supposing you have a p-y-x file you want to see i want to look at the annotation i。

 want to look at this html if you do sython minus a file dot p-y-x it will generate file dot html。

 sitting next to the cmc and the p-y-x files and you can open that up and you'll get exactly the same。

 thing so in this cell magic it basically does both of those together compiles it generates the。

 extension for you and shows you the html representation here so it's kind of convenient so let's go over。

 this html and then we'll try and look at what's going on so the first thing it says is this function。

 is slow so anything that looks more yellow is slow if it's white that's a good line of code all right。

 that's so from here you see that the def outer is not a it's it's a slow function because it's not。

 cp-deft which means it's not a c function all right so it's a python function which means it has all。

 of the overhead of calling a python function all right so that's number one so if you click on this。

 plus or anywhere on that line it will actually show you the python code that's sorry the c code。

 that's generated from that line of cythem and you can see that there's a lot of。

 crummy code here and goes on and on and on okay so that's like that's the amount of c code generated。

 by this line but then more interesting is the next line which is white if you click that。

 that looks doesn't look too bad the variable names look a bit messy so you see under under p-y-x。

 t-1 that's some temporary variable uh py-x v-n so usually when it when you see py-x。

 underscore v at some variable that you've defined and the last character or the last set of characters。

 will be your actual variable so py-x v-n is this n here all right so where is this defined well。

 you'll have to look here and you'll see py-x v-n is defined here as an integer right because you。

 declared it as an integer so the nice thing is you can actually see the c code you can look at the。

 types and you can act if you know c you can actually read it all right you can make sense of what's。

 going on but if you look at the actual for loop it doesn't look too bad right it's a for underscore。

 py-x t-2 okay for let's forget the variable name looking terrible um if you ignore the under under。

 p-y-x under t you basically have t-2 is 0 while whatever t-2 less than t-1 and notice that everything。

 has been defined as some variable it doesn't actually put the constant on that all right even。

 though n may have been a constant but who knows you may have changed n i don't know all right so。

 they basically generate very general purpose code so py-x v-n is py-x t-1 all right so it does。

 this comparison and it keeps incrementing by one and the next line um so that's the that's the。

 underscore that's the for loop this is the inner loop that's the inner that's what being executed。

 inside that follow and there you see a mangled name for the function this is py-x f bla bla bla。

 underscore inner that's the wrapped um sitan function for your inner and it calls that with this argument。

 py-x v-n all right so that's as close as to see that you would have supposing you were to write。

 the same function in see yourself you obviously wouldn't use a name that's that mangled you'd。

 probably just call it inner so here the name is mangled for you but you can see that it's almost。

 a one-to-one mapping of the line of python code you had to a line of see does that make sense all。

 right similar with the follow simple straightforward translation so those lines are essentially as。

 fast as sitan can make it all right the next one unfortunately is a bit complicated because when。

 you're returning you got to do a bunch of stuff right so if you're returning an integer you need to say。

 pi int from int so you're going to get an integer converted to an integer create a python object。

 call an integer and then pass it along so that's this stuff and when you do this you need to do。

 increment and decrement uh left counts in python so it's doing all of that stuff for you and because。

 it's doing a bunch of additional gunk for you it costs you a little bit so returning from that cost。

 your tiny bit doesn't make sense so basically if you look at this line it's not as yellow as the。

 first line which means it's doing less than the first line but it's still doing a lot more than。

 this one line does this make sense so that's how you kind of so you you have to sort of train。

 yourself to read these annotation files but once you do it a few times you'll get used to it yes。

 no i'm not because i actually don't even know so the way i read this when i generate python stuff。

 is the more yellow it is the worse the code is so there are several things you can do so i will。

 try to walk you through what's happening when you start making changes um what you can do and how。

 do you change so the issue is this if you see something that's more yellow that's a bad line。

 you should try to do something to that the python the python code to make it less yellow you know。

 that's kind of what you're going to look at i'm not going to i don't know how many levels of yellow。

 there exist in the python code all right but i do know that if it's more yellow i want to make it。

 less yellow all right so and you already know enough kind of to make it less yellow all right yes。

 all right so great question so the question is line two line three looks beautiful i mean it's。

 white perfect line nine looks terribly yellow right so it looks like it's doing a lot of stuff。

 there so what's the difference i mean nothing changed right there's no type annotations they're。

 not done anything yet so let's click on it that's the best way to find out and first time you look。

 at it it's not going to be very helpful right to look at this and it's like definitely not very。

 helpful it's doing a lot of stuff and i have no clue what it's doing but the first thing you look at。

 is well the first thing you look at is a clue it says pyx t1 some temporary variable it's not pyx v。

 something is i int from int which means it's trying to store an integer that's generated somewhere。

 and store it in this variable that's okay which means this t1 is probably and where is it getting。

 it from it's getting it from vn so now i know that what this line is doing is it's storing。

 the count n in a temporary variable so this line is actually not too bad all right if it wasn't able。

 to convert it it does some error handling and stuff like that but look at the next line the next line。

 is pyx t2 is a pipe tuple it's creating a tuple for me all right then it sets the tuple item to some。

 from t1 right because it's it's not really it's not really converting this into this nice。

 efficient follow-up here and the reason is i the type of i is unknown to cyto so as far as。

 cytoon goes you've now introduced this i and you're actually using i here so okay so let's look at。

 the next line bear with me so i didn't follow what the first line is doing it's too much stuff。

 let's see what the second line's doing it's saying pi number in place add which basically is a python。

 c api call how do you have written this in c you would have just said res plus equals to i。

 semicolon right that's only the only syntactic change you would have made is probably add a semicolon。

 to this line if you were writing this in raw c by yourself right but clearly this guy is doing。

 pi number in place add so what's going on so it means if it's asking python to do the addition。

 it expects that i may have something strange it may be some object and you may be calling。

 additional functions in that object it may be a numpy array god knows what so it doesn't know。

 anything more to optimize it to efficient cytoon code all right so it suggests that i have missed。

 a type declaration so this is how i approach this the way i look at this is i look at this code and。

 say wait a minute it's starting to do a bunch of python functions like this just to do an addition。

 just to do an in-place addition that's a dead sign to you that you've missed a type declaration。

 somewhere so what have we missed in this case well we didn't declare anything we don't know what res is。

 it says it's zero but god knows what you're doing in the code below it's pure python so。

 remember the approach that cytoon takes is you give it any legal python code it will compile it to some。

 legal c code which will execute and produce the same results more or less。

 more or less i'm saying because there are types right so supposing i declared cdef。

 int cytoon knows that it's going to be an integer type now if i did some floating point arithmetic。

 inside and return that you don't have to worry about this in python right because i take an int。

 and i just make it as large as i want it's not going over flow no matter what i do to it it's just going。

 to take a longer time to execute c does not do that so you're going to get side effects in。

 um c code that you've not seen in your python code okay and this is the this is the problem。

 with dealing with two languages so if you have a python code and you're doing say factorial。

 you do factorial 20 it's going to work beautifully you shove that down to c and now the type where。

 not support doing a factorial because integers are not arbitrary integers in python they're not。

 arbitrary length so that's the more or less part i'm saying so if it's if it's not a crazy function。

 that's going to explode like the factorial if it's a reasonable thing you may get the right most of。

 the time you will get the right answer all right but beyond that this code could as well have i。

 could have created a list here done some crazy thing with a list created a bunch of objects and。

 then returned a integer sythan would be happy because i'm just creating a bunch of lists i'm。

 doing some processing and as far as the c function goes it's just done some crazy thing inside and。

 spat out an integer which i can use does this make sense so what you need to do is you need to tell。

 sythan a little more information so that it is able to optimize this so maybe let's try that。

 so now let's now declare this and say c def res sorry int uh res c def int i and now i'll run the。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_105.png)

 same thing again what did i do and now it looks beautiful right line nine is now line nine is not。

 the same line but line 11 was what was line line and now you see it's perfect it looks as clean as。

 we can expect from python from sythan so does this make sense so if you see yellow moral of the story。

 if you see yellow somewhere you probably missed a type declaration and if you've made all the type。

 declarations that you think you can make you're probably good and if it's still yellow you basically。

 say okay that's the best i can get does this make sense this is the first step yes。

 okay and it's still optimizing so which means sythan is doing a bunch of type inference。

 it's trying to find out if you use that variable or not so usually in python code i don't think。

 sythan is doing this so maybe so maybe let's try and make this a bad line of code by doing this。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_107.png)

 i will use that underscore。

![](img/b8d9e1d8490d7c84cfc812d37b0318c6_109.png)

 and it's still figured it out that is pretty amazing， hmm， sythan's awesome。

 okay well i don't know so what does it do with， okay so let's that's a good hypothesis so let's do plus one now that might。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_111.png)

 yeah there you go the experts there all right yeah so um yeah general rule is that if you're。

 going up on the board you become an idiot so i'm definitely by definition i'm not the expert so。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_113.png)

 okay so you have the answer so i didn't do anything special with this all i did was add a one plus one。

 here i didn't follow pipette but so now you see immediately what it's saying i have obscene。

 sorry piantasin does some typecasting ask python to go ahead and do some addition for you so now。

 that's going to be slow all right okay that makes sense。

 all right so let's go back and clean this up。

![](img/b8d9e1d8490d7c84cfc812d37b0318c6_115.png)

 all right so the main takeaway here is if you see a yellow line that's a slow line。

 and you should try and optimize it all right so the next part is an exercise so now that you have。

 this and it's all yellow or largely yellow i want you to take the time well kurt wants you to take the。

 time to fix this annotated use the annotations try and make it as white as you can and。

 finally profile this and take a look at you know how much time things are taking to execute。

 so we'll walk around maybe give you five minutes to do this and just remember make it less yellow。

 that's that should be a moral and the way you make it less sell you is to declare things as。

 declare your types and if it's a def function that you're calling make it a cp def right all。

 the stuff you've learned up and off declaring types and doing def to cp def or c def okay。

 okay so i've been reminded that we don't have a lot of time。

 but i don't think you're going to get much out of stuff unless you do a little bit of this。

 i think it's worth spending two three minutes so you want to try is that okay two three minutes。

 try to get this to be less yellow and， in the meantime i will answer any questions you may have。

 so again you just have to modify the implementations of outer and inner to see what。

 difference it makes in runtime and it co-generated that's really what you need to do。

 i think i've actually done the that's the solution so all right so i've given you a couple of minutes。

 i'm not as nice and instructor as dylan is because if you don't ask me questions i will。

 not hesitate to ask you questions so any questions。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_117.png)

 no questions you leave me no choice yes thank you， if you use cp def so where did you use cp def。

 yes okay so great question so his question is so let me follow what he's doing i'm i have my。

 code was this guy is nice and white as in so there's no yellow here is very efficient。

 so i'm gonna now make this cdef as cp def and then see what happens and there you go。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_119.png)

 so notice that when i make it cpdef it makes that line little yellow。

 right the reason is it's a really good question because it helps to know。

 that when you define something as cpdef it is not a pure or c function which means it still has to be。

 a python like function which means it's returning something that's like a python thing now internally。

 if you're calling a cpdef， scytheon may be smart enough to call the c variant but it still has to。

 declare the code to make it a legal python function and that's the reason you see it as yellow all right。

 and sometimes if this is hurting you in your performance in your profiling numbers。

 try your best to make it a cdef function so the idea here is when you're really wanting to push。

 your performance you move as much as you can to see okay that's kind of where you're trying to go。

 move it as much as you can to native c as you can but using the convenience of doing it with scytheon。

 so that you don't have to write all the boilerplate gunk code that you have to write with c all right。

 and just by changing a single character you can make it also accessible with python so that's the。

 nice thing that scytheon allows you to do all right does that answer your question all right great so。

 yeah so since no one asked me questions so how would i make the outer。

 any faster so look at this outer is still dirty can i make it faster。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_121.png)

 yeah so first thing well a problem it's okay great so somebody said cdef and if i do cdef the。

 problem is i cannot call it from python so the only choice i have is cpdef so if i do cpdef it。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_123.png)

 probably should make it slightly less yellow i don't know if it did make it slightly less or。

 slightly more but yeah it it should be a little better because if i were to call this out of function。

 from another scytheon defined function in this it would probably be a lot more efficient。

 and this i leave as homework exercise for you all right yes please。

 very good so that's the next nice thing we can do is we could say int。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_125.png)

 but still didn't make it doesn't visually look to me more less yellow but yes if this were to be。

 used again inside scytheon you may not see as many performance gains so if someone was trying to call。

 this outer so let's say you added another function king saying def outer outer。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_127.png)

 and then you just say return outer n right so if i did this every time i call outer outer。

 maybe i put this in a loop you would find that outer outer is actually not as fast as you would。

 have expected again because you forgot to declare the return value so these are things that we make。

 mistakes right so it's i'm really happy he brought that up so sometimes you think you've done something。

 right but you've not quite done it right because you're calling it from python and sometimes it's。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_129.png)

 good to go all the way down to a cdef because then it will bomb if you do not so if i do cdef。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_131.png)

 and i do not so let's do this this will not compile like i imagine so it did。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_133.png)

 scytheon's more awesome than i thought okay but still it's little more yellow than it was。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_135.png)

 if you remember so now it's act aha so we have a problem here so now this guy is not returning a。

 integer is now returning a pi object it's saying static pi object star blah blah。

 inner takes an integer all right so let me change this and make this cdef int inner。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_137.png)

 and now let's see what it does let's look at the code static int all right so it returns an integer。

 and not a python object does this make sense so if i did not declare the return type by default。

 it will assume that it's going to return a python object and if you're going to add two python。

 objects it's going to be ridiculously slow all right but if you're going to add two integers。

 it's going to be incredibly fast because it's as fast as c can make it does it make sense so once。

 again this just shows you that looking at this code and if you have a basic understanding of c。

 they should help you all right is this clear right does that answer your question Philip okay great。

 okay so shall we move on to the next i hope this has given you a flavor of what you typically do。

 and this is i mean this is really what we end up doing when you write python code you write it。

 you annotate it you look at the html look at all the yellow stuff make sure you were removed。

 as much of the yellow as you can by adding type declarations and making sure you define your。

 functions carefully yes so we can make up here like c-initors on the next one the list。

 reverse one we're still dealing with python objects we can't do that is there any way to get better than。

 that very good question so not really so if you still want python objects you're going to take a hit。

 so there are two things that you need to generally avoid you don't want to create a heck of a lot of。

 python objects so if you have any code anywhere supposing you're doing a large something that's。

 executing for a long time if you're generating a huge number of python objects and sometimes this。

 happens even without you knowing it because if you're generating temporary it's going to generate。

 python objects that is very slow can be very slow so usually where you use python is in。

 you profile your code and you find out which functions are the slowest so if you're passing an。

 int list to that function and you write your code out using the list and iterating over the list。

 getting items out of that list will be slow but if you know the types and you type cast them and。

 you do the correct c code that part can be made very fast so if you write a simple sum function。

 for example which takes a list and you're sure that all the types inside that list are integers。

 you can actually write pretty fast code with cycle but if you have to create and return python types。

 you have your kind of autolack you have to create it so the way out of this is you go one level。

 below so if you want to create a list you don't want to create a list but you want to create something。

 more low level in c you allocate memory in c which means it comes with all of its。

 attendant problems so you have to make sure you allocate memory you free memory all of that。

 stuff you need to take care of so now you're back in c land so you need to make sure you。

 do all of the due diligence there but you can do that as well so usually that's what's done either。

 you use say if you're using c++ you can use the stl create a vector and do arithmetic on that。

 if you're using numpy though there's cool tricks that you can play and that's what we'll be looking。

 in the next session all right shall we move on i assume the silence means i can so okay so i urge。

 you to you know play with some of this experiment try writing your own little functions annotate them。

 and you know the ipython notebook interface really makes it easy for you to do this and the more you。

 do it the better you get at you know learning cycle so let's move on to probably the most。

 important chapter in your tutorial which is how do you do this with numpy arrays because this is。

 extremely important most most people actually focus here so this is the sixth ipython notebook。

 let me go all right so here's a i we don't have too much time to go into this xkcd。

 um so i'm going to treat this just as some function that we're trying to optimize all right so。

 what we're trying to optimize is an entropy function which essentially is doing this which。

 is the shannon entropy which is minus if you have an numpy array p log p all right sigma。

 sum of all of that so essentially we have this little one function here one line。

 written in numpy and we want to see can we write a cythan equivalent can we speed this up how would。

 i write this if it were not this simple function but if i wanted to write this in raw cythan how would。

 i do it all right so let's first execute this we have a little function here now we'll do a。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_139.png)

 cythanized version of this the first thing you need to note here is two things。

 um okay we have important numpy as np that's just plain python but in this cythan code over。

 here we have two things one is the important numpy as np that you've already seen but i suspect。

 this is new is c import you've done before okay cool so are you anybody have questions on c import。

 c import yes， earlier you were importing two different things in the namespace they would name the same thing。

 you've imported so i think array from the standard library and then from cythan you。

 imported cythan that array with c report how would like if i now call array which of those two is。

 being called actually i would assume it would be clobbered no oh or the scene namespace。

 so cyin port things are only available inside of c defined things and just regular imported。

 things are available only on the python side all right so here in this example you see import numpy。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_141.png)

 as np that's a python space namespace import this guy is a c import so c and p is in the c namespace。

 so what cythan does is they have a shim around numpy which is all c so when it generates the c code。

 it has all those trucks and stuff that it requires all the functions are declared as c functions so it。

 doesn't have to go through the python board so that's why it gets faster so what it also does is it。

 allows us to declare this px because i can't declare px as an int or a double or anything like that。

 and there's a way to do it but we're not declaring it as a pointer either because it's not a pointer。

 you're not saying it's a pointer to double or anything like that the numpy array is not just a pointer。

 has a bunch of additional stuff so what this let's just do is it let's just declare p of x p_x as a。

 numpy array however it doesn't say anything more about it since it's a numpy array it doesn't give us。

 type information so it's still not going to really be super fast it's probably going to be just as fast。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_143.png)

 as the numpy version maybe even slower so if you look at this again yellow lines hint that it's slow。

 spython stuff so if you look at this it's doing a lot of stuff。

 i don't even want to look at it so close it what about this one again so this is kind of。

 doing a bunch of stuff python function call， where the hell is it doing anything yeah so this is a mess right。

 this is not very helpful but it tells you that it's not really a very good line of code because it's。

 actually calling out to python because i'm saying np。sum np。sum is a python function so as far as。

 sythan goes it has no clue it doesn't know any type information because np。sum does not declare。

 its types doesn't have any more information than that so okay so let's get to the lowdown on。

 what's the import so sythan introduces a new keyword c import that allows interfacing with。

 other sythan code at cc level at compile time this is in distinction to the python's regular。

 import statement which interfaces with other python modules at runtime so the statement c import。

 as c np allows sythan to interface with numpy arrays at the c level at compile time for improve。

 performance this import statement causes the sythan comparator look for a numpy。txt all right this。

 is important so somewhere down in your installation sythan when you install pip install or conda install。

 or whatever there's a directory it has called includes inside deep inside the。

 sythan package you will see and includes i think i capitals and there you will find a bunch of。

 libraries and all of these libraries will be 。pxd so you have py pyx and you have pxd so pxd are。

 kind of like the c header dot h equivalent so they basically give you information about。

 kind of type declaration information about each of the functions or structures or objects that。

 you have all right so that's how you kind of share information about types using pxd files。

 does that make sense so if you have a pyx file all of the declarations in that pyx file are。

 local to that pyx file but if you make it a pxd file you can kind of include it in other。

 all right so um all right okay so if you really want to look at the numpy。pxd。

 i think it's not going to be very instructive right now but sometimes it's useful so maybe i will。

 try and do that， i will i'm doing this on purpose so that you don't have to see the okay maybe i can。

 all right yeah i just did this um i just did sythan file that shows me that it's installed。

 somewhere here so now i cut paste this and get out of this and this uh includes yes so numpy。

 init dot pxd and there you go so this is all sythan code so if you want to learn more sythan。

 this is a good way to do it go look at their declarations how do they declare a bunch of variables。

 how do they include stuff from header files how do they declare types and so it basically has a。

 lot of information about structures and stuff in numpy um different types like the complex types。

 and it also declares all these functions here py array data and dra so on and so forth so when。

 you actually do by when you look at the site c code that's generated it's actually you know。

 using these declarations and substituting them there with the appropriate header files so for。

 example if you look at py array and dim so oh sorry。

 let's look for py array and dim so all of this is inside this header file um numpy array object。

 and everything indented one to the right is basically pulled out from there and these are。

 the declarations for that particular header file so that's how it works and so now it basically。

 declares all of these all of these types all of these functions are therefore an array object so。

 numpy is array object dot h which is the c api for numpy all of that is now exposed in python and。

 because you have this installed if you just say c import blah blah blah it pulls that adds these。

 declarations so that sythan knows about those functions and it can call them directly。

 maybe that's too much internal detail so let's get back um all right so now we'll run some。

 experiments we'll try to call this with some data so what we do is we from sypy。stat's import。

 poison which is a which should generate poison distribution uh for us so we now create this with。

 the value 10 i think that's equivalent to lambda 10 i don't know um and then we look at the probability。

 mass function it's a discrete probability distribution um with n is 10 and now we calculate the entropy。

 using each of these functions and they all produce these numbers which is nice so now let's time it。

 and see how well numpy's or sypy's implementation does takes me 1。19 milliseconds per loop。

 however python version takes one point okay what is that that's a lot faster already。

 and this i don't understand because i don't know maybe it's a version of sypy that i have。

 all right okay fine so it shows that our python implementation is actually faster so。

 probably this maybe let's look at what the hell this is doing， okay so it's doing dist。

entropy and i don't know what it's doing that's looking at dist。

 infrastructure so i'm not gonna look closer um all right so um sypy's implementation is really slow。

 it's 1。26 milliseconds and the python version no sython here is 9。88 microseconds and even if i say。

 the slowest took its cache to if i multiply this by 6 that's still um 54 microseconds so it's like。

 20 times faster then i don't know so probably there's a bunch of extra code that um sypy's。

 code is doing that this is just doing np some so it's faster not yes roughly。

 i'm sure that the sypy entropy is probably doing a lot more work it's probably checking types doing。

 a bunch of stuff okay maybe i don't know what sypy's doing yeah and it's hidden and deep in the。

 dist stuff so i'm not going to go and find out what it's doing but that's not the interest here so now。

 the question is let's see what the sython guy is doing and let's see whether it's any faster or。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_145.png)

 it's slower i expect it to be roughly the same which it is so the question is can we make it faster。

 but instead of doing it the the just numpy arrays can we write this out by hand ourselves so the first。

 version that we have is a version that says shannon entropy v1 we declare the type saying c and p and。

 dra and then declare the types as much as we can so okay so this is v1 so let's run this and it looks。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_147.png)

 pretty good except um this guy this guy looks terrible i don't like it and i don't want to look at it。

 um so what do we do and but let's see what we got from this because we've done some optimization。

 and it's now 26。2 but it doesn't say something was cached anymore so um if i may be allowed to。

 multiply 6 into 10 that's 60 maybe it's okay for me to say we got a 2x performance improvement。

 by just declaring some of the outer types maybe all right the best case all right so the first。

 thing that's different in this is this strange little function here from libc。mat in c import log。

 as c log so what is this doing so if i just did from mat import log and call that you have to。

 remember that mat's log is a python function even though mat's log is a python function that。

 internally calls a c function it's still a python function as far as satan's concern and so if you。

 just did that it'll be terribly slow so maybe let's try that i'm gonna do this from mat import log。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_149.png)

 as c log okay and then run this that's 37。8 microseconds so it added another 10 microseconds。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_151.png)

 because it's a python function all right so it's not terrible but it's worse than doing this。

 which is like 29 26。2 all right so that's the first thing that's nice is that there is a libc。mat。

 from where you can pull out all the standard library mat functions and that will just be a。

 direct c call so let's um if you look at this if i can find out where that line is uh。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_153.png)

 looks like i can't yes so if you look at this the actual log function is here。

 and that was actually a nice function it's the rest of the gun actually getting pyxt6。

 that's a pain because i have to do pi float as double so the problem here is。

 because this array was declared as just a numpy array satan does not know underneath what is the。

 type of the values that are inside that numpy array so it can't do any further optimizations so again。

 if it's yellow something is missing and in this case it's missing with the argument to c log。

 so what you now need to do is um you need to first declare the type so the first thing you can do is。

 you can simply say nd array of double and that's the syntax of how you say it's a numpy array having。

 double data types yes two times five minute warning all right。

 ah okay so i'll try and finish as fast as i can， where are we okay so we started here the first thing we introduced was c log which is from libc。

 。math c import again remember c import it is not import because you're basically saying log is a。

 function c function that you should be able to call into so every time you see c log in the code。

 replace it with that math。h function okay and again i invite you to go look in that includes directory。

 how to find it just import satan c capitals look at the file it'll find out the file look inside。

 there look at i in includes you'll see a directory called libc there they will see a math。txt。

 yank that out read it and you'll see all the declarations all right so what's happening here is。

 every time satan sees c log it will actually make a call to that function all right the rest of the。

 issues are with p of x of i p sub x of i how does it know what type that is so to find that。

 it would help if we declare it so the way to do that is to simply add this so that's the only。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_155.png)

 change from the previous code all you say is cnp ndra double and the type of this is px shape of zero。

 all right that's there in the same thing okay and now let's run this and it's a lot it's a lot。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_157.png)

 in this case you can see that it's a lot less yellow so if you look at that。

 notice that it's doing some buffering stuff but， this has to do with how the data is actually stored in that numpy array so you remember that。

 numpy arrays are not just single flat one-dimensional arrays they may be contiguous they may be。

 non-contiguous they may have strides all of that information again we have not supplied。

 but now if you were to run this this should be a lot faster， and it's 1。

6 microsecond so it's about eight times faster all right okay the final thing。

 i think here okay there's memory views is turning off bounds checking so one of the things if you。

 look at this code is it's going to be checking if you're indexing beyond the range of valid values。

 all right so what you can do is you can shut off any bounds checking and make sure you do this only。

 when you know your codes right and it works fine otherwise you'll start getting segfarts。

 your ordinary nice well-behaved python code will suddenly start giving you segfarts and。

 blowing up your python interpreter so beware of doing this but if you do it。

 it looks lovely it's white right because essentially it doesn't have to do all of that。

 additional type checking and this version will probably be even faster， i hope， marginality no。

 it's only marginally faster all right okay so， we have we have one minute so instead of going on and on about this i think。

 i think i should stop here but so what i will do is i will give you a quick overview in one minute。

 of the remaining six notebooks yeah i'll try and do that so so what this goes on to do is so now i。



![](img/b8d9e1d8490d7c84cfc812d37b0318c6_159.png)

 think you have some exposure to using seithon and the general idea so the general idea i think the。

 mentor model you need to have is seithon allows you to sort of mix see and python in a python。

 friendlies syntax so you can start with straight out python code annotated a bit and get some。

 performance but the more performance you need you need to push more stuff down into see。

 and the annotation support that they have is a useful way for you to get from python to see。

 and find out where your stuff is slow the next part of this same notebook introduces a syntax that's。

 more general purpose it says something about something called memory views so instead of saying。

 numpy array you can just say double bracket colon colon and that basically says it is some buffer type。

 which is of double which means it doesn't necessarily even have to be a numpy array it could be just a。

 standard python array data type and it will work all right so the nice thing is it it makes the。

 syntax a little easier and it will generate efficient code so this sort of will introduce。

 you how to use memory views and so you can start writing your code using memory views and the。

 nice thing is if you use the memory views syntax you can pass it in umpire and it will work transparent。

 all right so this is something that you will see in this。

 and if i can find the rest yes there you go。

![](img/b8d9e1d8490d7c84cfc812d37b0318c6_161.png)

 all right the next notebook seven so if you can give me two minutes i will finish this。

 basically takes an exercise looks at a pandas data frame and tries to do some processing with it。

 and the moral of the story is again so don't get fooled into thinking that you're going to generate。

 pandas in sythan no what he does is he takes the pandas problem reduces it to a numpy problem。

 and then uses all of the stuff that you learned to optimize that and get performance from the。

 sythan code all right and you can get significant performance you know then he moves on to extension。

 types which is really important but it again builds on similar syntax that you've seen up to now so。

 it's not completely alien to you it's something reasonably similar to what you've done but now it's。

 talking about extension types which means you can create a class in um where is this。

 so you can create a class so he basically takes up an example of a random number generator creates a。

 class for it does it impure python translates that to sythan and then shows you how you can optimize。

 that code to get good performance and generate a property c code all right so this is really useful。

 because what this lets you do is create sythan python objects which are all implemented in sythan。

 which means you get all of the methods of that object will be implemented in c which gives you。

 like really good performance um and then he goes on to look at a uh pymc mc based example again you。

 don't need to know mcmc he's basically using that as a problem to motivate uh how to do this。

 and then again takes that tries to bring it down from a pure python implementation bring it down。

 to sythan and work through that and actually get performance okay and the last one is uh sythan。

 mcmc taking it to 11 um the idea here is he converts this into a standalone example。

 so the way in which that works is fairly simple you take you create a pyx file with your python。

 your sythan code and then you need to create this setup。

py which is how python's packaging stuff works， and there you need to spell out saying that's the file these are the dependencies or whatever or。

 if it's a simple single sythan file you can just say from sythan import extension or sy， sythan。

distutals import extension instead of using standard distutals extension you just use。

 sythan's extension and then write your setup。py he has a template that you can use and then run。

 python setup。py it will compile your python file your python pyx file into a c file and then into a。

 module all the stuff that your numpy your ipython notebook has been doing it will do explicitly on。

 the background for you and create a module that you can use that you can also ship with your code。

 which means if you're creating a package you can supply this and when they run python setup。

 py install or whatever it will compile it build it install it in the right place and then you can use。

 it just like any other python module so that's the full rundown and I think you should be able to go。

 back and work through all of this and get a reasonable idea of what's going on okay so that's the best。

 we could do in the absence of quit he will be back later this week right we don't know okay。

 so if he is you can ask him all the difficult questions but we will be around and anything that。

 we can help you with we will be happy to explain thank you all， you， [BLANK_AUDIO]。

