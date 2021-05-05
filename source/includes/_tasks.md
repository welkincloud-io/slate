# Tasks

APIs for working with tasks care plan: overview and goals

The collection supports several interactions

1. Allows to obtain a list of tasks (can be sorted and filtered).
3. Allows to create a new tasks.
3. Allows to update an existing task by ID.
4. Allows to subscribe / unsubscribe to task notifications.
5. Allows to add a comment to task.


## Create new task

> Request

```python
import requests

url = "https://api.live.welkincloud.io/gh/sb-demo/tasks"

payload={
    "name": "Review patient",
    "description": "Review new patient profile",
    "dueDate": "2021-05-20T00:00:00.000Z",
    "status": "TODO",
    "priority": "URGENT",
    "assignee": {
        "id": "20eb246e-8099-4c7c-854c-5e0f9a366ddb"
    },
    "watchers": [{
        "id": "20eb246e-8099-4c7c-854c-5e0f9a366ddb"
    }],
    "patient": {
        "id": "d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1"
    },
    "comments": [{
        "text": "Lorem ipsum..."
    }]
}
headers = {
    "Authorization": "Bearer {}".format(token)
}

response = requests.request("POST", url, headers=headers, data=payload)
```

>Response

```json
{
  "id": "28b38060-db66-4183-bcaa-34751308573a",
  "createdAt": "2021-05-05T07:24:09.101Z",
  "updatedAt": "2021-05-05T07:24:09.101Z",
  "name": "Review patient",
  "description": "Review new patient profile",
  "dueDate": "2021-05-20T00:00:00.000Z",
  "status": "TODO",
  "priority": "URGENT",
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
      "id": "94852cc2-ecbc-4fa1-8641-a8f2252b9ffb",
      "createdAt": "2021-05-05T07:24:09.133Z",
      "author": {
        "id": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
        "name": "Jane Dou"
      },
      "text": "Lorem ipsum..."
    }
  ]
}
```

### Example overview
A new task is created with the name `Patient Review` 
with the description `New Patient Profile Review` 
and the priority `URGENT` 
and comment `Lorem ipsum...`.
The task assigned to user with id `20eb246e-8099-4c7c-854c-5e0f9a366ddb`.
The task visible for users specified in the fields `author`, `assignee`, `watchers` 
(in our example, this is the same user).
The task must be completed by `May 20, 2021`.

### HTTP Request
**Method**: ***POST***

**Endpoint**: `{url}/{tenantName}/{instanceName}/tasks`

in our example it would be:
`https://api.live.welkincloud.io/gh/sb-demo/tasks`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| name | body | Short name of the task | Yes | string |
| description | body | Detailed text description of the task| No | string |
| priority | body | task priority | Yes | `LOW`, `MEDIUM`, `HIGH`, `URGENT` |
| status | body | task status | Yes | `TODO`, `IN_PROGRESS`, `COMPLETED`, `CANCELED` |
| dueDate | body | deadline for the task | No |Datetime in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format  |
| assignee | body | user responsible for the task | Yes | `{"id": ""}`  |
| patient | body | task-related patient | No | `{"id": ""}` |
| watchers | body | users subscribed to task notifications | No | [`{"id": ""}`] |
| comments | body | simple text comments to task | No | [`{"text": ""}`] |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Created |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

## Update task

> Request

```python
import requests

url = "https://api.live.welkincloud.io/gh/sb-demo/tasks/{}".format(task_id)

payload = {
    "name": "New name",
    "description": "Review new patient profile",
    "dueDate": "2021-07-20T00:00:00.000Z",
    "priority": "MEDIUM",
    "status": "IN_PROGRESS",
    "assignee": {
        "id": "03a87f5b-3a04-4be8-b0ad-7a34a5b2892d"
    },
    "patient": {
        "id": "d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1"
    }
}

headers = {
    "Authorization": "Bearer {}".format(token)
}

response = requests.request("PATCH", url, headers=headers, data=payload)
```

>Response

```json
{
  "id": "28b38060-db66-4183-bcaa-34751308573a",
  "createdAt": "2021-05-05T07:24:09.101Z",
  "updatedAt": "2021-05-05T07:24:09.101Z",
  "name": "New name",
  "description": "Review new patient profile",
  "dueDate": "2021-07-20T00:00:00.000Z",
  "status": "IN_PROGRESS",
  "priority": "MEDIUM",
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
      "id": "94852cc2-ecbc-4fa1-8641-a8f2252b9ffb",
      "createdAt": "2021-05-05T07:24:09.133Z",
      "author": {
        "id": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
        "name": "Jane Dou"
      },
      "text": "Lorem ipsum..."
    }
  ]
}
```

### Example overview
Updated `name`, `dueDate`, `status`, `priority` fields

### HTTP Request
**Method**: ***PATCH***

