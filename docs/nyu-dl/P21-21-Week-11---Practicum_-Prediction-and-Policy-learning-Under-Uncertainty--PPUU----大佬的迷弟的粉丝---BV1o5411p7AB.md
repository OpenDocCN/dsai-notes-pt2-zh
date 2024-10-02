# P21：21.Week 11 – Practicum_ Prediction and Policy learning Under Uncertainty (PPUU) - 大佬的迷弟的粉丝 - BV1o5411p7AB

okay so let's get started with today，lesson and let's see what Yan likes to。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_1.png)

do research on alright so today we're。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_3.png)

going to be talking about model，predictive policy learning with。

uncertainty regularization for driving，in dense traffic what a mouthful the。

nice part is that in roughly 50 minutes，you're going to be able to understand。

every word in this title and you，actually should be able to even be ready。

to implement this because we basically，know all the basic components that we。

have cover so far and so this is just，you know put together something but how。

perhaps not in a trivial way but but I，don't think it's too crazy so this is。

work done by my friend and colleague me，Kyle enough myself and then Yong here at。

grant a few years back I think it was，2019 so last year I think oh maybe the。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_5.png)

year before I don't know all right。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_7.png)

so let's see how you can learn how to，drive the model free reinforcement。

learning way right so pay attention to，the car here in in the back this display。

guy so let's say I'd like to train this，this guy with model free reinforcement。

learning so how would you go about that，so you would have to try。

um to do things that are maybe not good，and then if you hear uh shouldn't do。

those things right because it's not good，and so you have to die a few times right。

before actually learning not to die but，that's arguably not the way you learn。

how to drive right especially if you're，driving your your parents car and you。

don't really want to crash your parents，car before learning how to not crash。

your parents car right so let's figure，out a more principled way to learn how。

to drive a car right so I would argue，here and this is just you know my。

intuition is that if you if you have a，car now you're driving a hundred。

kilometers per hour which is like thirty，meters per second if you look 30 meters。

in front of you that will mean that you，look one second in the future right and。

therefore you can see that you know the，road center turns slightly to the left。

in one second in the future therefore I，would like to change the steering wheel。

right now such that in one second I will，be you know following the ended。

trajectory and where the street takes me，to okay so here I'm just trying to you。

know push forward the idea that we need，to look in the future in order to be。

able to make you know some sort of nice，like you know plan of action right so。

you'd like to figure out that if，something is not good you may not want。

to do it so it's that you don't get into，trouble so but hmm was the main problem。

here others other people are problem，right so here you have that you know the。

eCos around you are quite not，deterministic therefore it might be。

slightly hard to take an account every，possible thing that might happen right。

so let me give you like an introduction，here or a small recap of the what are。

the main components in this system here，so we have a agent here represented by。

this pink brain which gets as input a，state s T and produces in action is an。

output which is a T which is for example，my steering control and my acceleration。

or braking signal moreover I observe a，cost which is you know a consequence of。

taking a specific action a given that I，find myself in state s T ok so if I。

should be okay let me see there are chat，messages here let me see what's going on。

okay people are laughing cool alright on，the other side you had the real world。

the real world given a internal state，you get a new action and then you。

produce the new state ok and also you，produce what is the result this。

consequence city to provide to your，agent and so this is how you know how。

you can have like a network interacting，with a real world you take actions given。

a specific state and the word give you，gives you the next state and the next。

consequence so this is model free，because you interact with the real world。

but then the nice part is that you can，do interaction with the model of the。

world okay so under on the left hand，side instead of trying things in the。

real world and you know try to cook and，you burn something and then that's not。

good you burnt also your hand burn my，arm nasty making cookies maybe you would。

like to try in your mind first how can I，make cookies without getting burnt maybe。

don't touch the oven with your hands，right that would be very。

smart option right all right so how how，can we get how can we think right how。

can we ponder how can we make this kind，of interaction between my actions and。

the expected consequences you know of，taking a specific action with actually。

without actually taking the action right，so how can I avoid to burn myself again。

tonight while baking without actually，getting burned right so you want to，think ahead。

don't touch what's hot hmm okay all，right so how do we train this word model。

the same way we trained it last week，right so we start with initial state we。

provide some you know action which was，random last week and this week instead。

is not for example the action here might，be the action taken by some expert that。

we observed like mom cooking for you of，dead don't know and you can see what is。

the the current state and then you can，have the next state dinner is ready。

mmm I'm gonna gray I'm actually hungry，p。m。 all right more or you also had the。

consequence 15 they're going to be you，know your mouth is watering anyhow。

you're gonna be providing now like a，distance between this state that are。

observed in the real world in the state，that are provided to you by the model of。

the world and then you have an MSc loss，right so that's just regression so you。

try to regress what is the next state，given that you start from the initial。

same state and you provide like specific，action okay so far this is something we。

already seen last week just give you an，overview again right all right keep coin。

if you don't complain so let's figure，out here what we can do for example in。

my case in this case I don't have my，model out putting a cost or I don't have。

the word out put in a cost and more，specifically I have that in my case。

I will have my brain here my agent that，again takes a state and provides an。

action which is feeding this model and，then I have my cost is going to be a。

differentiable function of the state，okay which is exactly what we had seen。

last week right with the final you know，destination to be you know the specific。

thing that you gramm run back，propagation through time and back，propagation through time would be。

unrolling this loop right so you go，forward you go like that and then you do。

a back problem okay all right cool so。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_9.png)

let me introduce to you right now the，data set right so far littles you know。

just like setting up the problem so here，it's my actual real case scenario I have。

six cameras seven cameras mounted on it，on the top of a 30-story building facing。

the i-80 interstate segment on the of，the highway array and so here I have。

these cameras recording these cars first，part is going to be fixing the。

perspective right such that I can have，like a hovering view where I cat op down。

view moreover here we extract some，bounding boxes for each baked-on right。

so there is detection there is，regression of the you know well。

detection and figuring out the size of，this bounding boxes and then there is。

tracking because these bounding boxes，are following my cars and so you can see。

here the red track on the left hand side，or you can see like the the red pickup。

car a pickup truck that is you know from，both views or from the top camera down。

to one single view here I can input，these cars into my you know Python。

program item game emulator game engine，and I can draw this representation in。

this case you can still see the red，tractor the pickup pickup pickup truck。

and then on the bus on the right hand，side so here for every each and every。

vehicle the blue the cyan one I have two，vectors the vector PT which is。

representing the position of the vehicle，the，we are part VT which is the velocity。

which is you know vector representing，the VX and V Y component and then。

