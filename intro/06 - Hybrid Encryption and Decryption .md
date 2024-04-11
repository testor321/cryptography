# Hybrid Encryption and Decryption

## Generate a passphrase key. See num bytes is little less than 256

openssl rand -out passphrase.key 245

## AES Encrypt Large data using generated passphrase

openssl enc -aes-256-cbc -kfile passphrase.key -md sha256 -base64 -pbkdf2 -in dataimage.png -out dataimage-aes

## RSA Encrypt the passphrase

openssl pkeyutl -encrypt -pubin -inkey bob-public.pem -in passphrase.key -out passphrase_enc.key

## Send the dataimage-aes and passphrase_enc.key across

## Bob RSA Decrypts the passphrase

openssl pkeyutl -decrypt -inkey bob-private.pem -in passphrase_enc.key -out passphrase.key

## Bob will AES Decrypt the data using the passphrase

openssl enc -d -aes-256-cbc -kfile passphrase.key -md sha256 -base64 -pbkdf2 -in dataimage-aes -out dataimage_original.png
