# 沃顿商学院《AI For Business（AI用于商业：AI基础／市场营销+财务／人力／管理）》（中英字幕） - P45：11_Scott Wong访谈.zh_en - GPT中英字幕课程资源 - BV1Ju4y157dK

 Scott Wong is Vice President of Machine Learning for Foundation Search and Voice Science at SiriusXM。



![](img/a63ceec66cc04d98ed1931758605ad7d_1.png)

![](img/a63ceec66cc04d98ed1931758605ad7d_2.png)

 His team builds reusable machine learning systems that power recommendations and discovery across SiriusXM。

 Pandora and other products。 Welcome and excited to talk to you today。

 To ground us in your perspective， can you tell us about your role at Pandora as a VP of Machine Learning Search and Voice and your career journey？

 Yeah， thanks for having me today， Mary。 I'm the Vice President in the Product Development Organization focusing on machine learning for Pandora and SiriusXM。

 My team leads research and development for foundational machine learning systems， search and voice。

 The foundational systems are reusable machine learning components like core representations of listeners and their interests。

 They're ensembles of recommendation strategies and experimentation frameworks like multi-arm bandit systems。

 In Search， we build machine learning driven ranking models to help listeners find exactly what they're looking for。

 And in Voice， we use natural language understanding， dialogue management， content tagging。

 personalization and a few other techniques to help listeners explore audio entertainment in innovative ways。

 I think it's now been about 20 years ago that Pandora was born from what many people might not know is called the Music Genome Project。

 So that's a bit of trivia for you out there。 And it became the first music recommender system for consumers。

 So with that， could you describe how the project， the Music Genome Project was conceived and then how Pandora was developed from that project？

 Yeah， absolutely。 The Music Genome Project is an initiative where a team of professional music colleges sit down and listen to music tracks day in and day out every day。

 annotating over 450 different attributes about those tracks。

 So that's things like what's the time signature， harmonics， vocals， genre， time periods。

 instrumentation， language， tons and tons of different dimensions about what any given track is really about under the hood。

 And so if you understand those genes， the things that make up the attributes of music that you're listening to。

 you can really identify what are similar tracks， what are similar artists。

 And this becomes the basis of something in recommender systems called a content-based recommendation strategy。

 It's really great for a cold start scenario where you don't have interactions with users yet。

 You're just trying to get things off the ground。 And so this first strategy was tremendously successful and is really what made Pandora get off the ground。

 On top of that， the Music Genes are really interesting and are fun。

 It's fun to look at something that you're listening to and you didn't even know that there were。

 only kind of the twangy harmonics or nasal， male vocals or something like that。

 So it's really fun just to look at each piece of music and look at the things that you enjoy yourself。

 Even to today， the Music Genome Project is a tremendous data asset and we're continuing to find new。

 innovative ways to leverage it every day。 It's like the music DNA discovered there。

 And I also liked how you talked about the cold start scenario。

 That's a really important term for people to understand as they're looking at different projects when they're starting。

 So kind of drilling down even more into your recommendation in Pandora。

 personalization has been a major focus of customer experience from the beginning when Pandora was able to allow listeners to indicate their likes and dislikes with the unique。

 you know， thumb up， thumb down。 So how does your team utilize this continuous feedback loop and why have listeners been able to continue to enjoy the Pandora platform given that it was started at this technology。

 it started 15 years ago， which is quite remarkable。 Yeah， yeah。 So as I mentioned。

 the Music Genome Project really enabled the first round of content based strategies for the recommender system。

 But after people start using a product and actually listening。

 providing implicit and explicit feedback， that's really the next source of， you know， digital gold。

 I'd say。 You know， listener feedback data really enables the next generation of recommender strategies。

 So there are a few other broad categories of strategies in recommender systems。

 We talked about content based strategies。 User based strategies are things like， you know。

 people like you also like this other thing。 And so you can。

 you can explain and learn based on what people do and discover hidden similarities between content and preferences。

 There are also strategies called collaborative filtering strategies where you simultaneously look at which listeners are similar。

 which content is similar， and you kind of do that all at the same time。 So that flywheel。

 once you get it going， is extremely powerful。 The thumbs， you know， as you mentioned。

 thumbs up and thumbs down are very explicit signals about a track that a listener liked or didn't like on a particular station。

 And that framework is super powerful for us。 On an individual level。

 it lets people personalize their own stations， steers it towards their own tastes。 But in aggregate。

 there's something even more powerful going on。 So thumbs form a labeled training set， you know。

 about which tracks are successful on which stations。 So in general。

 this is where machine learning really comes in。 This is a。

 similarly to a supervised learning problem where you really have labeled data。

 You know which tracks have in aggregate been successful on each different station。

 So beyond those generalities， you know， we've also had improvements in content based strategies since the beginning。

 We've had improvements in metadata， both at the ingestion layer as well as using machine learning to learn and identify similarities between disparate sources of metadata。

 So you probably， you know， back in the day had your own Napster account where you download 10 different versions of the same track。

 all with slightly different artists names and slightly different durations。

 We need to use machine learning to actually identify that those are the same track in fact。

 And beyond that， the music， you know， project's been going for 20 years。

 And so we have about 2 million tracks that have been human analyzed in that project。

 but we have tens of millions of tracks that listeners can play every day。

 So how do we take the best of what humans have and the best I for those genes and scale it up to a much。

 much， much larger catalog。 So we have a phrase that we talk about a lot， humans for quality。

 machines for scale。 So one of the things that we do is we've developed a system called the machine listening system。

 where a model listens directly to the audio of different songs。

 Songs in the back catalog songs that are new when they come in。

 And given the label training data we have from the music genome project。

 we can predict a lot of those attributes about new music that none of the humans internally have ever listened to。

 And so collectively when you put all these different techniques together。

 we can power algorithmic radio stations， starting from over 30 million different sources。

 Could you potentially walk us through various ways your teams use machine learning for three distinct stakeholders because our listeners or viewers would be interested in this。

 One would be marketing and advertisers。 So that's one stakeholder。

 The other one would be the song creators and the podcasters that you guys also serve as well。

 And then I can't leave out people like me， the listener。

 So if you could just maybe give us a little bit of an example。

 maybe across those different stakeholders and how you guys use machine learning for that。 Yeah。

 absolutely。 So advertising and marketing are， we bucket them together often because they're very business focused concerns。

 but there are different use cases in there。 So when we think about marketing。

 one of the great things that we do is think about how do we upsell somebody on subscription。 So。

 and we call that smart conversions。 How do we look at the behavior that you're doing in the app at any point in time？

 Who are the right people to target upsells to when is the right time to do it？

 Should we be including any kind of promotions at the same time？

 And we build machine learning models to maximize the effectiveness of those interventions。

 Similarly， for push and email campaigns， what is the right design layout？

 What are the right subjects？ Where are the right topics？

 If you send somebody an email and they're saying， come back in， listen to this artist。

 we want to find the best， the best artist for that person。

 So we need to use recommendations inside the content itself。 And then lastly， for advertising。

 one of the things that we spend a lot of time researching is how effective are our ads。

 And we're out there in the market every day selling ads to businesses。

 And we need to prove that actually they deliver value。

 So can we use tools internal to the system like surveys and validation to model and learn how effective our ads are in different contexts？

 Yeah， for creators， creators and listeners form a nice sort of marketplace around recommendations。

 So on one hand， creators really want to find who is my target audience？ Who's going to love me？

 I've got a message that I want to get out there。 So we help a lot of creators。

 especially creators that are yet to be discovered or newer to the marketplace。

 identify the listeners that are going to be most interested in their content。

 So that's one kind of recommendation。 The other kind of recommendation is， alright。

 you're a listener。 I want to find stuff that is best for you。 And really。

 machine learning is used everywhere in the listener-facing system。 So radio。

 the next song that will come up next is machine learning based。

 Your home screen that we call for you is trying to help you discover new things based on machine learning。

 Search， voice， natural language understanding， getting inside of talk content like podcasts and live radio。

 All uses machine learning to enhance the listener experience。 It's all around us。 You're here。

 It's constantly made you。 That's good to that。 I think that's great to understand that。

 And then also earlier， when you were giving some examples。

 you talked about implicit and explicit signals。 So we're going to just dive into that just a bit because we talked about gathering the data。

 And as you build the models and train it， you gave the example of explicit and implicit signals。

 So do you just like maybe define those and maybe give one example of how you use both implicit and explicit data in maybe one of those stakeholders。

 examples you just provided？ Yeah， yeah， absolutely。 So。

 I think explicit signals are the easiest things to define。 That's when a listener goes in and says。

 it doesn't have to be a listener， but I'll go through a listener example。

 A listener goes in and says， yes， I really like this a lot。

 That looks something like a thumb up or a thumb down on a radio station。

 or it's adding it to your own personal collection or a favorite so that you can find it again later。

 Implicit signals are， they're less specific about what a listener's intent is。

 So do you complete a track？ How long are you listening to the same station？

 Did you click through a recommendation and read an artist's description and bio？

 So all of those pieces of information give us an understanding of what are you interested in doing in this app？

 What are your core interests and how can we help you get where you want to go？ So。

 I think at the end of the day， when you're collecting the data， don't throw anything away。

 You want to keep it all。 You want to keep it as well structured as you can。

 You want to think hard about it to make sure that people can discover it going forward。

 When you sit down to try to build a model and build a machine learning model to train it。

 you want to know what you're really trying to do。 Marrying the right data with the right model for the right business use case is the core challenge of a machine learning scientist or engineer or a data scientist。

 It's not just sitting down and tweaking with some parameters and training a model。

 It's really identifying what is meaningful in this data。 So， for example。

 I talked about thumbs before。 How do we use that in radio？ How do we use it for machine learning？

 And so what metrics do we care a lot about when you listen to a radio station？

 One thing is definitely how long you listen to it， but that's kind of hard to predict。

 And what am I even going to do with that in the system if I know you're going to listen to something for a long time？

 A much more actionable thing to predict is what's the probability that if you were to give a thumb on this song right now that it would be up or down？

 And then my job as a record system is to provide you lots of songs on the station。

 I think you are going to thumb up。 So those explicit signals like thumbs become the label training set that we can identify features。

 We can do error analysis to identify which things do we think we're going to be thumbs up but actually got thumbs down。

 So there's a whole lot of work that goes into the pipeline end to end。

 And then the kind of last step out the door is once you've developed a model。

 once you think that you have something that's going to work， you've got to test it。

 You've got to see if it really works。 So we do offline analysis against our production logs。

 But we also do the experiments in the app directly all the time every day。

 And we use other causal inference techniques to learn the best way to evolve the system。 Wow。

 that was the thank you for adding in the testing into the to the answer of the implicit and explicit signals。

 It also leads us now to the next area because you focus a lot on the data and how important the data is and the questions and testing。

 But let's talk just a little bit about the model and specifically around how you know company how do you how do companies choose accurate models and balance。

 you know， accuracy versus explainability。 And specifically， in your role at pandemic Pandora is our。

 how do they value both of these objectives or the value of simultaneously。

 Do they see them differently， you know， separate。 If you just talk a little bit about that accuracy。

 explainability， especially in light of like， you just gave us all this great information about you have to do your data。

 So， maybe you could tell us how you approach those two terms in models。 Yeah， yeah， like。

 like all fun things。 It's not one size fits all。 So it depends a lot exactly on what you're trying to do。

 I would say that there are a couple important things to think about early on。 It's， you know。

 what is the task。 So is it the kind of thing where making a mistake is very costly。

 or is it the kind of thing where， you know， it's all right。 If。

 if there's some flexibility in how accurate the prediction is。

 The next is who is the consumer of the model。 What's the level of trust that that person already has in the system。

 And what investment are they willing to make to have a relationship with it。 So， for example。

 on our for you， and the nation page， we think that customers go there to discover new music。

 And you want or new podcasts， new shows， everything like that， new topics。

 And so when when somebody goes there， you want to push the envelope of what's going to be useful and interesting。

 But you also want to make sure that it's explainable because humans。

 when you meet your friend and they say， oh， you've got to try this thing。 Because you like this。

 you're going to like that。 And so you at the end of the day， it's okay to have a model。

 which is going to explore more territory， take some risks， and be able to explain itself。

 When you get deeper into the system， where you have a scientist that's looking at a model trying to make improvements on it every day。

 they probably already have a high level of trust in the system。 They know where it's come from。

 They've tried lots of different things。 They're making a deep investment on what's really going to be powerful。

 And frankly， what's going to be interpretable or explainable to them is going to be different than what's explainable to a listener。

 They have domain specific knowledge about what each technique is good at or bad at。

 So in that situation， you probably are more inclined to take on more complicated models that are less explainable to the general public and then identify and explain reasons after the fact of why a recommendation might be made。

 But absolutely， there isn't a one-size-fits-all answer。

 And there are things that we both think about。 We think about both of those things a lot in many contexts。

 I really appreciate how you tied trust into explainability and what level of explainability。

 You don't have to explain what the data scientists might know。

 but it does have to be explained to a point where the trust is either it's building with the service or company。

 not detracting from it so that you have to go to that level of explainability。 That was that was。

 thank you so much for explaining that。 We talked a little bit about testing in the marketplace。

 A/B testing。 I don't know if there's any other if you want to go into that a bit more。

 if you can explain possibly how AI improves the efficiency of testing for Pandora gives a little insight to that。

 Yeah， so I think the gold standard of knowing that something makes a change is。

 makes an improvement or a detracting your system is using causal inference techniques。

 And A/B tests are a cut and dry way to say， "I made an intervention。

 I have a random sample of people that got one version of our product and I have a random sample of people that got a different version of our product。

