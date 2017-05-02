# Exporting Data using ExifTool

I decided to export the data as a CSV so that I could look at it in Excel before diving in with R.

Using this program was very simple: Open command prompt, navigate to the program's folder and with one line create the CSV:
```exiftool -csv -r C:\Users\Alex\Pictures\D80 >exif.csv```

The `-csv` option is specifying the output, `-r` is to go recursively through the sub-folders in my photography folder, `C:\Users\Alex\Pictures\D80` is my photography folder, and `exif.csv` is the output file.

We now have our CSV, and can manipulate it with our program/language of choice.
