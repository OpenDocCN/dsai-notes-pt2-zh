# SciPy 2018视频专辑 - P7：SciPy 2018视频专辑 (P7. Interactive Data Visualization Leveraging Jupyter, Rust and - GalileoHua - BV1TE411n7Ny

 Thank you Chelsea。 Yeah， so that's a really long title。

 Hopefully we'll walk through it together today， and you'll understand why I had to make it so long and I couldn't make it any shorter。

 But first I want to tell you all a little about me。 This is my first time at SciPy。

 so I'm gonna give a little introduction。 Thank you。

 I got my PhD from the University of California Berkeley just under a year ago。 I got。

 a lot of work in radiation transport， so simulating radiation moving through space。

 And this was in collaboration with Oak Ridge National Labs and a lot of my work was done。

 as a member of the Berkeley Institute for Data Science。 So I hovered around kind of creeped。

 on the bed solos but I wasn't actually a fellow。 Now I'm at the University of Illinois at。

 Urbana-Champaign at the National Center for Supercomputing Applications specifically in the Data Exploration Lab。

 There's a lot of members of the Data Exploration Lab here at SciPy this week。 You might have。

 seen Nathan Goldbaum give an update on YT， the package I'm gonna be kind of talking about today。

 Yesterday in the Tools Plenary session you might have seen Megan Lang give a talk on。

 interfacing science models in using CIS interface。 That was two days ago or you might have seen。

 Casper Kovalik give a talk on the whole tale。 And I'm also involved in scientific computing。

 I'm in a software carpentry instructor。 I maintain the software carpentry get lesson and I'm a。

 member of the curriculum advisory committee for software carpentry and I'm a part of the。

 committee for diversity inclusion and scientific computing on NEMVocus。 That's a lot of stuff。



![](img/bb412fc545e07a2acf0d9da61331c993_1.png)

 So we're in the data visualization section。 All of us care about data visualization and。

 I'm gonna be specifically talking mostly about a package called YT today。 YT is a package。

 that is designed to visualize multidimensional data。 It was originally designed for astronomical。

 data but now as Nathan mentioned yesterday it is branching into other domains。 So I've given。

 a little selection of different domains that YT is branching into。 Here we have meteorology。

 We have an original astronomy data set。 We have high energy physics and oceanography。

 This is like an earthquake simulation and so seismology and then also relativistic physics。



![](img/bb412fc545e07a2acf0d9da61331c993_3.png)

 on the last one。 So we can visualize our data and when we want to publish papers we want。

 to get some really high quality images but in between that we want to interactively visualize。

 our data and see where the interesting things are。 And so this is a different step in the。

 data visualization sort of pathway that we want to go down。 Interactivity allows on the。

 fly parameter tuning。 We can change the color map to bring out features that interest us。

 We might change the min and the max values of our data that are being visualized because。

 we are interested in them。 But it also allows for this exploration of our data。 We can zoom。

 in on a feature that we care about and maybe we see things that we didn't expect in our。

 simulations or in our observations。 This reveals the interesting science and it also allows。

 science to be accessible。 We might have a data set that we want to share with the public。

 And interactive data visualization allows our science to be accessible to non-scientists。

 Maybe to scientists that don't really like coding very much or find coding really intimidating。

 And also the people who are new to the data set。 So these can be like I might pass my。

 radiation simulation data to a friend and they don't really know it very well。 Giving them。

 an interactive tool to browse that data and visualize it interactively is very helpful。



![](img/bb412fc545e07a2acf0d9da61331c993_5.png)

 to them。 And there's a lot of interactive tools that exist in the Python ecosystem。 We。

 care about this。 This is our community。 So I'm going to be specifically talking about。

 interactive visualization with YT today。 YT has some interactive features already。 But I'm。

 going to be talking about the niche area where you're going to be having data maybe on a。

 remote server or something like that。 And you want to browse it on your local machine。



![](img/bb412fc545e07a2acf0d9da61331c993_7.png)

 So I'm going to do like we were talking about the last one。 I'm going to do a live demo。 So。



![](img/bb412fc545e07a2acf0d9da61331c993_9.png)

 we'll see how this goes。 So we can -- so I especially want to talk about how amazing。

 the Jupyter widget ecosystem is。 IPy widgets has developed a whole suite of tools that you。

 can use to interactively browse your data in a Jupyter notebook。 I'm going to show you。



