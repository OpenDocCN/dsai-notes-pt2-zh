# P31：Supervised and self-supervised transfer learning (with PyTorch Lightning) - 大佬的迷弟的粉丝 - BV1o5411p7AB

so welcome to class today um today we're，so welcome to class today um today we're。

so welcome to class today um today we're，going to be talking about transfer。

going to be talking about transfer，learning，learning，uh with a supervised and unsupervised。

uh with a supervised and unsupervised，perspective，perspective，uh here today we have william falcon a。

uh here today we have william falcon a，expert，expert，in uh the tools we are going to be using。

in uh the tools we are going to be using，for explaining to you how this stuff。

for explaining to you how this stuff，works，works，which is going to be telling us a little。

which is going to be telling us a little，bit more about，bit more about，this topic okay so william。

this topic okay so william，the floor is yours uh alfredo thank you。

the floor is yours uh alfredo thank you，so much for having me here and excited。

so much for having me here and excited，to，to，share this with the whole class and。

share this with the whole class and，everyone so okay，everyone so okay，today we're going to be doing。

today we're going to be doing，self-supervised and supervised transfer。

self-supervised and supervised transfer，learning so this is going to come up a。

learning so this is going to come up a，lot for people，lot for people。

so if you're working in industry or，so if you're working in industry or，doing any kind of research。

doing any kind of research，you're going to run into something where。

you're going to run into something where，you may not have enough data and you。

you may not have enough data and you，need to have some model that's been。

need to have some model that's been，trained on something，trained on something。

else and then you can use that to kind，else and then you can use that to kind。

of jump start your process right，of jump start your process right。

so we'll cover it in the context of，so we'll cover it in the context of，computer vision today but。

computer vision today but，this can transfer to nlp um speech，this can transfer to nlp um speech。

anything you want learning，anything you want learning，[Laughter]，[Laughter]，okay pun intended。

okay pun intended，and and some domains may not work as，and and some domains may not work as。

well but you know，well but you know，i'm confident that in the next few years。

i'm confident that in the next few years。

![](img/f8f008e2808f19882aa25f551e7c2493_1.png)

i'm sure we'll figure，i'm sure we'll figure，figure out a way to do that so the first。

figure out a way to do that so the first，thing i'm going to do is someone install。

thing i'm going to do is someone install，lightning，lightning，and uh and lightning is a lightweight。

and uh and lightning is a lightweight，and uh and lightning is a lightweight，wrapper for pytorch。

wrapper for pytorch，for high performance research right so，for high performance research right so。

if you're using pytorch，if you're using pytorch，it basically organizes your pytorch code。

it basically organizes your pytorch code，so you can leverage，so you can leverage。

things like multiple gpu training tpus，things like multiple gpu training tpus。

and different things that，and different things that，require a lot of expertise and frankly。

require a lot of expertise and frankly，are things you don't need to deal with。

are things you don't need to deal with，when you're trying to work，when you're trying to work。

on like you know build models and the，on like you know build models and the。

second framework that i'm going to，second framework that i'm going to，install this bolts。

install this bolts，right so bolts is our other framework，right so bolts is our other framework。

and it is for，and it is for，hyper um it is it's like a research，hyper um it is it's like a research。

toolkit basically so i can't find my，toolkit basically so i can't find my，mouse there's okay。

mouse there's okay，um so it's a research toolkit so if you，um so it's a research toolkit so if you。

ever，ever，wondered uh if you're starting something，wondered uh if you're starting something。

well you know it's also used in industry，well you know it's also used in industry，as well but。

as well but，if you're starting a project and you're，if you're starting a project and you're。

looking for a model，looking for a model，and um you don't find one，and um you don't find one。

you can look for in bolts right and then，you can look for in bolts right and then，this will be。

this will be，one maybe possibly one of the latest，one maybe possibly one of the latest。

models but it's already been implemented，models but it's already been implemented，tested，tested。

and documented so that you can start，and documented so that you can start，from a good，from a good。

good spot so you don't have to sit here，good spot so you don't have to sit here。

and try to implement the baseline，and try to implement the baseline。

yourself for three months to see if you，yourself for three months to see if you，get it right。

get it right，um you can just kind of subclass and，um you can just kind of subclass and，build on that。

build on that，and boltz has a pretty robust library of，and boltz has a pretty robust library of。

social supervised learning it's，social supervised learning it's，a lot of stuff that uh you know it's。

a lot of stuff that uh you know it's，personally done in my research as well。

personally done in my research as well，and things that we've implemented from。

and things that we've implemented from，the latest papers，the latest papers。

okay if i would like to learn more about，okay if i would like to learn more about。

these things where can i find more，these things where can i find more。



![](img/f8f008e2808f19882aa25f551e7c2493_3.png)

resources yes you can go to lightning，resources yes you can go to lightning，repo，repo。



![](img/f8f008e2808f19882aa25f551e7c2493_5.png)

right so this is um，right so this is um，i mean i think probably the easiest。

i mean i think probably the easiest，thing is to go to python lightning dot。

thing is to go to python lightning dot，ai here，ai here，so we have the the landing page there。

so we have the the landing page there，and then we have，and then we have。

everything documentation videos about，everything documentation videos about。

lightning about the team and everything，lightning about the team and everything。



![](img/f8f008e2808f19882aa25f551e7c2493_7.png)

else and then there you can click on，else and then there you can click on，docs，docs。

right and then go straight to the docs，right and then go straight to the docs。

get started here in the lightning in two，get started here in the lightning in two，steps，steps。

read this and at the end of this you，read this and at the end of this you。

should know everything you need to know，should know everything you need to know。

again if you know pytorch this should，again if you know pytorch this should。

take like four minutes to understand，take like four minutes to understand。

um where's the bolt yeah and then bolts，um where's the bolt yeah and then bolts。

is going to be um let's see if we can，is going to be um let's see if we can，have it on，have it on。



![](img/f8f008e2808f19882aa25f551e7c2493_9.png)

the page as well um，the page as well um。

![](img/f8f008e2808f19882aa25f551e7c2493_11.png)

let's see yeah so we have the bolts here，let's see yeah so we have the bolts here。

so you can click on that and then visit，so you can click on that and then visit。

bolts and then this is its own，bolts and then this is its own，documentation as well right。

documentation as well right，so you can click on it look at the，so you can click on it look at the。

introduction guide and then we will walk，introduction guide and then we will walk，you through。

you through，the main ideas about bolts so bolts is a，the main ideas about bolts so bolts is a。

newer project so it is faster moving，newer project so it is faster moving。

um so it will change pretty frequently，um so it will change pretty frequently，uh lightning is。

uh lightning is。

![](img/f8f008e2808f19882aa25f551e7c2493_13.png)

is 1，0 is stable so um you know feel，is 1，0 is stable so um you know feel。

free to use it for whatever you want，free to use it for whatever you want，as well all right okay so。

as well all right okay so，um installing this i believe i'm in a。

um installing this i believe i'm in a。

![](img/f8f008e2808f19882aa25f551e7c2493_15.png)

gpu，gpu，instance um yeah the cool thing is，instance um yeah the cool thing is。



![](img/f8f008e2808f19882aa25f551e7c2493_17.png)

lighting you can actually use tpus and，lighting you can actually use tpus and。

gpus but i'm going to use gpus right now，gpus but i'm going to use gpus right now。

tpus are dodgy sometimes uh，tpus are dodgy sometimes uh，okay so the first thing i want to cover。

okay so the first thing i want to cover，is，is，like when do you want to fine-tune right。

like when do you want to fine-tune right，so，so，i i think that's there are certain。

i i think that's there are certain，things you can ask yourself，things you can ask yourself。

to understand if what you're about to do，to understand if what you're about to do。



![](img/f8f008e2808f19882aa25f551e7c2493_19.png)

is you know it's useful for fine-tuning，is you know it's useful for fine-tuning。

so let me place this image here uh so i，so let me place this image here uh so i。

made a little diagram for everyone，made a little diagram for everyone。

okay okay thanks so let's start with the，okay okay thanks so let's start with the。

green spots right so，green spots right so，i think the first question is do you。

i think the first question is do you，have a lot of data if the answer is yes。

have a lot of data if the answer is yes，then you likely don't need to fine-tune。

then you likely don't need to fine-tune，right now do you also have time and。

right now do you also have time and，computes，computes，right you can have a lot of data but if。

right you can have a lot of data but if，it's super costly to train then uh。

it's super costly to train then uh，you're you're going to want to，you're you're going to want to。

find something pre-trained but if you，find something pre-trained but if you。

have the money and the time and the，have the money and the time and the，compute，compute。

then just go ahead and train on your，then just go ahead and train on your。

data right and when you're done run in，data right and when you're done run in，your test data set。

your test data set，now if you don't have a lot of data then，now if you don't have a lot of data then。

you should try to find a pre-trained，you should try to find a pre-trained，model for your data。

model for your data，that matches your data distribution，that matches your data distribution。

right so this is super important because，right so this is super important because。

most vision models are trained on image，most vision models are trained on image，nets right so。

nets right so，if you want to do something like i don't，if you want to do something like i don't，know。

know，cancer detection or x-rays that that's，cancer detection or x-rays that that's。

