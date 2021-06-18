# Encounters

APIs for working with an encounter infrastructure: records, assessment links, comments, template, disposition, disposition-formation

## Encounter records

### Description
Get all encounter records by patient id

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/patients/{patientId}/encounters`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/encounters`

> Response

```json
{
    "data": [
        {
            "id": "8208e50a-1a88-440d-8ad1-d847115cca89",
            "patientId": "eac29796-6943-4307-bfe6-6b424d8b4b4b",
            "cdtId": "aedc7247-a561-4b02-9e2a-86433b092b05",
            "version": 207,
            "jsonBody": {
                "startDatetime": "2021-04-15T07:41:48.272Z",
                "calendarEventId": null,
                "external_guid": null,
                "notes": null,
                "activeUserId": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
                "description": "test2",
                "created_at": "2021-04-14T10:23:00.983Z",
                "dispositionId": "e0e3eaa8-5f52-4a14-b578-31e810ae9b48",
                "source_type": null,
                "external_id": null,
                "title": "test2",
                "activeUserName": "MY NAME",
                "created_by_name": "MY NAME",
                "created_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
                "updated_by_name": "MY NAME",
                "updated_at": "2021-04-15T07:42:06.637Z",
                "templateName": null,
                "updated_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
                "id": "8208e50a-1a88-440d-8ad1-d847115cca89",
                "source_id": null,
                "endDatetime": null,
                "source_name": null,
                "status": "OPEN"
            }
        }
    ],
    "metaInfo": {
        "page": 0,
        "pageSize": 20,
        "totalElements": 1,
        "numberOfElements": 1,
        "totalPages": 1,
        "firstPage": true,
        "lastPage": true
    }
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| statuses | args | Encounter status. Available statuses: DRAFT,OPEN,ACTIVE,FINALIZED | no | string array |
| page | args | Pagination: page number | no | integer |
| size | args | Pagination: page size | no | integer |
| sort | args | Sort field with sorting order(asc or desc) after coma | no | field,order |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Get all encounter records with related data by patient id

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/patients/{patientId}/full-encounters`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/patients/08632f11-cb33-4b5b-aece-aaa360f9f747/full-encounters`

> Response

```json
{
    "data": [
        {
            "encounter": {encounter record},
            "disposition": {disposition record},
            "calendarEvent": {calendar event record},
            "userRelatedToCalendarEvent": {user record},
            "assessmentLinks": [assessment links],
            "comments": [comments]
        }
    ],
    "metaInfo": {
        "page": 0,
        "pageSize": 20,
        "totalElements": 1,
        "numberOfElements": 1,
        "totalPages": 1,
        "firstPage": true,
        "lastPage": true
    }
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| statuses | args | Encounter status. Available statuses: DRAFT,OPEN,ACTIVE,FINALIZED | no | string array |
| page | args | Pagination: page number | no | integer |
| size | args | Pagination: page size | no | integer |
| sort | args | Sort field with sorting order(asc or desc) after coma | no | field,order |
| onlyWithCalendarEvent | args | Exclude all information not related to calendar event, except encounter record  | no | boolean |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Get all encounter records by user id

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/users/{userId}/encounters`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/users/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/encounters`

> Response

```json
{
    "data": [
        {
            "id": "8208e50a-1a88-440d-8ad1-d847115cca89",
            "patientId": "eac29796-6943-4307-bfe6-6b424d8b4b4b",
            "cdtId": "aedc7247-a561-4b02-9e2a-86433b092b05",
            "version": 207,
            "jsonBody": {
                "startDatetime": "2021-04-15T07:41:48.272Z",
                "calendarEventId": null,
                "external_guid": null,
                "notes": null,
                "activeUserId": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
                "description": "test2",
                "created_at": "2021-04-14T10:23:00.983Z",
                "dispositionId": "e0e3eaa8-5f52-4a14-b578-31e810ae9b48",
                "source_type": null,
                "external_id": null,
                "title": "test2",
                "activeUserName": "MY NAME",
                "created_by_name": "MY NAME",
                "created_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
                "updated_by_name": "MY NAME",
                "updated_at": "2021-04-15T07:42:06.637Z",
                "templateName": null,
                "updated_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
                "id": "8208e50a-1a88-440d-8ad1-d847115cca89",
                "source_id": null,
                "endDatetime": null,
                "source_name": null,
                "status": "OPEN"
            }
        }
    ],
    "metaInfo": {
        "page": 0,
        "pageSize": 20,
        "totalElements": 1,
        "numberOfElements": 1,
        "totalPages": 1,
        "firstPage": true,
        "lastPage": true
    }
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| userId | path | ID of user | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| statuses | args | Encounter status. Available statuses: DRAFT,OPEN,ACTIVE,FINALIZED | no | string array |
| page | args | Pagination: page number | no | integer |
| size | args | Pagination: page size | no | integer |
| sort | args | Sort field with sorting order(asc or desc) after coma | no | field,order |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Get all encounter records with related data by user id

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/users/{userId}/full-encounters`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/users/f5b84d92-7989-45f4-bb5f-d85336c8e4b6/full-encounters`

> Response

```json
{
    "data": [
        {
            "encounter": {encounter record},
            "disposition": {disposition record},
            "calendarEvent": {calendar event record},
            "userRelatedToCalendarEvent": {user record},
            "assessmentLinks": [assessment links],
            "comments": [comments]
        }
    ],
    "metaInfo": {
        "page": 0,
        "pageSize": 20,
        "totalElements": 1,
        "numberOfElements": 1,
        "totalPages": 1,
        "firstPage": true,
        "lastPage": true
    }
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| userId | path | ID of user | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| statuses | args | Encounter status. Available statuses: DRAFT,OPEN,ACTIVE,FINALIZED | no | string array |
| page | args | Pagination: page number | no | integer |
| size | args | Pagination: page size | no | integer |
| sort | args | Sort field with sorting order(asc or desc) after coma | no | field,order |
| onlyWithCalendarEvent | args | Exclude all information not related to calendar event, except encounter record  | no | boolean |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Get encounter record by a patient id and encounter id

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/patients/{patientId}/encounters/{encounterId}`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/encounters/336ae731-c674-4b85-941a-ef3b37d93b82`

> Response

```json
{
            "id": "8208e50a-1a88-440d-8ad1-d847115cca89",
            "patientId": "eac29796-6943-4307-bfe6-6b424d8b4b4b",
            "cdtId": "aedc7247-a561-4b02-9e2a-86433b092b05",
            "version": 207,
            "jsonBody": {
                "startDatetime": "2021-04-15T07:41:48.272Z",
                "calendarEventId": null,
                "external_guid": null,
                "notes": null,
                "activeUserId": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
                "description": "test2",
                "created_at": "2021-04-14T10:23:00.983Z",
                "dispositionId": "e0e3eaa8-5f52-4a14-b578-31e810ae9b48",
                "source_type": null,
                "external_id": null,
                "title": "test2",
                "activeUserName": "MY NAME",
                "created_by_name": "MY NAME",
                "created_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
                "updated_by_name": "MY NAME",
                "updated_at": "2021-04-15T07:42:06.637Z",
                "templateName": null,
                "updated_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
                "id": "8208e50a-1a88-440d-8ad1-d847115cca89",
                "source_id": null,
                "endDatetime": null,
                "source_name": null,
                "status": "OPEN"
            }
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| encounterId | path | ID of encounter | Yes | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Get encounter record with all related data by a patient id and encounter id

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/patients/{patientId}/full-encounters/{encounterId}`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/patients/08632f11-cb33-4b5b-aece-aaa360f9f747/full-encounters/7d72c423-48bc-4fc6-aa35-72a6cdd0c4ca`

> Response

```json
{
    "data": [
        {
            "encounter": {encounter record},
            "disposition": {disposition record},
            "calendarEvent": {calendar event record},
            "userRelatedToCalendarEvent": {user record},
            "assessmentLinks": [assessment links],
            "comments": [comments]
        }
    ],
    "metaInfo": {
        "page": 0,
        "pageSize": 20,
        "totalElements": 1,
        "numberOfElements": 1,
        "totalPages": 1,
        "firstPage": true,
        "lastPage": true
    }
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| encounterId | path | ID of encounter | Yes | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Create an encounter for patient

### HTTP Request
***POST*** `/{tenantName}/{instanceName}/patients/{patientId}/encounters`

in our example it would be:

***POST*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/encounters`

> Request

```json
{
    "title": "Title",
    "description": "Description",
    "templateName": "template-1",
    "calendarEventId": null,
    "notes": "test"
}
```

> Response

```json
{
            "id": "8208e50a-1a88-440d-8ad1-d847115cca89",
            "patientId": "eac29796-6943-4307-bfe6-6b424d8b4b4b",
            "cdtId": "aedc7247-a561-4b02-9e2a-86433b092b05",
            "version": 207,
            "jsonBody": {
                "startDatetime": "2021-04-15T07:41:48.272Z",
                "calendarEventId": null,
                "external_guid": null,
                "notes": null,
                "activeUserId": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
                "description": "test2",
                "created_at": "2021-04-14T10:23:00.983Z",
                "dispositionId": "e0e3eaa8-5f52-4a14-b578-31e810ae9b48",
                "source_type": null,
                "external_id": null,
                "title": "test2",
                "activeUserName": "MY NAME",
                "created_by_name": "MY NAME",
                "created_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
                "updated_by_name": "MY NAME",
                "updated_at": "2021-04-15T07:42:06.637Z",
                "templateName": null,
                "updated_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
                "id": "8208e50a-1a88-440d-8ad1-d847115cca89",
                "source_id": null,
                "endDatetime": null,
                "source_name": null,
                "status": "DRAFT"
            }
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Created |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Update encounter record by encounter id

### HTTP Request
***PATCH*** `/{tenantName}/{instanceName}/patients/{patientId}/encounters/{encounterId}`

in our example it would be:

***PATCH*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/encounters/336ae731-c674-4b85-941a-ef3b37d93b82`

> Request

```json
{
    "title": "Title",
    "description": "Description",
    "templateName": "template-1",
    "status": "OPEN",
    "calendarEventId": null,
    "notes": "test"
}
```

> Response

```json
{
            "id": "8208e50a-1a88-440d-8ad1-d847115cca89",
            "patientId": "eac29796-6943-4307-bfe6-6b424d8b4b4b",
            "cdtId": "aedc7247-a561-4b02-9e2a-86433b092b05",
            "version": 207,
            "jsonBody": {
                "startDatetime": "2021-04-15T07:41:48.272Z",
                "calendarEventId": null,
                "external_guid": null,
                "notes": null,
                "activeUserId": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
                "description": "test2",
                "created_at": "2021-04-14T10:23:00.983Z",
                "dispositionId": "e0e3eaa8-5f52-4a14-b578-31e810ae9b48",
                "source_type": null,
                "external_id": null,
                "title": "test2",
                "activeUserName": "MY NAME",
                "created_by_name": "MY NAME",
                "created_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
                "updated_by_name": "MY NAME",
                "updated_at": "2021-04-15T07:42:06.637Z",
                "templateName": null,
                "updated_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
                "id": "8208e50a-1a88-440d-8ad1-d847115cca89",
                "source_id": null,
                "endDatetime": null,
                "source_name": null,
                "status": "OPEN"
            }
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| encounterId | path | ID of encounter | Yes | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Delete encounter record by encounter id

### HTTP Request
***DELETE*** `/{tenantName}/{instanceName}/patients/{patientId}/encounters/{encounterId}`

in our example it would be:

***DELETE*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/encounters/336ae731-c674-4b85-941a-ef3b37d93b82`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| encounterId | path | ID of encounter | Yes | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

## Encounter comments

### Description
Get all encounter comments by encounter id

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/patients/{patientId}/encounters/{encounterId}/comments`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/encounters/336ae731-c674-4b85-941a-ef3b37d93b82/comments`

> Response

```json
[
    {
        "id": "0e692ed3-b250-42ee-a17b-f65e69efcc07",
        "createdAt": "2021-04-21T06:59:30.079Z",
        "updatedAt": "2021-04-21T06:59:30.079Z",
        "createdBy": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
        "updatedBy": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
        "createdByName": "MY NAME",
        "updatedByName": "MY NAME",
        "encounterId": "d74e3745-3692-4555-acb6-e4db94643f56",
        "text": "comment1"
    },
    {
        "id": "45955cdb-8d72-4f02-905f-34f7c158c351",
        "createdAt": "2021-04-21T06:59:35.170Z",
        "updatedAt": "2021-04-21T06:59:35.170Z",
        "createdBy": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
        "updatedBy": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
        "createdByName": "MY NAME",
        "updatedByName": "MY NAME",
        "encounterId": "d74e3745-3692-4555-acb6-e4db94643f56",
        "text": "comment2"
    }
]
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| encounterId | path | ID of encounter | Yes | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Get encounter comment by encounter id and comment id

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/patients/{patientId}/encounters/{encounterId}/comments/{commentId}`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/encounters/336ae731-c674-4b85-941a-ef3b37d93b82/comments/0e692ed3-b250-42ee-a17b-f65e69efcc07`

> Response

```json
{
        "id": "0e692ed3-b250-42ee-a17b-f65e69efcc07",
        "createdAt": "2021-04-21T06:59:30.079Z",
        "updatedAt": "2021-04-21T06:59:30.079Z",
        "createdBy": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
        "updatedBy": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
        "createdByName": "MY NAME",
        "updatedByName": "MY NAME",
        "encounterId": "d74e3745-3692-4555-acb6-e4db94643f56",
        "text": "comment1"
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| encounterId | path | ID of encounter | Yes | UUID |
| commentId | path | ID of comment | Yes | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Create a comment for encounter

### HTTP Request
***POST*** `/{tenantName}/{instanceName}/patients/{patientId}/encounters/{encounterId}/comments`

in our example it would be:

***POST*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/encounters/336ae731-c674-4b85-941a-ef3b37d93b82/comments`

> Request

```json
{
    "text": "comment"
}
```

> Response

```json
{
        "id": "0e692ed3-b250-42ee-a17b-f65e69efcc07",
        "createdAt": "2021-04-21T06:59:30.079Z",
        "updatedAt": "2021-04-21T06:59:30.079Z",
        "createdBy": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
        "updatedBy": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
        "createdByName": "MY NAME",
        "updatedByName": "MY NAME",
        "encounterId": "d74e3745-3692-4555-acb6-e4db94643f56",
        "text": "comment"
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| encounterId | path | ID of encounter | Yes | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Created |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Update comment for encounter by comment id

### HTTP Request
***PUT*** `/{tenantName}/{instanceName}/patients/{patientId}/encounters/{encounterId}/comments/{commentId}`

in our example it would be:

***PUT*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/encounters/336ae731-c674-4b85-941a-ef3b37d93b82/comments/0e692ed3-b250-42ee-a17b-f65e69efcc07`

> Request

```json
{
    "text": "comment2"
}
```

> Response

```json
{
        "id": "0e692ed3-b250-42ee-a17b-f65e69efcc07",
        "createdAt": "2021-04-21T06:59:30.079Z",
        "updatedAt": "2021-04-21T06:59:30.079Z",
        "createdBy": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
        "updatedBy": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
        "createdByName": "MY NAME",
        "updatedByName": "MY NAME",
        "encounterId": "d74e3745-3692-4555-acb6-e4db94643f56",
        "text": "comment2"
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| encounterId | path | ID of encounter | Yes | UUID |
| commentId | path | ID of comment | Yes | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Delete comment for encounter by comment id

### HTTP Request
***DELETE*** `/{tenantName}/{instanceName}/patients/{patientId}/encounters/{encounterId}/comments/{commentId}`

in our example it would be:

***DELETE*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/encounters/336ae731-c674-4b85-941a-ef3b37d93b82/comments/0e692ed3-b250-42ee-a17b-f65e69efcc07`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| encounterId | path | ID of encounter | Yes | UUID |
| commentId | path | ID of comment | Yes | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

## Encounter assessment links

### Description
Get all assessment links by encounter id

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/patients/{patientId}/encounters/{encounterId}/assessments`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/encounters/336ae731-c674-4b85-941a-ef3b37d93b82/assessments`

> Response

```json
[
    {
        "id": "44b6c521-b85f-47a5-9c93-7c5d56c19efb",
        "patientId": "552f1ea6-960e-4b3c-be50-35d7a1d01fc4",
        "cdtId": "0c9ce071-7dca-4714-8350-f75cbf01f2da",
        "version": 192,
        "jsonBody": {
            "created_at": "2021-03-30T10:31:11.151Z",
            "source_type": "ENCOUNTER",
            "fromTemplate": false,
            "created_by_name": "MY NAME",
            "created_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
            "relation": "ASSESSMENT",
            "updated_by_name": "MY NAME",
            "updated_at": "2021-03-30T10:31:11.151Z",
            "assessmentName": "ccc",
            "updated_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
            "id": "44b6c521-b85f-47a5-9c93-7c5d56c19efb",
            "source_id": "91996e95-fa68-4f28-be9b-3d108cf081a8",
            "assessmentRecordId": null,
            "source_name": "__encounter__"
        }
    },
    {
        "id": "e88a7909-438f-4584-b219-0ce538bb24d8",
        "patientId": "552f1ea6-960e-4b3c-be50-35d7a1d01fc4",
        "cdtId": "019b8736-5769-40a3-af22-787421e68b7e",
        "version": 191,
        "jsonBody": {
            "created_at": "2021-03-30T09:42:26.250Z",
            "source_type": "ENCOUNTER",
            "fromTemplate": true,
            "created_by_name": "MY NAME",
            "created_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
            "relation": "ASSESSMENT",
            "updated_by_name": "MY NAME",
            "updated_at": "2021-03-30T09:42:26.250Z",
            "assessmentName": "wel-1388",
            "updated_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
            "id": "e88a7909-438f-4584-b219-0ce538bb24d8",
            "source_id": "91996e95-fa68-4f28-be9b-3d108cf081a8",
            "assessmentRecordId": null,
            "source_name": "__encounter__"
        }
    }
]
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| encounterId | path | ID of encounter | Yes | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Get assessment link by encounter id and assessment link id

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/patients/{patientId}/encounters/{encounterId}/assessments/{encounterAssessmentId}`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/encounters/336ae731-c674-4b85-941a-ef3b37d93b82/assessments/0e692ed3-b250-42ee-a17b-f65e69efcc07`

> Response

```json
{
        "id": "44b6c521-b85f-47a5-9c93-7c5d56c19efb",
        "patientId": "552f1ea6-960e-4b3c-be50-35d7a1d01fc4",
        "cdtId": "0c9ce071-7dca-4714-8350-f75cbf01f2da",
        "version": 192,
        "jsonBody": {
            "created_at": "2021-03-30T10:31:11.151Z",
            "source_type": "ENCOUNTER",
            "fromTemplate": false,
            "created_by_name": "MY NAME",
            "created_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
            "relation": "ASSESSMENT",
            "updated_by_name": "MY NAME",
            "updated_at": "2021-03-30T10:31:11.151Z",
            "assessmentName": "ccc",
            "updated_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
            "id": "44b6c521-b85f-47a5-9c93-7c5d56c19efb",
            "source_id": "91996e95-fa68-4f28-be9b-3d108cf081a8",
            "assessmentRecordId": null,
            "source_name": "__encounter__"
        }
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| encounterId | path | ID of encounter | Yes | UUID |
| encounterAssessmentId | path | ID of assessment link | Yes | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Create an assessment link for encounter

### HTTP Request
***POST*** `/{tenantName}/{instanceName}/patients/{patientId}/encounters/{encounterId}/assessments`

in our example it would be:

***POST*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/encounters/336ae731-c674-4b85-941a-ef3b37d93b82/assessments`

> Request

```json
{
    "assessmentName": "some-form",
    "assessmentRecordId": null
}
```

> Response

```json
{
        "id": "44b6c521-b85f-47a5-9c93-7c5d56c19efb",
        "patientId": "552f1ea6-960e-4b3c-be50-35d7a1d01fc4",
        "cdtId": "0c9ce071-7dca-4714-8350-f75cbf01f2da",
        "version": 192,
        "jsonBody": {
            "created_at": "2021-03-30T10:31:11.151Z",
            "source_type": "ENCOUNTER",
            "fromTemplate": false,
            "created_by_name": "MY NAME",
            "created_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
            "relation": "ASSESSMENT",
            "updated_by_name": "MY NAME",
            "updated_at": "2021-03-30T10:31:11.151Z",
            "assessmentName": "some-form",
            "updated_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
            "id": "44b6c521-b85f-47a5-9c93-7c5d56c19efb",
            "source_id": "91996e95-fa68-4f28-be9b-3d108cf081a8",
            "assessmentRecordId": null,
            "source_name": "__encounter__"
        }
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| encounterId | path | ID of encounter | Yes | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Created |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Update assessment link for encounter by assessment link id

### HTTP Request
***PATCH*** `/{tenantName}/{instanceName}/patients/{patientId}/encounters/{encounterId}/assessments/{encounterAssessmentId}`

in our example it would be:

***PATCH*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/encounters/336ae731-c674-4b85-941a-ef3b37d93b82/assessments/0e692ed3-b250-42ee-a17b-f65e69efcc07`

> Request

```json
{
    "assessmentRecordId": "196f6201-78bb-4a34-8334-4b969699772b"
}
```

> Response

```json
{
        "id": "44b6c521-b85f-47a5-9c93-7c5d56c19efb",
        "patientId": "552f1ea6-960e-4b3c-be50-35d7a1d01fc4",
        "cdtId": "0c9ce071-7dca-4714-8350-f75cbf01f2da",
        "version": 192,
        "jsonBody": {
            "created_at": "2021-03-30T10:31:11.151Z",
            "source_type": "ENCOUNTER",
            "fromTemplate": false,
            "created_by_name": "MY NAME",
            "created_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
            "relation": "ASSESSMENT",
            "updated_by_name": "MY NAME",
            "updated_at": "2021-03-30T10:31:11.151Z",
            "assessmentName": "some-form",
            "updated_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
            "id": "44b6c521-b85f-47a5-9c93-7c5d56c19efb",
            "source_id": "91996e95-fa68-4f28-be9b-3d108cf081a8",
            "assessmentRecordId": "196f6201-78bb-4a34-8334-4b969699772b",
            "source_name": "__encounter__"
        }
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| encounterId | path | ID of encounter | Yes | UUID |
| encounterAssessmentId | path | ID of assessment link | Yes | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Delete assessment link for encounter by assessment link id

### HTTP Request
***DELETE*** `/{tenantName}/{instanceName}/patients/{patientId}/encounters/{encounterId}/assessments/{encounterAssessmentId}`

in our example it would be:

***DELETE*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/encounters/336ae731-c674-4b85-941a-ef3b37d93b82/assessments/0e692ed3-b250-42ee-a17b-f65e69efcc07`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| encounterId | path | ID of encounter | Yes | UUID |
| encounterAssessmentId | path | ID of assessment link | Yes | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

## Encounter disposition record

### Description
Get disposition for encounter

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/patients/{patientId}/encounters/{encounterId}/disposition`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/encounters/336ae731-c674-4b85-941a-ef3b37d93b82/disposition`

> Response

```json
{
    "id": "b4d5fd02-50c6-4a47-9fdc-65e6e97c841d",
    "patientId": "552f1ea6-960e-4b3c-be50-35d7a1d01fc4",
    "cdtId": "8ba794c6-2265-4574-8618-8f5e449b1889",
    "version": 191,
    "jsonBody": {
        "updated_by_name": "MY NAME",
        "updated_at": "2021-03-29T12:31:06.529Z",
        "cpt": null,
        "updated_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
        "created_at": "2021-03-29T12:29:57.307Z",
        "source_type": "ENCOUNTER",
        "id": "b4d5fd02-50c6-4a47-9fdc-65e6e97c841d",
        "source_id": "336ae731-c674-4b85-941a-ef3b37d93b82",
        "icd-10": "val",
        "created_by_name": "MY NAME",
        "created_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
        "source_name": "__encounter__"
    }
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| encounterId | path | ID of encounter | Yes | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Update disposition for encounter

### HTTP Request
***PATCH*** `/{tenantName}/{instanceName}/patients/{patientId}/encounters/{encounterId}/disposition`

in our example it would be:

***PATCH*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/encounters/336ae731-c674-4b85-941a-ef3b37d93b82/disposition`

> Request

```json
{
    "cpt": null,
    "icd-10": null
}
```

> Response

```json
{
    "id": "b4d5fd02-50c6-4a47-9fdc-65e6e97c841d",
    "patientId": "552f1ea6-960e-4b3c-be50-35d7a1d01fc4",
    "cdtId": "8ba794c6-2265-4574-8618-8f5e449b1889",
    "version": 191,
    "jsonBody": {
        "updated_by_name": "MY NAME",
        "updated_at": "2021-03-29T12:31:06.529Z",
        "cpt": null,
        "updated_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
        "created_at": "2021-03-29T12:29:57.307Z",
        "source_type": "ENCOUNTER",
        "id": "b4d5fd02-50c6-4a47-9fdc-65e6e97c841d",
        "source_id": "336ae731-c674-4b85-941a-ef3b37d93b82",
        "icd-10": null,
        "created_by_name": "MY NAME",
        "created_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
        "source_name": "__encounter__"
    }
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| encounterId | path | ID of encounter | Yes | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

## Encounter disposition formation

### Description
Get disposition formation

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/formations/{version}/encounter-disposition`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/formations/current/encounter-disposition`

> Response

```json
{
    "id": "c8578422-7369-45d3-b8ff-e4d6a9dc99f9",
    "name": "__encounter_disposition__",
    "title": null,
    "label": null,
    "version": 218,
    "internal": true,
    "readable": true,
    "updatable": true,
    "type": "MULTI_RECORD",
    "relation": "ENCOUNTER_DISPOSITION",
    "fields": [
        {
            "name": "notes",
            "type": "text",
            "dictionary": null,
            "searchable": false,
            "bulkEdit": false,
            "phi": false,
            "meta": {
                "required": false
            }
        },
        {
            "name": "id",
            "type": "text",
            "dictionary": null,
            "searchable": false,
            "bulkEdit": false,
            "phi": false,
            "meta": {
                "required": false
            }
        },
        {
            "name": "created_at",
            "type": "datetime",
            "dictionary": null,
            "searchable": false,
            "bulkEdit": false,
            "phi": false,
            "meta": {
                "required": false
            }
        },
        {
            "name": "created_by",
            "type": "text",
            "dictionary": null,
            "searchable": false,
            "bulkEdit": false,
            "phi": false,
            "meta": {
                "required": false
            }
        },
        {
            "name": "created_by_name",
            "type": "text",
            "dictionary": null,
            "searchable": false,
            "bulkEdit": false,
            "phi": false,
            "meta": {
                "required": false
            }
        },
        {
            "name": "updated_at",
            "type": "datetime",
            "dictionary": null,
            "searchable": false,
            "bulkEdit": false,
            "phi": false,
            "meta": {
                "required": false
            }
        },
        {
            "name": "updated_by",
            "type": "text",
            "dictionary": null,
            "searchable": false,
            "bulkEdit": false,
            "phi": false,
            "meta": {
                "required": false
            }
        },
        {
            "name": "updated_by_name",
            "type": "text",
            "dictionary": null,
            "searchable": false,
            "bulkEdit": false,
            "phi": false,
            "meta": {
                "required": false
            }
        },
        {
            "name": "source_name",
            "type": "text",
            "dictionary": null,
            "searchable": false,
            "bulkEdit": false,
            "phi": false,
            "meta": {
                "required": false
            }
        },
        {
            "name": "source_type",
            "type": "text",
            "dictionary": null,
            "searchable": false,
            "bulkEdit": false,
            "phi": false,
            "meta": {
                "required": false
            }
        },
        {
            "name": "source_id",
            "type": "text",
            "dictionary": null,
            "searchable": false,
            "bulkEdit": false,
            "phi": false,
            "meta": {
                "required": false
            }
        },
        {
            "name": "external_id",
            "type": "text",
            "dictionary": null,
            "searchable": false,
            "bulkEdit": false,
            "phi": false,
            "meta": {
                "required": false
            }
        },
        {
            "name": "external_guid",
            "type": "text",
            "dictionary": null,
            "searchable": false,
            "bulkEdit": false,
            "phi": false,
            "meta": {
                "required": false
            }
        }
    ],
    "_containsPHI": false
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| version | path | Version of formation | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Update disposition formation

### HTTP Request
***PUT*** `/{tenantName}/{instanceName}/formations/draft/encounter-disposition`

in our example it would be:

***PUT*** `https://api.live.welkincloud.io/gh/sb-demo/formations/draft/encounter-disposition`

> Request

```json
{
    "name": "__encounter_disposition__",
    "fields": [
        {
            "name": "icd-10",
            "type": "text",
            "meta": {
                "required": true
            }
        },
        {
            "name": "cpt",
            "type": "select",
            "dictionary": {
                "name": "cpt",
                "field": "value"
            },
            "meta": {
                "required": false
            }
        }
    ]
}
```

> Response

```json
{
    "id": "c8578422-7369-45d3-b8ff-e4d6a9dc99f9",
    "name": "__encounter_disposition__",
    "title": null,
    "label": null,
    "version": 218,
    "internal": true,
    "readable": true,
    "updatable": true,
    "type": "MULTI_RECORD",
    "relation": "ENCOUNTER_DISPOSITION",
    "fields": [
          {
           "name": "icd-10",
           "type": "text",
           "dictionary": null,
           "searchable": false,
           "bulkEdit": false,
           "phi": false,
           "meta": {
               "required": false
           }
        },
        {
        "name": "cpt",
        "type": "select",
        "dictionary": {
           "name": "cpt",
           "field": "value"
        },
        "searchable": false,
         "bulkEdit": false,
         "phi": false,
         "meta": {
             "required": false
         }
        },
        {
            "name": "id",
            "type": "text",
            "dictionary": null,
            "searchable": false,
            "bulkEdit": false,
            "phi": false,
            "meta": {
                "required": false
            }
        },
        {
            "name": "created_at",
            "type": "datetime",
            "dictionary": null,
            "searchable": false,
            "bulkEdit": false,
            "phi": false,
            "meta": {
                "required": false
            }
        },
        {
            "name": "created_by",
            "type": "text",
            "dictionary": null,
            "searchable": false,
            "bulkEdit": false,
            "phi": false,
            "meta": {
                "required": false
            }
        },
        {
            "name": "created_by_name",
            "type": "text",
            "dictionary": null,
            "searchable": false,
            "bulkEdit": false,
            "phi": false,
            "meta": {
                "required": false
            }
        },
        {
            "name": "updated_at",
            "type": "datetime",
            "dictionary": null,
            "searchable": false,
            "bulkEdit": false,
            "phi": false,
            "meta": {
                "required": false
            }
        },
        {
            "name": "updated_by",
            "type": "text",
            "dictionary": null,
            "searchable": false,
            "bulkEdit": false,
            "phi": false,
            "meta": {
                "required": false
            }
        },
        {
            "name": "updated_by_name",
            "type": "text",
            "dictionary": null,
            "searchable": false,
            "bulkEdit": false,
            "phi": false,
            "meta": {
                "required": false
            }
        },
        {
            "name": "source_name",
            "type": "text",
            "dictionary": null,
            "searchable": false,
            "bulkEdit": false,
            "phi": false,
            "meta": {
                "required": false
            }
        },
        {
            "name": "source_type",
            "type": "text",
            "dictionary": null,
            "searchable": false,
            "bulkEdit": false,
            "phi": false,
            "meta": {
                "required": false
            }
        },
        {
            "name": "source_id",
            "type": "text",
            "dictionary": null,
            "searchable": false,
            "bulkEdit": false,
            "phi": false,
            "meta": {
                "required": false
            }
        },
        {
            "name": "external_id",
            "type": "text",
            "dictionary": null,
            "searchable": false,
            "bulkEdit": false,
            "phi": false,
            "meta": {
                "required": false
            }
        },
        {
            "name": "external_guid",
            "type": "text",
            "dictionary": null,
            "searchable": false,
            "bulkEdit": false,
            "phi": false,
            "meta": {
                "required": false
            }
        }
    ],
    "_containsPHI": false
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

## Encounter templates

### Description
Get all encounter templates

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/formations/{version}/encounters`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/formations/current/encounters`

> Response

```json
[
    {
        "id": "a2063f42-395c-469f-8f4e-825af9223bef",
        "name": "temp-1",
        "title": "MyTitle",
        "assessmentNames": [
            "assessment-1"
        ]
    },
    {
        "id": "fdfea00b-e7f5-4c31-a7a0-affda858a9f6",
        "name": "temp-2",
        "title": "MyTitle",
        "assessmentNames": [
            "assessment-2"
        ]
    }
]
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| version | path | Version of formation | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Get encounter template by name

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/formations/{version}/encounters/{encounterTemplateName}`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/formations/current/encounters/temp-1`

> Response

```json
{
        "id": "a2063f42-395c-469f-8f4e-825af9223bef",
        "name": "temp-1",
        "title": "MyTitle",
        "assessmentNames": [
            "assessment-1"
        ]
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| version | path | Version of formation | Yes | string |
| encounterTemplateName | path | Name of template | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Create a template for encounter

### HTTP Request
***POST*** `/{tenantName}/{instanceName}/formations/draft/encounters`

in our example it would be:

***POST*** `https://api.live.welkincloud.io/gh/sb-demo/formations/draft/encounters`

> Request

```json
{
    "name": "temp-1",
    "title": "MyTitle",
    "assessmentNames": [
        "assessment-1"
    ]
}
```

> Response

```json
{
        "id": "a2063f42-395c-469f-8f4e-825af9223bef",
        "name": "temp-1",
        "title": "MyTitle",
        "assessmentNames": [
            "assessment-1"
        ]
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Created |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Update encounter template by encounter template name

### HTTP Request
***PUT*** `/{tenantName}/{instanceName}/formations/draft/encounters/{encounterTemplateName}`

in our example it would be:

***PUT*** `https://api.live.welkincloud.io/gh/sb-demo/formations/draft/encounters/temp-1

> Request

```json
{
    "name": "temp-1",
    "title": "MyTitle",
    "assessmentNames": [
        "assessment-2"
    ]
}
```

> Response

```json
{
        "id": "a2063f42-395c-469f-8f4e-825af9223bef",
        "name": "temp-1",
        "title": "MyTitle",
        "assessmentNames": [
            "assessment-2"
        ]
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| encounterTemplateName | path | Name of template | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Delete encounter template by template name

### HTTP Request
***DELETE*** `/{tenantName}/{instanceName}/formations/draft/encounters/{encounterTemplateName}`

in our example it would be:

***DELETE*** `https://api.live.welkincloud.io/gh/sb-demo/formations/draft/encounters/336ae731-c674-4b85-941a-ef3b37d93b82`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| encounterTemplateName | path | Name of template | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
