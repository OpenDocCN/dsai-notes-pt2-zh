# P52：SciPy 2018视频专辑 (P52. Introduction to Geospatial Data Analysis with Python _ SciP - GalileoHua - BV1TE411n7Ny

 Welcome everybody to the Geospatial tutorial。 I'm Sir Dre from the University of California。

 Riverside and it's my privilege to be one of the co-chairs for the SciPy meeting。 So welcome。

 How many of you this is your first SciPy？ Excellent。

 So that means it's your first workshop here as well。 Good。

 This is going to be a joint effort between myself。 You want to introduce yourself to yours？



![](img/81e8c90c191b11ba7052bce0b0522fb5_1.png)

 Yeah， so I'm Joris。 I'm from Belgium working in France currently and one of the Geopandas meetings。

 And then we also have Levi Wolf， University of Bristol， works on the Pycel team and Danny。



![](img/81e8c90c191b11ba7052bce0b0522fb5_3.png)

 Arevis Bell， who's at the University of Liverpool also on Pycel。 So this is a joint effort between。



![](img/81e8c90c191b11ba7052bce0b0522fb5_5.png)

 Geopandas and Pycel。 First time we're doing this。 So it should be exciting。 So it's going to be a。



![](img/81e8c90c191b11ba7052bce0b0522fb5_7.png)

 four-part session。 Yours will start and Danny will take over， then we'll have the break， probably。

 and then the second half it'll be myself and Levi。 So because there's four of us， we have。

 chances to help if people are stuck with the installation or have questions while we're going。



![](img/81e8c90c191b11ba7052bce0b0522fb5_9.png)

 through this。 Are we going to talk about the binder？ Yeah， so if you don't get everything。

 working and installed but you want to follow now because you are going to start， you can try。

 There is a button on the Geop repo， launch binder， and normally， so that should create。



![](img/81e8c90c191b11ba7052bce0b0522fb5_11.png)

 a working environment with all the materials online。 It may not be the fastest。

 but it should be a backup， if you case it is not working locally。

 So that's something that you can try。 Maybe to start to get a little bit an ID who has already used Geopandas before。

 Some of you who has already used PySAL or related libraries a few bit less。

 For those that didn't use Geopandas yet， did you already use， Panda's library itself？ Yes。

 most of you did。 So that's good because we will， assume a little bit that you are familiar with Panda。

 We won't explain everything of Panda， so that's， will be helpful that you are familiar with that。

 So we are going to start with， so the first part will be an introduction to Geopandas and related libraries to start working。

 with your special data， reading in data， doing some queries on it， to some manipulations。

 and then after the break we'll go to the PySAL part which is more than the special data analysis。

 Data science parts。 So to get started， so in case， yeah that's a question。

 who is not familiar with Jupiter notebook？ Everybody is familiar。

 you may be used it for the previous tutorial as well， so that's good。 So。

 we start the notebook in the directory that you downloaded or cloned with Git。

 then you should see something like this， and it is a bit。

 So we are going to start with the first notebook， notebook one， and introduction to Geospatial data。



![](img/81e8c90c191b11ba7052bce0b0522fb5_13.png)

 [pause]。

![](img/81e8c90c191b11ba7052bce0b0522fb5_15.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_16.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_17.png)

 Is this big enough to be readable in the back？ I can increase it a bit more。



![](img/81e8c90c191b11ba7052bce0b0522fb5_19.png)

 Is there a way to turn off those ways？ Yeah， probably yes。 That's better。 Okay。

 so maybe another question。 Who have you followed the Cartopite tutorial yesterday？ A few。

 So you can explain what the difference is between， roster and vector data。

 Somebody wants to try or give an example， but are the examples that， were given in the tutorial？

 Yeah， indeed。 So the vector data， it's here in the title as well， choose spatial vector data。

 The tutorial will mostly focus on that kind of spatial data where we。

 have polygons like neighborhoods in a city， points， line strings。 So that's the type of。

 geospatial data that we will mostly see in this tutorial。 On the other hand， we also have roster。

 data， I think typically satellite images， a variety of images with pixels。

 So we will mostly focus on， vector data。 And because vector data， if you have points。

 you have a set of points with， let's say， points of interest within a city。

 you often have additional information about those， points or polygons。

 You have attributes about those points and that fixed aid。 You typically。

 want to put this in a table where you have different attributes for each point。 So each row。

 is the metadata linked to a certain location in space。 So therefore， that fits very natural。

 in a table and then in Python using a panel's data frame。 So that's the kind of data that we。



![](img/81e8c90c191b11ba7052bce0b0522fb5_21.png)

 will start with。 And the first thing， if you want to start with that， of course。

 is we have to get some， data。 And in JS， in special data， you have many different file formats。

 also some very specific， file formats， like shape files， geo JSON files， geo package files。

 And geo pandas provides some， provides an easy way to read in all those different data formats using the。

 GEDA library under the hood。 So the GEDA library is used by in it's a very like base library for。

 the full open source geo ecosystem， used in many libraries applications for reading and writing。



![](img/81e8c90c191b11ba7052bce0b0522fb5_23.png)

 data。 So here's a small example in the material that you download。 We provided the zip file that。

 we got from natural earth data with all the countries of the world。 So we can use the。



![](img/81e8c90c191b11ba7052bce0b0522fb5_25.png)

 geo pandas with file function to read in those data。 And if you look at the first few rows。



![](img/81e8c90c191b11ba7052bce0b0522fb5_27.png)

 and you see it's a data set， all the countries that are all the name of the countries。

 content on extocated population GDP。 And then here， there is a column called geometry。 So that's。

 important to see， I have to know， because we read it with geo pandas， we go back to the geo data。

 frame， I will explain a bit of difference with the normal data frame。

 There is here a geometry column， and in this case。

 it are polygons because our countries are polygons。 We can also quickly plot。



![](img/81e8c90c191b11ba7052bce0b0522fb5_29.png)

 it。 So you will see we have all the countries of the world。



![](img/81e8c90c191b11ba7052bce0b0522fb5_31.png)

 So those things I explained。

![](img/81e8c90c191b11ba7052bce0b0522fb5_33.png)

 Yeah， for sure。 It's very simple for each of us。 But if you would have another data set， I mean。

 this is called the known data data。 The data set is in， so you can call it correctly， or is it。

 small， or you don't want to find anything？ The plot method itself is naive to that。 It will just。

 plot the coordinates that it gets on the map。 But there are， we will see later on。

 make us to confirm and make sure that it's okay。 But that's something in Jupyter that you have to。

 do yourself， to make sure that both are in the same coordinate system and things like that。



![](img/81e8c90c191b11ba7052bce0b0522fb5_35.png)

 So what we did get， what we got， the countries data set is geo data frame。



![](img/81e8c90c191b11ba7052bce0b0522fb5_37.png)

 And as I already explained， so we have our geometry column， and then the other columns are at the。



![](img/81e8c90c191b11ba7052bce0b0522fb5_39.png)

 attributes of those geometries。 Some special things about this compared to a normal data frame。

 is that you can always access this geometry column with a dot geometry attribute。



![](img/81e8c90c191b11ba7052bce0b0522fb5_41.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_42.png)

 And this gives us a geo series。 So it's like geo data frame is a subclass of a data frame。

 geo series is a subclass of a series。 So it has all functionality of a normal series， but it。

 adds some additional functionality， some additional methods and attributes specific。

 for the type of data， for the geo spatial data。 So as a small example， we can get the area。



![](img/81e8c90c191b11ba7052bce0b0522fb5_44.png)

 of each polygon with the area attribute on our geo series。 And we will see later on in the。

 tutorial， many other methods that are available on the geo data frame and the geo series。



![](img/81e8c90c191b11ba7052bce0b0522fb5_46.png)

 It's of course still a data frame。 So we can， as everything that you know from using pandas。



![](img/81e8c90c191b11ba7052bce0b0522fb5_48.png)

 will still work。 Like we can access the population column and calculate the mean。



![](img/81e8c90c191b11ba7052bce0b0522fb5_50.png)

 like this。 Or what we can do is we can filter our data set， we can take a subset of our data set。



![](img/81e8c90c191b11ba7052bce0b0522fb5_52.png)

 in this case。 So I get a continent column， I compared with Africa。 So this will give you true。



![](img/81e8c90c191b11ba7052bce0b0522fb5_54.png)

 files。 It will give you a Boolean series。 And because it's a Boolean series， we can use it to。



![](img/81e8c90c191b11ba7052bce0b0522fb5_56.png)

 filter our original data frame like this。 So to only get all the countries that are。



![](img/81e8c90c191b11ba7052bce0b0522fb5_58.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_59.png)

 that have in the continent column Africa。 And in that way you can easily use a familiar pandas。

 syntax to take a subset of your data。 In this case， all the countries of Africa。



![](img/81e8c90c191b11ba7052bce0b0522fb5_61.png)

 Yeah。

![](img/81e8c90c191b11ba7052bce0b0522fb5_63.png)

 So here a summary of what I said。 So the geo data frame will allow those specific。



![](img/81e8c90c191b11ba7052bce0b0522fb5_65.png)

 spatial operations。 So up to now we have seen a small example with polygons。



![](img/81e8c90c191b11ba7052bce0b0522fb5_67.png)

 But as we already said in the beginning， you know， set points can have lines or line strings in。

 the terminology that we use here。 Or you can have combinations of multiple points， multiple lines。



![](img/81e8c90c191b11ba7052bce0b0522fb5_69.png)

 multiple polygons， and a single geometry。 So in this case for our countries， it's a bit。



![](img/81e8c90c191b11ba7052bce0b0522fb5_71.png)

 a long representation。 But so this was a polygon。 So now we are going to import a few other data sets。



![](img/81e8c90c191b11ba7052bce0b0522fb5_73.png)

 also from natural earth websites。 So everyone with some cities， cities are represented by points。



![](img/81e8c90c191b11ba7052bce0b0522fb5_75.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_76.png)

 and some rivers， which are represented by a line string。 So it's a line。

 If I would get here changes print with a type， you will see that this is a shapely， line string。

 So shapely is a library that Jupyndas uses under the hood to， represent those points。

 lines and polygons， those geometry objects。 And it's also the library that。

 provides all the specific geo spatial methods。 It actually does it by itself interfacing to the。

 geo-sea library， which is for example also used by Post。js。 So it's actually the same。

 sea library under the hood as Post。js that provides all the functionality for geo-pandas。



![](img/81e8c90c191b11ba7052bce0b0522fb5_78.png)

 Up to now we read data in from a file。 If needed， you can also construct some points or polygons。



![](img/81e8c90c191b11ba7052bce0b0522fb5_80.png)

 yourself。 For example， here with the point you provide X and Y or longitude length latitude。



![](img/81e8c90c191b11ba7052bce0b0522fb5_82.png)

 or with a polygon you provide a list of coordinates。 So very easy。

 Further on in the tutorial we will also see quite a lot of methods that are available on the geo-data。

 frame。 Important to remember is that often those will also work on individual objects。 For example。

 for the polygons I saw here a bit above the area that you can with the area attribute。



![](img/81e8c90c191b11ba7052bce0b0522fb5_84.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_85.png)

 gets the area of each。 So I will write it here with the area attribute。



![](img/81e8c90c191b11ba7052bce0b0522fb5_87.png)

 get the area of each polygon in my series。 If I have a single polygon and I want to know。



![](img/81e8c90c191b11ba7052bce0b0522fb5_89.png)

 this single polygon I can also get the area of that。 So it's mostly a one-to-one mapping of。

 methods for the geo-series or the individual objects。 So then related to any question we had before。

 So people who follow the card by tutorial will now be。



![](img/81e8c90c191b11ba7052bce0b0522fb5_91.png)

 quite familiar with the importance of projection system for having something on the map。

 Geo-planets is for the rest as I said naive to your coordinate reference system。 It will not。

 do automatic reprojection or something like that。 So you need to ensure yourself that。

 for example if you are putting multiple things together that they both have the same。

 current reference system。 But it provides some functionality to do that。

 So the geo-data frame has a geo-series as well as a CRS for coordinate reference system attributes。

 And in this case you will see here for the countries that we have EPSG 4326 which indicates that it's。

 the most widely used just limited latitude based on VGS84。



![](img/81e8c90c191b11ba7052bce0b0522fb5_93.png)

 We can then plot this just without any specific map projection。



![](img/81e8c90c191b11ba7052bce0b0522fb5_95.png)

 But we can also change。 I will hear。 For example and we can use the two CRS methods。



![](img/81e8c90c191b11ba7052bce0b0522fb5_97.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_98.png)

 To convert our geo-series from one code reference system to another。

 The easy way is to provide the EPSG code so every。

 or most code in preference system have such a code。 Here I put a link of one。

 On the website you can also search for the correct code that you need。

 But in this case I'm going to convert our， coordinates to that indicator or volt indicator in this case。

 So with two CRS you will see that if you look at the data。 So before。



![](img/81e8c90c191b11ba7052bce0b0522fb5_100.png)

 now you see here numbers within the 0 to 180 range because this was in latitude long latitude。

 If you now look at the new one you will see now this range is much higher。



![](img/81e8c90c191b11ba7052bce0b0522fb5_102.png)

 And if you also plot it you will see that it has now a different projection。



![](img/81e8c90c191b11ba7052bce0b0522fb5_104.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_105.png)

 And Greenland is much bigger than it was before。 In the counterpart tutorial we saw where those projection systems or map projections。



![](img/81e8c90c191b11ba7052bce0b0522fb5_107.png)

 and in general those current reference systems are important。

 For example if you want to plot things you get all different options。

 Also there is conversion functionality also important if you。

 get data from different sources and often they are provided in different reference systems so。

 you want to convert them to a common one or specifically for。



![](img/81e8c90c191b11ba7052bce0b0522fb5_109.png)

 for geopandas。 The second point here is also important。

 So you can calculate distances with geopandas but it will just assume that your coordinates are。

 in the Cartesian plane and for that if you want to have a distance metric that you want to understand。

 like how many kilometers is my two points from each other you typically want to be in meters and。

 not in degrees。 So if you have a data set in latitude and longitude latitude and you want to。

 calculate distances in meters with your pandas you need to convert it to a current reference system。

 that has a meter unit and not in degrees。 So that's another good reason in geopandas that you。

 might want to do this。

![](img/81e8c90c191b11ba7052bce0b0522fb5_111.png)

 Okay so to end this initial introduction and then we'll get to some exercises。

 Here is an example how you can plot different things together because I already showed how to。

 plot the countries data sets。 We will assign the result to an axe which is a map of deep axe。

 axis objects so we can use that to add the other plots as well by here providing that I want to。

 plot my rivers and plot my cities on the same map。 And for the west it's also based on map tips so。

 the typical ways to style the plots are available here as well。 In this case I say I don't want any。

 fill no face color。 I don't want to fill map polygons I only want to have an edge around it。



![](img/81e8c90c191b11ba7052bce0b0522fb5_113.png)

 and the cities have to be in red so that looks then something like this。 So rather at the points。

 the line swings and the polygons。 Okay are there any questions up to now about this part？

 If not we will go to the notebook with a bigger exercise so that you can start practicing a bit。



![](img/81e8c90c191b11ba7052bce0b0522fb5_115.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_116.png)

 It's this one so case conflict mapping that you can open。

 I will give you a short introduction about the data set and then you can start with the exercises。



![](img/81e8c90c191b11ba7052bce0b0522fb5_118.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_119.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_120.png)

 So the data set that I provided here is a data set about artisanal mining sites in eastern。

 Congo so it's an organization the IPS from which I got data did like visits of mining sites and。

 inspected the different mining sites of their data on how many workers are the active if it's。

 controlled by an armed group or not what minerals are they mining so it's a survey on mining sites。

 in Congo。 So you have some some background there。 They provide a。



![](img/81e8c90c191b11ba7052bce0b0522fb5_122.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_123.png)

 yeah public API to get the data。 So I put here an example how you can do this with。

 directly interfacing with their API but let's start with the exercise to。



![](img/81e8c90c191b11ba7052bce0b0522fb5_125.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_126.png)

 read the geogation data because you can also download is a geo-adjacent。 So this data set is。

 available in the data directory in the repo so the first exercise is to read the data from the。

 geogation file and inspect the first inspected bits。 The final note before you can start。

 So I would advise you to really try it yourself but if you are stuck and we are not available。

 I would first try to ask us to give you an explanation or give you a hint but if you want to see the。

 solution or you're already and you want to compare it you can always comment this out and run the cell。

 and you will see a possible solution。 It will not be exactly the same as your solution maybe。

 that doesn't mean that your solution is bad because there are often several ways to do something。

 but in that way you can check it and you can maybe already go a bit further if you are。

 so much faster than as we are going or。 So you can try with that exercise if you're ready。

 you can try run the code here and do the exercises below as well so you can certainly already go until。



![](img/81e8c90c191b11ba7052bce0b0522fb5_128.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_129.png)

 here point two。 I will go through some of the first exercise and highlight some。



![](img/81e8c90c191b11ba7052bce0b0522fb5_131.png)

 questions that we had。 So to start with to read in a file we use jupyndas read file。



![](img/81e8c90c191b11ba7052bce0b0522fb5_133.png)

 and then we pass the directory or the file named the path， like this and we call it in data visits。

 So we know the panel's functionality to check the first few rows and just to give you a bit。



