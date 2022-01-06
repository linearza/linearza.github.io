---
layout: post
title:  "Phoenix, Postgres.app and the default user"
date:   2016-06-01 14:31:00
categories: postgres config
---

I decided to work through [this][tutorial] great introductory [Phoenix framework][phoenix] tutorial by Erik today.
At the point of running the initial `$ mix ecto.create` command however, it bombed on me, with this little message: 

```
** (Mix) The database for PhoenixApi.Repo couldn't be created, reason given: psql: FATAL:  role "postgres" does not exist
```

Turns out, there is a solution to fix it for this and all other such cases. Postgres.App, it seems, does not create the default `postgres` user on installation but rather uses the the default `$USER`. Most tutorials assume the initial default. To fix it, simply run the following:

```
/Applications/Postgres.app/Contents/Versions/9.*/bin/createuser -s postgres
```

More info [here][solution].


[tutorial]: http://www.programwitherik.com/how-to-guide-the-phoenix-framework-and-ember-js-2
[solution]: http://stackoverflow.com/a/17813013
[phoenix]: http://www.phoenixframework.org/