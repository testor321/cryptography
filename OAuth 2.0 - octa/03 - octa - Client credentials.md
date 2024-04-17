
# Client credentials

## Create a Client of type Client Credentials Grant Type

```less
To create an application with Client Credentials grant type, do the following

Applications -> Applications
    Create App Integration

Select sign-on method as 'API Services'
Enter an App Integration Name 'FakebookCron'
Click 'Save'
```

## STEP 1 : Construct a Token Request for Client credentials

```less
ENDPOINT => https://dev-74235182.okta.com/oauth2/default/v1/token
HTTP TYPE => POST

grant_type=client_credentials
client_id=
client_secret=
scope=fakebookapi.read
```

## STEP 2 : Send Token Request and extract Token

## STEP 3 : Send a FakeBookAPI request (Get All Books)

```less
ENDPOINT   => http://localhost:8080/books
HTTP TYPE  => GET

{Pass Bearer token in header}
```

## STEP 4 : Send a FakeBookAPI request (Get one Books)

```less
ENDPOINT  => http://localhost:8080/books/1
HTTP TYPE  => GET

{Pass Bearer token in header}
```

## STEP 5 : Send a FakeBookAPI request (Create a book)

```less
ENDPOINT => http://localhost:8080/books
HTTP TYPE => POST

{Pass Bearer token in header}
{Pass JSON in BODY}
{
    "id": 6,
    "title": "book",
    "author": "author",
    "cost": 17.99,
    "numPages": 1000
}
```

## STEP 6 : Introspect

```less

ENDPOINT => https://dev-74235182.okta.com/oauth2/default/v1/introspect
HTTP TYPE =>

client_id
client_secret
token
```

## STEP 7 : Send request to get JSON Web Key Set URL (JWKS Url)

```less
ENDPOINT   
HTTP TYPE  
```

## STEP 8 : userinfo

```less
ENDPOINT   
HTTP TYPE  

{Pass Bearer token in header}
```
