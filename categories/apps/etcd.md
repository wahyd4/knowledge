# etcd

etcd is a strongly consistent, distributed key-value store that provides a reliable way to store data that needs to be accessed by a distributed system or cluster of machines. It gracefully handles leader elections during network partitions and can tolerate machine failure, even in the leader node.

## Set up a ETCD cluster

https://github.com/kelseyhightower/kubernetes-the-hard-way/blob/master/docs/07-bootstrapping-etcd.md

##  Tips

### Make the k8s embedded single etcd to be a cluster

Unfortunately, there is no straightfoward way to change the existing embedded etcd to a cluster.
But we can leverage etcd `make-mirror` command to replicate the existing etcd to a new cluster.
The steps are:

1. Follow the guide to setup a new etcd cluster
2. Run the following command to replicate k8s emmbedded etcd data to the new cluster

```
sudo ETCDCTL_API=3 etcdctl make-mirror https://new_etcd_node:2379 --endpoints=https://192.168.1.2:2379  --cacert=/k8s_etcd/ca.crt   --cert=/k8s_etcd/server.crt   --key=/k8s_etcd/server.key   --dest-cacert=/new_etcd/ca.pem   --dest-cert=/new_etcd/etcd.pem   --dest-key=/new_etcd/etcd-key.pem
```
3. On one of the new cluster node, to verify the data
```
sudo ETCDCTL_API=3 etcdctl get --prefix=true "" -w json  --endpoints=https://127.0.0.1:2379   --cacert=/new_etcd/ca.pem   --cert=/new_etcd/etcd.pem   --key=/new_etcd/etcd-key.pem
```

### Join another existing cluster

1. Run the join command on an existing node, for instnace
```
sudo ETCDCTL_API=3 etcdctl member add server-2 --peer-urls=https://192.168.1.xxx:2380  --endpoints=https://192.168.1.xxx:2379,https://192.168.1.xxx:2379   --cacert=/etc/etcd/ca.pem   --cert=/etc/etcd/etcd.pem   --key=/etc/etcd/etcd-key.pem
```
2. Prepare for the configursations for the new node, and remember to set `--initial-cluster-state` to existing, add put all the existing nodes to `--initial-cluster` field
3. Start the etcd service of the new node
