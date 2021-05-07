# Custom Data Types (CDT)

Custom data types in Welkin are associated with a Patient. In REST terms, they are a sub-resource to the patient object

Each CDT has a set of system fields associated with it and a set of custom fields that you will create in the designer

## System Fields

Field Name | Type | Description
--------- | ----------- | --------
id | UUID | Unique autogenerated identifier
updated_by | UUID |UUID of user or client who updated the record
updated_by_name | String | Full name of the user or api client that updated the record
updated_at | Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | Date and time of the last update to the record
created_by | UUID | UUID of user or client who created the record
created_by_name | String | Full name of the user or api client that created the record
created_at| Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | Date and time when the record was created
source_type | String | Source type of the record (for example: ASSESSMENT if assessment type  generated this record)
source_name | String | Name of the source type (for example: my_medication_assessment if assessment type  generated this record)
source_id | UUID | record ID of the source

## Working with CDT records

### Description
Get all cdt records

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/patients/{patientId}/cdts/{cdtName}`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/cdts/vitals`

> Response

```json
{
    "name": "vitals",
    "data": {
        "content": [
            {
                "id": "8c0684ac-217e-45f4-8727-5587220dd512",
                "patientId": "eac29796-6943-4307-bfe6-6b424d8b4b4b",
                "cdtId": "ba36a882-bbec-49ea-a99a-c84aac025f3f",
                "version": 70,
                "jsonBody": {
                    "external_guid": null,
                    "source_record_id": null,
                    "weight": 1,
                    "created_at": "2021-01-28T13:35:36.861Z",
                    "source_type": null,
                    "external_id": null,
                    "created_by_name": "MY NAME",
                    "created_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
                    "updated_by_name": "MY NAME",
                    "systolic": 1,
                    "diastolic": -1,
                    "updated_at": "2021-01-28T13:35:36.861Z",
                    "pulse": 1,
                    "temperature": -1,
                    "updated_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
                    "id": "8c0684ac-217e-45f4-8727-5587220dd512",
                    "source_id": null,
                    "blood_sugar": 1,
                    "source_name": null,
                    "height": -1
                }
            }
        ],
        "pageable": {
            "sort": {
                "sorted": false,
                "unsorted": true,
                "empty": true
            },
            "pageNumber": 0,
            "pageSize": 20,
            "offset": 0,
            "paged": true,
            "unpaged": false
        },
        "last": true,
        "totalPages": 1,
        "totalElements": 1,
        "numberOfElements": 1,
        "first": true,
        "number": 0,
        "sort": {
            "sorted": false,
            "unsorted": true,
            "empty": true
        },
        "size": 20,
        "empty": false
    }
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| cdtName | path | Name of cdt | Yes | string |
| fields |  args |<list fields>: fields=name,phone | No | string array
| page | args | page number | No | integer
| size | args |page size | No | integer
| sort | args | Sort field with sorting order(asc or desc) after coma | no | field,order |
| filters | args |key=v1,v2,v3 | No | key-value
| dateStart | args |Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | No | datetime
| dateEnd | args |Date_time in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format | No | datetime

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Get cdt record by id

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/patients/{patientId}/cdts/{cdtName}/{cdtRecordId}`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/cdts/vitals/8c0684ac-217e-45f4-8727-5587220dd512`

> Response

```json
{
    "id": "8c0684ac-217e-45f4-8727-5587220dd512",
    "patientId": "eac29796-6943-4307-bfe6-6b424d8b4b4b",
    "cdtId": "ba36a882-bbec-49ea-a99a-c84aac025f3f",
    "version": 70,
    "jsonBody": {
        "external_guid": null,
        "source_record_id": null,
        "weight": 1,
        "created_at": "2021-01-28T13:35:36.861Z",
        "source_type": null,
        "external_id": null,
        "created_by_name": "MY NAME",
        "created_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
        "updated_by_name": "MY NAME",
        "systolic": 1,
        "diastolic": -1,
        "updated_at": "2021-01-28T13:35:36.861Z",
        "pulse": 1,
        "temperature": -1,
        "updated_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
        "id": "8c0684ac-217e-45f4-8727-5587220dd512",
        "source_id": null,
        "blood_sugar": 1,
        "source_name": null,
        "height": -1
    }
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| cdtName | path | Name of cdt | Yes | string |
| cdtRecordId | path | ID of cdt record | Yes | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Create cdt record

### HTTP Request
***POST*** `/{tenantName}/{instanceName}/patients/{patientId}/cdts/{cdtName}`

in our example it would be:

***POST*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/cdts/{cdtName}`

> Request

```json
{
    "weight": 1,
    "systolic": 1,
    "diastolic": -1,
    "pulse": 1,
    "temperature": -1,
    "blood_sugar": 1,
    "height": -1
}
```

> Response

```json
{
    "id": "8c0684ac-217e-45f4-8727-5587220dd512",
    "patientId": "eac29796-6943-4307-bfe6-6b424d8b4b4b",
    "cdtId": "ba36a882-bbec-49ea-a99a-c84aac025f3f",
    "version": 70,
    "jsonBody": {
        "external_guid": null,
        "source_record_id": null,
        "weight": 1,
        "created_at": "2021-01-28T13:35:36.861Z",
        "source_type": null,
        "external_id": null,
        "created_by_name": "MY NAME",
        "created_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
        "updated_by_name": "MY NAME",
        "systolic": 1,
        "diastolic": -1,
        "updated_at": "2021-01-28T13:35:36.861Z",
        "pulse": 1,
        "temperature": -1,
        "updated_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
        "id": "8c0684ac-217e-45f4-8727-5587220dd512",
        "source_id": null,
        "blood_sugar": 1,
        "source_name": null,
        "height": -1
    }
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| userId | path | ID of user | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| cdtName | path | Name of cdt | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Created |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Update cdt record by id

### HTTP Request
***PATCH*** `/{tenantName}/{instanceName}/patients/{patientId}/cdts/{cdtName}/{cdtRecordId}`

in our example it would be:

***PATCH*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/cdts/vitals/8c0684ac-217e-45f4-8727-5587220dd512`

> Request

```json
{
   "pulse": 222
}
```

> Response

```json
{
    "id": "8c0684ac-217e-45f4-8727-5587220dd512",
    "patientId": "eac29796-6943-4307-bfe6-6b424d8b4b4b",
    "cdtId": "ba36a882-bbec-49ea-a99a-c84aac025f3f",
    "version": 70,
    "jsonBody": {
        "external_guid": null,
        "source_record_id": null,
        "weight": 1,
        "created_at": "2021-01-28T13:35:36.861Z",
        "source_type": null,
        "external_id": null,
        "created_by_name": "MY NAME",
        "created_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
        "updated_by_name": "MY NAME",
        "systolic": 1,
        "diastolic": -1,
        "updated_at": "2021-01-28T13:35:36.861Z",
        "pulse": 222,
        "temperature": -1,
        "updated_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
        "id": "8c0684ac-217e-45f4-8727-5587220dd512",
        "source_id": null,
        "blood_sugar": 1,
        "source_name": null,
        "height": -1
    }
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| userId | path | ID of user | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| cdtName | path | Name of cdt | Yes | string |
| cdtRecordId | path | ID of cdt record | Yes | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Update cdt records with bulk. Allowed only for list fields with bulk edit flag

### HTTP Request
***PATCH*** `/{tenantName}/{instanceName}/patients/{patientId}/cdts/{cdtName}`

in our example it would be:

***PATCH*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/cdts/vitals`

> Request

```json
{
    "rows": [
        {
            "id": "8c0684ac-217e-45f4-8727-5587220dd512",
            "jsonBody": {
                "list_field": "a"
            }
        }
    ]
}
```

> Response

```json
{
    "rows": [
        {
            "id": "8c0684ac-217e-45f4-8727-5587220dd512",
            "jsonBody": {
                "external_guid": null,
                "weight": 1,
                "created_at": "2021-01-28T13:35:36.861Z",
                "source_type": null,
                "external_id": null,
                "list_field": "a",
                "created_by_name": "MY NAME",
                "created_by": "f5b84d92-7989-45f4-bb5f-d85336c8e4b6",
                "updated_by_name": "MY NAME",
                "systolic": 1,
                "diastolic": -1,
                "updated_at": "2021-05-05T14:29:23.368Z",
                "pulse": 1,
                "temperature": -1,
                "updated_by": "2116dedb-1833-42a3-9a09-77ba00e20959",
                "id": "8c0684ac-217e-45f4-8727-5587220dd512",
                "source_id": null,
                "blood_sugar": 1,
                "source_name": null,
                "height": -1
            },
            "result": {
                "status": "OK",
                "content": null
            }
        }
    ]
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| userId | path | ID of user | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| cdtName | path | Name of cdt | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Delete cdt record by id

### HTTP Request
***DELETE*** `/{tenantName}/{instanceName}/patients/{patientId}/cdts/{cdtName}/{cdtRecordId}`

in our example it would be:

***DELETE*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/cdts/vitals/8c0684ac-217e-45f4-8727-5587220dd512`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| userId | path | ID of user | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| cdtName | path | Name of cdt | Yes | string |
| cdtRecordId | path | ID of cdt record | Yes | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |