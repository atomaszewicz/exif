# Exif?
Exchangeable Image Format (Exif) is a standard for image files that specifies how to format the image's metadata. This metadata describes the photo and how it was taken: did you use flash? what was your shutter speed? what is the image's resolution? "Exif" is often used to refer to the metadata itself and will be for this project.

## Terminology
Here are some definitions of terms that will come up in this project:

**ISO**: The camera's sensitivity to light. The higher the number, the more sensitive. My camera has an ISO range of 100-10,000. <br />
**Shutter Speed**: The amount of time the camera allows light in for. Measure in seconds and my camera can shoot from 1/4000s-30s  <br />
**Focal Length**: A measure of the field-of-view (FOV) and maginification of a camera lens. Usually measured in mm, a larger focal length means a smallers FOV but larger magnification. Focal lengths generally range from 18mm-200mm, with standard sizes being 35mm and 50mm. <br />
**Equivalent Focal Length**: My camera has a 2/3 size sensor, which ends up making the focal length 3/2 times as big. Thus the 18-135mm zoom lens, when used on my camera, is the equivalent of a 27-202.5mm lens. <br />
**Aperture**: The size of the diaphragm that the light travels through in the lens. This ends up translating into how much of the scene is in focus. Higher numbers mean a smaller hole, and more in focus. When you detail a lens, you generally say it's largest aperture (smallest number). Aperture is also called "f-stop" or indicated by f/x, where x as a number (usually between 1.4 and 64). 

# Outline
Investigating the EXIF metadata of the photos I have taken with my Nikon D80, with a kit lens of focal length 18-135mm with a largest aperture of f/3.5-5.6, depending on the focal length. The purpose of this project is to study my style of photography, and investigate what camera/lens I should purchase next.

# Data
To begin, I chose a 5 month period (Jan-May 2016) wherein I took ~2500 photos. This decision was made because in June 2016 I purchased an old manual 50mm lens which didn't log certain aspects of the Exif data.

It is simple to view an individual image's Exif data (Windows: Right Click -> Properties -> Details) but less so for a couple thousand images. After looking online, I found Phil Harvey's ExifTool (http://www.sno.phy.queensu.ca/~phil/exiftool/). Using this program, I exported the Exif of my photos into a CSV, which I then cleaned and studied. Sifting through the exported CSV's columns in Excel, I made an new Excel spreadsheet (.xlsx filetype) with just the relevant data. In this new spreadsheet, I have changed the focal length to equivalent focal length.

# Analysis
Analyzing the new spreadsheet in R Studio, I studied aspects of the Exif to learn about my style of shooting.

# Results
I shot most at aperture f/3.5, focal length equivalent 27mm, ISO 200, and a shutter speed 1/200 seconds. 

The aperture is the lens' largest and focal length is the lens' smallest, so this means that I would often shoot without adjusting the lens. One could interpret this as meaning that I either am impatient in shooting and/or shoot things on-the-fly. A common rule is to ISO and shutter speed as reciprocals, a rule which I evidently follow.

As mentioned, shooting at lower focal lengths means that the scene is less magnified, and you have a larger FOV. Since I shoot most at my lens' lowest focal length, this could indicate that I like capturing large scenes.

Having used f/3.5, my lens' largest aperture the most (and even my 2nd most used aperture was f/5.6, which is the lens' largest aperture for focal lengths above 70mm) means that I like to have a lot of light in my scene, but not a lot in focus. The later point implies that I like isolating one subject to have in focus.





# Future Improvements
To improve this project, I could bring in a much larger pool of data to work with. To accomplish this I would sort the photos post-June 2016 to using the 50mm lens and the kit lens, then analyze these data sets seperately. I could also analyze the time of day that I take pictures at the most (I did not do this due to some mis-calibrated dates-and-times data)
