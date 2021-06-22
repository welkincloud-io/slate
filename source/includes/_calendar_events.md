
# Calendar Events

```json
{
 "id": "313c2029-493b-4114-8b86-788d631a1851",
 "createdBy": "9565d236-f654-4116-bfb4-c10a5e840a9c",
 "createdAt": "2021-05-03T13:39:12.847Z",
 "updatedBy": "9565d236-f654-4116-bfb4-c10a5e840a9c",
 "updatedAt": "2021-05-03T13:39:12.847Z",
 "eventTitle": "Weekly Appointment with Jack",
 "eventDescription": "",
 "startDateTime": "2020-01-01T00:00:00.000Z",
 "localStartDateTime": "2020-01-01T03:00:00.000+03:00",
 "endDateTime": "2020-01-31T23:59:59.000Z",
 "localEndDateTime": "2020-02-01T02:59:59.000+03:00",
 "allDayEvent": false,
 "duration": 2678399,
 "externalId": null,
 "externalIdUpdatedAt": "2021-06-11T18:10:45.711Z",
 "eventType": "APPOINTMENT",
 "eventStatus": "SCHEDULED",
 "eventMode": "IN-PERSON",
 "eventColor": null,
 "hostId": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
 "additionalInfo": {
   "remarks": "",
   "location": "",
   "attachment": ""
 },
 "participants": [
   {
     "id": "d4e6eb8b-b627-461d-a17d-292083446df8",
     "participantId": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
     "participantRole": "psm",
     "participationStatus": "",
     "attended": false
   },
   {
     "id": "8416e538-7417-4f3d-aaf5-19d212ae6f3b",
     "participantId": "4f684417-7868-467a-ae0a-f7aa8a4323e6",
     "participantRole": "patient",
     "participationStatus": "",
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

Field Name|  Field description
--------- |  ----------------
hostId | ID of user which owns the event
additionalInfo | Custom object without strict defined structure
externalId | Custom string for object identification, must be different for each event
externalIdUpdatedAt | Timestamp when calendar event externalId has been updated

Please note that `participants` field must contain participant with `id=hostId`

## Create Calendar Event

```python
import requests
h = {
    "Authorization": "Bearer {}".format(token)
}
data = {
    "createdBy": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
    "eventTitle": "Weekly Appointment with Jack",
    "eventDescription": "",
    "startDateTime": "2020-01-01T00:00:00.000Z",
    "endDateTime": "2020-01-31T23:59:59.000Z",
    "eventType": "APPOINTMENT",
    "eventStatus": "SCHEDULED",
    "eventMode": "IN-PERSON",
    "hostId": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
    "externalId": "externalId",
    "additionalInfo": {
        "location": "",
        "remarks": "",
        "attachment": ""
    },
    "participants": [
        {
            "participantId": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
            "participantRole": "psm",
            "attended": false
        },
        {
            "participantId": "4f684417-7868-467a-ae0a-f7aa8a4323e6",
            "participantRole": "patient",
            "attended": false
        }
    ]
}

r = requests.post("https://api.live.welkincloud.io/gh/sb-demo//calendar/events", 
  json=data, headers=h)