unlikely going to transfer，unlikely going to transfer，right because an imagenet you don't have。

right because an imagenet you don't have，that kind of data you also don't have。

that kind of data you also don't have，people right，people right。

um so you have to you have to be mindful，um so you have to you have to be mindful。

of what you're using this for，of what you're using this for，so you know it's not just blindly the。

so you know it's not just blindly the，the magic of the neural network's gonna。

the magic of the neural network's gonna，work，work，and then um so yeah so if you。

and then um so yeah so if you，if you do have something that matches。

if you do have something that matches，that kind of distribution then you can。

that kind of distribution then you can，use a pre-trained model right，use a pre-trained model right。

so when you think about transfer，so when you think about transfer。

learning we have two parts you have the，learning we have two parts you have the。

pre-trained model that was trained on，pre-trained model that was trained on，something else。

something else，and then you have the stuff you're going，and then you have the stuff you're going。

to add on top of that to uh，to add on top of that to uh，to transfer that right and then you can。

to transfer that right and then you can，fine tune in your own data，fine tune in your own data。

uh so this is very important so i would，uh so this is very important so i would，keep this in mind。

keep this in mind。

![](img/f8f008e2808f19882aa25f551e7c2493_21.png)

and um and then and then the next things，and um and then and then the next things，are this right so。

are this right so，then you have two major options you have，then you have two major options you have。

supervised yourself supervised right，supervised yourself supervised right。



![](img/f8f008e2808f19882aa25f551e7c2493_23.png)

so on on a model that was that's，so on on a model that was that's。

pre-trained using supervised training，pre-trained using supervised training。

learning uh was trained likely for，learning uh was trained likely for。

classification so something for imagenet，classification so something for imagenet，for example。

for example，um and by doing that you've introduced，um and by doing that you've introduced。

bias into that model right，bias into that model right，you've you forced it to learn a。

you've you forced it to learn a，representation that is going to make。

representation that is going to make，classification easier，classification easier。

but there's no guarantee that that's，but there's no guarantee that that's。

going to make something like，going to make something like，segmentation or detection or anything。

segmentation or detection or anything，else that's easy，else that's easy。



![](img/f8f008e2808f19882aa25f551e7c2493_25.png)

um and so you want to be mindful of that，um and so you want to be mindful of that，right，right。

so the self-supervised i like i said，so the self-supervised i like i said，it's experimental。

it's experimental，but it might be i might be able to，but it might be i might be able to。

generalize better so it was not trained，generalize better so it was not trained。

for classification which means that，for classification which means that。

if you want to do segmentation or object，if you want to do segmentation or object，detection。

detection，um the representations uh might might，um the representations uh might might。

transfer better，transfer better，so um so that's interesting and then um。

so um so that's interesting and then um，you know they're like i don't know if。

you know they're like i don't know if，you're following the literature probably。

you're following the literature probably，not but there are about，not but there are about。

seven or eight options that you have to，seven or eight options that you have to，do this so。

do this so，amd um moko cpc，amd um moko cpc，pearl simclear byo and suave right so in。

pearl simclear byo and suave right so in，order，order，the latest one is swab um and if you're。

the latest one is swab um and if you're，interested in understanding the。

interested in understanding the，difference between all of these，difference between all of these。



![](img/f8f008e2808f19882aa25f551e7c2493_27.png)

um you know i recently published a paper，um you know i recently published a paper。

with uh with professor cho，with uh with professor cho，um a few months ago and then we wrote。

um a few months ago and then we wrote，this article um，this article um。

kind of going into all the details and，kind of going into all the details and。



![](img/f8f008e2808f19882aa25f551e7c2493_29.png)

how to how to，how to how to，compare all of them and you know what。

compare all of them and you know what，what what the differences are because。

what what the differences are because，they're really not that different um。

they're really not that different um，so i'm going to be using suave for this。

so i'm going to be using suave for this，particular case for our，particular case for our。

self-supervised transfer learning okay，self-supervised transfer learning okay。

um so the first thing is i'm going to，um so the first thing is i'm going to。

the first case that we're going to look，the first case that we're going to look。

at is going to be this supervised，at is going to be this supervised，transfer learning。

transfer learning，so this is likely the case that you're，so this is likely the case that you're。

going to run into an industry most of，going to run into an industry most of，the time，the time。

right so you have a small data set of，right so you have a small data set of，images，images。

and some compute budget and in this case，and some compute budget and in this case。

we're going to pull out a wrestling 50，we're going to pull out a wrestling 50。

right so there are many restaurants 18，right so there are many restaurants 18，50，50。

one whatever 101 152 but，one whatever 101 152 but，50 is kind of like a sweet spot it's not。

