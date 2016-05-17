# Login endpoints

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

## DELETE /api/v2/login
Logs out the user, invalidates the session.

* **Permissions:** N/A
* **Authentication:** true

### Returns:
``` JSON
{ }
```
## POST /api/v2/login/lock
Locks the current session. Need to [unlock](#delete-apiv2loginlock) before reusing the session. There is a limit to when it can be unlocked.

* **Permissions:** N/A
* **Authentication:** true

### Returns:
``` JSON
{
    "maxUnlock": "{Date} Maximal date till the locked session is expired and removed."
}
```

## DELETE /api/v2/login/lock
Unlocks a locked session. This needs to be done before the session expires.

* **Permissions:** N/A
* **Authentication:** true

### Parameters:
``` JSON
{
    "password": "{String} Plaintext password"
}
```

### Returns:
``` JSON
{ }
```

### Errors:
Error name | Description
--- | ---
EDENIED | Session expired.
