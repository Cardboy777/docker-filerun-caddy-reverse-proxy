# Custom Caddy/FileRun Docker-Compose Configuration

At the time of publishing, this repo contains a working example of [FileRun](https://filerun.com/) with mariaDB working behind a reverse proxy configured via [Caddy-Docker-Proxy](https://github.com/lucaslorentz/caddy-docker-proxy).

## Some Caveats

There are some minor customizations that I've made in order to better suit my personal needs. I'll highlight a few below, but this configuration is intended as a starting point. Tinker to your heart's content.

### FileRun

The FileRun image hosted on Dockerhub contained build errors and I was unable to get it working.

As such, the Dockerfile is a slightly modified version from the [filerun/docker repo](https://github.com/filerun/docker), so as to make use of Dockerfile's [multi-stage builds](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#use-multi-stage-builds) as well as update the download links for Libre Office and ImageMagick (Note: I used the most up to date versions of these software and not the ones from original image. I have yet to run into any issues but if you have compatibility problems try updating the download links with the older ones listed in the source repo).

The filerun directory containing entrypoint.sh and all its files is identical to the one found in the source repo.

The caddy configuration in the docker-compose labels is a mix of copy-pasted code from a variety of sources. (It was weeks ago so I have no memory of where from)

### Caddy

I use a Dockerfile with a custom build for caddy so that I could create a caddy instance with both [lucaslorentz's awesome Caddy Docker Proxy plugin](https://github.com/lucaslorentz/caddy-docker-proxy) as a well as the [Cloudflare DNS Plugin](https://github.com/caddy-dns/cloudflare). If you aren't using Cloudflare as your DNS, you're probably better off using the [lucaslorentz/caddy-docker-proxy](https://hub.docker.com/r/lucaslorentz/caddy-docker-proxy) docker image or [one of caddy's](https://hub.docker.com/_/caddy).
