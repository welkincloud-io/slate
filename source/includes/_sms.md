# Sms

`URL Structure: {{url}} / {{tenantName}} / {{instanceName}} / sms`

in our example it would be:

`https://api.live.welkincloud.io/gh/sb-demo/sms`

## Get all sms

> ***GET request***

```python
import requests
h = {
        "Authorization": "Bearer {}".format(token)
    }

r = requests.get("https://api.live.welkincloud.io/gh/sb-demo/sms", headers=h)
print(r.json())
```

> The above request returns JSON structured like this:

```json
{
  "content": [
    {
      "id": "92c6f2c6-61b7-46ad-b1a8-3ca541b88c0f",
      "sendNow": false,
      "scheduledAt": "2021-05-04T19:50:09.808Z",
      "sentAt": "2021-05-04T19:50:11.234Z",
      "receivedAt": null,
      "date": "2021-05-04T19:50:11.234Z",
      "careTeam": "Nick Snow",
      "patientInfo": "John Doe",
      "timezone": "America/Los_Angeles",
      "sender": "de23c848-65aa-45a1-bf7b-f1d36a6e4ebe",
      "from": "+15625345699",
      "receiver": "830b8744-2c0f-4750-ad6d-5c2c94ada65d",
      "to": "+15625345678",
      "direction": "OUT",
      "externalId": "SM993260f0b8744163ae3a56ce9d158a05",
      "starred": false,
      "senderName": "Nick Snow",
      "receiverName": "John Doe",
      "message": "sms message",
      "parts" : 1,
      "status": "DELIVERED"
    }
    ....pagination links omitted
  ]
}
```

Following Query Parameters can be used to sort or find approporiately

We can use any combination of this parameters in single request: Example: {{url}}/{{tenantName}}/{{instanceName}}/sms?status=DELIVERED, FAILED&phone=+15625345678&starred=true

Parameter | Description | Examples
--------- | ----------- | --------
sort |Allows one to specify the sort order of the returned sms collection | https://api.live.welkincloud.io/gh/sb-demo/sms?sort=firstName,desc
size |When specified, size per page | https://api.live.welkincloud.io/gh/sb-demo/sms?size=20
page |When specified, page number | https://api.live.welkincloud.io/gh/sb-demo/sms?page=1
search |When specified, will execute a search based on message field | https://api.live.welkincloud.io/gh/sb-demo/sms?search=sometext
sender |When specified, search by sender id | https://api.live.welkincloud.io/gh/sb-demo/sms?sender=de23c848-65aa-45a1-bf7b-f1d36a6e4ebe
receiver |When specified, search by receiver id | https://api.live.welkincloud.io/gh/sb-demo/sms?sender=de23c848-65aa-45a1-bf7b-f1d36a6e4ebe
direction |When specified, search by direction (IN or OUT) | https://api.live.welkincloud.io/gh/sb-demo/sms?direction=IN
starred |When specified, search by starred (boolean value) field (as an important sms) | https://api.live.welkincloud.io/gh/sb-demo/sms?starred=true
from |When specified, search by 'from' phone | https://api.live.welkincloud.io/gh/sb-demo/sms?from=test@gmail.com
to |When specified, search by 'to' phone | https://api.live.welkincloud.io/gh/sb-demo/sms?to=test@gmail.com
phone |When specified, search by 'to' or 'from' phone | https://api.live.welkincloud.io/gh/sb-demo/sms?email=test@gmail.com
senderName |When specified, search by sender name | https://api.live.welkincloud.io/gh/sb-demo/sms?senderName=Jon doe
receiverName |When specified, search by receiver name | https://api.live.welkincloud.io/gh/sb-demo/sms?receiverName=Jon doe
status |When specified, search by status [SCHEDULED, ACCEPTED, SENT, RECEIVED, DELIVERED, UNDELIVERED, FAILED, UNRECOGNISED]| https://api.live.welkincloud.io/gh/sb-demo/sms?status=DELIVERED

## Get email by id

`URL Structure: {{url}} / {{tenantName}} / {{instanceName}} / sms / {{uuid}}`

> ***GET request***

```python
import requests
h = {
        "Authorization": "Bearer {}".format(token)
    }

r = requests.get("https://api.live.welkincloud.io/gh/sb-demo/sms/92c6f2c6-61b7-46ad-b1a8-3ca541b88c0f", headers=h)
print(r.json())
```

> The above request returns JSON structured like this:

```json
{
  "id": "92c6f2c6-61b7-46ad-b1a8-3ca541b88c0f",
  "sendNow": false,
  "scheduledAt": "2021-05-04T19:50:09.808Z",
  "sentAt": "2021-05-04T19:50:11.234Z",
  "receivedAt": null,
  "date": "2021-05-04T19:50:11.234Z",
  "careTeam": "Nick Snow",
  "patientInfo": "John Doe",
  "timezone": "America/Los_Angeles",
  "sender": "de23c848-65aa-45a1-bf7b-f1d36a6e4ebe",
  "from": "+15625345699",
  "receiver": "830b8744-2c0f-4750-ad6d-5c2c94ada65d",
  "to": "+15625345678",
  "direction": "OUT",
  "externalId": "SM993260f0b8744163ae3a56ce9d158a05",
  "starred": false,
  "senderName": "Nick Snow",
  "receiverName": "John Doe",
  "message": "sms message",
  "parts" : 1,
  "status": "DELIVERED"
}
```
## Send an email

Creates sms record and send it.

***Note***: Welkonnect module should be configured

## Send a basic email
***Note***: Configuration for Twilio service should be added.

`URL Structure: {{url}} / {{tenantName}} / {{instanceName}} / sms`

> ***POST request. Send sms***

```python
import requests
h = {
    "Authorization": "Bearer {}".format(token)
}
data = {
    "message": "Hi dear patient!",
    "sendNow": true,
    "receiver": "8b676172-78f8-4cc6-b105-5329c8a58ef2"
}

r = requests.post("https://api.live.welkincloud.io/gh/sb-demo/sms", 
  json=data, headers=h)
```

> The above request returns JSON structured like this:

```json
{
  "id": "92c6f2c6-61b7-46ad-b1a8-3ca541b88c0f",
  "sendNow": false,
  "scheduledAt": "2021-05-04T19:50:09.808Z",
  "sentAt": "2021-05-04T19:50:11.234Z",
  "receivedAt": null,
  "date": "2021-05-04T19:50:11.234Z",
  "careTeam": "Nick Snow",
  "patientInfo": "John Doe",
  "timezone": "America/Los_Angeles",
  "sender": "de23c848-65aa-45a1-bf7b-f1d36a6e4ebe",
  "from": "+15625345699",
  "receiver": "8b676172-78f8-4cc6-b105-5329c8a58ef2",
  "to": "+15625345678",
  "direction": "OUT",
  "externalId": "SM993260f0b8744163ae3a56ce9d158a05",
  "starred": false,
  "senderName": "Nick Snow",
  "receiverName": "John Doe",
  "message": "Hi dear patient!",
  "parts" : 1,
  "status": "DELIVERED"
}
```

## Update sms

Updating a sms could have some different behaviour, depending on email status.

1. When sms was sent, and it has direction = OUT (user sent it to patient),
   it can have one of following status [ACCEPTED, SENT, DELIVERED, UNDELIVERED, FAILED]
   In this case, we can only update 'starred' field and mark this sms as an important

2. When, sms direction = IN (patient sent sms to user), it could be also UNRECOGNISED (when system couldn't recognise know patient's phone number)
   In this case, we can assign this sms to patient manually

3. When sms has status [SCHEDULED]. We can do full update of this sms

## Update sms. Mark as an important sms

`URL Structure: {{url}} / {{tenantName}} / {{instanceName}} / sms / {{uuid}}`

> ***PUT request. Mark as an important sms***

```python
import requests
h = {
    "Authorization": "Bearer {}".format(token)
}
data = {
    "starred" : true
}

r = requests.post("https://api.live.welkincloud.io/gh/sb-demo/sms/4fb7f28d-91ca-4f89-bad2-f43ed41ed6bb", 
  json=data, headers=h)
```

> The above request returns JSON structured like this:

```json
{
  "id": "92c6f2c6-61b7-46ad-b1a8-3ca541b88c0f",
  "sendNow": false,
  "scheduledAt": "2021-05-04T19:50:09.808Z",
  "sentAt": "2021-05-04T19:50:11.234Z",
  "receivedAt": null,
  "date": "2021-05-04T19:50:11.234Z",
  "careTeam": "Nick Snow",
  "patientInfo": "John Doe",
  "timezone": "America/Los_Angeles",
  "sender": "de23c848-65aa-45a1-bf7b-f1d36a6e4ebe",
  "from": "+15625345699",
  "receiver": "8b676172-78f8-4cc6-b105-5329c8a58ef2",
  "to": "+15625345678",
  "direction": "OUT",
  "externalId": "SM993260f0b8744163ae3a56ce9d158a05",
  "starred": true,
  "senderName": "Nick Snow",
  "receiverName": "John Doe",
  "message": "sms message",
  "parts" : 1,
  "status": "DELIVERED"
}
```

## Update sms. Assign to patient

`URL Structure: {{url}} / {{tenantName}} / {{instanceName}} / sms / {{uuid}}`

> ***PUT request. Assign to patient***

```python
import requests
h = {
    "Authorization": "Bearer {}".format(token)
}
data = {
    "sender" : de23c848-65aa-45a1-bf7b-f1d36a6e4ebe
}

r = requests.post("https://api.live.welkincloud.io/gh/sb-demo/sms/4fb7f28d-91ca-4f89-bad2-f43ed41ed6bb", 
  json=data, headers=h)
```

> The above request returns JSON structured like this:

```json
{
  "id": "4fb7f28d-91ca-4f89-bad2-f43ed41ed6bb",
  "sendNow": false,
  "scheduledAt": "2021-05-04T19:50:09.808Z",
  "sentAt": "2021-05-04T19:50:11.234Z",
  "receivedAt": null,
  "date": "2021-05-04T19:50:11.234Z",
  "careTeam": "Nick Snow",
  "patientInfo": "John Doe",
  "timezone": "America/Los_Angeles",
  "sender": "de23c848-65aa-45a1-bf7b-f1d36a6e4ebe",
  "from": "+15625345699",
  "receiver": "8b676172-78f8-4cc6-b105-5329c8a58ef2",
  "to": "+15625345678",
  "direction": "OUT",
  "externalId": "SM993260f0b8744163ae3a56ce9d158a05",
  "starred": true,
  "senderName": "Nick Snow",
  "receiverName": "John Doe",
  "message": "sms message",
  "parts" : 1,
  "status": "DELIVERED"
}
```


## Update sms. Full update when [SCHEDULED]

`URL Structure: {{url}} / {{tenantName}} / {{instanceName}} / sms / {{uuid}}`

> ***PUT request. Full update when [SCHEDULED]***

```python
import requests
h = {
    "Authorization": "Bearer {}".format(token)
}
data = {
    "message": "Hi dear patient!",
    "sendNow": true,
    "receiver": "8b676172-78f8-4cc6-b105-5329c8a58ef2"
}

r = requests.post("https://api.live.welkincloud.io/gh/sb-demo/sms/4fb7f28d-91ca-4f89-bad2-f43ed41ed6bb", 
  json=data, headers=h)
```

> The above request returns JSON structured like this:

```json
{
  "id": "4fb7f28d-91ca-4f89-bad2-f43ed41ed6bb",
  "sendNow": false,
  "scheduledAt": "2021-05-04T19:50:09.808Z",
  "sentAt": "2021-05-04T19:50:11.234Z",
  "receivedAt": null,
  "date": "2021-05-04T19:50:11.234Z",
  "careTeam": "Nick Snow",
  "patientInfo": "John Doe",
  "timezone": "America/Los_Angeles",
  "sender": "de23c848-65aa-45a1-bf7b-f1d36a6e4ebe",
  "from": "+15625345699",
  "receiver": "8b676172-78f8-4cc6-b105-5329c8a58ef2",
  "to": "+15625345678",
  "direction": "OUT",
  "externalId": "SM993260f0b8744163ae3a56ce9d158a05",
  "starred": true,
  "senderName": "Nick Snow",
  "receiverName": "John Doe",
  "message": "Hi dear patient!",
  "parts" : 1,
  "status": "DELIVERED"
}
```
## Delete sms

`URL Structure: {{url}} / {{tenantName}} / {{instanceName}} / sms / {{uuid}}`

***Note*** Sms could be deleted only in statuses [SCHEDULED, UNRECOGNISED]

> ***DELETE request***

```python
import requests
h = {
        "Authorization": "Bearer {}".format(token)
    }

r = requests.get("https://api.live.welkincloud.io/gh/sb-demo/sms/4fb7f28d-91ca-4f89-bad2-f43ed41ed6bb", headers=h)
print(r.json())
```
