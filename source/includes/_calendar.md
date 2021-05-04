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
