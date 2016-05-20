# User endpoints

## GET /api/v2/user/avatar/{username}
Get the avatar of a user.

* **Permissions:** N/A
* **Authentication:** false

### URL Parameters:
Parameter | Description
--- | ---
username | MD5 of the user to get the avatar for.

### Returns:
``` PNG
{Raw png image}
```

### Errors:
Error name | Description
--- | ---
ENOTFOUND | User not found.
