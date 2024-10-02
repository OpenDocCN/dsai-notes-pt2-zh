# P55：SciPy 2018视频专辑 (P55. Keynote - SciPy 1.0 and Beyond - A Story of Code and Commun - GalileoHua - BV1TE411n7Ny

 It's great to be here。 I'm a first time or two， so come say hi after my talk。 I agree。

 it is an amazing community。 I'm from Holland originally， so I've been to a lot of Euro-side pies。

 I came here last night， only sat down at breakfast this morning and immediately met three people that I've been talking with for years。

 I'm glad to be here in this invitation。 I'm glad to be here。 I've got this invitation。

 I probably already asked who knows what's pie pie is。

 I'm wondering who has used pie pie in the last year， directly？ About half or so。

 I think that's a good thing。 Five years ago， I think a lot more people would have stuck up their hands。

 I see that the community has grown， but also we've got a lot more high-level packages that may use pie pie under the hood。

 but you actually don't need to go into side pie anymore。

 You can do things with a few lines of code that you would have had to write a page of code for a while ago。

 What is side pie？ I'll start with this slightly cryptic quote from Travis。

 who was one of the founders of side pie。 He said， "Side pie was a distribution masquerading as a library。

"， Basically， what happened there is we had an array object before NumPy， numeric。

 and then a bunch of people started using that for science。 They stuck their heads together and said。

 "Let's put everything in a bundle and call it side pie。"。

 It's not a library like most other ones with a single purpose。 It does a lot of different things。

 My own definition would be a little bit more simple。

 It's basically fundamental tools for scientific computing。

 You've got an array in NumPy and any kind of algorithm that applies to many different scientific fields probably ended up in side pie。

 Close pie。 Yes， I can。 For all those of you who don't use side pie。

 I'll give a very brief tour of what's actually in it。 If you go to the website。

 you'll see there are 16 sub-modules。 It won't classify them very much。

 but for me they fall in five categories。 The first one is math building blocks。

 If you've done a physics or chemistry or some kind of engineering degree。

 these math building blocks probably cover most of what you learned in that whole degree。

 There's linear algebra， dense and with sparse arrays。

 Then there's Fourier transforms and special functions。

 That's the lowest level stuff that you can find in side pie。

 Then you've got the biggest chunk that's numerical algorithms。 So numerical optimization。

 if I have a function， I find the optimal value for it。 Then there's integration。

 both integration of functions and ordinary differential equations。 And then interpolation。

 which is basically if I have a bunch of data points but I want to know the value somewhere in between。

 how do you get that？ You run an interpolation routine from side pie。 Keeps on going。

 There's more numerical algorithms clustering。 So basically how do I group data？

 The very basics of it are in side pie。 If you want to do a lot with it。

 you're probably better off using side get learn because there's a whole zoo of clustering algorithms in side get learn。

 They tend to be a bit more performant as well。 But for the basics and making the picture that I showed there。

 side pie is a pretty good bet。 So it even does some plotting。

 I didn't put that on but that's about the only plot that it does。 Then graph algorithms。

 so that solves problems for you。 If I have to visit 10 cities and I know the distance between each two cities。

 what's the shortest path to visit all 10？ So something you probably need less often but if you need it。

 it's quite powerful。 The last one， computational geometry。 So if you have an object。

 let's say a 3D object like this thing and I have a bunch of points that I measured on the surface。

 how do I calculate the surrounding volume of it？ It doesn't have to be a 3D object。

 can be any dimension， but that's a computational geometry。 Then， I said before。

 the data structure is numpy and the algorithms are side pie。 It's not really like that。

 There are actually two quite important data structures in side pie。 The first one is sparse arrays。

 sparse matrices。 We got Hamier talking about sparse arrays in a later today。

 Sparse matrices are basically matrices that mostly filled with zeros and once in a while there's a value that's nonzero。

 So they have their own data structure because you don't need to store all those zeros。

 So you only need to store what you have nonzero values and what that value is。

 That gives you a much more efficient representation so you can work with much bigger problems and still fit them into memory。

 This is mainly an important data structure because large parts of scikit learn are built on this。

 So scikit learn guides help us maintain it as well。 It's very useful。 The second one is kd trees。

 If you have a bunch of points unstructured in space and you want to write some algorithms where you need to know。

 the 10 closest points for every point。 That's when you would use something like a kd tree。

 What I think is the highest level of code available in SciPy is data analysis algorithms。 The first。

 probably the single biggest module in SciPy is statistics。

 There's about 100 probability distributions that you can use to draw random numbers from or probability density functions。

 Then there's hypothesis test so it includes most of the things you would have gotten in your undergraduate statistics degree。

 If you want more esoteric or fancy stuff that's why we have stats models。

 But SciPy does that covers a lot of what you would need in daily life。

 If you have signal processing， you want to filter them。 That's when you go to SciPy。signal。

 Last one， image processing。 The basics are in SciPy。

 Filtering things like edge detection and then scikit image。

 It's a great package built on top of SciPy as well。 Again。

 it's got more and fancier stuff available。 The last one。

 I'm probably missing a few things but the last book is utilities。

 The most important thing there is probably support for a lot of scientific data formats。

 This has been a lifesaver especially for me personally。

 I've worked in a company before that was dominated by people writing Matlab code。

 If you have to work with other people in a big engineering project。

 you can't go off and rewrite everything。 There's only two ways。

 You only write Matlab code yourself which is frustrating if you get to do Python at home。

 The other thing is you save wherever you can。 Matlab stuff to a binary file and you read it in。

 That's what SciPy supports。 If you're an astronomer， you have the same experience with IDL。

 There's a lot of these data formats。 I think everything except HGF5 which is large enough to and complex enough to have a few libraries of its own。

 It's not really much anything else fits in SciPy。 That's it in a very big nutshell in three minutes。

 I thought I would give a little bit of history because there's a lot of history。

 The first SciPy release is back in 2001。 Before I was even using it。

 I started becoming a user in 2004。 I still got the whole -- let's write NumPy。

 NumPy was named SciPy core at some point。 It lived in a SciPy repository until Travis took it out again。

 At that point， everything that was in SciPy except for some plotting。 In 2007。

 it's a bit limiting to have this one subversion repository that does， kind of everything。

 Let's create some psychics。 There were a lot of psychics that didn't really take off。

 We got some like scikit learned， image that's models that are。

 success stories in their own right now。 In 2008， the documentation marathon。

 this was actually where I got involved。 This was at that point we didn't have GitHub。

 We didn't have nice documentation。 It was kind of unapproachable compared to what it is today。

 The whole scientific Python ecosystem。 This was the first attempt at making it more approachable。

 There was a professor in Florida， a guy named Joe Harrington who needed to teach NumPy and。

 figure out that it was hard to do if things are not documented。 He said， I have $10。

000 worth of grant money。 Let's build a wiki editor。

 Wikipedia style where everyone can write documentation。

 Someone built that wiki editor and people started writing doc strings。 Within， I'd say。

 one summer NumPy went from the worst documented package。

 out there to being maybe not yet on par with commercial alternatives but not， too far away as well。

 How I got involved and I kind of liked the experience in the community and that's why I， stayed。

 I'm not sure if Joe is around。 I haven't heard from him much in the community lately but if you're here。

 Joe， come up to me， and buy your beer。 After that， we went to a six month release cycle。

 That's when I started as release manager。 At the point before me。

 David and I was extremely productive as well。 I'm not doing it anymore。 Nobody really stepped up。

 I'm a user for a while。 I've written some documentation。 Maybe I should do that。

 I didn't really know what I was in for。 It took me three months for me to get at first release out。

 It's been good since。 Then we moved to GitHub。 We were one of the first libraries to support Python 3。

 One of the first to adopt Travis CI with continuous integration。

 Then it took another four years before we finally sat in。 Now we have a version 1。0。 [Applause]。

 Why did it take so long？ 16 years is a long time in computing especially。

 I was now working forestry。 A tree grows in about 28 years in New Zealand and about 18 in Canada。

 Then it's okay。 In computing， it's a really long time。 Why now？

 There's probably a few reasons for it。 First of all， to get to one point though。

 that's when you have the impression something is stable。 Something is used in production。

 I think it was stable long before that。 There are many in every industry。

 there are mission critical products being built on top of， SciPy。

 You have NASA missions that use it。 You have the machines in which Intel prints computer chips having SciPy in them。

 You have hedge funds prototyping their algorithms。 You have Apple shipping it as part of Mac OS。

 Keep on going。 It's been stable for a while despite being called 0。x。 Also， calling something 0。19。

0 or something， that's a really terrible marketing。 It's not just SciPy that does this。

 You have pandas at version 0。23 right now。 I could learn at 0。21 or something。

 You have stats models at the same。 They all point something。 This is horrible marketing。

 I think two reasons。 One is institutional。 Someone has to stick their hand up and say。

 I think we should make a 1。0。 If there are reasons not to do it， let's just fix them right now。

 That's kind of a hard thing to do。 People don't like to have these discussions。

 They prefer to write code and have some fun。 The other one， I think for me。

 it was -- but actually made a list of what we should do before calling it 1。0。

 It was more about community than it was about code。 Some of these community aspects。

 the first thing I wrote down is we would like to have a governance structure。

 What that means simply said is you write down somewhere who makes decisions and how。

 If there is a conflict， how do you resolve it？ At the moment， we have a pretty simple structure。

 We have one called benevolent dictator for life， the same as Python。 So。

 sidebar has the benevolent dictator。 Then we have a steering committee of all the people who are regularly active。

 It doesn't really matter which structure you choose。 If you run a project。

 it's important that you choose one。 We've needed it exactly zero times so far inside by。

 Most decisions are made by consensus。 There are people who feel strong in another one。

 I don't really agree， but I'll step aside。 It's very often that there is an actual conflict。

 You don't want to be figuring out this governance structure when you do get a conflict。

 The other thing that matters is how you set it up。

 It doesn't really matter what you choose in the end。 Most things will work。

 But the process of deciding on it， you have to involve people and you have to take any of their concerns seriously。

 Then we have a code of conduct。 That took a long time as well。 Code of conduct。

 I don't think I've got to talk about why people need them。

 Whole talks have been given about that at many conferences。 But you need one。

 It needs to have a few attributes。 It needs to have a report or mechanism。 If something goes wrong。

 what do you do？ And many projects have that now。 What I see go wrong very often is that it's basically being pushed through or decided by a few people what exactly should be in it。

 Again， I think it's the process that's important。 It took a long time for Sci-Fi because there were a lot of people with concerns。

 You've got to take those seriously because otherwise you might invite new people into your community by having a code of conduct。

 But at the same time， you might push them away by introducing it in the wrong way。

 This requires basically talking。 A website or a mailing list is not always the best form for this。

 You might create multiple avenues for this。 Have an open call that anyone can come into。

 If there are people with serious concerns， just call them up one-on-one and talk for an hour and say what they are。

 Try to see their point of view and maybe invite them to co-write the whole thing。 In the end。

 we got a code of conduct that everybody was happy with。 At least everyone who spoke up。

 You never know。 You never say everyone。 But that was a pretty big achievement， I think。

 Then we have a roadmap。 A roadmap， I think， is important for a couple of reasons。

 It's a good place to document where you want to go。

 what are the big ticket items that you want to fix in your library or new issues or new features that you want to introduce。

 It matters to new contributors。 If they want to start somewhere random。

 unless you tell them this is the important place where we really need help。

 And it matters to companies。 If someone wants to sponsor your library。

 I want to give you money or people time to help improve it。 It's one of the first things to look at。

 It's not enough by itself that won't attract any sponsors， but if you don't have it。

 it's a good place for them to look at once and then these guys are not really serious。

 They don't really know what they want to do。 And then I have one technical one for one point now。

 Windows wheels。 So。 [laughter]， I think this is actually worth an applause。

 This was a horrible technical matter story。 So that's basically， if you say pip installs scipy。

 it will try and grab a wheel。 And if not， it will try to compile something from source。

 Compiling something from source is fine on Linux。 It's also with a little bit more trouble fine on Mac。

 On Windows， no one will get it done。 This was the main reason why it took me three months to get that first release out in 2010。

 I knew how to build something。 I had a Linux machine。 At some point。

 I got a few tourist instructions from David saying， "Ah， yeah， you installed wine。"。

 And then you kind of cross compile on Linux for Windows and then you've got to test it。

 And of course it didn't work the first time。 You just have no idea what you're doing wrong。

 And it remained a massive pain， I think， for side by， for every project。

 especially the chips for TrankCode as well。 Because that's the major issue until last year。

 So the people who did this， I helped a little bit， but I think Pauli did a lot of work。

 Pauli did a lot。 We had an anonymous contributor who did a lot and a guy named Carl Clefner。

 Matthew Brad， I like those guys。 These are a lot of credits for getting that done。 [applause]。

 And I think those are the key things for me that made it a real 1。0。

 So if you package all of that together， there's technical stuff。

 but the technical stuff is never done。 We had some other lists。 Things we wanted to deprecate。

 things we wanted to improve。 You can always do that later。

 So as long as you get a few of the basics of your community in place， you're a long way towards a 1。