print("Response Code: {}".format(r.status_code))
print(r.json())
```

> Returned json 

```json
{
  "id": "313c2029-493b-4114-8b86-788d631a1851",
  "createdBy": "9565d236-f654-4116-bfb4-c10a5e840a9c",
  "createdAt": "2021-05-03T13:39:12.847Z",
  "updatedBy": "9565d236-f654-4116-bfb4-c10a5e840a9c",
  "updatedAt": "2021-05-03T13:39:12.847Z",
  "eventTitle": "Weekly Appointment with Jack",
  "eventDescription": "",
  "startDateTime": "2020-01-01T00:00:00.000Z",
  "localStartDateTime": "2020-01-01T03:00:00.000+03:00",
  "endDateTime": "2020-01-31T23:59:59.000Z",
  "localEndDateTime": "2020-02-01T02:59:59.000+03:00",
  "allDayEvent": false,
  "duration": 2678399,
  "eventType": "APPOINTMENT",
  "eventStatus": "SCHEDULED",
  "eventMode": "IN-PERSON",
  "eventColor": null,
  "externalId": "externalId",
  "externalIdUpdatedAt": "2021-06-11T18:10:45.711Z",
  "hostId": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
  "additionalInfo": {
    "location": "",
    "remarks": "",
    "attachment": ""
  },
  "participants": [
    {
      "id": "d4e6eb8b-b627-461d-a17d-292083446df8",
      "participantId": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
      "participantRole": "psm",
      "participationStatus": "",
      "attended": false
    },
    {
      "id": "8416e538-7417-4f3d-aaf5-19d212ae6f3b",
      "participantId": "4f684417-7868-467a-ae0a-f7aa8a4323e6",
      "participantRole": "patient",
      "participationStatus": "",
      "attended": false
    }
  ]
}
```

1. HTTP Method: POST
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/calendar/events`

### Event required fields: 

* startDateTime
* endDateTime
* hostId
* participants
* participants.participantId
* participants.participantRole

## Get Event By ID

```python
import requests
h = {
    "Authorization": "Bearer {}".format(token)
}

r = requests.get("https://api.live.welkincloud.io/gh/sb-demo/calendar/events/313c2029-493b-4114-8b86-788d631a1851", 
   headers=h)

print("Response Code: {}".format(r.status_code))
print(r.json())
```

> Returned Json

```json
{
  "id": "313c2029-493b-4114-8b86-788d631a1851",
  "createdBy": "9565d236-f654-4116-bfb4-c10a5e840a9c",
  "createdAt": "2021-05-03T13:39:12.847Z",
  "updatedBy": "9565d236-f654-4116-bfb4-c10a5e840a9c",
  "updatedAt": "2021-05-03T13:55:59.652Z",
  "eventTitle": "New event title",
  "eventDescription": "",
  "startDateTime": "2020-01-01T00:00:00.000Z",
  "localStartDateTime": "2020-01-01T03:00:00.000+03:00",
  "endDateTime": "2020-01-31T23:59:59.000Z",
  "localEndDateTime": "2020-02-01T02:59:59.000+03:00",
  "allDayEvent": false,
  "duration": 2678399,
  "eventType": "APPOINTMENT",
  "eventStatus": "SCHEDULED",
  "eventMode": "IN-PERSON",
  "eventColor": null,
  "externalId": "externalId",
  "externalIdUpdatedAt": "2021-06-11T18:10:45.711Z",
  "hostId": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
  "additionalInfo": {
    "remarks": "",
    "location": "",
    "attachment": ""
  },
  "participants": [
    {
      "id": "d4e6eb8b-b627-461d-a17d-292083446df8",
      "participantId": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
      "participantRole": "psm",
      "participationStatus": "",
      "attended": false
    },
    {
      "id": "8416e538-7417-4f3d-aaf5-19d212ae6f3b",
      "participantId": "4f684417-7868-467a-ae0a-f7aa8a4323e6",
      "participantRole": "patient",
      "participationStatus": "",
      "attended": false
    }
  ]
}
```

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/calendar/events/313c2029-493b-4114-8b86-788d631a1851`

## Get Event By External ID

```python
import requests
h = {
    "Authorization": "Bearer {}".format(token)
}

r = requests.get("https://api.live.welkincloud.io/gh/sb-demo/calendar/events/externalId?type=EXTERNAL_ID", headers=h)

