# P80：80. L14_7 Multi-Machine Training - Python小能 - BV1CB4y1U7P6

 Okay， so let's move to single machine multi-gpues to multi-mushings with multiple GPUs。

 So this is a pretty cheap GPU cluster Alex has like four years ago。

 The case take $40 and we bought CPUs from Facebook。 Facebook have data center。 They can。

 every year they're gonna， the old CPUs， they don't need any more sale on eBay， for 20 bucks。

 So we bought like， we like a chocolate and it's pretty like 200 bucks and 10 chocolate。

 Then we bought a very cheap motherboard and very cheap one。 So this is a pretty cheap cluster。

 The whole cluster have 16 machines。 Only maybe take 20。

000 boxes and we might leave a bit of coin at that time and pay all this， cost。 And that's， you know。

 that's like four years ago。 Nowadays you cannot get any benefit anymore。



![](img/011d1a4d9c701bd7328d99ae7116d547_1.png)

 Okay， so that's a single GPU or multi-GPU single machine。

 And then to multi-mushings what do we do here？ We probably assume that data is on a distributed file system。

 On a shared file system or like on anything you can， every machine can access。

 Then we have multiple machines。 Each machine have multiple GPUs here。

 And the parameters may be not on a single machine anymore。 It's maybe cross。

 we can split the parameters and the cross to different machines。 So here， for example。

 if I use a rest net， if you use the rest of 50， we have 50 layers。 We maybe just four machines。

 Each machine maybe take just 12 layers。 So each machine get a part of the model。

 Then we're going to read data through the network and also send and push the gradients。

 across the network we have。 Okay， that's only， but for the others。

 pretty similar to a single machine， multi-GPU training。 Remember that we have maybe hierarchy here。

 So the GPU communication with the single machine is pretty fast。 So here， for PCIe。

 you have 63 gigabyte per second GPU with the single machine。

 Then GPU to CPU to local CPU is the lowest， 16 gigabyte per second。

 But machine to machines are pretty slow。 Here， it's maybe my PhD defense three years ago。

 it's kind of 1。25 gigabytes per second。 You can see that for local GPU to CPU， GPU to CPU。

 and CPU to remote CPU， every time it's， like a 10-time reduce of the bandwidth we have。

 So we need to care about all the hierarchy。 So what we can do here， we run locally。

 we just store the parameters on GPUs and the， communicated GPUs and then aggregate the gradients across all the GPUs and send out to the remote。

 CPUs。 So that's the only thing we can get。 So we can think about these parameters。

 we call the primary server and these kinds of key， values store， we have two levels here。 Okay。

 Any questions so far？ Okay。 It's too hard？ >> Actually， just out of curiosity。

 I imagine that with a multi-machine setup， that is very， unlikely for something to go wrong。 Say。

 like a GPU brings out or computer disk gets shut down。 >> Yeah。

 >> I give math to this kind of situation and stuff with the CPU。 So yes。

 like I didn't put a picture here。 So we have to go back a little bit。



![](img/011d1a4d9c701bd7328d99ae7116d547_3.png)

 So this is a machine room， like just the office soon in this building， but it's an SEMU。

 Then the multi-machine's there， the GPU eats a lot of power， like it's cheap， like 2- to， 300 watt。

 And before NEPs， everybody running experiments， everybody running full time， all the GPUs are。

 using full powers， then we are out of power， which means the whole building is out of power。

 And it's just one day for NEPs， everybody running experiments and the rush for the paper。

 the guy who did a checkpoint frequently submitted the paper。

 The guy who didn't save the result frequently， nothing's left。 So yes。

 you're going to see that GPU may burn out， like CPU is less stable than CPU。

 A GPU is less stable than CPU's。 And this data is better。

 especially on class and we use server grid GPUs。 You torrid more high temperatures。

 but here we use consumer GPUs。 It's pretty easy to get broken。 From systems back， yes。

 we have a lot of things to deal with all these four columns。 With one machine style。

 we can move the workload to another machine， but the best choices， like。

 you do checkpoint for every APOC。 Therefore， every two minutes you checkpoint the result and if something goes wrong。

 it's， just a restart from the latest checkpoint。 Okay。

 let's show exactly how the iterating runs or multi-mushings。



