## POST /api/v2/login
Logs in a user with specified credentials.

* **Permissions:** N/A
* **Authentication:** false

### Parameters:
``` JSON
{
    "username": "{String} Username",
    "password": "{String} Plaintext password",
    "secondAuth": {
        "{Object|Optional} Second auth object"
    }
}
```

### Returns:
``` JSON
{
    "SID": "{String} 7IxFfGBOzXYt8UZiobp2g3p",
    "user": {
        "{Object} User object"
    }
}
```

#### Object definition:
* [Second auth object](objects/#second-auth-object)
* [User object](objects/#user-object)

### Errors:
Error name | Description
--- | ---
EINVALID | Invalid username
EINVALID | Invalid password
EINVALID | Second auth failed

### Other:
Sets a cookie called `SID`, containing the created session. This is the same ID as returned in JSON.