print("Response Code: {}".format(r.status_code))
print(r.json())
```

> Returned Json

```json
{
  "id": "313c2029-493b-4114-8b86-788d631a1851",
  "createdBy": "9565d236-f654-4116-bfb4-c10a5e840a9c",
  "createdAt": "2021-05-03T13:39:12.847Z",
  "updatedBy": "9565d236-f654-4116-bfb4-c10a5e840a9c",
  "updatedAt": "2021-05-03T13:55:59.652Z",
  "eventTitle": "New event title",
  "eventDescription": "",
  "startDateTime": "2020-01-01T00:00:00.000Z",
  "localStartDateTime": "2020-01-01T03:00:00.000+03:00",
  "endDateTime": "2020-01-31T23:59:59.000Z",
  "localEndDateTime": "2020-02-01T02:59:59.000+03:00",
  "allDayEvent": false,
  "duration": 2678399,
  "eventType": "APPOINTMENT",
  "eventStatus": "SCHEDULED",
  "eventMode": "IN-PERSON",
  "eventColor": null,
  "externalId": "externalId",
  "externalIdUpdatedAt": "2021-06-11T18:10:45.711Z",
  "hostId": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
  "additionalInfo": {
    "remarks": "",
    "location": "",
    "attachment": ""
  },
  "participants": [
    {
      "id": "d4e6eb8b-b627-461d-a17d-292083446df8",
      "participantId": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
      "participantRole": "psm",
      "participationStatus": "",
      "attended": false
    },
    {
      "id": "8416e538-7417-4f3d-aaf5-19d212ae6f3b",
      "participantId": "4f684417-7868-467a-ae0a-f7aa8a4323e6",
      "participantRole": "patient",
      "participationStatus": "",
      "attended": false
    }
  ]
}
```

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/calendar/events/externalId?type=EXTERNAL_ID`


## Find Events

```python
import requests
h = {
    "Authorization": "Bearer {}".format(token)
}

r = requests.get("https://api.live.welkincloud.io/gh/sb-demo/calendar/events?from=2020-01-15T14:00:00.000Z&participantIds=301b2895-cbf0-4cac-b4cf-1d082faee95c&sort=createdAt,asc&to=2020-02-11T00:00:00.000Z&eventType=APPOINTMENT", 
   headers=h)

print("Response Code: {}".format(r.status_code))
print(r.json())
```

> Returned json

```json
{
  "content": [
    {
      "id": "313c2029-493b-4114-8b86-788d631a1851",
      "createdBy": "9565d236-f654-4116-bfb4-c10a5e840a9c",
      "createdAt": "2021-05-03T13:39:12.847Z",
      "updatedBy": "9565d236-f654-4116-bfb4-c10a5e840a9c",
      "updatedAt": "2021-05-03T13:39:12.847Z",
      "eventTitle": "Weekly Appointment with Jack",
      "eventDescription": "",
      "startDateTime": "2020-01-01T00:00:00.000Z",
      "localStartDateTime": "2020-01-01T03:00:00.000+03:00",
      "endDateTime": "2020-01-31T23:59:59.000Z",
      "localEndDateTime": "2020-02-01T02:59:59.000+03:00",
      "allDayEvent": false,
      "duration": 2678399,
      "eventType": "APPOINTMENT",
      "eventStatus": "SCHEDULED",
      "eventMode": "IN-PERSON",
      "eventColor": null,
      "externalId": "externalId",
      "externalIdUpdatedAt": "2021-06-11T18:10:45.711Z",
      "hostId": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
      "additionalInfo": {
        "remarks": "",
        "location": "",
        "attachment": ""
      },
      "participants": [
        {
          "id": "d4e6eb8b-b627-461d-a17d-292083446df8",
          "participantId": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
          "participantRole": "psm",
          "participationStatus": "",
          "attended": false
        },
        {
          "id": "8416e538-7417-4f3d-aaf5-19d212ae6f3b",
          "participantId": "4f684417-7868-467a-ae0a-f7aa8a4323e6",
          "participantRole": "patient",
          "participationStatus": "",
          "attended": false
        }
      ]
    }
  ],
....pagination links omitted
}

```

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/calendar/events/`

Parameters| Format | Description
--------- | ----------- | --------
participantIds | list of id and values, either users or patients | participantIds=28f393a8-62b3-4b4b-aa42-da769ce4489
from | Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | from=2021-01-28T23:10:04.874Z
to |Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | to=2021-01-28T23:10:04.874Z
eventType | Enum of allowed values | "GROUP_THERAPY", "APPOINTMENT", "LEAVE"
sort | Allows one to specify the sort order of the returned patients collection	 | sort=createdAt,asc
includeCancelled | Boolean value | Should or not API return cancelled events (default: false)

Example URLs: 

1. `https://api.live.welkincloud.io/gh/sb-demo/calendar/events?from=2020-01-15T14:00:00.000Z&participantIds=301b2895-cbf0-4cac-b4cf-1d082faee95c&sort=createdAt,asc&to=2020-02-11T00:00:00.000Z&eventType=APPOINTMENT`

