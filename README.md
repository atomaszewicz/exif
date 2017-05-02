# Exif?
Exchangeable Image Format (Exif) is a standard for image files that specifies how to format the image's metadata. This metadata describes the photo and how it was taken: did you use flash? what was your shutter speed? what is the image's resolution? "Exif" is often used to refer to the metadata itself and will be for this project.

# Outline
Investigating the EXIF metadata of the photos I have taken with my Nikon D80, with a 18-135mm f/3.5-5.6 kit lens. The purpose of this project is to study my style of photography, and investigate what camera/lens I should purchase next.

# Data
To begin, I chose a 5 month period (Jan-May 2016) wherein I took ~2500 photos. This decision was made because in June 2016 I purchased an old manual 50mm lens which didn't log certain aspects of the Exif data.

It is simple to view an individual image's Exif data (Windows: Right Click -> Properties -> Details) but less so for a couple thousand images. After looking online, I found Phil Harvey's ExifTool (http://www.sno.phy.queensu.ca/~phil/exiftool/). This program attracted me because it featured a command-line option, you can ouput Exif to a CSV, and it supported many file types.

# ExifTool
Using this program was very simple: Open command prompt, navigate to the program's folder and with one line create the CSV:
```exiftool -csv -r C:\Users\Alex\Pictures\D80 >exif.csv```
The `-csv` option is specifying the output, `-r` is to go recursively through the sub-folders in my photography folder `C:\Users\Alex\Pictures\D80` is my photography folder and `exif.csv` is the output file.


# Future Improvements
To improve this project, I could bring in a much larger pool of data to work with. I would sort the photos post-June 2016 to using the 50mm lens and the kit lens, then analyze these data sets seperately.  
