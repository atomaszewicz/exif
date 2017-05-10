# Exif?
Exchangeable Image Format (Exif) is a standard for image files that specifies how to format the image's metadata. This metadata describes the photo and how it was taken: did you use flash? what was your shutter speed? what is the image's resolution? "Exif" is often used to refer to the metadata itself and will be for this project.

## Terminology
Here are some definitions of terms that will come up in this project:

**ISO**: The camera's sensitivity to light. The higher the number, the more sensitive. If a scene is dark, one needs to shoot at a high ISO, in broad day, lower ISO will suffice. My camera has an ISO range of 100-10,000. <br />
**Shutter Speed**: The amount of time the camera allows light in for , it is measured in seconds. Faster shutter speeds (thousandths of a second) are used when capturing quickly moving things, and used for things like sports. Longer shutter speeds (upwards of a quarter of a second) are usually used for long exposures, such as for night sky. My camera can take exposures between 1/4000s-30s.  <br />
**Focal Length**: A measure of the field of view (FOV) and maginification of a camera lens. Usually measured in mm, a larger focal length means a smallers FOV but larger magnification. Focal lengths generally range from 18mm-200mm. Zoom lenses allow one to choose from a range (discrete, not continuous) of focal lengths, whereas a fixed focal length lens gives you only one focal length (for example, 35mm is a very popular fixed focal length for lenses).<br />
**Equivalent Focal Length**: My camera has a 2/3 sized sensor, which ends up making the focal length 3/2 times as big. Thus a 35mm lens on a 2/3 sized sensor would be the equivalent of a 52.5mm. <br/>
**Aperture**: The size of the diaphragm that the light travels through in the lens. This ends up translating into how much of the scene is in focus. Higher numbers mean a smaller hole, and more in focus. When you detail a lens, you generally say it's largest aperture (smallest number). Aperture is also called "f-stop" or indicated by f/x, where x as a number (usually between 1.4 and 64). Here is a picture that might help explain aperture better:

![Aperture V Aid](http://acdsystems.com/images/community/posts/aperture-Photographer-CheatSheet-Segments.jpg)

# Outline
In this project we investigate my style of photography by analyzing Exif data for photos i've taken. The inspiration came from trying to decide what camera and lens to buy next. We select photos on my hardrive, scrape the Exif into a CSV, and analyze in RStudio and Excel.

# Data
The data we use is from a 5 month period (Jan-May 2016) wherein I took ~2500 photos. This decision was made because during this period, I used only 1 camera and 1 lens. This helps keep a level of objectivity, as different combinations of cameras and lenses have different focal lengths, apertures, and different cameras have different shutter speeds and ISO ranges. Further, the lens I used was a zoom lens which allows an extra degree of freedom over fixed focal length lenses. 

It is simple to view an individual image's Exif data (Windows: Right Click -> Properties -> Details) but less so for a couple thousand images. After looking online, I found Phil Harvey's wonderful ExifTool (http://www.sno.phy.queensu.ca/~phil/exiftool/). Using this program, I exported the Exif of my photos into a CSV, cleaned it up, then made an Excel spreadsheet(.xlsx filetype) of just the data I was interested in studying. 

# Analysis
Analyzing the new spreadsheet in R Studio, I studied aspects of the Exif to learn about my style of shooting. See [Analysis](https://github.com/atomaszewicz/exif/edit/master/RStdo/Analysis.md) for more details.

# Results

|Feature|Mode|
|-------|----|
|Aperture|3.5|
|Shutter Speed|0.005|
|Focal Length|27|
|ISO|200|

We note that though my camera can go up to ISO-10,000, I never shot above ISO-3200. This is no surprise, as I know the quality of the image begins to deteriorate above ISO-3200 on my decade-old camera. Further, I took more than half (52.9%) of my photos below and including ISO-500, which figures, as I mostly shoot in the daytime.

The mode aperture is f/3.5, my camera's largest, I shoot between f/3.5 and f/5.6 almost half the time (43.7%) and I rarely shoot an aperture smaller than f/11, with this occuring on only 14.5% of my shots. So it is clear that I like large apertures, which implies that I like to have a lot of light in my scene, but not a lot in focus (i.e. isolating the subject with the focus).

A shutter speed of 1/200 s is relatively slow, this agrees with what I know: that I mostly shoot still life, and rarely things like sports. The fastest shutter speed I used was 1/4000s, the maximum for my camera, but the slowest was 1.1s, not quite the 30s. In fact, I rarely did anything slower than 1/4s, with only 36 such occasions (1.5% of my shots).


As mentioned, shooting at lower focal lengths means that the scene is less magnified, and you have a larger FOV. Since I shoot most at my lens' lowest focal length, this could indicate that I like capturing large scenes.

A rule-of-thumb is to properly expose your image (neither overexpose nor underexpose) is to have your shutter speed as the reciprocal of your ISO. With the modes being 1/200s (0.05) and 200 (respectively), it is clear that I follow this rule, conciously or not.


# Future Improvements
To improve this project, I could study the Exif data of the 2 old lenses i bought after selling my zoom. I might even think of a way to estimate the aperture (which is missing from the Exif of photos taken on the old lenses) and study that Exif alongside the zoom lens'. 

Another improvement would be to fix the date-and-time data in order to analyze what day-of-the-week/time-of-day I shoot at most, and then how these factors change as the seasons change and the sun is up/down at different times and the weather changes.

Lastly, as we saw in the focal length section, the focal length mode (equiv. 27mm) was used over 50% of the time. To improve this analysis, we could account for the fact that this is the base focal length by 'toning down' this the number of occurances of this focal length, which i believe would give a better representation of my shooting style, and how often I shoot in each 'Range' (see Analysis:Focal Length for more discussion).
