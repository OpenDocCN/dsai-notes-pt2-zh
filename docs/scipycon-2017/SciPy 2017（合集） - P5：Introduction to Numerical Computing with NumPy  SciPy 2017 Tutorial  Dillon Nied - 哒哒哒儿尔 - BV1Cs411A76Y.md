# P5：Introduction to Numerical Computing with NumPy  SciPy 2017 Tutorial  Dillon Nied - 哒哒哒儿尔 - BV1Cs411A76Y

 So I'd like to take this moment to wish you all a very good morning。

 So about two of you are also having a good morning， and the rest of you are still sleeping， perhaps。

 That's all right。 We'll wake you up quickly。 My name is Dylan。 I'm your instructor for the morning。

 I work for a company called Enthot。 Also with us in the room today is my esteemed colleague Alex。

 They're in the back corner。 He will be here to help answer your questions。

 especially during the parts of the class， where you'll be working on exercises。

 Now Alex has also been responsible for putting together this whole tutorial session。

 So could I see by a show of hands how many of us have learned something amazing so far？ All right。

 Can we get a round of applause for Alex and the hard work he's done？

 So we're here this morning to talk about NumPy。 And this is going to be a big Indian talk。

 so we're going to put the most significant， parts first。

 The very first thing that I would like to do is pull up the code of conduct for this conference。

 which you'll see at the very memorable endpoint e-home/220975/493434。

 If you haven't looked at this already， I highly recommend that you do so。

 This is something that we take very， very seriously about making this a place that is。

 amenable to productive scientific discourse。 I would like to go a step further than that and say that if at any point during this conference。

 you do not feel as if you are enthusiastically welcomed here。 I would like you to come talk to me。

 If I make you uncomfortable， you can talk to Alex or any one of the conference organizers。

 If bringing this up with someone in person makes you feel uncomfortable。

 You can message one of the conference organizers on Slack to let them know what's happening。

 It says all of the usual things about being kind to people。

 all the things about making sure you are taking other people's perspectives into mind。

 not making careless jokes or careless comments。 I think that is the most important thing。

 The next important thing is before we can talk about NumPy。

 we are going to talk about how we are going to talk about NumPy。

 The general structure for this morning session is going to look like this。

 I will talk for a little bit。 I will alternate between doing some doodling on the whiteboard here and some typing on my computer。

 For the part where you see me entering code， I encourage you very， very strongly to type along。

 One of the things that we know is that the absolute worst possible way for you to learn this content is to hear me talk about it。

 We are going to minimize these parts of the tutorial as much as we possibly can。

 I am going to give you the least possible amount of information to make you successful in working on the exercises that we are going to have you spend time on。

 These exercises themselves will come in two flavors。

 The first will be little practice things that I will put here on the slide。

 It will say create in a right that looks like this， do this thing with it。

 then do this thing with it。 The other exercises are going to be a little more involved。

 They are going to involve， they are going to require that you open up a Python program。

 You are going to make some edits to it and look at the result to achieve some number of steps。

 Some number of goals。 When we get to this part， I will give you a brief introduction to those exercises。

 We will let you fly to work on them on your own。 We will circulate around the room to answer any questions that you might have。

 One more additional piece of information。 It is very important that the coffee disappears at 10。30。

 We will be taking a break sometime before then to make sure you all have a chance to recaffeinate。

 For this class， I am going to be using a canopy。 It is going to give me all the things I need to show you NumPy and none of the things I don't need。

 If you are working in the terminal， that is fine。 If you are working in a notebook， that is fine。

 There will be minor differences in syntax between them。



![](img/9e8acb55f096297e396601a0d7edd911_1.png)

 I will try to highlight those when we get to them。

 One of the chief ones is that during these exercises there are going to be a lot of bonus components。



![](img/9e8acb55f096297e396601a0d7edd911_3.png)

 where you are asked to plot and array that you have created。

 To make the plotting work correctly inside of an interactive session。

 like an IPython terminal we see here， we are going to enter some IPython magic。 Magic， Mat， Plot。

 Live。 If you are in a notebook and not in an IPython session。

 you want to follow this up with the word inline， IN， L-I-N-E like so。 If you are in a notebook。

 you can see the text。 If you are in a notebook， you can see the text。 If you are in a notebook。

 you can see the text。 If you are in a notebook， you can see the text。 If you are in a notebook。

 you can see the text。 If you are in a notebook， you can see the text。

 Please do let me know if there is a word I use that you have not heard before。

 Raise your hand and ask me to define it for you。 If I use a word that you have heard。

 but I am not using it in the way you know it， you should also ask me as well。

 If you feel uncomfortable raising your hand， I see that some of you have the little pink sticky notes from the software。

 Crap or D sessions， you can use those as well。

![](img/9e8acb55f096297e396601a0d7edd911_5.png)

 We are here today to talk about a library called NumPy。

 NumPy is the library inside of the Python ecosystem and it is going to solve a very big problem for us。



![](img/9e8acb55f096297e396601a0d7edd911_7.png)

 We like working in Python。 Python is an amazing language。 It makes it very easy to do common things。

 It makes it possible to do uncommon things。 It is clean to write。 It is easy to read and understand。

 It is relatively easy to debug。 It is safe as a programming language。

 It does all of these amazing things under the hood for us to make sure we are not doing things like corrupting our computer。

 Python has one major weakness。 Python is not particularly good at math。

 The way we are going to get around this weakness is with using the NumPy library。

 The very first thing we are going to do is show you what this looks like。

 What I would like to do is generate two ranges of data。

 One is going to be in a native Python data structure。

 All we are going to do is calculate the sum of that data。

 We are going to do the same thing with a NumPy array。

 We are going to generate a NumPy array of data， find the sum of that。

 What we are going to see is we are going to time how long it takes each of those processes to complete。

 To start with， I can make something like a test list。

 This test list is going to be something that has， we will say， we will just do 1000 integers。

 The range function in Python is built in。 That is going to generate a list of integers from 0 to 999。

 I will notice I have wrapped this in a list coercion。 If you are using Python 3。

 the range function has lazy behavior。 To make sure we get an actual data structure out of this。

 we are going to core-sit into being evaluated eagerly by using our list constructor。

 The next thing we are going to do is create our NumPy array that has the same number of elements in it。

 The first thing we are going to do is import NumPy library。 It is spelled N-U-M-P-Y。

 You will see I have used my alias importing here。 I am importing it as another name。

 This is not a law in the world of Python， but it is a very strong convention。

 When you look at other people's codes， you will almost always see NumPy imported under the name NP。

 This makes it easy following the convention of for you or for anyone else。

 If they are looking at some function inside of a Python module and they see that NP name in there。

 we know immediately what that is。 I have imported my NumPy library。 I am going to use the NumPy。

 the concomitant function to range， which is called a-range。 Once again。

 we are going to make an object that has 1000 elements in it。

 Now what we want to do is take the summation of both of these data structures and we are going to time how long it takes using iPython's magic time。

 In the world of Python， we have a whole suite of nifty functions that start with this percent sign。

 We call these magic functions。 The one that we want to use here is magic time。

 It is spelled T-I-M-E-I-T。 We are going to time how long it takes to call Python's built-in summation function on test list。

 which is a Python native data structure。 Python is going to run this function。

 this expression a whole bunch of times。 It is going to give me its best guess as to how long this takes to execute ignoring all of the other stuff my computer is doing。

 like talking to the projector， running PowerPoint in the background。

 I Python's best guess for how long this takes from my computer。

 It looks like it is about 5 microseconds。 On your computer the timing might be different and that is okay。

 We are going to do the same thing but instead of using the Python function on the Python data structure。

 we are going to use NumPy's function on our NumPy data structure。

 Once again we will have our magic time。 We are going to use np。

sum which is NumPy's summation function and we are going to do this on our test array。

 Just like before， Python is going to run this a whole bunch of times for us。

 It is going to give us its best guess for how long this is going to take。

 For our small data structure that has 1000 elements what we see is that using NumPy makes this code run about twice as fast。

 This difference is going to get larger as we increase the size of our data structures。

 For an array that has a million elements in it， what we are going to see is that using NumPy is going to be 1 to 2 orders of magnitude faster。

 So somewhere between 10 times faster and 100 times faster。

 To give this a little bit of context this is the difference between waiting a second for something to complete and waiting several minutes。

 That is exactly what we are going to talk about。 The question was is the speed。

 performance gain only true for integer arithmetic and the answer is true for any kind of mathematical operation you will be doing。

 NumPy versions are always going to be faster than the Python versions。

 There are two primary reasons for this。 To explain why I am going to start drawing some pictures on the board。

 The first thing we are going to see is we are going to draw out what a list looks like to Python。

 We are going to talk about how we grab items out of that list。

 We are going to draw what a data structure looks like in NumPy and how Python pulls data out of NumPy arrays。

 This is going to involve me walking away from the microphone so I will raise my voice so you can hear me better。



![](img/9e8acb55f096297e396601a0d7edd911_9.png)

 It is not because I am upset by drawing。 If we think about the way that memory looks in our computer in a Python list we are going to have some array。



![](img/9e8acb55f096297e396601a0d7edd911_11.png)

![](img/9e8acb55f096297e396601a0d7edd911_12.png)

 Where that array is dynamically resized and that array consists of pointers。



![](img/9e8acb55f096297e396601a0d7edd911_14.png)

![](img/9e8acb55f096297e396601a0d7edd911_15.png)

 Each one of these pointers you can think of as an address that knows where the objects inside of that array live。



![](img/9e8acb55f096297e396601a0d7edd911_17.png)

![](img/9e8acb55f096297e396601a0d7edd911_18.png)

 This one right here for example might look somewhere else in memory where I have the string doing。



![](img/9e8acb55f096297e396601a0d7edd911_20.png)

![](img/9e8acb55f096297e396601a0d7edd911_21.png)

 This one here might be looking somewhere else in memory that contains another array。



![](img/9e8acb55f096297e396601a0d7edd911_23.png)

![](img/9e8acb55f096297e396601a0d7edd911_24.png)

 Another Python list。 What this means is that when I go to retrieve one item if that item is something like an integer or a floating point number or a string。



![](img/9e8acb55f096297e396601a0d7edd911_26.png)

 Every time I do this I am adding one look up。 I have to go somewhere else in memory to fetch a thing。

 If I have nesting in my data structures I might have two lookups I have to perform and I might have three。

 The time for any one of these individual acts is very small。



![](img/9e8acb55f096297e396601a0d7edd911_28.png)

 We are talking on the scale of dozens of nanoseconds so it is very fast。



![](img/9e8acb55f096297e396601a0d7edd911_30.png)

 If it happens once。 But typically when we are constructing NumPy arrays it is not just because we want to add one and two together。



![](img/9e8acb55f096297e396601a0d7edd911_32.png)

 It is because we have millions of elements that we need to sumate to take the standard deviation of to find out where the maximum value is。



![](img/9e8acb55f096297e396601a0d7edd911_34.png)

 Adding 40 or 60 nanoseconds to each one of those binary operations between elements becomes very large。



![](img/9e8acb55f096297e396601a0d7edd911_36.png)

![](img/9e8acb55f096297e396601a0d7edd911_37.png)

 This isn't just 20 nanoseconds when you are doing it for millions and millions of things。



![](img/9e8acb55f096297e396601a0d7edd911_39.png)

 We are on the scale of seconds now。 Human noticeable slowdowns。