0。 And we've got a really good community。 We've got hundreds of thousands， maybe millions of users。

 We've got 100 to 120 contributors every release。 And we've got about 15 active maintainers。

 There's no single definition of maintainer， but depending on how you can't。

 I think we've got about 15， like people who regularly come back， you know， away and review。

 who will request， things like that。 And maintainers are actually the single most important element of your project。

 So there's a lady named Nadia Eggball who writes a lot about self-first sustainability。

 and she said， "Maintainers are the keystone species of software development。"。

 And that means something special to ecologists。 Keystones species are the species that make a whole ecosystem work。

 And I think it's true。 But code by itself is nice， but it goes still very quickly。 You know。

 every time a new library comes out or a new Python version， you have to do a lot of stuff。

 But maintainers， it won't work for very long。 So you've got to actively work on getting more of those。

 We've got 15， but we had 16 modules。 So we still only have less than one maintainer per module。

 That's not a lot。 The modules are big。 They're basically individual packages。

 So getting these maintainers that requires basically to actively hunt for them。

 You've got to -- we've got all these things like code of conduct and contributor guidelines。

 and ways to make it nice to start contributing。 But those contributions， like they matter。

 but they mostly matter the ones that kind of keep coming back。

 And then go on and review other people's contributions。 Because otherwise。

 your development doesn't scale。 And this may require -- just keep an eye on -- if it's the same person。

 sending the third pull request， maybe send them a private message saying， hey， thanks for that。

 Do you want to do more？ What's your interest？ It's not rocket science。

 but it requires more talking than just on GitHub， like a bad code。

 So this is a list of our current set of maintainers。 So this is just for the last four years。

 How many commits per year？ So you see a lot of people with， you know， consistent， you know。

 100 or more commits every year。 Just great。 So remember in the very first conference I went to。

 in EuroSight Buy， Fernando Perez showed a similar picture like this。 And basically。

 there were only two names for SciPy。 And then after his talk， like。

 we walked to the elevator and he walked -- I was walking with Pali， who was the other contributor。

 and he was walking behind us。 And he was joking， like， you know。

 you guys shouldn't go and you elevator together with me。 Because if it crashes， like， SciPy is dead。

 And it was a joke， but he wasn't really kidding。 It was a pretty bad situation。 So， you know。

 if you get a couple of new people in every year， it makes your library live a lot longer。

 And then your community is also important to figure out what you want。 So。

 got a recent email from Matt。 Matthew Rocklin， one of the lead author of "Dascal of People Will Know Him。

"， Got the pleasure of meeting in this morning at breakfast。

 And it was a response to something and say， like， you know。

 removing masterrays completely from NumPy。 If that makes it go faster， you know， that excites me。

 Well， masterrays are， you know， something that are absolutely essential to Map。lib。 So。

 not the best idea。 But you see that？ That's what he wants。 He wants to go faster。 Then。

 on the other hand， you know， here you've got， from a few months ago。

 there was a very interesting Twitter debate。 A couple of very long time users。

 previous contributors saying， like， "Great at SciPy is now 1。0。 You know。

 maybe it will finally become stable。"， Like， same community。 Now， maybe you can have both。

 but it's a lot of work。 So， there was the outcome of that discussion as well。

 Those people have pointed out， like， you can do all of that， you know。

 and you can have innovation and stability， but it costs a lot of time。 Right？ And， you know。

 it would be nice if someone paid for that。 So， we got， you know。

 Peter Wang weighed in with a lot of good points， and at the end， they're like， you know。

 this kind of， you know， problem， where you get people to， you know， do all this work for free。

 and you want them to， you know， create new stuff， but also keep old stuff， working indefinitely。

 you know， that's the kind of thing that burns out maintainers。 And I think， you know。

 something that happened to me at some point， which I never thought would happen。 Yeah， so。

 I think that was in 2014 or so。 Like， I had a pretty busy job， you know。

 for quite a bit of pressure， 40， 50 hours a week， and then come home and do some more on them pies。

 some on side pies， some on them focus。 And at some point， it got a bit too much， and I thought。

 okay， I'll just stop reading my private email for a little bit。 Right？ And then， you know。

 I thought， you know， maybe a lot more emails， I'll stop reading it for a little bit longer。

 At some point， HR at my company forwarded an email from Travis。 I said， you know。

 I want to ask about your employee Ralph， because， you know， we've heard from him in six weeks。

 maybe something happened to him。 I thought I'd just turn it off yesterday， you know。 So， you know。

 consider myself pretty， you know， stable person that wouldn't happen to me。

 but it can happen to you， and it can happen to everyone。 And the important lesson for me was， like。

 you know， that email from Travis， like， you know， made the light switch go off。

 and that actually helped me just deal with it。 So。

 if that happens to someone in your community and says， like， "Oh， I can't do this right now。

 I'm way too stressed or overworked， or you just don't hear anything at all where you really should be。

