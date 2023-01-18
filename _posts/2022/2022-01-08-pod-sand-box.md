---
title: "PodSandbox"
categories:
  - Document
tags:
  - container
  - kubernetes
  - pod
  - lifecycle
toc: true
toc_label: "Table of Contents"
toc_icon: "cog"
---


In order to meet the pod spec, `kubelet` will creating the environment(infra container) for the pod and `add/update/remove` containers in that environment and the pod as a whole, we will call the pod environment as `PodSandbox`.

So, we can call it as the container level interface, and it allows `kubelet` to directly control the life cycles of the containers.


## Features

The features that the `PodSandbox` must be have:

* GNU/Linux namespace(isolate) or the whole virtual machine and the others
* The specific policies of the level of pod request and the limitations


## The detail of the whole phase

Before the startup the container of pods, `kubelet` startup an infra container, and executing `/pause` and let the main process hold on forever, and the `infra` container maintaining all the namespaces of the pod. And the application containers in the pods join the network and the other namespaces to implementing the namespace sharing.

The shared environment was created by the infra container was abstract as `PodSandbox`, `kubelet` to invoke the interface(`RunPod-Sandbox`) of CRI can startup a `PodSandbox`, and to invoke `CreateContainer` to creating the container.


[The ContainerManager interface of CRI](https://github.com/kubernetes/kubernetes/blob/d24fe8a801748953a5c34fd34faa8005c6ad1770/staging/src/k8s.io/cri-api/pkg/apis/services.go)


