# Verify

## Description
People keep trying to trick my players with imitation flags. I want to make sure they get the real thing! I'm going to provide the SHA-256 hash and a decrypt script to help you know that my flags are legitimate.
Additional details will be available after launching your challenge instance.

To decrypt the file once you've verified the hash, run `./decrypt.sh files/<file>`.

## Attachments
- `ssh -p 52220 ctf-player@rhea.picoctf.net`
- Use the password `f3b61b38`. Remember, in a shell, passwords are hidden!
- Accept the fingerprint with `yes`, and `ls` once connected to begin.
- Checksum: fba9f49bf22aa7188a155768ab0dfdc1f9b86c47976cd0f7c9003af2e20598f7

## Hints
- Checksums let you tell if a file is complete and from the original distributor. If the hash doesn't match, it's a different file.
- You can create a SHA checksum of a file with `sha256sum <file>` or all files in a directory with `sha256sum <directory>/*`.
- Remember you can pipe the output of one command to another with `|`. Try practicing with the `'First Grep'` challenge if you're stuck!

## Writeup
After reading the challenge description and the given hint, I realized that I needed to do something with `sha256sum <file>` command, `|` operator and `grep <string>` command.
I knew that `sha256sum` command is used to create a SHA checksum of a file, `|` operator is used to connect the output of one command directly to the input of another command and `grep` command is used for searching for lines that match a specified pattern.
On connecting with the challenge instance, I used `ls` command for listing all files and directories and got the output as `checksum.txt`, `decrypt.sh` and `files`.
Then I used `sha256sum *` command and got the output as:
```
da498696036e38f06e75a154878b42a28e14701405140a71f1f5a1e147e071d1  checksum.txt
6eb5ce37a3581f5fb6f8f432186dbb49855670a39008dd4602bc4722c0f84c4e  decrypt.sh
sha256sum: files: Is a directory
```
Then I navigated to the `files` directory using `cd files` command and there I used the `ls` command to get the output as:
```
02kLdPvr  5guDO1cS  DQlu1oVQ  MkEdjeVZ	TSGfXer8  bXmTLFnK  jg2ztGlp  t1UlIMzc
0AEMwSHP  5oxXh5Er  DUx15XmG  MoKJFjOi	TdeDBXMf  byaxGEzl  jpTG7wle  t3cJ6Gfp
0QBK0M73  5uH65mOX  Ds4StPpk  Mrl2cMHD	Tz1xgD5A  c5K8wpvT  k1uy8MT2  tYVdC1Z0
0ReLqo7l  6GarVCiO  DxLqi3sV  Ms5Mvz12	U6Za1XXb  cAehfago  k3Je1oZv  tqcK3Nrs
0pYtGDyN  6JGob933  DyULYdws  N36WmSck	W2hZvcID  cAgx0hQ8  l4aPZsIN  uF2fheP1
13eD2Klj  7GdIoG6L  EI5Rua6h  NTsSRBdP	WJFLBATt  cBdFMzZa  lCWOa2m6  uFoxxMAD
15s8svF3  7M36N0ZG  EtkxnTjE  NULNnaKd	WLCnFHkD  caVHWehf  lY9YUKSk  uHK0HPxg
1BX0cysv  7S05biBB  EwczAgxU  NbwekSHV	WOHDiZ4q  cbKOHVgV  lpgH0BeK  uVGzmmri
1QyIAyVK  7SXF5dDA  F7pJKgt3  O5vpRSXk	WY59WpIg  cxjAxbcB  lty8luMw  uiBoxr24
1WzFkIC5  7XpL7kA2  FA1DL0lH  O8mpr58x	WZcRSCOi  d5EQVHHc  mAZwT81W  urhbGMnd
1fPO7Wz1  7ZEsnWZx  FaSiQOUR  OFSlnCKK	WjjIvWrX  dGbl67gA  mL2zl8ME  v7gF2ZIR
1iUcIRwR  7dnW8EpS  GBMBtUcG  OHWOluJj	WpLyF4xC  diVxZXPr  miUtTQRm  vJ3qPWEu
1kzeT7Bq  7e0ugnNi  GGpU931s  OgbJmSsl	WruPiHQS  dmc1Epts  nYMkLfqq  vMdtOisa
1s9fb01L  7enMn1rk  GTH1LeLw  OvH6KubA	XKypMMiJ  dzxHhn9S  ngS5ThOq  vT94qEUU
2EHy0UNu  7iM83rpT  Giagg0HI  P0pMREh2	XZocCx02  ePMDz1YQ  niAMHayw  vZ9Qc5Cg
2HLMOyNv  7qVcsxIn  Gup9YNYb  PK3nRKAh	Xkrt40pJ  eqMPkSW0  np9TOAIR  vZXXKL7g
2SLddvKm  7x5Qa3WK  Gyn3Qful  PVAhaXhI	XmYppXhk  eyrV73UR  o4p7FB5l  vlXYHLR4
2y6eiPnY  87590c24  HUGRY61E  PbCHfm8l	Y9apvJeb  fANUtdte  oNQJCg54  vy3RDHxy
2ypuxhr6  8pMqC98d  HUqcWryv  PisLwk6C	YJZwL09m  fFbQAlD7  oNq64S7j  wH52POYK
34asQJAj  9E2Ci7r7  HVhGYkYw  PucU9ljB	YXeLAbOj  fG3pxqYw  oX1HkX8C  wR9DoLPS
3FS3M7tr  9LgFu97C  HkwhoPkp  PyzlgxBl	YmQKA23p  fM4Y8XlN  opYpNJ2C  whsqK6Xi
3HWGffFE  9hbn5BeA  Hw4z4pGA  QU8jejZq	YoOZ5qVn  frJix6dy  p0yUpsYe  wp0CW0xc
3KQWpDpt  9twFwHiq  I7ySGmF3  QUesl6sJ	Yqx2G9d1  fzjMwVlq  p8McbjLN  x0ODxbKK
3RwrWxAh  AHwWjpbL  IihMQr2S  QjfpcKtL	YrKlF95C  g33i1myO  pGy7EVYy  x0THPKVQ
3UI1Q3Im  ANd9SGuS  Ijh6n9yp  QkF8ZdDf	ZS6vNpit  gNe3d0tj  pbXSC543  xPX9SADx
3XFTF7vi  AXwbPGqz  Iqbw9pQz  RD85xyJi	ZS7jkTUt  h6P0bHfg  q2mcPs3c  xa0pHpo3
3azP1Vr5  Ae01ONEX  JHLXVG98  RGc1b7Dz	ZTxbKkJG  hIbQdK4d  qhTEo0LL  y2TwAQsl
3bwissRA  AfqV5hAX  JKlfmBiL  RH4yp5nD	ZXWIGnQR  hueXtQsv  qxtRkCQq  yCXEcn1e
3llQZxg9  AuXnIN8I  JPzzPv2R  RHX0dhSU	a2OU257J  i9nzJ3r6  r0zVMZkQ  yRSmctoR
3niXrkT4  Av9IEmci  JZuYuOle  S7zBjDOu	a5BwxEPT  iBekBdEx  raIgZC8T  ybQ7iIWc
4E42FQrx  BVQMsUMN  K4w4LSpK  SOpZbONn	aAv6C6d8  ia64o1VA  rse22gSC  z8QLAIjY
4RWg3C81  BYWVMQ8G  KM1rOvYX  SXfbixMa	aCxWJytK  inbE9V4Z  s1T1hXGi  zKjekGtU
4WsDciyV  Bb0A4ZUF  KRxkl4ki  SibjLvWM	aR087rW1  iyKEK5tY  sHWDCVFR  ze9Qihpg
4YmX8P1z  BjOuTdvt  KaGA7sxA  SliwhkVP	b9BDTW02  j21jebUD  sODASTm7  zfFqIJrW
4lpXJyrZ  CDVB02i6  Kopd5uAS  SuTmtwHT	bJ8uPssG  jFn9chPx  sTNxbYIX  ziobqxT9
5L6bCEOe  CLcdCN8f  Kqq1CiRK  TAh3haNF	bJquvh3E  jGGKUWQ9  sbuTFkuC
5VDBcjMu  CfZp4f2N  MCFq06DD  TIC1KArZ	bOxuzUXf  jQrw8bQO  scPPxxi7
5aE4Zjfg  D3FjiyXm  MRW8xKE7  TJect2dg	bSkjXxrA  jS1LPICH  srli5tAs
```
I realized that it was impractical to create a SHA checksum for each file and then manually match it with the given checksum `fba9f49bf22aa7188a155768ab0dfdc1f9b86c47976cd0f7c9003af2e20598f7`. 
Instead, I used the command `sha256sum * | grep fba9f49bf22aa7188a155768ab0dfdc1f9b86c47976cd0f7c9003af2e20598f7` which gave the output as `fba9f49bf22aa7188a155768ab0dfdc1f9b86c47976cd0f7c9003af2e20598f7 87590c24`.
After finding the required file, I navigated to the `home` directory using `cd ~` command and there I executed the `decrypt.sh` shell script using `decrypt.sh files/87590c24` command which led me to the flag: `picoCTF{trust_but_verify_87590c24}`.

