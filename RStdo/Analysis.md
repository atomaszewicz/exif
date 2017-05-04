# Loading and Analyzing Exif Data in R Studio

First we set the working directory

```R
setwd("C:/Users/Alex/Documents/Data/Camera")
```

Then we load a package to handle Excel files (since I saved my cleaned-up Exif CSV as an .xlsx)

```R
load.packages("xlsx") 
```
 ```R
 require("xlsx")
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
     ux[which.max(tabulate(match(x, ux)))]}
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
|Aperture|3.5|
|Shutter Speed|0.005|
|Focal Length|27|
|ISO|200|

The aperture is the lens' largest and focal length is the lens' smallest, so this means that I would often shoot without adjusting the lens. One could interpret this as meaning that I either am impatient in shooting and/or shoot things on-the-fly. A common rule is to ISO and shutter speed as reciprocals, a rule which I evidently follow.

As mentioned, shooting at lower focal lengths means that the scene is less magnified, and you have a larger FOV. Since I shoot most at my lens' lowest focal length, this could indicate that I like capturing large scenes.

Having used f/3.5, my lens' largest aperture the most (and even my 2nd most used aperture was f/5.6, which is the lens' largest aperture for focal lengths above 70mm) means that I like to have a lot of light in my scene, but not a lot in focus. The later point implies that I like isolating one subject to have in focus.

A shutter speed of 1/200 s is relatively slow, this agrees with what I know: that I mostly shoot still life, and rarely things like sports.

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
NROW(c(subset(exif$Shutter.Speed,Shutter.Speed>0.1)))
[1] 143
NROW(c(subset(exif$Shutter.Speed,Shutter.Speed>0.1)))/NROW(exif)
[1] 0.058
```

So I only used a shutter speed of slower than 1/10s 5.8% of the time, a bit more often than I expected. In hindsight, long exposures are quite difficult, and often take many attempts, so though I didn't have many sessions, for each one I would take many photos.

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
The largest aperture I used was f/3.5, my camera's largest, and smallest used was f/36, it's smallest, with only one such occurance. Further, I think that I rarely shoot below f/11, since I like bright scenes and to have less in focus i.e. isolate the subject.

```R
NROW(c(subset(exif$Aperture,Aperture<=11)))/NROW(exif)
[1] 0.855
```
This agrees with my presumption, I shoot below (inclusive) f/11 a total of 85.5% of the time.



blah blah blah

Let's visualize our data. First we will load our favorite plotting plugin:

```R
install.packages("ggplot2")
require("ggplot2")

```R
ap<-ggplot(exif,aes(Aperture))+geom_bar()+ylab("Counts")+scale_x_continuous(breaks=c(3.5,5,10,15,20,25,30),limits=c(3,30))+ggtitle("Aperture Usage*",subtitle="18-135mm f/3.5-5.6 Nikkor Lens, Nikon D80")+labs(caption="*2500 shots (Jan-May 2016)")
```
Graphing the ISO:

```R
iso<-ggplot(exif,aes(ISO))+geom_bar()+ylab("Counts")+scale_x_continuous(breaks=c(0,500,1000,1500,2000,2500,3000))+ggtitle("ISO Usage*",subtitle="Nikon D80")+labs(caption="*2500 shots (Jan-May 2016)")\
```
Graphing the Focal Length Equivalent:

```R
fl<-ggplot(exif,aes(Focal.Length))+geom_bar()+ ggtitle("Focal Length Usage*",subtitle="27-202mm (Equivalent) Nikkor Lens on Nikon D80")+xlab("Focal Length (Equivalent)")+ ylab("Counts")+scale_x_continuous(breaks=c(27,40,60,80,100,120,140,160,180,200,400))+ labs(caption="*2500 shots (Jan-May 2016)")
```
Graphing Shutter Speed:

```R
ss<-ggplot(exif,aes(Shutter.Speed))+geom_histogram(binwidth=0.0005)+ggtitle("Shutter Speed Usage*",subtitle="Nikon D80")+xlab("Shutter Speed[seconds]**")+ylab("Counts")+scale_x_continuous(limits=c(0,0.26),breaks=c(0.001,0.005,0.01,0.05,0.1,0.25),labels=c("1/1000","1/200","1/100","1/20","1/10","1/4"))+labs(caption=" *2500 shots (Jan-May 2016) \n **1/2000 second Bin Size")+theme(axis.text.x=element_text(angle=90,vjust=c(-0.3,0.4,0.9,0.4,0.4,0.4)))
```
Noting that we cut off anything about 1/4s due to (A) Few data points about 1/4s and (B) To improve readibility and resolution of region with most data.
