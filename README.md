# Tugas Scraping Budaya

readme_teks = f"""# RTM 1 - Akuisisi Data Publik: {NAMA_SUMBER}

Disusun oleh: **Clementin Christianingsi Mune Harum** (NIM: **2501010363**)

## 1. Sumber Data
* **Nama Sumber:** {NAMA_SUMBER}
* **URL:** {BASE_URL} (Indeks Sitemap: `{SITEMAP_URL}`)
* **Penerbit:** {PENERBIT}

## 2. Tanggal dan Jam Akses
* **Waktu Mulai Akuisisi:** {waktu_mulai.strftime("%Y-%m-%d %H:%M:%S WITA")}
* **Waktu Selesai Akuisisi:** {waktu_selesai.strftime("%Y-%m-%d %H:%M:%S WITA")}

## 3. Metode Akuisisi
* **Metode:** Web Scraping menggunakan Python (`requests` dan `BeautifulSoup4`).
* **Halaman Target:** Daftar URL artikel/publikasi yang diekstrak dari `{SITEMAP_URL}` (mengambil {len(hasil_data)} record halaman).
* **Selector HTML & XML Semantik:**
  * ID Postingan (`post_id`): segmen ID unik pada elemen `<loc>`
  * Judul artikel (`judul`): tag `<h1>`
  * Kategori topik (`kategori`): tag `<a rel="category tag">` atau `<span class="cat-links">`
  * Tanggal pembaruan (`tanggal_pembaruan`): tag `<lastmod>` pada sitemap XML
  * Ringkasan artikel (`ringkasan`): tag `<meta name="description">` atau 200 karakter pertama dari `<div class="entry-content">`

## 4. Batasan Etika
* **Hasil Pemeriksaan `robots.txt`:** Diperiksa secara terprogram menggunakan `urllib.robotparser.RobotFileParser` pada `{ROBOTS_URL}`. Hasil `can_fetch()` menunjukkan akses ke halaman artikel publik diizinkan (`True`), sedangkan jalur `/wp-admin/` dilarang (`Disallow`).
* **Lisensi:** {LISENSI_DATA}.
* **Jeda Antar-Request:** Diterapkan jeda sopan selama **{JEDA_DETIK} detik** (`time.sleep({JEDA_DETIK})`) dan batas `timeout=10` detik pada setiap permintaan HTTP.
* **Data yang Sengaja Tidak Diambil:** Halaman administrator (`/wp-admin/`), file gambar mentah beresolusi tinggi (`.jpg`, `.png`, `.webp`), teks artikel lengkap, serta data pribadi pengguna tidak diambil.

## 5. Penjelasan Kolom Dataset (`{path_file_data}`)
* `post_id`: Nomor identifikasi unik postingan artikel pada situs Museum Nasional (string).
* `judul`: Judul lengkap artikel, pameran, atau koleksi budaya (string).
* `kategori`: Klasifikasi topik atau kategori publikasi artikel (string).
* `tanggal_pembaruan`: Tanggal pembaruan terakhir artikel dalam format `YYYY-MM-DD` (string).
* `ringkasan`: Intisari atau deskripsi singkat dari isi artikel (string).

## 6. Cara Menjalankan Ulang Notebook
1. Instal pustaka Python yang diperlukan: `pip install requests beautifulsoup4 lxml pandas`
2. Buka berkas `notebooks/akuisisi_{SUMBER_SLUG}.ipynb` di Jupyter Notebook atau Google Colab.
3. Pastikan variabel identitas (`NAMA_MAHASISWA`, `NIM`, `EMAIL_KAMPUS`) pada bagian awal notebook sudah terisi.
4. Jalankan seluruh sel dari awal hingga akhir melalui menu **Runtime -> Restart session and run all**.
"""

with open("README.md", "w", encoding="utf-8") as f_readme:
    f_readme.write(readme_teks)

print("Semua berkas dan README.md berhasil dibuat dengan sukses!")
