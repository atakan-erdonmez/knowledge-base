Hey everyone! In this blog, I will share my Minecraft server installation with Pterodactyl. I am not completely done yet, I just did the basics, and I couldn't test it yet. So there might be multiple parts to this.

## Why Pterodactyl?
I was using a simple jar file and running the java -jar command to execute it. However, since it was hard to control and maintain it. I needed to restart it manually, and it was hard to take backups and adjust settings.

So I was looking for a game server software. I saw AMP, but didn't want to give money right now, which let me to Pterodactyl. It seemed kinda complex, so it was a great challenge for me.


## Installation Steps
### Test VM
In my Proxmox server, I created a VM from my Ubuntu server template. Then, I followed the Pterodactyl documentation exactly. I am not used to using Redis and PHP, so it was a little different experience for me. I mainly followed the given example code.

https://pterodactyl.io/panel/1.0/getting_started.html

It installed necessary software and dependencies. Then, I continued to set up the database.

Since this was a test installment, I didn't use SSL and used my local IP instead of a domain and FQDN. I basically copied all the commands and researched them.

### Webserver Config

I went with nginx, and didn't use SSL to simplify the process. I just followed the documentation.

### Wings
Installing wings was a little weird, because the documentation doesn't exactly specify the workflow. I had some hard time understanding what is egg and what is wings. And still I am not 100% sure.

However, after following the documentation, I was able to install wings and daemonize it. 

### Configuring Wings

After that, I dove into GUI. I first created a location, then a node. Since I was just trying this out, I didn't give much attention to details like allocations. However, as far as I can see, there are lots of options and this software can be used in much much bigger instances with multiple nodes. 

![[Nodes.png]]![[Server.png]]

I just put config details when it asked, and I generally didn't constraint anything.

Right now, it looks like it is done. I will try if its working as soon as I can sit in front of my gaming PC.