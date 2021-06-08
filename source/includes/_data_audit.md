# Data audit

## Find data audit event

It is a typical API to work with data audit

`URL Structure: {{url}} / {{tenantName}} / admin /audit-data`

in our example it would be:
`https://api.live.welkincloud.io/gh/admin/audit-data`

```json
{
  "eventEntity": "PATIENT",
  "url": "https://api.live.welkincloud.io/gh/sb-demo/patients/ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8",
  "subjectUsername": "johndoe",
  "subjectUserId": "03f51404-a300-4857-b10c-0d6a1a1b88ae",
  "subjectActor": "USER",
  "subjectFullName": "Json Doe",
  "patientFullName": "Charlie Schwarzenegger",
  "patientId": "ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8",
  "instance": "sb-demo",
  "eventSubtype": "PATIENT_UPDATED",
  "sentAt": "2021-04-27T04:33:36.933Z",
  "record": {
    "id": "6801d498-26f4-4aee-961b-5daffcf193c8",
    "firstName": "Charlie",
    "lastName": "Schwarzenegger",
    "middleName": "Mc",
    "birthDate": "2012-08-12T00:00:00.000Z",
    "email": "1@1.com",
    "phone": "+13363034233",
    "country": "USA",
    "state": "American Samoa",
    "city": "Los Angeles",
    "zip": "99451",
    "addressLine1": "Hollywood Blvd 2021",
    "timezone ": "America/Los_Angeles",
    "patientTerritories": []
  }
}
```

Fields description:

Field Name |   Format  |  Description| Allowed values
---------  |   -----   |  ---------| -------
cdtName  |  String |  Cdt name
entity  |   Enum of allowed values   |  Type of the entity | CDT, PATIENT
subjectUsername  |  String |  Username of a person performing the action
subjectUserId  |  UUID |  Id of a person performing the action
subjectFullName  |  String |  Full name of the person performing the action
subjectActor  |   Enum of allowed values   |  Client type of the person performing the action | API_CLIENT, PATIENT, CS_TOOL_CLIENT, USER
instance  |  String |  Instance name
patientFullName  |  String |  Full name of the patient who the action was taken on
patientId | UUID |  Id of the patient who the action was taken on
sentAt  |  Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format |  When action happens
cdt |  Cdt |  Object describe all fields with types
operation  |  Enum of allowed values  |  Type of action operation |CREATE, UPDATE, DELETE
record |  Object |  Object after performing the action on it

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/admin/audit-data?size=20&page=0&sort=createdAt%2Cdesc&dateStart=2021-02-26T17%3A00%3A00.000Z&entity=PATIENT`

Parameters| Format | Description | Allowed values
--------- | ----------- | -------- | -----------
cdtName | String | If type is CDT then may filter by name
entity | Enum of allowed values | Type of the entity | CDT, PATIENT
subjectUsername | String | Username of the person performing the action
subjectFullName | String | Full name of the person performing the action
subjectActor | Enum of allowed values | Client type of the person performing the action | API_CLIENT, PATIENT, CS_TOOL_CLIENT, USER
instance | String | Instance name
patientFullName | String |  Full name of a patient who the action was taken on
operation | Enum of allowed values | Type of action operation |CREATE, UPDATE, DELETE
dateEnd | Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | Filter by sentAt
dateStart |Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | Filter by sentAt
includeFormation | Boolean | Include cdt formation
