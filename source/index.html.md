---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - python
  
toc_footers:
  - <a href='https://welkinhealth.com'>Visit our Website</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - data_audit
  - security_audit
  - webhook_audit
  - errors
  
search: true

code_clipboard: true
---

# Introduction

<aside class="warning">
Welkin is currently in Closed Beta state, and APIs are subject to changes
</aside>


Welcome to Welkin V8 Release.

When reading this API, we take a liberty and assume that you are familiar with the following Welkin concepts, but for the sake of clarity will shortly repeat them here:

1. **Tenant (Organization)** - This is a customer space, dedicated to one customer. Every customer will have its own tenant that will host customer users, apps and instances
2. **Instance (Environment)** - This is a separate database inside a tenant. Typical customer will have 2-3 instances, representing customer development, testing and live environments, as you build out your Welkin care program
3. **API client** - this is an auto-generated pair of key and secrets, that allows you to access variety of API that Welkin exposes
4. **Security Policies and Roles** - set of rules that dictates what API your client can access and what actions are allowed to be performed
5. **Designer** - Codeless editor for configuring Care Program and all the elements of that program, including Permissions and Roles
6. **Admin** - Admin app that allows one to assign permissions and roles to API clients (among other things)
7. **Care** - Care portal that users will be using to deliver care to patients

For better demonstration of the API, we will use the following setup:

1. Organization (Tenant): **gh**
2. Instance (Environment): **sb-demo**

# Creating API Client
Though this is better covered in our User Guide document, we are going to repeat the steps here, to ensure successful setup

1. Create API client in your Organization 
  * Navigate to Admin -> API Clients -> Create Client
  * Copy the Client Name and Secret Key or download it.

2. Navigate to the API Client page you created
  * Configure appropriate access for the client (Instance Access, Roles, Security Policies)

Reminder: Security Policies and Roles are defined in the Designer and assigned in the Admin

