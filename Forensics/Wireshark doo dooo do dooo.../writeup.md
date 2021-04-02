# Wireshark doo dooo do doo...

**Description**

Can you find the flag? shark1.pcapng.

**Solution**

We open the file with wireshark and look at the HTTP object list. 2 objects stand out: files with names `\` and `instance-action`

Saving both of these and looking at them:
```
manifold@killerqueenmain:~$ cat instance-action
nonemanifold@killerqueenmain:~$ cat %5c
Gur synt vf cvpbPGS{c33xno00_1_f33_h_qrnqorrs}
manifold@ComputerGaming2:~$
```
That looks like a flag! Since we can clearly see the wrapper, it is likely encoded with substitution cipher, the simplest of which is a caesar cipher. With the offset +13, we decode the string: The flag is picoCTF{p33kab00_1_s33_u_deadbeef}

Flag: `picoCTF{p33kab00_1_s33_u_deadbeef}`
