# P28：SciPy 2018视频专辑 (P28. Resurrecting Ancient Proteins in Python _ SciPy 2018 _ Zach - GalileoHua - BV1TE411n7Ny

 I'm going to tell you a little bit about resurrecting ancient proteins in Python。

 That's my Twitter handle and my GitHub account。 If you want to check this out。

 these slides are on GitHub， but I need to make a Git push， to update them。

 So they're a little bit out of date。 Really quick one of shout out to Jeremy Anderson。

 He couldn't be here today to help me give this talk， but he was very supportive and。

 putting this together。 So I want to give him credit。 All right。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_1.png)

 Can you guys hear me okay？ All right， cool。 So I'll start with the question of who am I。

 So how many people in this room are biologists？ Raise your hand。

 How many of you guys study evolutionary biology？ Very few of you good。

 I'll apologize to the couple in the back because I am not really an evolutionary biologist and。

 I don't know if I'm qualified to give this talk at all。 It's kind of a side hobby of mine that I do。

 And in trying to go after that side hobby， I found that the software out there for this。

 particular field is a little bit tricky to use。 And so a lot of this talk is trying to develop tools and make that a little simpler。

 So I started as a condensed matter physicist at Cal Poly San Luis Bispo and I was not a。

 good experimentalist。 So I moved into software and like all good physicists。

 I started using MATLAB at the time， and then learned about a free alternative to that Python。

 And while I was there， I ran into Dr。 Brian Granger。 He was actually my quantum mechanics professor。

 And some of you may know him。 He was basically the first developer of the IPython notebook。

 And so while I was there， I got the opportunity to talk with him one-on-one and he offered me。

 the opportunity to work as a core developer of the IPython notebook back in 2012。

 And so I worked for that for a year and then for better or for worse， I decided to go to。

 graduate school at the University of Oregon where I wandered into an evolutionary biophysics。

 lab with very little background in that field。 So I kind of masquemarade myself as a physicist and an evolutionary biologist and I guess a。

 software developer。 So I'm not sure if I'm good at any of them。

 but together they make a lethal combination。

![](img/8f08c26f76ecd14129d7e0ab7949ecb3_3.png)

 All right。 So I want to start up from what the acknowledgments of my lab just because it really is through。

 them that I've learned the most in graduate school。 So that's my advisor， Mike Harms。

 That's the lab that I work in and big。 And then everyone else that you see there are the people that I work with from day to。

 day， their grad students in that lab。 Some of them have graduated and move on。

 Jeremy Anderson is the guy that I mentioned at the beginning of the top who helped me put。

 this together。 I also got to give a shout out to Beer Theory Society。

 It's a group of grad students that get together once a week to drink beer and talk about science。

 All right， and I should say I just defended my thesis three weeks ago。 So Mike， fresh， thank you。

 That was to say that when I submitted my talk to SciPy in March， I didn't know I was。

 going to defend in June。 And so some of the software I'm going to propose today is very。

 very alpha because I proposed。