![](img/9e8acb55f096297e396601a0d7edd911_41.png)

 We are using NumPy array instead of having references to references to references。

 What we have in memory is an unresized dense array that actually contains inside of it the data that we are interested in。



![](img/9e8acb55f096297e396601a0d7edd911_43.png)

![](img/9e8acb55f096297e396601a0d7edd911_44.png)

 There is no double lookup。 There is no triple lookup。

 If I want the one I go to where I know the one is and that is where my data is to。



![](img/9e8acb55f096297e396601a0d7edd911_46.png)

 This is one source of our speed improvement。

![](img/9e8acb55f096297e396601a0d7edd911_48.png)

 The bulk of it though comes from the fact that Python is what we call a dynamically typed language。



![](img/9e8acb55f096297e396601a0d7edd911_50.png)

![](img/9e8acb55f096297e396601a0d7edd911_51.png)

 What this means is that we don't have to let the Python interpreter know in advance what kind of data we are giving it。

 Is this going to be a list？ Is it going to be a dictionary？

 Is it an integer or is it a floating point number？



![](img/9e8acb55f096297e396601a0d7edd911_53.png)

 This makes it very nice for us when we are in code in Python because we can get rid of a lot of the boilerplate。



![](img/9e8acb55f096297e396601a0d7edd911_55.png)

 We can write code that is more easily composable， more easily extendable。



![](img/9e8acb55f096297e396601a0d7edd911_57.png)

 The downside is if I have a simple operation in Python where for example。



![](img/9e8acb55f096297e396601a0d7edd911_59.png)

 I want to take the sum of the number zero and the number one。

 There are a lot of intermediate translation and checking steps that occur。



![](img/9e8acb55f096297e396601a0d7edd911_61.png)

 So in Python C's the zero plus one， the first thing it is doing is it is translating that plus operator。

 to a Dunder add method on that integer。

![](img/9e8acb55f096297e396601a0d7edd911_63.png)

 It has a lot of checks。 So for example， does the Dunder add method of an integer here work with whatever is given as an argument to this method call？



![](img/9e8acb55f096297e396601a0d7edd911_65.png)

 I have to check if this number is large enough that I have to put in a different kind of data structure and a larger amount of memory。



![](img/9e8acb55f096297e396601a0d7edd911_67.png)

![](img/9e8acb55f096297e396601a0d7edd911_68.png)

 I have to check if there is an explicit not implemented statement on the left-hand side of this operation。



![](img/9e8acb55f096297e396601a0d7edd911_70.png)

![](img/9e8acb55f096297e396601a0d7edd911_71.png)

 So then I can go and check on the right-hand side。



![](img/9e8acb55f096297e396601a0d7edd911_73.png)

 And again， each one of these error checking steps。

 each one of these layers of misdirection only adds a tiny fraction of time。

 But if you give Python a list of objects， it has no way of knowing if every object in that list is going to be an integer or even if it is going to be a number。



![](img/9e8acb55f096297e396601a0d7edd911_75.png)

![](img/9e8acb55f096297e396601a0d7edd911_76.png)

 So it has to perform all of these checks every single time。 So again， if we do it once。

 it is not a big deal。 If we have to do this a million times。

 this adds substantially to the runtime of our programs。



![](img/9e8acb55f096297e396601a0d7edd911_78.png)

 Now in contrast， when we create arrays in NumPy， arrays of numerical data。

 we tell NumPy in advance these are going to be very specifically 64-bit integers。



![](img/9e8acb55f096297e396601a0d7edd911_80.png)

![](img/9e8acb55f096297e396601a0d7edd911_81.png)

![](img/9e8acb55f096297e396601a0d7edd911_82.png)

 These are going to be 32-bit floating point numbers。 These are going to be 128-bit complex numbers。



![](img/9e8acb55f096297e396601a0d7edd911_84.png)

 So that when NumPy goes to perform our addition， it doesn't have to do these type checks on every single object in this array。



![](img/9e8acb55f096297e396601a0d7edd911_86.png)

 It knows for every single one of these， I am always doing 64-bit integer addition。

 And it is going to perform all of these operations for us at the level of the code written in C。

 not written in pure Python。

![](img/9e8acb55f096297e396601a0d7edd911_88.png)

 So not only are we avoiding all of these type checks。

 we are going to avoid also a lot of the overhead that we get from the Python interpreter itself。



![](img/9e8acb55f096297e396601a0d7edd911_90.png)

 But at some point you must make a check。 You only make it once。 Exactly， you only make it once。

 Let's say you are reading a data file and it has an error or a number。

 It has an string and you try to load it into a NumPy array。 It will give you an error。



![](img/9e8acb55f096297e396601a0d7edd911_92.png)

 So the question was， if I am reading some data in off of disk and it contains something that is not representable as a number。

 do I have to check while I am doing the addition for that？



![](img/9e8acb55f096297e396601a0d7edd911_94.png)

 And the answer is you will see that error at read time。



![](img/9e8acb55f096297e396601a0d7edd911_96.png)

 So if you read a data off of disk and you tell NumPy。

 this is only going to consist of 64-bit floating point numbers。

 And there is some data in there that doesn't fit that format。

 You will see that exception immediately。

![](img/9e8acb55f096297e396601a0d7edd911_98.png)

 So the benefit to using NumPy is we are going to be getting these one to two orders of magnitude performance gain。

 The cost that you are going to have to pay is we are going to move away from all of the nice protections that Python gives us。



![](img/9e8acb55f096297e396601a0d7edd911_100.png)

![](img/9e8acb55f096297e396601a0d7edd911_101.png)

 And what that means is that the numbers in NumPy are going to behave a little bit differently than the numbers that we are used to seeing inside of Python。



![](img/9e8acb55f096297e396601a0d7edd911_103.png)

![](img/9e8acb55f096297e396601a0d7edd911_104.png)

 We are also going to see that while the data structure itself supports many of the same methods we are used to using in Python lists。

 there are some restrictions to how we can use those。



![](img/9e8acb55f096297e396601a0d7edd911_106.png)

 So on array looks a lot like a list， but there are some very important differences。



![](img/9e8acb55f096297e396601a0d7edd911_108.png)

 In terms of the data structure itself， a Python list is allowed to be。



![](img/9e8acb55f096297e396601a0d7edd911_110.png)

![](img/9e8acb55f096297e396601a0d7edd911_111.png)

![](img/9e8acb55f096297e396601a0d7edd911_112.png)

 heterogeneous， by which I mean it contains data of different types。



![](img/9e8acb55f096297e396601a0d7edd911_114.png)

![](img/9e8acb55f096297e396601a0d7edd911_115.png)

 A Python list is also allowed to be resized。 So one of the principal uses of a list inside of Python is to accumulate data inside of a loop。



![](img/9e8acb55f096297e396601a0d7edd911_117.png)

![](img/9e8acb55f096297e396601a0d7edd911_118.png)

![](img/9e8acb55f096297e396601a0d7edd911_119.png)

 So when you are generating data one by one， you append it onto the end of that list。



![](img/9e8acb55f096297e396601a0d7edd911_121.png)

 Our NumPy arrays in contrast are required to be homogeneous in their data types。



![](img/9e8acb55f096297e396601a0d7edd911_123.png)

![](img/9e8acb55f096297e396601a0d7edd911_124.png)

![](img/9e8acb55f096297e396601a0d7edd911_125.png)

 So if I have a two dimensional array that I am trying to use as some sort of a tabular data structure。

 I am required that every individual item inside of that table has the same data type。



![](img/9e8acb55f096297e396601a0d7edd911_127.png)

 They can all be integers， they can all be floating point numbers， they can all be strings if I want。

 but they cannot be any mix of those things。 The other principal difference is that a NumPy array is a fixed size。



![](img/9e8acb55f096297e396601a0d7edd911_129.png)

![](img/9e8acb55f096297e396601a0d7edd911_130.png)

 Now this is 99% sure you can change the size of a NumPy array。

 but this is a very expensive operation。

![](img/9e8acb55f096297e396601a0d7edd911_132.png)

![](img/9e8acb55f096297e396601a0d7edd911_133.png)

 I am sorry， the Python list is a type of type of type of type of type。 It is a homo array。



![](img/9e8acb55f096297e396601a0d7edd911_135.png)

 I am missing the second word， does A， the Python has this homo array。

 There is any array module in Python。

![](img/9e8acb55f096297e396601a0d7edd911_137.png)

 You can import and use the array data structure。 That is not the same thing as a NumPy array。



![](img/9e8acb55f096297e396601a0d7edd911_139.png)

![](img/9e8acb55f096297e396601a0d7edd911_140.png)

![](img/9e8acb55f096297e396601a0d7edd911_141.png)

 We have seen here that the data structure itself is going to be different in some key ways。

 The data inside the data structure are also going to change。 To show you what this looks like。

 we are going to have to create a handful of NumPy arrays so we can see in real time how they are working differently。

 The very first thing that I would like to do is create an array。

 We are going to make an array of integers。 We are going to use the constructor function for arrays inside of NumPy to do this。

 We will give it a very bland and boring name like the letter A。 Here is my name。

 I have my assignment operator。 Yes？ Oh， of course。 Mm-hmm。 I have my name A。

 I have my assignment operator。 On the right-hand side， we are going to ask for a NumPy array。 So NP。

A array with an open and a closed parenthesis。 In cli the open and closed parenthesis。

 I am going to initialize my array with some data。 Here we will have the integers -1， 0， 1 and 100。

 We are going to add one more thing。 I will explain later what this is doing。

 We are going to use the optional argument DType to specify the data type we would like this array to have。

 The DType is going to be INT8。 This is a string literal that tells NumPy I want an 8-bit integer。

 I can enter to execute this line of code and then here is my NumPy array。

 My first question for you is when we are working with numbers in Python and base Python。

 what happens when I try to divide a number by zero？ That is exactly right。

 I get a zero division error。 If I say I want to divide one by zero。

 here is Python telling me this is something that is warning me against。

 This is probably not what I meant to do， so it is going to raise an exception as a way of letting me know。

 We are going to do the same thing where we divide a number by zero。

 but we are going to divide the data inside of our NumPy array A。

 The name A and then divided by and then A0， do I see a zero division error？ I do get a warning， yes。

 There is no exception that gets raised。 The result of this is a valid data structure。

 It is a NumPy array that is filled with zeros。 Yes？ You get infinities。

 I would bet that what you have done is you have created an array of floating point numbers instead of an array of integers。

 So good instincts。 Now we are going there next。 The reason for this is that when we are living inside of NumPy。

 we are no longer dealing with Python data types。 These are not Python integers。

 These are the kinds of integers you have access to if you are writing this code yourself in C。

 They behave according to the IEEE specifications for how numbers should behave and not according to Python's ideas of not surprising you。

 You might find this to be a surprising result that a number divided by zero is zero。

 The Dart Cabal that controls numbers has decided this is how this works。 Yes。

 There is one more thing that we are going to do。 If I ask you a question。

 like how do I take the square of a number in Python， what would you tell me？ Yeah。

 I can multiply it by itself。 That is one option。 Or I can use my double splat operator to ask Python to square the number。

 So here what we are doing is we have the Python integer 100 and we are squaring it。

 And we get the result 10，000 which is not surprising to us。 This is what we expect。

 And I can take this to any power。 And this integer will get larger and larger and larger。

 Up to some point， and I will scroll up again。 Up to some point where we see this little L at the end of the number。

 If you are on Python 3， this is a lighted。 So you won't see the L anymore。

 But this is Python's way of letting us know that this integer is now too large to fit into the size that is default on our system。

 So for most of you it will be 64 bits。 But in Python we are allowed to have integers that are arbitrarily large。

 So as our integers get bigger， Python will allocate more and more memory to holding those values。

 So we don't have to worry about things like numbers doing weird tricks。

 Antigures surprisingly becoming negative。 And NumPy we are not protected from this。

 So if I take that array A and I square it， we see that -1 squared is 1 which is what I expect。

 0 squared is 0。 This is also what I expect。 1 squared is 1 or still feeling good。

 And 100 squared is 16。 Right？ We remember this from our multiplication tables 100 times 100 is 16。

 So what's happened here is I have told NumPy when I created this array。

 that I only wanted to give 1 by 8 bits to each one of these integers。 And the number 10。

