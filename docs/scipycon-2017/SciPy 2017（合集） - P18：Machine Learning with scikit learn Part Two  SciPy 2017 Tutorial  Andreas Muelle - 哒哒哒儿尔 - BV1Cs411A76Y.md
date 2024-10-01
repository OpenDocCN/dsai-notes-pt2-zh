# SciPy 2017（合集） - P18：Machine Learning with scikit learn Part Two  SciPy 2017 Tutorial  Andreas Muelle - 哒哒哒儿尔 - BV1Cs411A76Y

 Yeah， I think we can get started。 So I'm just asking the Slack channel。

 So there's going to be a book of， a way for my machine learning book with Sarah on Thursday。

 if you want a book for free。 At four。 All right。 So let's come back。

 So we're going to continue where we， left off before the break。

 which is with working with text data。 So far we had categorical and continuous features。



![](img/92aed0107e5ed9540c8a768811cdbac0_1.png)

 And now we'll talk about basically how to work with long free texts。

 There's different kinds of texts。 So we had， for example， the name in the Titanic data set。

 The name is not really the way that， natural language works because they're usually relatively unique。

 Someone pointed out that if you check for Mr。 or Sir， something in the name。

 then that gives you some accuracy。 But usually when we talk about text data。

 what we mean is like long free text， like an email or a book or a product review。

 And so these are very different from the numerical data we had so far。 Because the text has like。

 it's not numbers， it's strings， and they have varying length。 And they can be very long。

 And the links doesn't necessarily inform us a lot about the content。

 So we need to have a way to break up or transform these string data。

 into some numerical representation。 So let's say we want to do spam detection， for example。

 just from the text of an email。 So we start off by just having a string。

 So each sample now is one string。 So say one of our samples is this is the string。

 this is how you get ads。 And so now we're going to transform this to numerical representation。

 using the back of worked feature extraction。 The first step is to break this up into words。

 or some normalized form of words， which is called tokenization。

 There's like in the natural language processing community。

 there's like a lot of very complex ways you can do this。 We do something very simple。

 We basically split by white space and then lowercase everything。

 And this gives you sort of normalized words that we call tokens。

 Then you do this for each text in your train data set， and you build a vocabulary。

 So this will basically give you something like a dictionary， of all the English language。

 which might have some domain， specific words。 For example， if you do movie reviews。

 you might have a lot of actor names and movie titles。 So once we built this whole vocabulary。

 we can encode each individual sample。 And the way we do this is for each word of a vocabulary。

 we count how often this is a word appear in our sample。 So here we had the sample。

 This is how you get ants。 And so most words in English language， don't appear in the sentence。

 So they're all zero。 The word ants appears once， the word get appears once。

 the word you appears once。 The word this appears once to。 And none of the other words appear at all。

 So we have a fixed length vector now， which is as long as the vocabulary size。

 So that's usually tens of thousands or hundreds， of thousands of entries。

 And basically all of them are zero。 As Alex mentioned in the beginning。

 we don't really want to store all these zeros， because we're very wasteful。

 So we use a sparse matrix representation， that only stores the words that actually appear。

 This is called the bag of word representation， because you only count the absence on presence of words。

 So it's kind of shoving all the words into one big bag， and you don't really care about the order。

 So no matter what the order is of the words， this will give you the same representation。

 So now we have a very large representation， but it is like an numerical representation of the data。

 And so now we can do any kind of machine learning with it。

 So let's show how to do this with scikit-learn。 So here I have x， which has two data points。

 One is the string。 Some say the world will end in fire。 Second one is some say in ice。

 So I have two data points。 And now I can use the count vectorizer， which。

 implements the bag of words encoding。 So this is a transformer。 So we instantiate it。

 and then we can fit and transform data。 So fit just builds this vocabulary。

 This is a very small data set， so it only has， I don't know， we'll probably see。

 Only has a couple of words in it。 Usually， as I said， this will be tens of thousands or hundreds。

 of thousands。 So here we only have these couple of words， and fire eyes and say some， the will word。

 They're sorted。 And I can use the transform method， which， will give the numerical representation。

 which， is a sparse matrix。 Again， the rows are sampled， so we have two rows。

 And the columns are the different features。 Each feature corresponds to the frequency of one word。

 There's nine words in the dictionary， so x has to shape 2 times 9。 And there's 12 words in total。

 And so there's 12 non-zero elements in the sparse matrix。 Here。

 you can make this into NumPy array with two array。 And so you can actually look at all the entries。

 And I'm not going to go through all of this， but you can see that。

 And then fire appear in the first one， eyes in the second one， in say。

 and some appear in both of them， and then the rest appear only in the first one。 So here。

 everything is one or zero。 It could be any larger integer count。

 if the word would appear multiple times。 And so I said， if you--， basically。

 there's a method called inverse transform， which， tries to go from the output back to the input。

 And here in this case， you only recover， which words are present。

 because the order is not preserved。 So if you want to try to interpret the bag of words。

 representation of x， you can only， see that the second row had eyes in， say， and some。

 but you don't know the order。 There's a couple of variants of this， that I want to discuss。

 So this very basic bag of word actually， works reasonably well in many cases。

 So one modification of this is what's called TFIDF encoding。

 This is basically a rescaling of the representation。 So you start off doing exactly the same thing。

 but we want to give less weight towards that appear very， commonly。 So the word the， for example。

 is probably not very informative。 And so we might want to have our classifier pay less attention。

 to it。 So TFIDF stands for term frequency inverse， document frequency。

 And so term frequency means how often does a term， appear in a document？

 And inverse document frequency-- so document frequency， means how many documents does it appear in？

 And so the actual formula， is it here somewhere？ No。 The actual formula doesn't matter that much。

 But basically， you divide the counts of each word。

 in a document by the logarithm of the frequency over documents。

 So if something appears basically in all documents， it's going to be downweighted a lot。

 You can think of this as soft stuff words。 So stuff words that appear very often。

 and you often want to remove。 This does something similar， but basically。

 the more frequent something is， the less important that is。 What it also does is it normalizes。

 So basically， it applies to normalizer， which makes everything each row unit norm。

 And so here you can see the result of transforming， the same text again。

 So the zeros and non-zeros are the same as before， because the same words appear。

 So you can see there's fractions。 That's because we normalized everything。

 So you see the second row。 The numbers are bigger than the first row， because it's shorter text。

 And so-- or， sorry， because there's fewer non-zero entries。

 and because it's normalized there larger。 And you can see that for the first row here。

 the terms or the words that appear only in the first row， get 0。39。

 whereas the ones that appear in both get a 0。28。 And for the second one。

 the ones that appear only in the second one， get a 0。63， the one that appear in both get a 0。45。

 All right。 So basically， we're just downweighting stuff， low-earthmically that appears very often。

 And sometimes it helps。 Sometimes it doesn't。 It depends a lot on your data set and the structure of the data。

 Another modification of this basic bag of word representation。

 is using biograms or more general N-grams。 The idea here is that we recover some of the information。

 of the order of the words。 So for example， for some words， the order is really important。

 For example， if you say not and then a word， it means the opposite。

 So you really want to capture this。 If you have a sentence and you know not appears somewhere。

 but you don't know where it appears， you have no idea what the sentence means。

 And so what you try to do with N-grams， is you look not only at a single word。

 but you look at pairs or higher tuples of neighboring words。 So if you start with the string。

 this is how we get Ns。 The 1 grams or unigrams are just this and is and how， and you and get an Ns。

 And 2 grams are all pairs of two neighboring words。 So this is how you get get Ns。

 So you can think of it as like a sliding window of 2， that goes over the whole text。

 And you can do this for arbitrary lengths。 And so you can take all the overlapping windows。

 Very typical values of these are like 1， 2， 3。 The things if you have a very large corpus。

 these can grow very quickly。 So basically， they grow exponentially in size。

 unless you do some stuff to prune down the number of words。

 Because if you have a million single words， then you have often something like a million squared。

 2 grams and a million 2 power of 3 grams。 And you can't really store that。 Yeah？ [INAUDIBLE]。

 3 grams cross sentence boundaries？ Yes。 In the second learning implementation， yes。

 Because basically what we do is just we do the tokenization， step。

 which is we just split by white space。 And then we do a sliding window over these tokens。

 You can-- I'm sure you can find libraries that have， implementations that are more fancy than that。

 So maybe I should mention there's like an LTK and Spacy。

 are two center libraries to do more sophisticated stuff， with text。

 And sometimes they can give you some boost in performance。

 But this is sort of the very simple method， and it gives you a reasonable baseline。

 So to do N grams， you can use the N gram range parameter， which。

 gives you the minimum maximum length of tuples， that you want to look at。 So N gram range 2。

 2 means get all the one--， all the bi grams。 So minimum length 2 and maximum length 2。

 I do this on the fire and ice。 And these are the features that are extracted。

 and in fire in I say in say the--， some say and so on。 So these are all possible two grams。

 Actually， because this is like very short， very atypical text。

 the dimensions doesn't get much bigger。 But if we use unigrams and bi grams--。

 so here I do N gram range 1， 2。 So I look at all unigrams and all bi grams。 So this is this。

 Now I have twice as many features。 So yeah， more commonly you get more something。

 like Nealea Square。 So you get a lot more features。 One way to reduce this down again。

 is to look only at things that appear at least 10 times， or something like that。

 then you can bring down。

![](img/92aed0107e5ed9540c8a768811cdbac0_3.png)

 a number of features again。 So another way to encode text data。

 in particular if you have something like names， is character N grams。

 So character N grams do the same thing， as we just did with words， but with characters。

 This is usually not super helpful for normal text。 It's helpful for names or if you want。

 to find out the language or something， or if you want to categorize words into whether they are。

 a name or not a name， for example。 And you can do that by just setting the analyzer equal to char。

 So by default it's word。 You can set it to char and then it's， going to be a character analyzer。

 Sometimes that's also helpful for text， if there is a lot of misspelling or if there。

 is a lot of obfuscation， like people， using numbers instead of letters， for example。

 You can get the common word stamps， by looking at character N grams。

 Usually you'd take more than one or two， you take a sequence of five or six characters。

 And so here's all the bi-grams for the sum， say the world one and some say in the ice。 And yeah。

 So all of them look like they are one， but they also have a white space next to it。

 So what I'd like you to do as an exercise， is compute the bi-grams and trigrams from the set of Python。

 and treat each line as a separate document， and then compute the TFIDF encoding of the data。

 and find out what are the things that have the highest TFIDF。 And so here's a text you just need。

 to split it by new lines so you get separate documents。

 And so I'll give you like five minutes for that。 So all right。

 let's have a quick look at the solution。 So here we're splitting the zen by new lines。

 And then for bi-grams， trigrams and programs， we look at what's the most common N gram。

 So we create a convectarizer with N gram rate， where minimum and maximum are the number。

 We transform it。 And then the counts gives us just a back-of-word representation。

 We do some x is equal to 0。 This gives us the overall counts and the whole text。

 And then doing Archmax gives us the most common one。 So the most common bi-gram is better than。

 Most common trigram is better than。 And the most common 4 gram if the implementation is。

 Because that appears-- it's the only 4 gram， that appears twice， I think。 So then for TFIDF。

 we try with norm L2 and with norm equal， to 1。 So with norm L2， that means basically long text。

 get penalized。 Because everything is given the same length， that I've representation。

 So there's readability counts that has counts once。 Counts doesn't appear anywhere else。

 So the inverse document frequency is very high。 Because it doesn't appear anywhere。

 And it appears once out of two words。 So because it's very short and the word doesn't appear。

 anywhere else。 It's very high。 I think this is the Archmax that's returned now。

 But I think the same is true for readability。 Readability also doesn't appear anywhere else。

 So the Archmax is ambiguous。 If we don't do norm equal to non。

 we don't get the things relative to the size of the string。

 We just get sort of the more absolute counts。 And then we get special because special appears only。

 in one of the documents。 So again， the inverse document frequency。

 is very high because it's as rare as possible。 And the term appears twice in this one。

 So basically here， because we didn't penalize being longer。

 special appearing twice beats the count that only appears once。 Questions？ No？ OK。

 So questions on Slack。 So now， actually it said we do a text classification， with the IMDb data set。

 But actually we're doing text classification， with the SMS spam detection data set。

 So this is-- and that they are both fun。 So here， our data set is a couple of SMS texts。

 So here are the first 10 ones。 So I don't know if you folks remember texts。

 Or these are like what texts used to be。 So they are really short。

 I don't remember the character limit， but they have a very short character limit。 Originally。

 I think now， like phones do whatever。 And obviously， they have great jargon and spelling mistakes。

 And yeah， they're generally slightly weird English。 I think these are from the UK。

 but I'm not entirely sure。 There's dollars in here。 But you can see that a lot of them。

 are just sort of normal texts or what counts as normal。

 But then there are some that are clearly spam。 So here， free entry in a two week competition。

 to win blah， blah， blah。 And had your mobile 11 month or more， you are entitled to clearly spam。

 And so we want to detect whether an SMS is spam or not。

 And here you can see sort of what we have the data set。 And there's zero is ham。

 So it's normal message one is spam。 So it's a spam message。 There's 4。

800 normal text messages and 747 spam messages。 And so both X and Y， we just have a list of strings。

 Sorry， X is a list of strings。 Y is a list of zeros and ones。 As always。

 we split our data set into a training， and a test set。

 We set the test set size here to the value it's by default， anyway。

 Because this test is pretty imbalanced， so there's like， what's this？

 Seven times as many ham and spam messages。 So it's probably good if we stratify to keep this ratio。

 It also means that when we measure accuracy in the end， well。

 we maybe not want to use actually accuracy， because accuracy will be hard to interpret。

 And we might look at different metrics。 All right， so now we're going to use the convectorizer。

 with the defaults， which are only using 1 grams。 We fit on a training set。

 and then we transform the training， and the test set。 We can check out how big the vocabulary is。

 And actually， it's really small。 It's only 7，500， because we only have very few samples。

 and they are all very short。 So pretty small vocabulary。 So this is the size of our training set， 4。

000 something， samples with 7，500 rows， columns。 It's also interesting to look at what。



![](img/92aed0107e5ed9540c8a768811cdbac0_5.png)

 are these features that are actually extracted， so what are the words that are found。

 We can see that the first couple of words are all numbers。

 I guess some of them might be phone numbers， even。 I'm not sure how informative these are。

 and we could think about trying to get rid of them。 If you look somewhere in the middle here。

 you can see that these are relatively normal English words。

 I don't see any really obvious misspellings here， actually。 You see several forms of the same word。

 crash， crash， crashing。 I'm not sure what crazy it is。 Well， this is。

 but generally looks like normal words。 So we also transform a test data set， so we have 1。

