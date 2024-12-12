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

# GDB baby step 1

## Description
Can you figure out what is in the `eax` register at the end of the `main` function? Put your answer in the picoCTF flag format: `picoCTF{n}` where `n` is the contents of the `eax` register in the decimal number base. If the answer was `0x11` your flag would be `picoCTF{17}`.

## Attachment
https://artifacts.picoctf.net/c/512/debugger0_a

## Hints
- gdb is a very good debugger to use for this problem and many others!
- `main` is actually a recognized symbol that can be used with gdb commands.

## Writeup
After reading the challenge description and the given hints, I realized that I needed to dive deep inside the given file and find the `eax` register inside the `main` function using the GDB debugger to find the required hexadecimal value for obtaining the flag. 
On surfing the internet, I learned that GDB stands for `GNU Debugger`. 
It is a tool used for debugging programs at both the source code and assembly level. 
It allows us to view functions, traverse through memory locations, disassemble code and various other things. 
I initially navigated to the `~/Downloads` directory using `cd` command. 
I then initiated GDB and used the `file debugger0_a` command to help GDB read the symbols (names of variables, functions and types) present in the file, but no debugging symbols were found. 
I then used the `help` command and went through the `status` class because it was tagged as the one containing list of commands related to inquiries and stuff. 
There I found the `info functions` command with the usage mentioning that it displays all function names or those matching regular expressions.
This command was relevant to our challenge as we need to find the `main` function. 
Upon executing it, I got a list of functions with one labeled as `0x0000000000001129  main`. 
Then, I again used the `help` command and went through the `data` class because it was tagged as the one containing list of commands related to examination of data. 
There I found the `disassemble` command with the usage mentioning that it disassembles a specified section of memory. 
This command was relevant to our challenge as we need to find the `eax` register within the `main` function. 
Upon executing it, entire order of instructions that the CPU follows for the `main` function was disassembled and displayed on the terminal with one labeled as `0x0000000000001138 <+15>:	mov    $0x86342,%eax`. 
After analyzing this instruction, I realised that `0x86342` was the required hexadecimal value. 
I then converted it to decimal number base using the online decoder found at `https://www.rapidtables.com/convert/number/hex-to-decimal.html?x=86342`, which led me to the value of `n` as `549698` and the flag: `picoCTF{549698}`.

# ARMssembly 1

## Description
For what argument does this program print `win` with variables `87`, `3` and `3`? File: chall_1.S Flag format: picoCTF{XXXXXXXX} -> (hex, lowercase, no 0x, and 32 bits. ex. 5614267 would be picoCTF{0055aabb})

## Attachment
https://mercury.picoctf.net/static/52fa2dfbc7fb145f0a4bf7fd2a89fc49/chall_1.S

## Hint
Shifts

## Writeup
Upon downloading the `.S` file, I had no idea how it worked or how to run its content.
On surfing the internet, I learned that it is a source file written in assembly language which contains assembly code for a specific architecture (ARM, x86, etc..) and is processed by an assembler into machine code.
Upon going through the source code file, I saw the assembly program that consisted of two main functions `func` and `main`.
On surfing the internet, I understood the functionality and working of each command and got to know that the main goal was performing arithmetic operations on the number given by user as the input and printing a specific message based on the result.
Here is what I understood:
```
func:
    sub sp, sp, #32 ----------> Saves the stack pointer and allocates 32 bytes on the stack for local variables
    str w0, [sp, 12] ----------> Stores the value of w0 at sp + 12
    mov w0, 87 ----------> Moves 87 into w0
    str w0, [sp, 16] ----------> Stores 87 at sp + 16
    mov w0, 3 ----------> Moves 3 into w0
    str w0, [sp, 20] ----------> Stores 3 at sp + 20
    mov w0, 3 ----------> Moves 3 into w0 again
    str w0, [sp, 24] ----------> Stores 3 at sp + 24
    ldr w0, [sp, 20] ----------> Loads the value at sp + 20 which is 3 into w0
    ldr w1, [sp, 16] ----------> Loads the value at sp + 16 which is 87 into w1
    lsl w0, w1, w0 ----------> w0 = w1 << w0 or 87 << 3 = 696 (Left bitwise shift)
    str w0, [sp, 28] ----------> Stores the result 696 at sp + 28
    ldr w1, [sp, 28] ----------> Loads the value at sp + 28 which is 696 into w1
    ldr w0, [sp, 24] ----------> Loads the value at sp + 24 which is 3 into w0
    sdiv w0, w1, w0 ----------> w0 = w1 / w0 or 696 / 3 = 232 (Division)
    str w0, [sp, 28] ----------> Stores the result 232 at sp + 28
    ldr w1, [sp, 28] ----------> Loads the value at sp + 28 which is 232 into w1
    ldr w0, [sp, 12] ----------> Loads the initial value at sp + 12 into w0
    sub w0, w1, w0 ----------> w0 = w1 - w0 or 232 - initial value (Subtraction)
    str w0, [sp, 28] ----------> Stores the result at sp + 28
    ldr w0, [sp, 28] ----------> Loads the value at sp + 28 into w0
    add sp, sp, 32 ----------> Deallocates the 32 bytes from the stack
    ret ----------> Returns from the function
main:
    stp x29, x30, [sp, -48]! ----------> Saves the register and frame pointer to the stack
    add x29, sp, 0 ----------> Sets the frame pointer to the current stack pointer
    str w0, [x29, 28] ----------> Stores the value of w0 at x29 + 28
    str x1, [x29, 16] ----------> Stores the value of x1 at x29 + 16
    ldr x0, [x29, 16] ----------> Loads the value at x29 + 16 which is x1
    add x0, x0, 8 ----------> x0 = x0 + 8 (Addition)
    ldr x0, [x0] ----------> Dereferences the address and loads the value at that address
    bl atoi ----------> Calls the 'atoi' function to convert the value of x0 to an integer
    str w0, [x29, 44] ----------> Stores the converted integer value at x29 + 44
    ldr w0, [x29, 44] ----------> Loads the converted integer value at x29 + 44
    bl func ----------> Calls the function 'func' with the converted integer as the argument
    cmp w0, 0 ----------> Compares the result which is value of w0 to 0
    bne .L4 ----------> If result is not 0, jumps to .L4
    adrp x0, .LC0 ----------> Loads address of the string "You win!" into x0
    add x0, x0, :lo12:.LC0 ----------> Adds 12 bits of the address to x0
    bl puts ----------> Calls the function 'puts' to print "You win!"
    b .L6 ----------> Jumps to the end of the program
.L4:
    adrp x0, .LC1 ----------> Loads address of the string "You Lose :(" into x0
    add x0, x0, :lo12:.LC1 ----------> Adds 12 bits of the address to x0
    bl puts ----------> Calls the function 'puts' to print "You Lose :("
.L6:
    nop ----------> No operation or end of the function
    ldp x29, x30, [sp], 48 ----------> Restores the register and frame pointer and deallocate the stack space
    ret ----------> Returns from the 'main'
```
In the `main` function, I noticed that the value of `w0` is compared to `0` where the value of `w0` depends on the input provided by the user as defined in the `func` function: `w0 = w1 - w0 or 232 - initial value`.
This meant that I needed to provide `232` as the input or initial argument for the program to execute the winning part.
I then converted it to hexadecimal base using the online decoder found at `https://www.rapidtables.com/convert/number/decimal-to-hex.html`, which led me to the value as `000000E8` and the flag: `picoCTF{000000e8}`.

# vault-door-3

## Description
This vault uses for-loops and byte arrays. The source code for this vault is here.

## Attachment
https://jupiter.challenges.picoctf.org/static/a648ca6dd275b9454c5d0de6d0f6efd3/VaultDoor3.java

## Hint
Make a table that contains each value of the loop variables and the corresponding buffer index that it writes to.

## Writeup
Upon going through the source code file, I found the syntax of Java quite similar to C, so I was able to understand the entire code using my knowledge of C as I don't have any prerequisite knowledge of Java.
I understood that the program first ensures that the password is exactly 32 characters long and then creates a new password string named `buffer` by copying characters from the input password in a specific order.
The modified password is then compared to a fixed string: `jU5t_a_sna_3lpm18gb41_u_4_mfr340`.
If they match, access to the vault is granted. Otherwise, the access is denied.
So based on the identified logic, I created a C program to carry out this password retrieval task. Here is the code:
```bash
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
int main() 
{
    int i=0;
    char password[]="jU5t_a_sna_3lpm18gb41_u_4_mfr340";
    char buffer[33];
    for(i=0;i<8;i++) 
    {buffer[i]=password[i];}
    for(i;i<16;i++) 
    {buffer[i]=password[23-i];}
    for(i;i<32;i+=2) 
    {buffer[i]=password[46-i];}
    for(i=31;i>=17;i-=2) 
    {buffer[i]=password[i];}
    buffer[33]='\0';
    printf("Correct Password: %s \n",buffer);
    return 0;
}
```
Running this program led me to the `Correct Password` as `jU5t_a_s1mpl3_an4gr4m_4_u_1fb380` and the flag: `picoCTF{jU5t_a_s1mpl3_an4gr4m_4_u_1fb380}`.
