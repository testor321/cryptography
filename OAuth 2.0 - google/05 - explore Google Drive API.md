# explore Google drive API

## STEP 1: From your Google Developer Console, create a client ID and client secret

```less
client_id=
client_secret=
```

## STEP 2 : Find the Service Endpoint and Scope needed to call the Google Drive API

```less
Service Endpoint = https://www.googleapis.com/drive/v3/files
Scopes = https://www.googleapis.com/auth/drive.metadata.readonly
```less

## STEP 3 : Construct Authorization Request to send to the Google Authorization Server 

```less
code_verifier = This is a test code verifier

ENDPOINT   => https://accounts.google.com/o/oauth2/v2/auth
HTTP TYPE  => GET

https://accounts.google.com/o/oauth2/v2/auth?

response_type=code
client_id=
scope=openid%20profile%20email%20https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fdrive.metadata.readonly
state=state123
redirect_uri=http://localhost:8080/oauth2/code/google
access_type=offline
prompt=consent
code_challenge=
code_challenge_method=S256
```

[PKCE generator tool](https://tonyxu-io.github.io/pkce-generator/)

## STEP 4 : Send Authorization Request using Chrome and extract Authorization Code

```less
=> Start the Web Server using python (Optional) 
=> Use Google Chrome to send request and capture the code

code=
```

## STEP 5 : Find the Google Token Endpoint and construct a Token Request

```less
ENDPOINT   => <find token endpoint> 
HTTP TYPE  => POST
https://oauth2.googleapis.com/token
grant_type=authorization_code
client_id=7
client_secret=
code=
redirect_uri=http://localhost:8080/oauth2/code/google
verifier=This is a test code verifier
```

## STEP 6 : Send Token Request using Postman and examine the Response

```less
access token= 

For how long is the access token valid ? 
```

## STEP 7 : Send Google Drive Request using Postman to receive all your Google Drive documents

```less
ENDPOINT   => https://www.googleapis.com/drive/v3/files
HTTP TYPE  =>  GET
```

## STEP 8 : Identify ID Token and examine contents of the JWT token using jwt.io

what user specific claims do you see in the ID Token ?

## STEP 9 : Find the User Info endpoint and send a Request to the User Info endpoint

```less
ENDPOINT   => https://openidconnect.googleapis.com/v1/userinfo
HTTP TYPE  =>  GET

After getting Response - 
    - what user specific claims do you see in the ID Token ? 
```

## STEP 10 : Find the Token Info endpoint and send a Request to the Token Info endpoint

```less
ENDPOINT   => https://www.googleapis.com/oauth2/v1/tokeninfo
HTTP TYPE  =>  POST

access_token=

After getting Response - 
    - Do you see any user claims like given_name or email in the Response ? 
    - How is it different than the UserInfo response?
```

## STEP 11 : Let Access Token expire and check that you cannot call the Drive API with expired token

```less
After getting Response - 
    - Did you get an error ? 
```
