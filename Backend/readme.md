# Backend API Documentation

## User Registration -- /users/register endpoint

### HTTP Method
POST 

Registers a new user in the system.

### Request Body

```json
{
  "fullname": {
    "firstname": "string", // required, min 3 characters
    "lastname": "string" // optional, min 3 characters if provided
  },
  "email": "string", // required, valid email format
  "password": "string" // required, min 6 characters
}
```

### Response

#### Success Response

- **Code:** 201 CREATED

```json
{
  "token": "jwt-token-string",
  "user": {
    "_id": "mongodb-generated-id",
    "fullname": {
      "firstname": "string",
      "lastname": "string"
    },
    "email": "string"
  }
}
```

#### Error Response

- **Code:** 400 BAD REQUEST

```json
{
  "errors": [
    {
      "msg": "Invalid Email",
      "param": "email",
      "location": "body"
    },
    {
      "msg": "First name must be at least 3 characters long.",
      "param": "fullname.firstname",
      "location": "body"
    },
    {
      "msg": "Password must be at least 6 characters long.",
      "param": "password",
      "location": "body"
    }
  ]
}
```

### Validation Rules

- Email must be valid
- First name must be at least 3 characters long
- Password must be at least 6 characters long
- Last name, if provided, must be at least 3 characters long

### Security

- Password is hashed using bcrypt before storage
- JWT token is generated upon successful registration
