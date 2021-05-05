# Documents - Document Summary

Documents are based on CDTs - we have one common system CDT (formation) with name “_document_summary” 
and all document types will be created with a “link” to this summary. So relation between Document Summary 
Record and Document Type Record is one-to-one.

“_document_summary” can’t be edited.

“_document_summary” has such fields set by default:
 - type - it’s the “link” between summary and document types - each created document type will be shown in this list like option.
By default, we have 3 document types: Assessment (name - doc-type-assessment), Docusign (name - doc-type-docusign) and Others (name - doc-type-others).
 - files - for storing document files. Currently, users can upload only jpg, jpeg, png and pdf files.

## Get All Documents Summary Records

```python
import requests
h = {
        "Authorization": "Bearer {}".format(token)
    }

r = requests.get("https://api.live.welkincloud.io/welkonnect/commcenter/patients/ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8/document-summary", headers=h)
print(r.json())
```

> The above request returns JSON structured like this:

```json
{
  "content": [{
    "id": "4a59584c-af30-49c4-8601-b43b4fbeb741",
    "patientId": "ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8",
    "cdtId": "fba56b12-d39b-47d8-9b03-bf4812a481ad",
    "version": 45,
    "jsonBody": {
      "external_guid": null,
      "created_at": "2021-04-30T16:59:05.691Z",
      "source_type": null,
      "external_id": null,
      "type": "doc-type-docusign",
      "created_by_name": "Jon Snow",
      "created_by": "03f51404-a300-4857-b10c-0d6a1a1b88ae",
      "updated_by_name": "Jon Snow",
      "updated_at": "2021-04-30T16:59:27.110Z",
      "updated_by": "03f51404-a300-4857-b10c-0d6a1a1b88ae",
      "files": [{
        "id": "f1941755-41d9-4dc7-b3f6-4f23811fba1c",
        "size": 141826,
        "storageKey": "key",
        "contentType": "application/pdf",
        "originalName": "fileName.pdf"
      }],
      "id": "4a59584c-af30-49c4-8601-b43b4fbeb741",
      "source_id": null,
      "source_name": null
    }
  }]
}
```

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/welkonnect/commcenter/patients/ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8/document-summary`
3. HTTP Response Codes: 200

Following query parameters can be used:

Parameter | Description | Examples
--------- | ----------- | --------
sourceId  | Used for filtering by source id | https://api.live.welkincloud.io/welkonnect/commcenter/patients/ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8/document-summary?sourceId=360a30fb-257f-4bdc-8dc9-9d28f7f7cb69

## Get Document Summary Record By Id

> The above request returns JSON structured like this:

```json
{
  "id": "4a59584c-af30-49c4-8601-b43b4fbeb741",
  "patientId": "ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8",
  "cdtId": "fba56b12-d39b-47d8-9b03-bf4812a481ad",
  "version": 45,
  "jsonBody": {
    "external_guid": null,
    "created_at": "2021-04-30T16:59:05.691Z",
    "source_type": null,
    "external_id": null,
    "type": "doc-type-docusign",
    "created_by_name": "Jon Snow",
    "created_by": "03f51404-a300-4857-b10c-0d6a1a1b88ae",
    "updated_by_name": "Jon Snow",
    "updated_at": "2021-04-30T16:59:27.110Z",
    "updated_by": "03f51404-a300-4857-b10c-0d6a1a1b88ae",
    "files": [{
      "id": "f1941755-41d9-4dc7-b3f6-4f23811fba1c",
      "size": 141826,
      "storageKey": "key",
      "contentType": "application/pdf",
      "originalName": "fileName.pdf"
    }],
    "id": "4a59584c-af30-49c4-8601-b43b4fbeb741",
    "source_id": null,
    "source_name": null
  }
}
```

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/welkonnect/commcenter/patients/ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8/document-summary/4a59584c-af30-49c4-8601-b43b4fbeb741`
3. HTTP Response Codes: 200

## Create Document Summary Record

> The above request returns JSON structured like this:

```json
{
  "id": "4a59584c-af30-49c4-8601-b43b4fbeb741",
  "patientId": "ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8",
  "cdtId": "fba56b12-d39b-47d8-9b03-bf4812a481ad",
  "version": 45,
  "jsonBody": {
    "external_guid": null,
    "created_at": "2021-04-30T16:59:05.691Z",
    "source_type": null,
    "external_id": null,
    "type": "doc-type-docusign",
    "created_by_name": "Jon Snow",
    "created_by": "03f51404-a300-4857-b10c-0d6a1a1b88ae",
    "updated_by_name": "Jon Snow",
    "updated_at": "2021-04-30T16:59:27.110Z",
    "updated_by": "03f51404-a300-4857-b10c-0d6a1a1b88ae",
    "files": [{
      "id": "f1941755-41d9-4dc7-b3f6-4f23811fba1c",
      "size": 141826,
      "storageKey": "key",
      "contentType": "application/pdf",
      "originalName": "fileName.pdf"
    }],
    "id": "4a59584c-af30-49c4-8601-b43b4fbeb741",
    "source_id": null,
    "source_name": null
  }
}
```

1. HTTP Method: POST
2. HTTP URL: `https://api.live.welkincloud.io/welkonnect/commcenter/patients/ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8/document-summary/`
3. HTTP Response Codes: 201

## Update Document Summary Record

> The above request returns JSON structured like this:

```json
{
  "id": "4a59584c-af30-49c4-8601-b43b4fbeb741",
  "patientId": "ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8",
  "cdtId": "fba56b12-d39b-47d8-9b03-bf4812a481ad",
  "version": 45,
  "jsonBody": {
    "external_guid": null,
    "created_at": "2021-04-30T16:59:05.691Z",
    "source_type": null,
    "external_id": null,
    "type": "doc-type-docusign",
    "created_by_name": "Jon Snow",
    "created_by": "03f51404-a300-4857-b10c-0d6a1a1b88ae",
    "updated_by_name": "Jon Snow",
    "updated_at": "2021-04-30T16:59:27.110Z",
    "updated_by": "03f51404-a300-4857-b10c-0d6a1a1b88ae",
    "files": [{
      "id": "f1941755-41d9-4dc7-b3f6-4f23811fba1c",
      "size": 141826,
      "storageKey": "key",
      "contentType": "application/pdf",
      "originalName": "fileName.pdf"
    }],
    "id": "4a59584c-af30-49c4-8601-b43b4fbeb741",
    "source_id": null,
    "source_name": null
  }
}
```

1. HTTP Method: PUT
2. HTTP URL: `https://api.live.welkincloud.io/welkonnect/commcenter/patients/ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8/document-summary/4a59584c-af30-49c4-8601-b43b4fbeb741`
3. HTTP Response Codes: 200

## Delete Document Summary Record

1. HTTP Method: DELETE
2. HTTP URL: `https://api.live.welkincloud.io/welkonnect/commcenter/patients/ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8/document-summary/4a59584c-af30-49c4-8601-b43b4fbeb741`
3. HTTP Response Codes: 200

## Upload Document Summary Record File

> The above request returns JSON structured like this:

```json
[{
  "id": "bcade721-fa3d-46fe-9013-d07033212c6a",
  "originalName": "fileName.png",
  "size": 488030,
  "contentType": "image/png",
  "storageKey": "key"
}]
```

1. HTTP Method: POST
2. HTTP URL: `https://api.live.welkincloud.io/welkonnect/commcenter/patients/ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8/document-summary/4a59584c-af30-49c4-8601-b43b4fbeb741/files`
3. HTTP Response Codes: 201
4. Content-Type: multipart/form-data; 
5. Files should be with key “files” (few files allowed)

## Download Document Summary Record File

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/welkonnect/commcenter/patients/ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8/document-summary/4a59584c-af30-49c4-8601-b43b4fbeb741/files/bcade721-fa3d-46fe-9013-d07033212c6a`
3. HTTP Response Codes: 200
4. Content-Type is taken from file (e.g. image/png, image/jpeg)

# Documents - Document Types

## Get All Documents Types

```python
import requests
h = {
        "Authorization": "Bearer {}".format(token)
    }

r = requests.get("https://api.live.welkincloud.io/welkonnect/commcenter/formations/current/document-types", headers=h)
print(r.json())
```

> The above request returns JSON structured like this:

```json
[{
  "id": "be91b865-d60e-434d-86f8-e47489d75a12",
  "name": "doc-type-assessment",
  "title": "Assessment",
  "label": "Assessment",
  "version": 45,
  "internal": true,
  "readable": true,
  "updatable": true,
  "type": "MULTI_RECORD",
  "relation": "DOCUMENT_TYPE",
  "fields": [{
    "name": "notes",
    "type": "text",
    "dictionary": null,
    "searchable": false,
    "bulkEdit": false,
    "phi": false,
    "meta": {
      "required": false
    }
  }]
}, ...
]
```

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/welkonnect/commcenter/formations/current/document-types`
3. HTTP Response Codes: 200

## Get Document Type By Name

> The above request returns JSON structured like this:

```json
{
  "id": "be91b865-d60e-434d-86f8-e47489d75a12",
  "name": "doc-type-assessment",
  "title": "Assessment",
  "label": "Assessment",
  "version": 45,
  "internal": true,
  "readable": true,
  "updatable": true,
  "type": "MULTI_RECORD",
  "relation": "DOCUMENT_TYPE",
  "fields": [{
    "name": "notes",
    "type": "text",
    "dictionary": null,
    "searchable": false,
    "bulkEdit": false,
    "phi": false,
    "meta": {
      "required": false
    }
  }]
}
```

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/welkonnect/commcenter/formations/current/document-types/doc-type-assessment`
3. HTTP Response Codes: 200

## Create Document Type

> The above request returns JSON structured like this:

```json
{
  "id": "be91b865-d60e-434d-86f8-e47489d75a12",
  "name": "doc-type-assessment",
  "title": "Assessment",
  "label": "Assessment",
  "version": 45,
  "internal": true,
  "readable": true,
  "updatable": true,
  "type": "MULTI_RECORD",
  "relation": "DOCUMENT_TYPE",
  "fields": [{
    "name": "notes",
    "type": "text",
    "dictionary": null,
    "searchable": false,
    "bulkEdit": false,
    "phi": false,
    "meta": {
      "required": false
    }
  }]
}
```

1. HTTP Method: POST
2. HTTP URL: `https://api.live.welkincloud.io/welkonnect/commcenter/formations/current/document-types/`
3. HTTP Response Codes: 201

## Update Document Type

> The above request returns JSON structured like this:

```json
{
  "id": "be91b865-d60e-434d-86f8-e47489d75a12",
  "name": "doc-type-assessment",
  "title": "Assessment",
  "label": "Assessment",
  "version": 45,
  "internal": true,
  "readable": true,
  "updatable": true,
  "type": "MULTI_RECORD",
  "relation": "DOCUMENT_TYPE",
  "fields": [{
    "name": "notes",
    "type": "text",
    "dictionary": null,
    "searchable": false,
    "bulkEdit": false,
    "phi": false,
    "meta": {
      "required": false
    }
  }]
}
```

1. HTTP Method: PUT
2. HTTP URL: `https://api.live.welkincloud.io/welkonnect/commcenter/formations/current/document-types/doc-type-assessment`
3. HTTP Response Codes: 200

## Delete Document Type

1. HTTP Method: DELETE
2. HTTP URL: `https://api.live.welkincloud.io/welkonnect/commcenter/formations/current/document-types/doc-type-assessment`
3. HTTP Response Code: 200

## Get Document Type Record

```python
import requests
h = {
        "Authorization": "Bearer {}".format(token)
    }

r = requests.get("https://api.live.welkincloud.io/welkonnect/commcenter/patients/ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8/document-summary/4a59584c-af30-49c4-8601-b43b4fbeb741/doc-type-docusign`", headers=h)
print(r.json())
```

> The above request returns JSON structured like this:

```json
{
  "id": "cf10883b-8510-4aeb-a7b6-7e3a6e0f0f2d",
  "patientId": "ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8",
  "cdtId": "b34b45b7-18f6-42ee-bd64-26a039205ed1",
  "version": 45,
  "jsonBody": {
    "external_guid": null,
    "notes": "some notes...",
    "created_at": "2021-05-04T16:44:46.623Z",
    "source_type": "DOCUMENT_SUMMARY",
    "external_id": null,
    "created_by_name": null,
    "created_by": "36ba66b6-305c-4664-b343-b2e1dd2dd611",
    "updated_by_name": null,
    "updated_at": "2021-05-04T16:44:46.623Z",
    "updated_by": "36ba66b6-305c-4664-b343-b2e1dd2dd611",
    "id": "cf10883b-8510-4aeb-a7b6-7e3a6e0f0f2d",
    "source_id": "4a59584c-af30-49c4-8601-b43b4fbeb741",
    "source_name": "DOCUMENT_SUMMARY"
  }
}
```

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/welkonnect/commcenter/patients/ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8/document-summary/4a59584c-af30-49c4-8601-b43b4fbeb741/doc-type-docusign`
3. HTTP Response Codes: 200

## Create Document Type Record

> The above request returns JSON structured like this:

```json
{
  "id": "cf10883b-8510-4aeb-a7b6-7e3a6e0f0f2d",
  "patientId": "ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8",
  "cdtId": "b34b45b7-18f6-42ee-bd64-26a039205ed1",
  "version": 45,
  "jsonBody": {
    "external_guid": null,
    "notes": "some notes...",
    "created_at": "2021-05-04T16:44:46.623Z",
    "source_type": "DOCUMENT_SUMMARY",
    "external_id": null,
    "created_by_name": null,
    "created_by": "36ba66b6-305c-4664-b343-b2e1dd2dd611",
    "updated_by_name": null,
    "updated_at": "2021-05-04T16:44:46.623Z",
    "updated_by": "36ba66b6-305c-4664-b343-b2e1dd2dd611",
    "id": "cf10883b-8510-4aeb-a7b6-7e3a6e0f0f2d",
    "source_id": "4a59584c-af30-49c4-8601-b43b4fbeb741",
    "source_name": "DOCUMENT_SUMMARY"
  }
}
```

1. HTTP Method: POST
2. HTTP URL: `https://api.live.welkincloud.io/welkonnect/commcenter/patients/ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8/document-summary/4a59584c-af30-49c4-8601-b43b4fbeb741/doc-type-docusign`
3. HTTP Response Codes: 201

## Update Document Type Record

> The above request returns JSON structured like this:

```json
{
  "id": "cf10883b-8510-4aeb-a7b6-7e3a6e0f0f2d",
  "patientId": "ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8",
  "cdtId": "b34b45b7-18f6-42ee-bd64-26a039205ed1",
  "version": 45,
  "jsonBody": {
    "external_guid": null,
    "notes": "some notes...",
    "created_at": "2021-05-04T16:44:46.623Z",
    "source_type": "DOCUMENT_SUMMARY",
    "external_id": null,
    "created_by_name": null,
    "created_by": "36ba66b6-305c-4664-b343-b2e1dd2dd611",
    "updated_by_name": null,
    "updated_at": "2021-05-04T16:44:46.623Z",
    "updated_by": "36ba66b6-305c-4664-b343-b2e1dd2dd611",
    "id": "cf10883b-8510-4aeb-a7b6-7e3a6e0f0f2d",
    "source_id": "4a59584c-af30-49c4-8601-b43b4fbeb741",
    "source_name": "DOCUMENT_SUMMARY"
  }
}
```

1. HTTP Method: PUT
2. HTTP URL: `https://api.live.welkincloud.io/welkonnect/commcenter/patients/ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8/document-summary/4a59584c-af30-49c4-8601-b43b4fbeb741/doc-type-docusign`
3. HTTP Response Codes: 200

## Delete Document Type Record

1. HTTP Method: DELETE
2. HTTP URL: `https://api.live.welkincloud.io/welkonnect/commcenter/patients/ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8/document-summary/4a59584c-af30-49c4-8601-b43b4fbeb741/doc-type-docusign`
3. HTTP Response Code: 200
