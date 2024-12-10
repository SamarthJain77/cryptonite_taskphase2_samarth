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
Running this program with `DLSeGAGDgBNJDQJDCFSFnRBIDjgHoDFCFtHDgJpiHtGDmMAQFnRBJKkBAsTMrsPSDDnEFCFtIbEDtDCIbFCFtHTJDKerFldbFObFCFtLBFkBAAAPFnRBJGEkerFlcPgKkImHnIlATJDKbTbFOkdNnsgbnJRMFnRBNAFkBAAAbrcbTKAkOgFpOgFpOpkBAAAAAAAiClFGIPFnRBaKliCgClFGtIBAAAAAAAOgGEkImHnIl` as the input gave the output as:
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
Upon going through the source code file, I recognised the syntax of Python, so I was able to understand the entire code. I understood that the encoder takes an input string `plaintext` and performs various steps to encrypt it.
First of all, it generates two random numbers `a` and `b` which are used to create two values `u` and `v` via the `generator()` function. 
It computes `u = g^a % p` and `v = g^b % p` using modular exponentiation where `p` and `g` are prime numbers.
The values of `u` and `v` are then used to compute `b_key = u^b % p` and `key = v^a % p`.
If the two keys match, `shared key = key` is confirmed to be valid and is used in the encryption process.
After the shared key is obtained, the `plaintext` string is encrypted using the `dynamic_xor_encrypt()` function. 
This function applies an `XOR` operation to each character of the `plaintext` using `text_key` which is `trudeau` in this case.
The message is reversed first and for each character, `encrypted_char` is obtained by the `XOR` between the ASCII value of the character and the corresponding ASCII value of the key character.
This process returns `cipher_text` which is a scrambled version of the plaintext which is stored as `semi_cipher`.
After the `XOR` operation, `semi_cipher` is further encrypted.
The `encrypt()` function does this by multiplying each character's ASCII value by the `shared key` and further multiplying the result by `311` and appending the final result to the `cipher` list.
The final output is a list of numbers that represent the encrypted version of the original message.
So based on the identified logic, I created a Python program to carry out the `plaintext` retrieval task. Here is the code:
```
from random import randint
import sys


def generator(g, x, p):
    return pow(g, x) % p


def encrypt(plaintext, key):
    cipher = []
    for char in plaintext:
        cipher.append(((ord(char) * key*311)))
    return cipher


def is_prime(p):
    v = 0
    for i in range(2, p + 1):
        if p % i == 0:
            v = v + 1
    if v > 1:
        return False
    else:
        return True


def dynamic_xor_encrypt(plaintext, text_key):
    cipher_text = ""
    key_length = len(text_key)
    for i, char in enumerate(plaintext[::-1]):
        key_char = text_key[i % key_length]
        encrypted_char = chr(ord(char) ^ ord(key_char))
        cipher_text += encrypted_char
    return cipher_text


def test(plain_text, text_key):
    p = 97
    g = 31
    if not is_prime(p) and not is_prime(g):
        print("Enter prime numbers")
        return
    a = randint(p-10, p)
    b = randint(g-10, g)
    print(f"a = {a}")
    print(f"b = {b}")
    u = generator(g, a, p)
    v = generator(g, b, p)
    key = generator(v, a, p)
    b_key = generator(u, b, p)
    shared_key = None
    if key == b_key:
        shared_key = key
    else:
        print("Invalid key")
        return
    semi_cipher = dynamic_xor_encrypt(plain_text, text_key)
    cipher = encrypt(semi_cipher, shared_key)
    print(f'cipher is: {cipher}')
    
 
def decrypt(cipher, key):
    plaintext = ""
    for encrypted_value in cipher:
        decrypted_value = encrypted_value // (key*311)
        plaintext += chr(decrypted_value)
    return plaintext
    
    
def dynamic_xor_decrypt(plaintext, text_key):
    cipher_text = ""
    key_length = len(text_key)
    for i, char in enumerate(plaintext[::-1]):
        key_char = text_key[i % key_length]
        encrypted_char = chr(ord(char) ^ ord(key_char))
        cipher_text += encrypted_char
    plaintext = cipher_text
    cipher_text = ""
    key_length = len(text_key)
    for i, char in enumerate(plaintext[::-1]):
        key_char = text_key[i % key_length]
        encrypted_char = chr(ord(char) ^ ord(key_char))
        cipher_text += encrypted_char
    plaintext = cipher_text
    cipher_text = ""
    key_length = len(text_key)
    for i, char in enumerate(plaintext[::-1]):
        key_char = text_key[i % key_length]
        encrypted_char = chr(ord(char) ^ ord(key_char))
        cipher_text += encrypted_char
    return cipher_text


def untest():
    p = 97
    g = 31
    a = 95
    b = 21
    u = generator(g, a, p)
    v = generator(g, b, p)
    key = generator(v, a, p)
    b_key = generator(u, b, p)
    shared_key = None
    if key == b_key:
        shared_key = key
    else:
        print("Invalid key")
        return
    cipher = [237915, 1850450, 1850450, 158610, 2458455, 2273410, 1744710, 1744710, 1797580, 1110270, 0, 2194105, 555135, 132175, 1797580, 0, 581570, 2273410, 26435, 1638970, 634440, 713745, 158610, 158610, 449395, 158610, 687310, 1348185, 845920, 1295315, 687310, 185045, 317220, 449395]
    semi_cipher = decrypt(cipher, shared_key)
    flag = dynamic_xor_decrypt(semi_cipher, "trudeau")
    print (flag)
    
    
if __name__ == "__main__":
    # message = sys.argv[1]
    # test(message, "trudeau")
    untest()
```
Running this program led me to the flag: `picoCTF{custom_d2cr0pt6d_66778b34}`.