moreover I given that I know what is the，kinematics of driving a car or a bicycle。

I can invert the kinematics of these，cars that have been driven by you know。

experts and I can figure out what the，actions are that you know what the。

actions of the driver are in the sense，that if the car moves with a rectilinear。

uniform motion you have no action right，so if you don't apply any acceleration。

which is longitudinal or transverse you，have you know the car keeps going so if。

you have a rectilinear uniform motion，there is no action every time you try to。

diverge from this you know motion for，example to accelerate you break or you。

steer then you have some basically you，know action involved right you can。

invert the kinematic model in order to，figure out what the action is cool so。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_11.png)

here again in this representation which，is the thing that I call machine。

representation I have again the same，vehicle there the other pickup car and。

one on the right hand side so in this，case each vehicle here has a bounding。

box which is representing my viewable，area so each car can only view that kind。

of box around itself and so for example，here I can extract the first box where。

April replace myself in the centre and I，movie I move myself to the blue channel。

again such that i'ma I'm not like I make，myself different from the others and the。

red lane the red channel represents the，lane and the green channel represents。

the others wake on other vehicles you，have the other guy here this one here。

that one and the last one okay and here，you can see again the pickup pickup。

truck there the red one and then here，you have a piece of the bus so these are，my images I T or。

serve Asians right these are，representing two things the state of the。

lanes of the street basically and the，second part is going to be they。

represent the traffic situation，surrounding me，so overall the set of PT the position。

within the velocity and I team this，observation represent my state s T so as。

T represents the current state at a，specific time T right for my given。

vehicle so far any question how is it，clear I mean we already seen basically。

everything so far last week and I just，gave you like an overview about the。

specific data sets so there are no new，concept so far so it should be clear。

right yeah no okay you're very quiet，today，maybe it's my audio on okay you're not。

texting so I expect you to be okay yes，it's clear okay thank you all right cool。

so the cost right so we define before we，said before that my cost is going to be。

a function of my state so let's see how，I compute this cost there are two。

different costs there is a lane cost，that is basically telling me whether I。

am on the lane like within the lane on，like inside the lane or I am going off。

lane off road and the other one is going，to be a cost that is gonna be telling me。

how close I am to other vehicles so the，first one it looks like this on my。

y-axis so the x-axis the direction of，motion y-axis is gonna be the one that。

is you know 90 degrees to the left in，their form you can think about having a。

potential it is like a house on top of，you if you overlay this with the red。

channel there is some intersection on，the left hand side this intersection the。

height of that intersection will go to，zero if you are exactly in the center of。

the two lanes if you are shifted the，words one side you're gonna get you know。

some nonzero intersection and if you're，exactly on top of the lane you get is，actually the。

on the on the on the top of this，triangle right on the other side you。

have the proximity cost so I have，exactly the same but for the other。

vehicles night so in this case I have，one longitudinal sorry transverse。

potential I have one longitudinal，potential which is changing the length。

with the speed so the faster I go and，the more I would like to look ahead and。

behind in this case in in the slower I，go I can you know I don't really care so。

much about things that too far I just，look close to myself so we could plug。

these two things in my environment you，can see now that there is an。

intersection for example here that is，pretty high for the purple because we。

are exactly in front of in front of us，but then the orange is quite low because。

it's you know further away in the front，so you can simply do the multiplication。

of the two you can get what is my，current proximity cost okay so how does。

this look right now I can show you for，example for a situation where we go at。

20 kilometers per hour you have all，these vehicles are very close to each。

other and then if you go at 50，kilometers per hour you know on average。

every one is a bit further away so if，you multiply that potential that is in。

the Y and the other one that was in the，X you get something that looks like this。

okay and in the case that we go at a，higher speed you cannot get something。

like this because I gain the extension，in the X direction depends on the speed。

and you can tell like that is the right，one is further far reaching front and。

back cool so how do we get this final，cost well my final cost right now at。

least as we what we establish this paper，we just multiplied this potential mask。

with the green channel and then we pick，the max basically we figure out which。

one is the closest car or close the same，the the part closest to us belongs to。

some other object and so if you multiply，element wise multiply。

these two guys and then you take the max，you get a number and the cool part is。

that differentiable right so now you can，run gradients through on the network。

such that you know you can compute some，actions such that that value overall is。

going to be reduced and it goes to zero，such that you avoid collisions all right。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_13.png)

so let me give you now the outline of，the talk of the lesson for today so。

first we said we had to learn how to，mimic the word rain so that was pretty。

abstract so far now we can start getting，concrete you know tools and information。

so first we want to learn and mimic the，real world second part we'd like to use。

the you know the learned model of the，environment in order to train this agent。

by you know making thinking how to drive，so first you learn how other vehicles。

behave in the real world second part，given that you have an understanding of。

how other people interact you try to，think what would happen if I you know。

perform such an such action in this in，this condition finally we can figure out。

what is a nice way to evaluate a，possible way to evaluate this policy。

back in the real world right so once，you've thought how to drive let's figure。

out whether you can drive cool so let's，get started with the first part the。

world model predicting what's next given，history and action so this is gonna be。

something that you already had seen a，few lessons back but let me give you。

again like a full picture here so we，have a world model which is fed with my。

s1 to T which is a sequence of States，and each state represent is represented。

by a position vector P T a velocity，vector in V T and these context images I。

T these observations so this is a set of，things of course as you can tell you。

will have different you know in，different input branches in your net，right because。

there are different kind of data one is，you know four-dimensional vector the。

other is an image you'd like to use a，convolutional net moreover this word。

modern gets an action and the word model，will produce a prediction for the next。

action on the other side you had the，real word which is telling you well。

these happen instead okay so that's a，target okay so how do we train this。

stuff as we said it's just a regression，problem so we just train with MSE right。

so we have my state like a sequence of，state an action we provide this to this。

predictor module the predictor gives me，some kind of hidden representation of。

the you know of whatever future then I，have a decoder which is decoding this。

hidden representation of the future and，this one this one should give me a。

prediction right so this is pretty，straightforward right you have a。

predictor that predicts the past into，the hidden representation of the future。

they have a decoder which is decoding，the hidden representation of the future。

into the actual future so we have a，target on the other side so all you need。

to do is going to be having this tool，going inside an MSc then you minimize。

the MSE by training these two modules so，does it work what's the action here so。

the action here is for example the，acceleration and the steering steering。

command that the we have observed in our，data set right so my state's s1 to t are。

a sequence of you know observations of，position velocities and context images。

in the action are the action taken by，the driver that I obtained by inverting。

the kinematic model of the car PT is the，position of the car and VT is the。