![](img/bb412fc545e07a2acf0d9da61331c993_11.png)

 though that this can be limiting sometimes。 Especially when you have larger data sets。

 or if you have an image that's quite large or you're re-rendering things a lot。 So I'm。

 going to import -- I'm using YT here。 Is this also readable to everybody？ Okay。 You want， a bigger？

 Okay。 Oops。 Sorry。 Yeah， I'm trying it。 Okay。 I'll talk through it。 I don't know。

 why it's not going zooming this time。 Okay。 So I'm going to interact。 This first execution。

 is I'm loading my data set。 This is on my machine and I have -- I'm going to be loading。

 isolated galaxy which is a data set that you can download with -- that's in the documentation。

 of YT。 It's something that's used as -- to introduce beginners to YT。 So yes， I want to。



![](img/bb412fc545e07a2acf0d9da61331c993_13.png)

 download that。 Oh， great。 Huh？ Oh， thank you。 That was me leaning on it。 Oh， I see what。

 I did there。 Thanks， everybody。 There we go。 Okay。 Well， good。 Now everything's going super。



![](img/bb412fc545e07a2acf0d9da61331c993_15.png)

 well。 So I've imported my data。 I get some information from YT about my data set。 And。

 now I'm going to try and use Jupyter widgets out of the box with this data set。 So I'm。

 creating -- I'm using a set of widgets to create -- I'm setting some traits first。 So。

 traitlets are things that I can sync with Jupyter widgets and they -- you can use -- so if you。

 have a trait， you can sync it with one of the slider widgets or something like that and。

 it'll update。 So I'm going to set up a visualization using these traitlets。

 And then I have an image。

![](img/bb412fc545e07a2acf0d9da61331c993_17.png)

 I have a image that I'm going to deposit my data into。 Okay。 So the first render doesn't。

 quite work， but if I zoom slightly， the first thing here is supposed to be zoom。 And then。



![](img/bb412fc545e07a2acf0d9da61331c993_19.png)

 the next two widgets are X and Y。 So we can see it's a very isolated galaxy。 There's nothing。



![](img/bb412fc545e07a2acf0d9da61331c993_21.png)

 around it。 And if I start zooming and moving around， what this is going to do is this is。



![](img/bb412fc545e07a2acf0d9da61331c993_23.png)

 going to -- I'm going to have to update the image and I'm going to have to re-pixelize。

 it to update the view if I zoom out。 And if I do this， I'm going to let go now and it's。



![](img/bb412fc545e07a2acf0d9da61331c993_25.png)

![](img/bb412fc545e07a2acf0d9da61331c993_26.png)

 going to keep moving。 And Y。T。 is printing some error messages， which is why now we have。



![](img/bb412fc545e07a2acf0d9da61331c993_28.png)

 this extra box。 So if I go down， I can see that I've recreated this fixed resolution buffer。



![](img/bb412fc545e07a2acf0d9da61331c993_30.png)

 This is part of Y。T。 And basically the fixed resolution buffer will take a slice and it。



![](img/bb412fc545e07a2acf0d9da61331c993_32.png)

 will create an array that is fixed。 So if I have a data set that has a mesh that's variable。

 it's going to make it so it's all equal。 So if I want 500 by 500 pixels， it's going to。

 give me the array in that fixed resolution。 So I have to re-update it every time with that。



![](img/bb412fc545e07a2acf0d9da61331c993_34.png)

![](img/bb412fc545e07a2acf0d9da61331c993_35.png)

 new fixed resolution， even though I have a slice that I had already taken out。 And I've。

 done this lots of times。 So you can imagine as you peruse your data set， you're going to。

 be regenerating images lots and lots of times。 So if you have a really large data set on a。

 machine or even on your computer， this can be very slow。 Okay。 So I mentioned that this。



![](img/bb412fc545e07a2acf0d9da61331c993_37.png)

![](img/bb412fc545e07a2acf0d9da61331c993_38.png)

 can be very slow。 What's really happening when we start rendering images in a browser， but。

 from on our local machine or even on a remote server， we send a request from the browser。

 to the machine。 And then that's going to like serialize the data， it's going to calculate。

 the image and then it's going to send it back and we're going to pull that image down from。

 this remote server onto our machine。 And then we have a visualization。 Super cool。 But as。

 I said before， you can get， you can do this lots and lots of times。 So when might this。



