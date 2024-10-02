# 【NYU】纽约大学深度学习入门课程（with pytorch）中英文字幕 - P29：Week 15 – Practicum part B - Training latent variable energy based models (EB - 大佬的迷弟的粉丝 - BV1o5411p7AB

so we share the screen，so we share the screen，so we share the screen，and i'm opening the chat。

and i'm opening the chat。

![](img/bb303e6bd2ce61b2618b7c50f74c9469_1.png)

all right so i have the chat open so you，all right so i have the chat open so you。

can interact with me，can interact with me，and so a small recap from last time last。

and so a small recap from last time last。

![](img/bb303e6bd2ce61b2618b7c50f74c9469_3.png)

time we've been talking about energy，time we've been talking about energy。

uh and actually we've been talking about，uh and actually we've been talking about，inference。

inference，how to find set how to find y check uh，how to find set how to find y check uh。

how to compute y，how to compute y，f and e okay and so let me just start。

f and e okay and so let me just start，i guess with the the last slide from。

i guess with the the last slide from，last time so we，last time so we。

had computed this f infinity uh which is，had computed this f infinity uh which is，called，called。

uh zero temperature limit uh free energy，uh zero temperature limit uh free energy。

uh as a function of my y and y is going，uh as a function of my y and y is going。

to be a two dimensional，to be a two dimensional，vector right so whenever i'm going to be。

vector right so whenever i'm going to be，plotting this f，plotting this f。

infinity of y it's going to be a scalar，infinity of y it's going to be a scalar。

field means this a height，field means this a height，over like a 2d region okay。

over like a 2d region okay，so we saw already this stuff that since。

so we saw already this stuff that since，it's gonna have different height i'm。

it's gonna have different height i'm，gonna represent with the，gonna represent with the。

color purple the height equals zero，color purple the height equals zero。

and then color equal green for，and then color equal green for，equal one and then everything that is。

equal one and then everything that is，above and beyond，above and beyond。

the free energy equal tool is going to，the free energy equal tool is going to，be in，be in。



![](img/bb303e6bd2ce61b2618b7c50f74c9469_5.png)

yellow okay and so，yellow okay and so，this is how this stuff looks i，this is how this stuff looks i。

would like to remind you that this free，would like to remind you that this free。

energy was the quadratic，energy was the quadratic，uh a cliton distance from the model。

uh a cliton distance from the model，manifold right so all points that are。

manifold right so all points that are，within the um within the model manifold。

within the um within the model manifold，they have zero cost right，they have zero cost right。

this is sorry zero energy free energy，this is sorry zero energy free energy，because again the。

because again the，the distance between them and the，the distance between them and the。

manifold is zero so zero squared is zero，manifold is zero so zero squared is zero。

and then as you move away it's gonna，and then as you move away it's gonna，it's gonna increase up。

it's gonna increase up，uh quadratically so，uh quadratically so，uh so far everything should be uh。

uh so far everything should be uh，known understood and you know you you。

known understood and you know you you，took yeah you had one week to to go over。

took yeah you had one week to to go over，this stuff so，this stuff so。

i i assume everyone is quite familiar，i i assume everyone is quite familiar。

so something that you may notice right，so something that you may notice right。

now is gonna be in the side，now is gonna be in the side，of these ellipse you're going to have。

of these ellipse you're going to have，like a region that is slightly，like a region that is slightly。

slightly lighter right you can see a，slightly lighter right you can see a，lighter degree of。

lighter degree of，purple so what's going on over there so，purple so what's going on over there so。

let me show you this，let me show you this，uh image here uh with the height。

uh image here uh with the height，you know proportional to the actual。

you know proportional to the actual。

![](img/bb303e6bd2ce61b2618b7c50f74c9469_7.png)

height of this um，height of this um，of this free energy okay so i'm gonna。

of this free energy okay so i'm gonna，change the color map such that，change the color map such that。

uh you can clearly see what's going on，uh you can clearly see what's going on。

and i'm gonna be using this one which is，and i'm gonna be using this one which is，called，called。

cold warm so cold means like，cold warm so cold means like，f infinity equals zero i'm going to be。

f infinity equals zero i'm going to be，using the blue color，using the blue color。

for f infinity equal 0，5 i'm gonna be，for f infinity equal 0，5 i'm gonna be，using，using。