300 test samples。 Obviously， it names number of features。

 Now that we have this numerical representation of the data。

 we can just apply any cycle to learn model。 As we mentioned before， linear models。

 are particularly well suited to text data。 In particular here， you can see that we have about twice。

 as many features as we have training data points。 So we could totally overfit everything here if we wanted to。

 And yeah， so having something simple like a linear model， might be a good idea。

 So binary classification task， so we use logistic regression。 So we fit it on the training set。

 And now I use the score function and test set。 And you can see， OK， so it's 98。5% accurate。

 so it's very accurate。 Even though there's the strong class imbalance that was like 7， to 1。

 so I want to calculate what the default rate is。 Possibly。 But yeah。

 so this is clearly way above that。 And so we more or less solved this task。

 Depending on how important it is that we actually detect， all of the spam。

 But this is doing pretty well。 We can compare this to the training sets。 On the training set。

 we're basically near perfect。 We haven't overfitted everything。 If we completely overfit。

 we would have 1。0。 We could try to think about making the model a little bit。

 simpler and maybe get a little bit better on the test data， set。 But before we do this。

 we're going to visualize， some of the coefficients。

 So what I'm going to do is I have the classifier and the， feature names from the vectorizer。

 And we look at the coefficients， the linear coefficients， like these guys。

 So there's one coefficient per word。 And we're going to look at the ones that are largest in。

 magnitude， so the highest and the smallest ones。 And then we're going to plot them。

 And we get something like this。 I'm not sure how well you can see this。

 So the negative ones are associated with the class 0， so， with the not spam class。

 And the positive ones are associated with the spam class。

 First thing that I see is that the blue ones are much， bigger than the red ones。

 So it's easier to pick a word that's， indicative of being spam than being， indicative of not spam。

 And so you can look at this end here。 And it will tell you what are the words that are most。

 indicative of it being spam in their TXT UK， I guess， because it's some URL。 Ringtone， reply， call。

 text， one， chat， stop， new， claim， service， mobile， free， cost， message， price。 Yeah。

 and then some more URL stuff。 So here are the ones that are indicative of not being spam。

 Like there's some short hands。 There's pronouns like mine and he and sorry， which is。

 probably not often in a spam message。 And so it's like a relatively easy data set。



![](img/92aed0107e5ed9540c8a768811cdbac0_7.png)

 And with even this very small data set。

![](img/92aed0107e5ed9540c8a768811cdbac0_9.png)

 we can do a pretty good spam detection。 So one way to try to regularize a model， make it simpler。

 is to remove some of the features。 Particular here， I use minDF equal to 2， which means I only。

 include words that have a minimum document frequency of 2。

 So a thing that appears only in one text message is very， unlikely to informative。 So if I do this。

 let's see if I actually got better or worse。

![](img/92aed0107e5ed9540c8a768811cdbac0_11.png)

 I got a tiny bit worse on the test set actually， which is， somewhat surprising。

 But I want to see how many features there are。 So there's now only 3，400 features。

 So it's much less than before。 Maybe I actually want to also look at some of the--， No。

 in a whole corpus。 Basically， I kicked out everything that appeared only。

 once in the whole training corpus， because I feel like I。

 can't relearn anything if it appears only once。

![](img/92aed0107e5ed9540c8a768811cdbac0_13.png)

 And basically， half of the words appeared only in once。 And so you can see--， wow， some of the--。

 interestingly， some of these numbers are still there。

 So I guess they are used in multiple spam calls or messages。

 But the test accuracy is a tiny bit lower， but I would。

 probably trust this model more just because it uses much， less features and is nearly as good。

 We can also do visualization of the coefficients。 And yeah。

 I actually don't really see a big difference。 Because the ones that are important。

 that were all the。

![](img/92aed0107e5ed9540c8a768811cdbac0_15.png)

 ones that appeared more commonly anyway。 Yeah？

![](img/92aed0107e5ed9540c8a768811cdbac0_17.png)

 If one wanted to assign a much bigger penalty for a， classified， non-spam， message to spam。

 the reverse， situation， so would it be easy to do that？



![](img/92aed0107e5ed9540c8a768811cdbac0_19.png)

 Yes。 So there's multiple ways to do this。 The easiest way is basically to change your interpretation。

 of the outcome。 So right now， like logistic regression gives you a， probability estimate。

 And right now， it thresholds the probability as 0。5。 So if the probability is higher than 0。5。

 you say it's spam。 And the easiest way to achieve what you want is basically。

 to change this threshold。 Right now， you have to do that manually， but I think that。

 is sort of the best way to do it。 And this way， you can--， I mean。

 I think we talked about this a little bit later， but。

 there are several ways you can think about how important， are false positives or is false negatives。

 And depending on what the trade-off is or on what kind of。

 cost you assign to the different kinds of mistakes， you， can adjust your threshold。 So yeah。

 I wouldn't actually put this in the machine learning， model。

 I would put this in the decision making after the， machine learning model。 All right。

 so here's a summary of the machine learning with， text， but also with all kind of different things。

 modalities that are not just standard numeric data。 So basically， you want to use the vectorizer。

 which like the， dict vectorizer or the con vectorizer here in this case， and create feature vectors。

 And then we can use the feature vectors together with some， supervised information， some labels。

 to fit the model。 And of course， we need to use the same vectorization method。

 for any new documents。 So as a result， I would like you to--， sorry， as an exercise。

 I would like you to use the TFIDF， vectorizer instead of the con vectorizer。 Compare the results。

 Are they any better？ Are they any worse？ How are they different？ How are the coefficients different？

 You can look at the largest coefficients again。 And how does changing the min-DF and the n-gram range for。

 TFIDF and con vectorizer？ How does this change the outcome？

 And how does this change the important features？ And so maybe I'll give you like 10 minutes to play around。

 with that。 All right， let's have a look at the solution。



![](img/92aed0107e5ed9540c8a768811cdbac0_21.png)

 So here the code basically doesn't change for TFIDF， vectorizer。 We just do the same thing。

 We did before with the con vectorizer。 We instantiate it。 We fit it on the training data。

 Then we call the transformation of the vectorizer on the， training and the test data。

 And then here I fit the logistic regression model， compute the scores on training test data。

 and look at the， coefficients。

![](img/92aed0107e5ed9540c8a768811cdbac0_23.png)

 So here you can see that the model actually performs。



![](img/92aed0107e5ed9540c8a768811cdbac0_25.png)

 quite a bit worse。 Though there are some parameters。



![](img/92aed0107e5ed9540c8a768811cdbac0_27.png)

 Actually， let me try this。 Well， if you change parameters in logistic regression。



![](img/92aed0107e5ed9540c8a768811cdbac0_29.png)

 which we didn't do， then you can get about the same。



![](img/92aed0107e5ed9540c8a768811cdbac0_31.png)

 performance。 There's a lot of different things to tune basically。



![](img/92aed0107e5ed9540c8a768811cdbac0_33.png)

 With the default parameters of the logistic regression， so。



![](img/92aed0107e5ed9540c8a768811cdbac0_35.png)

 you get 97% accuracy， which is worse than what you got。



![](img/92aed0107e5ed9540c8a768811cdbac0_37.png)

 before。 But yeah， so here， what I did now is at the。



![](img/92aed0107e5ed9540c8a768811cdbac0_39.png)

![](img/92aed0107e5ed9540c8a768811cdbac0_40.png)

 increase regularization a little bit， and then you get， something like this here。

 which I can't really， interpret。 So now let's see what happens if we change the。



![](img/92aed0107e5ed9540c8a768811cdbac0_42.png)

 Mindy-Affin-Engram range。 So I'm just going to run through one thing here。

 You can see by yourself how this changes the number of， features， for example。

 Let me actually do this here。 So here， wow。 I only got 1，000 features if I use the。



![](img/92aed0107e5ed9540c8a768811cdbac0_44.png)

 n-gram range 1， 2， 3， and do Mindy-Aff equal to 10。

 Let's see what happens if I do Mindy-Aff equal to--， let's do three。 Three seems more reasonable。

 Then I have about as many features as I had originally。



![](img/92aed0107e5ed9540c8a768811cdbac0_46.png)

 with the 1-grams。

![](img/92aed0107e5ed9540c8a768811cdbac0_48.png)

 You see that in the top features， not many of them show up。



![](img/92aed0107e5ed9540c8a768811cdbac0_50.png)

 Your call 1， 2， are you show up and have to。

![](img/92aed0107e5ed9540c8a768811cdbac0_52.png)

 But for the spam ones， nothing really shows up。 I think there was someone you used Mindy-Aff equal to 10。

 Yeah， you have。

![](img/92aed0107e5ed9540c8a768811cdbac0_54.png)

 Which is-- yeah， makes sense。

![](img/92aed0107e5ed9540c8a768811cdbac0_56.png)

 You have one x-x。 All right。 Questions about this？ All right。



![](img/92aed0107e5ed9540c8a768811cdbac0_58.png)

![](img/92aed0107e5ed9540c8a768811cdbac0_59.png)

 So， yes。 So basically， adding more n-grams will make a dictionary， much larger。

 but increasing minimum document frequency， you can make it a little bit smaller again。

 So if I don't use minimum document frequency， you see I get 83，000 different 3-grams。



![](img/92aed0107e5ed9540c8a768811cdbac0_61.png)

 And I get very specific features like ringtone king。 So， yes。

 that's enough for doing text classification for now。



![](img/92aed0107e5ed9540c8a768811cdbac0_63.png)

![](img/92aed0107e5ed9540c8a768811cdbac0_64.png)

 So what we're going to do next is talking about model， evaluation， particular crystallization。

 and different ways to score a model。 So we saw already accuracies， maybe not always。

 the right answer for classification。 And we also saw that the results you get depend a lot。

 on how did you split your data set。 So what we did so far is we used our data set。

 We split it into training and test part， build a model on a training part。

 find a model on a test part。 So as we saw， it's kind of not really that robust。

 because changing the split changes the outcomes quite a bit。 Also。

 it means you have less data to train your model。 Because basically。

 if you want to have a good estimate， of how well your model does， you。

 want to have a lot of test data。 But it means you have less training data。

 which means that your model will probably be worse。

 So the standard technique to combat this and get a more robust。

 estimate of what our model does is called， K-fold cross validation。

 The idea here is that we split our data into so-called fold。

 So let's say we use five equally sized parts。 Instead of doing training and test。

 we do these five parts。 And now we build five different models。 For the first model。

 fold one is the test set， and the remaining four folds are the training set。

 Then I build a second-- so I build on a training set， I score on test set。

 I get one accuracy value or whatever my metric is。 Then I build a second model for the second split。

 where fold two is the test set。 And again， I get my score。 And so I repeat this five times。

 Now I have five different evaluations of my model。 I can see what's the difference in these。

 Does it depend a lot on the split of the data， what the outcome is？

 And I can also compute the mean of them， for example。

 or the median to have a more robust evaluation。 What's also great about this is that splitting in this way。

 each data point is in the test set exactly once。 If you split your data just once and randomly。

 you could be very lucky， and all the hard examples， are in the training set。

 Or you could be very unlucky， and all the hard examples， are in the test set。

 And so there might be a lot of variance。 But if you do a five-fold cross validation。

 then all the data is in the test set exactly once， and in the training set exactly four times。

 And so you can average out a lot of the variance。 Can anyone come up with a shortcoming of this method？

 Oh， yeah， if the data is ordered， then this is not a good idea。 Yes。

 Because then you should also just do it randomly。 Order data as a whole thing by itself。 Yeah。

 So here， this takes five times as long。 So usually people do five or 10-fold cross validation。

 Or you can also do repeated cross validation， but you do five-fold cross validation。

 but shuffle the data five different times。 So you have 25 evaluations。

 So you spend at least five or 10 times as much time。 Also。

 the outcome of this not only is not a model。 It's like five scores。

 So if you want to actually train a model， I mean， usually the way to do it is retrain a model。

 This only tells you how good is a model。 It doesn't really provide your model。 Right。

 so now let's apply cross validation to the nearest， neighbor classifier on the iris data set just。

 to get a feel of how this works。 So basically what you want to know is how well。

 does a Kenya's neighbor classifier do on the iris data set？ So we load our iris data set。

 We have x and y， and we have the classifier。 Actually， do we actually want to do this？ Well。

 all right， let's do this。 So the data in iris is sorted。 So to get rid of some silly side effects。

 we're going to shuffle it real quick。 And so if you wanted to implement cross validation yourself。

 it's relatively easy。 Where relatively easy is like 15 lines。

 So basically what we take is we take--， don't want to run through this。 Well。

 I think you can really code very yourself。 But we create a test mask， which basically is full size。

 once or full size times true。 And then the rest is negating that gives you a test set。



![](img/92aed0107e5ed9540c8a768811cdbac0_66.png)

 Sorry， I gave you this training set。 And so here is the mask we get。 So here。

 the Boolean mask for a test set， is the first 30 samples in the first split。

 the second 30 samples in the second split， and so on。

 So the y is the data that's in the training set， and the black is the data as in the test set。

 And so for each of them， we computed a score。 So this is accuracy。

 And so we have five different accuracy values。 And you see they go between 90% and 100%。



