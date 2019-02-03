[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/
[appurl]: https://freshrss.org/
[hub]: https://hub.docker.com/r/lsioarmhf/freshrss-aarch64/

THIS IMAGE IS DEPRECATED. PLEASE USE THE MULTI-ARCH IMAGES AT `linuxserver/freshrss`

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# lsioarmhf/freshrss-aarch64
[![](https://images.microbadger.com/badges/version/lsioarmhf/freshrss-aarch64.svg)](https://microbadger.com/images/lsioarmhf/freshrss-aarch64 "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/lsioarmhf/freshrss-aarch64.svg)](http://microbadger.com/images/lsioarmhf/freshrss-aarch64 "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/lsioarmhf/freshrss-aarch64.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/lsioarmhf/freshrss-aarch64.svg)][hub][![Build Status](https://ci.linuxserver.io/buildStatus/icon?job=Docker-Builders/arm64/arm64-freshrss)](https://ci.linuxserver.io/job/Docker-Builders/job/arm64/job/arm64-freshrss/)

[FreshRSS][appurl] is a free, self-hostable aggregator for rss feeds

[![freshrss](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/freshrss-banner.png)][appurl]

## Usage

```
docker create \
--name=freshrss \
-v <path to data>:/config \
-e PGID=<gid> -e PUID=<uid> \
-p 80:80 \
lsioarmhf/freshrss-aarch64
```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. 
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`


* `-p 80` - the port(s)
* `-v /config` - local storage for freshrss site files
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation

It is based on phusion-baseimage with ssh removed, for shell access whilst the container is running do `docker exec -it freshrss /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application 
`IMPORTANT... THIS IS THE ARM64 VERSION`

Create a user and database in your mysql/mariadb server (not root) and then follow the setup wizard in the webui. Use the IP address for "host" of your database server.

## Info

* To monitor the logs of the container in realtime `docker logs -f freshrss`.

* container version number 

`docker inspect -f '{{ index .Config.Labels "build_version" }}' freshrss`

* image version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' lsioarmhf/freshrss-aarch64`

## Versions

+ **05.09.18:** Rebase to alpine 3.8.
+ **18.03.18:** Update nginx config to resolve api not working.
+ **09.01.18:** Rebase to alpine 3.7.
+ **30.05.17:** Rebase to alpine 3.6.
+ **03.05.17:** Update to php 7.1x.
+ **24.02.17:** Initial Release.
