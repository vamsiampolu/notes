Koa is a framework that uses async-await to define middleware. This has three advantages:

1. async processing can be done without using callbacks

2. middleware is bi-directional, one can move back up the middleware once the last middleware finishes executing.

3. better error-handling because we can rely on `try/catch` instead of needing specialized error handling middleware

In koa, middleware have a bubble phase and a capture phase, during the bubble phase one passes control to the next middleware
in the chain using `await next()`. Once the last middleware is reached, each middleware is hit in the reverse order of definition
 as control travels up the middleware chain.

A middleware that does not want any middleware downstream to manipulate the response would avoid calling `await next()`.

A koa middleware has two arguments, a  `ctx` which is a combination of the properties on `req` and `res` and a `next` which
is used to pass control to the next middleware in the chain.

```
const responseTime = () => {
  return async function responseTime(ctx,next) {
    var start = new Date()
    await next()
    var ms = new Date() - start
    ctx.set('X-Response-Time',ms+'ms')
  }
}
```

When defining middleware, prefer wrapping it within a function so that we can specify options when initializing the middleware like we have done with
`responseTime`. When installing middleware using koa2, you want koa-middleware@next instead of koa-middleware. A middleware would need to support async functions in
order to be used with koa2. To use a middleware, just define it as:

```
app.use(middleware())
```

koa apps can have more debugging info printed in the console:

```
DEBUG=koa* babel-node index.js
```

If a middleware does not show up when using `koa`, use:

```
middleware._name = 'middlewareName'
```