![](img/011d1a4d9c701bd7328d99ae7116d547_5.png)

 So here， assume we have two workers。 Again， this is single batch。 If you have 100 examples。

 every machine we get 50 examples here。 Then， as before。

 we need further partition into two parts and to copy to each GPU。

 So each GPU gets still like 25 examples for each GPU。 Similarly， on the primary server。

 we first copy the parameters into each machine and each， machine further copy to each GPU。

 So we have two levels here。 Remember that。 So each GPU now gets the part of data。

 gets the whole parameters， will compute the part， of the gradients for the green boxes。 Then。

 we found the gradients over all GPUs in the single machine。 That's what we did before。 Then。

 every machine gonna push the gradients out to the remote machine to update。 Finally。

 every parameters can update this parameter here。 Okay， so that is the whole loop。

 The only difference here， we have two hierarchy here， we first do locally and then do remotely。

 The reason we gonna sum the gradients on the machine first， because if gradients 100 megabyte。

 you send GPU by GPU， you have two GPUs gonna send 200 megabytes。 If you sum the gradient together。

 you only get 100 megabyte。 That's the only reason。 That is what we called synchronize。gd。

 So synchronize。gd means every work around synchronously。 Every batch。

 every GPU runs the same workload and the start and stop at the same time。

 And we assume on GPUs and each GPU can process big examples per time， then synchronize。gd equals。

 to just the normal mid batch。gd with batch size n times b。

 So which means usually if fixed n times b， no matter how many GPUs we have， we always。

 get the same convergence result as just a single GPU。 Okay， that's a benefit of synchronize。gd。

 In the ideal case that， well， if we gonna train n GPUs， we gonna lead to n times speed。

 up comparing to single GPU。 But you need to pay a lot of overhead data communications。

 a lot of things we have。 We already showed that。 Then for performance。

 let's talk a little bit about more performance。 So we have two kinds of major things here。

 The first one is called T1。 It's a time to compute the gradients for big examples in each GPU。

 So it's a time we spend on computing， which is compute the fault path and the backward， path。

 So then assume the prime to have m prime meters。 The worker will send the recieve。

 send the gradients and receive the prime meters at each， batch。

 So T2 is the time to send and receive 2m prime meters over the network。 So then the wartime。

 which is the real time we pay for each batch equals the max of T1， and T2。

 And this applied to send single GPU， single machine model GPU training and multi-machine。

 training as well。 So we showed that for non-net T1 is pretty small because pretty computing the small non-net。

 pretty fast。 But communicating is relatively bigger than T1。

 So which means it's communication per minute。 So well。

 what we can do here that we can increase B or N that we can get the logic batch， size。

 And then the good thing here， no matter the batch size we have， we always send and receive。

 the same amount of data。 So T2 doesn't change。 T2 is not related to the batch size we have。

 So we can always increase the batch size B so that T1 is a bit larger。 So if T1 is larger。

 then we almost get the linear speed up here。 But we see that if we can increase the B or N。

 we get to a very large batch size。 We maybe get the network from how to train。

 which means we can pay more data epochs to， get the desired accuracy we want。

 So here we're going to show a picture here。 This is batch size per GPU。

 assuming we fixed the number of GPUs and why the higher the better， the lowest words。

 First you can see the blue line， which is a trainee efficiency， which is the number of。

 the epochs to stop。 If we increase the batch size。

 we probably need more data epoch to reach out to the final， model。 And the blue， the yellow line。

 which is system performance， because every time we increase， the batch size， the T2 doesn't change。

 but the increase the T1 so we just hide all this， data communication overhead。

 which means it's good for system performance。 It's better to get a linear speed up or perfect speed up。

 So the optimal choice is usually a trade-off between two things。 Okay， question？

 >> Is the previous line， does T1 and T2 happen in parallel？ >> Yes， they happen parallel。

 So that's why the water is max of T1 and T2， not the T1 plus T2。

 >> But how does it happen in parallel？ >> You need the parameters first and then you need to compute the gradient。

 >> Okay， so that's a good question。 Remember that before we have computed 10 major multiplication and sent to CPU。

 We can parallelize that because what's the first time one's finished， I sent data and。

 at the same time it can be the second one， sent the second one。 So it can run in parallel。

 So in like a data pipeline for that。 Okay。 So there's a lot of practical suggestions to using multi-GPU or multi-machine training。

 Firstly， you need a larger data set。 You don't use M-list。

 If the training or single GPU takes two minutes to finish， then it's hard to scale up to multi-GPUs。

 So if you're going to try and see for 10 and multi-GPUs， well， you're going to pay the。

 machine to machine communication overhead that's going to dominate that。 Secondly， for the hardware。

 you're going to choose the hardware， have good GPU and machine， to machine batteries。

 If you use Cloud， you don't need to match that because the Cloud provider usually takes。

 care of that for you。 But you're going to do things locally。 For example， what we。

 Alex and I did at the CPU that we first bought a general motherboard。

 and find like a cheaper motherboard doesn't have very good GPU communications。

 And then we like spend a week for another one and replace it one by one。 After that。

 we find machine to machine communication is not good enough。

 You're going to buy a lot of switch to connect a lot of things。 That other。

 if you can solve the things from the hardware， you don't need to matter too， much on the software。

 It's like a must。 I need to worry about that less。

 The third one is usually people don't pay too much attention to that。

 Well if you increase the number of GPUs， the CPU slides not so fast enough。

 If you load a lot of GPUs in a single box， the CPU is going to be the bottleneck。

 Especially we're going to talk about a few minutes later and let me see if we have time。

 Later we're going to show that the data loading and data preparing take a lot of CPU cycle。

 Which means you are not fast enough to generate the data to fit into the network。

 Which means the bottleneck is on CPU。 So you need to benchmark how many images you can process per second and compare to the。

 how many images and gradients you can compute on the GPUs。

 And also you're going to pick up a good model that is have good communication overhead。

 This is a computation。 The flop we talked about before versus communication overhead。

 The communication overhead is the model size。 So the primitives we have。 For example。

 in septune it's pretty good。 Higher flops but the model size is pretty small like a 10 megabyte。

 Restonat is okay。 Restonat 50 has 550 megabyte data and it's okay but it's a little less than 0。2。

 Alex and I are the worst。 Alex and I have a lot of dense layers at the end which takes you 700 megabytes the model。

 Which is tens larger than the rest of the data in septune。

 But Alex and I are tended faster than restonat。 Which means the communication versus computational ratio。

 Alex and I are 100 times worse comparing to restonat。 Unfortunately， the system community。

 the system research communities benchmark Alexnet。 Because it's pretty hard to workload。

 Like you have so many things to stand and but it's not so fast。

 The system community is saying oh that's a great thing。 That's a hard problem we can solve it。

 We can do extremely fast network communications。 We can design chips for that。

 Sun chips for dense layers。 Sun chips for convolution layers that spend three years on that。

 That is because NVIDIA always use Alexnet as a benchmark to show our new GPUs is like。

 runs two times faster on Alexnet。 But they don't know that the computer vision community have been using Alexnet for four。

 years。 Sorry about that。 So the chip vendors spend a lot of time to optimize Alexnet。

 They put their heart then nobody use that anymore。 Okay， so if you choose the hardware。

 choose data set， choose a network then you're going， to choose the NUNI rate。

 Are you going to choose the optimization methods？ You want to use a launch in a lot of batch size and to good system performance and also。

 you want to。 Well because launch batch size can be made to train much slower we have a lot of tricks。

 to do that。 We may not talk about it in this class but usually we can up to maybe a thousand maybe。

 tens thousand of batch size without decreased training performance。

 A lot of tricks to do that like linear rhythm warm up a lot of fancy tricks to do that。 That's all。

 Yeah， so for example performance， logic data set， good hardware， data is really so fast。

 and good model， good optimization method， you need a lot of things。

 So if the performance is not so great you can debugging by this order as well。 Okay。

 any questions so far？ Okay， let's see if you have the result already。 Well。

 you can see that we use the rest net。 We first use a single GPU batch size， it will be a large。

 this small rest net we can use， a large batch size， 0。1 linear weight。 Each epoch takes 60 seconds。

 the accuracy is here and we change to two GPUs double the， batch size， double the linear rate。

 You can see that the speed up is almost two times the speed up here。 That's because this each epoch。

 each batch maybe takes like 0。1 seconds and we can run， two parallelism within the batch size。

 So this is a reasonable workload。 If the whole data epoch take two seconds it's too hard to optimize。

 And the test accuracy is not compatible actually so it is a little bit faster at the end but。

 here almost compatible but not too much。 In general C410 still small data set。

 you can still tune a little bit but usually multi-GPU， on C410 you can get good speed up here。



![](img/011d1a4d9c701bd7328d99ae7116d547_7.png)

 [BLANK_AUDIO]。