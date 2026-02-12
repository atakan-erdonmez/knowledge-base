Each config data has 3 parts:
#### 1) metadata
It includes name, labels etc

#### 2) specification
It includes replicas, selector, template, ports etc.
- It will have different attributes for different services

#### 3) status
It will be automatically generated. It will check if the desired status is equal to actual status.
- It is updated continuously
- The status information comes from etcd


> You generally store the config with your code


# Config File

[[Manifest Basics]]


In order to stop a deployment, you either have to delete the deployment, or scale to 0 pods
`kubectl delete deploy my-deployment`

> Deployments create ReplicaSet, and they create pods