![](img/8f08c26f76ecd14129d7e0ab7949ecb3_5.png)

 it before it was ready。 But yeah， we'll talk about that。

 So that's my part of the warning is that you're going to be looking at some really alpha stuff。

 But I think that the ideas that emerge from it still hold。

 And so this is kind of a proposal to the evolutionary biology field about how we can make。

 phylogenetics， evolutionary biology， and data analysis like that a little bit easier， reproducible。

 and actually update it。 A lot of the software you see in this field is about 20 years old。

 And so we're just now starting to put a modern face on it。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_7.png)

 So in the harm's lab， we're interested in studying protein evolution。

 And the reason why is life has evolved a vast array of proteins that execute all the necessary。

 functions of life。 This is an incredible process。 If you're not sure what a protein is， it's OK。

 I didn't as a physicist。 My thought or my definition of a protein is just a linear chain of these subunits molecules。

 we call amino acids that fold up into these beautiful three dimensional structures。

 And they become little molecular machines that can carry out all the processes across all。

 living organisms。 And it's amazing that they can do that because evolution has had to innovate and diversify。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_9.png)

 and create this vast array to meet all the demands of life over the past billions of， years。

 And so just to even begin to tease apart that question we got to ask， how do they just。

 evolve just a simple change and function， innovate just a little bit。

 And so that's where I'm going to start my question today。

 And I'm going to focus on these steroid hormone receptors。 This is not my data。

 This is not even my work。 I just wanted to show that we could go back into a paper in the literature and reproduce。

 their results。 And so I'm not by no means an expert in this protein。

 But I'll give you a little intro。 So these guys are important for regulating all kinds of transcription on DNA。

 And the way they work is they wait for a hormone molecule to come by， bind onto these proteins。

 That induces a conformational change of these proteins that then allow them to bind onto， DNA。

 And by doing that it allows downstream transcription of the DNA。

 So you can target a bunch of different genes that way and get all kinds of things out the。

 other end。 There are two classes of these receptors， the estrogen receptor。

 And I'm going to call them the non-aromatic steroid receptors。

 So this is kind of a whole class in their own。 But what's interesting about these is they both recognize different hormone molecules。

 that turn on their function for transcribing， allowing transcription。

 But they recognize totally different molecules。 But they're very similar in structure and in sequence。

 So it's very interesting that there's very little difference between these two molecules。

 and yet they differentiate very highly at the level of transcription， allowing transcription。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_11.png)

 and recognizing molecules at the front end。 And so this implies that they have a common ancestor because of their similarities that。

 arose way back in the day and then have recently diverged into these two classes。

 And so that's the question that these people that I have in the citations in the bottom。

 right corner are probing。 And so to do that， they use a science known as phylogenetics where you pull these sequences。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_13.png)

 So we have a bunch of sequences of these particular proteins from various different organisms。

 thanks to the awesome technology that we've had to be able to sequence a lot of organisms， genomes。

 And you can actually go and look in those genomes， pull out the sequences for these proteins。

 from these databases。 So I'm doing that for our estrogen receptors and our steroid receptors。

 pulling out those， sequences， they're longer than this。

 I'm just showing a small chunk of these proteins。 And you can align them using some alignment software。

 sequence alignment software， all， together。 And then so each one of these rows I should say represents a different estrogen receptor。

 protein in a different species。 And so this is across various different species。

 And you can build a relationship， hierarchy， topology tree that relates each of these proteins to。

 one another based on just their sequence information， how similar they are to one another。

 And so you can get these beautiful topologies that also show the relationship between the。

 two classes of receptors。 And I won't go into the details about how this is done。

 This is not the point of this talk。 I'll be happy to talk about it afterwards。

 What's really interesting is by doing this you can find and infer a node in which you saw。

 divergence occur。 And so this would be the most likely point in time， so the X axis on this is time。

 the。

![](img/8f08c26f76ecd14129d7e0ab7949ecb3_15.png)

 most likely point in time that these two classes diverge。

 And then you can actually use that information， that sequence information to try to infer the。

 sequence of that node。 This is a technique known as ancestral sequence reconstruction。

 which just runs the clock backwards， looking at the sequences at each node along the way to then infer this ancestor。

 And then you can get that sequence from these programs， synthesize that through a process。

 we call protein resurrection， which is take a brief moment to really appreciate this because。

 I'll show later this， these proteins are upwards of 200 million years old， because these proteins。

 only exist in， or this goes back to the earliest of all vertebrates that you see here。

 And you're resurrecting these things in lab that you don't see today in nature。

 And then you can measure their function and see exactly what that protein would have been。

 doing at that state in time。 And then you can start to characterize what changes occurred along this node towards these。

 diverging branches， and what are the mutations that are responsible for these new innovation。

 and function。

![](img/8f08c26f76ecd14129d7e0ab7949ecb3_17.png)

 So how is ancestral sequence reconstruction and phylogenetics overall done？

 It's usually doing these four steps。 You gather sequences from some sort of database。

 You align the sequences using some sequence alignment tool。

 You build a phylogenetic tree that infers relationships between those aligned sequences。

 and then you reconstruct the ancestors based on that tree topology。

 Sounds simple because it's only four steps。 Except that each one of these steps has multiple programs that can do them。

 And each one of these programs are written in various different low-level languages that。

 don't always compile on certain machines and don't work cross-platform。

 You can get different results between different versions。

 Some of them take different input and output depending on the version。

 So you have the problem of the multiple different tools you have to choose from and know how。

 to put your data into its format。 And then over here on this right side I'm showing all the formats。

 the file formats you， have to deal with as a bioinformatician and if you're a bioinformatics person you probably。

 know all these。 The top little chunk is all the sequencing plus many more than that actually。

 And then all the different tree formats and even within a single tree format you can have。

 different requirements of needing node labels versus branch lengths and things like that。

 So there's three categories of problems that arise from all this that make a huge barrier。

 for people to get into file and genetics an evolutionary biology。

 And that is one you have to worry about compiling programs on different machines。

 And that's really troubling。 Dealing with multiple formats and being able to convert a lot of time is wasted on just。

 trying to manage these formats and putting your data in the format that's necessary。

 And then like I said all of these come often times with just a command line interface in。

 the written in C++ or Java or some sort of program that you can't easily install and。

 manage and interact with in a way that's reproducible and easy to install on multiple， machines。

 So there's no Python at least as of 10 years ago。