a gray color and then for everything，a gray color and then for everything，that is above and beyond。

that is above and beyond，f infinity one is going to be in red，f infinity one is going to be in red。

and so this is going to be um the the，and so this is going to be um the the。

image you saw before now that was like，image you saw before now that was like，simply saw from。

simply saw from，uh from top here i'm gonna show you the，uh from top here i'm gonna show you the。

contour，contour，so each uh line here they share the same，so each uh line here they share the same。

value of the free energy，value of the free energy，okay so let me spin this little guy so。

okay so let me spin this little guy so，it's that you can see all around。

it's that you can see all around，as you can tell all the regions like the。

as you can tell all the regions like the，height，height，around the the the ellipse that is。

around the the the ellipse that is，with the the manifold ellipse is gonna。

with the the manifold ellipse is gonna，have zero energy，have zero energy。

and as you move away from that you're，and as you move away from that you're。

gonna have like a quadratic thing right，gonna have like a quadratic thing right。

so you're gonna have like a parabola，so you're gonna have like a parabola。

uh what you notice is that in the center，uh what you notice is that in the center。

so on the outside of course is going to，so on the outside of course is going to。

be like a parabola but in the center，be like a parabola but in the center。

those two things are going to be going，those two things are going to be going，up on a peak。

up on a peak，right and this might，right and this might，or might not be wanted and so the。

or might not be wanted and so the，this we're gonna start today lesson by。

this we're gonna start today lesson by，learning how to relax，learning how to relax。

this uh free energy this infinite zero，this uh free energy this infinite zero。

temperature limit free energy，temperature limit free energy，to a more you know uh a free energy。

to a more you know uh a free energy，without，without，local minima such that you know it's a。

local minima such that you know it's a，bit more smooth，bit more smooth。

let me take here a cross section of this，let me take here a cross section of this，you know bathtub。

you know bathtub，for y one equals zero so i'm gonna be，for y one equals zero so i'm gonna be，chaff。

chaff，chopping it in a correspondence of y one，chopping it in a correspondence of y one，equals zero。

equals zero，so what we get is going to be the，so what we get is going to be the。

following you're gonna see now，following you're gonna see now。

that those two branches are gonna be my，that those two branches are gonna be my。

parabolic branches right，parabolic branches right，so again what is this free energy free。

so again what is this free energy free，energy，energy，was the square distance of your given。

was the square distance of your given，point，point，to the closest point on the manifold。

to the closest point on the manifold，right，right，so if you're on the manifold which is。

so if you're on the manifold which is，like location，like location，0，4 for example then the distance。

0，4 for example then the distance，between you，between you，and the manifold is going to be zero and。

and the manifold is going to be zero and，therefore the square of zero is going to。

therefore the square of zero is going to，be zero，be zero，as you move away let's say we move to。

as you move away let's say we move to，the right hand side of this，the right hand side of this，0。

4 as you move linearly to the right，0，4 as you move linearly to the right，hand side，hand side。

you're going to be increasing，you're going to be increasing，quadratically right that's why we。

quadratically right that's why we，observe，observe，this energy free energy going up。

this energy free energy going up，quadratically，quadratically。

similarly what happens on the other side，similarly what happens on the other side，of course。

of course，the same happens as you move towards the，the same happens as you move towards the。

zero right and so as you move towards，zero right and so as you move towards。

the zero you're gonna get，the zero you're gonna get，that you try to climb up that parabola。

that you try to climb up that parabola，and we have this peak over here and so。

and we have this peak over here and so，in the next，in the next，slide we're gonna be learning how to。

slide we're gonna be learning how to，smooth that peak，smooth that peak。

i'll let you i tell you later why we uh，i'll let you i tell you later why we uh，what is very why。

what is very why，this is very useful like why we why my，this is very useful like why we why my，why。

why，we might want to do so okay，we might want to do so okay，so free energy we we know right the the。

so free energy we we know right the the，minimum，minimum，value of the energy e that。

value of the energy e that，is spanning across y and z right so，is spanning across y and z right so。

you have this energy we saw that uh for，you have this energy we saw that uh for。

a given y we have like an energy over z，a given y we have like an energy over z。

and then the free energy was the value，and then the free energy was the value。

of the energy correspondent，of the energy correspondent，to the location where we have the。

to the location where we have the，minimum value right so the minimum value。

