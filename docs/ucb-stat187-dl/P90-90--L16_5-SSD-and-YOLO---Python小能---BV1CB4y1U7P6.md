# P90：90. L16_5 SSD and YOLO - Python小能 - BV1CB4y1U7P6

 So first let's talk about the SSD。 It's called single-shot， multi-box detections。

 So the idea is pretty simple。 So the major difference between。

 RCN and SSD is that how the bondbox are generated。 In the RCN family， we have a fancy algorithm to。

 how to generate the bondbox so that we want to， have the bondbox cover as much as possible。 For SSD。

 it's much simpler。 So here for SSD for each pixel。

 we can generate multiple bondboxes and center that as this pixel。 The multi-means。

 we give different size， different shape， different ratio。 For example。

 if we give N sizes from S1 to SN and M ratios from R1 to R M。

 So size means the relative size to the original image。 The ratio is the width with height。

 So then the idea here is generate M plus M minus 1 ankle boxes。 So it's not but N times M。

 It's M plus M minus 1。 The way how it generates ankle boxes is first pick the first ratio R1。

 and then change the size for S1 to SN。 So this is for the first N boxes。

 and then we're going to fix S1。 This is the size and then change the ratio from R1 to R1。

 We already have for R2 to RM。 So in total， we have N plus M minus 1。

 The reason why we don't want to do N plus M， which means given any shape， any size and any ratio。

 we generate one ankle boxes。 That's because it may be giving you too much。

 Like if you pick N equal to 10， M equal to 10， it give you 100 ankle boxes。

 So which means 100 ankle boxes for every pixel。 If it's 100 by 100 image， you get 10K pixels。

 another 10K ankle boxes， then you just run out of memory。 So this is a trade-off。

 We want to vary the size and the ratio， and we generate a linear combination of it。 OK。

 so then the whole model is like this one。 So we first give an image。 We fit into the base network。

 The base network do a feature instruction。 You can choose an SSD， you can choose a rest net。

 you can choose any one as the base network。 Then the base net will be not output。

 A tiny one is kind of give you output like 32 by 32 feature map。 And then given this feature map。

 we generate the ankle boxes。 And for each ankle box， we're going to do a category prediction。

 and a bound box prediction。 The other thing here， we've got multi-box or multi-scale。

 is like the base network give you maybe 32 by 32 feature map。

 And can further have the width and height。 And then on the reduced the feature map。

 I'm going to generate another bunch of ankle boxes。

 and then do another category prediction and a bound box， prediction。 I do multiple times。

 So the basic idea here， the bottom， which， is the output of the base network。

 the feature map is still， large。 So I can generate small ankle boxes to catch up the small objects。

 And in the top， every time we reduce the width and height， of the feature map。

 and we generate slightly larger ankle， boxes。 So we can try to catch up larger objects here。

 So the major difference here that we， don't need to predict how the ankle boxes are they。

 And then for each pixel， we just generate a bunch of them。 So that makes the pipeline much easier。

 Question。 So we're no longer learning like the aspect of the show。 I mean。

 or the size instead we're just， having these different level scales and just change the， growth。

 Or I mean， we just have different s， y， and r1。 Yes。

 so the thing that we don't have a linear algorithm to， predict the ankle box。

 we just have to pick up the different， s1 and r1 so that we can catch up all these different。

 shapes。 So these hyperparameters。 So we can show you that how usually we pick up the hyper。

 parameters。 But then you see that there's a lot of overlapping。 That's true。

 We can see how to make the classifier and the predictor， much efficient to handle all the things。

 So that's SST。 Another one。 So you can see this is the SST performance。

 The x-axis is the throughput， number of， mh per second。 The y is the accuracy， you can think about。

 So we can go up to the right corner， the better。 So you can see that SSC much faster can point out fast as。

 the yellow ones compared to the blue one。 Well， the accuracy is OK。 Like SST is two。

 three years ago， or two， three years ago， algorithm。

 So you'll always see we cannot show you a little bit of， leather。 This is last year。

 So SST at that time outperformed fast-dossy and， family a lot on speed。

 But they sacrificed accuracy， but people still use it at， that time。

 especially when they're faster inference。 Question？ [INAUDIBLE]， [INAUDIBLE]， Well， I'm both。

 We can talk about what is map a leather。 OK。

![](img/05fab0db4e7a87b062198d26472634f4_1.png)

 So another one is the yellow one。 No， the green one。 It's called a yellow。 You only look one。

 This is kind of front UW。

![](img/05fab0db4e7a87b062198d26472634f4_3.png)

 The idea is pretty simple。 We were not diving deeper into that family。 The idea is like on SST。

 all these anchor boxes just， are highly overlapped。 For each pixel， nearby pixels。

 we generate a bunch of， anchor boxes almost like they are going to overlap。 For you law。

 we don't want so much overlapped anchor， boxes。 What it does is like， give an input image。

 give an input， feature map。 I can't even divide it by S rows and by S colors， which。

 you generate as times S， like anchor boxes。 So everyone's not overlapped。

 Then for each anchor boxes， we can predict the B boundary， boxes。

 because we reduced a lot of the anchor box。 And we have maybe have more boundary boxes。

 But then for each anchor box， we can predict the B。 Usually you want it to one boundary boxes。

 So that's a basic idea。 That's why you only look for one。 That is。

 the anchor boxes will be not overlapped。 I will not go to the detail about--， you will have a V2。

 have V3。 Basically， you will be once very different to SST， but V2， very close to SST。

 Fast-out C and all these families very close to each other。 And how to do prediction。

 how to do class prediction， how to do boundary box prediction， they're very close to each other。

 And V3 added another tiny improvement。 But the basic idea， it'll make it faster。

 So you can see that the u-lock， the green one， up to the right one， which is， I think， two times。

 maybe 1， to 0。2 times 1。5 times faster than the tiny SST。 But we can improve that course a lot。



![](img/05fab0db4e7a87b062198d26472634f4_5.png)

 Okay。