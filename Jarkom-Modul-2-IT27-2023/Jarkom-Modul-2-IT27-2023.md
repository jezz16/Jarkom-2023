# IT 27

## Anggota Kelompok
1. ***Arfan Yusran (5027211017)***
2. ***Andana Satrio Herdiansah (5027211031)***


_______________________________________________

### Nomor 1

#### Soal
Yudhistira akan digunakan sebagai DNS Master, Werkudara sebagai DNS Slave, Arjuna merupakan Load Balancer yang terdiri dari beberapa Web Server yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Buatlah topologi dengan pembagian sebagai berikut. Folder topologi dapat diakses pada drive berikut 


#### Jawab
 ![image](https://github.com/jezz16/Jarkom-2023/assets/99706251/14a17199-0db0-473a-9bc4-57e47ccaa66a)


### Nomor 2
#### Soal 
Buatlah website utama pada node arjuna dengan akses ke arjuna.yyy.com dengan alias www.arjuna.yyy.com dengan yyy merupakan kode kelompok.


#### Jawab
1. Buat script bash
```
#!/bin/bash

#Install bind9
apt-get install apache2 -y

# Menyiapkan website arjuna.it27.com
echo "Mengunduh arjuna.it27.com.zip..."
wget 'https://drive.google.com/uc?export=download&id=17tAM_XDKYWDvF-JJix1x7txvTBEax7vX' -O arjuna.it27.com.zip

echo "Mengunzip arjuna.it27.com.zip..."
unzip arjuna.it27.com.zip

echo "Mengubah nama folder menjadi arjuna.it27.com"
mv arjuna.yyy.com arjuna.it27.com

echo "Mengcopy website arjuna.it27.com ke direktori yang sesuai..."
cp -r arjuna.it27.com /var/www/
```
2. lalu jalankan bash dengan command ``` exec bash```
3. Setelah itu konfigurasi situs web, dapat dilakukan dengan membuat berkas konfigurasi di direktori /etc/apache2/sites-available/ :
Copy file 000-default.conf menjadi file arjuna.it27.com
 ```
cp 000-default.conf arjuna.it27.com

<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    ServerName arjuna.it27.com
    ServerAlias www.arjuna.it27.com
    DocumentRoot /var/www/arjuna.it27.com
</VirtualHost>
```

### Nomor 3
#### Soal 
Dengan cara yang sama seperti soal nomor 2, buatlah website utama dengan akses ke abimanyu.yyy.com dan alias www.abimanyu.yyy.com.


#### Jawab
1. Buat script bash
```
#!/bin/bash

apt-get update
#Install bind9
apt-get install apache2 -y

# Menyiapkan website abimanyu.it27.com
echo "Mengunduh abimanyu.it27.com.zip..."
wget 'https://drive.google.com/uc?export=download&id=1a4V23hwK9S7hQEDEcv9FL14UkkrHc-Zc' -O abimanyu.it27.com.zip

echo "Mengunzip abimanyu.it27.com.zip..."
unzip abimanyu.it27.com.zip

echo "Mengubah nama folder menjadi abimanyu.it27.com"
mv abimanyu.yyy.com abimanyu.it27.com

echo "Mengcopy website abimanyu.it27.com.zip ke direktori yang sesuai..."
cp -r abimanyu.it27.com /var/www/
```
2. lalu jalankan bash dengan command ``` exec bash```
3. Setelah itu konfigurasi situs web, dapat dilakukan dengan membuat berkas konfigurasi di direktori /etc/apache2/sites-available/ :
Copy file 000-default.conf menjadi file abimanyu.it27.com
 ```
cp 000-default.conf abimanyu.it27.com

<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    ServerName abimanyu.it27.com
    ServerAlias www.abimanyu.it27.com
    DocumentRoot /var/www/abimanyu.it27.com
</VirtualHost>
```

### Nomor 4
#### Soal 
Kemudian, karena terdapat beberapa web yang harus di-deploy, buatlah subdomain parikesit.abimanyu.yyy.com yang diatur DNS-nya di Yudhistira dan mengarah ke Abimanyu.


#### Jawab
Sebelum menyelesaikan soal pastikan setiap node telah menginstall package yang diperlukan dengan menggunakan script
```
#!/bin/bash
apt-get update
apt-get upgrade -y
apt-get install bind9 -y
apt-get install dnsutils -y
apt-get install nginx -y
apt-get install apache2 -y
apt-get install php -y
apt-get install lynx -y
```
Di yudhistira
1. Tambahkan script dibawah ke dalam file `/etc/bind/named.conf.local`
    ```
    zone "arjuna.it27.com" {type master; file "/etc/bind/arjuna/arjun.it27.com}
    zone "abimanyu.it27.com" {type master; file "/etc/bind/abimanyu/abimanyu.it27.com}
    ```
2. Copy file `/etc/bind/db.local` ke `/etc/bind/arjuna/arjuna.it27.com` dan `/etc/bind/abimanyu/abimanyu.it27.com`. Kemudian ubah kedua   
   file tersebut menjadi:
   arjuna.it27.com
   ```
   ;
   ; BIND data file for local loopback interface
   ;
   $TTL    604800
   @       IN      SOA     arjuna.it27.com. root.arjuna.it27.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
   ;
   @       IN      NS      arjuna.it27.com.
   @       IN      A       10.77.2.3
   www     IN      CNAME   arjuna.it27.com.
   @       IN      AAAA    ::1

   ```
   abimanyu.it27.com
   ```
   ;
   ; BIND data file for local loopback interface
   ;
   $TTL    604800
   @       IN      SOA     abimanyu.it27.com. root.abimanyu.it27.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
   ;
   @               IN      NS      abimanyu.it27.com.
   @               IN      A       10.77.2.4
   www             IN      CNAME   abimanyu.it27.com.
   parikesit       IN      A       10.77.2.4
   @               IN      AAAA    ::1
   ```
3. Kemudian pastikan nameserver client mengarah ke ip yudhistira dan lakukan ping ke arjuna.it27.com dan parikesit.abimanyu.it27.com
   ![ping arjuna](https://github.com/jezz16/Jarkom-2023/assets/113823539/5d353d68-e0b6-45fb-a878-8c72cf80fd61)
   ![ping parikesit](https://github.com/jezz16/Jarkom-2023/assets/113823539/2f0a96f1-c902-4540-adff-5c2e5a2e0a4f)

### Nomor 5
#### Soal 
Buat juga reverse domain untuk domain utama. (Abimanyu saja yang direverse)


#### Jawab
Di yudhistira
1. Tambahkan script dibawah ke dalam file `/etc/bind/named.conf.local`
   ```
   zone "2.77.10.in-addr.arpa" {type master; file "/etc/bind/abimanyu/2.77.10.in-addr.arpa";};
   ```
2. Copy file `/etc/bind/db.local` ke `/etc/bind/abimanyu/2.77.10.in-addr.arpa` dan ubah menjadi seperti berikut :
   ```
   ;
   ; BIND data file for local loopback interface
   ;
   $TTL    604800
   @       IN      SOA     abimanyu.it27.com. root.abimanyu.it27.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
   ;
   2.77.10.in-addr.arpa.   IN      NS      abimanyu.it27.com.
   4                       IN      PTR     abimanyu.it27.com.
   ```
3. Kemudian pastikan bahwa konfigurasi telah berhasil dengan commad `host -t PTR "ip node abimanyu"`
   ![reverse dns](https://github.com/jezz16/Jarkom-2023/assets/113823539/f91d5e25-e19a-4871-91df-c154e33053bf)

### Nomor 6
#### Soal 
Agar dapat tetap dihubungi ketika DNS Server Yudhistira bermasalah, buat juga Werkudara sebagai DNS Slave untuk domain utama.


#### Jawab
Untuk yang di Yudhistira
1. Ubah sript yang ada di `/etc/bind/named.conf.local` menjadi seperti script dibawah
   ```
   zone "arjuna.it27.com" {type master; also-notify { "ip slave"; }; allow-transfer { "ip slave"; }; file "/etc/bind/arjuna/arjun.it27.com}
   zone "abimanyu.it27.com" {type master; also-notify { "ip slave"; }; allow-transfer { "ip slave"; }; file "/etc/bind/abimanyu/abimanyu.it27.com}
   zone "2.77.10.in-addr.arpa" {type master; file "/etc/bind/abimanyu/2.77.10.in-addr.arpa";};
   ```
2. Ubah sript yang ada di `/etc/bind/named.conf.options` menjadi seperti script dibawah
   ```
   options {
        directory "/var/cache/bind";

        // If there is a firewall between you and nameservers you want
        // to talk to, you may need to fix the firewall to allow multiple
        // ports to talk.  See http://www.kb.cert.org/vuls/id/800113

        // If your ISP provided one or more IP addresses for stable
        // nameservers, you probably want to use them as forwarders.
        // Uncomment the following block, and insert the addresses replacing
        // the all-0's placeholder.

        // forwarders {
        //      0.0.0.0;
        // };

        //========================================================================
        // If BIND logs error messages about the root key being expired,
        // you will need to update your keys.  See https://www.isc.org/bind-keys
        //========================================================================
        //dnssec-validation auto;
        allow-query { any; };

        auth-nxdomain no;    # conform to RFC1035
        listen-on-v6 { any; };
   };
   ```
Untuk yang di Werkudara
1. Ubah sript yang ada di `/etc/bind/named.conf.local` menjadi seperti script dibawah
   ```
   zone "arjuna.it27.com" {type slave; masters { 10.77.1.2; }; file "/var/lib/bind/arjuna.it27.com";};
   zone "abimanyu.it27.com" {type slave; masters { 10.77.1.2; }; file "/var/lib/bind/abimanyu.it27.com";};
   ```
2. Ubah sript yang ada di `/etc/bind/named.conf.options` menjadi seperti script dibawah
   ```
   options {
        directory "/var/cache/bind";

        // If there is a firewall between you and nameservers you want
        // to talk to, you may need to fix the firewall to allow multiple
        // ports to talk.  See http://www.kb.cert.org/vuls/id/800113

        // If your ISP provided one or more IP addresses for stable
        // nameservers, you probably want to use them as forwarders.
        // Uncomment the following block, and insert the addresses replacing
        // the all-0's placeholder.

        // forwarders {
        //      0.0.0.0;
        // };

        //========================================================================
        // If BIND logs error messages about the root key being expired,
        // you will need to update your keys.  See https://www.isc.org/bind-keys
        //========================================================================
        //dnssec-validation auto;
        allow-query { any; };

        auth-nxdomain no;    # conform to RFC1035
        listen-on-v6 { any; };
   };
   ```
3. Pastikan nameserver client mengarah ke werkudara dan lakukan ping ke arjuna atau abimanyu untuk memastikan konfigurasi berjalan
   ![ping slave](https://github.com/jezz16/Jarkom-2023/assets/113823539/86e5d261-4190-40e8-ae3e-74320337ae41)

### Nomor 7
#### Soal 
Seperti yang kita tahu karena banyak sekali informasi yang harus diterima, buatlah subdomain khusus untuk perang yaitu baratayuda.abimanyu.yyy.com dengan alias www.baratayuda.abimanyu.yyy.com yang didelegasikan dari Yudhistira ke Werkudara dengan IP menuju ke Abimanyu dalam folder Baratayuda.


#### Jawab
Di yudhistira
1. ubah script yang ada di `/etc/bind/abimanyu/abimanyu.it27.com` menjadi
   ```
   ;
   ; BIND data file for local loopback interface
   ;
   $TTL    604800
   @       IN      SOA     abimanyu.it27.com. root.abimanyu.it27.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
   ;
   @               IN      NS      abimanyu.it27.com.
   @               IN      A       10.77.2.4
   www             IN      CNAME   abimanyu.it27.com.
   parikesit       IN      A       10.77.2.4
   ns1             IN      A       10.77.3.2
   baratayuda      IN      NS      ns1
   @               IN      AAAA    ::1
   ```

Di werkudara
1. Tambahkan script yang ada di `/etc/bind/named.conf.local` dengan script yang ada dibawah
   ```
   zone "baratayuda.abimanyu.it27.com" {type master; file "/etc/bind/baratayuda/baratayuda.abimanyu.it27.com";};
   ```
2. Copy file `/etc/bind/db.local` ke `/etc/bind/baratayuda/baratayuda.abimanyu.it27.com` dan ubah menjadi seperti berikut :
   ```
   ;
   ; BIND data file for local loopback interface
   ;
   $TTL    604800
   @       IN      SOA     baratayuda.abimanyu.it27.com. root.baratayuda.abimanyu.it27.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
   ;
   @       IN      NS      baratayuda.abimanyu.it27.com.
   @       IN      A       10.77.2.4
   www     IN      CNAME   baratayuda.abimanyu.it27.com.
   @       IN      AAAA    ::1
   ```
3. Lakukan ping ke `baratayuda.abimanyu.it27.com` untuk memastikan
   ![ping baratayuda](https://github.com/jezz16/Jarkom-2023/assets/113823539/8404723a-8534-4cba-9e77-3ff47c4f0bbe)

### Nomor 8
#### Soal 
Untuk informasi yang lebih spesifik mengenai Ranjapan Baratayuda, buatlah subdomain melalui Werkudara dengan akses rjp.baratayuda.abimanyu.yyy.com dengan alias www.rjp.baratayuda.abimanyu.yyy.com yang mengarah ke Abimanyu.


#### Jawab
Di werkudara
1. Tambahkan script yang ada di `/etc/bind/named.conf.local` dengan script yang ada dibawah
   ```
   zone "rjp.baratayuda.abimanyu.it27.com" {type master; file "/etc/bind/baratayuda/rjp.baratayuda.abimanyu.it27.com";};
   ```
2. Ubah file `/etc/bind/baratayuda/baratayuda.abimanyu.it27.com` menjadi seperti berikut :
   ```
   ;
   ; BIND data file for local loopback interface
   ;
   $TTL    604800
   @       IN      SOA     baratayuda.abimanyu.it27.com. root.baratayuda.abimanyu.it27.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
   ;
   @       IN      NS      baratayuda.abimanyu.it27.com.
   @       IN      A       10.77.2.4
   www     IN      CNAME   baratayuda.abimanyu.it27.com.
   ns1     IN      A       10.77.3.2
   rjp     IN      NS      ns1
   @       IN      AAAA    ::1
   ```
3. Copy file `/etc/bind/db.local` ke `/etc/bind/baratayuda/rjp.baratayuda.abimanyu.it27.com`. Kemudian ubah file tersebut menjadi:
   ```
   ;
   ; BIND data file for local loopback interface
   ;
   $TTL    604800
   @       IN      SOA     rjp.baratayuda.abimanyu.it27.com. root.rjp.baratayuda.abimanyu.it27.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
   ;
   @       IN      NS      rjp.baratayuda.abimanyu.it27.com.
   @       IN      A       10.77.2.4
   www     IN      CNAME   rjp.baratayuda.abimanyu.it27.com.
   @       IN      AAAA    ::1
   ```
4. Lakukan ping ke `rjp.baratayuda.abimanyu.it27.com` untuk memastikan
   ![ping rjp](https://github.com/jezz16/Jarkom-2023/assets/113823539/bf197668-329a-4666-a236-53d405bf0e5a)

### Nomor 9
#### Soal 
Arjuna merupakan suatu Load Balancer Nginx dengan tiga worker (yang juga menggunakan nginx sebagai webserver) yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Lakukan deployment pada masing-masing worker.


#### Jawab
1. Install nginx ke load balancer dan seluruh node webserver dengan command dibawah ini
   `apt-get install nginx -y`

2. Cek instalasi dengan command `service nginx status`
   ![status nginx](https://github.com/jezz16/Jarkom-2023/assets/113823539/bff15ae1-c997-4eb8-bab0-e82f6e8c3cf3)





