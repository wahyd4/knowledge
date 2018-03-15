# Docker

## Orchestration

### Rancher
### Kubernetes

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

#### Several ways to access a service inside Kubernetes cluster
* ClusterIP, Can only be accessed inside the cluster. You can access inside `kubectl proxy`
* NodePort, You can access the service by a specific public port between `30000–32767`, if the cluster server IP changes, then your service' endpoint url changes.
* LoadBalancer, it's kind of external service, all the requests go through the loadbalancer. Every service needs a new IP for this.
* Ingress, can be shared among multiple services, you can have different types of ingress controllers: gec, nginx, contour,istio and so on.

Links:
* [Kubernetes NodePort vs LoadBalancer vs Ingress? When should I use what?](https://medium.com/google-cloud/kubernetes-nodeport-vs-loadbalancer-vs-ingress-when-should-i-use-what-922f010849e0)

## Benefits

	- escape the app dependency matrix
	- Solve the environment issue. it works on my machine.
## Network

- Bridge
- Host

## Tips

	- difference between `cmd` and `entrypoint`
	- difference between `copy` and `add`

        Basically they are similar, copy files and folder to destination. While ADD has some features (like local-only tar extraction and remote URL support) that are not immediately obvious. Consequently, the best use for ADD is local tar file auto-extraction into the image, as in ADD rootfs.tar.xz /.
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