For this example we will assume Client Name is **VBOPNRYRWJIP** and Secret Key is **+}B{KGTG6#zG%P;tQm0C**


# Authentication

> To obtain a Bearer token:

```python
import requests

params = {'secret': '+}B{KGTG6#zG%P;tQm0C'}
r = requests.post('https://api.live.welkincloud.io/gh/admin/api_clients/VBOPNRYRWJIP', json=params)
print(r.json())
```

> Successful response will look like:

```json
{
  "clientName": "VBOPNRYRWJIP",
  "token": "eyJraWQiOiJvaGloUEZOREk2WmE5WEtXNEVIdTdVaFFob1l3Ull0aFFFMmpIY1MrczZrPSIsImFsZyI6IlJTMjU2In0.eyJjdXN0b206dHlwZSI6IkFQSV9DTElFTlQiLCJzdWIiOiIzZWQyMjNjOS1hNjFmLTRmMDktOGUzMi0wNGRkNjU2NDY2YzQiLCJhdWQiOiIycTJ0YmRnanV0Y3Zqdjg5NGY0Zm4wcXRnMCIsImV2ZW50X2lkIjoiMWVmYTc4MWItMzMzNy00MWI4LWExZjYtNTlmY2ZmYWYzMjgxIiwidG9rZW5fdXNlIjoiaWQiLCJhdXRoX3RpbWUiOjE2MTUyMjg0MjcsImlzcyI6Imh0dHBzOlwvXC9jb2duaXRvLWlkcC51cy1lYXN0LTEuYW1hem9uYXdzLmNvbVwvdXMtZWFzdC0xXzBjOVhLV1pFQSIsImN1c3RvbTppZCI6IjAyZDI0MzU5LTU0ZWYtNGQ4Mi05MmRjLWZiY2RjOTQyNDJjMCIsImNvZ25pdG86dXNlcm5hbWUiOiJNVE5LREdVQUdQVUUiLCJleHAiOjE2MTUyMzIwMjcsImlhdCI6MTYxNTIyODQyN30.ktjPG0CIHP0As8e8I1UGMP1kocvjd4AIeQBZlZ0esMz414Dpsb6gwPNuDhJS-ej_gh_tZNSw4tePdxQcagfJHp64ByOuv3ZtAHPAm5l5dEZOcVxG4l4O45Mn1hIGhqP6vizNVBFlBWTnzYTyPlbJKS2PMeMsWPqxUDKeoEffczr2sb9VptUMg2dgY-vz6VZvZjtpPfWjKjnJHeIVMxUiW-9LcR-6BK2DHj5qwlzOkDs89rnqE_OFMUiyLfQlvQuoglSRUUiXNXGiU88YCNNzzG7fb3luuwFXBAdwWhK7pXM4o355eDp2bH-EFx_q82mJBy7lB0DfZTm1AHHjcn8BXg",
  "enabled": true
}
```

Once you finished the steps, lets review the URL structure that is typically generated for such setup:

`URL Structure: https://api.live.welkincloud.io/{}/admin/api_clients/{}`

There are several variables in this structure:

1. First variable is your Tenant name. We will use **gh** as a tenant name through this set of api docs
2. Second variable is your client name. We will use **VBOPNRYRWJIP** as a api client name


In order to Authenticate in Welkin, one needs to follow few steps:

1. HTTP Method: POST
2. HTTP URL: `https://api.live.welkincloud.io/gh/admin/api_clients/VBOPNRYRWJIP` 
3. HTTP Reponse Codes: 201, 400, 500

There are three field in response object:

Field Name | Description | Examples
--------- | ----------- | --------
clientName | Echos back the name of API client you used
token | Bearer token that you will use in subsequent requests
enabled | will indicate if the client is enable. This is also controlled in the Admin app

# Patients

Collection of all patients would be located at the following URL

`URL Structure: https://api.live.welkincloud.io/{}/{}/patients`

In our example that is `https://api.live.welkincloud.io/gh/sb-demo/patients`

The collection supports several interactions

1. Allows to obtain a list of patients (can be sorted)
2. Allows to obtain a filtered list of patients based of email address (commonly referred as FINDER)
2. Allows to create a new patient

## Get All Patients

```python
import requests
h = {
        "Authorization": "Bearer {}".format(token)
    }

r = requests.get("https://api.live.welkincloud.io/gh/sb-demo/patients", headers=h)
print(r.json())
```

> The above request returns JSON structured like this:

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

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patients`
3. HTTP Reponse Codes: 201, 400, 500

Following Query Parameters can be used to sort or find approporiately

Parameter | Description | Examples
--------- | ----------- | --------
sort |Allows one to specify the sort order of the returned patients collection | https://api.live.welkincloud.io/gh/sb-demo/patients?sort=firstName,desc
email |When specified, will execute a search for a patient based of email address | https://api.live.welkincloud.io/gh/sb-demo/patients?email=1@1.com


## Create a Patient

Creating a new Patient is a simple as posting to a Patient Collection resource

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
print(r.json())
```

> The above request returns JSON structured like this:

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
1. HTTP Method: POST
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patients`
3. HTTP Reponse Codes: 201, 400, 500



## Get a Specific Patient By ID

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

To get a patient by a known ID

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patients/6801d498-26f4-4aee-961b-5daffcf193c8`
3. HTTP Reponse Codes: 200, 400, 500


## Delete a Specific Patient

<aside class="warning">
This operation is not supported yet
</aside>

# Custom Data Types (CDT)

Custom data types in Welkin are associated with a Patient. In REST terms, they are a sub-resource to the patient object

Each CDT has a set of system fields associated with it and a set of custom fields that you will create in the designer

## System Fields

Field Name | Type | Description
--------- | ----------- | --------
id | UUID | Unique autogenerated identifier
updated_by | UUID |UUID of user or client who updated the record
updated_by_name | String | Full name of the user or api client that updated the record
updated_at | Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | Date and time of the last update to the record 
created_by | UUID | UUID of user or client who created the record
created_by_name | String | Full name of the user or api client that created the record
created_at| Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | Date and time when the record was created 
source_type | String | Source type of the record (for example: ASSESSMENT if assessment type  generated this record)
source_name | String | Name of the source type (for example: my_medication_assessment if assessment type  generated this record)
source_id | UUID | record ID of the source

## Working with CDT records

Lets examine the URL structure

`https://api.live.welkincloud.io/{tenant}/{instance}/patients/{patient-id}/cdts/{cdt-name}/{cdt-record-id}`


Let's consider the following example.
CDT that was created in the designer is **vitals** with three fields
1. blood_sugar
2. systolic
3. diastolic

In our example the collection URL is
`https://api.live.welkincloud.io/gh/sb-demo/patients/6801d498-26f4-4aee-961b-5daffcf193c8/cdt/vitals`

This collection is collection of records for a vitals cdt object, associated with a specific patient as described by the patient id

## Create CDT Record

```python
import requests
h = {
        "Authorization": "Bearer {}".format(token)
}

data = {
    "blood_sugar": random.randint(90, 300),
    "diastolic": random.randint(90, 220),
    "systolic": random.randint(60, 140),
}

r = requests.post("https://api.live.welkincloud.io/gh/sb-demo/patients/a02a0310-5fca-4af8-aa87-c14d6b4d5723/cdt/vitals", 
  json=data, headers=h)

print("Response Code: {}".format(r.status_code))
print(r.json())
```
> The above request returns JSON of the created record, with system fields 

```json

{
  "id": "e46bfff7-62c9-407b-a0a1-5d522aeab9d0",
  "patientId": "a02a0310-5fca-4af8-aa87-c14d6b4d5723",
  "cdtId": "11f9d7c0-5065-433e-937e-8abfee98ff31",
  "version": 5,
  "jsonBody": {
    "created_at": "2021-03-22T06:40:08.482Z",
    "source_type": None,
    "created_by_name": "API_CLIENT:VBOPNRYRWJIP",
    "created_by": "16d7a4ff-cce4-4c9c-bcc9-74d1b00b72bf",
    "updated_by_name": "API_CLIENT:VBOPNRYRWJIP",
    "diastolic": 174,
    "systolic": 100,
    "updated_at": "2021-03-22T06:40:08.482Z",
    "updated_by": "16d7a4ff-cce4-4c9c-bcc9-74d1b00b72bf",
    "id": "e46bfff7-62c9-407b-a0a1-5d522aeab9d0",
    "source_id": None,
    "blood_sugar": 196,
    "source_name": None
  }
}
```
1. HTTP Method: POST
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patients/a02a0310-5fca-4af8-aa87-c14d6b4d5723/cdt/vitals` 
3. HTTP Reponse Codes: 201, 400, 500


## Reading CDT Record

```python
import requests
h = {
        "Authorization": "Bearer {}".format(token)
}


r = requests.get("https://api.live.welkincloud.io/gh/sb-demo/patients/a02a0310-5fca-4af8-aa87-c14d6b4d5723/cdt/vitals/11f9d7c0-5065-433e-937e-8abfee98ff31", headers=h)

print("Response Code: {}".format(r.status_code))
print(r.json())
```
> The above request returns JSON of the created record, with system fields 

```json

{
  "id": "e46bfff7-62c9-407b-a0a1-5d522aeab9d0",
  "patientId": "a02a0310-5fca-4af8-aa87-c14d6b4d5723",
  "cdtId": "11f9d7c0-5065-433e-937e-8abfee98ff31",
  "version": 5,
  "jsonBody": {
    "created_at": "2021-03-22T06:40:08.482Z",
    "source_type": None,
    "created_by_name": "API_CLIENT:VBOPNRYRWJIP",
    "created_by": "16d7a4ff-cce4-4c9c-bcc9-74d1b00b72bf",
    "updated_by_name": "API_CLIENT:VBOPNRYRWJIP",
    "diastolic": 174,
    "systolic": 100,
    "updated_at": "2021-03-22T06:40:08.482Z",
    "updated_by": "16d7a4ff-cce4-4c9c-bcc9-74d1b00b72bf",
    "id": "e46bfff7-62c9-407b-a0a1-5d522aeab9d0",
    "source_id": None,
    "blood_sugar": 196,
    "source_name": None
  }
}
```
1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patients/a02a0310-5fca-4af8-aa87-c14d6b4d5723/cdt/vitals/11f9d7c0-5065-433e-937e-8abfee98ff31` 
3. HTTP Reponse Codes: 200, 400, 500


## Updating CDT Record

```python
import requests
h = {
    "Authorization": "Bearer {}".format(token)
}

data = {
    "blood_sugar": "200",
}

r = requests.patch("https://api.live.welkincloud.io/gh/sb-demo/patients/a02a0310-5fca-4af8-aa87-c14d6b4d5723/cdt/vitals", 
  json=data, headers=h)

print("Response Code: {}".format(r.status_code))
print(r.json())
```
> The above request returns JSON of the record, with system fields 

```json

{
  "id": "e46bfff7-62c9-407b-a0a1-5d522aeab9d0",
  "patientId": "a02a0310-5fca-4af8-aa87-c14d6b4d5723",
  "cdtId": "11f9d7c0-5065-433e-937e-8abfee98ff31",
  "version": 5,
  "jsonBody": {
    "created_at": "2021-03-22T06:40:08.482Z",
    "source_type": None,
    "created_by_name": "API_CLIENT:VBOPNRYRWJIP",
    "created_by": "16d7a4ff-cce4-4c9c-bcc9-74d1b00b72bf",
    "updated_by_name": "API_CLIENT:VBOPNRYRWJIP",
    "diastolic": 165,
    "systolic": 128,
    "updated_at": "2021-03-22T06:50:37.739Z",
    "updated_by": "16d7a4ff-cce4-4c9c-bcc9-74d1b00b72bf",
    "id": "e46bfff7-62c9-407b-a0a1-5d522aeab9d0",
    "source_id": None,
    "blood_sugar": 200,
    "source_name": None
  }
}
```

All updates are partial updates, meaning that we will update only the fields you will send to the server

1. HTTP Method: PATCH
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patients/a02a0310-5fca-4af8-aa87-c14d6b4d5723/cdt/vitals/11f9d7c0-5065-433e-937e-8abfee98ff31` 
3. HTTP Reponse Codes: 200, 400, 500

## Find CDT records

Use finder parameters to filter output of the collection for a given patient

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patients/a02a0310-5fca-4af8-aa87-c14d6b4d5723/cdt/vitals` 

Parameters| Format | Description
--------- | ----------- | --------
fields | <list fields> | fields=name,phone
page | page number Integer |UUID of user or client who updated the record
size | page size Integer
filters | key=v1,v2,v3
dateStart | Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | dateStart=2021-01-28T23:10:04.874Z
dateEnd |Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | dateEnd=2021-01-28T23:10:04.874Z

# Users

This API allows one to work with User records

## Create User Record

```json     
{
   "username": "johndoe",
   "email": "j.doe@email.com",
   "phone": "+15552009845",
   "timezone": "America/Los_Angeles",
   "firstName": "John",
   "lastName": "Doe",
   "credentials": "MD"
}
```

Users API url consist of the following structure

`https://api.live.welkincloud.io/{}/admin/users` 

In our example, the url would be:
`https://api.live.welkincloud.io/gh/admin/users` 




1. HTTP Method: POST
2. HTTP URL: `https://api.live.welkincloud.io/gh/admin/users` 


## Read User Record

```json     
{
   "username": "johndoe",
   "email": "j.doe@email.com",
   "phone": "+15552009845",
   "timezone": "America/Los_Angeles",
   "firstName": "John",
   "lastName": "Doe",
   "credentials": "MD"
}
```

User Record API url consist of the following structure

`https://api.live.welkincloud.io/{}/admin/users/{}` 

In our example, the url would be:
`https://api.live.welkincloud.io/gh/admin/users/johndoe` 

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/admin/users/johndoe` 

## Update User Record (Partial update)

```json     
{
   "username": "johndoe",
   "email": "j.doe@email.com",
   "phone": "+15552009845",
   "timezone": "America/Los_Angeles",
   "firstName": "John",
   "lastName": "Doe",
   "credentials": "MD"
}
```

If you with to update some of the user fields, but not all, you can use `PATCH`

1. HTTP Method: PATCH
2. HTTP URL: `https://api.live.welkincloud.io/gh/admin/users/johndoe` 


## Update User Record (Full update)

```json     
{
   "username": "johndoe",
   "email": "j.doe@email.com",
   "phone": "+15552009845",
   "timezone": "America/Los_Angeles",
   "firstName": "John",
   "lastName": "Doe",
   "credentials": "MD"
}
```

If you with to update entire User Object, you can use `PUT`

1. HTTP Method: PUT
2. HTTP URL: `https://api.live.welkincloud.io/gh/admin/users/johndoe` 


## Delete User Record 

1. HTTP Method: DELETE
2. HTTP URL: `https://api.live.welkincloud.io/gh/admin/users/johndoe` 


# Calendar

## Working Hours


```json
{
 "psmId": "28f393a8-62b3-4b4b-aa42-da769ce4489a",
 "createdBy": "28f393a8-62b3-4b4b-aa42-da769ce4489a",
 "startDateTime": "2020-01-01T00:00:00.000Z",
 "endDateTime": "2020-01-31T23:59:59.000Z",
 "daysInfo": [
   {
     "day": 1,
     "startTime": "09:00:00",
     "endTime": "18:00:00"
   },
   {
     "day": 2,
     "startTime": "09:00:00",
     "endTime": "18:00:00"
   }
 ]
}
```

Note: 
1. psmId is userId. We will change it in the future releases to reflect that
2. day field represents day of week (1 - monday, 2 - tuesday, ...)



Using Working Hours API, users (doctors, clinicians) can set flexible working hours that vary from week to week. It is beneficial for people involved part-time.



`URL Structure: {{url}} / {{tenantName}} / {{instanceName}} /calendar/ work-hours`

in our example it would be:
`https://api.live.welkincloud.io/gh/sb-demo/calendar/work-hours`

1. HTTP Method: POST
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/calendar/work-hours`

## Read Work Hours
```json     
[
   {
       "psmId": "28f393a8-62b3-4b4b-aa42-da769ce4489a",
       "details": [
           {
               "workHoursId": "d22d0c67-691f-4f1c-991b-09cce97ec7ce",
               "createdBy": "28f393a8-62b3-4b4b-aa42-da769ce4489a",
               "createdAt": "2021-01-14T02:31:55.000Z",
               "updatedBy": "28f393a8-62b3-4b4b-aa42-da769ce4489a",
               "updatedAt": "2021-01-14T02:31:55.000Z",
               "startDateTime": "2020-01-01T00:00:00.000Z",
               "endDateTime": "2020-01-31T23:59:59.000Z",
               "daysInfo": [
                   {
                       "daysInfoId": "249414bb-a6a5-42a2-9ddf-d75ce16dcae3",
                       "startTime": "09:00:00",
                       "endTime": "18:00:00",
                       "day": 1
                   }
               ]
           }
       ]
   }
]
```

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/calendar/work-hours`

Parameters| Format | Description
--------- | ----------- | --------
psm-ids | list of id and values | psm-ids=28f393a8-62b3-4b4b-aa42-da769ce4489
from | Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | from=2021-01-28T23:10:04.874Z
to |Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | to=2021-01-28T23:10:04.874Z

Example:
1. `https://api.live.welkincloud.io/gh/sb-demo/calendar/work-hours
?psm-ids=28f393a8-62b3-4b4b-aa42-da769ce4489a
&from=2020-01-01T00:00:00.000Z
&to=2020-01-31T23:59:59.000Z
`

2. `https://api.live.welkincloud.io/gh/sb-demo/calendar/work-hours
?psm-ids=28f393a8-62b3-4b4b-aa42-da769ce4489a,18f393a8-62b3-4b4b-aa42-da769ce4489a
&from=2020-01-01T00:00:00.000Z
&to=2020-01-31T23:59:59.000Z
`

## Update Work Hours

Updating work hours by ID

```json
{
 "psmId": "28f393a8-62b3-4b4b-aa42-da769ce4489a",
 "updatedBy": "28f393a8-62b3-4b4b-aa42-da769ce4489a",
 "startDateTime": "2020-01-01T00:00:00.000Z",
 "endDateTime": "2020-01-31T23:59:59.000Z",
 "daysInfo": [
   {
     "day": 1,
     "startTime": "10:00:00",
     "endTime": "19:00:00"
   },
   {
     "day": 2,
     "startTime": "10:00:00",
     "endTime": "19:00:00"
   }
 ]
}
```
1. HTTP Method: PUT
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/calendar/work-hours/c7a4251f-d70e-4ccb-8c96-1038c76fd737`

# Calendar Events

```json
{
 "createdBy": "28f393a8-62b3-4b4b-aa42-da769ce4489a",
 "eventTitle": "Weekly Appointment with Jack",
 "eventDescription": "",
 "startDateTime": "2020-01-01T00:00:00.000Z",
 "endDateTime": "2020-01-31T23:59:59.000Z",
 "eventType": "APPOINTMENT",
 "eventStatus": "SCHEDULED",
 "eventMode": "IN-PERSON",
 "hostId": "28f393a8-62b3-4b4b-aa42-da769ce4489a",
 "additionalInfo": {
   "location": "",
   "remarks": "",
   "attachment": ""
 },
 "participants": [
   {
     "participantId": "28f393a8-62b3-4b4b-aa42-da769ce4489a",
     "participantRole": "psm",
     "attended": false
   },
   {
     "participantId": "2279cbc9-0cb5-410b-9566-7f22b8f4263f",
     "participantRole": "patient",
     "attended": false
   }
 ]
}

```

It is a typical calendar API to create and manage events

`URL Structure: {{url}} / {{tenantName}} / {{instanceName}} /calendar/ events`

in our example it would be:
`https://api.live.welkincloud.io/gh/sb-demo/calendar/events`

Fields description: 

Field Name|  Supported Values
--------- |  ----------------
eventType | "GROUP_THERAPY", "APPOINTMENT", "LEAVE"
eventStatus |"SCHEDULED", "CANCELLED", "COMPLETED", "MISSED"
eventMode | "IN-PERSON", "CALL", "VIDEO"
participantRole | "patient", "psm"

## Create Calendar Event

1. HTTP Method: POST
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/calendar/events`

## Get Event By ID

```json
{
 "createdBy": "28f393a8-62b3-4b4b-aa42-da769ce4489a",
 "eventTitle": "Weekly Appointment with Jack",
 "eventDescription": "",
 "startDateTime": "2020-01-01T00:00:00.000Z",
 "endDateTime": "2020-01-31T23:59:59.000Z",
 "eventType": "APPOINTMENT",
 "eventStatus": "SCHEDULED",
 "eventMode": "IN-PERSON",
 "hostId": "28f393a8-62b3-4b4b-aa42-da769ce4489a",
 "additionalInfo": {
   "location": "",
   "remarks": "",
   "attachment": ""
 },
 "participants": [
   {
     "participantId": "28f393a8-62b3-4b4b-aa42-da769ce4489a",
     "participantRole": "psm",
     "attended": false
   },
   {
     "participantId": "2279cbc9-0cb5-410b-9566-7f22b8f4263f",
     "participantRole": "patient",
     "attended": false
   }
 ]
}

```

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/calendar/events/2dfbd113-5282-4f70-b456-d8cf7ecb5573`

## Find Events

```json
{
   "content": [
       {
           "id": "62b94a26-7ec4-478f-baaf-bca9c8d20d88",
           "createdBy": "28f393a8-62b3-4b4b-aa42-da769ce4489a",
           "createdAt": "2020-12-18T11:19:46.000Z",
           "updatedBy": "28f393a8-62b3-4b4b-aa42-da769ce4489a",
           "updatedAt": "2020-12-18T14:34:37.000Z",
           "eventTitle": "Patient Appointment",
           "eventDescription": "problem in hands",
           "startDateTime": "2020-01-15T16:00:00.000Z",
           "endDateTime": "2020-01-15T17:00:00.000Z",
           "allDayEvent": false,
           "duration": 3600,
           "eventType": "APPOINTMENT",
           "eventStatus": "RESCHEDULED",
           "eventMode": "IN-PERSON",
           "hostId": "28f393a8-62b3-4b4b-aa42-da769ce4489a",
           "additionalInfo": {
               "remarks": "Please wear mask",
               "location": "Room 1408",
               "attachment": ""
           },
           "participants": [
               {
                   "id": "544286e3-9b5f-4f4a-bda0-a038878b87a3",
                   "participantId": "28f393a8-62b3-4b4b-aa42-da769ce4489a",
                   "participantRole": "psm",
                   "participationStatus": "Yes",
                   "attended": false
               }
           ]
       }
   ],
   "pageable": {
       "sort": {
           "sorted": false,
           "unsorted": true,
           "empty": true
       },
       "offset": 0,
       "pageNumber": 0,
       "pageSize": 20,
       "paged": true,
       "unpaged": false
   },
   "last": true,
   "totalPages": 1,
   "totalElements": 1,
   "size": 20,
   "number": 0,
   "sort": {
       "sorted": false,
       "unsorted": true,
       "empty": true
   },
   "numberOfElements": 1,
   "first": true,
   "empty": false
}

```

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/calendar/events/2dfbd113-5282-4f70-b456-d8cf7ecb5573`

Parameters| Format | Description
--------- | ----------- | --------
participantIds | list of id and values, either users or patients | participantIds=28f393a8-62b3-4b4b-aa42-da769ce4489
from | Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | from=2021-01-28T23:10:04.874Z
to |Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | to=2021-01-28T23:10:04.874Z
eventType | Enum of allowed values | "GROUP_THERAPY", "APPOINTMENT", "LEAVE"

## Update Calendar Event by ID

```json
{
 "updatedBy": "28f393a8-62b3-4b4b-aa42-da769ce4489a",
 "eventTitle": "Patient Appointment",
 "eventDescription": "problem in hands",
 "startDateTime": "2020-01-15T16:00:00.000Z",
 "endDateTime": "2020-01-15T17:00:00.000Z",
 "eventType": "APPOINTMENT",
 "eventStatus": "SCHEDULED",
 "eventMode": "IN-PERSON",
 "hostId": "28f393a8-62b3-4b4b-aa42-da769ce4489a",
 "additionalInfo": {
   "location": "Room 1408",
   "remarks": "Please wear mask",
   "attachment": ""
 },
 "participants": [
   {
     "id": "4ebfd582-3b20-43d9-b4ee-e658194caeb0",
     "participantId": "28f393a8-62b3-4b4b-aa42-da769ce4489a",
     "participantRole": "psm",
     "attended": false
   },
   {
     "id": "9fe72d19-c0c8-4ebe-8a91-e8f19d4ca7bc",
     "participantId": "28f393a8-62b3-4b4b-aa42-da769ce4489b",
     "participantRole": "patient",
     "attended": false
   }
 ]
}

```

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/calendar/events/2dfbd113-5282-4f70-b456-d8cf7ecb5573`

## Update event invitation response by ID

```json
{
   "participantId": "2279cbc9-0cb5-410b-9566-7f22b8f4263f",
   "participationStatus": "Yes"
}

```
1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/calendar/events/2dfbd113-5282-4f70-b456-d8cf7ecb5573/invitation-response`


## Delete Calendar Event by ID

Note: Only future events can be deleted

1. HTTP Method: DELETE
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/calendar/events/2dfbd113-5282-4f70-b456-d8cf7ecb5573`

## Get Summary for the User

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/calendar/psm-event-summary?from=2020-01-15T14:00:00.000Z&to=2020-02-11T00:00:00.000Z&psmIds=28f393a8-62b3-4b4b-aa42-da769ce4489a`

Parameters| Format | Description
--------- | ----------- | --------
psm-ids | user id | psm-ids=28f393a8-62b3-4b4b-aa42-da769ce4489
from | Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | from=2021-01-28T23:10:04.874Z
to |Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | to=2021-01-28T23:10:04.874Z

# Schedule

There are two APIs that are relevant to the schedules feature:

## Get Schedules

`URL Structure: {{url}} / {{tenantName}} / {{instanceName}} / calendar /psm-schedules`

in our example it would be:
`https://api.live.welkincloud.io/gh/sb-demo/calendar/psm-schedules`


Parameters| Format | Description
--------- | ----------- | --------
psmIds | list of id and values | psmIds=28f393a8-62b3-4b4b-aa42-da769ce4489
from | Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | from=2021-01-28T23:10:04.874Z
to |Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | to=2021-01-28T23:10:04.874Z

Example:

`https://api.live.welkincloud.io/gh/sb-demo/calendar/psm-schedules
?psmIds=28f393a8-62b3-4b4b-aa42-da769ce4489a,18f393a8-62b3-4b4b-aa42-da769ce4489a
&from=2020-01-01T00:00:00.000Z
&to=2020-01-31T23:59:59.000Z
`

## Get Available Schedules

`URL Structure: {{url}} / {{tenantName}} / {{instanceName}} / calendar / available-psm-schedules`

in our example it would be:
`https://api.live.welkincloud.io/gh/sb-demo/calendar/available-psm-schedules`


Parameters| Format | Description
--------- | ----------- | --------
psmIds | list of id and values | psmIds=28f393a8-62b3-4b4b-aa42-da769ce4489
from | Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | from=2021-01-28T23:10:04.874Z
to |Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | to=2021-01-28T23:10:04.874Z

Example:

`https://api.live.welkincloud.io/gh/sb-demo/calendar/psm-schedules
?psmIds=28f393a8-62b3-4b4b-aa42-da769ce4489a,18f393a8-62b3-4b4b-aa42-da769ce4489a
&from=2020-01-01T00:00:00.000Z
&to=2020-01-31T23:59:59.000Z
`


