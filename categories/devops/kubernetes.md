# Kubernetes

## Terminology

### Pod
  - Single container
  - Multiple containers
      - share ip
      - share volumes
### Node

Basically is a Kubernetes client or agent which runs a bunch of pods.

### Service
  - ClusterIP (default)
  - NodePort （ access by port）
  - LoadBalancer (external ip)
  - ExternalName dns
### Deployment

A Deployment provides declarative updates for Pods and ReplicaSets.

You describe a desired state in a Deployment, and the Deployment Controller changes the actual state to the desired state at a controlled rate. You can define Deployments to create new ReplicaSets, or to remove existing Deployments and adopt all their resources with new Deployments.

### Replica Set
    A ReplicaSet’s purpose is to maintain a stable set of replica Pods running at any given time. As such, it is often used to guarantee the availability of a specified number of identical Pods.
### Service rolling update
### DaemonSet
  - running a cluster storage daemon, such as ·glusterd`, `ceph`, on each node
  - running a logs collection daemon on every node, such as `fluentd` or logstash.
  - running a node monitoring daemon on every node, such as Prometheus Node Exporter, collectd, New Relic agent, or Ganglia gmond.
### StatefulSets
  - Ordered, graceful deployment and scaling
  - Stable, persistent storage.
  - Stable, unique network identifiers.
  - Ordered, graceful deletion and termination.
### Proxy
### DNS
  - service.namespace
### Secrets
    For storing keys, credentials and certificates. For instance: database token, 3rd party API keys.
### Persistent volumes

- Available
    - a free resource that is not yet bound to a claim
- Bound
    -  the volume is bound to a claim
- Released
    - the claim has been deleted, but the resource is not yet reclaimed by the cluster
- Failed
    - the volume has failed its automatic reclamation

## Several ways to access a service inside Kubernetes cluster

* ClusterIP, Can only be accessed inside the cluster. You can access inside `kubectl proxy`
* NodePort, You can access the service by a specific public port between `30000–32767`, if the cluster server IP changes, then your service' endpoint url changes.
* LoadBalancer, it's kind of external service, all the requests go through the loadbalancer. Every service needs a new IP for this.
* Ingress, can be shared among multiple services, you can have different types of ingress controllers: `gec`, `nginx`, `contour`, `istio` and so on.

Links:
* [Kubernetes NodePort vs LoadBalancer vs Ingress? When should I use what?](https://medium.com/google-cloud/kubernetes-nodeport-vs-loadbalancer-vs-ingress-when-should-i-use-what-922f010849e0)

## Zero down time deployment
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

## Some useful commands

```bash
kubectl config set-context context-name --namespace default-namespace-name #default active context
kubectl config view #view config
kubectl get nodes #get nodes
kubectl get namespaces #get all namespaces
kubectl get pods #get pods
kubectl get deployments #get deployments
kubectl logs -f <pod> --tail 200 # tail logs from some pod
kubectl get services #get services
kubectl get ingress #get ingresses
kubectl get hpa # get horizontal auto scaling policies
kubectl get all # get all kinds of units
kubectl get secrets <secret-id> -o yaml #view a secret details with yaml format, fields are encrypted with base64

```

## Kubernetes port forward

`kubectl port-forward` allows using resource name, such as a pod name, to select a matching pod to port forward to Which is perfect for testing the remote service/pods in your local. e.g. Forward your db port to a local port, you can connect to your remote db even it doesn't have a public IP.

```bash
kubectl port-forward redis-master-765d459796-258hz 7000:6379

kubectl port-forward pods/redis-master-765d459796-258hz 7000:6379

kubectl port-forward deployment/redis-master 7000:6379

kubectl port-forward rs/redis-master 7000:6379

kubectl port-forward svc/redis-master 7000:6379
```

## Kubernetes Dashboard

### Deploy Dashboard

```bash
kubectl create -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml
```
### Access dashboard

```bash
# First fetch cluster info, make sure cluster is running properly
kubectl cluster-info

# Normally the url for dashboard would be
http://your_ip:8080/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/

```

## Configure Kubectl to access remote Kubernetes cluster

Here is a very simple config which use HTTP and `not secure`, should only for local testing purpose

### Config

Having a yaml file called `config-demo` in your current folder

```yaml
apiVersion: v1
clusters:
- cluster:
    server: https://your_cluster_ip:5443
  name: development
contexts:
- context:
    cluster: development
    namespace: dev
    user: developer
  name: dev
current-context: dev
kind: Config
preferences: {}
users:
- name: developer
```

### Connect to remote cluster

```bash
kubectl get all --kubeconfig=config-demo --all-namespaces
```
For long term usage, you will need to copy the content to your `~/.kube/config` file

## Helm

Add Kubernetes yaml template engine and the package manager for Kubernetes

### How to use

```bash
helm init
helm upgrade --install -f abc/values-staging.yaml some-name ./abc
# abc/values-staging.yaml the value file
# some-name the release name
# abc the template folder
helm delete --purge mqtt  # mqtt the release name

