---
title: Summary
author: A. Kiflan Jiyaad Mafazi. A
date: 2025-10-12
category: Jekyll
layout: post
---

# Cassini (Edgecore AS7716-24SC-O)

## 1. Informasi Umum Software

Perangkat Cassini yang digunakan saat ini menjalankan sistem operasi **OcNOS** (Open Compute Network Operating System) buatan **IP Infusion**, dengan detail versi sebagai berikut:

| Komponen | Informasi |
|-----------|------------|
| **Software Product** | OcNOS |
| **Versi** | 1.1.0.2 |
| **Software Feature Code** | OTN_IPBASE |
| **Hardware Model** | Edgecore AS7716-24SC-O-AC-F |
| **Install Method** | FTP via ONIE |
| **Software Baseline Version** | 1.3.8.80 |
| **Build Tahun** | 2020 |
| **ONIE Info** | x86_64-accton_as7716_24sc-r0 |

Sistem ini berbasis **Linux embedded**, dan berfungsi sebagai *Network Operating System (NOS)* yang mengatur layer switching, routing, dan management interface pada perangkat Cassini.

## 2. Fitur yang Didukung pada Build Saat Ini (`OTN_IPBASE`)

Build **IPBASE** dari OcNOS hanya mengaktifkan fitur dasar, seperti:

- Manajemen melalui **CLI**, **Telnet**, dan **SSH**
- Konfigurasi **IP routing (IPv4/IPv6)** dan **ARP**
- Dukungan protokol **BGP**, **OSPF**, dan **VRRP**
- Monitoring hardware dasar (fan, power, temperature)
- SNMP dan logging sistem
- Fitur VLAN, STP, dan QoS dasar
- Interface management (`mgmt0`, `eth`, `ce`)

Namun, build ini **tidak mencakup fitur Optical Transport Network (OTN)** dan **coherent optics**, yang merupakan fungsi utama Cassini di lapisan L1.

## 3. Kekurangan dan Keterbatasan yang Ditemui

Berikut adalah keterbatasan yang teridentifikasi selama pengujian menggunakan firmware `OcNOS 1.1.0.2 - OTN_IPBASE`:

| Aspek | Keterbatasan |
|--------|---------------|
| **Fitur Coherent Optical (CFP2-DCO)** | Tidak tersedia. Command seperti `coherent-module`, `hardware-profile`, dan `interface coherent-module` tidak dikenali. |
| **Lisensi OTN** | Lisensi optical transport tidak termasuk dalam build ini, menyebabkan DCO tidak dapat diaktifkan. |
| **Versi Lama (2020)** | Tidak kompatibel dengan beberapa modul baru seperti *Finisar FTLC9558REPM* atau *CFP2-DCO generasi baru*. |
| **CLI Parser Terbatas** | Tidak tersedia perintah `show platform`, `show feature all`, atau `hardware-profile`. |
| **Software Feature** | Hanya mendukung konfigurasi IP/MPLS, tanpa optical control. |
| **ONIE Access** | Direktori `/etc/onie-release` tidak ditemukan, indikasi OS di-flash langsung tanpa mode ONIE aktif. |
| **Status DCO** | Modul CFP2-DCO terpasang fisik, tapi tidak dikenali oleh sistem (`show coherent-module summary` menunjukkan 0 slot aktif). |

> Build ini hanya berfungsi sebagai **router/switch 100G Ethernet**, tanpa kemampuan **optical transmission atau DWDM control** yang seharusnya dimiliki Cassini.

## 4. Dampak dari Keterbatasan Software

<div class="image-row">
    <div class="image-column">
        <img src="/assets/gitbook/images/alt/cfp2-dco_status1.png" alt="Status LED 1">
        <p class="caption">
            Cek status CFP2-DCO tidak tampil pada CLI OcNOS
        </p>
    </div>
</div>