# miniRSA

## Description
Let's decrypt this: ciphertext? Something seems a bit small.

## Attachment
https://jupiter.challenges.picoctf.org/static/d21037ad23ed84cfff20a84768a0f2b2/ciphertext

## Hints
- RSA [tutorial](https://en.wikipedia.org/wiki/RSA_(cryptosystem))
- How could having too small an e affect the security of this 2048 bit key?
- Make sure you don't lose precision, the numbers are pretty big (besides the e value)

## Writeup
After reading the challenge description and the given hint, I realized that I needed to do something with the way RSA encryption works.
RSA encryption formula is `C = M^e mod n` where:
- C is the ciphertext or encrypted message
- M is the plaintext or decrypted message
- e is the public key exponent
- n is the modulus or part of the public key which is calculated as p*q, where p and q are large prime numbers

Upon opening the text file, I found the following values:
```
n: 29331922499794985782735976045591164936683059380558950386560160105740343201513369939006307531165922708949619162698623675349030430859547825708994708321803705309459438099340427770580064400911431856656901982789948285309956111848686906152664473350940486507451771223435835260168971210087470894448460745593956840586530527915802541450092946574694809584880896601317519794442862977471129319781313161842056501715040555964011899589002863730868679527184420789010551475067862907739054966183120621407246398518098981106431219207697870293412176440482900183550467375190239898455201170831410460483829448603477361305838743852756938687673

e: 3

ciphertext (C): 2205316413931134031074603746928247799030155221252519872650073010782049179856976080512716237308882294226369300412719995904064931819531456392957957122459640736424089744772221933500860936331459280832211445548332429338572369823704784625368933
```
I noticed that the value of `C` was smaller than the value of `n` leaving us with the possibility that the value of `M^e` was either smaller or greater than `n`.
I decided to check both possibilities.
I started with the first possibility which simplified the formula to `C = M^e` or `M = C^(1/e)`.
So based on the identified logic, I created a Python program to carry out the `M` retrieval task.
Here is the code:
```
C = 2205316413931134031074603746928247799030155221252519872650073010782049179856976080512716237308882294226369300412719995904064931819531456392957957122459640736424089744772221933500860936331459280832211445548332429338572369823704784625368933

def cuberoot(num):
    if num < 0:
        return -cuberoot(num)
    
    low = 0
    high = num
    while low <= high:
        mid = (low + high) // 2
        mid_cube = mid ** 3
        if mid_cube == num:
            return mid
        elif mid_cube < num:
            low = mid + 1
        else:
            high = mid - 1

result = cuberoot(C)
hexresult = hex(result)
print(hexresult)
```
Running this program gave a hexadecimal string `0x7069636f4354467b6e3333645f615f6c41726733725f655f63636161373737367d` as the output.
I then decoded it using the online decoder found at `https://www.duplichecker.com/hex-to-text.php`, which revealed the flag: `picoCTF{n33d_a_lArg3r_e_ccaa7776}` ruling out the second possibility.
