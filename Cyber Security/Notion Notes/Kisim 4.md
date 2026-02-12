- [cupp.py](http://cupp.py): Kisiye ozel wordlist
    
- cewl -d <derinlik> -m<min cha> <link> -w /path/ : Web sitesindeki kelimeler
    
- Secure, HttpOnly (no js), path=/, SameSite gibi ozellikler cookie guvenligini arttirir ve CSRF riskini azaltir
    
- Mail header injection'da yakalanan pakette mail &bcc=hedefmail& eklenirse mail oraya da yonlendirilir
    
- locate webshells ile shell'ler bulunabilir
    
- SSRF stands for Server-Side Request Forgery: Sanki kendi kendine istek atiyormus gibi gostermektir. RFI kullanir. Server'daki kodu RFI ile calistirip recursive gibi islem yapilir.
    
- sqlmap -r ile bir dosya taranabilir (—dbs)
    
- Web tarayicilarinda Inspect→Application kismindan hassas veriler kontrol edilmelidir
    
- padbuster araci ile cookie bilgisi decode edilebilir
    
    - padbuster [http://giris.php](http://giris.php) <cookie_value> 1(blocksize deneme yanilma) <cookie_name>=<cookie_value> —encoding 0 → Cookie cozumlenir (cozumlu hali user=atakan olsun)
    - Ardindan "—encoding 0 —plaintext user=admin" ile 'Oracle Padding' saldirisi gerceklesmis olur
- nikto gelismis bir web-server scanner'dir. nikto -h <host>.
    
- cadaver: WebDAV kullanan bir server-yonetim uygulamasi. cadaver <URL>
    
- WebDAV: Sunucudaki dosyalari kontrol edip islem yapmaya yarayan protokol
    
- nosniff: Bir HTTP ozelligi. Dosyanin icerigine bakarak uzantisina karar verir.
    
- sslscan: SSL/TSL scanner. sslscan [options] [host:port | host]
    
- nmap script uzantisi *.nse'dir
    
- &,; gibi karakterler ile command exec yapilabilir
    
- CSRF'te orneginde sifre degistirince URL'de gozukur. Link duzenlenip kurbana ulastirlirsa sifresi linkteki degere gore degisir
    
- BurpSuite Proxy→Send to Intruder→login+password add→Intruder-cluster bomb set payloads ile brute force yapilir
    
- SQL Injection'da BurpSuite Proxy ile yakalann veriler .hed uznatisi ile export edilir. Ardindan "sqlmap -r dosyaadi.hed —dbs ile cesitli parametreler denenerek database bulunur
    
- Blind veritabani islemleri cok uzun surebilir
    
- Robots.txt ifsasi ile cesitli dosyalar elde edilebilir
    
- Bazen tarayicida SQLINJ calismiyormus gibi gozukur. Bu durmda tragigin BurpSuite tarafindan izlenmesi gerekir
    
- URI'da php&s1=<script></script>&s2 gibi bir kod varsa script taginin icine &s2 disina &s3 yazarak fragment edilebilir
    
- CAPTCHA atlatirken "User Agent Switcher" web eklentisi kullanilarak mobil cihazdan giriyormus gibi gosterilip bypass edilebilir
    
- IP rejection atlatilirken BurpSuite ile Content-Length: altina X-Forwarded-For: eklenir
    
    - Content-Length: 42
    - X-Forwarded-For: <Spoofed IP>

### Eski mufredat

- WebPageMaker ile websayfasi hazirlanabilir
    
- HizliResim websitesi ile internete kalici bir resim yuklenebilir (linkler icin)
    
- weevely: Web-shell for post-exploitation
    
    weevely generate <pass> <path>
    
    weevely <URL> <pass>
    
- PhoneInfoga ile telefon numaralari hakkinda bilgi toplanabilir
    
- Shellter(win) programi ile payload uygulamalarin icine gomulerek malware'lar antiviruslerden gizlenebilir
    
- hash-identifier ile hash tipi belirlenebilir
    
- findmyhash ile hash daha once kirilmis mi diye internete bakilabilir
    
- john —format=raw-MD5 <path> —show
    
- [wphashcrack.py](http://wphashcrack.py) ile hash kirilabilir