![](img/81e8c90c191b11ba7052bce0b0522fb5_135.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_136.png)

 so an ID I will show that later。 So because there are quite some columns and we don't need all。



![](img/81e8c90c191b11ba7052bce0b0522fb5_138.png)

 the columns for the tutorial so I provide here some code to select a subset of the columns。



![](img/81e8c90c191b11ba7052bce0b0522fb5_140.png)

 and if you now look at it so what is the data that we have here so we have point data and so our。

 minimal our mining sites are points。 The communication between a world is mine there。

 whether there is an armed group， a number of workers and then a name of the mine so ID。



![](img/81e8c90c191b11ba7052bce0b0522fb5_142.png)

 etc and a date when it was visited。 I provided here a little bit of code to create a subset of。



![](img/81e8c90c191b11ba7052bce0b0522fb5_144.png)

 the data so we are only going to take those that were visited by。



![](img/81e8c90c191b11ba7052bce0b0522fb5_146.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_147.png)

 IPIS so by again doing a boolean filtering operation here where for all rows where this column contains。

 the IP string and also where there are at least more than zero workers so the active mines。



![](img/81e8c90c191b11ba7052bce0b0522fb5_149.png)

 and I still sorting by date some mines for us visited several times I did the。

 credit by grouping by the code and taking the last one so the last if mine was visited several。

 times take the last one and finally yeah converted back to the data field because by doing the group by。

 we lost the fact that it was a geo data frame。 So now what we have here the data here has。



![](img/81e8c90c191b11ba7052bce0b0522fb5_151.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_152.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_153.png)

 still and so we have now a data set with a bit more than two thousand mining sites。



![](img/81e8c90c191b11ba7052bce0b0522fb5_155.png)

 The other data set that we are going to use throughout this exercise is a data set on protected。

 areas so natural national parks in the in the in Congo so yeah we again provided the link。



![](img/81e8c90c191b11ba7052bce0b0522fb5_157.png)

 where we got the data um I will just show here the results so you can。



![](img/81e8c90c191b11ba7052bce0b0522fb5_159.png)

 if you do it similarly sorry。

![](img/81e8c90c191b11ba7052bce0b0522fb5_161.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_162.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_163.png)

 whoops I have here apparently not the latest version。



![](img/81e8c90c191b11ba7052bce0b0522fb5_165.png)

 so if we did it similarly as how it was。

![](img/81e8c90c191b11ba7052bce0b0522fb5_167.png)

 sorry group。

![](img/81e8c90c191b11ba7052bce0b0522fb5_169.png)

 this zip file。

![](img/81e8c90c191b11ba7052bce0b0522fb5_171.png)

 yeah thank you so this should work I think no so apparently so yeah the same thing。



![](img/81e8c90c191b11ba7052bce0b0522fb5_173.png)

 apparently some people already had that problem。

![](img/81e8c90c191b11ba7052bce0b0522fb5_175.png)

 the zip file was just renamed constant another bit it was zipped as conservation。



![](img/81e8c90c191b11ba7052bce0b0522fb5_177.png)

 flash rdc blah blah blah inside the zip file it still has different names。



![](img/81e8c90c191b11ba7052bce0b0522fb5_179.png)

 ah okay sorry for that um so let's go to um group， quickly check and the。



![](img/81e8c90c191b11ba7052bce0b0522fb5_181.png)

 so if you look in the data directory。

![](img/81e8c90c191b11ba7052bce0b0522fb5_183.png)

 um， yeah so um normally as if files also work like。



![](img/81e8c90c191b11ba7052bce0b0522fb5_185.png)

 I already understand okay so the problem is indeed。



![](img/81e8c90c191b11ba7052bce0b0522fb5_187.png)

 shape files are annoying that's actually the reason。

 because shape files say you um for those that are not familiar with shape files it's a file。

 format but it's not a file it are actually multiple files that you always need to have together。

 that's the reason that people often make it a zip file or an archive another archive。

 but then yeah depending on how you zip it and the support for reading it directly from a zip。

 archive is not I mean it works because we used it in the previous notebook but it doesn't work。

 always depending on if it's still in a sub folder in the in the in the zip file or things like that so。

 in case it doesn't you don't get it working with the zip with the archive you can simply unpack it。

 and then point to the uh direct you or the or one of the shape uh the shape inside it doesn't matter。

 both work um yeah and that will work um。

![](img/81e8c90c191b11ba7052bce0b0522fb5_189.png)

 so I suppose that this will not work because I didn't unzip it if you want it from the zip file。

 directly I put here because it's a bit complex in this case I actually put it here you can do it。



![](img/81e8c90c191b11ba7052bce0b0522fb5_191.png)

 with this line but since that's quite complex the easier thing in this case is to un unpack。

 the zip the archive and then you can read it like this um so you can either copy paste this one。

 and comment that one that will work with the zip file we provided or unpack it and um do it like this。

 um just so。

![](img/81e8c90c191b11ba7052bce0b0522fb5_193.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_194.png)

 so to quickly have a idea of what is inside these datasets um so we do a plot so you recognize a。



![](img/81e8c90c191b11ba7052bce0b0522fb5_196.png)

 little bit the the outline of kunghu in here so here are polygons and each polygon is one。

 national park so for example if we oops if you look at the protected areas heads。



![](img/81e8c90c191b11ba7052bce0b0522fb5_198.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_199.png)

 um you will see that the there are quite some columns but the last one our geometric column。



![](img/81e8c90c191b11ba7052bce0b0522fb5_201.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_202.png)

 are polygons um and somewhere in it there is a name of the name of the national park okay。



![](img/81e8c90c191b11ba7052bce0b0522fb5_204.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_205.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_206.png)

 we'll give you again a bit of time to get here and you can further continue with。



![](img/81e8c90c191b11ba7052bce0b0522fb5_208.png)

 with this part of the exercise。

![](img/81e8c90c191b11ba7052bce0b0522fb5_210.png)

 so if you didn't succeed with reading in the files the working line was inside the solution。



![](img/81e8c90c191b11ba7052bce0b0522fb5_212.png)

 um， okay um yeah you have quite some material so it's not uh no problem if you're not ready yet。



![](img/81e8c90c191b11ba7052bce0b0522fb5_214.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_215.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_216.png)

 that will go quickly through some of the solutions and then we will switch to doing some actual。



![](img/81e8c90c191b11ba7052bce0b0522fb5_218.png)

 special operations so， you might already have noticed so the wait the data if you check the coronet reference system of both。



![](img/81e8c90c191b11ba7052bce0b0522fb5_220.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_221.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_222.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_223.png)

 so you can see so both have a different coronet reference system so um for example um。



![](img/81e8c90c191b11ba7052bce0b0522fb5_225.png)

 yeah it's actually in the the second so i will first show this so if you would like to make。



![](img/81e8c90c191b11ba7052bce0b0522fb5_227.png)

 because we now have the areas and the points of the same area so to see their relationship we。

 want to plot them together how can we do this we can uh plot our data um this returns and。

 and uh not for deep access um and then on um i also want to plot the protected areas。

 on this axis and let's say that i want to use a green color because they're national parks。



![](img/81e8c90c191b11ba7052bce0b0522fb5_229.png)

 um so you already see if you told it because q-a-man is naive to the current reference system。

 you see it doesn't match so we need to first uh convert our um two data sets to a common。



![](img/81e8c90c191b11ba7052bce0b0522fb5_231.png)

 reference system another reason。

![](img/81e8c90c191b11ba7052bce0b0522fb5_233.png)

 that we want uh would like to uh to do this， is if you want to do distance based calculations um for example here we are going to import from。

 shapely a point to create a single point like this um so in this case。

 i need to use those coordinates but be careful um so in jubyana and same in carterpai it's always。

 longitudes latitude so x and y so be careful about the the order which you put is here so the。



![](img/81e8c90c191b11ba7052bce0b0522fb5_235.png)

 uh 1。66 is uh south so north south is our y and we need to put this uh last i think if i'm not。



![](img/81e8c90c191b11ba7052bce0b0522fb5_237.png)

 mistaken so like this and then we come at the question was calculate the distances of all minds to。



![](img/81e8c90c191b11ba7052bce0b0522fb5_239.png)

 this point and then find the five smallest ones so the five minds closest to koma koma is。

 one of the bigger cities in the key group province near the border with randa。

 so how do you calculate this we have our uh mine sites we can use the distance。

 method for this um and if you give it a single point it will calculate the distance for each。

 of our points in the data sets to um to uh um to go by so and if you want now want the the five。



![](img/81e8c90c191b11ba7052bce0b0522fb5_241.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_242.png)

 closest vendors so they want the smallest distances we can for example sort those。

 um so they will be ascending so the five first values are here but of course 0。38 it doesn't say。



![](img/81e8c90c191b11ba7052bce0b0522fb5_244.png)

 that much in degrees so if you want to use jubyana with distances you again need to convert your。

 current reference system to something in units that has a meter as unit and not in longitudes。



![](img/81e8c90c191b11ba7052bce0b0522fb5_246.png)

 latitudes so now so both are reasons to to convert our current reference systems。



![](img/81e8c90c191b11ba7052bce0b0522fb5_248.png)

 so let's convert them so the first one was um is already I showed before so the。



![](img/81e8c90c191b11ba7052bce0b0522fb5_250.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_251.png)

 long detletitudes here um apparently so the um was provided by the data as we downloaded。



![](img/81e8c90c191b11ba7052bce0b0522fb5_253.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_254.png)

 was in uh world uh makator um and we will both uh convert both to the local detention so typically。



![](img/81e8c90c191b11ba7052bce0b0522fb5_256.png)

 if you have data that are not spanning the full world but a certain country or certain city and you。

 can use um the local detem zone and your um special curve so that you won't have big distortions in。

 in the shapes or in the distances uh that you calculate as long as your data are relatively um。

 fitting uh or proper for that utem zone so again you can look here at the link that will indicate。



![](img/81e8c90c191b11ba7052bce0b0522fb5_258.png)

 for which area this utem zone is is appropriate uh how do you convert our data so remember we can。



![](img/81e8c90c191b11ba7052bce0b0522fb5_260.png)

 use a two crs method um and then it's provided here we want to oops sorry we want to use this uh。

 epsg code so we can provide that here like that and that will convert so our data was in not uh。



![](img/81e8c90c191b11ba7052bce0b0522fb5_262.png)

 long as the latitude and now you see uh this is no longer the case so we can call this utm。



![](img/81e8c90c191b11ba7052bce0b0522fb5_264.png)

 I will then quickly show the other one as well oops so we can do this for both so for both the data。

 the mining sites are the protected areas and if we now uh plot them together I will see now they。



![](img/81e8c90c191b11ba7052bce0b0522fb5_266.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_267.png)

 are in the same area um I will give this green color um like that and make the points maybe a bit。

 smaller so we can use here at the typical map or clip um uh keywords to style our um is that smaller。

 yes um like that we can for example give it some alpha to have it um overlay。



![](img/81e8c90c191b11ba7052bce0b0522fb5_269.png)

 yeah there are too many points to really see the effect of this but so you can use at the typical。



![](img/81e8c90c191b11ba7052bce0b0522fb5_271.png)

 map or clip functionality in this case we want to maybe also um set our uh axis off if we don't want。



![](img/81e8c90c191b11ba7052bce0b0522fb5_273.png)

 so what this function will do is just remove the full um box around it with the because in this。

 case those those uh x and y labels are not that's uh interesting so we can this set is off。

 um and we can also make it for example a little bit bigger um let's say 15 15 so like this。



![](img/81e8c90c191b11ba7052bce0b0522fb5_275.png)

 um so the next exercises I try to do this a bit in a few steps to quickly customize the plot a little bit。



![](img/81e8c90c191b11ba7052bce0b0522fb5_277.png)

 um so you can always go through if you want those exercises but um for the tutorial now we will。



![](img/81e8c90c191b11ba7052bce0b0522fb5_279.png)

 switch to um some actual spatial operations and for that you can uh open the second notebook uh so。



![](img/81e8c90c191b11ba7052bce0b0522fb5_281.png)

 on book two spatial operations uh relationships and operations how's that can people read these。



![](img/81e8c90c191b11ba7052bce0b0522fb5_283.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_284.png)

 how about at the very very back can people read these more or less yeah no binoculars required。

 cool all right well so welcome everyone to the second part of the works of the tutorial i'm。

 Daniel Rebusbel from the University of Liverpool and in this second session what we're going to do is。

 looking at um what's called spatial relationships or spatial predicates so how can we put in relation。

 different observations that have a location um pinpoint right so before anything else let's go ahead and。

 import pandas and japanas and let's read all of the data to make our life easier later。



![](img/81e8c90c191b11ba7052bce0b0522fb5_286.png)

 um and this is almost like going back to um you know to middle school when you had different。

 shapes and different objects and you you wanted to combine them in in different ways so there's。

 um there's a bunch of different operations we can do in the japan the supports um and the。



![](img/81e8c90c191b11ba7052bce0b0522fb5_288.png)

 ones we're going to look at today are of these kinds so if we have two objects and these two objects。

 could be a polygon or a point or a line so all vector um objects we can check whether one is within。

 another one we can check whether to touch each other we can and that you know that could be for。

 the case of polygons which we'll build up later on in terms of the contiguity concept that certain。

 Levi will will look at later um or whether a line is touching another polygon or the two lengths。



![](img/81e8c90c191b11ba7052bce0b0522fb5_290.png)

 crosses so crossing of objects and again that could happen between two lines if you're looking at roads。

 or streets that could be very useful or if you have a polygon and a line as we'll play in a little bit。

 or whether there's an overlap and so on so this is a few examples there's a whole list um of spasal。



![](img/81e8c90c191b11ba7052bce0b0522fb5_292.png)

 relations and like for everything that matters in life there's a page on Wikipedia for that so。



![](img/81e8c90c191b11ba7052bce0b0522fb5_294.png)

 um i won't bother you a lot more with that for now um so let's start the way we've designed this。

 is first we're going to look at these relationships at an individual level so at an at an atomic level。

 so say you have a polygon or you have a point or a line and you want to check whether that point。

 is within a polygon or whether the line is crossing the polygon and then that's useful and conceptually。

 i think for me at least is is the more useful way to get my head around what japan is at the。

 end of the day is doing but then in most cases you won't have one polygon or you won't have one line。

 you'll have a whole street network which is made up of segments and you want to check for each of。

 them and you don't want to do that manually so japan does makes it very easy to broadcast those。

 operations across a lot of observations so before anything let's get started with um。



![](img/81e8c90c191b11ba7052bce0b0522fb5_296.png)

 atomic relationships so you can tell that it wasn't me it was from belgian on the team that wrote these。

 exercises and let's just pick a random example here and pick the country of belgian。

 and then we can actually well actually i'll first go over what this does so why are we doing we're。

 querying the country's data data frame and we're keeping all of the observations where the name。

 column equals belgian which there's only one last time i checked in the world and then for the entire。

 row we keep only the geometry column right and then that will still give us a geo data frame。

 and because what we want to query exactly is the geometry we use this helper here called squeeze。

 which if there's only one observation in a geo data frame will squeeze it into geo series。

 and because that's only a single column it'll really squeeze it into the。

 geographic object so if we do that uh the notebook has a really nice rendering um printing method so。



![](img/81e8c90c191b11ba7052bce0b0522fb5_298.png)

 when you just run belgian you'll get the shape of belgian so object number one let's do the second。



![](img/81e8c90c191b11ba7052bce0b0522fb5_300.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_301.png)

 one paris uh there's another member of the team that happens to work in paris even though he's not。

 french um so let's pick paris and brussels as two points and that'll give us two um point objects。

 right and the approach we take to do that is exactly the same we query the data frame we keep the。

 geometry only and then we squeeze it into the geographic object yeah quick question so when。

 you just created that map of belgian there you didn't call map bot mode uh so there's a built-in map。

 yeah yeah so the question is very good point i just said belgian and all of a sudden it plots。



![](img/81e8c90c191b11ba7052bce0b0522fb5_303.png)

 belgian i didn't have to say belgian plot right and the reason is because um so actually let me。

 very quickly so you're the difference yeah so if i do these it's gonna print the polygon。



![](img/81e8c90c191b11ba7052bce0b0522fb5_305.png)

 and then it's gonna plot the polygon but because belgian is already the polygon object there's a。



![](img/81e8c90c191b11ba7052bce0b0522fb5_307.png)

 built-in rendering quick print on the notebook that will print the polygon um and this is only just。

 for a quick check-in because you can't really use it to combine different shapes or anything it's not。

 um it's just a quick look up so to speak this is built into geo canvas not user。

 wow that's a good question yeah so just like a rich representation of the shape。

 yeah if you want to see the coordinates you need to do a quick statement yeah no i'm just saying that。

 this must be part of the package of the imported piece yes yeah but it only works on Jupiter。

 there only works on a notebook or in the rich console display it's a shapely shapely special。

 pretty repertive for you yeah so it's equivalent to i don't know if you've noticed pandas data frames。

 if you print them on an interpreter they'll print as a string if you print them on the notebook they'll。

 render as a nice html table this is equivalent to that yeah yeah so then we do the same for two。