![](img/bb412fc545e07a2acf0d9da61331c993_40.png)

 become cumbersome？ We have the total time to generate a single image on the server。 And。

 I've kind of selected a couple of different things that I think might spend time， that。

 you might spend time doing that。 You have the signal， like the request signal to request。

 this image， the time to serialize the data， the time to calculate the image on the server。

 the time to pull it back down onto your， into your browser， and then the time to display， the image。

 But when you're doing it with this， this process， you have to do this end times。

 and all of these times are going to， all of these specific time variables are going to。

 be multiplied by end interactions。 So if I zoom， I might have like 20 images that are。

 created in a zoom action if I want that animation with these data sets。 So what if instead of。



![](img/bb412fc545e07a2acf0d9da61331c993_42.png)

 sending the image back from the server， we send the request and we get a chunk of the data。

 a chunk of the data that interests us and then we do the calculation and the display of the。

 image in the browser。 So we pull some of the data into the browser rather than the image， itself。

 Pushing data to the client makes sense as if we can make the time to calculate。



![](img/bb412fc545e07a2acf0d9da61331c993_44.png)

 the image on the client side smaller than the time to calculate it on the server side。

 So I've kind of condensed those t， those small t's in the previous slide into two kind of。

 big chunks that I think are interesting。 So there's the number of interactions we have。

 times the time t client is the time to calculate the image on the client side in the browser。

 And then we're going to add this with the time， the data， like how large the chunk of。

 the data we're sending from the server divided by whatever our speed is。 So if we have an。

 extremely fast internet connection， this is going to be a very small component。 But we。

 want that in particular to be less than this。 So the time to generate the image on the server。

 plus the time to generate the time that it's going to take to transfer it。 So the data divided。

 by the rate to transfer it back and forth。 And you can see that we've taken this end and。

 the number of interactions is only times the time to generate the image on the client on。

 the left side。 So I've kind of talked through those。 So how might this happen？ What are the。

 big features that we think we can make that happen？ First of all， I kind of mentioned the。

 more interactions you do， the more time you're going to be generating， you're going to be。

 wasting transferring images from your server up onto your local machine or down onto your。

 local machine。 Also， as you increase the size of the image， this is going to get more and。

 more cumbersome， right？ Because this term over here is going to get much larger。 And also。

 if we can decrease the time to calculate the image on the client side， that's going to。

 make this a more beneficial transfer。 So this is just an illustration kind of giving you， an idea。

 If you have a data set that has this multi-resolution data， we can overlay what。

 the grid looks like。 And you can see towards the edge of the data， we have a pretty sparse。

 set of data， but there are some interesting regions where our mesh is much， much finer。

 Now if we're going to be exploring this data set using a traditional method where you transfer。

 the image every time you update， and if you want like a 10 by 10 pixel image， that's not。

 going to be a big deal。 But as you increase the pixel resolution， you're actually becoming。

 very inefficient because you have all this sparse data and you're sending hundreds and。

 hundreds of pixels that are exactly the same value in these outer regions。 So we created。



![](img/bb412fc545e07a2acf0d9da61331c993_46.png)

![](img/bb412fc545e07a2acf0d9da61331c993_47.png)

 a widget that does this。 Let's see if I can push plus in the right place this time。 So。



![](img/bb412fc545e07a2acf0d9da61331c993_49.png)

 this is the same data set。 And we have some controls here。 They go away。 But this is actually。



![](img/bb412fc545e07a2acf0d9da61331c993_51.png)

 a fairly large image。 I've chosen a 1000 by 1，000 pixel image。 And I'm using iPod widgets。



![](img/bb412fc545e07a2acf0d9da61331c993_53.png)

 layout to shrink it down so it's not stretched weirdly during this interaction。 So I can change。



![](img/bb412fc545e07a2acf0d9da61331c993_55.png)

 the color scale to log。 I can also change the color map to whatever I want it to be。 And。



![](img/bb412fc545e07a2acf0d9da61331c993_57.png)

![](img/bb412fc545e07a2acf0d9da61331c993_58.png)

![](img/bb412fc545e07a2acf0d9da61331c993_59.png)

 then I can click an image and it updates way faster than if I was using traditional widgets。

 I also can drag it。 It's going to -- and that will update immediately。 Whereas if I did。

 a drag event like this， if I built this in purely on the Python side with the widget。

 it would be much， much slower。 Because this is very significant transferring this 1000。

 pixel array back and forth into the browser。 So what does this mean？ Like we built this。



![](img/bb412fc545e07a2acf0d9da61331c993_61.png)

 widget。 It's cool。 It seems kind of neat。 Maybe not cool as an awesome cat plot。 But， you know。

 it's pretty cool。 But with a single fixed upfront cost， we eliminate the requirement。

 to transfer all of those images between the server and the client。 This is useful in some。

 cases but not all。 So， you know， if you have a data set that's really dense and you have。

 an extremely fast internet connection， then maybe it's not going to be useful to use this。

 But this is useful for a lot of different cases。 So I'm going to kind of talk through。

 what is happening。 And a little bit I'm going to tell you more about WebAssembly。 But so。

 I'm going to tell you how the first render kind of works。 So we have our data from YT。

 We send a couple of different arrays。 PX and PY are the center points of each of those。

 mesh cells that you saw。 So you can see it's variable。 And PDX and PDY are the half width。

 values of each of those mesh cells。 And then value could be any field that you're interested， in。

 It could be density。 It could be temperature or something like that。 And I have a little。

 key down here。 So the yellow is going to be a function that we built in WebAssembly。 This。

 is custom。 And then traitlets are things that we can like you saw before。 These are things。

 that we can sync。 And these are on the Python side。 These are accessible to any user。 So。

 you could modify these as you wanted to。 And then -- so we're going to pass this in to， our widget。

 It's called YT-PY-Canvas。 And all of those arrays are going to go into a。

 widget called the fix resolution buffer viewer。 This has two custom WebAssembly modules。 There's。

 a variable mesh which is the data structure we store all of the data in。 And then there's。

 a fix resolution buffer which is like the view of the data that we're interested in。

 So we pull that like little chunk out。 The variable mesh isn't going to change after we've。

 uploaded the data。 We're going to pass it into a data array。 We're going to -- this is。

 going to make a data array and we're going to pass it to our normalizer。 So we pass that。

 array and we want to do another performance important function。 So we're going to pass。

 it into WebAssembly again。 And that's going to be color maps。 This is the name of the module。

 but it's actually normalizing and it's creating an image array out of the data array。 So it's。

 taking the single array that's all data points and it's going to make it into this RGBA image。

 And then we're going to pass that image array back into the fix resolution buffer viewer。



![](img/bb412fc545e07a2acf0d9da61331c993_63.png)

 which deposits it in a canvas and then renders the image。 If we change the color map， I've。



![](img/bb412fc545e07a2acf0d9da61331c993_65.png)

 now highlighted this in red。 Nothing upstream of this needs to change。 So we don't actually。

 have to interact -- we don't have to interact at all with the variable mesh or the fix resolution。

 buffer because we didn't change where the view was。 So what this is going to do is send。

 the data array back through the color maps WebAssembly function。 It's going to change。

 the image array and the rendered image。 If we do a canvas interaction though， we're。



![](img/bb412fc545e07a2acf0d9da61331c993_67.png)

 going to be moving the fix resolution buffer around in the variable mesh。 So the view width。



![](img/bb412fc545e07a2acf0d9da61331c993_69.png)

 this is if we change the -- if we zoom in， then that's going to change where the fix。

 resolution buffer is。 That's going to consequently change the data array， the image array and then。



![](img/bb412fc545e07a2acf0d9da61331c993_71.png)

 the rendered image。 So I said -- I just mentioned that we did this stuff in WebAssembly but I。

 didn't really say what WebAssembly was。 So WebAssembly is what a lot of the Web is built， on。

 It's a language that's supposed to work seamlessly with JavaScript but it's the performance。

 important parts of the Web。 So instead of using JavaScript and serializing to JSON all， of our data。

 we can put it directly in WebAssembly if we build custom WebAssembly modules。 But。

 because WebAssembly was designed with interacting with JavaScript in mind， these two can seamlessly。

 interact together。 We also have a sandbox memory environment so all of our calculations are。

 going to be done in the browser and it's not going to happen anywhere else。 And this reduces。

 that T client that I talked about in that equation earlier。 And why Rust？ Well， so you。

 can compile into WebAssembly from a lot of languages from C or C++。 So I have never programmed。

 before this in Rust or JavaScript and Rust was extremely approachable。 It had a pretty。

 low time to get up to speed。 It was super fun。 I didn't expect that。 I don't know。 And。

 it's performant。 It's designed with compiling to WebAssembly in mind。 So to do this， to。



