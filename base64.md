# Base 64 Encoding and Decoding

## Help

base64 --help

## base64 Encoding. watch out for EOL (End Of Line) Char

> -n will not append a EOL

echo -n "This is a line" | base64

## base64 Decoding

echo -n VGhpcyBpcyBhIGxpbmU= | base64 -d

## base64 Encoding of file

base64 dataimage.png

base64 dataimage.png > dataimage-base64.txt

## Decoding

base64 -d dataimage-base64.txt > dataimage-decoded.png