50 is kind of like a sweet spot it's not，so big that it's super expensive to。

so big that it's super expensive to，train and，train and，it's not so small that it won't do。

it's not so small that it won't do，anything interesting for you，anything interesting for you。

remember this was pre-trained on，remember this was pre-trained on，imagenet and it was pre-it was。

imagenet and it was pre-it was，pre-trained for classification，pre-trained for classification。

and imagenet is a data set that has a，and imagenet is a data set that has a，thousand categories。

thousand categories，each of them has a thousand images so，each of them has a thousand images so。

it's like one million，it's like one million，uh roughly one million images right so。

uh roughly one million images right so，that's that's why，that's that's why。

it's actually very successful because，it's actually very successful because。

you know this huge amount of，you know this huge amount of，uh data allows us to distill a very uh。

uh data allows us to distill a very uh，a model that has a very good prior in。

a model that has a very good prior in，terms of natural images right because。

terms of natural images right because，it's been like those thousand classic。

it's been like those thousand classic，classes are uh，classes are uh，names of natural like objects。

names of natural like objects，so that's why usually it works quite。

so that's why usually it works quite，well but nevertheless as you pointed out。

well but nevertheless as you pointed out，before，before，if you want to uh use a network for。

if you want to uh use a network for，medical images where，medical images where。

the you know statistics of your images，the you know statistics of your images，are completely。

are completely，different then what they are in an image，different then what they are in an image。

now then is completely like，now then is completely like，hopeless to have you know any kind of。

hopeless to have you know any kind of，decent result，decent result。

nevertheless let's start with what is，nevertheless let's start with what is。

you know commonly done for，you know commonly done for，normal images right yeah so i think um。

normal images right yeah so i think um，i think to start you know we can we're。

i think to start you know we can we're，using this library called torch mission。

using this library called torch mission，right so，right so，by the torch team as well and um in。

by the torch team as well and um in，there we have，there we have。

a bunch of pre-trained models so this，a bunch of pre-trained models so this，one's a restaurant 50。

 um so i'm going，one's a restaurant 50。 um so i'm going，to set this to true，to set this to true。

so i can i can load that model um，so i can i can load that model um。

which is going to download i assume some，which is going to download i assume some，weights，weights。

uh great okay so there are the weights，uh great okay so there are the weights。

and then uh now we can use this to run，and then uh now we can use this to run，predictions right。

predictions right，so let's pretend that our you know data，so let's pretend that our you know data。

set that we will actually care about，set that we will actually care about。

um has 10 classes right and，um has 10 classes right and，those classes are like frog horse。

those classes are like frog horse。

![](img/f8f008e2808f19882aa25f551e7c2493_31.png)

whatever so we，whatever so we，i'm cheating because there's a data set。

i'm cheating because there's a data set，called c410 right so，called c410 right so。



![](img/f8f008e2808f19882aa25f551e7c2493_33.png)

c410 and，c410 and，this data so looks like this right so，this data so looks like this right so。



![](img/f8f008e2808f19882aa25f551e7c2493_35.png)

again，again，there are they're tiny images they're 32，there are they're tiny images they're 32。

by 32 pixels and three channels per，by 32 pixels and three channels per，color，color。

um but you know it's it's a useful toy，um but you know it's it's a useful toy。

data set it's better than numbness，data set it's better than numbness。

um especially because you're using，um especially because you're using。

preacher on an image tonight and like，preacher on an image tonight and like。

i'm pretty sure an image that they're，i'm pretty sure an image that they're。

not a lot of fake digits or handwritten，not a lot of fake digits or handwritten，digits，digits。

so it wouldn't transfer super well but，so it wouldn't transfer super well but。

there are dogs and cats and birds and，there are dogs and cats and birds and，all that stuff so。

all that stuff so，same kind of domain uh sorry same kind，same kind of domain uh sorry same kind。

of category，of category，uh yes great so let's uh let's use that。

uh yes great so let's uh let's use that，guy so we're gonna set up，guy so we're gonna set up。

our our data set right so let's let's，our our data set right so let's let's。



![](img/f8f008e2808f19882aa25f551e7c2493_37.png)

pull in um，pull in um，c part 10 again from torch vision，c part 10 again from torch vision。

yep and then we are going to use，yep and then we are going to use。



![](img/f8f008e2808f19882aa25f551e7c2493_39.png)

these transforms right so um something，these transforms right so um something。

that's useful normally for，that's useful normally for，these cases is to normalize your image。

these cases is to normalize your image，so we're gonna make it，so we're gonna make it。

uh zero mean and then one for standard，uh zero mean and then one for standard。

deviation right so we're going to add，deviation right so we're going to add。

