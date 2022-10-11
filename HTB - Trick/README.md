# HTB - Trick
## Information Gathering

![](ipHtb.png)

Hal pertama yang harus kita lakukan adalah mengumpulkan sebanyak mungkin informasi  mengenai server yang akan kita serang. Disini gw ingin mencari tahu port/service dan OS apa yang dijalankan pada server tersebut.
langsung saja gw menggunakan masscan untuk melihat port apa saja yang terbuka

>masscan --rate 500 -p1-65535,U:1-65535 -e tun0 10.10.11.166

* --rate 500   = kecepatan proses scanning
* -p1-65535    = menscan port number dari 1 - 65535
* U:1-65535    = menscan port number UDP dari 1 - 65535
* -e           = network interface
* 10.10.11.166 = ip target

![](masscan.png)

ternyata yang terbuka adalah port 80,53,22,25. sekarang gw akan menggunakan nmap untuk melihat service, versi, dan OS yang dijalankan

>nmap 10.10.11.166 -p 80,53,22,25 -T5 -A

* 10.10.11.166 = ip target
* -p           = port
* -T5          = set timing 5 (mempercepat scan)
* -A           = all (os scan, script, version, traceroute) 

![](nmap.png)

ternyata server tersebut menjalankan ssh,smtp, dns, http. gw pribadi akan memulai enumerasi dati http>dns>smtp>ssh, dan jangan lupa pada nmap juga ditemukan bahwa host yang digunakan adalah trick.htb. maka tambahkan tersebut pada /etc/hosts

![](etchosts1.png)

jika sudah waktu nya melakukan enumerasi

## Enumeration

### Port 80 :http

kita dapat mengakses protocol http dari browser

![](web1.png)

langsung saja gw mencari direktori atau file apa saja yang berada pada web tersebut menggunakan ffuf

![](ffuf1.png)

ternyata pada web tersebut tidak ada file atau direktori yang menarik

lalu yang gw lakukan selanjut nya  mengenum subdomain nya menggunakan ffuf

![](ffufsubdo1.png)

dan ternyata juga tidak ditemukan. berarti untuk sejenak gw bakal berpindah untuk mengenum dns mungk