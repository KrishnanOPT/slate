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
{"status":"success","data":{"page":0,"totalPages":1,"elements":2,"totalElements":2,"ruleMatches":[{"governanceMatchId":"6018010b5213a86743b77918","commitId":"3132.00","matchedOn":"2021-02-01T13:24:26.979Z","author":"1830468e-0d24-4e58-9f1d-6c5136b8548a","auditRuleId":"601800e55213a86743b7470f","auditRuleName":"Created By Automation","snapshotId":"8b8aa4d5-97a7-3fc5-aee5-5d0984dd6167","changeDescription":"AffectedObject: crosscode-core-services-0.0.7-SNAPSHOT.jar\n\nnew object: crosscode-core-services-0.0.7-SNAPSHOT.jar"},{"governanceMatchId":"6018010c5213a86743b7792d","commitId":"3133.00","matchedOn":"2021-02-01T13:24:28.283Z","author":"1830468e-0d24-4e58-9f1d-6c5136b8548a","auditRuleId":"601800e55213a86743b7470f","auditRuleName":"Created By Automation","snapshotId":"87474358-c6fb-3c94-93c6-521dbfa864e4","changeDescription":"AffectedObject: Code-First-Demo\n\nnew object: Code-First-Demo"}]}}
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

# AuthController
# Dependency
# Ingestion