this on here and i'm not going to add it，this on here and i'm not going to add it。

right now because i want to actually，right now because i want to actually，plot the image for you。

plot the image for you。

![](img/f8f008e2808f19882aa25f551e7c2493_41.png)

so you can see what it looks like um so，so you can see what it looks like um so，i，i。

do this and then that will actually，do this and then that will actually。

download i need to import that，download i need to import that，transforms right um here from torch。

transforms right um here from torch，vision import transforms，vision import transforms。

okay so this is going to download，okay so this is going to download，extracts，extracts。

and then we have this data set great so，and then we have this data set great so，that's ready to go。

that's ready to go，so let me just plot it now so i'm just，so let me just plot it now so i'm just。

going to copy paste，going to copy paste。

![](img/f8f008e2808f19882aa25f551e7c2493_43.png)

some matplotlib code to do that um，some matplotlib code to do that um。

and i'm going to also plot delay so show，and i'm going to also plot delay so show。



![](img/f8f008e2808f19882aa25f551e7c2493_45.png)

you what the label is，you what the label is，um and there you go so you can't really。

um and there you go so you can't really，tell，tell，but that's like it's a super nice frog。

but that's like it's a super nice frog，i can't tell it's beautiful like a red。

i can't tell it's beautiful like a red，and orange eye，and orange eye。

but if you look at label six i mean，but if you look at label six i mean，let's just verify right so。

let's just verify right so，zero one two three four five six so yeah。

zero one two three four five six so yeah，that looks like a，that looks like a。

it looks like this guy kind of，it looks like this guy kind of。



![](img/f8f008e2808f19882aa25f551e7c2493_47.png)

uh yeah so so that's the frog so let's，uh yeah so so that's the frog so let's。

normalize it now so that's，normalize it now so that's。



![](img/f8f008e2808f19882aa25f551e7c2493_49.png)

the neural network oh it's already，the neural network oh it's already，downloaded okay oh wow。

downloaded okay oh wow，so that's great and um，so that's great and um。

cool so now now we we don't want to，cool so now now we we don't want to，iterate through these images。

iterate through these images，like one at a time right so see here。

like one at a time right so see here，this is an image，this is an image。

a single image so we actually want to do，a single image so we actually want to do。



![](img/f8f008e2808f19882aa25f551e7c2493_51.png)

batch of images right so，batch of images right so，we're going to use the data loader for。

we're going to use the data loader for，that so i pull that in and i'm going to。

that so i pull that in and i'm going to，say，say，batch size 32 and i do want to shuffle。

batch size 32 and i do want to shuffle，that so there it is，that so there it is。



![](img/f8f008e2808f19882aa25f551e7c2493_53.png)

and then obviously you know to iterate，and then obviously you know to iterate。

through this it's just a simple for loop，through this it's just a simple for loop。

right so four batch，right so four batch，in data loader get the batch expand it。

in data loader get the batch expand it，out，out，print the shapes just so you can see。

print the shapes just so you can see，what they look like so 32 is the batch。

what they look like so 32 is the batch，size which is great，size which is great。

three channels 32 heights and 32 with，three channels 32 heights and 32 with，pixels，pixels。

right and then our labels are 32 so just，right and then our labels are 32 so just，32，32，scalars um。

scalars um，and then um now we're gonna i also need，and then um now we're gonna i also need。

to modify my rest nuts so if you，to modify my rest nuts so if you，remember the rest net。

remember the rest net。

![](img/f8f008e2808f19882aa25f551e7c2493_55.png)

was trained for imagenets and as you，was trained for imagenets and as you。

said there are a thousand classes there，said there are a thousand classes there。

so it won't really work when i have a，so it won't really work when i have a，data set with 10 classes。

data set with 10 classes。

![](img/f8f008e2808f19882aa25f551e7c2493_57.png)

so for that i need to modify my rest and，so for that i need to modify my rest and。

at 50 to take that so，at 50 to take that so，um i think they're cheating because。

um i think they're cheating because，actually the rest of 50，actually the rest of 50。

has the rest net 50 plus these fc，has the rest net 50 plus these fc。

fully connected layers at the end right，fully connected layers at the end right，so um，so um。

we're going to replace that last fully，we're going to replace that last fully，connected layer which。

connected layer which，i don't know what the size of the the，i don't know what the size of the the。

output is of that rest net，output is of that rest net，50。 um but i know that i need to have，50。

 um but i know that i need to have，10 as to the output because that's going。

10 as to the output because that's going，to be the number of glasses that i have。

to be the number of glasses that i have，right，right，so what's happening under the hood is。

so what's happening under the hood is，you have，you have，this like rest nut right a bunch of。