minimum value right so the minimum value，of this，of this，e is going to be my free energy。

e is going to be my free energy，now i'm going to be introducing a，now i'm going to be introducing a。

relaxed version which is going to be，relaxed version which is going to be，this uh purple f so。

this uh purple f so，this purple f function parameterized by，this purple f function parameterized by。

beta，beta，is going to be simply this expression uh，is going to be simply this expression uh。

what is this beta，what is this beta，right so this beta it's in，right so this beta it's in。

physics it's called the inverse，physics it's called the inverse，temperature，temperature。

the thermo thermodynamic inverse，the thermo thermodynamic inverse，temperature or the。

temperature or the，coldness and it's simply one over，coldness and it's simply one over。

uh kb which is the boltzmann constant，uh kb which is the boltzmann constant。

multiplied by the temperature okay，multiplied by the temperature okay。

so again if t that capital t the，so again if t that capital t the，temperature is very very very high。

temperature is very very very high，like it's very warm like you're on the。

like it's very warm like you're on the，sun beta is gonna be，sun beta is gonna be。

extremely small right it's gonna be zero，extremely small right it's gonna be zero。

instead if temperature the temperature，instead if temperature the temperature，is cold like。

is cold like，zero kelvin then automatically you're，zero kelvin then automatically you're。

gonna get that beta，gonna get that beta，it's plus infinity right and so。

it's plus infinity right and so，now you can understand why，now you can understand why。

i call my f infinity the zero，i call my f infinity the zero，temperature limit，temperature limit。

free energy so it's zero temperature，free energy so it's zero temperature，it's super cold right。

it's super cold right，so capital t is zero meaning beta is，so capital t is zero meaning beta is。

plus infinity，plus infinity，so again if you have this free energy。

so again if you have this free energy，with so-called free energy，with so-called free energy。

the free energy is going to be exactly，the free energy is going to be exactly。

the minimum otherwise if you relax，the minimum otherwise if you relax。

this constraint as you warm up a little，this constraint as you warm up a little，bit this free energy。

bit this free energy，the free energy is going to be a，the free energy is going to be a。

summation of multiple，summation of multiple，things right so this s here is the s for。

things right so this s here is the s for，sum is a summation of all these。

sum is a summation of all these，components here multiplied by the，components here multiplied by the。

interval cool，interval cool，this symbol over here it's simply the。

this symbol over here it's simply the，measure，measure，of the domain of z so in our case。

of the domain of z so in our case，uh z goes from zero to two pi and。

uh z goes from zero to two pi and，therefore，therefore，this item over here it simply means two。

this item over here it simply means two，pi，pi，okay all right all right but who。

okay all right all right but who，who remembers what this kbt is right。

who remembers what this kbt is right，what is this kbt why are we talking。

what is this kbt why are we talking，about energies right，about energies right。

so again from physics no 101 you might，so again from physics no 101 you might，remember that。

remember that，the average，the average，translational kinetic energy was the two。

translational kinetic energy was the two，third，third，kbt no and therefore kbt or two third。

kbt no and therefore kbt or two third，kbt，kbt，express the uh kinetic energy right of。

express the uh kinetic energy right of，this，this，let's say gas with all those particles。

let's say gas with all those particles，and so the temperature allows you to。

and so the temperature allows you to，express，express，uh the energy right so you have。

uh the energy right so you have，temperature and energy are connected。

temperature and energy are connected，um so you can make uh，um so you can make uh。

a quick you know check check here and，a quick you know check check here and。

beta since it's going to be the inverse，beta since it's going to be the inverse。

of kbt it's going to be in one over，of kbt it's going to be in one over。

joule right and so here we have these，joule right and so here we have these。

one over joule means that this stuff is，one over joule means that this stuff is。

joule therefore f is going to be an，joule therefore f is going to be an，energy，energy。

and then inside this exponential we have，and then inside this exponential we have，one over，one over。

joule times the e which is joule and，joule times the e which is joule and。

then if you multiply the two you，then if you multiply the two you。

then the two you know units cancel out，then the two you know units cancel out，so，so。

everything works just fine，everything works just fine，all right all right all right um and。

all right all right all right um and，also yes，also yes，the the dimension of z cancel out with。

the the dimension of z cancel out with，this dimension right so everything is。

this dimension right so everything is，just pure，just pure，uh pure number okay again these are this。

