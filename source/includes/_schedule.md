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


