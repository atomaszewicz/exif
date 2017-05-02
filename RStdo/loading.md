# Loading the Exif Data in R Studio

First we set the working directory

```R
>setwd("C:/Users/Alex/Documents/Data/Camera")```

Then we load a package to handle Excel files (since I saved my cleaned-up Exif CSV as an .xlsx)

```R
>load.packages("xlsx") ``` <br />
 ```R
 >require("xlsx")```

Then we load our file into a data.frame for R Studio, calling it 'exif', and working with the 1st (and only) page of the xlsx

```R
exif<-read.xlsx("exif.xlsx",1)```

Since R doesn't have a built-in function to find the mode of a dataset, we build one ourselves:

```R
Mode <- function(x) {
     ux <- unique(x)
     ux[which.max(tabulate(match(x, ux)))]
 }```
 
 Then we study the mode of our columns of interest:
 
 ```R
 prop<-names(exif)```
 
 ```R
 for(x in 3:6){
      print(prop[x]: Mode(exif[[x]])
    }```
   



