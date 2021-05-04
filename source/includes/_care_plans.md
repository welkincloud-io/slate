# Care plans

APIs for working with patient care plan: overview and goals

## Get care plan by patientId

> Request

```python
import requests

url = "https://api.live.welkincloud.io/gh/sb-demo/patients/{}/care-plan"
    .format(patientId)

payload={}
headers = {
    "Authorization": "Bearer {}".format(token)
}

response = requests.request("GET", url, headers=headers, data=payload)
```

>Response

```json
{
  "id": "c5b5a589-257f-482d-b6a6-907a6c45cd00",
  "createdByName": "John Dou",
  "createdAt": "2021-05-04T05:53:47.211Z",
  "updatedByName": "John Dou",
  "updatedAt": "2021-05-04T07:36:59.435Z",
  "patientOverview": {
    "createdByName": "John Dou",
    "createdAt": "2021-05-04T07:36:39.793Z",
    "updatedByName": "John Dou",
    "updatedAt": "2021-05-04T07:36:59.434Z",
    "overview": "Lorem ipsum dolor sit amet..."
  }
}
```

### Description
Get overview and system fields

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/patients/{patientId}/care-plan`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/care-plan`

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

## Create patient overview

> Request

```python
import requests

url = "https://api.live.welkincloud.io/gh/sb-demo/patients/{}/care-plan/overview"
    .format(patientId)

payload = {
    "overview": "Lorem ipsum dolor sit amet..."
}
headers = {
    "Authorization": "Bearer {}".format(token),
    'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, json=payload)
```

> Response

```json
{
    "createdByName": "John Dou",
    "createdAt": "2021-05-04T07:36:39.793Z",
    "updatedByName": "John Dou",
    "updatedAt": "2021-05-04T07:36:59.434Z",
    "overview": "Lorem ipsum dolor sit amet..."
}
```

### HTTP Request
***POST*** `/{tenantName}/{instanceName}/patients/{patientId}/care-plan/overview`

in our example it would be:

***POST*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/care-plan/overview`

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
| 201 | Created |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |


## Update patient overview

> Request

```python
import requests

url = "https://api.live.welkincloud.io/gh/sb-demo/patients/{}/care-plan/overview"
    .format(patientId)

payload = {
    "overview": "Lorem ipsum dolor sit amet..."
}
headers = {
    "Authorization": "Bearer {}".format(token),
    'Content-Type': 'application/json'
}

response = requests.request("PUT", url, headers=headers, json=payload)
```

> Response

```json
{
    "createdByName": "John Dou",
    "createdAt": "2021-05-04T07:36:39.793Z",
    "updatedByName": "John Dou",
    "updatedAt": "2021-05-04T07:36:59.434Z",
    "overview": "Lorem ipsum dolor sit amet..."
}
```

### Description
Update patient overview

### HTTP Request
***PUT*** `/{tenantName}/{instanceName}/patients/{patientId}/care-plan/overview`

in our example it would be:

***PUT*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/care-plan/overview`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |


## Create Goal

> Request

```python
import requests

url = "https://api.live.welkincloud.io/gh/sb-demo/patients/{}/care-plan/goals"
    .format(patientId)

payload = {
    "goalTemplateName": "example-template-name"
}
headers = {
    "Authorization": "Bearer {}".format(token),
    'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, json=payload)
```

> Response

```json
{
  "id": "57827fdb-d240-46f9-8e6a-a89441cf8718",
  "createdByName": "John Dou",
  "createdAt": "2021-05-04T09:21:31.205Z",
  "updatedByName": "John Dou",
  "updatedAt": "2021-05-04T09:21:31.205Z",
  "name": "Example",
  "type": "Test",
  "priority": "LOW",
  "status": "ACTIVE",
  "templateName": "example-template-name"
}
```

### Description
Create goal for patient by goal-template
> Note: The goal-template must already be created in the designer.

### HTTP Request
***POST*** `/{tenantName}/{instanceName}/patients/{patientId}/care-plan/goals`

in our example it would be:

***POST*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/care-plan/goals`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| dto | body | dto | Yes | json |


**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 201 | Created |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |


## Update Goal

> Request

```python
import requests

url = "https://api.live.welkincloud.io/gh/sb-demo/patients/{}/care-plan/goals/{}"
    .format(patientId, goalId)

payload = {
    "name": "Another goal name",
    "priority": "HIGH",
    "status": "REMOVED"
}
headers = {
    "Authorization": "Bearer {}".format(token),
    'Content-Type': 'application/json'
}

