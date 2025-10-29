---
title: Summary v2
author: A. Kiflan Jiyaad Mafazi. A
date: 2025-10-12
category: Jekyll
layout: post
---

---

# Rangkuman Perangkat Cassini Edgecore AS7716-24SC

## **1. Rangkuman Spesifikasi Sistem Cassini (OcNOS 1.1.0.2)**

| Atribut | Detail |
| --- | --- |
| **Software Product** | OcNOS (Open Compute Network Operating System) |
| **Software Version** | 1.1.0.2 |
| **Hardware Model** | Edgecore Cassini AS7716-24SC-O-AC-F |
| **Software Feature Code** | OTN-IPBASE |
| **System Configuration Code** | S0 |
| **Package Configuration Code** | P0 |
| **Software Baseline Version** | 1.3.8.80 |
| **Install Method** | FTP |
| **ONIE SysInfo** | x86_64-accton_as7716_24sc-r0 |
| **Build Date** | November 24, 2020 |
| **License Type** | IPBASE (standar, tidak termasuk modul optik atau transport) |

Versi ini termasuk dalam rilis awal OcNOS untuk platform Cassini, yang berfokus pada **fitur routing IP dasar** (L2/L3) dan belum memiliki dukungan penuh terhadap **fungsi transport optik seperti CFP2-DCO management atau coherent optical monitoring.**
Build ini tidak termasuk feature pack RON (Reconfigurable Optical Network) yang biasanya digunakan untuk manajemen optical transponder.

## **2. Detail Perangkat Keras**

| Komponen | Deskripsi | Status |
| --- | --- | --- |
| **Model Sasis** | Edgecore Cassini AS7716-24SC | Terdeteksi |
| **Platform** | Disaggregated Optical Packet Transponder | Aktif |
| **Processor** | CPU x86_64 | Terbaca |
| **Power Supply (PSU)** | 2 Unit (Redundant 1+1) | Aktif |
| **Cooling System (Fan)** | 3 + 1 Redundant Dual-Rotor Fans | Aktif |
| **Management Port** | RJ-45 100/1000BASE-T | Aktif |
| **Console Port** | RJ-45 Serial (RS-232) | Aktif |
| **Line Card Slots** | 8 Slot (Support CFP2-DCO / 200G) | Modul tidak terdeteksi |
| **QSFP28 Ports** | 16 Port Fixed (100G Ethernet) | Terbaca secara fisik, tidak aktif di OS |
| **Transceiver Modules** | Finisar FTLC9558REPM (QSFP28) | Tidak terbaca oleh OS |
| **Optical Management** | Coherent Module (CFP2-DCO) | Tidak terdeteksi |
| **Storage (Flash)** | Embedded | Aktif |
| **System Fans & Sensor** | Berfungsi | Terbaca |

Semua komponen dasar seperti PSU, kipas, dan port manajemen terdeteksi dengan benar, tetapi modul optik (QSFP28 / CFP2-DCO) tidak muncul di sistem karena driver atau profil hardware ayng dibutuhkan belum termuat dalam versi IPBASE ini.

## **3. Spesifikasi Perangkat Lunak**

| Komponen | Fungsi | Status / Catatan |
| --- | --- | --- |
| **OcNOS Kernel** | Sistem operasi utama berbasis Linux untuk switching/routing | Aktif |
| **Feature Set** | IPBASE (hanya mendukung routing dasar dan manjaemen switch) | Aktif |
| **Routing Protocols** | Static Route, OSPF, BGP (dasar) | Tersedia |
| **Optical Transport Features** | CFP2-DCO, Optical Channel, Coherent Module | Tidak tersedia |
| **System Management** | CLI, SNMP, Syslog, AAA | Tersedia |
| **Virtualization / VM** | Fitur terbatas (tidak mendukung VM Optical) | Tidak aktif|
| **Bootloader / ONIE** | x86_64-accton_as7716_24sc-r0 | Terpasang, versi lama |
| **Upgrade Support** | Melalui FTP | Terbatas (belum mendukung HTTP/USB ONIE) |
| **Security Features** | User Roles, AAA, Radius/TACACS | Aktif |
| **Licensing Mode** | IPBASE Edition | Non-optical, tidak mencakup modul DCO |

OcNOS 1.1.0.2 masih menggunakan arsitektur klasik dengan dukungan terbatas pada L2/L3 control-plane. Tidak terdapat fitur:
- Optical Power Monitoring
- Coherent Transceiver Diagnostic
- Optical Channel Grouping (OTN Layer)
- Manajemen coherent module CFP2-DCO
Selain itu, sistem tidak memiliki modul CLI seperti `show coherent-module` atau `hardware-profile coherent-module enable`, yang menjadi indikator bahwa build ini belum termasuk Optical Feature Pack (RON).

## **4. Fitur dan Fungsi yang Tidak Didukung**

| Fitur | Status | Dampak |
| Coherent Module Management (CFP2-DCO) | Tidak tersedia | Modul tidak terdeteksi |
| Optical Power & Wavelength Monitoring | Tidak tersedia | Tidak bisa baca nilai optik |
| Transceiver Diagnostic (QSFP28) | Tidak tersedia | Tidak bisa validasi link |
| ONIE Installer Upgrade | Versi lama | Proses upgrade sulit |
| CLI Optical Commands | Tidak dikenal | CLI terbatas |
| Telemetry / gNMI Optical Data | Tidak ada | Tidak bisa integrasi monitoring eksternal |
| Optical Transport Layer (OTN) | Tidak aktif | Cassini tidak berfungsi sebagai transponder |

## **5. Analisis Keseluruhan**

Berdasarkan hasil pemeriksaan dan data sistem:
 - Sistem saat ini berfungsi normal sebagai **perangkat L2/L3 switch-router**.
 - Namun, **fungsi utama Cassini sebagai optical packet transponder belum aktif**, karena software belum memuat modul *coherent optical driver*.
 - Versi OcNOS yang digunakan (1.1.0.2) sudah **lawas dan berumur lebih dari 4 tahun** yang membuatnya tidak lagi mendapatkan pembaruan kompabilitas hardware modern.
 - Fitur optical hanya tersedia di **build RON (Reconfigurable Optical Network)** atau **OcNOS Advanced Optical Release**, yang berisi dukungan penuh untuk CFP2-DCO, QSFP28, optical power minitoring, dan channel wavelength configuration.

---

# Rankuman Perangkat DCSG AGCV208S

Tidak bisa digunakan walau perangkatnya aktif.