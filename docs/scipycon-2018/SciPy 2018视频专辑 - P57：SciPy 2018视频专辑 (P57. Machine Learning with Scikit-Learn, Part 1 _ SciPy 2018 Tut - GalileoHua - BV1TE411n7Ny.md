# P57：SciPy 2018视频专辑 (P57. Machine Learning with Scikit-Learn, Part 1 _ SciPy 2018 Tut - GalileoHua - BV1TE411n7Ny

 For this first introduction on the slides， I will first talk about what is machine learning。

 the main concept， then specifically， focus on what is scikitler on the library。

 And then I give you some context on when， and why we would use machine learning in some。

 data driven organization。 So predictive modeling or machine learning。

 is the ability to make some predictions of the outcome， of repeated events。

 So we have to use some observations， past observations， historical records of what。



![](img/c04d678b99df1406ae3dbf232bf3d810_1.png)

 we are interested in。 And we have to make the assumption。

 that the behavior that we are trying to model， is repeated in time。

 It has some structure that is predictable， basically。

 We cannot make machine learning on random observations。

 So the way that we do that is to use statistical tools， mathematics。

 to try to extract some kind of statistical summary， of the historical data and turn that summary。

 into some kind of executable model。 So an executable model is going to be a program。

 that you can run on your computers。 There are still a bunch of seats there。

 So you could see machine learning as an alternative。

 to programming hard coded rules written by experts that。

 know about the phenomenon that you're trying to model。 So for instance。

 if you know the laws of physics， you can write some kind of simulator， give some initial condition。

 and then a random program， to predict what's going to follow。

 But if you don't know the laws of the phenomenon， that you're observing， like for instance。

 if you're trying to build a recommender system that， will recommend in movies to users。

 you don't know how to model the taste of users， and how that will evolve over time。

 unless you are a very good psychologist。 And in that case， what you can do。

 is use the historical records， the past watching behavior， movie watching behavior of the users。

 to try to find how the movies are related， and to make good predictions on which movie。

 they are going to suit which particular users。 In practice， it's not necessarily an alternative。

 to hard coded written rules by experts， because for instance for our movie recommendation system。

 there is no expert available on us， that is able to make this kind of recommendation。

 for a population of 1 million of different people。

 It would be too expensive to try to hire experts to do this。

 So it's not tractable and machine learning， can fit in that kind of situation。

 Another rule of thumb when machine learning might be useful。

 is when the frequency of repeated event is quite high。 So you have maybe at least thousands。

 of repeated observations and maybe millions。 And making an individual mistake is not too costly。

 If it costs a lot like human lives or millions of dollars， to make a single mistake， you might not。

 want to use machine learning， because you're， going to make a mistake。 But for instance。

 if you recommend a bad movie to someone， it's not that big of a problem。



![](img/c04d678b99df1406ae3dbf232bf3d810_3.png)

 But as long as the recommender system， is better than not making any recommendation， basically。

 So here is an example to make things more concrete。

 So assume that you're running some kind of real estate。

 agency and you have a database of past transactions。

 So your database has columns with different types of values。

 So the first column is the type of housing， that has been sold in the past。

 The second column is the number of rooms。 So it's an integer。

 The first one is a categorical variable。 The third one is the surface in square meters。

 Then whether a Boolean flag were done or not， it's close to mass transit。 There is a seat here。

 There is no more seats。 And finally， there is a final column， here。

 which is the price of the transaction。 So this is historical data。 So you record it in a database。

 just， based on the operation of the agency。 So the vocabulary that we are going。

 to use to describe the structure of this data， is that the records， the rows of that matrix。

 are going to be called the samples， or the samples part of the training set。

 The columns that we are going to use as input to the model， are going to be called the features。

 And the output of the model， what we are trying to predict， is the target。

 And so basically based on these historical records。

 we are trying to find some kind of statistical relationship。

 between the target variable in this column， and the input variable， the features basically。

 And so we are going to extract this relationship， based on the training samples， based。

 on the statistical distribution of the training samples。



![](img/c04d678b99df1406ae3dbf232bf3d810_5.png)

 Then if you have a new potential customer， asking for an estimation of their own properties。

 you can ask them to describe their properties。

![](img/c04d678b99df1406ae3dbf232bf3d810_7.png)

 with the same features that you use to describe， the past transactions。

 And for those new properties， you don't know yet the price， because you haven't sold them yet。

 so you cannot know the price。 But then you can use the statistical model。

 that you train on the historical data， to give an estimate on what would be a good price to sell。

 those houses。 And you can also ask the model to give you， some kind of confidence interval。

 for instance。 So those two records here are what we call the test samples。

 that we are going to apply the model on those tests， samples to make some predictions。

 So the general data flow that we use for predictive modeling。

 is to start from some original historical records。 So depending on the domain of application。

 the original data representation that we have， can be very different from time to time。

 So for instance， you could use text documents， if you want to do moderation of comments on the website。

 Images for image classification， from images taken， from the camera of a mobile phone， for instance。

 of our specific sensors in an industrial application。 The sound recordings， if you want。

 to do a speech recognition， for instance， structured transactions in a database with columns。



![](img/c04d678b99df1406ae3dbf232bf3d810_9.png)

 or an Excel file， so on。 There is no more seats。 So the original data representation。

 is very domain specific。 And you might not be able to work directly。

 to do the statistical analysis of that data。 The original data format， the data representation。

 might not be suitable。 So what is important also is that for each of those records。

 in that database， you also have some kind of target， levels that you are interested in。

 For instance， for text document， it， could be whether or not a comment is offensive or not。

 If you want to do automatically moderation， or if it's a spam or not a spam。 If it's an image。

 you might ask human annotators， to label what is the interesting content of the image。

 So you need to record those target levels。 For sounds， you need some transcription。

 of what is interesting in the sound。 And in the transactions， it could。

 be one of the column of the database。 Like in this case， we just record。

 the activity of the operations。 And we have this target column that we're interested in。

 And we naturally have the labels based， on the operation of the system。 But in each of those cases。

 the first step， is to extract some kind of numerical representation。

 of the original data that will fit basically， in a two-dimensional numpy array or numerical metrics。

 And the important step is that this transformation， is domain-specific。

 But we need to make sure that those numbers here， they capture the interesting part of that original data。

 So this transformation， there is no generic way to do it。 It's very domain-specific。

 So you need some domain expertise as a data scientist。

 to know how to do this kind of feature extraction。 Nowadays， for sound and images， for instance。

 there are generic ways to do that， that are machine learning driven like neural networks。

 But for many other domains， you really， need some kind of domain-specific expertise。

 Once you have this numerical feature values， feature vectors。

 you can use a generic machine learning， algorithm， such as the ones that are provided in a psychic。

 learn。 And the result of that computation， of applying the machine learning to the feature vectors。

 and the labels will result in some executable model， which。

 is a program that you can save on the hard drive， and move it to another machine or maybe deploy it。

 on a mobile phone。 And then you can forget about this and only focus， on the model。

 The model will take new observations， the new recordings with the same original data representation。

 You need to apply the same feature transformation， feature extraction step。

 If it's not the same as this arrow here， the model is going to output meaningless predictions。

 But if you apply something that is consistent and repeatable。

 then the model will be able to predict the expected model。 It's going to be complicated。 OK。

 But there is a sit here。 But-- OK。 Maybe we can have an additional chair。 All right。



![](img/c04d678b99df1406ae3dbf232bf3d810_11.png)

 So all these operations， you could， for instance， if you have a small data site and you。

 want to do some kind of linear regression， to extract some trend from the data。

 especially if it's a transaction log that is naturally， represented in an Excel spreadsheet。

 maybe you can just transform the columns， to do some passing of the data or stuff like that。

 extract some features in new columns， and apply some linear regression routines from Excel。

 to extract your model， basically。 If you want to productionize this。

 to make it possible to deploy that as a program， it's better to use a generic programming language。

 and then such as Python so that you can package it， as a software， run tests， deploy it。

 with a continuous integration system， and stuff like that。 And furthermore。

 Python is able to scale to a larger amount， of data， like gigabytes of data in RAM easily。

 whereas with Excel it might be problematic。 And typically， if you want to do that in Python。

 you can use the pandas library to do what， is data transformation， extraction， feature， extraction。

 and stuff like that， and then use， psychic learn for the mathematical part。

 of the statistical predictive modeling part。 If your data is very big。

 the original data transformation， might not fit on a single machine in memory。 In that case。

 you might want to use， some kind of big data system， like a hive running， on Hadoop cluster。

 which is basically， some kind of SQL engine that run distributed operations， on the cluster。

 But there are many alternatives to do that。 And generally。

 when you extract the feature vectors here， even if the original data might be very big。

 the statistical summary that you extract， as feature vector for machine learning。

 might be much smaller。 And if it's the case， then you can use psychic learn。

 to build a model by loading the resulting feature vectors。

 in memory and running psychic learn naturally。 You can， as an alternative。

 use an analytics database， on the Cloud， for instance， such as Redshift or Google Big。

 Query or stuff like that， and do the same。 And this is very common pattern。



![](img/c04d678b99df1406ae3dbf232bf3d810_13.png)

 And also， you can use alternative， if you don't want to use Python。 There are also， for instance。

 Spark， that can do both the data pre-processing part， and also some features for machine learning。

 And nowadays， you could also use a desk， for the scalable data pre-processing part。

 and a psychic learn for the machine learning part。 And this， we are going to present it。

 a bit during the conference。 So here are some typical applications， for real life machine learning。

 predictive modeling。 So those are all users of psychic learn。

 They publicly communicated about their use of psychic learn。 So， for instance， the New York Times。

 has a team of data scientists that， works on modeling the virality and the engagement of the readers。

 the variety of the news and the engagement of the readers。 RBNB is using a lot of machine learning。

 to do fraud detection or pricing modeling for apartments。 Spotify is building a recommender system。

 to build personalized， reduced base， on the listening behaviors of the users。

 to build automatic playlists that， are personalized for each individual users。

 BHBox does a lot of inventory forecasting and trends， detection in fashion or in any other items。

 You can also use machine learning， to do a predictive modeling of the operation。

 of a complex industrial system。 And in that case， the goal is to build a model。

 of the regular operation of the system。 And as soon as you detect a drift。

 then you can detect that there might be a problem。 And if you let it happen without intervention。

 that might lead to some kind of accident that， might be very costly。

 So you can send a maintenance team before the accident happens。

 And this is what we call the predictive maintenance。 And for this kind of operation， you。

 could use what we call anomaly detection， which， is a family of machine learning algorithms。

 And finally， there is a OK Cupid that， has a weird particular case of a recommender system。



![](img/c04d678b99df1406ae3dbf232bf3d810_15.png)

 for personality matching for the team website。

![](img/c04d678b99df1406ae3dbf232bf3d810_17.png)

 And there are many others applications， so fraud detection， churn。

 those are very common applications。 So this is all business application。 But here at SIPI。

 it's maybe more scientific audience。 And so you can guess that machine learning and psychic learn。

 can be used also to help solve scientific application， in astronomy， genetics， or whatever。 OK。

 so now a psychic learn。 So a psychic learn is an open source machine learning， library。

 So it's written in Python because it's SIPI。 We rely a lot on NumPy for the arrays and linear algebra。

 routines on SIPI for some data structures， like sparse matrices and also for optimization algorithms。

 And we also have some quite extensive use of SIPI， to be able to accelerate some very compute。

 intensive algorithms that do not naturally--， that are not naturally expressible。

 using a combination of vector operations such as what。

 we could do with NumPy linear algebra operations。 So NumPy is very fast as long as you're。

 doing NumPy array operations like a vector matrix， multiplication， for instance。

 But sometimes you need to do nested for loops， for algorithms such as decision trees， for instance。

 And in that case， NumPy cannot be used to accelerate， the computation。 And in that case。

 we use SIPI。 The main feature that is very interesting in a psychic learn。

 I think the reason why a psychic learn became popular， is that when we designed the library。

 we made a lot of effort to ensure， that the API is very simple。

 The public API is very simple and very homogeneous。

 so that we have many machine learning algorithms that， are implemented in the library。

 And most of them， they will implement two of those methods--， fit and predict or fit and transform。

 We will explain later what it means。 So this is， I think。

 what makes a psychic learn very interesting。 And finally， we also provide some additional tools。

 like model assessments， to evaluate， the quality of a model， the predictive quality of a model。

 model selection to automatically select， the hyper parameters of the model。



![](img/c04d678b99df1406ae3dbf232bf3d810_19.png)

 We will also present that this afternoon， I guess。 And also how to build and some balls of models。

 For instance， some models like decision trees， that are not very good when you train them individually。

 But if you're trying a big ensemble of them， they are much more accurate。

 So I have questions so far on everything， that I presented。 No？ [INAUDIBLE]， So， sitan。

 we use it whenever we need--， you have typically when we have two nested loops that。

 run over many iterations， like millions of iterations， for each of them。 And some operations。

 like metrics， metrics， multiplication， you can express them and compute them very efficiently。

 using NumPy because NumPy and other hood， is using a blast implementation， so linear algebra。

 routines。 But some operation， like making prediction or training， a decision tree algorithm。

 it's not a vector operation。 So it's iterating of our column of values and computing。

 entropy and stuff like that。 But it's a sequence of scalar operations。 And in that case。

 NumPy cannot be used to accelerate， the computation。

 And we need some kind of a compiled level native programming， language to do that。

 So sitan is basically some kind of extension， of the Python syntax that will be converted to a C program。

 and that will be compiled using GCC or another C compiler。

 and then be embedded in the Python program as an extension。

 Alternative to sitans include the number， for instance。 Nowadays。

 we could have used number when we started the， cyclone project number， which didn't exist。

 So we started with sitan。 NumPy is more dynamic because it can compile on the fly。 Whereas sitan。

 you have to compile ahead of time， which， has pro and cons。

 But we are reasonably happy with sitan so far。 So we don't plan to switch anytime soon。



![](img/c04d678b99df1406ae3dbf232bf3d810_21.png)

 But if we were to start the library nowadays， maybe we， would have used NumPy instead。

 So it's just like Jackson， right？ Like what？

![](img/c04d678b99df1406ae3dbf232bf3d810_23.png)

 - Jackson。 - Jackson？ - The Java implementation of Python。 - Ah。

 not exactly because I think the Java implementation。



![](img/c04d678b99df1406ae3dbf232bf3d810_25.png)

 of sitan is still an interpreter。 Well， here it's really a compiler。

 It is a new kind of program that is--， we sitan generate a C program that is compiled， and then。

 it's native code that is an extension。 But yeah， maybe Jitan， the GVM is able to do some kind of。

 optimization at runtime， but I'm not sure how much they can， do。

 So if we take the predictive modeling data flow that I。

 presented earlier and just put it vertically， so we start， from the training data。

 So here the feature extraction is already being done。

 And so the train data is an empire array with two， dimensions。

 the number of records and the number of。

![](img/c04d678b99df1406ae3dbf232bf3d810_27.png)

 features。 And we also have a single， for instance， vector for the。

 training labels for each of those records。 And so this is also an empire array。

 So we call the inputs x and the output y。 And x is two-dimensional or an empire array and y is one。

 dimensional empire array of labels， target values。 And so to build a label in Scikit-Learn。

 we just import a， class from one of the packages of Scikit-Learn。

 We instantiate the class by giving some hyperparameters。

 And then we fit the model on the training data。 Once we have done this。

 the model is been modified in， place and we can call predict on new data。

 So this new data has the same number of columns as the， training set。

 So it's also an empire array with two-dimensional， empire array， basically。

 And this time it will return an estimation for y。 There is no room left。 You can sit on the stairs。

 And so basically it will return an empire array as the， output for the predictions。

 And if you have the access to the true labels for the test， set。

 then you can compute some performance metric for the。

 model to see whether or not your model is able to， generalize on new data。

 So we could also compute the accuracy score on the training， set on x-train and y-train。

 But generally it's much less interesting because we want to。

 have a model that is able to make good prediction on future。

 data that we don't have access at training time。 So as I said previously。

 all the models in Scikit-Learn are， very homogeneous API。

 So here this is a very simplistic Python program that。

 does exactly the same operation but with a different， model。

 This time we use support vector machines from SK-Learn SVM。 We create the model。 We call fit。

 We make some prediction。 And then we compute some performance metric。

 Here we use F1 score instead of accuracy。 It's just another classification metric。

 So because the model has a fit and predict method， it's all。

 the model for classification in Scikit-Learn have the same， fit and predict method。

 So you can replace that model by another classifier in， Scikit-Learn， for instance。

 logistic regression。 And only the first two lines need to change。

 And the rest of the training and prediction and evaluation， are the same。

 If I switch between the two slides， you can see that only， the first two lines change。

 And if you want to try something that is more complex， than just a linear classifier。

 you can use a random forest， for instance， and again， only the first two lines change。 Oops。 Sorry。

 So why we have so many machine learning models， why there。

 is no one good models that works everywhere？ It's because most of those models。

 they make some strong， statistical assumptions on the distribution of the data and。

 how the labels are related to the input samples。 So here I have three classification problems。

 One of the goal is to predict whether a dot will be blue or。

 red based on the location in a 2D space。 So the input features are two continuous variables that are。

 the x and y axis on this 2D plane。 So the first data set， you have two groups of dots that are。

 nested in one and into the other。 Like not overlapping， but there is a half-moons， basically。

 like the one into the other。 The second data set has the blue dots in the middle and red。

 dots all around， plus some noise。 And the last one is two blobs， blue on the left and red on。

 the right， but there is also noise， so they overlap a bit。

 And so you can see that in the first column here， we have a。

 machine learning algorithm which is called nearest， neighbors classification。

 K nearest neighbors classification。 And so you see that it's able to find a statistical。

 decision function here that find the boundary between the two， areas。

 And here it's able to identify that in the center， that， are the blue and outside there is the red。

 And some kind of straight line here in that case。 So this model is some kind of database that can generalize。



![](img/c04d678b99df1406ae3dbf232bf3d810_29.png)

 by computing distances to new data points。 But it doesn't make us any strong assumption on the。

 structure of the data。 And in most cases， it's able to find approximately good， separation。

 But you see that the decision boundary is very noisy。 So that might be a problem。 Here。

 the second column is a linear model。 And you see that the boundary that separates the blue region。

 from the red region is a straight line in the 2D space。 And so especially in that case。

 making this assumption that， there is a straight line that separates the blue from the。

 red is completely wrong。 So in that case， it's making a bigger like the quality of。

 the predictions here are very bad。 However， here it's the correct assumption because there is。

 no-- it's the best way that you can separate the blue from， the red。 So here。

 this model is the best。 And it's also the fastest to train because linear models。

 generally are really fast to train。 So it's a good baseline to try fast。 And there are also。

 for instance， support vector machines， with RBF kernel that is basically some kind of smooth。

 version of a Kenerys neighbors。 You can interpret it this way。 And in this case。

 you can see that the decision boundary is， much less noise。

 So it might be better in all those cases。 But maybe in high dimensional data， that might not。

 always be the case。 You also have decision trees here in this column， and。

 random forest next to decision trees， which is basically an， ensemble of decision trees。

 And you can see that it's kind of good in most of them。 And there are many other algorithms。

 I won't go further。 The main point here is that depending on the assumptions。

 that you can make on your data， sometimes a linear model。

 is going to be the best one that you can get。 Other times。

 you really need some kind of non-linear models， like decision trees or a support vector machine with a。

 non-linear kernel。 Otherwise， you will get bad predictions。

 And we will see in the notebooks how to evaluate those， qualities。 So yes？

 So the colors here in the background are basically the， predictions of the model。

 If you take a new point in a location that is not a。

 location that you have observed in the training set， how the， model will predict the class。

 And if it's dark red， it's going to be very confident that， it's a red location。 If it's dark blue。

 very confident that it's a blue， location。 And if it's whitish， it's going to be not very。

 confident。 So it's going to give you a probability of 0。6 that it's， red， for instance。

 And you can use this confidence level or so to， decide not to make a prediction where you're not。

 confident enough。 And you prefer to give no answer than a bad answer， for， instance。 Sometimes。

 depending on the application， maybe a good， idea to do this。

 So if you want to know about all the models that are。

 implemented in scikit-learn for classification， regression， clustering， dimensionality， reduction。

 model， section， and pre-processing， we will explain what those， mean in the tutorial today。

 But there is also extensive documentation online。 I think this is another reason for the success of the。

 scikit-learn project is that from the beginning， we decided， to document everything。

 So we reject pull requests if the documentation is not up， to date。

 And I think this makes also a very good resource to gain。

 deeper knowledge on how the machine learning， algorithm work and in which case they work and in which。

 case they tend to fail。 So don't hesitate to use this。 And you can just Google and most of the time。

 if you， Google scikit-learn something， you will find the， documentation。

 So now let's step back a bit and think about where to use， predictive models。

 So assume that you are running some kind of data-driven， organization。

 So the input for the stream of data that you will collect is， the user activity of your application。

 if it's a mobile， application， or some desktop application， or workstation。

 application that you connect it to a network。 Or sometimes you don't have users。

 but you have a network， of sensors in a IoT application， for instance。 But in all those cases。

 basically each of those client， components will emit a stream of events that you can。

 collect in a distributed event log with queues。 That will basically make sure that you record all the。

 events for the users， even if one of the machines here dies。 There is some kind of redundancy。

 And make that stream of events categorize a variable to。

 different kind of services in your application。 And basically。

 it's very often the case that if you have a， high throughput of events collected from the client。

 applications， sometimes you need to make very quick， decisions。

 So you will have some kind of stream processing system that。

 is also distributed for redundancy and scalability。

 That is being to make transformation very quickly and。

 to put the result in some kind of database that is serving a， web user application web interface。

 for instance， or a， mobile app。 So this is some kind of online transaction processing。

 system or online database。 And that answers the query of the user to refresh a page。

 So for instance， if you consider a Twitter application， if， some user uses a mobile phone to tweet。

 you will send the， tweet to this system here to make sure that you don't， lose it。 Then process it。

 like find the list of all the followers， that you see the tweet。

 And then start in the database in the timeline of all those， users。

 And if any of the followers refresh the page， we ask this。



![](img/c04d678b99df1406ae3dbf232bf3d810_31.png)

 and see the new tweet collected with all the other， tweets that have been tweeted recently。

 So this typically takes less than one second or a couple of。



![](img/c04d678b99df1406ae3dbf232bf3d810_33.png)

 second maximum。 And then you typically have some kind of a long time batch。

 processing system that is able to perform operation on， histories of collected events。

 So for instance， the first step is to store the data in some。

 kind of structured distributed storage。 It can be a structured lecture。

 It can be just a HDFS distributed file system。

![](img/c04d678b99df1406ae3dbf232bf3d810_35.png)

 And then you have on top of that a distributed batch。

 processing system that can aggregate compute statistic on。

 whole historical part of the system and output some kind of， statistical summary。

 So these operations， you can store the result in a， structured database for fast analytical queries。

 So if you have business analysts in your organization， you。

 might want to output some kind of dashboards for running the。

 company and seeing how the trends of the sales evolve in， different regions of the world。

 for instance。 But you can also use this analytical database or directly。

 this distributed batch processing system to extract， features for building productive models。



![](img/c04d678b99df1406ae3dbf232bf3d810_37.png)

 And predictive models， they can also put some kind of， forecasting for the business analyst。

 But they can also be used for making recommendations to， kind of hand-hands the application for。

 for instance， for Twitter， you can highlight the recommended tweets， like。

 a statistical summary of the most important tweets。



![](img/c04d678b99df1406ae3dbf232bf3d810_39.png)

 And also you could use the predictive models， embed a。

 copy of the predictive model directly in the stream， processing system for automated moderation。

 like， spam filtering also。

![](img/c04d678b99df1406ae3dbf232bf3d810_41.png)

 So that you don't store the tweets that are spam， you， rejected them from the beginning。



![](img/c04d678b99df1406ae3dbf232bf3d810_43.png)

 So to do this kind of architecture， this is really。

 a pattern that you would see in many organizations。 There are standard machine learning。

 not machine， learning， open source systems to do each of those steps。 Like for instance。

 for the distributed queue system， you， can use Kafka。 For the streaming system。

 you can use Apache storm or， Spark streaming or Apache Flink。

 For the database that starts the result and is very fast， to answer the queries。

 you can use HBase or， Cassandra or stuff like that。 For distributed system for the storage。

 long-term storage， you can use HDFS and Hadoop or some store on Amazon S3。

 You can use MapReduce Hadoop for batch processing system， Redshift as an analytical database。

 SiteKitLion for， instance for machine learning and so on。 But you can use other combinations。

 like Spark can do， many things， so it's quite popular。 And you can also use it from Python。

 I think I will stop here for the slides and now we are， gonna switch to the Notebooks。 Okay。

 so first， I hope that you could all get cloned this， and get that folder。 As I said previously。

 we made some changes yesterday。 So if you use Git， you can do a Git pool to get the latest， changes。

 Otherwise， don't worry， to match the changes are very small。 So there is a bunch of Notebooks。

 The first ones are introductory and in the afternoon。



![](img/c04d678b99df1406ae3dbf232bf3d810_45.png)

 we will focus on the last ones。 So we will also， the first Notebooks are just summarizing also some of the。

 concepts that are presented in presentation。 And then we will also introduce our， how to use the。

 scientific computing tools ecosystem from Python to make。

 sure that you are comfortable with everything。 So Guillaume is gonna give you a。 - So hi everyone。

 So I think that's the first Notebook， who already。

 like introduced extensively how you can use machine， learning。

 so that will just be like a wrap up of what you， said and the small details， for instance。

 on the data set， that we'll use during the day， okay， so it's specific。 So what is machine learning。

 really， really speak about it。 So we have usually two phase where we try to train a model。

 and learn the models and then the second phase where we're。

 trying to test some model and how good it can generate。

 So we have a training phase and a generalization phase。 So to do that。

 usually we need data and the one that we'll， use in the first steps is a data set which is called Iris。

 So it's a biology database of only 150 samples。 So usually the toy data sets， okay。

 is to play around。 And it was used in the times to actually differentiate， three types of Iris。

 so the Cetosa， Vercicholors and， Vercenica， which for anybody like me， I cannot even see。

 the differences， but for people which are used to it， because they look at the Cetpal， so one type。

 I mean， you have the petal and the Cetpal which are in the two， parts of the flowers and then also。

 I mean， with the size， and the width and the height of those， they can actually。

 differentiate the species。

![](img/c04d678b99df1406ae3dbf232bf3d810_47.png)

 So a lot of the thing as a being will be to， for instance。

 play with this data set and try to classify those。 So how do we basically represent our data sets？

 Or you already mentioned it， we have a kind of metrics。

 where each row is a clear samples and a feature is a column。

 So here's a feature for this Iris data sets。 Thanks。 Is， for instance， the width of the petals。

 a second column， will be the height of the petals and then the width of。

 the Cetpal and the height of the Cetpal for the to the column。

 So we have for this data set four features， which just， represents the dimensions。

 We could add several features， for instance， colors and stuff like that later on。

 So then there's two way of doing machine learning， and one is classification。

 the other one is the regressions。 So classifications， typically， is one of the flowers。

 When the target， what we try to classify is actually a category。 So for instance。

 one of the three types of flowers， or for instance， classify spam via non-spam。

 That's the categories。 And the second task or program is regressions， where actually our target。

 is a continuous variables。 So for instance， from some sensor， you。

 want to predict the temperature of tomorrow。 So temperature will be a continuous variable between 0。

 and a lot of Fahrenheit。 And you will try to find the point there。

 So is where you have-- and those one， because you will use the target。

 So you will learn-- you have x and you have a corresponding， target， you will learn a model that。

 will find the relationship between both。 And the second type of machine learning。

 that you have is unsupervised learning。 So you just have you x。 You don't have any targets。

 And from that， you will try to find a structure inside， the data themselves。 So in this case。

 we have this type of taxonomy， so where you have machine learning， unsupervised learning。

 unsupervised learning。 So we spoke a lot about classification， for instance， with the flower case。

 regression for instance， estimating temperatures。 We have something a bit more ranking。

 when you want to make recommendations system， where。

 you want to say that this is better than this--， I mean， this movie is better than the other one。

 so you have kind of this。 And in the unsupervised case， you have three families。



![](img/c04d678b99df1406ae3dbf232bf3d810_49.png)

 so Olivia already spoke about an honorary detection。



![](img/c04d678b99df1406ae3dbf232bf3d810_51.png)

 with the predictive maintenance， for instance。

![](img/c04d678b99df1406ae3dbf232bf3d810_53.png)

 And the other case is more to simplify。

![](img/c04d678b99df1406ae3dbf232bf3d810_55.png)

 the representation of data。 So clustering would be to try to group samples together。

 to reduce the complexity。

![](img/c04d678b99df1406ae3dbf232bf3d810_57.png)

 And the dimension reduction could， be to reduce the number of features。

 So find if we have a space with a lot of features。



![](img/c04d678b99df1406ae3dbf232bf3d810_59.png)

 we want to find a subspace with a smaller feature where we just， project into that space。

 And we can use this， for instance， for visualization。 So imagine that you have 50 features。

 and you can see only 2D with your highs。 You could project this into 2D and then。

 see if there is a structure there in 2D dimension only。



![](img/c04d678b99df1406ae3dbf232bf3d810_61.png)

 So that's about these things。 So do you have any question on those？



![](img/c04d678b99df1406ae3dbf232bf3d810_63.png)

 Yeah。 Can you mention targets and then you mention labels？ So are they the same thing？

 They are exactly the same things。 So usually we sell--。

 I don't know if we sell labels for classifications。 Yeah。

 We'd say labels is more for categorical variables， categorical targets。 And when you do regression。

 it's a continuous variable。 So you could call it a label， but maybe it's an abuse。 Yeah。

 it's an abuse。 And also sometimes when we do regression。

 we can have multiple targets at the same time。

![](img/c04d678b99df1406ae3dbf232bf3d810_65.png)

 You can predict the price and the temperature and power， or something like that。



![](img/c04d678b99df1406ae3dbf232bf3d810_67.png)

 Just to add some point about this。 So sometimes， in supervised learning。



![](img/c04d678b99df1406ae3dbf232bf3d810_69.png)

 it's used to find a simplified representation of the data。

 that you can use to gain some insight as a human， to see the data set。

 Like if you find groups of users for marketing purpose， for instance。

 you can simplify your audience， and present that in a slight deck to business people。



![](img/c04d678b99df1406ae3dbf232bf3d810_71.png)

 Our dimensionality reduction is useful for visualization。



![](img/c04d678b99df1406ae3dbf232bf3d810_73.png)

 to project into the space。 But it can also be used as a pre-processing step。

 for supervised learning。 So this is another application of unsupervised learning。



![](img/c04d678b99df1406ae3dbf232bf3d810_75.png)

 is to find a new representation of the data， without the labels。 And then you hope that it's going。



![](img/c04d678b99df1406ae3dbf232bf3d810_77.png)

 to be useful if you stack a classification model on top， of that new representation， for instance。

 So this is another application of unsupervised learning。



![](img/c04d678b99df1406ae3dbf232bf3d810_79.png)

 [INAUDIBLE]， [INAUDIBLE]， [INAUDIBLE]， Yeah。 Yeah， both things。 So in the WebPAD。e issue。

 you have the classification， of unsupervised learning， so like clustering methods。

 and classification methods and regression methods。



![](img/c04d678b99df1406ae3dbf232bf3d810_81.png)

 So you can easily find which one you want to tackle down。 So now， Olivia will start with how。

 to use a notebook with tricks and shortcuts。 So if you open the second notebook。

 maybe it was a bit quick， but this is a notebook number two。 In the list， it's this one。 So here。

 I decided to hide the toolbar， but if you use， the traditional Jupyter notebook。

 you have this toolbar。 If you use a Jupyter lab， you have a similar toolbar。

 It might be slightly different。 But in both cases， you have a button。

 to execute the current cell and move on to the next cell， which， is this button。 In practice。

 I would recommend not， to use the mouse and the click and try。

 to learn the shortcuts to do the same。 So I will just hide this because otherwise it。

 takes too much place。 So something that is very also important。



![](img/c04d678b99df1406ae3dbf232bf3d810_83.png)

 is that Jupyter gives you the ability， to introspect the API of functions or classes。

 that we are going to use。 And for instance， you can use a shift plus tab。

 when you open some function。 And it also makes it possible to read the documentation。

 using the question mark。 Oops， sorry， I didn't meant to commit this yesterday。

 So I'm going to give you some keyboard shortcuts， that are very useful for Jupyter。 So first。

 to get the list of the keyboard shortcuts， what you can do is press escape to make sure。

 that the selection of the cell is in blue mode here。 And then press H。

 And then you see all the keyboard， shortcuts that are available。



![](img/c04d678b99df1406ae3dbf232bf3d810_85.png)

 And there are two groups of keyboard shortcuts， some that are for the edit mode and some that。



![](img/c04d678b99df1406ae3dbf232bf3d810_87.png)

 are for the command mode。 To go into command mode， you have to press escape。



![](img/c04d678b99df1406ae3dbf232bf3d810_89.png)

 And basically， the selection will be blue， and you're in command mode。

 If you click on a cell or if you press enter on a cell。

 you will enable the edit mode of that specific cell。

 So it's very important to know in which mode you are。



![](img/c04d678b99df1406ae3dbf232bf3d810_91.png)

 So first， let's go into the blue mode， command mode， by pressing escape。



![](img/c04d678b99df1406ae3dbf232bf3d810_93.png)

 Then you can press B。 So when you press B， it will insert a cell。



![](img/c04d678b99df1406ae3dbf232bf3d810_95.png)

 below your current location。 If you use the arrow keys， you can move the selection around。

 And you see here we have a code cell， where you can write Python code， for instance， print test。

 And execute it by pressing shift enter。 OK。 So you can move the arrow back to the original location。

 on the same cell and press enter again。 And you see it switches to green mode。



![](img/c04d678b99df1406ae3dbf232bf3d810_97.png)

 And then you can， if you move the arrows here， you can move around horizontally in the text。

 If you press enter here， you have a new line， print another line， for instance。

 And then press shift enter again。 And it moves on to the next one。

 So something that is weird here is that I pressed enter also， in this cell。

 And you see that here I have this weird representation。 If I press shift enter again， it's。

 executing the text basically and basically rendering the HTML。

 So if I double click here or if I press enter， you see to edit the text。

 because this cell is marked on a cell。

![](img/c04d678b99df1406ae3dbf232bf3d810_99.png)

 So you have two types of cell。 Either the code cells like this one， Python code cells。

 or marked on code cells。 So what you can do is switch the cell type from one type。

 to the next by first pressing escape to be in command mode。 And then if you press M on a cell。

 it will convert it into a text cell。 So here it ignores that it's Python anymore。

 and doesn't execute it anymore。 It's just HTML text or marked on text。

 If you want to switch back to Python mode， you can press escape to make sure that you're in blue mode。

 And then why？ And then you're back to your two Python。



![](img/c04d678b99df1406ae3dbf232bf3d810_101.png)

 You can execute again。 So in the text cell， you can also put images。 So for instance。

 if you go before， like there is a big cell at the beginning。 If you double click on it， you see。



![](img/c04d678b99df1406ae3dbf232bf3d810_103.png)

 that this is actually marked on with a mix of text titles。

 and also this syntax to insert some images。 So I don't want to modify it。

 That is just if you get this representation， don't worry。 You can just press shift enter and you。

 go back to the HTML rendering of the marked on。 So if you select the cell where we have executed the print。

 statement， you see that there is a counter here that。

 is incremented and that say that this is the instruction， that we have executed。

 If you press control enter instead of shift enter， it's going to execute this cell in place。

 and not move the cursor around。 So if I do that several times， you。

 can see that this counter is incremented。 You can also define a variable like a equal one here。



![](img/c04d678b99df1406ae3dbf232bf3d810_105.png)

 Press shift enter。 And then insert a new cell， a new Python cell。



![](img/c04d678b99df1406ae3dbf232bf3d810_107.png)

 So here I'm on the here and I would， like to insert a cell here。 If I press B。

 it's going to insert a cell below。 In your opinion， what should I press to insert a cell above？ A。

 So let's do A。 And here if I do print A to print， the value of my variable here， you。

 see that the two cells that are related， they are running the same environments。

 If I define a variable here， I can access the content， of that variable in the next cell。

 So they are all running together， which means that we need to run the cell in order。 Otherwise。

 we might access a variable that is undefined， and get an exception message。 For instance。

 if I press B and B has never been defined before， I get a name error and it says B is not defined。

 When you get an error message in Python， it's very important to actually read the error message。

 And not panic。 And the part of the error message that is most important。

 is generally at the bottom of the trace back。 So I don't know why the rendering is weird here。

 So usually you have this kind of trace back， and then the error message and then maybe several steps。

 And finally， the inner， the original problem。 And so here it says exactly that B is not defined。

 So what we can do is define B equals 2， and now we don't have a message。

 So here we use a print to see the value of B， but it's also possible to just be at the end。

 And then we have out the output is basically， the last Python object in the cell。

 It's also printed by default。 It's also interesting to know that you。

 can delete a cell and move it around。 For instance， you select the first cell here。

 You can press X and then V。 And basically it's copy and paste。 So you need to be in a cut and paste。

 You need to be in command mode to do that。 So press escape first， X， and then move somewhere else。

 and V to paste it。 OK。 So if you press-- if you delete cell by mistake。

 and you don't-- and for instance， you copy something else， and you lose the ability to press V。

 you can also use the edit menu here， and you have undo delete cells that you can do。



![](img/c04d678b99df1406ae3dbf232bf3d810_109.png)

 or repeat it several times to get yourselves back， if you delete them by your--， OK。

 So I think that's it for the main keyboard shortcuts。 Now we're going to talk a bit about NumPy。

 So NumPy is a baseline library， a building block library， for the full SciPy ecosystem。

 So it gives you the ability to build a numerical arrays。

 and to do algebraic operations on the solar arrays， and linear algebra in particular。

 So for instance， we can use--， so this is a convention to import NumPy as NP。

 to have some kind of short alias for the NumPy library。 And then we can do NP， some modular。

 some functions。

![](img/c04d678b99df1406ae3dbf232bf3d810_111.png)

 or classes to use it。 So for instance， if you want to use a function。

 and you don't know what parameters that function take。

 you can put your cursor inside the function here， and press shift tab。 Actually。

 I need comma here and it doesn't work。 Ah， yeah， I need to import NumPy first。

 Then if I press shift tab here， you。

![](img/c04d678b99df1406ae3dbf232bf3d810_113.png)

 see that I have the documentation。 If I press shift tab a second time--， groups。 [INAUDIBLE]， Oh。

 plus here。 OK。

![](img/c04d678b99df1406ae3dbf232bf3d810_115.png)

 That's weird。 There is something weird on my machine。



![](img/c04d678b99df1406ae3dbf232bf3d810_117.png)

 If you press plus here， you can see， the full documentation of that function。

 And here there is a single parameter that is important， which is the seed。

 And it takes place in what it is。 So-- and also， for instance， if you don't remember。



![](img/c04d678b99df1406ae3dbf232bf3d810_119.png)

 the end of something， you can press， tab after the dot here。

 And it will give you the list of classes that are in that module。

 or the list of functions that are available in that module。 So here I want to use random state。

 and then seed equals 1， 2， 3。 So I will create a random state object， and call it R&D in a variable。



![](img/c04d678b99df1406ae3dbf232bf3d810_121.png)

 And then use that R&D variable that a random state object。

 to sample some data using the uniform distribution， between 0 and 1。

 And I will generate an array with two axes。 And the first axis， a three-dimension。

 and the second axis， I have five dimensions。 And so then I can print my array。 It can execute again。

 And so when you print an empire array， you see that it looks like a Python list that are nested。

 and without the commas。 It's just the string representation of the array。



![](img/c04d678b99df1406ae3dbf232bf3d810_123.png)

 Alternatively， what we can do is just do that with x。 Here， and we see that it's an array。

 It's more explicit。 And basically we have values between 0 and 1。 They're all positive。

 And you can see that we have three rows and five columns。

 So what the size here can be either an integer。

![](img/c04d678b99df1406ae3dbf232bf3d810_125.png)

 or a shape using a tuple。

![](img/c04d678b99df1406ae3dbf232bf3d810_127.png)

 For instance， if we want more levels， we can have three axes。

 And here you can see that we have three nesting levels--， 1， 2， 3。

 So we come back to the original array。 Something that is interesting also。

 is that if you press A to have a new cell， all of the array， have a shape。

 So the shape is the n-dimensional size of the array。

 So the number of rows and the number of columns。 And if you have 3D。

 then it's just axes in the right order。 And also， there is a data type。 So if I press Bx。dtype。

 and it's the type of the elements， of the array。 So here it's 64-bit floating point values。

 so decimal values。 You can also have integers or Boolean variables， and so on。 Complex variable。

 And different level of precision。 So once an array， we can use this syntax。

 to access a specific value。 So because my array has two axes， I can use an integer index。

 the first row， and the first column。 And I will get this element at this location。

 I can check that 0。69 is this one。 So if I change this， if I take one instead， I will get this one。

 So here， first is the lines and the rows and then the columns。

 And also something that is very important to know， is that in Python， when you index。

 it starts at 0。 It's not like MATLAB or R。 That's started one。 In Python， it started 0。

 You can also get a full row instead。

![](img/c04d678b99df1406ae3dbf232bf3d810_129.png)

 of a single element of the row。 So here we take the full second row。

 And this is actually an empire array。 If I remove the print here--。

 you can see it's an empire array。 And it's basically a slice of the previous array。

 It's also possible to slice a column， by using this marker， the column marker。 So here。

 it means that basically we take all the rows that， match the first column。

 This is some kind of wild count。 So if I do that， we take the first column。

 So we have three elements。 We have three rows in the first column。 If I go back here。

 we take those three values vertically。

![](img/c04d678b99df1406ae3dbf232bf3d810_131.png)

 So here， it's also possible to use this notation， to get the row by taking--。

 by putting it explicitly like that。 If you have a single integer， it's the first axis。

 But you can be more precise and slice this way also。 This slice notation is actually a shortcut。



![](img/c04d678b99df1406ae3dbf232bf3d810_133.png)

 for 0 to minus 1， which means take everything。 Yeah。 Not minus 1， actually。

 because the last one is excluded or worse。

![](img/c04d678b99df1406ae3dbf232bf3d810_135.png)

 So you can actually put integers like 0 to 2， for instance。

 to slice a specific part of 0 to 1 and so on--。

![](img/c04d678b99df1406ae3dbf232bf3d810_137.png)

 1 to 2 and stuff like that。 And you can use minus 1 if you want to--。

 or minus 2 if you want to start counting from the end， of the array。

 So when you just have the column， it basically take everything。 Otherwise。

 you can put integer before and after the column， for the beginning and the end。



![](img/c04d678b99df1406ae3dbf232bf3d810_139.png)

 And the end is not included。 All right。 So this is like Python list slicing。

 But the difference with Python list， is that we can have n dimensions。

 So we can take many slices and on different axes。

![](img/c04d678b99df1406ae3dbf232bf3d810_141.png)

 There is this notion also of transposing an array。



![](img/c04d678b99df1406ae3dbf232bf3d810_143.png)

 So this is the same array。 But this time， if you look at the shape--， the shape-- I don't know。

 I need to put it inside here。 The 3 and the 5 have been switched。

 So we have now 5 columns-- 5 rows and 3 columns。 And basically， we are just switching the 2。

 So it's doing this operation--， the transpose operation in mathematics。

 So instead of working with random data， we can also generate data that has some structure。

 So for instance， if we want to create a single 1D array， with value between 0 and 12， and we。

 want 5 values between 0 and 12 with a fixed interval， we can use that。

 So you see that the first one is 0， the last one is 12。

 and then we have 5 values and they are equally spaced。

 It's also possible to turn a one-dimensional array， which， will generally treat as a vector--。

 as a row vector-- into a column vector， by adding a new axis and taking the values。



![](img/c04d678b99df1406ae3dbf232bf3d810_145.png)

 as the column like this。

![](img/c04d678b99df1406ae3dbf232bf3d810_147.png)

 So if we do this NP new axis， basically， it's some kind of marker that will reshape the data。



![](img/c04d678b99df1406ae3dbf232bf3d810_149.png)

 automatically to introduce a new axis in the array。 And by default， the value is 1。

 So we have one column like this。 So it's a bit weird， but it's very useful。

 because for machine learning and scikit-learn， the input features are always two-dimensional arrays。



![](img/c04d678b99df1406ae3dbf232bf3d810_151.png)

 Even if you have a single feature， we will use that to put that as a column so that we know。

 that the model knows that it's to be treated like a feature， and not a single sample， basically。

 So we can also use that to generate the data again。 And so as previously， I've demonstrated。

 that you can use a shape to access the shape attribute。 It's also possible to do a reshape。

 And as long as the new values match--。

![](img/c04d678b99df1406ae3dbf232bf3d810_153.png)

 the product of the new values might match， the product of the older sizes。

 then you can reshape the array。 But if you compare this to what we did with the transpose--。

 so if I go back here， here you see transpose。 The first is 0。69。 But then the second is also 0。43。

 And then 0。28。6 here。 So remember that pattern。 If I go here， you see that they are not。

 following the same pattern。 Because basically here， when we reshape here。

 and we are not transposing， we are just， rearranging the data into a new structure。

 But the order has been preserved， compared to all the values taken in the original order。

 So maybe it's a bit weird。 I can give you another example， price A。 So if I do n pay， that range。

 for instance， of 12--， so this is just an integer array with values between 0 and 11。 So 12 values。

 that increment。 So 12 is 3 times 4， for instance。 So I can reshape this as 3 times 4。 And basically。

 I will have three rows and four columns。 It's the same data that arranged as a two-dimensional array。

 I can also arrange it as four rows with three columns。 It's also possible to do that。

 And you see that the order is always the same。 Start 0， 1， 2， 3， 4， 5， 6， 7， 8。

 So reshaping is just creating a new view on the same data。

 But the internal ordering of the data stays the same。 It's not a transposition operation。

 You see that the order is always the same。 Finally， it's also possible to do what。

 we call fancy indexing。 So it's basically we use an empire array with integer values。

 to index another array。 So let me print a x just before。 So here， we are going to use 3， 1。

 0 to index on the columns。

![](img/c04d678b99df1406ae3dbf232bf3d810_155.png)

 This is the second axis。 So this is the columns。 So we are going to take the column number 3， 0， 1。

 2， 3。 First， this column here， here。 Then the column number 1， then the number column 0。

 in that order， and we are going to extract a copy of x。

 with those columns and ignore the other columns。 So you see。

 the first here is the third column here。 It's the fourth column because we started 0。



![](img/c04d678b99df1406ae3dbf232bf3d810_157.png)

 It's column number 3。 It's taking the first column in the output。

 And this column is taking the second column。 And then the first column is taking as the third column here。

 OK。 And here we have 3， 1， 0 because we printed it here。



![](img/c04d678b99df1406ae3dbf232bf3d810_159.png)

 Maybe I can remove it。 It's going to be easier to see。 OK。 So when we do that。

 we make a memory copy。 When we do a reshape， it's just a new view on the same data。

 And here we are forced to make a memory copy， because we are completely rearranging the data。



![](img/c04d678b99df1406ae3dbf232bf3d810_161.png)

 You have questions on this？ Yeah。 Why would you have a reshape your data？ What are the applications？

 Reshaping the data can be useful， for instance， if you have a three-dimensional array of images。



![](img/c04d678b99df1406ae3dbf232bf3d810_163.png)

 a set of images， and each of the images， have a height and width as three different dimensions。

 Sometimes you want to access the pixel values as a vector。

 and you don't care about the location of the pixels anymore。 So if you have images of 8 by 8。

 if you have 42 images。

![](img/c04d678b99df1406ae3dbf232bf3d810_165.png)

 and they are--， sorry， I should take this。 So if you have an array and they are gray-level images。



![](img/c04d678b99df1406ae3dbf232bf3d810_167.png)

 there are no colors。 You can have 42 images and a height of 8 pixels。



![](img/c04d678b99df1406ae3dbf232bf3d810_169.png)

 and width of 8 pixels。 You can also treat those as a two-dimensional array。

 with 64 pixel values for each of the images， and you don't care about the specific location。

 And for our sake-it-learn， most of the machine learning， algorithm。

 they need this kind of 2D data structure。

![](img/c04d678b99df1406ae3dbf232bf3d810_171.png)

 They cannot work naturally on images， for instance。

 So you need to find some 2D representation of the data， and the most natural way to do that。

 would be to just do reshape。 Sometimes it's a bad idea to do it， but it can only application。

 [INAUDIBLE]， Yeah， so if you have the data stored like this， you can reshape it like this。

 and then you， can pass it that to Matplotlib。 And Matplotlib will recognize that this is an image。

 and make it possible to display it。 There is another type of array。 Yes？ Sorry。

 So you had to make memory copy that because you arranged the array， but you didn't change it。 No。

 yeah。 X is still the same。 If I execute this cell again， it's still the same。



![](img/c04d678b99df1406ae3dbf232bf3d810_173.png)

 And if I modify， for instance， I can copy that into Y， store the result into a variable name Y。

 I will display Y here。 I can change the values in Y。 For instance， 0， 0 equals 0。 I will display Y。

 So you see that now Y is 0 here。 If I look at X， there are no zeros anywhere。

 So X has not been modified。 Because when you do fancy indexing， you're forced to make a copy。

 basically。 Most of the time， Numpy will not make any copy when it's。

 not necessary to avoid using too much memory。 If you want to make a copy explicitly。

 it's possible to do， for instance， here， I can define a variable Z， which。



![](img/c04d678b99df1406ae3dbf232bf3d810_175.png)

 is a copy of X。 And then you can modify Z without modifying X。



![](img/c04d678b99df1406ae3dbf232bf3d810_177.png)

 So it's also possible to make a copy explicitly， sometimes useful。



![](img/c04d678b99df1406ae3dbf232bf3d810_179.png)

 When you do fancy indexing， it's making just a copy， of the fragment of the data that is indexed。

 And otherwise， Numpy tries to not make any copy。

![](img/c04d678b99df1406ae3dbf232bf3d810_181.png)

 if it's not necessary。 And when you reshape， it doesn't make a copy。 If you slice also， previously。

 we， used the slice notation， for instance， here。 Here， it's not a copy。

 It's just a view on the original data。 So it's not allocating any new memory。 So slicing， reshaping。

 they create， views and fancy indexing that makes a copy。



![](img/c04d678b99df1406ae3dbf232bf3d810_183.png)

 OK， no more questions？ Yes？ [INAUDIBLE]， So you could use a list of integer to do fancy indexing。

 And Numpy will basically convert the list into an array， implicitly。

 So there is another data structure， that you use fully， especially for machine learning， which。



![](img/c04d678b99df1406ae3dbf232bf3d810_185.png)

 is called as passmatrix。 And Numpy does not support sparse arrays by default。

 Maybe that's going to change in the future， but so far it's not the case。

 So to have a sparse data structure for two-dimensional arrays， we can use Sipy's passmatrices。

 So metrics is a two-dimensional array。

![](img/c04d678b99df1406ae3dbf232bf3d810_187.png)

 There are numpy matrices， but they are a bit weird， and they are not sparse anyway。

 So most of the time， I would advise， you to not use the numpy matrices。

 but just using the numpy arrays。 But for historical reasons， the sparse data structure， in Sipy。

 they are only for two-dimensional arrays， and they are called matrices。

 So let's create a numpy array with random values， like we did previously。 So this time。

 we have 10 rows and five columns， with values between 0 and 1。

 What we can do is use this notation here， to put some zeros to the small values。



![](img/c04d678b99df1406ae3dbf232bf3d810_189.png)

 So if the value in x is lower than 0。7。

![](img/c04d678b99df1406ae3dbf232bf3d810_191.png)

 anywhere it's lower than 0。7， we will put a zero in it。 So if I do that。

 you see that only the big values， have been kept and all the others are replaced， by a zero value。

 If you do that， in numpy， you will still store， all the values that are zero。

 and that might be very costly on large data structures。 So for instance。

 here the data size can do n bytes。 It's 400 bytes， so it's very small。

 but we are storing all the zero values in memory。

![](img/c04d678b99df1406ae3dbf232bf3d810_193.png)

 To avoid this， what we can use is to import。

![](img/c04d678b99df1406ae3dbf232bf3d810_195.png)

 the sparse module from Sipy， and to use the CSR compressed pass-through matrix。

 data structure from Sipy to convert the x array， into a sparse matrix。 And if we do that。

 if you print it using print， you see that basically internally what it does。

 it's stored the locations of the non-zero values， and their values。

 And so if you have very few non-zero values， it's much more efficient to just all the location。



![](img/c04d678b99df1406ae3dbf232bf3d810_197.png)

 of the values plus the value that's just storing the values。

 in a bigger memory chunk with the right locations。



![](img/c04d678b99df1406ae3dbf232bf3d810_199.png)

 You can always convert a sparse matrix back， to a numpy array by using two array。

 but be very careful if you do that， because whenever we use a sparse matrices。

 in scikit-learn for real applications， the array might not fit in memory。

 Even if the sparse matrix fits in memory， the numpy array might not fit in memory。

 So you can do that on toy data set for debugging， but never do that on real data。

 because otherwise you will shut down your computer， basically。 It will be very slow and then crash。

 Sometimes you get an error before， but it can be a verb or a metric。

 So to create a sparse matrix in real applications， you cannot create the numpy array first。

 because it's too big。 So what we do is that we can use a little matrix listing list。

 and with this sparse data structure。

![](img/c04d678b99df1406ae3dbf232bf3d810_201.png)

 it's possible to modify it， to add new element， like random values here in the loop。

 very efficiently。 So a little matrix is very efficient， to append new values in it。 However。

 it's not very efficient， to do a linear algebra operation on little metrics。

 So what we want to do most of the time， so you can convert it back to an array。

 If you need to do a machine learning， for instance， on a linear matrix。

 what you would do is convert it， to a compressed parse row， or compressed parse column， CSC or CSR。

 And some algorithms， they are very efficient with CSR。 And other columns， they work column wise。

 like random for instance， and they would be much more efficient， with CSC data structures。

 So we would use either a little matrices， or CO matrices， it's another kind of matrix。

 to create the data from reading some values， from a file or a sensor or something like that。

 and append that into the data structure， and then convert it to a CSR。

 CSC to do the actual mathematical operation， linear algebra operation。 So for sparse matrices。

 there are many representations， and each of them has a straight off。 CSR and CSC。

 they are very efficient for linear algebra。

![](img/c04d678b99df1406ae3dbf232bf3d810_203.png)

 Little and CO， they are efficient for building， the matrix from another representation。

 And diagonal is only four diagonal matrices， and I don't remember what are the drawers of the others。

 In practice in scikit-learn， most of the model in scikit-learn。

 they are efficient if you have these representations。 So finally， we also want to use matplotlib。



![](img/c04d678b99df1406ae3dbf232bf3d810_205.png)

 So matplotlib is a graphical plotting library， for data， typical in an empire is。 So first。

 we connect matplotlib to the notebook， so that when we use matplotlib。



![](img/c04d678b99df1406ae3dbf232bf3d810_207.png)

 we will not create new windows for how to display the results。

 but it will include the result directly。

![](img/c04d678b99df1406ae3dbf232bf3d810_209.png)

 to the Jupyter notebook， so you can use matplotlib inline。 Then there is a convention to import。

 the pipe plot sub-module of matplotlib as PLT， which is basically the main entry point。

 from an API point of view to define， interactively a plot in a notebook。



![](img/c04d678b99df1406ae3dbf232bf3d810_211.png)

 So you can use PLT。plot that takes X value， X array and a Y value。

 So X is gonna be values between 0 and 10。

![](img/c04d678b99df1406ae3dbf232bf3d810_213.png)

 and 100 intermediate steps and 4G。 Each of those values we will compute。

 the sign function at each of those locations， and we get this。

 So this is the input and this is the output of X， and Y here basically。

 And so you see that it's very smooth， because matplotlib is doing some kind of interpolation。

 but if I do less steps， you see that， then we see the actual values。 If I put many more。

 it still works。 Also， there is this specific semicolon here。



![](img/c04d678b99df1406ae3dbf232bf3d810_215.png)

 If I remove it， you see this， which is ugly。

![](img/c04d678b99df1406ae3dbf232bf3d810_217.png)

 because basically matplotlib PLT plot， return a plot object， the lines to the object。



![](img/c04d678b99df1406ae3dbf232bf3d810_219.png)

 In a list， a Jupyter notebook will always print。

![](img/c04d678b99df1406ae3dbf232bf3d810_221.png)

 in the output section， the last object that you have。



![](img/c04d678b99df1406ae3dbf232bf3d810_223.png)

 So if you want to silence this， you can use the semicolon。

 And basically that will return none instead。

![](img/c04d678b99df1406ae3dbf232bf3d810_225.png)

 and none is not displayed。 It's just a trick to avoid this noisy output。



![](img/c04d678b99df1406ae3dbf232bf3d810_227.png)

 Okay， so if you have data， you can also do a scatter plot。



![](img/c04d678b99df1406ae3dbf232bf3d810_229.png)

 So here we have two arrays， they have the same size。



![](img/c04d678b99df1406ae3dbf232bf3d810_231.png)

![](img/c04d678b99df1406ae3dbf232bf3d810_232.png)

 and we will put on the x axis， the first array， and y axis， the second array。



![](img/c04d678b99df1406ae3dbf232bf3d810_234.png)

 And then for each of those combinations， we will get a dot， and this is what we call a scatter plot。



![](img/c04d678b99df1406ae3dbf232bf3d810_236.png)

 So those are Gaussian distributed values。 They are sampled independently of one another。



![](img/c04d678b99df1406ae3dbf232bf3d810_238.png)

 So you can treat the pair of the two values， as a multivide Gaussian with a spherical coherence matrix。



![](img/c04d678b99df1406ae3dbf232bf3d810_240.png)

 If you like mathematics。

![](img/c04d678b99df1406ae3dbf232bf3d810_242.png)

 This is a scatter plot。 So the scatter plot is very useful to display data。



![](img/c04d678b99df1406ae3dbf232bf3d810_244.png)

 if you have two dimensional data。 You can also display histograms。



![](img/c04d678b99df1406ae3dbf232bf3d810_246.png)

 For instance， we just have x。 Sorry， I did not meant to do that。



![](img/c04d678b99df1406ae3dbf232bf3d810_248.png)

 So let's press B here， and I can do PLT， that is of x and maybe beans equals 50。

 So here you see that it outputs a ton of non-interesting stuff， and then the actual value。

 the actual graphical representation。 So here we'll use a semicolon to get rid of that。

 And here you have a one dimensional distribution of the data。

 empirical distribution of the data using a histogram。

 So typically we use a histogram for one dimensional data， and scatter plot for two dimensional data。

 And if you have n dimensional data， you need some kind of dimension integer reduction。



![](img/c04d678b99df1406ae3dbf232bf3d810_250.png)

 to be able to do a scatter plot。 Okay， finally， it's also possible to use PLT in show。

 if you have two dimensional data with the continuous values。 So for instance。

 here we have x that vary between one and 12， and with many intermediate steps。

 Why would we convert x into a column vector？ And then if we do this kind of operation。

 NumPy will do what we call broadcasting， and will generate a two dimensional array。

 And the values of each of those locations， is gonna be dependent on x and y。



![](img/c04d678b99df1406ae3dbf232bf3d810_252.png)

 And it's gonna be a two dimensional array。 If I press this， you can see that it's 100 by 100。



![](img/c04d678b99df1406ae3dbf232bf3d810_254.png)

 And if I use impshow， I see the value using some column up， which is very this by default。

 So basically， I think yellow is high and blue is very low。



![](img/c04d678b99df1406ae3dbf232bf3d810_256.png)

 And it's also possible to use a contour plot， to do the same kind of representation but using lines。

 And there is a convention that zero here， is at the top left corner。

 where here it's at the bottom left， corner。 So it's a transpose representation。

 but it's basically the same same kind of representation。



![](img/c04d678b99df1406ae3dbf232bf3d810_258.png)

 But here you have continuous colors and here you have lines。 So so possible to do contour F。

 I guess， and to get this kind of representation， contour contour F。 Okay。



![](img/c04d678b99df1406ae3dbf232bf3d810_260.png)

 Finally， Matt Plakly， but also the ability。

![](img/c04d678b99df1406ae3dbf232bf3d810_262.png)

 to do some simple 3D plotting。 It might be useful for impressing people， on a PowerPoint slide。

 In practice， I think it's useless， and this kind of 2D representation is better。 Did you have。

 you actually see the data better？ If you really want to do 3D volumic representation。

 you might need other libraries like Maya V， for instance。 Okay。

 so I think that's it for this introduction， to the tools that we're gonna use for machine learning。

 So the dependencies of Scikit-Lan basically。 Okay， so now we'll switch to the ferna books。

 And I think that then we'll have a break， probably。 (mumbling)。

 So we'll stop for around 10 for the break。

![](img/c04d678b99df1406ae3dbf232bf3d810_264.png)

 So this one， again， records bits how we organize and represent our data。 So。

 and we will go back to the first example， which is the iris data set。 Okay。

 so we already explained that each line， will be a sample， so in this case it will be a flower。

 And then for each of the line， we will get the feature。



![](img/c04d678b99df1406ae3dbf232bf3d810_266.png)

 So， for instance， the height of the petals， the width of the petal。

 and then the same for the sample。 So we'll have 150 lines， which will be， for instance。

 150 flowers and four features， which will be the feature that we extracted by hands。



![](img/c04d678b99df1406ae3dbf232bf3d810_268.png)

 that the biologist got。 So， the descriptions were really， saw the beautiful flower before。



![](img/c04d678b99df1406ae3dbf232bf3d810_270.png)

 And we already saw how we were basically。

![](img/c04d678b99df1406ae3dbf232bf3d810_272.png)

 organizing our data。 Yeah， the question is already the one that we， since half an hour， so is。

 how do you represent the data， what is and sample and features？



![](img/c04d678b99df1406ae3dbf232bf3d810_274.png)

 I think that now we more or less know。 So I will go directly on how do we basically load。

 this data set into cycle and so this data set， is one of the cyclone。

 which is embed in side cyclone。 And we are using for benchmarking or training some algorithms。

 And this is based into this module， which is a scale on data sets。



![](img/c04d678b99df1406ae3dbf232bf3d810_276.png)

 And from that， we have a load iris， which basically will return us the full data sets。

 So if we execute this part and that we check， so iris， iris will be basically a bunch。

 which is a dictionary kind of type of objects。 And we can check the keys and we'll see that。

 basically we have the data that should correspond， to our matrix X。

 we'll see later how many features， and how many samples。 We'll have the targets。

 which will be our classes。 And then we'll have the target names， because in cyclone。

 we only handle numerical data， but in this case， we don't have numerical data。

 we have the name of flowers。 So we have a connection between an integrals， and the flowers name。



![](img/c04d678b99df1406ae3dbf232bf3d810_278.png)

 And then we have some extra thing， which are the descriptions of the data sets。

 So seeing that we have like zero data set， we want also to explain where they come from。

 what they contain and extra information。

![](img/c04d678b99df1406ae3dbf232bf3d810_280.png)

 So the first thing that we can do is。

![](img/c04d678b99df1406ae3dbf232bf3d810_282.png)

 from the iris， we can get the data。

![](img/c04d678b99df1406ae3dbf232bf3d810_284.png)

 and check the size of the matrix。 So if we execute this， then the first column， sorry。

 the number of rows will correspond， to the number of samples and the number of current。

 will correspond to the number of features。

![](img/c04d678b99df1406ae3dbf232bf3d810_286.png)

 And what we can check is that we have 100， 50 flowers， with four different features。

 And if we just display the first row， we obtain basically our four numbers of four features。



![](img/c04d678b99df1406ae3dbf232bf3d810_288.png)

 Now we can also check what's the relationship。

![](img/c04d678b99df1406ae3dbf232bf3d810_290.png)

![](img/c04d678b99df1406ae3dbf232bf3d810_291.png)

 between our data and our target。 And we see that in the first case。



![](img/c04d678b99df1406ae3dbf232bf3d810_293.png)

 we add 150 samples by four features。

![](img/c04d678b99df1406ae3dbf232bf3d810_295.png)

 and in the second case， we have one class， for each flowers。 We can either print it and we'll see。



![](img/c04d678b99df1406ae3dbf232bf3d810_297.png)

 that actually there are numerical data， and there are not the name of the flowers。

 And that's why we have a target name here， which will make the correspondences between zero。

 and the name of the flower if we want to have， something nicer for the user if we want to display。

 okay？

![](img/c04d678b99df1406ae3dbf232bf3d810_299.png)

 - So just precision。 So here we see that we are using integers， not floating point values。

 So this is very important because in scikit-learn， if we give as a target an integer。

 it's interpreted as a classification problem， most of the time。 And if it's a floating point value。

 it's a regression， a continuous variable。

![](img/c04d678b99df1406ae3dbf232bf3d810_301.png)

 - Yeah， so it's a convention。 It's not always the case sometimes。



![](img/c04d678b99df1406ae3dbf232bf3d810_303.png)

 you can use integers for regression， but for classification， you cannot give， floating point values。

 you should give integers。

![](img/c04d678b99df1406ae3dbf232bf3d810_305.png)

 as the target values。 And what it means that if you can print the target again。



![](img/c04d678b99df1406ae3dbf232bf3d810_307.png)

 is that， so here is the first species。

![](img/c04d678b99df1406ae3dbf232bf3d810_309.png)

 this is the second species and this is the third species。

 And there is no meaning in the absolute values， of those numbers， like it doesn't mean。

 that this species is closer to this one than this one。

 You cannot compute the difference between the species， by computing the difference of those numbers。



![](img/c04d678b99df1406ae3dbf232bf3d810_311.png)

 They are just indicator values， categorical variables。 - Yeah， and we'll see later also that's。



![](img/c04d678b99df1406ae3dbf232bf3d810_313.png)

 I mean， this something that you have to take care， when you process categorical variables。

 So what we can do here is to try to find out， how many of the first class do we have of the class zero。

 how many of the flower of the class one do we have。



![](img/c04d678b99df1406ae3dbf232bf3d810_315.png)

 by using bean cons。 So we can use them by uncalled bean cons。

 And then we'll see that we will have 50 zeros， 51 and 52。 So we have a balanced data set in the way。

 that we have the same number for each species。

![](img/c04d678b99df1406ae3dbf232bf3d810_317.png)

 So do you have any question on that？ Yeah？

![](img/c04d678b99df1406ae3dbf232bf3d810_319.png)

 Okay。 So here， so is what I was explaining。 The class zero will actually correspond to the setosa。

 the one to the versicolors and the two to the versionica。 And how can we find this relationship。

 is by printing the target names。

![](img/c04d678b99df1406ae3dbf232bf3d810_321.png)

 And now we can zero find the relationship。

![](img/c04d678b99df1406ae3dbf232bf3d810_323.png)

 So the first thing that we can do is to plot。

![](img/c04d678b99df1406ae3dbf232bf3d810_325.png)

![](img/c04d678b99df1406ae3dbf232bf3d810_326.png)

 the distributions of one of the feature。

![](img/c04d678b99df1406ae3dbf232bf3d810_328.png)

 So for instance， we selected the petal widths。

![](img/c04d678b99df1406ae3dbf232bf3d810_330.png)

 which is a feature which is here。

![](img/c04d678b99df1406ae3dbf232bf3d810_332.png)

 We took the feature number three。

![](img/c04d678b99df1406ae3dbf232bf3d810_334.png)

 So we took only the third column。 And then we just took the third column。



![](img/c04d678b99df1406ae3dbf232bf3d810_336.png)

 and then we plot the Easterram for each classes。

![](img/c04d678b99df1406ae3dbf232bf3d810_338.png)

 So we took the setosa and we plot the Easterram， which is in blue。 We took then the versicolors。

 which is orange， and then we plot for the green one。 So by just looking at this。

 we can already investigate。 For instance， if we can easily distinguish。



![](img/c04d678b99df1406ae3dbf232bf3d810_340.png)

 one class compared to others。 Okay？ In the same way， already Olivier spoke about this Easterram。



![](img/c04d678b99df1406ae3dbf232bf3d810_342.png)

 and then he was also speaking about the scatter plots， where we can actually visualize 2D。

 So we can go a bit further by only not only plotting， one single feature， but two features。 Okay？

 So to do that， we can put a feature on the x-axis。

 a feature on the y-axis and do the same scatter plotting。 And in that case， for instance。

 we selected， so for the y-axis， we took the first features， for the x-axis。

 we took the last features。 So it's better to name them。 So we took the Cepal length for the y-axis。

 and the petal width for the single axis。 And then we plotted each individual。

 each individual features values。 Okay？ - So can you show how we get the feature names in the code？



![](img/c04d678b99df1406ae3dbf232bf3d810_344.png)

 - Yeah， so the features names is easier。 So we get the index zeros。



![](img/c04d678b99df1406ae3dbf232bf3d810_346.png)

 and then we take the list， which contains the feature names， and we take the corresponding name。



![](img/c04d678b99df1406ae3dbf232bf3d810_348.png)

 Okay？ And then we get how plots。 So for instance， here we can already find out。

 that using only these two features。

![](img/c04d678b99df1406ae3dbf232bf3d810_350.png)

 we will be able with a symbol line， to precisely classify the blue。

 which is the Cetosa flowers compared to others。 And here it will be a bit more noisy。

 to make the selection。 Okay？ So just by visual accru。 So now the other size is just to pre-run with。

 I mean， you can pre-run with the index of x and y， and to see which representations。



![](img/c04d678b99df1406ae3dbf232bf3d810_352.png)

 is actually the best one to try to distinguish the three classes。 Okay？

 So here what we are trying to do is to go from four dimensions。



![](img/c04d678b99df1406ae3dbf232bf3d810_354.png)

 to actually two dimensions to try to simplify our program。 So is what we say here。

 so that's the kind of exercise of dimension redictions already。 So we already spoke about it。

 Here we do it by hand， and then we'll say see over techniques to do that。



![](img/c04d678b99df1406ae3dbf232bf3d810_356.png)

 So you can try to pre-run， and find the best combination of those。



![](img/c04d678b99df1406ae3dbf232bf3d810_358.png)

 - So the goal is to find a graphical representation， when you can draw a straight line。

 that will perfectly separate the different groups。



![](img/c04d678b99df1406ae3dbf232bf3d810_360.png)

 Here we cannot draw a line to separate the versicolor， from the virginica。



![](img/c04d678b99df1406ae3dbf232bf3d810_362.png)

 but you can see that it's very easy just using the petal widths。

 to separate the cetos from the two others。

![](img/c04d678b99df1406ae3dbf232bf3d810_364.png)

 So let's try a good representation。

![](img/c04d678b99df1406ae3dbf232bf3d810_366.png)

 - Two and two。 - Two and two。 (audience laughs)， Maybe one feature is enough。

 Actually there is probably some overlap。 So what we could do is。



![](img/c04d678b99df1406ae3dbf232bf3d810_368.png)

 yeah， there is some overlap here。 So it's actually， we cannot see it。



![](img/c04d678b99df1406ae3dbf232bf3d810_370.png)

 but there are some bad classification here。 - Because you got it one point or another point。

 so you don't see it。 - Okay， so no perfect classification。 It's actually。

 maybe it's not possible to find only two features， to completely separate the species。

 and you actually need the four features， and we cannot just represent them in two dimensions。

 But you can see that there are some combinations， that are better than others。 - Okay。

 so do you have any question on generic stuff？ Okay， so one of the scatter plot。

 which you can use to see those interactions， is actually in pandas。

 So it's a side of the side of the pipeline。

![](img/c04d678b99df1406ae3dbf232bf3d810_372.png)

 but basically they have this scatter matrix， where you can， so you can create a data frame。

 putting the data and the eye-conting， I mean， to have the name of the features。

 you give the feature names。 And then you can plot these matrices， which I think we'll use C-born。

 probably on those wood。 And we'll show you basically all the interaction。

 of what we're trying by hand now。 So that's the uni-innovariate histogram。



![](img/c04d678b99df1406ae3dbf232bf3d810_374.png)

 Okay， so it's like the isram of the first feature， the isram of the second feature。

 third and fourth。

![](img/c04d678b99df1406ae3dbf232bf3d810_376.png)

 And then here this is scatter plot that we are doing。 So the first column with the second features。

 et cetera， et cetera。 So only by looking at this one， we were， I mean， it's what we're trying。



![](img/c04d678b99df1406ae3dbf232bf3d810_378.png)

 by just moving the indexes。 So if you have a reasonable number of features， not so much data。

 because then after that you just see， like a lot of points。

 you can maybe look at those type of visualizations， that can be helpful， okay？

 So what do we have in Saikit-learn。

![](img/c04d678b99df1406ae3dbf232bf3d810_380.png)

 to actually play with data？ So we have two type of， I mean， three type of things。

 So we saw right now the load function。 So usually we have a couple of very small datasets。

 which are embedded inside the package， and you can use and start with load。

 While we have much bigger datasets， that you can like， which are， for instance。

 much more time-consuming and useful benchmark， which are with fetch。

 So we'll first need to fetch the data from internet。 They are not included inside the package。



![](img/c04d678b99df1406ae3dbf232bf3d810_382.png)

 And then the last one is simulated data。

![](img/c04d678b99df1406ae3dbf232bf3d810_384.png)

 So we generate the data， and usually they start with the make。 So for instance。

 make blocks and stuff like that， or make lessifications。 So as explained here。

 you can already try by yourself， so you can import from a scalar import datasets。

 and then use the auto-completions to see what you have。



![](img/c04d678b99df1406ae3dbf232bf3d810_386.png)

 So that's a set dot load。

![](img/c04d678b99df1406ae3dbf232bf3d810_388.png)

 and then we'll see that we have different things。 So we have things specifically for our regressions。

 or for classifications。

![](img/c04d678b99df1406ae3dbf232bf3d810_390.png)

 And like this you can play with some modern standards。

 and understand how this is working or the specificities， okay？ And the same。

 you can check the fetch， and you will see a couple of like， those one will need to be downloaded。

 okay？

![](img/c04d678b99df1406ae3dbf232bf3d810_392.png)

 Yeah， so be careful because some of the datasets， are kind of large and if you might need like 200 megabytes。

 just to unload it。 And if you work with text， the fetch news groups are， for instance。

 already the fetch news group is quite large， and that's why we propose some like already pre-processed data。

 sometimes。 So you have to check the documentation， to know which one are the pre-processed。

 if you want only to work on the second part。

![](img/c04d678b99df1406ae3dbf232bf3d810_394.png)

 and the classifications。 So right now what we'll do is that we'll--， - Just a note。

 So all those datasets， they are only provided， for debugging machine learning algorithms。

 like to try and evaluate machine learning algorithm。

 on some standard dataset that are used in the literature， so that you can compare。

 that you can reproduce the results， by comparing the accuracy on some standard dataset。

 Most of the time you want to work on your own personal data， and in that case those are useless。

 You don't need to fetch anything。 There is only one function that may be interesting。



![](img/c04d678b99df1406ae3dbf232bf3d810_396.png)

 For instance， datasets。loadSVM_LIGHT， loadSVM_LIGHT file。

 So this SVM_LIGHT file format is used by some people。



![](img/c04d678b99df1406ae3dbf232bf3d810_398.png)

![](img/c04d678b99df1406ae3dbf232bf3d810_399.png)

 to pass around some data as a text file format， and this is a parser for that file format。

 that can be used in the machine learning community。



![](img/c04d678b99df1406ae3dbf232bf3d810_401.png)

 So it can be used on your own data， but most of other applications typically。

 what you would do is find a way to query your database， using a， I don't know， a SQL connector。

 like SQL RKME for instance， run a query， extract the data， convert it into an empire array。

 the way you want or maybe extract that as a CSV file， and you spend as to read the CSV。

 and convert it into an empire array。

![](img/c04d678b99df1406ae3dbf232bf3d810_403.png)

 or pass the data frame directly to scikit long。 - And you have a lot of files。

 so which does something like--， - Yeah。 - You can-- - That's a。

 and so my point is that if you want to work， on your own data， you just need to find a way。

 to load your data into an empire arrays， or append as data frame and that's it。



![](img/c04d678b99df1406ae3dbf232bf3d810_405.png)

 You don't need to use any of this， you don't need to bunch object or whatever。

 You just need an X and a Y， that are in empire arrays， all data frames。 - Okay。

 So now we'll work with a second datasets to see， so this one will be interesting。

 because it's about images， so we have the program that Olivier mentioned here。

 with vectors and how do we handle images， when we want to make classifications。

 And this is called digits， so it's a smaller dataset than MNIST， I think。

 And it corresponds to actually numbers written by hands， of size eight by eight pixels。

 and the task will be to classify and written image， to find the number which is written on it。 Okay。

 So here the dataset is loss digits， so we can load it exactly the same way。

 that we did for the iris datasets。 And then we can check what are the keys。

 and we have exactly the same like information size， so data targets， the target name。

 And we have an additional one which is images。 And this is because data。

 will be the vectorized versions。 So we have one line per image and 64 features。

 while that images will be number by image， by the width。 Okay， so if we take the first image。

 then we can already plot the image or show the image。 So if we show the data。

 so we have one type of image， the data， so we have 1，797 images with 64 features。

 And if we plot the first line。

![](img/c04d678b99df1406ae3dbf232bf3d810_407.png)

 we see that we have integral between zero and 16。 Okay。 And that the target is corresponding。

 to a number between zero and nine。

![](img/c04d678b99df1406ae3dbf232bf3d810_409.png)

 Okay。

![](img/c04d678b99df1406ae3dbf232bf3d810_411.png)

 So here is what I was explaining。

![](img/c04d678b99df1406ae3dbf232bf3d810_413.png)

 so that's the difference between the data and the images。 So one is the vectorized versions。

 and the other one is actually the real images。 So if I take the first sample here。

 if I slice over the first dimension， I will get eight by eight metrics， which represent an image。

 (mouse clicking)， So， and how to get from one to another。 So it was the trick of the reshaping。

 so that you can use the reshape， and then you can get from data to images， or from images to data。

 Okay。 So now the more interesting things is to actually， plot those data。

 So here we will try to plot each image。 So if we check， we have EM show， okay。

 And we'll get an image， so which correspond to an index。 So here the index is 64。

 So basically we have a matrix here of eight image， by eight image。 And we will just show the image。

 which is between zero and the 64th image。 And then we will just have a chroma app in grayscale。

 okay。 And we've been to operations just to show。 And then we will add a text on the bottom left。

 which will correspond to the target。 So what you see here is actually the real data。

 And here this is the target， which is associated， okay。 So that's just to show。

 You can see that this is very low resolution images， eight by eight pixels。 And for instance。

 this one is kind of hard to tell。 So you can expect that even if even human beings。

 have trouble like classifying this one or this one。

 maybe the model won't be able to make perfect classification， either， so。 Okay。

 so now the exercise will be to try to load another dataset， which is about faces， okay。

 So it's useful either face recognition， I think。 And basically do the exercise by loading the data。

 So you will need to and plotting it basically。 So you have a couple of minutes to play around。

 load the data， fetch the data。 So it is a small package， so it's one at five megabytes。

 So it should be okay。 And then just plots using EM show or with another color map。

 So similarly to what we did before， okay。 Do you have any questions in the meanwhile？ - Okay。

 - How do you use the loading of a library data service？ - I will go in check。 (indistinct chatter)。

 (indistinct chatter)， - Okay， so some of you had problems downloading this。



![](img/c04d678b99df1406ae3dbf232bf3d810_415.png)

![](img/c04d678b99df1406ae3dbf232bf3d810_416.png)

 You had SSL errors or stuff like that。 It might be cause because you have a HTTP proxy。

 on your corporate laptops， and you need to set up， an environment viable。

 which is kind of complicated。

![](img/c04d678b99df1406ae3dbf232bf3d810_418.png)

 to get right。 So for this exercise， just follow on the screen。 But for the next ones。

 we will need to make sure， that you could execute the Python fetch data。py stuff。 So if you haven't。

 and you cannot do， because of proxy configuration issues。

 use a USB key and try to download the notebook/data sets。

 up folder and zip it in the right location， on your own folder。 So it's under notebooks/data sets。

 okay。 From someone else。 - Okay， so before to check the solution。

 anybody have any question on what to try or no？ - Okay。

 so small tips because we didn't see up to now。 So when you have a solution usually in notebooks。

 you have something that's say like a commands， and then percentage load。

 And this is actually loading the content of the file， which is in that locations in the notebook。

 So for us it's kind of practical， because we can load the solutions and directly play it， okay。

 So for you it's like if you don't know what this line， was meaning， that's the meaning。

 You can just uncomment it， and it will load the solutions， okay。

 So basically the code is really similar than before。

 We have the only difference that we use the fetch。



![](img/c04d678b99df1406ae3dbf232bf3d810_420.png)

 or leave it in phases。

![](img/c04d678b99df1406ae3dbf232bf3d810_422.png)

 So here you can see I already downloaded one， so I didn't have on the computers。



![](img/c04d678b99df1406ae3dbf232bf3d810_424.png)

 So the first time that we executed it， by if it's working， it will download the data sets into。

 so here into a generic folder， which is in a scikit-learn data， in basically the users folder， okay。

 because this is the default locations。 So now if I'm executing again， it will not read on the data。

 because the data already cached， okay。 So that's why you don't like read on load。

 or all the other things。 Then the rest of the code is more as exactly the same， than before。

 So we have faces， which is something， which is if we check the keys will be。

 equivalent to the previous thing that we had before。 So we have the data， we have the images。

 and we have the targets， okay。 So we don't have feature name of a target name。

 because here it was not meaningful。 And then we just create a figures of a given size。



![](img/c04d678b99df1406ae3dbf232bf3d810_426.png)

 so six by six inch， and then we will just make subplots。 And then we will take the 64 first image。

 okay， of the data sets， which we will index here， okay。 So we'll make a loop over the 64 first。

 and just show an image every times， on a grid of eight by eight。 And then we apply a bone column up。

 which is not a great scale， I mean， it's kind of a great scale column up there。

 And then we put an interpolations， if the product is bigger than the size of the image。

 So do you have any question on those？ Or you succeeded？

 So of course here you could plot random images， if you actually。

 instead of creating I between the round 64， you could check random images。

 that could be between zero and the number of image。 And if you wish to see some of the things， okay。

 Okay， so that's all for this notebook。 That's how basically we load data。

 So now we'll pass to the notebook on the trini， and testing data， which is a force not books， okay。

 So I will already set up my per clip and numpy， which is the first time。

 Don't forget to execute it after that doesn't work。 So when we do machine learning。

 we already saw that we have two faces。 So we call it like you have a phase。

 where you learn the models and a phase， where you want to see and to see if your model。

 is generalizing on new data。 So that's a testing phase basically。 And if you want to simulate。

 because basically what you do is that you will have， data sets where you know everything。

 but if you want to simulate the case， that you have a production system。

 you have to simulate the phase that basically， you don't know anything about your target。

 So I should have at the training， I should have all the information， data per target。

 And then when I want to evaluate my models， to know how good my model is， I will just need my data。

 but don't give any information about the targets。 So the training， what we will see here。

 is how to basically split data， such that we do properly these two， I mean。

 we split the data into categories。 Okay， one for the training， the other one for the evaluations。

 So we'll reuse the iris data sets。 Okay， so we already saw before that。

 we can use the data which we will call X， and the target that we'll call Y。

 So if you check the documentation X and Y are， I mean。

 are recall a lot of time in different algorithms。 So X usually we always refer to data。

 Y always refer to targets。 Okay， that's kind of conventions。

 So we can load the data and now we can plot， basically the targets and we'll get our rate。

 that we already saw before。 With 50 zero， 51 and 52。 So if you would like， for instance， you say。

 okay， I don't need to cycle learn， to basically split my data into training and testing。 I mean。

 I can just slice a portion of my data， for my training using slicing with NumPy。

 The problem is that if you are not careful， and that you forget to take care or to look at your data。

 you might have only the zeros into your training， and do not shuffle your data。

 And that's basically what the tools of cycling， are allowed you to do。 I mean。

 they allow you to do a proper splitting， okay？ We've all taken care about those things。

 So the first function that help you for that， is the train test splits。

 And this is in the model selections modules。 So the idea is that you import this function， okay？

 And then you will give you x data， you y data， and then you will say the proportion。

 of training samples that you want。 And then the proportion of testing samples that you want。

 So here we want half of the data， that will go for the training and half of the data。

 that will be in the testing。 And then here we set the random state。

 which is a seed which will first shuffle the data， okay？

 So we'll first shuffle the data and then split half and half。 Okay？ Yep。

 - Does that have to equal one， will you get those two？ - Sorry？ - Does that have to equal one？

 - I'm。 - No， actually， this makes it possible to sub sample。 So it cannot be larger than one。

 because otherwise you would have another lab between training tests。

 But you can also put integers if you want， to have a small training set of just 20 elements。

 for instance， you can put train size equal 20。 If it's lower than one is treated as a refraction。

 if it's larger than one is treated， as an absolute number of samples。 But the two together。

 they have to be less than 100%。 And it will make sure。

 that there is no overlap between training tests。 And if you don't， you can omit train size。

 and just give test size。 And in that case， it gives you the complement， for the training set。

 - Question。 - Yep。 - So yesterday during our TensorFlow session， we split our data in three ways。

 test， validate， train validate and test。 Do we also use similar approach？

 We will work with classic ML algorithms。 - Yes， so what you could do is use。

 train test split several times。 Want to split what we call the development set。

 and the evaluation set。 And then， so where is it？

![](img/c04d678b99df1406ae3dbf232bf3d810_428.png)

 So you can have a full data set where you have everything。 And then you can split some。

 do a first 20 split， to keep something for the final evaluation。

 And we call it to make it more explicit。 We can call it final level。

 And this we can call it development set。 And inside this you can split again。

 a train and a validation set， for instance， or test set。

 It's just that we can do that several times， look at the value of the model and the validation set。

 tweak the model again， or reevaluate the model with the new high parameters。

 and do that several times。 And at the end， once we have found the best model。

 we can finally evaluate it on some things， that we have never seen before。

 The thing is that if you evaluate the model， and change something， you cannot reevaluate。

 with the same validation set or test set， because you use it， you can only use it once。



![](img/c04d678b99df1406ae3dbf232bf3d810_430.png)

 for the final evaluation。 So we will see also this afternoon。

 that you can do cross-validation instead of a single， train validation split。

 When you do deep learning with TensorFlow， and stuff like that， training a model is so costly。

 that you cannot use cross-validation， because it's too compute intensive。

 And so you do a single trace validation split， instead of using cross-validation。



![](img/c04d678b99df1406ae3dbf232bf3d810_432.png)

 But it's basically the same。 Here we could use cross-validation here。

 and use the final evaluation set for the final evaluation。 Okay， so here I will go back to。 Okay。

 no battery， anyway。 So two half and half。 And then we can observe all the data that have been selected。

 So we'll just check the train Y。 So here it's returned four variables。 So the training X。

 so the training data， then the testing data， and then the training target。

 and then the testing targets。 And now we can basically plot， for instance。

 the training Y and we'll see that our labels， just to verify that we are the shuffling。

 Our labeler have been shuffled previous， to basically make the split， okay？

 So that's why it's more powerful than just using NumPy， because we took about the shuffling。

 - Sorry， to refresh this is that if we just use NumPy， to slice in the middle， you would have zero。

 and once in the training set and once and twos in the test set。

 And we would not be able to predict any twos， because in the training set we have never seen twos。

 - So basically you will have this in your training， and your testing will be something like this。

 So you will never train on two and here you will only。

 I mean you will test on two that you never saw before， and by yourself。 - So yeah。

 if you want to be able to predict twos， you need to have seen a couple of examples。

 of the class number two in the training set， otherwise the model will never think about trying to predict two。

 So this is why we need to do some random permutation， before doing the train test split。

 - So here we printed the train labels， and then we see that you have also shuffled。

 the testing labels。 So we have a kind of tip which is stratifying。

 So stratifying mean that when we make the split here。

 we didn't care about the proportion of each class。



![](img/c04d678b99df1406ae3dbf232bf3d810_434.png)

 when we make the split。 So for instance we said that we have 50 level。

 of each classes at the beginning。 So when we make the split we didn't take care。

 about the proportion that we have in the training， and testing if they are equal。

 Because naturally they were equal afterwards， they might not be because of random sampling。

 So we can first take what was the proportions。 So for instance here that's the full dataset。

 So we saw that we have 50 example in each， which represent about 33。3% of the class zero。

 and the second class and the third class。 So this is highly balanced。

 I mean it is completely balanced。 And one that we make our splitting here。

 and that we change the same proportion， we see that we have 30% of the first class。

 40 of the second one and 30 of the third one。 So on the training set we imbalanced our data。

 and having more basically of the second class。 And it's also have an impact on the testing。

 because this is a complementary in the case。 So we have less of the second class。 So it should be。

 I mean if we want to conserved， basically the proportions in training and testing。

 in the same way that we have in the original data。

 we can pass a parameters which is called stratify， and we can give them the target。

 and it will take care about splitting， to have as much as possible the same proportions。

 So if we repeat this and now we can see， that the proportion of all the classes in that case。

 have been respecting in the training and the testing class。 Okay， yep。

 - What if you have severe class imbalance， and a very small sample？

 - Then you might have the corner case， where I mean if you have one samples。



![](img/c04d678b99df1406ae3dbf232bf3d810_436.png)

 I not exactly sure it will fail or not。 - So if you have a one class that for instance。



![](img/c04d678b99df1406ae3dbf232bf3d810_438.png)

 has a single sample then I think it will be automatically， be put in the training set。

 But honestly doing machine learning。

![](img/c04d678b99df1406ae3dbf232bf3d810_440.png)

 with a single example is less so。 But if you have an imbalance data set。

 it will preserve the imbalance。 Like if you have in the full data set。

 if you have like 80% of the first class， and 10 and 10 for instance。

 if we try to preserve as much as possible， 80， 10 and 10， 80， 10 and 10 everywhere。

 - And that and basically that's the best， because in the real life， if this is because of real life。



![](img/c04d678b99df1406ae3dbf232bf3d810_442.png)

 you will exactly get this when you want to train your models。

 So you need to preserve that in new training and the testing。

 And then you have to be sure to use good metric， when you evaluate your models。

 to be sure that basically you will not see wrong。

![](img/c04d678b99df1406ae3dbf232bf3d810_444.png)

 I mean you will not fool yourself。 - Yeah， you want basically the class proportion。



![](img/c04d678b99df1406ae3dbf232bf3d810_446.png)

 in the test set to be the same as the real class proportion。



![](img/c04d678b99df1406ae3dbf232bf3d810_448.png)

 Otherwise you cannot interpret the accuracy， that you get on the test set。

 If the class proportion does not reflect， the actual distribution。



![](img/c04d678b99df1406ae3dbf232bf3d810_450.png)

 Okay， so now we'll train our first models on those data。



![](img/c04d678b99df1406ae3dbf232bf3d810_452.png)

 So we'll use a can-ear's neighbors。 So he's a classifier that will check the neighbors。

 So at sample we check the samples around him， to know which class he is。 Okay。

 so here as Olivia already presented。

![](img/c04d678b99df1406ae3dbf232bf3d810_454.png)

 at all the being we'll use the fit and predict functions。



![](img/c04d678b99df1406ae3dbf232bf3d810_456.png)

 So fits will make the training。 And so what we do is that we create an instance。

 of a can-ear's neighbors。 We fit only on the training part of the data。



![](img/c04d678b99df1406ae3dbf232bf3d810_458.png)

 And then we will predict only on the test parts。

![](img/c04d678b99df1406ae3dbf232bf3d810_460.png)

 And in that case you can see， that we never used test Y at any points。



![](img/c04d678b99df1406ae3dbf232bf3d810_462.png)

 Okay， a part of afterwards when we make the evaluations。 Okay， so we train， we predict。



![](img/c04d678b99df1406ae3dbf232bf3d810_464.png)

 And then here we will check basically the accuracy。 So how many times the testing。



![](img/c04d678b99df1406ae3dbf232bf3d810_466.png)

 and the prediction agree together？ And we make the sum and we divide by the length of Y。



![](img/c04d678b99df1406ae3dbf232bf3d810_468.png)

 And it tells us that we have 96% of right answers。



![](img/c04d678b99df1406ae3dbf232bf3d810_470.png)

 Okay， so it's a fraction of correct answer。 And this score is called， I mean。

 that's the accuracy basically。 So now we can even try to go a bit more in depth。

 by just changing which of the levels， have been correctly classified。 So we can use numpy。

war and we say， okay， when predict Y is equal equal。



![](img/c04d678b99df1406ae3dbf232bf3d810_472.png)

 so agree with the test Y。 And it will give us the list of the indices。



![](img/c04d678b99df1406ae3dbf232bf3d810_474.png)

 of the， of the， that are well classified。 And we can do the same with the indices。

 which are not correctly classified。 So in that case we have three samples。

 which are not well classified。 And as we did before， we could make a 2D scatter plots。

 and choose two axes where we want us to visualize the data， and check which one of those。

 for instance， have not been classified compared to others。 So for instance here。

 we plot our first class， which is a green class or that's a third one。



![](img/c04d678b99df1406ae3dbf232bf3d810_476.png)

 but the three classes of the， of the， of the flower。 And then we， in red， we classified basically。

 the misclassified samples。

![](img/c04d678b99df1406ae3dbf232bf3d810_478.png)

 So now there's an exercise on basically， cutting， I mean， finding the levels of those。

 of those samples and modify basically the discader plots。 Yeah， you have the question before。

 - This is generally the case when it's more difficult。

 for us to characterize samples that are not only。

![](img/c04d678b99df1406ae3dbf232bf3d810_480.png)

 interpreted between the clusters。 - Yeah， in that case， yes。 I mean。

 in that case it will be more linked to the neighbors。

 But it's basically that will be the exercise of， trying to understand why those samples are misclassified。

 - So keep in mind that here we are doing a 2D representation， of a four dimensional space。

 So it might be the case that the cluster， are well separated in four D in high dimension。

 but when we project on two axis， we have some overlap。

 But maybe in the full data set it's not the case。 Here apparently it's also the case or the。

 wise-scale neighbors would not make any mistake。 So。

 - It's four D because we have simple heights and widths。

 and petal heights and widths and centimeters。 - Okay， so yeah， here's the exercise is to。

 basically understand why those three samples， are misclassified and then is also a bit of protein。

 by just giving， so， classifying and giving the index， of those three points in the scatter plots。



![](img/c04d678b99df1406ae3dbf232bf3d810_482.png)

 Okay。 - So basically if you read the instructions。



![](img/c04d678b99df1406ae3dbf232bf3d810_484.png)

 you can set different markers。 So in matplotlib when you do a scatter plot。

 there is a marker keyword argument in the scatter plot。



![](img/c04d678b99df1406ae3dbf232bf3d810_486.png)

 function and you can give， if you look at the， documentation of matplotlib by using a shift tab。



![](img/c04d678b99df1406ae3dbf232bf3d810_488.png)

 or going to the matplotlib website， you can see that you can give different markers。

 for the different points and use the matplotlib legend， to be able to see the different markers。



![](img/c04d678b99df1406ae3dbf232bf3d810_490.png)

 what they mean and what is the true class。

![](img/c04d678b99df1406ae3dbf232bf3d810_492.png)

 and what is the， for each of the errors。 - Yeah， so here for instance， what would be interesting。

 is to know which class it should be， and in which class we classify to understand。

 why is it that color or why is it misclassified。

![](img/c04d678b99df1406ae3dbf232bf3d810_494.png)

 - If you don't want to do it with matplotlib， what you can also do is for each of those data points。



![](img/c04d678b99df1406ae3dbf232bf3d810_496.png)

 that you identified previously， if you can scroll up。



![](img/c04d678b99df1406ae3dbf232bf3d810_498.png)

 So here you have the indices。

![](img/c04d678b99df1406ae3dbf232bf3d810_500.png)

 Okay， here you have the indices of the three data points。

 you can just print the beta lens and sepal widths， to see which is which and print the class。

 for each of them and see why it made a mistake。 Try to understand why it made a mistake。

 - So as before， when you think that you have， found the， I mean， why you can put the stickers。

 and like this we can move forward afterwards。

![](img/c04d678b99df1406ae3dbf232bf3d810_502.png)

![](img/c04d678b99df1406ae3dbf232bf3d810_503.png)

 Okay， so by just looking at the data we want any protein。



![](img/c04d678b99df1406ae3dbf232bf3d810_505.png)

 we can already check。

![](img/c04d678b99df1406ae3dbf232bf3d810_507.png)

 So we already say before the incorrect indexes。

![](img/c04d678b99df1406ae3dbf232bf3d810_509.png)

 So is this variable that was defined here。 So NP where prediction are different from the test Y。

 and then we're getting pho indexes。

![](img/c04d678b99df1406ae3dbf232bf3d810_511.png)

 Okay， so I just print here those pho indexes， and we can already check what was the class in the test Y。

 and what is the class that we actually predicted。

![](img/c04d678b99df1406ae3dbf232bf3d810_513.png)

 So in that case， we predicted two and two for the first one。

 and a class one in that case and then the one we swap， we predict in one and it should be two。

 So to find out which sample or which one， we can select the data and basically we took the。

 feature one and two because they are the feature。

![](img/c04d678b99df1406ae3dbf232bf3d810_515.png)

 which we are putting here。 So here in X we plotted the second column， and in Y the third column。

 So here we are just getting the second and third column， and we take the value of that correspond。

 to the incorrect samples。 So if we check just for the last one which is。

 it's only one that we swap from one to two。 So is that position 2545 and if we check this one。

 is this sample which is here。 So what we said is that we predict， predicting class one。

 class one should be this class。 Okay， so we predicting orange and it was actually a green。 Okay。

 and those one where I've been predicting green， and they were a class orange。

 So the feeling behind it because what the nearest neighbor， is doing is checking the。

 in that case by default， we check the five nearest neighbors。

 So we check the five nearest neighbors around that point。

 and of course there is more orange than green。 So the classification will predict as an orange point。

 but the truth was that it was a green one。 Similarly for those one we check that the five nearest。

 neighbors that were the closest to those point were green。

 So we classify as green but actually it was some orange one。 Okay， so the reason is because our。

 our heuristic， that to check like the five closest didn't work， for those three specific samples。

 Okay， so I can load the protein。 So this is just repeating what we did before， but in a nice way。

 Okay， and now we just， I mean we just express the same thing than what we saw。 So it can be， okay。

 Maybe you can show the matplotlib。 Yeah， here we are using specific markers here。 X， S and V。

 V is the， the triangle that goes to the bottom。 S is square and X is the cross。

 And you see that we are passing the marker， for each of the correct， incorrect indices。

 And we pass the label also as a， I as the label， so the index。

 And so this makes it possible to have this， that has been displayed here automatically as the legend。

 Okay， so this is matplotlib stuff。 And so can you display this？ Okay。

 so you see that here we have a gray point， that is in the middle of the， no， yeah gray point。

 that is in the middle of the green ones， and here another green one that is in the middle。

 of the gray point and stuff like that。 So in your opinion， how we could fix the model here。

 to make it avoid those kind of mistakes？ Remove outliers， but those are not outliers。

 they are real there。 There are not significant outliers there， in the middle of the density。

 high density region of the data。 And they are not mistakes， they are， they are， I don't know。

 I'm not a biologist。 But let's assume that the biologists did not make any。

 mistake in labeling the train set。 We could project of the rise， but this is for visualization。

 and the carnivorous neighbor's classifier， has actually used the whole four dimensions。

 It used just those two， it used the four dimensions。

 just that we can see the problem with those two dimensions， is enough that we can see the problem。

 but the model has used the four dimensions。 - If you alter the split of the classes。

 in your training set， so it's weighted a little bit more， heavily towards the misclass by examples。

 or try making synthetic data。 - So I think it's good to have the split。

 that preserve the natural balance of the data。 And here they are naturally well balanced。

 I'm not sure it's representative of the true distribution， in nature。

 but changing that is not likely to。

![](img/c04d678b99df1406ae3dbf232bf3d810_517.png)

 like it's just the class two and one and two。

![](img/c04d678b99df1406ae3dbf232bf3d810_519.png)

 that are building mislabels。 I'm not sure we can reweight those to fix that issue。

 So first what we could do is maybe focus on a larger region， so a larger number of neighbors。



![](img/c04d678b99df1406ae3dbf232bf3d810_521.png)

 like change the value of care， in K-nearest neighbor's classification。 But for this case。

 I'm not sure it's gonna fix it。 Maybe it's just fundamentally the features。

 that we use are not enough。 So maybe in this case， the only way to fix it。

 might be to collect additional features， like the colors or information on specific patterns。

 that you could see on the flowers or stuff like that。

 Or if you can do biopsy and do genetic analysis， that may be even better feature。

 And you could use that as additional feature。 Sometimes the data itself is what is limiting the model。

 and it's not actually a choice in the model。 Another way that we could do is maybe the metric space。

 that we are using is not good。 Maybe we should rescale the， like maybe divide。

 by the standard deviation of the distribution， and maybe in that new space， the metric space。

 would naturally split the data more。 I'm not sure it's gonna work in this case。 It's quite unlikely。

 But there might be some alternative metric space， where the classes are better separated。

 Like the sentiment of space has no guarantee， that to be the best space。 There was a question of。

 no？ Yes？ - [inaudible]， Maybe the data in the boundary is different from what？



![](img/c04d678b99df1406ae3dbf232bf3d810_523.png)

 - I'll play a different criterion。 - Yeah， we could also try another model。



![](img/c04d678b99df1406ae3dbf232bf3d810_525.png)

 like a random forest or something else。 But because there is this overlap in that region。

 it's quite likely that any other model， will fail in a similar manner。 - Yeah。

 probably when you will focus on those samples， and you misclassify some others。

 because now you look at this specifically。 - You get some improvement by changing the neighbors。

 to six or eight over the one。 - Okay， okay。 So changing the neighbors to a larger neighborhood。

 might remove some of the classification error， the mistakes。 However。

 be careful that we have a very small number， of test samples， so maybe just by chance。

 that it's working better。 But indeed that might improve a bit。

 And we'll try to play with that in the next notebook， actually。 Okay。

 so do you have any other question， about training， splitting， and it's fine？ Okay。

 so next one will be about supervised learning， and specifically about the frame of classifications。

 So up to now， classification is what we did。 Okay， so our target is the category。

 We have a defined number of categories， and we try to predict a category。

 So no continuous variables。 So here we'll look at basically two models。

 One will be the Canyars neighbors， and the one that will be linear classifiers。 I run by Fizzes VMO。

 logistic regressions， and see a bit like how those things are working。

 So first cells to import Matlab， Lib and Numpy。 So now what we'll do is that we'll create synthetic data。

 Data set， okay， so we play up to now with Iris。 So now we'll just make our own data。

 which is called make blobs。 So it's make blobs， we can tell how many blobs。

 do we want in our data sets， we can set our random states， and then we can also explain basically。

 how the what the standard deviation of those blobs。 So by executing this， we get X。

 which contain 100 samples with two features， and the Y which is also 100 samples。

 We can plot the vice-versed features， as we already did before。 We have the associated classes。



![](img/c04d678b99df1406ae3dbf232bf3d810_527.png)

 And we can make， because we have two dimensions， we can plot also what our data look like。



![](img/c04d678b99df1406ae3dbf232bf3d810_529.png)

 So if we do that， we get that data set， that we just generated。 So two class， zero and one。



![](img/c04d678b99df1406ae3dbf232bf3d810_531.png)

 and they are blobs because they are basically， Gaussian distributions， okay？

 And they are like two circles。 So they have the same standard deviations in both。

 I mean both circle have the same standard deviations。 - And so you see in this case。



![](img/c04d678b99df1406ae3dbf232bf3d810_533.png)

 that the standard deviation is so large， that there is a significant overlap。

 So we cannot expect by using just those two features。



![](img/c04d678b99df1406ae3dbf232bf3d810_535.png)

 to get a perfect classification accuracy。 Actually， for this specific data。

 if you know that the true distribution is two blobs， that are Gaussian distributed。



![](img/c04d678b99df1406ae3dbf232bf3d810_537.png)

 with the same standard deviation and spherical covariance， what is the best model that you can。

 what is the perfect classification model？ It's not perfect， but what is the best model。

 that you can make？ Do you have an idea？ - A Gaussian model， but what do you mean？

 How would the decision-bound array look like？ - Not a straight line。 - A straight line？

 Not a straight line。 A quadratic line。 Actually， it is a straight line。



![](img/c04d678b99df1406ae3dbf232bf3d810_539.png)

 the best boundary that you can make。 So if you know the true parameters of the true distribution。

 it's gonna be the centers of the Gaussians。 So you would have two centers。

 one approximately here and another one here。

![](img/c04d678b99df1406ae3dbf232bf3d810_541.png)

 What you could do is take the line， that goes through the two centers。

 and in the middle draw the perpendicular line， and that would be the best decision-bound array。

 that you could get。 It would not be perfect， there would be some bad classification on each side。

 but this would be the best classification model， and it would be a linear model。

 It would be a linear decision-bound array。 However， we don't know the true position of the samples。

 We don't know the true parameters of the distribution。 So we have to find a model。

 that is just using those samples， those data points that have been sampled， from the distribution。

 and we're using those finite data points that we have。

 What is the best classification model that we can train？ And we don't know ahead of time。

 that those two classes are Gaussians distributed。 So we don't even know that the best decision-bound array。

 is a straight line。 It's not just using those data points。

 it's not easy to see that it's a straight line。 Okay， any questions about that？



![](img/c04d678b99df1406ae3dbf232bf3d810_543.png)

 Okay。 So how we did before， we saw that it was important to make a training， and the testing split。

 So we just do exactly the same， and we will use 25% for the testing。

 and the 75 over percent for the training， and we apply a stratifications， to stratify the data。

 Just to not be to have any issues with that。 So we got our data in X-train， X-test， Y-train。



![](img/c04d678b99df1406ae3dbf232bf3d810_545.png)

 and Y-test， okay， as before。 And it's to recall basically the API。

 So we will call our fit to run our models， and then we will be able to predict using。

 and I mean to evaluate the generalization of our models， using predict， okay。

 And then we will use an evaluation to see， if our predictions are the same than the testing， okay。

 So we'll really solve it about that。 So what we'll do here is to use linear models。

 which is logistic regression， which is pretty the most basic models， but kind of powerful。

 And we'll create an instance with the default parameters。 Okay。

 so if you want to know a bit more about the parameters， or here， but for some months。

 we'll just focus on like using the default one。 So we create our models and then we can check the shape。

 of our data to be sure that we are properly， split in our data。

 So we will have 75 samples with two features， and the corresponding predictions。

 And the first thing that we do is that we fit。 So we'll learn our models on those data。

 So one that we learn our models， here we see that the output is also a model。 So fit。

 you return the model itself。 So it's allowing to do something， for instance， dot fit， dot predict。

 we could do that， okay。

![](img/c04d678b99df1406ae3dbf232bf3d810_547.png)

 It's allowing to chain functions。 That's why we have these outputs。

 So we can learn our model and one that we learn our models。

 we can make the predictions as we did before， on the testing data， okay。 So here we have X test。

 we don't know anything about Y test。 We get our predictions and now we can print。

 basically the predictions and the testing。 And we see that we have misclassifications。

 and some others that agree together。 And the same way that we did before。

 we can compute the ratio of good predictions， when the prediction agree with the grant proof。

 And here we obtain an accuracy of 72%， okay。 Just can you please insert a new cell， not just there。

 Just above this one to display the value， of prediction equal equal X test。

 - So that will return a Boolean mask。 Okay。 - So those are value true and false。

 whether or not they agree。 And basically what we want， the accuracy is the proportion。

 of true in that mask。 And so when you compute n-pay mean， it's the average n-pay mean。

 And basically you can treat false as zero and true as one。

 And it's gonna just count the number of ones， and divide by the total number of elements。

 This works because Boolean values are integers basically。 - So， second and purpose。

 I mean the classifier。

![](img/c04d678b99df1406ae3dbf232bf3d810_549.png)

 and regular solator we'll see。 You have fit， predict and you have one overall function。

 which is called score， a method。

![](img/c04d678b99df1406ae3dbf232bf3d810_551.png)

 And this allow us to just output a specific score。

 which is actually for the classifier will be this accuracy。

 And in that case we can give already the data， and what should be basically the grant proof。

 And it will automatically compute the accuracy， under the hood and give us basically the score directly。

 So we don't have to make predicts。

![](img/c04d678b99df1406ae3dbf232bf3d810_553.png)

 and then make the checking， we can already use that score。



![](img/c04d678b99df1406ae3dbf232bf3d810_555.png)

 and it will return us this。 However， be aware that for classifier， it will be the accuracy。

 So if you have imbalance data set that you do that score， it will return using the accuracy。

 which is not a good metric in that cases。 So you might want to use some other metrics。



![](img/c04d678b99df1406ae3dbf232bf3d810_557.png)

 - Can you give， do you have an idea， why the accuracy is not a good classification metric。

 for imbalance data？ So imbalance data is when you have for instance。

 95% of samples that are of class spam， not spam for instance and 5% of the samples。

 at our spam for instance。 - Well， I think if you had a classifier。



![](img/c04d678b99df1406ae3dbf232bf3d810_559.png)

 that just said everything is not spam， it would be perfect or pretty close。

 99% accuracy but also you can't。

![](img/c04d678b99df1406ae3dbf232bf3d810_561.png)

 - Yes， exactly。 So I repeat so that it's recorded on the video。

 If you have a classifier that predict always constantly。



![](img/c04d678b99df1406ae3dbf232bf3d810_563.png)

 the majority class like not spam， it will already have an accuracy of 95% accuracy。

 which is not very informative。 It's misleading because you might think。

 that is a higher accuracy classifier， but it's just a baseline that is predicting。



![](img/c04d678b99df1406ae3dbf232bf3d810_565.png)

 a constant target variable。 So in that case we could use alternative metrics， such as。

 - Balance accuracy for instance。 - Balance accuracy， ROC， AUC or F1 score。

 They are all in psychic learn， and you can read the documentation if you。

 - And we'll focus on that this afternoon。 I mean this is something about the metrics。

 So we can also maybe try to understand， if our classifier was already classifying。



![](img/c04d678b99df1406ae3dbf232bf3d810_567.png)

 good on the training set， because I mean it was the logistic regression， doesn't learn。

 I mean have to learn boundaries， but you can already make mistake。



![](img/c04d678b99df1406ae3dbf232bf3d810_569.png)

 and we can check like this， if it's able to generalize well or not。

 So for instance we are making an error， of I mean an accuracy of 0。9， and then we try to 0。72。

 so we are not good enough to generalize here。 So because we have only two dimension。

 we can visualize with a scatter plot。

![](img/c04d678b99df1406ae3dbf232bf3d810_571.png)

 and plot basically the decision boundary， of our classifier。 So here we have our first class。

 second class， and we see that the logistic regression。

 just try to find the line that best splits the two blocks。

 and then we see that because the two block overlaps， then we have some points which are。

 misclassifying on each side of the lines。 - Maybe you could insert a new cell。

 and use the double question marks， to display the source code of the plot。

 to desecip right of function。

![](img/c04d678b99df1406ae3dbf232bf3d810_573.png)

 So if you have， here we give you a way to directly plot， the decision boundary， but it's no magic。

 If you want to know how it works under the hood， you can use a double question mark。

 and you see the source code， and in particular what we can see。

 looking for the coefficients of the model。 Okay。 - So yeah we just make a。

 we call it decision function， of image width。 - Yeah， this is what I would not have。



![](img/c04d678b99df1406ae3dbf232bf3d810_575.png)

 implemented this way， okay。 Anyway， what is it？

![](img/c04d678b99df1406ae3dbf232bf3d810_577.png)

 Maybe you can stop this， remove it， close it。 What is important for this model。



![](img/c04d678b99df1406ae3dbf232bf3d810_579.png)

 it's a linear model and if you introspect the attribute。



![](img/c04d678b99df1406ae3dbf232bf3d810_581.png)

 which is called co-f on the classifier。 Not co-f。 So you see that you have this co-f underscore。

 The underscore means that it's an attribute， that is derived from the data。



![](img/c04d678b99df1406ae3dbf232bf3d810_583.png)

 and there is also an intercept underscore attribute。



![](img/c04d678b99df1406ae3dbf232bf3d810_585.png)

 And basically this is a weight parameter， for the first feature。

 and this is the weight parameter for the second feature， and basically those two plus this one。

 give you the parameter for the fine function， that is the straight line in that two dimensional space。

 So you can derive the equation for that line。

![](img/c04d678b99df1406ae3dbf232bf3d810_587.png)

 from those three parameters， that were found directly from the data。 Okay。

 they were just afterwards。 So it's fine。 Yep。 Okay。

 So how we saw before you can use another type of classifier。 So the first one has the assumption。

 that you can find a linear separation， between the two classes。 Okay。

 So you try to find the coefficient， that best splits the two class。 In the lower case you can use。

 for instance， the Cast Nails neighbors， which will make not such an assumption。

 what you will base is decision on his neighbors。

![](img/c04d678b99df1406ae3dbf232bf3d810_589.png)

 So he's a non-parametric approaches with parameters。 So we can import the Kanias neighbors。

 and here maybe 30 is a bit too much。 - Can I try one？ - One， okay， let's try the minimum one。

 So we'll just look at the next， the closer samples to take our decisions。

 So we see that here we call the same fit， and the same predict functions to do our testing。

 and protein。 So here we are fitting our classifiers。

 and how we make this cataprots only on the training data。



![](img/c04d678b99df1406ae3dbf232bf3d810_591.png)

 Okay， and that's our decision boundaries here。 Okay， so we have like a straight line here。

 because we don't have samples next to each other。 And then here we see that our decisions。

 really rely on the sample next。 So we have a very weird decision boundaries。



![](img/c04d678b99df1406ae3dbf232bf3d810_593.png)

 which try to isolate every sample， and that when， because the sample is alone。



![](img/c04d678b99df1406ae3dbf232bf3d810_595.png)

 it will just focus on these samples。 And before we go further， I'm sorry。



![](img/c04d678b99df1406ae3dbf232bf3d810_597.png)

 But try on your laptop to change that parameter， to higher values and see what it does。

 And neighbors to maybe 30 for instance。 Okay， so this is with a NABOS equals five you get this。

 It's a， because it's disconnected the decision boundary。



![](img/c04d678b99df1406ae3dbf232bf3d810_599.png)

 Maybe 30 again。 And so if you use 30， you see that it's going。

 the decision boundaries is getting smoother， and it looks like a straight line actually。

 So in that case， it's going towards the optimal model。



![](img/c04d678b99df1406ae3dbf232bf3d810_601.png)

 It's not a guarantee， but in that case。

![](img/c04d678b99df1406ae3dbf232bf3d810_603.png)

 a higher value of NABOS is better。

![](img/c04d678b99df1406ae3dbf232bf3d810_605.png)

 - So when you have a small numbers of neighbors， you will really focus on all the samples next to you。

 and having like a very local decision boundary。 Which might lead to what we call overfitting。

 And when you want to avoid these things。

![](img/c04d678b99df1406ae3dbf232bf3d810_607.png)

 and regularize somehow， you will get larger numbers。 And then you get such much more like now。

 - So yeah， the fact that we have this overlap， is caused by the noise that is just the fact。

 that the two distributions are very， have a scale that is very large and overlapping。

 And so if you just make the K&RS neighbors decision， boundary focus on local features。

 by using NABOS equals one， then you will basically memorize all the noise， from the training set。

 And this noise does not generalize to the test set。 So if you're too local， it's a bad idea。

 and you're memorizing the noise。 If you're too global， maybe you will be too smooth。

 and not be able to adapt to the structure of the data。



![](img/c04d678b99df1406ae3dbf232bf3d810_609.png)

 So we need to try different values。

![](img/c04d678b99df1406ae3dbf232bf3d810_611.png)

 and use the validation set to find the best one。 - So for instance， if I go back to just one。

 because it was like one corner case， we have this very weird decision boundary。

 and that's our training set。 And I can check the score on the training set。

 And of course I get one because I learned the distance， like of all the data。 - Yeah， actually。

 it's a question。 - Try to think why it's when we have NABOS equal one。

 why the model is making perfect predictions。 Try to think how the model works internally。

 To make a classification， it will find the nearest neighbor。 And the nearest neighbor is itself。

 So it's gonna find its own set， true classes。 So because we are evaluating on the training set。

 we just memorize and do a query in the database， and we find ourselves and we make a perfect prediction。

 each time because we just have a perfect memory， of the training set。

 But then on the validation set or the test set。 - So you can already make the plot。

 and check how only seeing the test data， how they are on the boundaries。

 So already we see that query here， we have like a very， let's say， complicated boundaries。

 This is a boundary for not pretty， not specific reason。 It's because it was only noise。

 and we just make this specific decision there。 And for instance here， we do like coming back。

 and this point is classifying on the blue line， not for， I mean， just because of noise， okay。 So。

 and then you can check the score， and you get 0。76， which is already better。

 than the linear classifier。 But then you can increase and check how it's generalized。

 So here we obtain a line。 In that case， because we have more neighbors。

 we make even errors on the training set。 But when we look at the decision here， I mean。

 it's more meaningful。 And if we check the score， we make a bit less errors on the testing， okay。

 Because we are able to through regularization， to improve the results。

 - So there's basically a trade-off， between model flexibility。 So if the model is too flexible。

 it will memorize the noise。 But if the model is too constrained， too smooth。

 then it might not be able to capture， the interesting part of the distribution of the training set。

 And so there is this trade-off in model complexity。

 And most of the cyclical and machine learning models， there are some hyper parameters。

 that can control the complexity， the flexibility of the model。

 And we need to adjust that to find the best value。 - Okay。

 so now the exercise is to load the iris data sets， because now we are playing with blobs。

 So load the iris data sets， prep with the number of neighbors， and check what's the best trade-off。

 I mean by splitting the data into training， testing， and checking what are the research。

 what's the best there。 So yeah。 - So you can choose an arbitrary trend to split， like for instance。

 80% for the trend set， and 20% for the test set。 And train， Kenerys neighbors on the training set。

 and they score it on the test set， and print the score both on the trend set。

 and on the test set to compare the influence of N-nebors。

 and find the best value of N-nebors on the iris data set。 Okay。

 so it's a recap of what we've seen previously。 So let's have five minutes。 One question， yeah？

 - You can get it， we'll help with the--， - Okay。 - Okay。 (muffled speaking)， - Okay。



![](img/c04d678b99df1406ae3dbf232bf3d810_613.png)

 So I will load directly the solutions。 So we already saw that we can load the iris data set。

 from second learn。 We load also the module to make the train test split。



![](img/c04d678b99df1406ae3dbf232bf3d810_615.png)

 So here we get the X and Y， okay？ And we put it， we put the data in X， the targeting Y。



![](img/c04d678b99df1406ae3dbf232bf3d810_617.png)

 and we split our data by taking 25% for the testing， and the complement for the training。

 stratify our Y to be sure that we have。

![](img/c04d678b99df1406ae3dbf232bf3d810_619.png)

 the same proportion everywhere。 And here it's coming back to the question that we had before。

 on splitting data to test， to train validations and testing。



![](img/c04d678b99df1406ae3dbf232bf3d810_621.png)

 So why do we want to make， what we are doing right now is trying， to optimize any parameters。

 So we need to have the testing completely separated。

 that we never saw to actually see the performance， of our final models， and what we'll do is。

 re-split the training into a train and validations， and to evaluate the influence of the K。

 on the validation set。 So here we split to train and test。

 and here we further re-split the training， into validations and the sub-training。

 So you see that basically you have these things here， train valve and the test。

 That's why we have three things。 And now what we are doing is for different value， of the neighbors。

 we'll compute the train score， the train score on which we just fit our KNN， on the train sub。

 so on this X train sub and Y train sub， and score on the train sub in that case。

 and we'll check the validation score， on the validation set here。 - Why is it X train and Y test？

 - Because this one will be totally at the end， when we find our base neighbor。

 - What is the best size for several？ - Yeah， that's me。 So we did half and a half。 Yeah。

 because this Irish data set is very small。

![](img/c04d678b99df1406ae3dbf232bf3d810_623.png)

 Here we use a large test size， and the training set is gonna be small in the end。

 So here it's the proper way to do it。

![](img/c04d678b99df1406ae3dbf232bf3d810_625.png)

 but on such small data set， we would also need to do what we call cross validation。

 to be more efficient with respect。

![](img/c04d678b99df1406ae3dbf232bf3d810_627.png)

 to the size of the data set。 And this is something that we will introduce later this afternoon。

 So here I just split everything。 So here we split twice our data， to get training。

 validations and tests。 And our inner loop is to evaluate the influence of K。

 and to find what is the best K that we can find。 So we train the models and then we evaluate on the validations。

 and we make a loop for the different K。 So we get like 20 outputs。

 and now the idea will be to find what K is maximizing， basically on the validation sets。

 We don't care about the training sets， it's just to see if training is actually。

 if the testing is generating on the training。

![](img/c04d678b99df1406ae3dbf232bf3d810_629.png)

 but what we are trying to maximize here is the second number。

 So basically the accuracy that we get on the validation sets。 And the optimal K that we found was。

 a pre nine。 - No， it's not。 - I know exactly why it's nine， but。 - Yeah。

 in this case it's weird because K equals four， you have a good one。 - Two。

 - And a key equal two or so。 And also this guy， 12。



![](img/c04d678b99df1406ae3dbf232bf3d810_631.png)

 So there is a good region of good case here。

![](img/c04d678b99df1406ae3dbf232bf3d810_633.png)

 and good region at the beginning。 And it's quite unusual。

 but it's probably because we have the random， train split and maybe when Andreas would this not book。

 the first time， nine was the best one。

![](img/c04d678b99df1406ae3dbf232bf3d810_635.png)

 but it's no longer the case。 And this is really an artifact of the fact。

 that we have a very small data set。 So it's not stable to find a good K here in this case。

 Apparently you can say K equals 12 is good。

![](img/c04d678b99df1406ae3dbf232bf3d810_637.png)

 K equals one is good or two is good。 That's kind of unusual。 If you have a larger data set。

 it's likely， that there is a region of K that is good。

 and most of all the values will be slightly worse。 - So now that we found out or that we think。

 that we found our best neighbors， I mean numbers of neighbors， we create a new classifiers。

 and now we'll fit on the wall training sets。 Okay， so training plus validation together。

 and now we will predict on the set。

![](img/c04d678b99df1406ae3dbf232bf3d810_639.png)

 that we completely didn't use up to now。 Okay， because we already optimize the parameters。

 of our models。 Okay， and now yeah， he's two。 And now we find that our accuracy is 0。947s。

 which is a bit lower than what we found on our validation。

 but it doesn't matter because our set is too small。 Okay， that's， but here this is by hand。

 how you would do to search any parameters。 So for instance， when you have models。

 you have several parameters and sometimes you want， to find the best case， the best C。

 for the logistic regression， et cetera， et cetera。

 And this afternoon we'll see that you can do that， in scikit-learn just by a single line。

 not doing it the follow-up yourself。 Okay， and avoiding that you mess up。

 with basically the split of the data。 Okay， so you just give the data。

 you say I want to optimize these parameters， and then you will make the splitting for you。

 But understood is what he's doing。

![](img/c04d678b99df1406ae3dbf232bf3d810_641.png)

 and is a good result to see。 Okay， do you have any question about this？



![](img/c04d678b99df1406ae3dbf232bf3d810_643.png)

 - Maybe what you can do is change the random C， here for the two splits。 One and one， for instance。

 42。 And see if the location here。

![](img/c04d678b99df1406ae3dbf232bf3d810_645.png)

 so we see that the top， actually， now in this case， K11 is even better。

 - It's really weird that the validation accuracy， is larger than training accuracy。

 It's because those data sets are so small， that we cannot trust those numbers。

 - So don't do machine learning with 150 samples。 That doesn't work。 So yeah， we get better results。

 Non-synificant。 Okay， do you have any question on that？ Oh， it seems clear。 Yeah？ Okay。

 so we can move to the next notebook， which is supervised， but in that case。

 we'll focus on the regression instead of the classifications。

 So hope to know with the classifications， our target was a category， spline， non-spam。

 which type of flowers， I mean， which species of flowers。 So now it will be a bit different。

 It will be a continuous variable， so predicting the temperatures or the humidity。

 and this type of things。 So we'll see that basically this is the same strategies。

 It's just that's our output and our score。 We will evaluate with different metric。

 So we import multiple lib and numpy。 And now we'll create X。

 which will be between minus three and three。 Okay？ And we want 100 samples。

 which are equally spaces。 Okay？

![](img/c04d678b99df1406ae3dbf232bf3d810_647.png)

 That will be our X value。 And then we will create a Y。

 which will be a sign of the four X plus X plus， a bit of noise。 Okay？

 So we create Y and now we can plot the relationship。



![](img/c04d678b99df1406ae3dbf232bf3d810_649.png)

 between X and Y。 Okay？ So what we have is we have our X， which is going up， which is including。

 And then we have our sign， which is added to this X。



![](img/c04d678b99df1406ae3dbf232bf3d810_651.png)

 Okay？ And then fluctuation for the noise。 So there is a linear trend plus a local periodic variation。

 So it's a global warming， Samarans， winter。 So in this case， you see that Y is linked。

 to a single variable as an input。 So the target variable Y is linked， to a single feature basically。

 So here it's a bit of a very specific case， where we have a single feature in the input space。



![](img/c04d678b99df1406ae3dbf232bf3d810_653.png)

 So one way of doing regression is to actually use， ordinary least square to actually find。



![](img/c04d678b99df1406ae3dbf232bf3d810_655.png)

 how X and Y is related。

![](img/c04d678b99df1406ae3dbf232bf3d810_657.png)

 And as， or you've mentioned before， one thing that we absolutely need in Saikit-Learn。

 is that our X， our big X， so our data matrices， need to be a 2D data。

 And here is a case that we have only a single features。 And to transform this 1D matrices into 2D。

 we can create a new axis using Np。new axis， as we saw in the NumPy introductions。 Okay？

 So if we do that， we see that we go from a single array， a vectors of 100 numbers to an array。

 a 2D array of a column with hundreds lines。 Okay， 100 rows。

 So the same way that we did for the classification， we can split into a train and the test。



![](img/c04d678b99df1406ae3dbf232bf3d810_659.png)

 our data with the same functions。

![](img/c04d678b99df1406ae3dbf232bf3d810_661.png)

 So we just jump a line。 And here we decide that our test set will be 25%， and a random。

 and here stratify don't apply。

![](img/c04d678b99df1406ae3dbf232bf3d810_663.png)

 Okay？

![](img/c04d678b99df1406ae3dbf232bf3d810_665.png)

 Because we have a continuous variable。 So we can split our data。

 And the same way that we're doing before， we can fit a linear regression。

 which will learn what how to fit these lines。

![](img/c04d678b99df1406ae3dbf232bf3d810_667.png)

 So we create a regressor with linear regressions， and fits X train and Y train。 So as before。

 we have some coefficients。 So here it will be the slope of the lines。

 because we will try to fit the line。 So it will be a slope of the line。

 plus the intercept on the Y axis。 And so， and basically we can draw this line， okay？

 Because the other way， the weights multiply by the inputs， plus the intercept that we found。

 And if we plot that， it's what we obtain。 So that's our real data。 And the line that we just found。

 is basically the line that across the data in the meters。

 So you see that basically with linear regression here， we are not a ball。 I mean。

 simply with the data that we have， we are not a ball to find the nonlinearity of the sign。



![](img/c04d678b99df1406ae3dbf232bf3d810_669.png)

 We find the linear trend of the X， but we don't find the nonlinearity。

 So is what we can basically predict， and check our predictions。

 And we see that when we predict the prediction。

![](img/c04d678b99df1406ae3dbf232bf3d810_671.png)

 correspond of the point which are basically on that line。



![](img/c04d678b99df1406ae3dbf232bf3d810_673.png)

 because it's a linear regression。 Okay， so here we are making predictions。

 for each of the X values in the training set。

![](img/c04d678b99df1406ae3dbf232bf3d810_675.png)

 So this point， like the blue point， basically we create points here。



![](img/c04d678b99df1406ae3dbf232bf3d810_677.png)

 So the blue points are with the true target， and the orange points are the same X values。

 but the output is the output of the model。 So the Y value is the output of the model。

 And so you see that everything has been projected。



![](img/c04d678b99df1406ae3dbf232bf3d810_679.png)

 to this line。 And what the ordinary least squares model。



![](img/c04d678b99df1406ae3dbf232bf3d810_681.png)

 linear regression does is trying to minimize， the distance between the orange points。

 and the matching blue points taken， the difference taken to the square。

 And you take the sum of all the squared differences。

 and this is what we call the least squares model。 And it's trying to find the coefficients。

 for the linear trend that will minimize， the sum of the squares。 - So that's why you straight line。

 is exactly in the middle of the sign， because it's what minimize the distance， between every points。

 okay？ So that's more or less， because it's a bit of noise。

 So now you can predict the same way on some new data。 And you will see exactly the same things。

 that we point that we didn't predict。 We will predict them on the same line， okay？

 So a way to evaluate in that case， will be to， so we saw that for classification， we use accuracy。

 In the case of recurations， we are using the coefficient of determinations。

 So it's an r squared score。 So when we go to regular。score， because this is a regular。

 in that case it will output us this score， where one， means that all the points are well predicted。

 And then it will go to minus infinity。

![](img/c04d678b99df1406ae3dbf232bf3d810_683.png)

 when this is not well predicted。

![](img/c04d678b99df1406ae3dbf232bf3d810_685.png)

 - So here it's a bit misleading， because here this formula is for the mean square error。

 which is a error。 And here this is a score。 So this is the r2 score。

 So a score in secular is something higher， it's better。



![](img/c04d678b99df1406ae3dbf232bf3d810_687.png)

 And here we know that for the r2 score， the perfect model as a score of one。

 a random model as a score around zero， and a model that has been badly。

 really badly designed and predicted， very antichorated stuff would be a negative values。

 And the mean square error is actually， the function that the linear regression model。

 is trying to minimize。 It's trying to minimize this subject。

 If maybe you can import it from a scalar matrix。 - Scale matrix。 - MSC， mean square error。 - Yeah。

 - No， it's just。 - Mean square error of a way， way through or way prediction。

 and a way test and then prediction。 - Yeah， but I didn't have the way test。 - I hope I'm sorry。

 - Okay， sorry。 - I didn't。 - See， it's way test first。 - Yeah， it's true first。 In that case。

 it's symmetric。 So it's not a problem， but in general， in psychic learn for the metrics。

 we put the true value first， and then the predicted value second。 So here， this quantity。

 we try to minimize it， and a perfect model will be zero error。 This quantity here。

 which is the r square， we try to maximize it and the perfect model， would be one。

 we'd have a score for one。

![](img/c04d678b99df1406ae3dbf232bf3d810_689.png)

 We could also have additional metrics， like the absolute deviation。

 mean absolute deviation or other regression metrics。 We will see more， I think this afternoon。



![](img/c04d678b99df1406ae3dbf232bf3d810_691.png)

 mean absolute error here。 - So yeah， the advantages of those type of errors。 So the r square。

 they are not linked。

![](img/c04d678b99df1406ae3dbf232bf3d810_693.png)

 to the target that we use。 So for instance， when you use a mean absolute error。

 it means that this is the error， that you do， for instance， if you measure temperatures， in degree。

 these mean absolute errors， it's in degree as well。 So it's linked to what you are measuring。

 So you can interpret it as a human。 The r square， it just distances to what you are。

 like basically regressing and it's more difficult to interpret。 - There's no direct interpretation。

 because you cannot see the dimension of。 - But yeah， the notebook on the metrics this afternoon。

 is just focusing on that， so we'll come back。 So here it's just more to see that in classification。

 score correspond to accuracy， in regression score， correspond to this coefficient of determinations。

 which are also called r square。 So now there's an either size in which we'll try。

 to make our linear regression a bit smarter， by succeeding to predict， I mean。

 to account for the nonlinearity。 So to do that， we need to concatenate a sign of 4x in x。

 So we'll add the second column and this is the definition， with how to do that with concatenate。

 And then to redo our building of splitting our data， and see how our fitting and predict changes。

 And we'll see that that should be better。 - So the goal of the exercise to generate a new data set。

 that has two columns。 The first column is the same as previously。

 and the second column is sinus of 4x。 So we complete the sign function of 4 times x。

 and we store the result in the second column。 So you concatenate two columns。

 you can use this function from numpy。 And then you redo the splitting， you retrain the model。

 and you see whether or not you can make better prediction， this way。 - Yes you。 - Okay。

 So basically， because the model is linear by nature， we can do nonlinear feature extraction。

 to kind of remove that limitation of the model， to find a better prediction。 [BLANK_AUDIO]。

