![[OpenStack Hierarchy.png]]
# Most Common Services
## Nova
Primary compute engine, responsible for instance scheduling, creation and termination.

Supports:
- QEMU/KVM
- Hyper-V
- VMware ESXi
- Zen

For scaling, you would put the Nova instances in a **Server Group** with anti-affinity policy (to prevent ending up in the same host) and front them with a **Load Balancer (Octavia)**.

## Glance
Image service, responsible for uploading, managing, and retrieving cloud images for instances running on OpenStack. Works across variety of stores. It uses *Ceph* to store images


## Neutron
It provides network connectivity between instances, enabling multi-VM deployments. It uses SDN technologies, including Open Virtual Network (OVN), Open vSwitch (OVS), Juniper Contrail etc.

## Cinder
It is a block storage component that is responsible for provisioning, management and termination of persistent block devices. They can later be attached to instances for persistent block storage.

## Swift
Swift is another storage component that provides a highly available and scalable object storage service similar to S3. It enables storing and retrieving unstructured data objects using a RESTful API for both OpenStack services and instances running on the cloud.

## Keystone
An identity service, providing authentication and authorization functions for the users for multi-tenancy. It can be integrated with external systems like LDAP or Active Directory.

# Less Common Services
## Horizon 
It is a dashboard to use with a web browser. Ships with 3 main dashboards: User dashboard, System dashboard, and Settings dashboard.

## Heat
It is a service to orchestrate multiple composite cloud applications using templates

## Other

| Service    | Description                                        |
| ---------- | -------------------------------------------------- |
| Mistral    | Workflow management through YAML                   |
| Ceilometer | Telemetry for billing and components               |
| Trove      | Database as a service, relational & non-relational |
| Ironic     | Provisioner of bare metal instead of VM            |
| Octavia    | Load balancer                                      |