velocity of the car so a position，velocity in the 80 is the acceleration。

right so PT x and y position VT x and y，velocity 80 x and y，acceleration basically is it preferred。

to add the decoder instead simply using，a predictor to improve the accuracy so。

the predictor predicts what's gonna be，the hidden state of the future okay so。

the predictor gets the past and compress，it and tries to give you what is the。

future you know the future hidden，representation then you have this code。

you'd like to decode it right this is，just you know one neural net but we'd。

like to separate those into blocks okay，so the action at eighty is calculated，from st plus one。

yeah so these actions are the ground，truth action coming from the yeah from。

the ground truth thanks how do we，calculate st we don't how do we get，actual sto。

the actual str i show you before right，the the camera are checking the the cars。

going on the highway i get the bounding，boxes i track the bounding boxes and。

therefore i have all those you know，positions x and y's over time and then。

those are DX the PT positions you can，also compute the velocity right you know。

position time t plus 1 minus position at，times T divided by time you have the。

velocity wait I'm still a little，confused on the role of the decoder is。

it just converting the vector，representation of the future from the，predictor into actual real-world。

predictions yeah that's correct，so the decoder is just like semantic the。

subdivision right now it's just one，neural net and you can think about the。

neural net has having an encoder and，decoder all the time right you can。

decide where you want to have the hidden，representation how do we hold on how do。

we determine the dimensionality of a，spread output well it depends on your。

network right so whatever your network，is outputting in my case I think it 128，dimensional。

vector foresty since there are variable，number of cars surrounding our agent。

vehicle then okay that's a good question，is the size of SD viable so st。

represents the position and velocity of，myself and then i have an image。

which shows me the occupancy grid，basically shows me what the surrounding。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_15.png)

right so I show you here this is my，image IT which represents the。

configuration of the lanes of the street，and what is the configuration of the。

vehicles you have not different number，of vehicles other weight vehicles in the。

left image and the right image，nevertheless an image can just show your。

any number of vehicles right so that's，very cute way of using images just for。

the fact that I don't need to have a，variable length set of you know things。

right otherwise you should have used，some kind of you know attention or asset。

network or some other you know crafty，things this one you know you can use。

images is a mean of representing，information these are not natural images。

right these are completely synthetic，images but I can use them in order to。

cope with the fact that I have a，different number of items nearby me yeah。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_17.png)

I think I answer everyone，yeah that's a boolean green yeah yeah it。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_19.png)

is a boolean grid right so my image has，RGB and each of them are or 0 or 1 in。

this case they are I you can see the，pixels and they are a little bit blurry。

because there is like I think some up，sampling with by linear by linear up。

sampling here in this case let me think，yeah I think there is something like。

that maybe I should be a boolean grid，that's correct I think here we do okay。

there is down sampling this there is，down sampling so these images actually。

are larger in there are binary but then，there are too large so it's so that we。

actually make them forth and by doing，the fourth you know scaling down they。

start looking like a little blurring，right now otherwise if you have a car。

that turns you're gonna have all that，kind of staircase right right now。

instead if you have this kind of blurred，version it's no like that stir-crazy。

okay too many questions with with a，differentiable cost function do we back。

propagate from the end of the trajectory，all the way back yeah it's gonna be yeah。

sure that's correct we are gonna see，this in the second part right this is。

first part where I train a regression，network so here it was the first model。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_21.png)

right so you have like a encoder decoder，which is not because it's a predictor。

predictor decoder just from because of，the fact that the amount stuff on the。

left hand side is from the past right，that's why you need a predictor that。

gives you the next thing in line but，otherwise you can think about an encoder。

but it's not correct way of thinking，just you know similar，does it work so on the left hand side。

you have the actual future the thing，that really happened on the right hand。

side you get the deterministic you know，predictor decoder and the network that I。

just show you train with MSC in order to，replicate the thing on the left this is。

from the testing set of course and it's，been trained on the training set so on。

the top right you're gonna see the，frames you're gonna have a 10 frame per。

second and the direction of motion is，going forward and the blue guy is our。

self the green guys are the others and，the red are the lanes so you can see。

here that after 3 seconds for 5 seconds，everything gets quite up yep，nothing works。

ok how nice I just taught you something，that doesn't work how happy are you are，you happy。

no I can't hear you but okay I mean yeah，thank you for the no the not happy okay。

alright so what's happening okay who can，tell them you should know right what's。

happening because Jana has been talking，about this stuff all along this past。

three weeks so what's the problem here，latent variables your cadet the solution。

what's the problem okay，the MSE loss yeah I was the actual，problem oh okay someone answer is。

someone answer LM whose LM I don't know，its average in future outcomes yeah yes。

yes is someone answer stop okay this is，basically everything that can happen。

from that initial point in time you know，you have everything else therefore it。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_23.png)

looks like that you know every kind of，image looks up like a blur the image。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_25.png)

right so again you had this example from，yan if you have a pencil on on a plane。

and I since I can't really draw in 3d，I'm gonna give you the top-down view on。

the right-hand side let's say you make，it falling right one two three four。

times five six whatever and if you，compute what is the average right。

folding location well this is since is a，you know X&Y is just you know coordinate。

the average final location is like oh，the pen never fed and it's really wrong。

right otherwise if you actually use a，pixel space you would have like the。

overlay anyhow the problem is this one，right you have a multi possible future。

and then you only try to regress the，average teacher right how do we fix it I。

really told me we latent variable the，ACS no no no no I want latent variable。

latent variable this is okay cool this，is the the energy base stuff he likes a。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_27.png)

lot and we like it all right because we，like young。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_29.png)

so okay and actually you already know，everything here so this is the original。

Network I just show you before it，doesn't work and let's fix this so in。

the center we're going to be summing，something and with some this。

low-dimensional latent variable in green，ZT which goes through a you know。

expansion expansion module such that he，fixed the image the dimensionality so。

where's this ZT coming from well I guess，you can tell so that T is going to be。

chosen such that the prediction is，minimized you know that the MSE is。

minimized for this specific peak of the，prediction right so you can do inference。

right so you train everything it's a，real train actually because we trained a。

deterministic one now you can do，inference of the latent variable such。

that you can still get the MSE to zero，by doing gradient descent into latent。

space right so you can change that set，into two to chain chain chain chain。

chain until the emissive dies，this is very expensive because you have。

two degrees in the same thing to the，damn thing there otherwise you can just。

plug this you know you can actually，predict that latent how do you do that。

with an encoder and there you go where，did the encoder is so the encoder gets。

the future state and gives you the mean，and variance from which you sample the。

