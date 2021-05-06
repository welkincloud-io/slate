# Users - App Access

This API allows to configure users access to designer, care portal and parts of admin portal

## Get application access

> Request

```python
import requests

url = "https://api.live.welkincloud.io/gh/admin/application-accesses/{}".format(user_id)

payload={}
headers = {
    "Authorization": "Bearer {}".format(token)
}

response = requests.request("GET", url, headers=headers, data=payload)
```

>Response

```json
{
  "id": "daa7948d-c52c-4129-b64b-848ecc7a5c93",
  "userId": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
  "adminAccessEnabled": true,
  "auditSecurityAccessEnabled": true,
  "instanceAccesses": [
    {
      "instanceId": "62378f09-e1e5-4fc6-a095-5fdb84f8b36b",
      "instanceName": "stage",
      "instanceDescription": "",
      "workshopAccessEnabled": true,
      "auditDataAccessEnabled": false
    },
    {
      "instanceId": "51f7d7cd-f1ba-426f-971a-4305d7d6abe2",
      "instanceName": "live",
      "instanceDescription": "",
      "workshopAccessEnabled": true,
      "auditDataAccessEnabled": false
    }
  ]
}
```

### HTTP Request
**Method**: ***GET***

**Endpoint**: `{{url}}/{{tenantName}}/admin/application-accesses/{{userId}}`

in our example it would be:
`https://api.live.welkincloud.io/gh/admin/application-accesses/20eb246e-8099-4c7c-854c-5e0f9a366ddb`

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

## Create/Update application access

> Request

```python
import requests

url = "https://api.live.welkincloud.io/gh/admin/application-accesses/{}".format(user_id)

payload = {
    "userId": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
    "adminAccessEnabled": True,
    "auditSecurityAccessEnabled": True,
    "instanceAccesses": [
        {
            "instanceId": "62378f09-e1e5-4fc6-a095-5fdb84f8b36b",
            "instanceName": "stage",
            "instanceDescription": "",
            "workshopAccessEnabled": True,
            "auditDataAccessEnabled": True
        },
        {
            "instanceId": "51f7d7cd-f1ba-426f-971a-4305d7d6abe2",
            "instanceName": "live",
            "instanceDescription": "",
            "workshopAccessEnabled": False,
            "auditDataAccessEnabled": False
        }
    ]
}
headers = {
    "Authorization": "Bearer {}".format(token)
}

response = requests.request("PUT", url, headers=headers, data=payload)
```
>Note: PUT request works like Create or Update,
so there is no need to create app-access with POST request

>Response

```json
{
  "id": "04ea5d75-bbe1-4bd0-ba3d-5d6a449c91f7",
  "userId": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
  "adminAccessEnabled": true,
  "auditSecurityAccessEnabled": true,
  "instanceAccesses": [
    {
      "instanceId": "62378f09-e1e5-4fc6-a095-5fdb84f8b36b",
      "instanceName": "stage",
      "instanceDescription": "",
      "workshopAccessEnabled": true,
      "auditDataAccessEnabled": true
    },
    {
      "instanceId": "51f7d7cd-f1ba-426f-971a-4305d7d6abe2",
      "instanceName": "live",
      "instanceDescription": "",
      "workshopAccessEnabled": false,
      "auditDataAccessEnabled": false
    }
  ]
}
```

### Example overview
Allowed access to admin portal, security audit and two instances: `stage` and `live`. 
For `stage` also allowed access to designer and data audit, but not for `live`.

### HTTP Request
**Method**: ***PUT***

**Endpoint**: `{{url}}/{{tenantName}}/admin/application-accesses/{{userId}}`

in our example it would be:
`https://api.live.welkincloud.io/gh/admin/application-accesses/20eb246e-8099-4c7c-854c-5e0f9a366ddb`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| tenantName | path | Name of tenant | Yes | string |
| userId | path | User identifier | Yes | UUID |
| adminAccessEnabled | body | Allow access to admin portal | Yes | boolean |
| auditSecurityAccessEnabled | body | Allow access to security audit in admin portal | Yes | boolean |
| instanceAccesses | body | Allow access to instances | Yes | list of objects |
| instanceAccesses.instanceName | body | Allow access to care-portal of instance by name | Yes | string |
| instanceAccesses.workshopAccessEnabled | body | Allow access to designer-portal of instance | Yes | boolean |
| instanceAccesses.auditDataAccessEnabled | body | Allow access to audit in admin | Yes | boolean |


**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |