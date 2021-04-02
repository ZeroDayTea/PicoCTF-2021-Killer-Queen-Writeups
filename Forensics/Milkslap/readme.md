# Milkslap

**Description**

🥛

**Problem**

There is a flag somewhere on this website: http://mercury.picoctf.net:58537/. I would like it.

**Hints** 

Look at the problem category

**Solution**

The website consists of a gif with a man getting milk spilled on him. Since the hint references the problem category, which is forensics, we should find the image.
Going to the source and then the css, we find that the image the image is at the url `http://mercury.picoctf.net:58537/concat_v.png`

The image is a 1280x47520 png. This is probably where the flag is. Downloading the image, we can now run various forensics programs on it. Steghide needs a password, so it isn't that.
Binwalk finds nothing out of the ordinary. The program zsteg does find something though:

```
manifold@pwnmach1n3:~$ zsteg concat_v.png
imagedata           .. file: dBase III DBT, version number 0, next free block index 3368931841, 1st item "\001\001\001\001"
b1,b,lsb,xy         .. text: "picoCTF{imag3_m4n1pul4t10n_sl4p5}\n"
b1,bgr,lsb,xy       .. <wbStego size=9706075, data="\xB6\xAD\xB6}\xDB\xB2lR\x7F\xDF\x86\xB7c\xFC\xFF\xBF\x02Zr\x8E\xE2Z\x12\xD8q\xE5&MJ-X:\xB5\xBF\xF7\x7F\xDB\xDFI\bm\xDB\xDB\x80m\x00\x00\x00\xB6m\xDB\xDB\xB6\x00\x00\x00\xB6\xB6\x00m\xDB\x12\x12m\xDB\xDB\x00\x00\x00\x00\x00\xB6m\xDB\x00\xB6\x00\x00\x00\xDB\xB6mm\xDB\xB6\xB6\x00\x00\x00\x00\x00m\xDB", even=true, mix=true, controlbyte="[">
b2,r,lsb,xy         .. file: SoftQuad DESC or font file binary
b2,r,msb,xy         .. file: VISX image file
b2,g,lsb,xy         .. file: VISX image file
b2,g,msb,xy         .. file: SoftQuad DESC or font file binary - version 15722
b2,b,msb,xy         .. text: "UfUUUU@UUU"
b4,r,lsb,xy         .. text: "\"\"\"\"\"#4D"
b4,r,msb,xy         .. text: "wwww3333"
b4,g,lsb,xy         .. text: "wewwwwvUS"
b4,g,msb,xy         .. text: "\"\"\"\"DDDD"
b4,b,lsb,xy         .. text: "vdUeVwweDFw"
b4,b,msb,xy         .. text: "UUYYUUUUUUUU"
manifold@pwnmach1n3:~$
```

flag: `picoCTF{imag3_m4n1pul4t10n_sl4p5}`
