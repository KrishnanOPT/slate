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

OnPath

# Governance
## History
### Get Audit history dates
> To get the dates of audit, use this code:

```shell
curl --location --request GET '{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/audit/history/68bcd5a4-5707-32a5-b500-77b6467180ca/dates?page=0&size=10' \
--header 'Content-Type: application/json' \
--data-raw '{
	"name" : "Any Database Added",
	"ruleType" : "Added",
	"firstNode" : "Database"
}'
```

```javascript
var settings = {
  "url": "{{http(s)}}://{{baseUrl}}:{{basePort}}{{contextPath}}/audit/history/68bcd5a4-5707-32a5-b500-77b6467180ca/dates?page=0&size=10",
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
> Make sure to use the correct values for variables `{{http(s)}}, {{baseUrl}}, {{basePort}}, {{contextPath}}`

> The above command returns JSON structured like this:

```json
{
	"name" : "Any Database Added",
	"ruleType" : "Added",
	"firstNode" : "Database"
}
```
#### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
cdoId |  | An example is 68bcd5a4-5707-32a5-b500-77b6467180ca

<aside class="success">
Will list all the audit dates
</aside>

## Rules
## Matches
# FusionAuth
# AuthController
# Dependency
# Ingestion