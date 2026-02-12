---
tags:
  - Package_Manager
---


- RPM keeps the information of all the installed packages under /var/lib/rpm

- Five basic modes for RPM command:

	- Install: rpm -ivh packet.rpm (-i install -v verbose -h yuzdelik goster hashtag kullanarak)
	- Remove: rpm -e
	- Upgrade: rpm -Uvg packet.rpm
	- Verify: rpm -Vp packet.rpm (verify package)
	- Query: rpm -ql BitTorrent (look for program in system [related files dependencies etc.] -ql query list)




- -i : Install
- -e : Erase
- -u : uninstall
- -v : Verbose
- -q : Query (check if installed)
- -a : All
- -p : Package
- -i : Information
- —nodep : Don’t check dependencies

rpmverify : verify integrity of RPM packages

**Useful commands:**
    
    - rpm —checksig packet.rpm : Check signature
    - rpm -qpR packet.rpm : Check for dependencies (-q query package -p list capabilities that package provides -R list capabilities on which this package depends)
    - rpm -ivh —nodeps packet.rpm (—nodeps dont resolve dependencies)
    - rpm -qa —last : List all recently installed rpm packages (-qa query all)
    - rpm -qa : All installed packages
    - rpm -ev —nodep packet : Remove package without checking dependencies
    - rpm -qf /usr/bin/htpasswd : Query a file that which RPM packages it belongs
    - rpm -qi vsftpd : Package informatioin (-qi query info)
    - rpm -qip packet.rpm (Information about RPM package)
    - rpm -qdf /usr/bin/vmstat : Display documentation files about a program or packet
    - rpm -Va : Verify all packages