## Update Calendar Event by ID

```python
import requests
h = {
    "Authorization": "Bearer {}".format(token)
}
data = {
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

r = requests.put("https://api.live.welkincloud.io/gh/sb-demo/calendar/events/313c2029-493b-4114-8b86-788d631a1851", 
  json=data, headers=h)

print("Response Code: {}".format(r.status_code))
print(r.json())
```

> Returned json 

```json
{
  "id": "313c2029-493b-4114-8b86-788d631a1851",
  "createdBy": "9565d236-f654-4116-bfb4-c10a5e840a9c",
  "createdAt": "2021-05-03T13:39:12.847Z",
  "updatedBy": "9565d236-f654-4116-bfb4-c10a5e840a9c",
  "updatedAt": "2021-05-03T13:55:59.652Z",
  "eventTitle": "Patient Appointment",
  "eventDescription": "",
  "startDateTime": "2020-01-01T00:00:00.000Z",
  "localStartDateTime": "2020-01-01T03:00:00.000+03:00",
  "endDateTime": "2020-01-31T23:59:59.000Z",
  "localEndDateTime": "2020-02-01T02:59:59.000+03:00",
  "allDayEvent": false,
  "duration": 2678399,
  "eventType": "APPOINTMENT",
  "eventStatus": "SCHEDULED",
  "eventMode": "IN-PERSON",
  "eventColor": null,
  "externalId": null,
  "externalIdUpdatedAt": "2021-06-11T18:10:45.711Z",
  "hostId": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
  "additionalInfo": {
    "location": "Room 1408",
    "remarks": "Please wear mask",
    "attachment": ""
  },
  "participants": [
    {
      "id": "d4e6eb8b-b627-461d-a17d-292083446df8",
      "participantId": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
      "participantRole": "psm",
      "participationStatus": "",
      "attended": false
    },
    {
      "id": "8416e538-7417-4f3d-aaf5-19d212ae6f3b",
      "participantId": "4f684417-7868-467a-ae0a-f7aa8a4323e6",
      "participantRole": "patient",
      "participationStatus": "",
      "attended": false
    }
  ]
}

```

1. HTTP Method: PUT
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/calendar/events/2dfbd113-5282-4f70-b456-d8cf7ecb5573`


Note: see [list](#event-required-fields) of the required fields

## Patch update event by ID

```python
import requests
h = {
    "Authorization": "Bearer {}".format(token)
}
data = {
    "eventTitle": "New event title"
}


r = requests.patch("https://api.live.welkincloud.io/gh/sb-demo/calendar/events/313c2029-493b-4114-8b86-788d631a1851", 
  json=data, headers=h)