![](img/81e8c90c191b11ba7052bce0b0522fb5_309.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_310.png)

 points paris and brussels and we can see that you know that gives us also a similar representation but。

 because it's a point it's not terribly useful unless you have multiple points or um more complicated。

 point objects right but it's there and sometimes i actually use it a lot when you have to uh when you。

 don't know your data set and you want to make sure that it's what you think it is and if you think。

 it's a point it'll print a point at least you're in your own business um and then finally let's。

 create so we have two points we have a polygon let's create a line for that what we do is we import。

 the the class line string from shape please so this is another geographic or geometric object。

 it's really the API is really neatly designed so all you have to pass is well you can create it in。

 different ways but the simplest one is you just pass a list of separate points and i'll give you a。

 line that goes from point one to point two and so it's i mean in this case we're just creating a line。

 that goes from Paris to Brussels and same as with the other ones again this line is not terribly。



![](img/81e8c90c191b11ba7052bce0b0522fb5_312.png)

 complex so this doesn't help us a lot but if you had a you know more intricate trajectory it would。

 still render it and it can be useful to to explore and then we can also combine so we have once we。



![](img/81e8c90c191b11ba7052bce0b0522fb5_314.png)

 have object like everything else in python and pandas for for data we can combine them very very。

 easily right so in japan does we can create a geo series that actually has different geometries so。



![](img/81e8c90c191b11ba7052bce0b0522fb5_316.png)

 usually you wouldn't well i'm not gonna say in most of my use case at least you wouldn't want to。

 have in one data set different types of geometry so you wouldn't want to combine points with polygons。

 with lines but you can if you want and it's really easy again you can create a geo series that your。

 is presented before with the list that just includes all of the all of the objects and then we can。

 pipe it directly into the plotting function and i'll give us a plot and then this is to go back to。



![](img/81e8c90c191b11ba7052bce0b0522fb5_318.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_319.png)

 your question this is not the delight representation this is a full flat matplot plot right that it's。



![](img/81e8c90c191b11ba7052bce0b0522fb5_321.png)

 combining all of the object in in the geo series okay so i'm gonna um switch gears a little bit in。



![](img/81e8c90c191b11ba7052bce0b0522fb5_323.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_324.png)

 the way i'm organizing it is i'm gonna give you two minutes for a super quick example so all of you。

 kind of come back from sleep mode while you were pretending to listen to me um and i'm gonna ask。



![](img/81e8c90c191b11ba7052bce0b0522fb5_326.png)

 you to create a similar figure to this one but that connects france spain paris and madread and。



![](img/81e8c90c191b11ba7052bce0b0522fb5_328.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_329.png)

 then i'll give you a price if you can get where i'm from um and it's not friends so i'm gonna give you。



![](img/81e8c90c191b11ba7052bce0b0522fb5_331.png)

 two minutes very quickly to try to recreate a similar plot to this one but with france spain。



![](img/81e8c90c191b11ba7052bce0b0522fb5_333.png)

 paris and madread and if you have any questions just please raise your hand and we'll be moving around。



![](img/81e8c90c191b11ba7052bce0b0522fb5_335.png)

 okay i'll i'll move in just to keep it more dynamic but um i'll post the exercises to the。



![](img/81e8c90c191b11ba7052bce0b0522fb5_337.png)

 kit hub repo later but um they're here just uh one sec。



![](img/81e8c90c191b11ba7052bce0b0522fb5_339.png)

 so you should have got something similar to this how have i done it first i pull out spain。

 the same way we just query the data frame for everything within spain keep the geometry and。

 squish it into a geometric object same formadread on the city's data frame then france and paris we。

 already had it and then we throw everything into a list um that contains spain's friends madread paris。

 and then on the fly we can build a line that goes from paris to madread all of that gets um。

 squashed into the geo series and then directly we pipe that into the plot plot engine yeah。

 any questions。

![](img/81e8c90c191b11ba7052bce0b0522fb5_341.png)

 what what sir。

![](img/81e8c90c191b11ba7052bce0b0522fb5_343.png)

 oh that's because it's um it's a complete map。

![](img/81e8c90c191b11ba7052bce0b0522fb5_345.png)

 so um i don't know i called it friends fr so france has the colony well the old colony。

 uh what is it uh what yan france has the french quayon i wouldn't say you're testing my geography。

 yeah yeah i don't want to go on the record but i'll say is the french quayon um。

 not that i've worked on the permanent geography or anything but all right so that's a um a quick way。



![](img/81e8c90c191b11ba7052bce0b0522fb5_347.png)

 for um pulling out geographies and then playing with them um very easily right but then what i。



![](img/81e8c90c191b11ba7052bce0b0522fb5_349.png)

 what i said we were going to do in this notebook is well now that we have a couple of points a polygon。

 a line we want to learn how to put those in relationship right so how can we check whether the。

 the point of brassals is within belgium or the point of um paris is within or not belgium and so。

 on and of course in this toy example this is all very obvious but the logic is the same when you。



![](img/81e8c90c191b11ba7052bce0b0522fb5_351.png)

 want to blow it up to a much larger data set right so let's start with the simple stuff um so we can。



![](img/81e8c90c191b11ba7052bce0b0522fb5_353.png)

 query whether brassals is within belgium and this almost reads like english um and then we get a。



![](img/81e8c90c191b11ba7052bce0b0522fb5_355.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_356.png)

 return true right so under the hood what is doing is taking a point object and doing what's called a。

 point in polygon operation with the polygon that we pass for belgium right um and we could do the。

 same for paris is it within belgium that is not right and you'll tell us false。



![](img/81e8c90c191b11ba7052bce0b0522fb5_358.png)

 this is using the point as the reference and then calling the within operator we can also say。

 flip it around and say well if i have a polygon the polygon can contain a point or not right and。

 then we can say in this context that belgium contain brassals true right we could do friends。

 contains brassals false yeah so that's for contains and within it's the two sides of the。



![](img/81e8c90c191b11ba7052bce0b0522fb5_360.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_361.png)

 point in polygon coin right and in some cases if you have a lot of polygons you might want to use。



![](img/81e8c90c191b11ba7052bce0b0522fb5_363.png)

 contains or with and if you have a lot of points you might want to use within it depends on what your。

 ultimate goal is you want to use one or the other it'll be more more useful。

 oops um so that was points and polygons now what if we have a um a line so let's go back to the。



![](img/81e8c90c191b11ba7052bce0b0522fb5_365.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_366.png)

 line where that was going from brassals to paris which is your assist commute does it does belgium。



![](img/81e8c90c191b11ba7052bce0b0522fb5_368.png)

 contain it well no right because it goes part of the line goes within belgium the other part。

 within france so again it contains what checks is whether the um the object on the left in this。

 case polygon fully encapsulates the object on the on the right um and again you can flip it around and。



![](img/81e8c90c191b11ba7052bce0b0522fb5_370.png)

 well not flip it around you can use the intersect to see just as it crossed is there any sort of a。

 touching between this polygon and this line even if it's not complete so the line might not be fully。

 within the polygon but is it part of the line inside the polygon you can use the intersect。

 and the line does intersect yep it's does it so your your problem is that。



![](img/81e8c90c191b11ba7052bce0b0522fb5_372.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_373.png)

 lines are also there will align to 22 the line is a line like that。



![](img/81e8c90c191b11ba7052bce0b0522fb5_375.png)

 okay so yeah we'll okay any questions so far on these basic relationships all right so then i'll。



![](img/81e8c90c191b11ba7052bce0b0522fb5_377.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_378.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_379.png)

 i'll move on and then i said well this is very useful conceptually right if you want to understand。

 and under the hood but well how do you do it on an atomic level say if you have a point and you。

 have a polygon or you want to put in relation a line and a polygon but usually in real world you。

 we don't have one line and two points we'll have a lot of points and a lot of polygons and we want。

 to use those we want to use these sort of relationships comfortably with larger data sets right so。

 happily for us japan does that very easily it basically broadcasts everything that you or almost。

 everything you can do at an atomic level it'll do it efficiently at a data frame your data frame。



![](img/81e8c90c191b11ba7052bce0b0522fb5_381.png)

 level yeah so remember how we said whoops ldum contains peris falls that was one polygon。



![](img/81e8c90c191b11ba7052bce0b0522fb5_383.png)

 checking whether one polygon contains a point but we actually happen to have a lot of polygons in。

 our country's data set so we can say directly countries contains peris and what it returns is a。



![](img/81e8c90c191b11ba7052bce0b0522fb5_385.png)

 column of bullions so for every row in the country's data set so for every country in this case it。

 goes and check whether that country contains the polygon of paris the point of paris and then it。

 returns the output so these will only occur once right this will be true only once。



![](img/81e8c90c191b11ba7052bce0b0522fb5_387.png)

 fair enough yes okay yes yes that's true i don't think paris taxes is in this data set。

 but but then again this is the heavy lifting in line 25 the heavy lifting happens all of the。



![](img/81e8c90c191b11ba7052bce0b0522fb5_389.png)

 checking the computation required to check happens but then actually for humans like me who don't like。

 to read falls and through but actual names you can then use this in combination with this standard。

 pandas logic for querying data sets or data frames um to subset the country's data set data frame。



![](img/81e8c90c191b11ba7052bce0b0522fb5_391.png)

 to only those lines where the country's contains peris query is true and we can just do this and。



![](img/81e8c90c191b11ba7052bce0b0522fb5_393.png)

 in this case yeah um maybe we should expand it to have a Texas country that has peris in there。

 and makes it true but that again there's nothing spacial that happens in this line but this is also。



![](img/81e8c90c191b11ba7052bce0b0522fb5_395.png)

 really useful to show that a lot of the pandas logic for manipulating tabular data sets applies。

 entirely here it's just that we're expanding that with geographic capability or geospatial。

 geometric capability really yeah。

![](img/81e8c90c191b11ba7052bce0b0522fb5_397.png)

 yeah is that a new object or just a view of that which slice of the data frame。



![](img/81e8c90c191b11ba7052bce0b0522fb5_399.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_400.png)

 this well this is a query so i would imagine is a um a view that i mean it's whatever pandas would。



![](img/81e8c90c191b11ba7052bce0b0522fb5_402.png)

 do in in this standard so it's exactly， same way of querying a data frame here right so i'm not sure exactly whether that uh。



![](img/81e8c90c191b11ba7052bce0b0522fb5_404.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_405.png)

 that would be what would that be a copy or a view it's a view i would say yeah。

 is it copy so it's a copy yeah okay um all right so but in any case that would there's nothing。



![](img/81e8c90c191b11ba7052bce0b0522fb5_407.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_408.png)

 specific to japanas when you do that query that was my point right and then here's another quick。



![](img/81e8c90c191b11ba7052bce0b0522fb5_410.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_411.png)

 example that i mean that would that will work with any sort of geometry the japanas support。

 right so in this case we have we can pull out the amazon uh river in the same way we query the。

 amazonas river in the rivers data frame keep the geometries queued it in and then we can look at。

 which countries cross the amazon or into seg and it will give as well brazil columbia improve。

 yeah and again we're using at the core it's a geowquary the crosses one that returns a boolean。



![](img/81e8c90c191b11ba7052bce0b0522fb5_413.png)

 and then we pipe that into a simple filtering for a data frame for pandas data frame and that。



![](img/81e8c90c191b11ba7052bce0b0522fb5_415.png)

 will return the the countries we want and so far we've seen the crosses that contains the intersects。



![](img/81e8c90c191b11ba7052bce0b0522fb5_417.png)

 there's a full reference here and again these all builds on the the so-called de 9am model for。

 predicates and geographic objects there is a wiki page for that if you're gonna read and if not the。

 shapely tutorial the shapely shapely manual on on this is is very fairly comprehensive so if you're。

 really interested in the details please go go there um so with that another two three minute quick。



![](img/81e8c90c191b11ba7052bce0b0522fb5_419.png)

 exercise for you to shake off my boring voice can you find all of the countries that are contiguous。



![](img/81e8c90c191b11ba7052bce0b0522fb5_421.png)

 to brazil in the data set and here's a hint by contiguous i mean countries that touch brazil yeah。

 so i'll give you um two minutes something like that。



![](img/81e8c90c191b11ba7052bce0b0522fb5_423.png)

 it's french cayenne right i'm french cayenne das touch brazil so france is a neighbor of brazil see。



![](img/81e8c90c191b11ba7052bce0b0522fb5_425.png)

 here's one lesson you can walk out of this workshop that you probably didn't know。

 um on the python side there's a couple of things you could learn from these first thing we just pick。



![](img/81e8c90c191b11ba7052bce0b0522fb5_427.png)

 pick out brazil um same way we query for the name brazil we keep the geometry we squeeze it into a。

 geometric object and then all of the heavy lifting happens here countries that touches brazil and。

 then we just filter on the country's data set to keep the the roads yeah any questions here and。



![](img/81e8c90c191b11ba7052bce0b0522fb5_429.png)

 on this method in these ways no cool so then the final part of this notebook is about is。



![](img/81e8c90c191b11ba7052bce0b0522fb5_431.png)

 covering spacial operations so far we've talked about spacial relations right so how can we put。

 in relationship two objects and check whether they um meet the requirements of different types。

 of relations whether they touch whether they cross whether they um intersect and so on now。

 another big set of um gis functionality really or geographic geometric functionality in japan。

 this is about um spacial operations so things that you can do you can create based on geographic。

 objects not really just checking for existing objects but create a new objects that follow some。

 sort of rule that you're interested in um and again i'm not going to cover all of them because。

 i mean we could spend a whole day on on shapely really um but if you do learn the the basic grammar。

 it all pretty much works the same and the patterns are the same so you the kind of objects you get。

 back would always be geo series or geo data frames and really just getting into what the spacial。

 operation during trend interest it is uh will do okay so um a very common one very common operation。



![](img/81e8c90c191b11ba7052bce0b0522fb5_433.png)

 is buffers so if we have points or if we have any object but these just want to to understand is。

 if we have a point we can draw a buffer of x of x meters around it and then that really is a polygon。

 a circular polygon and that's very useful to combine later on with all of the relation operations。

 that we've just seen right so if you want to see whether any point is within 500 meters of another。

 point one way to do it is checking distance another way to do it is create a buffer for that point。

 and then check for pointing polygon with the other ones so the real power of all of these comes。

 not at the atomic level but when you start combining them all of the different ones。

 and putting them together and because at the end of the day everything happens in the same。

 um python objects it's all shapely geometries stuffed into geo data frames or geo serieses。

 it's all very very easy to combine and put together chain one after the other and then build。



![](img/81e8c90c191b11ba7052bce0b0522fb5_435.png)

 fairly complicated um operations at the end of the day so in this case what do we have is just a。



![](img/81e8c90c191b11ba7052bce0b0522fb5_437.png)

 simple plot of the polygon of Belgium that we had before the brassholes location and then around。

 brassholes we've drawn a buffer of 0。5 can anyone tell me what 0。5 means here because usually you。

 want to say well i want a buffer of 500 meters around my point of interest or um what is 0。5。

 does anybody remember from its degrees right because our data right now they're expressed in。

 longitudinal attitude so if you wanted to do distances um as your is said before you need to。

 convert the crs to something that's expressed in meters or miles and then run um create a buffer。

 around it and then in that case you could say say if you had converted into something that's expressed。

 in meters you could just pass 500 and that would be a 500 meter buffer yeah if you can。



![](img/81e8c90c191b11ba7052bce0b0522fb5_439.png)

 create those points and then convert all the shapes more from a circle to the。

 yes uh sorry what say the so the questionnaire you can because if you have if you create a buffer。

 it agrees and you can convert it to a different crs will the corresponding buffer the projection。

 yes so well so the question is if you say you have a point then you create a buffer around your。

 point in long lad and then you come convert that buffer into a different crs right that's so。

 the answer is if you convert the buffer yes because at the end of the day the buffer is nothing but。

 another polygon object which if you can convert and it has a crs attached to it you can project it。

 you can manipulate it in any way in the same way that you've manipulated any other object before。

 so if you had say um this and this is going to be life programming so i'm not。

 things can go wrong but， what was the code for does anybody remember when the code was。



![](img/81e8c90c191b11ba7052bce0b0522fb5_441.png)

 is what three four three four somebody has the， yours do you remember the crs four meters in in europe。

 which one yeah yeah there you go。

![](img/81e8c90c191b11ba7052bce0b0522fb5_443.png)

 no four three two six okay anybody has anything else。

 oh sorry actually that can anybody tell me what this error is。



![](img/81e8c90c191b11ba7052bce0b0522fb5_445.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_446.png)

 so the and this is really good i run into this problem all the time so i'll highlight here to。

 hopefully save you some time so if you look at the error it says polygon object has no attribute。

 to crs this is so two crs is a geo pandas method right so it will only work on geo series or geo。

 data frames yeah shapely objects i'm gonna say this don't have a crs attached to it right。

 they they have coordinates but they don't have a crs attribute that attribute comes under geo data。

 on the japanas object whether it's geo series or geo data frame and because of that then the two crs。

 the crs conversing all of that happens within geo pandas so you can do i told you life programming。

 is never a good idea， there you go。

![](img/81e8c90c191b11ba7052bce0b0522fb5_448.png)

 sorry yours what was the Belgium one um it is third one three seven oh。



![](img/81e8c90c191b11ba7052bce0b0522fb5_450.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_451.png)

 there you go okay so what have i done here this is the same buffer we had before in degrees right。

 so the buffer we created at the in degrees and then we stuff that into the geo series and we make。

 sure we explicitly enter this ers for the geo series and because it is i'm projected this is the。

 same as the city's ers so you could specify in any way then once you have that geo series then you。

 can use two crs to convert we project it into the um epsg which is expressed in meters and then if we。

 plot it then we have that this original um buffer which when you create it is a perfect circle when。