"， Like a private email can do wonders。 All right， so for me， it's community first。

 but there's also some code。 So， we had a bunch of cool code in SciPy， so I'll show you a few things。

 So， there's two things important for me in SciPy。 And why it was SciPy 1。0 was milestone。

 One is user-friendly interfaces。 So， this is an example I took for my day job。

 where basically we have New Zealand， you've got a big database of， biosecurity samples coming in。

 So， that map on the right shows where they're taken， and in the end， you know。

 if you want to analyze that and， you know， figure out why we've got， you know， insects or， you know。

 diseases in forests， and either weather data。 So， there's a function called grid data。

 and that basically allows you to say， like， here are my coordinates。

 here are the coordinates where I have， you know， weather stations， you know， match them up。

 figure out which weather station I need， for which biosecurity sample。 And， you know。

 the interesting thing is not like the exact piece of code， but it's basically one line of code。

 And that's how it should be。 And I think we have a lot of interesting algorithms in SciPy。

 but we think a lot， of the engineering went into， you know。

 going from just a powerful algorithm to a， powerful algorithm or set of algorithms that work in a single line of code。

 And so here's another example。 This one is new in 1。0。 So solve IVP， initial value problem。

 So this is for a couple of differential equations。

 And the interesting part of that set of code is this for loop。 The form method in， you know， RK45。

 et cetera。 So those are method names。 So we've had all of those algorithms inside by probably since 2001。

 But they were all slightly different。 And I wanted to try all of them。 You probably have to write。

 you know， five times as much code as this。 So， and you could， you know。

 before you could read the documentation， it would tell you， like， if you have a stiff problem。

 use the rod out solver。 Like， you know， I've got ordinary differential equations in my， integrated。

 but how do I know if I have a stiff problem？ No idea。 So it's easier to try them all。

 So this few lines of code tries all of them， you know， figures out the error for each of them。

 And it tells me that in this case， yeah， can't read the colors。

 But RK45 seems to be a pretty good one。 So I'd like to see more of this in the future。 I think we。

 you know， a couple of models that are in， that are in， pretty good shape now。

 but user-friendly interfaces are super important。 And then the other one is performance。

 So in terms of performance， like， probably the single biggest thing we did is。

 create site and bindings for a lot of the code in SciPy。 So all of the SciPy。

