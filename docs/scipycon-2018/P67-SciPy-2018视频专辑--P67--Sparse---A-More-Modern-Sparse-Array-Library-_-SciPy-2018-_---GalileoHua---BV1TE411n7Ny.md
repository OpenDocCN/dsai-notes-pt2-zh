# P67：SciPy 2018视频专辑 (P67. Sparse - A More Modern Sparse Array Library _ SciPy 2018 _ - GalileoHua - BV1TE411n7Ny

 >> Hello， everyone。 I'm here to present a library that Matt Rockland started and I picked。

 up a few months ago。 So it's about sparse arrays rather than sparse microservices and。

 Ralph mentioned in his doc。 So here are a few shout outs to people who have helped me throughout。

 these few months that I've been doing Python。 First of all， the Berkeley Institute of Data。

 Science for bringing me out here， helping me give my talk。 And I'm focusing on Numpy for。

 bringing up some of the other expenses that I had。 Matt Rockland for really mentoring。

 me since his start and Ralph Gommers for introducing me to Numpy and really giving me a lot of。

 support。 And I'd like to thank every single other contributor to the library。 So who am， I？ Well。

 I've been using Python since 2017， so I'm fairly new user actually。 I'm active。

 on the Numpy mailing list。 I've helped make quite a few architectural decisions so far。

 I've had no formal CS education。 I've been a hobbyist programmer for a long time but。

 really no training。 So the question， I guess， that comes to mind is what are sparse arrays？

 Where do you use them？ And the answer is， sparse arrays are arrays with a lot of null or zero。

 elements in them。 So a null element， can you be any element here？ It's zero。 For Boolean， arrays。

 it would be false and so on。 And as you can see， this is an example array that。

 has a lot of zeros in it。 Real ones are really much bigger than this。 Okay。 So why use sparse。

 arrays when dense arrays can do everything， theoretically， right？ Okay。 So the main two。

 reasons are you have less memory usage and more performance。 So since you only have to。

 store nonzero elements and somehow a notion of their position somehow， you use a lot less。

 memory than you would for a dense array。 And you get more performance out of it because。

 for memory operations， you can just skip over the zeros。 You don't store them。 You don't。

 think about them。 It's faster。 Okay。 Where do you find sparse arrays？ Think of any physical。

 system that's loosely coupled， that doesn't have too much coupling between its various。

 states or various components。 So think of RGS and CMA matrices of or transition matrices。

 of Markov systems， practical Markov systems。 This is a very good example for sparse arrays。

 Think of solving systems of collisions。 You get dense or sparse gradients or maybe you。

 could even get sparse Jacobians when you do solutions of these equations。 Finite state。

 controllers have matrices that are arrays that are very sparse。 And I just see messages。

 of graphs because graphs are usually， well， they're not really highly connected in most， situations。

 So the standard solution to sparse arrays in the sci-fi ecosystem has been sci-fi。

 to sparse for a very long time。 And that's fine and feature complete， but it has a number。

 of problems that I've mentioned。 So it's limited to two dimensional arrays， unlike the。

 NDR interface which has n dimensions。 We also tended to adopt the Italian first perspective。

 from the start。 So I always posted in the sci-fi mailing list when we had any kind of。

 large design decision to make。 We use NumPy protocols to ensure as much compatibility。

 as we can with NDRAs。 So as a result， a lot of functions that work on NumPy arrays work。

 on spicer arrays out of the box。 Okay， so with that， I get to the bulk of my talk。 The。

 first thing is how we store them currently， how we form element-wise operations on them， reductions。

 indexing， transposing， reshaping and mixtures into products。 I would like to。

 emphasize that these aren't the only features we have right now。 There are a lot more。 This。

 is just some of what I would like to cover。 Okay， so storage format。 We talked about storing。

 a sparse array and the simplest format for n dimensions is basically a coordinate format。

 It can be easily generalized to n dimensions。 So for example， you could see this matrix， here。

 And you could see， for example， the three in the top row has a row index of zero。

 and a column index of two and the data is three。 And similarly for all the other indices。 We。

 also see the density of such a sparse array is 。25 because 25% of the elements are non-null。

 Let's talk about element-wise operations here。 So suppose we want to add two sparse arrays。

 and remember that only the non-zero elements are stored and only their positions are stored。

 We don't really have an array that we could loop through to do this。 So what we do is we。

 first identified the elements currently in our library that are non-zero for both arrays。

 So those are highlighted in yellow here。 And we performed the operation on those。 Great。

 Then we highlight the elements that are zero and one array and non-zero and the other。 And。

 similarly really for the third array as well。 This gives you three groups of elements that。

 you would perform operations on。 And by combining these back and re-sorting them so that they're。

 in canonical order you get back the result array。 And other optimization that we had in。

 this library and let me emphasize that this is a broadcasting scenario in NumPy if you're。

 familiar with it。 And this is element-wise multiplication that we're talking about here。

 Is that you could have very large broadcasting scenarios。 So talk about two sparse arrays。

 being multiplied and one of them has to be broadcasted to a very large dimension。 What。

 we used as an optimization here is that this yellow tree would be masked with one time with。

 any of the zeros and one time with one。 And basically what our algorithm that we used。

 would realize is that when you multiply it through it zero you get it zero。 So it doesn't。

 have to be actually stored in the result array。 And so you kind of skip over doing it three。

 times and just do it once。 And remember that in a real situation this may be quite a lot， larger。

 So here are some more details if you're interested。 We used the array of fun protocols。

 so that universal functions work out of the box on sparse arrays。 For n input you function。

 algorithm is generalized so we use a two to the n minus one batches of processing。 That's。

 one for each off and on array and one removed batch which says hey all arrays are off this。

 is supposed to be null anyway。 We're working on a way to loop through the coordinates so。

 that's faster and you only loop through the arrays once。 And sorting is slow。 So right。

 now about 30 to 40 percent of the time in all operations is usually taken up by sorting。

 We're working on switching to a radix sort from quick sort which should be quite a lot， faster。

 And well the problem is that a lot of operations on sparse arrays actually give， you denser arrays。

 So think of taking the cosine which maps zero to one。 We're working。

 on making those sorts of arrays slower and supporting more use cases but in the end you。

 want to make this an error so that you don't get a dense matrix at the end and get a lot。

 of performance degradation which can be a lot harder to debug than just raising an error。

 Let's talk about reductions now。 Reductions are actually quite challenging to do in general。

 but we have managed to implement the subclass of all reductions for sparse arrays。 So addition。

 is easy。 Summing along the rows is easy。 You just sum all the nonzero elements right。

 Let's talk about something more interesting。 Let's talk about taking the product along the， rows。

 So what we do here is we take the product of the nonzero elements and we also store。

 some additional marker that says hey there are additional zeros here that gives you this。

 Remember that the third row was nonzero so we don't even store it。 And for the six and。

 the two you get a marker that says there's a zero after this and for the five you say this。

 is no zeros。 So you reduce an extra time with zero where you get a yes or a true and what。

 you get in the end is you get this out which is the correct answer for products。 For those。

 of you following this algorithm you may have realized that these are the restrictions that。

 you would have but in practice a lot of reductions is what is some products min-max and all are。

 all supported。 In the future we plan to add arg-min and argmax as well。 We also use the。

 array of uniform protocol for reductions so sum in all of the uniform productions work。

 with the restrictions that we specified before。 Sorting takes up a lot of time still so we're。

 working on improving that and general reductions are implemented by transposing and reshaping。

 to two-dimensional array and doing it in the reverse order at the end。

 Let's talk about how we index sparse arrays so suppose we want to grab this yellow tree。

 here and what we can do is since the coordinates are all sorted we could first grab the row and。

 then we could grab the tree with a simple binary search because they're all sorted but。

 we could also get a situation like this where for example you get a lot of elements that。

 you have to address and so addressing each of these rows is one binary search and addressing。

 each of these elements is another binary search and you get about 12 binary searches which is。

 more than the number of non-zero elements in this array right it's crazy。 So what you。

 can actually do is you could directly filter out the coordinates so you can filter out。

 by rows that gets rid of the five there and you can filter out by columns which get rid。

 of the one here and then you apply a simple transformation and you're back to simple array。

 the elements that you want and then you could calculate the new coordinates。 So in practice。

 what we do is we follow a hybrid scheme where we weigh the number of expected binary searches。

 versus the amount of elements which we left and we would have to filter and whichever one。

 is faster we just pick that one and roll with it and the problem is that this is not fully。

 compatible with NumPy in the sense there's no view so everything is a new array even a slice。

 and even an integer index right now and it's slower than NumPy because we actually have。

 to do binary searches or sometimes filter coordinates so that's not ideal。 Transposing。

 what we're reshaping works exactly as you would expect for transposing we simply switch the。

 order of the coordinates and re-ordered so that it's still in canonical order for reshaping。

 we convert the coordinates to a linear index and then convert back and that that day essentially。

 reshapes the whole array and for matrix re-tensor products we reshape both arrays into 2D multiple。

 array uses matrices using a BLAST implementation there are BLAST implementations even for sparser。

 arrays and then we convert back to the required dimensions。 We're actually looking for more。

 people to start using this so that we could get more feedback on what's important and。

 what we should prioritize so you're welcome to use it the API is not yet stable at this。

 point it's mostly stable but not quite it has really a comprehensive documentation so we。

 have that going for it as thoroughly CI tested so this should be very little bugs if any。

 Plan features that we have for this library is right now a COO is the only format that's。

 supported we also have the DOK format which is more rightable but we plan to have a format。

 that's a generalization of these formats which would make sense in a lot of scenarios。

 and for a lot of libraries that expect this format such as for example scikit learn we。

 tend to get we tend to get a lot of result in sparse errors right now sometimes in some。

 operations so we tend we intend to make those lower by having a number of features we plan。

 to support more of the NumPy API through protocols I'm really really pushing protocols at this。

 point because it's useful not just for my library but also for Dask and X-ray and a number。

 of others we would welcome contributions if anyone is interested just talk to me find。

 me I'm always available and like Ralph said we're planning on integrating into site by。

 at this some point once this library is more feature complete and the API is more stable。

 I thank you for your time and I'd be honored to take any questions any may anyone may have。

 thanks thanks very much and welcome to the python family and I was wondering we have。

 time we have time for several questions and we have one mic over there I'm over here with。

 one mic I'm willing to run around a little bit who is a first time sci-fi attendee anyone。

 first time a few hands okay cool we have 800 people registered for the conference this year。

 which is a quite a quite an incredible growth for the conference okay I can't I don't see。

 it all right please hi thanks for your talk I had a question I guess you kind of briefly。

 mentioned it on the last slide you have like that air that pops up like you know result。

 not sparse like you know if you add a bunch of sparse arrays like there's some echo and。

 in the sound is can we fix that there's some echo and sound I can't hear his question problem。

 sorry could you repeat your question sorry then so on the last slide you were mentioning。

 the was it like result not sparse so is that like when you like add a bunch of sparse arrays。

 like you get a result that's like a dense array how what's the plan going forward to kind。

 of deal with those types of things like you know oh this won't be sparse let's just convert。

 it to like a dense NumPy array so this is really a diff so by a density result。

 on sparse errors we only raise them when when a function is mapping a zero to a non-zero。

 currently so things like taking the cosine of a of a sparse array or or maybe like one。

 minus a sparse array that would that would make it dense so we really don't raise it if。

 you add a bunch of sparse arrays because that would keep the results sparse and we also。

 raise an error when for example you're performing the reduction and and and access that is entirely。

 composed of zeros reduces to a non-zero access so those are the main scenarios that you get。

 that that sort of error I have another question over here let me let me let me just a quick。

 one so our compressed row storage and column storage are they implemented already like a。

 conversion at least or not yet we do support conversion to cypys CSR and CSC matrices and。

 from those formats as well but those formats are natively implemented at this library it。

 is planned and it is a prioritized feature arise of now thank you please great talk I。

 was curious as you mentioned converting to numpy arrays and numpy has this protocol was。

 done to array protocol do you use that protocol for through sparse arrays convertible is that。

 useful or not yes I have been using the area you from protocol extensively it's it's used。

 to achieve interoperability with numpy so the area you from protocol I use it for reductions。

 and for you funk applications universal functions and I'm all the me and the number of other。

 people are also working on the array function protocol which allows you to dispatch an arbitrary。

 function to any kind of object so we plan to use that one as well yeah okay thanks okay。

 I have another question over here hi yes Roger sir we hear my question is you have this sparse。

 matrix because you want to eliminate zeros and you're raising a dense error matrix if you go。

 through a cosine function what if you had the ability to say it's a sparse matrix with a constant。

 offset so you can have a cosine function and it will still be sparse is everything adds a one to it。

 yes that is actually a plan feature we call it arbitrary field values so the idea is that we。

 actually store the null value and allow it to be something other than zero and if like zero is mapped。

 to a one for example like in one minus x then we store the full value to be one it is a plan。

 feature yes Anthony you have a question over there is that Anthony's go but I can't see it no it's。

 a manure okay I really look like Anthony no but you are so related that my mind you know made the。

 connection so is the plan for this to eventually like be a replacement for sci-fi sparse that is the。

 plan yes so you're gonna implement like all the linear algebra as well I don't plan to implement。

 it myself but there are a number of C and Fortran libraries that already do it but I do like are you。

 gonna integrate with with this like yeah we do plan to wrap those libraries okay another question here。

 thank you I suppose my question is sort of related to the previous question I think the people are。

 interested in sparse algebras sparse exclusion arrays not only because they offer more efficient。

 storage but also because they offer quite a savings in in in performance that when you perform certain。

 operations and because efficiencies at stake here you want to go native and go interface to libraries。

 was a question probably is do you foresee any developments where you would allow to implement to。

 use libraries for efficient implementation of linear algebra or something else like core operations。

 like numpy does for certain things certain you funks may be implemented in C is there a way for。

 sparse to support a C interface to improve efficiency good question so you funks already are implemented。

 you funks work right now they're not as fast fast as in sci-fi sparse but they are implemented and。

 we also are working on making them faster there are some actually we use number as the back end as。

 the fast computational library for for this project and there are few features that we require our。

 numbers and before we can move forward some with some things but those features have come very。

 recently number point a point 29 so there's you found applications should be faster and about linear。

 algebra we we don't plan to implement linear algebra directly inside our library but as I'm。

 thinking that that's I've talked with Ralph and that seems to be his view as well that once we pass。

 a point where we have all the essential data structures implemented then sci-fi I will work with。

 sci-fi developers and I might work directly in sci-fi to actually wrap the core of linear algebra。

 routines with sparse arrays。 Any more questions？ Very exciting project especially for the PDE。

 people in the room so thank you。 Final question yes no final question yes we do have one okay。

 speaking speaking to your experience as a new contributor to the whole sci-fi ecosystem could you。

 speak to how you would try to encourage other people to get involved and start contributing as。

 well I mean it's not a question that has anything to do with sparser sparser arrays but I'm something。

 I'm really concerned about so I would say that I would do what Matt and Ralph really did with me so I。

 would encourage someone not tell them that their code is bad instead tell them how they could。

 improve it and tell them that this is a good effort right yeah so yeah that's that's the best。

 you can do you can encourage someone to get involved you could invite them to get involved but in。

 the end it's it's obviously the own choice but obviously the better the community the more welcoming。

 they are someone will want to get involved。