what is it Irish variational predictive，network actually is a variational。

conditional predictive network because，you actually start from a actual action。

89 so 80 is the condition is it，advisable to help the output fed into a。

encoder for the latent variable during，training oh never mind okay all right。

yeah that's that's how yeah okay that，was the answer yeah so you don't have to。

all right this is just a very convenient，way to get that said T I guess in the。

next next lab when we do the energy，based model we're going to do first。

inference right but inference is not，take you forever because every time you。

have to try try try try try try a new，Zed then where you start with why is。

there an arrow from St plus 1 to F Inc，because unless you know what will happen。

how will you find that ZT right so that，Z T is the missing information that you。

can't have from the past because，something happened you know now my。

roommate is gonna be coming naked inside，oh okay now it doesn't do that things。

you know that's unpredictable part and，may never happen before yeah hopefully。

likely okay the point was that given，that I have no idea about what's gonna。

happen next in the future you know a，meteorite crashes here you can't really。

predict the unpredictable unpredictable，part right you don't know what's going，on。

therefore during training I look in the，future what's happening huh I see。

something as I get information from the，future and from that information I can。

predict the latent variable okay so，someone's gonna say oh you're cheating。

right because you look in the future and，you don't have the future at testing。

time right when you drive you don't have，access to the future but since your。

training here you can kind of cheat and，look look what's happened there but we。

can fix this how do we fix that so this，is the posterior blind of a variational。

encoder and you fix it this way right，you enforce the posterior the decoder。

they saw the encoder there to be giving，you a distribution that is as close as。

possible to the prior to that K ed right，and so in this case you learn how to。

predict basically mean meaningful latent，variable ZT trying to you know。

disconnect as well from that kind of，future okay I'm not sure what Allah is，it。

I'm not I'm not really understanding the，f X part FX means a expansion so that T。

is the latent might be you know 16，dimensional vector very tiny thing and。

the F bread must can easily be like some，kind of spatial information right so。

given that is the state is an image are，gonna be like you know throughout New。

York neural-net I'm gonna be making it，convolutional nets a bit smaller it's。

gonna be still spatial I won't be，collapsing in one vector such that my X。

FX be explained expander will expand my，16 dimensional vector may be in two。

sixteenth lanes of the same size of this，F pred hidden representation okay such。

that I can sum them together could you，repeat how you're putting the。

restriction on the model not being able，to look at actually interstates so right。

now only by looking in the future you，can figure out what's happening okay so。

this F encoder is trained to produce the，latent variable which is minimizing that。

MSC so that's not the variational at，encoder encoder there on the top part。

yeah it's gonna be trying to predict the，latent that really gives you you know。

zero prediction error but then on the，other side you also enforce that encoder。

to give you something that is close to a，normal to to the prior feed over there。

so the fact that there is like a KL term，between the posterior and the Q and the。

P allows you later on to sample from the，prior when you are actually doing you。

know you're using this network see you，build a prior distribution and then。

during into the viewing test time，instead of looking at the actual future。

state you sample from the distribution，label you just learn you just assemble。

from the prior distribution so this is，going to be a fixed prior you fix the。

prior which is a normal distribution，even forced the encoder you know to。

stick with this kind of prior or you can，even learn what is the distribution of。

those latent variables you can do many，things this is what actually we managed，to to get better。

best result with okay look do you，enforce the encoder to give you。

something that looks like a prior which，is a Gaussian you know independent。

Gaussian and then from independent in，also I saw what's called I saw something。

I forgot that you know the unitary，identity matrix right for the covariance。

and so later on we are gonna be just，sampling from that prior distribution to。

get late into that to look you know，reasonable okay thanks sure okay there。

are many more questions how do the，latent variable prevent the averaging oh。

well that's actually so basically，whenever okay，so let's say we train the brains on the。

bottom the deterministic part right so，at the end you're gonna get a prediction。

for the you know predicted state for the，future state which is looking like some。

kind of possible but you know average，future now for a specific future you can。

figure out now you know by doing，gradient descent you can minimize that。

MSE by changing that additional latent，variable this is how latent variable。

models work right so for every training，sample you have one latent variable。

which is gonna give you exactly zero and，the seed loss you can train first with。

all of them such that you can get a very，initial starting point which is the。

average prediction and then you can，refine that average average prediction。

by adding this additional latent，variable and that value for the latent。

variable can be found for example by，doing gradient descent meaning you。

minimize the MSE like you minimize this，MSE loss by getting gradients coming。

down here the gradient comes here and，then you get gradients here so you can。

do that equal you know exact gets Z，minus ETA gradient of the loss with。

respect to to the Z right got it okay，awesome，no that wasn't someone else saying got，it okay。

someone had a question before okay I，don't know oh no it was the answer I。

gave so basically we are adding the F，bread，f bread our prediction of what will。

happen with FX the representation of the，what actually happens now FX is not what。

actually happens if X is what I couldn't，figure out that would have happened。

okay so f pred output it's what I I can，you know I would guess you know my best。

prediction for what happens tomorrow is，going to be that the Sun will rise might。

not be the case so the the Zed that，comes down to the F expander will add。

that component that will you know manage，to fix my broken prediction right so the。

lower branch will try to do as the best，job it can without having knowledge of。

the future and the other one allows me，to refine my prediction to be actually。

correct okay but in this case we have，access to the actual future so it's kind。

of cheating nevertheless you enforce，that this generation of latent variable。

is going to be as close as possible to，my prior distribution，I hope it makes more sense but maybe we。

can go further and then you may get a，little bit clearer clear mind well last。

question is Syd Garon okay starting to，make sense answer is it guaranteed that。

there exists a Zed which gives us M s is，zero I think I'm not sure about。

guarantees but if your network is，reasonably well behaved I guess yeah。

you're guaranteed you know if your，network capacity is can over fit but you。

can't over fit because you know there，are noise in the data you can reduce you。

can zero out that noise by adding this，additional term so it's guaranteed if。

the network is properly sized yeah okay，cool so inference how do we drive okay。

we already spoiled okay more question，training time we try to learn qz4 that。

close to prior petesy test time okay，yeah I'm getting there hold on all right。

test time not test driving time right，how do the hell do you use this stuff。

variation of predicted condition and，predicted net for inference cool so we。

had this lower branch in this lower，dimensional latent variable not a no。

sixteen dimensional vector and where it，comes from we sample from prior right。

because we enforce that the encoder，there was trying to you know shoot it。

towards this distribution hmm cool then，what do you do next you get the。

prediction you put it back so you do a，outer aggressive step right you get next。

