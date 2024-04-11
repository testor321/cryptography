# Asymmetric Encryption & Decryption

## Create a certificate request && Create a private key and self signed certificate

openssl req -x509 -nodes -sha256 -days 3650 -newkey rsa:2048 -keyout private.key -out certificate.crt
> -nodes - don't encrypt the private key
> -newkey rsa:2048

## openssl genrsa

generates a RSA private key

## Help

openssl genrsa -help

## Create a RSA private key of size 2048

openssl genrsa -out alice-private.pem 2048\
openssl genrsa -out bob-private.pem 2048

## Encrypted. it will ask for secret

openssl genrsa -aes256 -out private_enc.pem 2048

## Create public key

will ask for secret if encrypted

openssl rsa -in alice-private.pem -pubout -out alice-public.pem\
openssl rsa -in bob-private.pem -pubout -out bob-public.pem

## The pkeyutl command can be used to perform low-level public key operations using any ## supported algorithm. encrypted using rsa

echo "Run for your life Now!" > important.txt

## Alice wants to send to bob. So encrypt using bob's public key

openssl pkeyutl -encrypt -pubin -inkey bob-public.pem -in important.txt -out important.enc

if important.txt is > key size we will have issue

## Bob will decrypt it using his private key

openssl pkeyutl -decrypt -inkey bob-private.pem -in important.enc
