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

To setup, the server should respond with `headers`:

```
Content-Type: text/event-stream
Cache-Control: no-cache
Connection: keep-alive
```

when the client requests the event stream.


Each message is represented by plain text and can consist of:

```
id:
retry:
event:
data:
```

Multiple lines are allowed when specifying an `event`. A newline can be used at the end of a line to indicate that
the message is continued on the next line. To terminate a message use two newline charecters at the end of the line.

If `event` is not specified, the payload is treated as an `unnamed event`.

There can be multiple `data` lines. If `retry` is not specified, a default value of `3 seconds` is used.

During the `reconnection` process, the laat id recieved will be sent back to the server.


On the client side, you use an `EventSource`. Events are available for:

 + open

 + close

 + error

and any events you send down from the `server`.

---
