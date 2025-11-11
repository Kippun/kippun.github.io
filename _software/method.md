---
title: Integrasi Antara VM
author: Muhammad Rizki Akbar & A. Kiflan Jiyaad Mafazi. A
date: 2025-09-23
category: Jekyll
layout: post
---

## Langkah SSH Ubuntu ke OcNOS menggunakan Oracle VBox

Dalam proses pembelajaran jaringan, integrasi antara Virtual Machine (VM) yang menjalankan OCNOS dan Ubuntu Server sebagai penghubung atau client adalah langkah penting untuk memahami bagaimana sistem operasi jaringan dapat dikonfigurasi dan diakses layaknya perangkat jaringan fisik. Pemanfaatan VM memungkinkan simulasi dilakukan tanpa perangkat keras asli, sehingga lebih fleksibel, efisien, dan hemat biaya.

Tujuan utama integrasi ini adalah:

- Menyiapkan lingkungan OCNOS di VM agar memiliki alamat IP yang valid.
- Menghubungkan OCNOS dengan VM Ubuntu melalui jaringan virtual.
- Mengakses OCNOS via SSH sehingga administrasi bisa dilakukan secara remote, bukan hanya lewat console bawaan.
- Melalui integrasi ini, akan didapatkan pengalaman yang mirip dengan pengelolaan switch/router sungguhan, namun dalam bentuk simulasi.

## Konfigurasi IP pada OcNOS di Virtual Machine

Buka OcNOS dalam Virtual Machine

![Tampilan CLI OcNOS VM](/assets/gitbook/images/step_ocnos/01.png)
<br>

Konfigurasi IP pada OcNOS dilakukan menggunakan perintah berikut:

```bash
OcNOS>en
OcNOS#conf t
OcNOS(config)#int eth0
OcNOS(config-if)#ip add 192.168.80.2/24
OcNOS(config-if)#commit
OcNOS(config-if)#shutdown
OcNOS(config-if)#exit
OcNOS(config)#do ping 192.168.80.1
```

Setelah konfigurasi dilakukan, hasil yang muncul akan seperti gambar berikut:

![Ping antar Ethernet OcNOS VM](/assets/gitbook/images/step_ocnos/02.png)

> *Jika terjadi RTO (Request Time Out), artinya konfigurasi IP tidak berhasil. Periksa kembali langkah pengaturan OcNOS atau pastikan perintah yang dimasukkan sudah sesuai.*

<br>

Jika ping menggunakan IP yang dibuat sudah berhasil, langkah selanjutnya adalah membuat user baru dengan perintah berikut:

```bash
OcNOS#config terminal
OcNOS(config)#username <sesuai keinginan> password <sesuai keinginan (panjang 8-32 karakter)>
OcNOS(config)#commit
OcNOS(config)#end
OcNOS#end
```

> *Sebagai contoh pada simulasi ini, nama user yang digunakan adalah "admin" dan password "admin123"*

## Akses OcNOS VM Melalui SSH dari Ubuntu VM

Untuk melakukan integrasi OcNOS VM dengan Ubuntu VM, langkah pertama adalah konfigurasi OcNOS. Atur Network pada Adapter 2, 3, dan 4 dengan konfigurasi berikut:

- Attached to: Bridged Adapter
- Name: Pilihan nama adapter akan berbeda di setiap perangkat (gunakan default)
- Adapter Type: Pada bagian ini setiap device memiliki tipe yang berbeda, gunakan tipe default seperti:
  - AMD PCNet FAST III (Am79C973)
  - Intel PRO/1000 MT Desktop (82540EM)
  - Paravirtualized Network Adapter (virtio-net)
- Promiscuous Mode: Allow All
- Check Box pada Cable Connected pastikan tercentang

![Konfigurasi Ubuntu VM](/assets/gitbook/images/step_ubuntu/01.png)

Pertama, jalankan CLI Ubuntu dan gunakan perintah berikut untuk konfigurasi IP. Isikan password super user jika diminta.

```bash
sudo ip addr add 192.168.80.3/24 dev enp0s3
```

Selanjutnya, gunakan perintah berikut untuk mengaktifkan interface enp0s3:

```bash
sudo ip link set enp0s3 up
```

Setelah itu, lakukan uji ping ke OcNOS menggunakan IP yang sudah dibuat (pada contoh ini IP OcNOS adalah 192.168.80.2):

```bash
ping 192.168.80.2
```
<br>

