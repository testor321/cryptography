# Hashing (Digest)

## Help

openssl dgst -help

## Default digest sha256

openssl dgst dataimage.png

openssl dgst -sha512 dataimage.png\
openssl dgst -sha512 -binary dataimage.png\
openssl dgst -sha512 -binary -out dataimage-dgst dataimage.png  

## For Text data. watch out for EOL

echo -n xxx | openssl dgst -sha512

> the same data will generate the same hash

## Password.Default salt

openssl passwd -6

> because salt will be generated/addded randomly, then hash will be differenr

## own salt

openssl passwd -6 -salt ThisIsASalt password

> because salt is static, then hash will the same
