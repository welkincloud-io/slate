# Webhook audit

## Find webhook audit event

It is a typical API to work with webhook audit 

`URL Structure: {{url}} / {{tenantName}} / admin /audit-webhook`

in our example it would be:
`https://api.live.welkincloud.io/gh/admin/audit-webhook`

```json
 {
  "id": "bd20fc04-2b88-45ad-a52e-76d0d0a649ab",
  "sentAt": "2021-04-09T18:10:21.067Z",
  "eventEntity": "ASSESSMENT",
  "patientId": "2295910b-bd94-4fe6-b3c4-3023861c34e1",
  "instance": "demo",
  "status": "DELIVERED",
  "eventSubtype": "ASSESSMENT_COMPLETED",
  "record": {
    "name": "webhook_test",
    "url": "https://webhook.site/e40b03da-2e33-46be-80c4-b9bbbd172aae",
    "headers": [
      {
        "name": "webhook_header",
        "value": "webhook_header_value"
      }
    ],
    "queryParameters": [
      {
        "name": "wh_query",
        "value": "wh_query_value"
      }
    ]
  }
}
```

Fields description:

Field Name |   Format  |  Description| Allowed values
---------  |   -----   |  ---------| -------
instance  |  String |  Instance name
eventEntity | Enum of allowed values | Entity with which the webhook was called
eventSubtype | Enum of allowed values | Type of performing action
status | Enum of allowed values | Webhook call status | SENT, DELIVERED, FAILED,
patientId | UUID |  Id of the patient who the action was taken on
record |  Object |  Object after performing the action on it
headers | List | List of headers with which the webhook is configured and was called
queryParameters | List |  List of parameters with which the webhook is configured and was called

1. HTTP Method: GET
2. HTTP URL: `https://api.dev.welkincloud.io/lotus/admin/audit-webhook?size=20&page=0&sort=createdAt%2Cdesc&dateStart=2021-02-26T17%3A00%3A00.000Z&instance=test`

Parameters| Format | Description | Allowed values
--------- | ----------- | -------- | -----------
instance | String | Instance name
dateEnd | Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | Filter by sentAt
dateStart | Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | Filter by sentAt
eventSubtype | Enum of allowed values | Type of performing action
entity | Enum of allowed values | Entity with which the webhook was called | CDT,  ASSESSMENT