![](img/81e8c90c191b11ba7052bce0b0522fb5_453.png)

 you repreject it in not necessarily the case perfect circle yeah it's more of an ellipse。



![](img/81e8c90c191b11ba7052bce0b0522fb5_455.png)

 any questions no all right and um well buffer is one once we have the buffer as i said the real。



![](img/81e8c90c191b11ba7052bce0b0522fb5_457.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_458.png)

 power of all of these comes when you these are all building blocks right this is like a lego any lego。

 piece doesn't do anything is when you put it all together that makes about the car whatever you're。

 trying to do so the real power of these comes when you start combining say buffers with intersections。

 with unions and and so on um so the intersection just a couple of examples to show you it'll take。



![](img/81e8c90c191b11ba7052bce0b0522fb5_460.png)

 all of the object geographic objects you um you pass and return the intersection of everything right。

 so everything the the area that is um shared by all of the objects in the in the series your passion。

 the union will pass all of the area that you're passing will kind of put it into one。



![](img/81e8c90c191b11ba7052bce0b0522fb5_462.png)

 the difference will return the area that is not commonly shared in this case between the buffer。



![](img/81e8c90c191b11ba7052bce0b0522fb5_464.png)

 and and the belgian polygon and as i said this is just a couple of examples there's a lot of。



![](img/81e8c90c191b11ba7052bce0b0522fb5_466.png)

 other operations um i'll just tell you one final one um that is particularly useful um these union。



![](img/81e8c90c191b11ba7052bce0b0522fb5_468.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_469.png)

 in many cases in many cases that's what you want you you have a bunch of polygons you want to。

 create them create one out of them that contains all of them。

 there is a difference between union and unary union and i can't remember it now。



![](img/81e8c90c191b11ba7052bce0b0522fb5_471.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_472.png)

 but you want to use unary union that's the lesson so in this case if you want to create a polygon。

 so say you have all of the african countries and what you want to do is a polygon of african not。

 a composite of different smaller polygons so you you start with african countries。

 with just a simple query and then you call the unary union and i'll give you a polygon。



![](img/81e8c90c191b11ba7052bce0b0522fb5_474.png)

 that combines all of the geometries that you've passed in yeah。



![](img/81e8c90c191b11ba7052bce0b0522fb5_476.png)

 any questions so i have another quick example but i think i'm gonna in the sake of time i'm gonna。



![](img/81e8c90c191b11ba7052bce0b0522fb5_478.png)

 skip it because it's it's too easy for you guys um so i'm gonna move over to the last bit i wanted。



![](img/81e8c90c191b11ba7052bce0b0522fb5_480.png)

 to cover and then um will continue any questions before this yeah。



![](img/81e8c90c191b11ba7052bce0b0522fb5_482.png)

 so the question is does the intersection union difference and so on is in shapely and japan does。

 the answer is um they have a lifting happens in shapely but you can access it through japan does。

 so when you you do um same as we've done above with the intersects contains crosses and so on。

 all of that really is um shapely operations which is to say that's really geo separations。

 so geo pandas exposes them to you in an easy way to use with geo data frames and geo serieses。

 yeah yeah more questions no all right so then let's move on to uh the third notebook the spacial。



![](img/81e8c90c191b11ba7052bce0b0522fb5_484.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_485.png)

 joints and hopefully i can get to them 20 minutes or so。



![](img/81e8c90c191b11ba7052bce0b0522fb5_487.png)

 okay so before anything let's import everything we'll need data and libraries。



![](img/81e8c90c191b11ba7052bce0b0522fb5_489.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_490.png)

 just a quick recap um so we're gonna see here spacial joints the really i mean。



![](img/81e8c90c191b11ba7052bce0b0522fb5_492.png)

 computation is a very different but conceptually they're very similar to non spacial joints so if。

 you're familiar with pandas and with joining and merging data frames based on keywords um。

 conceptually is the same idea is the idea of a spacial joint is if you have two geo data frames。

 or two tables that have some sort of geographic pinpointing that you can put on a on a map in some。

 way we're gonna join them based on the location of their observations rather than the traditional。

 keyword joint so here's a non spacial example would be let's pick up but just a few cities uh。



![](img/81e8c90c191b11ba7052bce0b0522fb5_494.png)

 burn in Switzerland Brussels London Paris and then manually just for the sake of the example。

 let's add the countries that they're in and then this is just a subset of our cities data frame。



![](img/81e8c90c191b11ba7052bce0b0522fb5_496.png)

 yeah nothing special there's the name there's the geometry and then there's a country。



![](img/81e8c90c191b11ba7052bce0b0522fb5_498.png)

 and then let's also um subset the country so we have two small manageable kind of data frames。

 that we can at least they can directly relate to rather than 400 observations that doesn't really。



![](img/81e8c90c191b11ba7052bce0b0522fb5_500.png)

 mean much to me so the idea of non spacial joints is you have a table that has a column for a country。



![](img/81e8c90c191b11ba7052bce0b0522fb5_502.png)

 which is for example in the cities you have a column that is the country where the city is and then you。

 have another table with information on countries and as part of that table on countries you have a。

 key that is the country code so if you have that common column in the two tables you can join them。



![](img/81e8c90c191b11ba7052bce0b0522fb5_504.png)

 together with the join or the merit commands and there's nothing spacial i mean in this case。



![](img/81e8c90c191b11ba7052bce0b0522fb5_506.png)

 you're doing a spacial in the sense that you're joining cities to countries but。

 computationally you're not joining anything spacial you're just saying i know this table has a column。

 that is shared with this other um table and then we're going to use that common keywords to join them。

 yeah and then what you end up uh that uh here is with a merit uh table that has the。



![](img/81e8c90c191b11ba7052bce0b0522fb5_508.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_509.png)

 option the data you had for the city so the name the geometry and the um country code and then on。

 to the right of that has been appended the information for the countries yeah so again nothing。



![](img/81e8c90c191b11ba7052bce0b0522fb5_511.png)

 implicitly spacial in this join now that is great when you do have the column in both tables right。

 and but that's not always the case in many cases and that's one of the to me one of the key powers of。

 of space and and geographies that you can use it as a kind of sort of common index that you can。

 use to combine data without having that extra column so um how can we do that。



![](img/81e8c90c191b11ba7052bce0b0522fb5_513.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_514.png)

 to your pandas has an s join which plays on the join in in pandas that does a spacial join。

 so in this case where we have cities and countries again it's going back to the previous notebook of。

 pointing polygon is the point within the polygon yes if so then i'm gonna pen all of the information。

 in the polygon data to the points yeah so again we want to do that join without having to explicitly。



![](img/81e8c90c191b11ba7052bce0b0522fb5_516.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_517.png)

 say if we don't have that data which country every city is we're just gonna i mean that in from we。

 have that information encoded in their location so let's go ahead and run it the way you do it is。



![](img/81e8c90c191b11ba7052bce0b0522fb5_519.png)

 the s join tries to use as much of the join api in pandas so if you've played without a lot of it is。

 is similar or tries to mimic that translate you need into the into geographic grammar so to speak so。

 we're gonna join cities which is a bunch of points with countries which is a bunch of polygons。

 then there's an op attribute for operation and here all of the operations that we've looked at before。

 all of these basal operations so um the within the crosses the intersects touches and so on applies。

 and then how this is uh just traditional database jargon right so it's and in this case we're saying。

 left so we're saying that the city's data frame is your preference table and then to that you want to。

 pen the information in the in the one that's in the right in the in the countries one yeah this。



![](img/81e8c90c191b11ba7052bce0b0522fb5_521.png)

 this makes sense cool oops and then what do we end up with we end up with a table that has all of。



![](img/81e8c90c191b11ba7052bce0b0522fb5_523.png)

 the information that cities had and all of the information that countries has and it's been。

 joined by location and because we use the within we use every point we'll get the information of the。

 polygon for which the point is within it right if that makes sense。



![](img/81e8c90c191b11ba7052bce0b0522fb5_525.png)

 any questions。

![](img/81e8c90c191b11ba7052bce0b0522fb5_527.png)

 yeah。

![](img/81e8c90c191b11ba7052bce0b0522fb5_529.png)

 let's say， so the question is what if there's a point that is not within any polygon， so。



![](img/81e8c90c191b11ba7052bce0b0522fb5_531.png)

 before i tell you a lie。

![](img/81e8c90c191b11ba7052bce0b0522fb5_533.png)

 um yes so that really depends on how you specify the how right so if you say left is going to keep。



![](img/81e8c90c191b11ba7052bce0b0522fb5_535.png)

 every observation in the left right um and if something in the left doesn't find a match in the。

 right it'll just throw a a missing value for those rows so it'll it'll give you a row with all of the。

 the columns but the columns that come from the right will be missing missing data if you said。

 inner which is the default actually um what it would do is it would give you okay it would give you。

 just uh the subset that where everything is dense so to speak um and if you said um how right it would。

 keep everything on the right yeah does that make sense， anymore yeah。

 uh what happened in one so the question is on the join um the join output has only one geometry。



![](img/81e8c90c191b11ba7052bce0b0522fb5_537.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_538.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_539.png)

 which in this case is the one for cities what happened to the one of the countries。

 um that gets discarded and that is because by um by agreement uh geodata frame will only have one。

 geometry column is there any way to keep it i mean is there any way to have multiple geometries。

 i don't know if there is technically but you shouldn't um in the sense that the idea of a。

 geodata frame is having a one observation for a single geometric object so if you want it to have。

 two i think and i guess this yours will probably be better but my view is if you want to have two。

 observations just make it two rows for every uh for every observation save you have imagine that you。

 you want to keep um countries and countries you want to keep the polygon and the point of the capital。

 then instead of having a row with two geometries one for the polygon of the country and one for the。

 point of the um capital you would do either two tables as we've been doing here or potentially you。

 could consider having two rows one for the country with the polygon and one for the country with the。

 point of the capital but by by agreement geopandas would only have one geometry um per row and this is。

 kind of in in agreement with how post-GIS works and and so on yeah so so i was just thinking preparing。

 that to an outer joint canvas where you could actually and you'd have missing values right。

 and very well it didn't exist and you'd have a little left of the right but so you i mean i was。

 thinking the analogies that you'd have the geometry you'd have two geometries one with missing values。

 but no that's not how you do it sorry what's the question so if you did an outer joint yeah。

 right where you have you're uh you're doing a joint but you're missing you you have you have。

 yeah you have two different variables describing the same concept was different in any system we。

 were just that missing value yeah that would work the same here though that would work the same。

 yeah so you could um it's another twist of the previous question because you do have the how。



![](img/81e8c90c191b11ba7052bce0b0522fb5_541.png)

 attribute the how argument you can say um how outer and then say in this case imagine there were。



![](img/81e8c90c191b11ba7052bce0b0522fb5_543.png)

 some cities without a country and some countries without a city it would still put in there it's。

 just that the the row of cities without a country will have missing values on the country columns。

 and the countries without a city will have missing values on the city columns but you couldn't have。

 two geometries with one geometries no no yes yes it would it would only keep one i believe so yeah。

 yeah so then for some it would keep the geography the city and for those where the left was not all。



![](img/81e8c90c191b11ba7052bce0b0522fb5_545.png)

 it would keep the geography for the country and that or would that be actually sorry i'm wrong。



![](img/81e8c90c191b11ba7052bce0b0522fb5_547.png)

 and i just lied to you there is no outer for that very reason so um yeah。

 see so you can do left it will keep your geometry on the left you can do right it'll keep your geometry。

 on the right or you can do inner and it'll use the intersection but then we'll retain we'll retain。

 only the left if that makes sense there's no outer sorry it should have said。



![](img/81e8c90c191b11ba7052bce0b0522fb5_549.png)

 okay any more questions okay so then let's um move on to the final one there's a couple of。



![](img/81e8c90c191b11ba7052bce0b0522fb5_551.png)

 exercises i'm gonna skip time so right now spasal joints are really about combining data。

 but you don't modify geometries right with the spasal joints you just have say points in polygon。

 you put them in relationship but the output of that join is still the original。

 geometry you're passing in sometimes that's what i mean in in a lot of cases that's what you want。

 in other cases what you want actually is through that operation generate a new。

 a new set of geometries and this is equivalent so the spasal joint relates to the spasal relationships。



![](img/81e8c90c191b11ba7052bce0b0522fb5_553.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_554.png)

 the way that spasal operations relate to the overlay right so if you want to do。



![](img/81e8c90c191b11ba7052bce0b0522fb5_556.png)

 a combination that results in new geometries you would want to use an overlay。



![](img/81e8c90c191b11ba7052bce0b0522fb5_558.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_559.png)

 and then you specify the spasal operations that you you want to do with the how again with the how。

 argument so let's say for instance that we want to get um we have the african countries。



![](img/81e8c90c191b11ba7052bce0b0522fb5_561.png)

 and then we draw a buffer around the cities so let's say um we're delimiting urban areas in Africa。

 and then what we really want to get is a map of the rural area so all of the parts of Africa。

 that are not within the area within an urban area so then we can call the overlay。



![](img/81e8c90c191b11ba7052bce0b0522fb5_563.png)

 we pass Africa as the polygon cities and then what do we want as the output we want the difference。



![](img/81e8c90c191b11ba7052bce0b0522fb5_565.png)

 of those two yeah and then that's what the overlay returns so。



![](img/81e8c90c191b11ba7052bce0b0522fb5_567.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_568.png)

 again just to reiterate the spasal joint combines information using location as the joining column。



![](img/81e8c90c191b11ba7052bce0b0522fb5_570.png)

 but it doesn't modify the geometries the spasal overlay does modify the geometries and you can。

 apply you can use um all of the spasal operations to modify those geometries and create combinations。

 yeah any questions。

![](img/81e8c90c191b11ba7052bce0b0522fb5_572.png)

 so the idea what I mean why was required here so it was just the example I had was let's say。



![](img/81e8c90c191b11ba7052bce0b0522fb5_574.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_575.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_576.png)

 would you let's just keep Africa this is our polygons and then we have our cities our cities。

 are points right and by definition points have zero area an area of zero so because it's。

 does not they don't have dimension it's a single point um but let's say in the example I gave。



![](img/81e8c90c191b11ba7052bce0b0522fb5_578.png)

 was let's say that we want to keep the non-urban area so let's call the rural areas the rural Africa。

 so how can we define that let's say we pick every city and then we define the urban area as a buffer。

 around that point so let's say in this case it was two degrees around the centroid。

 and then you're turning cities from points into polygons circles really and that's what we were。

 calling in this simple toy example urban areas then let's say how do we get the rural areas by。

 getting all of the country miners that part of the country that is urban。



![](img/81e8c90c191b11ba7052bce0b0522fb5_580.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_581.png)

 yeah which is this and in this case it's two because cities is expressed in latitude and longitude。

 and then it's degrees but say if you had if you projected it to something in meters you could。

 express that that number would reflect meters and you could say a buffer of 500 meters a buffer of。

 one kilometer if you did say one kilometer you will have to enter a thousand but because it's always。

 in the unit that this errs is expressed but yeah it looks like if you increase the buffers and you。

 start getting overlaps between your buffers it kind of cancels out the difference operation。

 starts including it again your way to account for that what do you mean that's a bug in jubangas。



![](img/81e8c90c191b11ba7052bce0b0522fb5_583.png)

 and hopefully fixed in the next release that hopefully during the sprints and over released。

 there you go yeah that's an answer you're currently at some。



![](img/81e8c90c191b11ba7052bce0b0522fb5_585.png)

 for those coordinate cases， what did you want the rural parts to actually be unique for each city like based on populations or。

 something like that how would you go on also creating that cities。

 so the question is how can you create tailored buffers to every city。



![](img/81e8c90c191b11ba7052bce0b0522fb5_587.png)

 in that case the way i would do it i mean this this is again a good example of just combining。



![](img/81e8c90c191b11ba7052bce0b0522fb5_589.png)

 different operations right so then i would probably end up doing。

 so well i'll explain you and then if i can life program it or maybe i'll do it in the in the break。

 is we're coming up to the time but the idea would be you can use an apply function and then apply。

 that row by row and as part of that apply function define the value you want so you could for instance。

 have a column another column in every row say imagine we had information and population for the。

 cities so then as part of that apply function as part of that function you define to pass through。

 apply you could say then i know that in this row there's going to be a pop column use that and。

 transform in this way to come up with a radius and then that radius take it into the buffer。

 generate the buffer so at that point again it it's just more general python programming。

 rather than specific functionality that is and i think that that's a feature in not a fact really。

 because what japan does is doing is making all of the geos operations pythonic in a way that you。

 can plug them in with the rest of your workflow yeah does that make sense so maybe on the break i'll。

 try to life code that but i'm not going to embarrass myself i'm not going to finish up with an。

 environment so anymore questions on this yeah， okay does not touch。

 uh do you have data that you see， that just reads everything that gdol can read yeah and geodetabase i think gdol can store for it。

 there is a driver yeah it's so basically we can read actually most gdol can read it into a tabular。

 format and if it's tabular format and gdol can read it you can improve it except kml but it's because。

 it's not a tabular format oh okay never try to comment on geories he always knows more but yeah i。

 mean basically i don't think it in it it in operates in any way with hardpights it basically does as。

 far as it can tell pretty much the same or it's comparable except this is based on a fully open。

 sort of stack and if you compare it for example with qgis yeah many of the operations you can。

 use yes you can do in japanese and even many of the things are actually using the same lavis on the。

 hood yeah qgis will also use gdol and will also use qs for certain things they also have their own。

 custom algorithms implemented for many things as does japan or so but many of the yeah core open source。

 software stack in the juice is this and i know it's sacrilege in this room but if anyone uses r。

 the s of package is pretty much the same it relies on geos for all of the geospace operation。

 so at the end of the day when you draw a buffer whether you do it in r and qgis on geopandos。

 the heavy lifting is being done by the same code which is geos。

 all right so do i have a break or we switch maybe just so yeah one more i was gonna。



