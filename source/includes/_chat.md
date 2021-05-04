# Chat

## Send message 

> Request body

```json
{
    "message": "hello, world!"
}
```

> Response

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


Sending message from patient to care team

## Webhook

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

## Find messages

```json
{
   "meta": {
       "nextPageToken": "eyJ0eXBlIjoiTE9DQUxfU0VBUkNIIiwicGFnZVNpemUiOjIsImJvcmRlckRhdGUiOiIyMDIxLTAzLTA1VDE2OjA2OjQ0LjEyMVoiLCJxdWVyeSI6ImhlbGxvIiwiYmVmb3JlIjp0cnVlfQ==",
       "prevPageToken": "eyJ0eXBlIjoiTE9DQUxfU0VBUkNIIiwicGFnZVNpemUiOjIsImJvcmRlckRhdGUiOiIyMDIxLTAzLTA1VDE2OjA3OjMxLjI5OFoiLCJxdWVyeSI6ImhlbGxvIiwiYmVmb3JlIjpmYWxzZX0=",
       "pageSize": 1,
       "found": true
   },
   "content": [
       {
           "meta": {
               "nextPageToken": "eyJ0eXBlIjoiTE9DQUxfRklORCIsInBhZ2VTaXplIjoyLCJib3JkZXJEYXRlIjoiMjAyMS0wMy0wNVQxNjowNzozMS4yOThaIiwiYmVmb3JlIjp0cnVlfQ==",
               "prevPageToken": "eyJ0eXBlIjoiTE9DQUxfRklORCIsInBhZ2VTaXplIjoyLCJib3JkZXJEYXRlIjoiMjAyMS0wMy0wNVQxNjowNzozMS4yOThaIiwiYmVmb3JlIjpmYWxzZX0="
           },
           "message": {
               "sender": {
                   "clientType": "PATIENT",
                   "id": "795412db-3bea-499a-be10-3e6839349197",
                   "titleName": null
               },
               "message": "Hello from API client: 3",
               "externalId": "IM873a5e02c4cc4c7d84b23a7ccd73fc7e",
               "createdAt": "2021-03-05T16:07:31.298Z"
           }
       }
   ]
}
```

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