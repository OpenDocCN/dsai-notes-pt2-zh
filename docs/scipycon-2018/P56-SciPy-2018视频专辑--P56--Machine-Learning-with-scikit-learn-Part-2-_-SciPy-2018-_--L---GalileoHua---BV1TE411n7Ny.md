# P56：SciPy 2018视频专辑 (P56. Machine Learning with scikit-learn Part 2 _ SciPy 2018 _  L - GalileoHua - BV1TE411n7Ny

 I hope that you got the opportunity to get this， to install it。

 to run a Jupyter Notebook or JupyterLab。 And we are just in the middle of Notebook number six。

 I think。 Of six， yes。 And we had the break。 For the lunch break， we were doing this exercise。

 in the middle of the Notebook number six。 If you want to catch up。

 you need to execute the search before， and then we will go on from there。 OK。

 so just to recall what was the idea。 The idea is that we had a variable x that was x plus sine 4x。

 if I remember well。 And the idea was to integrate sine of 4x as a new column。

 and to see if we can catch up the nonlinearity， patterns from the signals。

 and if we can make the linear model， a bit smarter。 So for that， I can load the solutions。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_1.png)

 So here， we can see that in the x-train and x-test。

 we augment the feature by concatenating to x-train， NP4 sine of x-train and the same for the test。

 And now we just feed the data with this extra column， and predict using this extra column。

 and make the similar plot than here。 OK。 So now when we do that， we see that the orange points can。

 follow basically the sine， which was not possible before， because we engineer a feature that。

 grasp these sine x nonlinearity。 So even with linear models， if you actually can understand。

 or if you know something about your model， that you can augment features。

 A symbol in your model can actually answer to you。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_3.png)

 I mean， can precisely what you want。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_5.png)

 So that was a sense of why adding a new column。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_7.png)

 So do you have any questions or maybe--， So maybe if you consider that the model is the two-step。

 of adding a new feature that is a nonlinear derivative， of the original x-train。

 plus fitting a linear regression， model， the two steps together， they， form a nonlinear model。

 And this way we can basically add some prior knowledge。

 on the problem into the featured extraction part， and then use a simple linear regression model in the end。

 to make the final prediction。 So this is why linear models are still， very useful in practice。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_9.png)

 It's very easy to do feature engineering， when you know a little bit about how the target variable。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_11.png)

 and the input variable are related。 And then you just use a linear model。

 to blend all the feature together in the end。 So now we just saw a linear model， which。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_13.png)

![](img/a165a3dbdfe2a42de38b6b11de2edad6_14.png)

 was a linear regression。 And now we'll play with the canyrows neighbors。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_16.png)

 but the regressor one。 So it's working a bit similarly to the canyrows neighbors。

 but for the regressions。 So in that case， we can define as well。

 the number of neighbors of the regressor， and we can fit and train our models on the training data。

 And similarly， we can already predict。 So for the moment， we just predict on the train。

 And as we know， because we have a neighbors of one。

 so we'll always have the best accuracy that we want， when we do on the training。

 because we have the same samples。 And when we find that， we see that the yellow--， I mean。

 the prediction are exactly， placed on the data that we had originally， which makes sense。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_18.png)

 Now what we're interested in interesting。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_20.png)

 is actually to do that on the testing data。 And we see that the parametric model。

 is doing natively a bit better than the linear models。

 because using information from neighbors to interpolate。

 And somehow it's grasping a bit of the nonlinearity。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_22.png)

 Then we can also make the score and compare， the score of the coefficient of determinations here。

 which。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_24.png)

 is a 191， and which was much slower here。 So here it was 0。79。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_26.png)

 What we didn't try-- and we could have tried it。 Here is one that we make this。

 We could have checked what it was。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_28.png)

 So if I execute this， yeah， that was not a good idea。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_30.png)

 It's not the same data anymore。 Just the x。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_32.png)

![](img/a165a3dbdfe2a42de38b6b11de2edad6_33.png)

 But because it's my x。 So I want to just--， OK。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_35.png)

 And now if I compute the score--。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_37.png)

 It's xx。 OK， yeah， xx。 And here--。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_39.png)

 [INAUDIBLE]。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_41.png)

![](img/a165a3dbdfe2a42de38b6b11de2edad6_42.png)

 OK。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_44.png)

 And here I was 0。96。 And here I'm still under it。 So just by using-- I mean the linear model。

 could grasp if you have the information。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_46.png)

 [INAUDIBLE]。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_48.png)

 Yeah， so here we can check if we increase the number of neighbors。 So let's say 10 or 5。

 So we'll see first on the training what it changed。 And now we see that with all our points。

 I mean we will not have an accuracy of like a L square of 1。

 Our prediction will not be exactly what， we have inside the data。

 But that we are still following the trend。 And it's a bit more regularized。

 So we don't fit the noise。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_50.png)

 So it looks really like a sign in that case。 And then when we do that on the prediction。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_52.png)

 it doesn't change so much。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_54.png)

 But it should improve a bit。 So we went to from 0。91 to 0。94 as what we saw this morning。

 because we are a bit more robust to noise。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_56.png)

 So here what is interesting is that K- and error snobors， has no-- it's a non-parametric model。

 It makes no assumption on the structure of the data， or little assumptions。

 The only assumption is that the local structure， local distances between the points is meaningful。

 And that's interesting because compared to the linear model， we had to do the feature engineering。

 to capture the periodicity in the signal。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_58.png)

 And here it could automatically find this periodic structure， by itself。 However。

 keep in mind that it's not， able to extrapolate the periodicity outside of the region。

 of the training set。 If we were to predict on the right or on the left。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_60.png)

 it would never find a periodic structure。 Whereas for the linear one。

 it would be perfectly extrapolate， because we have an article that into the model in the feature。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_62.png)

 and in the linear trends。 OK， so now the idea is to use the same models。

 But instead of doing it on this simulated data， it's to load the Boston data set， which。

 is a data set for regressions， which have more features。 And just use those different regressors。

 and see what's the scoring on those。 So with the train test and splitting the data。

 and just reproducing the same thing。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_64.png)

 So the Boston data set is a very old data set， that is being used in statistics。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_66.png)

 It's a housing price data set。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_68.png)

 So the goal is to predict the price of houses， in different regions， neighborhoods of Boston。

 based on the descriptors that you can find in the desk。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_70.png)

 attributes。 So I will load the solutions。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_72.png)

 So if we just check out what we are here。 So the first line now we are used to it。

 So first we import the modules and basically the function。

 which will allow us to load the Boston data sets。 We import the function to splits。

 And as a first try， we just import the linear regressions。 So the three first line here are just。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_74.png)

 to get the data and the targets for the data sets， for the Boston data set。

 and then call the things to split。 XY。 So we'll keep 25% for the testing。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_76.png)

 We create two instances。 One regressor specifically for the linear regressions。

 One regressor specifically for the Canabers Regressor。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_78.png)

 with an A-bose of one。 And then we fit our linear regressions， XY。

 And we can get the score on the training and on the testing。

 And we do exactly the same with the Canabers。 We fit on the training sets。

 And then we score on the training and on the testing。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_80.png)

 So if we do that， we see that with a neighbor of one， we have a score of--， I mean。

 a perfect score with the nearest neighbors， while this is not the case for the linear regressions。

 However， the Canabers' neighbors is， not able to generalize on the data。

 while it is quite a bit better for the linear regression。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_82.png)

 in that case。 We could even try， maybe， for instance。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_84.png)

 to increase a bit the number of neighbors， and see if it's changing something。

 And we see that we decrease on the training， but we don't overfit noise when we do that on the testing。

 So it means that sometimes it will， be useful to make a per-parinator search to search。

 what's the best parameters for the prim that we want to do。 One more comment on this。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_86.png)

 So you see that Canyars' neighbors doesn't really， work on this data set。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_88.png)

 Do you have an idea of what could， be a cause of the really bad behavior of that model。

 on this data？ So look at the description of the data。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_90.png)

 [INAUDIBLE]， Neighbor 3。 It works。 [INAUDIBLE]， OK， it's equivalent to linear， but it's not there。

 0。5。 But there are still a potential significant problem。 That could-- yeah。

 It's because the different features， have different rules about it。 Yeah， exactly。

 So those different features， they， have different physical units。

 They vary on very different scales。 So there is really no guarantee that Euclidean distance。

 on those units make any sense。 So for instance， here you have a proportion。

 of a residential land zone。 So it's a proportion between 0 and 1。

 And here you have a concentration of parts per 10 million。

 There is no guarantee that this is between 0 and 1。 The age is between 0 and 100， for instance。

 So very wide variations。 So some of this feature would be much more impacting， the distances。

 And others will be completely ignored。 And if the ones that are varying and very low variance。

 are actually the most predictive， they will be ignored by the model。

 So what we could do is do some kind of pre-processing。

 to make sure that they are all approximately on the same scale。

 And also we could also remove the variables that， are too noisy。

 And this is actually the topic of the--， What was the next？ Next notebook。

 How to do this kind of pre-processing？ Do you typically do that with the j-nars there？

 To do scaling？ Yes。 You need to have some distance that is meaningful in some way。

 And comparing different physical units is not meaningful。 So you need to make it dimensionless。

 So you can choose different kinds of scaling， like divided by the standard deviation， for instance。

 But sometimes this is problematic if you have outliers， or very weird distributions。

 You could also use a quantile normalization， where all the values are between 0 and 1。

 And 1 means that 0。1 would mean that 10% of the value， will be below that。

 So it's some kind of cumulative density distribution， normalization。

 And maybe another thing is that， usually， yeah， we， have very--， I mean。

 kind of small number of samples。 And the kind of neighbors is not an algorithm that。

 will scale with the number of samples。 So usually whenever you start to have much more data。

 you will not be able to use it。 Yeah， but if you have more data， it's， going to be more accurate。

 But then in practice， very few people， use the k-nars neighbors in practice。

 because it needs to record the full training set。 So you need to have a copy of the full training set。

 to make a prediction。 So for instance， if you want to ship that as a small model。

 that you embed in a mobile phone， it's too big。 It might be also too slow to compute the distance。

 to all the data-pointing training sets。 And also， it can also be a problem from a privacy point。

 of view， because if you ship the model， and there is the full training set。

 with all the data of all your users inside the model， that you can decode quite easily。

 then it's another issue。 So in practice， it's not used--。

 the k-nars neighbors is not very used much， as a traditional production system。

 But it's a very good baseline。 If you want to compare more advanced algorithms。

 like random forest or something like that， it's good to， as a sanity check。

 to compare to a k-nars neighbors。 Any other questions before that we go？ No？ OK。

 So next one is about unsupervised learning， which will be about some transformation。

 So we spoke about scaling， so we'll go towards that。 And the second thing will be about dimension--。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_92.png)

 dimensionality， reduction through PCN and such kind of methods。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_94.png)

 OK。 So the first part will be about transformations。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_96.png)

 So we can import the top one。 So how we explain here is that because different features can。

 be scaled differently， then it can impact algorithms。 So in the k-nars neighbors， it can impact。

 the way that you compute the distances， some of our algorithms， that will be based on， for instance。

 gradient descent， or you will not be able to make， the optimization properly。

 So usually you have always a pre-processing step， which， try to scale the features。

 And then you have to put a bit of an analogy there。

 to know what the best scaling apply to your features。

 So one of the standard way-- and that might work maybe 90%。

 of the time-- is actually to standardize by re-centering。

 the data and having a unique scale per features。 So how does that work？

 So if we take a quick example where we have an empire array， with 1， 2， 3， 4， 5。

 the idea is to center by removing the mean， and divide by the standard deviations。 In this case。

 we'll have unique standard deviations。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_98.png)

 So if we do that， then we see that the value of 3， which， was the mean in that case。

 will be center to 0s。 And if we take here and we compute the standard deviation， it will be 1。 OK？

 Yeah。 That's STD。 0， 9， 9， 9， 9， 9， 9。 And most one。 So this is probably one of the most used。

 And when you have continuous feature， if you don't have any knowledge about your data。

 it's something which is widely used。 So we can try to do that on the iris data sets。

 because we saw that we have different height and widths。 But then we can also have different--。

 I mean， we can be the widths is larger than the height or， otherwise。

 So we'll probably benefit from standardizing the data first。 So the first thing that we do。

 we do as we do is really， we split the data into training and testing。 And here we keep proportions。

 which I think is 80% by default。 That's what the random state is。

 The random state is to be able to make the splitting， deterministic。

 So we saw that we have a shuffling。 So it mean that if I execute this several times across Python。

 that I restart Python， then I will have different shuffling， because it is random。

 The random state can be set such that the results will be， always the same。

 So the randomness is deterministic。 So it will shuffle， but always in the same sequence。

 [INAUDIBLE]， Yeah， we will go the same results。 So it's to be able to compare across sessions that things。

 are the same。 So yeah， we are using internally the Mercem twister algorithm。

 from implemented in NumPy， which is a random number generator。 And it needs an integer seed。

 And when you give it a seed， it will return you an object， which， is the random state object。

 So here you can either pass a NumPy random state object， an instance of that class。

 or the integer seed， to create that object again。 And yeah， so because as we said previously。

 when we do the train test split， we do a shuffling。

 before taking the train test split in case there， is some structure in the labels。 For instance。

 if we want to break that structure， so we need some permutation of the data。

 But we want to be able to report you several times the same， results when we run the notebook。

 So this is why we fix the random state seed。 In practice。

 it's very important if you fix the seed to， check that if you change the seed， the final conclusion。

 from your analysis doesn't change。 But it might be useful to regenerate exactly the same， figures。

 So imagine that。 [INAUDIBLE]， Yeah， if you want， for instance， to just see the impact of。

 your classification methods， but you don't want the pre-processing， of an impact there。

 you will fix the seed， such that every classifier will see the same data， for。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_100.png)

 instance， so you can fix the random state for this case。

 So here we split the training and the testing。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_102.png)

 And then we can check what is the mean and sustainability， deviation on the training。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_104.png)

 So we get for each feature， so for the first feature， second， and third and fourth。

 we get the mean for each feature， and， then we get the standard deviations。

 And this actually does information that we use later to。

 rescale the training data and the testing data。 So an important thing to keep in mind is that we don't。

 rescale all the data at once。 We are computing the statistic that allows to。

 scale on the training data only。 So the testing data should be kept out。

 And that's something that need to be--， I mean， you need to be careful。 Otherwise。

 you bring knowledge from the training--， I mean， from the testing into the training。

 So then you can have--。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_106.png)

 I mean， you can curb you fitting。 So instead of this by hand， what we are using is actually a。

 module which is pre-processing， which have a lot of， different scalars。

 One of them is a standard scalar， which is actually the。

 one that we implemented at the first step here。 So he's doing this on the zerood。 So to do that。

 we just import the standard scalars， create， an instance， and then we give it the training data to。

 learn basically the statistic of the mean and the standard。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_108.png)

 deviations。 And then we will transform the data。 So at fit time， it's computing the statistics。

 So now if we do scalar dots mean， we'll obtain the same。

 statistic that we previously computing by hand。 And exactly the same for the scale。

 So why in your opinion， why do you have four numbers here？ For the mean or the scale？

 Because there were four features initially in the data。

 the height and width of the petal and height and width of。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_110.png)

 the sample。 And those basically standard scalar is treating all the。

 features independently of one another。 It's a univariate pre-processing that is applied independently。

 on all the features。 So now how to scale basically the data is we'll call， transform。

 which we'll use those statistics which have， been learned， and which transform for the data。

 So we get exactly the same dimensions。 And if we have an print the data before and after。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_112.png)

 So from inside， we'll just show the first five lines。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_114.png)

