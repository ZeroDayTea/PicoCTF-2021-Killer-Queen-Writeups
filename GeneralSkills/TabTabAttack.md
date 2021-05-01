# Tab, Tab, Attack
## Category - General Skills
## Author - SYREAL

### Description: 
Using tabcomplete in the Terminal will add years to your life, esp. when dealing with long rambling directory structures and filenames: Addadshashanammu.zip

### Solution:
The challenge gives us a zip file to download which we download and unzip with the command
```
zerodaytea@DESKTOP-QLQGDSV:/mnt/c/Coding/CTFs/PicoCTF2021/GeneralSkills$ unzip Addadshashanammu.zip
Archive:  Addadshashanammu.zip
   creating: Addadshashanammu/
   creating: Addadshashanammu/Almurbalarammi/
   creating: Addadshashanammu/Almurbalarammi/Ashalmimilkala/
   creating: Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/
   creating: Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi/
   creating: Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis/
   creating: Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku/
  inflating: Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku/fang-of-haynekhtnamet
```
Assuming that the flag will be in the last directory we can use the tab autocomplete feature of the linux terminal to change our directory to the last one in the unzipped set of
folders. Simply typing "cd A" and then pressing the tab key 7 times, the folder names will be autocompleted and we will end up in the "Ularradallaku" directory. This is because
there is only one directory within each directory in the tree so there is only one possible option that can be autocompleted.
```
zerodaytea@DESKTOP-QLQGDSV:/mnt/c/Coding/CTFs/PicoCTF2021/GeneralSkills$ cd Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku/
zerodaytea@DESKTOP-QLQGDSV:/mnt/c/Coding/CTFs/PicoCTF2021/GeneralSkills/Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku$ ls
fang-of-haynekhtnamet
```
After we change our current working directory to the last one we end up with a file named "fang-of-haynekhtnamet". Running the file command we see that it is a 64-bit ELF
executable file and we execute it using "./" in the linux terminal to get the flag.
```
zerodaytea@DESKTOP-QLQGDSV:/mnt/c/Coding/CTFs/PicoCTF2021/GeneralSkills/Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku$ file fang-of-haynekhtnamet
fang-of-haynekhtnamet: ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 3.2.0, BuildID[sha1]=5fffe70019957f0a27a70bb886b2cfb9f9b21d6e, not stripped
zerodaytea@DESKTOP-QLQGDSV:/mnt/c/Coding/CTFs/PicoCTF2021/GeneralSkills/Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku$ ./fang-of-haynekhtnamet
*ZAP!* picoCTF{l3v3l_up!_t4k3_4_r35t!_76266e38}
```

Note:
During the actual competition this challenge required launching an instance on the picoCTF webshell and using the tab autocomplete feature there. No actual zip file was
given as is currently in the picogym.

### Flag:
```
picoCTF{l3v3l_up!_t4k3_4_r35t!_76266e38}
```
