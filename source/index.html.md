---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - python
  
toc_footers:
  - <a href='https://welkinhealth.com'>Visit our Website</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

Welcome to Welkin V8 Release.

Welkin is currently in Closed Beta state, and APIs are subject to changes

For better demonstration of the API, we will use:

1. Organization (Tenant): **gh**
2. Instance (Environment): **sb-demo**

In order to better understand what it means, lets review the URL structure


and 

`Patients URL Structure: "https://api.{}.welkincloud.io/{}/admin/api_clients/{}"`

The first variable is Environment type. For most of your use cases, that would be "live", 
though "sandbox" is going to be supported soon

The second variable is your Organization Name and the t
# Authentication

In order to Authenticate in Welkin, one needs to follow few steps:

1. Create API client in your Organization 
   * Navigate to Admin -> API Clients -> Create Client
   * Copy the Client Name and Secret Key or download it. 
   For this example we will assume Client Name is **QRUPCFEHJRJK**
   and Secret Key is **+}B{KGTG6#zG%P;tQm0C**
2. Navigate to the API Client page you created
   * Configure appropriate access for the client (Instance Access, Roles, Security Policies)

Welkin V8 Token URL follows convention that can be described like this:
 
`Token URL Structure: "https://api.{}.welkincloud.io/{}/admin/api_clients/{}"`

> To authorize, use this code:

```python
    import requests
    TOKEN_BASE_URL = "https://api.{}.welkincloud.io/{}/admin/api_clients/{}"

    token_url = TOKEN_BASE_URL.format("live", "gh", "QRUPCFEHJRJK")
    print("Token URL {} ".format(token_url))

    params = {'secret': '+}B{KGTG6#zG%P;tQm0C'}
    r = requests.post(token_url, json=params)
    print("Response Code: {}".format(r.status_code))
```
> Make sure to replace `secret` with your Secret Key.

> The above command returns JSON structured like this:

```json
{
  "clientName": "MTNKDGUAGPUE",
  "token": "eyJraWQiOiJvaGloUEZOREk2WmE5WEtXNEVIdTdVaFFob1l3Ull0aFFFMmpIY1MrczZrPSIsImFsZyI6IlJTMjU2In0.eyJjdXN0b206dHlwZSI6IkFQSV9DTElFTlQiLCJzdWIiOiIzZWQyMjNjOS1hNjFmLTRmMDktOGUzMi0wNGRkNjU2NDY2YzQiLCJhdWQiOiIycTJ0YmRnanV0Y3Zqdjg5NGY0Zm4wcXRnMCIsImV2ZW50X2lkIjoiMWVmYTc4MWItMzMzNy00MWI4LWExZjYtNTlmY2ZmYWYzMjgxIiwidG9rZW5fdXNlIjoiaWQiLCJhdXRoX3RpbWUiOjE2MTUyMjg0MjcsImlzcyI6Imh0dHBzOlwvXC9jb2duaXRvLWlkcC51cy1lYXN0LTEuYW1hem9uYXdzLmNvbVwvdXMtZWFzdC0xXzBjOVhLV1pFQSIsImN1c3RvbTppZCI6IjAyZDI0MzU5LTU0ZWYtNGQ4Mi05MmRjLWZiY2RjOTQyNDJjMCIsImNvZ25pdG86dXNlcm5hbWUiOiJNVE5LREdVQUdQVUUiLCJleHAiOjE2MTUyMzIwMjcsImlhdCI6MTYxNTIyODQyN30.ktjPG0CIHP0As8e8I1UGMP1kocvjd4AIeQBZlZ0esMz414Dpsb6gwPNuDhJS-ej_gh_tZNSw4tePdxQcagfJHp64ByOuv3ZtAHPAm5l5dEZOcVxG4l4O45Mn1hIGhqP6vizNVBFlBWTnzYTyPlbJKS2PMeMsWPqxUDKeoEffczr2sb9VptUMg2dgY-vz6VZvZjtpPfWjKjnJHeIVMxUiW-9LcR-6BK2DHj5qwlzOkDs89rnqE_OFMUiyLfQlvQuoglSRUUiXNXGiU88YCNNzzG7fb3luuwFXBAdwWhK7pXM4o355eDp2bH-EFx_q82mJBy7lB0DfZTm1AHHjcn8BXg",
  "enabled": true
}
```




The first variable is Environment type. 
For most of your use cases, that would be **live**, though **sandbox** is going to be supported soon

The second variable is your Organization Name, in our example that is **gh**

The third variable is your Client Name that you previously generated in the steps above: **QRUPCFEHJRJK**

Full URL to obtain token is:

`https://api.live.welkincloud.io/gh/admin/api_clients/QRUPCFEHJRJK`

<aside class="notice">
Don't forget to use your Organization Name and Environment Name and replace the values in this example 
</aside>



# Patients

## Get All Patients

`Patients URL Structure: https://api.{}.welkincloud.io/{}/{}/patients`

In our example that is `https://api.live.welkincloud.io/gh/sb-demo/patients`


### HTTP Request

`GET https://api.live.welkincloud.io/gh/sb-demo/patients`

### Query Parameters

Parameter | Description | Examples
--------- | ----------- | --------
sort |Allows one to specify the sort order of the returned patients collection | https://api.live.welkincloud.io/gh/sb-demo/patients?sort=firstName,desc
email |When specified, will execute a search for a patient based of email address | https://api.live.welkincloud.io/gh/sb-demo/patients?email=1@1.com



```python
import requests
h = {
        "Authorization": "Bearer {}".format(token)
    }

r = requests.get("https://api.live.welkincloud.io/gh/sb-demo/patients", headers=h)
print("Response Code: {}".format(r.status_code))
print(r.json())
```

> The above command returns JSON structured like this:

```json
{"content": 
  [
    {
      "id": "6801d498-26f4-4aee-961b-5daffcf193c8",
      "firstName": "Charlie",
      "lastName": "Schwarzenegger",
      "middleName": "Mc",
      "birthDate": "2012-08-12T00:00:00.000Z",
      "email": "1@1.com",
      "phone": "+13363034233",
      "country": "USA",
      "state": "American Samoa",
      "city": "Los Angeles",
      "zip": "99451",
      "addressLine1": "Hollywood Blvd 2021",
      "timezone ": "America / Los_Angeles",
      "patientTerritories": [],
      "careTeam": []
    }
....pagination links omitted
  ]
}
```

## Create a Patient

### HTTP Request

`POST https://api.live.welkincloud.io/gh/sb-demo/patients`


```python
import requests
h = {
        "Authorization": "Bearer {}".format(token)
    }

data = {
        "firstName": "Charlie",
        "lastName": "Taylor",
        "birthDate": "2012-3-12T00:00:00.000Z",
        "timezone": "America/Los_Angeles",
        "phone": "+15556491369",
        "email": "Charlie.Taylor@superemail.com"
    }

 r = requests.post("https://api.live.welkincloud.io/gh/sb-demo/patients", json=data, headers=h)
print("Response Code: {}".format(r.status_code))
print(r.json())
```

> The above command returns JSON structured like this:

```json

{
  "id": "e3dd671a-86f0-4951-80fb-13b12766292f", 
  "externalGuid": None, 
  "firstName": "Charlie", 
  "lastName": "Taylor", 
  "middleName": None, 
  "birthDate": "2012-03-12T00:00:00.000Z", 
  "email": "Charlie.Taylor@superemail.com", 
  "phone": "+15556491369", 
  "country": None, 
  "state": None, 
  "city": None, 
  "zip": None, 
  "addressLine1": None, 
  "addressLine2": None, 
  "timezone": "America/Los_Angeles", 
  "patientTerritories": None, 
  "careTeam": None
}
```

## Get a Specific Patient

### HTTP Request

`GET https://api.live.welkincloud.io/gh/sb-demo/patients/6801d498-26f4-4aee-961b-5daffcf193c8`


```python
import requests
h = {
        "Authorization": "Bearer {}".format(token)
    }

r = requests.get("https://api.live.welkincloud.io/gh/sb-demo/patients/6801d498-26f4-4aee-961b-5daffcf193c8", 
  headers=h)
print("Response Code: {}".format(r.status_code))
print(r.json())
```

> The above command returns JSON structured like this:

```json
{
  "id": "6801d498-26f4-4aee-961b-5daffcf193c8",
  "firstName": "Charlie",
  "lastName": "Schwarzenegger",
  "middleName": "Mc",
  "birthDate": "2012-08-12T00:00:00.000Z",
  "email": "1@1.com",
  "phone": "+13363034233",
  "country": "USA",
  "state": "American Samoa",
  "city": "Los Angeles",
  "zip": "99451",
  "addressLine1": "Hollywood Blvd 2021",
  "timezone ": "America / Los_Angeles",
  "patientTerritories": [],
}  
```


## Delete a Specific Patient

### HTTP Request

`DELETE https://api.live.welkincloud.io/gh/sb-demo/patients/6801d498-26f4-4aee-961b-5daffcf193c8`

<aside class="notice">
This operation is not supported yet</aside>


