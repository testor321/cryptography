# Use postman (intro)

## Authentication

Copy the bearer token to the Authentication field to be explicit about where to include the token

Alternatively create a global variable (say JWT-TOKEN) and use the variable in all requests {{JWT-TOKEN}}. Then just set the variable JWT-TOKEN with the correct bearer token whenever needed.

The documentation for Postman is at the following location.

[Introduction | Postman Learning Center](https://learning.postman.com/docs/getting-started/introduction/)

[Download Postman | Try Postman for Free](https://www.postman.com/downloads/)

## STEP 1 : Construct Authorization Request for grant type = Authorization code

```less
ENDPOINT   => https://accounts.google.com/o/oauth2/v2/auth
HTTP TYPE  => GET
```

```sh
https://developers.google.com/identity/protocols/oauth2
https://developers.google.com/identity/protocols/oauth2/scopes
https://developers.google.com/identity/protocols/oauth2/scopes#photoslibrary
  https://www.googleapis.com/auth/photoslibrary.readonly
```

```sh
response_type=code
client_id=
scope=openid profile email https://www.googleapis.com/auth/photoslibrary.readonly
state=state123 (custom, non-default)
redirect_uri=http://localhost:8080
access_type=offline
prompt=consent
```

```curl
https://accounts.google.com/o/oauth2/v2/auth?response_type=code&client_id=CLIENT_ID&scope=openid%20profile%20email%20https://www.googleapis.com/auth/photoslibrary.readonly&state=state123&redirect_uri=http://localhost:8080&access_type=offline&prompt=consent
```

## STEP 2 : Send Authorization Request and extract Code

=> Start the Web Server (Optional)

```sh
python.exe -m http.server 8080
```

=> Use Google Chrome to send request and capture the Authorization code

code=.....

## STEP 3 : Construct a Token Request

postman

Collections/gphoto reader OAuth2/Get Token

```text
ENDPOINT   => https://oauth2.googleapis.com/token
HTTP TYPE  => POST
```

```less
grant_type=authorization_code
client_id=
client_secret=
code=
redirect_uri=http://localhost:8080
```

## STEP 4 : Send Token Request and extract Token

=> Note that Google does not return Access Token as JWT token (ID Token is returned as JWT)

```json
{
    "access_token": "",
    "expires_in": 3598,
    "refresh_token": "",
    "scope": "https://www.googleapis.com/auth/userinfo.profile https://www.googleapis.com/auth/photoslibrary.readonly openid https://www.googleapis.com/auth/userinfo.email",
    "token_type": "Bearer",
    "id_token": ""
}
```

## STEP 5 : Send Google Photos API Request - Get All Albums

```less
https://developers.google.com/photos/library/reference/rest/v1/albums/list
GET https://photoslibrary.googleapis.com/v1/albums
ENDPOINT   => https://photoslibrary.googleapis.com/v1/albums
HTTP TYPE  =>  GET

+ Authotization - Type: Bearer Token = access token
```

## STEP 6 : Send Google Photos API Request - Get one Album

```less
ENDPOINT   => https://photoslibrary.googleapis.com/v1/albums/AEdbX8UrISleTu-EF9K9hPgeUKGllwBcZjqPwCpulKZ5rGh9WodMj56PKYjsgyM_JpHrzn-Ups4j
HTTP TYPE  =>  GET
+ Authotization - Type: Bearer Token = access token
```

## STEP 7 : Send Google Photos API Request - See Photos of an Album

```less
ENDPOINT   => https://photoslibrary.googleapis.com/v1/mediaItems:search
HTTP TYPE  => POST
+ Authotization - Type: Bearer Token = access token
+ Body - raw - JSON ->

{
  "albumId": "album ID"
}
```

Request body

```json
{
  "albumId": string,
  "pageSize": integer,
  "pageToken": string,
  "filters": {
    object (Filters)
  },
  "orderBy": string
}
```

WAIT for more than 1 hour and demonstrate that the access token is invalid

## STEP 8 : Get Token Info (should fail because token has expired)

*** This is used by the Resource Server

```less
ENDPOINT   => https://www.googleapis.com/oauth2/v1/tokeninfo
HTTP TYPE  => POST

Body -> x-www-form-encoded
access_token=
```

```json
{
    "error": "invalid_token",
    "error_description": "Invalid Value"
}
```

## STEP 8 : Refresh Token

```less
ENDPOINT   => https://oauth2.googleapis.com/token
HTTP TYPE  =>  

grant_type=refresh_token
client_id=
client_secret=
refresh_token=
```

=> Get a new access token and call the API

## STEP 9 : Send User Info Request

*** This is used by the Client only if access token has openid scope

```less
ENDPOINT   => https://openidconnect.googleapis.com/v1/userinfo
HTTP TYPE  =>  GET

Auth Header => bearer roken
```

## STEP 10 : Send request to get JWKS

```less
# decode JWT token
https://jwt.io
# decode public key
https://8gwifi.org/jwkconvertfunctions.jsp

ENDPOINT   => https://www.googleapis.com/oauth2/v3/certs
HTTP TYPE  =>
```
