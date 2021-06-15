# Dictionaries

APIs for working with dictionary infrastructure: records and formation
There are 3 dictionaries by default:
1. Timezone(timezone) - cannot be changed or populated
2. CPT(cpt) and ICD-10(icd-10) - cannot be changed, but can be populated

## Dictionary records

### Description
Get all dictionary records by name

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/dictionaries/{dictionaryName}`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/dictionaries/cpt`

> Response

```json
{
    "dictionaryName": "cpt",
    "lastUpdatedAt": "2021-05-11T07:08:37.209Z",
    "records": [
        {
            "id": "eb5d2e64-0f10-4014-b54d-7720028af60f",
            "createdAt": "2021-05-11T07:08:37.192Z",
            "updatedAt": "2021-05-11T07:08:37.192Z",
            "fullValue": "2222",
            "deleted": false,
            "values": {
                "value": "2222"
            }
        },
        {
            "id": "017e9b2f-c82d-4262-af0d-4827b7fb65c4",
            "createdAt": "2021-05-11T07:08:37.209Z",
            "updatedAt": "2021-05-11T07:08:37.209Z",
            "fullValue": "3333",
            "deleted": false,
            "values": {
                "value": "3333"
            }
        },
        {
            "id": "001806e2-3464-40b2-8adb-e756abe31fb1",
            "createdAt": "2021-04-09T09:24:44.566Z",
            "updatedAt": "2021-04-09T09:24:44.566Z",
            "fullValue": "1111",
            "deleted": false,
            "values": {
                "value": "1111"
            }
        }
    ]
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| dictionaryName | path | Name of dictionary | Yes | string |
| dateStart | args | From updated_at value | no | ISO datetime |
| dateEnd | args | Before updated_at value | no | ISO datetime |
| showDeleted | args | Show or hide deleted records | no | boolean |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Get dictionary record by name and id

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/dictionaries/{dictionaryName}/{dictionaryRecordId}`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/dictionaries/cpt/001806e2-3464-40b2-8adb-e756abe31fb1`
> Response

```json
{
     "id": "001806e2-3464-40b2-8adb-e756abe31fb1",
     "createdAt": "2021-04-09T09:24:44.566Z",
     "updatedAt": "2021-04-09T09:24:44.566Z",
     "fullValue": "1111",
     "deleted": false,
     "values": {
         "value": "1111"
     }
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| dictionaryName | path | Name of dictionary | Yes | string |
| dictionaryRecordId | path | Record ID | Yes | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Add value to dictionary

### HTTP Request
***POST*** `/{tenantName}/{instanceName}/dictionaries/{dictionaryName}`

in our example it would be:

***POST*** `https://api.live.welkincloud.io/gh/sb-demo/dictionaries/cpt`
> Request

```json
{
    "records": [
        {
            "values": {
                "value": "4444"
            }
        }
    ]
}
```

> Response

```json
{
    "dictionaryName": "cpt",
    "lastUpdatedAt": "2021-06-15T10:59:43.568Z",
    "records": [
        {
            "id": "e5df4668-18c0-4551-8021-3e0168ffbbb4",
            "createdAt": "2021-06-15T10:59:43.568Z",
            "updatedAt": "2021-06-15T10:59:43.568Z",
            "fullValue": "4444",
            "deleted": false,
            "values": {
                "value": "4444"
            }
        }
    ]
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| dictionaryName | path | Name of dictionary | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Created |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Remove all values from dictionary and set new. Records will be deleted completely

### HTTP Request
***PUT*** `/{tenantName}/{instanceName}/dictionaries/{dictionaryName}`

in our example it would be:

***PUT*** `https://api.live.welkincloud.io/gh/sb-demo/dictionaries/cpt`
> Request

```json
{
    "records": [
        {
            "values": {
                "value": "6666"
            }
        },
        {
            "values": {
                "value": "7777"
            }
        }
    ]
}
```

> Response

```json
{
    "dictionaryName": "cpt",
    "lastUpdatedAt": "2021-06-15T11:22:16.546Z",
    "records": [
        {
            "id": "7599f47b-4a66-439a-9bf6-c51877900a41",
            "createdAt": "2021-06-15T11:22:16.543Z",
            "updatedAt": "2021-06-15T11:22:16.543Z",
            "fullValue": "6666",
            "deleted": false,
            "values": {
                "value": "6666"
            }
        },
        {
            "id": "0de7e286-4c57-49b2-8ace-b064fc9a6c3e",
            "createdAt": "2021-06-15T11:22:16.546Z",
            "updatedAt": "2021-06-15T11:22:16.546Z",
            "fullValue": "7777",
            "deleted": false,
            "values": {
                "value": "7777"
            }
        }
    ]
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| dictionaryName | path | Name of dictionary | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Created |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Update dictionary record by name and id

### HTTP Request
***PUT*** `/{tenantName}/{instanceName}/dictionaries/{dictionaryName}/{dictionaryRecordId}`

in our example it would be:

***PUT*** `https://api.live.welkincloud.io/gh/sb-demo/dictionaries/cpt/001806e2-3464-40b2-8adb-e756abe31fb1`
> Request

```json
{
    "values": {
        "value": "4445"
    }
}
```

> Response

```json
{
    "id": "001806e2-3464-40b2-8adb-e756abe31fb1",
    "createdAt": "2021-04-09T09:24:44.566Z",
    "updatedAt": "2021-06-15T11:18:31.233Z",
    "fullValue": "4445",
    "deleted": false,
    "values": {
        "value": "4445"
    }
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| dictionaryName | path | Name of dictionary | Yes | string |
| dictionaryRecordId | path | Record ID | Yes | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Delete dictionary record by name and id

### HTTP Request
***DELETE*** `/{tenantName}/{instanceName}/dictionaries/{dictionaryName}/{dictionaryRecordId}`

in our example it would be:

***DELETE*** `https://api.live.welkincloud.io/gh/sb-demo/dictionaries/cpt/001806e2-3464-40b2-8adb-e756abe31fb1`

> Response

```json
{
    "id": "001806e2-3464-40b2-8adb-e756abe31fb1",
    "createdAt": "2021-04-09T09:24:44.566Z",
    "updatedAt": "2021-06-15T11:19:48.993Z",
    "fullValue": "4445",
    "deleted": true,
    "values": {
        "value": "4445"
    }
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| dictionaryName | path | Name of dictionary | Yes | string |
| dictionaryRecordId | path | Record ID | Yes | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

## Dictionary formation

### Description
Get all dictionary formations

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/formations/{version}/dictionaries`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/formations/current/dictionaries`

> Response

```json
[
    {
        "name": "cpt",
        "title": "CPT",
        "internal": false,
        "fields": [
            {
                "name": "value",
                "type": "text"
            }
        ]
    },
    {
        "name": "icd-10",
        "title": "ICD-10",
        "internal": false,
        "fields": [
            {
                "name": "value",
                "type": "text"
            }
        ]
    },
    {
        "name": "timezone",
        "title": "Timezone",
        "internal": true,
        "fields": [
            {
                "name": "timezone",
                "type": "text"
            }
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
Get dictionary formation by name

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/formations/{version}/dictionaries/{dictionaryName}`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/formations/current/dictionaries/timezone`

> Response

```json
{
    "name": "timezone",
    "title": "Timezone",
    "internal": true,
    "fields": [
        {
            "name": "timezone",
            "type": "text"
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
| version | path | Version of formation | Yes | string |
| dictionaryName | path | Name of dictionary | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Create new dictionary formation

### HTTP Request
***POST*** `/{tenantName}/{instanceName}/formations/draft/dictionaries`

in our example it would be:

***POST*** `https://api.live.welkincloud.io/gh/sb-demo/formations/draft/dictionaries`

> Request

```json
{
    "name": "alphabet",
    "title": "Alphabet",
    "fields": [
        {
            "name": "lowercase-character",
            "type": "text"
        },
        {
            "name": "uppercase-character",
            "type": "text"
        }
    ]
}
```

> Response

```json
{
    "name": "alphabet",
    "title": "Alphabet",
    "internal": false,
    "fields": [
        {
            "name": "lowercase-character",
            "type": "text"
        },
        {
            "name": "uppercase-character",
            "type": "text"
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

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Created |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Update dictionary formation by name

### HTTP Request
***PUT*** `/{tenantName}/{instanceName}/formations/draft/dictionaries/{dictionaryName}`

in our example it would be:

***PUT*** `https://api.live.welkincloud.io/gh/sb-demo/formations/draft/dictionaries/alphabet

> Request

```json
{
    "name": "alphabet",
    "title": "Alphabet",
    "fields": [
        {
            "name": "character",
            "type": "text"
        }
    ]
}
```

> Response

```json
{
    "name": "alphabet",
    "title": "Alphabet",
    "internal": false,
    "fields": [
        {
            "name": "character",
            "type": "text"
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
| dictionaryName | path | Name of dictionary | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

### Description
Delete dictionary formation by name

### HTTP Request
***DELETE*** `/{tenantName}/{instanceName}/formations/draft/dictionaries/{dictionaryName}`

in our example it would be:

***DELETE*** `https://api.live.welkincloud.io/gh/sb-demo/formations/draft/dictionaries/alphabet

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| dictionaryName | path | Name of dictionary | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
