---
title: CodeLogic API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

Welcome to the CodeLogic API! You can use our API to access CodeLogic API endpoints.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

## Register for access
Register with CodeLogic to get access URL's for testing, use the baseUrl that is provided to access the API calls. 

# Authenticate
These are set of methods that are called for authenticating the user on CodeLogic servers
## Authenticate
To authenticate into CodeLogic server.

`
/authenticate?username={{username}}&password={{password}}
`

> API call

```shell
wget --no-check-certificate --quiet \
  --method POST \
  --timeout=0 \
  --header '' \
   '{baseUrl}/authenticate?username={{username}}&password={{password}}'
```

```javascript
var requestOptions = {
  method: 'POST',
  redirect: 'follow'
};

fetch("{baseUrl}/authenticate?username={{username}}&password={{password}}", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
};
```

Return value from API
<aside class="notice">
{
   "access_token":"eyJhbGciOiJSUzI1N-----UUjw",
   "expires_in":28799,
   "token_type":"Bearer",
   "userId":"1830468e-0d24-4e58-9f1d-6c5136b8548a"
}
</aside>

# History
History API is for getting 
## Get Audit history dates
> To get the list of all audit settings:

```shell
curl --location --request GET '{baseUrl}/audit/history/{cdoId}/dates?page=0&size=10' \
--header 'Content-Type: application/json' \
--data-raw '{
	"name" : "Any Database Added",
	"ruleType" : "Added",
	"firstNode" : "Database"
}'
```

```javascript
var settings = {
  "url": "{baseUrl}/audit/history/{cdoId}/dates?page=0&size=10",
  "method": "GET",
  "timeout": 0,
  "headers": {
    "Content-Type": "application/json"
  },
  "data": JSON.stringify({"name":"Any Database Added","ruleType":"Added","firstNode":"Database"}),
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```
> To get the correct value for `cdold` you will need to use `Authenticate` API with the username and password to get the value of `cdold`.  

> The above command returns JSON structured like this:

```json
{
	"name" : "Any Database Added",
	"ruleType" : "Added",
	"firstNode" : "Database"
}
```
### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
cdoId |  | An example is 68bcd5a4-5707-32a5-b500-77b6467180ca

<aside class="success">
Will list all the audit dates
</aside>

## GET Audit History Ids For Date

To get the list of audit settings added for a particular date

```shell
curl --location --request GET '{baseUrl}/audit/history/:cdoId/ids?page=0&size=5&date=2020-09-28' \
--header 'Content-Type: application/json' \
--data-raw '{
	"name" : "Any Database Added",
	"ruleType" : "Added",
	"firstNode" : "Database"
}'
```

```javascript
var settings = {
  "url": "{baseUrl}/audit/history/:cdoId/ids?page=0&size=5&date=2020-09-28",
  "method": "GET",
  "timeout": 0,
  "headers": {
    "Content-Type": "application/json"
  },
  "data": JSON.stringify({"name":"Any Database Added","ruleType":"Added","firstNode":"Database"}),
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```

To get the correct value for `cdold` you will need to use `Authenticate` API with the username and password to get the value of `cdold`.  


# Rules
# Matches

# FusionAuth
# AuthController
# Dependency
# Ingestion