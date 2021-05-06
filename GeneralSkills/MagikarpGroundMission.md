# Magikarp Ground Mission
## Category - General Skills
## Author - SYREAL

### Description: 
Do you know how to move between directories and read files in the shell? Start the container, `ssh` to it, and then `ls` once connected to begin. 
Login via `ssh` as `ctf-player` with the password, `b60940ca`

### Solution:
The challenge gives us the option to start an instance by clicking "Start Instance" which gives us an ssh port to connect to as well as a user and a password for that user to use
when connecting to the given port. Starting the instance and then sshing to it with the ssh command on linux gives us a bash shell to use to find the flag.

```
zerodaytea@Patryk:~$ ssh ctf-player@venus.picoctf.net -p 52218
The authenticity of host '[venus.picoctf.net]:52218 ([3.131.124.143]:52218)' can't be established.
ECDSA key fingerprint is SHA256:NrQkIxNEQQho/GA7jE0WlIa7Jh4VF9sAvC5awkbuj1Q.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[venus.picoctf.net]:52218,[3.131.124.143]:52218' (ECDSA) to the list of known hosts.
ctf-player@venus.picoctf.net's password:
Welcome to Ubuntu 18.04.5 LTS (GNU/Linux 5.4.0-1041-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage
This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

ctf-player@pico-chall$
```
If this is the first time you are sshing to the particular network you will have to type "yes" aftering being prompted whether to add the network host to the list of your 
computer's known hosts. We are then prompted for the password to our ctf-player user which we get from the description and are able to get our bash shell. Looking at the files
in our current directory we see a "1of3.flag.txt" file which we cat out as well as a "instructions-to-2of3.txt" file which we cat out to get a hint for where to find the next
part of the flag.
```
ctf-player@pico-chall$ ls
1of3.flag.txt  instructions-to-2of3.txt
ctf-player@pico-chall$ cat 1of3.flag.txt
picoCTF{xxsh_
ctf-player@pico-chall$ cat instructions-to-2of3.txt
Next, go to the root of all things, more succinctly `/`
ctf-player@pico-chall$
```
We get the first part of the flag and proceed to go to the root directory as the instructions told us to in order to find the next part of the flag. In the root directory we see
a "2of3.flag.txt" file which we cat out to get the second part of the flag and a "instructions-to-3of3.txt" file which we cat out to get a hint for where to find the third and
final part of the flag.
```
ctf-player@pico-chall$ cd /
ctf-player@pico-chall$ ls
2of3.flag.txt  bin  boot  dev  etc  home  instructions-to-3of3.txt  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
ctf-player@pico-chall$ cat 2of3.flag.txt
0ut_0f_\/\/4t3r_
ctf-player@pico-chall$ cat instructions-to-3of3.txt
Lastly, ctf-player, go home... more succinctly `~`
ctf-player@pico-chall$
```
We use the instructions given and change to the home directory which is also often represented by the tilde symbol "~". Here we see the third and final part of the flag which 
we cat out and add to our previous parts to get the complete flag.
```
ctf-player@pico-chall$ cd ~
ctf-player@pico-chall$ ls
3of3.flag.txt  drop-in
ctf-player@pico-chall$ cat 3of3.flag.txt
c1754242}
ctf-player@pico-chall$
```

### Flag:
```
picoCTF{xxsh_0ut_0f_\/\/4t3r_c1754242}
```