**Endpoint**: `{url}/{tenantName}/{instanceName}/tasks/{taskId}`

in our example it would be:
`https://api.live.welkincloud.io/gh/sb-demo/tasks/28b38060-db66-4183-bcaa-34751308573a `

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| taskId | path | Task identifier | Yes | UUID |
| name | body | Short name of the task | Yes | string |
| description | body | Detailed text description of the task| No | string |
| priority | body | task priority | Yes | `LOW`, `MEDIUM`, `HIGH`, `URGENT` |
| status | body | task status | Yes | `TODO`, `IN_PROGRESS`, `COMPLETED`, `CANCELED` |
| dueDate | body | deadline for the task | No |Datetime in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format  |
| assignee | body | user responsible for the task | Yes | `{"id": ""}`  |
| patient | body | task-related patient | No | `{"id": ""}` |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

## Batch update of tasks status

> Request

```python
import requests

url = "https://api.live.welkincloud.io/gh/sb-demo/tasks"

payload = {
    "taskIds": [
        "28b38060-db66-4183-bcaa-34751308573a"
    ],
    "status": "COMPLETED"
}

headers = {
    "Authorization": "Bearer {}".format(token)
}

response = requests.request("PATCH", url, headers=headers, data=payload)
```

>Response

```json
[
  {
    "id": "28b38060-db66-4183-bcaa-34751308573a",
    "createdAt": "2021-05-05T07:24:09.101Z",
    "updatedAt": "2021-05-05T08:47:42.891Z",
    "name": "Updated task",
    "description": "Create new patient profile",
    "dueDate": "2021-12-01T12:16:38.514Z",
    "status": "COMPLETED",
    "priority": "URGENT",
    "patient": {
      "id": "d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1",
      "name": "John Dou"
    },
    "assignee": {
      "id": "03a87f5b-3a04-4be8-b0ad-7a34a5b2892d",
      "name": "John Dou"
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
        "id": "94852cc2-ecbc-4fa1-8641-a8f2252b9ffb",
        "createdAt": "2021-05-05T07:24:09.133Z",
        "author": {
          "id": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
          "name": "Jane Dou"
        },
        "text": "some comment"
      }
    ]
  }
]
```

### Example overview
Update tasks status for list of tasks (only one task in example).
Method returns a list of updated tasks.

### HTTP Request
**Method**: ***PATCH***

**Endpoint**: `{url}/{tenantName}/{instanceName}/tasks`

in our example it would be:
`https://api.live.welkincloud.io/gh/sb-demo/tasks/28b38060-db66-4183-bcaa-34751308573a`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| taskIds | body | Task identifiers | Yes | [`UUID`] |
| status | body | task status | Yes | `TODO`, `IN_PROGRESS`, `COMPLETED`, `CANCELED` |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

## Get task by ID

> Request

```python
import requests

url = "https://api.live.welkincloud.io/gh/sb-demo/tasks/{}".format(task_id)

payload = {}

headers = {
    "Authorization": "Bearer {}".format(token)
}

response = requests.request("GET", url, headers=headers, data=payload)
```

>Response

```json
{
  "id": "28b38060-db66-4183-bcaa-34751308573a",
  "createdAt": "2021-05-05T07:24:09.101Z",
  "updatedAt": "2021-05-05T07:24:09.101Z",
  "name": "New name",
  "description": "Review new patient profile",
  "dueDate": "2021-07-20T00:00:00.000Z",
  "status": "IN_PROGRESS",
  "priority": "MEDIUM",
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
      "id": "94852cc2-ecbc-4fa1-8641-a8f2252b9ffb",
      "createdAt": "2021-05-05T07:24:09.133Z",
      "author": {
        "id": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
        "name": "Jane Dou"
      },
      "text": "Lorem ipsum..."
    }
  ]
}
```

### Example overview
Get complete information about one task by ID

### HTTP Request
**Method**: ***GET***

**Endpoint**: `{url}/{tenantName}/{instanceName}/tasks/{taskId}`

in our example it would be:
`https://api.live.welkincloud.io/gh/sb-demo/tasks/28b38060-db66-4183-bcaa-34751308573a`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| taskId | path | Task identifier | Yes | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

## Search tasks

> Request

```python
import requests

url = "https://api.live.welkincloud.io/gh/sb-demo/tasks?assigneeId={}".format(userId)

payload = {}

headers = {
    "Authorization": "Bearer {}".format(token)
}

response = requests.request("GET", url, headers=headers, data=payload)
```

>Response

