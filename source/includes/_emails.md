# Emails

`URL Structure: {{url}} / {{tenantName}} / {{instanceName}} / emails`

in our example it would be:

`https://api.live.welkincloud.io/gh/sb-demo/emails`

## Get all emails

> ***GET request***

```python
import requests
h = {
        "Authorization": "Bearer {}".format(token)
    }

r = requests.get("https://api.live.welkincloud.io/gh/sb-demo/emails", headers=h)
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
      "from": "n.snow@dev.welkincloud.io",
      "receiver": "830b8744-2c0f-4750-ad6d-5c2c94ada65d",
      "to": "j.doe@gmail.com",
      "direction": "OUT",
      "externalId": "20210504195011.1.4A9919421A983FF7@dev.welkincloud.io",
      "starred": false,
      "senderName": "Nick Snow",
      "receiverName": "John Doe",
      "subject": "Email subject",
      "body": "Email body.",
      "status": "DELIVERED",
      "secure": false,
      "attachments": null
    }
    ....pagination links omitted
  ]
}
```

Following Query Parameters can be used to sort or find approporiately
 
We can use any combination of this parameters in single request: Example: {{url}}/{{tenantName}}/{{instanceName}}/emails?status=DELIVERED, FAILED&email=some-email@email.com&starred=true

Parameter | Description | Examples
--------- | ----------- | --------
sort |Allows one to specify the sort order of the returned emails collection | https://api.live.welkincloud.io/gh/sb-demo/emails?sort=firstName,desc
size |When specified, size per page | https://api.live.welkincloud.io/gh/sb-demo/emails?size=20
page |When specified, page number | https://api.live.welkincloud.io/gh/sb-demo/emails?page=1
search |When specified, will execute a search based on subject and body fields | https://api.live.welkincloud.io/gh/sb-demo/emails?search=sometext
sender |When specified, search by sender id | https://api.live.welkincloud.io/gh/sb-demo/emails?sender=de23c848-65aa-45a1-bf7b-f1d36a6e4ebe
receiver |When specified, search by receiver id | https://api.live.welkincloud.io/gh/sb-demo/emails?sender=de23c848-65aa-45a1-bf7b-f1d36a6e4ebe
direction |When specified, search by direction (IN or OUT) | https://api.live.welkincloud.io/gh/sb-demo/emails?direction=IN
starred |When specified, search by starred (boolean value) field (as an important email) | https://api.live.welkincloud.io/gh/sb-demo/emails?starred=true
from |When specified, search by 'from' email | https://api.live.welkincloud.io/gh/sb-demo/emails?from=test@gmail.com
to |When specified, search by 'to' email | https://api.live.welkincloud.io/gh/sb-demo/emails?to=test@gmail.com
email |When specified, search by 'to' or 'from' email | https://api.live.welkincloud.io/gh/sb-demo/emails?email=test@gmail.com
senderName |When specified, search by sender name | https://api.live.welkincloud.io/gh/sb-demo/emails?senderName=Jon doe
receiverName |When specified, search by receiver name | https://api.live.welkincloud.io/gh/sb-demo/emails?receiverName=Jon doe
status |When specified, search by status [SCHEDULED, ACCEPTED, DELIVERED, REJECTED, FAILED, UNRECOGNISED]| https://api.live.welkincloud.io/gh/sb-demo/emails?status=DELIVERED

## Get email by id

`URL Structure: {{url}} / {{tenantName}} / {{instanceName}} / emails / {{uuid}}`

> ***GET request***

```python
import requests
h = {
        "Authorization": "Bearer {}".format(token)
    }

r = requests.get("https://api.live.welkincloud.io/gh/sb-demo/emails/92c6f2c6-61b7-46ad-b1a8-3ca541b88c0f", headers=h)
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
  "from": "n.snow@dev.welkincloud.io",
  "receiver": "830b8744-2c0f-4750-ad6d-5c2c94ada65d",
  "to": "j.doe@gmail.com",
  "direction": "OUT",
  "externalId": "20210504195011.1.4A9919421A983FF7@dev.welkincloud.io",
  "starred": false,
  "senderName": "Nick Snow",
  "receiverName": "John Doe",
  "subject": "Email subject",
  "body": "Email body.",
  "status": "DELIVERED",
  "secure": false,
  "attachments": null
}
```