response = requests.request("PATCH", url, headers=headers, json=payload)
```

> Response

```json
{
  "id": "57827fdb-d240-46f9-8e6a-a89441cf8718",
  "createdByName": "John Dou",
  "createdAt": "2021-05-04T09:21:31.205Z",
  "updatedByName": "John Dou",
  "updatedAt": "2021-05-04T09:21:31.205Z",
  "name": "Another goal name",
  "type": "Test",
  "priority": "HIGH",
  "status": "REMOVED",
  "templateName": "example-template-name"
}
```

### Description
Update goal details: name, status, priority.

### HTTP Request
***PATCH*** `/{tenantName}/{instanceName}/patients/{patientId}/care-plan/goals/{goalId}`

in our example it would be:

***PATCH*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/care-plan/goals/57827fdb-d240-46f9-8e6a-a89441cf8718`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| goalId | path | ID of goal | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| dto | body | dto | Yes | json |


**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

## Goal details

> Request

```python
import requests

url = "https://api.live.welkincloud.io/gh/sb-demo/patients/{}/care-plan/goals/{}"
    .format(patientId, goalId)

payload = {}
headers = {
    "Authorization": "Bearer {}".format(token),
    'Content-Type': 'application/json'
}

response = requests.request("GET", url, headers=headers, json=payload)
```

> Response

```json
{
  "details": {
    "id": "57827fdb-d240-46f9-8e6a-a89441cf8718",
    "createdByName": "Jane Dou",
    "createdAt": "2021-05-04T09:21:31.205Z",
    "updatedByName": "Jane Dou",
    "updatedAt": "2021-05-04T09:37:11.206Z",
    "name": "Example",
    "type": "Test",
    "priority": "HIGH",
    "status": "ACTIVE",
    "templateName": "example-template-name"
  },
  "tasks": [
    {
      "id": "ce9e012e-4ae8-4366-9987-bbf5ebdf4a2d",
      "createdAt": "2021-05-04T09:21:31.571Z",
      "updatedAt": "2021-05-04T09:21:31.571Z",
      "name": "task1",
      "description": "",
      "dueDate": "2021-05-05T12:21:31.534Z",
      "status": "TODO",
      "priority": "LOW",
      "patient": {
        "id": "d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1",
        "name": "John Dou"
      },
      "assignee": {
        "id": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
        "name": "Jane Dou"
      },
      "author": {
        "id": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
        "name": "Jane Dou"
      },
      "watchers": [
        {
          "id": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
          "name": "Jane Dou"
        }
      ],
      "comments": [
        {
          "id": "c84992c2-568e-41b0-ab51-903c83e46d81",
          "createdByName": "Jane Dou",
          "createdAt": "2021-05-04T10:01:21.108Z",
          "updatedByName": "Jane Dou",
          "updatedAt": "2021-05-04T10:01:21.108Z",
          "text": "test comment"
        }
      ],
      "goalId": "57827fdb-d240-46f9-8e6a-a89441cf8718",
      "watchersType": "POINT_OF_CONTACT"
    }
  ],
  "comments": []
}
```

### Description
Get extended goal view: details, tasks, comments.

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/patients/{patientId}/care-plan/goals/{goalId}`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/care-plan/goals/57827fdb-d240-46f9-8e6a-a89441cf8718`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| goalId | path | ID of goal | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

## Goals list

> Request

```python
import requests

url = "https://api.live.welkincloud.io/gh/sb-demo/patients/{}/care-plan/goals"
    .format(patientId)

payload = {}
headers = {
    "Authorization": "Bearer {}".format(token),
    'Content-Type': 'application/json'
}

response = requests.request("GET", url, headers=headers, json=payload)
```

> Response

```json
{
  "data": [
    {
      "id": "57827fdb-d240-46f9-8e6a-a89441cf8718",
      "createdByName": "John Dou",
      "createdAt": "2021-05-04T09:21:31.205Z",
      "updatedByName": "John Dou",
      "updatedAt": "2021-05-04T09:37:11.206Z",
      "name": "Example",
      "type": "Test",
      "priority": "HIGH",
      "status": "ACTIVE",
      "templateName": "example-template-name"
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

### Description
Get goals list (can be filtered by status)

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/patients/{patientId}/care-plan/goals`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/care-plan/goals`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| status | query | Goal status | No | ACTIVE,REMOVED,COMPLETED |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| page | query | Page Index | No | integer |
| size | query | Page Size | No | integer |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

## Goal comments list

> Request

```python
import requests