1. **Modul DCO tidak berfungsi**
   - Cassini tidak dapat melakukan *optical line transmission* melalui slot CFP2-DCO.
   - Semua fungsi coherent optics, FEC, dan laser tuning tidak aktif.
   - Modul DCO terbaca aktif pada CLI OcNOS pada slot 4 dan 5 namun tidak dapat diaktifkan.

2. **Tidak bisa uji fitur optical layer**
   - Pengujian *end-to-end optical transport* antar Cassini tidak bisa dilakukan.
   - Tidak dapat melakukan monitoring sinyal optik (power, modulation, wavelength).

3. **Keterbatasan integrasi**
   - Tidak bisa dihubungkan ke *Optical SDN Controller (ONOS)* karena tidak mendukung *NETCONF/YANG module* untuk DCO.

## 5. Rekomendasi Perbaikan & Alasan Teknis

| Rekomendasi | Penjelasan Teknis |
|--------------|-------------------|
| **Upgrade ke OcNOS RON (Research Optical Network)** | Build ini mengaktifkan command `coherent-module`, `hardware-profile`, dan `interface coherent-module`, serta mendukung manajemen CFP2-DCO dan optical transmission. |
| **Gunakan ONIE Mode untuk Install Baru** | Reinstall melalui ONIE agar sistem bersih, mendeteksi storage, dan memunculkan file `/etc/onie-release`. Hal ini memastikan bootloader mengenali hardware sepenuhnya. |
| **Verifikasi Lisensi Optical Transport** | Hubungi IP Infusion / Edgecore untuk lisensi RON/ADVANCED agar fitur DCO dapat diaktifkan. |
| **Update ke Versi Minimal OcNOS 2.0+** | Versi ini sudah menyertakan dukungan CFP2-DCO standar (Finisar, Fujitsu, Acacia) dan mendukung *coherent optical telemetry*. |

## 6. Alasan Teknis Perlunya Upgrade

- **Build 1.1.0.2 (IPBASE)** berfokus pada routing layer, bukan optical transport.  
- **Build RON / ADVANCED** menambahkan dukungan *DWDM, OTN, dan coherent control* sesuai arsitektur Cassini.  
- Tanpa build yang mendukung pada OcNOS **versi 2.0 keatas**, fitur yang dimiliki sangat terbatas dan membuat fitur berupa mengaktifkan modul CFP2-DCO tidak bisa digunakan serta . 
- Dengan upgrade firmware, Cassini bisa menjalankan perannya sebagai **open optical platform**, mendukung *long-haul link*, *DWDM control*, dan *telemetry monitoring*.

## 7. Kesimpulan

Cassini dengan build **OcNOS 1.1.0.2 - OTN_IPBASE** masih berfungsi untuk operasi jaringan dasar (Layer 2/3), namun belum dapat digunakan untuk fungsi utama sebagai **optical transport system**.  
Untuk mengaktifkan fitur CFP2-DCO dan coherent optics, **diperlukan upgrade software ke build RON atau ADVANCED**, melalui **reinstall via ONIE** dan **aktivasi lisensi optical** dari vendor.




































---

# Dissagregated Cell Site Gateway - (DCSG AGCV208S)

## 1. Deskripsi Umum
Perangkat **DCSG (Disaggregated Cell Site Gateway)** tipe **AGCV208S** merupakan perangkat jaringan terbuka (*open networking device*) yang dirancang untuk mendukung sistem operasi jaringan berbasis *disaggregation*, seperti **OcNOS**, **SONiC**, atau sistem operasi lain yang kompatibel dengan **ONIE (Open Network Install Environment)**.  
Secara umum, perangkat ini tidak dilengkapi dengan sistem operasi bawaan, sehingga perlu dilakukan instalasi OS secara manual melalui ONIE.

## 2. Kondisi Fisik dan Indikator LED

<div class="image-row">
    <div class="image-column">
        <img src="/assets/gitbook/images/alt/dcsg_status1.jpg" alt="Status LED 1">
        <p class="caption">
            Status LED SYS Hijau menyala beberapa saat
        </p>
    </div>
    <div class="image-column">
        <img src="/assets/gitbook/images/alt/dcsg_status2.jpg" alt="Status LED 2">
        <p class="caption">
            Status LED SYS mati mengindikasikan OS belum aktif atau dalam mode ONIE
        </p>
    </div>
</div>

Berdasarkan hasil observasi terhadap indikator LED pada perangkat, didapatkan kondisi sebagai berikut:

| LED | Warna | Status | Keterangan |
|:--|:--:|:--:|:--|
| SYS | Hijau (berkedip) | Aktif | Menandakan perangkat sedang melakukan proses booting atau berada dalam mode ONIE |
| PWR | Merah (menyala stabil) | Anomali | Mengindikasikan adanya masalah pada daya, seperti hanya satu PSU aktif atau ketidaksesuaian tegangan |
| FAN | Hijau (menyala stabil) | Normal | Sistem pendinginan berfungsi dengan baik dan seluruh kipas terdeteksi normal |

> Dari hasil di atas, dapat disimpulkan bahwa perangkat dalam kondisi menyala dan melakukan proses inisialisasi, namun belum sepenuhnya menjalankan sistem operasi utama.

## 3. Akses Melalui Port Konsol
Upaya untuk mengakses sistem melalui **port konsol RJ45** maupun **port USB-C** menunjukkan hasil sebagai berikut:
- Akses menggunakan **PuTTY dan Tera Term (Windows)** serta **Minicom (Ubuntu)** tidak menampilkan keluaran apapun pada terminal, meskipun konfigurasi *baud rate* dan parameter serial telah disesuaikan (115200 8N1, tanpa *flow control*).
- Kondisi tersebut menunjukkan bahwa perangkat **tidak menjalankan sistem operasi (OcNOS)** atau masih berada dalam tahap **bootloader ONIE tanpa keluaran ke konsol**.
- Kemungkinan lain adalah **perbedaan pinout pada kabel konsol**, sehingga komunikasi TX/RX tidak terbaca dengan benar.

## 4. Analisis dan Kemungkinan Penyebab


Berdasarkan observasi yang dilakukan, terdapat beberapa kemungkinan penyebab perangkat tidak dapat diakses, antara lain:

1. **Sistem operasi jaringan (OcNOS/SONiC) belum terpasang atau rusak.**  
   Perangkat hanya menjalankan ONIE tanpa sistem operasi utama yang dapat diakses melalui konsol.
2. **Permasalahan suplai daya.**  
   Indikator PWR berwarna merah mengindikasikan adanya anomali pada salah satu PSU atau tegangan masukan yang tidak sesuai.
3. **Perbedaan pinout kabel konsol.**  
   Kabel konsol dengan standar Cisco kemungkinan tidak cocok dengan konfigurasi pinout perangkat ini.
4. **Kegagalan proses booting.**  
   LED SYS yang berkedip menandakan proses boot sedang berlangsung, namun sistem operasi tidak berhasil dimuat sepenuhnya.

## 5. Kesimpulan
Perangkat **DCSG AGCV208S** dapat menyala dan menunjukkan tanda aktivitas melalui LED indikator, namun belum dapat diakses melalui antarmuka konsol. Berdasarkan hasil pengujian, perangkat kemungkinan:
- Berada pada tahap **bootloader (ONIE)** tanpa sistem operasi terpasang, atau  
- Mengalami **anomali pada subsistem daya**.

Untuk melanjutkan proses analisis dan pemulihan, langkah-langkah yang disarankan meliputi:
- Verifikasi **pinout kabel konsol** yang digunakan.  
- Pemeriksaan **kondisi dan keseimbangan PSU ganda**.  
- Instalasi ulang **sistem operasi jaringan** melalui ONIE menggunakan media USB atau koneksi jaringan.