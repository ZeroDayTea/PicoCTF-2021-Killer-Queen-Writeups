# Python Wrangling
## Category - General Skills
## Author - SYREAL

### Description: 
Python scripts are invoked kind of like programs in the Terminal... Can you run this Python script using this password to get the flag?

### Solution:
The challenge gives us three links to download three different files named "ende.py", "pw.txt", and "flag.txt.en". Looking at the extension of "flag.txt.en" we can deduce that it
is an encoded version of the flag which we need to decode. As the challenge description says we can probably run the "ende.py" python script to decode it. We cat out the 
password.txt file as it may be necessary and then try to run the python script with:
```
python3 ende.py
```
Output:
```
Usage: ende.py (-e/-d) [file]
```
Seeing as -e and -d tags that can be used when running the python script we can deduce that the -d tag would decode and we can pass the "flag.txt.en" file in as the [file] 
parameter. Running the python script command as such prompts us for the password where we can paste in the password gotten from catting out the "pw.txt" file.
Final Command:
```
python3 ende.py -d flag.txt.en
```

### Flag:
```
picoCTF{s4n1ty_v3r1f13d_2aa22101}
```
