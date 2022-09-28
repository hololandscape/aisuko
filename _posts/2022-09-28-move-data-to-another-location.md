---
title: "Moving data to another location"
categories:
  - Document
  - Blog
tags:
  - English
  - GNU/Linux
  - rsync
  - docker
toc: true
toc_label: "Table of Contents"
toc_icon: "cog"
---


# How to move data to another location

For example, if we want to copy docker files to new location.

```

systemctl stop docker

# This is equivalent to using -rlptgoD. Archive mode includes all the necessary options like copying files recursively, preserving(symbolic links, file permissions, user&group ownership and timestamps)
rsync -aP /var/lib/docker/ /path/to/new/docker/location

remove -rf /var/lib/docker

systemctl start docker
```

# rsync command in GNU/Linux

rsync(remote synchronization) is a software utility for Unix-Like systems that efficiently sync files and directories between two hosts or machines.

There are basically two ways in which rsync can copy/sync data:

* Copying/Syncing to/from another host over any remote shell like ssh, rsh.
* Copying/Syncing through rsync daemon using TCP.

And rsync uses delta transfer algorithm, it copies only the differences between the source files present in the local-host and the existing files in the destination or the remote host.


# References list:

* https://evodify.com/change-docker-storage-location/
* https://mrkandreev.name/snippets/how_to_move_docker_data_to_another_location/
* https://www.geeksforgeeks.org/rsync-command-in-linux-with-examples/