000 cannot be represented inside of 8 bits。 So when we hit the maximum extent of that number。

 we started back at the negative end and counted up。 Which here is 16。

 If you would like to Google this later， the technical name for what we've just witnessed is called integer overflow。

 So we are also not protected from this。 Let's try something else a little different。

 So we've been dealing with integers。 But NumPy also supports floating point numbers。

 So numbers like 4。5。 They cannot be represented as these infinite precision integers。

 And what we're going to do is we're going to make ourselves an array of floating point numbers。

 by coercing our integer array into a floating point array。 We can give it the name B。

 And we're going to say that I want my array B to be that array A。

 And we're going to coerce it with a method called as type。 A。ASTYPE。

 And here we will make you a 32-bit floating point number。

 And I'm going to do this by supplying the string literal float32 FLOAT32。

 So here is my floating point array B。 And you'll notice that there are little periods after each number to let me know that I'm now dealing with floats。

 And we take this array B and we do what we did to the integers。 We divide them by zero。

 We're going to see something even more different。 So we are still not getting a zero division error。

 But this time instead of ending up with an array of zeros。

 we have an array that has two infs that stands for infinity。

 One negative inf that's negative infinity。 And this thing here in the middle that's letters N A N。

 Now this stands for not a number。 And you can think about it as roughly corresponding to the meaning of something that is undefined。

 It is impossible for me to tell you what the result of a zero divided by zero is so I'm not going to try。

 And you'll see inside of the scientific libraries in the world of Python。

 this special object N A N is often used to present missingness inside of your data。

 So if I'm receiving some array where I don't have valid data for some of the values。

 those values will be coded as NANs as not a number。 Not a number has a peculiar law around it。

 If we look at the NAN object which we can access from inside the NumPy namespace N P dot N。

 And we ask Python is N P dot N an equivalent to so using the double equal sign operator itself。

 Python tells us that this is not true。 Now the logic behind this is that something is undefined if it's impossible to know what it is。

 There's no way to tell whether or not it's the same thing as some other thing。

 So a quality comparisons against N P dot NAN always always return false。

 One of the consequences of this is that if you are used to working in a library where it's capable of filtering out missing data。

 selecting all the locations where the data is equivalent to missingness or N P dot N。

 This will not work for you in NumPy。 This will not work for you in the scientific Python ecosystem。

 In practice every library that you'll use has its own built-in helper function for finding NAN values。

 In the world of NumPy this is called isNAN。 So we can ask Python is N P dot NAN a NAN and this does return true。

 And this does return true。 So this is the output in A to the type。

 Can you assign a value of a NumPy array to that output？

 Are the infinite NANs and the other infinite Ns the same type？

 So the question was in the output of 18 are those infinites and NANs the same type of data and the answer is yes。

 So that in NumPy we are required that the data we put inside of an array be homogeneous。

 So that encoding of infinity both positive and negative in the encoding of NAN are themselves defined in the specification。

 for how you encode floating point numbers using only zeros and ones。

 And now because of this you can never have an array of integers that has a NAN value inside of it。

 Because NAN is specifically defined in the standard for floating point numbers and not in the standard for integers。

 Yeah of course good question。 So we get amazing performance gains when we use NumPy for our numerical work inside of Python。

 The cost is that we have to start thinking hard about numbers。

 about the binary representation of numbers， in the way those numbers interact with each other。

 At this point I would like to pause now that we have given you the scary doomsday you have to think about C data types。

 I would ask if there are any questions。 Seeing none of the strategy we are going to take to talk about NumPy arrays is the first thing we are going to think about is our access pattern。

 So how are we putting data into those arrays， how are we getting data back out。

 Then we are going to spend some time thinking about how we perform operations on those arrays。

 We are going to separate this into what we will call mathematical operations and reducing operations and we will explain what that differences later。

 After we talk about how to do useful things we will go back into thinking about the actual structure of these arrays for really nice tricks that we can do with them。

 So we have seen that one of the easy ways to create arrays inside of NumPy is to use that array constructor。

 We have also seen that we can use a range to generate a sequence of integers in the same way that we can use a range in the world of Python。

 There are a number of other sort of convenience functions inside of the NumPy namespace for generating very common kinds of arrays。

 So for example I might want to generate an array that is only zeros and there is a function that does this called zeros。

 I might want to generate an array of ones and there is a function that does this called np。ones。

 And I might want to generate an array that is filled with nothing and I can do this with a function called np。

empty。 Now if you ever use np。empty and we will later today in this class each of these constructor functions is going to take the size of the thing that I would like to create。

 So for example I can ask for two by two array and you will see that it is not quite empty。

 It is filled with a bunch of what is essentially gunk。

 So this is whatever was left over in that memory address before it became my NumPy array。

 First image is to zero。 Close， yeah。 But for us right now let's keep working with that array A。

 And the first thing that we are going to talk about is given that I have an array。

 How do I retrieve data back out of that array？ Now for those of us who are familiar with working with lists inside the world of Python arrays are going to work very similarly。

 So they are going to support the get item behavior and they are also going to support the slicing behavior。

 There is going to be one key difference that will get two in a minute。

 So if you are used to grabbing individual items add them an array using the square bracket syntax。

 So I have a list using the square bracket syntax。 This also works on array。

 Just like lists in Python arrays are zero indexed。

 So if I want the first item inside of my array if I want that negative one I ask for the item in the zero with position。

 Now you will notice what is being returned to me here is the scalar value -1。

 I am not being returned a NumPy array。 So just like in Python when I use my get item syntax I also destroy that data structure。

 So I am not receiving the -1 inside of a thing。 I am just receiving the -1。

 Just like in Python I am allowed to use integers to count forward across the items in an array。

 I can also use negative integers to count backwards from the end of an array to the beginning。

 So if I want the last item inside of an array which is a very common operation to perform I ask for the value in the -1/th position。

 And here is that 100 that we put at the end of our array。

 So in the same way the NumPy is going to support the get items syntax from Python。

 It also supports the slicing syntax from Python。 So if I want to grab the first two items out of my array I can ask for that array A have my open and my closed square bracket。

 And I can slice from the zero with position up to but not including the two-th position。

 So just like in the world of Python my slicing bounds are always inclusive at the lower end and always exclusive at the upper end。

 And just like in Python when I use slicing the objects that are returned back to me are in the same kind of data structure that I originally contained them。

 So I'm not getting a list of the numbers -1 and 0。

 I'm not getting it to pull up the numbers -1 and 0。

 I'm receiving a NumPy array of length 2 with the data -1 and 0 in it。

 Just like in the world of Python if I am slicing all the way from the beginning of a list I can align that first number。

 And just like in Python I'm allowed to specify a step size for my slicing operations。

 So if I want to slice from the beginning of a list -sorry from the beginning of an array all the way to the end of an array and only grab every other item。

 I can use the syntax inside the square brackets colon colon 2。

 Just like in the world of Python I can take one of these get item calls。

 So asking for the -1 item and I can put it on the left hand side of an assignment operator。

 And now instead of retrieving the data from that location it's permitted to insert data into that location。

 So instead of getting that item I am setting an item in that place。

 So let's say that we want to replace that value of 100 with something like 5。

 We can insert the integer 5 into that last position。

 And when I look at my array A that 100 is gone and the 5 is there instead。

 So this tells us that NumPy arrays even though they are a fixed size are mutable they are changeable。

 I'm allowed to swap in data into my NumPy array。 Now the next thing that I would like to do is I would like to make a two-dimensional NumPy array。

 Now I could write out my nested lists inside of lists and use that inside of my array constructor to generate this data structure。

 What we are going to do is we are going to use a shorthand method that is going to involve less typing for everyone and less chance of making a typo。

 We are going to make an array we will overwrite the B array with a two-dimensional array。

 We are going to create first by calling A range so np。a range。 np。

a range is going to give us a one-dimensional NumPy array of sequential integers。

 We will have the integers from 0 to 11。 So I give the number 12 into my A range call。

 Now because np。a range is returning a NumPy array。

 I can treat it as if it is already a NumPy array and immediately call a method of array objects where that method is called a reshape。

 And I'm going to reshape this one-dimensional array into a two-dimensional array whose shape is 4 by 3。

 And we will scroll you up。 Now when we have two-dimensional arrays it is going to be very very tempting to refer to rows and columns inside of that array。

 Especially if you are someone who is coming from a language like R or a language like MATLAB。

 I'm going to try very hard not to use either of those words that mental model will not help you in NumPy。

 The reason is that in NumPy we are allowed to have any dimension of arrays。

 So we can have a three-dimensional array， a four-dimensional array， a 12-dimensional array。

 And inside of multiple dimensions the concept of a row or a column is not going to make much sense。

 So for example if I have a one-dimensional array in NumPy it is not the same thing as a column vector。

 It is not going to be a four-by-one array， it is just an array of length four。

 And this is going to be important when we talk about performing operations between arrays later。

 So when I create an array of shape four by three， what we see is that four is in the direction going up and down on my screen。

 the dimension of length three is going left to right。

 And this is verbally awkward but this is how I will try to refer to these things。

 the dimension of length four and the dimension of length three。

 So if I have a list that is nested in Python， I have to change together my square brackets to select first from the outermost container。

 and then from successive inner containers。 In the world of NumPy I am allowed to specify that information all in one go。

 and the syntax is going to look very similar to the syntax we used before。

 With the exception that they are all going to be in one set of square brackets with each get item call。

 and/or each slicing call separated by commas。 The order of the individual get items and set items is going to match the order of the shape tuple we use to create this data structure。

 So the first call we provide to either get item or slice is going to be in the dimension of length four。

 and the second one is going to be the dimension of length three。

 If you are ever working with an array and you have forgotten what shape it is or what order the numbers come in。

 you can always check the shape attribute of an array。 We don't want A， we want B。

 So here is my array B。 Its shape is a four by three array。

 So if I want to get some data out of this array， maybe I would like to retrieve just the number eight。

 I have the name of my object B， followed by my open and my closed square brackets。

 I am going to use my get item syntax so I am supplying single integers。

 And we are going to count in each dimension where the data point we want is。

 So in the dimension of length four， that eight is in the zeroeth， oneeth， twoeth location。

 So I have a two followed by a comma。 And in the dimension of length three， it is in the zeroeth。

 oneeth， oh， twoeth in that way as well。 So I can ask for my array B at location two comma two。

 And there is the value that I wanted the eight。 I can also supply slicing calls in two dimensions。

 So integers that include at least one colon。 Yes。 Can you also do like the double brackets。

 like two in a bracket instead of brackets and then another two instead of brackets instead of a comma？

 Yes we can。 This will be better for a reason that we won't understand for like another hour or two。

 So we can also slice in two dimensions。 If for example。

 I want the first two items in both the dimension of length four and also the dimension of length three。

 I can change my two comma two to a colon two comma colon two。 And I will scroll up a little bit。

 And here are the first two locations in each one of those dimensions。

 When I was using that get item syntax in two dimensions。

 I was reduced down to a single scalar value。 So there was no containing data structure around me。

 When I am slicing in two dimensions， I maintain each one of those dimensions in my NumPy array。

 Now I can also mix and match， get item calls and slicing calls inside of these square brackets。

 So for example， I might decide that out of my array B in the dimension of length four。

 what I would like are the middle two locations。 Sorry that will be one colon three。

 Putting the dimension of length three， so when going from left to right， I only want the last one。

 So I use my negative one because I don't want to have to count upwards in my head。

 And we see that what gets returned to us is still a NumPy array but it is a one dimensional NumPy array。

 So in the world of NumPy， in my multidimensional arrays， any time I use my get item syntax。

 I collapse one of those dimensions。 So what do you think I would do？ What is a solution？

 If I wanted to retrieve just the five in the eight。

 but I would like my results still to be a two dimensional data structure。

 a two dimensional NumPy array。 So I could use reshape， that's true。

 In this particular instance though， it's possible for me to do this in the call already。

 So I'm going to add one character to line 42 and it's going to return to us a two dimensional NumPy array with the same data。

 Yes？ Do you use a colon to make that slicing in it？ That's exactly right。 So I can append a colon。

 So this is no longer getting the item out and collapsing that dimension。

 It is slicing the item out and maintaining that dimension， preserving it。

 And here is my two dimensional NumPy array with the five in the eight。 [pause]。

 You're saying when you don't have the colon， you don't have colon。 You're collapsing the right。

 is that the word you use？ Or you don't maintain its dimensionality？ That's exactly right。

 So the question was， is what I'm saying is what I'm saying。 That whenever I have a get item call。

 so one of these integers that does not include any colon at all。

 is it always true that I'm collapsing one of those dimensions and the answer is yes？

 So how does it know where to move？ For example， before you use minus one， it's called the last。

 But let's say you use minus two。 So how does it know if it moves in the iso-js or in these short dimensions or the long dimensions？

 If I'm understanding your question correctly， you're asking me how does NumPy know whether this negative one here is applying to the dimension of length four or the dimension of length three？

 And the answer is that it knows by its position inside the square brackets。

 So I have two slicing calls now separated by a comma。

 And what we can do is we can look at that shape attribute of B to see that the very first thing I supplied to that slicing call。

 everything before the comma corresponds to the dimension of length four。

 because it's in the zero with position they both are。 Whereas the second slicing call。

 because it's in the one-th position， corresponds to the one-th position of my shape tuple。

 [ Inaudible ]， The question was in line 42 if I use minus one at the end， will I get the eight？ No。

 So if I use negative two， I'm going to be stepping two things backwards。

 And maybe it'll help if we look at B again。 So instead of slicing out the five in the eight here and the last position。

 I'm in the second last position slicing out the four in the seven。 [ Inaudible ]。