# Scan Surprise

## Description
I've gotten bored of handing out flags as text. Wouldn't it be cool if they were an image instead?
You can download the challenge files here:
- challenge.zip

Additional details will be available after launching your challenge instance.

## Attachments
- https://artifacts.picoctf.net/c_atlas/15/challenge.zip
- The same files are accessible via SSH here: `ssh -p 58976 ctf-player@atlas.picoctf.net`
- Use the password `1db87a14`. Remember, in a shell, passwords are hidden!
- Accept the fingerprint with `yes`, and `ls` once connected to begin.

## Hints
- QR codes are a way of encoding data. While they're most known for storing URLs, they can store other things too.
- Mobile phones have included native QR code scanners in their cameras since version 8 (Oreo) and iOS 11
- If you don't have access to a phone, you can also use zbar-tools to convert an image to text

## Writeup
Upon examining the QR code in the image, I noticed that it was neither altered nor tampered with and was easily scannable.
Scanning it revealed the flag: `picoCTF{p33k_@_b00_19eccd10}`.

# Secret of the Polyglot

## Description
The Network Operations Center (NOC) of your local institution picked up a suspicious file, they're getting conflicting information on what type of file it is. They've brought you in as an external expert to examine the file. Can you extract all the information from this strange file?
Download the suspicious file here.