url = "https://api.live.welkincloud.io/gh/sb-demo/patients/{}/care-plan/goals/{goalId}/comments"
    .format(patientId)

payload = {}
headers = {
    "Authorization": "Bearer {}".format(token),
    'Content-Type': 'application/json'
}

response = requests.request("GET", url, headers=headers, json=payload)
```

> Response

```json
[
  {
    "id": "c84992c2-568e-41b0-ab51-903c83e46d81",
    "createdByName": "John Dou",
    "createdAt": "2021-05-04T10:01:21.108Z",
    "updatedByName": "John Dou",
    "updatedAt": "2021-05-04T10:01:21.108Z",
    "text": "test comment"
  }
]
```

### Description
Get list of comments related to goal

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/patients/{patientId}/care-plan/goals/{goalId}/comments`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/care-plan/goals/57827fdb-d240-46f9-8e6a-a89441cf8718/comments`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| goalId | path | ID of goal | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Created |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

## Add Goal comment

> Request

```python
import requests

url = "https://api.live.welkincloud.io/gh/sb-demo/patients/{}/care-plan/goals/{goalId}/comments"
    .format(patientId)

payload = {
    "text": "test comment"
}
headers = {
    "Authorization": "Bearer {}".format(token),
    'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, json=payload)
```

> Response

```json
{
  "id": "c84992c2-568e-41b0-ab51-903c83e46d81",
  "createdByName": "John Dou",
  "createdAt": "2021-05-04T10:01:21.108Z",
  "updatedByName": "John Dou",
  "updatedAt": "2021-05-04T10:01:21.108Z",
  "text": "test comment"
}
```

### Description
Add comment to goal

### HTTP Request
***POST*** `/{tenantName}/{instanceName}/patients/{patientId}/care-plan/goals/{goalId}/comments`

in our example it would be:

***POST*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/care-plan/goals/57827fdb-d240-46f9-8e6a-a89441cf8718/comments`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| goalId | path | ID of goal | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Created |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

## Goal tasks list

> Request

```python
import requests

url = "https://api.live.welkincloud.io/gh/sb-demo/patients/{}/care-plan/goals/{goalId}/tasks"
    .format(patientId)

payload = {}
headers = {
    "Authorization": "Bearer {}".format(token),
    'Content-Type': 'application/json'
}

response = requests.request("GET", url, headers=headers, json=payload)
```

> Response

```json
[
  {
    "id": "c84992c2-568e-41b0-ab51-903c83e46d81",
    "createdByName": "John Dou",
    "createdAt": "2021-05-04T10:01:21.108Z",
    "updatedByName": "John Dou",
    "updatedAt": "2021-05-04T10:01:21.108Z",
    "text": "test comment"
  }
]
```

### Description
Get list of tasks related to goal

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/patients/{patientId}/care-plan/goals/{goalId}/tasks`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/care-plan/goals/57827fdb-d240-46f9-8e6a-a89441cf8718/tasks`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| goalId | path | ID of goal | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Created |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

## Add Goal task

> Request

```python
import requests

url = "https://api.live.welkincloud.io/gh/sb-demo/patients/{}/care-plan/goals/{goalId}/tasks"
    .format(patientId)

payload = {
    "name": "New task",
    "description": "Create new patient profile",
    "dueDate": "2021-12-01T12:16:38.514Z",
    "status": "TODO",
    "priority": "URGENT",
    "assignee": {
        "id": "20eb246e-8099-4c7c-854c-5e0f9a366ddb"
    }
}
headers = {
    "Authorization": "Bearer {}".format(token),
    'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, json=payload)
```

> Response

```json
[
  {
    "id": "c84992c2-568e-41b0-ab51-903c83e46d81",
    "createdByName": "John Dou",
    "createdAt": "2021-05-04T10:01:21.108Z",
    "updatedByName": "John Dou",
    "updatedAt": "2021-05-04T10:01:21.108Z",
    "text": "test comment"
  }
]
```

### Description
Add custom task to goal

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/patients/{patientId}/care-plan/goals/{goalId}/tasks`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/patients/d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1/care-plan/goals/57827fdb-d240-46f9-8e6a-a89441cf8718/tasks`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientId | path | ID of patient | Yes | UUID |
| goalId | path | ID of goal | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Created |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |