# Assessments

## Basics
An assessment consists of 3 parts: main, scoring, condition settings.

The main part contains a list of sections. Each section contains a list of fields. The **viewType** parameter in the
field indicates how the field will be displayed. The parameter can take one of two values: *readOnly* and *question*. 
The *readOnly* value of the parameter indicates that the field will be displayed as a text comment. The *question* 
value of the parameter indicates that the field will be displayed as a question with the possibility of user input. 
If the value of the **viewType** parameter is equal to *question* then parameters **refCdtName**, **refCdtFieldName** 
and **meta** are required. The combination of parameter values **refCdtName** and **refCdtFieldName** must be unique
among all fields in the assessment.

The scoring part describes the rules for calculating the assessment score. The **formula** parameter indicates how the
score will be calculated. The parameter can take one of two values: *SUM* and *AVG*. The *SUM* value of the parameter
indicates that the group scores will be summed up. The *AVG* value of the parameter indicates that the average of the 
group scores will be calculated. Each group also has the **formula** parameter which takes the same values. The group
score calculates from the field's scores. To associate fields in scoring with questions, you must specify
 **refCdtName** and **refCdtFieldName**.

The condition settings are divided into two parts: **elements** and **events**. The **elements** part describes how 
sections or questions will be displayed based on user answers. The **events** part describes which custom events will 
be hit based on user answers.

The collection supports several interactions

1. Allows to obtain a list of assessment
2. Allows to obtain a certain assessment
3. Allows to obtain a list of CDTs that is associated with an assessments

## Get All Assessments

> To obtain a Bearer token:

```python
import requests

params = {'secret': '+}B{KGTG6#zG%P;tQm0C'}
r = requests.post('https://api.live.welkincloud.io/gh/sb-demo/formation/current/assessments', json=params)
print(r.json())
```

> Successful response will look like:

```json
[
  {
        "id": "8be00831-fdeb-4b21-a4bc-e5bc52462806",
        "title": "PHQ v1",
        "name": "phq_v1",
        "version": 1,
        "sections": [
            {
                "title": "Over the last 2 weeks, how often have you been bothered by any of the following problems?",
                "name": "section-1",
                "order": 0,
                "fields": [
                    {
                        "label": "Little interest or pleasure in doing things",
                        "refCdtName": "phq",
                        "refCdtFieldName": "little_interest_pleasure",
                        "order": 0,
                        "viewType": "question",
                        "meta": {
                            "type": "select",
                            "required": true
                        },
                        "prePopulatedValue": null
                    },
                    {
                        "label": "Feeling down, depressed, or hopeless",
                        "refCdtName": "phq",
                        "refCdtFieldName": "feeling_down_depressed_hopeless",
                        "order": 1,
                        "viewType": "question",
                        "meta": {
                            "type": "select",
                            "required": true
                        },
                        "prePopulatedValue": null
                    },
                    {
                        "label": "Trouble falling or staying asleep, or sleeping too much",
                        "refCdtName": "phq",
                        "refCdtFieldName": "trouble_falling_staying_asleep_sleeping_too_much",
                        "order": 2,
                        "viewType": "question",
                        "meta": {
                            "type": "select",
                            "required": true
                        },
                        "prePopulatedValue": null
                    },
                    {
                        "label": "Feeling tired or having little energy",
                        "refCdtName": "phq",
                        "refCdtFieldName": "feeling_tired_having_little_energy",
                        "order": 3,
                        "viewType": "question",
                        "meta": {
                            "type": "select",
                            "required": true
                        },
                        "prePopulatedValue": null
                    },
                    {
                        "label": "Poor appetite or overeating",
                        "refCdtName": "phq",
                        "refCdtFieldName": "poor_appetite_overeating",
                        "order": 4,
                        "viewType": "question",
                        "meta": {
                            "type": "select",
                            "required": true
                        },
                        "prePopulatedValue": null
                    },
                    {
                        "label": "Feeling bad about yourself, or that you are a failure, or have let yourself or your family down",
                        "refCdtName": "phq",
                        "refCdtFieldName": "feeling_bad_about_yourself_failure_let_yourself_family_down",
                        "order": 5,
                        "viewType": "question",
                        "meta": {
                            "type": "select",
                            "required": true
                        },
                        "prePopulatedValue": null
                    },
                    {
                        "label": "Trouble concentrating on things, such as reading the newspaper or watching television",
                        "refCdtName": "phq",
                        "refCdtFieldName": "trouble_concentrating_things",
                        "order": 6,
                        "viewType": "question",
                        "meta": {
                            "type": "select",
                            "required": true
                        },
                        "prePopulatedValue": null
                    },
                    {
                        "label": "Moving or speaking so slowly that other people could have noticed. Or the opposite—being so fidgety or restless that you have been moving around a lot more than usual .",
                        "refCdtName": "phq",
                        "refCdtFieldName": "moving_speaking_slowly_fidgety_restless",
                        "order": 7,
                        "viewType": "question",
                        "meta": {
                            "type": "select",
                            "required": true
                        },
                        "prePopulatedValue": null
                    }
                ]
            }
        ],
        "scoring": {
            "formula": "SUM",
            "groups": [
                {
                    "name": "phq",
                    "title": "PHQ",
                    "fields": [
                        {
                            "refCdtName": "phq",
                            "refCdtFieldName": "little_interest_pleasure",
                            "type": "select",
                            "scores": [
                                {
                                    "score": 0,
                                    "answer": "0 -Not at all"
                                },
                                {
                                    "score": 1,
                                    "answer": "1 - Several days"
                                },
                                {
                                    "score": 2,
                                    "answer": "2 - More than half the days"
                                },
                                {
                                    "score": 3,
                                    "answer": "3 - Nearly every day"
                                }
                            ]
                        },
                        {
                            "refCdtName": "phq",
                            "refCdtFieldName": "feeling_down_depressed_hopeless",
                            "type": "select",
                            "scores": [
                                {
                                    "score": 0,
                                    "answer": "0 -Not at all"
                                },
                                {
                                    "score": 1,
                                    "answer": "1 - Several days"
                                },
                                {
                                    "score": 2,
                                    "answer": "2 - More than half the days"
                                },
                                {
                                    "score": 3,
                                    "answer": "3 - Nearly every day"
                                }
                            ]
                        },
                        {
                            "refCdtName": "phq",
                            "refCdtFieldName": "trouble_falling_staying_asleep_sleeping_too_much",
                            "type": "select",
                            "scores": [
                                {
                                    "score": 0,
                                    "answer": "0 -Not at all"
                                },
                                {
                                    "score": 1,
                                    "answer": "1 - Several days"
                                },
                                {
                                    "score": 2,
                                    "answer": "2 - More than half the days"
                                },
                                {
                                    "score": 3,
                                    "answer": "3 - Nearly every day"
                                }
                            ]
                        },
                        {
                            "refCdtName": "phq",
                            "refCdtFieldName": "feeling_tired_having_little_energy",
                            "type": "select",
                            "scores": [
                                {
                                    "score": 0,
                                    "answer": "0 -Not at all"
                                },
                                {
                                    "score": 1,
                                    "answer": "1 - Several days"
                                },
                                {
                                    "score": 2,
                                    "answer": "2 - More than half the days"
                                },
                                {
                                    "score": 3,
                                    "answer": "3 - Nearly every day"
                                }
                            ]
                        },
                        {
                            "refCdtName": "phq",
                            "refCdtFieldName": "poor_appetite_overeating",
                            "type": "select",
                            "scores": [
                                {
                                    "score": 0,
                                    "answer": "0 -Not at all"
                                },
                                {
                                    "score": 1,
                                    "answer": "1 - Several days"
                                },
                                {
                                    "score": 2,
                                    "answer": "2 - More than half the days"
                                },
                                {
                                    "score": 3,
                                    "answer": "3 - Nearly every day"
                                }
                            ]
                        },
                        {
                            "refCdtName": "phq",
                            "refCdtFieldName": "feeling_bad_about_yourself_failure_let_yourself_family_down",
                            "type": "select",
                            "scores": [
                                {
                                    "score": 0,
                                    "answer": "0 -Not at all"
                                },
                                {
                                    "score": 1,
                                    "answer": "1 - Several days"
                                },
                                {
                                    "score": 2,
                                    "answer": "2 - More than half the days"
                                },
                                {
                                    "score": 3,
                                    "answer": "3 - Nearly every day"
                                }
                            ]
                        },
                        {
                            "refCdtName": "phq",
                            "refCdtFieldName": "trouble_concentrating_things",
                            "type": "select",
                            "scores": [
                                {
                                    "score": 0,
                                    "answer": "0 -Not at all"
                                },
                                {
                                    "score": 1,
                                    "answer": "1 - Several days"
                                },
                                {
                                    "score": 2,
                                    "answer": "2 - More than half the days"
                                },
                                {
                                    "score": 3,
                                    "answer": "3 - Nearly every day"
                                }
                            ]
                        },
                        {
                            "refCdtName": "phq",
                            "refCdtFieldName": "moving_speaking_slowly_fidgety_restless",
                            "type": "select",
                            "scores": [
                                {
                                    "score": 0,
                                    "answer": "0 -Not at all"
                                },
                                {
                                    "score": 1,
                                    "answer": "1 - Several days"
                                },
                                {
                                    "score": 2,
                                    "answer": "2 - More than half the days"
                                },
                                {
                                    "score": 3,
                                    "answer": "3 - Nearly every day"
                                }
                            ]
                        }
                    ],
                    "formula": "SUM"
                }
            ]
        },
        "programs": [
            {
                "program": "coaching",
                "phases": [
                    "active",
                    "internal_referral_needed",
                    "treatment_completed"
                ]
            },
            {
                "program": "group_therapy",
                "phases": [
                    "active",
                    "treatment_completed"
                ]
            },
            {
                "program": "individual_therapy",
                "phases": [
                    "active",
                    "internal_referral_needed",
                    "treatment_completed"
                ]
            },
            {
                "program": "relationship_therapy",
                "phases": [
                    "active",
                    "internal_referral_needed",
                    "treatment_completed"
                ]
            }
        ],
        "template": null,
        "conditionSettings": null,
        "_containsPHI": true
    }
]
```