## Attachment
https://artifacts.picoctf.net/c_titan/97/flag2of2-final.pdf

## Hint
This problem can be solved by just opening the file in different ways

## Writeup
After reading the challenge description and the given hint, I realized that I needed to tweak the file extension to extract relevant information.
Upon opening the document with `.pdf` extension, I found one half of the flag: `1n_pn9_&_pdf_724b1287}`.
Then I changed the file extension to `.jpg`, which revealed the other half of the flag: `picoCTF{f1u3n7_`.
Combining both halves led me to the complete flag: `picoCTF{f1u3n7_1n_pn9_&_pdf_724b1287}`.

# CanYouSee

## Description
How about some hide and seek?
Download this file here.

## Attachment
https://artifacts.picoctf.net/c_titan/130/unknown.zip

## Hints
- How can you view the information about the picture?
- If something isn't in the expected form, maybe it deserves attention?

## Writeup
Upon viewing the image, I assumed it was connected to a movie or series. 
I searched all over the Internet but found nothing pertinent to the challenge. 
Consequently, I began analyzing the image's information and metadata using the online data viewer at `https://www.metadata2go.com`, which led me to a base64 encoded string `cGljb0NURntNRTc0RDQ3QV9ISUREM05fNmE5ZjVhYzR9Cg==` present as `attribution_url`.
I then decoded it using the online decoder found at `https://base64.guru/converter/decode/text`, which led me to the flag: `picoCTF{ME74D47A_HIDD3N_6a9f5ac4}`.
