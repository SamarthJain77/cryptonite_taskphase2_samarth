# interencdec

## Description
Can you get the real meaning from this file.
Download the file here.

## Attachment
https://artifacts.picoctf.net/c_titan/1/enc_flag

## Hint
Engaging in various decoding processes is of utmost importance

## Writeup
Upon opening the text file, I recognized that it contained a base64 encoded string.
I then decoded it using the online decoder found at `https://base64.guru/converter/decode/text`, which led me to another base64 encoded string: `b'd3BqdkpBTXtqaGx6aHlfazNqeTl3YTNrX2xoNjBsMDBpfQ=='`.
I tried to decode it but faced an error because base64 encoding uses the specific character set `(A-Z, a-z, 0-9, +, /)` but the string had a special character `'`.
So I decided to focus on the string `d3BqdkpBTXtqaGx6aHlfazNqeTl3YTNrX2xoNjBsMDBpfQ==` present within `''` and decoded it, which led me to a ciphertext: `wpjvJAM{jhlzhy_k3jy9wa3k_lh60l00i}`.
I recognized that it was encrypted using Caesar Cipher with the key set to `10`.
I then decoded it using the online decoder found at `https://www.boxentriq.com/code-breaking/caesar-cipher`, which led me to the flag: `picoCTF{caesar_d3cr9pt3d_ea60e00b}`.

# Mod 26

## Description
Cryptography can be easy, do you know what ROT13 is? 

## Attachment
cvpbPGS{arkg_gvzr_V'yy_gel_2_ebhaqf_bs_ebg13_uJdSftmh}

## Hint
This can be solved online if you don't want to do it by hand!

## Writeup
After reading the challenge description and the given hint, I realized that the string was encrypted using ROT13 Cipher.
I then decoded it using the online decoder found at `https://rot13.com`, which revealed the flag: `picoCTF{next_time_I'll_try_2_rounds_of_rot13_hWqFsgzu}`.

# The Numbers

## Description
The numbers... what do they mean?

## Attachment
https://jupiter.challenges.picoctf.org/static/f209a32253affb6f547a585649ba4fda/the_numbers.png

## Hint
The flag is in the format PICOCTF{}

## Writeup
Upon viewing the image and reading the given hint, I realized that the flag was encrypted in such a way that the numbers represent the positional value of the letters they belong to. 
I then decoded it using the online decoder found at `https://www.boxentriq.com/code-breaking/numbers-to-letters`, which revealed the flag: `picoCTF{thenumbersmason}`.

# 13

## Description
Cryptography can be easy, do you know what ROT13 is?

## Attachment
cvpbPGS{abg_gbb_onq_bs_n_ceboyrz}

## Hint
This can be solved online if you don't want to do it by hand!

## Writeup
After reading the challenge description and the given hint, I realized that the string was encrypted using ROT13 Cipher.
I then decoded it using the online decoder found at `https://rot13.com`, which revealed the flag: `picoCTF{not_too_bad_of_a_problem}`.

# C3

## Description
This is the Custom Cyclical Cipher!
Download the ciphertext here.
Download the encoder here.
Enclose the flag in our wrapper for submission. If the flag was "example" you would submit "picoCTF{example}".

## Attachments
- https://artifacts.picoctf.net/c_titan/47/ciphertext
- https://artifacts.picoctf.net/c_titan/47/convert.py

## Hint
Modern crypto schemes don't depend on the encoder to be secret, but this one does.

## Writeup
Upon going through the source code file, I recognised the syntax of Python, so I was able to understand the entire code.
I understood that the encoder takes an input string `chars` and for each character, finds its index in `lookup1`.
It then calculates the transformation `(cur - prev) % 40`.
This transformation is then used to select a character from `lookup2` to append to the output while the encoder keeps track of the previous index `prev` to compute the transformation for the next character.
So based on the identified logic, I created a Python program to carry out the decoding task.
Here is the code:
```
import sys
chars = ""
from fileinput import input
for line in input():
  chars += line

lookup1 = "\n \"#()*+/1:=[]abcdefghijklmnopqrstuvwxyz"
lookup2 = "ABCDEFGHIJKLMNOPQRSTabcdefghijklmnopqrst"

out = ""

prev = 0
for char in chars:
  cur = lookup2.index(char)
  original = (cur + prev) % 40
  out += lookup1[original]
  prev = original

sys.stdout.write(out)
```
Running this program with `DLSeGAGDgBNJDQJDCFSFnRBIDjgHoDFCFtHDgJpiHtGDmMAQFnRBJKkBAsTMrsPSDDnEFCFtIbEDtDCIbFCFtHTJDKerFldbFObFCFtLBFkBAAAPFnRBJGEkerFlcPgKkImHnIlATJDKbTbFOkdNnsgbnJRMFnRBNAFkBAAAbrcbTKAkOgFpOgFpOpkBAAAAAAAiClFGIPFnRBaKliCgClFGtIBAAAAAAAOgGEkImHnIl` as the input to get the output as:
```
#asciiorder
#fortychars
#selfinput
#pythontwo

chars = ""
from fileinput import input
for line in input():
    chars += line
b = 1 / 1

for i in range(len(chars)):
    if i == b * b * b:
        print chars[i] #prints
        b += 1 / 1
```
I noticed that `()` was missing in the `print` statement which seemed unusual to me so I started surfing the internet to find that it was a Python2 code.
So I converted it into a Python3 code:
```
#asciiorder
#fortychars
#selfinput
#pythontwo

chars = ""
from fileinput import input
for line in input():
    chars += line
b = 1

for i in range(len(chars)):
    if i == (b * b * b):
        print (chars[i]) #prints
        b += 1
```
I noticed that to run this program, an input was required so I started searching for it throughout the code. While searching, I found `#selfinput` written in the code. Taking it as a hint, I ran the program using the entire code as the input and to my surprise, it led me to the string `adlibs` and the flag: `picoCTF{adlibs}`.

# Custom encryption

## Description
Can you get sense of this code file and write the function that will decode the given encrypted file content.
Find the encrypted file here flag_info and code file might be good to analyze and get the flag.

## Attachments
- https://artifacts.picoctf.net/c_titan/94/enc_flag
- https://artifacts.picoctf.net/c_titan/94/custom_encryption.py

## Hint
Understanding encryption algorithm to come up with decryption algorithm.

## Writeup
