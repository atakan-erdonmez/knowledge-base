In order to changes to the cluster, you have to talk with *API server*. To do that, you can use UI, API or CLI, which is kubectl. 
- It can be used for any cluster like cloud, minikube etc.


| kubectl Command                     | Action                                     |
| ----------------------------------- | ------------------------------------------ |
| run NAME --image=nginx              | Quickly run a pod without manifest         |
| port-forward NAME LOCALPORT:CTPORT  |                                            |
| exec -it NAME -- sh                 | Interactive shell to container             |
| kubectl cp LOCALFILE REMOTE:RFILE   |                                            |
| get RESOURCE                        |                                            |
| - `kubectl get pods`                | Shows the pods                             |
| - `kubectl get pods -n kube-system` | Show pods in kube-system namespace         |
| - `kubectl get namespace`           | Show namespaces                            |
| apply \| delete -f FILE \[--all]    | Apply the YAML file, like creating a file. |
| describe RESOURCE RESOURCE_NAME     |                                            |
| - `kubectl describe pod my_pod`     | Give detailed info about an object         |
| delete RESOURCE RESOURCE_NAME       |                                            |
| create ns NAMESPACE_NAME            | Create namespace                           |
| kubectl top {pods \| nodes}         | Get usage metrics from objects             |
| kubectl logs demo-pod               | Show logs                                  |
| kubectl get pods -L LABEL           | Show the label as a separate column        |



## Scale & Deployment

| kubectl Command                                     | Action |
| --------------------------------------------------- | ------ |
| kubectl scale deploy demo-deploy --replicas 3       |        |
| kubectl get deploy                                  |        |
| kubectl create deployment demo-deploy --image=nginx |        |

## Rollout & History

`kubectl rollout history deploy demo-deployment` -> show history
`kubectl rollout undo deploy demo-deployment` -> roll back to the previous version