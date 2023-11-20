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



### Nomor 1

#### Soal
Semua CLIENT harus menggunakan konfigurasi dari DHCP Server

#### Jawab



### Nomor 2

#### Soal
Client yang melalui Switch3 mendapatkan range IP dari [prefix IP].3.16 - [prefix IP].3.32 dan [prefix IP].3.64 - [prefix IP].3.80

#### Jawab



### Nomor 3

#### Soal
Client yang melalui Switch4 mendapatkan range IP dari [prefix IP].4.12 - [prefix IP].4.20 dan [prefix IP].4.160 - [prefix IP].4.168

#### Jawab



### Nomor 4

#### Soal
Client mendapatkan DNS dari Heiter dan dapat terhubung dengan internet melalui DNS tersebut

#### Jawab



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
