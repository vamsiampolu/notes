**Server Sent Events**

What?

A real time one-way communication mechanism from server to client.

Use cases:

+ Useful when pushing continuous updates regarding the score of a `game`.

+ For broadcasting updates to product or service availability

No long-polling or web sockets nessecary. Will only work with the mime-type `text/event-stream`
from the server.

---

How?

Each messagge consists of

```
id
retry
event
data
```

There can be multiple `data` lines. If `retry` is not specified, a default value of `3 seconds` is used.

During the `reconnection` process, the laat id recieved will be sent back to the server.

On the server side, you just write the messages as `strings`(??)

On the client side, you use an `EventSource`. Events are available for:

 + open

 + close

 + error

and any events you send down from the `server`.

---