![](img/a165a3dbdfe2a42de38b6b11de2edad6_115.png)

 And after scaled， scaling。 So we got those one。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_117.png)

 So we see that basically here we have making an operation， need。

 So the operation is just removing the mean and divided by， the standard deviations。

 And now if we check after scaling the mean and the， standard deviations。

 we will obtain what we saw before。 So the data are centered to zero or to， I mean， we have a。

 small numerical errors。 But the standard deviations is equal to one。 OK？

 And then when we want to make these standardizations or， these normalizations on the new test。

 we don't call fits。 We call directly transform on the data。 And then we see that in that case。

 we are not exactly， equal to 0， which is maybe normal。 I mean。

 we didn't standardize considering only those data。 We use the statistic that we computed before to。

 standardize those one。 So we can have a slight differences。

 So here this is to explain that basically we should。

 properly scale the data at training and at testing， because if we don't do that。

 then here in that case we， then scale the data。 So we scale the training data but not the testing。

 And we see that compared to when it was properly placed， they are all over the place。

 So they are not in the same scale。 So basically， if we do a Kenya's neighbors， the neighbors。

 are not anymore at the same location。 So it will give very wrong results。

 So what is applying on the training need to be applying， on the testing。

 but the statistic that need to be， computed need to be computed on the training， not on the。

 testing。 So one figure which give a summarize of whatever is。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_119.png)

 in-cycle learning， they're following。 So right now we saw the standard scalars。

 So imagine that that's our original data。 And to show how they are， basically， we see that 0 is。

 here and they have a big shift where they are center around， 6。5 and 12。5 here。

 And then they don't have the same scale in x and y。

 And the standard scalars just bring all those data at zeros。

 and make that the standard deviation in both axes， in， both features， i-core。

 And then we have a kind of different standardizers that， have different characteristics。

 So for instance， the min/max scalars will scale all the， data between 0 and 1 in each axis。

 And that could be useful， for instance， when we have sparse， data。

 and that we don't want to shift our data， because we， want to keep the sparse entry to 0。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_121.png)

 And that's one case。 The robust scalars is when we have some outliers and that we。

 don't want to take those outliers into considerations。

 So it will take the distar inter-quarting in that case。

 It's actually to compute the statistics for the scaling， operation。 For the standard scalar。

 we use the standard deviation。 And for the robust scalar， we take the distance between the。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_123.png)

 fourth quartile and the third quartile， which means like a。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_125.png)

 20% percentile and a 75% percentile， 25% area。 And basically， this is interesting， because assume。

 that in the original data， you had one single data point， that was much higher on one axis。

 And on the other axis， you did not have this kind of out， layer。

 It means that the standard deviation across the first， axis would have been--。

 the scale would have been completely shrank by the one， single out layer。

 And then we would not apply the same scaling on the two， different axes。

 And a robust scalar is kind of a protection against that。 It will not remove the outliers。

 but it will make the， scaling much more independent of the outliers， of the extreme， values。

 And quartile transformers is a bit different。 It's a bit similar in the sense that it's projecting。

 everything between 0 and 1。 But it will ensure that if you have a value around 0。5， you。

 have half of the data set that is below 0。5 and half of the， data set that is above 0。5。 Basically。

 it's using the cumulative density， distribution， function of the distribution to be able to map。

 those data from the original space to this 0， 1 space。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_127.png)

 And this will shrink the outliers to 0 and 1。 They will disappear completely if you do that。

 So this is a bit weird because it's not a linear scaling， like robust scalar。

 We don't divide by a constant value。 We apply a non-parametric transformation on the data。

 That might induce deformation， but also provide robustness， against outliers。

 And then the two last is the same class， so is a normalizer。

 But we have different ways of normalizing。 We can project all the points on the--。

 so every row will be normalized individually， and they will， be projected on the sphere。

 So that's the L2 normalizations， and the L1， normalization will be on the diameter， basically。

 So it's a bit less use， let's say， I think。 So yeah， for instance， this kind of normalization。

 can be useful for if you have only positive features that， are count values and， for instance。

 in text documents。 And you have a very different number of words， in two different documents。

 but the topic should not， be dependent on the length of the document。

 So you can divide by the total number of words， in the document。

 And this is approximately equivalent to doing this。 So it might be useful for some operations。 Also。

 maybe for computer vision， it， can also be useful to normalize by the average pixel。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_129.png)

 value in a single image。 So this is pair-- those normalizers， they are pair samples。

 pair line normalization， whereas those， they are pair column normalization。 So it's a bit different。

 Does the scaling you choose depend on your data， your model， or combination of the word？

 Combination of-- so for instance， if you use trees， you will not need， probably。

 those normalizations， because the way that the model is working will not--。

 it will not have the frame of scaling。 I mean， you will learn that。

 And then it will depend on the data。 So for instance， I mentioned， like。

 when you have sparse matrices。 So you will not apply a standard scalars。

 Or when you have sparse matrices， you don't want to move all the zeros entry。

 to something different， because you want to still--。

 you don't want to basically densify your matrix。 So--， Because it's standard scalar。

 you will shift by the average。 So all the zeros will be shifted to some negative value。

 for instance。 And then you will break the sparsity pattern。 And all the entries will be non-zero。

 and you will explode the memory usage， of the representation。 Whereas with min/max scalars。

 zero values， will stay at zero values， assuming， that all the values are positive。

 all the non-zero values are positive。 So this will preserve the sparsity pattern。

 and will make it tractable to represent the data in memory。

 And then now we speak about continuous data。 Then you have categorical data， and you will not。

 normally rise the same way as well。 So it's like data dependent as well。 So you have both。

 model and data。 But generally， what you are seeing for linear models， and nearest neighbors。

 and most of them。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_131.png)

 need this type of things。 So if you assume that your data is。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_133.png)

 approximately univariate Gaussian variables， and there are no extreme values， then the most common。

 normalizer is the standard scalar。 And actually， some models make some assumptions。

 that the data is approximately Gaussian with uninvariance。 And if you use any others。

 it will break that assumption。 But in practice， it doesn't make that much of a big difference。

 If you use Robascara and stuff， standard scalar， if you don't have a lot of layers。

 that's approximately the same。 Even quantile transformer or min/max scalars。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_135.png)

 sometimes the accuracy won't be impacted too much。

 You can use trying test split to measure the accuracy。

 to make sure that you're not making any mistake。 It doesn't impact too much of the results。 OK。

 Any other questions？

![](img/a165a3dbdfe2a42de38b6b11de2edad6_137.png)

 OK。 So now we will pass to one very user， organisms， which is used for dimensionality reduction。

 which， is called PCA， so principal component raises。 And the idea is to find a projection。

 So for instance， if we have 10 features， is to find a subspace with much less features。

 where those features are still discriminative。 And to do that。

 we will find the transformation which， basically maximizes variance。 So let's start。 So here。

 just to give an idea of what the transformation is， doing， here we have some original data。

 which are basically an ellipsis， which is rotated。 And if we consider that we would like somehow。

 if there is two classes， we might， want to project the data such that--， I mean。

 basically the PCA will find， the two axes， the two component， which， wears a variances maximally。

 So one axis is the wrong--， this axis and the second component is on that axis。

 And one that we transform the data basically， is just that we just rotate the cloud。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_139.png)

 And then we can look at the data to a single component。

 So by projecting all these points into the second component。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_141.png)

 or into the first component， and is what we are seeing here。

 So it's like when we drop the second component， and here is only with the first component that we。

 project。 So if we imagine the following points where we have two clouds--。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_143.png)

![](img/a165a3dbdfe2a42de38b6b11de2edad6_144.png)

![](img/a165a3dbdfe2a42de38b6b11de2edad6_145.png)

 so first blob and the second blobs。 In this original feature space， we cannot basically。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_147.png)

 find a linear transformation like out of the box。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_149.png)

 which splits very well the data。 While when we apply PCA-- so now we can apply PCA。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_151.png)

 So PCA is inside the decomposition modules。 We can create an instance。

 fit and transform the instance。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_153.png)

 and then check what is the projections。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_155.png)

 And we'll find that what we did is just， like finding the variances， similarly to what we did here。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_157.png)

![](img/a165a3dbdfe2a42de38b6b11de2edad6_158.png)

 And then now we can maybe find one of the two component， in which we can split easily the data。

 So we don't need the two component。 We can keep only one component over the two。

 which will lead us to perfect discriminations。 So for instance， in that case， we。

 can-- if we project all those data onto that axis， we'll have the violate points。

 We'll have distribution around the Gaussian prey， around here inside that part。

 While the yellow point will be projected inside this part here。 So the second principle component。

 will be very useful to discriminate， violate an yellow， point。

 While if we are projecting all the points on the first， component， all-- I mean。

 the marginal distribution， will just overlap。 Because all the variett points also。

 mean they are mixed with each other on the first component。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_160.png)

 So it's one of the drawbacks of PCA。 It just finds a component which maximizes the variances。

 But it doesn't tell you which component is more。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_162.png)

 discriminant than another。 So we can learn。 And basically， when we are learning。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_164.png)

 we can pass the number of component that we want to keep。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_166.png)

 So here we say x-blob have two features。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_168.png)

 And here in PCA， we'll say， OK， one that I will call transform。 I want to keep only n component。

 So in that case， we want one component， and it will keep the first component。

 And one that we transform the same data， and that we check the shape in this case。

 Now we have only one dimension。 So just to clarify it。 So in this case。

 we are using the first component。 And I've seen previously it's a bad idea。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_170.png)

 to keep only the first component。 So it's going to destroy our ability to discriminate。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_172.png)

 So in general， doing PCA might be useful。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_174.png)

 because it might reduce， remove the components that， are not too informative。

 y equals 0 and y equals 1。 OK。 So here you see that the two classes are overlapped。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_176.png)

![](img/a165a3dbdfe2a42de38b6b11de2edad6_177.png)

![](img/a165a3dbdfe2a42de38b6b11de2edad6_178.png)

![](img/a165a3dbdfe2a42de38b6b11de2edad6_179.png)

 And we cannot discriminate in that new space， which。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_181.png)

 is equivalent to this project on the first axis。 So PCA is fundamentally unsupervised。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_183.png)

 It doesn't use any kind of information。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_185.png)

 from the y variable。 And so it's just trying to find the components that。

 explain most of the variance of the original data layout。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_187.png)

 And sometimes if you reduce the dimension， and you're using PCA， it will make it possible to remove。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_189.png)

 low varying dimensions or subspaces。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_191.png)

 And which means that it can get rid of some noise。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_193.png)

 But sometimes the actual signal is in the low varying， subspace。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_195.png)

 And so when you trim that， you might destroy the signal。 So there is no guarantee。

 It's not a supervised transformation。 So there is no guarantee that it's actually good for us。

 as a pre-processing step for a supervised model。 But still it's often very useful。

 at least for visualization。 And this is where you have the linear discrimination， analysis。

 which use a y to make those kind of projections。 You will use a class information， for instance。

 But in get that case， it's not an unsupervised thing。 It's a supervised one。 Yeah。

 How do you use visual lines when you spell。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_197.png)

 more than two features？ So visualization is a big problem， because you have only。

 usually more than two features。 So yeah， we don't have the problem， because the data is。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_199.png)

 already two-dimensional。 So there is no point in using PCA in that case。

 But if the original data was four-dimensional， here you。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_201.png)

 will have n components equal to apply to something that is， higher-dimensional， then you transform。

 and the result， would be two。 And then you can use a scatterplot。

 I don't know if we have an example。 There is an example on the bottom using the digits data， sets。

 We have much more--， I mean， you have like 64 dimension， and we'll project。

 these into two dimensions to plot the numbers， as we say。 Yeah。 [INAUDIBLE]， Yeah。

 So this n component， if we check the help， can be a， there's， a number of commonants that you want。

 or it can be a float。 I think。 Yeah， it can be a float。

 And the float is actually the expand variant。 So you can say。

 I want to keep 90% of the component that--， I mean， the variance。 Yeah。

 of the relative sum of the eigenvectors of the eigenvalues。 Sorry。 Close this。 Yeah。

 And set to two here， and then execute it， and insert a new。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_203.png)

 cell， and do PCA。explain variants。 Good， sorry。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_205.png)

 Our ratio。 Explain variants ratio is more interesting。

 So here you see that the first component is capturing 97% or， 98% of the variance。

 And the second component， very small fraction of the variance。

 So you can also access this information， and you can trim the result based on it。

 And I think that if you don't pre-sag， I mean， if you don't， say anything。

 you have an algorithm that automatically。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_207.png)

 finds a number of components。 There are some heuristic。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_209.png)

 Seriously。 Yeah。 OK， so here are the examples where we want to basically。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_211.png)

 use PCA to actually be able to find how numbers are organized。 But I mean。

 these are more visualization purposes， because， we have 64 dimensions。

 and then plot what we can see in， two-dimensional plots， where we keep on。

 these two first components。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_213.png)

 So in that case， we have our data， which we already used， before。

 So every line is a 64 vectorized images。 And then we put all of these inside the matrix， and then。

 we apply PCA。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_215.png)

 And then we reprogram those data on some axes。 And then we see if the numbers are glued together in this case。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_217.png)

 So for instance， in that case， on the first component， that's the first component here。

 that's the second component， here。 And then we plot the label linked to the numbers。

 And we see some nice plot where things are kind of cluster。

 So all the 0 are cluster inside that first component， the， 4， the 1， couple of 2 here， the 2 here。

 So the first component is able to discriminate between 0 and 1， very efficiently。

 And the second component is able to discriminate between 4， and 2 very efficiently。

 or 5 and 3 very efficiently。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_219.png)

 And so maybe we can plot the actual first component。 Here。

 you see that it's something that can discriminate。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_221.png)

 between 0 and 1。 Because this pattern of white pattern will match 0s very well。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_223.png)

 And this vertical pattern will match 1 very well。 So it's a mix of 0 and 1， and you can see it。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_225.png)

 And here you have the 4。 Yeah， here is harder to see。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_227.png)

 So by looking at the actual structure of the component， themselves， sometimes you see--。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_229.png)

 those are the singular vectors of the central data。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_231.png)

 So yeah， and as the comments say here， so what's the， decision we took to find this new subspace。

 we didn't use， any information about the target itself。

 So everything was unsupervised in these regards。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_233.png)

 So now as an exercise， it's just to load the IRIS data sets。

 And to reduce the dimension from the 4th dimension that we， started being into a 2-dimensional--。

 I mean， and check the two first component of the PCA。

 So you can play during 5 minutes and see what those， components look like。 So yeah。

 project using a scatterplot。 Transform the data and do a scatterplot with the first two， components。

 And see if we can distinguish the three classes， using only those two components。 [INAUDIBLE]。

 [INAUDIBLE]， [SOUND]， [SOUND]， [SOUND]， [SOUND]， [SOUND]， [SOUND]， [SOUND]， OK。

 so we can have a look at the solution。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_235.png)

 So as we saw before， load the IRIS trend test splits。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_237.png)

 We import the PCA and the standard scalars to reuse what， we saw just before here。 We stratify。 OK。

 so first thing that we do is that we learn the standard， scalars。 We fit X-train。

 And then we create a component in which we will keep on it。 We'll train a PCA。 We create a PCA。

 in stands where we keep two components。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_239.png)

 Sorry。 And then we fit and transform。 So X-train。 And where we apply the standard scalars inside the PCA。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_241.png)

 And we do the same for the test。 And then we just make a scatter plot where we just use for the two。

 components。 And we go on the three different classes。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_243.png)

 So if we do that。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_245.png)

