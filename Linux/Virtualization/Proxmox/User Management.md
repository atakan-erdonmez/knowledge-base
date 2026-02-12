# Realms
PAM: Realm for actual Linux
PVE: For Proxmox 

A PAM user can ssh into a server, a PVE user can not. PVE user is generally enough for management and administration

A PAM user is not necessary to create in Proxmox GUI. You have to create it in the Linux shell in any way, it doesn't work if only created in GUI. In GUI, it only works as a reference, so you can understand that you have that user in the underlying linux

# Groups
To manage users, you can put them in groups. Then in Permissions tab, you can define group permissions
# Permissions
You can define permissions for users and groups