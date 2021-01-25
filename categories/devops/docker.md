# Docker

Easy to use, just drag and drop things.

## Benefits of using Docker

- Escape the app dependency matrix
- Solve the environment issue. it works on my machine.
- Very low resource allocation cost when compare with Virtual Machine. So on the same machine, you can run more containers and spend much less time.

## How Docker works

Very useful blog talking about how docker works internally: [Understanding the Docker Internals](https://medium.com/@nagarwal/understanding-the-docker-internals-7ccb052ce9fe)

![Docker](https://raw.githubusercontent.com/wahyd4/knowledge-mind-mapping/master/assets/images/docker.png)

Docker use

* Namespaces
* Cgroups
* Network
* Union File Systems

to isolate all kinds of resources.

### Namespaces

Docker makes use of kernel namespaces to provide the isolated workspace called the container. When you run a container, Docker creates a set of namespaces for that container. These namespaces provide a layer of isolation. Each aspect of a container runs in a separate namespace and its access is limited to that namespace.
Docker Engine uses the following namespaces on Linux:

- `PID` namespace for process isolation.
- `NET` namespace for managing network interfaces.
- `IPC` namespace for managing access to IPC resources.
- `MNT` namespace for managing filesystem mount points.
- `UTS` namespace for isolating kernel and version identifiers.
- `USER` namespaces is a feature of Linux that can be used to separate the user IDs and group IDs between the host and containers. It can provide a better isolation and security: the privileged user root in the container can be mapped to a non-privileged user on the host.

#### How to see a docker container's namespaces

```bash
> docker inspect 195de1a4b33c | grep Pid

	"Pid": 1496,
	"PidMode": "",
	"PidsLimit": null,

> cd /proc/1496
> ls

attr       auxv    clear_refs  comm             cpuset  environ  fd      gid_map  limits    map_files  mem        mounts      net  numa_maps  oom_score      pagemap      personality  root   schedstat  setgroups  smaps_rollup  stat   status   task    timerslack_ns  wchan
autogroup  cgroup  cmdline     coredump_filter  cwd     exe      fdinfo  io       loginuid  maps       mountinfo  mountstats  ns   oom_adj    oom_score_adj  patch_state  projid_map   sched  sessionid  smaps      stack         statm  syscall  timers  uid_map

> cd ns
> ls

cgroup  ipc  mnt  net  pid  pid_for_children  user  uts

```

### cgroups

![cgroups](https://raw.githubusercontent.com/wahyd4/knowledge-mind-mapping/master/assets/images/cgroups.png)

Control Groups are a Linux feature for organizing processes in hierarchical groups and applying resources limits to them. Docker also makes use of kernel control groups for resource allocation and isolation. A cgroup limits an application to a specific set of resources. Control groups allow Docker Engine to share available hardware resources to containers and optionally enforce limits and constraints.
Docker Engine uses the following cgroups:

- `Memory` cgroup for managing accounting, limits and notifications.
- `HugeTBL` cgroup for accounting usage of huge pages by process group.
- `CPU` cgroup for managing user / system CPU time and usage.
- `CPUSet` cgroup for binding a group to specific CPU. Useful for real time applications and NUMA systems with localized memory per CPU.
- `BlkIO` cgroup for measuring & limiting amount of blckIO by group.
- `net_cls` and net_prio cgroup for tagging the traffic control.
- `Devices` cgroup for reading / writing access devices.
- `Freezer` cgroup for freezing a group. Useful for cluster batch scheduling, process migration and debugging without affecting prtrace.

### Union File Systems

![filesystem](https://raw.githubusercontent.com/wahyd4/knowledge-mind-mapping/master/assets/images/docker-filesystem.png)


Union file systems operate by creating layers, making them very lightweight and fast. Docker Engine uses UnionFS to provide the building blocks for containers. Docker Engine can use multiple UnionFS variants, including AUFS, btrfs, vfs, and devicemapper.

### Container Format

Docker Engine combines the namespaces, control groups and UnionFS into a wrapper called a container format. The default container format is libcontainer.
### Security

Docker Engine makes use of `AppArmor`, `Seccomp`, `Capabilities` kernel features for security purposes.

- `AppArmor` allows to restrict programs capabilities with per-program profiles.
- `Seccomp` used for filtering syscalls issued by a program.
- `Capabilties` for performing permission checks.


### Docker VS VM

![Docker vs VM](https://raw.githubusercontent.com/wahyd4/knowledge-mind-mapping/master/assets/images/container.png)

## Network

- Bridge
- Host

## CMD

- has three forms
- CMD ["executable","param1","param2"]
	- exec form, preferred
- CMD ["param1","param2"]
	- as default parameters to ENTRYPOINT
- CMD command param1 param2
	- shell form
- The main purpose of a CMD is to provide defaults for an executing container. These defaults can include an executable, or they can omit the executable, in which case you must specify an ENTRYPOINT instruction as well.
- If CMD is used to provide default arguments for the ENTRYPOINT instruction, both the CMD and ENTRYPOINT instructions should be specified with the JSON array format.
- docker run could override the default specified in CMD.

## ENTRYPOINT

- docker run arguments will as the entrypoint’s parameters. not CMD’s override
- has two forms
- ENTRYPOINT ["executable", "param1", "param2"]
	- exec form, preferred
- ENTRYPOINT command param1 param2
	- shell form
- entrypoint setting can be override by docker run —entrypoint

## Security
	- https://docs.docker.com/engine/security/security/
	- use non root user
	- docker daemon attack surface
	- kernel security features

## Tips

### difference between `cmd` and `entrypoint`

	`cmd` can be override but entrypoint can't.

### difference between `copy` and `add`

	Basically they are similar, copy files and folder to destination. While ADD has some features (like local-only tar extraction and remote URL support) that are not immediately obvious. Consequently, the best use for ADD is local tar file auto-extraction into the image, as in ADD rootfs.tar.xz /.

### Reduce docker image size

- Use the small base docker image, e.g. `alpine`, `jessie` etc.
- Change docker image to multi stage, only copy the runtime files and dependencies to the final stage

A example of node js one

**Before**

```Dockerfile
FROM node:alpine as build	FROM node as build

WORKDIR /app

# copy the app, note .dockerignore	# copy the app, note .dockerignore
COPY . /app

RUN apk update \
  && apk add --no-cache git python alpine-sdk\
  && npm ci \
  && npm run build \
  && npm run generate

EXPOSE 3000

CMD [ "npm", "start" ]

```
**After**

```Dockerfile

FROM node as build

WORKDIR /app

# copy the app, note .dockerignore
COPY . /app

RUN npm ci \
  && npm run build \
  && npm run generate \
  && npm prune --production \
  && curl -sf https://gobinaries.com/tj/node-prune | sh \
  && node-prune

FROM node:alpine

WORKDIR /app

# copy from build image
COPY --from=build /app ./

EXPOSE 3000

CMD [ "npm", "start" ]
```
