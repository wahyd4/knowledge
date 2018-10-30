## Kubernetes

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

### Several ways to access a service inside Kubernetes cluster
* ClusterIP, Can only be accessed inside the cluster. You can access inside `kubectl proxy`
* NodePort, You can access the service by a specific public port between `30000–32767`, if the cluster server IP changes, then your service' endpoint url changes.
* LoadBalancer, it's kind of external service, all the requests go through the loadbalancer. Every service needs a new IP for this.
* Ingress, can be shared among multiple services, you can have different types of ingress controllers: gec, nginx, contour,istio and so on.

Links:
* [Kubernetes NodePort vs LoadBalancer vs Ingress? When should I use what?](https://medium.com/google-cloud/kubernetes-nodeport-vs-loadbalancer-vs-ingress-when-should-i-use-what-922f010849e0)

### Zero down time deployment
Set strategy type to `RollingUpdate` instead of `Recreate`
```yaml
spec:
  replicas: 1
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 50%
      maxSurge: 1
```

### Some useful commands

```bash

kubectl config set-context context-name --namespace default-namespace-name #default active context
kubectl config view #view config
kubectl get nodes #get nodes
kubectl get namespaces #get all namespaces
kubectl get pods #get pods
kubectl get deployments #get deployments
kubectl get services #get services
kubectl get ingress #get ingresses

```

### Kubernetes Dashboard

#### Deploy Dashboard

```bash
kubectl create -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml
```
#### Access dashboard

```bash
# First fetch cluster info, make sure cluster is running properly
kubectl cluster-info

# Normally the url for dashboard would be
http://your_ip:8080/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/

```