## Send an email

Creates email record and send it with one of the email service (Mailgun or paubox for secure email).

***Note***: Welkonnect module should be configured

## Send a basic email
***Note***: Configuration for Mailgun email service should be added.

`URL Structure: {{url}} / {{tenantName}} / {{instanceName}} / emails`

> ***POST request. Send basic email***

```python
import requests
h = {
    "Authorization": "Bearer {}".format(token)
}
data = {
    "subject" : "Email subject",
    "body" : "Testing.",
    "receiver" : "830b8744-2c0f-4750-ad6d-5c2c94ada65d",
    "sendNow": true
}

r = requests.post("https://api.live.welkincloud.io/gh/sb-demo/emails", 
  json=data, headers=h)
```

> The above request returns JSON structured like this:

```json
{
    "id": "4fb7f28d-91ca-4f89-bad2-f43ed41ed6bb",
    "sendNow": false,
    "scheduledAt": "2021-05-04T20:08:24.427Z",
    "sentAt": "2021-05-04T20:08:24.773Z",
    "receivedAt": null,
    "date": "2021-05-04T20:08:24.773Z",
    "careTeam": "Nick Snow",
    "patientInfo": "John Doe",
    "timezone": "America/Los_Angeles",
    "sender": "de23c848-65aa-45a1-bf7b-f1d36a6e4ebe",
    "from": "n.snow@dev.welkincloud.io",
    "receiver": "830b8744-2c0f-4750-ad6d-5c2c94ada65d",
    "to": "j.doe@gmail.com",
    "direction": "OUT",
    "externalId": "20210504200824.1.8E4ECC1A01B8F746@dev.welkincloud.io",
    "starred": false,
    "senderName": "Nick Snow",
    "receiverName": "John Doe",
    "subject": "Email subject",
    "body": "Testing.",
    "status": "ACCEPTED",
    "secure": false,
    "attachments": null
}
```

## Send a secure email

`URL Structure: {{url}} / {{tenantName}} / {{instanceName}} / emails`

***Note***: Configuration for Paubox email service should be added.

> ***POST request. Send secure email***

```python
import requests
h = {
    "Authorization": "Bearer {}".format(token)
}
data = {
    "subject" : "Email subject",
    "body" : "Testing.",
    "receiver" : "830b8744-2c0f-4750-ad6d-5c2c94ada65d",
    "sendNow": true,
    "secure" : true
}

r = requests.post("https://api.live.welkincloud.io/gh/sb-demo/emails", 
  json=data, headers=h)
```

> The above request returns JSON structured like this:

```json
{
    "id": "4fb7f28d-91ca-4f89-bad2-f43ed41ed6bb",
    "sendNow": false,
    "scheduledAt": "2021-05-04T20:08:24.427Z",
    "sentAt": "2021-05-04T20:08:24.773Z",
    "receivedAt": null,
    "date": "2021-05-04T20:08:24.773Z",
    "careTeam": "Nick Snow",
    "patientInfo": "John Doe",
    "timezone": "America/Los_Angeles",
    "sender": "de23c848-65aa-45a1-bf7b-f1d36a6e4ebe",
    "from": "n.snow@dev.welkincloud.io",
    "receiver": "830b8744-2c0f-4750-ad6d-5c2c94ada65d",
    "to": "j.doe@gmail.com",
    "direction": "OUT",
    "externalId": "c791efaa-add0-11eb-8529-0242ac130003",
    "starred": false,
    "senderName": "Nick Snow",
    "receiverName": "John Doe",
    "subject": "Email subject",
    "body": "Testing.",
    "status": "ACCEPTED",
    "secure": true,
    "attachments": null
}
```

## Send email with attachments

