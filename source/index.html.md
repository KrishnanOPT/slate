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
## Purpose
To get the login access token
## Pre-Requisites
You will need valid username and password combination.
## Call
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
To authenticate into CodeLogic server.
`
/authenticate?username={{username}}&password={{password}}
`
## Return Values
> Return value from API

```json
{
   "access_token":"eyJhbGciOiJSUzI1N-----UUjw",
   "expires_in":28799,
   "token_type":"Bearer",
   "userId":"1830468e-0d24-4e8-9f1d-6c5136b8548a"
}
```
### 404
When API call is not reachable
### 401
Server is too slow
# History
History API's are used for getting historical audit trails 
## Audit history dates
>API Call

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
> Return Values
```json
{
	"name" : "Any Database Added",
	"ruleType" : "Added",
	"firstNode" : "Database"
}
```

### Call
To get the list of all audit settings:

`
/audit/history/:cdoId/dates?page=0&size=10
`
### Purpose
To get the audit dates
### Pre-Requisites
You will need a valid cdoid
### Return Values
### Open Queries
* not clear what audit dates mean
* are these the dates when an governance rule is run
* list of errors returned by API 
* Result in JSON format
* How to get CDOID

## Audit History Ids For Date
>API Call

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

### Purpose
To get the list of audit settings added for a particular date
### Pre-Requisites
You will need a valid cdoid
### Call
To get the list of all audit settings:

`
/audit/history/:cdoId/ids?page=0&size=5&date=2020-09-28
`
### Return Values
#### 404
When API call is not reachable
### Open Queries
* not clear what audit dates mean
* are these the dates when an governance rule is run
* list of errors returned by API 
* Result in JSON format
* How to get CDOID

## Audit CDO for Id
>API Call

```shell
curl --location -g --request GET '{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/audit/snapshot/68bcd5a4-5707-32a5-b500-77b6467180ca' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Ing5cXo4QV9aZkpXWjJKMTFEV3VWSkFTdGZuRSJ9.eyJhdWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJleHAiOjE2MTI0OTE0MTksImlhdCI6MTYxMjQ2MjYxOSwiaXNzIjoiY29kZWxvZ2ljLmNvbSIsInN1YiI6IjE4MzA0NjhlLTBkMjQtNGU1OC05ZjFkLTZjNTEzNmI4NTQ4YSIsImp0aSI6IjA1MmFjOWNkLWY3MmYtNDVlNC1hOWJlLWQ1NTU0ZGYwZjgyNCIsImF1dGhlbnRpY2F0aW9uVHlwZSI6IlBBU1NXT1JEIiwiZW1haWwiOiJ0ZW1wb3JhcnlhZG1pbkBjb2RlbG9naWMuY29tIiwiZW1haWxfdmVyaWZpZWQiOnRydWUsImFwcGxpY2F0aW9uSWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJyb2xlcyI6WyJDb2RlTG9naWMgLSBBZG1pbiJdfQ.YLs2VGrhPWxJaNpoy0fmgenCCsyxnNM3kwC8ZuOtT4G6K-Bkw-ggeTu_AXnNIxmdX_JBhTzurefRs0Df4krOyQi7kMxRqMIcTS71i57UUu3vSKdyueq9HU6SpAAvOmEZbUFxAB5_ZkMAbve9JGwjNhKlzASsgQe-PGfqDhhRrzvSlmARAwIkXrX2nhQKgKAVENGU5gg5P5rM3Acn5TAohwna3de4AiGXd1ynsYUFHbmqDtmx5NkfNIHgo9_UZKppGtZQqE7wFENhOWQJxokutba9yV7njbOds2xrMDtIXjAJjvYuIXxyPSh0V71GiMwMPEdNVxl-o_yvZ1-IAPVc_g' \
--data-raw ''
```