![](img/81e8c90c191b11ba7052bce0b0522fb5_591.png)

 before that there is a set of exercises for these two notebooks on the same file that um。



![](img/81e8c90c191b11ba7052bce0b0522fb5_593.png)

 okay no the case conflict file has a set of exercises。



![](img/81e8c90c191b11ba7052bce0b0522fb5_595.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_596.png)

 yeah so you can always because we had a bit too much material for the two hours never say you're。



![](img/81e8c90c191b11ba7052bce0b0522fb5_598.png)

 not gonna want an environment so you can always continue there the exercises it applies everything。



![](img/81e8c90c191b11ba7052bce0b0522fb5_600.png)

 that then he showed on yeah so everything from space of operations on and same as the previous。

 session the solve the solutions are there so if you if you get stuck they're there。

 yeah so this concludes the first part which was really focused on getting to know geopandos。

 after the break we will still use geopandos but combined with many of the other data science。

 special data science tools that we will show you so let's say， yeah 10 15 minutes break。

 all right we'll play 12 so we should start all right welcome back in the second half i'm。



![](img/81e8c90c191b11ba7052bce0b0522fb5_602.png)

 sergere i think i introduced myself before we're gonna shift gears a little bit so the first part。

 was about geopossessing dealing with all the rich varieties of spatial data formats and coordinate。

 systems and geopossessing the spatial operations we could call that deterministic spatial analysis。

 that is you're interested in the spatial relationships between your observations。

 and the afternoon we're going to switch to looking at methods of visualization of spatial data there。

 was some notebooks in the first part that we didn't get to so we're visualizing spatial data with an。

 eye towards exploring spatial data to identify interesting patterns and then ultimately to modeling。

 spatial data so Levi will be covering some of the modeling capabilities we're primarily going to。

 be focusing on the library pie cell python spatial analysis library which started a long time ago。

 before we had things like shapely before we had geopandos before we had cardopi and we had to write。

 we the people work on pie cell work in area spatial kind of metrics spatial statistics geocomputation。

 and we want to develop analytics that would sit on top of these very elegant and strong。

 data processing geoprosses and but they're we didn't have them back in the day so now we're very。

 excited because we can focus more on the geo analytics and then partner with geopandos and。

 related so we're at that part of the the workflow if you want to think about it in terms of a。

 scientific workflow i'm going to be focusing on notebooks five and six and then turn it over to。



![](img/81e8c90c191b11ba7052bce0b0522fb5_604.png)

 Levi so visualization is a massive area in scientific computing but in in geography in particular yeah。

 i am not a cartographer i'm more of a statistician spatial statistician um so we're going to just delve。

 into a little bit of cartographic theory here in terms of coral path maps now coral means region。

 all right so we have aerial unit data polygons that we want to understand how some spatial attribute。

 that is some substantive variable you're interested in studying most of our work is in social sciences。

 so we could be looking at income levels or housing prices or market segmentation and we have observations。

 could be polygons could be points and we have an attribute that we're measuring for each location。

 we want to understand the spatial distribution of those attribute values in space we are going to。

 look at two sets of methods that are complementary we're going to look at visualization methods so。

 mapping is very powerful but we're also going to couple that with quantitative statistical measures。

 to get at the same question and try and understand the spatial distribution of these patterns so。

 coral path mapping the effectiveness of a coral path map is is largely a function of two things。

 okay um the first is given the distribution the statistical distribution of the attribute that。

 you're interested in what is the appropriate classification scheme this is essentially a one。

 dimensional clustering problem where you're trying to group observations based on their value similarity。

 into mutual exclusive classes and maximize the difference between the classes so you're trying。

 to summarize the statistical distribution of the data and there's an embarrassment or riches of。

 classification methods some of which we're going to look at shortly so that's one half of the。

 scissor the other half of the scissor is the symbolization you're going to use once you've。

 selected that classification scheme and it's those two together that are going to drive how effective。

 your visualization is and by effectiveness here that depends on the context so it could be you your。

 scientist trying to explore your data understand the spatial distribution another case is it could。

 be you're interested in identifying outliers in the data from a spatial perspective or from a value。

 perspective or some combination of these approaches so this notebook we're going to look at how we。

 carry out map classification ultimately then to build a quoropleth map so classification first。

 you have in we're going to work with the data set from Berlin so we're using geo pandas to read in。

 the data and the data this is from a workshop we gave in Basel a couple months ago where we talked。

 about how you download the data construct the day to do aggregation from points to polygon so these。

 are Airbnb listings that we're going to aggregate to polygons i。e。

 neighborhoods in Berlin so that's， the data set we're working with we can point you to the older notebooks that build the data set and。

 and use some of the functionality Danny and Juris cover this morning so the variable we're。

 interested in here is the median price is the font big enough for people in the back make it bigger okay。

 okay so we have median price and this is the median price of all the listings in a given district。

 right we're looking at the top five or the first five districts in the data frame here。

 okay so that's the variable of interest i could be an urban economist interested in。

 how the housing market functions in in Berlin so we're first going to understand the statistical。

 distribution of those values abstracted from geographical space so this is the median price and i think。

 it's in euros per evening the variable of interest so the observations are taken for each of the。

 districts and here we're summarizing the value distribution there's no geography here the space。

 if you will is the value of the attribute the median price okay it's a little bit of skewed。

 distribution not atypical for income data or uh dollar denominated data you have a couple very。

 high price listings and you see where the center of the distribution is off to the left here all right。



![](img/81e8c90c191b11ba7052bce0b0522fb5_606.png)

 so we're using c-borne there just to visualize the data uh we'll throw in a rug plot that shows you。

 the locations of the individual values at the bottom there on the the price scale okay so that。

 gives you a sense for the statistical distribution of the values ultimately here we're going to be。

 interested in how those values are distributed in geographical space in the city of Berlin across。

 these polygons which are the districts or the the neighborhoods and to get at that we're going to。



![](img/81e8c90c191b11ba7052bce0b0522fb5_608.png)

 pick up backup with the plot method for the geodata frames using the defaults so to do a core。

 oplithmott and geopandis we have the data frame which we've created we know how to do that we've done。

 this morning we've passed in a column column argument for which attribute do we want a plot。

 and it's the median price and we get default color scheme and default classification which we。

 don't know what they are yet we're going to get into this okay so that's the view of the spatial。

 distribution of the median prices anyone from Berlin okay so i won't get called out here for。

 not knowing anything about Berlin um okay so maps are very powerful because they tap into the way。

 our brains work in terms of we are pattern recognizing animals we wouldn't be here if our。

 ancestors weren't pattern recognizing animals so effective map design is about tapping into。

 those the way our brains work but you can make an argument that we're perhaps too good at pattern。

 recognition in that we can pick up on false positives things that we think are there but they're。

 actually not there because of the way the the implementation of the visualization was done and。

 there's a couple of dimensions that complicate things for real world maps these polygons are。

 not all the same size nor are they the same shape all right and larger shapes tend to dominate。

 our cognitive load so to speak so we're drawn to them and then makes it difficult because from a。

 statistical perspective each one of these observations should have equal weight but when we put that on。

 a map things get much more complicated okay so let's peek in under the hood a little bit and try。



![](img/81e8c90c191b11ba7052bce0b0522fb5_610.png)

 and understand what's going on we're gonna number one make the map a little bit bigger。

 so the default i believe for that the first map that we saw was saw was to use um quintiles。

 for the classification so we take the housing values we sort them from lowest to highest and。

 we break them into five equal size groups and then we assign a color hue to each other groups。



![](img/81e8c90c191b11ba7052bce0b0522fb5_612.png)

 using a sequential hue so that we get the impression of where the high values are and where the low values。

 are all right so we're doing that again here we're being explicit so the scheme is the classification。



![](img/81e8c90c191b11ba7052bce0b0522fb5_614.png)

 scheme and that comes from pie cell there's uh that pandas has a wrapper around to use several。

 the the classification schemes in pie cell not all of them for having to do with the complexity of the。

 the function signatures but this is the default that we saw earlier just making it bigger here。

 all right。

![](img/81e8c90c191b11ba7052bce0b0522fb5_616.png)

 so we bumped up the size of the map we made it explicit for our classification scheme。

 and we can get increasing granularity so now we're going to add a legend so we see what the breaks are。

 for the different bins according to this quantization of the the attribute okay so the darker colors are。

 for the lower values of the rents the lighter hues are for the higher income or sorry higher。

 valued rents question so far all right so the defaults quantiles we could do quartiles by just。



![](img/81e8c90c191b11ba7052bce0b0522fb5_618.png)

 changing the argument k to four and instead of splitting into fifth we're splitting into quarters。

 based on the value distribution all right and you can change that to whatever you want um。

 octiles deciles by just manipulating k。

![](img/81e8c90c191b11ba7052bce0b0522fb5_620.png)

 so the classification scheme is important but also the color ramp that you use and there's。

 a lot of interest in color ramps and visualization um color brewer which comes from Cindy Brewer she。

 was a colleague of mine a long time ago at sending a state so the very effective website for helping。

 you decide what color scheme to use for a Cora Plath map depending on if your attribute is quantitative。

 or categorical is that it is a diverging value distribution and so on and what what is your。

 intended medium are you going to print a hard copy map or you're going to put it on a beamer。

 so it's an excellent excellent tool and many of the libraries in the in the python world have。

 already pulled into color brewer and then extended it with other things like palatable and so on。



![](img/81e8c90c191b11ba7052bce0b0522fb5_622.png)

 so we just changed the color scheme here keep the number of classes constant。



![](img/81e8c90c191b11ba7052bce0b0522fb5_624.png)

 so we can first look at okay what's the impact of the choice of the color scheme for the ramp。

 all right the default versus orange to red or green to blue remember it's the same attribute。

 just that one dimension of this symbolization changes alternatively we could change the classification scheme。

 and we're going to get into these in a in a second so we could use quartiles or equal interval or。

 an optimization approach fisher janks again same collection of values for the neighborhoods but。

 the classification scheme differs and then obviously you could change both the color scheme and the。

 classification scheme okay so geo panel supports the classifiers and pie cell that have a common。

 signature that is they typically take k the number of classes that you want to define right but there。

 are other classifiers in pie cell so there's a package in pie cell called map classify that just。

 does the classification it doesn't do do the visualization that's not the goal the goal is to。

 make it quick and easy to get different classifiers and then you can couple them with whatever you。

 want carto pie jupandas um fully and so on so the classifiers that we have in map classify。

 box plot equal interval fisher janks sampling which is for large problems head tail breaks and。



![](img/81e8c90c191b11ba7052bce0b0522fb5_626.png)

 we're gonna we're gonna look at a couple of these have people encounter map classifiers before。

 is this new to most of you because okay so we'll do a little bit of a slower pace than i was。



![](img/81e8c90c191b11ba7052bce0b0522fb5_628.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_629.png)

 planning on okay so equal intervals the first one we're looking at here。

 this takes the minimum value in the data set the maximum value of the data set and ask the user。

 how many classes do you want in this case i said five and then what it's going to do is subdivide。

 that range into five equally spaced equally with intervals okay and so we call the equal interval。



![](img/81e8c90c191b11ba7052bce0b0522fb5_631.png)

 class we pass the attribute y which is our income the housing values and k and what we get back is。

 an instance of our classifier object and its rep rep is just the classification scheme okay so you。

 see that we have um five classes you have the upper and lower bound for each of the classes。

 and you have the count of the number observations that fall in each of the classes so this is purely。

 based on the value distribution there's no geography here。

 there's other attributes for the classifier object so yb means the bin。



![](img/81e8c90c191b11ba7052bce0b0522fb5_633.png)

 y's bin so it's similar to a label and scikit learn if you're doing clustering。

 tells you which of those bins is each of the observations falling into。

 second classifier which was the default in the plot for a coral path and geo pandas is the。



![](img/81e8c90c191b11ba7052bce0b0522fb5_635.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_636.png)

 is the quantiles so same type of signature you pass in the attribute y and the number of classes。



![](img/81e8c90c191b11ba7052bce0b0522fb5_638.png)

 same repper， so quantiles this is quintiles we have five if you squint at the screen the idea behind quintiles is。

 you unlike equal intervals where the widths are the same across the classes here the number of。

 observations in each of the classes should be the same equal count all right but what do we see here。

 do we have equal count， which class has the most observations。

 the first one has 39 observations right which is more than one fifth of the observations。

 and this is a common problem when you're doing corporate mapping with。

 values where you have a lot of duplicates a lot of ties all right so for quintiles in this case。

 you sort the data and you find the 20th percentile right now if you have a lot of low values or a lot。

 of values that are duplicates you could have that be say i don't know 32 euros but if you have 100。

 neighborhoods that have 32 then you have a problem because if you rank the data you have ties all。

 right and this is inconsistent across all mapping packages how they deal with the ties。

 what you do so what we do is we just bump it up to get the the ties and then if the tie was say at。

 32 and we had 132 we moved the bottom of the first quintile to the hundredth ranked observation okay。

 at least we tell you what we do other packages don't tell you you have to guess。



![](img/81e8c90c191b11ba7052bce0b0522fb5_640.png)

 all right so y-benz and there you see that's it's only 57 unique values in the attribute。

 distribution and that causes problems for quantile classifiers all right so how do you decide。

 which classifier to use well it depends on what your objective is and there's different objective。

 functions so one that's built into the classifier is a measure of fit and this is like trying to come。

 up with a good clustering solution this is absolute deviation around the class meetings。



![](img/81e8c90c191b11ba7052bce0b0522fb5_642.png)

 and we're going to compare five four different classifiers for the same number of classes so。

 five classes and i want to maximize the internal homogeneity of the classes and maximize the。

 external heterogeneity and what the difference is between things belonging to different groups to。

 be as large as possible and the difference is between things that belong to the same class。

 small as possible so lower values is better for this and we see that the Fisher-Janks class。

 has the lowest fit it's guaranteed to okay so but fit is not necessarily always the ultimate。



![](img/81e8c90c191b11ba7052bce0b0522fb5_644.png)

 objective here why not well there's classifiers that are used to detect outliers in the data so。

 extreme values and those extreme values could be error observations data errors or they could。

 actually be interesting true values that you want to flag there's two classifiers you could use for。

 this purpose standard deviation and mean where the for the standard deviation you take you define。

 the classes based on distance from the mean in multiples of the standard deviation so you're。

 getting out in the tails explicitly or a box plot and we'll see images of box plots later but the idea。

 here is you have the 50th percentile the data from the 25th percentile the 75th and the core of the。

 data set and then you have things called whiskers and fences that are going to help us bound outliers。

 it'll be clear when we get back to the visualizing the maps。



![](img/81e8c90c191b11ba7052bce0b0522fb5_646.png)

 okay so using these classifiers in geo-panas for the classifiers that are not built into geo-panas。



![](img/81e8c90c191b11ba7052bce0b0522fb5_648.png)

 you can do that so if we wanted to do the box plot classifier to identify outliers with geo-panas。

 this one's not by default so you have to sort of build it in so first we're going to have a simple。

 list with the legends for our label so a label is zero means you're a lower outlier your low extreme。

 value one means you're low whisker so you're on the whisker of the box plot Q2 and Q3 are the 25th to。

 50th and 50th to 75th percentile so they're sort of central observations they're not extreme。

 and then we have the high whisker in the box plot and high outliers so those are our legends for our。

 label then we loop over our box plot classifier and we extract the bin label which label is each。

 observation in and then we're going to use that list and attach it to the data frame as a new。

 column in the data frame right and then plot that because geo-panas can support can support that we。

 just treated as a categorical data type in geo-panas and then we can exploit the plotting function。

 okay so then。

![](img/81e8c90c191b11ba7052bce0b0522fb5_650.png)

 we don't have any low whiskers so there's no low extreme values but we do have a couple of high。

 outliers right and the high outliers here they are more than 1。5 times the inner quartile range。

 above the 75th percentile so these are the really extreme high value neighborhoods or high rent。

 neighborhoods all right and so now we're seeing that we're pairing the statistical distribution。

 with its articulation in space into your graphical space， okay。



![](img/81e8c90c191b11ba7052bce0b0522fb5_652.png)

 questions on， the classifiers is that fairly straightforward tells us gives us different ways to group the data。

 and then we pair that with the plotting function geo-panas to do a core uplift map。

 no questions on that fairly straightforward， we don't we do not have a low outlier in this case yeah right。

 right we teach i teach a 15 week course on geovisualization so we spend a lot of time on classifiers so we're。



