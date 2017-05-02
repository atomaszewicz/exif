# Exporting Data using ExifTool

Using this program was very simple: Open command prompt, navigate to the program's folder and with one line create the CSV:
```exiftool -csv -r C:\Users\Alex\Pictures\D80 >exif.csv```

The `-csv` option is specifying the output, `-r` is to go recursively through the sub-folders in my photography folder, `C:\Users\Alex\Pictures\D80` is my photography folder, and `exif.csv` is the output file.