![](img/9e8acb55f096297e396601a0d7edd911_143.png)

 So the question was what is the difference between a shape tuple that looks like this？

 Two comma one and a shape tuple that looks like this。 And the difference is that this tuple。

 the shape tuple corresponds to a one-dimensional data structure。

 Now because of the way the Python syntax works， I can't just have a two inside of parentheses。

 This is just a two with grouping parentheses around it。

 So the definition of the syntax for creating a tuple does not actually require the parentheses。

 but it requires the comma。 So a two followed by a comma is a tuple of length one that only has the two in it。

 So are you a MATLAB user？ So if you're used to thinking about things in terms of column vectors and row vectors。

 the two comma one would be the column vector。 But in this case。

 it's still a two-dimensional data structure。 So the next thing we're going to do is take this into。

 we're going to answer a question。 Yes？ [ Inaudible ]， That's a terrific question。

 So the question was， if I have my array B， how do I get out just the first item instead of the last item？

 So what magic mix of integers and columns am I going to use to retrieve that data？

 So I will have my array B。 And what I can do is in each direction。

 I can slice from the very beginning up to， but not including the item in the one-th position。

 So here is my two-dimensional array that only has that very first value in it at zero。 Yes？

 [ Inaudible ]， Sure。 So the question was， I often receive data and I have no idea what's in it。

 How do I find out how many columns and rows it has？

 The answer is that you can use that shaped tuple。 So if you have not set this explicitly yourself。

 it's still a thing that exists。 It's still an attribute that is defined on all NumPy arrays。

 And only if you're dealing with two-dimensional data。

 only if you're unwilling to let go of the ideas of rows and columns。

 you can think about the first item as being a rows and the second item being the number of columns。

 But the very next thing we're going to do is turn this into a three-dimensional NumPy array。

 where the idea of columns and rows maybe won't be so helpful。 Yes？ [ Inaudible ]。

 So the question was， if I am trying to read in data from the CSV。

 is there a way to do that into a NumPy array？ The answer is yes。

 I'm not sure that we explicitly talk about it during the class。

 but you will use it in the exercises。 So in NumPy。

 there is a load TXT function that will read data off of disk， and turn it into a NumPy array。

 It's going to require that you specify some kind of file location。 You should also， just to be safe。

 specify the data type you're reading in。 But in addition。

 if I look at the documentation for the load TXT function。

 there's going to be an optional parameter called skip rows， which is right here。

 So if I know that I have one line in my file that's serving as those headers。

 I can skip that row entirely by setting skip rows to be one。 [ Inaudible ]。

 So the next thing that we're going to do is we're going to make a three-dimensional NumPy array。

 and we're going to extract some data out of that。 So we'll call this one C。 And just like before。

 it's going to be the result of using the A range function。

 to generate a range of sequential integers。 This time， you're going to ask for 24 integers。

 And the reason is that we're going to reshape this into a three-dimensional NumPy array。

 whose shape is 2 by 3 by 4。 [ Inaudible ]。

![](img/9e8acb55f096297e396601a0d7edd911_145.png)

 And if I look at my array C。

![](img/9e8acb55f096297e396601a0d7edd911_147.png)

 [ Inaudible ]， We see that the dimension of length 4 on my screen is left to right。



![](img/9e8acb55f096297e396601a0d7edd911_149.png)

 The dimension of length 2 is corresponding to in the zeroth position this entire two-dimensional array。

 And in the one-th position this entire two-dimensional array。

 That 3 in the middle is corresponding in the zeroth position to both the line 0， 1， 2， 3。

 and the line 12， 13， 14， 15。 So because screens are two-dimensional。

 these are displayed linearly one above the other。 But mentally you can think about them being stacked like this。

 So now you and I together are going to grab some data out of this three-dimensional array。

 Now let's say that we want to extract just the number 17。

 So I want to end up with that scalar value。 I don't want it inside of any kind of a data structure。

 And this tells you that I'm going to see me supplying what kind of calls。 Exactly right。

 I'll be supplying three get item calls， one get item four each dimension of my numpy array。

 So we'll have my array C。 We'll start out with our open and our closed square bracket。

 And the first thing I'm going to ask is the number 17 in the zeroth position in the dimension of length 2。

 or is it in the one-th position in the dimension of length 2？ One， exactly right。

 So I'll have one followed by a comma。 The next place I'm going to look is in the dimension of length 3。

 And is the 17 in the zero-th， the one-th， or the two-th position in the dimension of length 3。

 Another one。 And now finally we have to look in the dimension of length 4。

 So is that 17 in the zero-th， the one-th， the two-th。

 or the three-th location in the dimension of length 4？ One。 There is my 17。

 Let's try something a little trickier。 Now let's say that what I would like to have is this entire two-dimensional array up here。

 So I would like to end up with a two-dimensional array of shape 3 by 4。

 containing the values 0 through 11。 Since I'm starting off with a three-dimensional array。

 this tells you that I will have exactly one get item call。

 and two slicing calls inside of my square brackets。

 So here is my C with my open and close square brackets。 And the question is。

 what is the first thing I put in？ Is it a get item or is it a slice？

 It is a get item that is exactly correct。 And the reason is I want to collapse that dimension of length 2。

 So this will just be an integer followed by a comma。 My next question is， what is that integer？ 0。

 exactly right。 Now the next two things I'm going to put in， I know are going to be slicing calls。

 And what I'm going to use is I'm going to use the shorthand syntax to tell Python that I want to slice all the way from the beginning。

 all the way until the end。 So I can have just bare colons separated by commas。

 And here is my two-dimensional array of shape 3 by 4。 We'll do one more。

 one more of these on our three-dimensional array。 So my last question here is。

 what can I do if I want to extract a one-dimensional lump-i array containing the data from position 12。

 Sorry， I'm from the value 12 to the value 15。 And just like before， we'll start by asking。

 if I'm ending up with a one-dimensional array and we're starting with a two-dimensional array。

 how many get item calls am I going to have？ It's exactly right。

 I'm going to have two get item calls because I'm collapsing two dimensions。

 The dimension I'm going to be left with is the dimension of length 4。

 And what this tells me is that my get item calls are going to be supplied to the first two dimensions。

 The dimension of length 2 and the dimension of length 3。 So I have my name C。

 I have my open and my closed square bracket。 I know that the very last thing I supply is going to be the slicing operator。

 And now the question is， what are the first two things I put？

 So in the dimension of length 2 is the 12， 13， 14， 15 in the 0th or the 1th position。

 It's in the 1th position exactly right。 And in the dimension of length 3 is in the 0th。

 the 1th or the 2th position。 0。 Very good。 So here is that one-dimensional lump-i array with the 12。

 the 13， the 14， and the 15。 Yes？ Can you do it without the colon， the slicing colon， and get the 15？

 So I'm expected to supply a number of operators equal to the number of dimensions that I have。

 Is there any way we can get it from 8 to 15？ Is there any way that I can get from 8 to 15？ Yes。

 First one， 0 to 1， 0。 So the second one， 12 to 15 is first。

 So the answer is we're not going to be able to do it only using what we learned so far。

 I think what I would do in this case is I would reshape it and then grab the data out that way。

 Do you have other questions？ How would you go about reshaping it just in the single dimension array so that all the numbers follow each other？

 That's a good question。 The easiest way is going to be using something like flatten or rattle。

 Sorry， the question was， is there a way to take my three-dimensional lump-i array and to make it a one-dimensional array？

 Is there an easy way to do this？ The answer is that we have two ways of doing this。

 One is called flatten。 One is called rattle。 These are both methods defined on lump-i arrays。

 So if I have flattened this array first， it's going to be very easy to extract。

 Was it the 8 through the 15？ Yes。 But seeing no further questions。

 we're going to move into our first exercise of the day。



![](img/9e8acb55f096297e396601a0d7edd911_151.png)

 This will be a slide-based exercise and we're going to have you practice retrieving values from a two-dimensional lump-i array。

 So I'm not going to make you work in three dimensions， at least not yet。

 The very first thing you'll do is you'll create this array。

 again by using that A-range function followed by reshaping it into a five-dimensional array。

 And you're going to perform three separate data extractions。 First。

 this is probably the easiest one。 I would like you to extract the data that is outwind in yellow。

 The next thing that I would like you to do is to extract the data filled in with。

 I guess that's a red color。 And the very last thing， and this will be the trickiest。

 is to extract those four values， the five， the seven， and the other。 And then you use the five。

 the seven， the 15， and the 17 that are outlined in blue。 Yes？

 Since these are the same length both ways， how do you know which dimensions which？

 That's a good question。

