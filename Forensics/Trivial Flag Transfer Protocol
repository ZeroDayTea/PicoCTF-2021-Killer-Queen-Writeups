# Trivial Flag Transfer Protocol
## Category - Forensics
## Author - DANNY

### Description
Figure out how they moved the flag.

**Hints** 
What are some other ways to hide data?

**SOLUTION**

Searching on wikipedia, we see that TFTP is a protocol for transferring files. We open the pcap in wireshark and extract the files with TFTP. 
There are 5 files. Saving them all and looking at them, there are 2 text files and 3 bmp files.

bmp is a lossless and uncompressed format, so we will likely find the flag there. 

A .deb file is an installation file, which 7zip can open, for some reason. Inside, we find archive named data.tar.
We can open this with `tar -xvf data.tar`. This extracts a directory. Searching through it we find a folder `usr/share/doc/steghide`. The flag is likely encrypted in one of the bmps with the steghide program, which needs a password. We are getting closer.

Instructions.txt and plan are both text files with a bunch of letters that are all capitals. This could potentially a cipher, the first one that came to mind being a caesar cipher. Using a caesar cipher solver, we get these 2 messages from the files:

Instructions.txt: `TFTPDOESNTENCRYPTOURTRAFFICSOWEMUSTDISGUISEOURFLAGTRANSFER.FIGUREOUTAWAYTOHIDETHEFLAGANDIWILLCHECKBACKFORTHEPLAN`

plan: `IUSEDTHEPROGRAMANDHIDITWITH-DUEDILIGENCE.CHECKOUTTHEPHOTOS`

Interestingly, the offset for both of the ciphers is +13, which in hindsight should have been trivial because it is also ROT13.

The author of the plan used "the program", likely referring to steghide, with the password `DUEDILIGENCE`. We now have everything we need to find the flag.

```
manifold@pwnmachine:~$ steghide extract -sf picture1.bmp -p DUEDILIGENCE
steghide: could not extract any data with that passphrase!
manifold@pwnmachine:~$ steghide extract -sf picture2.bmp -p DUEDILIGENCE
steghide: could not extract any data with that passphrase!
manifold@pwnmachine:~$ steghide extract -sf picture3.bmp -p DUEDILIGENCE
wrote extracted data to "flag.txt".
manifold@pwnmachine:~$ cat flag.txt
picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}
manifold@pwnmachine:~$
```

Flag: `picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}`
