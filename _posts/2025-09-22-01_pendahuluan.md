---
title: Pendahuluan
author: Tao He
date: 2019-04-28
category: Jekyll
layout: post
---

OcNOS Virtual Machine dari IP Infusion berguna untuk mengenal OcNOS. OCNOS VM berjalan pada lingkungan x86 standar dan dapat digunakan untuk memvalidasi konfigurasi serta menguji fitur L2, L3, dan MPLS tanpa biaya. Tanpa perlu perangkat fisik, OCNOS VM dapat dijalankan pada *hypervisor* populer seperti **KVM, VirtualBox,** dan **VMware**.

Integrasi Ubuntu dengan OcNOS pada Oracle Virtual Machine dilakukan untuk mempermudah proses manajemen jaringan. Ubuntu berperan sebagai sistem operasi pendukung yang menyediakan sarana akses remote ke OcNOS VM melalui SSH dan console. Dengan menggunakan Ubuntu, administrator dapat melakukan konfigurasi, monitoring, serta validasi fitur OcNOS tanpa memerlukan perangkat keras tambahan. Selain itu, Ubuntu juga dapat diperlakukan sebagai *management station* yang terhubung langsung ke jaringan virtual OcNOS, sehingga seluruh aktivitas administrasi dapat dilakukan secara efisien dan terpusat.

Semua fungsionalitas dasar Layer 2, Layer 3, dan multicast tersedia. Dukungan MPLS juga tersedia, termasuk dukungan terbatas untuk penerusan MPLS.

## Manfaat dari VM OcNOS:

• Gratis 

• Tidak perlu menunggu perangkat keras 

• Mendapatkan familiaritas dengan perangkat lunak OcNOS 

• Memvalidasi konfigurasi 

• Menguji fitur L2, L3, dan MPLS tanpa risiko 

• Prototipe operasi jaringan Daftar Fitur CLI untuk fitur-fitur berikut tersedia.

## Fitur :

- ARP  support
- SSH/Telnet
- SNMP
- Debugging and logging
- AAA
- DHCP, DNS

## Fitur pada layer 2 :

- STP/RSTP/MSTP
- BPDU Guard and Root Guard
- VLAN
- Private VLAN
- LACP
- LLDP
- VLAN Interface
- QinQ
- 802.1x

## Fitur pada layer 3:

- IPV4 Routing
- VRF Support
- RIP v2, RIP NG
- BFD with
- BGP
- OSPF v2, OSPF v3
- VRRP
