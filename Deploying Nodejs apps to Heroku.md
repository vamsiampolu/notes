**Deploying Nodejs apps to Heroku**

1. Setup

  + install Node and Ruby

  + Run `heroku create` on your git repo

  + Push the `heroku` branch to github as `master`

  + `heroku ps:scale web=1`

  + `heroku open`

To check logs:

    heroku logs --tail

In your `Procfile` at the root of your app:

```
web: node index.js
```

+ Free dynos cannot have more than 18 hours of activity a day, if it is inactive for `30 minutes`, it goes to sleep. Any request can wake it up.

To stop running the app, use `heroku ps:scalue web=0`

To run the app locally use `heroku local web`

To integrate third party services(papertrail is used as an example here)

```
heroku addons:create papertrail
heroku addons
heroku addons:open papertrail
```

To run a `Node REPL` using Heroku use `heroku run node`, to run `BASH` use `heroku run bash`.

To setup `config` variables, use a `.env` file. To set config variables on heroku use `heroku config:set TIMES=2`

To view the `config` variables you have for heroku, use `heroku config`.

To provision a database use the heroku marketplace.

---
