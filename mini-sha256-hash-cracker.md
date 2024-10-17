# Mini SHA-256 Hash Cracker

This was an extra credit part to my midterm project in my Databases and Computer Security course. Documentation below.

## Code
```python
"""
Created on Tue Oct  8 10:39:39 2024

@author: simon

Crack the password:

I'm given this encrypted password: 8a798890fe93817163b10b5f7bd2ca4d25d84c52739a645a889c173eee7d9d3d
I know the decrypted password is three characters long.


"""
from itertools import permutations
import string
import hashlib

characters = string.ascii_letters # Both lowercase and uppercase letters


for x in permutations(characters, 3): # It was given that the password was 3 characters.
    
    temphash =''.join(map(str, x)).encode('ascii')
    code = hashlib.sha256()
    code.update(temphash) # These three lines help make the permutation readable
    
    temphash = code.hexdigest() # Hashing
    if temphash == "8a798890fe93817163b10b5f7bd2ca4d25d84c52739a645a889c173eee7d9d3d": # Checking 
        password = x
        break; 
        
delimiter = ''
finalpassword = delimiter.join(password)
        
print("The password is", finalpassword)
```

The password ended up being 'yes'.
