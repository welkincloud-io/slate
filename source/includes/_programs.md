# Programs

## Get all programs

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/formations/{version}/programs`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/formations/current/programs`

> Response

```json
[
    {
        "name": "lead-management-program",
        "title": "Lead Management Program",
        "description": "Program for lead management",
        "phases": [
            {
                "name": "start",
                "title": "Start",
                "description": "",
                "navigateTo": [
                    {
                        "name": "intake"
                    }
                ]
            },
            {
                "name": "end",
                "title": "End",
                "description": "",
                "navigateTo": []
            },
            {
                "name": "intake",
                "title": "Intake",
                "description": "Intake Phase",
                "navigateTo": [
                    {
                        "name": "pre-enrollment"
                    }
                ]
            },
            {
                "name": "pre-enrollment",
                "title": "Pre-Enrollment",
                "description": "Before customer signs, but shows interest",
                "navigateTo": [
                    {
                        "name": "documents-sent"
                    }
                ]
            },
            {
                "name": "documents-sent",
                "title": "Documents Sent",
                "description": "When documents are sent for signature",
                "navigateTo": [
                    {
                        "name": "enrolled"
                    }
                ]
            },
            {
                "name": "enrolled",
                "title": "Enrolled",
                "description": "Customer became a patient",
                "navigateTo": [
                    {
                        "name": "end"
                    }
                ]
            }
        ],
        "nodes": [
            {
                "id": "start",
                "data": {
                    "label": "Start"
                },
                "type": "input",
                "position": {
                    "x": 20,
                    "y": 20
                },
                "sourcePosition": "right",
                "targetPosition": "left"
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

## Get program by name

### HTTP Request
***GET*** `/{tenantName}/{instanceName}/formations/{version}/programs/{programName}`

in our example it would be:

***GET*** `https://api.live.welkincloud.io/gh/sb-demo/formations/current/programs/lead-management-program`

> Response

```json
 {
        "name": "lead-management-program",
        "title": "Lead Management Program",
        "description": "Program for lead management",
        "phases": [
            {
                "name": "start",
                "title": "Start",
                "description": "",
                "navigateTo": [
                    {
                        "name": "intake"
                    }
                ]
            },
            {
                "name": "end",
                "title": "End",
                "description": "",
                "navigateTo": []
            },
            {
                "name": "intake",
                "title": "Intake",
                "description": "Intake Phase",
                "navigateTo": [
                    {
                        "name": "pre-enrollment"
                    }
                ]
            },
            {
                "name": "pre-enrollment",
                "title": "Pre-Enrollment",
                "description": "Before customer signs, but shows interest",
                "navigateTo": [
                    {
                        "name": "documents-sent"
                    }
                ]
            },
            {
                "name": "documents-sent",
                "title": "Documents Sent",
                "description": "When documents are sent for signature",
                "navigateTo": [
                    {
                        "name": "enrolled"
                    }
                ]
            },
            {
                "name": "enrolled",
                "title": "Enrolled",
                "description": "Customer became a patient",
                "navigateTo": [
                    {
                        "name": "end"
                    }
                ]
            }
        ],
        "nodes": [
            {
                "id": "start",
                "data": {
                    "label": "Start"
                },
                "type": "input",
                "position": {
                    "x": 20,
                    "y": 20
                },
                "sourcePosition": "right",
                "targetPosition": "left"
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
| version | path | Version of formation | Yes | string |
| programName | path | Name of program | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

## Create a program

### HTTP Request
***POST*** `/{tenantName}/{instanceName}/formations/draft/programs`

in our example it would be:

***POST*** `https://api.live.welkincloud.io/gh/sb-demo/formations/draft/programs`

> Request

```json
{
  "name": "care_program_name_1",
  "title": "care_program_title_1",
  "description": "care_program_description_1",
  "phases": [
    {
      "name": "phase_name_1",
      "title": "phase_title_1",
      "description": "phase_description_1",
      "navigateTo": [
        {
          "name": "phase_name_2"
        }
      ]
    },
    {
      "name": "phase_name_2",
      "title": "phase_title_2",
      "description": "phase_description_2",
      "navigateTo": null
    }
  ]
}
```

> Response

```json
{
    "name": "care_program_name_1",
    "title": "care_program_title_1",
    "description": "care_program_description_1",
    "phases": [
        {
            "name": "phase_name_1",
            "title": "phase_title_1",
            "description": "phase_description_1",
            "navigateTo": [
                {
                    "name": "phase_name_2"
                }
            ]
        },
        {
            "name": "phase_name_2",
            "title": "phase_title_2",
            "description": "phase_description_2",
            "navigateTo": null
        }
    ],
    "nodes": null
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| userId | path | ID of user | Yes | UUID |
| tenantName | path | Name of tenant | Yes | string |
| instanceName | path | Name of instance | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Created |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |

## Update program by name

### HTTP Request
***PUT*** `/{tenantName}/{instanceName}/formations/draft/programs/{programName}`

in our example it would be:

***PUT*** `https://api.live.welkincloud.io/gh/sb-demo/formations/draft/programs/care_program_name_1`

> Request

```json
{
  "name": "care_program_name_1",
  "title": "care_program_title_1",
  "description": "care_program_description_1",
  "phases": [
    {
      "name": "phase_name_1",
      "title": "phase_title_1",
      "description": "phase_description_1",
      "navigateTo": null
    }
  ]
}
```

> Response

```json
{
    "name": "care_program_name_1",
    "title": "care_program_title_1",
    "description": "care_program_description_1",
    "phases": [
        {
            "name": "phase_name_1",
            "title": "phase_title_1",
            "description": "phase_description_1",
            "navigateTo": null
        }
    ],
    "nodes": null
}
```

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| userId | path | ID of user | Yes | UUID |
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

## Delete program by name

### HTTP Request
***DELETE*** `/{tenantName}/{instanceName}/formations/draft/programs/{programName}`

in our example it would be:

***DELETE*** `https://api.live.welkincloud.io/gh/sb-demo/formations/draft/programs/care_program_name_1`

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| userId | path | ID of user | Yes | UUID |
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
