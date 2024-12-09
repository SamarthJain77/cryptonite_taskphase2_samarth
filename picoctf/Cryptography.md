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
