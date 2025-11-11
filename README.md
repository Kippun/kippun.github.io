# Dokumentasi Proyek – Integrasi Software dan Hardware Open Networking  

Website ini dikembangkan sebagai dokumentasi teknis untuk proyek **pengembangan dan integrasi sistem jaringan berbasis Open Networking**.  
Fokus utama dokumentasi ini meliputi dua aspek penting:  

1. **Software Layer**, yang mencakup proses instalasi, konfigurasi, serta pengujian perangkat lunak seperti **OcNOS**, **Ubuntu Server**, dan tools pendukung jaringan.  
2. **Hardware Layer**, yang berfokus pada perangkat fisik seperti **Cassini** dan **DCSG**, mencakup identifikasi spesifikasi, prinsip kerja, serta kompatibilitas dalam sistem terbuka.  

Dengan adanya dokumentasi ini, diharapkan pengguna dan pengembang dapat memahami hubungan antara komponen virtual dan fisik dalam satu ekosistem jaringan yang terintegrasi.

## Teknologi yang Digunakan  

Beberapa komponen utama yang digunakan dalam pengembangan website ini:  

- **Jekyll** → *Static site generator* berbasis Ruby yang digunakan untuk membangun website dokumentasi.  
- **GitBook Jekyll Theme** → Template dokumentasi yang menghadirkan navigasi sidebar, tampilan sederhana, dan struktur konten yang konsisten.  
- **Markdown & HTML** → Bahasa utama untuk menyusun konten dokumentasi agar mudah dibaca dan dikelola.  
- **CSS & Font Awesome** → Digunakan untuk memperindah tampilan serta menambahkan ikon seperti GitHub, Twitter, dan lainnya.  
- **JavaScript** → Mengatur fitur interaktif seperti *search bar*, *dark/light mode*, dan navigasi dinamis.  

## Struktur Repositori  

Struktur direktori dalam proyek ini disusun agar memisahkan dokumentasi perangkat lunak, perangkat keras, dan informasi tambahan dengan jelas:  

- `/_fundamentals` `/_hardware` dan `/_software` → Berisi halaman dokumentasi utama.  
- `/assets` → Menyimpan gambar, CSS, JavaScript, serta ikon.  
- `/_includes` → File partial untuk komponen halaman (header, footer, sidebar, dll).  
- `/_layouts` → Template dasar untuk setiap jenis halaman.  
- `index.md` → Halaman utama (home) dari website.  

## Koleksi Jekyll (Collections)  

Website ini memanfaatkan fitur *collections* dari Jekyll untuk mengelompokkan konten:  

- **software** → Dokumentasi instalasi, konfigurasi, dan integrasi software jaringan.  
- **hardware** → Dokumentasi perangkat keras seperti Cassini, DCSG, dan modul jaringan.  
- **others** → Informasi umum seperti About Us dan lisensi proyek.  

Koleksi ini diatur agar tampil terstruktur di sidebar, memudahkan navigasi dan pembacaan.

## Lisensi  

Proyek ini dikembangkan menggunakan:  

- **[Jekyll](https://github.com/jekyll/jekyll)** — di bawah lisensi [MIT License](https://github.com/jekyll/jekyll/blob/master/LICENSE).  
- **[GitBook Jekyll Theme](https://github.com/sighingnow/jekyll-gitbook)** — juga tersedia di bawah [MIT License](https://github.com/sighingnow/jekyll-gitbook/blob/master/LICENSE).  

Lisensi MIT memperbolehkan penggunaan, modifikasi, dan distribusi ulang selama tetap mencantumkan atribusi kepada pembuat aslinya.

## Tujuan Dokumentasi  

Website ini dibuat untuk:  

- Mendokumentasikan seluruh proses integrasi antara **software (OcNOS, Ubuntu)** dan **hardware (Cassini, DCSG)**.  
- Menyediakan panduan teknis lengkap mulai dari konfigurasi hingga pengujian sistem.  
- Menjadi referensi pembelajaran bagi mahasiswa, teknisi, dan peneliti yang bekerja dengan sistem jaringan terbuka.  
- Menyediakan arsip digital terstruktur agar setiap langkah mudah dilacak dan diperbarui.  

✦ Dibangun dengan ❤️ menggunakan [Jekyll](https://jekyllrb.com/) dan [GitBook Jekyll Theme](https://github.com/sighingnow/jekyll-gitbook).  
