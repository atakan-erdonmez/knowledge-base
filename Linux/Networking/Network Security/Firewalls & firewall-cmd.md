- netfilter is a part of Linux kernel. It is the main firewall. It reads the input-output packets and allow/deny them.
- **netfilter** used iptables, ip6tables, arptables etc. But now, these are all deprecated. Instead, nftables is used.
- nftables has couple of advantages over iptables, including speed, better packet processing.

FirewallD **was** a frontend to iptables. It was directly modify netfilter directly. But now, it uses **nftables** with command **nft**.

An important note is, after each modification, you need to reload firewalld so that your changes can take place. (?)

`sudo firewall-cmd --reload`

## FirewallD

### Commands
| Command                                                                        | Description                            |
| ------------------------------------------------------------------------------ | -------------------------------------- |
| `firewall-cmd --list-all`                                                      | Default zone info                      |
| `firewall-cmd --get-default-zone`                                              | Get default zone                       |
| `firewall-cmd --get-active-zones`                                              | Get active zones                       |
| `firewall-cmd --list-services`                                                 | List all enabled services in firewalld |
| `firewall-cmd --zone=public --list-all`                                        | List everything about public zone      |
| `firewall-cmd --zone=public --remove-service=ssh`                              | Remove SSH from public zone            |
| `firewall-cmd --zone=public --add-service=ssh`                                 | Add SSH to public zone                 |
| `firewall-cmd --zone=public --add-port=2222/tcp`                               | Allow port 2222                        |
| `--permanent`                                                                  | Make changes persistent                |
| `firewall-cmd --zone=public --add-forward-port=port=80:proto=tcp:toport=12345` | Port forward 80 → 12345                |
| `firewall-cmd --zone=public --add-masquerade`                                  | Enable masquerading                    |
| `--add-forward-port=port=80:proto=tcp:toport=12345:toaddr=<IP>`                | Port forward with IP                   |



> Cockpit is a browser-based Linux administration tool.



### Zones

- Drop Zone
- Block Zone
- Public Zone
- External Zone
- DMZ Zone
- Work Zone
- Home Zone
- Internal Zone
- Trusted Zone

>[!Masquerade]
>Masquerading su: Normalde client’in attigi paket sunucuda client’tan gelmis gibi gozukurken masquerading acikken client firewall’a paketi yolluyor, firewall da masquerading yapip servera paketi sanki kendisi yolluyormus gibi gonderiyor. Yani proxy gibi davraniyor.



### Rich Rules

firewall-cmd \[option] \[rule]

| Option                            | Descriptoin                                                                                                                                                                                                 |
| --------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `--add-rich-rule='[RichRule]'`    | Add specified \[_RichRule_] rule to default zone. To add rule in other zone, provide its name as argument with _**--zone**_  <br>option. To add rule permanently use _**--permanent**_ option.              |
| `--query-rich-rule='[RichRule]'`  | Figure out whether the specified rule is added in default zone or not. To query in other zone, provide its name with _**--zone**_  option.                                                                  |
| `--remove-rich-rule='[RichRule]'` | Remove specified \[_RichRule_] rule from default zone. To remove rule from other zone, provide its name as argument with _**--zone**_  <br>option. To remove rule permanently use _**--permanent**_ option. |
| `-list-rich-rules`                | List all rules from default zone. To list rules from other zone, provide its name as argument with _**--zone**_  <br>option.                                                                                |



##### Syntax
```
[source] [destination]
{service|port|protocol|icmp-block|masquerade|forward-port}
[log] [audit]
[accept|reject|drop]
```



```

firewall-cmd —add-rich-rule='rule family=ipv4 source address=IP service name=ssh accept'

—add-rich-rule='rule family=ipv4 source address=IP service name=ssh log prefix=”SSH Access from webserver” level="notice" accept' (prefix kismi loglarda aciklama olarak gibi gozukuyor)

—add-rich-rule='rule protocol value=icmp reject’ : Reject ICMP

firewall-cmd --panic-on : Block all incoming/outgoing packets
```

conf dosyasinda lockdown=yes yaparak kurallari sabitleyebiliriz