prediction network next，yeah correct okay no one wrote anything，but I know you understood and so you。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_31.png)

keep feeding this stuff does it work yes，it works so here you can see again a。

comparison between the actual future on，the left hand side the deterministic。

branch that is just just the lower，branch strain as before and then here I。

give you four different draws from an，art and from a end distribution was。

called I can I can tell the help normal。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_33.png)

distribution so you have you know 200，times 4 so we have 800 samples from a。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_35.png)

normal distribution of size I don't know，16 and I feed you know on the first 200。

values to the first model then I start，again from from same past and I feed to。

new 100 no no 200 200 new values today，to the Leighton there then I have third。

time I get the same initial condition，and then I feed this sequence another。

third sequence of 200 variables pay。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_37.png)

attention here to the car on the。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_39.png)

right-hand side of me that isn't a，circle white circle and then the guy。

behind that guy right in this square。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_41.png)

okay and so if you show if you see here，you get basically that all these。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_43.png)

different predictions will predict a，different location for the car going。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_45.png)

there the dead one in the circle and a，car behind the one one in the square。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_47.png)

also has completely no arbitrary，prediction so this super cool right。

right now you have that each of these。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_49.png)

you know possible futures you know are，completely elucidated by my network so。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_51.png)

this stuff doesn't exist，but we have a network that generates。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_53.png)

future how cool is this right so before，maybe we had you know limited amount of。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_55.png)

training data now we have a network that，is just generating futures from the Hut。

like a magician right so this is super，super super cool you have infinite。

amount of data which is you know，completely different from what actually。

happened the actual future this data，comes from only observational data so，that we。

have seen in the actual reality but is，applied to this specific initial。

condition so what next now you can use，this huge amount of data to train this。

policy right this network that allows，you to control our agent such that it。

minimizes losses the loss that the cost，for the going over these lanes and the。

cost for you know colliding against，other vehicles okay。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_57.png)

the cool part is that okay I can tell。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_59.png)

the design I should yeah I can tell you，the cool part is that this future here。

these multiple futures come from the，specific sequence of latent variable you。

feed to this network right，what if you perform gradient ascent in。

the latent space you get your initial，you know sample from this normal。

distribution then you tweak these values，such that you up the hardness。

like you increase the hardness you don't， up you increase the hardness I like。

to swear you know but you increase the，hardness for example you try to increase。

the proximity cost right so you get the，sequence of latent where other cars are。

gonna be like kamikaze like they are，gonna be driving into you and like crazy。

so that's the super cool you have a，network that gives you futures that you。

want right okay I'm already too excited，I will not be able to sleep tonight。

okay question if we try to sample that。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_61.png)

from Pisa during test time it is，possible for us to look for a specific。

future for example I would like to know，the solution of turning left not moving。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_63.png)

forward so here here I don't let me，think，right right so this predictive network。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_65.png)

you feed the action right so this is a，condition a predictive network so we。

have the action here on the bottom part，so you actually display the whole point。

you can take different actions and the，whole future will change based on the。

action you take right I was mentioning，here we have a initial state that's you。

know the initial condition and then，given different latent you're gonna have。

different kind of behavior of the other，vehicles and then you can decide to。

tweak this latent by for example doing，gradient ascend in the latest pace by。

increasing that kind of collision term，such that you have in our crazy cars。

coming at you but nevertheless as you，pointed out here you can also figure out。

what are the outcomes of changing the，action right that's exactly how we're。

going to be training our policy that is，actually the whole thing right okay。

issues first issue so given given that。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_67.png)

you actually have access to the future，if you turn slightly to the left。

everything is gonna turn to the right，right because if you drive you know you。

turn to the left and how's gonna be like，like that right so if I turn to the left。

you just turn to the right and turning，to the right is gonna be contributing in。

a huge way to the MSC right so right now，you can I get basically that these MSC。

lofts can be minimized if you were，encoder and they're in the latent。

variable is gonna tell my bottom part，that everything is turned to turn to the。

right but this is absolutely not what we，want right because we know how to tell。

everything turns to the right because，that's deterministic right given the。

past given that I turned to the left the，steering wheel everything turns to the。

right I don't care I don't want to look，in the future to see everything turns to。

the right regardless of what I'm doing，with my steering wheel right so this。

it's a very very huge terrible problem，because the network basically was。

learning to cheat right and was figuring，out that we were turning。

without us telling the system we turned，so that was terrible because basically。

this big arrow here is a leak of，information and therefore it was not any。

more sensitive to the current action I，was providing to my predictor right this。

was a very nice big nightmare how do you，now，kill that big arrow right so how do I。

get my predictive network to actually，care about the action I take so let me。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_69.png)

show you the EDD problem here so here we，have the real sequence of latent the one。

that I actually have computed from in，minimizing the MSE yeah that the answer。

that's correct so here I have the real，sequence of latent and the real sequence。

of actions that are taken by the DEA，agent，and so here you can see is actually。

speed up for time such that you can see，there is some kind of you know you know。

turning then you can see here random，variables but the real sequence of。

action you can see now that things are，kind of turning right you can see see。

things are turning on the left on the，last one there you have the real。

sequence of latent but simple actions。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_71.png)

and，you can clearly see the last pile at the，last point that the turning came from。

the mostly from the latent right so the，latent burial 1/10 encodes the rotation。

in the action that it's written a tilde，and those are same sample at random。

right so well symbol from other from，other episodes so the problem here is。

that the fact that we were turning can，we learn，so you'd like to learn that thing you。

would like to reject the fact that we，were turning right so the fact that the。

thing turns should be completely，explainable by the action right and I。

think yeah I don't know anyhow let me。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_73.png)

show you how we fix the problem，sorry explain again it was very unclear。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_75.png)

when you were saying first and last what，you were referring to okay I try again。

so here we have four different，rectangles right in the the last one on。

the right hand side you have the real，sequence of latent variable which are。

this the latent variable that allows me，to get the precise the correct future。

right so those are the latent variable，coming from the and from the encoder in。

the variational encoder and have a have，the real sequence of actions taken by，the expert okay。

the further the two blue the one that，have this blue here and this one here。

are you know simple simple latent，variable that the till that means they。

are sample so they are randomly sample，but I have the real sequence of actions。

and so I would expect to see the，steering and the last one on the left。

hand side I have the real sequence of，latent but then I have you know。

arbitrary actions and so if I show you。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_77.png)

again the animation you're gonna see。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_79.png)

here there is you know some amount of，steering involved okay and you know the。

steering comes from the actions then on，the other two examples here I show you。