```javascript
var settings = {
  "url": "{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/audit/snapshot/68bcd5a4-5707-32a5-b500-77b6467180ca",
  "method": "GET",
  "timeout": 0,
  "headers": {
    "Content-Type": "application/json",
    "Authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Ing5cXo4QV9aZkpXWjJKMTFEV3VWSkFTdGZuRSJ9.eyJhdWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJleHAiOjE2MTI0OTE0MTksImlhdCI6MTYxMjQ2MjYxOSwiaXNzIjoiY29kZWxvZ2ljLmNvbSIsInN1YiI6IjE4MzA0NjhlLTBkMjQtNGU1OC05ZjFkLTZjNTEzNmI4NTQ4YSIsImp0aSI6IjA1MmFjOWNkLWY3MmYtNDVlNC1hOWJlLWQ1NTU0ZGYwZjgyNCIsImF1dGhlbnRpY2F0aW9uVHlwZSI6IlBBU1NXT1JEIiwiZW1haWwiOiJ0ZW1wb3JhcnlhZG1pbkBjb2RlbG9naWMuY29tIiwiZW1haWxfdmVyaWZpZWQiOnRydWUsImFwcGxpY2F0aW9uSWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJyb2xlcyI6WyJDb2RlTG9naWMgLSBBZG1pbiJdfQ.YLs2VGrhPWxJaNpoy0fmgenCCsyxnNM3kwC8ZuOtT4G6K-Bkw-ggeTu_AXnNIxmdX_JBhTzurefRs0Df4krOyQi7kMxRqMIcTS71i57UUu3vSKdyueq9HU6SpAAvOmEZbUFxAB5_ZkMAbve9JGwjNhKlzASsgQe-PGfqDhhRrzvSlmARAwIkXrX2nhQKgKAVENGU5gg5P5rM3Acn5TAohwna3de4AiGXd1ynsYUFHbmqDtmx5NkfNIHgo9_UZKppGtZQqE7wFENhOWQJxokutba9yV7njbOds2xrMDtIXjAJjvYuIXxyPSh0V71GiMwMPEdNVxl-o_yvZ1-IAPVc_g"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```

### Purpose
To get the list of CDOID's
### Pre-Requisites
You will need a valid cdoid
### Call
To get the list of ??

`
/audit/snapshot/:id
`
### Return Values
#### 404
When API call is not reachable
### Open Queries
* not clear what audit dates mean
* are these the dates when an governance rule is run
* list of errors returned by API 
* Result in JSON format
* How to get id

## Audit History
>API Call

```shell
curl --location -g --request GET '{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/audit/history/68bcd5a4-5707-32a5-b500-77b6467180ca' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Ing5cXo4QV9aZkpXWjJKMTFEV3VWSkFTdGZuRSJ9.eyJhdWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJleHAiOjE2MDE2ODA1MjksImlhdCI6MTYwMTY1MTcyOSwiaXNzIjoiY3Jvc3Njb2RlLmNvbSIsInN1YiI6IjE4MzA0NjhlLTBkMjQtNGU1OC05ZjFkLTZjNTEzNmI4NTQ4YSIsImp0aSI6IjQ4ZjA4NzllLWRmNjctNGNkYS04NWVlLWI5NGNkNzI0MWFhNyIsImF1dGhlbnRpY2F0aW9uVHlwZSI6IlBBU1NXT1JEIiwiZW1haWwiOiJmdXNpb25hdXRoYWRtaW5AY3Jvc3Njb2RlLmNvbSIsImVtYWlsX3ZlcmlmaWVkIjp0cnVlLCJhcHBsaWNhdGlvbklkIjoiN2ZkMzI2ODAtNzAwZS00YmZjLTlhYzAtYmI3ZTE3ZjYzYjcwIiwicm9sZXMiOlsiTmVvNGNhcGUgLSBBZG1pbiJdfQ.lYGlbA4UG1NUhqcA_McKgs-X6LJUBAGAAVaDx-ItZrTJohXXtPnH70UR905E6Js78R75e76JYQDlsi-9eiqUBnZLcj4-_Xwgz1VR1XutnabDIkxLACxOo1F_LQTn1gU-U_ul-jJdM2g5x-ojv4er6fyHFj3S7BXPISwefLDYvm6DyHBi7AcbZMqrQJXbKuBko0RQKJwAVffeaL1mzeXMd1BFfLpAWHCF_al4I9ojZa3uuZsHQP6v3YD_wwq8XbTbewhBblDj95n_kJQaCa5HGr2OP6KrupY0ZWe0r2KYm8T6XKIeqI0AvuZcfuD5xT_eCwXpD0TYKSdDq1KwpioCiw' \
--data-raw ''
```