![](img/81e8c90c191b11ba7052bce0b0522fb5_654.png)

 getting a thumbnail sketch here yes， so just curious on the like the most quartiles you know that's pretty easy map。

 if i go to where would you ever have any questions clustering almost on your your legend。

 you know like as human i apologize you might say oh these all look similar and here's， yeah。

 i didn't go we did fish of janks which is an optimal classifier that'll that'll。

 do better than we can do by eye we also support user-defined classifiers so well not classifiers。

 but bins so if you wanted to pre-specify where you wanted the breaks to be you pass that into the。

 classifier and it'll return it in an object that then has all the functionality other questions。

 okay so now we're visualizing the data and as i said our brains are really powerful pattern。

 detectors but sometimes we could fool ourselves and find you know apparitions so people seeing。

 Jesus in the toast kind of thing this is a demonstrative phenomena there's a lot of literature and psychology。

 about our pattern recognition because we have to survive so we're trained to identify things that。

 might eat us or kill us or right so now we're going to couple the visualizations with statistical test。

 so we don't fool ourselves all right and this is in the notion of spatial order correlation。

 so it's auto correlation we know what correlation is right you have two variables and you want to see。

 if they're positively correlated that is when one is high is the other one high。

 when one is low is the other one low or they negatively correlated is their inverse relationship。

 so that's correlation auto here is that we're looking at one variable in this case the housing。

 prices and we're going to be interested in the question of whether the value in one neighborhood。

 is related to the values in the nearby neighborhoods okay so it's auto correlation because it's a single。

 variable but it's still going to be a form of auto correlation of correlation so we're using the same。

 data same plot from before and what we do with auto correlation first we're going to start with。

 what's on his global auto correlation we're going to pair two types of similarity together the first。

 is value similarity so we want to understand how far apart things are in attribute space in the value。

 of attribute space so high rents are far away from low rents okay and close rents are close but we。

 want to couple that with a notion of geographical similarity right so how we express that gets into。

 a large literature we're going to use what are known as spatial weights that define neighbors so。

 they're similar to like an adjacency matrix for network analysis if those of you took any of the。

 network tutorials all right spatial weights are very similar they have a similar mathematical。

 representation but our spatial weight here you can define it many different ways neighbors we're。

 going to use simple contiguity which is going to leverage some of the geo processing we saw。

 this morning and we're going to define neighboring districts as though that share a vertex or an edge。

 on their polygon borders and from that we're going to construct from pie cell a queen。

 contiguity structure that is if any two polygons share at least one vertex their neighbors okay now。

 we're reading a data frame here so we're peaking into that geometry column and running an algorithm。

 that detects the topology okay so our queen w is telling us who is a neighbor of who。

 and that's our geographical similarity you can think of this as a matrix although it's not a。

 matrix each row tells us for polygon zero who its neighbors are there's non zero values in that row。

 in this case ones where we have a neighbor between column row i and neighborhood j if they're not。

 neighbors it's a zero we're going to transform those ones to be row standardized so that now if we。

 summed across the row the value would be one so the weights get row normalized that's what we're。

 doing here we use the weights the wijs to develop a weighted average of the attribute values。

 in the local context that is for a given district we now know what the neighboring districts are。

 so we need an average of the housing values in that neighborhood and that's the operation that's。

 where the spatial weights come in so it's simply a weighted average of the values for the neighbors。

 and it's this variable called the spatial lag which we're going to then correlate with the。

 original housing price so it is in fact a correlation we've just constructed a spatially explicit variable。

 that captures local context and so we correlate them ultimately so that's our spatial lag。

 and we can plot it it's like a smoother for those of you who do remote sensing in a sense but this is。



![](img/81e8c90c191b11ba7052bce0b0522fb5_656.png)

 not a pixel image right these are your regular polygons so this tells us about what's going on。

 around a focal polygon right but it's the value in the polygon so it's looking at information in my。

 neighbor and bringing it back into my neighborhood and what we're interested in now is these two maps。



![](img/81e8c90c191b11ba7052bce0b0522fb5_658.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_659.png)

 the original price is on the left that's the quintile map and the spatial lag is on the right so。

 now we want to explore the correlation between those two maps so it's a bivariate correlation in a sense。

 this is also another course 15 weeks of spatial statistics so we're going to do a quick dive here。



![](img/81e8c90c191b11ba7052bce0b0522fb5_661.png)

 so are these correlated or not this is not a scatter plot this is very complex visually to get out。

 okay so we're going to use statistics to get out this and we're going to back up and make it simpler。

 to develop our notion of why these statistics work instead of having five classes we're going。

 to have a black and white map high values and low values so we're going to convert our binary we're。

 going to convert our housing values to high and low here and then i'm going to plot that map。

 to reduce the cognitive load so the dark polygons black are above the mean housing price or rent。



![](img/81e8c90c191b11ba7052bce0b0522fb5_663.png)

 white are low and now we're interested in the question of if those black polygons are randomly。

 distributed in space and conversely are the white polygons randomly distributed in space。

 or is there some structure there right and we're going to come up with statistical test to answer。



![](img/81e8c90c191b11ba7052bce0b0522fb5_665.png)

 that question the oldest tests are called join counts so is that map random or not that's our。

 question our null hypothesis is that if we had say 68 black polygons and you randomly assign them on。

 the map what would the map look like if there's no structure in the process generating the data。

 so we need a test against that hypothesis so join counts work with joins and all the join is。



![](img/81e8c90c191b11ba7052bce0b0522fb5_667.png)

 is when you have a pair of neighboring polygons and we know how many neighbors there are because。

 that comes from our w so for each join we then ask well what type of join is it is it a poor。

 neighborhood next to a poor neighborhood or a low low or white white or is it a rich neighborhood next。

 to a rich neighborhood dark dark black black or is it heterogeneous white next to black or black。

 next to white so there's only these three types of joins possible black black white white or black。

 white and join counts we're going to count up how many of those different types of joins did we get。



![](img/81e8c90c191b11ba7052bce0b0522fb5_669.png)

 in our actual data versus some reference distribution under the null the null that whatever governs。

 housing markets in Berlin is random spatially okay questions on those concepts。

 okay so we need to count the joins and in pie cell we have an as-de-module for exploratory。

 spatial data analysis it uses our w object together with our binary attributes so join counts you pass。

 in the yb which is the binary valued attribute and our spatial weights and then it creates an。

 instance of our JC object found out that there's was 121 black black joins on the actual map。

 114 black white and 150 black white and that's it that they're going to exhaust the number of joins。



![](img/81e8c90c191b11ba7052bce0b0522fb5_671.png)

 the number of joins is a attribute of the spatial weights because it's a binary weights matrix so。

 it tells us how many neighboring pairs are there and there's 385 so now we're back to the question。

 if you had six to eight black cells and that spatial structure for the joins what we would。

 expect for where those six to eight black cells would be co-located or not co-located。



![](img/81e8c90c191b11ba7052bce0b0522fb5_673.png)

 how many did we get we actually got 121 but we need a reference distribution all right to decide if。

 that count is higher or lower than what we would expect under the null and in pie cell there's two。

 ways to get a reference distribution there's analytically statisticians have derived what the。

 distribution should be so it's like looking up in the back of a stats book and comparing your value。

 to a table but they don't work so well because every map is different they're not regular lattices we。

 have different geometries so instead we rely on computationally based inference we're going to play。

 creator of the universe and simulate the null hypothesis by taking up the actual housing values。

 and shuffling them around the map randomly right because that's the null the null is that there's。

 no spatial structure we create one synthetic map we recalculate our statistic so now we have two。

 values for our statistic our observed value and this one from the synthetic map this is called a。

 permutation of the values we repeat this say a thousand times or ten thousand times depending on。

 how much you want to do and for each one of those we have a draw from the null distribution and from。

 that we collect all these and we compare our observed value against the null to decide if it's。

 significant or not and it's a pseudo significant value so we do that when we create the the。



![](img/81e8c90c191b11ba7052bce0b0522fb5_675.png)

 instance of the joint count on average for the fake maps you should have got 99 black black。

 joints that's the average but we have all those synthetic joints so if we do a kernel of the null。

 values that's the blue kernel that's what to expect under the universe where housing markets are。

 random spatially there's no housing markets that are random spatially in the world that that we know。

 of so this is not a surprise but how extreme is our observed value well that's the red that's the。

 value indicated by the red line so way out in the tail in fact none of the values from the fake。

 maps where as extreme is what we observed right so it's highly autocorrelated data here right。

 there's strong spatial structure there and hopefully you get a sense that this is a very。

 nice complementarity to the visualization of the map pattern because map patterns are complex to。



![](img/81e8c90c191b11ba7052bce0b0522fb5_677.png)

 process all right so that's our pseudo p-value that's one of the attributes that's calculated。



![](img/81e8c90c191b11ba7052bce0b0522fb5_679.png)

 and it's simply the number that we're as extreme or plus the one that we got because we pretend。

 like ours came from the null divided by the number of permutations I think it was at 999。

 plus the one we had that's all that value is the p-value。



![](img/81e8c90c191b11ba7052bce0b0522fb5_681.png)

 well we threw away a lot of information when we did the binary conversion。

 but that was just to try and develop our intuition of how the autocorrelation tests the logic of the。

 autocorrelation test so did that sink in I know it's all it's compressed there are there's an。

 industry of autocorrelation test there's new ones coming out all the time for spatial。

 correlation we're going to look at well what if you kept it in continuous space so now we'll look。

 at a test for the the actual values not the binary values it's called a meringue i for the。

 guy who invented it meringue was a statistician same idea you pass in the value array y and your。

 spatial weights and you get back an instance of meringue i had a observed value of 0。09 is。

 that larger not we don't know we need a reference distribution to compare it against and again。

 there's two ways there's analytical theoretically and then computationally based so we're going to。



![](img/81e8c90c191b11ba7052bce0b0522fb5_683.png)

 show the computationally based one here and for the continuous value it's slightly different。



![](img/81e8c90c191b11ba7052bce0b0522fb5_685.png)

 so the synthetic p-value is still below 5% which is your conventional cutoff for a significant。

 statistic so this is almost 2% it's not as extreme as the binary case but remember for the binary。

 case we threw away a lot of information we reduce a lot of the variation in the data because all the。

 high values are treated equally even though we know there's some very extreme high values this。

 we're retaining the full range of the values okay so it's still significant and then lastly to finish。



![](img/81e8c90c191b11ba7052bce0b0522fb5_687.png)

 off this section on order correlation test the these are these two tests were global they answer。

 the question about the map as a whole is that map random or is it not random yes or no but we have a。

 quantification of that there's a newer set of literature on what are called local spatial statistics。

 and here these local statistics are designed to identify the locations that are perhaps driving。

 the overall pattern or that deviate from the overall pattern or spatial outliers so we get into。

 notions of identifying hotspots and cold spots and we're going to do the same thing here this is a。



![](img/81e8c90c191b11ba7052bce0b0522fb5_689.png)

 scatter plot which shows us on the x-axis this is the housing price for a given neighborhood on x on y。

 it's a housing price for the spatial lag the weighted average in the neighborhood of that。

 neighborhood all right so the weighted average in the neighborhoods they're surrounding a district。

 and so the scatter plot lets us think about different types of spatial association local。

 spatial association so if you think about the vertical bar to the right of that those are above。

 average rent districts to the left those are the low rent districts but what about the y-axis。

 the above are high neighborhood values so high values in the neighborhood below neighborhoods that。

 are lower value surrounding me so we put the two together we have four quadrants if we're up here。

 what's this neighborhood what can we say about that neighborhood is it high or low。

 high and what about the market surrounding it they're also high so it's a high high location。

 and quadrant one quadrant two mathematicians go counterclockwise don't ask me why quadrant two。

 what do we know about this neighborhood is it above or below the average。

 it's below right it's to the left but what about its neighbors those are high right so this is low。

 surrounded by high sort of the donut hole in the middle good stuff on the on the uh。

 the outside of the donut down here in quadrant three these are。

 low low right so these are areas where you have low housing values surrounded by。

 neighborhoods with low housing values and then finally quadrant four。

 high value surrounded by low values right so these are like diamonds in the rough。

 so we have different types of spatial association here in quadrant one in quadrant three we have。

 positive spatial association or value similarity in space you have a high value next to a high value。

 quadrant one or low value next to the low value in quadrant three that's positive association。

 negative association is quadrants two and four low value surrounded by high values or。

 high value surrounded by low values all of those are different types of spatial association。

 if there was randomness on the map these points would be randomly distributed across these four。

 quadrants but they're not right they're concentrated in one and three and the slope of that line is。

 meringue's eye that global statistic so our local statistics now the first one instead of having one。



![](img/81e8c90c191b11ba7052bce0b0522fb5_691.png)

 statistic for the whole map now we have a statistic for each location and it tells us multiple things。

 the first thing the queue attribute tells us which quadrant is that statistic in is it one two three。

 or four okay in the scatter plot and then we're going to test if each one is significant or not。



![](img/81e8c90c191b11ba7052bce0b0522fb5_693.png)

 using permutations but now it's more complex for technical reasons we have to hold that location。

 fixed and permute the complement set because you can't be your own neighbor unfortunately。

 otherwise you would inflate the spatial dependence which means if we do 10，000 permutations。

 we have to do 10，000 different permutations for each location one free one set for each location。

 and then we can map these so now we're going to map those locations that were in quadrant one。



![](img/81e8c90c191b11ba7052bce0b0522fb5_695.png)

 in the scatter plot that were statistically significant that is there's something going on with that。

 location and its neighbors they're both coincidentally high not coincidentally but they're。

 coincident in space all right and where are they they're in the center of the city in this case。



![](img/81e8c90c191b11ba7052bce0b0522fb5_697.png)

 so those are our hotspots the other ones are not significant okay so we're treating them as we。

 don't care we just want to find out where the hotspots are for the market in this case。

 the other types of spatial association are the cold spots so the cold spots are those again that。



![](img/81e8c90c191b11ba7052bce0b0522fb5_699.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_700.png)

 were in quadrant three but we're statistically statistically significant and we plot those。

 their locations and then finally we can do it with the outliers so i'm going to jump to the。



![](img/81e8c90c191b11ba7052bce0b0522fb5_702.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_703.png)

 final map here so the outliers were in quadrants two which are the donuts and quadrant three the。

 diamonds in the rough so this gives you a view of the spatial distribution of the housing values。

 from a spatially explicit perspective is now we've coupled these quantitative summaries of local。

 spatial association together with the actual geography of burlin okay so this this is exploratory。

 set of methods this leads to questions about why this map is like it is the job of these methods。

 is to raise those questions the job of these methods is not to answer these questions。

 they're exploratory methods right so they're fitting in that part of the spatial analytical workflow。

 okay questions on on these so the way you're testing for statistical significance of all the。

 hotspots is basically perfuming randomly how are you doing that okay so for this guy right here。

 this polygon we know how many neighbors it has so it might have six neighbors so actually what we do。

 is we take the set of the observed values except that one we randomly select six from that set。

 and we recalculate its local statistic and you do that over and over again and then you just find。

 it out which is in the you know whether or not it's in the five or ten percent yeah essentially yeah。

 you find out how many more how many of the synthetic ones are more extreme than what we observed。

 okay great okay all right and then Levi's gonna turn to the well I'll let him talk about what he's。

 gonna turn to so I figured we've got about an hour left and we've got by the way my name is Levi。

 Wolf I'm an assistant professor at the University of Bristol and so we've got essentially three。



![](img/81e8c90c191b11ba7052bce0b0522fb5_705.png)

 notebooks left one of them is sort of a problem set based on the local lot of correlation stuff。

 that we just did that would give you more of a sort of hands-on sense for how these things work。

 what it means when you detect a cluster and sort of subjectively how to connect that to。

 what that means in your own maps would you like to do that or would you have them move on to。

 regression and clustering I guess problem set raise your hand。

 well a couple let's do the problem set because the only people who voted。



![](img/81e8c90c191b11ba7052bce0b0522fb5_707.png)

 oh okay no problem set raise your hand okay quite a few okay well then let's move past that then。



![](img/81e8c90c191b11ba7052bce0b0522fb5_709.png)

 if you want to check that out it's the case jenny in a bottle the trump vote it's on the。

 relationship between economic inequality and the change in vote from obama to trump。

 kind of some interesting stuff there that you can find in the local structure of vote by county。



![](img/81e8c90c191b11ba7052bce0b0522fb5_711.png)

 so the first thing that we're going to do is we're going to move。

 on to the progression notebook so this is notebook number seven。

 when we're talking about how to use geography in data science applications you can sort of think of it。

 most commonly and most useful applications as a data borrowing technique so when Serge was。

 talking about the spatial lag right what we're doing is we're constructing a new feature。

 that gives us the average of a particular feature in the area surrounding every single observation。

 right so if I have spatial data and I come up with some way to build a weights matrix right a weight。

 matrix for what we were talking about before is like an adjacency matrix kind of for the graph。

 of connectivity between the polygons you can have this for point data which we'll be doing here in a。

 second but if you come up with a way to express all of these spatial relationships at once。

 and you come up with a way to compute these neighborhood averages you can use them quite often。

 to do data science as synthetic data right but in reality what we're doing is we're using geography。

 as an instrument to give us additional features we would call this in other context feature engineering。

 so here I'm going to import a couple packages that we're going to be using and we're going to read。

 in the same Airbnb data that we saw from the other notebook but this time we're going to also get。



![](img/81e8c90c191b11ba7052bce0b0522fb5_713.png)

 information about the Airbnb prices at point level so this is a collection of I think about。

 14 000 prices of Airbnb listings in Berlin so these are nightly listing prices so every night。

 some of these may have different minimums so implicitly they're priced slightly differently so if this。

 were sort of a full analysis you'd have to take into account a couple of different things but in。