![](img/bb412fc545e07a2acf0d9da61331c993_73.png)

 create our functions in WebAssembly， we can annotate our -- this is in Rust so we can annotate。

 our functions with this WasmBinGen and this is saying we want to make these functions available。



![](img/bb412fc545e07a2acf0d9da61331c993_75.png)

 to JavaScript from WebAssembly。 Then when we compile that， we get an automatically created。



![](img/bb412fc545e07a2acf0d9da61331c993_77.png)

 JavaScript file and this is kind of what that structure， data structure is going to look。

 like when exposed from JavaScript。 Another package that we found very useful is Wasmpack。



![](img/bb412fc545e07a2acf0d9da61331c993_79.png)

 So this actually compiles all your Rust code into WebAssembly and then packages up in a。

 package that you can put on npm。 So it's super easy。 You just upload it and none of your users。

 really have to deal with compiling to WebAssembly from Rust or anything like that。 They just get。

 to download the npm package that's associated with it。 And this is actually me compiling our。

 project on my machine。 And there's some cute emojis that are also included which is pretty， cool。



![](img/bb412fc545e07a2acf0d9da61331c993_81.png)

 So I have a demo of a larger data set。 I just showed you like a sample data set from YT。



![](img/bb412fc545e07a2acf0d9da61331c993_83.png)

 So we have a couple of different things here。 This in particular is from a simulation of。

 a population two star which is like the second generation of stars that's formed after the。

 really light hydrogen helium based stars。

![](img/bb412fc545e07a2acf0d9da61331c993_85.png)

 And I'm loading this in the original data set。 So I mentioned that we're taking chunks of， data。

 The original data set is several hundred gigabytes of data。 We pulled a slice down for。

 this particular chunk。 So if I do the log， I can see this data set。 I can also change the。



![](img/bb412fc545e07a2acf0d9da61331c993_87.png)

 limits so it might be a little easier for you to see。 Maybe。 And I can do the same thing。



![](img/bb412fc545e07a2acf0d9da61331c993_89.png)

 just before。 So the slice is quite a bit smaller than the original data set。 But this。



![](img/bb412fc545e07a2acf0d9da61331c993_91.png)

 is because we made this into a widget， we can also leverage all the functionality of， the widgets。

 So we can link for example another field。 I've plotted density here。 But I can。



![](img/bb412fc545e07a2acf0d9da61331c993_93.png)

![](img/bb412fc545e07a2acf0d9da61331c993_94.png)

 link it。 There's another field in this particular simulation of temperature of this star forming。



![](img/bb412fc545e07a2acf0d9da61331c993_96.png)

 So I'm going to first create a slider that allows me to see things in log scale because。



![](img/bb412fc545e07a2acf0d9da61331c993_98.png)

 I know this data set is very sparse。 And then so I want to zoom in really far。 And then。

 I'm going to create a temperature one as well。 So let's see what happens。 Okay。 So let's。



![](img/bb412fc545e07a2acf0d9da61331c993_100.png)

![](img/bb412fc545e07a2acf0d9da61331c993_101.png)

 say I decide， okay， I really hate this color map on the other side。 I've now linked the。



![](img/bb412fc545e07a2acf0d9da61331c993_103.png)

 field on both sides so I can do a log and we can see both of them。 And this looks pretty， cool。

 These are really different。 But I can change the color map just using the trait。



![](img/bb412fc545e07a2acf0d9da61331c993_105.png)

 let's。 And then I can move these around as well。 And I can click to a new center that might。

 interest me。 And do that。 I also can use a projection。 So YT has tons and tons of really。



![](img/bb412fc545e07a2acf0d9da61331c993_107.png)

 interesting ways that you can explore your data that haven't been accessible in this， interactive。

 this directive in interactive way。 So this is doing everything I just did， in one giant cell。

 So I'm sorry it's like very much a wall of text。 And it's going to。

 take a little bit because I'm doing a projection instead of a slice which actually collapses。

 all of the data and brings out features from all the dimensions。 I've been showing XY slices。

 so far but this is including， this is trying to pull out some of the z dimensional data。



![](img/bb412fc545e07a2acf0d9da61331c993_109.png)

 Okay， so I have this。 These are pretty interesting。

 So let's say I think this is a pretty interesting， part。 I can start zooming。

 And this goes way faster than if I was doing this with anything。



![](img/bb412fc545e07a2acf0d9da61331c993_111.png)

 else。 If I was doing this with straight Python， I wouldn't be able to do this and I wouldn't。



