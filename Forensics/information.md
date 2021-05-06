# information
## Category - Forensics
## Author - SUSIE

### Description: 
Files can always be changed in a secret way. Can you find the flag? cat.jpg

### Solution:
The challenge gives us a link to download an image named "flag.jpg". Using exiftool to look at the exif data of the image in our terminal we see some interesting data under
"License".
```
zerodaytea@Patryk:/mnt/d/Coding/CTFs/PicoCTF2021/Forensics$ exiftool cat.jpg
ExifTool Version Number         : 11.88
File Name                       : cat.jpg
Directory                       : .
File Size                       : 858 kB
File Modification Date/Time     : 2021:03:16 10:37:17-06:00
File Access Date/Time           : 2021:04:22 15:09:49-06:00
File Inode Change Date/Time     : 2021:03:16 10:46:32-06:00
File Permissions                : rwxrwxrwx
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.02
Resolution Unit                 : None
X Resolution                    : 1
Y Resolution                    : 1
Current IPTC Digest             : 7a78f3d9cfb1ce42ab5a3aa30573d617
Copyright Notice                : PicoCTF
Application Record Version      : 4
XMP Toolkit                     : Image::ExifTool 10.80
License                         : cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9
Rights                          : PicoCTF
Image Width                     : 2560
Image Height                    : 1598
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 2560x1598
Megapixels                      : 4.1
```
As this string of characters look like base64 we base64 decode it using either an online tool such as https://www.base64decode.org/ or using the terminal by outputting 
the string and piping it into the base64 tool with the parameter "--decode" as such:
```
zerodaytea@Patryk:/mnt/d/Coding/CTFs/PicoCTF2021/Forensics$ echo "cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9" | base64 --decode
picoCTF{the_m3tadata_1s_modified}
```

### Flag:
```
picoCTF{the_m3tadata_1s_modified}
```
