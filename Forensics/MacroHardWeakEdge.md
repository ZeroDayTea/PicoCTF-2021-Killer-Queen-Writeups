# MacroHard WeakEdge
## Category - Forensics
## Author - MADSTACKS

### Description: 
I've hidden a flag in this file. Can you find it? Forensics is fun.pptm

### Solution:

We run `binwalk -e 'Forensics is fun.pptm'` This spits out a directory. Running `tree` on this directory, we see that there is a file named `hidden` at `_Forensics is fun.pptm.extracted/ppt/slideMasters/hidden`
Navigating to there and reading it, it is a string of letters seperated by spaces: `Z m x h Z z o g c G l j b 0 N U R n t E M W R f d V 9 r b j B 3 X 3 B w d H N f c l 9 6 M X A 1 f Q`

Removing the spaces and decoding it with base64, we get the flag:
```
manifold@pwnmach1n3:~/_Forensics is fun.pptm.extracted/ppt/slideMasters$ cat hidden | tr -d ' ' | base64 -d
flag: picoCTF{D1d_u_kn0w_ppts_r_z1p5}base64: invalid input
manifold@pwnmach1n3:~/_Forensics is fun.pptm.extracted/ppt/slideMasters$
```

flag: `picoCTF{D1d_u_kn0w_ppts_r_z1p5}`
