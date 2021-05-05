# Authentication

> To obtain a Bearer token:

```python
import requests

params = {'secret': '+}B{KGTG6#zG%P;tQm0C'}
r = requests.post('https://api.live.welkincloud.io/gh/admin/api_clients/VBOPNRYRWJIP', json=params)
print(r.json())
```

> Successful response will look like:

```json
{
  "clientName": "VBOPNRYRWJIP",
  "token": "eyJraWQiOiJvaGloUEZOREk2WmE5WEtXNEVIdTdVaFFob1l3Ull0aFFFMmpIY1MrczZrPSIsImFsZyI6IlJTMjU2In0.eyJjdXN0b206dHlwZSI6IkFQSV9DTElFTlQiLCJzdWIiOiIzZWQyMjNjOS1hNjFmLTRmMDktOGUzMi0wNGRkNjU2NDY2YzQiLCJhdWQiOiIycTJ0YmRnanV0Y3Zqdjg5NGY0Zm4wcXRnMCIsImV2ZW50X2lkIjoiMWVmYTc4MWItMzMzNy00MWI4LWExZjYtNTlmY2ZmYWYzMjgxIiwidG9rZW5fdXNlIjoiaWQiLCJhdXRoX3RpbWUiOjE2MTUyMjg0MjcsImlzcyI6Imh0dHBzOlwvXC9jb2duaXRvLWlkcC51cy1lYXN0LTEuYW1hem9uYXdzLmNvbVwvdXMtZWFzdC0xXzBjOVhLV1pFQSIsImN1c3RvbTppZCI6IjAyZDI0MzU5LTU0ZWYtNGQ4Mi05MmRjLWZiY2RjOTQyNDJjMCIsImNvZ25pdG86dXNlcm5hbWUiOiJNVE5LREdVQUdQVUUiLCJleHAiOjE2MTUyMzIwMjcsImlhdCI6MTYxNTIyODQyN30.ktjPG0CIHP0As8e8I1UGMP1kocvjd4AIeQBZlZ0esMz414Dpsb6gwPNuDhJS-ej_gh_tZNSw4tePdxQcagfJHp64ByOuv3ZtAHPAm5l5dEZOcVxG4l4O45Mn1hIGhqP6vizNVBFlBWTnzYTyPlbJKS2PMeMsWPqxUDKeoEffczr2sb9VptUMg2dgY-vz6VZvZjtpPfWjKjnJHeIVMxUiW-9LcR-6BK2DHj5qwlzOkDs89rnqE_OFMUiyLfQlvQuoglSRUUiXNXGiU88YCNNzzG7fb3luuwFXBAdwWhK7pXM4o355eDp2bH-EFx_q82mJBy7lB0DfZTm1AHHjcn8BXg",
  "enabled": true
}
```

Once you finished the steps, lets review the URL structure that is typically generated for such setup:

`URL Structure: https://api.live.welkincloud.io/{}/admin/api_clients/{}`

There are several variables in this structure:

1. First variable is your Tenant name. We will use **gh** as a tenant name through this set of api docs
2. Second variable is your client name. We will use **VBOPNRYRWJIP** as a api client name


In order to Authenticate in Welkin, one needs to follow few steps:

1. HTTP Method: POST
2. HTTP URL: `https://api.live.welkincloud.io/gh/admin/api_clients/VBOPNRYRWJIP`
3. HTTP Reponse Codes: 201, 400, 500

There are three field in response object:

Field Name | Description | Examples
--------- | ----------- | --------
clientName | Echos back the name of API client you used
token | Bearer token that you will use in subsequent requests
enabled | will indicate if the client is enable. This is also controlled in the Admin app

{{resources/*}}
<%= partial "partial4" %
