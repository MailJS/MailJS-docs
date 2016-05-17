# Object definitions

Here are the repeating objects defined.

## User object
``` JSON
{
	"username": "{String} Login name of the user",
	"_id": "{MongoID} Unique id of the user."
}
```

## Second auth object
``` JSON
{
	"type": "{String} Type of second auth. Accepting TOTP or recovery",
	"value": "{(String|Number)} Second auth key value. Type depends on the type of second auth."
}
```
