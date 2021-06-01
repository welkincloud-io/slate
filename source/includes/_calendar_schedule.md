
# Schedule

There are two APIs that are relevant to the schedules feature:

## Get Schedules

```python
import requests
h = {
    "Authorization": "Bearer {}".format(token)
}

r = requests.get("https://api.live.welkincloud.io/gh/sb-demo/calendar/psm-schedules", 
   headers=h)

print("Response Code: {}".format(r.status_code))
print(r.json())
```

> Returned json

```json
[
 {
   "psmId": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
   "workHours": [
     {
       "createdBy": "9565d236-f654-4116-bfb4-c10a5e840a9c",
       "updatedBy": "9565d236-f654-4116-bfb4-c10a5e840a9c",
       "createdAt": "2021-05-03T13:18:16.424Z",
       "updatedAt": "2021-05-03T13:18:16.424Z",
       "workHoursId": "18b80840-63ef-4849-9d3a-0d36a2ace332",
       "startDateTime": "2020-01-01T00:00:00.000Z",
       "endDateTime": "2020-01-31T23:59:59.000Z",
       "localStartDateTime": "2020-01-01T03:00:00.000+03:00",
       "localEndDateTime": "2020-02-01T02:59:59.000+03:00",
       "daysInfo": [
         {
           "daysInfoId": "24e217e0-f33e-495d-96ae-f19b6d15a4c3",
           "startTime": "09:00:00",
           "endTime": "18:00:00",
           "day": 1
         },
         {
           "daysInfoId": "d740b70f-1aa7-41c6-8890-0a75cd5535df",
           "startTime": "09:00:00",
           "endTime": "18:00:00",
           "day": 2
         }
       ]
     }
   ],
   "events": [
     {
       "id": "313c2029-493b-4114-8b86-788d631a1851",
       "eventId": "313c2029-493b-4114-8b86-788d631a1851",
       "eventTitle": "New event title",
       "eventType": "APPOINTMENT",
       "eventColor": "pink",
       "allDayEvent": false,
       "startDateTime": "2020-01-01T00:00:00.000Z",
       "localStartDateTime": "2020-01-01T03:00:00.000+03:00",
       "endDateTime": "2020-01-31T23:59:59.000Z",
       "localEndDateTime": "2020-02-01T02:59:59.000+03:00"
     }
   ]
 }
]
```

<aside class="notice">
  <b>events.eventId</b> field is deprecated and will be replased to <b>events.id</b> in the future. 
</aside>

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

```python
import requests
h = {
    "Authorization": "Bearer {}".format(token)
}

r = requests.get("https://api.live.welkincloud.io/gh/sb-demo/calendar/psm-schedules?psmIds=28f393a8-62b3-4b4b-aa42-da769ce4489a,18f393a8-62b3-4b4b-aa42-da769ce4489a&from=2020-01-01T00:00:00.000Z&to=2020-01-31T23:59:59.000Z", 
   headers=h)

print("Response Code: {}".format(r.status_code))
print(r.json())
```

> Returned json


```json
[
  {
    "psmId": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
    "workHours": [
      {
        "createdBy": "9565d236-f654-4116-bfb4-c10a5e840a9c",
        "updatedBy": "9565d236-f654-4116-bfb4-c10a5e840a9c",
        "createdAt": "2021-05-03T13:18:16.424Z",
        "updatedAt": "2021-05-03T13:18:16.424Z",
        "workHoursId": "18b80840-63ef-4849-9d3a-0d36a2ace332",
        "startDateTime": "2020-01-01T00:00:00.000Z",
        "endDateTime": "2020-01-31T23:59:59.000Z",
        "localStartDateTime": "2020-01-01T03:00:00.000+03:00",
        "localEndDateTime": "2020-02-01T02:59:59.000+03:00",
        "daysInfo": [
          {
            "daysInfoId": "24e217e0-f33e-495d-96ae-f19b6d15a4c3",
            "startTime": "09:00:00",
            "endTime": "18:00:00",
            "day": 1
          },
          {
            "daysInfoId": "d740b70f-1aa7-41c6-8890-0a75cd5535df",
            "startTime": "09:00:00",
            "endTime": "18:00:00",
            "day": 2
          }
        ]
      }
    ],
    "events": [
      {
        "id": "313c2029-493b-4114-8b86-788d631a1851",
        "eventId": "313c2029-493b-4114-8b86-788d631a1851",
        "eventTitle": "New event title",
        "eventType": "APPOINTMENT",
        "eventColor": null,
        "allDayEvent": false,
        "startDateTime": "2020-01-01T00:00:00.000Z",
        "localStartDateTime": "2020-01-01T03:00:00.000+03:00",
        "endDateTime": "2020-01-31T23:59:59.000Z",
        "localEndDateTime": "2020-02-01T02:59:59.000+03:00"
      }
    ]
  }
]
```

<aside class="notice">
  <b>events.eventId</b> field is deprecated and will be replased to <b>events.id</b> in the future. 
</aside>

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


