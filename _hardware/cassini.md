---
title: Cassini
author: Muhammad Rizki Akbar & A. Kiflan Jiyaad Mafazi. A
date: 2025-10-08
category: Jekyll
layout: post
---

# Cassini — Edgecore AS7716-24SC

![Cassini AS7716-24SC](/assets/gitbook/images/alt/cassini_as7716-24sc.webp)
<br>

**Cassini (AS7716-24SC)** adalah perangkat 100GbE *coherent switch / packet transponder* dengan *form factor* 1.5 RU yang dirancang untuk menggabungkan fungsi switching dan transport optik (DWDM/DCO). Perangkat ini cocok untuk inter-datacenter, metro dan long-haul network yang membutuhkan 100G/200G kapasitas tinggi serta fleksibilitas modul optik.

---

## Ringkasan Spesifikasi Cassini AS7716-24C

| Item | Nilai / Penjelasan |
| --- | --- |
| Model | AS7716-24SC (Cassini) |
| Form factor | 1.5 RU |
| Switching fabric / throughput | 3.2 Tbps (full duplex) |
| Switch ASIC | Broadcom StrataXGS™ Tomahawk™ Plus |
| Port tetap | 16 × QSFP28 (setiap port 1×40/100GbE; breakout ke 4×25/10Gbps) [LED mode tersedia untuk 100/40/25/10] |
| Slot ekspansi | 8 × line-card slot (untuk QSFP28 / ACO / DCO CFP2 module) — mix fleksibel untuk 200G/DCO. |
| CPU & storage | Intel® Xeon® D-1518 (4-core), DDR4 SO-DIMM 8 GB ×2, m.2 SSD 32 GB (MLC). |
| MACsec | Dukungan MACsec untuk link client & metro/WAN. |
| ONIE | ONIE pre-loaded (pasang NOS sesuai pilihan). |
| PSU | 1+1 redundant, hot-swappable (AC 100–240VAC / DC -40 to -72V opsi). |
| Power consumption | 1,035 W (max—quick start) / ≈1,100 W (full loading—datasheet note). |
| Cooling | Redundant fan trays (3+1 dual-rotor assemblies); airflow harus konsisten antara PSU & fan tray (F2B atau B2F). |
| Dimensi (WxDxH) | 442.5 × 550 × 66 mm (17.42 × 21.65 × 2.6 in). |
| Berat (net) | 11.6 kg (dengan 2 PSUs terpasang). |
| Lingkungan operasi | 0°C to 45°C; storage -40°C to 70°C; humidity 5%–95% non-condensing. |

---

## Penjelasan detail

### 1. Arsitektur umum & tujuan
- **Kombinasi switch + transport**: Cassini menyatukan switching high-capacity (3.2 Tbps) dengan kemampuan memasang modul optik koheren (DCO/ACO) — sehingga operator dapat mengurangi jumlah perangkat di path DWDM dan tetap menjalankan fungsi L2/L3 di tempat yang sama. Ini membuat deploy inter-datacenter dan metro lebih ringkas dan murah dalam manajemen.

### 2. Port & line-card
- **Port tetap 16×QSFP28**: untuk koneksi 100G (atau mode 40G), tiap port mendukung breakout (4 × 25G atau 4 × 10G). LED pada tiap QSFP28 menunjukan mode link (biru = 100G, oranye = 40G, putih/green untuk breakout).
- **8 slot line-card**: bisa diisi ACO (analog coherent optics CFP2), DCO (digital coherent optics CFP2), atau QSFP28 expansion card — memungkinkan konfigurasi hybrid (client non-coherent + line-side coherent). Rasio non-coherent : coherent yang didukung bisa fleksibel (mis. 1:1 sampai 15:1 tergantung skenario).

### 3. DCO vs ACO vs QSFP28
- **QSFP28** = transceiver non-coherent 100G (client side).  
- **ACO** (analog coherent optics) dan **DCO** (digital coherent optics) adalah opsi line-side untuk transmisi DWDM jarak jauh; DCO biasanya menawarkan kemampuan hot-swap di platform ini (catatan: line-card DCO mendukung hot-swap, ACO dan QSFP28 **tidak** — pasang ACO/QSFP28 saat sistem mati).