![](img/8f08c26f76ecd14129d7e0ab7949ecb3_19.png)

 So this is a large barrier to evolutionary biologists wanting to do this analysis and。

 they really have to spend a lot of time focusing on the technicality rather than the science。

 itself。 So recently there's been a lot of movement to make this better and I have to give a huge。

 shout out。 I actually didn't really explore this until I started thinking about this talk but Conda。

 obviously has been a big lifesaver for a lot of people。

 There's specifically there's this channel under Conda called Biokonda that makes things。

 like all those programs I listed on that left side on that other slide Conda installable。

 across platforms which is huge because they used to spend hours just trying to get that。

 to work on your machine。 The file format conversion has improved a little bit。

 There's tools like BioPython that you may use， Dendropie which handles tree data and。

 all these tools are awesome and there's a couple of more in Python。

 All of them are great for reading in parsing files and maybe spitting them out to different。

 formats。 The troubling thing though is that they still require a pretty deep knowledge of the tools。

 themselves to get them up and working and you oftentimes take 10s to 20 lines code just。

 to get you to convert formats。 And so I kind of treat this as kind of like what Ralph said in his keynote today which was。

 I view these as like the low level interface in Python that you will build better interfaces。

 on top of。 So it's kind of the core functionality that you need just to get started and then you。

 can build interfaces。 And that's what's missing right now is this high level interface for doing this kind of。

 science。 And that's the point of this talk。

![](img/8f08c26f76ecd14129d7e0ab7949ecb3_21.png)

 So what do I want？ I want to spend less time converting formats because again this is a hobby for me。

 not my， full time job。 So I don't want to spend time doing this。

 I want a familiar front end that we're all used to that allows me to explore this kind。

 of data and run these analyses very easy and interactively。

 And then I want something that's reproducible， something that maybe can open up in a Jupyter。

 notebook that I can pass off to people to recreate。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_23.png)

 So with that I'm going to introduce my first piece of software that I'll say is in beta。

 version not alpha version。 And this is a tool called Philo Pandas。

 And this is defined as the Pandas data frame for phylogenetic data。

 And the best way that I can show this is actually just showing you it in real time。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_25.png)

 So we're going to live code a little bit， which never works but roll with me here。 All right。

 So like I said， it's just a Pandas data frame that has a little bit of extra core functionality。

 But I think you'll find that core functionality pretty powerful。

 So you just import it just like you do Pandas。 And just like Pandas。

 all this has done is defined a few extra read calls。 If you know Pandas。

 Pandas has all these different read calls from different formats。

 That's the same thing you get here。 So if I go inside here。

 you can see that I've added a bunch of different read formats that。

 are specific for all those formats you need to use those tools in previous slides。

 So FASTA is a very popular one， Nexus， Fileip， FastQ and so on。 So it has all those functionality。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_27.png)

 So I'm just going to show in action I have the same data presented in different formats。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_29.png)

 here。 And you can just read them in。 You get a nice little data frame out the other end。

 It defines a few columns for you， some description and a label and then specifically the sequence。

 that's really important。 It creates a unique ID for it as well， but that's for internal purposes。

 It can do various different formats。 So Clustow and Fileip。

 you see you essentially get the same data frame depending on the data， to write in。

 The next thing that you get， of course， is write functions。 That's what you need。

 So if you're going to read them in， you better be able to write it out。

 The way it does this is it leverages Pandas' Accessor Extension API that was just recently。

 put into Pandas。 If you're not familiar with that， I can talk about it。

 But what this does is it allows you to attach an object with extra methods that are specific。

 to your use case and register them onto a data frame。 So that's what I'm doing here。

 This Accessor that I created just has the keyword "filo" that you see here。 And by doing that。

 I get all my， if you just call data frame。filo。2， you can get all these。

 different formats you can write out to。 And so， for example， if I call file of that too fasta。

 I don't give it a file name， it， will just return a string。

 I can see it wrote that data frame right out to a faster string。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_31.png)

 This makes converting formats really easy。