![](img/81e8c90c191b11ba7052bce0b0522fb5_715.png)

 general this is the spatial distribution of our prices in the neighborhood and then let's。



![](img/81e8c90c191b11ba7052bce0b0522fb5_717.png)

 or across these residential districts and then let's construct actually let's leave it like that。

 so the first off the first thing that we'll do is conduct a kernel regression right so some of you。

 have may may be aware of what a kernel regression does um in oh do you have a question no okay um。

 classically speaking how kernel regression works is in feature space you sort of usually it's。

 used in classification you may hear about voting classification algorithms and things like that。

 essentially what you're doing is given a new observation you try and figure out which class。

 that observation is a member of by looking at an adjacent number or a distance decay radius of nearby。

 observations in feature space so in the multi-dimensional space of features that you have and you're sort。

 of taking the neighbor that all of the people agree based on their class so if I'm a new observation。

 most of my neighbors are in class two then you would predict that I am also in class two that's kind。

 of in general how these uh uh kernel regression ideas work so that's in a classification context。

 in a prediction context you'd sort of take the neighborhood average so we would take if I got a。

 new Airbnb listing I might predict its price to be the average of its 10 nearest listings um and so。

 scikit does this stuff inside of the um kernel uh regression framework and we'll talk about that in。

 a second but here I'm going to pull out some data that's relevant to what we might think the price of。

 an Airbnb should be uh we have the number of people that the Airbnb says that it accommodates so this is。

 where the the host says you know this can sleep about six people across three beds or whatever um。

 you've got the full rating of uh the the listing itself so we call this the review scores rating。

 we've got the number of bedrooms in the listing the number of bathrooms in the listing the number of。

 beds in the listing the actual price and then the geometry so I'm just extracting this from the original。

 what the listing data frame which has a ton more information than what we need。

 and then here I'm in a structure sort of like a regressive framework where I've got some。

 predictor variables and then I'm trying to predict price of the Airbnb listing and here I'm just again。

 extracting this all from the data frame so we can work with it in shorthand the last thing I'm going。

 to do is I'm going to pull out the coordinates of all of the Airbnb listings from our data frame。

 and I'm going to do this by going through every single row of the data frame and pulling out its。

 xy coordinates stacking it into an array and then stacking that whole thing together itself as an。

 array so coordinates now is just an umpire a full of projected data this happens to be in web。

 mercator which is accurate enough for the scale of computations that we're doing here。

 so here now I've got this non-py array of xy coordinates which we'll use to to conduct these。

 regressions so the easiest sort of fundamental neighbor regressions that you can use are in the。

 scikit learn neighbors module and this has a bunch of functions that some of them operate similar to。

 the pie cell weighting functions for spatial weights ours tend to be a little bit more。

 geographically focused whereas the knn stuff and well the near neighbor stuff in scikit tends to。

 be a lot more general for future space stuff but then we're just going to split our data into。

 some training and some testing stuff for trying to predict these Airbnb neighborhoods and then。

 I'm going to do three different things down here if you look at this next cell I'm going to。

 fit three different neighbor regressions the first one is what I'm calling the spatial。

 neighbor regression so what this does is it only looks at the prices of airbnbs that we observe。

 and it tries to predict what the or it will eventually it will try and predict the price of any。

 testing data based on the closest elements inside of our training data does that make sense so we're。

 just using basic spatial distance inverse distance weighted as a way to predict our holdout set。

 so you could do this for any kind of feature data that you want to train a model on you could see。

 whether or not it holds you could you know do all sorts of hyperparameter optimization on this。

 some cities may have different urban structures so you have to use what are called。

 anisotropic distance measures which depend on the angle at which observations are related to one。

 another then we're going to check this against an attribute version and the attribute version。

 is going to pick prices from our our training set again but it's going to try and use these。

 exogenous regressors so these additional informations that we have about our airbnbs。

 the accommodation the the number of beds that kind of stuff it's sort of a more classic framework。

 we're going to try there and then we're going to try and mix these two things together we're。

 going to try and give an information about we're going to try and make predictions about airbnbs。

 just naively using the spatial coordinates of the longitude and latitude as features themselves。

 okay so there's three models here that we're about to fit it's a spatial one which is just。

 doing basic surface interpolation there's sort of what you would consider a more classical regression。

 which is using nearby features to predict nearby output and then we're using a hybrid version of。

 that then we're going to make our predictions what's up oh yeah。

 is there a reason why you declared data of k nearest。

 neighbors from respiratory times would that just need to be third ones and you could shoot it into。

 a few holes or pretty sure you don't have to to play that three times i just did it for。

 assuredness i mean the initialization of a psychic estimators pretty cheap so in this case so it's。

 you can you can change that as you want， so then we're going to predict all of these values based on what we've got so we're trying to predict。

 the spatial prediction is only going to use the coordinates of our observations to try and predict。

 prices the attribute based version is going to try and predict prices based on the nearest。

 exogenous information that we have so using our x matrix using the information on you know uh。

 accommodates or things like that we're going to pick the other ones that are nearest to the holdout。

 set in the feature space there's no information about geography at all it's only nearest in terms of。

 most similar in observed attribute and then finally we're going to fit what i'm calling this sort of。

 hybrid model which uses latitude and longitude as themselves part of the attribute set now when。

 you look at the accuracy of these things um you see that the spatial model has about 10 percent of。

 variance explained so just by using the outcome itself not including any of our exogenous。

 regressors we get an explained variance score of about 10 percent our exogenous regressor model the。

 one that uses the x information which could potentially be a huge amount of x information uh。

 attains about a 33 percent and finally when you mix both of them together naively you absolutely。

 tank your model score so what this is supposed to show you is that if you do want to try and use。

 spatial data you have to be careful about how you include it oftentimes it's not going to be。

 sufficient just to include a naive longitude and latitude into your data you should try and use。

 these concepts that were teaching you such as the spatial lag using neighborhood averages as。

 engineered features rather than just naively including information about spatial position。

 does that make sense cool are there any questions just on this little example here。

 does anyone want to see any alternative reconfigurations or refits yeah。

 uh i believe that i'm splitting into， yeah i think i'm only holding out 2。

000 observations or so so that that can change， the other thing is we don't necessarily know i haven't ensured that the holdout set is spatially。

 random so it could be that there's spatial structure in the holdout set that affects our prediction。

 accuracy i'm we're not going to talk about that but all that kind of stuff can be assessed using。

 local statistical techniques and and things we discussed previously all of that exploratory。

 data analysis stuff applies to any type of spatial data you just have to figure out how to express。

 the topology um so yeah i think we're only holding about like 2。

000 out are there any other questions， on this just basic example here none okay。

 so what i would suggest then if you're interested in looking at these kinds of kernel based。

 regressions for local data uh there's a package in the library analytic library that we work on。

 called gwr and gwr stands for geographically weighted regression。

 geographically weighted regression is kind of like a mixture of these two concepts of。

 feature space regression and spatial regression in essence what it's doing is it's fitting models。

 at each site if you've ever heard of kreeking or you've ever heard of spatial differential process。

 models these are all sort of a family of local smoothing models that all work in a sort of similar。

 way this one is a generalized additive model that uses spatial position to localize predictions and。

 estimates so the second thing we're going to do is i'm going to show you how to use this spatial lag。

 slash data borrowing technique in a more classical regression setup so we're not going to use this。

 knn regressing kind of stuff so here i need to do some conditioning on our weight symmetrics because。

 by default if we construct a spatial kernel uh weight uh it fills the diagonal with uh ones and。

 we want to make sure that we fill the diagonal with zeros so that our focal observation does not。

 contribute anything to its estimate of the surrounding averages so here i'm going to fit that kernel。

 weight which is just going to apply a Gaussian kernel to every observation it's going to adapt。

 the bandwidth to ensure that a particular k-nearest neighbor criterion is satisfied so i i believe we。

 include a whole notebook that goes way in depth on these weights matrices and how to model sort of。

 spatial relationships specifically but here i'm just using this to uh to provide it takes a while。

 uh bummer k is a hundred okay well， so so the point of doing this here in the same way that in the previous notebook we constructed an。

 jc and c graph using the queen's weight criteria this is going to give us a sort of weighted uh a。

 way to construct a spatially weighted average of the nearest hundred observations that we have in our。

 dataset so using this kernel weights it's kind of like if you use post gis or something like that when。

 you when you're doing spatial indexing queries what these weights objects represent sort of conceptually。

 is the output of an all-pairs spatial relationship query and we do this one time ahead of computation。

 so that we don't have to do it later when we're running the techniques it allows us to express。

 everything in terms of matrix and linear algebra rather than needing to express it in。

 sort of query language like post gis usually uses so now i've run this weighting function。

 we've got a kernel weight which gives us a Gaussian kernel centered on every single air b and b。

 that gives us a distance decay based on the Gaussian radial basis function based on the geographic。

 distance away from that observation so this is just an arbitrary way that i can say this observation。

 is related to this observation by this spatial kernel y'all have seen heat maps before this。

 probably is somewhat familiar now our data matrix remember is all of this data accommodates review。

 scores bedrooms bathrooms and beds so that kernel weights matrix is in general just an end by end。

 matrix that has been sort of specially constructed to give us certain attributes so when i compute。

 this wx i'm pre-multiplying that matrix by my data matrix and that will give me a new data matrix。

 which gives us the neighborhood average of every column in our original neighborhood matrix so this。

 stuff scales usually pretty well if i can get that weighting matrix i can use it as a filter to。

 construct spatial averages so now if i look at wx the matrix it's a numpy array but it's a。

 numpy array which reflects a weighted summary of all of the neighboring observations to that。

 specific observation so wx and x well let's grab wx zero just to show。

 so these two things are not related at all right so that the the the wx summarizes the。

 surroundings of the first observation and x summarizes the observation itself right if we look at the。

 actual neighbors for kw0 we get that it has all of these hundred neighbors with this gouch and kernel。



![](img/81e8c90c191b11ba7052bce0b0522fb5_719.png)

 weight now if we wanted it to be on the same scale as our input data we have to do one additional。

 thing we have to row standardize it and then construct the lag again we'll do that here i didn't。



![](img/81e8c90c191b11ba7052bce0b0522fb5_721.png)

 do that in the notebook originally so now our focal observation for our first observation。

 accommodates two people but the hundred hundred nearest air air bnb listings tend to accommodate。

 around three people does that make sense the focal observation the first observation has a review。

 score rating of a hundred but the hundred nearby air bnb listings only have a review score rating。

 of 92 since we've constructed this kernel weights all of these things become sort of。



![](img/81e8c90c191b11ba7052bce0b0522fb5_723.png)

 de facto queries that we've done the computation ahead of time okay so using stats models but you。



![](img/81e8c90c191b11ba7052bce0b0522fb5_725.png)

 could use your favorite regression package and achieve the same thing we're going to first check。



![](img/81e8c90c191b11ba7052bce0b0522fb5_727.png)

 out our model which is a standard ols trying to predict prices using the attribute information。

 that we had before and we're going to get sort of not a very good model it gives us an r square about。



![](img/81e8c90c191b11ba7052bce0b0522fb5_729.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_730.png)

 0。29 we get most of our effects are significant except for the the number of bathrooms effects so。

 i mean obviously we're not using this to do any like inferential science on the theory of why air。

 bnb prices are what they are but it would be interesting to note that bathrooms don't significantly。



![](img/81e8c90c191b11ba7052bce0b0522fb5_732.png)

 affect air bnb prices but then in addition to this we'll construct a hybrid table together。



![](img/81e8c90c191b11ba7052bce0b0522fb5_734.png)

 this xwx table which has let's just grab the head。

 so this table has both our focal observations now and then these lags right so for every single。

 attribute that we're using we're going to grab the lag attribute as well and then we're going to use。

 these together in a regression and when we do that we notice that the r squared bumps a little bit。

 so we've done this feature engineering now we've looked at constructing 100 the neighborhood average。



![](img/81e8c90c191b11ba7052bce0b0522fb5_736.png)

 of 100 nearest observations and we've gotten out this new regression where we find indeed some of。

 these contexts are actually statistically significant useful predictors and we've improved our model in。



![](img/81e8c90c191b11ba7052bce0b0522fb5_738.png)

 general so for instance when you're considering sort of the the review scores locally the the review。

 score of the air bnb matters but the quality of surrounding air bnb is also matters and in fact。

 that lag coefficient estimate is actually larger than the original one so that sort of gives you an。

 index of how desirable the area is sort of in this intrinsic unmeasurable quantity we've sort of。

 instrumented it with the neighborhood average of reviews does that make sense if you're staying in。

 an area with highly reviewed air bnb's it sort of gives us some information about that context in。



![](img/81e8c90c191b11ba7052bce0b0522fb5_740.png)

 which that every and b lives so there's an additional collection of functions in pie cell these live。

 under the pie cell the pie cell that spatial regression module and these all involve various。



![](img/81e8c90c191b11ba7052bce0b0522fb5_742.png)

 different types of spatially relevant specifications so let's just fit one here on。



![](img/81e8c90c191b11ba7052bce0b0522fb5_744.png)

 y and x wx table dot values。

![](img/81e8c90c191b11ba7052bce0b0522fb5_746.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_747.png)

 oop， no it's not going to work for yeah okay so there's some incongruousness between some of the stuff。

 that we're working on in pie cell right now but there are other methods such as these lag object。

 or sort of what they call lag regressions so here in the previous section we just fit a linear。

 regression that looks like this， and where this wx here reflects the neighborhood averaging that we've done right there's also。

 another class of models that can be fit in pie cell and other places you can fit them in stand。

 pimc is a little difficult and this class of models fits instead a version kind of like our。

 kernel regressor and you can throw in a wx if you want but you don't have to where you now have。

 your outcome on both sides and this sort of mixes the strength of the kernel regression。

 which borrows the similarity in the outcome to predict new outcomes in this regression you're。

 using the outcome as an endogenous factor you're saying that the the price nightly price of an。

 airbnb cannot be determined by itself you know i am competing if i'm an airbnb tenant or airbnb。

 lord whatever they call them uh i don't like airbnb lord but i guess i'll use that if i'm if i'm。

 running an airbnb shop and i'm pricing airbnb is i'm cognizant of the the price of surrounding。

 areas right so i can't i don't have full price setting ability in order for me to set my price。

 i need to be competing with the people that are spatially next to me right because they have a。

 similar set of amenities they have access to similar urban areas similar transit outcomes right so。

 because of this we can't necessarily say that we would expect all of these things to be independent。

 of one another and one way that we can model that is by this hybrid outcome method uh those get a。

 little bit more complicated because they become nonlinear regressions uh so mathematically speaking。

 there's probably not a way that we can efficiently solve this one in this particular kernel weights。

 configuration but there are ways as these get sparser to fit very well so doing them on tens of thousands。

 of observations as long as you've got really sparse connectivity works just fine um so this is。

 what we have on the regression section are there any questions as far as what we've talked about。

 on data borrowing as a conceptual method to bring in geography into your modeling using these。

 kinds of neighborhood averages no okay， yeah so i have written um some stuff to sample spatial models in a Gibbs sampler for multi-level。

 stuff um but and i've also written some code to do some of this in stan we don't do most of the。

 stuff comes from maximum likelihood estimation perspectives so in general like we don't we don't。

 support Bayesian inference the only the stuff that i've written as sort of packages under pie-sau。

 fit those kinds of models yes true as well there's um looking at local smoothing of attribute。

 weights sort of more on either outlier detection or local area modeling that that can get in time。

 but if you do want to if you are interested in fitting these kinds of endogenous outcome models。

 i would suggest that usually the prior like there's some tools in python um。

 i think it's probably best if you fit them in r there's like a well established Monte Carlo。

 sampler there well it's a Gibbs sampler metropolis with n Gibbs but the gradient stuff gets difficult。

 because this reduces to a difficult expression to differentiate so the conditional posteriors of。

 of the autoregressive component don't sample very well um so i just had a paper out last year i think。

 that looked at that kind of stuff and it's tough yeah the term you're using data borrowing refers to。

 the feature in here and stuff yes so it refers to constructing new attributes either from WX or。

 WY yeah yeah i mean you can call it what you like i thought that data borrowing was a good。

 descriptive name for what's going on uh formally speaking yes it is a form of of。

 weighting your your exogenous covariates but um semantically speaking your regression gains。

 strength because you're borrowing additional information based on its spatial configuration。

 of observations so yes yeah right so you're not i mean it yeah yeah so you're well i mean you do。

 get more parameters that have to be fit there so technically you do lose degrees of freedom to fit。

 those parameters but in general you're not making a more complex model yeah so you can you can。

 stuff it in any place where you use a linear model which i presume is all places for most people。

 any place you use your linear model you can bring in geography by using these data borrowing。

 techniques this stuff the endogenous regression is more difficult in general there's not a closed。

 form solution depending on what you do so like you have to use a different sampler if you want to do。

 this in a logit situation you can't fit it in particular ways in that way does that make sense。

 any other questions you all have a good idea about how you might apply this particular technique。

 in your future linear models okay so then we can move on to clustering and we can do the problem。