```javascript
var settings = {
  "url": "{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/audit/history/68bcd5a4-5707-32a5-b500-77b6467180ca",
  "method": "GET",
  "timeout": 0,
  "headers": {
    "Content-Type": "application/json",
    "Authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Ing5cXo4QV9aZkpXWjJKMTFEV3VWSkFTdGZuRSJ9.eyJhdWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJleHAiOjE2MDE2ODA1MjksImlhdCI6MTYwMTY1MTcyOSwiaXNzIjoiY3Jvc3Njb2RlLmNvbSIsInN1YiI6IjE4MzA0NjhlLTBkMjQtNGU1OC05ZjFkLTZjNTEzNmI4NTQ4YSIsImp0aSI6IjQ4ZjA4NzllLWRmNjctNGNkYS04NWVlLWI5NGNkNzI0MWFhNyIsImF1dGhlbnRpY2F0aW9uVHlwZSI6IlBBU1NXT1JEIiwiZW1haWwiOiJmdXNpb25hdXRoYWRtaW5AY3Jvc3Njb2RlLmNvbSIsImVtYWlsX3ZlcmlmaWVkIjp0cnVlLCJhcHBsaWNhdGlvbklkIjoiN2ZkMzI2ODAtNzAwZS00YmZjLTlhYzAtYmI3ZTE3ZjYzYjcwIiwicm9sZXMiOlsiTmVvNGNhcGUgLSBBZG1pbiJdfQ.lYGlbA4UG1NUhqcA_McKgs-X6LJUBAGAAVaDx-ItZrTJohXXtPnH70UR905E6Js78R75e76JYQDlsi-9eiqUBnZLcj4-_Xwgz1VR1XutnabDIkxLACxOo1F_LQTn1gU-U_ul-jJdM2g5x-ojv4er6fyHFj3S7BXPISwefLDYvm6DyHBi7AcbZMqrQJXbKuBko0RQKJwAVffeaL1mzeXMd1BFfLpAWHCF_al4I9ojZa3uuZsHQP6v3YD_wwq8XbTbewhBblDj95n_kJQaCa5HGr2OP6KrupY0ZWe0r2KYm8T6XKIeqI0AvuZcfuD5xT_eCwXpD0TYKSdDq1KwpioCiw"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```

### Purpose
To get the list of history logs for a CDOID
### Pre-Requisites
You will need a valid cdoid
### Call
To get the list of ??

`
/audit/history/:cdoId
`
### Return Values
#### 404
When API call is not reachable
### Open Queries
* not clear what audit dates mean
* are these the dates when an governance rule is run
* list of errors returned by API 
* Result in JSON format
* How to get id

# Rules
## Audit Rule - Create
>API Call

```shell
curl --location -g --request GET '{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/audit/history/68bcd5a4-5707-32a5-b500-77b6467180ca' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Ing5cXo4QV9aZkpXWjJKMTFEV3VWSkFTdGZuRSJ9.eyJhdWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJleHAiOjE2MDE2ODA1MjksImlhdCI6MTYwMTY1MTcyOSwiaXNzIjoiY3Jvc3Njb2RlLmNvbSIsInN1YiI6IjE4MzA0NjhlLTBkMjQtNGU1OC05ZjFkLTZjNTEzNmI4NTQ4YSIsImp0aSI6IjQ4ZjA4NzllLWRmNjctNGNkYS04NWVlLWI5NGNkNzI0MWFhNyIsImF1dGhlbnRpY2F0aW9uVHlwZSI6IlBBU1NXT1JEIiwiZW1haWwiOiJmdXNpb25hdXRoYWRtaW5AY3Jvc3Njb2RlLmNvbSIsImVtYWlsX3ZlcmlmaWVkIjp0cnVlLCJhcHBsaWNhdGlvbklkIjoiN2ZkMzI2ODAtNzAwZS00YmZjLTlhYzAtYmI3ZTE3ZjYzYjcwIiwicm9sZXMiOlsiTmVvNGNhcGUgLSBBZG1pbiJdfQ.lYGlbA4UG1NUhqcA_McKgs-X6LJUBAGAAVaDx-ItZrTJohXXtPnH70UR905E6Js78R75e76JYQDlsi-9eiqUBnZLcj4-_Xwgz1VR1XutnabDIkxLACxOo1F_LQTn1gU-U_ul-jJdM2g5x-ojv4er6fyHFj3S7BXPISwefLDYvm6DyHBi7AcbZMqrQJXbKuBko0RQKJwAVffeaL1mzeXMd1BFfLpAWHCF_al4I9ojZa3uuZsHQP6v3YD_wwq8XbTbewhBblDj95n_kJQaCa5HGr2OP6KrupY0ZWe0r2KYm8T6XKIeqI0AvuZcfuD5xT_eCwXpD0TYKSdDq1KwpioCiw' \
--data-raw ''
```

