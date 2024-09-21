# 沃顿商学院《AI For Business（AI用于商业：AI基础／市场营销+财务／人力／管理）》（中英字幕） - P6：5_数据管理基础设施.zh_en - GPT中英字幕课程资源 - BV1Ju4y157dK

 Welcome back。 In this session， we're going to talk about the data infrastructure that。



![](img/ee2fe5e50c30d22f9d3bef2c5159f79f_1.png)

 companies need to have in place before they can embark on large-scale AI-driven business。

 transformation。 To help us understand what kinds of data infrastructure companies need。

 to have in place， we have with us Chris Child， who is the Director of Product Management。

 at Snowflake。 Chris， welcome。 And please tell us a little bit about your background in， this space。

 Thanks， Karthik。 Excited to be here。 So， as you mentioned， I work at Snowflake， Computing。

 which is a cloud data warehouse company。 And I've spent my career working， in data。

 both as an investor and now as an operator， helping build systems that help。

 companies make better decisions and really run their businesses better。 So， Chris， I。

 think a good place for us to begin is to talk about， you know， what exactly is the database。

 and how exactly are companies thinking about all the different kinds of databases？ What。

 has been that evolution over the last several years？ Sure。 So， there's really two types。

 of databases that most companies end up needing。 The first is what we call a transactional。

 database。 And this is a system that keeps track of the important information that's。

 kind of running your business on a day-to-day basis。 So， if we take in a bank， for example。

 a bank would have a transactional database that keeps track of the balances for all the， customers。

 And you would use that every time someone starts a transaction to figure out。

 if there's enough money in their account to debit their account or credit their account。

 and keep the running balance going on。 These are very useful and they need to be very fast。

 They tend to be very expensive。 On the other hand， you end up with what's called an analytic。

 database or an analytic system to process much， much larger sets of data over a long。

 period of time。 So， continuing with the bank example， I might want to keep a history of。

 every transaction and every balance that each of my customers has ever had。 It'll be。

 very expensive to keep this in my transactional database。 So， I move that data to a separate。

 database to an analytic database where I can keep these massive long histories。 And there。

 I can ask questions like， "I'd like a list of all of my customers who's balanced grew。

 by at least 10% in four of the last five years。 My transactional database won't be able。

 to answer that， but my analytical database will。" So， the transition to analytics databases。

 clearly would involve investments in infrastructure。 What kind of infrastructure are we talking。

 about？ Yeah， so when you originally set up a data warehouse or an analytics database。

 you needed to buy a special hardware。 You needed to buy very expensive special software。

 from a variety of different vendors。 And again， we're talking about 20， 30 years ago， this。

 sort of where this methodology of storing your data came into play。 And so， as the。

 amount of data that people were collecting from lots of different sources， whether that。

 be from mobile apps， from websites， from marketing campaigns， or even from data you're collecting。

 physically in your stores about what's happening， or from your entire supply chain。 There's。

 a lot of different sources of data that started coming in。 Those types of specialized analytics。

 databases that ran on special hardware started to become very expensive to operate and started。

 not really being able to keep up with the performance needs of that massive amount of， data。 And so。

 this time we went through sort of the first big evolution of this。 And from。

 these custom built specialized analytics data warehouses， the massive amount of data started。

 getting stored in a new system called Hadoop。 Hadoop was developed by Google to process the。

 massive amounts of web data that they collect and track， and was also designed to run on。

 a giant network of very inexpensive hardware。 So instead of these specialized， very expensive。

 servers， you could run on hundreds of very cheap servers。 And the result was this was。

 a much more cost effective way to manage and process these massive， massive amounts of， data。 Now。

 isn't that really what creating a data lake all about and also aren't we in a process。

 of seeing many companies transition to newer big data tools or technologies like Spark， and others？

 Absolutely。 So the data lake is what people used to refer to the basically massive sets。

 of hard drives that they're storing all of this data in。 So it's a place you can pour。

 huge amounts of data like a lake， and then you can use tools like Hadoop or now Spark。

 which is a much more modern version of the Hadoop computation engine to pull data out， of that lake。

 run some calculations and transformations on it， and then put it back so that you can。

 find it later。 And traditionally what we saw is once people would sort of finish all those。

 calculations， they wanted to be able to query that data very quickly。 And so they would end。

 up putting that into those data warehouses that they were using originally。 Now they started。

 to refer those as data marts， which was where a small set of your customers or of your internal。

 users could go get a subset of the data。 But in order to get a new data set loaded， you。

 had to go back and write Hadoop or Spark jobs to get that data transformed and loaded into。

 those data marts or data warehouses。 For those of you who are not familiar， Hadoop and Spark。

 these are techniques for storing， and processing large amounts of data and essentially they involve distributed storage。

 distributed processing of the data and creating a lot of parallelization which helps their。

 data processing to happen faster。 Now coming back， Chris。

 we've also now seen a transition towards cloud data warehousing。

 So can you set up what exactly is a data warehouse？

 How does it fit in within this whole conversation。

 of companies moving their data to data lakes and data marts？ Absolutely。

 So a lot of people found that with these data lakes and data marts， it was。

 still hard to keep track of all of your data。 It was in different places that were massive。

 amounts of it。 It was an inconsistent format。 And accessing it often involved having your。

 engineering team actually write code that could run on these large parallelized systems。

 And so about 10 years ago， a lot of research started happening into what are now called。

 cloud data warehouses。 These are systems from Amazon or Google or from Snowflake， which are。

 a reimagining of the traditional data warehouse。 They're designed to run on massively parallel。

 sets of inexpensive hardware， just like Hadoop。 Generally， they're run on hardware that you。

 rent from cloud providers like Amazon or Google or Microsoft instead of having to manage those。

 servers yourself。 But from the outside， they look and operate and have the performance。

 of a traditional data warehouse。 So what that means is they use a language to speak to them。

 called SQL， which is what the data warehouses and databases use。 This means you can natively。

 use Tableau or looker or other sort of analytics and BI tools right on top of them。 Because。

 they use that standard language， they also integrate well with large sets of tools。 So。

 as we were talking a little bit about before， what you really want from your data platform。

 overall is somewhere to store all of this data， you need a set of ingest tools。 So how do you。

 get the data into your data platform？ And being SQL based， you can use any of a wide variety。

 of tools that are built specifically for that。 You then need a set of transformations to。

 take the raw data that's coming in and turn it into something useful。 And as I'm sure you've。

 talking about in this class， one of those techniques is machine learning that you can。

 use to take this raw data and score it and make predictions and figure out what's going， to happen。

 But there's also simple things like， I might be getting data about the set of actions。

 a user is taking on a daily basis。 And really， I want to look at that on a monthly basis。

 So one transformation would be just rolling that up to a monthly basis。 And then the final。

 piece you need is a query and visualization engine。 As we mentioned Tableau or looker。

 or other tools like that， a way to actually run queries and for your analyst team to build。

 dashboards and basically ask questions of the data once it's sort of been transformed。

 And so one of the big challenges that people had with Hadoop or even with a Spark based。

 ecosystem is that those tools often need to be custom built for that ecosystem。 Whereas。

 if you use a cloud data warehouse， you get high performance， you get the scalability of， Hadoop。

 but you also get access to the standard ecosystem of tools。 So Chris。

 when we started our conversation， I mentioned that before companies can start。

 using machine learning or other predictive technologies， they need to have a data infrastructure。

 in place。 Now putting this data infrastructure in place obviously costs the money and cannot。

 be taken lightly。 So what questions should a manager ask before they embark on such an， exercise？

 Absolutely。 So one of the mistakes that I've seen people make repeatedly is to think that。

 having this data infrastructure in and of itself is an important thing to do。 And so。

 they'll set this up and they'll load a bunch of data and they'll buy a bunch of tools and。

 they won't actually get any value out of it because what they didn't do was think ahead。

 of time about what they were trying to solve， what problems they had that they wanted to。

 solve with data。 So what I would suggest is anyone who's going to undertake this journey。

 think first carefully about the types of questions that you wish you could ask but you can't。

 because you don't have all of the data， the types of questions that you are answering。

 today but it's taking a long time。 An example of that is anything where you ask someone。

 on your team to go spend two weeks collecting data and running analysis in Excel， those are。

 decent candidates for the types of problems that you could solve in minutes if you have。

 the correct data infrastructure in place。 And finally， think about what data you need in。

 order to answer those questions。 It's generally not that useful to go collect every single。

 piece of data you can possibly think of。 Instead， what are the pieces of data that are important。

 to your business and are going to help you answer those critical business questions so。

 that you can run your business better and more efficiently。 It's really at the end of the， day。

 That's the whole goal。 Chris， that has been a very helpful set of tips and overview。

 of the data infrastructure companies need to think through。 Thank you so much for joining， us。

 Thank you， Karthik。 Appreciate it。 Thanks for having me。 [BLANK_AUDIO]。



![](img/ee2fe5e50c30d22f9d3bef2c5159f79f_3.png)