# Resource Owner Password Grant Type

## Create a Client of type Resource Owner Password Grant Type

```less
To create an application with Resource Owner Password grant type, do the following
From Applications page, click on "Create App Integration"
Select sign-on method as 'OIDC - OpenID Connect'
Select Application Type as 'Native Application'
Enter information on this page as in the Deep Dive for Resource Owner Password grant
    Name 
    Grant types allowed 
    Select Controlled access and 'Allow everyone in your organization to access'
    Click Save
```

## STEP 1 : Construct a Token Request for username and password

```less
ENDPOINT => https://dev-74235182.okta.com/oauth2/default/v1/token
HTTP TYPE  => POST

grant_type=password
client_id=0oagk4uuodqW61EgL5d7
client_secret
username=stathell@yandex.ru
password=
scope=openid profile email offline_access fakebookapi.read fakebookapi.admin
```

## STEP 2 : Send Token Request and extract Token

## STEP 3 : Send a FakeBookAPI request (Get All Books)

```less
ENDPOINT
HTTP TYPE  

{Pass Bearer token in header}
```

## STEP 4 : Send a FakeBookAPI request (Get one Books)

```less
ENDPOINT
HTTP TYPE  

{Pass Bearer token in header}
```

## STEP 5 : Send a FakeBookAPI request (Create a book)

```less
ENDPOINT
HTTP TYPE  

{Pass Bearer token in header}
{Pass JSON in BODY}
```
