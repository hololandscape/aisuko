---
title: "GNU Linux Namespace"
categories:
  - Document
tags:
  - GNU/linux
  - container
  - namespace
toc: true
toc_label: "Table of Contents"
toc_icon: "cog"
---


Namespaces are a fundamental aspect of containers on Linux.


### Overview

Namespaces are a feature of the Linux kernel that partitions kernel resources such that one set of process sees one set of resources and processes, but those namespaces refer to distinct resources.

A Linux system starts out with a single namespace of each type, used by all processes. Processes can create additional namespaces and join different namespaces.


### Namespace kinds

Namespace functionality is the same across all kinds: each process is associated with a namespace and can only see or use the resources associated with that namespace, and descendant namespaces where applicable.


* Mount(mnt)
Mount namespaces control mount points. Upon creation the mounts from the current mount namespace are copied to the new namespace, `but mount points created afterwards do not propagate between namespaces`(using shared subtrees, it is possible to propagate mount points between namespaces)

The clone flag used to create a new namespace of this type is `CLONE_NEWNS`


* Process ID(pid)

The PID namespace provides processes with an independent set of process IDs (PIDs) from other namespaces. PID namespaces are bested, meaning when a new process is created it will have a PID for each namespace from it current namespace up to the initial PID namespace. Hence the initial PID namespace is able to see all processes, albeit with different PIDs than other namespaces will see processes with.

The first process created in a PID namespace is assigned the process id number 1 and receives most of the same special treatment as the normal init process, most notably that orphaned processes within the namespace are attached to it.


* Network(net)

Network namespaces virtualize the network stack. On creation a network namespace contains only a loopback interface.

Each network interface is present in exactly 1 namespace and can be moved between namespaces.

Each namespace will have a private set of IP addresses, its own routing table, socket listing, connection tracking table, firewall, and other network-related resources.

Destroying a network namespace destroys any virtual interfaces within it and moves any physical interfaces within it back to the initial network namespace.


* Interprocess Communication(ipc)

IPC namespaces isolate processes from SysV style inter-process communication.This prevents processes in different IPC namespaces from using, for example, the SHM family of functions to establish a range of shared memory between the two processes. Instead each process will be able to use the same identifiers for a shared memory region and produce two such distinct regions.


* UTS

UTS(UNIX Time-Sharing) namespaces allow a single system to appear to have different host and domain names to different processes. 

* User ID(user)

User namespaces are a feature to provide both privilege isolation and user identification segregation across multiple sets of processes available since kernel 3.8. With administrative assistance it is possible to build a container with seeming administrative rights without actually giving elevated privileges to user processes. Like the PID namespace, user namespaces are nested and each new user namespace is considered to be a child of the user namespace that created it.

A user namespace contains a mapping table converting user IDs from the container's point of view to the system's point of view. This allows, for example, the root user to have user id 0 in the container but is actually treated as user id 1,400,000 by the system for ownership checks. A similar table is used for group id mappings and ownership checks.


* Control group (cgroup) Namespace

The [cgroup](./2021-12-30-cgroups.md) namespace type hide the identity of the control group of which process is a member. A process in such a namespace, checking which control group any process is part of, would see a path that is actually relative to the control group set at creation time, hiding its true control group position and identity.


* Time Namespace 

The time namespace allows process to see different system time in a way similar to the UTS namespace.


### Implementation details

The kernel assigns each process a symbolic link per namespace kind in `/proc/<pid>/ns`. The inode number pointed to by this symlink is the same for each process in this namespace. This uniquely identifies each namespace by the inode number pointed to by one of its symlinks.

Reading the symlink via reading returns a string containing the namespace kind name and the inode number of the namespace.


### Syscalls

Three `syscalls` can directly manipulate namespaces:

* `clone`, flags to specify which new namespace the new process should be migrated to
* `unshare`, allow a process(or thread) to disassociate parts of its execution context that are currently being shared with other processes(or thread)
* `setns`, enters the namespace specified by a file descriptor


### Destruction

If a namespace is no longer referenced, it will be deleted, the handling of the contained resource depends on the namespace kind. Namespaces can be referenced in three ways:

* by a process belonging to the namespace
* by an open filedescriptor to the namespace's file `proc/<pid>/ns/<ns-kind>`
* a bind mount of the namespace's file `/proc/<pid>/ns/<ns-kind>`


__References__

[Wikipedia](https://en.wikipedia.org/wiki/Linux_namespaces)
