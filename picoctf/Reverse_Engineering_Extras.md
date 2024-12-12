# Transformation

## Description
I wonder what this really is... enc 
`''.join([chr((ord(flag[i]) << 8) + ord(flag[i + 1])) for i in range(0, len(flag), 2)])`

## Attachment
https://mercury.picoctf.net/static/a757282979af14ab5ed74f0ed5e2ca95/enc

## Hint
You may find some decoders online

## Writeup
After reading the challenge description and the given hint, I understood how the flag was encrypted using the given encoding scheme.
It processes every two characters of the `flag` string at a time.
The `ord()` function converts the character at index `i` to its Unicode value and then left shift operator `(<<)` shifts the binary representation of Unicode integer value by 8 bits to the left.
Then the result of the shifted value is added to Unicode value of the character at index `i + 1`.
At last, the `chr()` function takes the integer and converts it back into a character and all the resulting characters from each iteration are combined into a single string.
Since it involved Unicode values, I suspected that applying Unicode Transformation Format (UTF) encoding to the given string might help.
So based on the identified logic, I created a Python program to carry out this flag retrieval task. Here is the code:
```bash
encoded_flag = "灩捯䍔䙻ㄶ形楴獟楮獴㌴摟潦弸彤㔲挶戹㍽"
print(encoded_flag.encode("utf-8"))
print(encoded_flag.encode("utf-16"))
print(encoded_flag.encode("utf-32"))
print(encoded_flag.encode("utf-7"))
print(encoded_flag.encode("utf-16-le"))
print(encoded_flag.encode("utf-16-be"))
print(encoded_flag.encode("utf-32-le"))
print(encoded_flag.encode("utf-32-be"))
```
Running this program led me to the flag: `picoCTF{16_bits_inst34d_of_8_d52c6b93}`.

# vault-door-training

## Description
Your mission is to enter Dr. Evil's laboratory and retrieve the blueprints for his Doomsday Project. The laboratory is protected by a series of locked vault doors. Each door is controlled by a computer and requires a password to open. Unfortunately, our undercover agents have not been able to obtain the secret passwords for the vault doors, but one of our junior agents obtained the source code for each vault's computer! You will need to read the source code for each level to figure out what the password is for that vault door. As a warmup, we have created a replica vault in our training facility. The source code for the training vault is here: VaultDoorTraining.java

## Attachment
https://jupiter.challenges.picoctf.org/static/03c960ddcc761e6f7d1722d8e6212db3/VaultDoorTraining.java

## Hint
The password is revealed in the program's source code.

## Writeup
Upon going through the source code file, I found the syntax of Java quite similar to C, so I was able to understand the entire code using my knowledge of C as I don't have any prerequisite knowledge of Java.
I understood that the program first checks whether the user's input matches the specific pattern `picoCTF{password}` and then extracts the actual password by removing the `picoCTF{` prefix and the `}` suffix.
The extracted password is then compared to a fixed string: `w4rm1ng_Up_w1tH_jAv4_3808d338b46`.
If they match, access to the vault is granted. Otherwise, the access is denied.
So based on the identified logic, I understood that the `password` is itself `w4rm1ng_Up_w1tH_jAv4_3808d338b46` which led me to the flag: `picoCTF{w4rm1ng_Up_w1tH_jAv4_3808d338b46}`.
