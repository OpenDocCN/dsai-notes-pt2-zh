# P97：97. L18_5 Text Preprocessing - Python小能 - BV1CB4y1U7P6

 Okay。 So now that we've seen how basic text statistics look like。

 let's look at how we actually would want to process text。

 And so the first thing we need to do is we need to tokenize text。 So by tokenization， I mean， well。

 we turn every word or every， you know， simple into an idea and so that text turns into a sequence of integers。

 basically。 So there are a number of ways how you can go about this。

 One is I can use a character encoding。 And that's very nice because， you know， if I have， you know。

 maybe 30 to 35 meaningful characters， I get a very， small vocabulary。 And so it's very。

 very easy to， you know， predict one new character at， the time。 And if I were to do this。

 I would never end up in a situation where I haven't。

 seen a particular word because it's composed out of those characters。 The problem is if I do this。

 then quite often the model doesn't work so well。 It doesn't work so well。

 I mean that the network actually needs to learn how to， spell properly。 Now for some languages。

 this is actually a good thing。 So if you， for instance。

 have a weird language like German where you have， you， know， not just the verbs。

 but also the nouns changing their shapes and forms or， Russian where you have， you know。

 six different cases and then you have single， line plural。 So。

 or if you have languages that attach a lot of stuff at the end of， words。

 so for weird languages like that， that's quite fine。

 It actually works quite well for Chinese for very obvious reasons。 Any thoughts？

 Why does it work well for Chinese or for Japanese for that matter？ Exactly。

 you have actually thousands of characters。 So this is actually pretty。

 much in the Goldilocks zone where you don't have too many， you don't have too few。

 So you get a representation of the meaningful granularity。 But if you have a small alphabet。

 then it's not so good。 Well， you can go to the other direction， right？ So， well。

 why can't you do the same， thing as what you know you would do with Chinese， also for English？ Well。

 and let's just pretend that， you know， every word is a token， right？

 The fact that this isn't quite the case is exactly what saves us in Chinese， but。

 for English and if we didn't have， well， for English it's not that bad yet， but。

 for pretty much any other language nouns and verbs really change their forms quite， drastically。

 Well， you get a really huge vocabulary。 And you may not be able to generalize， well， otherwise。

 for instance， you might have， seen some verb only in one form and not in all the other forms。

 So it's a huge vocabulary， it's quite costly and slow and the GPU vendor will。

 happily sell you a bigger GPU because of that， but it's a bad idea。

 So there's obviously something in the middle and that's called byte pairing， coding。

 So what people did is they said， well， let's just look for frequent common， substrings。

 Then you just order them， you aggregate， you know， the most frequent common substrings。

 and then you aggregate this， further and so you get basically something that looks almost like syllables。

 but， can be a little bit longer if you have some other substrings that are very common。

 And so this byte pairing coding gets you pretty much into a Goldilocks zone， which， well。

 if you were dealing with Japanese or Chinese， you would be pretty much， in already from the get-go。

 Okay。 The next thing that we need to do is， if you。



![](img/4fa8609d91cfeb3b3a3b2dbf7d41a715_1.png)

 think about it， you need to generate the mini-batch。 As we need to generate our training data。

 remember， we had this embedding and then， we want to predict the next character。

 So what you could do is you could， basically take the text and you break it up in this case into。

 you know， sub-sequences of five。 So you have different offsets and you just need to。

 count a little bit such that you don't end up going out of bounds， right？

 So it's very straightforward。 And then， so what you do is， you could， for instance。



![](img/4fa8609d91cfeb3b3a3b2dbf7d41a715_3.png)

 just randomly partition， say pick a random offset。 You distribute the。

 sequences at random over the mini-batch。 And this gives you sort of kind of。

 independent-ish samples。 They're not quite independent but under certain mixing。

 properties and so on。 You can essentially calculate all the problems away。 So， for instance。

 there's some nice work on beta mixing， Sarah Funder-Gere and。

 Don Mayer and others have done good work on that。 Trouble is you need to reset that。

 hidden state if you have a latent variable model， right？ Because every time you。

 drive a different sequence in a different part of that string， you don't know any。

 of the context where this came from， so you need to reset your hidden state。 Okay。

 We'll get to that in a lot more detail later。 The alternative is you use sequential partitioning。

 So you basically just， you， know， take a random offset and then， you know。

 distribute the sequences in， the mini-batch but you keep the sequence preserved over mini-batch。

 So basically， you have one mini-batch for this part and the next mini-batch is for， here。

 next mini-batch is for here and you keep on going through。

 This way you can carry the hidden state across the mini-batch。 Then， as we'll see。

 works a lot better。 Okay。 And now it's time for code。



![](img/4fa8609d91cfeb3b3a3b2dbf7d41a715_5.png)

 Okay。

![](img/4fa8609d91cfeb3b3a3b2dbf7d41a715_7.png)

 See？ There we go。 Okay。 So we read our time machine again。 Okay。 So we have about， you know， 178。

