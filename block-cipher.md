# Block Cipher

## Overview
Encryption and decryption for the Cipher Block Chaining (CBC) algorithm.

## Code
```python
import random

def encryption():
    
    global plaintext    
    plaintext = "Send me $100"
    list_of_plaintext_chars = list(plaintext)    
    interval = 7      
    iv = [random.randint(0, 1) for _ in range(interval)]
    permutation = random.sample(range(interval), interval)  
    cipher = []
    previous_block = iv
    
    for char in list_of_plaintext_chars:
        
        binary = format(ord(char), '07b')
        digitlist = [int(digit) for digit in binary]
        encrypted_block = []
        
        for i in range(interval):
            xor_result = digitlist[i] ^ previous_block[i]            
            encrypted_block.append(xor_result)        
            
        permuted_block = apply_permutation(encrypted_block, permutation)        
        cipher.extend(permuted_block)        
        previous_block = permuted_block
    
    return bits_to_binary_string(cipher), iv, permutation

def decryption(cipher, iv, permutation, plaintextlength):
    interval = 7 
    decrypted = []
    previous_block = iv    
    cipher_bits = [int(bit) for bit in cipher.replace(' ', '')]
    
    for i in range(0, len(cipher_bits), interval):
        
        current_block = cipher_bits[i:i + interval]       
        unpermuted_block = apply_permutation(current_block, sorted(range(interval), key=lambda x: permutation[x]))        
        decrypted_block = [unpermuted_block[j] ^ previous_block[j] for j in range(interval)]        
        decrypted.extend(decrypted_block)        
        previous_block = current_block
    
    return binary_to_string(decrypted)


def apply_permutation(input_block, permutation):
    return [input_block[i] for i in permutation]

def bits_to_binary_string(bits):
    return ' '.join(''.join(str(bit) for bit in bits[i:i + 7]) for i in range(0, len(bits), 7))

def binary_to_string(binary):
    
    char_list = [binary[i:i + 7] for i in range(0, len(binary), 7)]    
    text = ''.join(chr(int(''.join(map(str, b)), 2)) for b in char_list)    
    return text

ciphertext, iv, permutation = encryption()
print("Ciphertext is: ", ciphertext)

decrypted_text = decryption(ciphertext, iv, permutation, len(plaintext))
print("Plaintext is: ", plaintext)
```

## Video Demo
<iframe width="560" height="315" src="https://www.youtube.com/embed/cGlrd0PJ-v4?si=5un_6atVZIpeK4Rj" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