![](img/a165a3dbdfe2a42de38b6b11de2edad6_246.png)

 we have this for the training here and here for the testing。 So we。

 I know if it's really better or not， basically。 But basically here， this is the second component。

 the first， component that we found。 And it could be helpful to use the first component to identify。

 here the intersection to identify the first class and the， first class。

 And this is also true on the test sets。 And we still have troubles to distinguish the second and the。

 third class here。 So it's not necessarily better than what we are doing at the， being。 But it's not。

 we don't have like knowledge by hand。 This is automatic。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_248.png)

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_250.png)

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_252.png)

 And it's not a good thing。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_254.png)

 And it's not a good thing。 And it's not a good thing。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_256.png)

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_258.png)

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_260.png)

 And it's not a good thing。 And it's not a good thing。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_262.png)

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。

 And it's not a good thing。 And it's not a good thing。 And it's not a good thing。 [ Laughter ]。

 And the pandas tutorial is taught by a Belgian guy。 [ Laughter ]， We have to go and drop by there。

 Yeah。 Okay。 So we can take five minutes。 Fifteen minutes break。 [ Laughter ]， Just a second。

 [ Laughter ]， Okay。 Okay。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_264.png)

 So let's start。 First set is for multiple given numpy。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_266.png)

 So now the idea is that we can have --， we saw dimension reductions。 We saw some scaling。

 And now we'll see some algorithms that basically try to group together samples。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_268.png)

 and try to simplify in， like say， in the road directions。

 So the first thing to understand this parameter is to use simple --。

 simple blob dataset that will generate and try to understand how close doing is working。

 So let's start by creating a dataset using make blob， like we did before。 And by default。

 make blob will have three blobs， like this one。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_270.png)

 Okay。 So if you execute this one， this will create the x and the y targets。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_272.png)

 which we will not need because we are doing actually rhino clustering。

 So we will not need to transform the data。 And one that we plot the figure and the skaters is what we get。

 So we get three gushion blobs。 Okay。 And the first thing when we try to actually cluster is that we want to have --。

 without looking at the target themselves， just looking at the data。

 we want to find the group of sample that together seems to make sense。 For instance， in this case。

 the question I think that is --， on this case， what do you expect when you want to make tristering by case？

 Yeah。 Basically group each blob together。 So one blob here will be one class。

 This one should be a second class and this one should be a third class。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_274.png)

 So this can be done with one of -- I mean， the most --， maybe no algorithm is Kamins。

 And this is an algorithm in which you can -- you know， in advance how many cluster。 So in that case。

 we know that we have three burabs， so we should have three cluster。 And then we'll tell him， okay。

 find the three best cluster that you can find。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_276.png)

 So to do that， we just call Kamins and we explain how many cluster do we want。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_278.png)

 And then we can fit and predict at the same time。 And it will give us back the labels。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_280.png)

 Okay。 So now it means that you classify every samples in X as a label between zero because we say。

 that this is three cluster between zero and two。 One of the things is what we could think about if we plot it here。

 We see that actually make a perfect classification。 So， for instance。

 those points are cluster together。 This one is the second class and this one is the third class。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_282.png)

 But if we look at a comparison between Y， okay， which is the true label that we。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_284.png)

 generality at the bin and the label here， which were from the predictions and that we， ask him。

 are they all the same， he will say no。 Okay。 So then we have to go a bit more into details Y。

 And we could ask for printing Y and printing the labels。

 And here we see that two and one are not the same。 So it seems like the labels are shifted。

 So we can see this visually。 So here we have colors。 So this one is yellow colors， violet and green。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_286.png)

 And if we do exactly the same using the original data， we see that the yellow is on the bottom left。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_288.png)

 while here it was on the top。 The green here is on the bottom right。

 And this one on the top is actually here。 So because clustering doesn't know anything about the label that you have to assign。

 it makes， sense that actually when our algorithm even if a cluster pretty good what we wanted or give。

 us the results， it doesn't give the label that we expect。

 So it means that we cannot use a metric that we use in classification， for instance， for。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_290.png)

 clustering。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_292.png)

 So if we compute the accuracy， it will tell us that we have a 0% of accuracy because none。

 of the labels are corresponding。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_294.png)

 And this is what the case， we can even check the confusion metrics that will check class by class and。

 then come to the number of samples。 So here it means that all the samples from the first class were actually classified in the class 0s。

 Here all the samples of the third class were classified in the second class and all the， I mean。

 and the last one， like the first class in the third class。

 So the confusion metrics show us that instead to have everything in the diagonal as a perfect。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_296.png)

 permutation of the labels basically。 So the label values 0， 1， 2， they are just permuted。

 but the cluster membership， they match the。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_298.png)

 expected structure。 So two points together， if they are expected to be in the same cluster from the true。

 ground-true data。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_300.png)

 the K-means algorithm has recovered those relationships， the pairwise relationships。

 but they ignore the。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_302.png)

 absolute values of the cluster label names， but the integer identifies for the clusters。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_304.png)

 And this is expected because it didn't have access to those when training， so。 It's not a problem。

 So here we already give a bit of the answer。 Why？ I mean， okay， we have a perfect。

 we have a permutations。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_306.png)

 So now the question is how can we fix it？ Do you have any idea of how basically we can find a metric？



![](img/a165a3dbdfe2a42de38b6b11de2edad6_308.png)

 I mean， what should be a good metric to actually tell us that if we have a good clustering or not？

 You said that you should include labels in the training。

 The point is not to change the learning procedure。

 We still want to have an unsupervised learning procedure。 We want to keep K-means as it is。

 How can we fix the computation of the accuracy basically？

 We don't want to use accuracy because accuracy is a classification metric， so it's a supervised。

 classification metric。 But how can we evaluate the quality of the clustering。

 whether the clustering is good or not， without， looking at the absolute values of the labels。

 We just want to assess that the grouping are correct and not take into account the absolute。

 values of the labels。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_310.png)

 So we can look at the distribution of distances from each other clusters to the cluster center。

 We can look at the distribution of the distances to the cluster center。 That's a good suggestion。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_312.png)

 So if you can't use the metric， it's not a profit。 It's not a profit， right？ If you rotate it。

 it will be diagonally across the entire time。 So yeah。

 we could try to find a rotation and see if we can have a rotation of the computation。

 metrics that would be diagonal。 If it's the case， then we have a perfect clustering。

 But then it's hard if it wasn't zero value everywhere， it would be hard to find。

 Maybe it would be possible using some PCA， for instance， something I don't know， maybe。

 eigenvalue decomposition or something。 [ Inaudible ]。

 The difference between the original labels and the labels and the standard deviation。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_314.png)

 Yeah， but it would only work if they are exactly the same。 If there is some deviation that's --。

 What we could do is instead of focusing on the labels， instead look at pairs of data points。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_316.png)

 and see if we have a pair that is in the same group in the original label information。

 if that pair is still preserved according to our clustering algorithm。

 And the fraction of pairs that are preserved， for instance。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_318.png)

 And there are many kinds of variations of that idea that can be used as clustering metric。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_320.png)

 And I think there is one here in the solution of this exercise， which is called adjusted。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_322.png)

 REN score。 You can look up the Wikipedia definition。

 but basically it's based on that idea that we try。

 to look at pairs and the fraction of the time that a pair of samples that are in the same。

 cluster in the original label according to why are also a pair of samples in the same。

 cluster according to the clustering labels。 So in the case that we use this metric。

 we see that we get a perfect score of one because。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_324.png)

 yeah， we look at the pairs and because our clustering was perfect and it makes a lot of。

 sense because the pairs are just preserved and only the label is changing。 Okay。

 I think adjusted REN score can be negative。 Not sure。 If you have a random clustering。

 it could be slightly negative。 Yes。 But on average， if you have a random clustering。

 it should be close to zero。 And if it's perfect， it should be one。 Exactly one。 Yeah。

 it's close to zero because it's normally right。 And if you have something like 0。5。

 it means that your clustering algorithm has found some， repeatable structure。

 But it's not like very stable。 So here everything was fine because we knew in advance that we had three clusters and we。

 just， okay， find three clusters。 But sometimes it's not that easy to know basically the number of clusters that we have。

 So for instance， if we would have said we have two clusters。

 it means we wouldn't have been smart enough to actually tell us that， oh， I agree。

 you don't have three clusters。 I mean， you don't have two clusters。

 You have three and change automatically。 No， you would have cluster all the data into two different clusters。

 So you would have grouped together those two cloud off points and say， okay。

 that's one cloud and this is your over blobs。 Okay。

 So this is where this is complicated in real life to actually know how many clusters and these type of things。

 So here we can check basically where the cluster located。

 but probably one of the clusters will be here。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_326.png)

 And then I assume that the second cluster will be in the middle of the two cloud off points。

 My centroid will be in the middle。 Okay。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_328.png)

 So one or a stick way， which is a rule of thumb， okay， would be to actually try different。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_330.png)

 the same way that we did with the canoes neighbors。

 would be to try different numbers of clusters and then take the center of inertia。

 So actually the center of inertia， what we call inertia here is the sum of squares between clusters or something like that。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_332.png)

 And this is actually one of the suggestion that was suggested to evaluate the quality of the clustering。

 And this is the metric that came in， is actually trying to minimize when it's converging。 Yeah。

 so it's a dispersion。 So this one for instance have high dispersion， compared to this one。

 But the prime is that if you increase in a lot of very small one， very small cluster。

 then you will find a very small inertia because you over over cluster， let's say。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_334.png)

 But we'll see this later。 So here what we do is that we apply different number of cluster with cements and just check these inertia。

 So these dispersion and then we will check how these dispersion evolve depending of the number of cluster。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_336.png)

![](img/a165a3dbdfe2a42de38b6b11de2edad6_337.png)

 So here we have the number of clusters and these are distortions。 And we see that after three， okay。

 after one that we have three cluster， then the inertia is a kind of plateau。

 So the rule of form would be， okay， three would be the smaller and enough number of cluster just to represent our data peri。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_339.png)

 So basically this number is expected to decrease always and it's actually still decreasing a bit。

 Here the slope is non-zero， but there is a break here and we call this the elbow in the curve。

 And so if you can detect this elbow， it's a rule of thumb to find a number of cluster with cements。

 However， in some data set it might not be as trivial as this。

 It might be like very constant slope and then there is no strong elbow。

 And sometimes you might have two stuff that looks like elbows。

 That could be steps and then it's difficult to know what you should select。

 So it's where it's a bit complicated and some others， more advanced algorithm。

 I agree you don't have to precise that。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_341.png)

 They will try to find the specific number of clusters。 So what's the thing here？ You don't have。

 I mean， it's coming with some assumption， but basically this is difficult to find the right rules to say。

 I need that number of cluster because you don't have any idea of how your data are organized。

 So for instance， we don't have any idea of the distribution of the data。

 And it does not make any assumption on that。 So it means that you can have some incorrect number of blobs and they will just wrongly find them。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_343.png)

 When the shape is not wrong whatsoever， here you will cluster all these parts together because they are close to each other。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_345.png)

 But you will not know anything about that。 Basically， identity is like a kind of ellipsis。

 So basically it means makes the assumption that each blob is approximately spherical in the original representation。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_347.png)

 It doesn't try to find， it makes this assumption that the blobs are approximately the same shape。

 same number of elements， same sizes。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_349.png)