000 characters and that's the text。 And so I'm going to first produce an index and so I'm going to use a character。

 model here。 So I'm going to just， you know， look at all the characters in the， dataset。

 So raw dataset is， you know， my dataset and set of that conveniently。

 in Python just makes this all unique。 So index to char gives me that。

 And then char to index I need to just， you know， invert that mapping。

 And so then I get the recovery size and， you know， this is my count， right？

 So the first character is a comma， the second one is an S and so on。

 These are all the characters that actually occur in the dataset。 Okay。

 This is exactly why Python is so convenient。 Okay。

 Now what I can do is I can just look at what I get with characters and， the indices。

 So char to index of char。 Well， that's just my mapping for all the characters in the raw dataset that gives。

 me the set of indices。 That's this thing here。 So one number per character。

 And so sample of the first 20 characters is that。 And then I can do the opposite。 I just run a join。

 And I iterate over all the characters in the data in that sample。 And I perform that mapping。

 So again， this is convenient Python because， you're running the full loop inside an index。 Okay。

 For the first time you code this up， you're not going to do that。

 You're going to take the scenic route and then afterwards if you want to show off。

 pretty code you'll do that。 Otherwise it's error prone。 Yeah。 Anything surprising in there？ Nope。

 Okay。 So then now this is a bit of a， walker of a function。 This will generate random sub sequences。

 So we have all the indices here， the mini batch size， number of steps， the device， context。

 The device context makes sure that we can push things on to a GPU if we， want to。

 So here I compute a random offset。 And then I just throw away the first few characters before that offset。

 Then we can work out how many substrings we can actually generate。

 And that's basically whatever data that I've got left over， minus one。

 And then I need to divide this by the number of steps that I have。 All right。 Minus one。

 Otherwise I would have over counted the last one。 Then I discard everything that's half empty because I'm assuming that we have。

 plenty of data so I don't really need to be particularly frugal。

 And now I just partitioned the data into this。 So number of examples time number of steps。

 Number of steps。 So this is basically just reshuffling things。 And then， okay， we reshuffle。 Okay。

 So this is all pre-processing。 Now， who's ever coded up an iterator in， Python？ Okay。

 So an iterator in Python is a really， convenient thing。 You can essentially use it in a for loop。

 And whenever you say， well， give me a new observation， the iterator returns a new， thing。

 And we code it up like a function。 And rather than return， it does this thing called yield。

 So the goal is to yield。 Basically， whenever I call data iterator random。

 it gives me a new substring back。 So it does all of that at startup time。

 This is just some useful helper function that basically just extracts the data of a。

 certain subsequence。 And I'm just using the underscore to， indicate that， yeah。

 this is an internal function。 You shouldn't touch it。 And now I'm looping over the data。

 This is basically batch size times number of batches。 That's basically what I'm looking at。

 So many batch size， many strings at once。 And I'm going all the way up to batch size times number of batches。

 Okay。 So then batch indices。 That's just the starter here。 Today， generate x and y。

 So I extract exactly in the current and the next substring。 And then， well， we're done。 Okay。

 So let's see how this goes。 So I'm using a batch size of two and five， the sequences of five steps。

 Total sequence length is 30。 So in this case， well， I'm just， splitting out x and y pairs。

 So I basically have， you know， six， seven， eight， nine， ten。 And the y's are just shifted by one。

 So I get， you know， seven to eleven。 Likewise here， from 16 to 20， I get 17 to 21。 And that's。

 with that particular offset， as much as I could squeeze out。 And then， you know。

 there's another one。 One to five and eleven to fifteen。 I haven't covered this either yet。

 And the corresponding of y's。 So basically each of those blocks here is a mini batch。 Okay。

 And if I were to run this again， let me do it again。 I'll get something else。 Okay。

 So there's another way how to do it。 And that's basically sequential partitioning。 In that case。

 I just take my long sequence。 I break it up into， let's say。

 a half a mini batch of size three of three sub-segments。 I then basically fold those over， right？

 And here， another one。 This guy goes over here。 And then I go and trade it accordingly， right？

 So this will give me one， two， three， four mini batches。 And I'm going to read them in that order。

 Okay。 So this code， what you're seeing there， that's exactly that。 So again。

 I pick around them offset。 Okay。 Workout number of indices。

 So that's basically just trying to figure out how much data I have。 Then， since I have the targets。

 well， I need to basically leave one more term。 And then， yeah， I just have my trader again。

 except that now it goes in sequence through the data。 Okay。

 You may need maybe a few minutes at home to read through this。 Let me quickly show you what it does。

 So， similar situation as before， we had， you know， 30 observations。 In this case， I assumed， okay。

 well， we have basically sequence length of six， mini batch size of two。

 And so you can see the corresponding sub-sequences extracted。 So we have， you know， three to eight。

 it continues with nine to 14。 In the bottom here， we have 16 to 21， it continues with， well。

 22 to 27。 So if I were to run this again， well， in that case。

 only one fits because I just happen to be quite unlucky。 In terms of my offset， yeah。

 That's what you get。 Any questions？ Okay。

![](img/4fa8609d91cfeb3b3a3b2dbf7d41a715_9.png)

 [BLANK_AUDIO]。