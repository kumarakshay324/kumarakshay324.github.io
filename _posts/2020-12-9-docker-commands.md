---
layout: post
title:  "Common Docker Commands"
categories: [ Computer Programming  ]
tags: [blog_post]
---

I recently started Docker extensively for work and realised it was time to dump the common commands somewhere. That somewhere is HERE!

**Note: A common docker image terminal looks like user_name@container_id**

* Open a current docker image in another terminal

`docker exec -it container_id bash`

* Copy files from docker image to the host machine

`docker cp container_id:/path/to/file/in/docker /host/machine/destination/folder`



