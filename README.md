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
![Screenshot 2024-05-08 201857](https://github.com/rehanasalsabilla/Jarkom-Modul-2-it12-2024/assets/136863633/20a08202-6916-4533-9515-9cc0e77b9883)

## Config 

- Erangel :
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.239.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 192.239.2.1
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 192.239.3.1
	netmask 255.255.255.0
```

- Lipovka :
```
auto eth0
iface eth0 inet static
	address 192.239.1.2
	netmask 255.255.255.0
	gateway 192.239.1.1
```

- Stalber :
```
auto eth0
iface eth0 inet static
	address 192.239.1.3
	netmask 255.255.255.0
	gateway 192.239.1.1
```

- Severny : 
```
auto eth0
iface eth0 inet static
	address 192.239.1.4
	netmask 255.255.255.0
	gateway 192.239.1.1
```

- Pochinki : 
```
auto eth0
iface eth0 inet static
	address 192.239.3.2
	netmask 255.255.255.0
	gateway 192.239.3.1
```

- Apartments :
``` 
auto eth0
iface eth0 inet static
	address 192.239.2.5
	netmask 255.255.255.0
	gateway 192.239.2.1
```

- Mylta : 
```
auto eth0
iface eth0 inet static
	address 192.239.2.4
	netmask 255.255.255.0
	gateway 192.239.2.1
```

- Georgopol :
```
auto eth0
iface eth0 inet static
	address 192.239.2.3
	netmask 255.255.255.0
	gateway 192.239.2.1
```

- Ruins :
``` 
auto eth0
iface eth0 inet static
	address 192.239.2.2
	netmask 255.255.255.0
	gateway 192.239.2.1
```

- **Notes of Config**
  ```
  Lipovka : 192.239.1.2
  Stalber : 192.239.1.3
  Severny : 192.239.1.4
  Pochinki : 192.239.3.2
  Apartments : 192.239.2.5
  Mylta : 192.239.2.4
  Georgopol : 192.239.2.3
  Ruins : 192.239.2.2
  ```

### Sebelum memulai 
setiap node, kita inisiasi pada `.bashrc` menggunakan `nano`

- **Erangel**
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
  nameserver 192.239.3.2 # IP Pochinki
  nameserver 192.239.2.3 # IP Geogopol
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
![Screenshot 2024-05-08 204218](https://github.com/rehanasalsabilla/Jarkom-Modul-2-it12-2024/assets/136863633/eef4c995-68a5-432a-94fa-d1f7daa7f514)

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
![Screenshot 2024-05-04 025025](https://github.com/rehanasalsabilla/Jarkom-Modul-2-it12-2024/assets/136863633/2c1d184b-9638-468f-be5a-bb0ed9747d5b)
![Screenshot 2024-05-04 024911](https://github.com/rehanasalsabilla/Jarkom-Modul-2-it12-2024/assets/136863633/17204ded-6104-44ea-93c9-7bf7b6a6e208)
![Screenshot 2024-05-04 024846](https://github.com/rehanasalsabilla/Jarkom-Modul-2-it12-2024/assets/136863633/31bc3225-8408-4ea5-9980-ce9b8d3face1)

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

## Soal 11
Setelah pertempuran mereda, warga Erangel dapat kembali mengakses jaringan luar, tetapi hanya warga Pochinki saja yang dapat mengakses jaringan luar secara langsung. Buatlah konfigurasi agar warga Erangel yang berada diluar Pochinki dapat mengakses jaringan luar melalui DNS Server Pochinki

**Pochinki**
- Uncomment bagian berikut dan ganti dengan IP nameserver Erangel
```
forwarders {
    192.168.122.1;
};
```
- Uncomment
```
// dnssec-validation auto;
```
- Tambahkan
```
allow-query{any;};
```
### Script
![Screenshot 2024-05-08 203419](https://github.com/rehanasalsabilla/Jarkom-Modul-2-it12-2024/assets/136863633/6bba717d-4cc7-4d4b-b150-08bdc930b831)
- Restart ``service bind9 restart``
- Ubahlah nameserver pada node lain ke ``IP Pochinki`` lalu ping google.com
### Result
![Screenshot 2024-05-08 204218](https://github.com/rehanasalsabilla/Jarkom-Modul-2-it12-2024/assets/136863633/b7495bb3-f998-49be-91f3-6fdf715b63e6)
![Screenshot 2024-05-08 204243](https://github.com/rehanasalsabilla/Jarkom-Modul-2-it12-2024/assets/136863633/0c9e2bff-1f2a-4a38-bbea-133ae8a33694)
![Screenshot 2024-05-08 204402](https://github.com/rehanasalsabilla/Jarkom-Modul-2-it12
![Screenshot 2024-05-08 204301](https://github.com/rehanasalsabilla/Jarkom-Modul-2-it12-2024/assets/136863633/04eef4ec-33e7-4119-9957-2ccfd67a100e)
-2024/assets/136863633/bc9a5e76-d9ab-4d33-9524-fd73ff504912)
![Screenshot 2024-05-08 204338](https://github.com/rehanasalsabilla/Jarkom-Modul-2-it12-2024/assets/136863633/e48bcd02-d411-4be9-b013-4685d82e179e)
![Screenshot 2024-05-08 204319](https://github.com/rehanasalsabilla/Jarkom-Modul-2-it12-2024/assets/136863633/d285aaa2-134a-423b-afcd-7f7493627aec)
![Screenshot 2024-05-08 204421](https://github.com/rehanasalsabilla/Jarkom-Modul-2-it12-2024/assets/136863633/3a211279-f471-486e-9445-2505d53ffd8c)

## Soal 12
Karena pusat ingin sebuah website yang ingin digunakan untuk memantau kondisi markas lainnya maka deploy lah webiste ini (cek resource yg lb) pada severny menggunakan apache

### Script
```

echo -e "nameserver 10.78.1.2\nnameserver 10.78.1.3" > /etc/resolv.conf

apt-get update

apt-get install wget -y
apt-get install apache2 -y
apt-get install unzip -y
apt-get install libapache2-mod-php7.0 -y

wget --no-check-certificate 'https://docs.google.com/uc?export=download&id=$wget --no-check-certificate 'https://docs.google.com/uc?export=download&id=$
mkdir /var/www
mkdir /var/www/html

unzip dir-listing.zip -d dir-listing
unzip lb.zip -d lb

cp /root/lb/worker/index.php /var/www/html/index.php

service apache2 restart
```
- Menyambungkan Node severny dengan DNS kemudian melakukan instalasi apache2, dan modul lainnya
- Download resource
- copy resource ke /var/www/html/index.php
- Restart ``service bind9 restart``

#### Melakukan konfigurasi 
```lynx http://10.78.3.2/index.php```
### Result
![Screenshot 2024-05-08 205754](https://github.com/rehanasalsabilla/Jarkom-Modul-2-it12-2024/assets/136863633/5490757a-0bf0-4839-b4cb-5d6558020413)

## Soal 13
Tapi pusat merasa tidak puas dengan performanya karena traffic yag tinggi maka pusat meminta kita memasang load balancer pada web nya, dengan Severny, Stalber, Lipovka sebagai worker dan Mylta sebagai Load Balancer menggunakan apache sebagai web server nya dan load balancernya

### Script 
- Konfigurasi Mylta, seperti script dibawah ini
```
echo -e "nameserver 192.239.3.2\nameserver 192.239.2.3" > /etc/resolv.conf

apt-get update

apt-get install apache2 -y
apt-get install libapache2-mod-php7.0 -y
a2enmod proxy
a2enmod proxy_http
a2enmod proxy_balancer
a2enmod lbmethod_byrequests

rm /var/www/html/index.html

echo -e "<VirtualHost *:80>
        <Proxy balancer://mycluster>
                BalancerMember http://192.239.1.3
                BalancerMember http://192.239.1.4
        </Proxy>
        ProxyPreserveHost On
        ProxyPass / balancer://mycluster/
        ProxyPassReverse / balancer://mycluster/

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet" > /etc/apache2/sites-available/000-default.conf
service apache2 restart
```
- Copy konfigurasi ke /etc/apache/sites-available/000-default.conf

**Testing Load Balancer**
- menggunakan lynx dan setiap ip load balancer di restart akan menampilkan isi index.php dari worker secara bergantian

### Result 
![Screenshot 2024-05-08 212601](https://github.com/rehanasalsabilla/Jarkom-Modul-2-it12-2024/assets/136863633/78411c0f-bf86-4310-bc15-e28f4eeff661)
![Screenshot 2024-05-08 205812](https://github.com/rehanasalsabilla/Jarkom-Modul-2-it12-2024/assets/136863633/33b55e16-fbc3-444e-a6d5-b5fd78481249)

## Soal 14
Mereka juga belum merasa puas jadi pusat meminta agar web servernya dan load balancer nya diubah menjadi nginx

## Soal 15
Markas pusat meminta laporan hasil benchmark dengan menggunakan apache benchmark dari load balancer dengan 2 web server yang berbeda tersebut dan meminta secara detail dengan ketentuan:
- Nama Algoritma Load Balancer
- Report hasil testing apache benchmark 
- Grafik request per second untuk masing masing algoritma. 
- Analisis

### Script

## Soal 16
Karena dirasa kurang aman karena masih memakai IP, markas ingin akses ke mylta memakai mylta.xxx.com dengan alias www.mylta.xxx.com (sesuai web server terbaik hasil analisis kalian)

### Script
- Konfigurasi pada Pochinki. Tambahkan myla.it12.com pada `/etc/bind/named.conf.local`
```
zone "airdrop.it04.com" {
    type master;
    also-notify { 192.239.2.3; };
    allow-transfer { 192.239.2.3; };
    file "/etc/bind/zone/airdrop.it12.com";
};

zone "redzone.it12.com" {
    type master;
    also-notify { 192.239.2.3; };
    allow-transfer { 192.239.2.3; };
    file "/etc/bind/zone/redzone.it12.com";
};

zone "2.239.192.in-addr.arpa" {
    type master;
    file "/etc/bind/zone/2.239.192.in-addr.arpa";
};

zone "loot.it12.com" {
    type master;
    file "/etc/bind/delegasizone/loot.it12.com";
};

zone "mylta.it12.com" {
    type master;
    file "/etc/bind/zone/mylta.it12.com";
};
```
Lalu, kita perlu merubah IP menjadi nameserver dan aliasnya pada `/etc/bind/jarkom/mylta.it04.com` 
```

$TTL    604800
@       IN      SOA     mylta.it12.com. root.mylta.it12.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      mylta.it12.com.
@       IN      A       192.239.2.4
@       IN      AAAA    ::1
www     IN      CNAME   mylta.it12.com.

```
Setelah itu, pindah ke Mylta dan melakukan command `service apache reload` dan `service apache2 restart` lalu kita sudah dapat mengakses Mylta menggunakan nameservernya pada client seperti dibawah
```

root@Ruins:~# lynx http://mylta.it12.com/index.php


Exiting via interrupt: 2

root@Ruins:~# lynx http://www.mylta.it12.com/index.php


Exiting via interrupt: 2
```

## Soal 17
Agar aman, buatlah konfigurasi agar mylta.xxx.com hanya dapat diakses melalui port 14000 dan 14400.

### Script
- Konfigurasikan file .conf pada `/etc/apache2/sites-available` yaitu file `default-14000.conf` dan `default-14400` seperti berikut:
```
<VirtualHost *:14400>
        # The ServerName directive sets the request scheme, hostname and port that
        # the server uses to identify itself. This is used when creating
        # redirection URLs. In the context of virtual hosts, the ServerName
        # specifies what hostname must appear in the request's Host: header to
        # match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.

        ServerName mylta.it12.com
        ServerAlias www.mylta.it12.com

    <Proxy balancer://itbalancer>
        BalancerMember http://192.239.1.2:14400
        BalancerMember http://192.239.1.3:14400
        BalancerMember http://192.239.1.4:14400
        ProxySet lbmethod=byrequests
    </Proxy>

    ProxyPreserveHost On
    ProxyPass / balancer://itbalancer/
    ProxyPassReverse / balancer://itbalancer/


        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
        # error, crit, alert, emerg.
        # It is also possible to configure the loglevel for particular
        # modules, e.g.
        #LogLevel info ssl:warn

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        # For most configuration files from conf-available/, which are
        # enabled or disabled at a global level, it is possible to
        # include a line for only one particular virtual host. For example the
        # following line enables the CGI configuration for this host only
        # after it has been globally disabled with "a2disconf".
        # Include conf-available/serve-cgi-bin.conf
</VirtualHost>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet

ServerName 127.0.1.1.
```
Setelah itu kita tinggal run command `service apache2 restart` dan run command `service apache2 reload` agar dapat berjalan dengan konfigurasi apache2 terbaru

## Soal 18
Apa bila ada yang mencoba mengakses IP mylta akan secara otomatis dialihkan ke www.mylta.xxx.com

### Script
- Konfigurasi reverse DNS pada zone Mylta pada POCHINKI dengan mengkonfigurasi `/etc/bind/named.conf.local`
```
zone "4.2.239.192.in-addr.arpa" {
    type master;
    file "/etc/bind/zone/4.2.239.192.in-addr.arpa";
};
```
Lalu kita perlu mengonfigurasi file `"/etc/bind/zone/4.2.239.192.in-addr.arpa";` agar lebih mudah kita tinggal copy dengan konfigurasi mylta sebelumnya dengan command `cp /etc/bind/zone/mylta.it04.com /etc/bind/zone/5.2.168.192.in-addr.arpa`
Dengan konfigurasi `/etc/bind/zone/4.2.239.192.in-addr.arpa` seperti berikut:
```
$TTL    604800
@       IN      SOA     mylta.it12.com. root.mylta.it12.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      mylta.it12.com.
@       IN      A       192.239.2.4
@       IN      AAAA    ::1
www     IN      CNAME   mylta.it12.com.
```
Lalu kita atur juga bagian konfigurasi apache2 load balancing pada MYLTA pada file `000-default.conf`
dan saat kita run `lynx http://192.239.2.4:14400/index.php` maka hasilnya seperti berikut:
```
<VirtualHost *:80>
        # The ServerName directive sets the request scheme, hostname and port that
        # the server uses to identify itself. This is used when creating
        # redirection URLs. In the context of virtual hosts, the ServerName
        # specifies what hostname must appear in the request's Host: header to
        # match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.

        ServerName 192.239.2.4
        ServerAlias www.mylta.it04.com

    <Proxy balancer://itbalancer>
        BalancerMember http://192.239.1.2:8080
        BalancerMember http://192.239.1.3:8080
        BalancerMember http://192.239.1.4:8080
        ProxySet lbmethod=byrequests
    </Proxy>

    ProxyPreserveHost On
    ProxyPass / balancer://itbalancer/
    ProxyPassReverse / balancer://itbalancer/


    RewriteEngine On
    RewriteCond %{HTTP_HOST} ^192.239.2.4
    RewriteRule ^(.*)$ http://www.mylta.i12.com/$1 [R=301,L]

        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
        # error, crit, alert, emerg.
        # It is also possible to configure the loglevel for particular
        # modules, e.g.
        #LogLevel info ssl:warn

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        # For most configuration files from conf-available/, which are
        # enabled or disabled at a global level, it is possible to
        # include a line for only one particular virtual host. For example the
        # following line enables the CGI configuration for this host only
        # after it has been globally disabled with "a2disconf".
        # Include conf-available/serve-cgi-bin.conf
</VirtualHost>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet

ServerName 127.0.1.1.
```
## Soal 19 
Karena probset sudah kehabisan ide masuk ke salah satu worker buatkan akses direktori listing yang mengarah ke resource worker2

### Script

## Soal 20
Worker tersebut harus dapat di akses dengan tamat.xxx.com dengan alias www.tamat.xxx.com

### Script





