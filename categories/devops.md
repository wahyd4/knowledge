## AWS
- EC2
- EC2 container
- Cloudfront
- S3
- RDS

## CI
- Jenkins
- Gitlab CI
- Travis

## Docker
- Orchestration
	- Rancher
	- Kubernetes
		- Pod
			- Single container
			- Multiple containers
				- share ip
				- share volumes
		- Node
		- Service
			- ClusterIP (default)
			- NodePort （ access by port）
			- LoadBalancer (external ip)
			- ExternalName dns
		- Deployment
		- Replica Set
		- Service rolling update
		- DaemonSet
			- running a cluster storage daemon, such as glusterd, ceph, on each node
			- running a logs collection daemon on every node, such as fluentd or logstash.
			- running a node monitoring daemon on every node, such as Prometheus Node Exporter, collectd, New Relic agent, or Ganglia gmond.
		- StatefulSets
			- Ordered, graceful deployment and scaling
			- Stable, persistent storage.
			- Stable, unique network identifiers.
			- Ordered, graceful deletion and termination.
		- Proxy
		- DNS
			- service.namespace
		- Secrets
		- Persistent volumes
			- Available
				- a free resource that is not yet bound to a claim
			- Bound
				-  the volume is bound to a claim
			- Released
				- the claim has been deleted, but the resource is not yet reclaimed by the cluster
			- Failed
				- the volume has failed its automatic reclamation
- benefits
	- escape the app dependency matrix
	- Solve the environment issue. it works on my machine.
- Network
	- Bridge
	- Host
- Tips
	- difference between cmd and entrypoint
- CMD
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
- ENTRYPOINT
	- docker run arguments will as the entrypoint’s parameters. not CMD’s override
	- has two forms
		- ENTRYPOINT ["executable", "param1", "param2"]
			- exec form, preferred
		- ENTRYPOINT command param1 param2
			- shell form
	- entrypoint setting can be override by docker run —entrypoint
- Security
	- https://docs.docker.com/engine/security/security/
	- use non root user
	- docker daemon attack surface
	- kernel security features

## Linux
- ssh
- IP table
- Cron job
- ps aux
- tail
- nohup
- df -h
- free
- Tips
	- Change timezone
		- TZ=Asia/Shanghai;ln -snf /usr/share/zoneinfo/$TZ /etc/localtime
	- Check release
		- cat /etc/*-release
- Packages
	- htop
		- like top, but more
	- mosh
		- auto reconnect ssh

## Everything is code
- infrastructure as code
- CI config as code
- Dockerfile

## CD
- Capistrano
- Ansible
- Puppet

## HA High Availability
- LB - haproxy
- Keepalived -- vrrp
	- Nginx + Keepalived
- Heartbeat

## Network
- IP
	- Private IP Addresses
		- 10.0.0.0 – 10.255.255.255
		- 172.16.0.0 – 172.31.255.255
		- 192.168.0.0 – 192.168.255.255

## tools
- git
	- cherrypick
	- rebase
	- commit
	- checkout
		- checkout -b br com
	- push
		- --tags
			- push tags
		- —all
			- push all branchs
		- -f
			- force push
	- branch -d xx
		- delete a local branch
	- remote
		- show xxx
			- show info of a remote branch
		- add xxx
			- add a remote repo
	- branch
		- list all the branchs
	- mv Rename/move files and folder with git history records

      e.g. git mv -k ./a/b ./c/d   option `k` would avoid the "can not move directory into itself" error.
- oh-my-zsh
- IDE/tools
	- Intellij
	- vscode