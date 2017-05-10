# Exif?
Exchangeable Image Format (Exif) is a standard for image files that specifies how to format the image's metadata. This metadata describes the photo and how it was taken: did you use flash? what was your shutter speed? what is the image's resolution? "Exif" is often used to refer to the metadata itself and will be for this project.

## Terminology
Here are some definitions of terms that will come up in this project:

**ISO**: The camera's sensitivity to light. The higher the number, the more sensitive. If a scene is dark, one needs to shoot at a high ISO, in broad day, lower ISO will suffice. My camera has an ISO range of 100-10,000. <br />
**Shutter Speed**: The amount of time the camera allows light in for , it is measured in seconds. Faster shutter speeds (thousandths of a second) are used when capturing quickly moving things, and used for things like sports. Longer shutter speeds (upwards of a quarter of a second) are usually used for long exposures, such as for night sky. My camera can take exposures between 1/4000s-30s.  <br />
**Focal Length**: A measure of the field of view (FOV) and maginification of a camera lens. Usually measured in mm, a larger focal length means a smallers FOV but larger magnification. Focal lengths generally range from 18mm-200mm, with standard sizes being 35mm and 50mm. The focal lengths of a zoom lens are discrete values, not continuous. <br />
**Equivalent Focal Length**: My camera has a 2/3 size sensor, which ends up making the focal length 3/2 times as big. Thus the 18-135mm zoom lens, when used on my camera, is the equivalent of a 27-202.5mm lens. <br />
**Aperture**: The size of the diaphragm that the light travels through in the lens. This ends up translating into how much of the scene is in focus. Higher numbers mean a smaller hole, and more in focus. When you detail a lens, you generally say it's largest aperture (smallest number). Aperture is also called "f-stop" or indicated by f/x, where x as a number (usually between 1.4 and 64). Here is a picture that might help explain aperture better:

![Aperture V Aid](http://acdsystems.com/images/community/posts/aperture-Photographer-CheatSheet-Segments.jpg)

# Outline
Investigating the EXIF metadata of the photos I have taken with my Nikon D80, with a kit lens of focal length 18-135mm with a largest aperture of f/3.5-5.6, depending on the focal length. The purpose of this project is to study my style of photography, and investigate what camera/lens I should purchase next.

# Data
To begin, I chose a 5 month period (Jan-May 2016) wherein I took ~2500 photos. This decision was made because in June 2016 I purchased an old manual 50mm lens which didn't log certain aspects of the Exif data.

It is simple to view an individual image's Exif data (Windows: Right Click -> Properties -> Details) but less so for a couple thousand images. After looking online, I found Phil Harvey's ExifTool (http://www.sno.phy.queensu.ca/~phil/exiftool/). Using this program, I exported the Exif of my photos into a CSV, which I then cleaned and studied. Sifting through the exported CSV's columns in Excel, I made an new Excel spreadsheet (.xlsx filetype) with just the relevant data. In this new spreadsheet, I have changed the focal length to equivalent focal length.

# Analysis
Analyzing the new spreadsheet in R Studio, I studied aspects of the Exif to learn about my style of shooting.

# Results

|Feature|Mode|
|-------|----|
|ISO|200|
|Shutter Speed|0.005|
|Aperture|3.5|
|Focal Length|27|

We note that though my camera can go up to ISO-10,000, I never shot above ISO-3200. This is no surprise, as I know the quality of the image begins to deteriorate above ISO-3200 on my decade-old camera. Further, I took more than half (52.9%) of my photos below and including ISO-500, which figures, as I mostly shoot in the daytime.

A shutter speed of 1/200 s is relatively slow, this agrees with what I know: that I mostly shoot still life, and rarely things like sports. The fastest shutter speed I used was 1/4000s, the maximum for my camera, but the slowest was 1.1s, not quite the 30s. In fact, I rarely did anything slower than 1/4s, with only 36 such occasions (1.5% of my shots).

The mode aperture is f/3.5, my camera's largest, I shoot larger than f/5.6 almost half the time (43.7%) and I rarely shoot an aperture smaller than f/11, with this occuring on only 14.5% of my shots. So it is clear that I like large apertures, which implies that I like to have a lot of light in my scene, but not a lot in focus (i.e. isolating the subject with the focus).

As mentioned, shooting at lower focal lengths means that the scene is less magnified, and you have a larger FOV. Since I shoot most at my lens' lowest focal length, this could indicate that I like capturing large scenes.

A rule-of-thumb is to properly expose your image (neither overexpose nor underexpose) is to have your shutter speed as the reciprocal of your ISO. With the modes being 1/200s (0.05) and 200 (respectively), it is clear that I follow this rule, conciously or not.


# Future Improvements
To improve this project, I could bring in a much larger pool of data to work with. To accomplish this I would sort the photos post-June 2016 to using the 50mm lens and the kit lens, then analyze these data sets seperately. I could also analyze the time of day that I take pictures at the most (I did not do this due to some mis-calibrated dates-and-times data)
