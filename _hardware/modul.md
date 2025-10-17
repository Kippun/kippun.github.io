---
title: Modul Perangkat
author: A. Kiflan Jiyaad Mafazi. A & Muhammad Rizki Akbar
date: 2025-10-10
category: Jekyll
layout: post
---

---

# Modul Transceiver

Bagian ini membahas secara mendalam berbagai modul transceiver yang kompatibel dengan perangkat Edgecore Cassini dan DCSG. Modul-modul ini berperan sebagai komponen inti yang mengubah sinyal listrik dari perangkat jaringan menjadi sinyal optik yang dapat ditransmisikan melalui serat optik, dan sebaliknya. Setiap jenis modul, seperti QSFP28, CFP2-DCO, dan SFP 10G, memiliki fungsi, kecepatan, dan teknologi yang berbeda sesuai dengan kebutuhan jaringan.


## LUMENTUM CFP2-DCO 200G

<img src="{{ '/assets/gitbook/images/alt/sfp2-dco.webp' | relative_url }}" alt="Modul SFP2-DCO" width="40%">
<br>

Modul **CFP2-DCO (Coherent CFP2-Digital Coherent Optics)** merupakan salah satu jenis *pluggable optical transceiver* yang digunakan pada perangkat jaringan optik berkecepatan tinggi seperti **Edgecore Cassini** dan sistem **Disaggregated Optical Transport Network (OTN)**.  
CFP2-DCO berfungsi untuk mengonversi sinyal digital dari perangkat jaringan menjadi sinyal optik yang dapat ditransmisikan melalui serat optik jarak jauh menggunakan teknologi **coherent detection**.

Modul ini menjadi komponen penting dalam sistem transport optik modern karena mendukung **kecepatan transmisi hingga 200 Gbps atau lebih**, serta efisiensi tinggi dalam penggunaan spektrum optik.

### 1. Prinsip Kerja

CFP2-DCO bekerja berdasarkan teknologi **coherent optical communication**, di mana sinyal cahaya tidak hanya membawa informasi dalam bentuk intensitas, tetapi juga dalam fase dan polarisasi.  
Sinyal ini kemudian diproses secara digital oleh **Digital Signal Processor (DSP)** yang tertanam di dalam modul.

Secara garis besar, proses kerjanya meliputi tahapan berikut:

1. **Digital Input**: Data dikirim dari perangkat host (seperti router atau transponder) ke CFP2-DCO melalui antarmuka listrik.
2. **Modulasi Optik**: DSP di dalam modul memodulasi data menggunakan teknik seperti QPSK (Quadrature Phase-Shift Keying) atau 16QAM (Quadrature Amplitude Modulation).
3. **Transmisi Serat Optik**: Sinyal yang telah dimodulasi dikirimkan melalui serat optik menggunakan laser tunable (biasanya pada C-band).
4. **Demodulasi Coherent di Sisi Penerima**: Modul di sisi penerima mendeteksi dan mendekode sinyal optik menjadi data digital kembali.

### 2. Spesifikasi Teknis Umum

| Parameter | Nilai / Deskripsi |
|------------|--------------------|
| **Merek** | LUMENTUM |
| **Form Factor** | CFP2 (C Form-factor Pluggable 2) |
| **Teknologi** | Coherent Optical Transmission |
| **Kecepatan Data** | 100G / 200G (beberapa model mendukung 400G) |
| **Modulasi** | QPSK, 8QAM, 16QAM |
| **Wavelength** | C-Band (1530–1565 nm) |
| **FEC (Forward Error Correction)** | Soft-decision FEC untuk koreksi error tingkat lanjut |
| **Interface ke Host** | 8×25G atau 4×50G electrical interface (CAUI-4) |
| **Interface ke Fiber** | Duplex LC / SC atau konektor optik khusus |
| **Jarak Transmisi Maksimal** | Hingga 80km |
| **Kompatibilitas Standar** | CFP MSA, ITU-T G.698, OIF-400ZR (tergantung vendor) |

