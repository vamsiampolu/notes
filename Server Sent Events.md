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

If `EventSource` is not available in your browser(Edge or IE), use the [polyfill](https://github.com/Yaffle/EventSource)

+ Step 1: Create the `EventSource`:

```
source = new window.EventSource('stream')
```

Now, a `HTTP` request is sent to the server for `/stream`. The server responds with the appropriate mime-type and the `headers`.

+ Step 2: setup event handling for the `open` and `error` events

```
source.addEventListener('open',handleOpen,false)
source.addEventListener('error',handleError,false)
```

+ Step 3: Once a connection has opened, start listening for generic messages and any specific messages:

```
source.addEventListener('message',handleGenericMessage,false)
source.addEventListener('specificMessage',handleSpecificMessage,false)
```

If a message is sent with an event of `specificMessage` on the server, it can be handled by the latter and
if no event is used, it is handled by the former.

An example can be found [here](https://github.com/vamsiampolu/sse-rawhttp)

It is based on the [blog post](http://cjihrig.com/blog/server-sent-events-in-node-js/)

---

**References**

1. http://cjihrig.com/blog/server-sent-events-in-node-js/

2. http://cjihrig.com/blog/the-server-side-of-server-sent-events/

3. http://streamdata.io/blog/server-sent-events/

4. http://streamdata.io/blog/push-sse-vs-websockets/

---
