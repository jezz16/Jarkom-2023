# IT 27

## Anggota Kelompok
1. ***Arfan Yusran (5027211017)***
2. ***Andana Satrio Herdiansah (5027211031)***


_______________________________________________
### Topologi
![topologi](https://github.com/jezz16/Jarkom-2023/assets/113823539/0cc306cd-3d11-4695-a71b-340599a250ba)


### Konfigurasi
1. Aura
   ```
   auto eth0
   iface eth0 inet dhcp

   auto eth1
   iface eth1 inet static
	 address 10.77.1.1
	 netmask 255.255.255.0

   auto eth2
   iface eth2 inet static
	 address 10.77.2.1
	 netmask 255.255.255.0

   auto eth3
   iface eth3 inet static
	 address 10.77.3.1
	 netmask 255.255.255.0

   auto eth4
   iface eth4 inet static
	 address 10.77.4.1
	 netmask 255.255.255.0
   ```
3. Himmel
   ```
   auto eth0
   iface eth0 inet static
	 address 10.77.1.2
	 netmask 255.255.255.0
   ```
5. Heiter
   ```
   auto eth0
   iface eth0 inet static
	 address 10.77.1.3
	 netmask 255.255.255.0
   ```
7. Denken
   ```
   auto eth0
   iface eth0 inet static
	 address 10.77.2.2
	 netmask 255.255.255.0
   ```
9. Eisen
   ```
   auto eth0
   iface eth0 inet static
	 address 10.77.2.3
	 netmask 255.255.255.0
   ```
11. PHP Worker
    ```
    auto eth0
    iface eth0 inet static
	  address 10.77.3.4 - 10.77.3.6
	  netmask 255.255.255.0
    ```
13. Laravel Worker
    ```
    auto eth0
    iface eth0 inet static
	  address 10.77.4.4 - 10.77.4.6
	  netmask 255.255.255.0
    ```
15. Client
    ```
    auto eth0
    iface eth0 inet dhcp
    ```

    
### Nomor 0

### Soal
kalian diminta untuk melakukan register domain berupa riegel.canyon.yyy.com untuk worker Laravel dan granz.channel.yyy.com untuk worker PHP mengarah pada worker yang memiliki IP [prefix IP].x.1.

#### Jawab
Pertama lakukan iptables di aura
```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.173.0.0/16
```
Setelah itu lakukan setup dns di heiter dengan menjalankan script berikut :
```
#!bin/bash
echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt-get install bind9 -y

echo 'zone "riegel.canyon.it27.com" {
    type master;
    file "/etc/bind/jarkom/riegel.canyon.it27.com";
};

zone "granz.channel.it27.com" {
    type master;
    file "/etc/bind/jarkom/granz.channel.it27.com";
};' > /etc/bind/named.conf.local

mkdir -p /etc/bind/jarkom
cp /etc/bind/db.local /etc/bind/jarkom/riegel.canyon.it27.com
cp /etc/bind/db.local /etc/bind/jarkom/granz.channel.it27.com

echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     riegel.canyon.it27.com. root.riegel.canyon.it27.com. (
                        2023111401      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      riegel.canyon.it27.com.
@       IN      A       10.77.4.1     ;
www     IN      CNAME   riegel.canyon.it27.com.' > /etc/bind/jarkom/riegel.canyon.it27.com

service bind9 start
```


### Nomor 1

#### Soal
Semua CLIENT harus menggunakan konfigurasi dari DHCP Server

#### Jawab
Lakukan konfigurasi node client sesuai dengan yang ada di atas
```
auto eth0
iface eth0 inet dhcp
```


### Nomor 2

#### Soal
Client yang melalui Switch3 mendapatkan range IP dari [prefix IP].3.16 - [prefix IP].3.32 dan [prefix IP].3.64 - [prefix IP].3.80

#### Jawab
Lakukan konfigurasi dhcp server di himmel dengan menjalankan script berikut :
Script no1 - no5
```
#!/bin/bash
echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt-get install isc-dhcp-server -y

echo "subnet 10.77.1.0 netmask 255.255.255.0 {}" >> /etc/dhcp/dhcpd.conf

echo "subnet 10.77.2.0 netmask 255.255.255.0 {}" >> /etc/dhcp/dhcpd.conf

echo "subnet 10.77.3.0 netmask 255.255.255.0 {
    range 10.77.3.16 10.77.3.32;
    range 10.77.3.64 10.77.3.80;
    option routers 10.77.3.1;
    option broadcast-address 10.77.3.255;
    option domain-name-servers 10.77.1.3;
    default-lease-time 180;
    max-lease-time 5760;
}" >> /etc/dhcp/dhcpd.conf

echo "subnet 10.77.4.0 netmask 255.255.255.0 {
    range 10.77.4.12 10.77.4.20;
    range 10.77.4.160 10.77.4.168;
    option routers 10.77.4.1;
    option broadcast-address 10.77.4.255;
    option domain-name-servers 10.77.1.3;
    default-lease-time 720;
    max-lease-time 5760;
}" >> /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart

service isc-dhcp-server status
```
Untuk konfigurasi range ip pada switch 3 terletak pada bagian :
```
echo "subnet 10.77.3.0 netmask 255.255.255.0 {
    range 10.77.3.16 10.77.3.32;
    range 10.77.3.64 10.77.3.80;
    ...
}" >> /etc/dhcp/dhcpd.conf
```
Lakukan konfigurasi dhcp relay dengan menjalankan script ini di Aura :
```
#!/bin/bash

apt-get update
apt-get install isc-dhcp-relay -y
service isc-dhcp-relay start
```
dan isi ketentuan dhc relay sesuai seperti berikut
```
SERVERS="10.77.1.2"
INTERFACES="eth1 eth2 eth3 eth4"
OPTIONS=""
```


### Nomor 3

#### Soal
Client yang melalui Switch4 mendapatkan range IP dari [prefix IP].4.12 - [prefix IP].4.20 dan [prefix IP].4.160 - [prefix IP].4.168

#### Jawab
Untuk konfigurasi range ip pada switch 4 terletak pada bagian :
```
echo "subnet 10.77.4.0 netmask 255.255.255.0 {
    range 10.77.4.12 10.77.4.20;
    range 10.77.4.160 10.77.4.168;
    ...
}" >> /etc/dhcp/dhcpd.conf
```

### Nomor 4

#### Soal
Client mendapatkan DNS dari Heiter dan dapat terhubung dengan internet melalui DNS tersebut

#### Jawab
Agar bisa terhubung dengan internet lakukan konfigurasi dns server dengan menjalankan script ini di Heiter
```
echo 'options {
      directory "/var/cache/bind";

      forwarders {
              1.1.1.1;
      };

      // dnssec-validation auto;
      allow-query{any;};
      auth-nxdomain no;    # conform to RFC1035
      listen-on-v6 { any; };
}; ' >/etc/bind/named.conf.options

service bind9 restart
```
Untuk bagian konfigurasi dhcp server terletak pada bagian:
```
echo "subnet 10.77.3.0 netmask 255.255.255.0 {
    ...
    option routers 10.77.3.1;
    option domain-name-servers 10.77.1.3;
    ...
}" >> /etc/dhcp/dhcpd.conf

echo "subnet 10.77.4.0 netmask 255.255.255.0 {
    ...
    option routers 10.77.4.1;
    option domain-name-servers 10.77.1.3;
    ...
}" >> /etc/dhcp/dhcpd.conf
```


### Nomor 5

#### Soal
Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch3 selama 3 menit sedangkan pada client yang melalui Switch4 selama 12 menit. Dengan waktu maksimal dialokasikan untuk peminjaman alamat IP selama 96 menit

#### Jawab



### Nomor 6

#### Soal
Pada masing-masing worker PHP, lakukan konfigurasi virtual host untuk website berikut dengan menggunakan php 7.3.

#### Jawab



### Nomor 7

#### Soal
Kepala suku dari Bredt Region memberikan resource server sebagai berikut:
1. Lawine, 4GB, 2vCPU, dan 80 GB SSD.
2. Linie, 2GB, 2vCPU, dan 50 GB SSD.
3. Lugner 1GB, 1vCPU, dan 25 GB SSD.
aturlah agar Eisen dapat bekerja dengan maksimal, lalu lakukan testing dengan 1000 request dan 100 request/second.

#### Jawab



### Nomor 8

#### Soal
Karena diminta untuk menuliskan grimoire, buatlah analisis hasil testing dengan 200 request dan 10 request/second masing-masing algoritma Load Balancer dengan ketentuan sebagai berikut:
1. Nama Algoritma Load Balancer
2. Report hasil testing pada Apache Benchmark
3. Grafik request per second untuk masing masing algoritma. 
Analisis

#### Jawab



### Nomor 9

#### Soal
Karena diminta untuk menuliskan grimoire, buatlah analisis hasil testing dengan 200 request dan 10 request/second masing-masing algoritma Load Balancer dengan ketentuan sebagai berikut:
1. Nama Algoritma Load Balancer
2. Report hasil testing pada Apache Benchmark
3. Grafik request per second untuk masing masing algoritma. 
Analisis

#### Jawab
Dengan menggunakan algoritma Round Robin, lakukan testing dengan menggunakan 3 worker, 2 worker, dan 1 worker sebanyak 100 request dengan 10 request/second, kemudian tambahkan grafiknya pada grimoire.