"， And there's exactly one difference that you can attribute any ongoing changes to。

 So it's a very clear way to understand that the change that you made actually was the cause of changes in metrics rather than simply correlated with changes in metrics。

 A/B tests are the standard go-to way to make sure that things are actually doing what you want them to do。

 Before going and launching an A/B metric， you want to have some confidence that what you're doing is actually going to be good。

 So we run a lot of experiments， we call them offline experiments。

 They're not run in the product with real listeners or marketers or advertisers or creators。

 They're run against our logs。 So you do things like back tests and analyses to figure out how would this have performed in that situation。

 Because you want to preserve the power of your A/B experiments。

 You want to still be able to do them with large enough samples to identify the differences。

 One step further from A/B tests are a framework called multi-arm bandits where you simultaneously can run multiple experiments。

 So not just A/B but think A/B/C/D/E/F/A。 There's all these different arms。

 And it's adaptive over time。 So you start out by trying to learn a little bit about each of those arms。

 And as you go， the ones that are doing better， you really want to start getting people toward that experience。

 So you balance this explore and exploit trade-off to efficiently learn the differences in your treatments。

 as well as get the best treatment as fast as possible。

 And when doing both A/B testing and the multi-arm bandits。

 are you using the power of AI to help determine exactly which A/B testing parameter you want to do？

 Or is this， I'm just curious how you're using the AI and machine learning to actually choose possibly which multi-arm band and sphere in the A/B testing？

 Yeah， so there are lots of ways to come up with good tests， whether it be A/B or multi-arm bandits。

 Some of them are product intuition， where you might say， "Oh， you know what。

 I just feel like we're introducing too much repetition into the product right now in radio。

 Let me play with this knob， try out a couple different things and see what it's like。"。

 Others are very machine learning driven， where you've identified and you're running things offline first to say。

 "I have a whole suite of hyper parameters that I want to tune。

 I can go and do that against the data that I have。

 But you don't want to take too many experiments that have low likelihoods of success into the product because A。

 you don't want to risk giving people a really bad experience。 But B。

 you need to expose enough listeners to any given treatment to measure the change。

 So the more confident you are that there is an effect means that you're less likely to simply expose people to random variation。

 So you really are able to narrow down exactly the right test that you should bring to the market because again。

 you don't want to。 Also， you're being very careful with that trust and explainability of what you're doing because you really don't want the listener to know that you're also kind of testing some of these things out。

 I mean， you want information and such， but you don't want to damage that relationship。

 So I think that was really great。 So one of the areas you spoke about earlier was search and voice。

 So how do your teams integrate both consumer search and voice requests into the recommendation models and are using more natural language processing in these models？

 Yeah， so search is a really early signal that we can pick up。

 When something in the real world happens， there's an accident that occurs。

 There's a new release of a movie or something like that。

 People are starting to search for soundtracks or specific artists that might be getting married that day。

 And so people will start searching for that before it's a hugely detectable change in overall listening。

 So you can take that as an input， as a trending signal and feed it into the recommendation algorithms to say。

 "Well， I think people want more of this right now。" So that's a useful way to use search。 On voice。

 I think the relationship between our voice science and the recommendations is a little bit different than you think。

 The voice product really drives additional product use cases。 So for example。

 we've seen that people will ask for very thematic queries in voice。 They'll say。

 "Plain me 90s RMB with female vocals。"， And you go， "Wow， how do I even satisfy that request？"。

 You could solve it just directly in search and voice right there and try to identify those kinds of tracks and serve them back to someone。

 Or you could fundamentally look under the hood and say。

 "I need to build radio stations that enable people that kind of flexibility。"。

 And so how does the discoveries that we're seeing in the voice product influence an even broader scientific roadmap is frankly one of the funnest parts of my job？

 I can see why they've combined all these together for your team because they're all interrelated in that regard in terms of the discovery and the innovation。

 So finally， looking to the future， has there been what I'd really like to see is where do you see the combined strengths of both Pandora and SiriusXM for the consumers？

 Yeah， so SiriusXM acquired Pandora a little bit over two years ago。 And from the very beginning。

 they were a great compliment。 SiriusXM is an established leader in audio entertainment in North America。

 It's embedded in the car。 It has a really high margin satellite broadcast business。

 Pandora is famous in the United States in an increasingly competitive digital streaming environment。

 It's personalized。 It's a one-to-one relationship between you and the algorithm and it adapts to exactly who you are。

 Whereas broadcast is one to many。 So you program one station and every single person in America could listen to it。

 So from the beginning， we've always had the idea of how do we cross-pollinate listener experiences by bringing content from one area to another？

 How do we produce better subscription packages？ How do we do better marketing to the people that we know about？

 How do we build platforms for advertising across all of our different products？

 And then on the science side， it's how do we learn from each of these different pieces of data and the expertise that cross the board？

 So definitely playing with all of the feedback data that we get from Pandora and that interaction and working on how do we build similar things into a broadcast experience？

 And in fact， for a new fleet of cars that have started coming out in 2019。

 we actually are starting to get a lot of metrics reported back from them so we can start personalizing experiences directly into the car。

 Oh wow， that's really exciting。 I just bought a new 2018 car， so I'm looking forward to that。 Well。

 thank you so much， Scott。 It's been a pleasure to talk to you and incredibly insightful to learn more about Pandora and how they utilize AI and ML and data specifically that implicit and explicit data that you spoke about in our lives to enjoy more personalized music selection。

 So thank you so very much for joining us today。 Thank you， Mary。 All right。 [BLANK_AUDIO]。

