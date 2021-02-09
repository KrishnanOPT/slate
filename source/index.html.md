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
curl --location -g --request POST '{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/audit/rule' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Ing5cXo4QV9aZkpXWjJKMTFEV3VWSkFTdGZuRSJ9.eyJhdWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJleHAiOjE2MTAwNjg3OTgsImlhdCI6MTYxMDAzOTk5OCwiaXNzIjoiY29kZWxvZ2ljLmNvbSIsInN1YiI6IjE4MzA0NjhlLTBkMjQtNGU1OC05ZjFkLTZjNTEzNmI4NTQ4YSIsImp0aSI6ImNlYWQ5NDMxLWMwZmUtNDMwNy1hMTExLWFlYzQ2ZWQ4ZDNmMiIsImF1dGhlbnRpY2F0aW9uVHlwZSI6IlBBU1NXT1JEIiwiZW1haWwiOiJ0ZW1wb3JhcnlhZG1pbkBjb2RlbG9naWMuY29tIiwiZW1haWxfdmVyaWZpZWQiOnRydWUsImFwcGxpY2F0aW9uSWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJyb2xlcyI6WyJDb2RlTG9naWMgLSBBZG1pbiJdfQ.KefzDKqgUaxW1n753qIzesdipR_JIoX3fXpcIRaMHCrBsT45vs0jtPOJjm9xMK_hiFnyiPysrsE1CVu4u_moGPyiXb1te5YvTUl-EgPPPtAh0AsBbcCcm06XqTxfMMKzDuMhqVX_cQ6vAqcsOQDTJmTG6lff8d78Yrc2TLkBLzwqvxpJJF048D8dPB8Qm1hSVXzaOKYVFQOR5_DLi3_NSfqMjGaf1b2jInHK-EKSpGdcWWLG2BvwgO2dCkhSskmlKTBuPjQhCiNTQ0Lm8g40TT7aKELfsNjW6PUvfZ9VK2fy0TsYJ6UK8S1iyByxDouMMTHzPt0ZtpicAgfce8nffQ' \
--data-raw '{
	"name" : "Any Application Added",
	"ruleType" : "Added",
	"firstNode" : "Application"
}'
```

```javascript
var settings = {
  "url": "{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/audit/rule",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "Content-Type": "application/json",
    "Authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Ing5cXo4QV9aZkpXWjJKMTFEV3VWSkFTdGZuRSJ9.eyJhdWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJleHAiOjE2MTAwNjg3OTgsImlhdCI6MTYxMDAzOTk5OCwiaXNzIjoiY29kZWxvZ2ljLmNvbSIsInN1YiI6IjE4MzA0NjhlLTBkMjQtNGU1OC05ZjFkLTZjNTEzNmI4NTQ4YSIsImp0aSI6ImNlYWQ5NDMxLWMwZmUtNDMwNy1hMTExLWFlYzQ2ZWQ4ZDNmMiIsImF1dGhlbnRpY2F0aW9uVHlwZSI6IlBBU1NXT1JEIiwiZW1haWwiOiJ0ZW1wb3JhcnlhZG1pbkBjb2RlbG9naWMuY29tIiwiZW1haWxfdmVyaWZpZWQiOnRydWUsImFwcGxpY2F0aW9uSWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJyb2xlcyI6WyJDb2RlTG9naWMgLSBBZG1pbiJdfQ.KefzDKqgUaxW1n753qIzesdipR_JIoX3fXpcIRaMHCrBsT45vs0jtPOJjm9xMK_hiFnyiPysrsE1CVu4u_moGPyiXb1te5YvTUl-EgPPPtAh0AsBbcCcm06XqTxfMMKzDuMhqVX_cQ6vAqcsOQDTJmTG6lff8d78Yrc2TLkBLzwqvxpJJF048D8dPB8Qm1hSVXzaOKYVFQOR5_DLi3_NSfqMjGaf1b2jInHK-EKSpGdcWWLG2BvwgO2dCkhSskmlKTBuPjQhCiNTQ0Lm8g40TT7aKELfsNjW6PUvfZ9VK2fy0TsYJ6UK8S1iyByxDouMMTHzPt0ZtpicAgfce8nffQ"
  },
  "data": JSON.stringify({"name":"Any Application Added","ruleType":"Added","firstNode":"Application"}),
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```
> Return Values

```
{"status":"success","data":[{"name":"Krishnan_Audi","createdOn":"2021-02-05T12:50:46.186","firstNode":"Any","firstNodePropertyWatches":[],"firstNodeFilters":[{"id":"67f39a94-92e9-3822-b284-1246bab1b3a8"}],"ruleType":"Added","secondNodeFilters":[]},{"name":"Created By Automation","createdOn":"2021-02-01T13:23:49.685","firstNode":"Application","firstNodePropertyWatches":[],"firstNodeFilters":[],"ruleType":"Added","secondNodeFilters":[]}]}
```

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

## Audit Rule - Disable
>API Call

```shell
curl --location -g --request PATCH '{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/audit/rule/5ff743fd168e2a315db4160a/disable' \
--header 'Content-Type: application/json' \
--data-raw ''
```

```javascript
var settings = {
  "url": "{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/audit/rule/5ff743fd168e2a315db4160a/disable",
  "method": "PATCH",
  "timeout": 0,
  "headers": {
    "Content-Type": "application/json"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```
> Return Values

```
??
```

### Purpose
To disable an existing rule
### Pre-Requisites
You will need a valid rule id
### Call
To get the list of ??

`
/audit/rule/:id/disable
`
### Return Values
#### 404
When API call is not reachable
### Open Queries
* How to identify id
* list of errors returned by API 

## Audit Rule - Enable
>API Call

```shell
curl --location -g --request PATCH '{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/audit/rule/5ff743fd168e2a315db4160a/enable' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Ing5cXo4QV9aZkpXWjJKMTFEV3VWSkFTdGZuRSJ9.eyJhdWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJleHAiOjE2MTAwNjg3OTgsImlhdCI6MTYxMDAzOTk5OCwiaXNzIjoiY29kZWxvZ2ljLmNvbSIsInN1YiI6IjE4MzA0NjhlLTBkMjQtNGU1OC05ZjFkLTZjNTEzNmI4NTQ4YSIsImp0aSI6ImNlYWQ5NDMxLWMwZmUtNDMwNy1hMTExLWFlYzQ2ZWQ4ZDNmMiIsImF1dGhlbnRpY2F0aW9uVHlwZSI6IlBBU1NXT1JEIiwiZW1haWwiOiJ0ZW1wb3JhcnlhZG1pbkBjb2RlbG9naWMuY29tIiwiZW1haWxfdmVyaWZpZWQiOnRydWUsImFwcGxpY2F0aW9uSWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJyb2xlcyI6WyJDb2RlTG9naWMgLSBBZG1pbiJdfQ.KefzDKqgUaxW1n753qIzesdipR_JIoX3fXpcIRaMHCrBsT45vs0jtPOJjm9xMK_hiFnyiPysrsE1CVu4u_moGPyiXb1te5YvTUl-EgPPPtAh0AsBbcCcm06XqTxfMMKzDuMhqVX_cQ6vAqcsOQDTJmTG6lff8d78Yrc2TLkBLzwqvxpJJF048D8dPB8Qm1hSVXzaOKYVFQOR5_DLi3_NSfqMjGaf1b2jInHK-EKSpGdcWWLG2BvwgO2dCkhSskmlKTBuPjQhCiNTQ0Lm8g40TT7aKELfsNjW6PUvfZ9VK2fy0TsYJ6UK8S1iyByxDouMMTHzPt0ZtpicAgfce8nffQ' \
--data-raw ''
```

```javascript
var settings = {
  "url": "{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/audit/rule/5ff743fd168e2a315db4160a/enable",
  "method": "PATCH",
  "timeout": 0,
  "headers": {
    "Content-Type": "application/json",
    "Authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Ing5cXo4QV9aZkpXWjJKMTFEV3VWSkFTdGZuRSJ9.eyJhdWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJleHAiOjE2MTAwNjg3OTgsImlhdCI6MTYxMDAzOTk5OCwiaXNzIjoiY29kZWxvZ2ljLmNvbSIsInN1YiI6IjE4MzA0NjhlLTBkMjQtNGU1OC05ZjFkLTZjNTEzNmI4NTQ4YSIsImp0aSI6ImNlYWQ5NDMxLWMwZmUtNDMwNy1hMTExLWFlYzQ2ZWQ4ZDNmMiIsImF1dGhlbnRpY2F0aW9uVHlwZSI6IlBBU1NXT1JEIiwiZW1haWwiOiJ0ZW1wb3JhcnlhZG1pbkBjb2RlbG9naWMuY29tIiwiZW1haWxfdmVyaWZpZWQiOnRydWUsImFwcGxpY2F0aW9uSWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJyb2xlcyI6WyJDb2RlTG9naWMgLSBBZG1pbiJdfQ.KefzDKqgUaxW1n753qIzesdipR_JIoX3fXpcIRaMHCrBsT45vs0jtPOJjm9xMK_hiFnyiPysrsE1CVu4u_moGPyiXb1te5YvTUl-EgPPPtAh0AsBbcCcm06XqTxfMMKzDuMhqVX_cQ6vAqcsOQDTJmTG6lff8d78Yrc2TLkBLzwqvxpJJF048D8dPB8Qm1hSVXzaOKYVFQOR5_DLi3_NSfqMjGaf1b2jInHK-EKSpGdcWWLG2BvwgO2dCkhSskmlKTBuPjQhCiNTQ0Lm8g40TT7aKELfsNjW6PUvfZ9VK2fy0TsYJ6UK8S1iyByxDouMMTHzPt0ZtpicAgfce8nffQ"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```
> Return Values

```
??
```

### Purpose
To enable an existing rule
### Pre-Requisites
You will need a valid rule id
### Call
To get the list of ??

`
/audit/rule/:id/enable
`
### Return Values
#### 404
When API call is not reachable
### Open Queries
* How to identify id
* list of errors returned by API 

## Audit Rules
>API Call

```shell
curl --location -g --request GET '{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/audit/rule?page=0&size=10' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Ing5cXo4QV9aZkpXWjJKMTFEV3VWSkFTdGZuRSJ9.eyJhdWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJleHAiOjE2MDE1OTIwNTAsImlhdCI6MTYwMTU2MzI1MCwiaXNzIjoiY3Jvc3Njb2RlLmNvbSIsInN1YiI6IjE4MzA0NjhlLTBkMjQtNGU1OC05ZjFkLTZjNTEzNmI4NTQ4YSIsImp0aSI6IjQ4YWFmNDlhLTY0YWEtNDQ0My1iNjI0LWVlODRjYzRhOTI1NCIsImF1dGhlbnRpY2F0aW9uVHlwZSI6IlBBU1NXT1JEIiwiZW1haWwiOiJmdXNpb25hdXRoYWRtaW5AY3Jvc3Njb2RlLmNvbSIsImVtYWlsX3ZlcmlmaWVkIjp0cnVlLCJhcHBsaWNhdGlvbklkIjoiN2ZkMzI2ODAtNzAwZS00YmZjLTlhYzAtYmI3ZTE3ZjYzYjcwIiwicm9sZXMiOlsiTmVvNGNhcGUgLSBBZG1pbiJdfQ.k0orE-8XchdeFM6J9v7WbBhpuoYB6BWilvWKHKjqzwRCdv9ZaLYHkxPTh3aZzKcnOi4ir99r4KbfJ7lpdhawSjjjY1mgWlGIhzcsx1tHPvnvYYyyyapdb-YB0Rkp7JwuUAYecYwRKtwchEr0_Bl_juup41BjVb8d7GByQ6iJFTo-iIsxcir6CxrkgXwkqNZLZhfGoQY3o1pINYlGC9tCOw5bgp2IA0pY2xrwEhY7KJrrPIGVz2gNg-3PwTHMz2JE9KG073DqI4TZkqkYv_VNBwvuPLb8Ib5QgrwRSALAG6iMvvorXVqBtSIv9g-OT0Hz86hoJlEHoUvP7O4nsJ57nA' \
--data-raw '{
	"name" : "Any Database Added",
	"ruleType" : "Added",
	"firstNode" : "Database"
}'
```

```javascript
var settings = {
  "url": "{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/audit/rule?page=0&size=10",
  "method": "GET",
  "timeout": 0,
  "headers": {
    "Content-Type": "application/json",
    "Authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Ing5cXo4QV9aZkpXWjJKMTFEV3VWSkFTdGZuRSJ9.eyJhdWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJleHAiOjE2MDE1OTIwNTAsImlhdCI6MTYwMTU2MzI1MCwiaXNzIjoiY3Jvc3Njb2RlLmNvbSIsInN1YiI6IjE4MzA0NjhlLTBkMjQtNGU1OC05ZjFkLTZjNTEzNmI4NTQ4YSIsImp0aSI6IjQ4YWFmNDlhLTY0YWEtNDQ0My1iNjI0LWVlODRjYzRhOTI1NCIsImF1dGhlbnRpY2F0aW9uVHlwZSI6IlBBU1NXT1JEIiwiZW1haWwiOiJmdXNpb25hdXRoYWRtaW5AY3Jvc3Njb2RlLmNvbSIsImVtYWlsX3ZlcmlmaWVkIjp0cnVlLCJhcHBsaWNhdGlvbklkIjoiN2ZkMzI2ODAtNzAwZS00YmZjLTlhYzAtYmI3ZTE3ZjYzYjcwIiwicm9sZXMiOlsiTmVvNGNhcGUgLSBBZG1pbiJdfQ.k0orE-8XchdeFM6J9v7WbBhpuoYB6BWilvWKHKjqzwRCdv9ZaLYHkxPTh3aZzKcnOi4ir99r4KbfJ7lpdhawSjjjY1mgWlGIhzcsx1tHPvnvYYyyyapdb-YB0Rkp7JwuUAYecYwRKtwchEr0_Bl_juup41BjVb8d7GByQ6iJFTo-iIsxcir6CxrkgXwkqNZLZhfGoQY3o1pINYlGC9tCOw5bgp2IA0pY2xrwEhY7KJrrPIGVz2gNg-3PwTHMz2JE9KG073DqI4TZkqkYv_VNBwvuPLb8Ib5QgrwRSALAG6iMvvorXVqBtSIv9g-OT0Hz86hoJlEHoUvP7O4nsJ57nA"
  },
  "data": JSON.stringify({"name":"Any Database Added","ruleType":"Added","firstNode":"Database"}),
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```
> Return Values

```
??
```

### Purpose
To list all existing rule
### Pre-Requisites
You will need a valid session
### Call
To get the list of all rules

`
/audit/rule?page=0&size=10
`
### Return Values
#### 404
When API call is not reachable
### Open Queries
* How to identify id
* list of errors returned by API 

# Matches
## Governance Get Matches
>API Call

```shell
curl --location -g --request GET '{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/audit/governance/matches?page=0&size=10' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6IlBvcWlzckJtUTRPdk0tR2M1cnc5OCJ9.eyJpc3MiOiJodHRwczovL2Rldi1oZnhuOTd6MS51cy5hdXRoMC5jb20vIiwic3ViIjoiZWZTY0ZUbUpMM3FYcjI5R0FaMHZGZmluNzZsNFJkNDRAY2xpZW50cyIsImF1ZCI6Imh0dHA6Ly9jcm9zc2NvZGUubG9jYWwiLCJpYXQiOjE1OTgzNTE5OTIsImV4cCI6MTU5ODk1Njc5MiwiYXpwIjoiZWZTY0ZUbUpMM3FYcjI5R0FaMHZGZmluNzZsNFJkNDQiLCJzY29wZSI6InJlYWQ6Z3JhcGggd3JpdGU6Z3JhcGgiLCJndHkiOiJjbGllbnQtY3JlZGVudGlhbHMifQ.LEBp80NaAzfOtXdF7Y2HJ_05IoIJi1OCWtgM4v7gKB_CAX5Mg2XcxbZ6Nhn89-VxB_Hrx_jgM5jOmq3GSlcd9igrBqKBweX4P4-0xxabojlwOzwBwv0k_hU13WWBlsYsgNxIVZxuq0bYKJFuZt4SEjUSe7HTvHjjHzpDSV7lFiulD_cFZ8ukWo_DHHfKXfe6yIAcnF0EWCGh_6T_Bj_WLIhEoz-U-WknMang1XJqF-z5shVlbbt2jFVn77UAf_T5sMOZsOo2lc-LwdEG2zCTnFYJL7uZTadqNNyHPMj-WzMLgzqHYEL0pe0Ydxx6NwEsiH3FDWdRTAL8p_Al9wM_vw' \
--data-raw ''
```

```javascript
var settings = {
  "url": "{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/audit/governance/matches?page=0&size=10",
  "method": "GET",
  "timeout": 0,
  "headers": {
    "Content-Type": "application/json",
    "Authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6IlBvcWlzckJtUTRPdk0tR2M1cnc5OCJ9.eyJpc3MiOiJodHRwczovL2Rldi1oZnhuOTd6MS51cy5hdXRoMC5jb20vIiwic3ViIjoiZWZTY0ZUbUpMM3FYcjI5R0FaMHZGZmluNzZsNFJkNDRAY2xpZW50cyIsImF1ZCI6Imh0dHA6Ly9jcm9zc2NvZGUubG9jYWwiLCJpYXQiOjE1OTgzNTE5OTIsImV4cCI6MTU5ODk1Njc5MiwiYXpwIjoiZWZTY0ZUbUpMM3FYcjI5R0FaMHZGZmluNzZsNFJkNDQiLCJzY29wZSI6InJlYWQ6Z3JhcGggd3JpdGU6Z3JhcGgiLCJndHkiOiJjbGllbnQtY3JlZGVudGlhbHMifQ.LEBp80NaAzfOtXdF7Y2HJ_05IoIJi1OCWtgM4v7gKB_CAX5Mg2XcxbZ6Nhn89-VxB_Hrx_jgM5jOmq3GSlcd9igrBqKBweX4P4-0xxabojlwOzwBwv0k_hU13WWBlsYsgNxIVZxuq0bYKJFuZt4SEjUSe7HTvHjjHzpDSV7lFiulD_cFZ8ukWo_DHHfKXfe6yIAcnF0EWCGh_6T_Bj_WLIhEoz-U-WknMang1XJqF-z5shVlbbt2jFVn77UAf_T5sMOZsOo2lc-LwdEG2zCTnFYJL7uZTadqNNyHPMj-WzMLgzqHYEL0pe0Ydxx6NwEsiH3FDWdRTAL8p_Al9wM_vw"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```
> Return Values

```
{"status":"success","data":{"page":0,"totalPages":1,"elements":2,"totalElements":2,"ruleMatches":[{"governanceMatchId":"6018010b5213a86743b77918","commitId":"3132.00","matchedOn":"2021-02-01T13:24:26.979Z","author":"1830468e-0d24-4e58-9f1d-6c5136b8548a","auditRuleId":"601800e55213a86743b7470f","auditRuleName":"Created By Automation","snapshotId":"8b8aa4d5-97a7-3fc5-aee5-5d0984dd6167","changeDescription":"AffectedObject: crosscode-core-services-0.0.7-SNAPSHOT.jar\n\nnew object: crosscode-core-services-0.0.7-SNAPSHOT.jar"},{"governanceMatchId":"6018010c5213a86743b7792d","commitId":"3133.00","matchedOn":"2021-02-01T13:24:28.283Z","author":"1830468e-0d24-4e58-9f1d-6c5136b8548a","auditRuleId":"601800e55213a86743b7470f","auditRuleName":"Created By Automation","snapshotId":"87474358-c6fb-3c94-93c6-521dbfa864e4","changeDescription":"AffectedObject: Code-First-Demo\n\nnew object: Code-First-Demo"}]}}
```

### Purpose
????
### Pre-Requisites
You will need a valid session
### Call
To get the list of ??

`
/audit/governance/matches?page=0&size=10
`
### Return Values
#### 404
When API call is not reachable
### Open Queries
* Need to understand purpose
* list of errors returned by API 

# FusionAuth
## Password Flow Token
>API Call

```shell
curl --location -g --request POST '{{http(s)}}://{{baseUrl}}:{{fusionAuthPort}}/oauth2/token?grant_type=password&client_id={{clientId}}&client_secret={{clientSecret}}&username={{username}}&password={{password}}'
```

```javascript
var settings = {
  "url": "{{http(s)}}://{{baseUrl}}:{{fusionAuthPort}}/oauth2/token?grant_type=password&client_id={{clientId}}&client_secret={{clientSecret}}&username={{username}}&password={{password}}",
  "method": "POST",
  "timeout": 0,
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```
> Return Values

```
??
```

### Purpose
I think to login to Fusion Auth????
### Pre-Requisites
Not sure??
### Call
To get the list of ??

`
/oauth2/token?grant_type=password&client_id={{clientId}}&client_secret={{clientSecret}}&username={{username}}&password={{password}}
`
### Return Values
#### 404
When API call is not reachable
### Open Queries
* Need to understand purpose
* list of errors returned by API 
* from where I will get to know clientid and clientsecret?

# Dependency
## Dependency by Id
>API Call

```shell
curl --location -g --request GET '{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/dependency/decomposition/f3e361df-8003-375d-a59f-d33e42e07181' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Ing5cXo4QV9aZkpXWjJKMTFEV3VWSkFTdGZuRSJ9.eyJhdWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJleHAiOjE2MTA3NTY3MjAsImlhdCI6MTYxMDcyNzkyMCwiaXNzIjoiY29kZWxvZ2ljLmNvbSIsInN1YiI6IjE4MzA0NjhlLTBkMjQtNGU1OC05ZjFkLTZjNTEzNmI4NTQ4YSIsImp0aSI6ImYxZTA4NDliLTc2YmYtNDE4Mi1hODYxLTI2OTliNjFlZmZlYyIsImF1dGhlbnRpY2F0aW9uVHlwZSI6IlBBU1NXT1JEIiwiZW1haWwiOiJ0ZW1wb3JhcnlhZG1pbkBjb2RlbG9naWMuY29tIiwiZW1haWxfdmVyaWZpZWQiOnRydWUsImFwcGxpY2F0aW9uSWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJyb2xlcyI6WyJDb2RlTG9naWMgLSBBZG1pbiJdfQ.be3N8z7QBwv1XZAyuaC5i-cG8U2JIzOMWJVxYbM0Ta5-xQK7SduzI5hzMdkBg9k-s8FR5BV1bshY8hxeHkwWpSD0pwkqvg9u03sCfxi6J0l7_uvoYmHSy9tIstMEnrw2bIg2aZ7ZFfQ9O1ZXVoHXz0AG885KChAUalltJ0arcrwFMhyz7nvXnzFLn2h6iSgHQcUz45z5nSAqui-1eR-AdTahXcXUTw2ctVfSfL-Q6z1mqDGWzxAahAzUh0rSsT6m6Un24FZCCNDDYar-pxoTJ-aiOp7QRGt2vjabBUo7VdZ-79i0_LsvzzBeyaGYDBlFTnervrMXX990K2QO9vmvIQ' \
--data-raw ''
```

```javascript
var settings = {
  "url": "{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/dependency/decomposition/f3e361df-8003-375d-a59f-d33e42e07181",
  "method": "GET",
  "timeout": 0,
  "headers": {
    "Authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Ing5cXo4QV9aZkpXWjJKMTFEV3VWSkFTdGZuRSJ9.eyJhdWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJleHAiOjE2MTA3NTY3MjAsImlhdCI6MTYxMDcyNzkyMCwiaXNzIjoiY29kZWxvZ2ljLmNvbSIsInN1YiI6IjE4MzA0NjhlLTBkMjQtNGU1OC05ZjFkLTZjNTEzNmI4NTQ4YSIsImp0aSI6ImYxZTA4NDliLTc2YmYtNDE4Mi1hODYxLTI2OTliNjFlZmZlYyIsImF1dGhlbnRpY2F0aW9uVHlwZSI6IlBBU1NXT1JEIiwiZW1haWwiOiJ0ZW1wb3JhcnlhZG1pbkBjb2RlbG9naWMuY29tIiwiZW1haWxfdmVyaWZpZWQiOnRydWUsImFwcGxpY2F0aW9uSWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJyb2xlcyI6WyJDb2RlTG9naWMgLSBBZG1pbiJdfQ.be3N8z7QBwv1XZAyuaC5i-cG8U2JIzOMWJVxYbM0Ta5-xQK7SduzI5hzMdkBg9k-s8FR5BV1bshY8hxeHkwWpSD0pwkqvg9u03sCfxi6J0l7_uvoYmHSy9tIstMEnrw2bIg2aZ7ZFfQ9O1ZXVoHXz0AG885KChAUalltJ0arcrwFMhyz7nvXnzFLn2h6iSgHQcUz45z5nSAqui-1eR-AdTahXcXUTw2ctVfSfL-Q6z1mqDGWzxAahAzUh0rSsT6m6Un24FZCCNDDYar-pxoTJ-aiOp7QRGt2vjabBUo7VdZ-79i0_LsvzzBeyaGYDBlFTnervrMXX990K2QO9vmvIQ"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```
> Return Values

```
??
```

### Purpose
I think to return the details of dependency object ????
### Pre-Requisites
Not sure??
### Call
To get the list of ??

`
/dependency/decomposition/:id
`
### Return Values
#### 404
When API call is not reachable
### Open Queries
* Need to understand purpose
* list of errors returned by API 
* how to get to know id

## Dependency (TopLevel Nodes)
>API Call

```shell
curl --location -g --request GET '{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/dependency/decomposition?page=0&pageSize=1000' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Ing5cXo4QV9aZkpXWjJKMTFEV3VWSkFTdGZuRSJ9.eyJhdWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJleHAiOjE2MTA3NTY3MjAsImlhdCI6MTYxMDcyNzkyMCwiaXNzIjoiY29kZWxvZ2ljLmNvbSIsInN1YiI6IjE4MzA0NjhlLTBkMjQtNGU1OC05ZjFkLTZjNTEzNmI4NTQ4YSIsImp0aSI6ImYxZTA4NDliLTc2YmYtNDE4Mi1hODYxLTI2OTliNjFlZmZlYyIsImF1dGhlbnRpY2F0aW9uVHlwZSI6IlBBU1NXT1JEIiwiZW1haWwiOiJ0ZW1wb3JhcnlhZG1pbkBjb2RlbG9naWMuY29tIiwiZW1haWxfdmVyaWZpZWQiOnRydWUsImFwcGxpY2F0aW9uSWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJyb2xlcyI6WyJDb2RlTG9naWMgLSBBZG1pbiJdfQ.be3N8z7QBwv1XZAyuaC5i-cG8U2JIzOMWJVxYbM0Ta5-xQK7SduzI5hzMdkBg9k-s8FR5BV1bshY8hxeHkwWpSD0pwkqvg9u03sCfxi6J0l7_uvoYmHSy9tIstMEnrw2bIg2aZ7ZFfQ9O1ZXVoHXz0AG885KChAUalltJ0arcrwFMhyz7nvXnzFLn2h6iSgHQcUz45z5nSAqui-1eR-AdTahXcXUTw2ctVfSfL-Q6z1mqDGWzxAahAzUh0rSsT6m6Un24FZCCNDDYar-pxoTJ-aiOp7QRGt2vjabBUo7VdZ-79i0_LsvzzBeyaGYDBlFTnervrMXX990K2QO9vmvIQ' \
--data-raw ''
```

```javascript
var settings = {
  "url": "{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/dependency/decomposition?page=0&pageSize=1000",
  "method": "GET",
  "timeout": 0,
  "headers": {
    "Authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Ing5cXo4QV9aZkpXWjJKMTFEV3VWSkFTdGZuRSJ9.eyJhdWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJleHAiOjE2MTA3NTY3MjAsImlhdCI6MTYxMDcyNzkyMCwiaXNzIjoiY29kZWxvZ2ljLmNvbSIsInN1YiI6IjE4MzA0NjhlLTBkMjQtNGU1OC05ZjFkLTZjNTEzNmI4NTQ4YSIsImp0aSI6ImYxZTA4NDliLTc2YmYtNDE4Mi1hODYxLTI2OTliNjFlZmZlYyIsImF1dGhlbnRpY2F0aW9uVHlwZSI6IlBBU1NXT1JEIiwiZW1haWwiOiJ0ZW1wb3JhcnlhZG1pbkBjb2RlbG9naWMuY29tIiwiZW1haWxfdmVyaWZpZWQiOnRydWUsImFwcGxpY2F0aW9uSWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJyb2xlcyI6WyJDb2RlTG9naWMgLSBBZG1pbiJdfQ.be3N8z7QBwv1XZAyuaC5i-cG8U2JIzOMWJVxYbM0Ta5-xQK7SduzI5hzMdkBg9k-s8FR5BV1bshY8hxeHkwWpSD0pwkqvg9u03sCfxi6J0l7_uvoYmHSy9tIstMEnrw2bIg2aZ7ZFfQ9O1ZXVoHXz0AG885KChAUalltJ0arcrwFMhyz7nvXnzFLn2h6iSgHQcUz45z5nSAqui-1eR-AdTahXcXUTw2ctVfSfL-Q6z1mqDGWzxAahAzUh0rSsT6m6Un24FZCCNDDYar-pxoTJ-aiOp7QRGt2vjabBUo7VdZ-79i0_LsvzzBeyaGYDBlFTnervrMXX990K2QO9vmvIQ"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```
> Return Values

```
??
```

### Purpose
Returns all the top level dependency nodes.
### Pre-Requisites
Not sure??
### Call
To get the list of all the top level dependency nodes.

`
/dependency/decomposition?page=0&pageSize=1000
`
### Return Values
#### 404
When API call is not reachable
### Open Queries
* Need to understand purpose
* list of errors returned by API 

## Children By Id
>API Call

```shell
curl --location -g --request GET '{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/dependency/node/24ec4c5a-3ce3-3487-824c-9b864a628fa4/children' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Ing5cXo4QV9aZkpXWjJKMTFEV3VWSkFTdGZuRSJ9.eyJhdWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJleHAiOjE2MTA1ODQzMDcsImlhdCI6MTYxMDU1NTUwNywiaXNzIjoiY29kZWxvZ2ljLmNvbSIsInN1YiI6IjE4MzA0NjhlLTBkMjQtNGU1OC05ZjFkLTZjNTEzNmI4NTQ4YSIsImp0aSI6ImI1YzlkYmEzLWZiMDMtNDQ3Mi05YTBjLWQ0OTViNDBlMjdjMSIsImF1dGhlbnRpY2F0aW9uVHlwZSI6IlBBU1NXT1JEIiwiZW1haWwiOiJ0ZW1wb3JhcnlhZG1pbkBjb2RlbG9naWMuY29tIiwiZW1haWxfdmVyaWZpZWQiOnRydWUsImFwcGxpY2F0aW9uSWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJyb2xlcyI6WyJDb2RlTG9naWMgLSBBZG1pbiJdfQ.AIapcivF3FsWiRqTu0p43O4jaEgFSWg6QbdF1b2HXIhCFUBBbYew8CCC8s5cHSLlgFU6pG8rMkqNKoGg2mAf7KL5fg-X0mKS4f5_RY_yDHurNtkOjiAlQaWD4y7cYrAMTglAQIzhQhu6fru1x5tBah6dxF4m8YMFMDa0v4wXzTAm46OeqQgaTUsypx1cu38lhX1jPIjc2fTl63nduc0UgK08J7ukWL3qlx4SXwCWecgX0PPC-X7S9FKASIBrGcOogk8jlShsbfE1cm0NHAbxU0Ct0idHdK_vUodix7Sjf8X7HUWEOyTqPAA1RY0Vi7fXhkNza6ogrAn0w8DQ66kqKA' \
--data-raw ''
```

```javascript
var settings = {
  "url": "{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/dependency/node/24ec4c5a-3ce3-3487-824c-9b864a628fa4/children",
  "method": "GET",
  "timeout": 0,
  "headers": {
    "Authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Ing5cXo4QV9aZkpXWjJKMTFEV3VWSkFTdGZuRSJ9.eyJhdWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJleHAiOjE2MTA1ODQzMDcsImlhdCI6MTYxMDU1NTUwNywiaXNzIjoiY29kZWxvZ2ljLmNvbSIsInN1YiI6IjE4MzA0NjhlLTBkMjQtNGU1OC05ZjFkLTZjNTEzNmI4NTQ4YSIsImp0aSI6ImI1YzlkYmEzLWZiMDMtNDQ3Mi05YTBjLWQ0OTViNDBlMjdjMSIsImF1dGhlbnRpY2F0aW9uVHlwZSI6IlBBU1NXT1JEIiwiZW1haWwiOiJ0ZW1wb3JhcnlhZG1pbkBjb2RlbG9naWMuY29tIiwiZW1haWxfdmVyaWZpZWQiOnRydWUsImFwcGxpY2F0aW9uSWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJyb2xlcyI6WyJDb2RlTG9naWMgLSBBZG1pbiJdfQ.AIapcivF3FsWiRqTu0p43O4jaEgFSWg6QbdF1b2HXIhCFUBBbYew8CCC8s5cHSLlgFU6pG8rMkqNKoGg2mAf7KL5fg-X0mKS4f5_RY_yDHurNtkOjiAlQaWD4y7cYrAMTglAQIzhQhu6fru1x5tBah6dxF4m8YMFMDa0v4wXzTAm46OeqQgaTUsypx1cu38lhX1jPIjc2fTl63nduc0UgK08J7ukWL3qlx4SXwCWecgX0PPC-X7S9FKASIBrGcOogk8jlShsbfE1cm0NHAbxU0Ct0idHdK_vUodix7Sjf8X7HUWEOyTqPAA1RY0Vi7fXhkNza6ogrAn0w8DQ66kqKA"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```
> Return Values

```
??
```

### Purpose
Returns all child nodes of the node.
### Pre-Requisites
A dependency node needed
### Call
To get the list of all child nodes of the node.

`
/dependency/node/:id/children
`
### Return Values
#### 404
When API call is not reachable
### Open Queries
* Need to understand purpose
* list of errors returned by API 

## Labels
>API Call

```shell
curl --location -g --request GET '{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/dependency/cc358b29-c5cc-35b5-9565-c4c4692f1a85' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Ing5cXo4QV9aZkpXWjJKMTFEV3VWSkFTdGZuRSJ9.eyJhdWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJleHAiOjE2MDgxNjI1MDksImlhdCI6MTYwODEzMzcwOSwiaXNzIjoiY3Jvc3Njb2RlLmNvbSIsInN1YiI6IjE4MzA0NjhlLTBkMjQtNGU1OC05ZjFkLTZjNTEzNmI4NTQ4YSIsImp0aSI6ImZiMWUxYTNmLTI0ZTMtNGVjYy05YTgxLWViN2M4MTU1MjgxZCIsImF1dGhlbnRpY2F0aW9uVHlwZSI6IlBBU1NXT1JEIiwiZW1haWwiOiJmdXNpb25hdXRoYWRtaW5AY3Jvc3Njb2RlLmNvbSIsImVtYWlsX3ZlcmlmaWVkIjp0cnVlLCJhcHBsaWNhdGlvbklkIjoiN2ZkMzI2ODAtNzAwZS00YmZjLTlhYzAtYmI3ZTE3ZjYzYjcwIiwicm9sZXMiOlsiTmVvNGNhcGUgLSBBZG1pbiJdfQ.UpTHD_iEbCE7rXwoOVsh6bAaYArxQj0mUIhwa692o2qcQLquSjWMzwmDXY3GqqGuAWfOqI0xSRCYGOxdnRdB38MGCY27yXQreShwktQ1AFZ3PltYpDzJizE8GGS6Ew21ARU7zd7tCiGHvfL9KhLQIKvb-Nm7PedPzmuK9AGSTGCeJSu9APpKtZGgSQRewzTz7zAi4FcHtyWPaX5SuDfK4pBvW3ReCTgcbdBzRHVq2yxW0m1bizeQuULSu7_ywYiZpOoC5i6h9LWSnCRrxsabyOlcw8bBt1O4saf49TlgCeGh6G6_tCPX5SjUxS3_MnQqGpDgpVGRevGW2hlQwqznag' \
--data-raw ''
```

```javascript
var settings = {
  "url": "{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/dependency/cc358b29-c5cc-35b5-9565-c4c4692f1a85",
  "method": "GET",
  "timeout": 0,
  "headers": {
    "Authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Ing5cXo4QV9aZkpXWjJKMTFEV3VWSkFTdGZuRSJ9.eyJhdWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJleHAiOjE2MDgxNjI1MDksImlhdCI6MTYwODEzMzcwOSwiaXNzIjoiY3Jvc3Njb2RlLmNvbSIsInN1YiI6IjE4MzA0NjhlLTBkMjQtNGU1OC05ZjFkLTZjNTEzNmI4NTQ4YSIsImp0aSI6ImZiMWUxYTNmLTI0ZTMtNGVjYy05YTgxLWViN2M4MTU1MjgxZCIsImF1dGhlbnRpY2F0aW9uVHlwZSI6IlBBU1NXT1JEIiwiZW1haWwiOiJmdXNpb25hdXRoYWRtaW5AY3Jvc3Njb2RlLmNvbSIsImVtYWlsX3ZlcmlmaWVkIjp0cnVlLCJhcHBsaWNhdGlvbklkIjoiN2ZkMzI2ODAtNzAwZS00YmZjLTlhYzAtYmI3ZTE3ZjYzYjcwIiwicm9sZXMiOlsiTmVvNGNhcGUgLSBBZG1pbiJdfQ.UpTHD_iEbCE7rXwoOVsh6bAaYArxQj0mUIhwa692o2qcQLquSjWMzwmDXY3GqqGuAWfOqI0xSRCYGOxdnRdB38MGCY27yXQreShwktQ1AFZ3PltYpDzJizE8GGS6Ew21ARU7zd7tCiGHvfL9KhLQIKvb-Nm7PedPzmuK9AGSTGCeJSu9APpKtZGgSQRewzTz7zAi4FcHtyWPaX5SuDfK4pBvW3ReCTgcbdBzRHVq2yxW0m1bizeQuULSu7_ywYiZpOoC5i6h9LWSnCRrxsabyOlcw8bBt1O4saf49TlgCeGh6G6_tCPX5SjUxS3_MnQqGpDgpVGRevGW2hlQwqznag"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```
> Return Values

```
{
    "$schema": "http://json-schema.org/draft-07/schema",
    "$id": "http://example.com/example.json",
    "type": "object",
    "title": "The root schema",
    "description": "The root schema comprises the entire JSON document.",
    "default": {},
    "examples": [
        {
            "containedNodes": [
                {
                    "containedType": "SqlJdbcDatabase",
                    "containedNodes": [
                        {
                            "extendedPropertiesKey": "6018010e5213a86743b77c66",
                            "identity": "jdbc:postgresql://localhost:5432/ccdb",
                            "name": "ccdb",
                            "id": "68bcd5a4-5707-32a5-b500-77b6467180ca"
                        }
                    ]
                },
                {
                    "containedType": "JavaExecutable",
                    "containedNodes": [
                        {
                            "dataSourceId": "jCape",
                            "firstObserved": {
                                "low": 1572564501,
                                "high": 375
                            },
                            "SHA1": "082e211411d014bf8df83747f278b64c59d5e51c",
                            "lastObserved": {
                                "low": -2035703234,
                                "high": 375
                            },
                            "identity": "bootstrap.jar",
                            "dataType": "node",
                            "name": "bootstrap.jar",
                            "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                            "id": "67f39a94-92e9-3822-b284-1246bab1b3a8"
                        },
                        {
                            "firstObserved": {
                                "low": 1572570658,
                                "high": 375
                            },
                            "dataSourceId": "jCape",
                            "SHA1": "82f6f722baa0776891953c8ffcb3527fd21e79e2",
                            "lastObserved": {
                                "low": -2035702263,
                                "high": 375
                            },
                            "identity": "commons-daemon.jar",
                            "dataType": "node",
                            "name": "commons-daemon.jar",
                            "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                            "id": "5f881671-d9df-3301-8c07-3a237037e708"
                        },
                        {
                            "dataSourceId": "jCape",
                            "firstObserved": {
                                "low": 1572573583,
                                "high": 375
                            },
                            "SHA1": "99c11907918309fe94d7e7574a144c7c08077dd4",
                            "lastObserved": {
                                "low": -2035701448,
                                "high": 375
                            },
                            "identity": "maven-wrapper.jar",
                            "dataType": "node",
                            "name": "maven-wrapper.jar",
                            "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                            "id": "1dc13ac4-2dab-3871-94de-a5d8adacd350"
                        },
                        {
                            "dataSourceId": "jCape",
                            "firstObserved": {
                                "low": 1572580561,
                                "high": 375
                            },
                            "SHA1": "8001a1872aad3b3098bae512bfb7578f7e50da6d",
                            "lastObserved": {
                                "low": -2035699454,
                                "high": 375
                            },
                            "identity": "tomcat-juli.jar",
                            "dataType": "node",
                            "name": "tomcat-juli.jar",
                            "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                            "id": "c8b17300-3d0f-3f75-98ec-f322759ddf60"
                        },
                        {
                            "dataSourceId": "jCape",
                            "firstObserved": {
                                "low": 1572587026,
                                "high": 375
                            },
                            "SHA1": "9ce7690bad38c7d73a643f8121bc62b293bc1a4b",
                            "lastObserved": {
                                "low": -2035697289,
                                "high": 375
                            },
                            "identity": "jpetstore.war",
                            "dataType": "node",
                            "name": "jpetstore.war",
                            "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                            "id": "341459b7-665e-356e-aa48-485afb33cd22"
                        },
                        {
                            "firstObserved": {
                                "low": 1572593639,
                                "high": 375
                            },
                            "dataSourceId": "jCape",
                            "SHA1": "b457d582d4a5d86eedc28a7ac774a3d9ddf209aa",
                            "lastObserved": {
                                "low": -2035694138,
                                "high": 375
                            },
                            "identity": "spring-jdbc-5.3.3.jar",
                            "dataType": "node",
                            "name": "spring-jdbc-5.3.3.jar",
                            "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                            "id": "ceedea96-52e1-3b17-b1e0-4e4901ef0837"
                        },
                        {
                            "firstObserved": {
                                "low": 1572593641,
                                "high": 375
                            },
                            "dataSourceId": "jCape",
                            "SHA1": "29b29ac8940bfa8b07f7678e24018cee12f66706",
                            "lastObserved": {
                                "low": -2035694137,
                                "high": 375
                            },
                            "identity": "spring-jcl-5.3.3.jar",
                            "dataType": "node",
                            "name": "spring-jcl-5.3.3.jar",
                            "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                            "id": "df44cb4e-af09-3a64-9a87-445ccd896194"
                        },
                        {
                            "firstObserved": {
                                "low": 1572593643,
                                "high": 375
                            },
                            "dataSourceId": "jCape",
                            "SHA1": "9b9783ccb2a323383e6e20e36d368f8997b71967",
                            "lastObserved": {
                                "low": -2035694135,
                                "high": 375
                            },
                            "identity": "taglibs-standard-impl-1.2.5.jar",
                            "dataType": "node",
                            "name": "taglibs-standard-impl-1.2.5.jar",
                            "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                            "id": "6643157c-c256-37a3-a42b-cebb2288d12d"
                        },
                        {
                            "firstObserved": {
                                "low": 1572593645,
                                "high": 375
                            },
                            "dataSourceId": "jCape",
                            "SHA1": "f6f66e966c70a83ffbdb6f17a0919eaf7c8aca7f",
                            "lastObserved": {
                                "low": -2035694134,
                                "high": 375
                            },
                            "identity": "commons-logging-1.1.3.jar",
                            "dataType": "node",
                            "name": "commons-logging-1.1.3.jar",
                            "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                            "id": "0960e743-ec4c-3626-8e91-4bcdfd05884e"
                        },
                        {
                            "firstObserved": {
                                "low": 1572593648,
                                "high": 375
                            },
                            "dataSourceId": "jCape",
                            "SHA1": "5af35056b4d257e4b64b9e8069c0746e8b08629f",
                            "lastObserved": {
                                "low": -2035694133,
                                "high": 375
                            },
                            "identity": "log4j-1.2.17.jar",
                            "dataType": "node",
                            "name": "log4j-1.2.17.jar",
                            "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                            "id": "03e101fe-4fa0-353e-9571-63deaa66c42c"
                        },
                        {
                            "firstObserved": {
                                "low": 1572593652,
                                "high": 375
                            },
                            "dataSourceId": "jCape",
                            "SHA1": "ea35bf756a880c699768ae0750e1244017d6ae84",
                            "lastObserved": {
                                "low": -2035694131,
                                "high": 375
                            },
                            "identity": "spring-core-5.3.3.jar",
                            "dataType": "node",
                            "name": "spring-core-5.3.3.jar",
                            "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                            "id": "fd17823e-aebd-3b0d-8aab-2b2d9d3f1976"
                        },
                        {
                            "firstObserved": {
                                "low": 1572593658,
                                "high": 375
                            },
                            "dataSourceId": "jCape",
                            "SHA1": "d7b9366fd446a135fa0833249d6468dd2dda5b1a",
                            "lastObserved": {
                                "low": -2035694130,
                                "high": 375
                            },
                            "identity": "spring-aop-5.3.3.jar",
                            "dataType": "node",
                            "name": "spring-aop-5.3.3.jar",
                            "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                            "id": "260e3276-c697-32d5-b987-af42e05e4f08"
                        },
                        {
                            "firstObserved": {
                                "low": 1572593661,
                                "high": 375
                            },
                            "dataSourceId": "jCape",
                            "SHA1": "db244edbb790ec24719e8eec635bd82b8ea24f62",
                            "lastObserved": {
                                "low": -2035694128,
                                "high": 375
                            },
                            "identity": "spring-tx-5.3.3.jar",
                            "dataType": "node",
                            "name": "spring-tx-5.3.3.jar",
                            "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                            "id": "28b51c49-a878-39d8-b669-41cfdb69fa79"
                        },
                        {
                            "firstObserved": {
                                "low": 1572593664,
                                "high": 375
                            },
                            "dataSourceId": "jCape",
                            "SHA1": "b1f720a63a8756867895cc22dd74b51fb70e90ac",
                            "lastObserved": {
                                "low": -2035694127,
                                "high": 375
                            },
                            "identity": "hsqldb-2.5.1.jar",
                            "dataType": "node",
                            "name": "hsqldb-2.5.1.jar",
                            "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                            "id": "5ad79833-7cc9-347a-a26e-0492ecdf5f22"
                        },
                        {
                            "firstObserved": {
                                "low": 1572593667,
                                "high": 375
                            },
                            "dataSourceId": "jCape",
                            "SHA1": "ede9213003a7fe8659047c8220d4b68f65841b30",
                            "lastObserved": {
                                "low": -2035694125,
                                "high": 375
                            },
                            "identity": "stripes-1.6.0.jar",
                            "dataType": "node",
                            "name": "stripes-1.6.0.jar",
                            "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                            "id": "a0da8d7f-f2b7-3ff6-b015-182bc1ed15ca"
                        },
                        {
                            "firstObserved": {
                                "low": 1572593686,
                                "high": 375
                            },
                            "dataSourceId": "jCape",
                            "SHA1": "c3bb98c30f75fef1e229d1d03cf8457de22f1ba0",
                            "lastObserved": {
                                "low": -2035694124,
                                "high": 375
                            },
                            "identity": "taglibs-standard-spec-1.2.5.jar",
                            "dataType": "node",
                            "name": "taglibs-standard-spec-1.2.5.jar",
                            "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                            "id": "8cb5c9e3-432e-36c6-8fdd-6c251fadcae2"
                        },
                        {
                            "firstObserved": {
                                "low": 1572593690,
                                "high": 375
                            },
                            "dataSourceId": "jCape",
                            "SHA1": "991cb0e9ef7a641d78d12ea18e213124fed6e787",
                            "lastObserved": {
                                "low": -2035694123,
                                "high": 375
                            },
                            "identity": "spring-context-5.3.3.jar",
                            "dataType": "node",
                            "name": "spring-context-5.3.3.jar",
                            "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                            "id": "3865a1c4-a5ca-3e37-8172-5c6ebde19ee8"
                        },
                        {
                            "firstObserved": {
                                "low": 1572593697,
                                "high": 375
                            },
                            "dataSourceId": "jCape",
                            "SHA1": "855f38fc8b85901681495ac6c6379051ee688cd5",
                            "lastObserved": {
                                "low": -2035694121,
                                "high": 375
                            },
                            "identity": "spring-beans-5.3.3.jar",
                            "dataType": "node",
                            "name": "spring-beans-5.3.3.jar",
                            "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                            "id": "ff8d0b9b-da12-37a8-9cee-d057b6510cc7"
                        },
                        {
                            "firstObserved": {
                                "low": 1572593703,
                                "high": 375
                            },
                            "dataSourceId": "jCape",
                            "SHA1": "c98f680074d15abee6130a22683f5f5d8acdfa15",
                            "lastObserved": {
                                "low": -2035694119,
                                "high": 375
                            },
                            "identity": "spring-expression-5.3.3.jar",
                            "dataType": "node",
                            "name": "spring-expression-5.3.3.jar",
                            "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                            "id": "09bee465-5e47-3efc-9433-ddfc449642b8"
                        },
                        {
                            "firstObserved": {
                                "low": 1572593709,
                                "high": 375
                            },
                            "dataSourceId": "jCape",
                            "SHA1": "28ea8fe7d6c3998cf1d0cb8af64b9d58f04c7cb3",
                            "lastObserved": {
                                "low": -2035694118,
                                "high": 375
                            },
                            "identity": "mybatis-3.5.6.jar",
                            "dataType": "node",
                            "name": "mybatis-3.5.6.jar",
                            "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                            "id": "7077d426-adaa-32c4-ad32-7852764c19bd"
                        },
                        {
                            "firstObserved": {
                                "low": 1572593715,
                                "high": 375
                            },
                            "dataSourceId": "jCape",
                            "SHA1": "eae03712acdf041a3590b816460945d4bd2691bc",
                            "lastObserved": {
                                "low": -2035694117,
                                "high": 375
                            },
                            "identity": "mybatis-spring-2.0.6.jar",
                            "dataType": "node",
                            "name": "mybatis-spring-2.0.6.jar",
                            "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                            "id": "eb52a499-9f29-38f1-9f44-3423f10d56ae"
                        },
                        {
                            "firstObserved": {
                                "low": 1572593723,
                                "high": 375
                            },
                            "dataSourceId": "jCape",
                            "SHA1": "9112880371d9ff888ee1248563df80eacbec7e14",
                            "lastObserved": {
                                "low": -2035694115,
                                "high": 375
                            },
                            "identity": "spring-web-5.3.3.jar",
                            "dataType": "node",
                            "name": "spring-web-5.3.3.jar",
                            "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                            "id": "0784176e-d08f-3b1f-bbc1-fc8355303d2f"
                        },
                        {
                            "extendedPropertiesKey": "601800f15213a86743b757a2",
                            "identity": "crosscode-core-services-0.0.7-SNAPSHOT.jar",
                            "name": "crosscode-core-services-0.0.7-SNAPSHOT.jar",
                            "id": "8b8aa4d5-97a7-3fc5-aee5-5d0984dd6167"
                        }
                    ]
                },
                {
                    "containedType": "DotNetAssembly",
                    "containedNodes": [
                        {
                            "extendedPropertiesKey": "6018010b5213a86743b7791f",
                            "identity": "Code-First-Demo",
                            "name": "Code-First-Demo",
                            "id": "87474358-c6fb-3c94-93c6-521dbfa864e4"
                        }
                    ]
                }
            ],
            "referencedNodes": []
        }
    ],
    "required": [
        "containedNodes",
        "referencedNodes"
    ],
    "properties": {
        "containedNodes": {
            "$id": "#/properties/containedNodes",
            "type": "array",
            "title": "The containedNodes schema",
            "description": "An explanation about the purpose of this instance.",
            "default": [],
            "examples": [
                [
                    {
                        "containedType": "SqlJdbcDatabase",
                        "containedNodes": [
                            {
                                "extendedPropertiesKey": "6018010e5213a86743b77c66",
                                "identity": "jdbc:postgresql://localhost:5432/ccdb",
                                "name": "ccdb",
                                "id": "68bcd5a4-5707-32a5-b500-77b6467180ca"
                            }
                        ]
                    },
                    {
                        "containedType": "JavaExecutable",
                        "containedNodes": [
                            {
                                "dataSourceId": "jCape",
                                "firstObserved": {
                                    "low": 1572564501,
                                    "high": 375
                                },
                                "SHA1": "082e211411d014bf8df83747f278b64c59d5e51c",
                                "lastObserved": {
                                    "low": -2035703234,
                                    "high": 375
                                },
                                "identity": "bootstrap.jar",
                                "dataType": "node",
                                "name": "bootstrap.jar",
                                "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                                "id": "67f39a94-92e9-3822-b284-1246bab1b3a8"
                            },
                            {
                                "firstObserved": {
                                    "low": 1572570658,
                                    "high": 375
                                },
                                "dataSourceId": "jCape",
                                "SHA1": "82f6f722baa0776891953c8ffcb3527fd21e79e2",
                                "lastObserved": {
                                    "low": -2035702263,
                                    "high": 375
                                },
                                "identity": "commons-daemon.jar",
                                "dataType": "node",
                                "name": "commons-daemon.jar",
                                "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                                "id": "5f881671-d9df-3301-8c07-3a237037e708"
                            },
                            {
                                "dataSourceId": "jCape",
                                "firstObserved": {
                                    "low": 1572573583,
                                    "high": 375
                                },
                                "SHA1": "99c11907918309fe94d7e7574a144c7c08077dd4",
                                "lastObserved": {
                                    "low": -2035701448,
                                    "high": 375
                                },
                                "identity": "maven-wrapper.jar",
                                "dataType": "node",
                                "name": "maven-wrapper.jar",
                                "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                                "id": "1dc13ac4-2dab-3871-94de-a5d8adacd350"
                            },
                            {
                                "dataSourceId": "jCape",
                                "firstObserved": {
                                    "low": 1572580561,
                                    "high": 375
                                },
                                "SHA1": "8001a1872aad3b3098bae512bfb7578f7e50da6d",
                                "lastObserved": {
                                    "low": -2035699454,
                                    "high": 375
                                },
                                "identity": "tomcat-juli.jar",
                                "dataType": "node",
                                "name": "tomcat-juli.jar",
                                "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                                "id": "c8b17300-3d0f-3f75-98ec-f322759ddf60"
                            },
                            {
                                "dataSourceId": "jCape",
                                "firstObserved": {
                                    "low": 1572587026,
                                    "high": 375
                                },
                                "SHA1": "9ce7690bad38c7d73a643f8121bc62b293bc1a4b",
                                "lastObserved": {
                                    "low": -2035697289,
                                    "high": 375
                                },
                                "identity": "jpetstore.war",
                                "dataType": "node",
                                "name": "jpetstore.war",
                                "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                                "id": "341459b7-665e-356e-aa48-485afb33cd22"
                            },
                            {
                                "firstObserved": {
                                    "low": 1572593639,
                                    "high": 375
                                },
                                "dataSourceId": "jCape",
                                "SHA1": "b457d582d4a5d86eedc28a7ac774a3d9ddf209aa",
                                "lastObserved": {
                                    "low": -2035694138,
                                    "high": 375
                                },
                                "identity": "spring-jdbc-5.3.3.jar",
                                "dataType": "node",
                                "name": "spring-jdbc-5.3.3.jar",
                                "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                                "id": "ceedea96-52e1-3b17-b1e0-4e4901ef0837"
                            },
                            {
                                "firstObserved": {
                                    "low": 1572593641,
                                    "high": 375
                                },
                                "dataSourceId": "jCape",
                                "SHA1": "29b29ac8940bfa8b07f7678e24018cee12f66706",
                                "lastObserved": {
                                    "low": -2035694137,
                                    "high": 375
                                },
                                "identity": "spring-jcl-5.3.3.jar",
                                "dataType": "node",
                                "name": "spring-jcl-5.3.3.jar",
                                "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                                "id": "df44cb4e-af09-3a64-9a87-445ccd896194"
                            },
                            {
                                "firstObserved": {
                                    "low": 1572593643,
                                    "high": 375
                                },
                                "dataSourceId": "jCape",
                                "SHA1": "9b9783ccb2a323383e6e20e36d368f8997b71967",
                                "lastObserved": {
                                    "low": -2035694135,
                                    "high": 375
                                },
                                "identity": "taglibs-standard-impl-1.2.5.jar",
                                "dataType": "node",
                                "name": "taglibs-standard-impl-1.2.5.jar",
                                "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                                "id": "6643157c-c256-37a3-a42b-cebb2288d12d"
                            },
                            {
                                "firstObserved": {
                                    "low": 1572593645,
                                    "high": 375
                                },
                                "dataSourceId": "jCape",
                                "SHA1": "f6f66e966c70a83ffbdb6f17a0919eaf7c8aca7f",
                                "lastObserved": {
                                    "low": -2035694134,
                                    "high": 375
                                },
                                "identity": "commons-logging-1.1.3.jar",
                                "dataType": "node",
                                "name": "commons-logging-1.1.3.jar",
                                "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                                "id": "0960e743-ec4c-3626-8e91-4bcdfd05884e"
                            },
                            {
                                "firstObserved": {
                                    "low": 1572593648,
                                    "high": 375
                                },
                                "dataSourceId": "jCape",
                                "SHA1": "5af35056b4d257e4b64b9e8069c0746e8b08629f",
                                "lastObserved": {
                                    "low": -2035694133,
                                    "high": 375
                                },
                                "identity": "log4j-1.2.17.jar",
                                "dataType": "node",
                                "name": "log4j-1.2.17.jar",
                                "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                                "id": "03e101fe-4fa0-353e-9571-63deaa66c42c"
                            },
                            {
                                "firstObserved": {
                                    "low": 1572593652,
                                    "high": 375
                                },
                                "dataSourceId": "jCape",
                                "SHA1": "ea35bf756a880c699768ae0750e1244017d6ae84",
                                "lastObserved": {
                                    "low": -2035694131,
                                    "high": 375
                                },
                                "identity": "spring-core-5.3.3.jar",
                                "dataType": "node",
                                "name": "spring-core-5.3.3.jar",
                                "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                                "id": "fd17823e-aebd-3b0d-8aab-2b2d9d3f1976"
                            },
                            {
                                "firstObserved": {
                                    "low": 1572593658,
                                    "high": 375
                                },
                                "dataSourceId": "jCape",
                                "SHA1": "d7b9366fd446a135fa0833249d6468dd2dda5b1a",
                                "lastObserved": {
                                    "low": -2035694130,
                                    "high": 375
                                },
                                "identity": "spring-aop-5.3.3.jar",
                                "dataType": "node",
                                "name": "spring-aop-5.3.3.jar",
                                "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                                "id": "260e3276-c697-32d5-b987-af42e05e4f08"
                            },
                            {
                                "firstObserved": {
                                    "low": 1572593661,
                                    "high": 375
                                },
                                "dataSourceId": "jCape",
                                "SHA1": "db244edbb790ec24719e8eec635bd82b8ea24f62",
                                "lastObserved": {
                                    "low": -2035694128,
                                    "high": 375
                                },
                                "identity": "spring-tx-5.3.3.jar",
                                "dataType": "node",
                                "name": "spring-tx-5.3.3.jar",
                                "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                                "id": "28b51c49-a878-39d8-b669-41cfdb69fa79"
                            },
                            {
                                "firstObserved": {
                                    "low": 1572593664,
                                    "high": 375
                                },
                                "dataSourceId": "jCape",
                                "SHA1": "b1f720a63a8756867895cc22dd74b51fb70e90ac",
                                "lastObserved": {
                                    "low": -2035694127,
                                    "high": 375
                                },
                                "identity": "hsqldb-2.5.1.jar",
                                "dataType": "node",
                                "name": "hsqldb-2.5.1.jar",
                                "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                                "id": "5ad79833-7cc9-347a-a26e-0492ecdf5f22"
                            },
                            {
                                "firstObserved": {
                                    "low": 1572593667,
                                    "high": 375
                                },
                                "dataSourceId": "jCape",
                                "SHA1": "ede9213003a7fe8659047c8220d4b68f65841b30",
                                "lastObserved": {
                                    "low": -2035694125,
                                    "high": 375
                                },
                                "identity": "stripes-1.6.0.jar",
                                "dataType": "node",
                                "name": "stripes-1.6.0.jar",
                                "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                                "id": "a0da8d7f-f2b7-3ff6-b015-182bc1ed15ca"
                            },
                            {
                                "firstObserved": {
                                    "low": 1572593686,
                                    "high": 375
                                },
                                "dataSourceId": "jCape",
                                "SHA1": "c3bb98c30f75fef1e229d1d03cf8457de22f1ba0",
                                "lastObserved": {
                                    "low": -2035694124,
                                    "high": 375
                                },
                                "identity": "taglibs-standard-spec-1.2.5.jar",
                                "dataType": "node",
                                "name": "taglibs-standard-spec-1.2.5.jar",
                                "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                                "id": "8cb5c9e3-432e-36c6-8fdd-6c251fadcae2"
                            },
                            {
                                "firstObserved": {
                                    "low": 1572593690,
                                    "high": 375
                                },
                                "dataSourceId": "jCape",
                                "SHA1": "991cb0e9ef7a641d78d12ea18e213124fed6e787",
                                "lastObserved": {
                                    "low": -2035694123,
                                    "high": 375
                                },
                                "identity": "spring-context-5.3.3.jar",
                                "dataType": "node",
                                "name": "spring-context-5.3.3.jar",
                                "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                                "id": "3865a1c4-a5ca-3e37-8172-5c6ebde19ee8"
                            },
                            {
                                "firstObserved": {
                                    "low": 1572593697,
                                    "high": 375
                                },
                                "dataSourceId": "jCape",
                                "SHA1": "855f38fc8b85901681495ac6c6379051ee688cd5",
                                "lastObserved": {
                                    "low": -2035694121,
                                    "high": 375
                                },
                                "identity": "spring-beans-5.3.3.jar",
                                "dataType": "node",
                                "name": "spring-beans-5.3.3.jar",
                                "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                                "id": "ff8d0b9b-da12-37a8-9cee-d057b6510cc7"
                            },
                            {
                                "firstObserved": {
                                    "low": 1572593703,
                                    "high": 375
                                },
                                "dataSourceId": "jCape",
                                "SHA1": "c98f680074d15abee6130a22683f5f5d8acdfa15",
                                "lastObserved": {
                                    "low": -2035694119,
                                    "high": 375
                                },
                                "identity": "spring-expression-5.3.3.jar",
                                "dataType": "node",
                                "name": "spring-expression-5.3.3.jar",
                                "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                                "id": "09bee465-5e47-3efc-9433-ddfc449642b8"
                            },
                            {
                                "firstObserved": {
                                    "low": 1572593709,
                                    "high": 375
                                },
                                "dataSourceId": "jCape",
                                "SHA1": "28ea8fe7d6c3998cf1d0cb8af64b9d58f04c7cb3",
                                "lastObserved": {
                                    "low": -2035694118,
                                    "high": 375
                                },
                                "identity": "mybatis-3.5.6.jar",
                                "dataType": "node",
                                "name": "mybatis-3.5.6.jar",
                                "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                                "id": "7077d426-adaa-32c4-ad32-7852764c19bd"
                            },
                            {
                                "firstObserved": {
                                    "low": 1572593715,
                                    "high": 375
                                },
                                "dataSourceId": "jCape",
                                "SHA1": "eae03712acdf041a3590b816460945d4bd2691bc",
                                "lastObserved": {
                                    "low": -2035694117,
                                    "high": 375
                                },
                                "identity": "mybatis-spring-2.0.6.jar",
                                "dataType": "node",
                                "name": "mybatis-spring-2.0.6.jar",
                                "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                                "id": "eb52a499-9f29-38f1-9f44-3423f10d56ae"
                            },
                            {
                                "firstObserved": {
                                    "low": 1572593723,
                                    "high": 375
                                },
                                "dataSourceId": "jCape",
                                "SHA1": "9112880371d9ff888ee1248563df80eacbec7e14",
                                "lastObserved": {
                                    "low": -2035694115,
                                    "high": 375
                                },
                                "identity": "spring-web-5.3.3.jar",
                                "dataType": "node",
                                "name": "spring-web-5.3.3.jar",
                                "scanContextId": "d0a3d63f-21f5-455a-a3b5-f2c93fe26360",
                                "id": "0784176e-d08f-3b1f-bbc1-fc8355303d2f"
                            },
                            {
                                "extendedPropertiesKey": "601800f15213a86743b757a2",
                                "identity": "crosscode-core-services-0.0.7-SNAPSHOT.jar",
                                "name": "crosscode-core-services-0.0.7-SNAPSHOT.jar",
                                "id": "8b8aa4d5-97a7-3fc5-aee5-5d0984dd6167"
                            }
                        ]
                    }
                ]
            ],
            "additionalItems": true,
            "items": {
                "$id": "#/properties/containedNodes/items",
                "anyOf": [
                    {
                        "$id": "#/properties/containedNodes/items/anyOf/0",
                        "type": "object",
                        "title": "The first anyOf schema",
                        "description": "An explanation about the purpose of this instance.",
                        "default": {},
                        "examples": [
                            {
                                "containedType": "SqlJdbcDatabase",
                                "containedNodes": [
                                    {
                                        "extendedPropertiesKey": "6018010e5213a86743b77c66",
                                        "identity": "jdbc:postgresql://localhost:5432/ccdb",
                                        "name": "ccdb",
                                        "id": "68bcd5a4-5707-32a5-b500-77b6467180ca"
                                    }
                                ]
                            }
                        ],
                        "required": [
                            "containedType",
                            "containedNodes"
                        ],
                        "properties": {
                            "containedType": {
                                "$id": "#/properties/containedNodes/items/anyOf/0/properties/containedType",
                                "type": "string",
                                "title": "The containedType schema",
                                "description": "An explanation about the purpose of this instance.",
                                "default": "",
                                "examples": [
                                    "SqlJdbcDatabase"
                                ]
                            },
                            "containedNodes": {
                                "$id": "#/properties/containedNodes/items/anyOf/0/properties/containedNodes",
                                "type": "array",
                                "title": "The containedNodes schema",
                                "description": "An explanation about the purpose of this instance.",
                                "default": [],
                                "examples": [
                                    [
                                        {
                                            "extendedPropertiesKey": "6018010e5213a86743b77c66",
                                            "identity": "jdbc:postgresql://localhost:5432/ccdb",
                                            "name": "ccdb",
                                            "id": "68bcd5a4-5707-32a5-b500-77b6467180ca"
                                        }
                                    ]
                                ],
                                "additionalItems": true,
                                "items": {
                                    "$id": "#/properties/containedNodes/items/anyOf/0/properties/containedNodes/items",
                                    "anyOf": [
                                        {
                                            "$id": "#/properties/containedNodes/items/anyOf/0/properties/containedNodes/items/anyOf/0",
                                            "type": "object",
                                            "title": "The first anyOf schema",
                                            "description": "An explanation about the purpose of this instance.",
                                            "default": {},
                                            "examples": [
                                                {
                                                    "extendedPropertiesKey": "6018010e5213a86743b77c66",
                                                    "identity": "jdbc:postgresql://localhost:5432/ccdb",
                                                    "name": "ccdb",
                                                    "id": "68bcd5a4-5707-32a5-b500-77b6467180ca"
                                                }
                                            ],
                                            "required": [
                                                "extendedPropertiesKey",
                                                "identity",
                                                "name",
                                                "id"
                                            ],
                                            "properties": {
                                                "extendedPropertiesKey": {
                                                    "$id": "#/properties/containedNodes/items/anyOf/0/properties/containedNodes/items/anyOf/0/properties/extendedPropertiesKey",
                                                    "type": "string",
                                                    "title": "The extendedPropertiesKey schema",
                                                    "description": "An explanation about the purpose of this instance.",
                                                    "default": "",
                                                    "examples": [
                                                        "6018010e5213a86743b77c66"
                                                    ]
                                                },
                                                "identity": {
                                                    "$id": "#/properties/containedNodes/items/anyOf/0/properties/containedNodes/items/anyOf/0/properties/identity",
                                                    "type": "string",
                                                    "title": "The identity schema",
                                                    "description": "An explanation about the purpose of this instance.",
                                                    "default": "",
                                                    "examples": [
                                                        "jdbc:postgresql://localhost:5432/ccdb"
                                                    ]
                                                },
                                                "name": {
                                                    "$id": "#/properties/containedNodes/items/anyOf/0/properties/containedNodes/items/anyOf/0/properties/name",
                                                    "type": "string",
                                                    "title": "The name schema",
                                                    "description": "An explanation about the purpose of this instance.",
                                                    "default": "",
                                                    "examples": [
                                                        "ccdb"
                                                    ]
                                                },
                                                "id": {
                                                    "$id": "#/properties/containedNodes/items/anyOf/0/properties/containedNodes/items/anyOf/0/properties/id",
                                                    "type": "string",
                                                    "title": "The id schema",
                                                    "description": "An explanation about the purpose of this instance.",
                                                    "default": "",
                                                    "examples": [
                                                        "68bcd5a4-5707-32a5-b500-77b6467180ca"
                                                    ]
                                                }
                                            },
                                            "additionalProperties": true
                                        }
                                    ]
                                }
                            }
                        },
                        "additionalProperties": true
                    }
                ]
            }
        },
        "referencedNodes": {
            "$id": "#/properties/referencedNodes",
            "type": "array",
            "title": "The referencedNodes schema",
            "description": "An explanation about the purpose of this instance.",
            "default": [],
            "examples": [
                []
            ],
            "additionalItems": true,
            "items": {
                "$id": "#/properties/referencedNodes/items"
            }
        }
    },
    "additionalProperties": true
}
```

### Purpose
To get the list of the dependency tree labels.
### Pre-Requisites
Valid session for executing the API call.
### Call
Limit parameter defines the number of objects returned.
`
/middleware/api/dependencies/labels?limit=1000
`
Example:
`
http://192.168.56.102/codelogic/middleware/api/dependencies/labels?limit=1000
`
### Return Values
#### 404
When API call is not reachable
### Open Queries
* Changing the limit value does not seem to have any impact on the return values.
* list of errors returned by API 


## Impact  By Id
>API Call

```shell
curl --location -g --request GET '{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/dependency/impact/24ec4c5a-3ce3-3487-824c-9b864a628fa4' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Ing5cXo4QV9aZkpXWjJKMTFEV3VWSkFTdGZuRSJ9.eyJhdWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJleHAiOjE2MDgwODA3MzgsImlhdCI6MTYwODA1MTkzOCwiaXNzIjoiY3Jvc3Njb2RlLmNvbSIsInN1YiI6IjE4MzA0NjhlLTBkMjQtNGU1OC05ZjFkLTZjNTEzNmI4NTQ4YSIsImp0aSI6ImM2YTMyOGYwLTFkODgtNDg5Ny1iOGEyLWFmYTE3YjUyMDhlNyIsImF1dGhlbnRpY2F0aW9uVHlwZSI6IlBBU1NXT1JEIiwiZW1haWwiOiJmdXNpb25hdXRoYWRtaW5AY3Jvc3Njb2RlLmNvbSIsImVtYWlsX3ZlcmlmaWVkIjp0cnVlLCJhcHBsaWNhdGlvbklkIjoiN2ZkMzI2ODAtNzAwZS00YmZjLTlhYzAtYmI3ZTE3ZjYzYjcwIiwicm9sZXMiOlsiTmVvNGNhcGUgLSBBZG1pbiJdfQ.KlOfPD8ZK5mJCwoEly3m_f-_D-lnIkEPBZFeQc0HC6bpON477n4p9D5232W5RdZhV2V36qWOXgOBKBbD_akVQOPiNFD_RkWiu5OMRTmTc70VLT3NuFEt5czMyR5fxCLnCKAc_lczwjJpBZQLrh3k3MyK8QQg31a4j0CvBwxDR4I-I4DD7-dpakIZt8bZJvEFb5Q7tuK5Rw9_Sn6tI_MAX-H9chdDyBVmSw0FDqwomA1p7VZKcQwm7nee6gy7btxYWkA9zOTKgOql4aLscplJ-eC7tss2mKf6xHyhjh0-2gmIf8xkvlvkB_hCx8ZFMEObrrx80UPcBrLlVVRbYvRuhA' \
--data-raw '''
```

```javascript
var settings = {
  "url": "{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/dependency/impact/24ec4c5a-3ce3-3487-824c-9b864a628fa4",
  "method": "GET",
  "timeout": 0,
  "headers": {
    "Authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Ing5cXo4QV9aZkpXWjJKMTFEV3VWSkFTdGZuRSJ9.eyJhdWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJleHAiOjE2MDgwODA3MzgsImlhdCI6MTYwODA1MTkzOCwiaXNzIjoiY3Jvc3Njb2RlLmNvbSIsInN1YiI6IjE4MzA0NjhlLTBkMjQtNGU1OC05ZjFkLTZjNTEzNmI4NTQ4YSIsImp0aSI6ImM2YTMyOGYwLTFkODgtNDg5Ny1iOGEyLWFmYTE3YjUyMDhlNyIsImF1dGhlbnRpY2F0aW9uVHlwZSI6IlBBU1NXT1JEIiwiZW1haWwiOiJmdXNpb25hdXRoYWRtaW5AY3Jvc3Njb2RlLmNvbSIsImVtYWlsX3ZlcmlmaWVkIjp0cnVlLCJhcHBsaWNhdGlvbklkIjoiN2ZkMzI2ODAtNzAwZS00YmZjLTlhYzAtYmI3ZTE3ZjYzYjcwIiwicm9sZXMiOlsiTmVvNGNhcGUgLSBBZG1pbiJdfQ.KlOfPD8ZK5mJCwoEly3m_f-_D-lnIkEPBZFeQc0HC6bpON477n4p9D5232W5RdZhV2V36qWOXgOBKBbD_akVQOPiNFD_RkWiu5OMRTmTc70VLT3NuFEt5czMyR5fxCLnCKAc_lczwjJpBZQLrh3k3MyK8QQg31a4j0CvBwxDR4I-I4DD7-dpakIZt8bZJvEFb5Q7tuK5Rw9_Sn6tI_MAX-H9chdDyBVmSw0FDqwomA1p7VZKcQwm7nee6gy7btxYWkA9zOTKgOql4aLscplJ-eC7tss2mKf6xHyhjh0-2gmIf8xkvlvkB_hCx8ZFMEObrrx80UPcBrLlVVRbYvRuhA"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```
> Return Values

```
??
```

### Purpose
??
### Pre-Requisites
??
### Call
??

`
/dependency/impact/:id
`
### Return Values
#### 404
When API call is not reachable
### Open Queries
* Need to understand purpose
* list of errors returned by API 

## TopeLevelNode for Id
>API Call

```shell
curl --location -g --request GET '{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/dependency/parent/7ec45fc1-4600-398d-9661-434a0e108f7a' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Ing5cXo4QV9aZkpXWjJKMTFEV3VWSkFTdGZuRSJ9.eyJhdWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJleHAiOjE2MTA1ODQzMDcsImlhdCI6MTYxMDU1NTUwNywiaXNzIjoiY29kZWxvZ2ljLmNvbSIsInN1YiI6IjE4MzA0NjhlLTBkMjQtNGU1OC05ZjFkLTZjNTEzNmI4NTQ4YSIsImp0aSI6ImI1YzlkYmEzLWZiMDMtNDQ3Mi05YTBjLWQ0OTViNDBlMjdjMSIsImF1dGhlbnRpY2F0aW9uVHlwZSI6IlBBU1NXT1JEIiwiZW1haWwiOiJ0ZW1wb3JhcnlhZG1pbkBjb2RlbG9naWMuY29tIiwiZW1haWxfdmVyaWZpZWQiOnRydWUsImFwcGxpY2F0aW9uSWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJyb2xlcyI6WyJDb2RlTG9naWMgLSBBZG1pbiJdfQ.AIapcivF3FsWiRqTu0p43O4jaEgFSWg6QbdF1b2HXIhCFUBBbYew8CCC8s5cHSLlgFU6pG8rMkqNKoGg2mAf7KL5fg-X0mKS4f5_RY_yDHurNtkOjiAlQaWD4y7cYrAMTglAQIzhQhu6fru1x5tBah6dxF4m8YMFMDa0v4wXzTAm46OeqQgaTUsypx1cu38lhX1jPIjc2fTl63nduc0UgK08J7ukWL3qlx4SXwCWecgX0PPC-X7S9FKASIBrGcOogk8jlShsbfE1cm0NHAbxU0Ct0idHdK_vUodix7Sjf8X7HUWEOyTqPAA1RY0Vi7fXhkNza6ogrAn0w8DQ66kqKA' \
--data-raw ''
```

```javascript
var settings = {
  "url": "{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/dependency/parent/7ec45fc1-4600-398d-9661-434a0e108f7a",
  "method": "GET",
  "timeout": 0,
  "headers": {
    "Authorization": "Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6Ing5cXo4QV9aZkpXWjJKMTFEV3VWSkFTdGZuRSJ9.eyJhdWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJleHAiOjE2MTA1ODQzMDcsImlhdCI6MTYxMDU1NTUwNywiaXNzIjoiY29kZWxvZ2ljLmNvbSIsInN1YiI6IjE4MzA0NjhlLTBkMjQtNGU1OC05ZjFkLTZjNTEzNmI4NTQ4YSIsImp0aSI6ImI1YzlkYmEzLWZiMDMtNDQ3Mi05YTBjLWQ0OTViNDBlMjdjMSIsImF1dGhlbnRpY2F0aW9uVHlwZSI6IlBBU1NXT1JEIiwiZW1haWwiOiJ0ZW1wb3JhcnlhZG1pbkBjb2RlbG9naWMuY29tIiwiZW1haWxfdmVyaWZpZWQiOnRydWUsImFwcGxpY2F0aW9uSWQiOiI3ZmQzMjY4MC03MDBlLTRiZmMtOWFjMC1iYjdlMTdmNjNiNzAiLCJyb2xlcyI6WyJDb2RlTG9naWMgLSBBZG1pbiJdfQ.AIapcivF3FsWiRqTu0p43O4jaEgFSWg6QbdF1b2HXIhCFUBBbYew8CCC8s5cHSLlgFU6pG8rMkqNKoGg2mAf7KL5fg-X0mKS4f5_RY_yDHurNtkOjiAlQaWD4y7cYrAMTglAQIzhQhu6fru1x5tBah6dxF4m8YMFMDa0v4wXzTAm46OeqQgaTUsypx1cu38lhX1jPIjc2fTl63nduc0UgK08J7ukWL3qlx4SXwCWecgX0PPC-X7S9FKASIBrGcOogk8jlShsbfE1cm0NHAbxU0Ct0idHdK_vUodix7Sjf8X7HUWEOyTqPAA1RY0Vi7fXhkNza6ogrAn0w8DQ66kqKA"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```
> Return Values

```
??
```

### Purpose
??
### Pre-Requisites
??
### Call
??

`
/dependency/parent/:id
`
### Return Values
#### 404
When API call is not reachable
### Open Queries
* Need to understand purpose
* list of errors returned by API 

# Ingestion
# Search