```javascript
var settings = {
  "url": "{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/audit/history/68bcd5a4-5707-32a5-b500-77b6467180ca",
  "method": "GET",
  "timeout": 0,
  "headers": {
    "Content-Type": "application/json",
    "Authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Ing5cXo4QV9aZkpXWjJKMTFEV3VWSkFTdGZuRSJ9.eyJhdWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJleHAiOjE2MDE2ODA1MjksImlhdCI6MTYwMTY1MTcyOSwiaXNzIjoiY3Jvc3Njb2RlLmNvbSIsInN1YiI6IjE4MzA0NjhlLTBkMjQtNGU1OC05ZjFkLTZjNTEzNmI4NTQ4YSIsImp0aSI6IjQ4ZjA4NzllLWRmNjctNGNkYS04NWVlLWI5NGNkNzI0MWFhNyIsImF1dGhlbnRpY2F0aW9uVHlwZSI6IlBBU1NXT1JEIiwiZW1haWwiOiJmdXNpb25hdXRoYWRtaW5AY3Jvc3Njb2RlLmNvbSIsImVtYWlsX3ZlcmlmaWVkIjp0cnVlLCJhcHBsaWNhdGlvbklkIjoiN2ZkMzI2ODAtNzAwZS00YmZjLTlhYzAtYmI3ZTE3ZjYzYjcwIiwicm9sZXMiOlsiTmVvNGNhcGUgLSBBZG1pbiJdfQ.lYGlbA4UG1NUhqcA_McKgs-X6LJUBAGAAVaDx-ItZrTJohXXtPnH70UR905E6Js78R75e76JYQDlsi-9eiqUBnZLcj4-_Xwgz1VR1XutnabDIkxLACxOo1F_LQTn1gU-U_ul-jJdM2g5x-ojv4er6fyHFj3S7BXPISwefLDYvm6DyHBi7AcbZMqrQJXbKuBko0RQKJwAVffeaL1mzeXMd1BFfLpAWHCF_al4I9ojZa3uuZsHQP6v3YD_wwq8XbTbewhBblDj95n_kJQaCa5HGr2OP6KrupY0ZWe0r2KYm8T6XKIeqI0AvuZcfuD5xT_eCwXpD0TYKSdDq1KwpioCiw"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```
> Return Values

```{"status":"success","data":[{"name":"Krishnan_Audi","createdOn":"2021-02-05T12:50:46.186","firstNode":"Any","firstNodePropertyWatches":[],"firstNodeFilters":[{"id":"67f39a94-92e9-3822-b284-1246bab1b3a8"}],"ruleType":"Added","secondNodeFilters":[]},{"name":"Created By Automation","createdOn":"2021-02-01T13:23:49.685","firstNode":"Application","firstNodePropertyWatches":[],"firstNodeFilters":[],"ruleType":"Added","secondNodeFilters":[]}]}```

### Purpose
To get the create a new rule
### Pre-Requisites
You will need a valid session
### Call
To get the list of ??

`
/audit/rule
`
### Return Values
#### 404
When API call is not reachable
### Open Queries
* I had to pass page and size as well to get this working
* It returned an already created rule, so not sure how it creates a rule.
* list of errors returned by API 


# Matches

# FusionAuth
# AuthController
# Dependency
# Ingestion