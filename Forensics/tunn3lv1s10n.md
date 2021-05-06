# tunn3l v1s10n
## Category - Forensics
## Author - DANNY

### Description: 
We found this file. Recover the flag.

### Solution:
Seeing as the file is of an unknown file type we run exiftool on it to determine that it is a bitmap image (bmp). As the image does not display properly when we open it we figure
it must be corrupted somehow:

```
zerodaytea@Patryk:/mnt/d/Coding/CTFs/PicoCTF2021/Forensics/tunn3lv1s10n$ exiftool tunn3l_v1s10n
ExifTool Version Number         : 11.88
File Name                       : tunn3l_v1s10n
Directory                       : .
File Size                       : 2.8 MB
File Modification Date/Time     : 2021:05:05 19:55:58-06:00
File Access Date/Time           : 2021:05:05 19:56:19-06:00
File Inode Change Date/Time     : 2021:05:05 19:55:58-06:00
File Permissions                : rwxrwxrwx
File Type                       : BMP
File Type Extension             : bmp
MIME Type                       : image/bmp
BMP Version                     : Unknown (53434)
Image Width                     : 1134
Image Height                    : 306
Planes                          : 1
Bit Depth                       : 24
Compression                     : None
Image Length                    : 2893400
Pixels Per Meter X              : 5669
Pixels Per Meter Y              : 5669
Num Colors                      : Use BitDepth
Num Important Colors            : All
Red Mask                        : 0x27171a23
Green Mask                      : 0x20291b1e
Blue Mask                       : 0x1e212a1d
Alpha Mask                      : 0x311a1d26
Color Space                     : Unknown (,5%()
Rendering Intent                : Unknown (826103054)
Image Size                      : 1134x306
Megapixels                      : 0.347
```
Finding this wikipedia article about the BMP file format we step through the hex bytes of the image and modify in an attempt to fix them. To do this I would reccomend using a 
hex editor. Personally I use HexEditor Neo because it is free and I am familiar with it but any should work.
![Original Header Bytes](https://github.com/ZeroDayTea/PicoCTF-2021-Killer-Queen-Writeups/blob/main/Forensics/snip1.PNG)

As seen in the screenshot the first few bytes of the header to the bitmap image are:
```
42 4d 8e 26 2c 00 00 00 00 00 ba d0 00 00 ba d0
00 00 6e 04 00 00 32 01
```
Seeing as the number of bytes in the DIB header are wrong and the number of bits per pixel are also wrong we realize we need to edit the bytes at offset 0x0e and 0x1c. The
correct bytes are as follows:
```
42 4d 8e 26 2c 00 00 00 00 00 ba d0 00 00 28 00
00 00 6e 04 00 00 40 03
```
Changing the "ba d0" of the DIB header num-bytes to "28 00" and changing the "32 01" of the number of bits per pixel to "40 03" does the trick and we get the proper image.
Renaming the "tunn3lv1s10n" file to "tunn3lv1s10n.bmp" we are able to open it and get the flag.

![Final Image](https://github.com/ZeroDayTea/PicoCTF-2021-Killer-Queen-Writeups/blob/main/Forensics/tunn3l_v1s10n_fixed.bmp)

### Flag:
```
picoCTF{qu1t3_a_v13w_2020}
```
