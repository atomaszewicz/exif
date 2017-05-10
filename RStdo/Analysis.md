# Analyzing Exif Data with RStudio

First we set the working directory:

```R
setwd("C:/Users/Alex/Documents/Data/Camera")
```

Then we load a package to handle Excel files (since I saved my cleaned-up Exif CSV as an Excel ".xlsx" file)

```R
load.packages("xlsx") 
require("xlsx")
 ```
 
 We also load our favorite graph-creating package so that we can plot our data.
 
 ```R
install.packages("ggplot2")
require("ggplot2")
```

Then we load our file into a data frame for R Studio, calling it 'exif', and working with the 1st (and only) page of the xlsx

```R
exif<-read.xlsx("exif.xlsx",1)
```

## Mode
Since R doesn't have a built-in function to find the mode of a dataset, we find a clever, terse version online and impliment it:

```R
Mode <- function(x) {
     ux <- unique(x)
     ux[which.max(tabulate(match(x, ux)))]
}
 ```
 
 Then we study the mode of our columns of interest, and we might as well create a data frame of the modes while we're at it:
 
 ```R
mode<-data.frame()

for(i in 1:4){
   mode[i,1]<-colnames(exif[i])
   mode[i,2]<-Mode(exif[[i]])   
}

colnames(mode)<-c("Feature","Mode")
 ```
 We end up with a data frame that looks roughly like this:

|Feature|Mode|
|-------|----|
|ISO|200|
|Shutter Speed|0.005|
|Aperture|3.5|
|Focal Length|27|

