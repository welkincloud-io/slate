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
