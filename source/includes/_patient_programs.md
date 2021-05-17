# Patient programs

## Get all patient program records by id

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/patients/{patientId}/programs`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/patients/08632f11-cb33-4b5b-aece-aaa360f9f747/programs`

> Response

```json
{
    "data": [
        {
            "createdAt": "2021-01-21T07:38:32.333Z",
            "programName": "lead-management-program",
            "programTitle": "Lead Management Program",
            "programDescription": "Program for lead management",
            "assigned": true,
            "patientId": "08632f11-cb33-4b5b-aece-aaa360f9f747",
            "currentPhase": {
                "timestamp": "2021-01-21T09:38:44.323Z",
                "name": "intake",
                "title": "Intake",
                "description": "Intake Phase",
                "currentVersion": "59"
            },
            "status": "IN_PROGRESS",
            "compatibleWithCurrentVersion": true,
            "pathHistory": [
                {
                    "timestamp": "2021-01-21T09:38:44.323Z",
                    "name": "intake",
                    "title": "Intake",
                    "description": "Intake Phase",
                    "currentVersion": "59"
                }
            ]
        }
    ],
    "metaInfo": {
        "page": 0,
        "pageSize": 20,
        "totalElements": 1,
        "numberOfElements": 1,
        "totalPages": 1,
        "lastPage": true,
        "firstPage": true
    }
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| assignedPrograms | args | Assigned or unassigned programs | no | boolean |
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

## Get patient program record

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/patients/{patientId}/programs/{programName}`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/patients/08632f11-cb33-4b5b-aece-aaa360f9f747/programs/lead-management-program`

> Response

```json
{
    "createdAt": "2021-01-21T07:38:32.333Z",
    "programName": "lead-management-program",
    "programTitle": "Lead Management Program",
    "programDescription": "Program for lead management",
    "assigned": true,
    "patientId": "08632f11-cb33-4b5b-aece-aaa360f9f747",
    "currentPhase": {
        "timestamp": "2021-01-21T09:38:44.323Z",
        "name": "intake",
        "title": "Intake",
        "description": "Intake Phase",
        "currentVersion": "59"
    },
    "status": "IN_PROGRESS",
    "compatibleWithCurrentVersion": true,
    "pathHistory": [
        {
            "timestamp": "2021-01-21T09:38:44.323Z",
            "name": "intake",
            "title": "Intake",
            "description": "Intake Phase",
            "currentVersion": "59"
        }
    ]
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| programName | path | Name of program | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

## Update patient program status and assign program

### HTTP Request
***PATCH*** `/{tenantName}/{instanceName}/patients/{patientId}/programs/{programName}`

in our example it would be:

***PATCH*** `https://api.live.welkincloud.io/gh/sb-demo/patients/08632f11-cb33-4b5b-aece-aaa360f9f747/programs/prog-4`

> Request

```json
{
    "assigned" : true,
    "status" : "IN_PROGRESS"
}
```

> Response

```json
{
    "createdAt": "2021-05-17T09:13:33.332Z",
    "programName": "prog-4",
    "programTitle": "prog-4",
    "programDescription": "",
    "assigned": true,
    "patientId": "08632f11-cb33-4b5b-aece-aaa360f9f747",
    "currentPhase": null,
    "status": "IN_PROGRESS",
    "compatibleWithCurrentVersion": true,
    "pathHistory": []
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| programName | path | Name of program | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Created |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

## Change phase for patient program

### HTTP Request
***PATCH*** `/{tenantName}/{instanceName}/patients/{patientId}/programs/{programName}/phases`

in our example it would be:

***PATCH*** `https://api.live.welkincloud.io/gh/sb-demo/patients/08632f11-cb33-4b5b-aece-aaa360f9f747/programs/lead-management-program/phases`

> Request

```json
{
    "phaseName":"documents-sent"
}
```

> Response

```json
{
    "createdAt": "2021-01-21T07:38:32.333Z",
    "programName": "lead-management-program",
    "programTitle": "Lead Management Program",
    "programDescription": "Program for lead management",
    "assigned": true,
    "patientId": "08632f11-cb33-4b5b-aece-aaa360f9f747",
    "currentPhase": {
        "timestamp": "2021-05-17T12:18:10.295Z",
        "name": "documents-sent",
        "title": "Documents Sent",
        "description": "When documents are sent for signature",
        "currentVersion": "239"
    },
    "status": "IN_PROGRESS",
    "compatibleWithCurrentVersion": true,
    "pathHistory": [
        {
            "timestamp": "2021-01-21T09:38:44.323Z",
            "name": "intake",
            "title": "Intake",
            "description": "Intake Phase",
            "currentVersion": "59"
        },
        {
            "timestamp": "2021-05-17T12:18:10.295Z",
            "name": "documents-sent",
            "title": "Documents Sent",
            "description": "When documents are sent for signature",
            "currentVersion": "239"
        }
    ]
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| programName | path | Name of program | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Created |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

## Unassign patient from program

### HTTP Request
***DELETE*** `/{tenantName}/{instanceName}/patients/{patientId}/programs/{programName}`

in our example it would be:

***DELETE*** `https://api.live.welkincloud.io/gh/sb-demo/patients/08632f11-cb33-4b5b-aece-aaa360f9f747/programs/prog-4`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| programName | path | Name of program | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Created |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