that the same actions are not providing，the same amount of steering now that I。

had sample different latent variables，nevertheless if I use the you know exact。

same latent variable all the steering，happens because of the latent variable。

so my decoder will tell me if in my。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_81.png)

network that things were turning just，because they have been encoded in the。

latent variable rather than in the，action，all I can I think I was clear clear but。

let me show you how we fix this，maybe oh is it is it clear what I'm。

trying to show you yeah that was much，better so okay thank you see。

but repeating we say repetitive and it's，in Latin repetition helps that's why you。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_83.png)

had to practice practice practice okay，how do you fix the problem the problem。

is that we have a not a memory leak but，information leak right the information。

leaks from the from the future well it's，a bit late all right so how do we fix。

this problem we fix this problem by，simply dropping out this latent and。

picking it and sampling from the prior，distribution at random okay so we don't。

always rely on the output of the，posterior network the encoder but。

sometimes we pick from the posterior，from the prior in this way you can't。

encode the rotation anymore in the，latent variable because sometimes it。

will be missing and therefore the，network will be having to you know。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_85.png)

exploit the action you provide so in，this case the purple on the right hand。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_87.png)

side I show you two different sets of，latent variable but the real actions。

okay and this network has been trained，with this dropout trick in so in this。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_89.png)

case you can see that the rotation is，actually encoded by the action and no。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_91.png)

longer by the latent variables as it was，the case before so we fix this problem I。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_93.png)

think I should be speeding slightly a。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_95.png)

little because we're kind of running way，too late so sorry I didn't know sit，notice。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_97.png)

but okay what how do we train the agent，well this is pretty much what I said。

before on the right hand side we learned，so far the the model of the world from。

the real world on the left hand side，you're gonna be training this agent。

through using this predictive model so。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_99.png)

we have the agent which picks a initial，state the initial condition right。

position velocity in those context，images and gives you a control an action。

which is the acceleration in the，longitudinal direction and the。

acceleration in the transverse direction，alright so how does it work so this is。

how we train we have a state we feed a，state to the policy you get an action。

then you feed both of them to the world，model right what does the model tell you。

well you need to provide some you know，latent variable we also some possible。

way that the future can you know evolve，then you get a prediction cool you feed。

a prediction to these laws where the，lost is gonna be my cost of the task I'm。

trying to accomplish in my case is gonna，be the summation of the proximity cost。

the one that is telling me how close I，am to other vehicles plus some kind of。

you know cost associated to the beam in，the center of the lane cool so in the。

next state I I send it to the network，then the policy I get the next action I。

feed both of them to the world model you，get the latent variable you get a new。

prediction you send this to the loss and，more prediction like policy world model。

latent variable next guy loss and finish，you do a back propagation to train the。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_101.png)

policy model and doesn't work，what happened so we are basically。

falling outside a manifold the policy，manages to you know crank up those。

actions and give predictions that are，all black and all black is good because。

zero cost right so that's bad okay so，here we actually went outside the road。

and here we actually collided in two，other vehicles so let's maybe try to。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_103.png)

imitate other vehicles so how do you do，that well you can say that the loss is。

gonna be you know the task that we were，trying to accomplish plus some you know。

regularizer which is you know expert，regularizer，what is this stuff so here you try also。

to get the prediction by you know that，you would get by taking a specific。

action as close as possible to the，action the actual future so you do that。

for everyone but in this case you，actually have to kind of remove this。

latent variable because the latent，variable gives you a specific prediction。

it works better if you just work with，the average prediction we trained。

evaluation of the encoder to just remove。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_105.png)

it hmm does it work actually yeah，imitating the expert work so this is。

kind of imitation learning but imitation，learning with you know model day so I。

mean model basing imitation learning you，use your brain in order to try to。

imitate others all right can we do，better yes we can do better and that's。

going to be the end of the class so how，can we add a different kind of manifold。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_107.png)

attractor what am I talking about here，so forward model uncertainty so my。

predictive model outputs a prediction，given you know a state and the action。

and then I have my cost here so this is，for example my cost the point is that，you know there are。

always this cost can go whenever you're，outside the training region the one with。

the red points right so if you are，within the red points as I show you in。

the lab number three when we were doing，regression if you're within this。

training region you have zero variance，right across those points is it go away。

from those training region the variance，increases right guess what the variance。

is differentiable let's run within，descent so we can try to run gradient。

descent over the variance and yeah so，you minimize the variance by using SGD。

so this is my uncertainty regularizer，so I have my predicted my policy which。

is feeding my you know action to the，world model you get this latent variable。

here and you get a prediction also you，get the task cost here which is you know。

the minimization of the lane and，proximity cost yep in there you actually。

can get several models or you can use，some the drop out trick we haven't。

talked about but you can leave the drop，out on during inference such that you。

can have multiple predictions and now，you can compute the variance。

right of these predictions and you，multiply by a thing whatever a lambda。

scaler and then my model uncertainty，regularizer leave some of the two and。

you get the final loss to optimize and。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_109.png)

that's it so that's the whole model，where the final loss is going to be my，DC task。

plus this uncertainty this slides are，going to be in the next slide I give you。

the links so in this one I show you in。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_111.png)

pink that they actually managed to learn，how to drive by minimizing the。

uncertainty of the predictive model so，the action takes an taken by the policy。

are minimizing the uncertainty with，which the predictive network makes。

predictions right what a mouthful but it，works very well and evaluation I'll show。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_113.png)

you just very quickly here in the yellow。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_115.png)

is the original car and the blue is the，car controlled by our policy which got。

lost because they already the other guy，got you know went to a different path so。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_117.png)

our blue guy here has to survive this，jungle of other cars they cannot see us。

right so in this case we are slightly，ahead slightly behind slightly we are。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_119.png)

accelerating a lot and we survived in，the other case is well we are the blue。

guy the yellow one is the original guy，in the in the data and oh we again。

managed to diverge from the original，trajectory but we still survive until。

the end and slides as we were mentioning。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_121.png)

so okay this is like a summary of the，whole thing model predictive policy。

learning with uncertainty repolarization，for driving during dense traffic you。

should have understand everything now so，model prediction like okay and just you。

have the four different points that are，uncertain in the regularizer letting。

dropout large-scale data set and then，you have the additional cost for you。

know trying to mimic the experts，information and these are the links for。

everything so that's the title that's me，collaborators are well main authors we。

are both first outers Micahel and myself，and then division slides are here the。

article is here the code is available on，github on my github and this is a。

website and we also have a poster sorry，it'll be running so so so late but I。

hope you really enjoyed this small，project of ours there were so many。

