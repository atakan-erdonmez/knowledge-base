# Global Services

When you create a service with replicas, the Swarm creates that many instances.

However, if you want to have a service that exist in every replica, you should use **global service**.
`docker service create --name myservice2 --mode global nginx`
You can use this for a monitoring service for example.

# Reserving CPU & Memory
`--reserve memory` and `--reserve cpu` can be used to reserve resources for a specific service

# Constraint
When deploying or updating a service, you can apply a constraint (a filter) using tags to deploy on specific nodes.

`docker service create --name test --replicas 5 --constraint node.labels.ID==east`

## Add a Tag to a Node
`docker node update --label-add ID=east <node_id>`

# Placement Preferences
`--placement-pref 'spread=node.labels.datacenter'`
Means distribute containers evenly