# Nice Netcat
## Category - General Skills
## Author - SYREAL

### Description: 
There is a nice program that you can talk to by using this command in a shell: $ nc mercury.picoctf.net 35652, but it doesn't speak English...

### Solution:
Connecting to the port given with the netcat command gives us an output of a set of several integers.
Shell command:
```
nc mercury.picoctf.net 35652
```
Output:
```
112 
105 
99 
111 
67 
84 
70 
123 
103 
48 
48 
100 
95 
107 
49 
116 
116 
121 
33 
95 
110 
49 
99 
51 
95 
107 
49 
116 
116 
121 
33 
95 
57 
98 
51 
98 
55 
51 
57 
50 
125 
10 
```
Seeing as all these numbers are in decimal range we throw them into CyberChef with the recipe "From Decimal" to decode into ascii giving us the flag. 
CyberChef Recipe: https://gchq.github.io/CyberChef/#recipe=From_Decimal('Line%20feed',false)&input=MTEyIAoxMDUgCjk5IAoxMTEgCjY3IAo4NCAKNzAgCjEyMyAKMTAzIAo0OCAKNDggCjEwMCAKOTUgCjEwNyAKNDkgCjExNiAKMTE2IAoxMjEgCjMzIAo5NSAKMTEwIAo0OSAKOTkgCjUxIAo5NSAKMTA3IAo0OSAKMTE2IAoxMTYgCjEyMSAKMzMgCjk1IAo1NyAKOTggCjUxIAo5OCAKNTUgCjUxIAo1NyAKNTAgCjEyNSAKMTAgCg

### Flag:
```
picoCTF{g00d_k1tty!_n1c3_k1tty!_9b3b7392}
```
