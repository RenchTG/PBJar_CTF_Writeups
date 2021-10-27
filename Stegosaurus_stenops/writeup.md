# Challenge Info:

#### Challenge Name: Stegosaurus stenops

#### Challenge Author: ZeroDayTea

#### Challenge Description: This stenops swallowed the flag... and some unusually large rock

#### Files Provided: stegosaurus.jpg

# TLDR:

#### - Use some steg cracking tool like steghide or stegcracker to find hidden data in the file.
#### - Figure out that the hint 'rock' is leading you to the wordlist rockyou.txt.
#### - Write a script that brute forces the passphrase using words from rockyou.txt.

# In-Depth Solution: 

#### So when we first open up the image 

## Flag: flag{ungulatus_better_than_stenops}

# Script: 

```python
import os

with open("rockyou.txt", "r") as my_file:
	for line in my_file:
		os.system("steghide extract -sf stegosaurus.jpg -xf info.txt -p " + "\"" + line + "\"")
```
