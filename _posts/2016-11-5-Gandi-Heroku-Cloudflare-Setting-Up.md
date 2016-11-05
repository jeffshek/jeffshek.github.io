---
layout: post
title: Setting up SSL with Heroku, Gandi and Cloudflare
---
I had a bit of trouble setting up Heroku, Gandi and Cloudflare to play nicely with SSL / DNS Forwarding. Hopefully, this comes in handy for someone who ends up with similar issues. This configuration allows for SSL certification without having to deal with DNS Zones (a lot more trouble than it's worth)

### Gandi (Provides an SSL for free)

1. Update DNS on Gandi

~~~
# cloudflare provides two DNS addresses, replace these as needed
lee.ns.cloudflare.com
vera.ns.cloudflare.com
~~~

2. Setup SSL (standard is free)

### Cloudflare (Provides Shared SSL)

1. Manage DNS Records

~~~
| Type  | Name       | Value                 |
|-------|------------|-----------------------|
| cname | domain.com | domain.herokuapp.com  |
| cname | www        | domain.heroku.app.com |
~~~

2. Set SSL Crypto to Full (Not Flexible vs Full + Strict). I had a lot of problems finding this out. Otherwise, I was on a URL redirect loop.

### Heroku (Don't Need Heroku SSL)
1. Setup Custom Domains

~~~
| Domain Name    | DNS Target        |
| ---------------| ------------------|
| domain.com     | app.herokuapp.com |
| www.domain.com | app.herokuapp.com |
~~~

You do not need to purchase a SSL from Heroku!