### 3. Fungsi dan Manfaat dalam Arsitektur Cassini

Dalam perangkat **Edgecore Cassini** atau platform OTN sejenis, CFP2-DCO berperan sebagai **optical line interface** pada *line card slot*. Fungsi utamanya meliputi:

1. **Konversi Sinyal Digital ke Optik**  
   Mengubah data listrik berkecepatan tinggi dari prosesor jaringan menjadi sinyal optik yang siap dikirim ke jaringan transport.

2. **Transmisi Jarak Jauh**  
   Memungkinkan pengiriman data jarak jauh antar lokasi (metro, regional, atau long-haul) melalui serat optik dengan efisiensi spektral tinggi.

3. **Dukungan Multimodulasi dan Adaptasi Dinamis**  
   Modul mampu menyesuaikan modulasi dan baud rate sesuai kondisi jaringan, untuk menjaga stabilitas sinyal dan efisiensi bandwidth.

4. **Koherensi dan Deteksi Fase**  
   Dengan teknologi coherent detection, CFP2-DCO dapat mengoreksi distorsi sinyal dan degradasi optik akibat jarak jauh secara digital melalui DSP.

### 4. Kompatibilitas Perangkat

CFP2-DCO dapat digunakan pada slot **CFP2-compatible port** yang mendukung antarmuka **digital coherent**.  
Dalam konteks perangkat Cassini, port ini biasanya ditemukan pada **line card slot (1–8)** yang disediakan khusus untuk modul 200G atau CFP2-DCO.

Modul ini **tidak dapat berfungsi** pada slot QSFP28 atau SFP+ biasa, karena perbedaan arsitektur sinyal (non-coherent vs coherent).  
Selain itu, perangkat host harus memiliki sistem operasi jaringan (NOS) yang mendukung kontrol DCO, seperti:
- **OcNOS RON (Research Optical Network build)**, atau  
- **SONiC dengan Coherent Optics Extension**.