![](img/9e8acb55f096297e396601a0d7edd911_153.png)

 So in this case you would have to know that the direction going up and down is in the zeroth position in the shape tuple。

 So we have proposedly been creating arrays that are not the same length in each dimension for this reason。

 So we've all been working on this exercise where we have a two-dimensional non-pider array。



![](img/9e8acb55f096297e396601a0d7edd911_155.png)

 and we have three ranges of data that we would like to get out of it。



![](img/9e8acb55f096297e396601a0d7edd911_157.png)

 This thing at the bottom here that's outlined in yellow。

 these two things in the middle here that are filled in with red。

 and then these four data points that are outlined in blue。 So we'll start with that first one。

 which is the 20， the 21， the 22， the 23， and the 24。

 And I would like you to tell me what combination of slicing and get item calls can I use to retrieve this range of data？

 There's a little outer， please。 Excellent。 So in the direction going from the top to the bottom here。

 I want the item in the 4th position， so we're counting from zero， one， two， three， four。

 If I don't feel like counting all the way down from four， I can also ask for the negative 1th。

 the last item in this little area。 And the last item in this location。

 In the direction going from left to right， I want all of these data。

 so I can supply that single colon to say I want to slice all the way from the beginning。

 all the way up until the end。 So our next task was to grab two ranges of data。

 sort of in the middle。 One was this 1， 6， 11， 16， and 21， and the other was the 3， 8， 13， 18。

 and 23。 So what combination of get item and or slicing calls can I use to retrieve these values？

 So what we would like in the direction going from top to bottom is every single piece of data。

 So once again we'll use that bare colon。 In the direction going from left to right， though。

 we don't want to retrieve all the data。 We just want two of those individual items。

 We don't want anything in the 0th position。 We do want the data in the 1th position。

 so I specify the 1， but now we have something a little tricky。

 Because I don't want the data in the 2th position， but I do want the data in the 3th position。

 So the way that I can get around this is I can specify a step size where I say I would like to skip every other item。

 So I can skip the 2 and also the 4 and only retrieve the 1 and the 3。

 We're going to use the same step size trick for the last example， which is retrieving the 5， the 7。

 the 15， and the 17。 So what can I type a combination of get item and slicing calls do I need to retrieve these values？

 [inaudible]， Excellent。 So in the direction going from the top of my screen to the bottom。

 we don't want anything in the 0th position， so we can start slicing from the 1th location。

 And by stepping with a size of 2， we skip the 10， 11， 12 and go right to the 15， 16， 17。

 In the direction moving from left to right， we again want to skip every other thing。

 So we're starting with the 0th data， so we do want the 5 and the 15。

 So we start at the beginning and we do want to grab every other item because we want that 7。

 But here we're in a little bit of a bind because we also do not want the 9 and the 19。

 which is what I would get if I just used colon colon 2 for the second slicing call。

 So what I can do is I can ask Python to slice up to the 0， 1， 2， 3th position。

 but not include the items in the 3th position。 So we are stopping our every other stepping at this point。

 Do we have questions about this exercise？ So the reason that we start off retrieving data out of NumPy arrays using this combination of get item and slicing calls is that it is extraordinarily fast and efficient。

 In the reason is that unlike lists in Python， where I have nested data structures。

 the data from my NumPy array is all contained in one location。 We'll look at how this works later。

 but given a combination that strictly consists of get item and slicing calls。

 what I have is essentially random access to all of those data。 And by random。

 what I mean is it's the same random and ram for random access memory as I calculate locations by performing one or two multiplication in addition steps。

 And I can go directly to where my data are and I don't have to do any de-referencing or any searching。

 So I can look up all of the data using these two items specifically just by a little bit of math。

 So this happens in constant time。 So very fast and independent of the size of my array。 However。

 it's relatively inflexible。 So there are some ranges of data that I cannot retrieve。

 even if I have reshaping in the middle， strictly using combinations of slices and get items。

 So for that we have a second way of retrieving data from NumPy arrays。

 And the second way is going to be using something that for I don't know what reason is called fancy indexing。

 There are two kinds of fancy indexing。 One where we are allowed to specify non sequential integer locations of our data。

 And the second where we are actually going to apply masks。

 And we'll talk about each of these in turn。 So the first thing that I would like to do is regenerate our array A。

 So we can start thinking about this in one dimension first。 So here is my array A。

 one dimensional blank four。 Now if I want the very first item， the very last item。

 I could actually use a placing call for this。 But what I can do instead is inside of my square brackets actually pass in a list of index locations for each of these。

 So I can retrieve the data in the 0th location and in the 1th location。 Or the 0th。

 the 1th and the 3th。 Now the same practice applies to two dimensional data structures。

 So if we look at my array B， this was my 4 by 3 array。



![](img/9e8acb55f096297e396601a0d7edd911_159.png)

 I can use my square brackets for retrieving data。 But in this case instead of passing in one list of individual integer locations。

 I'm required to pass into one for each dimension。

![](img/9e8acb55f096297e396601a0d7edd911_161.png)

 So we'll have the list for the direction going from top to bottom and the list for the direction going from left to right。

 And the way that this is going to work is that inside of each list， I'm going to be specifying。

 sorry， across the two lists， I'm going to be specifying pairs that represent each position。

 each item I want in this direction， and simultaneously in this direction。 So for example。

 if one of the data points I want is the 2， this is in the 0th direction in the dimension of length 4。

 And in the 2th location in the dimension of length 3。 If I would also like the 6th。

 this is in the 2th location in the dimension of length 4。 And the 6th is in the 0th dimension。

 sorry， in the 0th location in the dimension of length 3。

 And here is my resulting array with the 2 and the 6th。 Now this also applies in 3 dimensions。

 where I will have 3 lists for my integers。 And the location for each individual data point is going to be separated。

 you can think about it as being the x， the y， and the z coordinate across these 3 lists。



![](img/9e8acb55f096297e396601a0d7edd911_163.png)

 So we can look at my array C。

![](img/9e8acb55f096297e396601a0d7edd911_165.png)

 This here is my 2 by 3 by 4 array。 And from my array C， I can give 3 sequential lists of integers。

 where let's say I want the 6 and the 17。 So the 6 is in the 0th location in the dimension of length 2。

 The 1th location in the dimension of length 3。 And the 2th location in the dimension of length 4。

 To get the 17， we go back to that first list and add in that it is in the 1th location in the dimension of length 2。

 It is also in the 1th location in the dimension of length 3。

 And finally it is also in the 1th dimension， sorry 1th location in the dimension of length 4。

 And here is my resulting array of a 6 and a 17。 Are we having fun？



![](img/9e8acb55f096297e396601a0d7edd911_167.png)

 So this is very tedious to do by hand。 Typically you will not be typing in the numbers yourself。

 counting in each dimension like this。

![](img/9e8acb55f096297e396601a0d7edd911_169.png)

 But you will see this is the output of some of NumPy's built-in functions。

 So if you ask for example where something is， you will get a result that looks like a list of lists like this。

 That you can supply into a get item lookup call attached to an array in this fashion。



![](img/9e8acb55f096297e396601a0d7edd911_171.png)

 By far the more common method of fancy indexing is going to be creating a mask。



![](img/9e8acb55f096297e396601a0d7edd911_173.png)

 Now we have not talked about mathematical operations on NumPy arrays yet。

 this will be the next big topic。 But the mathematical operations we apply to an array are performed element wise。

 So in turn vectorized to each individual data point inside of my data structure。

 So if I ask for my NumPy array C where those locations are greater than 16。

 what we will get back is a NumPy array of the same size and shape。

 Where instead of being filled with numbers it is filled with Boolean values。

 The Boolean values will be false in all of the locations in my original array that are less than or equal to 16。



![](img/9e8acb55f096297e396601a0d7edd911_175.png)

 And it will be true for all the locations in my array that are greater than 16。

 So the very first true value here is in the location of the 17 in my original data array。

 Now given that the mask I generate is the same size and shape as another array。



![](img/9e8acb55f096297e396601a0d7edd911_177.png)

 I can put this mask inside of square brackets， as a way to retrieve just the data that is satisfying some particular condition。

 Yes？ So the fancy indexing or returning flattened arrays。

 It is just generating a new array but it is not changing the C。 That is correct。

 So we are not performing any modifications to C。 C is still out there。

 Now there is one more thing that is going to make fancy indexing slower than doing our get items in our slices。



![](img/9e8acb55f096297e396601a0d7edd911_179.png)

 And the reason has to do with the way that NumPy thinks about efficiency。

 So if you use NumPy when you use your combination of get items in slices。

 it does not actually copy any data around in memory。 So for example。

 if I take my array C and I slice some data out of it。

 so maybe we will grab everything in the dimension of length 2。 I will scroll this up a little bit。

 I will grab one piece of data in the dimension of length 3 and then the middle 2 in the dimension of length 4。

 We can assign a name to the output of this。 We will call you D。 So here is my array D。

 A three-dimensional NumPy array。 But this is not actually its own separate data structure。

 So D is its own object but we haven't moved any data around。 If I want to be sure about this。

 on my array D， I have an attribute called the flags。

 That contains a number of facts about the NumPy array that I have created。

 The one that we are interested in is the one right here asking does this array control its own data？

 And the answer is no。

![](img/9e8acb55f096297e396601a0d7edd911_181.png)

 So my array D is a separate Python object but it hasn't created any copies of the 5， the 6， the 17。

 and the 18。

![](img/9e8acb55f096297e396601a0d7edd911_183.png)

 What it does is it holds references to the locations of those data inside of my original NumPy array。

 Now this can be good for efficiency purposes because copying data in memory is a very expensive operation。

 For us here with our little four data points this would be trivial but if you are dealing with a NumPy array that has millions of elements in it。

 we are talking about serious savings both in computational time and in memory space。

 The risk is changes that I make to D are also going to be reflected in C。 So for example。

 I can grab some item in D， we will grab the 5 is in position 0， 0， 0。

 And we will make you some large number like a thousand。 And sorry I will scroll up。

 When I look at my array D， we see that D has changed like we expected。

 And when I look at my array C， we see that C has also changed。

 Now this makes it very easy to extract sub arrays out of an array and manipulate them in place。

 So this might be exactly the behavior that you want but if you don't know that it's there this can be very surprising。

 So in contrast， when I use fancy indexing， NumPy will try really hard not to copy data around。

 But there are some things that it cannot represent with just a view。

 So if I use my up arrow to get this line back from history where we were grabbing everything out of C。

 we will receive us greater than 16。 We can give this a name as well。 We can call you E。

 And when we look at the flags of E， we see that when NumPy created this object。

 it also had to recopy all of that data to a new place in memory。 [silence]， Sorry。

 why is it now known data， why is E， it's known data？

 So E is its own data in this case because we have used something called fancy indexing。

 So because we've used this Boolean mask。 Now if we have time。

 we'll actually go over why this occurs towards the end of the tutorial to give you a short introduction。

 In memory， my NumPy arrays are these contiguous data structures but they're always one dimensional。

 So in my computer， this is always laid out in just one single line。

 NumPy tricks your computer into treating this one dimensional data structure as if it has multiple dimensions。

 by specifying a set of numbers to say this is how many bytes you move to pretend that you're moving in three dimensions。

 in four dimensions， in five dimensions。 So any recipe， any subset of data。

 and this is if you want to look at this， this is the strides attribute。

 And we might have a chance to talk about what these numbers mean later。 But any recipe。

 any sub-selection of data that I can represent by modifying the starting location of my array or the strides。

 I can represent very simply just by storing some mathematical formula somewhere in memory。

 And I don't have to move any data around。 Yes？ >> If you were to reshape D when you sliced it out of C。

 would it then put it in memory？ >> If I were to reshape D when I sliced it out of C。

 >> Like in the command where we said D， would we slice？ >> Oh， good question。

 So the question was if I， when I grabbed my array D out of array C， if I put a reshaping call。

 would this actually make a new copy of all this data？ And the answer is no。

 So I can perform as many reshaping operations on D as I want。

 And we'll talk about this a little bit later， but we're not actually modifying any of the data。

 the actual array portion that exists in memory。 So if I do reshape into like a four by one。



