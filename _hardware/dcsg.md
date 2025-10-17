---
title: DCSG
author: Muhammad Rizki Akbar & A. Kiflan Jiyaad Mafazi. A
date: 2025-10-08
category: Jekyll
layout: post
---


# Disaggregated Cell Single Gateway (DCSG AGCV208S)

![image](/assets/gitbook/images/alt/dcsg_agcv208s.webp)
<br>

Delta Agema™ DCSG (*Disaggregated Cell Site Gateway*) merupakan keluarga perangkat **open networking switch/router** yang dirancang untuk kebutuhan **jaringan 5G, backhaul, dan edge computing**.  
Perangkat ini mengadopsi arsitektur terbuka dengan **ONIE (Open Network Install Environment)**, memungkinkan operator memilih sistem operasi jaringan (Network OS/NOS) sesuai kebutuhan — misalnya SONiC, OcNOS, atau FlexSwitch.

DCSG digunakan sebagai **cell-site router**, **edge aggregation node**, atau **platform mobile backhaul** yang memerlukan *time synchronization* presisi tinggi seperti **IEEE 1588v2**, **SyncE**, dan **GPS-based ToD (Time of Day)**.

---

## Spesifikasi Umum DCSG Series

<div class="table-scroll">
  <table>
    <thead>
      <tr>
        <th>Model</th>
        <th>ASIC</th>
        <th>Port Depan</th>
        <th>Throughput</th>
        <th>CPU</th>
        <th>Memory</th>
        <th>Storage</th>
        <th>Konsumsi Daya</th>
        <th>Fitur Timing</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><b>AGC7008S</b></td>
        <td>Broadcom QumranUX</td>
        <td>8×10G SFP+ + 4×1G SFP + 4×1G RJ45</td>
        <td><b>120 Gbps</b></td>
        <td>Intel Denverton C3508</td>
        <td>2×16 GB DDR4</td>
        <td>128 GB SSD</td>
        <td>400 W</td>
        <td>Microsemi 1588, SyncE, 1PPS, 10 MHz I/O, BITS, GPS</td>
      </tr>
      <tr>
        <td><b>AGCV208S</b></td>
        <td>Broadcom QumranAX</td>
        <td>2×100G QSFP28 + 8×25G SFP28 + 4×10G SFP+ + 4×1G RJ45</td>
        <td><b>300 Gbps</b></td>
        <td>Intel Denverton C3508</td>
        <td>2×16 GB DDR4</td>
        <td>128 GB SSD</td>
        <td>400 W</td>
        <td>Microsemi 1588, SyncE, 1PPS, ToD, GPS</td>
      </tr>
      <tr>
        <td><b>DT-G26X2SL</b> <i>(DCSG 100G FlexE)</i></td>
        <td>Broadcom Qumran2U</td>
        <td>2×100G QSFP28 + 24×25G SFP28</td>
        <td><b>360 Gbps</b></td>
        <td>Intel Denverton C3708</td>
        <td>2×8 GB DDR4</td>
        <td>128 GB SSD</td>
        <td>500 W</td>
        <td>1588, SyncE, 1PPS, BITS, GPS</td>
      </tr>
      <tr>
        <td><b>DT-G28X2SL</b> <i>(DCSG 400G FlexE)</i></td>
        <td>Broadcom Qumran2A</td>
        <td>2×400G QSFP-DD + 2×100G QSFP28 + 24×25G SFP28</td>
        <td><b>800 Gbps</b></td>
        <td>Intel Denverton C3708</td>
        <td>2×8 GB DDR4</td>
        <td>128 GB SSD</td>
        <td>500 W</td>
        <td>1588, SyncE, 1PPS, ToD, GPS</td>
      </tr>
    </tbody>
  </table>
</div>

---

## Arsitektur dan Desain

### 1. **Disaggregated Hardware (Open Compute)**
DCSG menggunakan arsitektur *disaggregated* — artinya perangkat keras (hardware) dan perangkat lunak (software/NOS) dapat dipilih dan dikelola secara terpisah.  
Hal ini memberi fleksibilitas operator untuk:
- Memilih NOS sesuai kebutuhan (SONiC, OcNOS, atau lainnya).
- Mengintegrasikan ke dalam arsitektur SDN (Software Defined Network).
- Menghemat biaya dan mempercepat *feature rollout*.

### 2. **Performa & Kapasitas**
DCSG mendukung throughput antara **120 Gbps hingga 800 Gbps**, bergantung pada model.  
Dengan chipset Broadcom QumranUX/AX/2A, perangkat ini mendukung trafik multi-gigabit untuk jaringan 4G/5G backhaul, serta fitur buffering besar untuk menghindari *packet loss*.

### 3. **Presisi Waktu (Timing Accuracy)**
DCSG memiliki *ultra-precise timing function* — penting untuk sinkronisasi base station 5G.  
Dilengkapi dukungan:
- **IEEE 1588v2 (PTP)**  
- **SyncE (Synchronous Ethernet)**  
- **1 PPS I/O, 10 MHz I/O, ToD (Time of Day)**  
- **GPS receiver** untuk referensi waktu global  
- **BITS interface** (opsional untuk operator core network)

### 4. **Fleksibilitas Port & Form Factor**
Semua model DCSG menggunakan desain *compact 1RU* dengan kombinasi port serbaguna:
- Port *optical* SFP/SFP+/SFP28/QSFP  
- Port *copper* (RJ45)  
- Beberapa varian memiliki port FlexE (Flexible Ethernet) untuk transmisi yang bisa diatur sesuai kebutuhan (100G/400G).

### 5. **Kinerja & Efisiensi Daya**
- CPU: Intel Denverton C-series (2–8 core)  
- Memori: hingga 16 GB per channel (dual channel)  
- Penyimpanan: 128 GB SSD  
- Konsumsi daya rendah (400–500 W)  
- Pendinginan aktif dengan airflow depan-belakang

## Fitur Utama DCSG

| Kategori | Deskripsi |
|-----------|------------|
| **Open Networking** | Mendukung ONIE untuk instalasi sistem operasi jaringan terbuka |
| **Time Sync** | IEEE 1588v2, SyncE, GPS, BITS, 1PPS, ToD |
| **Fleksibilitas** | Varian port hingga 400G dengan dukungan FlexE |
| **Ketahanan** | Dirancang untuk lingkungan outdoor / backhaul |
| **Manajemen** | Konsol RJ45 + Ethernet management port + USB |
| **Performa Jaringan** | Throughput hingga 800 Gbps per perangkat |
| **Arsitektur Modular** | Cocok untuk backbone, edge router, atau cell-site gateway |

---

## Skema Penerapan
Perangkat DCSG dapat digunakan di beberapa lapisan jaringan:
- **Cell-Site Gateway (DCSG)** → sinkronisasi base station 4G/5G  
- **Aggregation Layer** → pengumpulan trafik dari BTS atau small cell  
- **Metro-Edge Router** → penghubung antar-kota / antar-DC  
- **Time-Sensitive Network** → aplikasi industri dan edge-AI