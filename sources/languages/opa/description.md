Opa is sadly a short-lived language, created in 2011 by the company MLState.
It's strongly focused on webapps, as it lets you write server-side and client-side
code, side by side. The client-code is compiled into JavaScript, and the server-code,
into Node.js. All using strong, static typing. Pretty nifty.

In version 0.9.0, it natively supported MongoDB, as if it had an ORM built in.
In 1.1.0, this support was extended to PostgreSQL too.

It reminds me a bit of React/JSX, as it's wholeheartedly designed for interoperability
with HTML. It's actually a first-class citizen. Blurring the line between client
and server code is something that I'm really fond of.

The problem is that, having had only 2 years of activity, the "user experience"
is really bad. Setting up the environment is... problematic, to say the least. It
requires installing NodeJS and OCaml, with dependencies of each one sprinkled in.
Which in turn need dependencies. Some of which have to be compiled from source.
In a time where installing a language (or anything really) should not take more
than 2 or 3 commands (apt update && apt install -y Stuff-0.1.1-dev), this was a
paaaain.

Luckily, there's this cute technology called containers.