![](img/a165a3dbdfe2a42de38b6b11de2edad6_350.png)

 And if one of those assumption is broken， then you see that the results of K-means are not very good。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_352.png)

 But K-means is one of base algorithms。 So in cyclones。

 there are a couple of algorithms which here we call， so you have K-means。

 mini batch K-means which is not here。 Which is min-shift， the second one。 Min-shift， DB scans。

 F-ini paragation， spectra-crystral string of word。

 And here is an image which makes a summary of how the different algorithms will behave on different types of data。

 Basically， that we saw before。 So for instance， this is a perfectly well separated blob。

 There are approximately the same number of points。 There are approximately spherical。 In that case。

 K-means work perfectly。 This is called mini batch K-means。

 It's like a more scalable variant of K-means。 And you see that if we break those assumptions we've seen previously。

 then it doesn't work really well。 And if you have this kind of nested data structures as the first line。

 it doesn't work at all。 If you compare to spectra-crystral string。

 which is also applying some kind of K-means， but in the eigen decomposition。

 of the affinity matrix of the distance matrix， this is able to find this kind of structure here quite easily。

 However， the problem with this guy is that it's not very scalable。 It's very compute-intensive。

 especially on other data points。 Here we have some other algorithms。

 one and a glometrifch clustering， which are two variants of what we call hierarchical clustering algorithms。

 And sometimes they are able to find this kind of data structure very well。 However。

 it's not perfect either， like for this kind of data it doesn't work。 Finally。

 dbscan here is a very nice in practice。 It's a density-based clustering algorithm。

 You don't give it the expected number of cluster。 It can find automatically a good number of cluster by itself。

 What you give it as a hyperparameter is the approximate size of the interactions between samples。

 some kind of scale hyperparameter。 And it's also interesting because here you see there is a valid point because it can detect outliers automatically。

 and it can decide to put some points as outliers。 So in practice。

 I think dbscan and there is an even more advanced version， which is called HDBscan。

 which is not implemented in scikit-learn but available as a third-party open source project。

 which is compatible with scikit-learn。 I think for many application， practical application。

 this one is very good。 And there is also birch， which is nice because it has the same nice properties as aggromative clustering。

 but it's much more scalable。 It can work in a incremental manner on a very large dataset。

 So it's also useful for that。 And finally， there is a Gaussian mixture models。

 which is a density modeling model。 But it can be interpreted as a clustering algorithm that is very similar to K-means。

 However， it's a soft assignment。 Instead of assigning each data point to each centroid。

 it will assign them with a probability， some likelihood value。

 so that instead of just having colors， you could have levels of confidence。 Furthermore。

 it has more flexibility than K-means， and it makes the assumptions that the blobs are Gaussian。

 but they can have a non-spherical covariance matrix。

 and it can estimate that covariance matrix also on the fly。 So if the data is Gaussian。

 then Gaussian mixture can be very good， and it's also as some kind of confidence level。

 If the data is not Gaussian， like the first two， it will fail similarly like K-means。 Okay。

 so there is no good general clustering algorithm。 In practice， though。

 GB scan is very useful for many practical applications。

 So now the idea would be to use K-means to clusters the digits images。

 So we know that we have 10 classes， so it would be to try to make a K-means clustering on the data。

 And then to visualize the center of the clusters， so we can get back the centrades。

 And from this centrades， just show the pictures。 And then to use the adjusted random score to know what would be the performance of search and supervised clustering。

 So to do the visualization， it's a bit complicated。 It's a lot of matplotlib code。

 but we did it previously with the digit， but if you don't know how to do it， you can skip that step。

 Just try to run K-means on the digit data and completely adjusted run score。

 That's a good first step。 And if you have the motivation or the matplotlib familiarity。

 you can also do the visualization。 [ Pause ]。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_354.png)

 >> So if we load the solutions， so we have this one。 Oops。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_356.png)

 Probably we need to load the data first。 So yeah， we need to load the data。

 So we need to load the data， so we load the digits。 And then from the digits。

 we can already start to create a clustering saying that we have 10 clusters。

 And then we want to predict the clusters from the data。 So we fit and predict from the data。

 And then here we can find out which， I mean， what is the shape of our cluster。

 And now we have a 10 by 64 because we have our 10 images。

 And 64 will be because we have the 8 by 8 pixel in a vectorized way。

 So now what we can do is to actually visualize those。

 So that's what is this part here to visualize the cluster。 So as cluster centers， yeah。

 the centroid， okay， the centroid of the cluster。 So here we go for the 10 centroids。

 We create the subplots and we go over the subplots。

 And we just show the if centroids which we reshape by 8 by 8 image。 So it's what we obtain。

 So for instance， the first centroid looked like a 4。 This one looked like a 1。

 This one looked like a 9。 0， 6， 2， 3， 1， 7。 Maybe 7 inch and 5。

 So somehow it seems that the centroid at least are meaningful when the commits find them。

 Which digit is missing here？ 8， 8， 8。 Can I tell you this one， like here， a mix of 1 and 8。 Yeah。

 because one is here and this is。 Yeah， because sometimes one has this shape and sometimes it's just a straight。

 Right？ Yeah， and the 8 is sometimes as so we bought， I mean， not very well。 So， yeah。

 so what I was saying is that the 8 is missing and you see that here we have a 1 with this part of the 1。

 And sometimes some of the ones， they are just a straight line without this tiny bit。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_358.png)

 And in that case， they tend to overlap with the 8。

 So it didn't find the concept of a pure 8 and a pure 1。

 It found two kinds of ones and one of them is mixed with the concept of 8。

 And it's kind of expected because K-min is not supervised or there is no constraint to enforce that the centroid should match the true levels。

 So then the second part here is to try to visualize into a 2D axis like what we did with PCA before。

 But instead to do it with PCA， we just use EZOMAP which is also kind of decompositions using manifold。

 And plots on those two axes to see if we can see the different groups。 So。

 and then we have like the different numbers on the training and the testing as you own or not。 No。

 it's the true levels and the。 And the true levels。 Okay， the first one。

 This is the color of the cluster labels and those match the digit class information。

 And you see that for most of them it's actually correct like the shades。 This yellow here。

 it's approximately this blue here， this green here is approximately easy。

 So we can actually compute the adjusted run score that is not part of the solution for some reason。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_360.png)

 Just compute it， you compare。 And then digit target。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_362.png)

 So it's quite good because it's。 yeah， 67 on the range between 0 and 1。 Actually， yes。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_364.png)

 It's expected to be close to 0 for random cluster assignments and close to 1 for perfect permutation。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_366.png)

 So。 It's better than random。 It's significantly better than random。 So yeah。

 it means that the structure of the pixel is actually matching quite well the labels that a human would put for this。

 So it's a good encoding。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_368.png)

 I think I'm missing something about this one。 So I definitely I think there's 10 different kinds of digits。

 Yes。 And it's a good question for 10 because you find 10 kinds of things。 Groups， yes。

 And I was able to get to the anomaly to show。 But I'm not sure I get。

 What's so really using the data is not the images。 It's just like image data into vectors。 Yeah。

 So how is it minimal？ But it's not matching。 But wait a minute。 Why it's not a cluster？

 It's matching an array into a cluster？ Yes。 So it's。

 So the original data for here we represent it in 2D。

 But we take the same pixel and we put them aligned in 64 values。

 And then it will compute distance between two vectors to see if they are in the same cluster or not。

 So there are for instance if I want to compute the distance between this one and this one。

 I will compute the distance between this pixel and this pixel。

 They are white so it's going to be 0 minus 0 equals 0。

 Plus the distance between this one and this one。 And I do that every time。

 And then this one is matched to this one。 So they are shaped as vector but the pixel they are always in the same order。

 So we can compute the distances。 But compared to。 So we treat the pixel as vectors。

 We ignore the two-dimensional arrangement between the pixels。

 So it means that if we do a slight shift， then we will destroy everything。

 And if we have a high resolution image that is not 8 by 8， that might not work very well anymore。

 So if we want to have this kind of translation， environments and stuff like that and 2D small perturbations。

 then we would need something that is not just vectors of pixels。

 But maybe we have some kind of pre-processing that extracts patches and slides of patches or something like that。

 Or use a convolutional neural network if you do neural network。 But for all our resolution images。

 this is enough to treat that as vectors of pixels and that should work。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_370.png)

 Okay， and the pictures that are below what are the pictures of？

 So this is a projection in 2D using the ISO map manifold learning system。

 which is some kind of non-linear PCA。 I don't remember exactly the mathematical dissivity definition。

 Yeah， one point here is one digit。 And here those are the cluster levels and here those are the true levels。

 So here all the purples here， there may be the ones or the zeros and all the ones and so on。

 So 2D the one and the eight pretty close together I remember about this picture。

 Do you get distinguished on them as easily？ Yeah， because we project 2D and originally it's 64D there is some overlap that is just caused by the projection。

 So even if the clustering algorithm is able to find good distinction， like for instance。

 this one that is in the middle， it's from this group here。 Actually， in that case it doesn't match。

 But。 Yeah， for instance， this one which is closer like here is actually from the same level here。

 And you see that it's correctly assigned to the core group。

 But it's not close to the bottom of that。 So there's some that will be very distinguishable and some that will be not very distinguishable。

 Yeah， so the fact that we are using a 2D visualization might induce some。

 So you should not focus too much on the special relationship。

 It's just the way it spread to see the grouping。 And we can see that the grouping they kind of match。

 Most of them。 You have a permutation of the colors。

 The colors don't mean the same meaning in the 2 plots。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_372.png)

 But the groupings are approximately the same。 And when we compute the app。

 I just in run score we see that it's a good clustering。 So it's stable。 It's fine。

 any other questions？

![](img/a165a3dbdfe2a42de38b6b11de2edad6_374.png)

 So。 Okay， can we go？ The next notebook is just some kind of summary of the API concept that we've introduced。

 So for all scikit-learn estimators， all the classes in scikit-learn that we can train on some data。

 they all have a fit method that will take either x alone if it's unsupervised or x and y if it's a supervised model。

 And in that case， y is the labels or the target variables。 And x is the feature matrix。

 So x most of the time is expected to be a two-dimensional array for the training data。

 And then we have additional methods。 That depends whether or not we are doing supervised classification or regression。

 or if we are doing unsupervised learning。 So first， for supervised estimators。

 we have a predicate method that will try to predict from a given x the expected value for y。

 So here we pass a new x and we will have a y prediction。

 And the data type of the y array that is returned by predict depends whether we are doing classification or regression。

 If it's classification， it is going to output integer labels。 If it's for regression。

 it's going to predict continuous values， floating point values。 For classifiers。

 sometimes some of the classifiers in the cycle learn have a natural probabilistic interpretation。

 Like for instance， logistic regression can give you some kind of confidence level normalized between 0 and 1。

 For each of the data points that you want on which you are making a prediction。

 If you are doing binary classification， for instance， the output is spam versus not spam。

 It can give you a probability whether it's for instance 0。9， probability that it's spam， and 0。1。

 probability that it's not spam， and the two probability should sum to one。

 You can also do multi-class classification。 For instance。

 you could classify the language of a text document out of 60 possible languages。 For instance。

 in that case， a predict pover will return you an array with first dimension is the number of text documents that you are trying to classify。

 The second dimension is going to be the probability for each of the possible languages。

 If you do the sum along that second dimension， they should sum to one。

 Sometimes the classification model does not give you a confidence value that is normalized between 0 and 1。

 You cannot directly interpret it as a probability。

 but it can still give you some kind of strength in the confidence。

 This is usually done by the decision function method that will give you a value that is either positive if it's likely that it's part of a specific class or negative if it's not likely that it's part of a specific class。

 And close to 0 if it's not shared whether or not it's part of the class。

 A very strong value can rank the predictions basically based on the decision function。

 but they are not normalized between 0 and 1。 It's between minus infinity and plus infinity and 0 is the boundary。

 Whereas here for predict pover， it's between 0 and 1 and 0。5 is the default threshold。

 Then you have the score function that takes for supervised model。

 It takes x and a y and we return a scoring metric by default。

 For classification the default scoring metric is accuracy。

 For regression model is the coefficient of determination r2 square coefficient。

 For some estimator you can also specify what kind of metrics you want to return。

 We'll see examples later。 And also some of the models， even if they are supervised。

 they can also transform the data。 There are very few examples of that。

 but some of them they can also have a natural internal representation of the data that they compute when they make their prediction。

 And it can be useful to introspect it。 However， the transform method is mostly useful for unsupervised estimator like PCA for instance。

 the scalers， the standard scaler and so on。 They are used to find a new representation of the data that can be useful either for visualization or for introspection by humans and see what kind of structure we found in the data。

 Also for pre-processing step for supervised model。 So when you have the transform method usually。

 oops sorry， you also have the fit transform method because you have fit and sometimes it's more efficient to do fit and transform at the same time than doing calling fit followed by transform。

 For clustering algorithm we also have the predict but it's different than the one here because the labels that are returned by the clustering algorithm。

 they don't have an absolute meaning。 It's just the integers that are returned are just used to group the samples to build groups but they don't mean anything intrinsically。

 And some unsupervised models， they also do density estimation so they can give you the likelihood that the data point is followed the structure of the model。

 So this can be useful in this case for instance for Gaussian mixture models that can be seen as a soft clustering algorithm but it's also a density estimation model。

 And this is interesting because then you can use that for instance for our anomaly detection。

 it's a way to do a numerical detection。 And then we have a score function that depends on the models。

 score for density estimation models or GMMs。 It could be the aggregate log likelihood。

 the sum of the log likelihood of the full test set and that can be used for selecting whether or not a hyper parameter is better than another one like we would do for the supervised model。

 But here a score takes a single argument which is just X test and no Y test because it's unsupervised。

 So as a summary for the predict method， it can be used for classification for regression and for clustering。

 So those two are supervised， this one is unsupervised。

 classification returns integers where regression returns floating point values and clustering returns also integers because it's kind of unsupervised classification basically。

 For transform it really depends on the kind of algorithm， it can be used for pre-processing。

 for scaling， it can be used for dimensionality reduction like we did with PCA for instance。

 Or it can be used for feature extraction， PCA is also some kind of feature extraction but there are other examples that we will see later like for text feature extraction for instance。

 And finally there is also automated statistical ways to detect whether a feature is informative or not for a specific supervised classification problem for instance。

 And then we have some transformers that are supervised and for feature selection for instance it can be very useful。

 And we also have examples in the coming notebooks。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_376.png)

 Okay。 Question？ Can you specify your own function for the model score？

 So by default the classifiers that will all have accuracy but what you can do is instead of calling score here。

 you call one of the functions from a cyclone matrix on the predictions for instance。

 We did it earlier with a mean square layer of accuracy so you're not forced to use this score。

 For other models like we will see later for model selection。

 for grid search for instance then you can pass to the grid search object the kind of score that you want to use to select the best model。

 Okay。 So now we have a case study so it's notebook number 10 where we're actually going to use some real data。

 some real features。 And to do that so we will introduce the concept of feature extraction or feature engineering。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_378.png)

