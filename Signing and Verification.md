# Signing & Verification (Using openssl dgst)


## Create a sha512 digest from dataimage.png, signs that digest with Alice's private key
## and outputs to dataimage-digest.sign
openssl dgst -sha512 -sign alice-private.pem -out dataimage-digest.sign dataimage.png

## Create base64 representation of dataimage-digest.sign
base64 dataimage-digest.sign > dataimage-digest.sign.base64 

## Create base64 representation of dataimage.png
base64 dataimage.png > dataimage.png.base64

## Alice will send both dataimage.png.base64 and dataimage-digest.sign.base64 to Bob 

## Bob will recover dataimage.png
base64 -d dataimage.png.base64 > dataimage.png.orig

## Bob will recover dataimage-digest.sign
base64 -d dataimage-digest.sign.base64 > dataimage-digest.sign.orig

## Bob will verify signature using Alice's public key
openssl dgst -sha512 -verify alice-public.pem -signature dataimage-digest.sign.orig dataimage.png.orig

# Signing & Verification (Using openssl pkeyutl)

## Take a sha512 hash of the dataimage.png 
openssl dgst -sha512 -binary -out dataimage-digest dataimage.png 

## Alice will Sign the Hash using her private key 
openssl pkeyutl -sign -inkey alice-private.pem -in dataimage-digest -out dataimage-digest.sign

## Not shown : Alice will base 64 encode both Signature and Original Data
## Not shown : Bob will base 64 decode both Signature and Original Data

## Bob will verify signature using Alice's public key
openssl pkeyutl -verify -pubin -inkey alice-public.pem  -in dataimage-digest -sigfile dataimage-digest.sign