```
### Install 3rd party packages
```bash
helm repo add gitlab https://charts.gitlab.io/ # add remote repo
helm repo update # update index
helm install mirantisworkloads/vernemq
```

### Tips

* Normally when you just updated the configmap the deployment or statefulset pod wouldn't updated, but you can add a label to deployment/statefulset yaml, when the value changes the pods will be recreated

```yaml
template:
  metadata:
    labels:
      app: vernemq
      configmapVersion: "{{ .Release.Revision }}"
```

### Deploy tools comparsion

https://blog.hasura.io/draft-vs-gitkube-vs-helm-vs-ksonnet-vs-metaparticle-vs-skaffold-f5aa9561f948/


## Horizontal scaling

### V1
```yaml
apiVersion: autoscaling/v1
kind: HorizontalPodAutoscaler
metadata:
  name: worker-auto-scaling
  namespace: x-prod
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: <deployment-name>
  minReplicas: 1
  maxReplicas: 2
  targetCPUUtilizationPercentage: 75 # trigger point
```

### V2
```yaml
apiVersion: autoscaling/v2beta2
kind: HorizontalPodAutoscaler
metadata:
  name: php-apache
  namespace: default
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: php-apache
  minReplicas: 1
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 50
  - type: Pods
    pods:
      metric:
        name: packets-per-second
      target:
        type: AverageValue
        averageValue: 1k
  - type: Object
    object:
      metric:
        name: requests-per-second
      describedObject:
        apiVersion: networking.k8s.io/v1beta1
        kind: Ingress
        name: main-route
      target:
        type: Value
        value: 10k
```
## Limit CPU and memory for pods

```yaml
ports:
- name: db-port
  containerPort: 2345
  protocol: TCP
resources:
requests:
  cpu: 30m
  memory: 64Mi
limits:
  cpu: 200m
  memory: 256Mi
```

## Kubernetes Operator

A Kubernetes Operator is an abstraction for deploying non-trivial applications on Kubernetes. It wraps the logic for deploying and operating an application using Kubernetes constructs. As an example, the `etcd` operator provides an `etcd` cluster as a first-class object.

### An example Operator

- deploying an application on demand
- taking and restoring backups of that application’s state
-handling upgrades of the application code alongside related changes such as database schemas or extra configuration settings
- publishing a Service to applications that don’t support Kubernetes APIs to discover them
- simulating failure in all or part of your cluster to test its resilience
- choosing a leader for a distributed application without an internal member election process

### Use Operator

```
kubectl get SampleDB                   # find configured databases

kubectl edit SampleDB/example-database # manually change some settings
```

### Some 3rd party operators

- Operator registry: https://operatorhub.io/
- Custom operators list: https://gist.github.com/philips/a97a143546c87b86b870a82a753db14c
- Prometheus operator: https://coreos.com/blog/the-prometheus-operator.html

## Tools

### Kubectx and kubens

Switch faster between clusters and namespaces in kubectl https

- kubectx for switching contexts
- kubens for switching namespaces

Github page: https://github.com/ahmetb/kubectx


## Other distributions

### OpenShift(OKD)

https://github.com/openshift/okd

OKD is the Origin community distribution of Kubernetes optimized for continuous application development and multi-tenant deployment. OKD adds developer and operations-centric tools on top of Kubernetes to enable rapid application development, easy deployment and scaling, and long-term lifecycle maintenance for small and large teams. OKD is also referred to as Origin in github and in the documentation. OKD makes launching Kubernetes on any cloud or bare metal a snap, simplifies running and updating clusters, and provides all of the tools to make your containerized-applications succeed.

#### Differences

- More strict on security, for example you can't run docker images with `root` user.
- Better UI and come with some management tools.
- Integrated CI/CD
- It's a Redhat product, OKD is its open-source project

![differences between Kubernetes and Openshift](https://raw.githubusercontent.com/wahyd4/knowledge-mind-mapping/master/assets/images/openshift.png)


### K3s

https://github.com/rancher/k3s

k3s is intended to be a fully compliant Kubernetes distribution with the following changes:

1. Removed most in-tree plugins (cloud providers and storage plugins) which can be replaced
   with out of tree addons.
2. Add sqlite3 as the default storage mechanism. etcd3 is still available, but not the default.
3. Wrapped in simple launcher that handles a lot of the complexity of TLS and options.
4. Minimal to no OS dependencies (just a sane kernel and cgroup mounts needed). k3s packages required
   dependencies
    * containerd
    * Flannel
    * CoreDNS
    * CNI
    * Host utilities (iptables, socat, etc)
