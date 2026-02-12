- DNS Analysis
    
    - dnsenum: Server records, subdomains, zone transfer etc. (S)
    - dnsrecon: DNS records, IP etc. (-d <domain>) (you can use -t brt for subdomains or -k for [crt.sh](http://crt.sh) certificate)
    - dig: Improved nslookup (S)
    - aux/gather/enum_dns: Zone transfer, reverse lookup etc.
    - dnswalk: Zone transfers (S)
    - fierce: IP, subdomain (—domain <>)
    - aux/scanner/dns/dns_amp
    - dnsdumpster


- Information
    
    - dmitry: DeepMagic (-winsepfb alayina bakiyor kullan)
    - maltego
    - aux/scanner/smtp/smtp_enum
    - aux/scanner/smtp/smtp_version
    - smtp-user-enum
    - urlcrazy: Similar domain finder
    - auxiliary/gather/search_email_collector: E-mail finder
    - theHarvester: E-mail finder (-d<dom>)
    - padbuster: Padding Oracle attacker
    - goofile: File searcher
    - admin/…/mysql_sql
    - auxiliary/scanner/mysql/mysql_schemadump
    - auxiliary/scanner/mysql/mysql_hashdump


- Identification
    
    - whois (S)
        
    - whatweb: Detailed scanner (S)
        
    - wafw00f: Firewall detection (S)
        
    - [recon-ng](https://www.notion.so/Recon-ng-Usage-7b7e7212529441b694ba4c505a2c40a7?pvs=21): General web framework
        
    - spiderfoot: Olagandisi OSINT framework (spiderfoot -l localhost:port)
        
    - aux/scanner/smtp/smtp_version: SMTP banner grabber
        
    - aux/scanner/portscan/tcp
        
    - smtp-user-enum
        
    - smtp-check: SMTP setup checker
        
    - ike-scan: Discover IKE usage (S)
        
    - webscarab: (old) proxy
        
    - ffuf
        
    - Spider
        
        dirb: Subdomain
        
        dnsmap: Subdomain
        
        dirbuster: Subdomain
        
        sublist3r: Subdomain
        
        Breacher: Admin panel finder



- Network
    
    - [nmap](https://www.notion.so/Nmap-Usage-c012c7b21d2d423e8ce16d2e8d50dc3d?pvs=21)
    - p0f: Sniff network
    - netdiscover
    - tcpdump
    - traceroute
    - tcptraceroute
    - macchanger
    - SMB
        - nmap -p 445 --script=smb-enum-shares.nse,smb-enum-users.nse MACHINE_IP
        - smbclient //<ip>/anonymous
        - smbget -R smb://<ip>/anonymous
        - nmap -p 111 --script=nfs-ls,nfs-statfs,nfs-showmount MACHINE_IP
        - enum4linux
        - metasploit `smb_enumshares`  and `smb_version`