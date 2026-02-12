## Node
A physical or a virtual server. Used for computation
## Pod
This is the smallest unit. It is a layer above the container. It is necessary for Kubernetes layer
- Usually *1 application* per Pod
- Each pod gets its *own IP address*
- When a pod dies, the same IP stays, due to the use of **service**

## Service
It is a permanent IP address. Lifecycle of Pod and Service are *not connected*. It is also a *load balancer*.
- There are two types: Internal and External
- Internal is the default. Used for internal communication between Pods
- External is used to access resources from outside, like a web service

## Ingress
It is a service to take external requests and forward them to internal resources
- To route traffic

## ConfigMap & Secret
Normally, for every small change, you have to re-build the image, re-deploy etc. ConfigMap solves this, as it is *external configuration of your application*.
- It holds configs like URLs, database configs etc.
>  ConfigMap is for non-confidential data only

For confidential data, K8s uses Secret.
- It is like ConfigMap, but for secret data

## Volumes
It is persistent data. Can be local or remote.

## StatefulSet
It is meant for stateful apps like MySQL, mongoDB, elastic etc. It make sure reads & writes are synchronized.
- It can be hard to set them up

>[!TIP]
>Since hosting stateful apps in a cluster is hard, DBs are often hosted **outside** of the cluster.