![Ping Ubuntu ke OcNOS VM](/assets/gitbook/images/step_ubuntu/02.png)
<br>
Selanjutnya, dari OcNOS, lakukan uji ping ke IP Ubuntu dengan perintah berikut:

```bash
do ping 192.168.80.3
```

Jika kedua Sistem Operasi (OS) sudah bisa saling terhubung, lakukan SSH dari Ubuntu ke OcNOS dengan perintah:

```bash
ssh admin@192.168.80.2
```

Pastikan IP yang dituju adalah IP OcNOS.

Akan muncul verifikasi koneksi. Ketik "yes" untuk melanjutkan, lalu masukkan password yang sudah dibuat di OcNOS.
Pada tahap ini, VM Ubuntu telah berhasil melakukan Remote Login via SSH, dan OcNOS bertindak sebagai server SSH.

# Melakukan Konfigurasi Ping dari OcNOS ke OcNOS Menggunakan ethernet 1 - ethernet 3

Konfigurasi ini dilakukan agar VM OcNOS bisa terhubung (diuji menggunakan ping) ke sesama VM OcNOS. Tujuannya adalah untuk melakukan simulasi *real networking* dan memahami cara menghubungkan antar router yang berbeda.

Pertama, buat *clone*/salinan dari VM OcNOS. Buka Oracle VirtualBox, lalu klik kanan pada VM OcNOS dan pilih menu "clone". Alternatifnya, klik kiri sekali pada VM lalu gunakan kombinasi tombol "ctrl + o".

![Klik kanan pada OcNOS VM](/assets/gitbook/images/sbs_ocnosclone/01.png)
<br>

Akan tampil menu *clone*. Biarkan pengaturan secara default dan klik Finish untuk melanjutkan.

![Konfigurasi VM](/assets/gitbook/images/sbs_ocnosclone/02.png)
<br>

Proses *clone* akan berjalan. Setelah selesai, VM salinan akan muncul di sidebar Oracle VBox sesuai penamaan yang dibuat.

![Tampilan VM OcNOS Clone](/assets/gitbook/images/sbs_ocnosclone/03.png)
<br>

Selanjutnya, masuk ke Settings pada OcNOS (VM asli) dan OcNOS Clone. Pilih menu Network, lalu terapkan konfigurasi berikut untuk adapter 2 - 4 di kedua VM:
- Attached to: internal network
- Name : intnet
- Promiscuous Mode: Allow All
- Cable Connected: Centang

![Konfigurasi VM OcNOS Clone](/assets/gitbook/images/sbs_ocnosclone/04.png)
<br>

Selanjutnya, jalankan VM OcNOS dan VM OcNOS Clone secara bersamaan. Lakukan login di keduanya untuk masuk ke tahap konfigurasi dengan kode berikut.

```bash
OcNOS>en
OcNOS #configure terminal
OcNOS config #do show ip int brief
```
<br>

Akan muncul tampilan output tabel status interface dari IP yang sebelumnya dibuat. Agar kedua VM OcNOS bisa saling terhubung, salah satu VM perlu dikonfigurasi dengan alamat IP yang berbeda namun masih dalam satu subnet. Contoh kode berikut mengubah IP pada salah satu VM:

```bash
OcNOS config #int eth0
OcNOS config-if #ip add 192.168.80.3/24
OcNOS config-if #commit
OcNOS config-if #no shutdown
OcNOS config-if #exit
OcNOS config #do show ip int brief
```
> *Catatan: Agar bisa terhubung, kedua VM harus berada di subnet yang sama (misalnya 192.168.80.x/24). Pastikan oktet 1-3 sama, dan hanya oktet ke-4 yang berbeda untuk setiap VM.*

![Konfigurasi IP](/assets/gitbook/images/sbs_ocnosclone/06.png)
<br>

Setelah IP diubah pada salah satu VM, lakukan uji ping ke IP VM lawannya. Contoh: jika VM OcNOS-1 menggunakan IP 192.168.80.2, jalankan `do ping 192.168.80.3` (begitu juga sebaliknya).

![Konfigurasi IP](/assets/gitbook/images/sbs_ocnosclone/07.png)

> *Koneksi berhasil jika tidak terjadi RTO (Request Time Out) dan kedua VM memberikan balasan ICMP Echo. Jika RTO, berarti koneksi gagal.*

<br>