`URL Structure: {{url}} / {{tenantName}} / {{instanceName}} / emails`

***Note***: Attachments will be stored in S3 bucket.

> ***POST request. Send secure email***

```python
import requests
h = {
    "Authorization": "Bearer {}".format(token),
    "Content-Type": multipart_data.content_type
}
multipart_data = MultipartEncoder(
    fields={
            'attachmentsAsFiles': ('file.py', open('file.zip', 'rb'), 'text/plain')
            'subject': 'subject', 
            'body': 'body',
            'receiver': '2f45e174-add6-11eb-8529-0242ac130003',
            'sendNow': 'true'
           }
    )

r = requests.post("https://api.live.welkincloud.io/gh/sb-demo/emails", 
  data=multipart_data, headers=h)
```

> The above request returns JSON structured like this:

```json
{
    "id": "4fb7f28d-91ca-4f89-bad2-f43ed41ed6bb",
    "sendNow": false,
    "scheduledAt": "2021-05-04T20:08:24.427Z",
    "sentAt": "2021-05-04T20:08:24.773Z",
    "receivedAt": null,
    "date": "2021-05-04T20:08:24.773Z",
    "careTeam": "Nick Snow",
    "patientInfo": "John Doe",
    "timezone": "America/Los_Angeles",
    "sender": "de23c848-65aa-45a1-bf7b-f1d36a6e4ebe",
    "from": "n.snow@dev.welkincloud.io",
    "receiver": "830b8744-2c0f-4750-ad6d-5c2c94ada65d",
    "to": "j.doe@gmail.com",
    "direction": "OUT",
    "externalId": "c791efaa-add0-11eb-8529-0242ac130003",
    "starred": false,
    "senderName": "Nick Snow",
    "receiverName": "John Doe",
    "subject": "subject",
    "body": "body",
    "status": "DELIVERED",
    "secure": true,
    "attachments": null
}
```

## Update email

Updating an email could have different behaviour, depending on email status.

1. When email was sent, and it has direction = OUT (user sent it to patient),
it can have one of following status [ACCEPTED, DELIVERED, REJECTED, FAILED]
In this case, we can only update 'starred' field and mark this email as an important

2. When, email direction = IN (patient sent email to user), we can assign this email to another patient manually. 
   
3. When email has status [SCHEDULED]. We can do full update of this email

## Update email. Mark as an important email

`URL Structure: {{url}} / {{tenantName}} / {{instanceName}} / emails / {{uuid}}`

> ***PUT request. Mark as an important email***

```python
import requests
h = {
    "Authorization": "Bearer {}".format(token)
}
data = {
    "starred" : true
}

r = requests.post("https://api.live.welkincloud.io/gh/sb-demo/emails/4fb7f28d-91ca-4f89-bad2-f43ed41ed6bb", 
  json=data, headers=h)
```

> The above request returns JSON structured like this:

```json
{
    "id": "4fb7f28d-91ca-4f89-bad2-f43ed41ed6bb",
    "sendNow": false,
    "scheduledAt": "2021-05-04T20:08:24.427Z",
    "sentAt": "2021-05-04T20:08:24.773Z",
    "receivedAt": null,
    "date": "2021-05-04T20:08:24.773Z",
    "careTeam": "Nick Snow",
    "patientInfo": "John Doe",
    "timezone": "America/Los_Angeles",
    "sender": "de23c848-65aa-45a1-bf7b-f1d36a6e4ebe",
    "from": "n.snow@dev.welkincloud.io",
    "receiver": "830b8744-2c0f-4750-ad6d-5c2c94ada65d",
    "to": "j.doe@gmail.com",
    "direction": "OUT",
    "externalId": "c791efaa-add0-11eb-8529-0242ac130003",
    "starred": true,
    "senderName": "Nick Snow",
    "receiverName": "John Doe",
    "subject": "Email subject",
    "body": "Testing.",
    "status": "DELIVERED",
    "secure": true,
    "attachments": null
}
```

## Update email. Assign to patient

`URL Structure: {{url}} / {{tenantName}} / {{instanceName}} / emails / {{uuid}}`

> ***PUT request. Assign to patient***

```python
import requests
h = {
    "Authorization": "Bearer {}".format(token)
}
data = {
    "sender" : de23c848-65aa-45a1-bf7b-f1d36a6e4ebe
}

r = requests.post("https://api.live.welkincloud.io/gh/sb-demo/emails/4fb7f28d-91ca-4f89-bad2-f43ed41ed6bb", 
  json=data, headers=h)
```

> The above request returns JSON structured like this:

```json
{
    "id": "4fb7f28d-91ca-4f89-bad2-f43ed41ed6bb",
    "sendNow": false,
    "scheduledAt": "2021-05-04T20:08:24.427Z",
    "sentAt": "2021-05-04T20:08:24.773Z",
    "receivedAt": null,
    "date": "2021-05-04T20:08:24.773Z",
    "careTeam": "Nick Snow",
    "patientInfo": "John Doe",
    "timezone": "America/Los_Angeles",
    "sender": "de23c848-65aa-45a1-bf7b-f1d36a6e4ebe",
    "from": "n.snow@dev.welkincloud.io",
    "receiver": "830b8744-2c0f-4750-ad6d-5c2c94ada65d",
    "to": "j.doe@gmail.com",
    "direction": "OUT",
    "externalId": "c791efaa-add0-11eb-8529-0242ac130003",
    "starred": true,
    "senderName": "Nick Snow",
    "receiverName": "John Doe",
    "subject": "Email subject",
    "body": "Testing.",
    "status": "DELIVERED",
    "secure": true,
    "attachments": null
}
```


## Update email. Full update when [SCHEDULED]

`URL Structure: {{url}} / {{tenantName}} / {{instanceName}} / emails / {{uuid}}`

> ***PUT request. Full update when [SCHEDULED]***

```python
import requests
h = {
    "Authorization": "Bearer {}".format(token)
}
data = {
    "subject" : "New Email subject",
    "body" : "new Testing.",
    "receiver" : "830b8744-2c0f-4750-ad6d-5c2c94ada65d",
    "scheduledAt": "2021-05-04T20:08:24.427Z",
    "secure" : true
}

r = requests.post("https://api.live.welkincloud.io/gh/sb-demo/emails/4fb7f28d-91ca-4f89-bad2-f43ed41ed6bb", 
  json=data, headers=h)
```

> The above request returns JSON structured like this:

```json
{
    "id": "4fb7f28d-91ca-4f89-bad2-f43ed41ed6bb",
    "sendNow": false,
    "scheduledAt": "2021-05-04T20:08:24.427Z",
    "sentAt": null,
    "receivedAt": null,
    "date": null,
    "careTeam": "Nick Snow",
    "patientInfo": "John Doe",
    "timezone": "America/Los_Angeles",
    "sender": "de23c848-65aa-45a1-bf7b-f1d36a6e4ebe",
    "from": "n.snow@dev.welkincloud.io",
    "receiver": "830b8744-2c0f-4750-ad6d-5c2c94ada65d",
    "to": "j.doe@gmail.com",
    "direction": "OUT",
    "externalId": "c791efaa-add0-11eb-8529-0242ac130003",
    "starred": true,
    "senderName": "Nick Snow",
    "receiverName": "John Doe",
    "subject": "New Email subject",
    "body": "New Testing.",
    "status": "SCHEDULED",
    "secure": true,
    "attachments": null
}
```

## Delete email

`URL Structure: {{url}} / {{tenantName}} / {{instanceName}} / emails / {{uuid}}`

***Note*** Email could be deleted only in statuses [SCHEDULED, UNRECOGNISED]

> ***DELETE request***

```python
import requests
h = {
        "Authorization": "Bearer {}".format(token)
    }

r = requests.get("https://api.live.welkincloud.io/gh/sb-demo/emails/4fb7f28d-91ca-4f89-bad2-f43ed41ed6bb", headers=h)
print(r.json())
```

