---
layout: post
title:  "Common Docker Commands"
categories: [ Computer Programming  ]
tags: [blog_post_unpublished]
---

I recently started Docker extensively for work and realised it was time to dump the common commands somewhere. That somewhere is HERE!

The official documentation exists [here] https://docs.docker.com/engine/reference/commandline/cp/

**Note: A common docker image terminal looks like user_name@container_id**

* Open a current docker image in another terminal

`docker exec -it container_id bash`

* Pull a Docker Image from the cloud

`docker pull user_name/build_environment_name:tag`

* Copy files from docker image to the host machine

`docker cp container_id:/path/to/file/in/docker /host/machine/destination/folder`

* Copy files from host machine to the docker image 

`docker cp /host/machine/file container_id:/path/to/destination/folder `