![](img/81e8c90c191b11ba7052bce0b0522fb5_749.png)

 set i'm going to ask another another poll maybe not we'll just do the clustering so we'll move to oh wait。

 is everyone following find does anyone need a break oh okay i guess you've been here for。

 three we've been here for three hours so it's it's a long time is everyone on clustering yeah。

 huh that's strange yeah so when it comes to clustering surge talks a lot about。

 the stuff that we have in pie style that will do map classification and in traditional geographic。

 perspective map classification is sort of a thing that we talk about for univariate data when we're。

 visualizing the structure distr spatial structure of our distribution of data and if any of you this。

 is only supposed to be an introductory workshop so we're not getting too heavy into the theory of。

 clustering in your data but if any of you have used stuff like multi-dimensional k-means or or。

 other things like that you know that it gives you this sort of dimension reduction technique it。

 allows you to take large amounts of data and express them in latent categories it's kind of what map。

 classification is supposed to do but then we can do it with much more data than what we had before。

 so what i'm going to show you here is how to search for and use these clustering methods on。

 larger data does that make sense cool so the first thing we're going to look at again is this。

 Berlin listings data set and i'm just showing you again how this Berlin listings data set looks。

 and then we're going to pull up the the scikit clustering module which you should all have。

 installed if you follow the directions and again i'm going to pull out a coordinate array。

 so most of the stuff that geopan is as useful for is to be able to sort of work with your。

 spatial data but again scikit doesn't really care about where it comes from once these。

 numpy arrays so we kind of have to play nice with that it would be nice if we could just send it。

 a geo-series and it understood how to get the coordinate array but it's um definitely not。

 there yet so the first kind of clustering technique that you may have heard of is db-scan right this。

 is a density-based scanning method that um it it looks at sort of local reachability tries to find。

 areas of high density and interconnection between observations and discover where。

 sort of regions exist so we're going to apply this db-scan just on the spatial information so。

 we're not going to consider anything about the attributes themselves we're going to do what's called。

 regionalization regionalization is slightly different from generic clustering in a spatial。

 context regionalization is a graph partition we're trying to split the data into contiguous sort of。

 geographically well-defined zones and what db-scan applied to spatial coordinates will do is give us。

 that right just like we usually use db-scan in feature space to give us well-defined zones with。

 attribute similarity internally this will give us well-defined zones where observations tend to be。

 closer to one another in this zone than they tend to be outside but that's only in the geographic。

 dimension not in the attribute dimension so here we've applied db-scan to the spatial coordinates and。

 I've tuned the epsilon here you have to do a a hyperparameter search depending on the projection。

 it's not insensitive to that so when you use these db-scan clusters you get information about what the。

 cluster discovers is the cores of every one of these clusters so these would be in other contexts like。

 affinity affinity propagative sampling and you'd get these things called exemplars so when you hear。

 core sample indices these are things that are sort of like the most cognizant elements of that cluster。

 and then we get this label array and as Serge was talking about in the map classifiers。

 this dot labels attribute is mainly what we're interested in right so we do these clustering。

 applications we get these labels and then we use these labels in order to visualize complex。



![](img/81e8c90c191b11ba7052bce0b0522fb5_751.png)

 patterns in the data so here what I'm recommending is that when you want to do this kind of study。

 you go through you use your psychic classifier you do whatever you want maybe you have a special。



![](img/81e8c90c191b11ba7052bce0b0522fb5_753.png)

 model in karas that you like and then you can again pop it back down into geopandas and plot。



![](img/81e8c90c191b11ba7052bce0b0522fb5_755.png)

 so mainly what we're doing is we're going most of the data analysis workflow is pull in your data。

 do some exploratory statistics to try and get your head around the spatial structure of the data。

 build some spatial weights matrices and then use those to do all your data science bring it back。

 in a geopandas plot work with it export it make dashboards things like that so when we've done。

 these clusterings in in db scan what we've done here is we've shown that every every single one of。

 these are latent density clusters so these represent areas where every and b listings are closer to one。

 another than they are to any other one and we see that mainly what we find is Berlin is a cluster。

 right well tuning the epsilon value will give you different sort of resolutions on those clusters。



![](img/81e8c90c191b11ba7052bce0b0522fb5_757.png)

 it'll tell you how far apart observations need to be in order to be considered disconnected so。

 many of you may have heard of hdb skin which is a hierarchical density based clustering technique。

 based on db skin does some of this tuning for you but also introduces more implicit parameters。

 the point of this was not to show you the best clustering the point of this was to show you that。

 some of these methods when you apply them just on the lat longs will give you these sort of。

 zonations and a lot of people want to solve zonation problems so when you do these kinds of。

 zonations keep that in mind if you set the epsilon to a much smaller value you get a lot more。



![](img/81e8c90c191b11ba7052bce0b0522fb5_759.png)

 yeah or it would error because you don't get connected graphs so like if we drop。

 in order of magnitude from the cluster and we pop it into the plot we'll see that most of the。

 clusters become either unaffiliated which is now the purple or so。

 yes yeah db scan itself is highly sensitive to the the structure of that so one thing that I find。

 to be helpful when i'm working with these kinds of classification labels is to sort on the labels。

 because when you get when you get the classification vector back from scikit you get negative one is。

 is like no classification found so when you sort based on the labels you can pop those below the。

 rest of the map gives you a nice sort of impression of where those clusters are found so here now。

 instead of saying at a thousand feet observations are going to be considered disconnected now i've。

 said at a hundred feet observations are going to be disconnected and use that to sort of give us。

 a sense of where these latent clusters of density exist and if you look closely。

 you can actually tell that some of these neighborhoods correspond or some of these clusters that are。

 found by db san correspond to clusters of neighborhoods in the actual shape pile of the。

 neighborhoods but we're not necessarily going to get into that because again this is contingent on a。

 lot of hyper parameters yeah i was getting the same visualization as you but i was looking at the。

 cluster dot p yeah it should be。

![](img/81e8c90c191b11ba7052bce0b0522fb5_761.png)

 hmm not sure。

![](img/81e8c90c191b11ba7052bce0b0522fb5_763.png)

 originally that should be a p i'm not sure why that's the case right now。



![](img/81e8c90c191b11ba7052bce0b0522fb5_765.png)

 i'll have to check on that and get back to you sorry about that。



![](img/81e8c90c191b11ba7052bce0b0522fb5_767.png)

 um regardless geopand is smart enough that it knows how many clusters there are in a given。

 discrete data set so it'll figure it out and we don't have to tell it。

 um any other questions on just basic zonation of data sets。

 oh okay let's move on so when you get actual aerial polygonal data how many of you tend to work。

 on like point data sets many okay how many tend to work on like aerial data sets where you've got。

 districts okay a couple i think there's a lot of people who do like econometric stuff or program。

 analysis that work on counties or zip file or zip zip code or things like that。

 so a lot of this stuff is applicable to lattices what we call them these collections of polygons that。

 touch one another but in general it's also applicable in theory to anything that's connected by an。

 adjacency graph so all of these lattice statistics are also themselves sort of graph methods weighted。

 graph methods or or what they call labeled graph methods sometimes if a node has particular。

 properties slightly different representations of the same thing that we're going to be talking。

 about here so again we've got this neighborhood data set where we've got the median price of。



![](img/81e8c90c191b11ba7052bce0b0522fb5_769.png)

 observations and first what we're going to do is we're going to look for just like we were before。

 do a map classification style approach we're going to look for three clusters inside of the。

 price data and the price data alone if you recall that's the median price distribution right so we。



![](img/81e8c90c191b11ba7052bce0b0522fb5_771.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_772.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_773.png)

 should probably find maybe two clusters maybe three clusters here i'm forcing it to be three。

 you can do some assessment we'll talk in a second about how that works and now we're mapping what。



![](img/81e8c90c191b11ba7052bce0b0522fb5_775.png)

 this distribution of median prices looks like when we're using this war to glumvertive clustering on。

 our input data again still univariate we're just visualizing the patterns in the price clustering。



![](img/81e8c90c191b11ba7052bce0b0522fb5_777.png)

 have you all heard of the very like many different kinds of cluster certainty metrics like silhouette。

 scores have you used them before no okay so a silhouette score is kind of like a regularized。

 distance although it's includes negative values as well it's it's a measure of how certain we are。



![](img/81e8c90c191b11ba7052bce0b0522fb5_779.png)

 about a given classification it's a function of how close the observation is to the center of its。

 cluster versus to the center of the closest cluster we could pick that is not that one so it's kind of。

 like we put it in cluster a and our second best choice would be cluster b how far apart is the。

 observation from its own cluster to our second choice standardized there's some stuff it's usually。

 varies between negative one and one negative one indicates lack of fit one indicates fit。

 and scikit has this silhouette samples function which allows us to compute this measure of fit for。

 every single observation in our sample so here we get a measure of how strongly these prices that。

 we fit before in this map are classified into their groups so just like before you can do sort of。

 spatial statistics on these kinds of things you can map classify has some stuff relating to this as。

 well but we're not going to deal directly in terms of these syllabus scores for the moment。

 when you visualize based on the Fisher-Janks algorithm which is a k means so that's a different。

 solver than the than the word of glumative clustering we get a different spatial distribution of our。



![](img/81e8c90c191b11ba7052bce0b0522fb5_781.png)

 attributes right so depending on what cluster you think is relevant here this is using board。



![](img/81e8c90c191b11ba7052bce0b0522fb5_783.png)

 here this is using a Fisher-Janks solver for class homogeneity you'll see that you get different。



![](img/81e8c90c191b11ba7052bce0b0522fb5_785.png)

 structures in addition our structure of certainty changes as well right so this silhouette map is。



![](img/81e8c90c191b11ba7052bce0b0522fb5_787.png)

 quite different visually from this silhouette map and again we can do sort of map comparison。

 techniques and statistical methods to compare these two things。



![](img/81e8c90c191b11ba7052bce0b0522fb5_789.png)

 and then of course you can plot these decision boundaries and see how these relationships vary。



![](img/81e8c90c191b11ba7052bce0b0522fb5_791.png)

 across different clusters when you're trying to summarize the quality of an overall fit you use。

 a weighted average of the silhouette scores so if you don't want to get the silhouette scores by。

 observation and rather just get a single map average estimate of how good your clustering is。

 you can use the psychic metrics dot silhouette score function and this will compute a weighted。

 average based on the number of observations in each cluster of those silhouette scores。

 propagating upwards so as you see here the Fisher-Janks estimate this k-means solution is slightly better。

 on homogeneity and separation than is the agglomerative clustering method okay so these are just again。

 we can do multi-dimensional versions of this because they're all just standard psychic clusters right so。



![](img/81e8c90c191b11ba7052bce0b0522fb5_793.png)

 if we wanted to then say fit let's do an agglomerative because that's kind of it's kind of simple。

 if we fit this agglomerative clustering and instead of using median price oh wait these are the districts。

 so we may not have as much information， yeah we don't have all of the information so in this particular data set i've only propagated up。

 one attribute i haven't propagated a more than one attribute so here we're just dealing but again。

 since these are psychic classifiers you can take any a number of features condense them into a labeling。

 set and then use them to do this kind of certainty analysis the second thing that's kind of helpful。

 is so we've seen zonation we've seen when you use db scan you can just construct these sort of。

 where our observations and how are they close to one another okay we've seen that we can do this。

 sort of map classification style approach where you look for high-dimensional clusters in your data。

 and you map the output of those clusterings the other thing that you can do is actually look for。

 zones that are homogenous on a given attribute and that's what i'm about to show you now。

 to do that we usually need to again build a topological relationship so i'm again going to use a particular。

 adjacency graph here i'm using a rook adjacency and rook adjacency is like queen adjacency but it。

 just means that you can only share an edge so if two polygons share a point they're not considered。

 neighbors under rook but they are considered neighbors under queen。 Does that make sense it's。

 just an analogy to chess we use it as sort of shorthand here so i'm saying that i want to。

 eventually find these clusters that are homogenous based on their attributes but then also i want。

 them to be internally connected i want them to form connected partitions of my global graph。

 and so to do this we can fit our price clusters into scikit using this structure here。

 so in the agglomerative clustering function you can actually pass a connectivity matrix and。

 pie cell constructs connectivity matrices from our weights objects on the fly so when you look at。

 oops when you look at rook graph dot sparse this is a sparse matrix that represents the adjacency。

 matrix in that weights object so any of the various types of kernel weights constructions。

 k and n weights constructions that we have will also express themselves in terms of these adjacency。

 graphs which you can then use you know you can ship this off in a network x if you want to use。

 sort of alternative types of graph partitioning but this way you can go really quickly。

 from fitting the adjacency structure in a spatial format like geo pandas straight into scikit。

 right so using these kinds of these methods so what we're going to do is we're going to look。

 for three clusters again but we're going to make it so that it obeys this connectivity graph this。

 this adjacency matrix and we're again only going to find it in the median price and we find three。

 clusters with relatively homogenous prices based on sort of uh the connectivity structure we fit。

 now you probably don't need to know a lot about briline to be able to tell me what this divide is。

 it's not actually precisely the correct divide but uh there there are some strong east west divisions。

 in briline right yeah there's there's uh there's a there's a lot that's gone on since then too um。



![](img/81e8c90c191b11ba7052bce0b0522fb5_795.png)

 so so in general we can fit these kinds of clusterings and again you can vary you can vary the。

 amount of clusterings that you find here say we wanted to find six。

 you get six clusters that are adjacent to one another。



![](img/81e8c90c191b11ba7052bce0b0522fb5_797.png)

 internally but have relatively homogenous prices so in general if you want to do this kind of。

 weighted zonation you can do it really quickly by moving straight from these connectivity objects。



![](img/81e8c90c191b11ba7052bce0b0522fb5_799.png)

 into scikit now one other thing that we can often use are these kinds of probabilistic。

 clusterings and scikit learn has a really nice Gaussian mixture model framework anyone who uses。

 Gaussian mixture models in other contexts you can do the same exact kind of analyses so here。

 i'm going to fit a Gaussian mixture classification just by forcing random state to be a particular。

 value here so that we get reproducible results passing along the price and then we're going to。

 give sort of a predicted price based on our mixture model and the most helpful thing is that。

 instead of using these silhouette scores which are what they call a post-hoc measure of fit。

 given the classification we compute the silhouette score we get these probabilistic measures。

 of class membership so here this is actually built directly into the model of clustering。

 most of the other clustering methods like a glambert of clustering and k-means。

 don't actually think about the silhouette score while they're fitting they only really think。

 about these measures of variance so these measures of deviation locally instead this is actually。

 built into the likelihood function of the Gaussian mixture model so when we recover predict proba。

 which is how certain we are that the that this observation falls among one of these three or。

 one of these six or one of these k classes we get a full matrix of prediction strength。

 so here i'm going to use just a very basic argmax here i'm going to grab the maximum。

 class and that gives us a sort of like a strength of label assignment here。

 and then again we can make this visualization of how strong our map predictions are。



![](img/81e8c90c191b11ba7052bce0b0522fb5_801.png)

 as well right but one thing you'll notice is that in general when we do these。

 a spatial clustering methods we get these unconnected graphs and we get these structures in the silhouette。

 scores which tend to not be very spatially patterned right what happens if we compute。

 the silhouette samples of things like the agglomerative method。



![](img/81e8c90c191b11ba7052bce0b0522fb5_803.png)

 did i say that yeah。

![](img/81e8c90c191b11ba7052bce0b0522fb5_805.png)

 ah that's a bummer i thought that this cell was there。



![](img/81e8c90c191b11ba7052bce0b0522fb5_807.png)

 i guess not we'll we'll go back to that so the point is anyway when you visualize these things for。

 the spatial versions of the zonation when you get these homogenous zonations uh you'll find out。

 that the spatial structure of the certainty is also very patterned right so when you enforce。

 spatial structure you actually usually lose something in terms of the fit of the cluster。

 and here i'm showing you the relationship between prediction strength on the spatially。

 constrained version and the Gaussian mixture version but the point is when you use the spatially。

 constrained stuff when you say i want contiguous zones those contiguous zones are usually never。

 going to be as homogenous as the zones that you don't force to be contiguous so you have to be。

 mindful how much do you really want that continuity how much does that really matter to what the。

 analysis you're doing is is it just for pretty maps if that's the case it may not actually be。

 worth it because the difference in the two can be rather stark however for the zonation stuff you。

 can move rather quickly from doing these top topological computations in Poisson straight out to a。

 matrix form into scikit using the tools that we've just talked about in clustering are there any。

 questions on the clustering notebook we've seen pure spatial clustering attribute clustering and。

 visualization and then sort of what we would call regionalization or contiguous zonation homogenous。

 zonation no questions this is a semester long course rather than a 14 day course but all right well。

 we've got about five four minutes so i guess we'll break just a slight bit early um if you have any。

 questions for me or my co-presenters come up talk to us we'd love to love to chat but otherwise。



![](img/81e8c90c191b11ba7052bce0b0522fb5_809.png)

 um there's a couple more resources in the in the repository like i said there's this。



![](img/81e8c90c191b11ba7052bce0b0522fb5_811.png)

 additional case study um we've also got some additional teaching materials based on spatial。

 data science and analytics in our various geographic data science repositories and a book in the works。

 so yeah please uh keep in touch and keep following us on more updates on this kind of stuff thanks。



![](img/81e8c90c191b11ba7052bce0b0522fb5_813.png)

![](img/81e8c90c191b11ba7052bce0b0522fb5_814.png)

 [applause]， [BLANK_AUDIO]。