# RFR-API
## Administrators
FIXME

### Attributes
<table>
  <tr>
    <th>Name</th>
    <th>Type</th>
    <th>Description</th>
    <th>Example</th>
  </tr>
  <tr>
    <td><strong>created_at</strong></td>
    <td><em>date-time</em></td>
    <td>when administrators was created</td>
    <td><code>"2012-01-01T12:00:00Z"</code></td>
  </tr>
  <tr>
    <td><strong>id</strong></td>
    <td><em>uuid</em></td>
    <td>unique identifier of administrators</td>
    <td><code>"01234567-89ab-cdef-0123-456789abcdef"</code></td>
  </tr>
  <tr>
    <td><strong>updated_at</strong></td>
    <td><em>date-time</em></td>
    <td>when administrators was updated</td>
    <td><code>"2012-01-01T12:00:00Z"</code></td>
  </tr>
</table>

### Administrators Create
Create a new administrators.

```
POST /administratorss
```


#### Curl Example
```term
$ curl -n -X POST https://api.hello.com/administratorss
```

#### Response Example
```
HTTP/1.1 201 Created
```
```javascript```
{
  "created_at": "2012-01-01T12:00:00Z",
  "id": "01234567-89ab-cdef-0123-456789abcdef",
  "updated_at": "2012-01-01T12:00:00Z"
}
```
### Administrators Delete
Delete an existing administrators.

```
DELETE /administratorss/{administrators_id}
```


#### Curl Example
```term
$ curl -n -X DELETE https://api.hello.com/administratorss/$ADMINISTRATORS_ID
```

#### Response Example
```
HTTP/1.1 200 OK
```
```javascript```
{
  "created_at": "2012-01-01T12:00:00Z",
  "id": "01234567-89ab-cdef-0123-456789abcdef",
  "updated_at": "2012-01-01T12:00:00Z"
}
```
### Administrators Info
Info for existing administrators.

```
GET /administratorss/{administrators_id}
```


#### Curl Example
```term
$ curl -n -X GET https://api.hello.com/administratorss/$ADMINISTRATORS_ID
```

#### Response Example
```
HTTP/1.1 200 OK
```
```javascript```
{
  "created_at": "2012-01-01T12:00:00Z",
  "id": "01234567-89ab-cdef-0123-456789abcdef",
  "updated_at": "2012-01-01T12:00:00Z"
}
```
### Administrators List
List existing administratorss.

```
GET /administratorss
```


#### Curl Example
```term
$ curl -n -X GET https://api.hello.com/administratorss
```

#### Response Example
```
HTTP/1.1 200 OK
```
```javascript```
[
  {
    "created_at": "2012-01-01T12:00:00Z",
    "id": "01234567-89ab-cdef-0123-456789abcdef",
    "updated_at": "2012-01-01T12:00:00Z"
  }
]
```
### Administrators Update
Update an existing administrators.

```
PATCH /administratorss/{administrators_id}
```


#### Curl Example
```term
$ curl -n -X PATCH https://api.hello.com/administratorss/$ADMINISTRATORS_ID
```

#### Response Example
```
HTTP/1.1 200 OK
```
```javascript```
{
  "created_at": "2012-01-01T12:00:00Z",
  "id": "01234567-89ab-cdef-0123-456789abcdef",
  "updated_at": "2012-01-01T12:00:00Z"
}
```

## Users
FIXME

### Attributes
<table>
  <tr>
    <th>Name</th>
    <th>Type</th>
    <th>Description</th>
    <th>Example</th>
  </tr>
  <tr>
    <td><strong>created_at</strong></td>
    <td><em>date-time</em></td>
    <td>when users was created</td>
    <td><code>"2012-01-01T12:00:00Z"</code></td>
  </tr>
  <tr>
    <td><strong>id</strong></td>
    <td><em>uuid</em></td>
    <td>unique identifier of users</td>
    <td><code>"01234567-89ab-cdef-0123-456789abcdef"</code></td>
  </tr>
  <tr>
    <td><strong>updated_at</strong></td>
    <td><em>date-time</em></td>
    <td>when users was updated</td>
    <td><code>"2012-01-01T12:00:00Z"</code></td>
  </tr>
</table>

### Users Create
Create a new users.

```
POST /userss
```


#### Curl Example
```term
$ curl -n -X POST https://api.hello.com/userss
```

#### Response Example
```
HTTP/1.1 201 Created
```
```javascript```
{
  "created_at": "2012-01-01T12:00:00Z",
  "id": "01234567-89ab-cdef-0123-456789abcdef",
  "updated_at": "2012-01-01T12:00:00Z"
}
```
### Users Delete
Delete an existing users.

```
DELETE /userss/{users_id}
```


#### Curl Example
```term
$ curl -n -X DELETE https://api.hello.com/userss/$USERS_ID
```

#### Response Example
```
HTTP/1.1 200 OK
```
```javascript```
{
  "created_at": "2012-01-01T12:00:00Z",
  "id": "01234567-89ab-cdef-0123-456789abcdef",
  "updated_at": "2012-01-01T12:00:00Z"
}
```
### Users Info
Info for existing users.

```
GET /userss/{users_id}
```


#### Curl Example
```term
$ curl -n -X GET https://api.hello.com/userss/$USERS_ID
```

#### Response Example
```
HTTP/1.1 200 OK
```
```javascript```
{
  "created_at": "2012-01-01T12:00:00Z",
  "id": "01234567-89ab-cdef-0123-456789abcdef",
  "updated_at": "2012-01-01T12:00:00Z"
}
```
### Users List
List existing userss.

```
GET /userss
```


#### Curl Example
```term
$ curl -n -X GET https://api.hello.com/userss
```

#### Response Example
```
HTTP/1.1 200 OK
```
```javascript```
[
  {
    "created_at": "2012-01-01T12:00:00Z",
    "id": "01234567-89ab-cdef-0123-456789abcdef",
    "updated_at": "2012-01-01T12:00:00Z"
  }
]
```
### Users Update
Update an existing users.

```
PATCH /userss/{users_id}
```


#### Curl Example
```term
$ curl -n -X PATCH https://api.hello.com/userss/$USERS_ID
```

#### Response Example
```
HTTP/1.1 200 OK
```
```javascript```
{
  "created_at": "2012-01-01T12:00:00Z",
  "id": "01234567-89ab-cdef-0123-456789abcdef",
  "updated_at": "2012-01-01T12:00:00Z"
}
```


