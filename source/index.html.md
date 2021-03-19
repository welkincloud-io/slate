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

# Custom Data Types (CDT)

Custom data types in Welkin are associated with a Patient. In REST terms, they are a sub-resource to the patient object

`CDT URL Structure: https://api.{env}.welkincloud.io/{tenant}/{instance}/patients/{patient-id}/cdts/{cdt-name}/{cdt-record-id}`

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

Let's consider the following example.
CDT that was created in the designer is **medication** with three fields
1. medication_name
2. medication_status
3. medication_start_date

In our example the collection URL is
`https://api.live.welkincloud.io/gh/sb-demo/patients/6801d498-26f4-4aee-961b-5daffcf193c8/cdt/medication`

## Create CDT Record

1. HTTP Method: POST
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patients/6801d498-26f4-4aee-961b-5daffcf193c8/cdt/medication` 
3. Request Body:
`    
  {
      "medication_name": "Tylenol",
      "medication_status": "active",
      "medication_start_date": "2012-04-23T18:25:43.511Z"
  }
`

```python
import requests
h = {
        "Authorization": "Bearer {}".format(token)
}

data = {
      "medication_name": "Tylenol",
      "medication_status": "active",
      "medication_start_date": "2012-04-23T18:25:43.511Z"
}

r = requests.post("https://api.live.welkincloud.io/gh/sb-demo/patients/6801d498-26f4-4aee-961b-5daffcf193c8/cdt/medication", 
  json=data, headers=h)

print("Response Code: {}".format(r.status_code))
print(r.json())
```

> The above command returns JSON of the created record, with system fields 
> HTTP Status for success is 201

## Reading CDT Record
1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patients/6801d498-26f4-4aee-961b-5daffcf193c8/cdt/medication/758463f9-0f7a-4696-8819-8c6d09f10375` 


```python
import requests
h = {
        "Authorization": "Bearer {}".format(token)
}


r = requests.get("https://api.live.welkincloud.io/gh/sb-demo/patients/6801d498-26f4-4aee-961b-5daffcf193c8/cdt/medication/758463f9-0f7a-4696-8819-8c6d09f10375", headers=h)

print("Response Code: {}".format(r.status_code))
print(r.json())
```
> The above command returns JSON of the record, with system fields 
> HTTP Status for success is 200

## Updating CDT Record
All updates are partial updates, meaning that we will update only the fields you will send to the server

1. HTTP Method: PATCH
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patients/6801d498-26f4-4aee-961b-5daffcf193c8/cdt/medication/758463f9-0f7a-4696-8819-8c6d09f10375` 


```python
import requests
h = {
        "Authorization": "Bearer {}".format(token)
}

data = {
      "medication_status": "inactive",
}

r = requests.patch("https://api.live.welkincloud.io/gh/sb-demo/patients/6801d498-26f4-4aee-961b-5daffcf193c8/cdt/medication", 
  json=data, headers=h)

print("Response Code: {}".format(r.status_code))
print(r.json())
```
> The above command returns JSON of the record, with system fields 
> HTTP Status for success is 200

## Find CDT records

Read multiple records example return all records. Use finder parameters to filter output

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patients/6801d498-26f4-4aee-961b-5daffcf193c8/cdt/medication` 

Parameters| Format | Description
--------- | ----------- | --------
fields | <list fields> | fields=name,phone
page | page number Integer |UUID of user or client who updated the record
size | page size Integer
filters | key=v1,v2,v3
dateStart | Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | dateStart=2021-01-28T23:10:04.874Z
dateEnd |Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | dateEnd=2021-01-28T23:10:04.874Z

# Users

Users API url consist of the following structure
1. {{url}}
2. {{tenantName}} - a tenant name reserved reserved for your company
3. {{instanceName}} - a name of HCRM instance
4. {{patientId}} - an id of Patient

In our example, the url would be:
`https://api.live.welkincloud.io/gh/admin/users` 

## Create User Record

```     
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

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/admin/users` 
3. Request Body (on the right -->)



## Read User Record
```     
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

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/admin/users/johndoe` 




## Update User Record (Partial update)

```     
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

```     
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


```
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
```     
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

```
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

```
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

```
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

```
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

```
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

```
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



