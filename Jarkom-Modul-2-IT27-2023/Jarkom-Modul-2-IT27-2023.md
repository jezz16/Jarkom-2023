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
xxxxxxxx


#### Jawab

