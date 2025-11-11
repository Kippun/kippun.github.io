---
title: Infrastruktur Open Network
author: A. Kiflan Jiyaad Mafazi. A
date: 2025-10-14
category: Jekyll
layout: post
---

*Open networking* atau yang dikenal sebagai *white box* adalah arsitektur jaringan yang memisahkan perangkat keras (hardware) dari perangkat lunak (software) dan vendornya (vendor lock), sehingga memberikan fleksibilitas untuk memilih dan mengkombinasikan komponen dengna software sesuai kebutuhan.

## Arsitektur Umum Open Network

Infrastruktur jaringan modern yang berbasis *open network* umumnya terdiri dari empat lapisan utama yaitu **access layer**, **backhaul layer**, **core layer**, dan **internet layer**.

<img src="{{ '/assets/gitbook/images/alt/infrastruktur.jpg' | relative_url }}" alt="infrastruktur open network" width="100%">
<br>

### 1. Access Layer

Lapisan ini adalah bagian terdekat dengan pengguna (end user). Fungsinya untuk menghubungkan *User Equipment* (UE) seperti ponsel, modem, atau perangkat Internet of Things (IoT) ke jaringan operator melalui antena (mast).

Komponen:
- **UE**: Perangkat pengguna akhir yang terhubung ke jaringan.
- **Mast / eNodeB**: Menara pemancar yang menghubungkan sinyal radio ke jaringan inti.
- **RRU & BBU** (Remote Radio Unit & Baseband Unit): Perangkat pada sisi radio yang menangani pemrosesan sinyal.
- **DCSG** (Disaggregated Cell Site Gateway): Perangkat *open networking* yang berfungsi sebagai gateway pada sisi seluler untuk menghubungkan trafik dari antena menuju jaringan backhaul. DCSG ini menggantikan perangkat proprietary dengan solusi berbasis *white box* dan sistem operasi NOS (Network Operating System)

### 2. Backhaul Layer

Lapisan ini bertugas untuk menghubungkan antara Access Layer dan Core Layer. Pada bagian ini, lalu lintas data yang berasal dari BTS atau cell site dikonsolidasikan menuju pusat jaringan menggunakan perangkat *aggregation router*.

Komponen:
- **Aggregation Router**: Menggabungkan beberapa trafik dari gateway dan mengarahkan ke backbone jaringan.
- **Cassini**: Perangkat *open optical transponder* yang digunakan untuk menggabungkan teknologi *optical transport* (DWDM) dan Ethernet/IP routing. Cassini memungkinkan transmisi data dengan kapasitas tinggi hingga 100G atau lebih dalam jaringan *backhaul* berbasis open network.

### 3. Core Layer

Lapisan ini merupakan pusat pemrosesa utama jaringan dengan fungsi mengelola kontrol, routing, serta autentikasi pengguna. Dalam konteks jaringan seluler, lapisan ini disebut sebagai *Mobile Core*.

Komponen:
- **Mobile Core** mencakup beberapa komponen:
    - MME (Mobility Management Entity)
    - HSS (Home Subscriber Server)
    - SGW (Serving Gateway)
    - PGW (Packet Gateway)
- **Cassini**: Digunakan juga di sisi core layer untuk memperluas kapasitas optik antar pusat data (*data center interconnect*).

### 4. Internet Layer

Lapisan ini merupakan pintu keluar jaringan ke internet publik. Data yang telah diproses dan diarahkan dari Core Layer akan menuju internet agar dapat berkomunikasi dengan layanan global seperti situs web, aplikasi, dan server Cloud.