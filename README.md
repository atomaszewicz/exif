# Exif?
Exchangeable Image Format (Exif) is a standard for image files that specifies how to format the image's metadata. This metadata describes the photo and how it was taken: did you use flash? what was your shutter speed? what is the image's resolution? "Exif" is often used to refer to the metadata itself and will be for this project.

## Terminology
Here are some definitions of terms that will come up in this project: 

**ISO**: The camera's sensitivity to light. The higher the number, the more sensitive. <br />
**Shutter Speed**: The amount of time the camera allows light in for. Usually measured in fractions of a second. <br />
**Focal Length**: A measure of the field-of-view (FOV) and maginification of a camera lens. Usually measured in mm, a larger focal length means a smallers FOV but larger magnification. <br />
**Aperture**: The size of the diaphragm that the light travels through in the lens. Often indicated with f/x (where x is a number (0,100)), or "f-stop". Higher numbers mean a smaller hole. When you talk about a lens, you generally say it's lowest aperture. <br />
**Equivalent Focal Length**: My camera has a 2/3 size sensor, which ends up making the focal length 3/2 times as big. Thus the 18-135mm lens, when used on my camera, is the equivalent of a 27-202.5mm lens.

# Outline
Investigating the EXIF metadata of the photos I have taken with my Nikon D80, with a kit lens of focal length 18-135mm with aperture f/3.5 at 18-69mm and f/5.6 at 70-135mm. The purpose of this project is to study my style of photography, and investigate what camera/lens I should purchase next.

# Data
To begin, I chose a 5 month period (Jan-May 2016) wherein I took ~2500 photos. This decision was made because in June 2016 I purchased an old manual 50mm lens which didn't log certain aspects of the Exif data.

It is simple to view an individual image's Exif data (Windows: Right Click -> Properties -> Details) but less so for a couple thousand images. After looking online, I found Phil Harvey's ExifTool (http://www.sno.phy.queensu.ca/~phil/exiftool/). Using this program, I exported the Exif of my photos into a CSV, which I then cleaned and studied.

# Data Cleaning
Sifting through the exported CSV's columns in Excel, I made an new Excel spreadsheet with just the relevant data.

# Analysis
Analyzing the new spreadsheet in R Studio, I studied aspects of the Exif to learn about my style of shooting.

# Results
I shot most at aperture f/3.5, focal length equivalent 27mm, ISO 200, and a shutter speed 1/200 seconds. The aperture and focal length are both the lens' lowest, so this means that I would often shoot without adjusting my settings. The next most used aperture was f/5.6, which makes sense as that is the lens' lowest for focal lengths above 70mm. A common rule is to ISO and shutter speed as reciprocals, a rule which I evidently follow.

# Future Improvements
To improve this project, I could bring in a much larger pool of data to work with. I would sort the photos post-June 2016 to using the 50mm lens and the kit lens, then analyze these data sets seperately.  