Konfigurasi untuk adapter 2 (eth1) hingga adapter 4 (eth3) mengikuti cara yang sama seperti eth0, hanya perlu penyesuaian IP-nya, seperti pada kode berikut.

```bash
OcNOS #configure terminal
OcNOS config #do show ip int brief
OcNOS config #int eth1
OcNOS config-if #ip add 192.168.81.3/24
OcNOS config-if #commit
OcNOS config-if #no shutdown
OcNOS config-if #exit
OcNOS config #int eth2
OcNOS config-if #ip add 192.168.82.3/24
OcNOS config-if #commit
OcNOS config-if #no shutdown
OcNOS config-if #exit
OcNOS config #int eth3
OcNOS config-if #ip add 192.168.83.3/24
OcNOS config-if #commit
OcNOS config-if #no shutdown
OcNOS config-if #exit
OcNOS config #write
OcNOS config #do show ip int brief
```

> *Catatan: Kode tersebut dijalankan di salah satu VM (misal, OcNOS Clone). Untuk VM OcNOS (asli), gunakan IP yang berbeda di oktet terakhir (misal, 192.168.81.2/24, 192.168.82.2/24, dst.). Pastikan setiap pasangan interface (eth1 ke eth1, eth2 ke eth2) berada di subnet yang sama.*

![Konfigurasi IP](/assets/gitbook/images/sbs_ocnosclone/08.png)
<br>

Setelah konfigurasi di kedua VM, lakukan uji ping ke IP lawan untuk setiap interface. Jika semua berhasil, koneksi antar VM OcNOS telah berhasil.

# Melakukan Konfigurasi untuk ethernet 1 - ethernet 3 untuk Terhubung dari Ubuntu ke OcNOS

Dalam proses implementasi jaringan berbasis VirtualBox, setiap mesin virtual dapat memiliki lebih dari satu adapter jaringan yang digunakan untuk membangun konektivitas antar perangkat. Pada skenario ini, koneksi tidak hanya dilakukan melalui adapter utama (Ethernet 0) yang umumnya digunakan untuk akses ke host atau internet, tetapi juga melalui Ethernet 1 hingga Ethernet 3 yang dikonfigurasi khusus untuk membangun komunikasi internal antar mesin virtual.

Konfigurasi ini bertujuan agar mesin virtual Ubuntu dapat terhubung secara langsung dengan mesin virtual OcNOS, sehingga komunikasi data seperti ping test maupun pertukaran paket dapat dilakukan melalui jaringan internal tanpa bergantung pada koneksi eksternal. Dengan demikian, pengujian dan simulasi jaringan dapat berjalan lebih fleksibel dan mendekati kondisi nyata dalam penerapan perangkat jaringan.

Untuk melakukan konfigurasi, buka Oracle VirtualBox dan masuk ke Settings VM Ubuntu. Buka menu Network, lalu terapkan konfigurasi berikut untuk Adapter 1 hingga Adapter 3.
- Attached to: Internal Network
- Name: intnet
- Promiscuous Mode: Allow All
- Cable Connected: Centang

![Konfigurasi Ethernet Ubuntu](/assets/gitbook/images/sbs_ubuntunew/01.png)

Setelah konfigurasi, nyalakan Ubuntu VM dan OcNOS VM yang sebelumnya sudah dikonfigurasi. Masukkan user dan password untuk melanjutkan.

Tahap selanjutnya adalah konfigurasi IP di Ubuntu untuk setiap adapter (0 hingga 3) menggunakan perintah berikut:

```bash
sudo ip addr add 192.168.80.5/24 dev enp0s3
sudo ip addr add 192.168.81.5/24 dev enp0s8
sudo ip addr add 192.168.82.5/24 dev enp0s9
sudo ip addr add 192.168.83.5/24 dev enp0s10
sudo ip link set enp0s3 up
sudo ip link set enp0s8 up
sudo ip link set enp0s9 up
sudo ip link set enp0s10 up
```

![Konfigurasi IP Ubuntu](/assets/gitbook/images/sbs_ubuntunew/02.png)

Selanjutnya, lakukan uji ping dua arah (dari Ubuntu ke OcNOS dan sebaliknya) untuk memverifikasi koneksi:

Ubuntu
```bash
ping 192.168.80.2
```

OcNOS
```bash
do ping 192.168.80.5
```

![Uji Ping antar Ubuntu dan OcNOS](/assets/gitbook/images/sbs_ubuntunew/03.png)