![](img/bb412fc545e07a2acf0d9da61331c993_113.png)

 be able to interact this easily with my data set。 Oops， sorry。 So we do have some limitations。



![](img/bb412fc545e07a2acf0d9da61331c993_115.png)

![](img/bb412fc545e07a2acf0d9da61331c993_116.png)

![](img/bb412fc545e07a2acf0d9da61331c993_117.png)

 of this widget。 It requires a 2D data slice。 You just saw that。 I talked a little bit about， it。

 So we can't fully interact in 3D yet。 And that's not a trivial change。 So that's。

 something that we're hoping to do in the future。 There's also potential for data sizes。 I've。

 shown this。 I've shown some pretty large data sets and we haven't reached a limit but it， exists。

 And we have limited functionality。 This is nowhere near。 The ability of a lot。

 of other interactive tools。 But this is the first web assembly that we know。 And it requires。

 multiple maintenance and packages and package ecosystems。 This is non-trivial and can be kind。

 of rough sometimes。 And it's still really early in development。 Moving forward， we want。

 to broaden the functionality。 We want to make it so it's even more intuitive for users to， use。

 We want to build out functionality with YT。 YT has all these cool features that we're。

 not exposing yet。 And we want to restructure the widget to enhance performance even more。

 There's some links。 I'm going to tweet this -- the slides to this talk。 If you're really。

 interested afterwards， you can go。 These are all linked to everything you're interested， in。

 And I want to give Louie Erber a shout out。 He gave a poster on build -- restructuring。

 some of your backends from seed arrest。 Also here at SciPy。 And we -- you can install this。



![](img/bb412fc545e07a2acf0d9da61331c993_119.png)

![](img/bb412fc545e07a2acf0d9da61331c993_120.png)

 very easy。 We have -- as of this morning， we have this widget on pi， pi。 And you don't。



![](img/bb412fc545e07a2acf0d9da61331c993_122.png)

 have to compile to rest。 And I'd like to thank the following individuals。 Matt Turk really。

 helped me with this。 Nathaniel Clazen did a lot of the early feasibility studies of this， work。

 Nathan Goldbound and Kastrich Helvallik helped me debug a lot of things。 I'm just going。

 to let you know that debugging in three languages sucks。 Also Britain Smith， he did -- he supplied。

 the data for these larger -- these -- the pop two data set。 And Katie Hoe is my great friend。



![](img/bb412fc545e07a2acf0d9da61331c993_124.png)

 and listened to the practice talk for this。 And I'd be happy to take any questions。 [ Applause ]。

 Great。 So I think we have time for one question。 Yeah。 Thank you very much。 Great talk。 Thank you。

 Yeah。 You talk a lot about the application side of it， the programming。 But as a user。

 support or a consultant， my worry is usually about the network， the memory。 So how much。

 does the memory count in serving as a bottleneck if you are computing from the HPC from the。

 server versus the client？ And how much memory do you need？ Because all the manipulations。

 you are doing that you're doing with the widget， how much memory do you need？ And at what point。

 do you have some sort of bottleneck？ Yeah。 So I have not done a full benchmark of when。

 we reach a bottleneck。 We know it exists， but I don't have something off the top of my head。

 for that。 I will say that this very large data set is a pretty good example of the types。

 of data sets that people would be interested in。 So we're pulling that slice down。 That slice。

 We saw the projection was like several hundred megabytes。 And that was directly in the browser。

 But I didn't pull a full 3D data set into the browser， so I don't know exactly what the。

 limit is yet。 And maybe one more question。 Yep。 Thank you for the nice talk。 Thank you。

 Question about transferring the data between JavaScript and the Web Assembly and doing。

 it for scientific data and scientific data types and bigger arrays。 Do you have any thoughts。

 or ideas on how to do that the best way to do that going forward？ So actually because。

 rest and Web Assembly are -- Web Assembly and JavaScript are designed to work together。

 We're actually just passing the pointer of the Web Assembly data through JavaScript。 We。

 have like -- we're using clamped arrays。 We don't have the like serialization to JSON。

 So it's actually like very friendly to transfer the data between JavaScript and Web Assembly。

 The hard part is getting it down into the Web Assembly in the first place。 Did that。

 answer your question？ Okay。 I'll be at the sprints tomorrow。 Also， if any of you have。

 any questions or like want to play around with this or something like that。 Thanks。 [APPLAUSE]。

 [BLANK_AUDIO]。