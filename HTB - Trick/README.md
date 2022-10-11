# HTB - Trick
## Information Gathering

![](ipHtb.png)

Hal pertama yang harus kita lakukan adalah mengumpulkan sebanyak mungkin informasi  mengenai server yang akan kita serang. Disini saya ingin mencari tahu port/service dan OS apa yang dijalankan pada server tersebut.
langsung saja saya menggunakan masscan untuk melihat port apa saja yang terbuka

>masscan --rate 500 -p1-65535,U:1-65535 -e tun0 10.10.11.166

* --rate 500   = kecepatan proses scanning
* -p1-65535    = menscan port number dari 1 - 65535
* U:1-65535    = menscan port number UDP dari 1 - 65535
* -e           = network interface
* 10.10.11.166 = ip target

![](masscan.png)
