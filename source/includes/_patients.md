# Patients

Collection of all patients would be located at the following URL

`URL Structure: https://api.live.welkincloud.io/{}/{}/patients`

In our example that is `https://api.live.welkincloud.io/gh/sb-demo/patients`

The collection supports several interactions

1. Allows to obtain a list of patients (can be sorted)
2. Allows to obtain a filtered list of patients based of email address (commonly referred as FINDER)
2. Allows to create a new patient

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
....pagination links omitted
  ]
}
```

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patients`
3. HTTP Reponse Codes: 201, 400, 500

Following Query Parameters can be used to sort or find approporiately

Parameter | Description | Examples
--------- | ----------- | --------
sort |Allows one to specify the sort order of the returned patients collection | https://api.live.welkincloud.io/gh/sb-demo/patients?sort=firstName,desc
email |When specified, will execute a search for a patient based of email address | https://api.live.welkincloud.io/gh/sb-demo/patients?email=1@1.com


## Create a Patient

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
        "email": "Charlie.Taylor@superemail.com"
    }

r = requests.post("https://api.live.welkincloud.io/gh/sb-demo/patients", json=data, headers=h)
print(r.json())
```

> The above request returns JSON structured like this:

```json

{
  "id": "e3dd671a-86f0-4951-80fb-13b12766292f", 
  "externalGuid": None, 
  "firstName": "Charlie", 
  "lastName": "Taylor", 
  "middleName": None, 
  "birthDate": "2012-03-12T00:00:00.000Z", 
  "email": "Charlie.Taylor@superemail.com", 
  "phone": "+15556491369", 
  "country": None, 
  "state": None, 
  "city": None, 
  "zip": None, 
  "addressLine1": None, 
  "addressLine2": None, 
  "timezone": "America/Los_Angeles", 
  "patientTerritories": None, 
  "careTeam": None
}
```
1. HTTP Method: POST
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patients`
3. HTTP Reponse Codes: 201, 400, 500



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
  "patientTerritories": [],
}  
```

To get a patient by a known ID

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patients/6801d498-26f4-4aee-961b-5daffcf193c8`
3. HTTP Reponse Codes: 200, 400, 500


## Delete a Specific Patient

<aside class="warning">
This operation is not supported yet
</aside>