![](img/92aed0107e5ed9540c8a768811cdbac0_68.png)

 And they have a mean of 69%。 So this is also-- so on a real application。

 I would be slightly concerned because that's， a pretty big standard deviation。 So yeah。

 that is because there's not a lot of data。 And because the model is pretty complex， I think。

 But so if I only told you it's 96%， you might think， oh， this is great。 But if I tell you。

 maybe it's also just like 90%， you might think differently about the model。

 So having an uncertainty estimate is cool。 OK， because this is such a commonly used method。

 nearly we have a function for this in scikit-learn。

 which is called cross-vault-score in the model selection， module。

 And the cross-vault-score function takes a classifier。

 Here this was an instance of our Kenya's neighbors。 And the data x and the labels y。

 And then it computes the cross-vault-score in accuracy。 So by default。

 it uses five-fold cross-vylidation。 We can set cv equal to a number and do-- sorry。

 a default does three-fold。 We can do five-fold or ten-fold or whatever fault we want。

 by setting an-- yeah？ So when you participate， you want to keep the ratio of each。

 added or used original data。 Yes， the question is， do you want。

 to keep the ratios between the categories？ Yes， you do。 This is called stratified cross-vylidation。

 where basically， yeah， you make sure that in each fold。

 you have the same fraction or the same ratio between classes， as the original data set。

 And that's what we're doing by default here。 So whenever you give it a classifier。

 then it'll do stratified cross-vylidation。 So if you want more control over what's happening there。

 there's some cross-vylidation generators， that are used to generate these splits。

 They're all in the model selection module as well。 So the standard ones are k-folds。

 which is just splitting， basically arbitrarily， stratified k-fold。

 which takes the class into account， shuffle split， which does repeated random splits。

 We actually also-- it's not released yet， but we also have repeated k-folds and repeated。

 stratified k-fold。 [INAUDIBLE]， So these iterators have split method， which take the data。

 and the targets and then generate some splits。 So here， for example， this is the stratified k-fold。

 with five splits on the iris data set。 It's maybe a little bit hard to read。

 but it only sees for a test set in the first fold， are the first 10 samples。

 then the samples from 50 to 60， then the samples from 100 to 110。

 So it'll be easier to look at this as a mask。 So this is sort of how the test mask looks on the iris data。

 set。 So the point is that the classes are sorted。 So this here corresponds to the first class。

 This here corresponds to the second class。 This corresponds to the third class。 And in each fold。

 you want to have a little bit of each of them。 Yeah？ [INAUDIBLE]， What's the problem？

 So the goal of cross-validation is to tell you--， model was a given set of hyperparameters。

 How good does it do on a given data set？ And it gives you an answer。

 And it gives you k different accuracy values， which you can aggregate。

 But you don't get a model out of it。 So if you want to model， for example。

 you could train on the whole data--， like if you say， oh， this result is good enough。

 I want to now apply this in my service， in my research， whatever。

 I train on the whole data set again， and then I have a model。

 But this is something that allows you to judge， is this a good model or not？

 And it allows you that more robustly than just， doing a single split。 Also。

 here's a comparison against--， so the top one is shuffle split。 It's stratified， k-fold。

 This one is k-fold。 So k-fold just takes the first 30， then the second 30， and so on。

 So that's not great。 On the iris data set， because it's sorted。 I mean。

 if you just take more splits， it looks like this。 So shuffle split is also kind of interesting。

 Shuffle split allows you to just repeat as many times， as you want with a given test set size。

 So here， what we're doing is basically we repeat five times。

 and we always take 20% of the data test set just randomly。

 And so we can set out-- so do it just like--， so there are five times。

 We can do it 20 times and just randomly sample more。

 This is nice because it decouples the size of the test set， from the number of repetitions。

 but it also， means that the same data points can--， not all the data points are in the test set。

 the same number of times。 So for that reason， I prefer repeated k-fold cross-validation。

 And repeated k-fold cross-validation， I do k-fold。

 and then I shuffle the data and then do k-fold again， multiple times。

 So-- and maybe just as a very quick exercise。

![](img/92aed0107e5ed9540c8a768811cdbac0_70.png)

 And if you want to use any of these generators in cross-vault， score。

 you just need to instantiate the method--， or instantiate the generator and give it as a CVR argument。

 So the CVR argument can either be a generator， or it can be an integer。

 And just as a very quick exercise， you can use cross-validation on the RSD test set。

 just a standard k-fold cross-validation with three folds， and see what happens。 [VIDEO PLAYBACK]。

 [END PLAYBACK]， [END PLAYBACK]， [END PLAYBACK]， [END PLAYBACK]， [END PLAYBACK]， [END PLAYBACK]。

 [END PLAYBACK]， [END PLAYBACK]， [END PLAYBACK]， [END PLAYBACK]， [END PLAYBACK]， it's 000 0。 Why？

 Yes。 The test set isn't always an unseen class。 So there， you split it into。

 thirds and each third is a different class so that there's no overlap between the training。

 set class and the test set classes so it can't do anything。 So you can get rid of this either。

 by shuffling the data or by using certified K-fold。 But by default， K-fold does not shuffle。

 and like it learn。 And that gives you these nice results。 All right。 So next I want to。



![](img/92aed0107e5ed9540c8a768811cdbac0_72.png)

 talk a little bit more about model complexity and selecting parameters of the model。 We already。

 talked in the beginning about how the number of neighbors changes to behavior of the K-neighbors。

 classifier or K-neighbors regressor。 So here's again like some illustration。 It shows you。

 this was sort of I think the thing that we used in the beginning where green is your。

 training data set。 The function is like this periodic function that goes up and here in。

 red I show different fits。 And if you use two neighbors you get the super wiggly function。

 that is way too noisy if you use， but it goes basically through nearly all of the training。

 data points。 If you use five neighbors you get those function that's pretty smooth and。

 pretty well approximates the true function。 And if you use 20 neighbors we basically smooth。

 the way the periodicity at least partially and we're sort of left mostly with this overall， trend。

 And so this is， so maybe you would say the model in the middle has about derived。

 kind of flexibility。 One on the left is too flexible it's overfitting the data it's focusing。

 too much on each individual data point whereas the model on the right is sort of too rigid。

 and doesn't really capture all the variation in the data。 So these are sort of the two concepts。

 of underfitting and overfitting。 Underfitting means your model is not complex enough and。

 overfitting means it's too complex。 And they're sort of a general trend in how training and。

 generalization relate to this。 So if you model complexity。 So if you have a model that's very。

 simple so it's very too to left。 Let's say this one is sort of very simple because it's。

 very smooth。 Then you will do badly on training and test sets but you will do equally badly。

 You can't really capture the variation in the training data sets but you can't， also。

 you don't focus too much on a training data set。 So you're equally badly on training and。

 test data sets。 If you allow your model to be more and more complex the training accuracy。

 or whatever your metric is will go up and up and up。 And if you allow the model to basically。

 learn the data set by heart you're going to get 100% accuracy on the training set。 As。

 the model complexity increases you also start to get better and better in generalization。

 performance because you're able to capture more of the variance in the data and more， structure。

 But there will be a wider and wider gap between what's your performance on the。

 training data set and your performance， your generalization performance on a test set。

 And so at some point if you make your model too complex the generalization performance。

 will actually go down。 And so somewhere there's a sweet spot of where the model has the right。

 complexity that generalizes the best。 And so a lot of like parameter tuning and finding。

 the right model is about finding the sweet spot where the model can capture enough of。

 the structure of the data but doesn't overfit。 But that's sort of more a mental image。 It's。

 not so how to do this。 It's usually pretty tricky in practice。



![](img/92aed0107e5ed9540c8a768811cdbac0_74.png)

 So here we're doing the thing。 I'm running this tiny test set with the sine wave again。

 Didn't want to plot it。 I thought it plotted it。 Well， okay。 So I'm doing the sine wave。

 and I try neighbors， K neighbors， with different numbers of neighbors。 1， 3， 5， 10 and 20。 And。

 so basically the way that I want to find a sweet spot is by doing a brute force search。

 I try each of them and I do cross validation and then I compute the average cross validation。

 score and then I might want to pick the one that has the best cross validation accuracy。

 and R square。 So this would be this one。 So maybe I said 10 neighbors is the best。 All， right。

 There's also a function that can help you to visualize this a little bit better。

 which is the validation curve。 Not validation plot。 So here you can see how the， it's not， accuracy。

 is it？ It's actually R square。 How does change this with the number of neighbors？

 And you can see this kind of reflects the curve that I had up in this sort of cartoon。

 And so if the model is very simple， which means a very high number of neighbors， high。

 number of neighbors corresponds to something that's very smooth， then the model does pretty。

 bad both on trading and test data set。 And then if I increase the number of neighbors。

 the model becomes better and better。 And then probably the best model is somewhere here。

 And then if I increase the number of neighbors even more， then we're overfitting the model。

 the accuracy on the training set goes way up。 The accuracy on the test set goes way down。

 So in general， a model usually has many parameters that might want to search。 And so we have。

 an example of a different class that we're not actually going to go into in detail。 So。

 more about that later is a lie。 So the sport vector regression， for example， has two important。

 parameters， C and gamma。 And so if you want to adjust these parameters， you do a brute。

 force search over all possible combinations usually。 And so I can do a cross-vault score。

 for each of them。 And then I can see that this one is probably pretty decent。 Or maybe this， one。

 And so because this is actually common pattern， again， we have a helper for this in， scikit-learn。

 which is called grit search CV。 Grit search CV is what we call a meta-estimator。

 because it takes a model， for example， support vector regression or linear regression or whatever。

 model you have。 And it creates a new model or a new estimator that uses this model internally。

 but also finds the best parameter for you。 So the way this works is you instantiate the。

 grit search CV with the model for which you want to adjust the parameters。 And then a， param grid。

 And the param grid is a dictionary which has as a key the parameter names。 So。

 for the sport vector regression， we have C and gamma。 And then as values， all the different。

 parameter values you want to try。 And what it does is it searches the product space of， these two。

 So all possible combinations。 And then you can also specify cross-validation， method。

 So here I think we did just k-fold。 And we tell it to be verbose so we see what's， happening。

 So this just constructs a new estimator， a new model， built on the sport vector regression。

 which does internal cross-validation to find the best parameters。 So when I call fit， what。

 it does is for each possible combination of these parameters is does the cross-validation。

 it finds the parameter that has the best cross-validated average score。

 And then it refits the model， on the whole data set that I pass it in。

 So here I pass it all x and y。 So it will refit， the whole model on x and y。

 And so here tries all possible combinations。 Blah blah。 Sorry， about that。

 And then because the scripts are a C。V。 is an estimator， it has fit and predict， and score。

 And so if I want to make a prediction now， I can just call predict。 And predict will。

 use the best model or the parameters that the model with the best parameters as found。

 by cross-validation trained on the whole data set。 So we actually don't have to worry about。

 what the best parameters are。 We can just call predict or score。 If we want to find out。

 what the best parameters are， we can look at the grid dot best param set tributes。 So。

 C equal to 10 and gamma equal to 1 where the best parameters。 And you can also look at。

 what the best cross-validation score is and best dot and grid dot best score。 So that's。

 the mean over all the cross-validation folds。 So what you still need to do here is you need。

 to know which parameters to search over and what the possible candidate values are but。

 you want to search。 And there's a lot about that in the documentation and the examples。

 And it's basically something that a sort of expert knowledge that hopefully is done， we。

 done a good job in the documentation to explain。 So for example， for this particular scene gamma。

 you use logarithmic search range。 So I didn't do 1， 2， 3， 4， 5， 6 but I did something that。

 is like exponentially increasing。 So the thing is that you might be tempted to use the best。

 cross-validation score and say this is how well my model does。

 The problem is this is too optimistic， because we train now， I don't know。

 how many combinations there are。 What did it do？ 1， 2， 3， 4， 5， 6， 7， 8， 9。 Okay。

 we did cross-validation nine times。 And this is the best out of these， nine。

 And so that means I use this score to select the best。 And so this means it's not。

 really an unbiased estimate of how well I will do on new data anymore because I selected the best。

 And so if I actually want to have a good estimate of how well this model will do in the future。

 I need to use an additional training test split。 Before we go into this， actually， I want to show。

 you how to analyze more the results of grid search。 So we have this best score and best。

 params but we also have CV results which is a dictionary that contains a whole bunch of things。

 So it contains for each split of the data the fit time， the， sorry， for each parameter combination。

 and each contains the mean fit time， the standard deviation of the fit time， score time， and so on。

 the parameter settings and for each of the splits that we have， the scores of the split。

 So that's the big table。 So the easiest way to look at it is using pandas。 So from the， dictionary。

 I create a pandas data frame。 And so each row here corresponds to one combination of。

 the parameters C and the parameter gamma。 And so you can see the scoring time and fit time。

 And where's the mean？ Yeah， the mean test score and mean training score， for example。



![](img/92aed0107e5ed9540c8a768811cdbac0_76.png)

 And so here we can look at the ones that have the， so these are the five samples that have the。

 highest test score if you're interested in the ones that have like generally good parameter。

 settings。 So I subset at a table here with just the parameter scene gamma and the test score。

 Actually， maybe I want to do the trans scores as well。 And so I sorted them by the test score。 Wow。

 they have widely varying trans scores。 I guess these are also widely varying test scores。 I mean。

 this is really a lot better than the other ones。 So I probably would use this one。 All right， yeah。

 so as I said， this is not really a good way to evaluate。 So this is。

 a good way to pick the parameters， but it's not a good way to evaluate how well will the student。

 the future。 A way to， another way to think about it is。

 let's say I use a model that has some randomness in it， and I train it a million times。

 and then I look at all the outcomes and I take the best one。 This is probably just the one that。

 randomly did best on this particular test set。 That doesn't mean it will randomly do best。

 on future data at all C。 So as I said， the solution to this is to have a separate test set。

 So we split our data and then training in a test set。 Then we do cross validation to find。

 parameters only on a training set using grid search CV。 And then we do a final evaluation on。

 a test set to see how good this is best model generalize。 Sure。 Okay， so I should have。

 I have a flow charge for doing this too， but it's not in the， slides unfortunately。

 So you started with your data set and you built a training set and a final。

 test data set for evaluation。 Use the training set to do cross validation to find the parameters。



![](img/92aed0107e5ed9540c8a768811cdbac0_78.png)

 using grid search CV。 Then using the best parameters。

 you build a new model on the whole training set。 Then you want to know how well this is model generalize to new unseen data。

 And so you do。

![](img/92aed0107e5ed9540c8a768811cdbac0_80.png)

 basically one final evaluation on the test data set that you held out。

 This will give you an unbiased， estimate of how well the model with these parameters will do in the future。

 The question is， did we end up where we started？ Kind of， because we are now using a single split。



![](img/92aed0107e5ed9540c8a768811cdbac0_82.png)

 into training test data in the outer loop。 So if you want to go crazy， you can also， you can。

 replace this outer loop by another cross validation， which is， so then you call it nested cross。

 validation。 But then again， the outcome is not a model， but the outcome is how well does a model。

 on which I tune to parameters perform in the future。 Because each inner split can find the best。



![](img/92aed0107e5ed9540c8a768811cdbac0_84.png)

 different settings of parameters。 And I think it's kind of complicated then。 So， yes。

 using a single， split of the data is not ideal， but it's kind of tricky to work around that。

 The idea here is that， you look at this test data only once。

 That still means it has a lot of variance， but you at least。

 you don't end up overfitting it by looking at it too often。 All right， so here。



