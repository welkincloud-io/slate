# Security audit

## Find security audit event

It is a typical API to work security audit

`URL Structure: {{url}} / {{tenantName}} / admin /audit-security`

in our example it would be:
`https://api.live.welkincloud.io/gh/admin/audit-security`

```json
{
  "sentAt":"2021-05-04T11:42:20.692Z",
  "subjectUsername":"johndoe",
  "subjectUserId":"c8701ee0-e26d-4177-bec5-dadd3d7519e1",
  "subjectActor":"USER",
  "subjectFullName":"Json Doe",
  "objectUsername":"johndoe",
  "objectUserId":"c8701ee0-e26d-4177-bec5-dadd3d7519e1",
  "objectActor":"USER",
  "objectFullName":"Json Doe",
  "eventSubtype":"USER_ACCESS_UPDATED",
  "record":{
    "auditSecurityAccessEnabled":true,
    "adminAccessEnabled":true,
    "id":"f3f40197-4e2f-48a7-b608-04a0bc5fb28c",
    "userId":"c8701ee0-e26d-4177-bec5-dadd3d7519e1",
    "instanceAccesses":[
      {
        "instanceId":"d002ef26-3b35-4ec1-b4bd-d7147cf07c9f",
        "instanceName":"sbx",
        "instanceDescription":"",
        "workshopAccessEnabled":true,
        "auditDataAccessEnabled":true
      },
      {
        "instanceId":"3879ba2b-d133-48d2-b841-dfad0eaac36a",
        "instanceName":"commcenter",
        "instanceDescription":"",
        "workshopAccessEnabled":true,
        "auditDataAccessEnabled":true
      }
    ]
  }
}
```

Fields description:

Field Name |   Format  |  Description| Allowed values
---------  |   -----   |  ---------| -------
cdtName  | String |  Cdt name
subjectUsername |  String |  Username of a person performing the action
subjectUserId | UUID |  Id of a person performing the action
subjectFullName |  String |  Full name of the person performing the action
subjectActor |  Enum of allowed values   |  Client type of the person performing the action | API_CLIENT, PATIENT, CS_TOOL_CLIENT, USER
objectUsername |  String |  Username of a person who the action was taken on
objectUserId | UUID |  Id of a person who the action was taken on
objectFullName |  String |  Full name of a person who the action was taken on
objectActor |  Enum of allowed values | Client type of a person who the action was taken on | API_CLIENT, PATIENT, CS_TOOL_CLIENT, USER
eventSubtype | Enum of allowed values | Type of performing action
record |  Object |  Object after performing the action on it

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/admin/audit-security?size=20&page=0&sort=createdAt%2Cdesc&dateStart=2021-02-26T17%3A00%3A00.000Z&objectActor=API_CLIENT`

Parameters| Format | Description | Allowed values
--------- | ----------- | -------- | -----------
subjectUsername | String | Username of the person performing the action
subjectFullName | String | Full name of the person performing the action
subjectActor | Enum of allowed values | Client type of the person performing the action | API_CLIENT, PATIENT, CS_TOOL_CLIENT, USER
objectUsername |  String |  Username of a person who the action was taken on
objectFullName |  String |  Full name of a person who the action was taken on
objectActor |  Enum of allowed values | Client type of a person who the action was taken on | API_CLIENT, PATIENT, CS_TOOL_CLIENT, USER
dateEnd | Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | Filter by sentAt
dateStart | Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | Filter by sentAt
eventSubtype | Enum of allowed values | Type of performing action
