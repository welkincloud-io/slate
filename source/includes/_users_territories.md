# Users - Regions and Territories

This API allows to configure users regions and territories.

## Get user terrtories by user id

> Request

```python
import requests

url = "https://api.live.welkincloud.io/gh/admin/user-territories/{}".format(user_id)

payload={}
headers = {
    "Authorization": "Bearer {}".format(token)
}

response = requests.request("GET", url, headers=headers, data=payload)
```

>Response

```json
{
  "id": "88a2f19c-adac-4171-87af-405aec1dea69",
  "createdAt": "2021-01-19T10:46:00.832Z",
  "updatedAt": "2021-05-04T05:53:13.150Z",
  "createdBy": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
  "updatedBy": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
  "userId": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
  "territories": [
    {
      "instanceName": "live",
      "name": "california",
      "territories": [
        "los-angeles"
      ]
    },
    {
      "instanceName": "stage",
      "name": "washington",
      "territories": [
        "seattle",
        "tacoma"
      ]
    }
  ]
}

```

### HTTP Request
**Method**: ***GET***

**Endpoint**: `{{url}}/{{tenantName}}/admin/user-territories/{{userId}}`

in our example it would be:
`https://api.live.welkincloud.io/gh/admin/user-territories/20eb246e-8099-4c7c-854c-5e0f9a366ddb`

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

## Create/Update user territories

> Note 1: PUT request works like Create or Update,
> so there is no need to create app-access with POST request

> Note 2: Regions and territories should be created in designer before 
> you can assign it for user.

> Request

```python
import requests

url = "https://api.live.welkincloud.io/gh/admin/user-territories/{}".format(user_id)

payload = {
    "territories": [
        {
            "name": "washington",
            "territories": [
                "seattle",
                "tacoma"
            ],
            "instanceName": "live"
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
  "id": "88a2f19c-adac-4171-87af-405aec1dea69",
  "createdAt": "2021-01-19T10:46:00.832Z",
  "updatedAt": "2021-05-04T05:53:13.150Z",
  "createdBy": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
  "updatedBy": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
  "userId": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
  "territories": [
    {
      "instanceName": "live",
      "name": "washington",
      "territories": [
        "seattle",
        "tacoma"
      ]
    }
  ]
}
```

### Example overview
Assigned region `washington` with territories `seattle`, `tacoma` 
for user `20eb246e-8099-4c7c-854c-5e0f9a366ddb`.

### HTTP Request
**Method**: ***PUT***

**Endpoint**: `{{url}}/{{tenantName}}/admin/user-territories/{{userId}}`

in our example it would be:
`https://api.live.welkincloud.io/gh/admin/user-territories/20eb246e-8099-4c7c-854c-5e0f9a366ddb`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| tenantName | path | Name of tenant | Yes | string |
| userId | path | User identifier | Yes | UUID |
| territories.name | body | Region name | Yes | string |
| territories.territories | body | Territory names | Yes | [string] |
| territories.instanceName | body | Instance name | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |