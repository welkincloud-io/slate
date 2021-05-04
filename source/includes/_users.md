# Users

This API allows one to work with User records

## Create User Record

```json     
{
   "username": "johndoe",
   "email": "j.doe@email.com",
   "phone": "+15552009845",
   "timezone": "America/Los_Angeles",
   "firstName": "John",
   "lastName": "Doe",
   "credentials": "MD"
}
```

Users API url consist of the following structure

`https://api.live.welkincloud.io/{}/admin/users`

In our example, the url would be:
`https://api.live.welkincloud.io/gh/admin/users`




1. HTTP Method: POST
2. HTTP URL: `https://api.live.welkincloud.io/gh/admin/users`


## Read User Record

```json     
{
   "username": "johndoe",
   "email": "j.doe@email.com",
   "phone": "+15552009845",
   "timezone": "America/Los_Angeles",
   "firstName": "John",
   "lastName": "Doe",
   "credentials": "MD"
}
```

User Record API url consist of the following structure

`https://api.live.welkincloud.io/{}/admin/users/{}`

In our example, the url would be:
`https://api.live.welkincloud.io/gh/admin/users/johndoe`

1. HTTP Method: GET
2. HTTP URL: `https://api.live.welkincloud.io/gh/admin/users/johndoe`

## Update User Record (Partial update)

```json     
{
   "username": "johndoe",
   "email": "j.doe@email.com",
   "phone": "+15552009845",
   "timezone": "America/Los_Angeles",
   "firstName": "John",
   "lastName": "Doe",
   "credentials": "MD"
}
```

If you with to update some of the user fields, but not all, you can use `PATCH`

1. HTTP Method: PATCH
2. HTTP URL: `https://api.live.welkincloud.io/gh/admin/users/johndoe`


## Update User Record (Full update)

```json     
{
   "username": "johndoe",
   "email": "j.doe@email.com",
   "phone": "+15552009845",
   "timezone": "America/Los_Angeles",
   "firstName": "John",
   "lastName": "Doe",
   "credentials": "MD"
}
```

If you with to update entire User Object, you can use `PUT`

1. HTTP Method: PUT
2. HTTP URL: `https://api.live.welkincloud.io/gh/admin/users/johndoe`


## Delete User Record

1. HTTP Method: DELETE
2. HTTP URL: `https://api.live.welkincloud.io/gh/admin/users/johndoe` 
