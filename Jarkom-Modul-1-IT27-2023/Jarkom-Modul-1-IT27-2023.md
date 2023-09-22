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
Filter ip.src == 10.21.78.111 atau tcp.stream eq 43
Jawaban : gunicorn
Filter ip address dengan alamat 10.21.78.111

Lalu tcp follow, dan disitu bisa dilihat tipe servernya