![](img/92aed0107e5ed9540c8a768811cdbac0_86.png)

 luckily， I mean， what happens is kind of complicated， but the implementation is very， simple。

 Actually， I don't know why we did， I wish I would have left here。 I guess we want to shuffle。

 So if you don't want to shuffle explicitly， you could just try 10 here instead of instantiating it。

 But so what you do is split your data into training and test set。 You define your parameter grid。

 you define your cross validation if you really want to。 You instantiate grid search with the model。

 and the parameters。 You fit the model on the training set。 This does all the nested cross。

 validation parameter search。 And then you do a score and score will use the model with the best。

 parameters trained on the whole training set。 And you evaluate it on a test set。 And yeah。

 and if you want， you can still look at the parameters that are where selected。

 So this is sort of the possibly not very best you could do， but this is sort of， I think。

 what is good practice。 What you can also do is just do a split of the data into three parts。

 This is usually what people do if they do deep learning， because training a model just takes。

 so much time that you don't want to spend time doing cross validation。

 So the minimum you need to do is basically have a training set。

 have a validation set to set parameters， and then have a final test set for evaluation。

 You can also do this with scikit-learn。 And， the easiest way to do this is just use shuffle split cross validation with the number of splits。

 equal to one。 So that basically means the inner cross validation loop only has a single split into。

 training and validation。 Then you can do the same thing。 Only it's going to be much quicker。

 but the parameters might not be as good。 Actually here there's no difference。 Cool。

 So what I'd like you to do is， use grid search CV to find the best number of N neighbors in K-neighbors classifier applied to the。

 dataset。 So what the digits dataset， split it into training and test set， do grid search。

 You need to define the parameter grid for N neighbors and then run the grid search。

 And please really， really try to do this before loading the data， because this is something。

 if you want to do machine learning in a real world， you will always have to do this。 So please。

 give it a go。 All right， maybe let's continue because we're way behind time。

 So just to go through the solution， so we're loading the digits dataset， we just put it into a。

 training and test set。 Ideally， we would also try to find。 Okay， if I have to。 There was a。

 I think there was like a blog post somewhere about people。

 looking at how many random states or how often 42 is used in GitHub relative to all other numbers。

 I'm not sure how much you're to blame for this。 Okay。

 so here the parameter grid is this time we only have one key and neighbors。 So N neighbors。

 against the parameter of the N neighbors classifier that we want to adjust。 Here I'm trying one。

 three， five， 10 and 50 that I just basically came up with。 So this should be much smaller than the。

 number of samples usually。 And so I say CV equal to five to do five-fold cross validation。

 give it a parameter grid and tell to be verbose。 And then I just call fit on a training set。

 So here you can see it has five-fold cross validation。 So for N neighbor equal to one， one， two。

 one， two， three， four， five different ones for three， again， five ones for five and so on。

 And then the score on the test set that we get is 98。4% accuracy and we achieve that with number。

 of neighbors equal to one。 So that's actually just using one neighbor is the best on the just data set。

 Questions about this？ All right， so we're going to skip 15 because we don't have that much time。

 So there's a method to change multiple pre-processing steps and classifiers。

 which is really awesome。 It's called pipelines and you should read up on it。

 We're not going to do it。 Instead， I want to talk a little bit more about model evaluation scoring metrics。

 So here are just a lot of digits and split it and train a model on it。 So by default。

 we use classifier。score， which is accuracy， but this is a very aggregate statistic。

 and mostly makes sense for balanced classification tasks。 It's very easy to interpret though。

 I mean， if I have 95% accuracy， it means I'm correct 95% of the time。

 At least it's easier to interpret with， balanced data set。

 Another thing that you should definitely look at is the confusion matrix。

 And the confusion matrix is much more fine-grained。 So here， this is for the digits data set again。

 Here， each row corresponds to one true class and each column corresponds to predicted class。

 And so basically this tells you how often was class i classified as class j。

 And so you want basically all the numbers on a diagonal to be high because these are。

 correctly classified ones and ones on all other entries should be small。 So you can also plot this。

 So here you can see the rows are the true labels and the columns are。



![](img/92aed0107e5ed9540c8a768811cdbac0_88.png)

 the predicted labels。 And so you can see that most of the mistakes are us predicting one。

 when it shouldn't have been one， for example， for the eight。 There were four eights that you。

 mistook as one。 And there were。 There's two fours that we mistook for one。

 And so you can find out what the mistakes are。 And yeah， so you see that we classified way too。

 many as one。 We also classified a couple of things。 I mistook them as nine。 Zero was very easy。

 There's no。 We never classified something else as zero wrongly and there's only one zero。

 that we doesn't classify as zero。 So this gives you a very fine-grained view into what happens。

 with the different classes。 But it's very hard to use this for model selection， grid search。

 because you can't really compare to confusion matrices and say which one is better。 There's another。

 A couple other metrics you might want to look at。 In particular precision and recall and F-score。

 These are all usually done for binary classification。 So in binary classification。

 we call one of the classes arbitrarily the positive class and the， other one negative。

 Usually the positive class is the one we're interested in。 So if you do， cancer screening。

 cancer will be the positive class。 But it's like sort of dependent on。

 the context and sort of arbitrary。 But depending on what which class you call the positive class。

 precision will be the true positives that is the correctly classified。

 positives divided by everything that was classified as positive。

 So true positives and false positives。 Do we have a picture here of the binary？ That's too bad。

 So PP， FP， FN， and which one FP are， basically the four entries of the binary confusion matrix。

 Let me just。 So this is the binary confusion matrix and this is。 So。 And you can。

 So this is the binary confusion matrix。 So positive classified as positive is true， positive。

 Positive classified as negative is false negative。 Negative classified as positive is false。

 positive。 Negative classified as negative is true negative。

 These are four numbers that are like very， fine-grained information about binary classification。

 And then there's like a whole， zoo of metrics you can derive from this。

 And so precision and recall are two that are very commonly， used。 And so these are basically。

 So precision is。 This entry divided by this row and recall is， this entry divided by the。 Sorry。

 this one divided by a column。 This one is divided by row。 So precision。

 says of the ones that are classified as positive， how many are actually positive。 And recall says。

 of all the ones that are positive， how many did I get？ Recall is also called coverage because。

 basically it's how many did I get？ And precision is how many of the ones that I got are actually true。

 And so depending on your application one or the other might be helpful。

 There's the F1 score is the geometric average of the two。 And so that kind of gives you some kind。

 of trade-off between these two values。 You can use the classification report to compute all of them。

 So these are binary metrics。 So if you do this with a 10 class classification problem such as。

 digits， you will get precision and recall for each class being the positive class。 So if the。

 if zero is my positive class and all the rest are the negative class， then precision is one and。

 recall is 0。95。 Support just needs the number of points in the class。 And then you can。

 for you can average these over different classes and these give you， different possible metrics。

 In particular for imbalanced classes， these can be better than just， using accuracy。

 So as an example， so for the digit dataset， by default， it's more or less balanced。

 where 10% of the data belongs to each of the classes。 Let's say we do a very imbalanced dataset。

 where we look at three versus all the rest。 Now we have a 9 to 1 imbalanced dataset。

 And now we can look at the score， for example， here。 I run cross-validation with a support vector。

 machine on this very imbalanced dataset and I get 90% accuracy。 Is this a good result？ No。

 Because it means if I always say it's not a three， I get 90% accuracy。

 So one could also argue it doesn't really tell us a lot to 90% because it might actually be sort of。

 the model might have learned something or it might not have learned something。

 but from the 90% alone we can't really tell。 But yes， if I use the dummy classifiers。

 just predict the most frequent class， I also get 90%。

 So a different way to look at this is would be， to look at the F1 score or precision and recall。

 What I often find even more helpful is to look at， the ROC curve。 So what the ROC curve is。

 it plots the false positive rate， where is the true positive， rate？

 True positive rate is the same as recall。 False positive rate is。

 false positives divided by false positives plus true negatives。

 So these are slightly different numbers than precision and recall， but they have。

 relatively similar interpretations。 But so what this curve does is it doesn't look at。

 only computing precision and recall or false positive rate and true positive rate， but。

 it looks at the continuous output of a classifier。 So here actually we。

 I tried a support vector machine with different values of gamma and I look at the decision function。

 So the decision function I mentioned earlier gives you a continuous uncertainty estimate。

 So this is just a binary task。 So here I get a number somewhere between positive infinity。

 negative infinity。 That tells me how much the model thinks it's class zero or it's class one。

 If I call predict， it'll give me zero whenever the decision function is below zero and one。

 whenever the decision function is above zero。 But often I don't。

 So this cutoff is not a good choice as I mentioned earlier。 So depending on is it more important to。

 have a high recall or a high precision？ Do I care more about getting all possible positives or。

 not making positive mistakes？ I might want to use a different threshold。

 So what the RC curve does is it goes through all possible thresholds。 So。

 basically at each value that appeared in a decision function， I do a threshold there。

 And for this threshold， I compute the recall and false positive rate。

 And so this gives me a continuum of all the possible trade-offs between true positive。

 rate and false positive rate that I could have。 And so here I drew these for three different values。

 of gamma。 For 0。1， 0。0， 0。0， 0。0， 0。0， 0。0， 0。5 and 1。

 And so all of the three have an accuracy of 90%。 Two of them have an AOC of 1， which is。

 the AOC is a summary of the curve， which is the area under， the curve。

 It stands actually for area under the curve。 And one has an AOC of 0。5。 So AOC of 1。

 means you're up here in the corner， which means you can get a false positive rate of near zero。

 with a true positive rate of one。 This means basically you made no false positives。

 but you got all the positives correctly， which is perfect classification。

 So what it says is there is a threshold。 If I pick this threshold， I basically get more or less。

 perfect classification for both of the first two settings。 For the third setting， I get。

 basically a diagonal line。 This is what you get for a chance performance。 It basically tells you。

 whenever I'm always as likely to add a true positive as to add a false positive， because they。

 sort of go with the same slope。 So all of these three models have the same accuracy。

 but some of them have perfect AOC and some of them have chance AOC。

 This tells you that this AOC is a much， much finer-grained metric to assess how good the。

 model is in particular for imbalanced data sets。 So it is 1 and 0。5。 These are independent of。

 how balanced or imbalanced the data set is。 So 0。5 will always be chance and 1 will always be perfect。

 So the reason why these have AOC 1 and accuracy 90% is probably the default threshold of 0。

 was not very good for this imbalanced data set。 So I encourage you whenever you do basically anything。

 always look at the AOC curve。 You can also look at the precision recall curve。

 which we don't have here。 That's sad。 That plots precision versus recall， again for all thresholds。

 And think about what kind of， trade-off you're interested in。

 It's very unusual that the false positive and the false negative， have the same cost to you。

 So these are， so this is the false positive rate， the true positive rate， and these are all the。

 possible thresholds。 These are just the unique values of decision function basically。

 So I look at all possible thresholds， so all thresholds that appear in the data。

 which is the decision function for each possible data point。 And for each of them。

 my compute false positive rate and true positive rate。 The warning is there is no multi-class。 Okay。

 yeah。 So right now there's no multi-class， implementation of AOC。 There's a pull request。

 but it's something like。 There's many ways to do it and there's no standard way in literature to how to do it。

 I think。 And so we're slightly undecided on what to do about this。



![](img/92aed0107e5ed9540c8a768811cdbac0_90.png)

 But for binary classification， it's definitely an amazing tool。 For multi-class classification。

 you can look at a PR， you can look at papers to see what kind of schemes people come up with。

 But so in the end， you need to basically figure out which trade-off is important for you。

 and then need a pick a threshold that is good for your trade-off。

 So if you want to use this metric or any other metric for cross-validation or grid search。

 you can do this very easily by using the scoring parameter of the cross-vault score。

 So there's a list of built-in scores。 For example， a rock AOC for the area on the curve。

 And if I do this， it'll just do cross-validation with rock AOC instead of accuracy。

 I could also probably do。 No， it's F1 micro-ride。 So if I put in accuracy， this is the default。

 You can look on the website。 There's all the different options you have explained。

 You can also look in this built-in scorers dictionary。 These are all the scores。

 Some of them are for classification， some of them are for regression。

 some of them are for clustering。 There's a lot。 And I think we're going to skip the exercise because we're running out of time。

 The exercise is about something called average per-class accuracy， which is also a nice metric。

 but not as commonly used。 [pause]， So yeah， we don't have that much。

 So definitely also look at the documentation on position recall curve。

 That's a similar curve that's sometimes a little bit more helpful even。 Do we want to break？

 I think we're going to break now， and come back in like 15 minutes。

 Then we're going to talk about linear models and trees， and forests。 And after that。

 I like to talk about some unsupervised methods。 So yeah， let's take a 50-minute break。 All right。

 So I'm going to talk a little bit about two families of models next。 Linear models and trees。

 These are two of the most widely used， most useful machine-lying models。

 And so I think it's good if you know a little bit more about them。

 So we're going to start with the notebook 17 in depth linear models。

 So we saw before a little bit about linear models for regression classification。

 So linear regression， was for regression， logistic regression for classification。

 And we want to talk a little bit， more about these models and related ones。 So for regression。

 we had this wonderful formula here that， I'll extra on the board and then I raised and he drew it again。

 And it's still there。 So in linear， models for regression。

 our output Y is a linear combination of the features。 So we have these， X test 0。

 It's just sort of the 0 is feature of test data point。 And we multiply this by the。

 coefficient we learned and we add these up for all possible features。

 And then there's some intercept， in the end。 And so let's look at how this works with a entire regression data set that we make here。

 which is 60 data points and 30 features。 And actually， most of these features are sort of noisy。

 and informative。 And that's just sort of a synthetic toy data set。 The simple method that we talked。

 about before is linear regression。 And here you can see the model that linear regression solves or。

 the problem that linear regression solves。 It's a convex optimization problem。 So here。

 the coefficients are called W and the intercept is called B。 And what we're saying is basically。

 that W times Xi plus B should be the same as Y in a least square sense。 So you take the two。

 norm of this， you sum it up over all the samples in the training sets over all the。

 eyes over all the data points we have。 And you want to find the coefficients W and the intercept B。

 that minimize this。 And this is a convex optimization problem。 And if you want， you can。

 throw like a center convex lever on this or you can just compute this with an SVD or many other。

 methods。 And so basically what this does is it says fit the training data perfectly with a linear。

 model or as well as you can with a linear model。 And so you can see that。



![](img/92aed0107e5ed9540c8a768811cdbac0_92.png)

 here the R squared and training set is pretty high。 It's about 0。87 and on a test set is 0。21。

 Because it's a synthetic data set， we actually know the true coefficients of the model。 So this。

 data set was actually generated with a linear relation。 Only we added some noise to it。 To both。

 X and Y。 And so after the noise we added or knowing the true model and taking into account the noise。

 with the true coefficients we could get an R squared of around 0。6。 This tells us that we really。

 overfitted the training set here and we're not doing it so well on the test set。 And clearly。

 there's like a really big gap between it training and the test set performance。 So we might want to。

 keep this model from overfitting so much。 So here is visualization of all the coefficients。

 So these are all the features。 I started them by， the true value of the coefficient in the true model。

 Obviously in the real world no model will， surely be linear but sort of this rather goes to illustrate more general points about the model。

 So if you have here these are your coefficients and this is what linear regression found and。

 so you see that many of them are much much larger。 So these are all 0。 Most of them are actually 0。

 But linear regression found very strong effects here。 So not great。 Yeah let's skip this。 Or well。

 it's real briefly。 So what you can see is also here we use that if。

 you increase the training set size things become better though。

 So linear regression if your training， set is pretty big will do well if your training set size is about the same magnitude as your。

 number of features you're likely to overfit a lot。 So here we have 30 features and so if you use。

 something like 40 samples you have get like very bad overfit。 But the more data so here we have。

 a synthetic data set so we can just sample more data from what we know is the model。 So if we use。

 more and more training data we overfit less and less and our tests error here actually goes up to。

 0。6 which is basically the true optimum。 So if I had twice as much data I could actually learn。

 the model but in the real world we can't really get it twice as much data usually or if you can。

 good for you if you can't you still want to be able to learn。 So we want to keep this model from。

 overfitting。 So one method that we talked about earlier is maybe do PCA reduce the number of features。

 but that's actually yeah so I don't like it as much but that's one possibility。

 Another option is to， use regularization。 So the most commonly used form of regularization for linear models is what is。

 called an L2 penalty。 The model that corresponds to this is called rich regression and it's very。

 similar to the model above。 So in addition to this term which says predict well on the training set。

 in the least square sense there's also another term that says the coefficients should be small。

 and there's an alpha which trades off between the two。

 If you set alpha equal to zero you get linear， regression。

 If you set alpha to infinity you get a coefficient vector that's all zeros and by changing。

 alpha you can go along this curve between overfitting and underfitting that we showed before。

 So here this is for the four different values of alpha and you can sort of see the curve that we。

 had before。 If alpha is very large we're penalizing a lot。

 We're saying the coefficients in double you， should be very small and so the training set score is not the best and the test set score also not。

 Then if you set alpha equal to 10 you get a test set score of 0。4 which is much better than what we。

 got with linear regression and if you decrease even more you overfit your training score is high but。

 your test score is low。 But so really this alpha parameter is a great way to control the complexity。

 We can also plot the coefficients。 So here's the same plot as above。

 only now with four different values of alpha。 So here alpha equal to 0。01 is very close to。

 what linear regression did。 Blue is a true coefficient and you can see with more and more。

 regularization basically all the points are drawn towards 0。 Yeah great search。

 There's slightly smarter things than great search but， basically great search。

 But yeah you need to do cross validation to find it。

 What you can also see here is that if you have a very high value of alpha then all the。

 large coefficients are pushed towards 0。 So this is not an unbiased model you buy us all。

 coefficients towards 0 which is why statisticians don't like this。 For predictive purposes it often。

 works very well。 And so again looking at training set sizes so here I compare。

 rich with alpha equal to 10 which was the optimum for I think for the 60 training set samples we had。

 and I compare it with varying training set size to linear regression。 And basically you can see if。

 your training set is very small using this penalty gives us a big improvement。

 Well here if you have， 40 samples you get worse than zero errors with linear regression but you get some reasonable。

 results with richer regression。 But if you have like many samples compared to number of features。

 you have they're basically indistinguishable。 So if you have a thousand samples and three。

 features then don't worry about it and don't grid search your alpha just use linear regression。

 If they're more similar in magnitude number of features and number of samples definitely try。

 richer regression。 So this is sort of the simplest way you can penalize linear regression to be more。

 simple。 There's another way that's very common which is called LaSueau which is an L1 penalty。

 Formula looks basically the same except the norm that we are using here is an L1 norm。 So before we。

 wanted the sum of squares of the coefficients to be small。 L1 norm is the sum of absolute values。

 So again we want W to be small we want the coefficients to be small。 But。

 so because of fun Kings of Mathematics maybe what this does is not only it pushes W to a zero。

 it pushes some coefficients to be exactly zero。 I mean you can think of this the L1 norm is the。

 convex relaxation of the L0 norm or something like this or you can just remember LaSueau。

 makes coefficients exactly zero。 And so this is great if you think most of your features are。

 useless or many of your features are useless。 Gives you a way to determine which are the useful。

 features。 So if you automatically so if you look at the this was richer regression even if I set。

 alpha to 100 which is like pretty big all the coefficients are non-zero。 They're all not super。

 big anymore but all of them are non-zero。 So my model is sort of hard to understand and it depends。

 on all of these features。 If I know that the true coefficients only a few of them are not zero。

 then I can use the LaSue model and discover automatically which ones are true。

 If these two model it's easier to understand and much more compact。

 Again I can do sort of a grid search for alpha or look at different accuracies for different。

 values of alpha。 Here you can see again sort of the same curve if you have very high。

 alpha you penalize the model a lot。 Both training and test scores are low。

 If you penalize a little bit， then the training scores go up。 Test scores go up。

 If you penalize too little you overfit。 We can but sort of to see that so this is very similar to what we saw in Rich。

 But if you look at， the coefficients it's quite different。

 So here you can see that if you set alpha equal to 10 or。

 to even to 1 a lot of these coefficients are exactly zero。

 And so when you write down the model you know， these features don't matter at all。

 And so here maybe only half of the features were actually。

 selected or maybe even less depending on the alpha parameter。

 Here's again what's called the learning curve how well generalized as a function of samples。

 Here LaSalle does better than Rich and linear regression。 The main reason it's true here is。

 because the true model we know the true model and we know the true model has most coefficients zero。

 In the real world you might not know this。 So LaSalle mostly works well either if you really。

 want to have something that's easy to interpret and has only very few nonzero coefficients。

 Or if you actually believe the true model to be what we call sparse to only have a few nonzero。

 coefficients。 In general it doesn't perform better unless this is true of like the real model。

 There's another model that's linked to here that I'm not going to go into detail which is called。

 elastic net。 Elastic net has both an L1 and an L2 penalty。 And so you have two parameters and。

 so basically you can interpolate between Rich and LaSalle and you can get the best of both worlds。

 And that's usually what performs the best in practice but you also you need to queue in two。

 parameters。 And again if you like if you have enough data just use linear regression because。

 it doesn't matter。 Questions about linear models for regression？

 So now we're going to do the same thing again for classification。

 So in classification we had a similar， decision function a linear combination only we looked at the sign of the results。

 I wrote it here， as greater than zero。 So if it's greater than zero predict one if it's smaller than zero I predict。

 minus one or something。 And so there's two models that basically implement this。

 logistic regression and linear SVC。 And for the purposes of this class they basically do the same。

 thing。 There's like they have different loss functions but I don't think we write them out no。

 So if you're interested in the math details one uses what's called the hinge loss the other one。

 uses what's called the log loss。 In practice I rarely found this to make a difference。

 The benefit of logistic regression is that it can estimate probabilities while linear SVC cannot。

 estimate probabilities。 And both of these models logistic regression and linear SVM you can have。

 an L1 penalty as in LASO or you can have an L2 penalty as in RICH。

 And here for historic reason the penalty is called C and it's more or less one over alpha。

 So a large C means less regularization a small C means more regularization。 And I could have made。

 the same plots as we saw above with the coefficient shrinking towards zero if you increase regularization。

 I thought that was kind of boring so I made a slightly different plot here。 And。

 here you have a 2D classification task binary classification and so on the left see a small so a。

 lot of regularization on the right sees large so less regularization and you have the decision。

 binary as a black line。 And so another way to think about it except for pushing the coefficients。

 towards zero which I find hard to imagine given this 2D line is it controls the influence of。

 each individual data point。 So if you look at this data set you might say oh blue is at the top。

 and red is at the bottom which sort of overall is true。 But you have these two outlier points this。

 one and this one for which this is not true。 If you have a lot of regularization the impact of。

 each individual data point is pretty small so you have a more or less horizontal line which says。

 blues on top red is at the bottom。 If you decrease the regularization you allow each individual。

 data point to have more influence。 And so basically the classifier tries harder to get each individual。

 point right。 And so if you said basically turn off the regularization you get something like this。

 where you get now one point more that's correctly classified so here we misclassified the right。

 point here is almost classified the right point here we classified the right point correctly。

 But now the vision boundary is much more crooked and it reflects less the sort of more global layout。

 You can't ideally would try to also classify this one correctly but that's impossible with a line。

 So you can think of the regularization either as pushing the coefficients towards zero or as。

 controlling the influence of each individual data point。 [ Pause ]。

 So maybe a little word about how to do how this works for multi-class classification。

 So I think for binary classification the formula is pretty clear。

 For multi-class it depends a little， bit on whether you use linear regression or logistic regression but in general you can think about it。

 as that's mostly true。 What said intuition is true is that you built a model for each class。

 versus the other classes。 So if I use linear SVC I will get this will build what's called the one。

 versus rest model。 So here I try to classify the gray point with the other points the black point。

 where the other points and the green point where the other points and I get three models and then。

 the model that is most certain will make the decision basically。 So if I call fit here I get。

 the coefficient which is of shape three times two that's number of classes times number of features。

 So I have three for each of the classes I have a different coefficient vector and for each of the。

 classes I have a different intercept。 And so here's a bunch of mod plot loop code that we don't need。

 to worry about too much but why did we do colors like this？ I don't understand why we did it。

 Give me one second。 I want different colors。 What's it called？ Is it called vega 10？

 They renamed it again right？ But they renamed it something right。 Does name is dedicated？

 Does anyone know the real name？ No more multi-geeks here。 Which ones？ These two？ This is green。

 This is orange。 And wow because I'm going to complain to my plot loop people because。

 this is now the standard color map and it's really really bad。 For continuous。

 If you plot multiple lines it'll use this。 If you plot three lines that's not great。

 Thanks for pointing that out。 Can someone make a note， to complain to Tom or Ben？

 When Ben comes in the next time we assault him okay？

 You see the guy with the classes that comes in regularly it's his fault。 Anyhow。

 Here are the decision lines learned by the three different models。

 So you can plot the coefficients and intercepts for each of the classes。

 give you a decision boundary and basically the one that gives you the highest decision value。



![](img/92aed0107e5ed9540c8a768811cdbac0_94.png)

 This will be the class。 So basically here this will be orange， here this will be blue。

 here this will be green and sort of the boundary is in between these lines exactly。

 And so basically you learned as many binary linear models as there are classes。



![](img/92aed0107e5ed9540c8a768811cdbac0_96.png)

 And so I want to as an exercise I want you to use logistic regression and classify the digits。

 data set and research the C parameter。 So C parameter you should search on a logarithmic。

 scale so 0。00， 1。01 and so on。 And see how that goes？

 You can also look at the coefficients if you want。

 And yeah also changed in learning curves that we plotted the buffs to the plots where we changed。

 the number of training data points。 How do they change if I change alpha？



![](img/92aed0107e5ed9540c8a768811cdbac0_98.png)

 And so maybe you can play around this for like five minutes。

 All right so let's look at the solution。 So for the grid search there isn't really anything new。

 It's just sort of so you practice more doing grid searches because you have to do them all the time。

 So we start by loading the digits data set we split it into a training and test set。

 We probably should stratify it which we didn't。 And then we define the parameter grid。

 The parameter we want to search is C。 So small C， high regularization， large C， less regularization。

 We instantiate grid search Cv， with logistic regression， primary grid and Cv equal to five。

 We fit it on the training data set。 And then， the we compute a test score and the best parameter。

 So the best parameter was 0。01， this one。 And the best test score is a 97%。 So we got 90% accuracy。

 And yeah basically whenever you use a linear model you should always grid search the regularization。

 and scale your data。 Except if it's digits then don't。 It's true。 [INAUDIBLE]， I am not， neither。

 So basically if the， if the magnitudes have semantic sense or like the differences in magnitudes are semantic then you。

 shouldn't scale but it's very rare but it's true for these pixel things。

 So here I did the same thing as above the learning curves and I just。

 the logistic regression against， rich in LaSue with alpha equal to 1。

 alpha equal to 10 and alpha equal to 100。 And so basically if。

 alpha equal to 1 we have very little regularization so rich in LaSue mostly behave like linear regression。

 as you can see here。 So they are like， they work somewhat better with。

 less training data but like the difference is smaller。 With alpha equal to 10 there was the best。

 results we got with grid search。 They are both much better so they get better results for all the。

 for all the numbers of training samples and they also get better results for like fewer training samples。

 If you set alpha very large you have a lot of regularization and so you can see that for both。

 rich and LaSue for very few data points they do pretty decently still comparatively。

 You can see also that the training data training error is much much lower so they're。

 much more underfitting and if you set alpha too large you can see here in the LaSue case it。

 basically never learns anything。 Probably all the coefficients are more or less zero all the time。

 even if you have a relatively big training data set。

 So if you're regularized too strongly you might not。

 get the same performance as if you didn't regularize。

 And here even with rich your performance is not as， good。

 I think you can see here the difference of alpha scaling with number of samples not number。

 of samples from this plot because it's not scaled with number of samples in LaSue and so it's really。

 not in slot。 Where is this？ Where rich converges。 Anyhow， you see it？ Very long conversation。

 Don't worry about it。 All right more questions about linear models regularization multi-class anything。

 So okay so let's talk about trees。 Trees work completely differently and I'm more or less the。

 opposite of linear models。 So trees are very highly nonlinear and they can be arbitrarily complex。

 And so why isn't there an image of this？ So basically decision trees learn to ask a series of。

 if else questions。 So you learn to make a decision by asking a question here there's like you found。

 an animal in nature and the first question you ask maybe is this animal bigger or smaller than a。

 meter or three feet for the Americans。 If it's bigger you ask if the animal has horns or not。

 And then you ask aren't longer than 10 centimeters and so you narrow down which kind of animal could。

 that be。 And so the next question you ask depends on the answers that you had before。

 So this is a binary tree of questions and sort of once you end up in the leaves of this tree you get。

 some answer。 And decision tree is basically try to automatically learn this series of questions。

 and what the right answers or so and what the outcome should be given the answers。

 So let's start with that decision tree regression。

 So we have this sort of same data set with the with the sine wave and the slope that we had before。

 for regression。 And so the questions that decision trees ask are not really about animals having horns。

 they are about thresholds on features。 So they always ask is feature xi greater equal threshold。

 ti or tj。 Here in this example is a 1d example。 So all questions will be about the one feature。

 And so all the questions will be is this greater than is the feature greater than zero to which。

 it greater than 1。1 something and so on。 And so the main parameter or one of the main parameters of。



![](img/92aed0107e5ed9540c8a768811cdbac0_100.png)

![](img/92aed0107e5ed9540c8a768811cdbac0_101.png)

 decision trees is the maximum depth。 So you by default decision trees are grown until。



![](img/92aed0107e5ed9540c8a768811cdbac0_103.png)

 each leaf only has a single answer in it。 So here the answer is the target value。 So if I。



![](img/92aed0107e5ed9540c8a768811cdbac0_105.png)

 don't restrict the depth of the decision tree I basically will have one value in each。



![](img/92aed0107e5ed9540c8a768811cdbac0_107.png)

 in each leaf and I'll totally overfit the data。 If I say max depth equal to five I'll do binary。



![](img/92aed0107e5ed9540c8a768811cdbac0_109.png)

 tree until depth five and then I stop splitting。 So basically the way the splits are found is。



![](img/92aed0107e5ed9540c8a768811cdbac0_111.png)

![](img/92aed0107e5ed9540c8a768811cdbac0_112.png)

![](img/92aed0107e5ed9540c8a768811cdbac0_113.png)

 by a kind of brute force search。 So you ask what is the first best question it tells me as much。



![](img/92aed0107e5ed9540c8a768811cdbac0_115.png)

 as possible about the data。 And so actually let's look at classification I think it might be a。



![](img/92aed0107e5ed9540c8a768811cdbac0_117.png)

![](img/92aed0107e5ed9540c8a768811cdbac0_118.png)

 little bit easier to see there。 So that's my favorite plot because I spent hours on creating it。



![](img/92aed0107e5ed9540c8a768811cdbac0_120.png)

 And now it doesn't work because I zoomed in。 Come on。 All right。



![](img/92aed0107e5ed9540c8a768811cdbac0_122.png)

![](img/92aed0107e5ed9540c8a768811cdbac0_123.png)

 So let's try this。

![](img/92aed0107e5ed9540c8a768811cdbac0_125.png)

![](img/92aed0107e5ed9540c8a768811cdbac0_126.png)

 So you have a data set here on the left which is like we want to try to learn classify red with。

 blue points。 And so here we have two features。 X axis and Y axis。 And so what yellow is in this。

 it tries to ask what is the most informative question or I can ask either asking a question about the。

 X axis or the Y axis and it tries all possible questions so basically all possible different。

 thresholds or like access parallel decision boundaries。 And what I found here is the first best。

 question is to ask whether X zero so here the X axis is greater or equal than 0。996。

 That's this line。 So this line is actually pretty good at separating red from blue。 It's the best。

 possible axis parallel line to separate red from blue。 And so if you would stop here then it would。

 say everything on the right is red。 Everything on the left is classified as blue。 And this is sort。

 of a drawing of the decision tree。 You can now keep going and recursively partition each side。

 So now again you ask what is the best possible question to learn more about the target。 And here。

 on the left hand side you can split here asking if X1 is smaller equal -1。2。06 and oh sorry it's。

 actually the other way around。 This is if X1 is smaller than 1。528 and if so you're in the top。

 here and you classify it as red otherwise you're in the bottom here and classify as blue。 And。

 similarly they're the same on the other side。 And so you can keep recursively adding more and more。



![](img/92aed0107e5ed9540c8a768811cdbac0_128.png)

 branches and keeps putting up the space more and more。 So you can think of this as a recursive。

 partitioning where for each region that you have unless it is already contains only one class you。

 ask what is the best way to split it up more so I can learn more about the classes。

 And so in the end you end up with this。 So you can see here you can sort of see the decision tree。

 and this is the result。 This is somewhat overfit the data because we didn't restrict the depth。

 It'll grow until everything is perfectly classified。

 So classify stuff here as red and here and here， and here and here。

 And so you can see that there's a line of blue here and here that maybe you might。

 not expect or you might not expect the red here。 So there's several ways to restrict these trees。



![](img/92aed0107e5ed9540c8a768811cdbac0_130.png)

 and keep them from overfitting。 So one is the maximum depth which you can like experiment here。

 with the slider。 Other possibilities are the maximum number of leaf nodes or。

 the maximum impurity which basically says how many wrong points need there be in a region。

 before I stop splitting。 Questions about trees？ So maybe one thing about them is。

 the way you describe that it sounds like if you limit the depth it won't really change the。

 top part of the tree at all。 No。 Yeah because it's a very greedy procedure you find the first best。

 question then for each region separately a second。 Are there any packages that go back and through？

 I'm pretty sure there's packages that go back and prune but not in a second learn。 Are you aware of？

 No。 So it's a regular question we have and the answer is often in practice for prediction which is。

 basically the only thing that we bother it doesn't really matter to pruning is mostly useful for simplifying。



![](img/92aed0107e5ed9540c8a768811cdbac0_132.png)

 the story about the model。 But it's just a matter of prediction you wouldn't care。

 Well mostly because we okay so for the recording question is can we go back and prune and the answer is。

 if you care about prediction which scikit learn mostly cares about you're not going to use trees。

 you've got to use random force which we're going to explain next and then you don't need to prune。

 If you want a very easy and interpretable model it's probably a good idea to go back and prune。

 and we both don't know of a package but we have pull requests for scikit learn and I think we。

 should add it but we don't have it right now。 All right so yeah the thing is decision trees tend。

 to overfit quite a lot and which is why people don't usually use them a lot instead what we're。

 going to what people using is random forests and what random forests are is basically just。

 many many trees that are trained on different subsets of the data。



![](img/92aed0107e5ed9540c8a768811cdbac0_134.png)

 So here's another neat animation。 So here this is using many trees of depth one that are trained。



![](img/92aed0107e5ed9540c8a768811cdbac0_136.png)

 on slightly different subsets of the data and then the aggregated results。 So basically each tree。

 can give you probabilities for each region of the input and ask what is the probability of each class。

 We aggregate this probability over all of the trees usually it's a couple of hundred and that。

 gives you much more robust result it's less likely to overfit and so here you can even for maximum depth。

 if we go to one you get reasonable results here and if you if you increase maximum depth it's going。

 to be like a little bit more spotty but the results much more reasonable than what we had。

 with just a single tree。 So the main way that or there's two ways in which the trees are made。

 different so there's randomization if it was like 10 times the same tree obviously it wouldn't。

 change anything。 So there's two ways the trees are randomized in the random forest one is。

 we take bootstrap samples of the data which means we draw with replacement。

 as many samples as we have in the original data set。

 So for each tree I create a new data set that's， as big as the original one but some samples don't appear and some appear multiple times。

 So an expectation about I think 66% of the data will appear in each tree。

 So this bootstrapping means that every data every tree sees different data and so they will be different。

 The second way in which the trees are different is that in each node in a tree we only consider。

 a subset of the features to split。 So that basically just adds some noise or randomness into the process。

 and makes sure the trees are sort of different。 So all the trees still overfit but they all。

 fit in different ways and if we average them everything is fine。 And so random forests are really。

 one of the best off-the-shove methods in particular because trees， I should emphasize。

 is trees don't care about scaling。 If you scale the features it doesn't matter to the tree at all。

 It tries all possible thresholds and all possible features。 So even if you do like a logarithm it。

 won't change anything。 It just cares about the order of the points for each feature independently。

 And so any like transformation that leaves this intact you can do a log you can do a square root。

 you can scale it doesn't matter to the tree at all。 And this way it's like it's very robust to。

 your representation of the data。

![](img/92aed0107e5ed9540c8a768811cdbac0_138.png)

 Yes。 Basically I don't have the exact formula in my head right now but basically if all of them are。

 better than chance and they're not very correlated then averaging them will make it better。

 It's sort， of wisdom of crowds。 If everybody is mostly is right more than by chance and we don't。

 and sort of there's everything's not perfectly correlated and everything will be better in aggregate。

 You can see this as a reduction of variance。 If you average things that are independent if you。

 average two things independently then you reduce the variance by two。

 Okay so and since trees are really at a very low bias if they are very deep then basically。

 they have very little bias in their predictions but they can have a high variance by averaging a lot。

 of high variance but independent models then then you have a good average model。

 I mean and in truth they're not independent obviously because they're all sort of built in。

 different parts of the data but that's yeah that's a general idea。 There's I mean there's a great。

 paper that's like super famous by Briman about random forests。 If you're interested in this you。

 should read it。 Yeah so for random forests there's one or two tuning parameters that you should care about。

 So there's one parameter that you need to set but not to tune which is the number of trees。

 Just more trees is always better and so number of estimators， a number of trees and you usually。

 want to set it in a number of hundreds。 If you you cannot never use too many but at some point。

 there's diminishing returns so everything will just take longer。 So you can try out a couple of。

 values or you can take the biggest value that you're patient enough to compute。 And the maybe the。

 most important parameter is how many features to pick。 The standard value is that each node。

 uses a square root of the number of features so if you have like 16 features each node will use four。

 they're randomly picked。 And so other options here this is a digit dataset so I'm trying square root which is 8 log 2 which。

 is like 4 or something and 10 just as 10。 And so this is one of the most important parameters that。

 kind of controls how different the trees are and the max depth basically controls the。

 overfitting of each tree but it also sort of limits the size of the tree which means they're。

 faster to grow and smaller to store。 If you have a big dataset and you don't limit the tree in any。

 way these can become really really big and so they can be and take a long time to build and they can。

 take a long time to load or they just like gigabytes and gigabytes and so it's hard to store them。

 So here I'm using grid search search of a number of features and a maximum depth on the digit。

 dataset and so here I'm actually not doing that much better than the linear model I think I do。

 about as good as the linear model。 Let's see so I'd use a square root number of maximum features。

 maximum depth of 9 which was the biggest I tried。 Maybe it should have tried a little bit more。

 But then obviously it takes longer。 But yeah generally this is one of the best after shelf methods。

 and you should probably try this on whatever problem you have。

 I think I'm going to skip the gradient boosting but just briefly talk about feature importancees。

 So random force can be a little bit hard to understand， because there's like hundreds of trees and。

 there's no much bottle up in line somewhere。

![](img/92aed0107e5ed9540c8a768811cdbac0_140.png)

 So but there's one way in which we can summarize， the tree somewhat。

 There's feature importancees which say how often was the feature selected。

 and how important was it to select this feature in all of the trees。 And so this aggregates over。

 all of the trees how important the feature is in a tree。 So what we're doing here is we're。

 classifying the digits with class one against one and zero。 Was it？ Oh yeah sorry。

 Yeah we classify digit one versus digit zero and so then we can get the feature importancees。



![](img/92aed0107e5ed9540c8a768811cdbac0_142.png)

![](img/92aed0107e5ed9540c8a768811cdbac0_143.png)

 which say which of the pixels are important to make the decision one versus zero。

 And so these are this has the same shape as the input。 So there's one importance per each feature。



![](img/92aed0107e5ed9540c8a768811cdbac0_145.png)

 and you can see them here。 So basically here if you're in the middle this is very important。

 and then there's sort of a ghostly like one this is very zero that's very important。 So if you have。

 stuff here on the outside that's important if you have stuff very in the center it's important。

 and that kind of makes sense because this is where the one is and where not a zero is and this is。

 where zero but not one has stuff。 This is very similar to looking at the coefficients of。



![](img/92aed0107e5ed9540c8a768811cdbac0_147.png)

 linear model though here these just say it's important it doesn't say in which they're sort of。



![](img/92aed0107e5ed9540c8a768811cdbac0_149.png)

 if there's a Montana's relationship if you have a coefficient in linear model it says a high value。

 here means class x or class y here you only say it's important for making a decision it doesn't say。

 it points in direction of this class and you can't really say that because trees are very nonlinear so。

 there doesn't need to be a Montana's relationship but still it's like it's a way to get out the。

 important features。 All right questions？

![](img/92aed0107e5ed9540c8a768811cdbac0_151.png)

 So all right that's it for me I'll head over to and over to Alex。



![](img/92aed0107e5ed9540c8a768811cdbac0_153.png)

![](img/92aed0107e5ed9540c8a768811cdbac0_154.png)

 Everybody's asleep。 Yeah and I'm gonna speak slowly and quietly so they can stay sleeping。

 Okay no shout。 Actually have a taser in my backpack so if you can test it like this。

 Okay so you're still alive right？ So to make sure you follow we're gonna start from the end so if you're not seeing the same thing。

 as me is because you're not paying attention to what I'm saying。 So what it's about to pop up。

 is notebook 22 so we just made a step in forward in time now at 22 and depending on what how much。

 time I spent on this we'll we we might go back。 So let me just plug this before it's too late。

 Okay so the objective of this notebook is to tell you as much as possible about。

 anomaly detection in something like 20 to 25 minutes。 So I guess it's a very， recurring problem。

 I mentioned this this morning very often people come to you and say okay here's my。

 hard drive here's the database here's whatever excel spreadsheet can you find me something that looks。

 interesting or I should be looking at or something which is weird that basically will spot something that is。

 not okay with one of my sensors or one of my person in the that is supposed to be filling all。

 these entries and these numbers and that starts to maybe make mistakes in when they type anything that。

 looks bad and that needs action。 So as you'll see this idea of anomaly is kind of a fuzzy concept。

 but still two people are at least two people I've tried to define it so let me just read this with you。

 So the first one is this quote from Johnson which says an outlier is an observation so sample。

 in a data set which appears to be inconsistent with the reminder of the set of data。

 Okay so to really， hand away the explanation we'll try to see afterwards in terms of stats in terms of quantified metric how。

 we can translate this to something that a computer can actually optimize or find。

 And the other one is an outliers and observation which deviates so much from the other observations。

 as to a rouse suspicions that it was generated by a different mechanism。

 Okay so any other mechanisms， can be sensors getting bad or too old or your operator just falling asleep。

 So there are different types of anomaly detection depending on the setup and let me try to simplify。

 all this。 So we mentioned this idea of supervised and unsupervised learning。

 The first one which is not really the one that I'm going to cover afterwards is the supervised。

 anomaly detection and it's typically a case where you have labels on both normal data and anomaly。

 data and you want to find a way to say okay this new data points isn't an anomaly and really what。

 it really means when people think about supervised AD is binary classification with one class which。

 is very rare。 Okay and everything you've heard today about binary classification you could apply。

 in this setup。 It's just one setup where one of the class does not appear very often。

 The two more interesting setup are the semi-supervised and completely unsupervised AD。

 So when people speak about semi-supervised anomaly detection it means that they have access to data。

 and they know that in this data there's no anomaly。 Okay it's only clean data。

 So they have access to， an entire distribution of data in which they know there's no issue and in some sense it's better than。

 nothing and that's why people call it semi-supervised。 Nothing would be here's all my data。

 There might be some anomaly in it。 I don't know。 I don't know what fraction just find me the ones。

 that are weird and this setup is really the tough one and this is what people call unsupervised AD。

 So you have data some of them are good some of them are not good just find a way out。

 The only assumption is the fact that anomalies are rare。 That's the only thing that you can。

 that you need to assume in order to be able to do anything。 If the anomaly are half of your samples。

 then there's no way you can figure out something。 Okay maybe you can do clustering and see if。

 you have two clusters but what is the anomaly doesn't make any sense if it's not rare。

 So let's see what this can all mean。 So I'm just going to generate some data with the make blobs。

 and just show you how it looks like。 Okay so I've got two blobs of data and so I've got some。

 high density regions which are the center of the blobs and some samples which are quite， off。

 Okay so I've got a fraction of point which is just due to random sampling， are away from the mass。

 Okay here on purpose I didn't simulate with only one blob。 Okay we could。

 just simulate with only one blob which would just be a Gaussian blob but you can apply an animated。

 anomaly detection in much richer context you don't have to have only one blob of data to find out。



![](img/92aed0107e5ed9540c8a768811cdbac0_156.png)

 So let's try to see how we can convert this idea of anomaly in the context of stats。 If you think。



![](img/92aed0107e5ed9540c8a768811cdbac0_158.png)

 about something which is rare you can see this as a point a sample for which the probability of。



![](img/92aed0107e5ed9540c8a768811cdbac0_160.png)

 of sampling this point is very low。 Okay so it was really unlikely to observe this point given the。