![](img/a165a3dbdfe2a42de38b6b11de2edad6_379.png)

 So there are mostly two kinds of features when we do machine learning。

 And if you only have numerical features then you can put them in a two-dimensional array with the first axis going to be the number of samples。

 the second axis going to be the number of features。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_381.png)

 And this is already the case with the iris dataset and here we have four features which are separate lengths。

 separate widths， petal lengths and petal widths。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_383.png)

 And those are whole in centimeters so they are directly numerical features so that we can directly use them to fit the machine learning models。

 It was also the case for all the images like the digits。

 we had the gray level values for the pixels。 Those are also naturally numerical features so we can use them directly for machine learning。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_385.png)

 There are other kinds of features that are categorical。

 For instance if you have a descriptor for an object and you can have three kinds of color for a product for instance。

 red， blue or purple。 In that case we will need to convert that to some kind of numerical representation to be able to fit that to logistic regression for instance because logistic regression is taking linear combinations of the feature values。

 So the feature values need to be numerical values otherwise we cannot do the mathematics。

 the arithmetic operations。 So what we could do is say that red is zero。

 blue is one and purple is two but then it's a problem。

 In your opinion why is it a problem to assign some kind of arbitrary integer values to categorical variables like this？

 Because you are no much greater than this。 Yeah， so when you give integers you have a natural ordering of the integer but that ordering might not reflect something that exists in the original data。

 For instance if you say that zero is red one is blue and purple is two it means that purple and blue are very close to one another and blue and red are close to one another。

 And red and purple are not as close to one another which is wrong。

 There is no like it doesn't really reflect the colors of the product。

 So if we do that we introduce a bias in the data that comes from nowhere。

 It's completely arbitrary and that might lead the model to make bad predictions basically。

 So in general for many machine learning algorithms we will instead of taking integer values for the colors we will take the color features。

 the color column and extract three different columns。

 One which will be color equals purple true or false。

 color equals blue true or false and color equals red true or false。

 If it's true we set it to one so it's numerical value。

 If it's false we set it to zero and we will expect that there is only one of them that will be set to true and all the others set to false。

 And in that case we have some kind of natural metric space that will reflect the distances between the color without introducing a bias basically。

 If it's the same color it has a distance of zero for those features。

 If it's a different color it has a distance of one。

 So if we do this kind of encoding of the color variable then we can concatenate it to the numerical variable and we have done the feature engineering basically。

 So this kind of transformation for the categorical variable is what we call one hot encoding because only one of them is expected to be hot set to one and the other are expected to be called set to zero。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_387.png)

 So one hot encoding is transforming a categorical variable with n possible values into n numerical variables with zero on one as values。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_389.png)

 Okay。 So here we took the example of the iris data set where we treat the target variable as an input feature and a categorical variable so possible to do that。

 But here we have another data set where the records are actually recorded as a dictionary。

 So we have a dictionary with two keys。 The first key is the city name and the second key is the temperature。

 The temperature value is a continuous variable。 So a floating point number。

 But the city variable is a categorical variable that has a finite number of possible values。

 Those are the cities in the world。 So Dubai， London and San Francisco。 Sorry。 Question？ No。 Okay。

 So if we define those measurements， then we can convert that as a numerical feature matrix by using what we call the dict vectorizer and cyclical。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_391.png)

 So dict vectorizer will return a size pass matrix。

 But that we can convert to an empire array just for visualization purpose。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_393.png)

 So if we do that， then you see that the city variable has been encoded。

 one at encoded into three variables。 And the temperature variable has been just stuck as a single column and concatenated。

 And if you look at the get feature names， you see that what is the meaning of the all those numerical values。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_395.png)

![](img/a165a3dbdfe2a42de38b6b11de2edad6_396.png)

![](img/a165a3dbdfe2a42de38b6b11de2edad6_397.png)

 So the dict vectorizer is doing already。 If you're original data， you can load it from a database。

 For instance， return this kind of data structure。 Then it's very easy to use that to do the feature engineering in one step。

 Sometimes it's more complicated to do。 And also sometimes you want to derive features by combining several features together as we did with PCA previously。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_399.png)

 So it's also possible to do that。 And sometimes we have original data that has very noisy columns。

 And we might want to use some of the columns in other fields， fill missing values。

 convert the categorical variables into numerical variables using one at encoded。

 And if you have this kind of program， typically， the original data format that is very common is CSV file format。

 which is very bad。 That is the way it is。 A better file format for this kind of structured column now data is called Parquet。

 which is very efficient。 If you have columns with different types like timestamp。

 text variable for categorical value， numerical values in different columns with different precision levels。

 Then you could use the Parquet file format。 And Pandas is also able to load this kind of file format。

 And then you can use Pandas to do the feature engineering。

 convert that into some kind of numerical and an empire array。

 and then use that resulting feature engineering to feed the cyclic log model。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_401.png)

 So here， if we load this file format， this CSV file that is downloaded in the dataset folder。

 then you can have a look at the column names， because Pandas is automatically reading the first line of the CSV file and interpreting that as the columns。

 the column names。 And you see that we have the passenger class column that is a Boolean value。

 whether or not the passenger has survived the Titanic event。 The name of the passenger， the sex。

 the age， so this is numerical variable。 Whether or not they are where siblings or spouses in the ship as passengers。

 P-arch， I don't remember what it means。 The number of parents and children aboard。

 Ticket is the ticket number。 Why not？ The fare， the price that they paid， the cabin number。

 The city where the port where they embarked， I think there are three ports。 Sherburg。

 Queenstown and Southampton。 Both is whether they were close to a live boat， maybe I'm not sure。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_403.png)

 Body identification number， so it's a unique number。

 And the home and destination are encoded as a single stream。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_405.png)

 So you can see that some of those variables are useful for us predictive features。

 but others are not useful at all。 So here， for instance。

 we might want to build a classification model that will predict whether or not a passenger is going to survive the Titanic or not based on the other attributes。

 So in your opinion， which attribute is not informative at all？



![](img/a165a3dbdfe2a42de38b6b11de2edad6_407.png)

 Ticket number。 Ticket number。 Why？ Who is it？ It's probably just a number。

 I think there is class and the passenger fare which is not applicable to the better the ticket。

 Yeah。 So it's likely that the ticket number is a unique value。

 So if it's unique for each individual passenger， there is no redundancy。

 so we are not able to do any kind of statistical structure extraction for unique values。

 Unless the ticket number is structured in a specific way， but then we might not want to use that。

 but we need to do some kind of feature engineering to extract the components of the feature number。

 Of the number。 And in your opinion， what feature can be very informative？



![](img/a165a3dbdfe2a42de38b6b11de2edad6_409.png)

 The sex。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_411.png)

 Age。 Body。 Body number。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_413.png)

 I think this is also a unique identification number， but it might be only zero。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_415.png)

 Yeah。 It by the minus one if they survived。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_417.png)

 So， but maybe they didn't find the body and in that case it's also missing。 I don't know。

 So sex and age。 Why is it the case that might be informative？ Yeah。

 Because women and children were apparently given the priority to enter the live boats。

 And so didn't die by joining in cold water， but it's not the case for all of them。

 And also another one that maybe that is apparently very important is the class， the passenger class。

 Do you know why？ Because the first class were at the top of the boat and close。

 very close to the live boats were the third class passengers were at the very bottom and they had to take a lot of time to reach the live boats basically。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_419.png)

 And so it was too late and because there were too few live boats。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_421.png)

 And we will see if the model are able to capture this kind of historical stuff that we know about the Titanic。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_423.png)

 So when we load the data in the data frame we can use Titanic head。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_425.png)

 So this is a function of pandas data frame。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_427.png)

 And the pandas data frame structure is very useful in this case because it has a natural way to represent heterogeneously type columns basically。

 Numpy arrays are very good when everything has the same data type。

 It's possible to just an umpire array with different types of different columns but this is really cumbersome。

 So if you have different types of different columns use pandas to do the pre-processing。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_429.png)

 So here you see that some of the columns have string values like the names。

 Other are string values but with two possible values。

 Here there are unique values basically the names are approximately unique。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_431.png)

 And other columns are naturally numerical data。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_433.png)

 So what we can do is extract the survived column as the target variable and those columns as the features that we want to use for prediction。

 So let's have a look at the features。 We will just focus on those。 The port of Embankment， the fare。

 So most of them are numerical but there is sex which is categorical and embarked which is also categorical。

 It can be soft and turn， Queenstown and Cherou。 So for the categorical variable we need to do the one-hot hand coding。

 So in pandas it's possible to just get them used to do that and it will do that automatically。

 So you see now that we have sex male and sex females。

 Those are two columns that come from this single column basically。

 And we have the same for embarked here， the three columns。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_435.png)

 So now that we have this we have only numerical features and we can do machine learning。

 We can call the psychic learn on that data。 So what's the point of this part？ Okay。

 it's just to focus on the get them is stuff。 I don't see the difference。

 It's just that we store the results basically。 So it's the same operation but this time we store the result and we will use that for machine learning。

 So you can append as data frame。 If it's only numerical value you can call the values attribute。

 And then what you get as a result is an empire array。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_437.png)

 And here you see that the data type is floating point values。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_439.png)

 If you still add string values or categorical variables here， the data type would be object。

 And in that case， a psychic learn will reject that because it's not valid input。 However。

 you can also see that there are still entries that are set to none。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_441.png)

 which means not a number。 And sometimes none is the case here for this column。 It's a missing value。

 It can be used to encode the fact that we don't know what was the age of that person。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_443.png)

 It wasn't recorded。 So in pandas none are naturally used to parse CSV file with empty missing values。

 So many machine learning algorithms will not naturally deal with NANs。

 So you need to find a way to fill the NANs with some arbitrary place-holder value that will be neutral in some respect。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_445.png)

 So in psychic learn what you can do is use this impute-er pre-processing to get rid of the NANs。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_447.png)

 And basically it will replace the missing values by the median age or the average age so that it's kind of neutral。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_449.png)

 There might be more advanced ways to deal with NANs。

 but this is some kind of way to deal with it when it's a numerical value。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_451.png)

 So here we do a trend test split and then we fit an impute-er on the training data。

 And then we transform the train and test data to replace the missing values with the statistics that were computed and the training data。

 So it's a bit like the scaling， but this time the statistics are used to do the feature imputation for the missing values。

 So here again we only do it with we find it on the train data and then we transform both the training and the test data with the same impute-er。

 So once we have done this you can see that we don't have any missing values anymore。

 So this has been recorded in train data finite。 So once we have this model a good practice is to try one of the dummy classifiers of scikitlon or the dummy models。

 Those are baseline models that give you some， they are very fast to train。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_453.png)

 And basically the dummy classifier with the strategy which is called most frequent will ignore the input data and just focus on the target variable。

 And output the most frequent class for the target variable which is in this case not survived。

 I think the majority of the people died。 And so if you do that you will have a 63% accuracy already because the two classes are not balanced。

 So using the dummy classifier is actually give you something that is higher than 0。5。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_455.png)

 So here there is an example， an exercise which is actually instead of using the dummy classifier to train a real machine learning algorithm you can try logistic regression or random forest classifier。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_457.png)

![](img/a165a3dbdfe2a42de38b6b11de2edad6_458.png)

![](img/a165a3dbdfe2a42de38b6b11de2edad6_459.png)

 And you can train and compute the score on the test data。

 And what you can do also is to try to remove some features and see if it can improve the test score。

 Okay。 So you can import random forest classifier。 I think we've never imported it so far。

 It's from skl。en。en。 And if you don't know what parameter you can use the default parameters but you can also have a look at the documentation to know what is the meaning of the different parameters。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_461.png)

![](img/a165a3dbdfe2a42de38b6b11de2edad6_462.png)

 And estimator， criterion and so on so you can play a bit with those values to change those values and see if it can improve them all。

 Okay。 So let's do this five minutes。 Question？ Yes？

 So the question is do we need to rescale the data？

 That's actually a good question and you can answer by trying。

 The answer is that for random forest classifier it won't change much because the decision trees algorithm are naturally approximately scale invariants。

 But for logistic regression it's a very good point。

 Like for linear models it generally helps a bit to scale correctly the data so that they are approximately on the same scale。

 And for nearest neighbors classifier it would be even more important。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_464.png)

 So the identifiers we should not take them as features so we should not scale them。

 But for all the other numerical values that once we have done this feature engineering using the get them is we can scale。

 We could use min max for instance min max scalar and for the categorical variable it will not change because it could be a scale between 0 and 1 and so they should stay the same。

 But for the fair here you see that some this is a price in dollar so you see that this is a very different scale 0 and 1。

 So using min max scalar is probably a good idea。 And all the features here are positive values so min max scalars is a good guess and there are no outliers I think。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_466.png)

 The age is approximately always the same the price there is no extreme values so you can use a min max scalar in that case。

 If you want to give it a try。 Yes another question。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_468.png)

 It's not even completing the difference between the two classes counting the number of times it's he survived and the number of time it is not survived and it's predicting the majority class。

 So it's not even looking at the values of X it just look at the values of Y and find the class that is the most likely and always predict this one。

 So it's actually not that the means it's a smart baseline but it's just a baseline it's completely not looking at X。

 So constant classifier basically。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_470.png)

 Okay。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_472.png)

 So let's have a look at the solution so first just to fit the model we can use the default hyper parameter so let's go ahead and put it in。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_474.png)

 So we can use the default hyper parameter so logistic regression without parameter we trained it on the full data and we compute the test set the test score on the test set。

 We do the same with random for a classifier here we typically the default value for an estimator and the second one is too small and we are going to change this default value in some point in the future。

 So we can use it to 100 or 500 typically the higher the better but at some point it's too expensive and at some point you have diminishing returns so just try some significantly 100 for instance and then you set it to 200 and you see if it that improved the result and if it doesn't improve go back to 100。

 And then we can also extract subset of the of the features and do the same do the imputation again and and do that so basically we do the same without the the feature which was called embarked previously and we do the same operations and we and we will compare the results。

 So here you see that logistic regression is slightly better than random forest classification and if we remove the embarked stuff logistic regression is actually slightly below and random forest is slightly better。

 So some features might be helpful on that depending on the model and maybe also here there is some random effect because we did a single trend test split and maybe for example the data we might have small variations。

 So maybe it's not that we should not draw conclusion from that small experiment because the values are still very close。

 Actually this is a bit different so that's weird。 Let's try to see if we change the random state here。

 That's still a significant difference。 Yeah that's weird。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_476.png)

 I wouldn't have expected this。 Okay anyway so here we did the we use pandas to do the get them is which is actually a problem because then it's hard to basically do the imputation and the scaling like we didn't do any kind of scaling but if we wanted to do a scaling operation we would have to mix and match pandas operation with scaling operations。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_478.png)

![](img/a165a3dbdfe2a42de38b6b11de2edad6_479.png)

 And furthermore here we need to do the get them is on the full data set before doing the trend test split which is actually cheating and we should not do that we should do the cover recall feature encoding after the trend test split。

 But with the pandas API it's not possible to do that easily。

 So actually this is something that was improved recently in the master branch of psychic learn is going to be part of the next release。

 Where is it here there is a new class which is called column transformer that makes it possible to to deal with a mixed data types in the input。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_481.png)

 So here is an example from the psychic on documentation on the deaf development branch so if you want to access it you can see go to psychic learn。

