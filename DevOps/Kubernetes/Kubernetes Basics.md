It needs one master node, and each worker node will have a "kubelet" process, which makes it possible for clusters to talk with each other and execute tasks. Kube-proxy is for maintaining network rules in each node

## Control Plane
It mainly runs an **API server**, which is also a container. It is the entry point to the cluster, which different K8s clients will talk to like UI, scripts, and CLI. You can use Kubectl to talk with it.

Other is **Controller Manager**, which keeps an overview in the cluster, like repairs, replacements, restarts, namespaces etc.

Another one is **Scheduler**, which is responsible for scheduling containers on different nodes based on workload. It decides where to put the Pod to.

Another one is **etcd**, which is a key-value storage which anytime holds the current state of the Kubernetes cluster. It keeps config data, status data of each node and container. Backup and is also made from etcd
> The most crucial maintenance tasks is backing up etcd. If etcd is lost, the cluster is lost



# Deployment
Deployments are blueprints for replicas, pods, etc. It is an abstraction of Pods.
- You mostly work with deployments, not Pods

> [!Warning]
> DB can't be replicated via deployment! 

To replicate DBs, you use [[Components#StatefulSet|StatefulSet]].

- Deployment = for **stateless** apps
- StatefulSet = for **stateful** apps or databases

## Creating a Pod
![[creating_pod.png]]