ISO-200 is quite low (my camera's ISO range is 100-10,000). I know that I mostly shoot in the day time, which this number reinforces. 

A shutter speed of 1/200 s is relatively slow, this agrees with what I know: that I mostly shoot still life, and rarely things like sports.

Having used my lens' largest aperture, f/3.5, the most means that I like to have a lot of light in my scene, but not a lot in focus (i.e. isolating the subject with the focus).

As mentioned, shooting at lower focal lengths means that the scene is less magnified, and you have a larger FOV. Since I shoot most at my lens' lowest focal length, this could indicate that I like capturing large scenes.

There is a rule-of-thumb that says having your shutter speed as the inverse of your ISO is a good way to properly expose (neither overexpose nor underexpose) your image. The modes for these are 1/200s (0.005s) and 200 respectively. This implies that I follow this rule, conciously or not.

## Aperture

Let's find the largest and smallest apertures that I shot with:

```R
min(exif$Aperture)
[1] 3.5
max(exif$Aperture)
[1] 36
NROW(c(subset(exif$Aperture,Aperture=36)))
[1] 1
```
The largest aperture I used was f/3.5, my camera's largest, and smallest used was f/36, it's smallest, with only one such occurance. Anything larger than f/11 is seen as 'large', and smaller 'small'. I think that I shoot mostly 'large', since I like bright scenes and to have less in focus i.e. isolate the subject.

```R
NROW(c(subset(exif$Aperture,Aperture<=11)))/NROW(exif)
[1] 0.855
```
This agrees with my presumption, I shoot larger than or equal to f/11 a total of 85.5% of the time. Further, larger than f/5.6 is seen as 'very large' and I would say I shoot in this category a lot.

```R
NROW(c(subset(exif$Aperture,Aperture<=5.6)))/NROW(exif)
[1] 0.437
```
So nearly half my shots (43.7%) are in the 'very large' aperture category! As mentioned above, I know that I shoot mostly with a large aperture, but i didn't know it was this extreme! 

Let's make a graph of this data:

```R
#We choose custom line breaks to help emphasize our mode, and make range (0,30) even though there is a data point at 33 to increase resolution
ap<-ggplot(exif,aes(Aperture))+geom_bar()
labs<-ylab("Counts")+,limits=c(3,30))+ggtitle("Aperture Usage*",subtitle="18-135mm f/3.5-5.6 Nikkor Lens, Nikon D80")+labs(caption="*2500 shots (Jan-May 2016)")
scale<-scale_x_continuous(breaks=c(3.5,5,10,15,20,25,30)
```
![Aperture Plot](https://github.com/atomaszewicz/exif/blob/master/RStdo/Plots/aperture.png?raw=TRUE)

## Shutter Speed

First, what is the fastest shutter speed I used?

```R
min(exif$Shutter.Speed)
[1]0.00025
```
So fastest is 0.00025s (1/4000 s), which is the quickest my camera can go.

Next, the slowest shutter speed:

```R
max(exif$Shutter.Speed)
[1] 1.1
```
1.1s is a ways from the 30s maximum of my camera, but since I rarely take long exposures, this comes as no surprise. Even slower than 1/10s will likely be blurry without a tripod (which I don't own) or a nice flat surface. Let's see how often I shot this slow:

```R
#First we see how many times I took a shot longer than 1/10s
NROW(c(subset(exif$Shutter.Speed,Shutter.Speed>0.1)))
[1] 143
#Then we find how often this happened, as a fraction of total shots
NROW(c(subset(exif$Shutter.Speed,Shutter.Speed>0.1)))/NROW(exif)
[1] 0.058
```

So I only used a shutter speed of slower than 1/10s 5.8% of the time, a bit more often than I expected. In hindsight, long exposures are quite difficult, and often take many attempts, so though I didn't have many sessions, for each one I would take many photos.

Graphing Shutter Speed:

```R
#Note that we again use custom breaks to increase visualization (and adjust them using the 'theme' environment so they don't overlap)
#We chose a bincount of 1/2000s as any smaller lead to poor aesthetic quality, and any bigger lost the importance of the data
#We cut off anything about 1/4s due to increase resolution (since longer shutter speeds than 1/4s were used rarely (1.5%))

ss<-ggplot(exif,aes(Shutter.Speed))+geom_histogram(binwidth=0.0005)
labs<-ggtitle("Shutter Speed Usage*",subtitle="Nikon D80")+xlab("Shutter Speed[seconds]**")+ylab("Counts")+labs(caption=" *2500 shots (Jan-May 2016) \n **1/2000 second Bin 
scale<-scale_x_continuous(limits=c(0,0.26),breaks=c(0.001,0.005,0.01,0.05,0.1,0.25),labels=c("1/1000","1/200","1/100","1/20","1/10","1/4"))Size")
x_axis<-theme(axis.text.x=element_text(angle=90,vjust=c(-0.3,0.4,0.9,0.4,0.4,0.4)))
```
![Shutter Speed Plot](https://github.com/atomaszewicz/exif/blob/master/RStdo/Plots/shutterspeed.png?raw=TRUE)

## Focal Length

We verify that the longest and shortest focal lengths are the same as the lens':

```R
max(exif$Focal.Length)
[1]202 
min(exif$Focal.Length)
[1]27
```
They are. How often did I shoot at the mode focal length of 27mm:

```R
NROW(c(subset(exif$Focal.Length,Focal.Length==27)))/NROW(exif)
[1] 0.517101
```

51.7% of the time! This is quite an interesting result. This fits in with my knowledge that I photograph many large scenes, which will require large field of views (FOV) and thus, short focal lengths. Let's see how often I shoot at the lens' 3 shortest focal lengths:

```R 
#First we find the 3 shortest focal lengths
s1<-min(exif$Focal.Length)
s2<-min(c(subset(exif$Focal.Length,Focal.Length!=s1)))
s3<-min(c(subset(exif$Focal.Length,Focal.Length!=s1&Focal.Length!=s2)))
#Now we print these values, using 'cat()' a stripped-down version of 'print()'
cat(s2,s3)
30 33
#Now we find the ratio of times we shot at these 3 focal lengths to all focal lengths
ss<-c(subset(exif$Focal.Length,Focal.Length==s1|Focal.Length==s2|Focal.Length==s3))
NROW(ss)/NROW(exif)
[1]0.6750814
```
So we shot at the 3 shortest focal lengths over two thirds of the time (67.5%).



To investiage this suprising result, let's first see what the next few modes are:

```R
#Finding mode 1 (m1) from our table of modes
m1<-subset(mode$Mode,mode$Feature=="Focal.Length")
#m2 is the mode, ignoring all of m1 values
m2<-Mode(c(subset(exif$Focal.Length,Focal.Length!=m1)))
print(m2)
[1] 30
#m3 is the mode ignoring m2 and m1
m3<-Mode(c(subset(exif$Focal.Length,Focal.Length!=m1&Focal.Length!=m2)))
print(m3)
[1] 33
```

We find mode 1 (m1) by looking in our table of modes called 'mode' under the feature "Focal Length". The second and third modes are the second and third shortest focal lengths, agreeing with my large FOV shooting style. Let's see how big the first mode is compared to the other two:

```R
#Ratio of m2 to m1
NROW(c(subset(exif$Focal.Length,Focal.Length==m2)))/NROW(c(subset(exif$Focal.Length,Focal.Length==m1)))
[1] 0.210
#Ratio of m3 to m1
NROW(c(subset(exif$Focal.Length,Focal.Length==m3)))/NROW(c(subset(exif$Focal.Length,Focal.Length==m1)))
[1] 0.095
```
So the second mode only has 21% as many occurances as the first, and the third mode, 9.5% as many. 

To see if this is significant, we explore the first few modes in the other 3 data sets and compare. 

Note: *At this point, I decide to only use the first 3 modes. I made this desicion after exploring the fourth, fifth and sixth modes of our datasets and realizing that the nature of all the features effects the later modes too strongly. You can see the graph [here](https://github.com/atomaszewicz/exif/blob/master/RStdo/Plots/6moderatio.png?raw=TRUE)*

First we create a function to display the mode ratios:

```R
#We take as unput 'x' which will be a feature (aperture, iso etc.), then find the 3 first modes, and print the ratios
m1m2m3function(x){
    m1<-Mode(x)
    m2<-Mode(c(subset(x,x!=m1)))
    cat("m2/m1:", NROW(c(subset(x,x==m2)))/NROW(c(subset(x,x==m1))), "\n")
    m3<-Mode(c(subset(x,x!=m1&x!=m2)))
    cat("m3/m1:", NROW(c(subset(x,x==m3)))/NROW(c(subset(x,x==m1))))
}
```
We use 'm2/m1' to signify the ratio of occurances of the second mode to the first, not the ratio of the modes numerical value. For example, the function gives output as this for the aperture mode ratios:
```R
m1m2m3(Aperture)
m2/m1: 0.646
m3/m1: 0.522
```
So there are 65% as many occurances of m2 as m1, and 52% as many occurances of m3 as m1:


Let's put all the mode ratio data into a table:

|Feature|m2/m1|m3/m1|Avg.|
|------|-----|-----|---|
|Aperture|0.646|0.522|0.584|
|Shutter.Speed|0.609|0.569|0.589|
|**Focal.Length**|**0.210**|**0.095**|**0.152**|
|ISO|0.752|0.709|0.730|
|Avg. (no F.L.)|0.669|0.599|0.634|

So compared to the out features, I shot the mode focal length (27mm) WAY more than the second and third modes (and by extension, all focal lengths). Since 27mm is my lens' shortest focal length, this might imply that I just leave my lens and take the shot without adjusting. It is common to take a photo without touching the settings, review the photo on the screen, then adjust your settings accordingly, which could explain why I shot at 27mm so often, even compared to the other two shortest focal lengths.

Now, your average photographer uses focal lengths between 18-200mm. 18-35mm is seen as 'wide angle', 35-70mm as 'normal', 70-135mm as 'medium telephoto' and 135-200mm 'telephoto'. So keeping in my that the focal length range of our lens is 27-202mm, we study how often I shoot in each range. 

```R
wide<-NROW(c(subset(exif$Focal.Length,Focal.Length<=35)))/NROW(exif)
norm<-NROW(c(subset(exif$Focal.Length,Focal.Length>35&Focal.Length<=70)))/NROW(exif)
mtele<-NROW(c(subset(exif$Focal.Length,Focal.Length>70&Focla.length<=135)))/NROW(exif)
tele<-NROW(c(subset(exif$Focal.Length,Focal.Length>135)))/NROW(exif)
```
Where our variables represent the fraction of shots in that category: wide, normal, medium telephoto and telephoto. Let's visualize this. We begin by making a data frame with this data:

```R
 style<-data.frame(Range=c("Wide","Normal","Med.Tele","Telephoto"),Fraction=c(wide,norm,mtele,tele))
```
First we look at the numbers in a table:

|Range|Fraction| 
|---|---|
|Wide|0.675|
|Normal|0.221|
|Med.Tele|0.091|
|Telephoto|0.013|

We see that I shot progressively less the longer the focal length.

Next we visualize with a pie chart:

```R
#We create a bar chart then turn it into a pie chart, creating custom breaks to help visualize the slices of pie
bar<-ggplot(style,aes(x="",y=Fraction,fill=Range))+geom_bar(width=1,stat="identity")
changes<-scale_y_continuous(breaks=(NULL),labels=(""))+xlab("")+ylab("")
pie<-bar+changes+coord_polar(theta="y",start=0)
```
![Range Pie Chart](https://github.com/atomaszewicz/exif/blob/master/RStdo/Plots/range_pie_nolab.png?raw=TRUE)

Now we plot a histogram of focal length:

```R
fl<-ggplot(exif,aes(Focal.Length))+geom_bar()
scale<-scale_x_continuous(breaks=c(27,40,60,80,100,120,140,160,180,200,400))
labs<-xlab("Focal Length (Equivalent)")+ ylab("Counts")+labs(caption="*2500 shots (Jan-May 2016)")ggtitle("Focal Length Usage*",subtitle="27-202mm (Equivalent) Nikkor Lens on Nikon D80")
```

![Focal Length plot](https://github.com/atomaszewicz/exif/blob/master/RStdo/Plots/focal%20length.png?raw=TRUE)


## ISO

Next I study my usage of ISO. Firstly, I know that I rarely shoot above ISO-3200, since my decade-old camera doesn't perform well above this ISO value.

```R
NROW(c(subset(exif$ISO,ISO>3200)))
[1] 0
```
There are no such rows, as expected.

Next I know that I shoot mostly in the day time, wherein one usually does not need to exceed ISO-500.

```R
NROW(c(subset(exif$ISO,ISO<=500)))/NROW(exif)
[1] 0.52891
```
This 52.9% is a little lower than I expected, so maybe, though I usually shoot in the day time, I photograph low-light scenes (which require a higher sensitivity to light i.e. higher ISO)

Now we visualize the ISO data:

```R
iso<-ggplot(exif,aes(ISO))+geom_bar()+ylab("Counts")
scale<-scale_x_continuous(breaks=c(0,500,1000,1500,2000,2500,3000))
labs<-ggtitle("ISO Usage*",subtitle="Nikon D80")+labs(caption="*2500 shots (Jan-May 2016)")\
```
![ISO Plot](https://github.com/atomaszewicz/exif/blob/master/RStdo/Plots/iso.png?raw=TRUE)
