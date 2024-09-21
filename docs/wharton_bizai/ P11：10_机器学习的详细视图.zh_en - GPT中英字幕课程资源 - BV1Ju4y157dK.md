# 沃顿商学院《AI For Business（AI用于商业：AI基础／市场营销+财务／人力／管理）》（中英字幕） - P11：10_机器学习的详细视图.zh_en - GPT中英字幕课程资源 - BV1Ju4y157dK

 Hello， in this lecture， we're going to go into the details of machine learning。



![](img/33371fd29fdcdcfa12400f3f3a0bb95f_1.png)

 In particular， I'll try and provide a high-level view of what is machine learning and what drives。

 the accuracy of machine learning models。 For the purposes of this discussion。

 I'll tend to focus only on supervised learning techniques。 There's a good reason for this。

 If we look at the practice of AI， I would say that almost 90% or maybe even higher than。

 90% of practical business uses of AI tends to be machine learning。

 And if you look at within machine learning， almost 90% of machine learning in practice。

 tends to be supervised machine learning。 So for the discussion of machine learning at a very high level。

 I'll tend to focus our， attention on supervised machine learning algorithms。 As I mentioned earlier。

 edit score supervised machine learning is all about taking a set。

 of input variables and predicting some outcome variable。

 Now we do this all the time in our real life。 For example。

 if you observe dark clouds and strong winds， we might predict that maybe， it's going to rain。

 Or we might look at what clothes somebody is wearing or better yet， how they're interacting。

 with us。 And we might make some inferences or predictions about whether we're likely to be good friends。

 with them。 Or at the workplace， we might look at a person's educational background。

 We might look at their job experience at their skills and predict whether they'll be successful。

 at the job。 These are all typical prediction problems that we are solving on a day to day basis。

 Now there are many business applications of these kinds of predictions。 Now for example。

 in a business setting， we are trying to predict whether somebody will， buy a product。

 We're trying to predict whether somebody will click or add。

 All of these predictions can be made using supervised learning if we have good training。



![](img/33371fd29fdcdcfa12400f3f3a0bb95f_3.png)

 data。 Let's consider an example。 Suppose we have data about users coming to our website。

 We might know how many pages have they viewed on our website in the past。

 We might know their zip code based on their IP address。

 We might know what device they're accessing our page from。

 And we might know the operating system of that device。 And ultimately。

 we're trying to predict whether this person will purchase a product， or not。

 Now that's a typical prediction problem one might have。 Now for the data we have about our users。

 meaning the input data that we use to make predictions。

 One refers to these input data as the predictors of our model or the features in our model or。

 sometimes just the data and the variables or the covariates of the model。

 There are many different names， but ultimately we can think of all these variables as the。

 inputs to our model。 Now given these inputs， we are also trying to predict something。

 That's the output of our model or the outcome variable。

 So we might describe the input variables using the letter X and we might describe the outcome。

 variable using the letter Y。 Now the prediction problem that we are facing is we are trying to figure out given the input。

 X we are trying to predict Y。 That is we are trying to figure out some function F that takes as an X as an input and predicts。

 Y。 The entire task of supervised machine learning comes down to coming up with a highly accurate。

 approximation of this function F so that we can predict Y as accurately as possible given。

 the inputs X。 Now the notion of accuracy is built in to what I just described。

 For any prediction problem we think of accuracy as essentially a measure of how often are the。

 predictions true or how close are the predictions to reality。

 So for example if we are trying to predict whether a person purchases or not， if we make。

 100 prediction and 93 of those 100 predictions are correct， we might say that the prediction。

 accuracy of our model is 93%。 We want this prediction accuracy to be as high as possible and so natural question is。

 to ask what drives the prediction accuracy of a model。

 One factor that drives the accuracy of a machine learning model is the quantity of data meaning。

 the number of distinct observations we have as an input into the model。

 So for example if we have data on only 100 customers who have been to our website in， the past。

 it would be very hard for us to make accurate predictions about future customers。

 visiting our website based on the observations of just these 100 users。

 On the other hand if we had data for a million users then we have a lot more data and so clearly。

 having more observations helps increase the accuracy of our model。

 Another driver of prediction accuracy is how much do we know about each observation。

 Now in the example I just described for each consumer we only knew the number of pages。

 they viewed in the past， we knew the operating system they use and we also happen to know。

 their location。 But this amount of data might not be sufficient for us to actually make the predictions。

 On the other hand if we had much more data about each user， for example we knew that。

 users interests， we also knew that person's income level， we also happen to know whether。

 they have made purchases from our website in the past and many more such observations。



![](img/33371fd29fdcdcfa12400f3f3a0bb95f_5.png)

 then the prediction accuracy of our model might go up significantly。

 In other words the two factors that seem to drive the accuracy of the model are the number。

 of rows which we can think about the number of data points and the number of columns which。

 we can think of as the number of features or the number of x variables available within， each row。

 Together they tend to drive the accuracy of machine learning models in very significant， ways。

 But by no means the only two factors， there's a number of other factors， for example how。

 relevant is the information you have available。 If we were trying to predict whether it's going to rain today。

 knowing how many people， are carrying umbrellas today is more useful than just knowing the color of the clothes。

 worn by people。 So clearly having more relevant data matters。

 Similarly the complexity of the model matters， if we restrict ourselves to use very simple。

 models they might not be able to capture very complex relationships that are out there。

 in the environment。 So some of the more modern machine learning methods like deep learning which I will describe。

 in a later lecture allow us to have more flexible and more complex relationships between the。

 input variables and the outcome variables and this helps increase the prediction accuracy。

 of models。 Another factor is what is referred to as feature engineering。

 This is essentially the ability of an analyst to use their domain knowledge to create new。

 features or new input variables that are predictive of the outcome。

 This comes down to having deep domain knowledge and identifying what new data might we add。

 to our data set or how might we transform our data set so that we can better make predictions。



![](img/33371fd29fdcdcfa12400f3f3a0bb95f_7.png)

 In short there are many different factors that drive the success of machine learning models。

 Certainly one has to think about many of these factors。

 It always starts with having high quality and high volume data with lots of rows and lots。

 of columns。 In the next lecture we will talk about some specific machine learning algorithms to give。

 you a better intuition of what exactly these machine learning algorithms do。 [BLANK_AUDIO]。



![](img/33371fd29fdcdcfa12400f3f3a0bb95f_9.png)