uh pure number okay again these are this，is not machine learning this is physics。

is not machine learning this is physics，just to give you a little bit of you。

just to give you a little bit of you，know uh，know uh，overview about what this stuff where。

overview about what this stuff where，this stuff comes from right so this is。

this stuff comes from right so this is，just from our friends from the physics。

just from our friends from the physics，department，department，all right all right all right so i want。

all right all right all right so i want，to compute this free energy in this。

to compute this free energy in this，relaxed version of this，relaxed version of this。

uh free energy uh since i don't want to，uh free energy uh since i don't want to。

compute this integral，compute this integral，i may not know how to do that i simply。

i may not know how to do that i simply，use a simple discretization right。

use a simple discretization right，and so i replace this latin s with a。

and so i replace this latin s with a，greek s right and then i replace this。

greek s right and then i replace this，latin d，latin d，with a greek t so everything else is。

with a greek t so everything else is，just the same so i go from the，just the same so i go from the。

time continuous to a discretization very，time continuous to a discretization very。

simple discretization it works，simple discretization it works，in our case because z is like one。

in our case because z is like one，dimension i saw you know everything is。

dimension i saw you know everything is，pretty easy uh，pretty easy uh。

moreover here i will just define and，moreover here i will just define and。

pay attention i am defining right now，pay attention i am defining right now，for this class。

for this class，okay this thing uh has been the，okay this thing uh has been the，soft mean of e so my。

soft mean of e so my，free energy uh the purple one，free energy uh the purple one。

it's simply the relaxation of the zero，it's simply the relaxation of the zero，temperature。

temperature，limit is going to be simply this soft，limit is going to be simply this soft，mean so。

mean so，the zero temperature the super cold one，the zero temperature the super cold one。

is simply the mean，is simply the mean，okay am i n min whereas if i，okay am i n min whereas if i。

compute if i relax if i turn on the，compute if i relax if i turn on the，temperature，temperature。

like i increase the thermostat i'm gonna，like i increase the thermostat i'm gonna，have this。

have this，soft mean which is this log，soft mean which is this log。

summation of exponential okay and i call，summation of exponential okay and i call，this actual。

this actual，soft mean why do i call it actual soft，soft mean why do i call it actual soft。

meme because other people，meme because other people，uh most of the people outside this class。

uh most of the people outside this class，will call this the soft means something。

will call this the soft means something，else and i will let you，else and i will let you。

know a bit more about these in a few，know a bit more about these in a few，slides okay，slides okay。

something that is super interesting is，something that is super interesting is。

computing the limit of this free energy，computing the limit of this free energy。

here for beta that goes to zero so，here for beta that goes to zero so。

whenever you increase the temperature，whenever you increase the temperature。

as the temperature on the sun like it's，as the temperature on the sun like it's。

super warm what is the most，super warm what is the most，relaxed version of this min。

relaxed version of this min，and so if you do that you're gonna see。

and so if you do that you're gonna see，that，that，this stuff ends up being the average but。

this stuff ends up being the average but，again this is just you know，again this is just you know。

um it's not relevant it's not too，um it's not relevant it's not too，important，important。

uh is the derivation just i can show you，uh is the derivation just i can show you，here，here。

and i just show you so you can you have，and i just show you so you can you have，access later。

access later，uh the limit of this free energy，uh the limit of this free energy。

for beta that goes to zero so it's very，for beta that goes to zero so it's very，warm，warm。

super warm it ends up being simply the，super warm it ends up being simply the，average，average。

of the energy okay across those heads，of the energy okay across those heads。

again not to uh you don't have to get，again not to uh you don't have to get，scared about that math。

scared about that math，all right so let's compute this free，all right so let's compute this free。

energy for，energy for，the cases we saw before right so we are。

the cases we saw before right so we are，still doing inference，still doing inference。

as last time but instead of using the，as last time but instead of using the。

cold inference the cold free energy，cold inference the cold free energy。

we're going to use this you know relaxed，we're going to use this you know relaxed，version，version。

for the y equal 23 so if you remember，for the y equal 23 so if you remember。

the y equal 23 was this x，the y equal 23 was this x，the green x on the right hand side and。

the green x on the right hand side and，then here the free energy was the square。

then here the free energy was the square，of the distance between the blue x and。