> **Dokumentasi modul bisa dilihat dengan klik** [**tautan berikut**](https://resource.fs.com/mall/doc/20240307155949t12wsr.pdf). 

---

## QSFP28 100G (FINISAR FTLC9558REPM)

<img src="{{ '/assets/gitbook/images/alt/ftlc9558repm.webp' | relative_url }}" alt="Modul FTLC9558REPM" width="50%">
<br>

QSFP28 merupakan jenis modul transceiver hot-pluggable yang dirancang untuk koneksi data berkecepatan tinggi hingga 100 Gigabit Ethernet di pusat data dan jaringan telekomunikasi. QSPF28 memiliki singkatan dari "Q" yaitu Quad yang berarti memiliki 4 saluran dan "SFP" merujuk pada Small Form-factor Pluggable yang merupakan modul kecil ringkas yang digunakan untuk menghubungkan perangkat jaringan seperti switch dan router ke kabel serat optik atau tembaga.

### 1. Prinsip Kerja

Modul Finisar **FTCL9558REPM** (QSFP28 100GBASE-SR4) berkerja berdasarkan konsep **parallel optical trensmission** menggunakan teknologi Multi-Mode Fiber (MMF) dan laser VCSEL (Vertical Cavity Surface-Emittin Laser).

Secara garis besar, proses transmisinya dapat dijelaskan sebagai berikut:

1. **Input Sinyal Digital**
   Data digital dengan total laju 100 Gb/s dikirim dari host sistem (seperti switch ASIC atau network processor) ke transceiver melalui antarmuka listrik CAUI-4, yang terdiri dari empat jalur paralel 25 Gb/s

2. **Konversi Elektrik ke Optik (Electrical-to-Optical Conversion)**
   Di dalam modul, setiap jalur 25 Gb/s dikonversi menjadi sinyal optik menggunakan laser VCSEL 850 nm.
   Keempat sinyal tersebut ditransmisikan secara bersamaan melalui empat serat optik (TX1–TX4) di dalam konektor MPO-12.

3. **Transmisi Melalui Serat Optik**
   Sinyal cahaya merambat di dalam multimode fiber (OM3 atau OM4) sejauh 70–100 meter, sesuai standar 100GBASE-SR4.

4. **Konversi Optik ke Elektrik (Optical-to-Electrical Conversion)**
   Di sisi penerima, empat sinyal optik yang masuk (RX1–RX4) diubah kembali menjadi sinyal elektrik oleh array photodiode (PIN receiver) dan dikirim ke host system.

### 2. Spesifikasi Teknis Umum

| Parameter | Nilai / Deskripsi |
| --- | --- |
| **Merek** | FINISAR |
| **Model** | FTLC9558REPM |
| **Kecepatan Data** | 100G |
| **Wavelength** | 840nm hingga 860nm |
| **Form Factor** | QSFP28, hot-pluggable |
| **Aggegate bit rate** |  Hingga 103.1 Gb/s |
| **Daya Konsumsi** | < 2.5 W |
| **Voltase Operasi Tunggal** | 3.3 V |
| **Rentang Temperatur Operasi** | 0 °C hingga +70 °C |
| **Optical Modulation** | 70m (OM3) / 100m (OM4) |
| **Media Jenis** | Multi-Mode Fiber (MMF), 4 x 25 Gbps (parallel optics) |
| **Konektor Optik** | MPO-12 receptacle (female) |
| **Antarmuka Listrik** | 4 x 25 Gbps (CAUI-4 style) |

### 3. Fungsi dan Manfaat dalam Arsitektur Cassini

Dalam sistem **Edgecore Cassini**, modul QSFP26 seperti FTLC9558REPM digunakan untuk lapisan Ethernet switching dan data aggregation, tidak seperti CFP2-DCO yang digunakan untuk transport optik jarak jauh.

Peran dan manfaatnya dapat dijelaskan sebagai berikut:

**1. Fungsi Utama**
   - **Interface Ethernet 100 GbE**
   Menyediakan koneksi berkecepatan tinggi antar perangkat Cassini, server, atau switch lain dalam domain LAN/MAN.

   - **Short-Reach Connectivity**
   Digunakan untuk koneksi jarak pendek (≤ 100 m) di dalam pusat data atau antar perangkat yang berada di rak yang sama.

   - **High-Density Aggregation Port**
   Dengan form factor QSFP28 yang ringkas, memungkinkan Cassini memiliki banyak port 100 G dalam ruang fisik terbatas.

**2. Manfaat dalam Arsitektur Cassini**

| Aspek | Manfaat |
| --- | --- |
| **Konektivitas** | Menghubungkan modul line card CFP2-DCO (optical transport) dengan fabric Ethernet di layer atas.
| **Fleksibilitas** | Dapat digunakan sebagai port 1 x 100G atau 4 x 25G (breakout mode), tergantung penggunaan |
| **Efisiensi Energi** | Konsumsi daya rendah (< 2.5 W) dibanding modul optical transport |
| **Kepadatan Port Tinggi** | Mendukung hingga 16 port QSFP 29 pada Cassini untuk throughput total > 1.6 Tb/s |
| **Integrasi Mudah (Plug-and-Play)** | Tidak memerlukan konfigurasi optik atau tuning wavelength seperti modul coherent |

> **Dokumentasi modul bisa dilihat dengan klik** [**tautan berikut**](https://www.epsglobal.com/Media-Library/EPSGlobal/Products/files/finisar/transceivers/FTLC9558REPM.pdf).

---

## SFP+ 10G (Youthton YSP96-8503M)

<img src="{{ '/assets/gitbook/images/alt/ysp96-8503m.webp' | relative_url }}" alt="Modul YSP96-8503M" width="30%">
<br>

SFP+ 10G merupakan jenis modul transceiver hot-pluggable yang dirancang untuk mendukung transmisi data berkecepatan tinggi hingga 10 Gigabit per detik (10 Gbps) pada jaringan Ethernet.

SFP+ merupakan singkatan dari Small Form-factor Pluggable Plus, yang merupakan versi pengembangan dari modul SFP (1 G). Modul ini banyak digunakan pada perangkat jaringan seperti switch, router, server, maupun perangkat penyimpanan jaringan (NAS dan SAN) untuk menyediakan konektivitas optik atau tembaga berkecepatan tinggi.

| Parameter | Nilai / Deskripsi |
| --- | --- |
| **Merek** | Youthton |
| **Model** | YSP96-8503M |
| **Form Factor** | SFP+ (Small Form-Factor Pluggable Plus) |
| **Kecepatan Data** | 10G
| **Wavelength** | 850nm |
| **Rentang Tempratur Operasi** | 0°C – 70°C |
| **Hot-Pluggable** | Supported |
| **Konektor Optik** | Duplex LC |
| **Media Jenis** | Multi-Mode Fiber (MMF) OM3/OM4 |
| **Optical Modulation** | 300m (OM3) / 400m (OM4) |
| Digital Diagnostic Monitoring (DDM) | Supported |

---

# Modul Pendukung

Selain modul transceiver, keberhasilan koneksi jaringan sangat bergantung pada media fisik yang digunakan untuk menghubungkannya. Bagian ini akan menjelaskan berbagai jenis kabel yang kompatibel dengan modul-modul yang disebutkan di atas. Kami akan mengulas jenis-jenis kabel serat optik dan kabel tembaga yang berfungsi sebagai jalur transmisi data, memastikan sinyal optik dapat merambat dengan efisien dan optimal sesuai dengan spesifikasi modul.

## Duplex LC

<img src="{{ '/assets/gitbook/images/alt/duplex_lc.webp' | relative_url }}" alt="Kabel Duplex LC" width="35%">

Duplex LC (Lucent Connector) merupakan kabel transmisi data optik yang dirancang memiliki dua serat optik dalam satu kabel dengan tujuan untuk mengirimkan data dalam dua arah secara bersamaan. Berbeda dengan kabel simplex yang hanya memiliki satu serat optik untuk transmisi satu arah, duplex menggunakan dua serat optik dalam satu kabel yang berfungsi untuk menghubungkan perangkat jaringan seperti switch dan router untuk transmisi data dua arah berkecepatan tinggi pada pusat data.

Kabel dengan tipe duplex LC pada lingkup perangkat seperti Cassini dan DCSG cocok untuk modul seperti SFP+ 10G dan CFP2-DCO yang membutuhkan tipe port perangkat SFP

> **Dokumentasi modul bisa dilihat dengan klik** [**tautan berikut**](https://assets.tripplite.com/product-pdfs/en/n37015m.pdf).

---

## MPO12

<img src="{{ '/assets/gitbook/images/alt/mpo12.webp' | relative_url }}" alt="Kabel MPO12" width="75%">
<br>

Kabel MPO12 adalah jenis kabel serat optik dengan kapasitas tinggi yang memiliki 12 serat optik dalam satu konektor tunggal dan digunakan untuk koneksi data berkecepatan tinggi. Fungsi MPO12 untuk menghemat ruang dan menyederhanakan pemasangan dalam pusat data dengan kepadatan tinggi (high-density) melalui konektor tunggal yang terintegrasi.

Kabel MPO12 sangan cocok untuk aplikasi seperti 40G dan 100G, serta dapat dipecah menjadi jaringan yang lebih kecil lagi seperti 4 x 10G atau 3 x 10G menggunakan kabel *breakout*

> **Dokumentasi modul bisa dilihat dengan klik** [**tautan berikut**](https://resource.fs.com/mall/doc/202306051416070c94mg.pdf).