```json
{
  "data": [
    {
      "id": "26f2bb83-d569-44ea-a76e-99513422cdd8",
      "createdAt": "2021-05-05T07:23:19.334Z",
      "updatedAt": "2021-05-05T07:23:19.334Z",
      "name": "New task",
      "description": "Create new patient profile",
      "dueDate": "2021-12-01T12:16:38.514Z",
      "status": "TODO",
      "priority": "URGENT",
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
      "watchers": [],
      "comments": []
    },
    {
      "id": "28b38060-db66-4183-bcaa-34751308573a",
      "createdAt": "2021-05-05T07:24:09.101Z",
      "updatedAt": "2021-05-05T08:47:42.891Z",
      "name": "Updated task",
      "description": "Create new patient profile",
      "dueDate": "2021-12-01T12:16:38.514Z",
      "status": "COMPLETED",
      "priority": "URGENT",
      "patient": {
        "id": "d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1",
        "name": "John Dou"
      },
      "assignee": {
        "id": "03a87f5b-3a04-4be8-b0ad-7a34a5b2892d",
        "name": "John Dou"
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
          "id": "94852cc2-ecbc-4fa1-8641-a8f2252b9ffb",
          "createdAt": "2021-05-05T07:24:09.133Z",
          "author": {
            "id": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
            "name": "Jane Dou"
          },
          "text": "some comment"
        }
      ]
    }
  ],
  "metaInfo": {
    "page": 0,
    "pageSize": 20,
    "totalElements": 2,
    "numberOfElements": 2,
    "totalPages": 1,
    "firstPage": true,
    "lastPage": true
  }
}
```

### Example overview
Search tasks by many parameters

### HTTP Request
**Method**: ***GET***

**Endpoint**: `{url}/{tenantName}/{instanceName}/tasks`

in our example it would be:
`https://api.live.welkincloud.io/gh/sb-demo/tasks`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| assigneeId | path | looks for tasks created for user | No | UUID |
| patientId | path | looks for tasks related to patient | No | UUID |
| watcherId | path | looks for tasks monitored by the specified user | No | UUID |
| authorId | path | looks for tasks created by user | No | UUID |
| status | path | looks for tasks with status | No | [`TODO`, `IN_PROGRESS`, `COMPLETED`, `CANCELED`]  - one or more comma separated |
| priority | path | looks for tasks with priority | No | [`LOW`, `MEDIUM`, `HIGH`, `URGENT`] - one or more comma separated |
| dueDate | path | looks for tasks whose deadline is on the specified day | No | Datetime in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format  |
| dueBefore | path | looks for  tasks whose deadline is up to the specified day| No | Datetime in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format  |
| description | path | looks for tasks whose descriptions partially matches the specified one | No | string |
| search | path | search by name or description | No | string |
| relatedUserId | path | search by assignee or watcher | No | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

## Add watcher to task

> Request

```python
import requests

url = "https://api.live.welkincloud.io/gh/sb-demo/tasks/{}/watchers".format(task_id)

payload = {
    "id": "20745195-bf3d-46af-9e74-db60c19b7e7b"
}

headers = {
    "Authorization": "Bearer {}".format(token)
}

response = requests.request("PATCH", url, headers=headers, data=payload)
```

>Response

```json

{
  "id": "28b38060-db66-4183-bcaa-34751308573a",
  "createdAt": "2021-05-05T07:24:09.101Z",
  "updatedAt": "2021-05-05T08:47:42.891Z",
  "name": "Updated task",
  "description": "Create new patient profile",
  "dueDate": "2021-12-01T12:16:38.514Z",
  "status": "COMPLETED",
  "priority": "URGENT",
  "patient": {
    "id": "d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1",
    "name": "John Dou"
  },
  "assignee": {
    "id": "03a87f5b-3a04-4be8-b0ad-7a34a5b2892d",
    "name": "John Dou"
  },
  "author": {
    "id": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
    "name": "Jane Dou"
  },
  "watchers": [
    {
      "id": "20745195-bf3d-46af-9e74-db60c19b7e7b",
      "name": "James Dou"
    }
  ]
}
```

### Example overview
The method allows you to subscribe the specified user to task update notifications.
Method returns task with new watchers.

### HTTP Request
**Method**: ***PATCH***

**Endpoint**: `{url}/{tenantName}/{instanceName}/tasks/{taskId}/watchers`

in our example it would be:
`https://api.live.welkincloud.io/gh/sb-demo/tasks/28b38060-db66-4183-bcaa-34751308573a/watchers`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| taskId | path | Task identifier | Yes | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

## Remove watcher from task

> Request

```python
import requests

url = "https://api.live.welkincloud.io/gh/sb-demo/tasks/{}/watchers/{}".format(task_id, watcher_id)

payload = {}

headers = {
    "Authorization": "Bearer {}".format(token)
}

response = requests.request("DELETE", url, headers=headers, data=payload)
```

>Response