org/dev and basically this is the documentation for the master branch of psychic learn so unreleased yet。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_483.png)

 And here we are also using the data set from the Titanic and we are also using pandas to pass the CSV file but then we are not using pandas to do the cut or recall feature encoding。

 Instead we are defining two psychic learn pipelines for the numerical features so age and fair for instance and for the categorical features embarked sex and P class。

 a passenger class we are going to define another pipeline of operation。

 So this pipeline of operation for the numerical values is going to combine the simple computer with the median for the numerical variables then followed by the standard scalar。

 And then for the categorical variables we do a simple imputer with a constant strategy that replace all the none by a missing label so that it's still a string。

 And then once we have these new string values for the missing variables we can use the one at the corner to convert that to the same kind of operation that get them is would have done。

 And if they are unknown elements at the test time we will just ignore them without any kind of warning。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_485.png)

 And once we have those two pipelines we can combine them using the column transformer and then we say the numerical features we will apply the numerical transformer for the categorical features we will apply the categorical transformer。

 and all the other features that are not part of the subset we will just drop them and ignore them basically。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_487.png)

 And when you have this then you can treat that as the feature engineering step the pre-processing step so it's a very complex pre-processing and create a new pipeline that will combine sequentially combine the pre-processor and the classifier logistic regression for instance。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_489.png)

 And then we can do a trend test split or cross validation and it will just do everything on the trend set and then apply the transformation on the test set。

 And then we have the final score which is correct which is very similar to what we got in the tutorial。

 And then we can use great search this is something that we are going to introduce soon。

 Okay so back to the tutorial。 So I think we finished this notebook so we can switch to the next one but before if there are any question on this。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_491.png)

 Nope。 Okay。 Okay so I close this。 So the next notebook number 11 is text feature extraction。

 So here so far we've dealt with numerical feature。

 natural numerical features and categorical variables。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_493.png)

 But there is another kind of data that can be used for classification but cannot be directly used as such we need to do some kind of transformation to be able to extract numerical features from those。

 And this is text documents。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_495.png)

 So the typical pipeline that we use for classification of text documents or at least a good baseline is what we call a bag of words encoding of text documents。

 So assume that you have a text document that is a single sentence。 This is how you get hands。

 The first step would be to split the white spaces and extract all the different words and maybe apply some kind of normalization like ignore the punctuation characters and put everything to lowercase or remove accents in some languages because they might not be consistent。

 Like in French sometimes people do not type the accents。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_497.png)

 So you can normalize this by removing the accents if you want。

 And so this is the job of the tokenizer that will take a string of characters like this that represent the full document and will output a list of smaller strings for the individual tokens。

 A token can be a word but a single word but can be something else and usually a token has been normalized。

 We have removed the casing information for instance。 So once we do this operation。

 this tokenizing operation for all the documents in the collection in the training set。

 And then we record how many unique tokens we found in all the documents across the whole training set。

 And we will call that list of unique tokens the vocabulary。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_499.png)

 And so we can order those tokens by alphabetical order。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_501.png)

 And we will assign a specific dimension to each individual word。 So if it's in alphabetical order。

 let's start with A。 And so Rdvark is going to be dimension zero and Zist is going to be dimension 100。

022 for instance and so on。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_503.png)

 And once we have this， we will， if you have a new sentence。

 so if you have this sentence for instance。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_505.png)

 it has the word get in it。 The get will be mapped to a one in that dimension in that space。

 There is a one for ends。 There is zero for Rdvark because the Rdvark word is not part of that sentence。

 And so you see that this sentence here after tokenization has been mapped to that space because we have this vocabulary。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_507.png)

 So the vocabulary is the link between the token representation to the numerical representation。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_509.png)

 It's some kind of many hot and caudic basically because we have several words per sentence。

 So there can be several ones here and all the missing the words that do not occur in this specific document will be mapped to zero。

 So because the vocabulary is very large， it means that we can have 50。

000 dimensions or one million dimensions。 So something that is very large depend on the size of the data set and on the language and on the tokenizer also。

 Because of that， we will have many zeros in the encoded representation of the document in the numerical representation of the document。

 So it's very important to use a sparse matrix。 Typically it's not possible to use an empire in this case anymore if you have a large document collection。

 So this is why I could learn as several models that support working with sparse matrices。

 Typically for text classification it's a requirement we cannot do otherwise。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_511.png)

 So here we have a small example with only a collection of only two documents。

 Those are two small sentences。 Some say the world will end in fire and the second document。

 second sentence， some say in ice。 So if you take the lens of the list X it's true because there are two documents。

 And each of them has a different number of words or number of characters but we don't care about that right now。

 So we just want to convert that list of text strings into a cypis sparse matrix of a bag of words encoding。

 So what we can do for that is use the convectorizer class from cyclone and it will basically do all these operations that I've presented previously in one step。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_513.png)

 So when you go fit on that list of document it will call a tokenizer， build a vocabulary。

 assign each of the world to a specific dimension arbitrarily。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_515.png)

 And then you can use the vectorizer to transform the list of text documents to a cypis sparse matrix。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_517.png)

 So here we have a sparse matrix with two rows and nine columns。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_519.png)

 Why do we have two rows and nine columns？ The number of sentences is two。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_521.png)

 So this is two rows and nine columns。 There are nine features of non-zero。

 It's actually that there are nine unique words across the documents。

 So for instance here some and say are repeated twice in the document so we ignore the repetition。

 But if you say that some say the world and so on are part of the vocabulary that is common for all the documents。

 And so each of the vocabulary entries will be mapped to a specific dimension。

 So here the vocabulary size is nine actually we can check that。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_523.png)

 Nine。 So this is why we have two and nine here。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_525.png)

 So when we print the cypis sparse matrix we have this representation that is not that informative。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_527.png)

 So it gives us the shape and it gives us the number of non-zero values。

 So it's interesting because we can see that it's already quite sparse even if we don't have that many documents。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_529.png)

 So because we have only two documents and nine dimensions we can convert it into an empire array。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_531.png)

 But for our realistic data set we would not be able to do that。

 And we can get some interpretation by asking for the feature names which is basically the vocabulary to the vectorizer。

 And basically the first dimension is end。 Then we have fire。

 Then we have ice and it's missing from the first document。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_533.png)

 And what is also interesting is that we can do the inverse transformation on the back of world representation back to the original token space。

 And here we see that the transformation was destructive because we did lose some information。

 We lose different kinds of information。 Do you have an idea what did we lose in the operation？

 It's kind of obvious。 The order of the world which is very important。

 And a tiny detail the punctuation is not there anymore because it was stripped away by the tokenizer。

 And the casing information is also not there anymore。

 But the most important part is that we did lose the order information。

 And this is why we call that a bag of words。 Because in a bag when you put stuff in a bag you lose the order because you shake the bag and then you don't know the order of insertion anymore。

 And so the bag of world representation is this。 We record that we have seen this world but we don't know in which context。

 Okay。 So there is a variant of bag of words representation which is called TFIDF vectorizer。

 Which will basically scale and give weights instead of having zero and one or zero or two if we see some words twice。

 We will have these positive values but that have been scaled to values that can be larger than one。

 But typically approximately all on the same scale。

 And actually what we are going to use for this scaling is the frequency of the world across documents。

 What we call the document frequency。 So for instance if you take the word "the" in English like that you're carrying here。

 It's a very frequent world so it's not informative for many classification tasks。

 So we would like to decrease the weight of that world and naturally rescale that dimension so that it's not that important。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_535.png)

 And so this is what the TFIDF vectorizer does naturally。

 It will compute the document frequencies and apply some mathematical rules using logarithms to downscale the world that are very frequent。

 And upscaled the world that are quite rare comparatively。

 So if you want to see the exact definition of the mathematical transformation you can use this notebook。

 You can also read the Wikipedia article on that。 But beware that there are many variants of that TFIDF normalization。

 And the one in the scikitlan is not necessarily the one from Wikipedia so you have to check the documentation of scikitlan。

 And the upper ammeter so that you can change it to something that is more standard。

 But we don't want to change it now because otherwise that might break the code from people。

 It's historical choices。 But in practice the normalization that is done in scikitlan is works well。

 It doesn't change much if you change the normalization parameters。

 Something that is more important actually is how we do the tokenization。

 If we want to preserve some information of the ordering what we can do is instead of considering the individual tokens as they mentioned。

 is take a sequence of two tokens and treat that as a dimension。

 So we will build artificial tokens that are actually the combinations of sequential tokens。

 So for instance if you have this original sentence this is how you get ends。

 The one gram representation would be extracting the individual tokens and treat that as individual dimensions。

 The diagram representation will be to extract this is how you get and get hands as tokens basically。

 And trigrams do the same for sequences of three elements。 Three words。

 So you can do also a combination of unigram and by gram for instance and do the concatenation of the two。

 and use that for your bag of words。 And typically this is what we do。

 We take one gram and two grams of words and this is a very often a good representation。

 So that we keep some local information of the word ordering but it's still fundamentally a bag of words。

 But sometimes you have words that changed with very different meaning when they are concatenated with one another。

 For instance if you take the word New York if you tokenize it as New New and York you lose the information that is New York City for instance。

 Whereas if you keep the bagram then you identify that the city of New York that has been mentioned。

 So to do a N gram extraction you can use the N gram range parameter of convectorizer of TFIDF vectorizer。

 So let's do that with convectorizer。 So you see now that in the vocabulary we have only by grams。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_537.png)

 And so if we do that extraction we have a different meaning for the bag of words。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_539.png)

 What we do often is instead of using just by grams we use a mix of unigrams and by grams and this is what is called N gram range。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_541.png)

 And we extract from one to two gram information。 So now in the vocabulary where the word and in fire。

 in ice and so on。 But only sequences of pairs of words that actually appear in the training set。

 And when you do that you notice that then the dimensionality of the data is increasing very quickly。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_543.png)

 Okay。 So if we take the same training set there is another option in convectorizer which is called analyzer equal character。

 So if we use the character analyzer which is an analyzer it's basically a tokenizer with some additional step。

 If we use the character analyzer instead of the word tokenizer then we have a very different vocabulary。

 We have this as the feature names the individual characters and because we took by grams。

 That's weird。 Ah yes there is a weight space here。 There are weight spaces。

 Maybe we could even do that。 Here we have the individual characters plus the by grams and so on。

 So in your opinion when would that be useful to do this kind of feature extraction to treat individual words。

 What kind of documents or kind of properties of documents we could better represent by using a by grams of a character instead of considering the full words。

 The states。 The states。 Okay so a small。 Yes but what kind of what what what what kind of attribute of those kind of data would we like to predict。

 We could try to predict the next character that's like if we want to do to do a smart keyboard that's actually a good a good potential application of this。

 Another application for language。 See this is what you said。

 Okay yeah if you want to do language predictions this is if you want the frequencies of sequences of two characters or three characters or four characters。

 You can very easily predict the language especially when the language has a different alphabet like in Arabic or Chinese or Japanese。

 Those are different characters than from Latin alphabets。

 But even for European languages for instance where they are all approximately the same alphabet the frequencies of by grams would be very different and it will be very easy to use that to build a classifier to detect the language。

 And you can have a high accuracy with this。 But however if you want to predict the topic of a document here you destroy most of the information。

 It's really or if you want to do sentiment analysis whether the document is positive or negative。

 This kind of representation is probably very bad。 So here there is an exercise which is to take the the Zen of Python by Tim Peters which is this text that explained the spiritual definition of what is good in Python。

 And use the TFIDF transformer。 So you need to treat that as a set of documents and you will basically split on the new line character。

 So you need to turn this big string into a list of strings and then use the TFIDF vectorizer to compute the TF and DF encoding out the data。

 And then use that to find the world that have the highest score。

 And you can also do that for by grams if you want。

 So try to find in the columns the ones that have the highest average score or the total score。

 And see if it's informative with respect to the Zen of Python。

 Okay that's five minutes so let's see the solution so we can move forward。

 So first we need to build the collection of text document by splitting the lines so we can use this。

 And then we will fit a different convectorizer for different values of N to extract the N grams。

 And for each of them we will extract the transformation。

 And then we will sum across the documents to count the number of times we see different words。

 And then we will compute the Archimax which will define the most frequent world。

 And for each of those cases and because this is gonna give you an integer value of the column。

 the number， the dimension of the specific column。 Then we will need to use the inverse vocabulary which is accessible using get feature names to find the most。

 the string representation of the most common world based on that vectorizer。

 I don't know why she's doing this。 And then we can do the same with the TFID vectorizer and we can normalize or not using the L2 norm。

 And we'll see what kind of impact it has。 I forgot to execute this。

 So if you extract diagrams using convectorizer， the most frequent background is better than。

 The most frequent diagram is better than。 And the most frequent foreground is if the implementation is。

 Let's have a look at this。 And you see that is better is very frequent because there is better is better is better。

 But for foregrounds it's very rare to have repeated foregrounds and there is only those two here that are repeated。

 Okay。 Then we do the same for the TFIDF。 And here with L2 normalization it's count and otherwise it's special。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_545.png)

 It's really hard to understand what is the TFIDF normalization is doing and especially when you combine it with the L2 normalization。

 But you see that it's changing the what is the most frequent world across the collection。

 So L2 norm which means that when we do that we will make sure that the result of the transformation。

 All the elements they have the vector of the encoding is basically as norm one。

 Whereas if we said norm equals none it might be left to the result of the TFIDF normalization by itself。

 So this is a second stage normalization that we have applied document by document。

 So in your opinion what why do we want to do a L2 normalization for document representation。

 What would be why would it be useful for which kind of application。

 It would be useful to normalize the co-efficient the extracted features for documents using the L2 normal document by documents。

 It can be done for count vectorizer or 40F vectorizer for both of them you could normalize。

 Basically the answer is that if we normalize we will basically make sure that a long document will be treated equally as a short document。

 Because if we don't normalize a very long document we have a very long norm and so that might impact the classifier。

 So for some applications like predicting the topic of a document whether it's a sport， business。

 I don't know technology。 You don't really care about the lens of the document。

 So normalizing by the lens of the document is actually a good idea because that makes the model invariant with respect to the lens。

 So it's a good inductive bias that you give to the model。

 For other applications for instance if you want to predict the complexity of a document then the lens might be very important。

 So it might be a bad idea to do this kind of normalization。 So it really depends on the application。

 So speaking of application the next notebook is putting this kind of feature extraction in practice by doing a spam detector for SMS messages。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_547.png)

 So here is one of the standard data sets where as an input we have a list of short text documents。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_549.png)

 And as the output we have a binary value Y which is one if it's a spam message and zero if it's a ham or a non-spam message。

 Something that is a regular document。 A regular valid legit message represents。

 So this data set should have been downloaded already if you run this command fetch data。

 And it should be in that folder， data set SMS spam as an SMS spam collection。

 We can open the file and split the tabs。 So this is a special sign for tabulations。

 And basically the document has been already tokenized and they use these tabs separated for the tokens。

 And each of the line in that text file is a specific SMS message。 So we just use that。

 And also the first， oh no actually I'm speaking， yeah。

 There is only a single tab which is separating the label from the text document。 Okay。

 So before the tab we have the label whether it's spam or not spam。

 And after the tab we have the actual text document。 The sentence basically。 So let's have a look。

 So here the first sentence is this one。 The first message is this one。

 And until during point crazy available only in the next year anyway。

 And if you look at the values of Y for the first 10 documents。

 we see that the first two documents are zero which means there are legit messages。

 And the third one is a spam message。 So let's have a look at the third one。

 And you see three entry in a two-weekly competition to win FA Cup final or whatever。

 So typically when you have the word free， win and stuff like that， it looks like a spam。

 So we will see if we can train a classifier to detect those kind of spam messages automatically from the labels that we have。

 So we can first， what's wrong with this？

![](img/a165a3dbdfe2a42de38b6b11de2edad6_551.png)

 And P， I did an import。 Numpy。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_553.png)

 Okay。 First it's a good idea to compute the relative frequency of the two classes。

 So because we are using positive integers， we can use a Numpy bin count to do so which is very efficient。

 And so you can see that most of the document， the vast majority of the documents are non-spam。

 they are regular messages。 But a fraction， a small fraction of them， they are the spam documents。

 So what we can do is actually see the fraction by doing， because Y as a value between zero and one。

 if we take NP mean of Y， we will see the fraction of spam messages and those are certain percent of the。

 messages are spam。 Here you see that Y is a list because we didn't convert it into an Numpy array。

 And even for the text is the list of strings。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_555.png)

 So we need to do some transformation for that。 The train test function from psychic learn。

 it works on lists。 It also works on Numpy arrays but it can also accept lists。

 And it will do the same kind of permutation as previously。 So if I do this， make it more visible。

 Okay。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_557.png)

 So， sorry。 Click the location。 So here we do the train test split as usual but this time on the list of text document and on the labels。

 And we keep 25% for the test set。 And we make sure that we respect the stratification so that the balancing of the two classes is preserved in the train and the test split。

 Okay。 Then we will use the come vectorizer as previously with the default attributes。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_559.png)

 So you can see that by default it's focusing on words。

 There are many attributes and there is also the regular expression that is being used by the tokenizer to identify words。

 If you want to customize that you can。 You can also pass a predefined vocabulary otherwise it will extract it automatically from the training set。

 So let's do that。 So we fit on the training set， again it's not defined， forgot to execute this。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_561.png)

 Okay。 So we fit on the training set and then we transform both the training set and the test set in two side pass matrices。

 So this time the vocabulary is significantly larger than previously but it's still not that big because the data set is not too big。

 And then the training set have been transformed this way。

 So this is the number of documents and this is the number of unique words in the training set。

 And each unique word has been assigned a specific dimension according to the vocabulary。

 So we can have a look at the feature names。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_563.png)

 The feature names are organized by alphabetical order。

 So if we take the first 20 elements we see many numerical codes because the numerical values are at the beginning in the alphabetical order。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_565.png)

 But if we have a look at 20 words in the middle of this you can see stuff that starts with the C。

 And those are regular English words so that looks fine。

 Those might be treated as noise if they are very rare but sometimes they can be repeated and they can be actually useful。

 Some of them might be codes for spams actually so it might be interesting to identify them as markers。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_567.png)

 So the test set has a 4，000 document and the train set has 4。

000 document a bit more and the test set is 25%。 So we have this and you see that the share the same vocabulary because we use the same vocabulary the same count vectorizer to transform the documents from the training test set in the same way。

 And this is very important to reuse the same vectorizer。

 If you use a different vectorizer that you train only on the test set you will have completely random predictions。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_569.png)

 So now that we have this we can actually train machine learning model so a logistic regression。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_571.png)

 It's using also the default parameters the hyper parameters。

 You can read the documentation as usual if you want to learn more about what they mean。

 But in the second one we try to give reasonably good default values。

 There is no guarantee that they are optimal but they should not completely fail either。

 So let's try to fit the model and then complete the score and you see that here we already have 80% accuracy on the test set。

 Is it a good score or a bad score？ It's good。 If we had a completely random model or baseline model what would be the accuracy？

 The baseline because the class are not balanced would be to always predict a not spam。

 And we would because there are certain percent of values that are not spam like a very baseline model that ignores the text and just predict a constant not spam output。

 We would have an accuracy of 87 approximately。 So it's still significantly better than that。

 But you see that the baseline is already as a high accuracy。

 So maybe we should not use the accuracy to quantify the model but make something like the precision or a F1 score or the ROK you see。

 But we will see that later in another notebook。 We can also have a look at the training set and we see that the score on the training set is slightly better。

 It's not perfect but it's slightly better。 And the gap between the two is actually what we call the overfitting and in this case there is not too much overfitting。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_573.png)

 So it's good。 Because we have a linear model we can have a look at the co-eff attribute of the model here。

 Once we have fitted the model this model we give weights to each individual world。

 each individual dimension with multiple to a world。

 And the absolute value of that co-efficient might give you the strength of the world and the sign might be indicative of whether or not it's a spam or not a spam。

 So what we can do is look at the top co-efficient。

 the top positive co-efficient and the top negative co-efficient。

 And for each of those co-efficient look at the feature names which is done here。

 Here we look at the feature names of the interesting co-efficient。

 And we will use a matplotlib to do a graphical summary of the most important co-efficients。

 So this is it。 So maybe it's a bit too small but if you do it on your screen you can read the names here。

 And so you see that for spam values the strongest words are those。 So there is TXT UK。

 So this is a bit weird。 Maybe TXT might be informative but UK maybe it's a bias of the training set because I think it was collected in the UK and maybe the spam in the UK。

 They have URLs with the dot UK at the end。 So that's something like that。

 But maybe in a different dataset that might not be the same。 However。

 Ringtone is likely to be a very much a spam marker。

 And you can see a price cost free mobile service claim one you want。

 This kind of stuff there are really strong markers and call 9。25 whatever to get your price。

 Those are really strong markers of spam。 Here you have negative stuff。

 So this is a bit weird like GT。 I don't know why。 We would have to look at specific sentences of those occurrences to know what those tokens mean。

 But something that you can see that the strongest value here is -1 and the biggest value here is +2。

 So actually the spam marker they have an absolute value that is significantly larger than the negative coefficients。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_575.png)

 We can also use this min-df = 2， which will basically trim the dimensions where we have unique words that are not repeated at least twice。

 So that if a word is too rare we remove it from the vocabulary because it's likely to not be informative。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_577.png)

 And we can do that and see the accuracy on the training test。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_579.png)

 And maybe it's likely better。 I don't remember。 And this is actually not better。

 What else did we change？

![](img/a165a3dbdfe2a42de38b6b11de2edad6_581.png)

 I don't remember。 Vectorizer we use the different values。

 So in this case apparently this is not significantly better。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_583.png)

 We can also use max-df = 0。9 for instance。 So that will remove words that are present more than 80% of the time。

 And this we can maybe remove stronger words that are very rare。 That will reduce the dimension。

 It doesn't change much。 But here the model is working on a smaller set of features。

 So it might be faster to predict。 So that might still be a good thing to do。

 And we could just try something lower like 0。8。 It's still approximately the same。

 That doesn't change much。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_585.png)

 We can also change the regularization parameter of this guy。 And it doesn't change anything。

 So those scores are very stable apparently。 So the feature names。

 the size of the vocabulary are shrinked by quite a bit here because I've used this to basically trim。

 some stuff that were not informative。 Words that are either too rare or too frequent。

 they are likely to be not informative。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_587.png)

 So we can remove them。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_589.png)

 And we can have a look at the feature names。 I don't know why we do that。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_591.png)

 And again the feature coefficient after we did that change in the vectorizer。

 And we still see stuff like ringtone， sexy now is the first one。 Girls。

 different kind of spam that were highlighted by this model。

 But I'm sure that we would find the same words just in a different order。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_593.png)

 So what is interesting here is that if you recap from this morning。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_595.png)

 this approximately is diagram。 And you see that here we are going from the text representation to the vector vector。

 You're using the vectorizer that fit transform。 Fit transform is extracting the vocabulary and then doing the transformation。

 And then we keep this VAC object for later so that we can apply the same transformation and new text document。

 This is very important。 And then to do the actual classification algorithm we will use a logistic regression and we will fit on the feature vectors。

 And then we will get the CLF is modified in place and it's actually the predictive model。

 And then we can call predict to make the prediction。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_597.png)

 So this is how the the scikitlan API maps to this generic data flow。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_599.png)

 So here there is an exercise which is actually to use TFIDF。

 I think it's more interesting to see the next notebook。 So I think we can skip this。

 We can just have a look at the result and in this case TFIDF is not better than convectorizer。

 However， what is very interesting is to use minDF and ngrams and that might improve the equality。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_601.png)

 Let's check。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_603.png)

 So you see if we use TFIDF the equality is actually worse than before。 We still have a ring turn。

 three calls， top claim， whatever。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_605.png)

 Those are the spam words。 They are approximately the same in maybe in a slightly different order。

 And here if we extract ngrams of words and we remove the ngrams that are less than 10 times so that we don't explode the number of dimensions。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_607.png)

![](img/a165a3dbdfe2a42de38b6b11de2edad6_608.png)

 That might improve a bit。 Actually we didn't compute the scores。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_610.png)

 I will take this course here。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_612.png)

 Actually it's still the same or approximately still the same。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_614.png)

![](img/a165a3dbdfe2a42de38b6b11de2edad6_615.png)

 But we use TFIDF vectorizer。 So let's use convectorizer。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_617.png)

![](img/a165a3dbdfe2a42de38b6b11de2edad6_618.png)

 You see that it's slightly better。 So using big grams it's very often the case that it's actually useful and we have a look at the big grams。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_620.png)

 Here there is U-have and probably U-have one if we have extracted chai grams with a short hash on up。

 For the important spam words we see unigrams。 But here you can see that there are one two for the those are like connection words or connection expression that are indicative of non-spam stuff。

 Apparently and statistically。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_622.png)

 Okay。 So let's move to the next one which is actually a very important one which is called cross validation。

 Maybe it's going to be the last one that we have time to do。

 So cross validation and scoring methods。 So this is not book number 13。

 So up until now to do the evaluation of the quality of the model we did a single train test split。

 So we start from all labeled data and we take the largest fraction of that for the training set and a smaller fraction of that like 25% for instance。

 As the test data。 However the quality of the model that the quality of the performance metric that we can measure on the test data because the test data might be small。

 Might depend a lot of the randomness of the splits。

 So if we change the random seed we might have very different values and so using this single split like that might be problematic because of the data。

 And then we might be problematic because we might be misled into thinking that some model is better than another one。

 Whereas the actual order would have changed if we had changed the order of the split or the randomness of the split。

 So instead of doing this what we can do is iterate this procedure many times with different train test splits。

 And when we do this procedure of doing that many times sequentially is what we call cross validation。

 So the most natural traditional way to do cross validation is what we call K-fold cross validation。

 So sometimes we said most of the time we would set K to 5 or 10。

 So if K is set to 5 we call that 5-fold cross validation。

 And basically we will split the full training set into the 5-fold with equal size approximately equal size。

 And each of the fold will be entered， considered as the test set。 And all the four of the fold。

 the green ones will be concatenated to create the train set。

 And so we will have 5 different splits where each of the fold will be used as a test set sequentially。

 And so we will basically train 5 different models independently of one another on those 5 variations of the data set。

 And for each of those model we will compute performance metric。

 And then we can take the average across the 5-fold to see to have something that is more stable and less dependent on a specific train test split basically。

 So we can do this using the iris data set and the K-neo classifier。

 Those are baseline benchmarks basically。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_624.png)

 So if we have a look at why in the iris data set you see that the data has been ordered by the class information。

 So that might be actually misleading because if we do a split。

 a 5-fold split we will have all the 0 in the same fold and that might be a problem。

 So instead we will do， we will use NumPy to do a permutation， a random permutation of the samples。

 And we can do that using X permutation and Y permutation and reassign that。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_626.png)

 Here you see Y has been randomly permitated and we apply the same permutation to X。

 So when we do train test split it does that automatically internally。

 There is also another utility function in scikit-long which is called shuffle that does also the same step。

 But if you are dealing with NumPy arrays it's very easy to use a NumPy permutation to do that automatically。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_628.png)

 So if we want to implement 5-fold cross-validation manually。

 assuming that we have done a random permutation first， then we can do this。 So we define K equals 5。

 we measure the number of samples， we will define the fold size as the number of samples divided using the Euclidean division by 5-fold。

 And then we will define the list of scores that we will aggregate and the list of masks for the test set。

 So what we call the test mask is going to be a mask of 0 except of a range of values between the fold index multiplied by the fold size。

 So we are going to set to true the range of samples that are going to be used for the test set。

 And all the other values that are set to false will be used for the training set。 So let's do this。

 And you see that then we use the test mask to extract the test set and the negative of the test mask to extract the training set。

 And then we fit the classifier on the training set and we compute the score on the test set as usual。

 And we collect all the scores and all the masks。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_630.png)

 So let's do this。 And what we can do is then use a matplotlib mat show to see the mask information。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_632.png)

 So here might be a bit small， but here the lines in that matrix are 0， 1， 2， 3， 4。

 So those are the 5 possible values for K， so the different folds。

 And you see those are the ranges of samples。 We have 150 samples in the full training set。

 For the first fold， for the first split we will take the first fold as the validation set。

 And all the white samples here for the training set。

 On the second line we will use that for the validation set。

 And all the whites are concatenated for the training set and so on。

 And we will train the 5 models independently and compute the scores and aggregate the scores。

 So here are the scores。 So you see on the first split it's 96， 97， then 90%， then 100%， 100%。

 and 93%。 So you see that there is a significant variability across the different splits。

 But then if we take the average， the average should be much more stable than the individual split。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_634.png)

 So in scikit-learn we have this utility function which is called cross-val score for the model selection package。

 And you just give it the classifier and the full training set and it will do that automatically for you。

 So you don't have to write this loop。 It's doing that automatically and internally for you。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_636.png)

 But it's good to know how it works so that it's not magic。

 But then you should get some similar results。 Actually here you see that by default we have only 3 folds because this is the default value of a scikit-learn right now。

 Actually a bad default value we should increase it to 5 as the default。

 But if we set to 5 then we have something similar to the previous iteration。

 In your opinion why it's interesting to use 3 fold cross validation and why it can be sometimes better to use 5 fold cross validation。

 So here's the pro and cons of using a small or large value for the number of folds。

 So if you get the contract pretty and you get numbers that are somewhat。

 Maybe you don't work too much but if you get numbers that are pretty high the very。

 Maybe you use more to make them more stable。 So actually if you try 3 you have a higher likelihood to have numbers that are similar but by chance。

 And actually it's kind of a contract with it but it means that you might not necessarily see the actual viability of the data。

 So the standard deviation when you compute it on 3 element might be artificially low by chance。

 Basically when you have 5 you might see more the confidence interval basically might be better。

 However when you try 5 it's much more expensive because you have to fit 5 models。

 So if the data set is big that might take more time than 3。

 So this is why we decided 3 in the beginning for scikit-learn because it's less compute intensive。

 But in practice it's still better to use 5。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_638.png)

 Another。 So when we do 5-volt course validation we should make sure that there is no overlap at all。

 Here you see the mask。 They are either truer and force。

 So for a specific split either you are in the test set or in the train set。 You cannot be gray。

 You are either black or white and there is no sample that is both of them。

 Here you see that we selected different folds for different cross-videation split。

 We could have folds that splits that would have partially been using the same。

 Or maybe we could use only details。 We will see later more examples。

 The second part of the question was。 I don't remember。 [inaudible]， Yeah。 [inaudible]， Yeah。

 [inaudible]， Yeah。 So if you have a very small data set and you use 5-volt course validation then the test set is going to be very small for instance。

 If you use 10-volt cross-videation it is going to be even smaller。

 And that might be a problem because then you have a lot of viability like computing the score on very few samples。

 So it might be a problem。 But you have read across many more splits。

 So all in all it is not necessarily a big problem。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_640.png)

 What is more of a problem is that the fact that if you use 3-volt cross-videation it means that you are going to use only 3-volt cross-videation。

 That you are going to use only 2-thirds of the data as the training set。

 And when you have a small data set in the first place and you use even smaller 2-thirds instead of 4-5th for instance。

 That is very small and the performance of the model tends to be much worse when you have a smaller training set。

 And so the estimate of the true validation error might be actually too pessimistic if you use CV equals 3。

 And so CV equals 5 tends to be a good tradeoff between being pessimistic。

 being able to capture the variability。 So in general people would tend to use CV equals 5 to 10 but 10 is going to be more expensive because you have to do a repeated experiment many more times。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_642.png)

 What are we evaluating here？ Are we evaluating the classifier itself or are we evaluating how good of the model we have for it？

 So that is a very good question。 Are we evaluating the classifier itself or how good the modeling is？



