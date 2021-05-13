# Patients

Collection of all patients would be located at the following URL

`URL Structure: https://api.live.welkincloud.io/{}/{}/patients`

In our example that is `https://api.live.welkincloud.io/gh/sb-demo/patients`

The collection supports several interactions

1. Allows to obtain a list of patients (can be sorted)
2. Allows to obtain a filtered list of patients based of email address (commonly referred as FINDER)
3. Allows to create a new patient
4. Allows to update an existing patient by ID

## Get All Patients

```python
import requests
h = {
        "Authorization": "Bearer {}".format(token)
    }

r = requests.get("https://api.live.welkincloud.io/gh/sb-demo/patients", headers=h)
print(r.json())
```

> The above request returns JSON structured like this:

```json
{"content": 
  [
    {
      "id": "6801d498-26f4-4aee-961b-5daffcf193c8",
      "firstName": "Charlie",
      "lastName": "Schwarzenegger",
      "middleName": "Mc",
      "birthDate": "2012-08-12T00:00:00.000Z",
      "email": "1@1.com",
      "phone": "+13363034233",
      "country": "USA",
      "state": "American Samoa",
      "city": "Los Angeles",
      "zip": "99451",
      "addressLine1": "Hollywood Blvd 2021",
      "timezone ": "America / Los_Angeles",
      "patientTerritories": [],
      "careTeam": []
    }
  ],
  "pageable": {
        "sort": {
            "sorted": False,
            "unsorted": True,
            "empty": True
            },
        "pageNumber": 2,
        "pageSize": 20,
        "offset": 40,
        "unpaged": False,
        "paged": True
	},
	"last": False,
	"totalElements": 357,
	"totalPages": 18,
	"first": False,
	"number": 2,
	"sort": {
		"sorted": False,
		"unsorted": True,
		"empty": True
	},
	"numberOfElements": 20,
	"size": 20,
	"empty": False
}
```

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patients`
3. HTTP Response Codes: 200, 400, 500

Following Query Parameters can be used to sort or find appropriately

Parameter | Description | 
--------- | ----------- | 
sort |Allows one to specify the sort order of the returned patients collection 
query |When specified, will execute a search for a patient based of email address, first name, last name and phone  
size | Pagination: Specifies number of records to return by each page. 
page | Pagination: Specifies what page to return
timezone | When specified, will execute a search by patient's timezone. Use empty string to find patients with no timezone configured (example 4)
territories | Use empty string to find patients with no territories configured (example 5)
cadence | Use empty string to find patients with no timezone configured (example 6)

Here are few examples:

1. https://api.live.welkincloud.io/gh/sb-demo/patients?sort=firstName,desc
2. https://api.live.welkincloud.io/gh/sb-demo/patients?email=1@1.com
3. https://api.live.welkincloud.io/gh/sb-demo/patients?size=20&page=2
4. https://api.live.welkincloud.io/gh/sb-demo/patients?timezone=
5. https://api.live.welkincloud.io/gh/sb-demo/patients?territories=
6. https://api.live.welkincloud.io/gh/sb-demo/patients?cadence=
 
## Create a Patient

> ***Note 1***: `patientTerritories` must contain valid territory that was previously created in the designer.
You can also omit this field when creating a patient and update it later.

> ***Note 2***: All careTeam members must be valid users, one of them must contain the `pointOfContact: True` flag,
otherwise the first user from careTeam will be marked as `pointOfContact`.
You can also omit this field when creating a patient and update it later.

Creating a new Patient is a simple as posting to a Patient Collection resource

```python
import requests

h = {
    "Authorization": "Bearer {}".format(token)
}

data = {
    "firstName": "Charlie",
    "lastName": "Taylor",
    "birthDate": "2012-3-12T00:00:00.000Z",
    "timezone": "America/Los_Angeles",
    "phone": "+15556491369",
    "email": "Charlie.Taylor@superemail.com",
    "patientTerritories": [
        {
            "name": "california",
            "territories": [
                "los-angeles"
            ]
        }
    ],
    "careTeam": [
        {
            "id": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
            "pointOfContact": True
        },
        {
            "id": "03a87f5b-3a04-4be8-b0ad-7a34a5b2892d",
            "pointOfContact": False
        }
    ]
}

r = requests.post("https://api.live.welkincloud.io/gh/sb-demo/patients", json=data, headers=h)
print(r.json())
```

> The above request returns JSON structured like this:

```json

{
  "id": "e3dd671a-86f0-4951-80fb-13b12766292f", 
  "externalGuid": null, 
  "firstName": "Charlie", 
  "lastName": "Taylor", 
  "middleName": null, 
  "birthDate": "2012-03-12T00:00:00.000Z", 
  "email": "Charlie.Taylor@superemail.com", 
  "phone": "+15556491369", 
  "country": null, 
  "state": null, 
  "city": null, 
  "zip": null, 
  "addressLine1": null, 
  "addressLine2": null, 
  "timezone": "America/Los_Angeles",
  "patientTerritories": [
    {
      "name": "california",
      "territories": [
        "los-angeles"
      ]
    }
  ],
  "careTeam": [
    [
      {
        "id": "03a87f5b-3a04-4be8-b0ad-7a34a5b2892d",
        "username": "johndou",
        "firstName": "John",
        "lastName": "Dou",
        "roles": [
          {
            "name": "caregiver",
            "primaryRole": true
          }
        ],
        "pointOfContact": false
      },
      {
        "id": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
        "username": "janedou",
        "firstName": "Jane",
        "lastName": "Dou",
        "roles": [
          {
            "name": "admin",
            "primaryRole": false
          },
          {
            "name": "root",
            "primaryRole": true
          }
        ],
        "pointOfContact": true
      }
    ]
  ]
}
```
1. HTTP Method: POST
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patients`
3. HTTP Response Codes: 201, 400, 500



## Get a Specific Patient By ID

```python
import requests
h = {
        "Authorization": "Bearer {}".format(token)
    }

r = requests.get("https://api.live.welkincloud.io/gh/sb-demo/patients/6801d498-26f4-4aee-961b-5daffcf193c8", 
  headers=h)
print("Response Code: {}".format(r.status_code))
print(r.json())
```

> The above command returns JSON structured like this:

```json
{
  "id": "6801d498-26f4-4aee-961b-5daffcf193c8",
  "firstName": "Charlie",
  "lastName": "Schwarzenegger",
  "middleName": "Mc",
  "birthDate": "2012-08-12T00:00:00.000Z",
  "email": "1@1.com",
  "phone": "+13363034233",
  "country": "USA",
  "state": "American Samoa",
  "city": "Los Angeles",
  "zip": "99451",
  "addressLine1": "Hollywood Blvd 2021",
  "timezone ": "America / Los_Angeles",
  "patientTerritories": []
}  
```

To get a patient by a known ID

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patients/6801d498-26f4-4aee-961b-5daffcf193c8`
3. HTTP Response Codes: 200, 400, 500

## Update a Specific Patient By ID

> Note: Using the Patch request, you should specify only those fields that you want to update.
All fields missing in the request will retain their previous values.

```python
import requests

data = {
    "id": "6801d498-26f4-4aee-961b-5daffcf193c8",
    "firstName": "Charlie",
    "lastName": "Schwarzenegger",
    "birthDate": "2012-08-12T00:00:00.000Z",
    "email": "2@2.com",
    "phone": "+13363034233",
    "country": "USA",
    "state": "American Samoa",
    "city": "Los Angeles",
    "zip": "99451",
    "addressLine1": "Hollywood Blvd 1111",
    "timezone": "UTC",
    "patientTerritories": [],
    "careTeam": [
        {
            "id": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
            "pointOfContact": True
        }
    ]
}

h = {
    "Authorization": "Bearer {}".format(token)
}

r = requests.patch("https://api.live.welkincloud.io/gh/sb-demo/patients/6801d498-26f4-4aee-961b-5daffcf193c8",
                   json=data, headers=h)
print("Response Code: {}".format(r.status_code))
print(r.json())
```

> The above command returns JSON structured like this:

```json
{
  "id": "1e57da59-42e2-4412-9152-11f37129b782",
  "externalGuid": null,
  "externalId": null,
  "mrn": null,
  "createdAt": "2021-05-04T11:38:24.672Z",
  "updatedAt": "2021-05-04T11:38:24.672Z",
  "createdBy": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
  "updatedBy": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
  "createdByName": "Alex Skripnik",
  "updatedByName": "Alex Skripnik",
  "firstName": "Charlie",
  "lastName": "Schwarzenegger",
  "middleName": "Mc",
  "birthDate": "2012-08-12T00:00:00.000Z",
  "gender": "UNKNOWN",
  "email": "1@1.com",
  "phone": "+13363034233",
  "country": "USA",
  "state": "American Samoa",
  "city": "Los Angeles",
  "zip": "99451",
  "addressLine1": "Hollywood Blvd 2021",
  "addressLine2": null,
  "timezone": "UTC",
  "patientTerritories": [],
  "careTeam": [
    {
      "id": "20eb246e-8099-4c7c-854c-5e0f9a366ddb",
      "username": "root",
      "firstName": "John",
      "lastName": "Dou",
      "roles": [
        {
          "name": "admin",
          "primaryRole": true
        }
      ],
      "pointOfContact": true
    }
  ]
} 
```

To update a patient by a known ID

1. HTTP Method: PATCH
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patients/6801d498-26f4-4aee-961b-5daffcf193c8`
3. HTTP Response Codes: 200, 400, 404, 500


## Delete a Specific Patient

<aside class="warning">
This operation is not supported yet
</aside>