questions I didn't plan there is another，explanation of this there is another。

explanation of this project on my，YouTube Israel is 20 minutes long maybe。

I've done a better job than today but，maybe I did a better job today since I。

was answering your questions so if there，are no other questions we gonna see each。

other next week and again if someone can，help out with the review of last scribes。

from the lab would be very helpful or，because I I have no idea how to deal。

with this otherwise is the mall is a，word model frozen when training the。

agent yeah as as we have seen last week，do we still have time for questions of。

course any time since when you're，training the network since it's kind of。

like a recurrent architecture are we。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_123.png)

worried about like vanishing gradients，and how do you with with such a complex。

model how do you like address that all，right so it's not that complex as in。

this is two layer neural net so the，policy is very stupid policy like it's。

very tiny the word model is a bit larger，but nevertheless we have batch norm。

which is keep you know helping out，sending things through like the，gradients throw and then。

I think we also used the Samsung，receiver connections because those are。

units yeah so you know the gradients，didn't give us big issues for training。

this model also we are doing 1330 times，steps in the future so it was like three。

seconds in the future given that we，start from I think two seconds in the。

past so we're always like five seconds，window temporal window for training the。

system I didn't quite understand how the，when we're doing the latent dropout how。

that works how that helps us with I，guess would you call it like like。

disentangling the action versus the，latent right so the problem was here。



![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_125.png)

right so the problem was that the fact，that we have access to the future if we。

make a small tiny change in my steering，steering wheel control everything will。

change which is a very large change，right and that MSC will to minimize that。

MSE you know a lot of information will，go through that way because it's a big。

change right so it's very is a brutal，change now and you know if that latent。

variable that way little Bible will try，to to acknowledge the fact that。

everything changes an 80 just changed，slightly right because it's just a tiny。

change of the steering wheel the problem，is that if you're forward if your。

predictive model on this is called，forward model is no longer looking at。

what is the steering wheel then you know，you can steer around but the network。

will not care about what is your control，may instead be you want to have a。

network that if you steer to the left，he's gonna tell you everything steers to。

the right by the fact that you steer to，the left so you had to disentangle this。

and to fix that the thing that really。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_127.png)

worked very well was this one which was，basically half of the time or maybe we。

had some shading I forgot but you know，some some times instead of you know。

sampling the latent variable，while training these automation of。

encoder instead of sampling it all the，time from your encoder sometimes it's。

just simple from the prior distribution，in this way rotation in the future。

cannot be explained by the latent，variable therefore there must be a path。

that connects the action to the future。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_129.png)

state right so if you break this arrow，you have to break this arm if I do this。

switching between this one and the other，you basically Blake you break this arrow。

for you know a fraction of the，iterations and therefore the arrow will。

not actually subsist because it cannot，use it right to make a prediction if。

sometimes it happens sometimes it，doesn't happen the network always sees。

this action right this action is gonna，be always turning left turn right that。

are mystically determing the fact that，is steer to the left to the right this。

is kind of a way to make the network，like see the action when it's performing。

the training yeah this was a big issue，without these things it doesn't work。

because you would have a network which，is not carrying at all something nice。

you can do is gonna be like adversarial，adversarial something you want to want。

to get a network which is gonna be，killing you like if the future changed。

because of the action or not and it said，the prior distribution for the latent。

variable is just like a Gaussian normal，okay all right cool thank you so much。

Yan keeps saying that we sample from，zero that was the previous previous。

version where we actually didn't even，have a variational encoder and we had。

just a encoder which was encoding the，mean so we we didn't have the same thing。

module we didn't have the variance just，we had an encoder which was just giving。

me this latent so that was the previous，version no sampling no V you just F ank。

you encode this guy and so sometimes you，were getting it from the encoder and。

sometimes you were picking it from zero，because we trained this first branch。

with this guy that was not here right so，we first trained this stuff。

deterministically which is or is it here。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_131.png)

so initially we trained these which，means set Z to 0 right so if you set the。

Z to 0 there you go you get this back，deterministic so basically whenever you。

do this dropouts trick you switch back，and forth between the deterministic and。

the stochastic version of the predictive，model，kula sounds crazy I think well yeah I I。

think you should be able to digest this，stuff because you're good you're good。

students it might interest you more，questions yeah al yeah so I wanted I。

just wanted to check my understanding of，latent variable models，it seems that different models use。

latent variables for different，objectives like the auto encoder uses it，to learn a low dimensional。

representation then we AE the，variational auto encoder builds on it to。

regularize the latent space so that it，can randomly sample from the Nathan。

space and then Gans and the model that，we just studied they use it to introduce。

randomness so that when we have the same，input and different outcomes the network。

doesn't have to output an average of the，predictions and so basically here we are。

using latent space to provide more，dimension led to the input to introduce。

randomness to the input so in this case，we have this latent variable to account。

for what cannot be account from the past，array so the point is that you know not。

everything is predictable and so if you，cannot predict everything you're gonna。

make some errors so this latent variable，allow you to tune your algorithm to。

actually you know zero out that error，and later on you can sample this latent。

variable in order to get you know proper，predictions so without the laden bag。

what you are getting that you know，masked version of the prediction it's。

blurry prediction instead in order to，get you know Chris predictions you want。

to refine your average prediction to the，specific case you have at hand right got。

it so it is basically using it to add，dimensionality to the input to make，things more specific。

I wouldn't say dimensionizer to the，import，I would say you add latent variables in。

order to provide the missing information，that would be required for you to make a。

proper prediction got it，good thank you of course more questions。

I know it's so it's so late I'm taking，this was very extreme extremely lengthy。

class I feel sorry more questions I，can't see you hold on stop share screen，okay。

Oh 50 people still here okay what do you，want to know else I also want to check。

my understanding for later was correct，so today tomorrow will tell us something。

that we cannot predict from the future，but you just said if we turn lab。

everything would be like to our right，but you don't want me to tell this。

information you want this information，all it comes from our action yeah。

exactly because if you if you if you，steer to their left everything will turn。

to the right right if you if you're，riding a bicycle and you're doing like。

that you're gonna go you exactly know，how you will evolve right you don't know。

if you're gonna be crashing into someone，and that's gonna be taken care by the。

latent variable and which is gonna be，you know patching your wrong prediction。

due to unforeseen events but everything，that is you know predictable should be。

done by the deterministic branch such，that you use the past information to。

determine what's happening next，but then you can't really name so it's。

like you know you're gonna be me trying，to touch the calm web web-cam here but。

then there is some wind because I open，the window so I go here and it goes。

there I go here and it goes here right，so if there is a additional component it。