![](img/8f08c26f76ecd14129d7e0ab7949ecb3_33.png)

 I can read in a fileip and I can spit out a fasta file。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_35.png)

 So that's really convenient。 The other thing that Fileip does is it doesn't just read sequencing data。

 it also reads tree， data。 And this is unique because this doesn't exist in a lot of ways where you can flatten tree。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_37.png)

 data that looks like this is really a non-human readable format。

 And it can turn it into a flattened format just like that。

 Where you can see that now we have columns that describe the parent that you come from。

 as a node in this tree and then the type of node you are， whether you're at the leafs。

 or you're an internal node。 Because it's a PANDAS data frame， you get all the cool slicing options。

 So I just called the leafs， right？ And I just standard PANDAS syntax and all of a sudden I can just slice up the elements。

 that I care about in that particular PANDAS data frame。 And to take it one step further。

 here's where the real magic happens is that you don't just。

 have to read in one format into a single data frame。

 You can read in multiple pieces of information into a single data frame and it knows how。

 to process that。 Specifically， imagine you read sequence data and then you have tree data that describes。

 how those sequences go together。 It all comes in so I'm going to read the sequence here。

 then read the tree data and show you， the data frame。

 And what you see is that the leafs of the tree all have sequences now while the internal。

 nodes don't。 Because the tree data doesn't have that yet， right？

 So we just compressed these two complex data sets right onto a single data frame that's。

 easy to map between。 So that's file of PANDAS that's the intro。 I'll show you why this is powerful。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_39.png)

 First of all， it kind of inadvertently and by accident， we created a grammar of file， of genetics。

 The reason why this is useful is if you've heard the term of grammar of something is。

 you can easily make views for a grammar using tools。 So last year。

 Jason Groud and I got to work on this fast extension so you actually view。

 your sequences as this colored alignment that you see here。

 The main thing is that if you've heard of a tool called Vega， which describes a grammar。

 of visualization， you can easily port this grammar of file of genetics onto those visualizations。

 and we can build trees in Vega really easily。

![](img/8f08c26f76ecd14129d7e0ab7949ecb3_41.png)

 And these are interactive by default because Vega is an interactive library。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_43.png)

 So to show that in action， I'll just read in that same data that I showed you on the。

 last one and I'll just visualize it as a Vega tree。

 And now this tool has this fast interactivity that you get from Vega， which is really， really。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_45.png)

![](img/8f08c26f76ecd14129d7e0ab7949ecb3_46.png)

 quick if you've ever done any tree visualizing software like Fig Tree， it's very slow and， clunky。

 This is just right in your IPython notebook or your Jupyter notebook and it's using the。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_48.png)

 modern power of something like Vega。

![](img/8f08c26f76ecd14129d7e0ab7949ecb3_50.png)

 And then of course the fast viewer that I showed you on another page， all in a single， notebook。

 The other thing that it lets you do is by having file of pandas or something like file。

 of pandas at your core， you can build interactive interfaces for file of genetics on top of that。

 where the whole purpose is just to populate that data frame。

 And then you get things like file of Vega or these visualization software for free。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_52.png)

 And so just as a， again， alpha alpha alpha version to show this and demonstrate this。

 I created this package called file of genetics， which now does the entire pipeline that I。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_54.png)

 showed you in earlier slides just following a simple Jupyter notebook set of calls。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_56.png)

 So this project， if we just import it， this is all available on GitHub as well。

 We'll just initialize this little thing I call a file of genetic project class。

 I'll just read in data using file of pandas。

![](img/8f08c26f76ecd14129d7e0ab7949ecb3_58.png)

 So I get there's my data that you see there。 So this is just sequence data。

 I'm going to go ahead and compute a tree。 So underneath the hood all this is doing is using file of pandas to construct the data。

 in the format that's necessary to then pipe it out to some external tool。

 One of those external tools tools I showed you earlier。

 You do that take a few seconds and what you'll see if we show that data frame is now we have。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_60.png)

 we populated that data frame with the tree data that we just computed。

 So now we have nodes that you see here and parents telling you which node where your。

 leaves are going to and how they're related。 And from that then you can go ahead and display that tree in real time in a nice interactive。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_62.png)

 way just like I did before。 You can even take this a step further and reconstruct these ancestors of this particular。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_64.png)

 tree which now you'll see if I compute that our nodes now have these extra sequence columns。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_66.png)

 which are the reconstructed sequences for this particular example。

 And because it's pandas you can do cool things like I just want to look at my reconstructed。

 sequences and I can just slice those out directly leveraging pandas' API。

 So there's our inferred ancestral sequences and then if you really want you can spit those。

 out faster。 Alright， so the whole promise of this was that I was going to tell you about this SR evolution。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_68.png)