### 4. Performa switching & tabel forwarding
- Perangkat memakai Broadcom Tomahawk+ yang memberikan throughput besar (3.2 Tbps) dan mendukung jumbo frames hingga 9216 bytes. Kapasitas tabel (MAC/VLAN/LPM/host) dipengaruhi oleh NOS yang dipasang, namun tipikal nilai tertera pada datasheet (contoh: IPv4/IPv6 LPM dan host entry berkisar pada puluhan ribu entri tergantung mode).

### 5. CPU, memori & storage (untuk NOS/manajemen)
- Kontrol plane memakai Intel® Xeon® D-1518 4-core; memori DDR4 SO-DIMM (8GB ×2) dan penyimpanan m.2 32GB. Artinya platform ini cukup kuat untuk menjalankan NOS komersial maupun beberapa NOS open-source. Pastikan NOS pilihan Anda kompatibel dengan ONIE.

### 6. Power, pendinginan & pemasangan rack
- **PSU**: 1+1 redundant, hot-swappable; mendukung AC 100–240VAC atau DC -40 to -72V (opsi). Saat beban penuh, sistem dapat mengonsumsi ~1,035–1,100 W tergantung konfigurasi kartu & modul. Catatan: bila menggunakan low-line VAC, dianjurkan pakai 2 PSU. 
- **Arus & airflow**: Semua modul PSU dan fan tray harus memiliki arah airflow yang sama (front-to-back atau back-to-front). Pastikan grounding rack sesuai standard dan gunakan dua orang untuk memasang di rack (karena berat).

### 7. Hot-swap & peringatan instalasi
- **Hot-swap**: DCO linecards = hot-swappable; ACO dan QSFP28 linecards = **tidak** hot-swappable (harus matikan sistem sebelum pemasangan). Namun transceiver (SFP/QSFP) **dapat** dihot-swap pada semua linecards. Selalu perhatikan arah aliran udara saat memasang modul PSU/fan.

### 8. Manajemen & software
- Preloaded **ONIE** memudahkan pemasangan NOS pilihan (open source atau komersial). Port manajemen: RJ-45 100/1000Base-T, konsol RJ-45 (ke DB-9), dan USB untuk penyimpanan installer atau log. Platform ini juga menyertakan transport library (API) untuk monitoring/otomatisasi L1. Dukungan MACsec memungkinkan enkripsi link client maupun metro.

### 9. LED & indikator cepat
- **Status normal**: PSU1/PSU2, Diag, dan Fan LED → hijau.  
- **QSFP28 port LEDs**: 1 LED biru = 100G; 1 LED oranye = 40G; 1–4 LED putih = 25G breakout; 1–4 LED hijau = 10G breakout. (Gunakan LED untuk verifikasi cepat mode link).

## Best practices & checklist sebelum produksi
1. Uji interoperabilitas linecard DCO/ACO dan transceiver yang akan dipakai — modul koheren sensitif dengan DSP/vendor.  
2. Pastikan perencanaan daya (1100 W+ headroom) dan pendinginan untuk konfigurasi penuh.  
3. Gunakan 2 orang untuk pemasangan rack & grounding dengan benar.  
4. Lakukan uji NOS di lab sebelum deploy (karena banyak fitur bergantung pada NOS).  
5. Catat batas hot-swap: jangan memasang ACO/QSFP28 tanpa mematikan unit. Gunakan DCO jika butuh hot-swap linecard.

## Use cases ideal
- Inter-Datacenter Connect (short/metro/long-haul) dengan kebutuhan 100G/200G.  
- Operator metro yang ingin menggabungkan switching & optical transport dalam satu box.  
- Migrasi jaringan dari 10/40G ke 100G tanpa mengganti keseluruhan infrastruktur DWDM.