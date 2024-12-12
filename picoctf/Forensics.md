# Trivial Flag Transfer Protocol

## Description
Figure out how they moved the flag.

## Attachment
https://mercury.picoctf.net/static/88553d672efbccbc5868002f4c6eb737/tftp.pcapng

## Hint
What are some other ways to hide data?

## Writeup
Upon downloading the `.pcapng` file, I had no idea how it worked or how to access its content.
On surfing the internet, I learned that it is a file which is used to capture and store network traffic packets, including their metadata and this content can be accessed using `Wireshark`, a widely used, open source network analyzer tool that captures and displays network traffic details in real time.
I downloaded it and imported the file to analyze the network traffic data.
Within the `Trivial File Transfer Protocol` layer, I noticed a series of hexadecimal digits.
Their ASCII representation mentioned about `instructions.txt` file.
To retrieve this file, I started looking for relevant options and settings.
After some trial and error, I discovered the `Export Objects` option under the `File` menu.
Selecting the `TFTP` option displayed a list of files:
- instructions.txt
- plan
- program.deb
- picture1.bmp
- picture2.bmp
- picture3.bmp

I saved all the files assuming they might be useful later.
Upon opening the `instructions.txt` file, I found that it contained a ciphertext `GSGCQBRFAGRAPELCGBHEGENSSVPFBJRZHFGQVFTHVFRBHESYNTGENAFSRE.SVTHERBHGNJNLGBUVQRGURSYNTNAQVJVYYPURPXONPXSBEGURCYNA`.
Using the online cipher analyzer at `https://www.boxentriq.com/code-breaking/cipher-identifier`, I identified that the text was encoded using a Caesar Cipher.
I then decoded it using the online decoder found at `https://www.boxentriq.com/code-breaking/caesar-cipher`, which revealed the plaintext: `TFTPDOESNTENCRYPTOURTRAFFICSOWEMUSTDISGUISEOURFLAGTRANSFER.FIGUREOUTAWAYTOHIDETHEFLAGANDIWILLCHECKBACKFORTHEPLAN`.
Upon reading this decrypted text, I realized that I needed to do something with the `plan` file.
Upon opening it, I found that it contained another ciphertext `VHFRQGURCEBTENZNAQUVQVGJVGU-QHRQVYVTRAPR.PURPXBHGGURCUBGBF`.
Using the online cipher analyzer at `https://www.boxentriq.com/code-breaking/cipher-identifier`, I identified that the text was again encoded using a Caesar Cipher.
I then decoded it using the online decoder found at `https://www.boxentriq.com/code-breaking/caesar-cipher`, which revealed the plaintext: `IUSEDTHEPROGRAMANDHIDITWITH-DUEDILIGENCE.CHECKOUTTHEPHOTOS`.
Upon reading this decrypted text, I realized that I needed to do something with the pictures.
I began analyzing the information and metadata of all the images but found nothing pertinent to the challenge.
Upon interpreting the text further, I understood that `program.deb` file might contain something useful so I unpacked it to find info related to `steghide` command which meant that I needed to carry out steganography analysis on the images.
I then started analyzing the images using the online tool found at `https://futureboy.us/stegano/decinput.html` but it asked for a password.
After testing various phrases, I found the valid passphrase as `DUEDILIGENCE`.
On successful analysis, `picture3.bmp` led me to the flag: `picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}`.

# tunn3l v1s10n

## Description
We found this file. Recover the flag.

## Attachment
https://mercury.picoctf.net/static/21c07c9dd20cd9f2459a0ae75d99af6e/tunn3l_v1s10n

## Hint
Weird that it won't display right...

## Writeup
Upon downloading the file, I had no idea how it worked or how to access its content because it had no extension.
I began analyzing the file's information and metadata using the online data viewer at `https://www.metadata2go.com`, which brought me to the conclusion that given file was a `BMP image` as mentioned in the `mime_type`.
I then viewed it using the online photo editor found at `https://www.photopea.com` but the image seem cropped for some reason and it led me to a fake flag: `notaflag{sorry}` so I started analyzing its data using the online hex editor at `https://hexed.it`.
On surfing the internet, I learned that width of the image is located at bytes 18-21 and height of the image is located at bytes 22-25.
I noticed that the width of the image was set to `6E 04 00 00` so I set the height of the image to the same values and exported it.
I then viewed the edited image, which led me to the flag: `picoCTF{qu1t3_a_v13w_2020}`.

# m00nwalk

## Description
Decode this message from the moon.

## Attachment
https://jupiter.challenges.picoctf.org/static/fc1edf07742e98a480c6aff7d2546107/message.wav

## Hints
- How did pictures from the moon landing get sent back to Earth?
- What is the CMU mascot?, that might help select a RX option

## Writeup
After reading the challenge description and the given hint, I surfed the internet to learn that `Slow-scan television (SSTV)` was the method used to transmit and receive images over radio frequenices during the Apollo 11 mission, marking the first human landing on the Moon.
I also discovered that `Carnegie Mellon University (CMU)`'s mascot is `Scotty` suggesting that the audio file given in the challenge needed to be decoded using the `SSTV` method with the mode set to `Scottie`.
I understood that it could be done using `Robot36 - SSTV Image Decoder`, a tool designed to decode Slow Scan Television images from audio files.
I downloaded it and imported the audio file through the microphone to initiate the decoding process.
On completion, I viewed the decoded image, which revealed the flag: `picoCTF{beep_boop_im_in_space}`.
