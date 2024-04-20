# PKCE extension

## STEP 1 : Construct Authorization Request

=> LOGOUT FROM THE ACCOUNT

### In reality Code verifiers must be automatically generated and long

code_verifier = This is a dumb verifier =>

```less
ENDPOINT   => https://accounts.google.com/o/oauth2/v2/auth
HTTP TYPE  => GET

https://accounts.google.com/o/oauth2/v2/auth?response_type=code&client_id=CLIENT_ID&scope=openid%20https://www.googleapis.com/auth/photoslibrary.readonly&state=state123&redirect_uri=http://localhost:8080&code_challenge=CODE_CHALLENGE&code_challenge_method=S256

response_type=code
client_id=164367926004-61e3duqcj3skc1q1f928s22v12897vcc.apps.googleusercontent.com
scope=openid%20https://www.googleapis.com/auth/photoslibrary.readonly
state
redirect_uri=http://localhost:8080
access_type=
prompt=
code_challenge=s7wFrWBVcw_zOncLadJr0Ek0OiyGpmuwMzLb5dy5Zvw
code_challenge_method=S256
```

=> code_challenge = Base64UrlEncode(SHA256Hash(CODE_VERIFIER))\
=> Use an online PKCE generator tool to do this\
=> code=

[PKCE generator tool](https://tonyxu-io.github.io/pkce-generator/)

## STEP 2 : Send Request and extract Code

=> Start the Web Server (Optional)
=> Use Google Chrome to send request and capture the code

## STEP 3 : Construct a Token Request

```less
ENDPOINT   =>
HTTP TYPE  =>

grant_type
client_id
client_secret
code
redirect_uri
verifier=
```

## STEP 4 : Send Request and extract Token

=> Note the elements of the ID token by using jwt.io

## STEP 5 : Construct Google Photos Request - Get All Albums

```less
ENDPOINT   => 
HTTP TYPE  =>  
```

## STEP 6 : Send Request and see one Album

```less
ENDPOINT   => 
HTTP TYPE  =>  
```

## STEP 7 : Send Request to see Album Photos

```less
ENDPOINT   => 
HTTP TYPE  =>  
```