![](img/a165a3dbdfe2a42de38b6b11de2edad6_644.png)

 That is actually not a specific classifier that we are evaluating because here you can see that we have 5 different classifiers。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_646.png)

 Each of those classifiers are trained independently on different splits。

 So it is not one single classifier that we are evaluating。

 It is actually the choice of the features plus the choice of the classifier type plus the choice of the classifier hyper parameters。

 It is the actual full modeling pipeline that we are evaluating。

 all the parameters of the modeling pipeline。 And we try to evaluate the ability of that pipeline to run correctly in future data that we haven't seen yet。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_648.png)

 And the choice of all those modeling decisions that we made。 Yes， you have other questions。 Okay。

 so this was a K-fold cross validation that they are actually variants。

 So in the SKL model selection you have actually classes like K-fold。

 stratified K-fold and shuffle split。 And there are many more。 Many more。

 So let's have a look at those classes。 So stratified K-fold with N split equals 5。

 And you see here that when we do a CV split on some data set， it will return train and test arrays。

 And those arrays are integer values that can be used to fancy index the training set。

 And so basically what is important here for stratified K-fold is that it will look at the target value of the classes。

 basically， to find splits that preserve the balancing of the classes when it does the split。

 So to make this more easy to understand， there is some visualization here。

 So here we do stratified shuffle split。 And here you see using a number of splits that is set to 5。

 And so here you see that for the first split it used for the test set a concatenation of samples from 0 to 10。

 then from 50 to 60， then from 100 to 110。 And it will take those three black areas to construct the validation set and all the remaining samples that are white to be concatenated to construct the test set。

 In your opinion， why is it the case that we have this structure with three diagonal stuff in the stratified K-fold split。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_650.png)

 Here we are using the original ARIS dataset。 So there are three classes in ARIS。

 but even more important than this。 In the original ARIS dataset they are sorted by classes。

 So if we want to make sure that we balance and we have each class that is represented in the test set for each of the test set we will construct。

 we need to make sure that we do this。 Because here we didn't do any kind of random permutation。

 So stratified K-fold by default is not random， it's like K-fold cross validation。

 they are not random。 So if you do not ask for a shuffle random permutation。

 they will try to preserve the order as much as possible。

 but stratified K-fold will preserve the order with the constraint that you want also to preserve the balancing of the classes。

 So let's try to deal with those two constraints at the same time。

 If we do the same with regular K-fold， then we have this that we did previously and it is on the original data。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_652.png)

 And this is problematic。 We can also do it with 10。 10 is going to do many more splits。

 But this might be problematic。 I think there is an example。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_654.png)

 Yeah， we will see that as an exercise。 I won't tell the answer to the exercise first。

 So we can also visualize other strategies like shuffle split。

 So shuffle split you choose the number of split like we did for K-fold。

 But we also select the size of the test set as with the train test split。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_656.png)

 So shuffle split is basically iterated shuffle train test split。 So if we do that， you see this。

 And basically we do not try to preserve the ordering。 And we completely permit the order。

 And we just take 20% of the samples for the test set。

 And we take random order 20% each time for each split。 So there are still five rows in that matrix。

 But you see that it's completely random。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_658.png)

 And we can do a shuffle split with 20。 And so we will train 20 different models independently of one another。

 But each time 20% of the samples will be used for the validation set。 Okay。

 So if you want to use one of those cross-validation objects。

 what you can do in scikit-learn is create the cross-validation strategy like this。

 You pass the parameters for the cross-validation。 And then you store that as a CV object。

 And then to cross-valid score instead of passing 3 or 5 or 10 here。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_660.png)

 you pass the CV object itself and the strategy is encoded there。

 By default it would use K-fold cross-validation or stratifold cross-validation for classification。

 But if you want to use an alternate cross-validation， you can use this one。

 And here you see that we have this kind of result。 And if we use 20 iteration instead。

 we have 20 results。 And then we can compute the average and standard deviation and so on。 Okay。

 So the exercise now is use K-fold cross-validation， the standard K-fold cross-validation。

 in the same way that we did here。 On the original ARIS dataset without permutation。

 And see what kind of score you get。 And how can you explain this？ So let's try in 5 minutes。

 Maybe 2 minutes。 Okay， let's see the result because I would just like to give you a highlight of the notebooks after that。

 So if we do the same with K-fold equals 3， and we use the original data without any manually shuffling。

 then we get 0， 0， 0。 So the accuracy of the model is completely bad。 The worst that you can get。

 Why is it the case？ Yeah， opinion。 So yeah， because in the validation set you would see samples that you've never seen in the training set。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_662.png)

![](img/a165a3dbdfe2a42de38b6b11de2edad6_663.png)

 If you see， for instance， here， I would use this。 Recall that here it would be like 450。 Yeah， 50。

 exactly。 So it means that the class number 0 will be all the samples from the class number 0 will be put in the test set for the first one。

 And the train set will be only samples from the class 1 and 2。

 So you always evaluate on something that you've never seen before。

 So you ask to predict a class that you cannot predict because you've never seen it。

 So it's really a pathological case in this case because we are exactly the matching of the ordering that matches the split of the K-fold class validation。

 So you have to be aware of this kind of， if your data is ordered as some kind of dependency in the ordering。

 you have to be aware of this。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_665.png)

 Otherwise you might be very surprised。 So now we have K-fold class validation or cross validation in general。

 It's interesting to combine this to be able to do some automated hyperparameter search。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_667.png)

 So I need to execute this so very quickly。 So typically， for many models in machine learning。

 there are some hyperparameters that control the model complexity。

 And if the model is not flexible enough， it will have a bad classification accuracy both on the training set and on the cross validation accuracy on the validation curve。

 So the green here is either the cross validation score or the test score for a single test split。

 And if you give more flexibility to the model， then it might be able to reach some kind of sweet spot。

 But if you give it too much flexibility， then it will start to memorize some noise from the training set。

 So the training set accuracy will go to 100% because it can memorize everything。

 including the noise。 But then the decision boundary of that model will be very noisy。

 And on the test set， that noise is actually detrimental。

 And it's harming the ability of the model to generalize。 If we memorize noise。

 it's not useful for making good prediction on the test set。 And so in that case。

 when we have a big gap between the train and test accuracy， we see that the model is overfitting。

 So here there's a gap between train and test。 And here is a gap between train and 100% accuracy。

 So those are two different kinds of gaps。 This one is called underfitting between train and 100% accuracy。

 And this one is overfitting between train and generalization。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_669.png)

 Okay， so the goal of machine learning is by basically to find good modeling decisions to trade off overfitting and underfitting。

 And to do that automatically， we can either do it manually by doing the same kind of operation that we did previously and do cross-validation。

 And doing cross-validation many times for different values of the hyperparameter。

 So these are the numbers for the K-nearest numbers regressor。 And you see that for N=1。

 we have an average score which is close to 50%。 N=5， we have some good value here。

 But if we increase too much， then we go below again。 So here in your opinion。

 which model is overfitting and which model is underfitting？

 What is overfitting and 20 is underfitting？ Yes。 It's a kind of contraintative because a small value for a number of numbers will give more flexibility to the model。

 It gives the flexibility to remember individual sample noise。

 Whereas with large number of neighbors， it will consider a larger fraction of the data set to make a single prediction。

 So it will have a very smooth decision boundary and that may be also a problem leading to underfitting。

 So this is actually underfitting and this is overfitting。 So to do this。

 we can do a plot where we see the evolution of a number of neighbors and we go in a reverse order。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_671.png)

 So that this plot is approximately matching this order。 We are here。

 we have model complexity and accuracy。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_673.png)

 And you see that for the training set， when you increase the flexibility。

 your training accuracy goes to 100% accuracy。 But then we have some kind of sweet spot for the generalization。

 And here we have a limit of N=1 and we are overfitting here。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_675.png)

 Here we have a big gap and we have a small gap underfitting overfitting。 Okay。

 We have the same kind of problem with other models。 This is a support vector regression。

 There are two high parameters， C and gamma。 And you can see that for some values of C and gamma。

 we have a good score。 Like this one is quite good， for instance。 And this one is even better。

 And for some， a combination is very bad， like minus close to zero。 And so here in this case。

 it's hard to tell that there is no single parameter that captures the complexity of the model。

 It's a combination of two high parameters。 But in practice。

 gamma is very important and then C can be important。

 But so it's hard to do these kind of analysis and pick up the best one manually。

 You would have to do a nested for loops for all the parameters。

 So what we can do instead is use this tool in Scikit-Learn。

 where basically you give a grid of parameter values that you want to explore。 Yep。

 And then you will wrap your support vector classifier or support vector regressor into this grid search object。

 And this is basically a way to automate the search for the good parameter combination for the model。

 So let's do this。 We call fit。 So this is what we call a meta estimator in Scikit-Learn because it's an estimator that has a fit method that is wrapping another estimator。

 that has also a fit method but doing that many times。 And at the end of this operation。

 you can make some prediction。 And it's actually taking the best model that it found。

 retrained it on the full training set， and used that for the final model。

 So we can also introspect the best code that it found during the cross-validation procedure。

 So it's doing an internal cross-validation procedure。 This is why it's called grid search CV。

 CV is for cross-validation。 And we can also have a look at the best parameter that we are used for the support vector machine model internally。

 So this is a very useful procedure。 There is an alternative in Scikit-Learn which is called randomized search CV。

 This is an alternative to grid search CV。 The difference is that grid search CV will try all the possible combination and randomize search cv's or sampling parameters。

 Because if you have many hyper parameters with many possible values。

 sometimes it's not tractable to try them also。 You have no choice but to take a random search。

 random combination。 Yes？ The Scikit-Learn have other optimization routines built in， like steepest。

 descents。 So there are two levels of optimization in Scikit-Learn。

 Either to train the tunable parameters from the support vector machines， for instance。

 So each of the models has its own optimizer internally。

 But there are also black box optimizers for the hyper parameters， like grid search CV。

 randomize search。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_677.png)

 And if you want a smarter optimization routine for Scikit-Learn hyper parameters。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_679.png)

 you can have a look at what is called Scikit-Optimize。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_681.png)

 which is a subparty project that is compatible with Scikit-Learn。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_683.png)

 It's also on GitHub。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_685.png)

 And it has some documentation。 It's using additional models to find the hyper parameters of Scikit-Learn models。

 So for instance， you have GP minimize for Gaussian process。

 You can also use random forest from Scikit-Learn or Gaussian gradient boosted regression trees from Scikit-Learn。

 to actually find the hyper parameters of another Scikit-Learn model。 So it's a bit weird。

 but it's like nested optimization。 One is optimizing the hyper parameter of another machine learning model。

 And basically， it's not using gradient information。

 It deals also with the fact that you have noise in the cross-validation procedure。

 and it's kind of robust to do that noise to find the optimal hyper parameters。 So you have。

 for instance， this base search CV， which is an alternative。

 it's a drop-in replacement for a grid search CV that is the same API。

 but we'll find the good hyper parameters。 And there are several strategies inside。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_687.png)

 Okay， so just to have a look at the end， when you have those results。

 you can also have a look at the individual results using Pandas， by loading grid CV results。

 And you see for each parameter combination that we are explored。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_689.png)

 Parram C， parameter， gamma， the training time， the score time， the training。

 cross-validation values and so on。 And so you can see everything that was computed and introspected。

 and do plots if you want to understand the behavior of your model。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_691.png)

 So I think we're going to stop here。 Just maybe conclude on this diagram。 So either you can。

 first you need to split your full training set into a training data subset， and a final test data。

 This final test data， you never use it until the end and use it only once。

 You cannot use it twice because otherwise you're cheating。

 And so once you have done this training test split， you can do what we call nested cross-validation。

 inside the training data to find the hyper parameter， for instance using grid search CV。

 to do this procedure to find what is the best hyper parameters， that you can use。

 you can repeat the cross-validation many times with different hyper parameters。

 then pick up the best parameter combination and then finally evaluate it on the test data。

 And this is the final evaluation of your expected generalization ability of the model。



![](img/a165a3dbdfe2a42de38b6b11de2edad6_693.png)

![](img/a165a3dbdfe2a42de38b6b11de2edad6_694.png)

 And okay， I will stop here。 There are many more notebooks if you're interested。

 And many of those notebooks are actually taken from examples from the book by Andreas Miller。

 with the authors of this notebook。 And so if you're interested in going further and having some more narrative explanations。

 on how to just like it learned， you can have a look at this book which is called Machine Learning in Python I think。

 [pause]。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_696.png)

 Book Andreas。

![](img/a165a3dbdfe2a42de38b6b11de2edad6_698.png)

 [laughter]， It's Introduction to Machine Learning with Python。

 And it's basically a book version of what we thought today with additional information。

 so if you're interested。 And Andreas Miller is also one of the core developer of a psychic lab。

 He's around the conference with my team。 Okay。 Thank you very much for your attention。 [applause]。

 [BLANK_AUDIO]。