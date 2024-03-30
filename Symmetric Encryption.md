# openssl enc for symmetric encryption and decryption 

## Help 
openssl enc -help 

## List of Ciphers
openssl enc -list

## AES encryption with secret hashed with SHA1. Salt is added automatically 
-md Use digest sha1 to create key
echo -n "this is junk" |  openssl enc -aes-256-cbc -k secret -md sha1 -pbkdf2

## AES encryption with secret hashed with SHA1. Output is base64 encoded
echo -n "this is junk" |  openssl enc -aes-256-cbc -k secret -md sha1 -pbkdf2 -base64

## Encrypting a file
openssl enc -aes-256-cbc -k secret -md sha1 -base64 -pbkdf2 -in dataimage.png 

## Encrypting a file and then save to outout file
openssl enc -aes-256-cbc -k secret -md sha1 -base64 -pbkdf2 -in dataimage.png -out dataimage-enc

## Decrypting an encrypted data. Make sure size is same 
openssl enc -d -aes-256-cbc -k secret -md sha1 -base64 -pbkdf2 -in dataimage-enc -out dataimage-original.png