of the distance between the blue x and，the green x right so the，the green x right so the。

the distance was 0，5 square would would，the distance was 0，5 square would would，have been 0。

25 and that would have been，have been 0，25 and that would have been，the free energy，the free energy。

uh zero temperature zero zero，uh zero temperature zero zero，temperature，temperature。

limit free energy but in this case we，limit free energy but in this case we，have now to consider。

have now to consider，all these contributions and so i'm gonna。

all these contributions and so i'm gonna，show you，show you，how all those little，how all those little。

z dz will contribute to this free energy，z dz will contribute to this free energy。

and so we choose a beta equal 1，and so we choose a beta equal 1，and we have now this so given that y。

and we have now this so given that y，prime is going to be this x on the right。

prime is going to be this x on the right，hand side，hand side，my free energy now comes from the。

my free energy now comes from the，addition of all these uh terms here the。

addition of all these uh terms here the，exponential，exponential，of you know minus the energy of。

of you know minus the energy of，all of this right so all the squares。

all of this right so all the squares，like the exponential of the negative。

like the exponential of the negative，squares right，squares right。

so as you can tell those points that are，so as you can tell those points that are，close to the。

close to the，x will have like a，x will have like a，smaller energy and therefore the。

smaller energy and therefore the，exponential will be larger，exponential will be larger。

and that's why you can see them but for，and that's why you can see them but for。

energy that are you know，energy that are you know，further away that are very high energy。

further away that are very high energy，you do not do the exponential of main。

you do not do the exponential of main，minus and large number you're going to。

minus and large number you're going to，get basically zero so they don't count。

get basically zero so they don't count，in this summation in this integral okay。

in this summation in this integral okay，first question for people at home。

first question for people at home，to just check if you are following。

to just check if you are following，how that where does 0，75 come from，how that where does 0。

75 come from，so where does this value over here come，so where does this value over here come，from。

from，and you're supposed to type on the chart，and you're supposed to type on the chart。

such that i can read，such that i can read，aloud what you're saying so i'm asking。

aloud what you're saying so i'm asking，once again，once again，where does this value over here 075。

where does this value over here 075，and someone is to reply，contribution to the energy yes yes no。

contribution to the energy yes yes no，contribution to the energy yes yes no。

the number 075 i i need you to tell me，the number 075 i i need you to tell me，how to compute 0。

75 where does that，how to compute 0，75 where does that，number come from，number come from。

you have all these closest why，you have all these closest why，till then yeah tell me uh how do i how。

till then yeah tell me uh how do i how，do i compute，do i compute。

x okay x minus beta e okay so how much，x okay x minus beta e okay so how much。

x okay x minus beta e okay so how much。

![](img/bb303e6bd2ce61b2618b7c50f74c9469_9.png)

![](img/bb303e6bd2ce61b2618b7c50f74c9469_10.png)

![](img/bb303e6bd2ce61b2618b7c50f74c9469_11.png)

![](img/bb303e6bd2ce61b2618b7c50f74c9469_12.png)

![](img/bb303e6bd2ce61b2618b7c50f74c9469_13.png)

![](img/bb303e6bd2ce61b2618b7c50f74c9469_14.png)

![](img/bb303e6bd2ce61b2618b7c50f74c9469_15.png)

![](img/bb303e6bd2ce61b2618b7c50f74c9469_16.png)

![](img/bb303e6bd2ce61b2618b7c50f74c9469_17.png)

![](img/bb303e6bd2ce61b2618b7c50f74c9469_18.png)

![](img/bb303e6bd2ce61b2618b7c50f74c9469_19.png)

![](img/bb303e6bd2ce61b2618b7c50f74c9469_20.png)

![](img/bb303e6bd2ce61b2618b7c50f74c9469_21.png)

![](img/bb303e6bd2ce61b2618b7c50f74c9469_22.png)

![](img/bb303e6bd2ce61b2618b7c50f74c9469_23.png)

![](img/bb303e6bd2ce61b2618b7c50f74c9469_24.png)

![](img/bb303e6bd2ce61b2618b7c50f74c9469_25.png)

![](img/bb303e6bd2ce61b2618b7c50f74c9469_26.png)

![](img/bb303e6bd2ce61b2618b7c50f74c9469_27.png)

![](img/bb303e6bd2ce61b2618b7c50f74c9469_28.png)