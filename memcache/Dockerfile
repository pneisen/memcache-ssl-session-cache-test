FROM ubuntu:14.04

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y memcached

EXPOSE 11211
CMD ["/usr/bin/memcached", "-u", "memcache", "-p", "11211", "-m", "64", "-c", "10240", "-vv"]
