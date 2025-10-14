---
title: Instalasi Virtual Machine, OcNOS, dan Ubuntu
author: Muhammad Rizki Akbar & A. Kiflan Jiyaad Mafazi. A
date: 2025-09-22
category: Jekyll
layout: post
---

Instalasi Virtual Machine dilakukan untuk menyediakan hypervisor yang akan menjalankan dua sistem operasi berbeda, yaitu OcNOS VM sebagai perangkat jaringan virtual dan Ubuntu sebagai sistem operasi manajemen. Dengan demikian, seluruh proses konfigurasi dan pengujian dapat dilakukan tanpa memerlukan perangkat keras fisik.”

---

## Instalasi Virtual Machine

- Untuk melakukan instalasi Oracle Virtual Box, pertama buka file *installer*nya dan pilih menu next untuk melanjutkan.

![Alt Text](/assets/gitbook/images/sbs_vm/01.png)

- Pada bagian ini pilih “I accept the terms in the License Agreement” untuk menyetujui EULA dari Oracle Virtual Box.

![Alt Text](/assets/gitbook/images/sbs_vm/02.png)

- Siapkan bahan terlebih dahulu:
    
    - Oracle Virtual box  : [Downloads – Oracle VirtualBox](https://download.virtualbox.org/virtualbox/7.1.6/VirtualBox-7.1.6-167084-Win.exe)
    
    - Install image Ocnos pada link berikut : [OcNOS Virtual Machine (VM)](https://www.ipinfusion.com/products/ocnos-vm/)

- Setelahnya akan diarahkan ke bagian dimana file dan folder akan di install.

![Alt Text](/assets/gitbook/images/sbs_vm/03.png)

- Setelah menyetujui file akan di install pada file path yang ditentukan, selanjutnya akan muncul peringatan mengenai gangguan jaringan yang akan terjadi pada saat pengunduhan paket. Untuk melanjutkan pilih menu “Yes”.

![Alt Text](/assets/gitbook/images/sbs_vm/04.png)

- Pada tahap selanjutnya akan muncul tampilan Custom Setup untuk mempermudah akses dan penggunaan VirtualBox. Untuk melanjutkan proses instalasi pilih menu “Next>”.

![Alt Text](/assets/gitbook/images/sbs_vm/05.png)

- Kemudian akan muncul tampilan untuk melakukan proses instalasi paket dari Oracle VirtualBox. untuk menyetujui pilih menu “Install”.

![Alt Text](/assets/gitbook/images/sbs_vm/06.png)

---

## Instalasi OS Ubuntu ke Virtual Machine

- Setelah selesai melakukan instalasi Oracle VirtualBox, buka virtual box kemudian pilih pada bagian New untuk melakukan konfigurasi awal.

![Alt Text](/assets/gitbook/images/sbs_ocnos/01.png)

- Setelah itu lanjutkan konfigurasi pemasangan
    - Nama : OcNOS-VM
    - Type : Linux
    - Subtype : Ubuntu
    - Version : Ubuntu (64-bit)

![Alt Text](/assets/gitbook/images/sbs_ocnos/02.png)

- Lakukan Konfigurasikan jumlah memori yang akan dialokasikan untuk mesin virtual. Dengan ukuran memori yang akan dijalankan.

![Alt Text](/assets/gitbook/images/sbs_ocnos/03.png)

- Lakukan proses ekstrak file image VM OcNOS yang sebelumnya sudah diunduh.

![Alt Text](/assets/gitbook/images/sbs_ocnos/04.png)

- Lalu pada “Hard Disk” lakukan konfigurasi seperti yang saya berikan dibawah ini.

![Alt Text](/assets/gitbook/images/sbs_ocnos/05.png)

![Alt Text](/assets/gitbook/images/sbs_ocnos/06.png)

![Alt Text](/assets/gitbook/images/sbs_ocnos/07.png)

![Alt Text](/assets/gitbook/images/sbs_ocnos/08.png)

- Lalu lakukan konfigurasi untuk display klik kanan pada image> setting> dan pilih vboxVG

![Alt Text](/assets/gitbook/images/sbs_ocnos/09.png)

![Alt Text](/assets/gitbook/images/sbs_ocnos/10.png)

- Langkah selanjutnya kita set up network untuk virtual box:
    - Attached to: Host-only Adapter
    - Name: VirtualBox Host-Only Ethernet Adapter
    - Adapter Type: Pada bagian ini setiap device memiliki tipe yang berbeda, gunakan tipe default seperti:
        - AMD PCNet FAST III (Am79C973)
        - Intel PRO/1000 MT Desktop (82540EM)
        - Paravirtualized Network Adapter (virtio-net)
    - Promiscuous Mode:  Allow All
    - Check Box pada Cable Connected pastikan tercentang

![Alt Text](/assets/gitbook/images/sbs_ocnos/11.png)

- Langkah selanjutnya dilanjutkan dengan konfigurasi untuk adapter 2, 3, dan 4.
    - Attached to: Host-only Adapter
    - Name: Setiap perangkat memiliki tipe yang berbeda (gunakan default).
    - Adapter Type: Pada bagian ini setiap device memiliki tipe yang berbeda, gunakan tipe default seperti:
        - AMD PCNet FAST III (Am79C973)
        - Intel PRO/1000 MT Desktop (82540EM)
        - Paravirtualized Network Adapter (virtio-net)
    - Promiscuous Mode:  Allow All
    - Check Box pada Cable Connected pastikan tercentang

![Alt Text](/assets/gitbook/images/sbs_ocnos/12.png)

- Lanjutkan untuk menambahkan data ports sesuai yang sudah saya buatkan

![Alt Text](/assets/gitbook/images/sbs_ocnos/15.png)

- Lalu di lanjut dengan masuk ke dalam Images OcNOS nya masuk dengan
    - Username : ocnos
    - Password : ocnos

![Alt Text](/assets/gitbook/images/sbs_ocnos/14.png)

Jika sudah masuk ke dalam terminal dari OcNOS, maka proses pemasangan sudah berhasil

![Alt Text](/assets/gitbook/images/sbs_ocnos/13.png)

---

## Instalasi Ubuntu Server Versi 22.04.5 ke Virtual Machine

Pemilihan Ubuntu sebagai sistem operasi pendukung yang akan digunakan pada Virtual Machine dikarenakan dukungan komunitas yang luas, serta stabilitas yang tinggi karena menggunakan versi Long Term Support (LTS), serta ringan dijalankan tanpa antarmuka grafis yang memudahkan untuk simulasi jaringan. Dukungan untuk layanan seperti Secure Shell (SSH) membuat Ubuntu mudah diintegrasikan dengan berbagai platform virtualisasi yang dibutuhkan untuk manajemen serta remote access pada integrasi dengan OcNOS.

Pertama untuk melakukan Instalasi paket [Ubuntu 22.04.5 LTS](https://releases.ubuntu.com/22.04/ubuntu-22.04.5-live-server-amd64.iso) melalui tautan tersebut.

Selanjutnya pada toolbar di bagian atas layar Oracle Virtual Machine, pilih tool "New" untuk membuat VM baru. Kemudian ikuti konfigurasi berikut:

- Name and Operating System
    - Name: (Menyesuaikan, disini menggunakan Ubuntu22.04LiveServer)
    - Folder: Letak folder yang akan diinstal
    - ISO Image: Letak file .iso Ubuntu yang sudah diunduh
    - Type: Linux
    - Subtype: Ubuntu
    - Version: Ubuntu (64-bit)

![Alt Text](/assets/gitbook/images/sbs_ubuntu/01.png)

- Unattend Install
    - Username: (Menyesuaikan, disini menggunakan ubuntu22)
    - Password & Repeat Password: Gunakan katasandi sesuai kebutuan dan mudah diingat

![Alt Text](/assets/gitbook/images/sbs_ubuntu/02.png)

- Hardware
    - Base Memory: 1024 MB (1 GB Memory, lebih besar lebih baik)
    - Processor: 1 CPU (lebih besar lebih baik)

![Alt Text](/assets/gitbook/images/sbs_ubuntu/03.png)

- Hard Disk
    - Hard Disk File Location and Size: 20GB (untuk ukuran 20 GB sudah sangat bagus, lebih besar lebih baik namun tidak dianjurkan karena boros reosurce device dari host itu sendiri)

![Alt Text](/assets/gitbook/images/sbs_ubuntu/04.png)

Setelah melakukan konfigurasi pada Ubuntu, kemudian jalankan Ubuntu VM dan lakukan instalasi sumber daya.

![Alt Text](/assets/gitbook/images/sbs_ubuntu/05.png)

Jika sudah mengunduh semua sumber daya, maka Ubuntu akan melakukan reboot dan akan memulai ulang boot seperti biasa Pada tahap ini tampilan CLI Ubuntu sudah muncul dan akan diminta untuk memasukkan username dan password yang sebelumnya sudah dibuat pada tahap konfigurasi **Unattend Install**.

![Alt Text](/assets/gitbook/images/sbs_ubuntu/06.png)

Apabila login berhasil, tampilan yang muncul akan seperti pada gambar, ditandai dengan pesan "Welcome to Ubuntu" dan prompt **ubuntu22@ubuntu22:~$**. Hal ini menandakan bahwa proses instalasi dan login telah berhasil.

Jika ada pesan kesalahan atau tampilan ini tidak dapat dicapai, nama pengguna dan kata sandi perlu diperiksa kembali.