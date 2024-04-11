# Implicit grant type

## STEP 1 : Construct Authorization Request

```less
ENDPOINT   => https://accounts.google.com/o/oauth2/v2/auth
HTTP TYPE  => GET

https://accounts.google.com/o/oauth2/v2/auth?response_type=token&client_id=164367926004-61e3duqcj3skc1q1f928s22v12897vcc.apps.googleusercontent.com&scope=openid%20https://www.googleapis.com/auth/photoslibrary.readonly&state=state123&redirect_uri=http://localhost:8080
```

## STEP 2 : Send Request and extract token

=> Start the Web Server (Optional)\
=> Use Google Chrome to send request and capture the code\
=> Note that Google does not return JWT token, so it verifies using an endpoint.

## STEP 3 : Construct Google Photos Request - Get All Albums

```less
ENDPOINT   => https://photoslibrary.googleapis.com/v1/albums
HTTP TYPE  =>  GET
```

## STEP 4 : Send Request and see one Album

```less
ENDPOINT   => https://photoslibrary.googleapis.com/v1/albums/ALBUM_ID
HTTP TYPE  =>  GET
```

## STEP 5 : Send Request to see Album Photos

```less
ENDPOINT   => https://photoslibrary.googleapis.com/v1/mediaItems:search
HTTP TYPE  =>  GET
```
