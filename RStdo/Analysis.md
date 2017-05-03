# Loading and Analyzing Exif Data in R Studio

First we set the working directory

```R
>setwd("C:/Users/Alex/Documents/Data/Camera")
```

Then we load a package to handle Excel files (since I saved my cleaned-up Exif CSV as an .xlsx)

```R
>load.packages("xlsx") 
```
 ```R
 >require("xlsx")
 ```

Then we load our file into a data.frame for R Studio, calling it 'exif', and working with the 1st (and only) page of the xlsx

```R
exif<-read.xlsx("exif.xlsx",1)
```

Since R doesn't have a built-in function to find the mode of a dataset, we build one ourselves:

```R
Mode <- function(x) {
     ux <- unique(x)
     ux[which.max(tabulate(match(x, ux)))]}
 ```
 
 Then we study the mode of our columns of interest, and we might as well create a data.frame while we're at it:
 
 ```R
 prop<-names(exif)
 ```
 
 ```R
 for(x in 3:6){
      print(prop[x]: Mode(exif[[x]])}
    ```
   

blah blah blah

Graphing the Aperture values:

```R
ap<-ggplot(exif,aes(Aperture))+geom_bar()+ylab("Counts")+ scale_x_continuous(breaks=c(3.5,5,10,15,20,25,30),limits=c(3,30))+ ggtitle("Aperture Usage*",subtitle="18-135mm f/3.5-5.6 Nikkor Lens, Nikon D80")+labs(caption="*2500 shots (Jan-May 2016)")
```
Graphing the ISO:

```R
iso<-ggplot(exif,aes(ISO))+geom_bar()+ylab("Counts")+ scale_x_continuous(breaks=c(0,500,1000,1500,2000,2500,3000))+          ggtitle("ISO Usage*",subtitle="Nikon D80")+ labs(caption="*2500 shots (Jan-May 2016)")\
```
Graphing the Focal Length Equivalent:

```R
fl<-ggplot(exif,aes(Focal.Length))+geom_bar()+ ggtitle("Focal Length Usage*",subtitle="27-202mm (Equivalent) Nikkor Lens on Nikon D80")+xlab("Focal Length (Equivalent)")+ ylab("Counts")+scale_x_continuous(breaks=c(27,40,60,80,100,120,140,160,180,200,400))+ labs(caption="*2500 shots (Jan-May 2016)")
```
Graphing Shutter Speed:

```R
ss<-ggplot(exif,aes(Shutter.Speed))+geom_histogram(binwidth=0.0005)+ggtitle("Shutter Speed Usage*",subtitle="Nikon D80")+   xlab("Shutter Speed [seconds]**")+ylab("Counts")+      scale_x_continuous(limits=c(0,0.26),breaks=c(0.001,0.005,0.01,0.05,0.1,0.25),labels=c("1/1000","1/200","1/100","1/20","1/10","1/4"))+ labs(caption=" *2500 shots (Jan-May 2016) \n **1/2000 second Bin Size")+ theme(axis.text.x=element_text(angle=90,vjust=c(-0.3,0.4,0.9,0.4,0.4,0.4)))
```
Noting that we cut off anything about 1/4s due to (A) Few data points about 1/4s and (B) To improve readibility and resolution of region with most data.
