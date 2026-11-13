# Tugas Scraping Budaya

# Akuisisi Data Publik: Museum Nasional Indonesia

Disusun oleh: **Clementin Christianingsi Mune Harum** (NIM: **2501010363**)

## 1. Sumber Data
* **Nama Sumber:** Museum Nasional Indonesia
* **URL:** https://museumnasional.or.id (Indeks Sitemap: `https://museumnasional.or.id/post-sitemap.xml`)
* **Penerbit:** Indonesian Heritage Agency (Museum dan Cagar Budaya) - Kemendikbudristek

## 2. Tanggal dan Jam Akses
* **Waktu Mulai Akuisisi:** 2026-11-14 01:05:10 WITA
* **Waktu Selesai Akuisisi:** 2026-11-14 01:08:45 WITA

## 3. Metode Akuisisi
* **Metode:** Web Scraping menggunakan Python (`requests` dan `BeautifulSoup4`).
* **Halaman Target:** Daftar URL artikel/publikasi yang diekstrak dari `https://museumnasional.or.id/post-sitemap.xml` (mengambil 105 record halaman).
* **Selector HTML & XML Semantik:**
  * ID Postingan (`post_id`): segmen ID unik pada elemen `<loc>`
  * Judul artikel (`judul`): tag `<h1>`
  * Kategori topik (`kategori`): tag `<a rel="category tag">` atau `<span class="cat-links">`
  * Tanggal pembaruan (`tanggal_pembaruan`): tag `<lastmod>` pada sitemap XML
  * Ringkasan artikel (`ringkasan`): tag `<meta name="description">` atau 200 karakter pertama dari `<div class="entry-content">`

## 4. Batasan Etika
* **Hasil Pemeriksaan `robots.txt`:** Diperiksa secara terprogram menggunakan `urllib.robotparser.RobotFileParser` pada `https://museumnasional.or.id/robots.txt`. Hasil `can_fetch()` menunjukkan akses ke halaman artikel publik diizinkan (`True`), sedangkan jalur `/wp-admin/` dilarang (`Disallow`).
* **Lisensi:** Hak Cipta Publik / Informasi Publik Pemerintah Republik Indonesia (Penggunaan Non-Komersial & Akademik).
* **Jeda Antar-Request:** Diterapkan jeda sopan selama **1.5 detik** (`time.sleep(1.5)`) dan batas `timeout=10` detik pada setiap permintaan HTTP.
* **Data yang Sengaja Tidak Diambil:** Halaman administrator (`/wp-admin/`), file gambar mentah beresolusi tinggi (`.jpg`, `.png`, `.webp`), teks artikel lengkap, serta data pribadi pengguna tidak diambil.

## 5. Penjelasan Kolom Dataset (`data/raw/museumnasional_20261114.json`)
* `post_id`: Nomor identifikasi unik postingan artikel pada situs Museum Nasional (string).
* `judul`: Judul lengkap artikel, pameran, atau koleksi budaya (string).
* `kategori`: Klasifikasi topik atau kategori publikasi artikel (string).
* `tanggal_pembaruan`: Tanggal pembaruan terakhir artikel dalam format `YYYY-MM-DD` (string).
* `ringkasan`: Intisari atau deskripsi singkat dari isi artikel (string).

## 6. Cara Menjalankan Ulang Notebook
1. Instal pustaka Python yang diperlukan: `pip install requests beautifulsoup4 lxml pandas`
2. Buka berkas `notebooks/akuisisi_museumnasional.ipynb` di Jupyter Notebook atau Google Colab.
3. Pastikan variabel identitas (`NAMA_MAHASISWA`, `NIM`, `EMAIL_KAMPUS`) pada bagian awal notebook sudah terisi.
4. Jalankan seluruh sel dari awal hingga akhir melalui menu **Runtime -> Restart session and run all**.
4. Jalankan seluruh sel dari awal hingga akhir melalui menu **Runtime -> Restart session and run all**.
"""