this like rest nut right a bunch of，layers here，layers here，and then at some point when that ends。

and then at some point when that ends，then you have this fully connected which。

then you have this fully connected which，is mapping，is mapping，the output from here um into whatever。

the output from here um into whatever，number of classes you have，number of classes you have。

right so this guy i want to replace um，right so this guy i want to replace um，you know depends。

you know depends，on the context you sometimes can drop it，on the context you sometimes can drop it。

put an identity function，put an identity function，whatever you want um okay so we'll。

whatever you want um okay so we'll，replace that，replace that。



![](img/f8f008e2808f19882aa25f551e7c2493_59.png)

let's just make sure that works okay，let's just make sure that works okay。

perfect so now we're good to go，perfect so now we're good to go。

um so let's go ahead and predict some，um so let's go ahead and predict some，stuff right so。

stuff right so，i'm just going to load another batch，i'm just going to load another batch。



![](img/f8f008e2808f19882aa25f551e7c2493_61.png)

here and then i'm going to run it，here and then i'm going to run it，through my rest net so。

through my rest net so，this image and then i'm going to look at。

this image and then i'm going to look at，the first 10 predictions only，the first 10 predictions only。

right um great so that looks good，right um great so that looks good。

um and i noticed that the high the，um and i noticed that the high the。

highest number is this first guy here，highest number is this first guy here，right，right，0。

7 looks like um so let me do a soft，0，7 looks like um so let me do a soft，max just to kind of like。

max just to kind of like，turn this into probabilities right um，turn this into probabilities right um。

great so 0，19，great so 0，19，uh that looks like the highest one so。

uh that looks like the highest one so，this is what the network would，this is what the network would。

predict for this particular image the，predict for this particular image the。

label and uh we're gonna use the，label and uh we're gonna use the。

arc max to pull the like the label name，arc max to pull the like the label name，i guess，i guess。

in this case um so we get to zero right，in this case um so we get to zero right。

so that makes sense because，so that makes sense because，that was the highest number as well。

that was the highest number as well，right um under 10 here where，right um under 10 here where。

where do we fit the image to the network，where do we fit the image to the network，oh up here。

oh up here，um right there uh but x was a 32 by 32，um right there uh but x was a 32 by 32，right，right。

and the rest net usually is trained on，and the rest net usually is trained on。

the 100 and something right pixels，the 100 and something right pixels，so yeah that's correct so it's。

so yeah that's correct so it's，convolutional though so um，convolutional though so um。

the inputs don't really matter as long，the inputs don't really matter as long。

as you don't shrink it too much right so，as you don't shrink it too much right so。

i'm cheating a little bit but，i'm cheating a little bit but，um the c510 is fine 32 won't won't。

um the c510 is fine 32 won't won't，disappear if you did like eminence。

disappear if you did like eminence，potentially you could have a crash。

potentially you could have a crash，because，because，at some point you'll downtime but way。

at some point you'll downtime but way，too much uh-huh，too much uh-huh。

okay um yeah so it's a beautiful part，okay um yeah so it's a beautiful part，about the rest nets。

about the rest nets，sorry about convolutional networks is，sorry about convolutional networks is。

you know the input can change，you know the input can change，um as well okay so let's put the the。

um as well okay so let's put the the，labels so i pulled the labels out。

labels so i pulled the labels out，um and they don't match right so，um and they don't match right so。

obviously you're like well this is，obviously you're like well this is，supposed to be，supposed to be。

this fancy pre-trained image in that，this fancy pre-trained image in that。

model but like it didn't predict the，model but like it didn't predict the，labels，labels。

so my labels are seven i predicted zero，so my labels are seven i predicted zero。

uh none of these none of these are great，uh none of these none of these are great。

except this one by chance so one out of，except this one by chance so one out of，ten，ten。

makes sense right expect a number given，makes sense right expect a number given，the classes。

the classes。

![](img/f8f008e2808f19882aa25f551e7c2493_63.png)

um yeah so they don't match so，um yeah so they don't match so，that the reason for that is because we。

that the reason for that is because we，haven't remember we replaced this layer。

haven't remember we replaced this layer，here，here。

![](img/f8f008e2808f19882aa25f551e7c2493_65.png)

right um where is it yeah here，right um where is it yeah here，uh nope not there here so we replace。

uh nope not there here so we replace，this layer so like，this layer so like。

all of the last logic if you replace，all of the last logic if you replace。

anything on this pre-trained model it's，anything on this pre-trained model it's。

not going to work right，not going to work right，and the last logic we we made completely。

and the last logic we we made completely，random so now i have to fine-tune this。

random so now i have to fine-tune this，thing，thing，so the process of fine-tuning is um。

so the process of fine-tuning is um，you know you can do it two ways you can。

you know you can do it two ways you can，take this pre-trained，take this pre-trained。

net net network and keep it kind of，net net network and keep it kind of。

frozen right so you're never gonna back，frozen right so you're never gonna back，properly get into it。

properly get into it，and then strap anything else on top of，and then strap anything else on top of。

that i'm gonna use a linear layer but，that i'm gonna use a linear layer but，you could use an svm。

you could use an svm，you could use logistic regression you，you could use logistic regression you。

can use a random forest，can use a random forest，any classifier uh doesn't matter um。

any classifier uh doesn't matter um，because what you're doing is you're。

because what you're doing is you're，using the neural network to extract。

using the neural network to extract，features，features，and then you're using some other。

and then you're using some other，classifier to use those features and。

classifier to use those features and，classify right and，classify right and。

if the network did its job they should，if the network did its job they should。



![](img/f8f008e2808f19882aa25f551e7c2493_67.png)

be linearly separable so then that，be linearly separable so then that。

svm would be fine at that point so，svm would be fine at that point so。

um in this case i'm going to be lazy i'm，um in this case i'm going to be lazy i'm。



![](img/f8f008e2808f19882aa25f551e7c2493_69.png)

![](img/f8f008e2808f19882aa25f551e7c2493_70.png)

![](img/f8f008e2808f19882aa25f551e7c2493_71.png)

![](img/f8f008e2808f19882aa25f551e7c2493_72.png)

![](img/f8f008e2808f19882aa25f551e7c2493_73.png)

![](img/f8f008e2808f19882aa25f551e7c2493_74.png)

![](img/f8f008e2808f19882aa25f551e7c2493_75.png)

![](img/f8f008e2808f19882aa25f551e7c2493_76.png)

![](img/f8f008e2808f19882aa25f551e7c2493_77.png)

![](img/f8f008e2808f19882aa25f551e7c2493_78.png)

![](img/f8f008e2808f19882aa25f551e7c2493_79.png)

![](img/f8f008e2808f19882aa25f551e7c2493_80.png)

![](img/f8f008e2808f19882aa25f551e7c2493_81.png)

![](img/f8f008e2808f19882aa25f551e7c2493_82.png)

![](img/f8f008e2808f19882aa25f551e7c2493_83.png)

![](img/f8f008e2808f19882aa25f551e7c2493_84.png)

![](img/f8f008e2808f19882aa25f551e7c2493_85.png)

![](img/f8f008e2808f19882aa25f551e7c2493_86.png)

![](img/f8f008e2808f19882aa25f551e7c2493_87.png)

![](img/f8f008e2808f19882aa25f551e7c2493_88.png)

![](img/f8f008e2808f19882aa25f551e7c2493_89.png)

![](img/f8f008e2808f19882aa25f551e7c2493_90.png)

![](img/f8f008e2808f19882aa25f551e7c2493_91.png)

![](img/f8f008e2808f19882aa25f551e7c2493_92.png)

![](img/f8f008e2808f19882aa25f551e7c2493_93.png)

![](img/f8f008e2808f19882aa25f551e7c2493_94.png)

![](img/f8f008e2808f19882aa25f551e7c2493_95.png)

![](img/f8f008e2808f19882aa25f551e7c2493_96.png)

![](img/f8f008e2808f19882aa25f551e7c2493_97.png)

![](img/f8f008e2808f19882aa25f551e7c2493_98.png)

![](img/f8f008e2808f19882aa25f551e7c2493_99.png)

![](img/f8f008e2808f19882aa25f551e7c2493_100.png)

![](img/f8f008e2808f19882aa25f551e7c2493_101.png)

![](img/f8f008e2808f19882aa25f551e7c2493_102.png)

![](img/f8f008e2808f19882aa25f551e7c2493_103.png)

![](img/f8f008e2808f19882aa25f551e7c2493_104.png)

![](img/f8f008e2808f19882aa25f551e7c2493_105.png)

![](img/f8f008e2808f19882aa25f551e7c2493_106.png)

![](img/f8f008e2808f19882aa25f551e7c2493_107.png)

![](img/f8f008e2808f19882aa25f551e7c2493_108.png)

![](img/f8f008e2808f19882aa25f551e7c2493_109.png)

![](img/f8f008e2808f19882aa25f551e7c2493_110.png)

![](img/f8f008e2808f19882aa25f551e7c2493_111.png)

![](img/f8f008e2808f19882aa25f551e7c2493_112.png)

![](img/f8f008e2808f19882aa25f551e7c2493_113.png)

![](img/f8f008e2808f19882aa25f551e7c2493_114.png)

