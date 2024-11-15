# P32：32. L7_4 Dropout - Python小能 - BV1CB4y1U7P6

 The last thing is called job out。 It's pretty popular like four years ago。 But nowadays。 we know that how it works and。

![](img/defc3a1b12b8631f55c631a8baabe4cc_1.png)

 how when we can apply job out。 The ideas like a good model should be。 robust to changes on the inputs。 So for example， you can recognize the object on the image。 you change the angle， change the light， change anything you should still recommend this image。 For example， for this figure， you still recognize what it is。





![](img/defc3a1b12b8631f55c631a8baabe4cc_3.png)

 no matter how many noises add into that。 So a long time ago， people already know that you can add a。 noise to the training data。 This is equivalent to adding a regularization to the loss， function。 But the idea of job out is like， because you have new， networks， you have multiple layers。 job out adding noises to the internal layers。 No adjust to the input。 In particular。

 if x is the output of a particular layer。

![](img/defc3a1b12b8631f55c631a8baabe4cc_5.png)

 then job out to get x prime， which is such that the， expectation of x prime is equal to x。 So we add the noise to x prime， but we don't change the， expectation at the least。 You have a motivate to do that。 In particularly， job out doing is that you choose a， probability p。 or we can't call it a job out probability， then with probability p， we set xi into 0。 Otherwise。

 we keep xi value， but divided by 1 minus p， so， that the expectation still doesn't change the expectation。 OK？ Now， how apply job out？



![](img/defc3a1b12b8631f55c631a8baabe4cc_7.png)

 Job out usually applies to the output of a， hint of fully connected layer。 So we only talk about fully connected layer yet。 So we're going to talk about different layers after that。 But job out usually is only applied to， fully connected layers。 The reason is because fully。 connected layer is the layer has the most of the， modal capacities between all the layers we cannot talk about。

 in the latter。 So that for these particular layers， we can apply job out。 as a regression to the layer。 In particular， what it works is like if edge， it's the。 output of a hint of layer， which means we try W， weight， plus bias， and apply the activation。 then we apply， job out to edge， to catch edge prime。 Then edge prime is fitting to the next layer。

 So if you talk about the example here， the internal， layer we have five how puts edge 1 to edge 5。 If we apply job out， we may likely to just set edge 2 and， edge 5 to be 0。 So which means we remove edge 1 and edge 5 values to the， next layer。 And we scale the rest of 3。 So we take on expectation we didn't change anything。 So then job out is probably--。

 it's not every time-- so every time we train， we run a， fault path， we actually apply job out。 which means every， time the one you drop out is different。 So you don't do the job out that first and the fix all， the things。 then you permanently lose edge 2 and edge 5。 So every time we drop different nodes。

 Any questions so far？



![](img/defc3a1b12b8631f55c631a8baabe4cc_9.png)

 So job-file is a regularization。 During inference， we should don't apply regularization。 because regularization makes the training because it's only。 useful to limit the choice of the weight during training。 During inference。 job-file is just a return that you put a， value。 So that is during inference and during training that we had。

 different behaviors。 So you can still apply job out， but in inference， we。 prefer have deterministic results。 So we don't do anything in inference。 Questions so far？





![](img/defc3a1b12b8631f55c631a8baabe4cc_11.png)

 Good。