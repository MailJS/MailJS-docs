# Welcome to the MailJS API docs.

This API covers all endpoints to use MailJS in your own application. This page covers the general guidlines of the API. Please take a look before proceeding with the actual API.

## Version

MailJS is constantly growing in code. These docs **only supports API v2**. Docs for v1 are not available, because it is obsolite. On every endpoint it is written from which version that specific endpoint has been introduced. Any changes at that specific endpoint is also defined right there.

## Authentication

There are two ways to authenticate in MailJS. It depends on the kind of application you are building which you want to use. Generally it is OAuth 2.0 you want to use.

### User auth.

User authentication is done with a POST request to the login endpoint. When done it gives back a session token. This is used to identify the user and should be supplied at every request, otherwise it will result in a EDENIED error (see [Error Codes](#error-codes)). Supplying of the token is mostly done automatially by a cookie. It is possible to supply the session token manually by setting the `x-token` header. This header has priority over a cookie.

The user has full access to the API, and is not limited by scopes like OAuth does. This is as long as the user has the required permissions to use the endpoint (see [Permissions/Scopes](#permissionsscopes)).

### OAuth 2.0.

Comming soon(tm).

## Permissions/Scopes

MailJS has a advanced permission system. A user is part of at least one group, which has specific permissions. These permissions define which endpoints are acceble for the user.

Scopes are used in [OAuth 2.0](#oauth-20) to limit the power of an application. Scopes behave the same as permissions.

Node | Description | Default
--- | --- | ---
users.view | Able to view all registered users. | false
users.invite | Able to create invitation tokens to invite new users. | false
users.update | Able to update generic information of a user (e.g. full name, birthday). | false
users.update.username | Able to update the username of a user. | false
users.update.password | Able to update the password of a user. | false
users.update.group | Able to update the groups of the user. **Warning!** *Only give this one to super admins. This node basicaly means they have **all** permissions.* | false
users.remove | Able to delete the user. | false
groups.create | Able to create a new group. | false
groups.update | Able to update generic information of a group (e.g. group name, group color). | false
groups.update.permissions | Able to update permission nodes of a user. **Warning!** *Only give this one to super admins. This node basicaly means they have **all** permissions.* | false
groups.remove | Able to delete existing groups. | false
mailbox.create | Able to create new mailboxes. | false
mailbox.invite | Able to create invites to a mailbox. | false
mailbox.removeUser | Able to remove a user from a mailbox. | false
mailbox.purge | Able to delete **all** email assosiated with the mailbox. **Warning!** *Emails of purged mailboxes are lost forever (a long time)!* | false
mailbox.delete | Able to delete a mailbox **Warning!** *Deleted mailboxes are lost forever (a long time)! Contact lists are lost too.* | false
mail.send | Able to send emails. | false
mail.send.external | Able to send emails over SMTP. | false

Mailbox admins have the following permissions of the mailbox:

 * mailbox.invite
 * mailbox.removeUser
 * mailbox.purge
 * mailbox.delete

## Error codes

The API can return a error on a request. Errors are identified with a non 200 response code. Errors are never in 200 response codes. Errors are build in the following format:

``` JSON
{
    "error": {
        "name": "{String} ERRORNAME",
        "message": "{String} Description of the error."
    }
}
```

The `ERRORNAME` string is a predefined string out of the following table:

Errorname | Response code | Description
--- | --- | ---
ENOTFOUND | 404 | The requested object is not found in the database.
EVALIDATION | 400 | User input validation failed. This could be because of a missing or a malformed object.
EINVALID | 400 | Invalid user input, but in the right format. For things like invalid passwords.
EFAILED | 500 | The server failed to compleat the requested task, because of an error.
EDATABASE | 500 | Database error.
EDENIED | 401 | Access to the requested endpoint has been denied.
ELIMIT | 429 | Rate limiter blocked the request. Wait till the limit has been cleared.

**Watch out!** 500 errors are rare, but might or might not follow the defined guildlines! These errors are *always* fatal!

## Thats it!

Now you have covered the basic usage of the API. Pick a subject you want in the sidebar to get started.
