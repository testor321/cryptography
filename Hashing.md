# Hashing (Digest)

## Help
openssl dgst -help

## Default digest sha256
openssl dgst dataimage.png

openssl dgst -sha512 dataimage.png
openssl dgst -sha512 -binary dataimage.png
openssl dgst -sha512 -binary -out dataimage-dgst dataimage.png  

## For Text data. watch out for EOL
echo -n xxx | openssl dgst -sha512

## Show again. Will hash to the same value. Danger
## Use of Hash in password

## Password.Default salt (show this twice)
openssl passwd -6

## own salt 
openssl passwd -6 -salt ThisIsASalt password