![](img/9e8acb55f096297e396601a0d7edd911_185.png)

 So the number is 1，000， 6， 17， and 18 aren't going anywhere。

 They're still in the same place as what I've done is I've changed just the number of attributes on my array。



![](img/9e8acb55f096297e396601a0d7edd911_187.png)

 So in this case I've changed the shape attribute and the strides attribute。 In this case。

 not the number of dimensions， although that sometimes happens too。 So reshaping operations。

 transposing operations， you can transpose arrays in NumPy with the 。t attribute。

 These are extraordinarily cheap operations because they modify just two or three integers that are being held in memory。

 So if something like a reshaping call or a transposing call makes it easy for you to do the kinds of calculations you need。

 you can， fearlessly apply these everywhere you want。 It's going to cost you almost nothing。 Yes？

 What was the C on data flag prior to the creation of D？ What was the C on data flag？ Oh。

 so this is a good question。 What you're going to see is not what you expect。 And I'll explain why。



![](img/9e8acb55f096297e396601a0d7edd911_189.png)

 So C was a three dimensional array that we created using the A range in the reshape call。

 And we would expect， since it's a very new thing that we've just made。

 that it would own its own data。 When we look at the own data， attribute it set to false。

 And the explanation is this。 When we created the array， that creation step happened in the A range。

 And it's that A range object that owns the data。 We've reshaped it and we've stored a reference to the reshaped version。

 Now we ourselves don't have a reference to the unreshaped data， but Python still does。

 So is that prior to D behind？ Exactly right。 Yes？ So you mentioned the transpose function of the derivative D。

 And I understand that for like a two dimensional array。

 When you did it on a three dimensional array here， how does that work？ How is that defined？

 What's that doing？ It looks like it left the first dimensional alone and did it transpose using the last two dimensions？

 Sure。 So I would love to answer that question like right now。

 But I don't actually know how transpose is working multiple dimensions。

 So I'm used to thinking about them in one or two and not in like 12。

 What I can do is I can look up the actual implementation and I'll get back to you with how they do it here。

 Thanks。 So seeing no further questions， I have another exercise that I would like you to do。

 Just like before， yes？ Okay， so you said when we first started that D didn't -- it only did some data。

 That was false。 Correct。 And now you're also saying because D would derive from C。

 And you're saying C itself doesn't own the dumb data either because really the reshape or。

 no the A range is the one that controls the data。 Correct。

 So when you have multiple calls like we said B equal and Q D dot A range and C equal and。

 Q D dot A range， are there two instances of the A range？

 One that owns what B is a copy of and the other one that owns what C is a copy of？

 So the question is if I understand correctly， does the A range function itself on this data？

 Are there separate ones that are being created every time I use this reshape？

 That's not quite correct。 So this is a little bit confusing and I'll draw you a picture in a second。

 Now the short takeaway is that if own data is set to true， you are guaranteed that this。

 array is the original owner of its NumPy array。

![](img/9e8acb55f096297e396601a0d7edd911_191.png)

 If it's false， it might be accessible through another name。 It might not be。

 So what's actually happening looks like this。

![](img/9e8acb55f096297e396601a0d7edd911_193.png)

 When I have my initial call to that E range function， E range is creating a NumPy array。



![](img/9e8acb55f096297e396601a0d7edd911_195.png)

![](img/9e8acb55f096297e396601a0d7edd911_196.png)

 We're going to sort of save this to talk about it later but we can talk about it now。



![](img/9e8acb55f096297e396601a0d7edd911_198.png)

 The NumPy array itself has two components。 It has some header that contains metadata and this is where all those attributes are like。

 the shape we looked at。 There's a dot n dim for the number of dimensions。

 In that header also contains a reference to where my actual array array is。



![](img/9e8acb55f096297e396601a0d7edd911_200.png)

 So this is where I would have my numbers like the floating point one， the floating point two。



![](img/9e8acb55f096297e396601a0d7edd911_202.png)

 the floating point three， the floating point four。



![](img/9e8acb55f096297e396601a0d7edd911_204.png)

 So E range produces this data structure。 When I do my reshape call。

 that reshape is applied to this data structure。

![](img/9e8acb55f096297e396601a0d7edd911_206.png)

![](img/9e8acb55f096297e396601a0d7edd911_207.png)

 What reshape is doing is it's creating just another header somewhere over here。



![](img/9e8acb55f096297e396601a0d7edd911_209.png)

 This header holds a reference to this original data but its shape is going to be different。

 Maybe in this case its shape is something like a two by two。



![](img/9e8acb55f096297e396601a0d7edd911_211.png)

 So this is the reason that our array C doesn't believe that it owns its own data。

 Even though we don't hold any reference through a name and Python to be able to access it。

 there is some object that exists somewhere that Python still has a reference to。



![](img/9e8acb55f096297e396601a0d7edd911_213.png)

 So what I asked was we called it twice so there would be two copies of two separate references。



![](img/9e8acb55f096297e396601a0d7edd911_215.png)

 and regulations so it's free。

![](img/9e8acb55f096297e396601a0d7edd911_217.png)

 Every time I use a constructor function like array， a range， zeros， empty， I'm getting both。



![](img/9e8acb55f096297e396601a0d7edd911_219.png)

 a new header and a new array。

![](img/9e8acb55f096297e396601a0d7edd911_221.png)

 What I'm doing calls like reshape or transpose， all I'm getting is the new header。



![](img/9e8acb55f096297e396601a0d7edd911_223.png)

 When I'm doing fancy indexing using those lists of integers or a Boolean mask。



![](img/9e8acb55f096297e396601a0d7edd911_225.png)

 NumPy will try really hard only to give me a new header but typically it's going to have to copy the entire array as well。



![](img/9e8acb55f096297e396601a0d7edd911_227.png)

 or the subset that I want。 If a goes away does it break or reference？



![](img/9e8acb55f096297e396601a0d7edd911_229.png)

![](img/9e8acb55f096297e396601a0d7edd911_230.png)

 So the question was is if there are no more references to this thing。

 this original combination from e-range。

![](img/9e8acb55f096297e396601a0d7edd911_232.png)

 does this object here stop working and the answer is no？



![](img/9e8acb55f096297e396601a0d7edd911_234.png)

 So Python's garbage collector， even if this disappears。



![](img/9e8acb55f096297e396601a0d7edd911_236.png)

 Python's garbage collector can see that this array is still being referred to by something。



![](img/9e8acb55f096297e396601a0d7edd911_238.png)

 So it's still being referred to by B or C or whatever we've decided to call this array。



![](img/9e8acb55f096297e396601a0d7edd911_240.png)

 So in Python， humans are allowed the whole references to objects by giving them a name。



![](img/9e8acb55f096297e396601a0d7edd911_242.png)

 and the assignment operator but objects also very frequently refer to each other。



![](img/9e8acb55f096297e396601a0d7edd911_244.png)

 So this array here will stay in memory until every single reference to it has either been deleted。



![](img/9e8acb55f096297e396601a0d7edd911_246.png)

 or has gone out of scope。

![](img/9e8acb55f096297e396601a0d7edd911_248.png)

 And then only then will the garbage collector come along and scrub it out。

 Talking a little bit about where data comes from， how arrays can own their own data or not own their own data。

 And this has sort of stemmed from a conversation that we are having about fancy indexing。

 and when we would or would not want to use it。 So the very next thing that I would like to have you do is to work on an exercise。

 This will be another short slide based exercise where you will be using fancy indexing to retrieve some data。



![](img/9e8acb55f096297e396601a0d7edd911_250.png)

 So once again we're going to have a two dimensional lump-high array。

 Once again it will be five by five。 And I would like you to do two things for me。

 The first thing I would like you to do is to extract all of the values here that are filled in with the color blue。

 This is not something that you will be able to do using slicing。

 The second thing I would like you to do is to retrieve all of the data from this numpy array。

 where that data is divisible by zero。 Not zero， sorry， divisible by three。 For this particular task。

 if you haven't used this before， I would recommend looking into the modulo operator。

 And Python this is the percent sign。 We've all been working on this exercise where we have a two dimensional five by five numpy array。

 And we have two tasks that we would like to perform。

 We would like to use fancy indexing first to extract the range of values here that are highlighted in blue。

 And secondly to extract all the numbers that are evenly divisible by three。

 So in the first task I want this sort of this off diagonal of the one， the seven。

 the thirteen and the nineteen。 So in this case what I would like to do is use the fancy indexing where I supply in each dimension。



![](img/9e8acb55f096297e396601a0d7edd911_252.png)

 individual， integer locations for each one of these items。



![](img/9e8acb55f096297e396601a0d7edd911_254.png)

 So since this is a two dimensional data structure。

 I will have two lists of indices that I'm supplying。



![](img/9e8acb55f096297e396601a0d7edd911_256.png)

 What am I going to put in my first list？ Zero comma one comma two comma three excellent。

 And what goes in the second list？ Exactly right。 One comma two comma three comma four and there are the values from my off diagonal。

 If you didn't want to type out the integers by hand you could have noticed that these are sequential integers。

 and that I have built in functions that will generate these for me。

 So we could do something like range instead。 That's exactly right。

 For the second task we wanted to discover and retrieve all of the data inside this array that is evenly divisible by zero。

 How can I do that？ So maybe we'll break this down a little bit。

 The first thing we'll look at is that a modulo three。

 so the modulo operator in Python is this percent sign。

 The modulo is going to return the remainder after taking three out of each of these numbers as many times as it can be done。

 So we see this NumPy array here that's being returned to me of the same size and shape。

 Let's fill it with zeros， ones and twos。 For all those operations where had I done my division I would have nothing left over versus I would have one left over versus I would have two left over。

 So essentially what I have here is an array full of remainders。

 Now to find out what's evenly divisible the next thing that I have to do is find all of those locations。

 where the values are strictly equivalent to zero。 So I can use my double equal sign comparison operator and now I have that boolean mask of the same size and shape filled with true and false values。

 where the choose correspond to all of the locations where there is no remainder after dividing by three。

 and the false corresponds to all those locations where there is a remainder。

 Now finally I can wrap this in square brackets and use this to retrieve just those numbers which are divisible by three。

 Now do we have any questions about this exercise？ Yes？ Yes？ A bracket x like this。

 I think you have an object that I don't。 So depending on what A is possibly。

 Then yes in that case that would work。 Seeing no further questions I have another exercise for you。

 This is going to be a longer exercise that is contained in a Python file。

 So what I would like you to do right now is to navigate to the location where you have either downloaded or cloned the materials from the repository for this tutorial。

 Inside of that location you have a PDF version of the slide exercises that you see me posting up here。

 You also have a folder called exercises。

