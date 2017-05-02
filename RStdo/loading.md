# Loading the Exif Data in R Studio

First we set the working directory

```>setwd("C:/Users/Alex/Documents/Data/Camera")```

Then we load a package to handle Excel files (since I saved my cleaned-up Exif CSV as an .xlsx)

```>load.packages("xlsx") 
  >require("xlsx")```

Then we load our file into a data.frame for R Studio, calling it 'exif', and working with the 1st (and only) page of the xlsx

```exif<-read.xlsx("exif.xlsx",1)
