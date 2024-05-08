# Jarkom-Modul-2-it12-2024

## Anggota
| Nama    | NRP     | 
| ------- | ------- | 
| Rehana Putri Salsabila     | 50272210     | 
| Muhammad Rifqi Oktaviansyah     | 5027221067     | 

## Soal 6
Beberapa daerah memiliki keterbatasan yang menyebabkan hanya dapat mengakses domain secara langsung melalui alamat IP domain tersebut. Karena daerah tersebut tidak diketahui secara spesifik, pastikan semua komputer (client) dapat mengakses domain redzone.xxxx.com melalui alamat IP Severny (Notes : menggunakan pointer record)

### Penyelesaian
- Run kode dibawah pada Pochinki
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
- Jalankan command
```
host -t PTR 192.239.1.4
```
### Result
![image](https://github.com/rehanasalsabilla/Jarkom-Modul-2-it12-2024/assets/143682058/40306607-27c4-402c-9263-4d94532fb7b2)

![image](https://github.com/rehanasalsabilla/Jarkom-Modul-2-it12-2024/assets/143682058/3ebb55e7-d791-4596-b740-21b6196cd66f)

## Soal 7
Akhir-akhir ini seringkali terjadi serangan siber ke DNS Server Utama, sebagai tindakan antisipasi kamu diperintahkan untuk membuat DNS Slave di Georgopol untuk semua domain yang sudah dibuat sebelumnya

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
