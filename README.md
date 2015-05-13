# Memcache SSL Session Cache Test

This docker-compose project will spin up a tcp load balanced, 3 node apache cluster with a shared Memcached server for
SSL session caching. We were looking at replacing [Distcache](http://distcache.sourceforge.net/) with Memcached at work
in our Apache cluster than needs SSL pass-through and distributed SSL session caching. There was very little documentation
out on the web, so I put together this project to try it out and provide an example. I also wanted to play with Docker some
more.

###To spin up the cluster:

1. Install [Docker](https://docker.com) and [Docker Compose](https://docs.docker.com/compose/#installation-and-set-up).
2. Add docker.example.com to your /etc/hosts file pointed at either your docker host or your boot2docker vm. ("boot2docker ip" to
get the ip from boot2docker)
3. Clone this repo
4. cd to this repo directory
5. docker-compose up

###Use this command to test:
```bash
openssl s_client -connect docker.example.com:443 -reconnect -no_ticket
```
Note: The -no_ticket is required as SSL tickets are not shared.

###Expected output from test:

- **This:** *New, TLSv1/SSLv3, Cipher is DHE-RSA-AES256-SHA*
- **Followed by 4 of these:** *Reused, TLSv1/SSLv3, Cipher is DHE-RSA-AES256-SHA*

Also, the Session-ID should be identical in each case.
