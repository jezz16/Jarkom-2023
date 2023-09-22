# IT 27

## Anggota Kelompok
1. ***Arfan Yusran (5027211017)***
2. ***Andana Satrio Herdiansah (5027211031)***


_______________________________________________

### Nomor 1

#### Soal
User melakukan berbagai aktivitas dengan menggunakan protokol FTP. Salah satunya adalah mengunggah suatu file.
Berapakah sequence number (raw) pada packet yang menunjukkan aktivitas tersebut? 
Berapakah acknowledge number (raw) pada packet yang menunjukkan aktivitas tersebut? 
Berapakah sequence number (raw) pada packet yang menunjukkan response dari aktivitas tersebut?
Berapakah acknowledge number (raw) pada packet yang menunjukkan response dari aktivitas tersebut?

#### Langkah Penyelesaian
1. Buka file pcap
2. Filter ftp file tersebut
3. cari request c75-GrabThePhisher.zip dan dapatkan hal yang diminta pada soal selanjutnya beralih ke response dari request tersebut.
   ![image](https://github.com/jezz16/Jarkom-2023/assets/99706251/faebbfaf-c56f-40a8-a964-4a95e58b5cf6)



### Nomor 2
#### Soal
Sebutkan web server yang digunakan pada portal praktikum Jaringan Komputer!

#### Langkah Penyelesaian
1. Buka file pcap
2. Filter file dengan ip.src == 10.21.78.111 atau tcp.stream eq 43
![soal2-1](https://github.com/jezz16/Jarkom-2023/assets/113823539/ad629944-73d4-4198-8e37-2be070c7fa3b)

3. Pilih salah sati paket dan tcp stream follow
![soal2-2](https://github.com/jezz16/Jarkom-2023/assets/113823539/3d73ebc9-be71-4e8d-8a11-00543a92ed05)

4. Lihat nama server yang tercantum
![soal2-3](https://github.com/jezz16/Jarkom-2023/assets/113823539/1e34ba8e-5460-4c53-8136-9e18a9a1a1a3)

![soal2-4](https://github.com/jezz16/Jarkom-2023/assets/113823539/be483628-2bf2-45c4-80c6-979ec8886d0f)


### Nomor 3
#### Soal
Dapin sedang belajar analisis jaringan. Bantulah Dapin untuk mengerjakan soal berikut:
a. Berapa banyak paket yang tercapture dengan IP source maupun destination address adalah 239.255.255.250 dengan port 3702?
b. Protokol layer transport apa yang digunakan?

#### Langkah Penyelesaian
1. Buka file pcap
2. Filter file pcap dengan ip.dst == 239.255.255.250 and udp.port == 3702 
3. Hitung jumlah paket yang ada dan lihat jenis protokol yang digunakan
   ![soal3-1](https://github.com/jezz16/Jarkom-2023/assets/113823539/550e516a-97b7-4acb-8fb5-0db37402e9fc)
   ![soal3-2](https://github.com/jezz16/Jarkom-2023/assets/113823539/69a9bfe3-e176-407a-b84e-f3c3dbebc5d7)


### Nomor 4
#### Soal
Berapa nilai checksum yang didapat dari header pada paket nomor 130?
#### Langkah Penyelesaian
1. Buka file pcap
2. Cari paket nomor 130 dan cari nilai checksumnya
   ![image](https://github.com/jezz16/Jarkom-2023/assets/99706251/ca7308b8-1e6b-4d66-bbb8-e88696ee54c0)

   
### Nomor 5
#### Soal
Elshe menemukan suatu file packet capture yang menarik. Bantulah Elshe untuk menganalisis file packet capture tersebut.
a. Berapa banyak packet yang berhasil di capture dari file pcap tersebut?
b. Port berapakah pada server yang digunakan untuk service SMTP?
c. Dari semua alamat IP yang tercapture, IP berapakah yang merupakan public IP?

#### Langkah Penyelesaian
1. Buka file pcap lalu follow tcp stream.
   ![image](https://github.com/jezz16/Jarkom-2023/assets/99706251/58f3dec6-fa06-43a9-a060-19bd99d3b414)

3. Setelah mendapat pw zipfile, lalukan decode base 64
   ![image](https://github.com/jezz16/Jarkom-2023/assets/99706251/9d55fe27-7871-4a70-b8f6-6f69f88ae36d)

4. Buka file connect dengan menggunakan pw yang sudah didapatkan
   ![image](https://github.com/jezz16/Jarkom-2023/assets/99706251/111c52dc-758c-41f4-b743-024f3f2bf242)

5. Masuk ke nc yang diberikan, lalu jawab pertanyaan sesuai file pcap
   ![image](https://github.com/jezz16/Jarkom-2023/assets/99706251/eb3fc036-1bbb-4745-8689-a066239c4e5a)


### Nomor 6
#### Soal
Seorang anak bernama Udin Berteman dengan SlameT yang merupakan seorang penggemar film detektif. sebagai teman yang baik, Ia selalu mengajak slamet untuk bermain valoranT bersama. suatu malam, terjadi sebuah hal yang tak terdUga. ketika udin mereka membuka game tersebut, laptop udin menunjukkan sebuah field text dan Sebuah kode Invalid bertuliskan "server SOURCE ADDRESS 7812 is invalid". ketika ditelusuri di google, hasil pencarian hanya menampilkan a1 e5 u21. jiwa detektif slamet pun bergejolak. bantulah udin dan slamet untuk menemukan solusi kode error tersebut.

#### Langkah Penyelesaian
Pada soal tersebut terdapat kata berhuruf kapital berupa "SUBSTITUSI", lalu ada juga a1 e5 u21 yang mewakili setiap huruf yang dapat diganti dengan angka sesuai urutan abjad. Terakhir di pesan errornya ada “server SOURCE ADDRESS 7812 is invalid”, di paket pcap yang dikirim ke 7812 source IP addressnya “104 18 14 101”, kalau diganti bisa jadi 10 4 18 14 10 1 (JDRNJA)
![image](https://github.com/jezz16/Jarkom-2023/assets/99706251/bd45c685-6d8a-42cb-ab77-9c8d45d9405e)

### Nomor 7
#### Soal
Berapa jumlah packet yang menuju IP 184.87.193.88?

#### Langkah Penyelesaian
1. Buka file pcap
2. Filter yang menuju IP 184.87.193.88
3. Hitung jumlah paket (6 paket)
   ![image](https://github.com/jezz16/Jarkom-2023/assets/99706251/5bc8b719-15f2-4654-897a-7b7244d386c7)


### Nomor 8
#### Soal
Berikan kueri filter sehingga wireshark hanya mengambil semua protokol paket yang menuju port 80! (Jika terdapat lebih dari 1 port, maka urutkan sesuai dengan abjad)

#### Langkah Penyelesaian
1. Tentukan filter yang benar (tcp.port == 80 || udp.port == 80)
   ![soal4-1](https://github.com/jezz16/Jarkom-2023/assets/113823539/ae2966c4-42ec-4d59-a279-215b45e21ab1)

2. Masukkan filter ke ncat terminal
   ![soal4-2](https://github.com/jezz16/Jarkom-2023/assets/113823539/24a51248-2d7a-4dd1-a45f-3c557c77b0b4)


### Nomor 9
#### Soal
Berikan kueri filter sehingga wireshark hanya mengambil paket yang berasal dari alamat 10.51.40.1 tetapi tidak menuju ke alamat 10.39.55.34!

#### Jawaban
ip.src == 10.51.40.1 && ip.dst != 10.39.55.34
![image](https://github.com/jezz16/Jarkom-2023/assets/99706251/e1a7e96c-b44c-45a1-9981-8c86518db872)

### Nomor 10
#### Soal
Sebutkan kredensial yang benar ketika user mencoba login menggunakan Telnet!
#### Langkah Penyelesaian
1. Buka file pcap
2. Filter Telnet, lalu follow TCP Stream
![image](https://github.com/jezz16/Jarkom-2023/assets/99706251/88156336-bfd4-427c-a739-97c629bf22f5)
3. Ganti nilai stream sampai mendapatkan kredensial yang sesuai
   ![image](https://github.com/jezz16/Jarkom-2023/assets/99706251/d209ca2f-1e00-406f-b535-5879f3a3076d)
   ![image](https://github.com/jezz16/Jarkom-2023/assets/99706251/706964eb-a43b-4e1c-a7fd-5aa445c6f5a6)


