Note: The actual files that hold these lists are in `/var/spool/cron` but we don’t manually edit them.

[https://crontab.guru/](https://crontab.guru/)



![[Cron1.png]]


![[cron2.png]]


- - - - - → Dakika (0-59), Saat (0-23), Gun (1-31), Ay (1-12), Haftanin gunu (0-6 0isSunday)

Examples:

0 11,16 * * * → 11 ve 16’da

0 11-16 * * * → 11’den 16’ya kadar her saat basi

0 */1 * * * → Saat basi

0-10/2 * * * * * → Ilk 10 dakika her 2 dakikada bir

set: Show all variables

env: Show environmental variables

local: Show local variables

crontab -l : List scheduled jobs

crontab -e : Edit scheduled jobs

/etc/crontab : System-wide cron


> Note: Prefer [[systemd timers]]
> For one-time events, you can use [[at]]