# GDB baby step 1

## Description
Can you figure out what is in the `eax` register at the end of the `main` function? Put your answer in the picoCTF flag format: `picoCTF{n}` where `n` is the contents of the `eax` register in the decimal number base. If the answer was `0x11` your flag would be `picoCTF{17}`.

## Attachment
https://artifacts.picoctf.net/c/512/debugger0_a

## Hints
- gdb is a very good debugger to use for this problem and many others!
- `main` is actually a recognized symbol that can be used with gdb commands.

## Writeup
After reading the challenge description and the given hints, I realized that I needed to dive deep inside the given file and find the `eax` register inside the `main` function using the GDB debugger to find the required hexadecimal value for obtaining the flag. On surfing the internet, I learned that GDB stands for `GNU Debugger`. It is a tool used for debugging programs at both the source code and assembly level. It allows us to view functions, traverse through memory locations, disassemble code and various other things. I initially navigated to the `~/Downloads` directory using `cd` command. I then initiated GDB and used the `file debugger0_a` command to help GDB read the symbols (names of variables, functions and types) present in the file, but no debugging symbols were found. I then used the `help` command and went through the `status` class because it was tagged as the one containing list of commands related to inquiries and stuff. There I found the `info functions` command with the usage mentioning that it displays all function names or those matching regular expressions. This command was relevant to our challenge as we need to find the `main` function. Upon executing it, I got a list of functions with one labeled as `0x0000000000001129  main`. Then, I again used the `help` command and went through the `data` class because it was tagged as the one containing list of commands related to examination of data. There I found the `disassemble` command with the usage mentioning that it disassembles a specified section of memory. This command was relevant to our challenge as we need to find the `eax` register within the `main` function. Upon executing it, entire order of instructions that the CPU follows for the `main` function was disassembled and displayed on the terminal with one labeled as `0x0000000000001138 <+15>:	mov    $0x86342,%eax`. After analyzing this output, I realised that `0x86342` was the required hexadecimal value. I then converted it to decimal number base using the online decoder found at `https://www.rapidtables.com/convert/number/hex-to-decimal.html?x=86342`, which led me to the value of `n` as `549698` and the flag: `picoCTF{549698}`.
