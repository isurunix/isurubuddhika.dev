---
title: "Expose Port 2375 on Rancher Dekstop"
date: 2024-12-25T09:38:05+05:30
draft: false
categories: ["guides"]
tags: ["docker","ci/cd","maven"]
---

# Expose port 2375 on Rancher Desktop

If you've been working with Docker on Windows for a there is big chance that you are aleready using Rancher Desktop instead of Docker Desktop after the licensing change Docker did in 2021. 

While Rancher Desktop makes it easy to manage Docker on Windows it does not expose the Docker socket over port `2375` by default. While Docker Desktop used to have a way to enable this by clicking a checkbox in the UI Ranches does not have such an option.

Exposing Docker socket over `2375` is required by older CI pipelines and if you are working with Maven and Java in a enterprise environment you are most likely to have `dockerfile-maven` in your toolchain which connects docker over this port.

Since Rancher does not expose this using any built-in mechanisms we need to manually expose it using a container. If you did a quick search on this you are mostlikely to find the `rancher/socat-docker` image which allows you to run a lightweight container which uses `socat` to exposr docker socket over port `2375`. However if you look at this image in Docker Hub you'd notice that it was published around 10 years ago and has neve been updated. So when you try to run a container from that in a new Docker setup you will endup with below error

```
docker: [DEPRECATION NOTICE] Docker Image Format v1 and Docker Image manifest version 2, schema 1 support is disabled by default and will be removed in an upcoming release. Suggest the author of quay.io/coreos/etcd:latest to upgrade the image to the OCI Format or Docker Image manifest v2, schema 2. More information at https://docs.docker.com/go/deprecated-image-specs/.
```

This is because the `rancher/socat-docker` uses a legacy Docker image format which is no longer compatible. However, it's quite simple to fix this. All you need to is to clone the rancher socat repository and build the image yourself. Then you can use the your local image to expose `2375` as you wish

## Steps to expose 2375 on Rancher Desktop

- Clone socat repository from GitHub
  ```bash
  git clone git@github.com:rancher/socat-test.git
  ```
- Build the Docker image
  ```bash
  cd socat-test
  docker build -t rancher/socat-docker .
  ```
- Run socat container using the image you just built
  ```
  docker run -d --restart always \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -p 2375:2375 --name expose-docker-on-2375 rancher/socat-docker

That's it and you should be use docker over 2375 now.

## TL;DR

To expose Docker socket over port 2375 on Rancher Desktop, you need to manually run a container using the `rancher/socat-docker` image. Since the official image is outdated, clone the `socat-test` repository from GitHub, build the image locally, and run it to expose port 2375. This is necessary for older CI pipelines and tools like `dockerfile-maven` that rely on this port.


