# Users - Policies and Roles

This API allows to configure users policies and roles.

## Get user policies and roles

> Request

```python
import requests

url = "https://api.live.welkincloud.io/gh/admin/user-permissions/{}".format(user_id)

payload={}
headers = {
    "Authorization": "Bearer {}".format(token)
}

response = requests.request("GET", url, headers=headers, data=payload)
```

>Response

```json
{
  "id": "16c2c714-2b1b-447a-a612-4249bf832035",
  "createdAt": "2020-12-07T10:02:12.234Z",
  "updatedAt": "2021-05-06T06:26:55.656Z",
  "userId": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
  "permissions": [
    {
      "permissionName": "caregiver",
      "instanceName": "stage",
      "type": "SECURITY_ROLE",
      "primaryRole": true
    },
    {
      "permissionName": "cdt_management",
      "instanceName": "stage",
      "type": "SECURITY_POLICY",
      "effectiveDate": "2021-12-01T00:00:00.000Z"
    },
    {
      "permissionName": "assessments_management",
      "instanceName": "stage",
      "type": "SECURITY_POLICY",
      "effectiveDate": "2021-12-01T00:00:00.000Z"
    },
    {
      "permissionName": "assessments_management",
      "instanceName": "live",
      "type": "SECURITY_POLICY",
      "effectiveDate": "2021-12-01T00:00:00.000Z"
    }
  ]
}
```

### HTTP Request
**Method**: ***GET***

**Endpoint**: `{{url}}/{{tenantName}}/admin/user-permissions/{{userId}}`

in our example it would be:
`https://api.live.welkincloud.io/gh/admin/user-permissions/20eb246e-8099-4c7c-854c-5e0f9a366ddb`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| tenantName | path | Name of tenant | Yes | string |
| userId | path | User identifier | Yes | UUID |


**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

## Create/Update policies and roles

> Note 1: PUT request works like Create or Update, 
> so there is no need to create user permissions with POST request

> Note 2: Both (policies and roles)
> should be created in designer before you can assign it for user.

> Request

```python
import requests

url = "https://api.live.welkincloud.io/gh/admin/user-permissions/{}".format(user_id)

payload = {
    "id": "16c2c714-2b1b-447a-a612-4249bf832035",
    "createdAt": "2020-12-07T10:02:12.234Z",
    "updatedAt": "2021-05-06T06:26:55.656Z",
    "userId": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
    "permissions": [
        {
            "permissionName": "caregiver",
            "instanceName": "stage",
            "type": "SECURITY_ROLE",
            "primaryRole": False
        },
        {
            "permissionName": "manager",
            "instanceName": "stage",
            "type": "SECURITY_ROLE",
            "primaryRole": True
        },
        {
            "permissionName": "cdt_management",
            "instanceName": "stage",
            "type": "SECURITY_POLICY",
            "effectiveDate": "2021-12-01T00:00:00.000Z"
        },
        {
            "permissionName": "manager",
            "instanceName": "live",
            "type": "SECURITY_ROLE",
            "primaryRole": True
        }
    ]
}
headers = {
    "Authorization": "Bearer {}".format(token)
}

response = requests.request("PUT", url, headers=headers, data=payload)
```

>Response

```json
{
  "id": "16c2c714-2b1b-447a-a612-4249bf832035",
  "createdAt": "2020-12-07T10:02:12.234Z",
  "updatedAt": "2021-05-06T06:26:55.656Z",
  "userId": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
  "permissions": [
    {
      "permissionName": "caregiver",
      "instanceName": "stage",
      "type": "SECURITY_ROLE",
      "primaryRole": false
    },
    {
      "permissionName": "manager",
      "instanceName": "stage",
      "type": "SECURITY_ROLE",
      "primaryRole": true
    },
    {
      "permissionName": "cdt_management",
      "instanceName": "stage",
      "type": "SECURITY_POLICY",
      "effectiveDate": "2021-12-01T00:00:00.000Z"
    },
    {
      "permissionName": "manager",
      "instanceName": "live",
      "type": "SECURITY_ROLE",
      "primaryRole": true
    }
  ]
}
```

### Example overview
For user with id `20eb246e-8099-4c7c-854c-5e0f9a366ddb` added permissions 
for `stage` and `live` instances.
For `stage` user has 2 available roles: `manager` (primary) and `caregiver`, and temporary policy `cdt_management`, it will be expired `Dec 01 2021`.
For `live` user has one role - `manager` (primary by default).

### HTTP Request
**Method**: ***PUT***

**Endpoint**: `{{url}}/{{tenantName}}/admin/user-permissions/{{userId}}`

in our example it would be:
`https://api.live.welkincloud.io/gh/admin/user-permissions/20eb246e-8099-4c7c-854c-5e0f9a366ddb`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| tenantName | path | Name of tenant | Yes | string |
| userId | path | User identifier | Yes | UUID |
| permissionName | body | name of policy or role | Yes | string |
| instanceName | body | name of instance | Yes | string |
| type | body | Policy or Role | Yes | `SECURITY_POLICY`, `SECURITY_ROLE` |


**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |