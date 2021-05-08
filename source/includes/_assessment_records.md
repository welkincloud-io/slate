# Assessment records

## Get all assessment records

To get all assessment records would be used at the following URL

`URL Structure: https://api.live.welkincloud.io/{tenantName}/{instanceName}/patients/{}/assessment-records`

1. First variable is your Tenant name. We will use **gh** as a tenant name through this set of api docs
2. Second variable is your Instance name. We will use **sb-demo** as an instance name through this set of api docs
3. Third variable is uuid ogf the patient whose records we want to receive

Example request:

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patients/ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8/assessments-records`
3. HTTP Response Codes: 200

## Get an assessment record

To get an assessment record would be used at the following URL

`URL Structure: https://api.live.welkincloud.io/{tenantName}/{instanceName}/patients/{}/assessment-records/{}`

1. First variable is your Tenant name. We will use **gh** as a tenant name through this set of api docs
2. Second variable is your Instance name. We will use **sb-demo** as an instance name through this set of api docs
3. Third variable is uuid of the patient whose records we want to receive
4. Fourth variable is uuid of the records which we want to receive

Example request:

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patients/ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8/assessments-records/some-uuid`
3. HTTP Response Codes: 200, 404

## Create an assessment record

To create an assessment record would be used at the following URL

`URL Structure: https://api.live.welkincloud.io/{tenantName}/{instanceName}/patients/{}/assessment-records`

1. First variable is your Tenant name. We will use **gh** as a tenant name through this set of api docs
2. Second variable is your Instance name. We will use **sb-demo** as an instance name through this set of api docs
3. Third variable is uuid of the patient for whom we want to create the record

Example request:

1. HTTP Method: POST
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patients/ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8/assessments-records/some-uuid`
3. HTTP Response Codes: 200, 404

## Update an assessment record

To update an assessment record would be used at the following URL

`URL Structure: https://api.live.welkincloud.io/{tenantName}/{instanceName}/patients/{}/assessment-records/{}`

1. First variable is your Tenant name. We will use **gh** as a tenant name through this set of api docs
2. Second variable is your Instance name. We will use **sb-demo** as an instance name through this set of api docs
3. Third variable is uuid of the patient for whom we want to update the record
4. Fourth variable is uuid of record which we want to update

Example request:

1. HTTP Method: PUT
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patients/ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8/assessments-records/some-uuid`
3. HTTP Response Codes: 200, 404

## Update answers of assessment record

To update answers of assessment record would be used at the following URL

`URL Structure: https://api.live.welkincloud.io/{tenantName}/{instanceName}/patients/{}/assessment-records/{}/answers`

1. First variable is your Tenant name. We will use **gh** as a tenant name through this set of api docs
2. Second variable is your Instance name. We will use **sb-demo** as an instance name through this set of api docs
3. Third variable is uuid of the patient for whom we want to update the record
4. Fourth variable is uuid of record whose answers we want to update

Example request:

1. HTTP Method: PUT
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patients/ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8/assessments-records/some-uuid/answers`
3. HTTP Response Codes: 200, 404

## Delete an assessment record

To delete an assessment record would be used at the following URL

`URL Structure: https://api.live.welkincloud.io/{tenantName}/{instanceName}/patients/{}/assessment-records/{}`

1. First variable is your Tenant name. We will use **gh** as a tenant name through this set of api docs
2. Second variable is your Instance name. We will use **sb-demo** as an instance name through this set of api docs
3. Third variable is uuid of the patient for whom we want to update the record
4. Fourth variable is uuid of record which we want to delete

Example request:

1. HTTP Method: DELETE
2. HTTP URL: `https://api.live.welkincloud.io/gh/sb-demo/patients/ee66e8e8-6ce1-40d3-b6cb-e5727c5347c8/assessments-records/some-uuid`
3. HTTP Response Codes: 200, 404


