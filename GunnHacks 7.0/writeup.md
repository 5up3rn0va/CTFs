## CRYPTOGRAPHY

### A Reasonably Simple Attack

Let's start off with the most straightforward RSA attack... Try decrypting this message. Here's the code used to 
generate the encryption: [reasonably_simple_attack.py](reasonably_simple_attack.py)
Hint : What missing information do we need to decrypt the message? How could we obtain that information?
How big can q be?


We are given values n, e, and c. We can use factordb to get the values for p and q.

![b](https://user-images.githubusercontent.com/47029515/104913199-46fdfa80-59b3-11eb-998d-73c274b527b4.png)
