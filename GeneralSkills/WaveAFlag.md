# Wave a Flag
## Category - General Skills
## Author - SYREAL

### Description: 
Can you invoke help flags for a tool or binary? This program has extraordinarily helpful information...

### Solution:
The challenge gives us a link to download a 64-bit ELF Executable file named "warm". Trying to run it with:
```
./warm
```
in a linux terminal gives us this output:
```
Hello user! Pass me a -h to learn what I can do!
```
Passing in a "-h" to the program as it asked us to do gives us a different output with the flag.
Final command:

```
./warm -h
```

### Flag:
```
picoCTF{b1scu1ts_4nd_gr4vy_30e77291}
```