![](img/92aed0107e5ed9540c8a768811cdbac0_162.png)

 distribution of normal data。 So if you think of it this way it means that you can just try to。

 estimate the density of your data set and then once you've estimated the density score every sample。

 by the probability of observing each of these samples and if the sample has a very low probability。

 then it's rare and somehow this probability can be matched as a quantified number of anomaly。 Okay。

 So let's see how we can do anomaly detection with kernel density。



![](img/92aed0107e5ed9540c8a768811cdbac0_164.png)

 So I'm going to use the kernel density estimator that you find in neighbors。kde。

 and which basically is as any cyclone estimator has a fit method and here you see I only fit on x。

 There's no x and y I just fit on my entire data set。 So you see it's pretty fast I mean the data is。

 very low dimensional I only have very few points kind of super fast and what I can do afterwards。

 in order to get access to the log probability so something that should be。

 what I'm interested in in order to do anomaly detection I can use the score samples。 So the score。

 samples is actually a method that gives you a score which is not a single score as the score。

 method that you've seen so far it gives you it gives you a score for each of your sample which。

 means that you have a hundred samples as input you're going to get a hundred values out。

 So this is actually exactly what you see here my x was actually 500 by 2 so let me just illustrate this。

 and if I do score samples I get 500 values which are the output of the score samples。

 and score samples contains a log likelihood of the data。 Okay so the log of a probability of。

 observing this sample under the density estimated during the fit。 Any question？

 Okay do you know any， other method that would be good for estimating a density？ Any idea？

 Okay sorry？ You could use a， histogram okay and you can basically that would be a completely non-parametric way of doing things。

 you bin and then you find every point that falls in a bin which is very low very few bins。

 in this histogram bin then it's somehow a sole measure of density and animal detection。

 One issue with these histograms is that if you're going to go in high dimensions then the number of。

 bins will go exponentially and you might even go into troubles。 There's other models that we did。

 not mention so far which are called Gaussian mixture models which are typically a way to describe your。

 data as a mixture of Gaussians。 Okay there are other types of them and that would typically be。

 super adapted to the data generated with the blocks。 Okay so all these density。

 estimation methods basically can give you this number of。

 rarity how much amount is this likely and action this into an omega-E scores。

 So here I'm just going to use this m quantiles function from a cypis stats which will allow me to。

 make a nice figure in order to illustrate the decision function that says if I'm inside these。



![](img/92aed0107e5ed9540c8a768811cdbac0_166.png)

 circles I'm in a high density region so all the points that fall inside these regions these two。

 blobby red curves if I fall inside these circles this well blobby curves they are not circles nor。

 ellipses they look like ellipses but it's just to date the data that make it so。

 I'm a normal observation so I'm inside and otherwise I'm outside。 Okay there's。



![](img/92aed0107e5ed9540c8a768811cdbac0_168.png)

 here I said that the quantiles at 95 percent it means that I constructed the data so that there was。

 5 percent of points which are outside and the rest is inside。

 What this pretty much tells you is that， there are two kind of parameters that appeared here one which is very explicit which I just。

 mentioned which is the fact that you assume that only 5 percent of the point were outside。

 So someone has to tell you if you need to decide this is anomaly this is not you need to set a。

 threshold about what fraction what's the contamination level of your database okay you can keep the。

 continuous value and then you can probably start by looking at the point which have the。

 lowest probability so the more likely to be an anomaly but if you need to threshold。

 into a threshold based on a fraction a percentage of of of anomaly that you can assume on your data。

 It can also be based on the fact that if you have a million samples and you only。

 it takes one hour to look at one sample and you have only one percent that works eight hours a day。

 probably less than if you're in a very socialist country like France。

 Try to make jokes to wake you up。 You need to basically adapt this budget of what's the number of sample that can people look at。



![](img/92aed0107e5ed9540c8a768811cdbac0_170.png)

![](img/92aed0107e5ed9540c8a768811cdbac0_171.png)

 in order to calibrate what's the contamination level that is realistic okay。 Otherwise you're。

 going to have a lot of alarms and if an expert need to look at all these alarms one by one that can。

 take a lot of time。 So this was the explicit parameters there's another one which is super。

 critical。 Any idea what implicitly I assumed when I looked at densities？ Somehow when。

 I just use a KDE so this is non-parametric but somehow I use still a Gaussian blob around each。

 of the samples so that probably points you in the right direction okay。

 I use a Gaussian blob which is， like a circular isotropic blob around each of the samples。

 So let's say if I scale my data I stretch， the data in some directions what's going to happen is it's going to change the output。

 It depends how you quantify the size。 If the size is completely based on Euclidean distance。

 and you scale the features differently then the Euclidean distance doesn't mean the same thing。

 So the implicit thing that is behind this is that I assume that to look at density I had a。

 ground metric and this ground metric was the Euclidean distance okay。

 This is something that is very， common in many methods you had issued this morning with k-means。

 All these methods I mean， k-means this one these methods rely somehow on a way to compare samples。

 How far are they from， each other？ You cannot compare you cannot evaluate densities if you don't have a notion of measure。

 what's the volume what's the distance between your points okay。

 So just keep this in mind because if， the metric doesn't make much sense for what you're doing think about doing animated detection and。

 you have categorical variables then you have things that are in continuous metrics you might be。

 you might have to think a bit how to do this yes。 Yes that's a very good point and there's an algorithm that is called local outlier factor。

 which is exactly addressing this issue and it's merged probably but for sure there's a PR that's。

 about to be finished or hopefully。 So the question is what if it's not blobby what is not circular？

 So here when I use the KDE this non-parametric way of estimating densities I did not really。

 assume that there were blobbys so you just see as a weight I mean we could probably do an example。

 with the two moons which is a classical non-linear like non-blobby types of simulated data where you。

 would see how it adapts to the curvy shape of your data for example。

 All right so historically there was a very popular method that was proposed in the late 90s。

 which is called one class SVM。 So SVM you haven't heard about them today so far they are very。

 they're really the new kids or the old kids on the blog from the eight 90s that were very much。

 studies in terms of math and also algorithms and implementation how to train these types of models。

 and so they have had the time where they were extremely popular and one class SVM is basically。

 an extension of the binary SVM's to the case where you only have one class meaning that you are in。

 unsupervised setup okay and the idea of one class SVM is to basically try to find a decision that。

 can be non-linear and based on kernels like regular SVM's and to have a decision function which is。

 sparse in the number of samples meaning try to find a few samples that allow me to separate what is。

 inside and what is outside。 One class SVM takes as parameters a new parameters which controls this。

 fraction of contamination okay so when you use a one class SVM you need to set the new and typically。

 if you set the new if you follow if you if you if you do it by the books has the theory tells you。

 if you know that you have a 5% contamination your reflex would be to use 5 like 0。05 for the new。

 parameter in practice we can discuss a lot about why it may not be a good solution when you are in。

 finite dimension and finite sample size so you have only have a limited number of samples and not。

 an infinite number but at least what the theory tells you is that you should use 0。05 if you are。

 trying to find the decision function with 5% anomalies。

 So this one class SVM again you can fit them， and you can predict and it will predict plus one if you are okay and minus one if you are an outlier。

 and anomaly。 So let me just illustrate this here all the red dots are the points which are actually。

 outside of the decision function the decision boundaries and I'll put it by the one class SVM。

 So here it looks very similar to what you got with the kernel density estimation what you can show。

 what you can read also is that kd's will fall apart in high dimension if you try to estimate。

 the density of your data set in high dimensions basically in high dimension the space is completely。

 empty okay even you have a lot of points if you're in a very high dimension the space will look empty。

 So estimating a density when you have an empty space is really hard。 So rather than estimating a。

 density which is kind of the if you have a density then you have a good way of scoring anomalies but。

 probably if you want to do scoring of anomalies you don't need the density you just need a decision。

 function that tells you if you're small or if you're high then you are an anomaly and this is a much。

 weaker thing to estimate than to estimate the true density。 And one class SVM is a way to estimate。

 this decision function and typically will work better in high dimension than the pure kd estimator。

 So it's kind of doing the same flavor of models okay it's also based on local Gaussian kernels。



![](img/92aed0107e5ed9540c8a768811cdbac0_173.png)

 this high zotropy but still but since you have this regularization by the。



![](img/92aed0107e5ed9540c8a768811cdbac0_175.png)

 disposit of the samples it would tend to scale better when you're high dimensions okay。



![](img/92aed0107e5ed9540c8a768811cdbac0_177.png)

 So support vector machines have this notion of vector support vectors and this typically the。



![](img/92aed0107e5ed9540c8a768811cdbac0_179.png)

![](img/92aed0107e5ed9540c8a768811cdbac0_180.png)

 support vectors are related to the point which are anomaly and here for example I'm plotting them。

 in a fancy column map that hopefully colorblind people can see。

 A tiny exercise for you that so you realize the difficulty of doing anomaly detection and why it's。

 not so easy problems is try to rerun this exact same code by changing the gamma parameter。

 The gamma， parameter is basically the bandwidth parameter on the kernel okay it's just one parameter and。

 just try to change it and see how much the story changes。 Yes。



![](img/92aed0107e5ed9540c8a768811cdbac0_182.png)

 So the question is can I just compute a center of mass and remove the samples which are far from。

 the center of mass if you do something like this it's basically assuming that your data is a circular。

 blob isotropy blob and you model the data with just an isotropy Gaussian distribution and then what。

 you're describing is pretty much equivalent to what's a proper model with Gaussian model and distance。

 would do。 These types of models can adapt to things that are really curvy that have multiple modes。

 what you describe would not work if you have two modes。



![](img/92aed0107e5ed9540c8a768811cdbac0_184.png)

![](img/92aed0107e5ed9540c8a768811cdbac0_185.png)

![](img/92aed0107e5ed9540c8a768811cdbac0_186.png)

 So you see the impact of the gamma see how complicated your life can be。

 Just you want a couple more minutes or I can continue。 Continue。 No objection。



![](img/92aed0107e5ed9540c8a768811cdbac0_188.png)

 So here I'm showing you the result with a very small gamma and a very high one a much higher one。



![](img/92aed0107e5ed9540c8a768811cdbac0_190.png)

 and you see how the story gets complicated。 If you use a very low gamma then you have a very。

 wide Gaussian kernel and you end up modeling your data with just one big mode okay whereas if I'm。

 here I put very tiny islands around each of my points I end up with a very complicated decision。

 function okay。 So even if the theory tells you that new should be 0。05 the gamma will change。

 completely the story okay。 So I mean there are ways around this and there are strategies to tune。

 parameters and very recently just around this I'd be happy to talk to you about this just be aware that。

 I mean this is a critical parameter。

![](img/92aed0107e5ed9540c8a768811cdbac0_192.png)

 Okay so this is really all nice and now I'm going to show you something that was added in the latest。



![](img/92aed0107e5ed9540c8a768811cdbac0_194.png)

 release version of Psychogon which is called Isolation Forest。 Isolation Forest is actually an。

 algorithm that is not extremely recent but has not very much has not been used very much because it。

 was lacking a good publicly available and document and implementation but still a very powerful method。

 So the idea of Isolation Forest is to use trees for anomaly detection。 So as you've seen with the。

 previous notebook with ND trees are extremely powerful methods they are basically trying to。

 split the space in tiles and inside of these things then basically divide the space and this is what。

 people call partitioning methods okay you partition the space in by just making split along the axis。

 directions。 The idea of Isolation Forest is to say if a sample is away from the mass I can isolate it。

 very easily in a very few decision by very few splits I can isolate the sample typically if I'm。

 on the x-axis and I've got one point which is far I just need one split to say okay now you're alone。

 you're isolated okay so now you do the following strategy you build trees that are completely random。

 okay so you build a tree you you you take a random features and then you take a random threshold。

 if you do this and your point is just in a rare location of the space it's very likely by doing this。

 random split that you're going to isolate a sample okay so the idea is to build a forest of random trees。

 and see on average how many splits do you need to isolate a sample it's kind of a natural and。

 smart idea I would say and the the nice thing about Isolation Forest is to basically come up with one。

 number that converts this intuitive explanation to a level of anomaly okay so they have a way to。

 pull this level of anomaly from much of perform a bunch of trees and to convert the death of the。

 trees into a number that it seems to be right stable across across trees so let's see how this behaves。

 so this is the same data as before and here I'm just using trees but I'm using actually a lot of trees。

 just to show you that there are actually trees I'm gonna take much less of them。

 and if I take only 30 then I've got a more chaotic boundary this is still too nice let's say I do。

 10 you see that you have a rather noisy behavior so by adding a lot of trees you regularize。

 the decision function okay so let's go back to 300 so let's skip this exercise because I just did。



![](img/92aed0107e5ed9540c8a768811cdbac0_196.png)

![](img/92aed0107e5ed9540c8a768811cdbac0_197.png)

![](img/92aed0107e5ed9540c8a768811cdbac0_198.png)

 it for you in real life in real time which is to look at the influence on the trees on the number。

 of trees so very little number of trees then you have a noisy boundary if you have a lot of trees。

 you'll see it's nice so maybe a question for you is is there any reason why you should not use too。

 many trees in other words does it make any sense to cross validate the number of trees。

 or find any types of reason why you should do 300 trees rather than 500 trees。

 and this is a question that also applies to random forest if you understood what I briefly said about。

 this idea of bias and variance you should be able to answer this question。

 yeah so this if if someone tells you I use 300 trees and instead of 5 000。

 the only good reason for doing this is running time for training and for prediction okay。

 even though you can do the training in parallel you can do the prediction in parallel you still。

 burn a lot of CPU time by adding more trees now what the theory tells you is that the more trees。

 you have the better okay but maybe it's enough to have 300 and you don't need 5 000 or the gain by。

 doing to 5 000 is negligible but in terms of running time that's a lot of time okay so here is the。

 same logic you're doing isolation forest if the more trees you use the better it should be。

 but at some points I mean your patience has limits at least mine but um okay so keep this in mind。

 typically you increase the number of trees keep the running time reasonable for your application。

 and and see at some point when you add more trees the results not going to change much and that's the。

 time to stop so let's try to do a real life uh uh applications of anomaly detection so we're gonna。



![](img/92aed0107e5ed9540c8a768811cdbac0_200.png)

![](img/92aed0107e5ed9540c8a768811cdbac0_201.png)

 use again the digits data sets and the game is can we use what we've just seen to figure out what。

 are the digits that are weird okay so the digits that are not properly drawn or that looks。

 suspicious okay and let's see if these all these fancy algorithms can spot digits that actually。

 look different from what a one would look like or a five would look like okay。

 so again so we load the digits we have this amount of samples 8 by 8 so 64 pixels this is just showing。



![](img/92aed0107e5ed9540c8a768811cdbac0_203.png)