![](img/8f08c26f76ecd14129d7e0ab7949ecb3_69.png)

 using the ancestral sequence reconstruction of silly steroid receptors。

 So I was going to try to do this in real time but it turns out that the computation takes。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_71.png)

 about 40 minutes。 So I won't make you wait。 So what I did was in this repo I'm going to import my phylogenetics project。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_73.png)

 Here's the code to actually repeat it。 It's like six lines of code to do a full ancestral sequence reconstruction。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_75.png)

 I'm just going to load that already saved project in and there's my fully reconstructed。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_77.png)

 ancestors。 You can see the sequences right here in this column and I can take that and visualize the。

 tree and it's going to be really ugly。 Bugs pre-alpha alpha。 I'll just compress this for a second。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_79.png)

 And so you can see the tree right here which is really ugly to look at right now but what's。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_81.png)

 really cool is if you， I promise if you start this long enough I'm running out of time。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_83.png)

 This is what their tree looks like and it looks exactly the same。 We recreated their exact results。

 This is the paper， a tree from their paper。 Just again a little fact right here。

 This is the ancestor that they were most interested in。

 This is the one that tells you this split from estrogen receptors to steroid receptors。

 That's a 300 million year old protein that they reconstructed in lab and they identified。

 using this process。

![](img/8f08c26f76ecd14129d7e0ab7949ecb3_85.png)

 So just to simplify that tree down using the colors from the first slide。

 This is basically how you can summarize it。 Our whole class of estrogen receptors were out here at the top and it turned out that。

 by doing this reconstruction they measured the farthest last common ancestor of this， entire tree。

 This very very very old protein and they found that it looked like an estrogen receptor and。

 that over the course of about 100 million years it evolved or it actually duplicated。

 So it went through gene duplication which means it made a copy of the gene and one was constrained。

 to keep the same function of doing this estrogen receptor。

 The other one was allowed to diverge and learn these other ways to receive other hormone， molecules。

 So that's what you're seeing here in green。 I won't get into the details because I don't have time。

 But they actually characterized mutations that occurred between these two nodes and identified。

 the key players that led to this innovation of function。

 So it looks like the oldest ancestor was an estrogen receptor。

 I encourage you to go read those papers。