print("Response Code: {}".format(r.status_code))
print(r.json())
```

> Returned json 

```json
{
  "id": "313c2029-493b-4114-8b86-788d631a1851",
  "createdBy": "9565d236-f654-4116-bfb4-c10a5e840a9c",
  "createdAt": "2021-05-03T13:39:12.847Z",
  "updatedBy": "9565d236-f654-4116-bfb4-c10a5e840a9c",
  "updatedAt": "2021-05-03T13:55:59.652Z",
  "eventTitle": "New event title",
  "eventDescription": "",
  "startDateTime": "2020-01-01T00:00:00.000Z",
  "localStartDateTime": "2020-01-01T03:00:00.000+03:00",
  "endDateTime": "2020-01-31T23:59:59.000Z",
  "localEndDateTime": "2020-02-01T02:59:59.000+03:00",
  "allDayEvent": false,
  "duration": 2678399,
  "eventType": "APPOINTMENT",
  "eventStatus": "SCHEDULED",
  "eventMode": "IN-PERSON",
  "eventColor": null,
  "externalId": null,
  "externalIdUpdatedAt": "2021-06-11T18:10:45.711Z",
  "hostId": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
  "additionalInfo": {
    "location": "Room 1408",
    "remarks": "Please wear mask",
    "attachment": ""
  },
  "participants": [
    {
      "id": "d4e6eb8b-b627-461d-a17d-292083446df8",
      "participantId": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
      "participantRole": "psm",
      "participationStatus": "",
      "attended": false
    },
    {
      "id": "8416e538-7417-4f3d-aaf5-19d212ae6f3b",
      "participantId": "4f684417-7868-467a-ae0a-f7aa8a4323e6",
      "participantRole": "patient",
      "participationStatus": "",
      "attended": false
    }
  ]
}
```

1. HTTP Method: PATCH
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/calendar/events/2dfbd113-5282-4f70-b456-d8cf7ecb5573`


## Update event invitation response by ID

```python
import requests
h = {
    "Authorization": "Bearer {}".format(token)
}
data = {
    "participantId": "2279cbc9-0cb5-410b-9566-7f22b8f4263f",
    "participationStatus": "Yes"
}


r = requests.put("https://api.live.welkincloud.io/gh/sb-demo/calendar/events/2dfbd113-5282-4f70-b456-d8cf7ecb5573/invitation-response", 
  json=data, headers=h)

print("Response Code: {}".format(r.status_code))
```

1. HTTP Method: PUT
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/calendar/events/2dfbd113-5282-4f70-b456-d8cf7ecb5573/invitation-response`

Note: all fields are required


## Delete Calendar Event by ID

Note: Only future events can be deleted

```python
import requests
h = {
    "Authorization": "Bearer {}".format(token)
}

r = requests.delete("https://api.live.welkincloud.io/gh/sb-demo/calendar/events/2dfbd113-5282-4f70-b456-d8cf7ecb5573", 
   headers=h)

print("Response Code: {}".format(r.status_code))
```

1. HTTP Method: DELETE
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/calendar/events/2dfbd113-5282-4f70-b456-d8cf7ecb5573`

## Get Summary for the User

```python
import requests
h = {
    "Authorization": "Bearer {}".format(token)
}

r = requests.get("https://api.live.welkincloud.io/gh/sb-demo/calendar/psm-event-summary?from=2020-01-15T14:00:00.000Z&to=2020-02-11T00:00:00.000Z&psmIds=301b2895-cbf0-4cac-b4cf-1d082faee95c", 
   headers=h)

print("Response Code: {}".format(r.status_code))
print(r.json())
```

> Returned json

```json
{
 "startDateTime": "2020-01-15T14:00:00.000Z",
 "endDateTime": "2020-02-11T00:00:00.000Z",
 "summary": [
   {
     "psmId": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
     "totalCreatedEvents": 1,
     "totalOccurredEvents": 1,
     "totalFutureEvents": 0,
     "eventStatusCount": {
       "SCHEDULED": 1
     },
     "totalWorkingHours": "63.0 hours",
     "totalEventHours": "394.0 hours",
     "occupancy": "625.4%"
   }
 ]
}
```

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/calendar/psm-event-summary?from=2020-01-15T14:00:00.000Z&to=2020-02-11T00:00:00.000Z&psmIds=301b2895-cbf0-4cac-b4cf-1d082faee95c`

Parameters| Format | Description
--------- | ----------- | --------
psm-ids | user id | psm-ids=301b2895-cbf0-4cac-b4cf-1d082faee95c
from | Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | from=2021-01-28T23:10:04.874Z
to |Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | to=2021-01-28T23:10:04.874Z
