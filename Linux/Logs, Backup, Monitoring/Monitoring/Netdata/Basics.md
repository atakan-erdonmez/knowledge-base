Netdata doesn't "store" any info, it only "streams".

Uses port 19999

- `systemctl status netdata`

/etc/netdata -> Main config file

/etc/netdata/netdata.conf -> default config file. To change, run the command below and rename


`sudo netdatacli dumpconfig > ~/netdata.conf` -> dump all config into a file

And apply changes via
`sudo netdatacli reload-health`

## edit-config file
creates a file with default config
`sudo ./edit-config health.d/cpu.conf`
# Installation


```
wget -O /tmp/netdata-kickstart.sh https://get.netdata.cloud/kickstart.sh && sh /tmp/netdata-kickstart.sh
```

For the cloud, you should add the nodes manually

> [!log2journal]
> It is a program used to send text-logs to journal. It belongs to Netdata

