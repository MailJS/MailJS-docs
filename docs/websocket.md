# WebSockets

Websockets are a big part of MailJS, it makes it able to send events to a user, and makes emails available in milliseconds after they reach the MailJS servers. When a client has been authenticated, the server authmatically starts sending trough events. There is no need to subscribe specificly. Please mind that the server does not accept binary. The server will terminate connections with binary enabled.

There are serveral structures of frames, distinctional by the `type` variable. The frames are defined as the following:
### Events (Server only)
``` JSON
{
	"type": "event",
	"eventName": "{String} Event specific",
	"data": "{Object} Event specific"
}
```

### Request (Client only)
``` JSON
{
	"type": "request",
	"": "{String} Event specific",
	"data": "{Object} Request specific",
	"id": "{String | Optional} Message ID, send back by the server in the response. Does not effect request behavior."
}
```

### Response (Server only)
``` JSON
{
	"type": "response",
	"": "{String} Request specific",
	"data": "{Object} Request specific",
	"id": "{String} Message ID, only applicably if send by the client."
}
```

### Error (Server only)
``` JSON
{
	"type": "error",
	"error": "{Error} Object specifying the cause of the error"
}
```

## Serverbound
These are frames send by the **client** to the **server**.

### Events
eventName | data | description
--- | --- | ---
test | test | test

## Clientbound
These are frames send by the **server** to the **client**.

### Events
eventName | data | description
--- | --- | ---
S:responsive | - | Send by the server when the socket is ready to use. Please wait till this message has been arived to ensure your frames are send trough
