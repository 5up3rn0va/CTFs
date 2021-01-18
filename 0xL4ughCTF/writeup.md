## MISC

### Sanity check
![Sanity check - misc](https://user-images.githubusercontent.com/47029515/104912931-f2f31600-59b2-11eb-8bb2-9d057977ce10.png)

You can find the flag under the description of Rules channel.

![b](https://user-images.githubusercontent.com/47029515/104913199-46fdfa80-59b3-11eb-998d-73c274b527b4.png)


## PROGRAMMING

### Hashem
![Hashem-Programming](https://user-images.githubusercontent.com/47029515/104913389-89273c00-59b3-11eb-96df-a1c76e1c4028.png)

From the challenge description we know that the password was less than 6 characters and consisted only of lowercase alphabets. This can easily be bruteforced but
we aren't given the type of hash used. I used an online hash analyzer for this.

![Screenshot from 2021-01-18 17-53-15](https://user-images.githubusercontent.com/47029515/104915404-985bb900-59b6-11eb-8f73-ae26fb5e63e6.png)

Let's try with MD5. We're also given the salt used in the hash `mmal7`. There are only two possible locations for the salt, either before or after the password. The flag format depends
on the position of the salt. Let's try attaching the salt as prefix first.

```python
import string
import hashlib

x = "bd737ce0d884c0dd54adf35fdb794b60"
chars = list(string.ascii_lowercase)

for i in chars:
    for j in chars:
        for k in chars:
            for a in chars:
                for b in chars:
                    m = hashlib.md5()
                    m.update("mmal7" + i+j+k+a+b)
                    if m.hexdigest() == x:
                        print "0xL4ugh{1_" + i+j+k+a+b + "}"
                        break
```

And bingo!

```
0xL4ugh{1_laugh}
```