Collection of all assessment formation would be located at the following URL

`URL Structure: https://api.live.welkincloud.io/{tenantName}/{instanceName}/formation/{}/assessments`

1. First variable is your Tenant name. We will use **gh** as a tenant name through this set of api docs
2. Second variable is your Instance name. We will use **sb-demo** as an instance name through this set of api docs
3. Third variable is your formation version. We will use **current** to get published version and **draft** to get
version in draft.

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/formation/current/assessments`
3. HTTP Response Codes: 200

## Get One Assessment

> To obtain a Bearer token:

```python
import requests

params = {'secret': '+}B{KGTG6#zG%P;tQm0C'}
r = requests.post('https://api.live.welkincloud.io/gh/sb-demo/formation/current/assessments', json=params)
print(r.json())
```

> Successful response will look like:

```json
{
        "id": "8be00831-fdeb-4b21-a4bc-e5bc52462806",
        "title": "PHQ v1",
        "name": "phq_v1",
        "version": 1,
        "sections": [
            {
                "title": "Over the last 2 weeks, how often have you been bothered by any of the following problems?",
                "name": "section-1",
                "order": 0,
                "fields": [
                    {
                        "label": "Little interest or pleasure in doing things",
                        "refCdtName": "phq",
                        "refCdtFieldName": "little_interest_pleasure",
                        "order": 0,
                        "viewType": "question",
                        "meta": {
                            "type": "select",
                            "required": true
                        },
                        "prePopulatedValue": null
                    },
                    {
                        "label": "Feeling down, depressed, or hopeless",
                        "refCdtName": "phq",
                        "refCdtFieldName": "feeling_down_depressed_hopeless",
                        "order": 1,
                        "viewType": "question",
                        "meta": {
                            "type": "select",
                            "required": true
                        },
                        "prePopulatedValue": null
                    },
                    {
                        "label": "Trouble falling or staying asleep, or sleeping too much",
                        "refCdtName": "phq",
                        "refCdtFieldName": "trouble_falling_staying_asleep_sleeping_too_much",
                        "order": 2,
                        "viewType": "question",
                        "meta": {
                            "type": "select",
                            "required": true
                        },
                        "prePopulatedValue": null
                    },
                    {
                        "label": "Feeling tired or having little energy",
                        "refCdtName": "phq",
                        "refCdtFieldName": "feeling_tired_having_little_energy",
                        "order": 3,
                        "viewType": "question",
                        "meta": {
                            "type": "select",
                            "required": true
                        },
                        "prePopulatedValue": null
                    },
                    {
                        "label": "Poor appetite or overeating",
                        "refCdtName": "phq",
                        "refCdtFieldName": "poor_appetite_overeating",
                        "order": 4,
                        "viewType": "question",
                        "meta": {
                            "type": "select",
                            "required": true
                        },
                        "prePopulatedValue": null
                    },
                    {
                        "label": "Feeling bad about yourself, or that you are a failure, or have let yourself or your family down",
                        "refCdtName": "phq",
                        "refCdtFieldName": "feeling_bad_about_yourself_failure_let_yourself_family_down",
                        "order": 5,
                        "viewType": "question",
                        "meta": {
                            "type": "select",
                            "required": true
                        },
                        "prePopulatedValue": null
                    },
                    {
                        "label": "Trouble concentrating on things, such as reading the newspaper or watching television",
                        "refCdtName": "phq",
                        "refCdtFieldName": "trouble_concentrating_things",
                        "order": 6,
                        "viewType": "question",
                        "meta": {
                            "type": "select",
                            "required": true
                        },
                        "prePopulatedValue": null
                    },
                    {
                        "label": "Moving or speaking so slowly that other people could have noticed. Or the opposite—being so fidgety or restless that you have been moving around a lot more than usual .",
                        "refCdtName": "phq",
                        "refCdtFieldName": "moving_speaking_slowly_fidgety_restless",
                        "order": 7,
                        "viewType": "question",
                        "meta": {
                            "type": "select",
                            "required": true
                        },
                        "prePopulatedValue": null
                    }
                ]
            }
        ],
        "scoring": {
            "formula": "SUM",
            "groups": [
                {
                    "name": "phq",
                    "title": "PHQ",
                    "fields": [
                        {
                            "refCdtName": "phq",
                            "refCdtFieldName": "little_interest_pleasure",
                            "type": "select",
                            "scores": [
                                {
                                    "score": 0,
                                    "answer": "0 -Not at all"
                                },
                                {
                                    "score": 1,
                                    "answer": "1 - Several days"
                                },
                                {
                                    "score": 2,
                                    "answer": "2 - More than half the days"
                                },
                                {
                                    "score": 3,
                                    "answer": "3 - Nearly every day"
                                }
                            ]
                        },
                        {
                            "refCdtName": "phq",
                            "refCdtFieldName": "feeling_down_depressed_hopeless",
                            "type": "select",
                            "scores": [
                                {
                                    "score": 0,
                                    "answer": "0 -Not at all"
                                },
                                {
                                    "score": 1,
                                    "answer": "1 - Several days"
                                },
                                {
                                    "score": 2,
                                    "answer": "2 - More than half the days"
                                },
                                {
                                    "score": 3,
                                    "answer": "3 - Nearly every day"
                                }
                            ]
                        },
                        {
                            "refCdtName": "phq",
                            "refCdtFieldName": "trouble_falling_staying_asleep_sleeping_too_much",
                            "type": "select",
                            "scores": [
                                {
                                    "score": 0,
                                    "answer": "0 -Not at all"
                                },
                                {
                                    "score": 1,
                                    "answer": "1 - Several days"
                                },
                                {
                                    "score": 2,
                                    "answer": "2 - More than half the days"
                                },
                                {
                                    "score": 3,
                                    "answer": "3 - Nearly every day"
                                }
                            ]
                        },
                        {
                            "refCdtName": "phq",
                            "refCdtFieldName": "feeling_tired_having_little_energy",
                            "type": "select",
                            "scores": [
                                {
                                    "score": 0,
                                    "answer": "0 -Not at all"
                                },
                                {
                                    "score": 1,
                                    "answer": "1 - Several days"
                                },
                                {
                                    "score": 2,
                                    "answer": "2 - More than half the days"
                                },
                                {
                                    "score": 3,
                                    "answer": "3 - Nearly every day"
                                }
                            ]
                        },
                        {
                            "refCdtName": "phq",
                            "refCdtFieldName": "poor_appetite_overeating",
                            "type": "select",
                            "scores": [
                                {
                                    "score": 0,
                                    "answer": "0 -Not at all"
                                },
                                {
                                    "score": 1,
                                    "answer": "1 - Several days"
                                },
                                {
                                    "score": 2,
                                    "answer": "2 - More than half the days"
                                },
                                {
                                    "score": 3,
                                    "answer": "3 - Nearly every day"
                                }
                            ]
                        },
                        {
                            "refCdtName": "phq",
                            "refCdtFieldName": "feeling_bad_about_yourself_failure_let_yourself_family_down",
                            "type": "select",
                            "scores": [
                                {
                                    "score": 0,
                                    "answer": "0 -Not at all"
                                },
                                {
                                    "score": 1,
                                    "answer": "1 - Several days"
                                },
                                {
                                    "score": 2,
                                    "answer": "2 - More than half the days"
                                },
                                {
                                    "score": 3,
                                    "answer": "3 - Nearly every day"
                                }
                            ]
                        },
                        {
                            "refCdtName": "phq",
                            "refCdtFieldName": "trouble_concentrating_things",
                            "type": "select",
                            "scores": [
                                {
                                    "score": 0,
                                    "answer": "0 -Not at all"
                                },
                                {
                                    "score": 1,
                                    "answer": "1 - Several days"
                                },
                                {
                                    "score": 2,
                                    "answer": "2 - More than half the days"
                                },
                                {
                                    "score": 3,
                                    "answer": "3 - Nearly every day"
                                }
                            ]
                        },
                        {
                            "refCdtName": "phq",
                            "refCdtFieldName": "moving_speaking_slowly_fidgety_restless",
                            "type": "select",
                            "scores": [
                                {
                                    "score": 0,
                                    "answer": "0 -Not at all"
                                },
                                {
                                    "score": 1,
                                    "answer": "1 - Several days"
                                },
                                {
                                    "score": 2,
                                    "answer": "2 - More than half the days"
                                },
                                {
                                    "score": 3,
                                    "answer": "3 - Nearly every day"
                                }
                            ]
                        }
                    ],
                    "formula": "SUM"
                }
            ]
        },
        "programs": [
            {
                "program": "coaching",
                "phases": [
                    "active",
                    "internal_referral_needed",
                    "treatment_completed"
                ]
            },
            {
                "program": "group_therapy",
                "phases": [
                    "active",
                    "treatment_completed"
                ]
            },
            {
                "program": "individual_therapy",
                "phases": [
                    "active",
                    "internal_referral_needed",
                    "treatment_completed"
                ]
            },
            {
                "program": "relationship_therapy",
                "phases": [
                    "active",
                    "internal_referral_needed",
                    "treatment_completed"
                ]
            }
        ],
        "template": null,
        "conditionSettings": null,
        "_containsPHI": true
    }
```

A certain assessment formation would be located at the following URL

`URL Structure: https://api.live.welkincloud.io/{tenantName}/{instanceName}/formation/{}/assessments/{}`

1. First variable is your Tenant name. We will use **gh** as a tenant name through this set of api docs
2. Second variable is your Instance name. We will use **sb-demo** as an instance name through this set of api docs
3. Third variable is your formation version. We will use **current** to get published version and **draft** to get
version in draft
4. Fourth parameter is assessment name. We will specify an assessment name which we want to get

Example request:

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/formation/current/assessments/phq_v1`
3. HTTP Response Codes: 200, 404

## Get CDT related to the assessment

> To obtain a Bearer token:

```python
import requests

params = {'secret': '+}B{KGTG6#zG%P;tQm0C'}
r = requests.post('https://api.live.welkincloud.io/gh/sb-demo/formation/current/assessments/cdt/_phq_v1', json=params)
print(r.json())
```

> Successful response will look like:

```json
    {
        "id": "f53fb1be-42cf-41c9-bfbc-b118bcd532ef",
        "name": "_phq_v1",
        "title": null,
        "label": "PHQ v1",
        "version": 13,
        "internal": true,
        "readable": false,
        "updatable": false,
        "type": "MULTI_RECORD",
        "relation": "ASSESSMENT",
        "fields": [
            {
                "name": "phq__little_interest_pleasure",
                "type": "select",
                "dictionary": null,
                "searchable": false,
                "bulkEdit": false,
                "phi": true,
                "meta": {
                    "label": "Little interest or pleasure in doing things",
                    "required": true,
                    "options": [
                        {
                            "label": "0 - Not at all",
                            "value": "0 -Not at all",
                            "refCdtName": null
                        },
                        {
                            "label": "1 - Several days",
                            "value": "1 - Several days",
                            "refCdtName": null
                        },
                        {
                            "label": "2 - More than half the days",
                            "value": "2 - More than half the days",
                            "refCdtName": null
                        },
                        {
                            "label": "3 - Nearly every day",
                            "value": "3 - Nearly every day",
                            "refCdtName": null
                        }
                    ]
                }
            },
            {
                "name": "phq__feeling_down_depressed_hopeless",
                "type": "select",
                "dictionary": null,
                "searchable": false,
                "bulkEdit": false,
                "phi": true,
                "meta": {
                    "label": "Feeling down, depressed, or hopeless",
                    "required": true,
                    "options": [
                        {
                            "label": "0 - Not at all",
                            "value": "0 -Not at all",
                            "refCdtName": null
                        },
                        {
                            "label": "1 - Several days",
                            "value": "1 - Several days",
                            "refCdtName": null
                        },
                        {
                            "label": "2 - More than half the days",
                            "value": "2 - More than half the days",
                            "refCdtName": null
                        },
                        {
                            "label": "3 - Nearly every day",
                            "value": "3 - Nearly every day",
                            "refCdtName": null
                        }
                    ]
                }
            },
            {
                "name": "phq__trouble_falling_staying_asleep_sleeping_too_much",
                "type": "select",
                "dictionary": null,
                "searchable": false,
                "bulkEdit": false,
                "phi": true,
                "meta": {
                    "label": "Trouble falling or staying asleep, or sleeping too much",
                    "required": true,
                    "options": [
                        {
                            "label": "0 - Not at all",
                            "value": "0 -Not at all",
                            "refCdtName": null
                        },
                        {
                            "label": "1 - Several days",
                            "value": "1 - Several days",
                            "refCdtName": null
                        },
                        {
                            "label": "2 - More than half the days",
                            "value": "2 - More than half the days",
                            "refCdtName": null
                        },
                        {
                            "label": "3 - Nearly every day",
                            "value": "3 - Nearly every day",
                            "refCdtName": null
                        }
                    ]
                }
            },
            {
                "name": "phq__feeling_tired_having_little_energy",
                "type": "select",
                "dictionary": null,
                "searchable": false,
                "bulkEdit": false,
                "phi": true,
                "meta": {
                    "label": "Feeling tired or having little energy",
                    "required": true,
                    "options": [
                        {
                            "label": "0 - Not at all",
                            "value": "0 -Not at all",
                            "refCdtName": null
                        },
                        {
                            "label": "1 - Several days",
                            "value": "1 - Several days",
                            "refCdtName": null
                        },
                        {
                            "label": "2 - More than half the days",
                            "value": "2 - More than half the days",
                            "refCdtName": null
                        },
                        {
                            "label": "3 - Nearly every day",
                            "value": "3 - Nearly every day",
                            "refCdtName": null
                        }
                    ]
                }
            },
            {
                "name": "phq__poor_appetite_overeating",
                "type": "select",
                "dictionary": null,
                "searchable": false,
                "bulkEdit": false,
                "phi": true,
                "meta": {
                    "label": "Poor appetite or overeating",
                    "required": true,
                    "options": [
                        {
                            "label": "0 - Not at all",
                            "value": "0 -Not at all",
                            "refCdtName": null
                        },
                        {
                            "label": "1 - Several days",
                            "value": "1 - Several days",
                            "refCdtName": null
                        },
                        {
                            "label": "2 - More than half the days",
                            "value": "2 - More than half the days",
                            "refCdtName": null
                        },
                        {
                            "label": "3 - Nearly every day",
                            "value": "3 - Nearly every day",
                            "refCdtName": null
                        }
                    ]
                }
            },
            {
                "name": "phq__feeling_bad_about_yourself_failure_let_yourself_family_down",
                "type": "select",
                "dictionary": null,
                "searchable": false,
                "bulkEdit": false,
                "phi": true,
                "meta": {
                    "label": "Feeling bad about yourself, or that you are a failure, or have let yourself or your family down",
                    "required": true,
                    "options": [
                        {
                            "label": "0 - Not at all",
                            "value": "0 -Not at all",
                            "refCdtName": null
                        },
                        {
                            "label": "1 - Several days",
                            "value": "1 - Several days",
                            "refCdtName": null
                        },
                        {
                            "label": "2 - More than half the days",
                            "value": "2 - More than half the days",
                            "refCdtName": null
                        },
                        {
                            "label": "3 - Nearly every day",
                            "value": "3 - Nearly every day",
                            "refCdtName": null
                        }
                    ]
                }
            },
            {
                "name": "phq__trouble_concentrating_things",
                "type": "select",
                "dictionary": null,
                "searchable": false,
                "bulkEdit": false,
                "phi": true,
                "meta": {
                    "label": "Trouble concentrating on things, such as reading the newspaper or watching television",
                    "required": true,
                    "options": [
                        {
                            "label": "0 - Not at all",
                            "value": "0 -Not at all",
                            "refCdtName": null
                        },
                        {
                            "label": "1 - Several days",
                            "value": "1 - Several days",
                            "refCdtName": null
                        },
                        {
                            "label": "2 - More than half the days",
                            "value": "2 - More than half the days",
                            "refCdtName": null
                        },
                        {
                            "label": "3 - Nearly every day",
                            "value": "3 - Nearly every day",
                            "refCdtName": null
                        }
                    ]
                }
            },
            {
                "name": "phq__moving_speaking_slowly_fidgety_restless",
                "type": "select",
                "dictionary": null,
                "searchable": false,
                "bulkEdit": false,
                "phi": true,
                "meta": {
                    "label": "Moving or speaking so slowly that other people could have noticed. Or the opposite—being so fidgety or restless that you have been moving around a lot more than usual .",
                    "required": true,
                    "options": [
                        {
                            "label": "0 - Not at all",
                            "value": "0 -Not at all",
                            "refCdtName": null
                        },
                        {
                            "label": "1 - Several days",
                            "value": "1 - Several days",
                            "refCdtName": null
                        },
                        {
                            "label": "2 - More than half the days",
                            "value": "2 - More than half the days",
                            "refCdtName": null
                        },
                        {
                            "label": "3 - Nearly every day",
                            "value": "3 - Nearly every day",
                            "refCdtName": null
                        }
                    ]
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
        "_containsPHI": true
    }
```

For each assessment, a CDT is created automatically to store user answers. If an assessment contains scoring section
separate CDT creates to store user scores. These CDTs are internal. As all internal CDTs they have '**_**' prefix.
CDT for scoring has '**_scoring**' postfix.

For example:

An assessment with name *phq_v1* has general CDT *_phq_v1* and CDT for scoring *_phq_v1_scoring*.

A certain CDT related to assessment would be located at the following URL

`URL Structure: https://api.live.welkincloud.io/{tenantName}/{instanceName}/formation/{}/assessments/cdt/{}`

1. First variable is your Tenant name. We will use **gh** as a tenant name through this set of api docs
2. Second variable is your Instance name. We will use **sb-demo** as an instance name through this set of api docs
3. Third variable is your formation version. We will use **current** to get published version and **draft** to get
version in draft
4. Fourth parameter is CDT name. We will specify a CDT name which we want to get

Example request:

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/formation/current/assessments/cdt/_phq_v1`
3. HTTP Response Codes: 200, 404

## Create an assessment

To create an assessment would be used at the following URL

`URL Structure: https://api.live.welkincloud.io/{tenantName}/{instanceName}/formation/draft/assessments`

1. First variable is your Tenant name. We will use **gh** as a tenant name through this set of api docs
2. Second variable is your Instance name. We will use **sb-demo** as an instance name through this set of api docs

Please note that you can create an assessment only in the **draft** version of the formation

Example request:

1. HTTP Method: POST
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/formation/current/assessments`
3. HTTP Response Codes: 200, 404

## Update an assessment

To update an assessment would be used at the following URL

`URL Structure: https://api.live.welkincloud.io/{tenantName}/{instanceName}/formation/draft/assessments/{}`

1. First variable is your Tenant name. We will use **gh** as a tenant name through this set of api docs
2. Second variable is your Instance name. We will use **sb-demo** as an instance name through this set of api docs
3. Third variable is your assessment name. We will specify an assessment name which we want to update

Please note on two things:

1. You can update an assessment only in the **draft** version of the formation
2. You cannot update an assessment name. To update the name of assessment you should recreate the assessment with the 
correct name

Example request:

1. HTTP Method: PUT
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/formation/current/assessments/phq_v1`
3. HTTP Response Codes: 200, 404

## Delete an assessment

To delete an assessment would be used at the following URL

`URL Structure: https://api.live.welkincloud.io/{tenantName}/{instanceName}/formation/draft/assessments/{}`

1. First variable is your Tenant name. We will use **gh** as a tenant name through this set of api docs
2. Second variable is your Instance name. We will use **sb-demo** as an instance name through this set of api docs
3. Third variable is your assessment name. We will specify an assessment name which we want to delete

Please note that you can create an assessment only in the **draft** version of the formation

Example request:

1. HTTP Method: DELETE
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/formation/current/assessments/phq_v1`
3. HTTP Response Codes: 200, 404


