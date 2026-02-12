## Bolum 2

- Torghost -s (start) -x (stop): 10 dakikada bir IP degistir
- macchanger -r (random) -p (permanent/asil) -m <manual> -a (another/randomvendor) eth0: Change MAC address

## Bolum 3

- theHarvester -d <domain> -b <search engine> -l <limit of mails>: E-mail harvester
- Reverse-IP domain check ile ayni sunucuda olan web-hostlari kesfedilebilir
- Netcraft site hakkinda bazi teknik bilgileri toplamaya yarar.
- Bazen sayfa kaynaginda bazi bilgiler yazilmis/unutulmus olabilir
- exploit-db, google hacking → google dorks
    - shodan→sunucu arama
    - postebin.com→Anonim paylasimlar, hacklenmis web siteleri, TR'de yasakli
    - pipl.com→kisi arama motoru
    - images.google, tineye→resim, gorsel arama motoru
- Bazen traceroute yerine tcptraceroute kullanmak ise yarayabilir
- wafw00f programi firewall tespitinde kullanilir (-l ile bulunabilen firewall'lar listelenir)
- -fierce -dns <>: DNS scan&subdomain
- -dnsrecon -d <>: DNS scan&enumeration
- ++dnsenum <>: DNS scanner
- fierce <>: otomatik brute-force, subdomain
- sublistr -d <domain> -b <bf>: Subdomain tespiti
- smtp-user-enum _M VRFY/EXPN/RCPT(Tekli/Coklu/?) -U ./wordlist -T <IP>: SMTP analiz
- finger -lmsp user@host: Kullanici host'ta var mi diye bakilir
- Emali'in orijinali incelenerek gectigi ve gonderildigi sunucular gibi bilgilere ulasilabilir.
- Banner grabbing icin telnet, nc, curl, msf vs nmap script'i kullanilabilir
- Banner yakalayarak servislerin versioynu gibi bazi kritik bilgiler ogrenilebilir
- whatweb ile banner bilgileri ogrenilebilir
- snmp-check: SNMP enumerator
- Sitede belge bulabilmek icin
    - Google → site: [istanbul.edu.tr](http://istanbul.edu.tr) filetype:pdf
    - FOCA (only windows)

## Bolum 4 (Kesif calismalari/nmap)

- nmap -sn ile aktif olan IP'ler builunur (ping scan - no port)
- nmap -iL ile coklu hedef dosyasi secilebilir (input filename)
- nmap —exclude ve —excludefile ile bazi IP'ler haric birakilabilir
- nmap -p <> ile belirtilen port, -p- ile tum portlar taranir
- nmap -sT → TCP, -sU → UDP, -p T:80 , -p U:53
- -O → OS taramasi
- -sV → versiyon bilgisi
- nmap -sA (TCP ACK) ile filtreleme/guvenlik duvari tespiti yapilabilir
- tcpdump host <IP> ile route'taki paketler izlenebilir. Normal nmap paketleri 24 byte'dir. -f ile 8'e -ff ile 16 byte'a dusurulebilir. Ya da —mtu ile manuel ayarlanabilir.
- nmap —spoof-mac <MAC>/0 ile mac spoofing yapilabilir (0→random mac)
- -D ile IP spoofing yapilabilir
- -oN normal -oX xml -F : fast
- -A ile agresif tarama gerceklesir: -sV -sC(script) -O —traceroute

## Bolum 5 (Guvenlik acigi tarama)

- Nessus: Parali coklu tarayici
- OpenVAS: Ucretsiz coklu (bozuk)
- Netsparker: Ucretli web
- Acunetix: Sureli coklu
- Zaproxy: Ucretsiz web
- Skipfish: Ucretsiz web
- Wapiti: Blackbox ucretsiz web
- Rapidscan: Ucretsiz web +80 program
- XSSPWN: Ucretsiz XSS +250 program
- Nosqlmap: Link sql
- dotdotslash: Directory traversal
- LFISuite: RFI/LFI scanner

## Bolum 6 (Exploit)

- exploit-db, pocketstormsecurity ile exploit aramasi yapilabilir
- wesng programiyla windows local exploit aranabilir (exploit suggester)
- bitsadmin bir windows dosya transfer sistemidir

## Bolum 7 (Eski)

- dnsenum: DNS bilgiler
- whatweb: Versiyon script bilgileri + programlama dilleri
- dirbuster: Dosya-dizin arayici
- theHarvester -d <domain> -l <limit> -b <search engine>: E-posta tespiti
- Breacher ile admin-panel bulunabilir
- urlcrazy: Benzer domain bulma
- Bazen SQL sorgularinda URI'da bosluk oldugu icin programlar SQL acigi tespit edemeyebilir. URL space filtering yapilmis olabilir
- Robots.txt: Search engine'lerin neleri indexleyecegini gosterir

Not: 64 bit programlar sadece 64 bit sistemlerde calisirken 32 bit programlar hem 64 bit hem de 32 bit'lik sistemlerde calisabilir