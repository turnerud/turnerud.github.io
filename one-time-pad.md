# One-Time Pad

## Overview

Encryption() takes a couple plaintexts, takes the binary of this plaintext, takes a randomly-generated binary key, and combines them using XOR to give a ciphertext.

Decryption() assumes one has the plaintext of one text (let's say P1), and the ciphertext to that text (let's say C1), as well as the ciphertext of another text (let's say C2). By reverse engineering the plaintext from the XOR of the ciphertext and key, one can decode C2 into plaintext.

## Code
```python
import random

global p1, p2, key, p1keylen, p2keylen, p1counter, p2counter, finalkeylen
global list_of_p1_chars, list_of_p2_chars, cipherp1list, cipherp2list
global cipherp1, cipherp2


def encryption():
    p1 = "Send me $100"
    p2 = "I will send you $100"
    
    list_of_p1_chars = list(p1)
    list_of_p2_chars = list(p2)
    key = []
    p1keylen = len(list_of_p1_chars) * 7
    p2keylen = len(list_of_p2_chars) * 7
    p1counter = 0
    p2counter = 0
    finalkeylen = max(p1keylen, p2keylen)
    
    cipherp1list = []
    cipherp2list = []
    
    key = [random.randint(0, 1) for _ in range(finalkeylen)]
    
        
    while p1counter < p1keylen:
        for x in list_of_p1_chars:
            binary = format(ord(x), '07b')
            p1digitlist = [int(digit) for digit in binary]
            for y in p1digitlist:
                if p1counter < p1keylen:
                    cipherp1list.append(str(int(y ^ key[p1counter])))  
                    p1counter += 1
                    
    while p2counter < p2keylen:
        for x in list_of_p2_chars:
            binary = format(ord(x), '07b')
            p2digitlist = [int(digit) for digit in binary]
            for y in p2digitlist:
                if p2counter < p2keylen:
                    cipherp2list.append(str(int(y ^ key[p2counter])))  
                    p2counter += 1
                    
           
    cipherp1 = ''.join([str(item) for item in cipherp1list])
    cipherp2 = ''.join([str(item) for item in cipherp2list])
 
    
    print("The ciphertext of p1 is: ", cipherp1)
    print("The ciphertext of p2 is: ", cipherp2)
    
    return cipherp1, cipherp2, key

def decryption(cipherp1, cipherp2, key):
    # GIVEN: C1, C2, Key
    # Needs to find P2 by XORing C2 with the key
    
    p2list = []
    c2keylen = len(cipherp2)  
    
    for i in range(c2keylen):
        p2list.append(str(int(cipherp2[i]) ^ key[i]))


    p2binary = ''.join(p2list)
    
    p2 = ''.join([chr(int(p2binary[i:i+7], 2)) for i in range(0, len(p2binary), 7)])
    
    print("The decryption of p2 is:", p2)


cipherp1, cipherp2, key = encryption()  
decryption(cipherp1, cipherp2, key)  
```
## Video Demo
<iframe width="560" height="315" src="https://www.youtube.com/embed/azfOXILbTvM?si=zpSY3cnCNzx3AKuI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