```json
{
  "id": "28b38060-db66-4183-bcaa-34751308573a",
  "createdAt": "2021-05-05T07:24:09.101Z",
  "updatedAt": "2021-05-05T08:47:42.891Z",
  "name": "Updated task",
  "description": "Create new patient profile",
  "dueDate": "2021-12-01T12:16:38.514Z",
  "status": "COMPLETED",
  "priority": "URGENT",
  "patient": {
    "id": "d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1",
    "name": "John Dou"
  },
  "assignee": {
    "id": "03a87f5b-3a04-4be8-b0ad-7a34a5b2892d",
    "name": "John Dou"
  },
  "author": {
    "id": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
    "name": "Jane Dou"
  },
  "watchers": []
}
```

### Example overview
The method allows you to unsubscribe the specified user from task.
Method returns task without removed watchers.

### HTTP Request
**Method**: ***DELETE***

**Endpoint**: `{url}/{tenantName}/{instanceName}/tasks/{taskId}/watchers/{watcherId}`

in our example it would be:
`https://api.live.welkincloud.io/gh/sb-demo/tasks/28b38060-db66-4183-bcaa-34751308573a/watchers/20745195-bf3d-46af-9e74-db60c19b7e7b`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| taskId | path | Task identifier | Yes | UUID |
| watcherId | path | Watcher identifier | Yes | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

## Add comment to task

> Request

```python
import requests

url = "https://api.live.welkincloud.io/gh/sb-demo/tasks/{}/comments".format(task_id)

payload = {
    "text": "Lorem ipsum..."
}

headers = {
    "Authorization": "Bearer {}".format(token)
}

response = requests.request("PATCH", url, headers=headers, data=payload)
```

>Response

```json
{
  "id": "28b38060-db66-4183-bcaa-34751308573a",
  "createdAt": "2021-05-05T07:24:09.101Z",
  "updatedAt": "2021-05-05T09:45:46.767Z",
  "name": "Updated task",
  "description": "Create new patient profile",
  "dueDate": "2021-12-01T12:16:38.514Z",
  "status": "COMPLETED",
  "priority": "URGENT",
  "patient": {
    "id": "d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1",
    "name": "John Dou"
  },
  "assignee": {
    "id": "03a87f5b-3a04-4be8-b0ad-7a34a5b2892d",
    "name": "Jane Dou"
  },
  "author": {
    "id": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
    "name": "Jane Dou"
  },
  "comments": [
    {
      "id": "728aa031-24d2-420e-ab1c-be0986896c09",
      "createdAt": "2021-05-05T09:51:03.145Z",
      "author": {
        "id": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
        "name": "Jane Dou"
      },
      "text": "Lorem ipsum..."
    }
  ]
}
```

### Example overview
The method allows you to add comments to the task.
Method returns task with new comment.

### HTTP Request
**Method**: ***PATCH***

**Endpoint**: `{url}/{tenantName}/{instanceName}/tasks/{taskId}/comments`

in our example it would be:
`https://api.live.welkincloud.io/gh/sb-demo/tasks/28b38060-db66-4183-bcaa-34751308573a/comments`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| taskId | path | Task identifier | Yes | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

## Remove comment from task

> Request

```python
import requests

url = "https://api.live.welkincloud.io/gh/sb-demo/tasks/{}/comments/{}".format(task_id, comment_id)

payload = {}

headers = {
    "Authorization": "Bearer {}".format(token)
}

response = requests.request("DELETE", url, headers=headers, data=payload)
```

>Response

```json
[
  {
    "id": "28b38060-db66-4183-bcaa-34751308573a",
    "createdAt": "2021-05-05T07:24:09.101Z",
    "updatedAt": "2021-05-05T08:47:42.891Z",
    "name": "Updated task",
    "description": "Create new patient profile",
    "dueDate": "2021-12-01T12:16:38.514Z",
    "status": "COMPLETED",
    "priority": "URGENT",
    "patient": {
      "id": "d6ea79ce-d3d6-4c2d-a27e-e4d1207f60f1",
      "name": "John Dou"
    },
    "assignee": {
      "id": "03a87f5b-3a04-4be8-b0ad-7a34a5b2892d",
      "name": "Jane Dou"
    },
    "author": {
      "id": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
      "name": "Jane Dou"
    },
    "comments": []
  }
]
```

### Example overview
The method allows you to remove unnecessary comments.
Method returns task without removed watchers.

### HTTP Request
**Method**: ***DELETE***

**Endpoint**: `{url}/{tenantName}/{instanceName}/tasks/{taskId}/comments/{commentId}`

in our example it would be:
`https://api.live.welkincloud.io/gh/sb-demo/tasks/28b38060-db66-4183-bcaa-34751308573a/comments/20745195-bf3d-46af-9e74-db60c19b7e7b`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |
| taskId | path | Task identifier | Yes | UUID |
| commentId | path | Comment identifier | Yes | UUID |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
