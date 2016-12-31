# thraxis/docker-medusa
[![](https://images.microbadger.com/badges/version/thraxis/docker-medusa.svg)](https://microbadger.com/images/thraxis/docker-medusa "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/thraxis/docker-medusa.svg)](https://microbadger.com/images/thraxis/docker-medusa "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/thraxis/docker-medusa.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/Thraxis/docker-medusa.svg)][hub]
[hub]: https://hub.docker.com/r/thraxis/docker-medusa/

## Usage

```
docker create --name=medusa \
-v <path to config>:/config \
-v <path to downloads>:/downloads \
-v <path to tv-shows>:/tv \
-e PGID=<gid> -e PUID=<uid>  \
-e TZ=<timezone> \
-p 8081:8081 \
linuxserver/medusa
```

**Parameters**

* `-p 8081` - the port(s)
* `-v /config` - where sickrage should store config files.
* `-v /downloads` - your downloads folder
* `-v /tv` - your tv-shows folder
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation
* `-e TZ` for timezone information, eg Europe/London

It is based on alpine linux with s6 overlay, for shell access whilst the container is running do `docker exec -it sickrage /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application 

Web interface is at `<your ip>:8081` , set paths for downloads, tv-shows to match docker mappings via the webui.


## Info

* To monitor the logs of the container in realtime `docker logs -f sickrage`.

* container version number 

`docker inspect -f '{{ index .Config.Labels "build_version" }}' docker-medusa`

* image version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' thraxis/docker-medusa`


## Versions

+ **14-10-16:** Add version layer information.
+ **30.09.16:** Fix umask.
+ **09.09.16:** Add layer badges to README.
+ **28.08.16:** Add badges to README.
+ **08.08.16:** Rebase to alpine linux.
+ **30.12.15:** Build later version of unrar from source, removed uneeded mako package.
+ **20.11.15:** Updated to new repo, by SickRage Team.
+ **15.10.15:** Initial Release.
