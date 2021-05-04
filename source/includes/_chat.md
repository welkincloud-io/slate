# Chat

`URL Structure: {{url}} / {{tenantName}} / {{instanceName}} / patient / {{patientId}} / chat`

in our example it would be:

`https://api.live.welkincloud.io/gh/sb-demo/calendar/events`


## Send message 

```python
import requests
h = {
    "Authorization": "Bearer {}".format(token)
}
data = {
    "message": "hello, world!"
}

r = requests.post("https://api.live.welkincloud.io/gh/sb-demo/patient/7272b601-bb09-4abf-87c0-ade48ddfaea0/chat/inbound", 
  json=data, headers=h)

print("Response Code: {}".format(r.status_code))
print(r.json())
```

> Returned json

```json
{
   "sender": {
       "clientType": "PATIENT",
       "id": "5cccfad8-c7b0-4fe8-a01e-eb80c0b234ab",
       "titleName": null
   },
   "message": "hello, world!",
   "externalId": "IM6f03096c79094f9b9466c7d009073ca1",
   "createdAt": "2021-02-08T17:17:29.000Z"
}
```

Send message from patient to care team. 

`URL Structure: {{url}} / {{tenantName}} / {{instanceName}} / patient / {{patientId}} / chat / inbound`

in our example it would be:

`https://api.live.welkincloud.io/gh/sb-demo/patient/7272b601-bb09-4abf-87c0-ade48ddfaea0/chat/inbound`

## Webhook

Webhook are sent to the configured endpoint when user sends a message to the patient. Webhooks are configured in the welkin admin panel. 

> Headers

```
X-WEBHOOK-API-KEY: Configured 3rdparty Api key
X-WEBHOOK-API-SECRET: Configured 3rdparty Api secret
```

> Webhook body

```json
{
  "patientId": "cdb303e7-844f-40f8-b634-fe99bfccce28",
  "patientUrl": "http://localhost:5000/test-den/chat2/patients/cdb303e7-844f-40f8-b634-fe99bfccce28",
  "tenantName": "test-den",
  "instanceName": "chat2",
  "message": "Webhook test..."
}

```

## Get messages

```python
import requests
h = {
    "Authorization": "Bearer {}".format(token)
}

r = requests.get("https://api.live.welkincloud.io/gh/sb-demo/patient/7272b601-bb09-4abf-87c0-ade48ddfaea0/chat", 
   headers=h)

print("Response Code: {}".format(r.status_code))
print(r.json())
```

> Returned json

```json
{
   "meta": {
       "nextPageToken": "eyJ0eXBlIjoiUFJPVklERVIiLCJ0d2lsaW9Ub2tlbiI6Ik9yZGVyPWRlc2MmUGFnZVNpemU9MSZQYWdlPTEmUGFnZVRva2VuPVBUMTAifQ==",
       "prevPageToken": null,
       "pageSize": 1,
       "found": true
   },
   "content": [
       {
           "sender": {
               "clientType": "USER",
               "id": "379a1c22-aac4-4741-a083-c3c80105ee94",
               "titleName": "Root Root"
           },
           "message": "Hello, World!",
           "externalId": "IMa1614231a02d456a84d6ad6e193adb66",
           "createdAt": "2021-03-09T12:23:18.000Z"
       }
   ]
}
```


Get messages for patient. 

`URL Structure: {{url}} / {{tenantName}} / {{instanceName}} / patient / {{patientId}} / chat `

in our example it would be:

`https://api.live.welkincloud.io/gh/sb-demo/patient/7272b601-bb09-4abf-87c0-ade48ddfaea0/chat`

### Query parametrs: 

Parameters| Description
--------- |  --------
includeArchived | if true, include archived messages to the result
pageSize | page size, mutually exclusive with pageToken
pageToken | token for fetching specific page, mutually exclusive with pageSize

### Response fields

Field | Description
--------- |  --------
nextPageToken | Token for receiving next page (null if this  page is last)
prevPageToken | Token for receiving previous page (null if this page is first)

## Search messages

```json
{
   "meta": {
       "nextPageToken": "eyJ0eXBlIjoiTE9DQUxfU0VBUkNIIiwicGFnZVNpemUiOjIsImJvcmRlckRhdGUiOiIyMDIxLTAzLTA1VDE2OjA3OjMxLjI5OFoiLCJxdWVyeSI6ImhlbGxvIiwiYmVmb3JlIjp0cnVlfQ==",
       "prevPageToken": "eyJ0eXBlIjoiTE9DQUxfU0VBUkNIIiwicGFnZVNpemUiOjIsImJvcmRlckRhdGUiOiIyMDIxLTAzLTA1VDE2OjA5OjUyLjYNVoiLCJxdWVyeSI6ImhlbGxvIiwiYmVmb3JlIjpmYWxzZX0=",
       "pageSize": 1,
       "found": true
   },
   "content": [
       {
           "meta": {
               "nextPageToken": "eyJ0eXBlIjoiTE9DQUxfRklORCIsInBhZ2VTaXplIjoyLCJib3JkZXJEYXRlIjoiMjAyMS0wMy0wNVQxNjowOTo1Mi42NTVaIiwiYmVmb3JlIjp0cnVlfQ==",
               "prevPageToken": "eyJ0eXBlIjoiTE9DQUxfRklORCIsInBhZ2VTaXplIjoyLCJib3JkZXJEYXRlIjoiMjAyMS0wMy0wNVQxNjowOTo1Mi42NTVaIiwiYmVmb3JlIjpmYWxzZX0="
           },
           "message": {
               "sender": {
                   "clientType": "PATIENT",
                   "id": "795412db-3bea-499a-be10-3e6839349197",
                   "titleName": null
               },
               "message": "Hello, world!",
               "externalId": "IM1da645db820a497a913d743009e91398",
               "createdAt": "2021-03-05T16:09:52.655Z"
           }
       } 
   ]
}
```