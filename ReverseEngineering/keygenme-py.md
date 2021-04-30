# keygenme-py
## Category - Reverse Engineering
## Author - SYREAL

### Description: 
keygenme-trial.py

### Solution:
The problem gives a file, after running it and playing with it for a bit, it shows that it is the "trial" version for a program, with a way to make it the full version. The parts that we are interested in are here:

```
username_trial = "MORTON"
bUsername_trial = b"MORTON"

key_part_static1_trial = "picoCTF{1n_7h3_|<3y_of_"
key_part_dynamic1_trial = "xxxxxxxx"
key_part_static2_trial = "}"
key_full_template_trial = key_part_static1_trial + key_part_dynamic1_trial + key_part_static2_trial

```
Some code later,
```
def enter_license():
    user_key = input("\nEnter your license key: ")
    user_key = user_key.strip()

    global bUsername_trial
    
    if check_key(user_key, bUsername_trial):
        decrypt_full_version(user_key)
    else:
        print("\nKey is NOT VALID. Check your data entry.\n\n")
        
def check_key(key, username_trial):

    global key_full_template_trial

    if len(key) != len(key_full_template_trial):
        return False
    else:
        # Check static base key part --v
        i = 0
        for c in key_part_static1_trial:
            if key[i] != c:
                return False

            i += 1

        # TODO : test performance on toolbox container
        # Check dynamic part --v
        if key[i] != hashlib.sha256(username_trial).hexdigest()[4]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[5]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[3]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[6]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[2]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[7]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[1]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[8]:
            return False



        return True

```

Theres a lot here, but after reading it we can understand what it is doing:

There are two parts of the key, which is our flag. The check flag function works by checking the first part of the key by comparing it to a string already in the program,
and it checks the second half by comparing each individidual charactor to another charactor in the SHA256 hash of the word "MORTON", interpreted as bytes. Then it adds a closing curly brace to the end, which is how we know that this is our flag.
Since SHA256 hashes are hashes, we can print out the individual characters with a script (Lets also add the first part and the closing curly brace so that there is less to copy and paste):
```
import hashlib
import base64

HASH = hashlib.sha256(b"MORTON").hexdigest()
LIST = [4,5,3,6,2,7,1,8]

print("picoCTF{1n_7h3_|<3y_of_", end = '')

for i in LIST:
    print(HASH[i], end = '')
print ("}")
```

Flag: `picoCTF{1n_7h3_|<3y_of_75fc1081}`