![](img/9e8acb55f096297e396601a0d7edd911_258.png)

 In that exercises folder is a sequence of subfolders。

 We won't have time to do all of these today but they are there if you would like to do them for homework。

 The first exercise that we are going to do is an exercise called Dow under selection。

 The exercise itself is in the file called Dow under selection。py。 In the Dow under selection。

py file you will see at the very top。 Coded as a module doc string is an explanation of the exercise that you will be doing。

 Very briefly in line 51 we are going to be using that NumPy load text function to bring in a NumPy or a current session。

 What you are going to do is retrieve subsections of the entire Dow dataset。

 For example one of the tasks you will be performing is retrieving or finding the location of just those days when more than 5。

5 billion shares of Dow stock were traded。 I will have you work on this exercise and I will again do the thing where I wander around the room and answer questions。

 We have all been working on this exercise。 One of the longer exercises where we have this file Dow under selection。

py。 We are reading in some stock data and performing a couple of operations on it。

 We are extracting data， counting that data and finding out where those data are。

 What I have done here is loaded in that Dow。csv file and the name Dow is my Dow array。

 I can do something like check the shape of my Dow array and tells me that I have 168 observations and I have six kinds of observations。

 The first thing I want to do is create one of those Boolean masks that will tell me which days have trading volumes that are greater than this large number of 5。

5 billion。 How could I accomplish that？ I will give you a hint that I will use the array Dow。

 This is one option that I have。 Instead of rating it all the zeros， I will use a short hand syntax。

 For those of you who have not seen this before， you can use scientific notation as a floating point number。

 This is giving me all these locations where my trading volume is greater than 5。

5 times 10 to the ninth。 What I would like is some sort of Boolean mask。

 I can erase that outer container。 What I might do is I might think that I can use this comparison directly。

 All the locations in Dow that are greater than 5。5 times 10 to the ninth。

 In this particular situation， it is returning to a two-dimensional array where they true or false for each one of those individual elements inside the array。

 It is telling me that none of my opening prices， for example， are greater than 5。5 billion。

 which would be very surprising。 It is a very expensive stock。

 What I would like to do is perform -- this is the correct comparison。

 but I would like to perform it on a subset of the data。

 What we can do is we can select all of my observations in the top to bottom direction。

 but only the data that represents the volumes。 If we look in here。

 we have a little helpful constant that is defined for us。

 It tells us that these are in the fourth location。 I can ask for the data in position 4。

 which is giving us only the trading volumes， and then I can ask where those are greater than 5。

5 times 10 to the ninth。 Here is my Boolean mask， where I have true values only for those locations where I have very high trading volumes。

 In the next question， it tells us to figure out how many days had a trading volume greater than 5。

5 billion。 The hint is to use the summation function。

 What I will do is use my up arrow to get this back。

 I will give you the name mask so I can do some stuff with you later。

 How can I use my mask in the summation function to tell me how many days had very high trading volumes？

 Exactly right。 I can ask for the sum of that mask。 It tells me that I have 18 days。

 Now you will notice specifically I am using the NumPy version of the summation function and not the Python version of sum。

 They will both give you the same answer。 But generally speaking。

 data structures that have methods defined on them in the same library are optimized to work well with each other。

 We might have time to look at this later， but what we will see is that NumPy summation function is much more efficient on NumPy arrays than Python summation function is。

 We can save ourselves a little bit of time by using the competent NumPy sum function on a NumPy data structure。

 My very last task was to use a function called "where" inside of the NumPy namespace to give me the locations of all the days with very high trading volumes。

 So how can I use "where" to tell me which integer locations have very high trading volumes？

 So I can use np。where and I can give it that boolean mask and this is giving me all of the locations in that mask that contain a true value。

 [ Inaudible ]， So our mask here is one-dimensional。

 It is reflecting the locations just in the top to bottom direction in the original array。

 not both the top to bottom and the left to right。 If we had that left to right direction。

 in addition to this array that contains the 12， the 13， the 15， the 51。

 there would be another array that just contained 4， 4， 4， 4， 4。 [ Inaudible ]。

 So I think it's just asking for the index， so the location in that top to bottom direction。 Yeah。

 All right， do we have any questions about this exercise？ [ Inaudible ]。

 So when you're looking at the function signature here for np。where。

 this x and the y here in the brackets， these are optional。

 So this isn't something that I'm required to pass in。 [ Inaudible ]， So the question was in np。

where， why did I supply just the boolean mask and not boolean mask， equivalence operator to true。

 I mean， the answer is that they reduce to the same thing。

 So if I ask for all the locations where true is true。

 it's going to return the same boolean mask to me。 So this is specific to the structure of this particular situation。

 But generally speaking in Python， every single object can be coerced into a string and every single object can be coerced into a boolean value。

 And it's very， we would call it idiomatic。 So if you've been writing Python for a long time。

 you will see people not include the strict comparison to true。

 They will just use the object itself and let that coercion happen implicitly。 [ Inaudible ]。

 So now that we've seen how we can extract data out of NumPy arrays in a very fast and efficient manner。

 And what we would like to do next is to see how we can perform operations on those kinds of arrays。

 We're going to structure our idea of performing operations on NumPy arrays into sort of two different camps。

 One of these we will call mathematical operations。

 And the other one we will call reduction operations。

 A mathematical operation is going to return an array of the same size and shape。

 A reduction operation is going to return an array that smaller。

 So when we say that it's a reduction， we mean we're reducing the amount of data that we end up having。

 So something like addition is going to be a mathematical operation。

 Something like taking the summation is going to be a reduction operation。

 Now inside of the world of NumPy， we can perform any kind of mathematical operations between NumPy objects。

 We have to be very， very concerned about the shape of things。

 And what I mean by that is that we have some array like A for example。

 Here is my two dimensional five by five。 I am allowed to do something like add a scalar to my array。

 However that scalar is added element wise to each item in my individual array。

 I am also allowed to add an array of the same size and shape。

 So I can add a five by five array to a five by five array。

 And what I get back is a five by five array。 But I cannot for example add together a five by five NumPy array with a length seven NumPy array。

 And if we try this， what we see is that we get an exception from NumPy saying that the shapes don't fit。

 It doesn't know how to map a one dimensional array of length seven onto a two dimensional five by five。

 Now in some languages， if one of those dimensions is evenly divisible by the other。

 the language itself will repeat the values from the smaller array。 NumPy won't do that either。

 Now the shapes that you'll need to perform these operations are going to vary depending on the kind of operation you're trying to do。

 So the way that they need to match up is going to be different for simple binary operations like this。

 Then it will be for something like the dot product of two matrices or the outer product of two matrices。

 But it's always something that you're going to have to worry about。 For these kinds of operations。

 bless you， we've seen that a scalar value works in array of the same size and shape works。

 I can also have a raise of two different shapes provided they are capable of being broadcast together。

 The word broadcast here has a specific meaning in the world of NumPy。

 It means they follow a set of rules that will allow them to be fit together as if they were the same size and shape。

 To see what this looks like， we can take our array A and we can try to add in a one-dimensional array of length five。

 And what we see here is that even though these are not the same size and shape。

 they are capable of being combined。 So when NumPy sees my attempt to combine this two-dimensional array with this one-dimensional array。

 the first thing that it's going to do is it's going to prepend a one in front of this five as many ones as it takes to make these two arrays have the same number of dimensions。

 Any non-one length dimension， so here the dimension of length five has to match exactly。

 So the very last dimensions in both of these arrays are of length five， so that's fine。

 All the arrays that don't match in length， one of the numbers has to be a one。

 So what we see here is this is being implicitly converted into something like this。

 where I'm adding a zero to everything on the left-hand most side and then a four to everything on the right-hand most side。

 Now this works for broadcasting together an array of multiple dimensions against an array that has a smaller number of dimensions。

 You can also broadcast arrays together when they are each something like one-dimensional or two-dimensional in a way that generates a resulting data structure that has a larger number of dimensions。

 or we should say a larger number of filled dimensions。

 So instead of adding my five by five array to my one by five array， I can do something like this。

 where I add NumPy to add together a five by one against a one by five。

 and the resulting data structure is a two-dimensional data structure of length five by five。

 Now because the broadcasting rules， sorry， one by four， this is my five by five。

 Now because the broadcasting rules include pre-pending ones。

 I don't have to include the explicit reshape call here。 So maybe we'll tally this。

 and we can write this down as a set of rules for doing math。 I guess that's not happening。

 Where we say that rule number one is that the very first thing I have to do is make sure my sheep's match。

 And by match we mean that one of them can be a scalar。

 they can be the exact same size and shape or that they can be broadcastable。 Rule number two。

 when we've seen this happen quite a bit already， is that my mathematical operations are applied element-wise。

 So if you are coming from a language like MATLAB， and are used to multiplying two matrices together and getting very explicitly the dot product of those two matrices。

 this does not happen in NumPy。 You'll have to ask for that dot product or the inner product or that outer product very explicitly。

 The next thing that we're going to have to worry about is what happens when we have special numbers inside of our array somewhere。

 So what I would like to do next is we are going to take this array A， or 5x5。

 and we're going to course it into an array of floating point numbers。

 so that I can insert one of those NAND values in it。

 So to the same name A we are going to reassign the output of A dot S type。

 We'll make you a 64-bit floating point number array。 And let's say in position two three。

 I want to insert an Np。N。 So we've gotten rid of the number 13 in what we have there instead as a missing value。

 Now the reason that we're doing this is that things that are not a number have special behavior when it comes to performing mathematical or what we haven't talked about yet。

 reduction operations。 And that special behavior is that they propagate。

 And what I mean by that is that any number added to Np。N is going to return Np。N。

 So if I have my array A and I try to add 5 to everything。

 we will see that everything has increased by 5。 My 0 has become a 5， my 1 has become a 6。 Sorry。

 I can't scroll this up。 Except for that not a number in position 13， which remains not a number。

 Now this probably makes sense。 This might not be surprising。

 but this behavior combined with the way that Np thinks about reduction operations might lead to a little bit of confusion。

 So in Np we have a whole range of functions inside of the Np namespace。

 We've seen one of them already。 That will allow us to do things like calculate the sum of an array。

 And if I do this， we see that the summation from my entire array is not a number。

 Now if we think about summation as starting off with the number like zero， in adding。

 in the elements of this array one by one， zero plus zero is zero， zero plus one is one。

 zero plus two is two。 This is working out really well。 And until we get to this nan。

 anything plus nan is nan， and then nan plus fourteen is nan， nan plus fifteen is nan。

 nan plus sixteen is nan。 So these nan numbers combined with the direction operations often leave you with no data left。

 at all。 Now by default， and this is our rule number four here， when I apply reduction operations。

 in NumPy， it will take an array and reduce it down to a single scalar value。

 But this is not always what I want， it's often not what I want。

 So we have an optional way of specifying which dimension or dimensions we would like to。

 be collapsed by the reducer。 So in the summation function， I have an optional second argument。

 That second argument is axis， and axis accepts an integer value where that integer value。

 sorry I can scroll up， the integer value corresponds to the position in the shape tuple of the dimension。

 I would like to disappear。 So in my five by five array。

 in the zeroth position is the dimension going up and down， this way。

 In the one-th position is the dimension going left to right。

 So if I want to collapse my data in the left to right direction， I can specify that I want。

 to collapse on the one-th axis。 And this value 10 corresponds to the zero plus one plus two plus three plus four。

 35 to these， numbers added together。 And here is that nan propagating here。 I would love to。

 Let's do this with a better array though。 So I have this array B that instead of being five by five is four by three。

 And we can use the difference in those dimensions to make this a little bit easier to think about。

 So here's my array B。 If I look at B dot shape， this is my shape tuple。

 It tells me that the dimension of length four is in the zeroth position。

 The dimension of length three is in the one-th position inside that tuple。

 So if I want to collapse the four and get a one-dimensional array of length three， I ask。

 for np dot sum of that array B with axis equal to zero。

 And here is my resulting numpy array of length three。 Conversely。

 if I want to maintain the dimension of length four and collapse the dimension of， length three。

 I can collapse across the one-th or in this case I'll use the negative one-th， axis。

 And now I've gone from a two-dimensional numpy array， two-way one-dimensional numpy array。

 to that one-dimensional numpy array of length four。 So the question was。

 in broadcasting do my arrays change size？ The initial arrays do not。

 So they are not resized or reshaped in any way。 But the resulting array can be unexpected as in quite the right word。

 But it can have a larger length than you used to mention than you might expect if you don't。

 know the broadcasting roles。 The question was， in broadcasting are they still doing the referencing？

 That depends on what you mean by referencing。 That's exactly right。

 So any of those implicit stages in between or the arrays are getting reshaped during the。

 broadcasting itself。 Those are not copying any data anywhere。

 But that resulting array will be a new object。 And so we've written on the board here our fourth rule for how math works in numpy。

 By default our reduction operations will collapse everything down to a single scalar， value。

 Now it might be the case that I'm working with a three-dimensional or a four-dimensional。

 numpy array and I want to collapse two or three dimensions。

 And in that case the axis keyword argument will accept a tuple of all of the axes you。

 would like to have collapsed。 And this is true for most reduction functions， not all。

 So there are some reducers that will only let you specify that you want everything to。

 be collapsed or only want access to be collapsed， but not some intermediate fraction。 Yes？

 So the question was can I help you understand how the word axes is being used？ I sure hope so。

 The axis is corresponding specifically to each dimension。

 So in your head if the word axis is confusing because it means other things to you， you can。

 replace that word axis with dimension。 I want to collapse dimension negative one。

 Negative one means the last dimension。 Exactly right。

 So negative one here meaning the last dimension。 That's exactly correct。

 So in this case it's a little silly。 Typing negative one is not significantly more easier than typing one。

 but I wanted you， to see that this does work。 So that if you're dealing with who knows。

 maybe a seven-dimensional numpy array， you might， want to count over is it the six axis or the seven axis if you know that you want the last。

 one， you can always just use this negative one。 Do you have other questions about this？

 So I have an exercise that I would like you to do。

 This is going to have you practice the mathematical part。

 We have separate exercises for the reducers。 And we'll spend a little bit of time talking about the different kinds of reductions that。

 we can do as well。 It's going to have you practice the mathematical portion of the numpy stuff。

 And this is another file we're going to open。 It's going to be in a folder called calc under return and a file called calc under return。