![](img/8f08c26f76ecd14129d7e0ab7949ecb3_87.png)

 It's really interesting stuff。 All right。 So with that it's time to make phylogenetics interactive。

 We can do it。 The technology is there and it's not that hard with the APIs that are available to us。

 I think phytopanus can help。 I'm obviously biased because I wrote it。

 But the main point is that it follows the interface that we all know。

 We use pandas regularly if you're a data scientist or a Python programmer。 And then， like I said。

 by accident we defined a grammar for phylogenetics that I think， could be really useful。

 And I am so open to criticism and conversation about that。

 Hopefully it can recruit people here to be interested。

 And then by doing that you can start using tools like Vega to visualize your data。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_89.png)

 So with that I'll say thank you。 And feel free to ping me on Twitter or whatever。

 So we have time for a few questions。 I'm going to let everybody raise hand and then I'm going to point so be patient with me。

 All right。 So I'm going to start here and then I'll come from that。 I think so。

 That was really cool。 So do you-- like I'm trying to get a sense of what you think the scope of your functionality。

 will be。 So do you plan on having sort of tree manipulation methods or would you imagine that would be。

 done before actually reading it in。 So for instance。

 like ladderizing the tree or rooting it or something like that。 Yeah。

 I totally think-- I think the final pandas will stay core。 Maybe I should say--。

 Final pandas will stay core to reading in writing out data and hopefully defining that。

 I think it's going to have to be like a format that we standardize。

 And then external tools like the file genetics package or like another tree package will actually。

 know how to map that and do things like ladderize a tree， figure out rooting processes。 And yeah。

 any type of computation you have to do on the tree， I think would be easy to。

 do once you have it in this format。 Yeah。 Okay。 First of all， it's a great work。

 And I'm working on the look at the sequence。 So it's a little bit different than the protein sequence。

 I'm just wondering if I want to apply this to the nucleotide sequence， first of all。

 how many number of six can handle， second， what makes them less of the sequence they， can handle？

 I don't know。 So I haven't actually like-- this is a fairly young project and it's been something that。

 I've only worked on recently。 Like I said， as a hobby really。

 So I haven't been able to test its limits。 Like how-- what kind of memory-- like what's it going to do on memory？

 Is it going to blow up your memory？ Is it going to be faster or slow at reading in large sequencing files？

 I'm not entirely sure。 So underneath the hood， all it is is BioPython。 That's what's reading in。

 So if BioPython can do it， this can do it。 It's just merely mapping it into a data frame。

 And then for the tree stuff， it's just using dendropi。 So the limits come from them。 And yeah。

 I think if this were to actually take off or it would be useful to anyone， I。

 think we can write a faster reading routine。 But yeah， so I don't know。

 But it works with nucleotide sequences， of course。 [INAUDIBLE]， Yes。 Yes。

 Dask has been like a hero for me in grad school。 Yeah， so that's kind of the reason。

 And like with technologies with Arrow moving forward， I mean， just--。

 I feel like if you link into the data frame at all， you're in a pretty good position。 Yeah。

 to really leverage modern software。 So when you're reconstructing an ancestor。

 certainly there's some uncertainty in the exact， sequences。 Yes。

 That any way to communicate the uncertainty， like you're more certain about some spots， than others。

 Yes。 Yeah。 So I didn't go into any of the details of the math on this。

 But the ancestral sequence reconstruction software itself is actually doing a maximum。

 likelihood-- it's solving a maximum likelihood function。

 But it can't-- there's so many possible outcomes that it can't obviously find a global optimum。

 It just can't sample enough。 And so it's doing a lot of little local gradient descents and then flipping into some other。

 place and doing the same thing。 And so you're getting a lot of what looks like maximum likelihood solutions。

 And then you're sampling from the maximum likelihood solutions。 And so you do have probabilities。

 posterior probabilities， for each residue， each site。 And so actually in that。

 if you looked at the columns， we have alternative sequences we propose。

 where there were residues that were low probability。

 Like our maximum probability was relatively low。 And so we flip that to the next best probability。

 So there's all kinds of tricks to try to characterize uncertainty in ancestral sequence reconstruction。

 None of them are good。 But I think it's something a lot of people are thinking about。

 But it's probably still a few years away because it's a hard problem。 Yeah。

 Thanks for the presentation。 Right here。 I'm the guy talking to you。 A little bit off the software。

 I'm just curious when you resurrect a 300 million year old protein。

 How do you ensure it's folded properly when you're testing its activity？ Yeah。

 that's a great question。 So they actually have a crystal structure of that protein。

 So in terms of whether you know it's folding properly， I think if it looks like your derived。

 sequences， the tips of your tree， it's a pretty good indication that that's a decent reconstruction。

 And it's functional。 What's interesting is they showed that it functioned just like the other proteins。

 It looked very similar。 In that particular story， I didn't say this。

 but it was more-- they used the word promiscuous， and that it could bind to a bunch of different hormones and then it specialized over time。

 Yeah。 So I mean， there's no-- maybe it could have taken a really weird， you know， back 300 million。

 years ago。 It had also something else that helped it fold in a different way。 That's possible。

 I think in that one， they're pretty certain just because-- I mean， the odds of it actually--。

 What's interesting is if you go just a little bit further out on the maximum likelihood。

 residues that we were talking about， it doesn't fold。

 So most sequences around it are actually completely non-functional or they don't fold。

 They're just in viable sequences。 So it's amazing that it works， I guess， would be my statement。

 It would be like the fact that you can't just throw amino acids in a test tube and expect。

 them to be a functional protein。 And the fact that these seem to recreate reproducibly。

 they're able to reproduce or recreate proteins， that work is a good indication it's doing something。

 And I guess it kind of all sorts。 Well， sorry。 We just-- you can carry on talking。

 I know it's a great conversation， but we have to end。



![](img/8f08c26f76ecd14129d7e0ab7949ecb3_91.png)

 Thank you so much。 Thank you。 Thanks for coming。 [applause]， (applause)， All right。

