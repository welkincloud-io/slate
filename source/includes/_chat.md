# Chat

`URL Structure: {{url}} / {{tenantName}} / {{instanceName}} / patient / {{patientId}} / chat`

in our example it would be:

`https://api.live.welkincloud.io/gh/sb-demo/calendar/events`


## Send message to care team

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
  "patientUrl": "https://api.live.welkincloud.io/gh/sb-demo/patients/cdb303e7-844f-40f8-b634-fe99bfccce28",
  "tenantName": "gh",
  "instanceName": "sb-demo",
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

### Response meta fields

Field | Description
--------- |  --------
nextPageToken | Token for receiving next page (null if this  page is last)
prevPageToken | Token for receiving previous page (null if this page is first)

### Response content fields
Field | Description
--------- |  --------
externalId | unique message ID
sender.clientType | "PATIENT", "USER"
sender.titleName | User firstname and lastname, joined by space. Exists only if clientType = "USER"


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

Note: You might want to see [Usage Example](#search-usage-example) for the search api. 

Query parametrs: 

Parameters| Description
--------- |  --------
query | Query for search
pageSize | How many search results per page will returns 
contentPageSize | How many messages per page will return [get messages](#get-messages) api when you'll pass `content.meta.nextPageToken` or `content.meta.prevPageToken` as `pageToken` param to that api
includeArchived | If true, include archived messages, otherwise not. 
pageToken | token for fetching next or previous search results, mutually exclusive with others params

Response fields: 

Field | Description
--------- |  --------
meta.nextPageToken | Token for fetching next search page
meta.prevPageToken | Token for fetching previous search page
content.[].meta.nextPageToken | Token for fetching messages which are located next to the found message. Should use in the [get messages](#get-messages) api.
content.[].meta.prevPageToken | Token for fetching messages which are located back to the found message. Should use in the [get messages](#get-messages) api.

## Archive messages

Archive chat message from specific date

<aside class="notice">
    This API is restricted from the API clients. 
</aside>

`URL Structure: {{url}} / {{tenantName}} / {{instanceName}} / patient / {{patientId}} / chat / archive `

in our example it would be:

`https://api.live.welkincloud.io/gh/sb-demo/patient/7272b601-bb09-4abf-87c0-ade48ddfaea0/chat/archive`


1. HTTP Method: POST
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patient/7272b601-bb09-4abf-87c0-ade48ddfaea0/chat/archive?archiveDate=2020-10-05T10:51:41.000Z`

### Query parametrs: 

Parameters| Description
--------- |  --------
archiveDate | All messages that have been posted before that date will be archived

## Restore archived messages

Restore all previously archived messages

<aside class="notice">
    This API is restricted from the API clients. 
</aside>

`URL Structure: {{url}} / {{tenantName}} / {{instanceName}} / patient / {{patientId}} / chat / restore `

in our example it would be:

`https://api.live.welkincloud.io/gh/sb-demo/patient/7272b601-bb09-4abf-87c0-ade48ddfaea0/chat/restore`


1. HTTP Method: POST
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patient/7272b601-bb09-4abf-87c0-ade48ddfaea0/chat/restore`


# Chat search usage example

![Chat usage example](chat_search.png)

## Fething first search page

> Returned data

```json
{
   "meta": {
       "nextPageToken": "eyJ0eXBlIjoiTE9DQUxfU0VBUkNIIiwicGFnZVNpemUiOjIsImJvcmRlckRhdGUiOiIyMDIxLTAzLTA5VDIzOjUzOjA4LjkyNloiLCJxdWVyeSI6ImhlbGxvIiwiYmVmb3JlIjp0cnVlfQ==",
       "prevPageToken": null,
       "pageSize": 2,
       "found": true
   },
   "content": [
       {
           "meta": {
               "nextPageToken": "eyJ0eXBlIjoiTE9DQUxfRklORCIsInBhZ2VTaXplIjoxLCJib3JkZXJEYXRlIjoiMjAyMS0wMy0wOVQyMzo1NDozOS4xNTJaIiwiYmVmb3JlIjp0cnVlfQ==",
               "prevPageToken": "eyJ0eXBlIjoiTE9DQUxfRklORCIsInBhZ2VTaXplIjoxLCJib3JkZXJEYXRlIjoiMjAyMS0wMy0wOVQyMzo1NDozOS4xNTJaIiwiYmVmb3JlIjpmYWxzZX0="
           },
           "message": {
               "sender": {
                   "clientType": "USER",
                   "id": "379a1c22-aac4-4741-a083-c3c80105ee94",
                   "titleName": "Root Root"
               },
               "receiver": {
                   "clientType": "PATIENT",
                   "id": "c4f64a1a-2c9c-4ec2-b1d2-2c8dd4ce1df1",
                   "titleName": null
               },
               "message": "Hello2",
               "externalId": "IMf03066157abb419287c202bbc0e417d0",
               "createdAt": "2021-03-09T23:54:39.152Z"
           }
       },
       {
           "meta": {
               "nextPageToken": "eyJ0eXBlIjoiTE9DQUxfRklORCIsInBhZ2VTaXplIjoxLCJib3JkZXJEYXRlIjoiMjAyMS0wMy0wOVQyMzo1MzowOC45MjZaIiwiYmVmb3JlIjp0cnVlfQ==",
               "prevPageToken": "eyJ0eXBlIjoiTE9DQUxfRklORCIsInBhZ2VTaXplIjoxLCJib3JkZXJEYXRlIjoiMjAyMS0wMy0wOVQyMzo1MzowOC45MjZaIiwiYmVmb3JlIjpmYWxzZX0="
           },
           "message": {
               "sender": {
                   "clientType": "USER",
                   "id": "379a1c22-aac4-4741-a083-c3c80105ee94",
                   "titleName": "Root Root"
               },
               "receiver": {
                   "clientType": "PATIENT",
                   "id": "c4f64a1a-2c9c-4ec2-b1d2-2c8dd4ce1df1",
                   "titleName": null
               },
               "message": "Hello1",
               "externalId": "IMc630b6cfab684e5683e0d593e2b244a1",
               "createdAt": "2021-03-09T23:53:08.926Z"
           }
       }
   ]
}
```

Let assume that we have the following chat (messages in the list are sorted from older to newest): 

* Hello0
* Hello1
* Test1
* Test2
* Hello2
* Test3
* Test4

So let’s search by query “Hello”. Assume pageSize=2 and contentPageSize=1 and make the following request

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patient/7272b601-bb09-4abf-87c0-ade48ddfaea0/chat/search?query=hello&pageSize=2&contentPageSize=1&includeArchived=true`

As you can see, two messages are found: the first is “Hello2” and the second is “Hello1”. “content” length is limited to pageSize, so to fetch next messages that matches query you should use pass “meta.nextPageToken” as pageToken.

## Fetching next search page

> Returned JSON

```json
{
   "meta": {
       "nextPageToken": null,
       "prevPageToken": "eyJ0eXBlIjoiTE9DQUxfU0VBUkNIIiwicGFnZVNpemUiOjIsImJvcmRlckRhdGUiOiIyMDIxLTAzLTA5VDIzOjUyOjU1LjYxMVoiLCJxdWVyeSI6ImhlbGxvIiwiYmVmb3JlIjpmYWxzZX0=",
       "pageSize": 2,
       "found": true
   },
   "content": [
       {
           "meta": {
               "nextPageToken": "eyJ0eXBlIjoiTE9DQUxfRklORCIsInBhZ2VTaXplIjoyLCJib3JkZXJEYXRlIjoiMjAyMS0wMy0wOVQyMzo1Mjo1NS42MTFaIiwiYmVmb3JlIjp0cnVlfQ==",
               "prevPageToken": "eyJ0eXBlIjoiTE9DQUxfRklORCIsInBhZ2VTaXplIjoyLCJib3JkZXJEYXRlIjoiMjAyMS0wMy0wOVQyMzo1Mjo1NS42MTFaIiwiYmVmb3JlIjpmYWxzZX0="
           },
           "message": {
               "sender": {
                   "clientType": "USER",
                   "id": "379a1c22-aac4-4741-a083-c3c80105ee94",
                   "titleName": "Root Root"
               },
               "receiver": {
                   "clientType": "PATIENT",
                   "id": "c4f64a1a-2c9c-4ec2-b1d2-2c8dd4ce1df1",
                   "titleName": null
               },
               "message": "Hello0",
               "externalId": "IM9ebf08fe2c59436593c3e64ae28d898a",
               "createdAt": "2021-03-09T23:52:55.611Z"
           }
       }
   ]
}
```

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patient/7272b601-bb09-4abf-87c0-ade48ddfaea0/chat/search?pageToken=eyJ0eXBlIjoiTE9DQUxfU0VBUkNIIiwicGFnZVNpemUiOjIsImJvcmRlckRhdGUiOiIyMDIxLTAzLTA5VDIzOjUzOjA4LjkyNloiLCJxdWVyeSI6ImhlbGxvIiwiYmVmb3JlIjp0cnVlfQ==`

And we received “Hello0” message, that’s the last message that matches query. 


## Fetch near-located messages

> Returned json

```json
{
   "meta": {
       "nextPageToken": "eyJ0eXBlIjoiTE9DQUxfRklORCIsInBhZ2VTaXplIjoxLCJib3JkZXJEYXRlIjoiMjAyMS0wMy0wOVQyMzo1NDozNi41ODVaIiwiYmVmb3JlIjp0cnVlfQ==",
       "prevPageToken": "eyJ0eXBlIjoiTE9DQUxfRklORCIsInBhZ2VTaXplIjoxLCJib3JkZXJEYXRlIjoiMjAyMS0wMy0wOVQyMzo1NDozNi41ODVaIiwiYmVmb3JlIjpmYWxzZX0=",
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
           "receiver": {
               "clientType": "PATIENT",
               "id": "c4f64a1a-2c9c-4ec2-b1d2-2c8dd4ce1df1",
               "titleName": null
           },
           "message": "Test2",
           "externalId": "IM9b366d9d29934008a8a500e4e834cd60",
           "createdAt": "2021-03-09T23:54:36.585Z"
       }
   ]
}
```

Let imagine the following situation: the user clicked on the found message, and we would like to open chat dialog and jump to the message. So we have to see messages that located near the found message. 

So we’re using the following request and pass “content[].meta.nextPageToken” as pageToken param: 

Note: We are not using search API, we are using [get messages](#get-messages) api

1. HTTP Method: GET
2. HTTP Url: `https://api.live.welkincloud.io/gh/sb-demo/patient/7272b601-bb09-4abf-87c0-ade48ddfaea0/chat?pageToken=eyJ0eXBlIjoiTE9DQUxfRklORCIsInBhZ2VTaXplIjoxLCJib3JkZXJEYXRlIjoiMjAyMS0wMy0wOVQyMzo1NDozOS4xNTJaIiwiYmVmb3JlIjp0cnVlfQ==&includeArchived=false`

As you can see, fetched message "Test2" located next to the found message "Hello2" 

