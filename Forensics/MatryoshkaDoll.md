# Matryoshka Doll
## Category - Forensics
## Author - SUSIE/PANDU

### Description: 
Matryoshka dolls are a set of wooden dolls of decreasing size placed one inside another. What's the final one? Image: this

### Solution:
The challenge gives us a link to download an image named dolls.jpg. Taking a hint from the challenge name of "Matryoshka Doll" we can assume there are hidden files inside this
file. To extract them we use binwalk as such.
```
zerodaytea@Patryk:/mnt/d/Coding/CTFs/PicoCTF2021/Forensics/MatryoshkaDoll$ binwalk -e dolls.jpg

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 594 x 1104, 8-bit/color RGBA, non-interlaced
3226          0xC9A           TIFF image data, big-endian, offset of first image directory: 8
272492        0x4286C         Zip archive data, at least v2.0 to extract, compressed size: 378955, uncompressed size: 383936, name: base_images/2_c.jpg
651613        0x9F15D         End of Zip archive, footer length: 22
```
We see a directory named "base_images" that we head into and find another image file named "2_c.jpg". 
```
zerodaytea@Patryk:/mnt/d/Coding/CTFs/PicoCTF2021/Forensics/MatryoshkaDoll$ cd _dolls.jpg.extracted/
zerodaytea@Patryk:/mnt/d/Coding/CTFs/PicoCTF2021/Forensics/MatryoshkaDoll/_dolls.jpg.extracted$ ls
4286C.zip  base_images
zerodaytea@Patryk:/mnt/d/Coding/CTFs/PicoCTF2021/Forensics/MatryoshkaDoll/_dolls.jpg.extracted$ cd base_images/
zerodaytea@Patryk:/mnt/d/Coding/CTFs/PicoCTF2021/Forensics/MatryoshkaDoll/_dolls.jpg.extracted/base_images$ ls
2_c.jpg
```
We try binwalk again to extract any hidden files from this image as such and change our working directory to that of the extracted files:
```
zerodaytea@Patryk:/mnt/d/Coding/CTFs/PicoCTF2021/Forensics/MatryoshkaDoll/_dolls.jpg.extracted/base_images$ binwalk -e 2_c.jpg

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 526 x 1106, 8-bit/color RGBA, non-interlaced
3226          0xC9A           TIFF image data, big-endian, offset of first image directory: 8
187707        0x2DD3B         Zip archive data, at least v2.0 to extract, compressed size: 196041, uncompressed size: 201443, name: base_images/3_c.jpg
383803        0x5DB3B         End of Zip archive, footer length: 22
383914        0x5DBAA         End of Zip archive, footer length: 22

zerodaytea@Patryk:/mnt/d/Coding/CTFs/PicoCTF2021/Forensics/MatryoshkaDoll/_dolls.jpg.extracted/base_images$ ls
2_c.jpg  _2_c.jpg.extracted
zerodaytea@Patryk:/mnt/d/Coding/CTFs/PicoCTF2021/Forensics/MatryoshkaDoll/_dolls.jpg.extracted/base_images$ cd _2_c.jpg.extracted/
zerodaytea@Patryk:/mnt/d/Coding/CTFs/PicoCTF2021/Forensics/MatryoshkaDoll/_dolls.jpg.extracted/base_images/_2_c.jpg.extracted$ ls
2DD3B.zip  base_images
```
Again we head to the base_images directory and see another image file named "3_c.jpg" on which we use binwalk again to extract more file and finally change our working
directory to that of the extracted files:
```
zerodaytea@Patryk:/mnt/d/Coding/CTFs/PicoCTF2021/Forensics/MatryoshkaDoll/_dolls.jpg.extracted/base_images/_2_c.jpg.extracted$ cd base_images/
zerodaytea@Patryk:/mnt/d/Coding/CTFs/PicoCTF2021/Forensics/MatryoshkaDoll/_dolls.jpg.extracted/base_images/_2_c.jpg.extracted/base_images$ ls
3_c.jpg
zerodaytea@Patryk:/mnt/d/Coding/CTFs/PicoCTF2021/Forensics/MatryoshkaDoll/_dolls.jpg.extracted/base_images/_2_c.jpg.extracted/base_images$ binwalk -e 3_c.jpg

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 428 x 1104, 8-bit/color RGBA, non-interlaced
3226          0xC9A           TIFF image data, big-endian, offset of first image directory: 8
123606        0x1E2D6         Zip archive data, at least v2.0 to extract, compressed size: 77649, uncompressed size: 79806, name: base_images/4_c.jpg
201421        0x312CD         End of Zip archive, footer length: 22

zerodaytea@Patryk:/mnt/d/Coding/CTFs/PicoCTF2021/Forensics/MatryoshkaDoll/_dolls.jpg.extracted/base_images/_2_c.jpg.extracted/base_images$ ls
3_c.jpg  _3_c.jpg.extracted
zerodaytea@Patryk:/mnt/d/Coding/CTFs/PicoCTF2021/Forensics/MatryoshkaDoll/_dolls.jpg.extracted/base_images/_2_c.jpg.extracted/base_images$ cd _3_c.jpg.extracted/
zerodaytea@Patryk:/mnt/d/Coding/CTFs/PicoCTF2021/Forensics/MatryoshkaDoll/_dolls.jpg.extracted/base_images/_2_c.jpg.extracted/base_images/_3_c.jpg.extracted$
```
We are given another "base_images" directory containing yet another image file named "4_c.jpg". Using binwalk on this file we extract the flag.txt file.
```
zerodaytea@Patryk:/mnt/d/Coding/CTFs/PicoCTF2021/Forensics/MatryoshkaDoll/_dolls.jpg.extracted/base_images/_2_c.jpg.extracted/base_images/_3_c.jpg.extracted$ cd base_images/
zerodaytea@Patryk:/mnt/d/Coding/CTFs/PicoCTF2021/Forensics/MatryoshkaDoll/_dolls.jpg.extracted/base_images/_2_c.jpg.extracted/base_images/_3_c.jpg.extracted/base_images$ ls
4_c.jpg
zerodaytea@Patryk:/mnt/d/Coding/CTFs/PicoCTF2021/Forensics/MatryoshkaDoll/_dolls.jpg.extracted/base_images/_2_c.jpg.extracted/base_images/_3_c.jpg.extracted/base_images$ binwalk -e 4_c.jpg

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 320 x 768, 8-bit/color RGBA, non-interlaced
3226          0xC9A           TIFF image data, big-endian, offset of first image directory: 8
79578         0x136DA         Zip archive data, at least v2.0 to extract, compressed size: 62, uncompressed size: 81, name: flag.txt
79784         0x137A8         End of Zip archive, footer length: 22

zerodaytea@Patryk:/mnt/d/Coding/CTFs/PicoCTF2021/Forensics/MatryoshkaDoll/_dolls.jpg.extracted/base_images/_2_c.jpg.extracted/base_images/_3_c.jpg.extracted/base_images$ ls
4_c.jpg  _4_c.jpg.extracted
zerodaytea@Patryk:/mnt/d/Coding/CTFs/PicoCTF2021/Forensics/MatryoshkaDoll/_dolls.jpg.extracted/base_images/_2_c.jpg.extracted/base_images/_3_c.jpg.extracted/base_images$ cd _4_c.jpg.extracted/
zerodaytea@Patryk:/mnt/d/Coding/CTFs/PicoCTF2021/Forensics/MatryoshkaDoll/_dolls.jpg.extracted/base_images/_2_c.jpg.extracted/base_images/_3_c.jpg.extracted/base_images/_4_c.jpg.extracted$ ls
136DA.zip  flag.txt
zerodaytea@Patryk:/mnt/d/Coding/CTFs/PicoCTF2021/Forensics/MatryoshkaDoll/_dolls.jpg.extracted/base_images/_2_c.jpg.extracted/base_images/_3_c.jpg.extracted/base_images/_4_c.jpg.extracted$ cat flag.txt
picoCTF{ac0072c423ee13bfc0b166af72e25b61}
```
Truly a Matryoshka-like situation.

### Flag:
```
picoCTF{ac0072c423ee13bfc0b166af72e25b61}
```
