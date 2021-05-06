
# Calendar Working Hours

Using Working Hours API, users (doctors, clinicians) can set flexible working hours that vary from week to week. It is beneficial for people involved part-time.


```json
{
 "psmId": "28f393a8-62b3-4b4b-aa42-da769ce4489a",
 "createdBy": "28f393a8-62b3-4b4b-aa42-da769ce4489a",
 "startDateTime": "2020-01-01T00:00:00.000Z",
 "endDateTime": "2020-01-31T23:59:59.000Z",
 "localStartDateTime": "2020-01-01T00:00:00.000+03:00",
 "localEndDateTime": "2020-01-31T23:59:59.000+03:00",
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

1. `psmId` is `userId`. We will change it in the future releases to reflect that
2. `day` field represents day of week (1 - monday, 2 - tuesday, ...)

`URL Structure: {{url}} / {{tenantName}} / {{instanceName}} /calendar/ work-hours`

In our example it would be:
`https://api.live.welkincloud.io/gh/sb-demo/calendar/work-hours`


## Create Work Hours

```python
import requests
h = {
    "Authorization": "Bearer {}".format(token)
}
data = {
    "psmId": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
    "createdBy": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
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

r = requests.post("https://api.live.welkincloud.io/gh/sb-demo/calendar/work-hours", 
  json=data, headers=h)

print("Response Code: {}".format(r.status_code))
print(r.json())
```

> The above request returns JSON of the created work hours

```json
{
  "psmId": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
  "details": [
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
  ]
}
```

1. HTTP Method: POST
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/calendar/work-hours`

### Work Hours required fields

* psmId
* startDateTime
* endDateTime
* daysInfo
* daysInfo.startTime
* daysInfo.endTime
* daysInfo.day

## Read Work Hours

```python
import requests
h = {
    "Authorization": "Bearer {}".format(token)
}

r = requests.get("https://api.live.welkincloud.io/gh/sb-demo/calendar/work-hours?psm-ids=301b2895-cbf0-4cac-b4cf-1d082faee95c&from=2020-01-01T00:00:00.000Z&to=2020-01-31T23:59:59.000Z", 
  headers=h)

print("Response Code: {}".format(r.status_code))
print(r.json())
```

> Returned json

```json     
[
  {
    "psmId": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
    "details": [
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
    ]
  }
]
```

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/calendar/work-hours`

Parameters| Format | Description
--------- | ----------- | --------
psm-ids | list of id and values | psm-ids=301b2895-cbf0-4cac-b4cf-1d082faee95c
from | Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | from=2021-01-28T23:10:04.874Z
to |Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | to=2021-01-28T23:10:04.874Z

URL examples:

1. `https://api.live.welkincloud.io/gh/sb-demo/calendar/work-hours
?psm-ids=301b2895-cbf0-4cac-b4cf-1d082faee95c
&from=2020-01-01T00:00:00.000Z
&to=2020-01-31T23:59:59.000Z
`

2. `https://api.live.welkincloud.io/gh/sb-demo/calendar/work-hours
?psm-ids=301b2895-cbf0-4cac-b4cf-1d082faee95c,18f393a8-62b3-4b4b-aa42-da769ce4489a
&from=2020-01-01T00:00:00.000Z
&to=2020-01-31T23:59:59.000Z
`

## Update Work Hours

Updating work hours by ID

```python
import requests
h = {
    "Authorization": "Bearer {}".format(token)
}
data = {
    "psmId": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
    "updatedBy": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
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

r = requests.put("https://api.live.welkincloud.io/gh/sb-demo/calendar/work-hours/c7a4251f-d70e-4ccb-8c96-1038c76fd737", 
  json=data, headers=h)

print("Response Code: {}".format(r.status_code))
print(r.json())
```
 
> Returned json

```json
{
 "psmId": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
 "updatedBy": "301b2895-cbf0-4cac-b4cf-1d082faee95c",
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

See [list](#work-hours-required-fields) of the required fields