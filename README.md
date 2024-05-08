# Jarkom-Modul-2-it12-2024

## Anggota
| Nama    | NRP     | 
| ------- | ------- | 
| Rehana Putri Salsabila     | 5027221015     | 
| Muhammad Rifqi Oktaviansyah     | 5027221067     | 

# Laporan Resmi
## Daftar Isi
- [Laporan Resmi](#laporan-resmi)
  - [Daftar Isi](#daftar-isi)
  - [Topologi](#topologi)
  - [Config](#config)
  - [Sebelum Memulai](#sebelum-memulai)
- [Soal 1](#Soal-1)
  - [Script](#script)
  - [Result](#result)
- [Soal 2](#Soal-2)
  - [Script](#script-1)
- [Soal 3](#Soal-3)
  - [Script](#script-2)
- [Soal 4](#Soal-4)
  - [Script](#script-3)
- [Soal 5](#Soal-5)
  - [Script](#script)
  - [Result](#result)
- [Soal 6](#Soal-6)
  - [Script](#script)
  - [Result](#result)
- [Soal 7](#Soal-7)
  - [Script](#script)
  - [Result](#result)
- [Soal 8](#Soal-8)
  - [Script](#script)
  - [Result](#result)
- [Soal 9](#Soal-9)
  - [Script](#script)
  - [Result](#result)
- [Soal 10](#Soal-10)
  - [Script](#script)
  - [Result](#result)
- [Soal 11](#Soal-11)
  - [Script](#script)
  - [Result](#result)
- [Soal 12](#Soal-12)
  - [Script](#script)
  - [Result](#result)
- [Soal 13](#Soal-13)
  - [Script](#script)
  - [Result](#result)
- [Soal 14](#Soal-14)
  - [Script](#script)
  - [Result](#result)
- [Soal 15](#Soal-15)
  - [Script](#script)
  - [Result](#result)
- [Soal 16](#Soal-16)
  - [Script](#script)
  - [Result](#result)
- [Soal 17](#Soal-17)
  - [Script](#script)
  - [Result](#result)
- [Soal 18](#Soal-18)
  - [Script](#script)
  - [Result](#result)
- [Soal 19](#Soal-19)
  - [Script](#script)
  - [Result](#result)
- [Soal 20](#Soal-20)
  - [Script](#script)
  - [Result](#result)


## Topologi
![image]()

## Config  --belom diatur
- **Pandudewanata**
  ```
  auto eth0
  iface eth0 inet dhcp

  auto eth1
  iface eth1 inet static
          address 192.173.1.1
          netmask 255.255.255.0

  auto eth2
  iface eth2 inet static
          address 192.173.2.1
          netmask 255.255.255.0

  auto eth3
  iface eth3 inet static
          address 192.173.3.1
          netmask 255.255.255.0
  ```
- **Yudhistira**
  ```
  auto eth0
  iface eth0 inet static
          address 192.173.1.2
          netmask 255.255.255.0
          gateway 192.173.1.1
  ```
- **Nakula**
  ```
  auto eth0
  iface eth0 inet static
          address 192.173.1.3
          netmask 255.255.255.0
          gateway 192.173.1.1
  ```
- **Werkudara**
  ```
  auto eth0
  iface eth0 inet static
          address 192.173.2.2
          netmask 255.255.255.0
          gateway 192.173.2.1
  ```
- **Sadewa**
  ```
  auto eth0
  iface eth0 inet static
          address 192.173.2.3
          netmask 255.255.255.0
          gateway 192.173.2.1
  ```
- **Prabukusuma**
  ```
  auto eth0
  iface eth0 inet static
          address 192.173.3.2
          netmask 255.255.255.0
          gateway 192.173.3.1
  ```
- **Abimanyu**
  ```
  auto eth0
  iface eth0 inet static
          address 192.173.3.3
          netmask 255.255.255.0
          gateway 192.173.3.1
  ```
- **Wisanggeni**
  ```
  auto eth0
  iface eth0 inet static
          address 192.173.3.4
          netmask 255.255.255.0
          gateway 192.173.3.1
  ```
- **Arjuna**
  ```
  auto eth0
  iface eth0 inet static
          address 192.173.3.5
          netmask 255.255.255.0
          gateway 192.173.3.1
  ```
- **Notes of Config**
  ```
  Pandudewanata	: 192.173.1.1 (Switch 1)
  Yudhistira	: 192.173.1.2
  Nakula	        : 192.173.1.3
  Pandudewanata	: 192.173.2.1 (Switch 2)
  Werkudara	: 192.173.2.2
  Sadewa	        : 192.173.2.3
  Pandudewanata	: 192.173.3.1 (Switch 3)
  Prabukusuma	: 192.173.3.2
  Abimanyu	: 192.173.3.3
  Wisanggeni	: 192.173.3.4
  Arjuna	        : 192.173.3.5
  ```

### Sebelum memulai --belom
setiap node, kita inisiasi pada `.bashrc` menggunakan `nano`

- **Pandudewanata**
  ```
  iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.173.0.0/16
  echo 'nameserver 192.168.122.1' > /etc/resolv.conf
  ```
- **Master & Slave**
  ```
  echo 'nameserver 192.168.122.1' > /etc/resolv.conf
  apt-get update
  apt-get install bind9 -y      
  ```
- **Client**
  ```
  echo -e '
  nameserver 192.173.1.2 # IP Yudhistira
  nameserver 192.173.2.2 # IP Werkudara
  nameserver 192.168.122.1
  ' > /etc/resolv.conf
  apt-get update
  apt-get install dnsutils -y
  apt-get install lynx -y
  ```

## Soal 1 
Untuk membantu pertempuran di Erangel, kamu ditugaskan untuk membuat jaringan komputer yang akan digunakan sebagai alat komunikasi. Sesuaikan rancangan Topologi dengan rancangan dan pembagian yang berada di link yang telah disediakan, dengan ketentuan nodenya sebagai berikut :
- DNS Master akan diberi nama Pochinki, sesuai dengan kota tempat dibuatnya server tersebut
- Karena ada kemungkinan musuh akan mencoba menyerang Server Utama, maka buatlah DNS Slave Georgopol yang mengarah ke Pochinki
- Markas pusat juga meminta dibuatkan tiga Web Server yaitu Severny, Stalber, dan Lipovka. Sedangkan Mylta akan bertindak sebagai Load Balancer untuk server-server tersebut

### Result 
**Ruins dan Apartments**
```
ping google.com -c 5
```
![image]()

## Soal 2
Karena para pasukan membutuhkan koordinasi untuk mengambil airdrop, maka buatlah sebuah domain yang mengarah ke Stalber dengan alamat airdrop.xxxx.com dengan alias www.airdrop.xxxx.com dimana xxxx merupakan kode kelompok. Contoh : airdrop.it01.com

### Script
Melakukan set up pada node DNS Master ( Pochinki )
**Pochinki**
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
    apt-get update
    apt-get install bind9 -y
    
echo 'zone "airdrop.it12.com" {
	type master;
	file "/etc/bind/jarkom/airdrop.it12.com";
    allow-transfer { 192.239.1.3; }; //IP Stalber
};' > /etc/bind/named.conf.local

cp /etc/bind/db.local /etc/bind/jarkom/airdrop.it12.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     airdrop.it12.com. root.airdrop.it12.com. (
                        2024050301      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      airdrop.it12.com.
@       IN      A       192.239.1.3  ; 
www     IN      CNAME   airdrop.it12.com.' > /etc/bind/jarkom/airdrop.it12.com


service bind9 restart
```

**Ruins**
Lakukan set up nameserver yang mengarah ke `IP Node Pochinki`
```
ping airdrop.it12.com -c 5
```
**Apartments**
Lakukan set up nameserver yang mengarah ke `IP Node Pochinki`
```
ping www.airdrop.it12.com -c 5
```


## Soal 3
Para pasukan juga perlu mengetahui mana titik yang sedang di bombardir artileri, sehingga dibutuhkan domain lain yaitu redzone.xxxx.com dengan alias www.redzone.xxxx.com yang mengarah ke Severny

### Script
Melakukan set up pada node DNS Master ( Pochinki )
**Pochinki**
```
echo 'zone "redzone.it12.com" {
	type master;
	file "/etc/bind/jarkom/redzone.it12.com";
    allow-transfer { 192.239.1.4; }; //IP Severny
};' > /etc/bind/named.conf.local

cp /etc/bind/db.local /etc/bind/jarkom/redzone.it12.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     redzone.it12.com. root.redzone.it12.com. (
                        2024050301      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      redzone.it12.com.
@       IN      A       192.239.1.4  ; 
www     IN      CNAME   redzone.it12.com.
' > /etc/bind/jarkom/redzone.it12.com


service bind9 restart
```
**Ruins**
Lakukan set up nameserver yang mengarah ke `IP Node Pochinki`
```
ping redzone.it12.com -c 5
```
**Apartments**
Lakukan set up nameserver yang mengarah ke `IP Node Pochinki`
```
ping www.redzone.it12.com -c 5
```


## Soal 4
Markas pusat meminta dibuatnya domain khusus untuk menaruh informasi persenjataan dan suplai yang tersebar. Informasi persenjataan dan suplai tersebut mengarah ke Mylta dan domain yang ingin digunakan adalah loot.xxxx.com dengan alias www.loot.xxxx.com

### Script
Melakukan set up pada node DNS Master ( Pochinki )
**Pochinki**
```
echo 'zone "loot.it12.com" {
	type master;
	file "/etc/bind/jarkom/loot.it12.com";
    allow-transfer { 192.239.2.4; }; //IP Mylta
};' > /etc/bind/named.conf.local

cp /etc/bind/db.local /etc/bind/jarkom/loot.it12.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     loot.it12.com. root.loot.it12.com. (
                        2024050301      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      loot.it12.com.
@       IN      A       192.239.2.4  ; 
www     IN      CNAME   loot.it12.com.
' > /etc/bind/jarkom/loot.it12.com


service bind9 restart
```

**Ruins**
Lakukan set up nameserver yang mengarah ke `IP Node Pochinki`
```
ping loot.it12.com -c 5
```
**Apartments**
Lakukan set up nameserver yang mengarah ke `IP Node Pochinki`
```
ping www.loot.it12.com -c 5
```


## Soal 5
Pastikan domain-domain tersebut dapat diakses oleh seluruh komputer (client) yang berada di Erangel

### Result
![image]()

## Soal 6
Beberapa daerah memiliki keterbatasan yang menyebabkan hanya dapat mengakses domain secara langsung melalui alamat IP domain tersebut. Karena daerah tersebut tidak diketahui secara spesifik, pastikan semua komputer (client) dapat mengakses domain redzone.xxxx.com melalui alamat IP Severny (Notes : menggunakan pointer record)

### Script
- Run kode dibawah pada Pochinki
#### Pochinki
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
    apt-get update
    apt-get install bind9 -y

echo 'zone "1.239.192.in-addr.arpa" {
        type master;
        file "/etc/bind/jarkom/1.239.192.in-addr.arpa";
};' > /etc/bind/named.conf.local

mkdir /etc/bind/jarkom

cp /etc/bind/db.local /etc/bind/jarkom/1.239.192.in-addr.arpa

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     redzone.it12.com. root.redzone.it12.com. (
                        2003101001      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
1.239.192.in-addr.arpa. IN      NS      redzone.it12.com.
4                       IN      PTR     redzone.it12.com.'> /etc/bind/jarkom/1.239.192.in-addr.arpa

service bind9 restart
```

- Ubah nameserver client ke Erangel dengan `echo nameserver 192.168.122.1 > /etc/resolv.conf`, lalu lakukan command ini untuk tiap client
```
apt-get update
apt-get install dnsutils
```
- Lalu kembali ke nameserver Pochinki dengan `echo nameserver 192.239.3.2 > /etc/resolv.conf`
- Jalankan command pada client
```
host -t PTR 192.239.1.4
```
### Result
![image](https://github.com/rehanasalsabilla/Jarkom-Modul-2-it12-2024/assets/143682058/40306607-27c4-402c-9263-4d94532fb7b2)

![image](https://github.com/rehanasalsabilla/Jarkom-Modul-2-it12-2024/assets/143682058/3ebb55e7-d791-4596-b740-21b6196cd66f)

## Soal 7
Akhir-akhir ini seringkali terjadi serangan siber ke DNS Server Utama, sebagai tindakan antisipasi kamu diperintahkan untuk membuat DNS Slave di Georgopol untuk semua domain yang sudah dibuat sebelumnya

### Script

### Pochinki
- Jalankan `nano /etc/bind/named.conf.local`
- Edit konfigurasi dimana IP Georgopol `192.239.2.3` akan dijadikan DNS Slave
```
zone "airdrop.it12.com" {
    type master;
    also-notify { 192.239.2.3; };
    allow-transfer { 192.239.2.3; };
    file "/etc/bind/airdrop/airdrop.it12.com";
};

zone "redzone.it12.com" {
    type master;
    also-notify { 192.239.2.3; };
    allow-transfer { 192.239.2.3; };
    file "/etc/bind/redzone/redzone.it12.com";
};

zone "loot.it12.com" {
    type master;
    also-notify { 192.239.2.3; };
    allow-transfer { 192.239.2.3; };
    file "/etc/bind/loot/loot.it12.com";
};
```
- Lalu, start bind9 dengan `service bind9 start`

### Georgopol
- Pada Goergopol run kode bash dibawah
```
#!/bin/bash

# Check for root privileges
if [ "$(id -u)" -ne 0 ]; then
    echo "Please run this script as root"
    exit 1
fi

config() {
    # Check if BIND9 is installed
    if ! dpkg -l | grep -q bind9; then
        apt-get update 
        apt-get install -y bind9 nano 
    fi

    # Create directory for zone files if it doesn't exist
    mkdir -p /etc/bind/jarkom/

    # Create a zone configuration
    cat <<EOL > /etc/bind/named.conf.local
zone "airdrop.it12.com" {
    type slave;
    masters { 192.239.3.2; }; 
    file "/var/lib/bind/jarkom/airdrop.it12.com";
};

zone "redzone.it12.com" {
    type slave;
    masters { 192.239.3.2; };
    file "/var/lib/bind/jarkom/redzone.it12.com";
};

zone "loot.it12.com" {
    type slave;
    masters { 192.239.3.2; };
    file "/var/lib/bind/jarkom/loot.it12.com";
};

EOL

    # Restart BIND to apply changes
    service bind9 restart
}

# Call the function to execute the configuration
config

```
- Matikan bind9 pada Pochinki dengan command `service bind9 stop`
- Buka file resolve.conf pada tiap-tiap client dengan command `nano /etc/resolve.conf` lalu, tambahkan IP Georgopol
```
nameserver 192.239.3.2
nameserver 192.239.2.3
```
- Coba cek dengan ping website yang telah dibuat
![image](https://github.com/rehanasalsabilla/Jarkom-Modul-2-it12-2024/assets/143682058/18b677cc-eb98-449c-a2ee-d7c95e382352)

Dapat dilihat bahwa website masih error ketika di ping untuk case saya.

## Soal 8
Kamu juga diperintahkan untuk membuat subdomain khusus melacak airdrop berisi peralatan medis dengan subdomain medkit.airdrop.xxxx.com yang mengarah ke Lipovka

### Script

- Pada Pochinki, run code bash dibawah
```
#!/bin/bash

# Configure each domain
    config() {
cat <<EOL > /etc/bind/jarkom/airdrop.it12.com
\$TTL 604800
@   IN SOA airdrop.it12.com. root.airdrop.it12.com. (
               2024050302; Serial
                        604800 ; Refresh
                        86400  ; Retry
                        2419200 ; Expire
                        604800 ); Negative Cache TTL
@   IN  NS  airdrop.it12.com.
@   IN  A   192.239.1.2 
www IN CNAME airdrop.it12.com.
medkit  IN  A   192.239.2.3
@   IN AAAA ::1
EOL


    # Restart BIND to apply changes
    service bind9 restart
}

# Call the function to execute the configuration
config
```

### Result

![image](https://github.com/rehanasalsabilla/Jarkom-Modul-2-it12-2024/assets/143682058/b0ed3550-6c7b-4019-abef-73c9e9bf6ed9)

## Soal 9 
Terkadang red zone yang pada umumnya di bombardir artileri akan dijatuhi bom oleh pesawat tempur. Untuk melindungi warga, kita diperlukan untuk membuat sistem peringatan air raid dan memasukkannya ke subdomain siren.redzone.xxxx.com dalam folder siren dan pastikan dapat diakses secara mudah dengan menambahkan alias www.siren.redzone.xxxx.com dan mendelegasikan subdomain tersebut ke Georgopol dengan alamat IP menuju radar di Severny

## Script

### Pochinki
Jalankan `cp /etc/bind/jarkom/redzone.it12.com /etc/bind/jarkom/siren.redzone.it12.com`
Jalankan `nano /etc/bind/jarkom/siren.redzone.it12.com` lalu isi seperti dibawah
```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     redzone.it12.com. root.redzone.it12.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      redzone.it12.com.
@       IN      A       192.239.1.4
www     IN      CNAME   redzone.it12.com.
siren   IN      A       192.239.2.3
ns1     IN      A       192.239.2.3
siren   IN      NS      ns1
@       IN      AAAA    ::1
```
- Run command `nano /etc/bind/named.conf.options`
- Tambahkan line berikut
```
allow-query{any;};
```
![image](https://github.com/rehanasalsabilla/Jarkom-Modul-2-it12-2024/assets/143682058/3ab9defd-fbf7-45c2-a3c8-d60417c5be16)

- Run command `nano /etc/bind/named.conf.local` lalu tambahkan
```
zone "siren.redzone.it12.com" {
    type master;
    file "/etc/bind/siren/siren.redzone.it12.com";
    allow-transfer { 192.239.1.4; };
};
```
Restart bind9 dengan `service bind9 restart`

### Georgopol 
- Run command `nano /etc/bind/named.conf.options`
- Tambahkan line berikut
```
allow-query{any;};
```
![image](https://github.com/rehanasalsabilla/Jarkom-Modul-2-it12-2024/assets/143682058/3ab9defd-fbf7-45c2-a3c8-d60417c5be16)

- Run command `nano /etc/bind/named.conf.local` lalu tambahkan
```
zone "siren.redzone.it12.com" {
    type master;
    file "/etc/bind/siren/siren.redzone.it12.com";
};
```
- Jalankan command cp /etc/bind/db.local /etc/bind/jarkom/siren.redzone.it12.com

- Buka dan edit file /etc/bind/jarkom/siren.redzone.it12.com dengan `nano /etc/bind/jarkom/siren.redzone.it12.com `
```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     siren.redzone.it12.com. root.siren.redzone.it12.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      siren.redzone.it12.com.
@       IN      A       192.239.1.4
www     IN      CNAME   siren.redzone.it12.com.
@       IN      AAAA    ::1
```
- Restart bind9 dengan `service bind9 restart`

### Testing
![image](https://github.com/rehanasalsabilla/Jarkom-Modul-2-it12-2024/assets/143682058/9f383230-1677-4a1f-b9b3-8a0c34b7a263)

Error ketika ping padahal sudah mengikuti step by step nya.

## Soal 10
Markas juga meminta catatan kapan saja pesawat tempur tersebut menjatuhkan bom, maka buatlah subdomain baru di subdomain siren yaitu log.siren.redzone.xxxx.com serta aliasnya www.log.siren.redzone.xxxx.com yang juga mengarah ke Severny

- Jalankan command `nano /etc/bind/jarkom/siren.redzone.it12.com` lalu edit isinya seperti dibawah
```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     siren.redzone.it12.com. root.siren.redzone.it12.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      siren.redzone.it12.com.
@       IN      A       192.239.1.4
www     IN      CNAME   siren.redzone.it12.com.
log     IN      A       192.239.1.4
www.log IN      CNAME   siren.redzone.it12.com.
@       IN      AAAA    ::1
```




