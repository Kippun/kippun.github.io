---
title: Software
author: Muhammad Rizki Akbar & A. Kiflan Jiyaad Mafazi. A
date: 2025-09-21
category: Jekyll
layout: post
---

## Oracle Virtual Box

<img src="{{ '/assets/gitbook/images/OracleVM.webp' | relative_url }}" alt="Logo OcNOS" width="25%">
<br>

VirtualBox adalah perangkat lunak hypervisor tipe-2 yang memungkinkan kamu menjalankan satu atau lebih sistem operasi (guest) di atas sistem operasi utama (host). VirtualBox bersifat cross-platform (tersedia untuk Linux, Windows, macOS) dan banyak dipakai untuk membuat lab virtual, pengujian, dan pembelajaran.

### Bagaimana VirtualBox bekerja (konsep dasar)

- VirtualBox berjalan di atas OS host (bukan langsung di hardware), sehingga disebut Type-2 hypervisor.
- Ia membuat mesin virtual (VM) yang punya CPU virtual, RAM, disk virtual, dan perangkat jaringan virtual.
- Setiap VM berperilaku seperti komputer terpisah sehingga kamu bisa instal Ubuntu, OcNOS, atau OS lain di VM tersebut.

### Fitur utama yang relevan untuk lab jaringan

- Snapshot - simpan status VM dan kembali kapan saja.
- Networking modes - NAT, Bridged, Host-only, Internal: fleksibel untuk skenario lab.
- Shared Folders & Guest Additions - mempermudah transfer file, clipboard bersama, sinkron waktu.
- USB passthrough - akses perangkat USB dari VM.
- Headless / Detach GUI - jalankan VM tanpa antarmuka grafis (berguna untuk server).
- Cross-platform & Gratis (Personal / Edu) - mudah dipakai oleh banyak orang.

---

## Open Compute Network Operating System (OcNOS)

<img src="{{ '/assets/gitbook/images/OcNOS.webp' | relative_url }}" alt="Logo OcNOS" width="50%">
<br>

OcNOS Virtual Machine dari IP Infusion berguna untuk mengenal OcNOS. OCNOS VM berjalan pada lingkungan x86 standar dan dapat digunakan untuk memvalidasi konfigurasi serta menguji fitur L2, L3, dan MPLS tanpa biaya. Tanpa perlu perangkat fisik, OCNOS VM dapat dijalankan pada *hypervisor* populer seperti **KVM, VirtualBox,** dan **VMware**.

Integrasi Ubuntu dengan OcNOS pada Oracle Virtual Machine dilakukan untuk mempermudah proses manajemen jaringan. Ubuntu berperan sebagai sistem operasi pendukung yang menyediakan sarana akses remote ke OcNOS VM melalui SSH dan console. Dengan menggunakan Ubuntu, administrator dapat melakukan konfigurasi, monitoring, serta validasi fitur OcNOS tanpa memerlukan perangkat keras tambahan. Selain itu, Ubuntu juga dapat diperlakukan sebagai *management station* yang terhubung langsung ke jaringan virtual OcNOS, sehingga seluruh aktivitas administrasi dapat dilakukan secara efisien dan terpusat.

Semua fungsionalitas dasar Layer 2, Layer 3, dan multicast tersedia. Dukungan MPLS juga tersedia, termasuk dukungan terbatas untuk penerusan MPLS.

### Mengapa Memilih OcNOS?

- Gratis 
- Tidak perlu menunggu perangkat keras 
- Mendapatkan familiaritas dengan perangkat lunak OcNOS 
- Memvalidasi konfigurasi 
- Menguji fitur L2, L3, dan MPLS tanpa risiko 
- Prototipe operasi jaringan Daftar Fitur CLI untuk fitur-fitur berikut tersedia.

### Keunggulan Utama OcNOS

- ARP  support
- SSH/Telnet
- SNMP
- Debugging and logging
- AAA
- DHCP, DNS

### Kemampuan Jaringan di Layer 2

- STP/RSTP/MSTP
- BPDU Guard and Root Guard
- VLAN
- Private VLAN
- LACP
- LLDP
- VLAN Interface
- QinQ
- 802.1x

### Kemampuan Routing di Layer 3

- IPV4 Routing
- VRF Support
- RIP v2, RIP NG
- BFD with
- BGP
- OSPF v2, OSPF v3
- VRRP

---

## Ubuntu

<img src="{{ '/assets/gitbook/images/Ubuntu.webp' | relative_url }}" alt="Logo OcNOS" width="35%">
<br>

Ubuntu adalah salah satu distribusi Linux yang paling populer dan dikembangkan oleh Canonical. Sistem operasi ini bersifat **open-source**, stabil, dan memiliki dukungan komunitas yang luas. Ubuntu tersedia dalam dua varian utama:

- **Ubuntu Desktop**: dilengkapi dengan antarmuka grafis (GUI) dan biasanya digunakan untuk keperluan sehari-hari seperti komputasi personal.  
- **Ubuntu Server**: versi tanpa GUI yang dioptimalkan untuk efisiensi, kestabilan, dan performa di lingkungan server maupun virtual machine.

Dalam proyek ini digunakan **Ubuntu Server 22.04 LTS** karena lebih ringan dan sesuai untuk kebutuhan jaringan.

### Mengapa Versi 22.04 LTS?
Versi **22.04 LTS (Long Term Support)** dipilih karena memberikan dukungan jangka panjang hingga **5 tahun** (sampai 2027). Beberapa keunggulannya antara lain:

- **Stabil dan Teruji**: Cocok untuk penggunaan server yang membutuhkan reliabilitas tinggi.  
- **Ringan**: Tidak ada antarmuka grafis sehingga resource CPU dan RAM lebih hemat.  
- **Dukungan Perangkat Keras**: Mendukung hardware modern dengan lebih baik.  
- **Keamanan**: Mendapatkan pembaruan keamanan secara berkala selama masa dukungan.  

### Persyaratan Sistem
Ubuntu Server memiliki kebutuhan sistem yang cukup fleksibel. Untuk menjalankan dalam virtual machine, spesifikasi minimal adalah:

- **CPU**: 1 GHz prosesor (x86_64 atau ARM64)  
- **RAM**: 1 GB (disarankan lebih besar untuk performa lebih baik)  
- **Storage**: 8 GB (disarankan ≥ 25 GB)  

Semakin besar resource yang disediakan, semakin lancar kinerja server dalam menjalankan layanan tambahan.

### Peran Ubuntu dalam Proyek
Dalam konteks dokumentasi ini, Ubuntu berfungsi sebagai **mesin pendukung** yang mengatur dan mengakses OcNOS VM melalui **SSH (Secure Shell)**. Dengan begitu, Ubuntu:

- Menjadi **penghubung** untuk remote akses ke OcNOS.  
- Menyediakan lingkungan untuk menjalankan perintah, skrip otomatisasi, maupun tool jaringan.  
- Memastikan manajemen konfigurasi dapat dilakukan dengan lebih fleksibel dan efisien.  

Singkatnya, Ubuntu Server bertindak sebagai **platform kontrol** yang mendukung jalannya simulasi jaringan berbasis OcNOS di dalam virtual environment.