special module has site and bindings now， and they're all auto-generated。

 so they're complete and easy to maintain。 So you can just import it in SciPy code and use it directly。

 and it won't go through Python at all。 And this can， depending on your problem， like， you know。

 you have problems where you do， you know， lots of little function calls， it can make things。

 you know， one or two orders of magnitude faster。 And a really nice example of these site and bindings are in。

 is this one。 This is a number example。 So you see this ad-jitz decorator with no Python is true。

 So what number will do is take this Python function， which calls a NumPy linolek function。 Sorry。

 And compile it into some low-level code。 So the site and bindings for SciPy linolek are actually used by NumPy。

 under the hood to take that NumPy linolek call and kind of translate it， into something that。

 you know， directly talks to the underlying， C or for-trend implementation。

 So even though I defined a Python function there， and the Python function called NumPy。

 because SciPy has site and bindings， this just became five times faster。

 Say the timings at the bottom。 So we've probably， you know， we've got all of linear algebra。

 all of BLAST and layback at least， and all of special site and bindings。

 It would be nice to see a little bit more。 I'm actually going to skip this one。 So what's next？

 So we've got a lot of cool features coming up， but we had a very interesting discussion about languages。

 So the moment SciPy is this， you know， pretty bad hybrid of five languages。 We've got Python。

 Sciton， C， C++， and Fortran。 So at the moment we prefer Sciton。

 And the reason is not because it's more performant。 The reason is because it's the easiest to read。

 You know， for people who work with Python， it's easiest to understand what Sciton code does。

 So that's why we like it。 It's easier to maintain。 And， you know， in terms of performance。

 all of these things are within a factor of， you know， one or two from each other。

 So it doesn't really matter。 So， but even Sciton is a significant overhead。

 and you have to compile it if you want to test it， et cetera。

 So there were some suggestions and can we use number or can we use Python。

 which is another compiler for pure Python code。 And the interesting part is， you know。

 what are the problems with adopting them？ So at least all of those， you know。

 kind of things you have to think about。 So you've got most important ones at the top。 Fortability。

 you know， runtime dependency and maturity。 I think， you know， those are ones that you have to have。

 And at the moment， those are the ones that Sciton is still the best at。 And， you know。

 no more probably the second best option。 Like， no more easier to read， right？

 You put somewhere in abjit。 You know， that's four characters and things all of a sudden become 10 or 100 times faster。

 That's great。 You know， I don't have -- that's much better than writing a 。py x file for Sciton。

 right？ And then running a compiler and then you have to hook it into a built system。

 And most contributors will be lost by then。 So -- but as long as Numba doesn't have the sportability。

 which I think will be， you know， majorly improved today or tomorrow and the release version of 。39。

 But if it doesn't -- if it doesn't have that， you know， we can't adopt it。

 But due to this discussion， you know， we -- you know， we made the Numba developers aware that。

 you know， these are the things we want。 And， you know， you think， like， you know。

 it's pretty obvious， you know， they should know that already。 But actually they don't， in all cases。

 For example， the debugging and optimization that now shows that， you know。

 this is just my -- my interpretation of it。 But it shows that Numba is easier to use than Sciton。

 That wasn't the case a few months ago。 Actually， you got， you know。

 whenever something in Numba broke， you got this horrible， like， you know， miles long trace back。

 but， you know， I couldn't make sense of it at least， you know。 But， you know， within， I think。

 three days of us explaining， like， this is the problem， and see， you know。

 Sciton is much nicer and does it like this， and you get these annotation features， et cetera。

 Somebody has fixed it in Numba and wrote it in a nice， iPiten， you know。

 Jupiter notebook extension to even， like， highlight it in notebooks。

 So I think now it's actually better in Sciton。 So you talk to these people， you know。

 they will do the right things。 Then， you know， should we actually grow？ You know。

 SciPit is already horribly big， and I think we've got it -- we've actually done -- we've。

 removed probably more in the last six years than we've added。 And that makes the library， you know。

 higher quality and easier to maintain。 It's probably a good thing。

 So we removed four top-level modules， and we've only added four subsub modules。 So， you know。

 we added a lot of features and code， but we've managed to narrow it on the scope of it。

 So I think we'll keep going in that way。 We may， you know。

 there's probably not much more whole modules that we should throw out， but we won't， grow in scope。

 I think。 We'll just make what we have work better， you know， or user-friendly。 Then， you know。

 what's coming technically？ There's about 190 open pool requests， so lots of little things。

 But these are for me a couple of big ones。 So support for newer laid-back versions。

 We've been stuck on the same one for ages， I think 3。2。1， because Apple doesn't。

 refuse to ship anything higher than that。 So we finally said， okay， that's good， but， you know。

 thank you， Apple。 We'll just drop you now。 So we'll drop the accelerates。 So we're now getting。

 you know， regular upgrades in laid-back versions， which matters a lot。

 if you do anything related to linear algebra。 Then sparse arrays。 So we had sparse matrices。

 and actually， you know， they work pretty well， they're performance， but the problem is。

 they act like a matrix and not like a NumPy matrix and not like a NumPy array。 So NumPy matrix。

 you know， we wanted to get rid of it， we wanted to get rid of it for ten years， you know， we can't。

 mainly because we have side-by-dots-bars。 So， I'm not going to say more about it， because， you know。

 Hamier is going to talk about it in the next session。 So I'm looking forward to that talk。

 Then there's a couple of very good， better optimizers。

 We had a lot of work done on better local optimizers。

 but now I've got a couple of global optimizers coming。

 And then the last big project is the GSSC project of this year。

 I've got a very good Google Summer of Scout student。

 and he's working on supporting all kinds of rotations， within side-by-dots-patial。

 and any kind of representation for it。 The first thing has been merged in about a week ago。

 so he's got a month to go， and that looks like a really nice thing to have。 And then。

 the last thing is， you know， should we remain volunteer only？ So in terms of community。

 that's for me the next step。 There's only so much you can do。 Like， if you look at， you know。

 we've got a good maintenance team now， but you're basically scavenging people's hours outside。

 you know， and evenings and weekends。 So， to really go well beyond that。

 we have to rely on people who get paid to actually work on side-by。

 And NumPy has an interesting experiment at this moment， so we've just got now， since， you know。

 a few weeks， I think， the second person working on NumPy full-time。 So， you know。

 it's got about a million dollars， so we've got a couple of people for two years and see what difference that makes for NumPy。

 And I think it will make a very big difference， see it already。 And the， you know。

 side-by may aim to go in the same direction。 And the question， of course， is always like。

 where do you get that money？ But， you know， first thing is like you have to realize that you want it。

 And one of the things， you know， you can think of big new features， but one of the things， you know。

 we've got， we've got thousand plus issues。 And I remember talking to Pali about three years ago。

 we had 600， and we were walking around at Euro-Sipy， and he looked at it and said， like。

 I can close all of those in a year。 Now， he's a pretty， you know， he's a pretty productive guy。

 so the average person would not do that in one year。 But still， you know。

 with a couple of many years of effort， it's feasible to kind of close all of them， you know。

 and then， you know， and then think about， you know， some bigger new features that you might want。

 And it's not crazy to want that。 And the way to get that money， well， there's no guarantees。

 It's a lot of hard work getting money for anything。 But it will involve non-focus。 So， non-focus is。

 I think most of you will know it。 It's a non-profit that， you know。

 that supports a lot of the core packages in our ecosystem。 So， it has multiple focuses。 Like。

 it runs the Pi Data conferences。 It's education， project sustainability。 But for me， you know。

 the reason we set it up was， you know， basically to get a more stable funding stream so that we could actually grow the ecosystem further。

 And it's starting to get there。 So， these are the current sponsors of non-focus。 So。

 these are the people that every year sponsor， like， some amount。 [applause]。

 I've got a lot of the non-focus staff here。 And they did a lot of the work on this。

 But you're starting to see a pattern here。 Like， at first it was a sponsor here and there。 I think。

 you know， Anaconda was the first one。 And then， you know。

 Microsoft at some point wanted to sponsor Jupiter。 So， like， why don't you do that via non-focus？

 But it starts to really look like a pattern there。 All the big companies are there。

 A lot of big finance companies that rely on Python。 So， it's not yet a， you know。

 it's not yet a stable funding stream that packages and projects can rely on。 But organically。

 I think a pattern is starting to appear there。 So， it looks very promising to me。 So。

 we'll see where we go from there。 And I want to thank the Side-Bye Core team。

 everyone who contributed and this community for， you know， making it a pleasurable experience。

 [applause]， We have time for a few questions。 So， if you have a question。

 there's a podium mic there。 I can also bring this over。 Just raise your hand。 [silence]。

 There's a podium mic， but he asked me first。 So， okay。 It's a very nice presentation。 Well。

 how do you determine where the boundaries of Side-Bye？ What is better suited to be in a side kit？

 And what you'd want to put the effort in continuing to maintain in core Side-Bye？ So。

 I think a hard boundary， I think， is， you know， it has to fit within the current scope of Side-Bye。

 So， we haven't added a new sub-module in ages。 So， it's better to start something， you know。

 if you're interested in something that's not already in there。

 to start it as a new scikit and just see if it's viable。 You can develop it much faster there。

 The other part is like there have been a lot of suggestions to， let's say。

 break up Side-Bye and maybe development would go faster。

 I think if you see which of the scikits are successful， it's mainly scikit-learn， scikit-image。

 and stats models， to some extent。 So， those are the parts that are， I'd say。

 really high level and that have a good， you know， active community around them， also。

 not just in Python， but like， they're active topics in， let's say， academic research as well。

 And it's stuff that you can say， like， that's what I'm doing， like， I'm working， you know。

 I'm a machine learning researcher or engineer。 So， those things make really good scikits， I think。

 If it's something like， let's say， interpolation， you know， it's a very important topic。

 but I don't think it would be very viable as a scikit。 Because there's not， like。

 you don't have this community goal， lessing around it and you won't have someone saying， like， hey。

 I'm an interpolation engineer， that's just， this is not how it works。 [ Pause ]。

 >> And thank you for the great presentation and also， and thanks。

 thanks for all of the people who contribute SciPy， maintain SciPy。

 I'm pretty shocked that they're only 15 plus people who are maintaining SciPy。

 And one thing I'm always very unclear about is， and as a user， we all want to give back eventually。

 but I'm not sure where exactly to even get started。 If， for example。

 I want to be one of the people who can contribute to maintaining this entire ecosystem。

 which has been so tremendously helpful， and is there a call for actions or some kind of calling for volunteers kind of thing？

 That's really explicit so that people can all come together and help。 Thank you。

 >> Thanks for your question。 Yeah， so there's no， like， call for actions in like。

 now we want volunteers。 It's like， we always want volunteers。 And there's， like。

 this conference is probably one of the best places to get started with that because you can ask people in person。

 We've got sprints on the weekend， you know， where most packages will have a lot of core developers。

 And， you know， there's always a place to start contributing。 Even if you're， you know。

 you're completely new， like， you know， maybe we can have a chat afterwards and see， you know。

 what interests you because that's very important。 And then， you know。

 what would be a suitable topic。 But yes， we definitely would appreciate your help。 >> Hello？ Okay。

 I've got two questions。 One question is just now I noticed that for the sponsors。

 they were not in alphabetical order。 So I just wonder were they ordered by how much money they provided？

 I don't know all of the numbers by heart， but yes， if you look on the NEM focused website。

 they are ordered。 So there's like sponsorship levels， like platinum gold silver brands。

 So I think that the platinum level is $100，000 per year。

 So I think that we now have four platinum sponsors。 So that's， you know， that doesn't yet add up to。

 like， lots of manpower， but it's starting to get significant。

 And the second question is you mentioned that now you， like， two developers， like。

 full-time developers， like， were employed。 So in addition to the developers。

 I just wonder will you consider， like， like， employee， like， full-time managers？

 Because I come from the University of Pennsylvania and I heard that we have， like， programmer， no。

 no， we have program that provides some kind of， like， education， like。

 degree for those people in nonprofit organizations to help them to manage nonprofit organizations。

 So I just wonder if that will help the program？ So I think it depends on size。 So there are larger。

 that there are people， like， Jupiter， for example， has a lot more funding。 So I got， I think。

 a $6 million grant， you know， a few years ago。 So they do have a project manager。

 I think there are other projects as well that have community managers。

 It's not something that I think you should do as the first thing。 So if you only have room for。

 like， one or two people， you probably want to recruit those， you know。

 from people you already know are working productively on NMPI。

 so you know it's going to be successful。 But yeah， certainly， once it grows beyond a few people。

 you need some kind of， you know， management or community organizing person as well。 Sorry。

 I can't hear you without the microphone。 Who's focused on fundraising？ Well。

 I think that's one of the things where NMPF focus comes in。 So it has a， you know。

 full-time staff and it has a focus on fundraising。 And since it represents Jupiter and NMPI and。

 you know， even projects outside the scientific Python system， like Julia and R Open Sci。

 it can talk to potential sponsors for all of these projects together。

 which is a lot more efficient than trying to do it as a project。 Hi Ralph， this is Anthony Scopats。

 So my question is what about your governance structure and what other governance models you considered and why you decided to go with a BDFL one and。

 you know， what's the， all is the process there like。

 So the major other one we considered was a consensus-based model。 So that is what NMPI has。

 for example。 And the difference is like it's probably better。

 Like most of us felt it was better to have a single person that can， you know， that is a BDFL。

 Because in the end it's a， what do you call like a full-back decision-making structure？

 Like you only need it when， you know， when every other option is exhausted。

 So at that point it would be good to have one person who everybody trusts that says， okay， you know。

 this was useful but now the discussion is kind of unresolved。 This is where we're going。

 Because if you do that as a community， like as a consensus-based group， it's still very hard。

 And NMPI hasn't had to do that yet， but to me it's not 100% clear that that's actually going to work。

 So of course you have to have that person that you all have consensus like we're going to call this person。

 you know， our benevolent dictator。 Not all projects have that。 Like in that case。

 like you have to consider a consensus-based model or maybe something else， a group of three leaders。

 There are many ways you can structure that。 But to me having a single leader in the end is helpful。

 So thank you。 We have a break now for half an hour。

 so I think you can head up to Ralph and ask him more questions if you would like that。

 But before we break， I have a small announcement。 So the reason I had to bump off Anthony when he first came up to ask the question is that there's actually a study saying that if the first person asking a question is non-male。

 it actually makes the number of people who actually ask questions a lot better distributed。

 I didn't want to say that up front， but now since I ended up screwing up。

 I want to make sure that it doesn't happen in the future。 So going forward in all of the talks。

 I request you to please try and ensure that the first person who asks a question is not a male。



![](img/afa3d5760af3b36ff43fd96beabb35d8_1.png)

 And that would mean that some of the non-males actually do get up and ask the first question。

 So that was the hard part。

![](img/afa3d5760af3b36ff43fd96beabb35d8_3.png)

 So since I've now said it， I hope you will help me make that happen。



![](img/afa3d5760af3b36ff43fd96beabb35d8_5.png)

 So thank you very much and let's break at this point。



![](img/afa3d5760af3b36ff43fd96beabb35d8_7.png)

 [applause]， [ Silence ]。