![](img/92aed0107e5ed9540c8a768811cdbac0_204.png)

 you one number a five that looks a nice five and what I'm gonna do here is resample or reshape this。



![](img/92aed0107e5ed9540c8a768811cdbac0_206.png)

![](img/92aed0107e5ed9540c8a768811cdbac0_207.png)

![](img/92aed0107e5ed9540c8a768811cdbac0_208.png)

 I've 64 and here I'm gonna focus on the five okay don't ask me why five because five is a good number。

 42 was not in the data set and you have all your time afterwards to try all the other numbers it's。

 actually the exercise that is just below so here just use fancy indexing to get from the data the。

 images that correspond to all the five okay so that's it's well that's why it's called x_5。

 and now I've got 182 images of five okay let's look at a few of them okay so this is the first five。



![](img/92aed0107e5ed9540c8a768811cdbac0_210.png)

 five the first five five from the data typically you see that the first one looks not too much like。

 a five and the other ones look nicer okay so let's use isolation forest to score each of these images。

 and see which were the ones that are the most normal and the ones that are the most。

 anomalous in the sense of isolation forest so I'm just gonna fit the model here。

 and just use then the decision function so the decision function is basically giving for each of。

 these samples the score of anomaly okay and the idea is that the lowest is this number the more。

 the sample is an anomaly so typically all the points that are in this part of the histograms all。

 the images that are in the part of the histograms are the normal points and then you have a few。



![](img/92aed0107e5ed9540c8a768811cdbac0_212.png)

 weird samples that are here okay so since it's digits I can look at them which is nice because。



![](img/92aed0107e5ed9540c8a768811cdbac0_214.png)

 I can visually assess as an expert in writing files how it's how they look like okay so。



![](img/92aed0107e5ed9540c8a768811cdbac0_216.png)

 and so these are the five that are the most in layers okay so they look all like nice files okay。



![](img/92aed0107e5ed9540c8a768811cdbac0_218.png)

 and now I can do the same thing with my outliers and here are the five that look weird and at least。

 if you are experts in five like I am you agree with me okay they are weird okay so it's magic okay。

 it's machine learning it's it's amazing and we found the bad fives and now your mission if you。

 accept it is to the same thing for all digits can you find me the bad zeros the bad ones etc。

 and does it work or just five was just a good number a couple more minutes good move on。



![](img/92aed0107e5ed9540c8a768811cdbac0_220.png)

![](img/92aed0107e5ed9540c8a768811cdbac0_221.png)

 move on all right so just execute this and see so this this is gonna give me the weird ones。



![](img/92aed0107e5ed9540c8a768811cdbac0_223.png)

 and you can just change the key of the value of K and you'll see the other digits right one word。

 about local outlier factor this is not released this should be released in the next few days provided。

 we find we find the time to do the pre-release and get everything fixed and merged before the final。

 release but it's still if you have the dev version you can you can play with Doth which is also a very。

 powerful method and Lough is anomaly detection using nearest neighbors so E4S， I4S。

 situation 4S was nearest was anomaly detection with trees the other one was anomaly detection。

 with kernel methods and Lough is animated detection with nearest neighbors okay just if you just try。

 to organize this in your head right so now I'm gonna jump back in time and jump to number。

 20 and show you more advanced clustering methods including db scan because I think db scan is cool。



![](img/92aed0107e5ed9540c8a768811cdbac0_225.png)

 so you're with me not book 20 we just have 18 minutes left so stay with me。

 right so we've seen so far K means K means is interesting what you need to provide as K means is what。

 it's K exactly and K stands for the number of blobs the number of clusters turns out if you do。

 clustering you have two ways of parameterizing the clustering other option one like K means you。

 set the number of clusters an option to you set some kind of distance or bandwidth parameters that says。

 if samples are less than this then they should be in the same cluster if they are further away。

 than this there should be in different clusters and by setting this more distance parameter then。

 you don't control exactly the number of clusters you just let the algorithm do what it can say it's。

 okay if the bandwidth is too big then you have very few clusters if the bandwidth is too little。

 then you have a lot of clusters okay it's just two different ways of parameterizing your clustering。

 algorithm so typically db scan is the other family you we're gonna need to specify what does it mean。

 for two samples to be close before doing db scan I want to show you something that is very old but。

 still very much used which is called the article clustering and makes this fancy graphs that people。

 call dendograms so let me try to illustrate what the article clustering does if you want to do。

 clustering you basically have two approaches either everything is connected and then you start splitting。

 stuff okay so you subdivide you have one cluster and then you subdivide that would be a top-down。

 approach or you have another way which is at the beginning every sample is is isolate is in its own。

 cluster and then you start merging stuff in order to reduce the number of clusters okay and this would。

 be typically a bottom-up approach the article clustering is exactly of this family you start from。

 all your data and then you need to find a way to say how am I gonna basically glue things together in。

 order to collapse all my samples and reduce the number of classes the rule that you use to say okay。

 this sample should be this could be squashed into one how do you decide this makes the different。

 types of the article clustering that you can have so let me illustrate this with this graph。

 imagine you start from the beginning you have a hundred samples and all of the samples are。

 one cluster so you have hundred clusters and you need to find a way how are you going to merge the。

 first two samples in order to have not a hundred clusters but 99 okay the most obvious things to do。

 is to say I'm going to find the two the two sample which are the the closest to each other in terms of。

 Euclidean distance and they're going to be one cluster containing two points two samples and then。

 you need to move on but then you need to find a way to say what does it mean for a cluster to be close。

 to another cluster okay because now you have 99 clusters but some are just one point and some are。

 multiple points option one is to use what people call single linkage and you say that the next。

 things that needs to be the next cluster that needs to be merged that needs to be merged are the ones。

 for which the minimum distance between any of the points is as small as possible is the smallest so。

 this is illustrated here I've got two clusters I evaluate the distance between the minimum distance。

 between every pair of points and the clusters that have this minimum distance gets merged okay。

 and you continue like this so this is what people call single linkage you can also do complete linkage。

 which is doing the somehow these opposites you merge clusters when the biggest distance between any pair。

 is the smallest okay it's just a different way of deciding how to merge stuff。

 you have another one which is not illustrated here which is called ward or ward clustering。

 W A R D which is not which is something which is based on variance this is not a min and a max but。

 it's mostly based on a criteria that's closer to k-means which tries to have blobs that have low variance。

 so let's see how this behaves I'm going to take my iris datasets so now that you know very well。



![](img/92aed0107e5ed9540c8a768811cdbac0_227.png)

 probably too well and I'm going to use the article clustering another going to take it from。

 scikit learn I'm going to take it from scipy so scipy has a cluster module and inside there。

 the submolecular hierarchy that contains a linkage function that computes the clustering and then。

 a dendogram function that will allow you to plot it so let's estimate the clustering and use the。

 dendogram to plot it okay so this fancy picture just shows you how the different samples were merged。



![](img/92aed0107e5ed9540c8a768811cdbac0_229.png)

![](img/92aed0107e5ed9540c8a768811cdbac0_230.png)

 okay starting from the beginning so it was typically done by aggregation from the beginning。

 you can use another criteria which would be this it would find a different tree okay。



![](img/92aed0107e5ed9540c8a768811cdbac0_232.png)

 you can use a different metric so here everything was based on the Euclidean distance。

 you could potentially decide that Euclidean is not what you want to do and you might want to。



![](img/92aed0107e5ed9540c8a768811cdbac0_234.png)

 change this metric parameter right so now if you want to stay in the world of scikit learn in order。



![](img/92aed0107e5ed9540c8a768811cdbac0_236.png)

 to for example get ask prediction the integer like for k-means there is this a geometric clustering。

 estimator that you find in the cluster module that implements this so if I do for example complete。

 linkage using Euclidean distance then I can do fit predict like I did with k-means and then I get。

 the prediction which is the class label or the cluster label for each of my samples。

 so here I set the number of clusters to three I could have changed something different but just。

 to illustrate how it looks like well it looks a bit similar to what we had just before just the。

 colors again are different same reason as what happened with k-means and you see here that at。



![](img/92aed0107e5ed9540c8a768811cdbac0_238.png)

 some yellow that are where in the green ones here everything is very well separated okay。



![](img/92aed0107e5ed9540c8a768811cdbac0_240.png)

 no surprise we've got 11 minutes so。

![](img/92aed0107e5ed9540c8a768811cdbac0_242.png)

 db scan so I'm not sure I'm keeping the best for the end。

 but db scan is still a very powerful method so it's not that all I mean there's a lot of。

 things that you've seen with us today that are quite old stuff db scan is surprisingly was proposed。

 and not so long ago and is not very much taught in ML courses it starts to be probably because。

 it's in psychitner but it's actually something that you should give it a try k-means is not the only。

 way to cluster samples take a message so the idea of of db scan is the following you need to provide。

 as input a radius or bandwidth or a distance parameter and you're going to say a point which is surrounded。

 by X number of points that are we're going to be calling the min PSTS the min points which are here。

 so here if I for example say min points is equal to three this point here that you see the blue。

 square is surrounded by three points that are within a certain radius so this is going to be a core point。

 okay basically he has samples enough samples at a minimum distance user provided this one is also。

 a core point this one is also a core point now this one is another type of point which people。

 call it border point a border point meaning that it has samples within the radius but it doesn't have。

 enough okay so typically there are points that are going to be at the border of the clusters make sense。

 and then you have some points which are noise points that are neither core points nor border points。

 and basically what db scan does is it samples a point from your data set and it tries to。

 grow the cluster until it has he sees core points if it has a core point it continues and it bit when。

 it sees a border point it stops that makes one cluster and then he's tried to sample a new point。

 that is never seen so you start to grow one cluster then you stop if you end up with only border points。

 and then you continue and if you sample a point which is just a noise point then you keep it as a noisy。

 point and you move on okay seems super simple intuitive and let's see how well this works。

 so this is the typical two moons that I said that I briefly mentioned for animated detection so I've。

 got two moon structures and what I'm hoping to recover with db scan is one cluster that would be。



![](img/92aed0107e5ed9540c8a768811cdbac0_244.png)

 like this and the other cluster that would be like this and you see that the cluster don't look like。

 blobs anymore okay they can have a very complex shape and so this is now the output of db scan。

 yellow is one cluster green is another cluster and these three points in darker color are actually。

 noisy points noise points they are outliers okay so now you might want to change a few。



![](img/92aed0107e5ed9540c8a768811cdbac0_246.png)

 things for example if you change epsilon and you take an epsilon which is much bigger what's going。



![](img/92aed0107e5ed9540c8a768811cdbac0_248.png)

 to happen only one cluster okay because everything is connected to everything with enough neighbors。



![](img/92aed0107e5ed9540c8a768811cdbac0_250.png)

 if I use an epsilon which is smaller then I've got tiny clusters okay so。



![](img/92aed0107e5ed9540c8a768811cdbac0_252.png)

 pick a good value take a message so let's see now so this exercise and you have seven minutes to do it。

 is try to apply k-means agglometric clusterings to these two circles data sets and see which one works。



![](img/92aed0107e5ed9540c8a768811cdbac0_254.png)

 and explain to me why it doesn't for some of these models so let's execute this and see。



![](img/92aed0107e5ed9540c8a768811cdbac0_256.png)

 how good the different models are and you see the first one is k-means and you see that k-means。



![](img/92aed0107e5ed9540c8a768811cdbac0_258.png)

 fails k-means you've seen this morning k-means try to find some isotropic blobs okay so the way to。

 separate these samples into isotropic blobs is basically to draw a line in the middle and this。

 will not capture the structure the complex structure that you see here same thing for your。

 article clustering you try to merge things according to a certain Euclidean distance typically the。

 linkage can have a strong effect effect on this that might help you a bit here and that clearly。

 db scan is the one that gives you the good value now issues you should screw up the value of epsilon。

 in db scan and you have by because you have bad luck you have one sample which is in between that。

 allows you to connect the two circles it's gonna fail also okay so we are about to conclude we have。



![](img/92aed0107e5ed9540c8a768811cdbac0_260.png)

 two minutes i just want to take two minutes to tell you what we did not have time to do。

 we didn't do 19 19 is on feature selection so imagine that you have your you have too many。

 features you want to know what are the ones that are the most predictive which are the。

 which are the features that have the most discriminative powers this idea of selecting the number of。

 features can also be motivated by production constraints if you're in the business when one。

 feature is multiple terabytes of storage maybe you don't want to work with all the teachers you want。

 to subsample because otherwise storing all the features is too much and you want to select the。

 one that had the most predictive power and so there are ways to do this just look at the notebook。



![](img/92aed0107e5ed9540c8a768811cdbac0_262.png)

 either in a unified way or multivided way the other thing we did not do is nonlinear dimension。

 reduction so maybe i can just show the figure oh they're not rendered here。



![](img/92aed0107e5ed9540c8a768811cdbac0_264.png)

![](img/92aed0107e5ed9540c8a768811cdbac0_265.png)

 so it gives you an idea of what you missed because we were too slow。

 it's let's illustrate this with digits and showing you how you can represent the digits in low。

 dimension using either PCA so you see that the cluster the digits are a bit overlapping there's。

 no clear distinction but still it looks in 2d and yes the zeros are far from the ones and。

 there's still some cluster that emerge but actually if you do it with tissney which is a fancy。

 nonlinear dimensional reduction method that in the next release will be even better than the。

 information that you have now that is slow and will not scale but hopefully this is fixed。

 at least in a PR about to be emerged you see that tissney can isolate the digits completely。

 in an unsupervised way okay so of course we pick the values of the parameters that make the picture。

 nice you still unsupervised problem so it means that there is a parameter somewhere。

 and in practice you need to find a good reason why you pick this value okay。



![](img/92aed0107e5ed9540c8a768811cdbac0_267.png)

 and so just going back here the other thing we did not mention at all is how you use scikit learn。

 to do out of core learning if you have a lot of data that don't fit in memory can you can you still。

 use scikit learn and the answer is yes there's a bunch of methods that allow you to learn a model。

 by using mini batches of data or stream of data where you see data as they come or you read them。

 progressively you read some data you update the model parameters you trash the data you take some。

 new data and you learn what we call online okay this idea of online learning is the right way。

 of scaling you're learning to very large data sets not all methods not all algorithms can do this。

 in scikit learn some can do they have a partial fit method partial fit because they can be fitted。

 with a fraction of the data okay so a partial fraction of the data。

 and basically this example is telling you how you train a model for text processing when you have a。

 lot of text and you're going to read text as in mini batches and learn progressively。

 and I think that's it all the rest we've done it of course we have a very extensive online。

 documentation you probably have seen it during the day there's a lot of things that you you can read。

 you can read the book of Andy which is a lot of stuff about scikit learn and more and there are。

 plenty of books in the pie data world using scikit learn that are worse exploring and I think I'm two。

 minutes late so I will stop here thank you very much， [BLANK_AUDIO]。

