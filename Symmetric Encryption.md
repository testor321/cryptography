# openssl enc for symmetric encryption and decryption

## Help

openssl enc -help

## List of Ciphers

openssl enc -list

## AES encryption with secret hashed with SHA512. Salt is added automatically

echo -n "this is junk" |  openssl enc -aes-256-cbc -k secret -md sha512 -pbkdf2

> -md Use digest sha1 to create key. The default algorithm is sha-256\
> -pbkdf2 Use password-based key derivation function 2

## AES encryption with secret hashed with SHA512. Output is base64 encoded

echo -n "this is junk" |  openssl enc -aes-256-cbc -k secret -md sha512 -pbkdf2 -base64

## Encrypting a file

openssl enc -aes-256-cbc -k secret -md sha256 -base64 -pbkdf2 -in dataimage.png

## Encrypting a file and then save to outout file

openssl enc -aes-256-cbc -k secret -md sha256 -base64 -pbkdf2 -in dataimage.png -out dataimage-enc

## Decrypting an encrypted data. Make sure size is same

openssl enc -d -aes-256-cbc -k secret -md sha256 -base64 -pbkdf2 -in dataimage-enc -out dataimage-original.png

## Other examples

The Advanced Encryption Standard (AES), is a block cipher adopted as an encryption standard by the U.S. government for military and government use. There are a few different cipher methods available for use in AES, the most commonly used ones are ECB and CBC.

ECB (Electronic Codebook) is essentially the first generation of the AES. It is the most basic form of block cipher encryption.

CBC (Cipher Blocker Chaining) is an advanced form of block cipher encryption. With CBC mode encryption, each ciphertext block is dependent on all plaintext blocks processed up to that point. This adds an extra level of complexity to the encrypted data.

We are going to use CBC for this example which requires both a Key and an Initialization Vector (IV). An initialization vector is a random number used in combination with a secret key as a means to encrypt data. This number is sometimes referred to as a nonce, or "number occuring once" as an encryption program uses it only once per session. The Key and IV need to be passed to the OpenSSL-ENC command in hex format.

The in AES-128, the key MUST have a length that is a multiple of 16, but the IV can be any length as it is really more like an inital offset value.

> echo -n 'thiskeyis16chars' | od -A n -t x1 |sed 's/ //g'
>>746869736b6579697331366368617273
>
> echo -n 'mynonrandomiv' | od -A n -t x1 |sed 's/ //g'
>>6d796e6f6e72616e646f6d6976

We now have our Key in HEX value: 746869736b6579697331366368617273
And our IV in HEX value: 6d796e6f6e72616e646f6d6976

So lets use them to encrypt a secret message: mysecretmessage

Here is a quick test of the Openssl-enc command for encrypting data using AES128:

> echo mysecretmessage | openssl enc -e -aes-128-cbc -K 746869736b6579697331366368617273 -iv 6d796e6f6e72616e646f6d6976 -nosalt -nopad -base64 -p
>>key=746869736B6579697331366368617273\
>>iv=6D796E6F6E72616E646F6D6976000000\
>>Js9rW0xBiQURttTdWSPqVg==

The message was encrypted and returned the cipher text in a base64 format as: Js9rW0xBiQURttTdWSPqVg==

Now lets use our key and IV to decrypt this message:

> echo Js9rW0xBiQURttTdWSPqVg== | openssl enc -d -aes-128-cbc -K 746869736b6579697331366368617273 -iv 6d796e6f6e72616e646f6d6976 -nopad -nosalt -base64 -p
>> key=746869736B6579697331366368617273
>> iv=6D796E6F6E72616E646F6D6976000000
>> mysecretmessage

Our base64 cipher text has now been decrypted to the plain-text value: **mysecretmessage**