![](img/f8f008e2808f19882aa25f551e7c2493_115.png)

![](img/f8f008e2808f19882aa25f551e7c2493_116.png)

![](img/f8f008e2808f19882aa25f551e7c2493_117.png)

![](img/f8f008e2808f19882aa25f551e7c2493_118.png)

![](img/f8f008e2808f19882aa25f551e7c2493_119.png)

![](img/f8f008e2808f19882aa25f551e7c2493_120.png)

![](img/f8f008e2808f19882aa25f551e7c2493_121.png)

![](img/f8f008e2808f19882aa25f551e7c2493_122.png)

![](img/f8f008e2808f19882aa25f551e7c2493_123.png)

![](img/f8f008e2808f19882aa25f551e7c2493_124.png)

![](img/f8f008e2808f19882aa25f551e7c2493_125.png)

![](img/f8f008e2808f19882aa25f551e7c2493_126.png)

![](img/f8f008e2808f19882aa25f551e7c2493_127.png)

![](img/f8f008e2808f19882aa25f551e7c2493_128.png)

![](img/f8f008e2808f19882aa25f551e7c2493_129.png)

![](img/f8f008e2808f19882aa25f551e7c2493_130.png)

![](img/f8f008e2808f19882aa25f551e7c2493_131.png)

![](img/f8f008e2808f19882aa25f551e7c2493_132.png)

![](img/f8f008e2808f19882aa25f551e7c2493_133.png)

![](img/f8f008e2808f19882aa25f551e7c2493_134.png)

![](img/f8f008e2808f19882aa25f551e7c2493_135.png)

![](img/f8f008e2808f19882aa25f551e7c2493_136.png)

![](img/f8f008e2808f19882aa25f551e7c2493_137.png)

![](img/f8f008e2808f19882aa25f551e7c2493_138.png)

![](img/f8f008e2808f19882aa25f551e7c2493_139.png)

![](img/f8f008e2808f19882aa25f551e7c2493_140.png)

![](img/f8f008e2808f19882aa25f551e7c2493_141.png)

![](img/f8f008e2808f19882aa25f551e7c2493_142.png)

![](img/f8f008e2808f19882aa25f551e7c2493_143.png)

![](img/f8f008e2808f19882aa25f551e7c2493_144.png)

![](img/f8f008e2808f19882aa25f551e7c2493_145.png)

![](img/f8f008e2808f19882aa25f551e7c2493_146.png)

![](img/f8f008e2808f19882aa25f551e7c2493_147.png)

![](img/f8f008e2808f19882aa25f551e7c2493_148.png)

![](img/f8f008e2808f19882aa25f551e7c2493_149.png)

![](img/f8f008e2808f19882aa25f551e7c2493_150.png)

![](img/f8f008e2808f19882aa25f551e7c2493_151.png)

![](img/f8f008e2808f19882aa25f551e7c2493_152.png)

![](img/f8f008e2808f19882aa25f551e7c2493_153.png)

![](img/f8f008e2808f19882aa25f551e7c2493_154.png)

![](img/f8f008e2808f19882aa25f551e7c2493_155.png)

![](img/f8f008e2808f19882aa25f551e7c2493_156.png)

![](img/f8f008e2808f19882aa25f551e7c2493_157.png)

![](img/f8f008e2808f19882aa25f551e7c2493_158.png)

![](img/f8f008e2808f19882aa25f551e7c2493_159.png)

![](img/f8f008e2808f19882aa25f551e7c2493_160.png)

![](img/f8f008e2808f19882aa25f551e7c2493_161.png)

![](img/f8f008e2808f19882aa25f551e7c2493_162.png)

![](img/f8f008e2808f19882aa25f551e7c2493_163.png)

![](img/f8f008e2808f19882aa25f551e7c2493_164.png)

![](img/f8f008e2808f19882aa25f551e7c2493_165.png)

![](img/f8f008e2808f19882aa25f551e7c2493_166.png)

![](img/f8f008e2808f19882aa25f551e7c2493_167.png)

![](img/f8f008e2808f19882aa25f551e7c2493_168.png)

![](img/f8f008e2808f19882aa25f551e7c2493_169.png)

![](img/f8f008e2808f19882aa25f551e7c2493_170.png)

![](img/f8f008e2808f19882aa25f551e7c2493_171.png)

![](img/f8f008e2808f19882aa25f551e7c2493_172.png)

![](img/f8f008e2808f19882aa25f551e7c2493_173.png)

![](img/f8f008e2808f19882aa25f551e7c2493_174.png)

![](img/f8f008e2808f19882aa25f551e7c2493_175.png)

![](img/f8f008e2808f19882aa25f551e7c2493_176.png)