py。 In this particular exercise you're given a numpy array。

 This is just a one-dimensional numpy array of stock prices。

 These stock prices I believe are coming from Apple。 Your job for this exercise。

 this is not the hard part。 Your job for this exercise is to calculate the return value for the stock for each day。

 using the formula given at the top of the file。 So it's today's price minus yesterday's price。

 quantity divided by yesterday's price。 So far this is really straightforward。 But here's the catch。

 I'm not going to let you write a loop。 So you have to perform this calculation without using the four keyword or the wild keyword。

 Now if you're used to thinking about vectorized mathematical operations， this will go pretty。

 quickly。 This might take you about five minutes。 If this is not how you're used to thinking about working with data structures。

 it might， take you a while。 There's a trick to it is why。

 So what I'd like you to do is think real hard about it and we'll give you about five。

 minutes to see if you can come up with a solution on your own。

 Then we're going to come back together as a class and I will draw you a hint on the board。

 So we've all been working on this exercise where we are applying this formula for calculating。

 the return of the stock given some one dimensional lump-high array。

 The first thing that I'm going to do is I'm going to change this formula a little bit。

 This just makes it easier for me to think about instead of today's price versus yesterday's。

 to do today's price versus tomorrow price。 So our new formula is that my return is the price of the stock tomorrow minus the stock。

 right now divided by the stock price right now。 And so conceptually if I am a person who is standing in location zero inside of a numpy。

 array， all of the tomorrows from where I'm standing are offset by one。 So for my numpy array。

 I have my prices here。 My tomatoes are going to be everything from position one onward。

 These are all of the tomorrow prices that exist。 So if I want to know tomorrow's price is minus today's prices。

 I can take my tomorrow's prices， and I can subtract today's prices。 When I try to do this though。

 I get this error message that says my operands could not be， broadcast together。

 They have the wrong shape。 I would like someone to explain to me what this error message is saying。

 Exactly right。 So I have two arrays that are almost the same size and shape。

 but one of them is just one， smaller and it's one smaller because I am very explicitly excluding right now。

 I'm excluding， today。 So there are sort of two different ways we can think about solving this。

 The first is that within the constraints of the numpy library， I have to have two things。

 that are the same shape。 And if I do prices one colon， minus prices one colon。

 I'll just end up with an array， filled with zeros because that's tomorrow's price minus tomorrow's price。

 So the next thing that I could try， the only option I have left， is to chop off the very。

 last price。 So everything up to not including the last price and here are the differences in the。

 prices between today's and tomorrow's。 Now conceptually what we're doing is that we think about what happens at the very end。

 of my array， so I'm in the last data point。 To calculate my return， I need tomorrow's price。

 but there's no more data left。 So I cannot calculate a return for that day。 So out of 253 was it？

 Yeah， out of 253 data points， I can only calculate 252 stock returns。

 So this is almost all the way there。 I need to add one more thing and that's that division。

 So I'm going to group my numerator and parentheses to make sure I'm dividing the quantity and。

 not just the last item。 And here again we will divide by our prices from all of the today's。

 My slash is facing the wrong way。 There we go。 So this here in 137 this is the solution for this particular exercise。

 Now while you are working on it， I went and I coded up a different solution when it did， use a loop。

 So we can take a look at it really quick。 Here's my bad solution。

 It's a function called bad solution and it has that for loop where I'm performing that。

 same calculation where the stock return for an individual day is tomorrow minus today。

 divided by today。 And this will give us the same answer but I'd like to ask something a little bit different。

 I'd like to ask which one of these is more performant。

 So just like before we can use that magic time function。

 In here we can apply it directly to this expression using NumPy's vectorized math and。

 it tells us it can calculate the returns for my 250 stock prices in about 2。2 microseconds。

 I will do another magic time it。 This time calling that bad solution function on those same prices。

 We are now at 104 microseconds so this is 50 times slower。

 And again typically the difference in the running time for each one of these solutions。

 is going to grow as my data get larger as well。 I mean in this particular case there is still a for loop happening somewhere but when we。

 use vectorized strategies like this where I'm creating not new data but references to。

 just one set of data somewhere and I'm letting NumPy vectorize the mathematical operations。

 between the eventual references those eventual values。

 All of that looping happens way way down low at the level of C。 And when I have that。

 looping very up high at the level I am in Python it's going to be a lot slower。

 So even though in the solution we are still using in my bad solution this is still NumPy。

 subtraction so I'm still taking advantage of that static typing。

 Specifically because I have that Python for loop in the way I'm getting a greatly diminished。

 performance。 So this is one of the common pain points in your code if you are doing a lot of math。

 in NumPy but it's inside of Python loops there might be a way to vectorize that using references。

 to the NumPy arrays themselves。 We have time in here to do one more big exercise。

 Before we can do that though we are going to have a brief tour of the reduction operations。

 that are available to us inside of NumPy。 So we've seen some of a bunch already that was np。sum。

 We also have other reduction functions to calculate statistical properties of arrays so for example。

 I could ask for the np。mean of my prices and just like some I can ask for the mean across。

 just one particular axis。 In this case prices is a one dimensional data structure so having an axis here wouldn't。

 make sense。 So I can ask for the mean of my prices and I have the same standard deviation and also。

 variance。 I might want to know the minimum or the maximum values and I can find this using np。

max of， prices。 So the maximum stock price for Apple in 2008 was 194 I'm assuming that's dollars。

 I can also ask for the minimum。 The minimum price was $80。50。

 Now for some of these reducers I have sort of friendly methods that instead of telling。

 you what the minimum or the maximum value is will tell you where it occurs。

 So if I wanted to know the integer location of the lowest price instead of asking for。

 the mean I can ask for the argument and it tells us that this minimum price occurs 225。

 days in to the year 2008。 Similarly I can also ask for the arg。

max and it tells us that the maximum stock price， was on the very first day so a lot of movement downhill for Apple in 2008。

 Now there's one thing to be aware of when I'm using things like arg。max and that has。

 to apply to a NumPy arrays that have multiple dimensions。

 So if we pull up let's pull up b our two dimensional NumPy array so this is my 4x3 array。

 And what I would like to do is I would like to ask where the np NumPy。arg。max is of my， array b。

 I'm calling the np。arg。max function on b and I don't get this information back in two dimensions。

 So it's not telling me that it is in position 32。 It tells me it's in position 11。

 So when you use functions like arg。max and arg。min the first thing that NumPy does is。

 it flattens it out into a one dimensional NumPy array。

 This is usually not the actual number you want to end up working with。

 There are a couple of ways that you can turn this 11 back into an index that knows about。

 two dimensions。 The easiest is to use a function defined inside of NumPy called unravel index。

 So if unravel is a way of flattening an index unravel is a way of unflatning the index。

 Unravel index is going to take some integer like 11。

 In the shape I would like it to be unraveled into。

 So in this case it will be the shape of the original array b。

 So putting this all together we can ask NumPy to dot unravel my index。

 The index I want to unravel is the output of calling np。arg。max on b and this gives me。

 my rabbled my flattened index location。 And then finally I'm going to give it b dot shape。

 For the shape of the two dimensional data structure I would like you to be unraveled into。

 And what this returns to us is the 2。32 which you should be able to convince yourselves is。

 the two dimensional location of the value 11。 So the last exercise we'll be working on here today is going to have you use。

 This is going to have you practice these reducers on a series of NumPy arrays。

 So this will be in another Python file inside of another exercise folder。

 This one is going to be called the wind statistics。

 And in wind under statistics is a file called the wind under statistics dot pi。

 It's going to have you read in some wind data where the first three， I don't want to call。

 them columns， but the first three data points are representations of the year， month and。

 day as numerical integers。 In the rest are wind speeds recorded across a bunch of different stations inside of Ireland。

 And you're going to practice finding things like the minimum， the mean， the maximum。

 You're going to do it for all the locations， you're going to do it for each location。

 There are some， I don't think they're marked as bonus。 Oh， maybe they are marked as bonus。

 There are some bonus questions at the end I don't expect we'll have time to get to those， today。

 And dear Python East us， it is now 12 o'clock。 This marks the end of our tutorial session。

 I don't want you however to take this as a signal that you are being forced to leave， the room。

 Maybe there's something we talked about during the tutorial today that you're still a little。

 unsure of。 Maybe you have a question about the broader Python ecosystem that you felt was inappropriate。

 to bring up during a class specifically on NumPy。 Maybe you've been really aching to sing a song to Alex。

 but you didn't want to interrupt。 I would like you to see this as an opportunity for all those things。

 to bring your questions， to us， to bring your concerns to us。

 And for those of you who are heading off to lunch， I would like to wish you an enjoyable。

 rest of the conference。 Thank you so much for your attention。 [APPLAUSE]， [BLANK_AUDIO]。

