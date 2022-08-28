---
title: "Rebuilding specific version Kubernetes"
categories:
  - Document
  - Blog
tags:
  - English
  - kubernetes
  - codespaces
  - docker
toc: true
toc_label: "Table of Contents"
toc_icon: "cog"
---


Here is an issue with opening Linux kernel memory, so the customers need to rebuild specific version of `kubelet`.


# Building

### Checking out to the specific version of Kubernetes

```
# For example, the target version is v1.20.15
git checkout v1.20.15
```


### Executing building command

`KUBE_BUILD_PLARFORMS` support different OS/architecture like `OSX` and `GNU/Linux`

```
# For example
=linux/arm64
=linux/amd64
```


### The complete command can be 

```
KUBE_GIT_VERSION=v1.20.15 ./build/run.sh make kubelet KUBE_BUILD_PLATFORMS=linux/arm64 GOFLAGS="-tags=nokmem"
```

And we can find the binary under the project root folder was named `_output`


# Testing

The command for checking for all the containers, if mem.txt is empty, kernel memory feature was already closed.


```
find /sys/fs/cgroup/memory/kubepods/ -name memory.kmem.slabinfo | xargs cat > /tmp/mem.txt
```


The command for checking specific container

```
cat /sys/fs/cgroup/memory/kubepods/burstable/pod<pod-uid>/<container-id>/memory.kmem.slabinfo
```

Checking `memory.kmem.slabinfo` that it does not contains `Input/output error`


```
cat: memory.kmem.slabinfo: Input/output error
```


# Reference:

https://github.com/kubernetes/kubernetes/issues/61937