is like moving my hand I will have to，deal with that for the specific case so。

I can only go here given that I know，that my finger will go forward from the，past to the future I。

exactly nowhere to go but if there are，additional you know inputs that are not。

under my control then you will not be，able to make accurate predictions unless。

you have some knowledge it's like okay，like going back to the example yan makes。

all the time with a pencil right so the，pen is gonna be falling one direction，let me get the pens。

get the pen if you let it go it's gonna，be falling in one direction goes another。

direction goes the third direction right，so you can first learn you know massive。

Network which is learning the dynamics，of falling right so you learn how a pen。

falls down the only little information，you know - you need to know that you。

can't know in advance is in which，direction it will fall so you're gonna。

have the big ass Network learning the，folding dynamics and then the last。

minimal amount of information that is，missing is in which direction you should。

actually you know initiate this folding，trajectory right so this is how it works。

bid network to learn the big bulk of，prediction little tiny little variable。

right so this latent variable again I，said is something like 16 dimensions。

it's very tiny like a very short vector，which is just providing you the missing。

information to make a sharp prediction，okay okay so to avoid the latent。

variable to tell us information that，should be predictable we are trying to。

approach the regularization term the KO，term from with the help of prior okay so。

yes so the KL term it's necessary for，you otherwise things will explode as we。

have seen in class right if you don't，have the KL this prediction will go as。

far as possible because they don't want，to overlap the second term is going to。

be the actual network will try to，collapse them right so whenever you。

introduce this KL you enforce the bubble，to be having variants of one and also。

all the mean to be close to zero such，that you feel that you know。

fear with little bubbles and then later，on given that now all these fears are。

within this bubble you can simple from，you know a Gaussian distribution like a。

normal distribution from the same size，so that's why we use the KL the part。

that allows you to be you know if you if，you have like if you put a lot of。

strength on the KL you are going to be，also reducing the amount of information。

so you can use that KL as a term to，reduce the amount of information coming。

from the future so that's definitely one，way of regularizing the the latent。

variable the other way is also the other，the other trick we are using is the drop。

out streak for the latent which is，sometimes you know sampling completely。

from the prior and such that now the，backbone the the big massive network the。

deterministic one cannot rely on，information it is you know not always。

present right okay and all this happen，in the training stage of the predictive。

model yeah okay okay yeah thank you，thank you so much yeah yeah could you so。

regarding that forward model uncertainty，is that uncertainty that comes from like。

trying to predict more in the future or，so the uncertainty there I I think I。

went a little faster the uncertainty，coming there is the fact that you know。

whenever you have your policy，trying to control the other guy you can。

you know press a lot the acceleration or，you can you know steer completely like，crazy。

and if you give yeah you know some，actions that are far from the training。

domain of that policy different policies，will reply will will respond in a。

different way right because if you train，several models on the same training data。

and then you test this multiple models，train on this data outside。

the training interval let's say let's，say this is oh I cannot speak with a pen。

in the mouth interval right and then we，had the you know a your test on our。

fryer here right so if you in this，training interval here all the model。

will agree and therefore the variance，across this training interval will be。

very tiny as you go away from the，training interval the variance will。

increase right the nice part is now that，given that this variance is you know。

it's a scalar value you can minimize the，variance by having the action going from。

clear draw here because here the，variance is tiny，right the variance here is minimum and。

here the variance is very large so you，can have actions that might great in。

your action space such that the variance，is minimized right so your variance now。

is your loss you do gradient descent in，action space for variance minimization。

and therefore you can travel no in this，action space which actually is to the。

arc is actually two dimensional right，it's so cool so you have you know X。

Direction y direction you have the day，the hill in this case you can plot the。

variance right so if the variance goes，up here you can go in the center down。

such that in this region where the，variance is low you know that all these。

different models will agree for the，future predictions therefore and those。

actions are coming from you know safe，Riaan right the actions are now coming。

from more like the training points，rather than outside point a training。

region let's say this way yeah right，okay thank you，of course more questions ask me，everything。

Emma Emma how do you say MEA all right，mark，you're done am I gonna be cooking dinner。

I have one question，so suppose we change the context of this，problem from regression to some。

classification problem for example water，predict are we going to crash or not or。

if you want to predict is there high，traffic or not then will the。

effectiveness of latent variables still，be present，like would latent variables improve the。

model even if it were a classification，setting and more because both from what。

I've observed it seems like latent，variables always improve the performance。

in like a generation when we want to，generate something like in generate an。

image or a music synthesis or some，regression prediction but in a。

classification setting how effective，will they be so we are actually working。

on this right now we are working on，classification，and maybe we can hear about more about。

this next week when we're going to be，talking about language this is actually。

was another student of Leon is working，on using latent variable models for。

performing classification that allows，you to pick for multiple multiple。

options so I guess you're gonna hear，about this one，not not today。

or you can ask yuan next time but again，we're gonna be I think we make it we can。

mention this next week，okay thanks all right，that's it all right have a good night。

have enjoy your meal I stay safe wash，your hands and the pen I don't was not。

sanitized but I haven't used it so good，point，don't touch your face don't on stay safe，why，[Music]。

how can you get more out of this course，right overall so let me give you a few。

suggestions first comprehension if，something was still not clear just ask。

me the question a section below the，video I will answer every question so。

you will get it eventually if you'd like，to I get more news about the field。

things I do on in terms of educational，content and things I find interesting。

you can follow up on Twitter and there，you have my handle I've seen that if。

you'd like to have updates about newer，videos don't forget to subscribe to the。

channel and activate the notification，bell if you actually like this video。

don't forget to put a thumbs up it helps，as well recommending this video to other。

people if you'd like to search the，content of this lesson we have our。

English transcription which is connected，directly to this video so every title in。

the transcription is clickable if you，click on the title you get the right。

director to the correct location on the，video in the same way each section of。

the video is the same title is in，transcription so you can go back and。

forth maybe English is not your first，language but l'italiano habla espanol。

new Obama speak Korean have no idea how，to speak Korean well we have several。

translations of this material available，on at the website so and we are also。

looking for more translations if you can，help as well it's really important that。

you actually try to do some of the，exercises and you play around with the。

notebooks and the source code we，provided in order to internalize and。

understand better the concepts we，explained during the lessons contribute。

this is really giving you the，opportunity to show your contribution。

for example you find some typos in the，write-up so you find some bugs in the。

notebooks you can fix those and you know，be part of this whole project by sending。

me a poor request on github or letting。

![](img/a3cd1ce3e8d76d5b64be81b79e17ee79_133.png)