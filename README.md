# 🧪 Web Scraping Publikasi Ilmiah: Scopus, Google Scholar, dan SINTA

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Selenium](https://img.shields.io/badge/Library-Selenium-green)
![SerpAPI](https://img.shields.io/badge/API-SerpAPI-orange)

## 👤 Author
**Nur'aini**
* 🎓 **Mahasiswa:** Program Studi Magister Statistika dan Sains Data, IPB University
* 📧 **Email:** Nuraiinii1001@gmail.com
* 🔗 **LinkedIn:** http://www.linkedin.com/in/nuraiinii01
---

## 📌 Deskripsi Proyek
Repositori ini mendokumentasikan proses **web scraping data publikasi ilmiah** menggunakan Jupyter Notebook. Script ini mengintegrasikan tiga sumber data utama:
1.  **Scopus** (via Selenium + Firefox WebDriver)
2.  **Google Scholar** (via SerpAPI `google_scholar_author`)
3.  **SINTA Kemdikbud** (via Requests + BeautifulSoup)

📦 **Output:** Dataset publikasi dalam format **CSV** yang siap digunakan untuk dokumentasi akademik atau *literature review*.

---

## ✨ Fitur Utama

### 1) 🧭 Scraping Scopus (Selenium)
Menggunakan **Selenium** dengan **Firefox (GeckoDriver)** untuk simulasi browser.
* **Otomatisasi:**
    * 🌐 Membuka Scopus & menangani *cookies*.
    * 🔐 Login otomatis menggunakan kredensial tersimpan.
    * 👤 Navigasi menu Author & input nama target.
    * 📄 Ekstraksi tabel publikasi.
* **Output:** `outputs/scopus_data.csv`
* **Kolom:** `Article`, `Title`, `Authors`, `Journal`, `Year/Volume`, `Article URL`.
* **Fitur Debug:** Menyimpan *screenshot* otomatis jika terjadi error (misal: gagal login atau CAPTCHA).

### 2) 🔎 Scraping Google Scholar (SerpAPI)
Menggunakan **SerpAPI** untuk mengatasi blokir anti-bot Google Scholar.
* **Fitur:**
    * 📄 Mengambil 100 artikel per halaman.
    * 🔁 *Pagination* otomatis (0, 100, 200...).
    * 🛠️ Sistem *retry* jika koneksi gagal.
    * 📊 Sorting artikel berdasarkan tahun terbaru.
* **Output:** `outputs/Google Scholar.csv`

### 3) 🏛️ Scraping SINTA (Requests + BeautifulSoup)
Mengambil data langsung dari halaman profil SINTA (`sinta.kemdikbud.go.id`).
* **Data yang Diambil:**
    * 👤 **Profil:** Nama, Afiliasi, Prodi, SINTA Score.
    * 🗂️ **Artikel:** Dari tab Google Scholar, Scopus, dan Garuda.
* **Output:** `outputs/sinta_profile_{id}.csv` & `outputs/sinta_articles_{id}.csv`
* **Keamanan:** Menggunakan rotasi *User-Agent* dan jeda waktu (*delay*) untuk mencegah pemblokiran.

---

## 🗂️ Struktur Repositori

```text
.
├── notebooks/
│   └── Nur'aini_M0501241058_Paralel_1.ipynb
├── outputs/
│   ├── scopus_data.csv
│   ├── Google Scholar.csv
│   ├── sinta_profile_6173018.csv
│   └── sinta_articles_6173018.csv
├── .gitignore
├── requirements.txt
└── README.md
```

---

## ⚙️ Instalasi

### 🟡 Opsi A — Google Colab (Termudah)
1.  Upload notebook ke Google Colab.
2.  Jalankan sel instalasi dependensi di awal notebook.
3.  Pastikan dependensi sistem (`firefox`, `geckodriver`) terinstal via `apt-get` (script sudah tersedia di notebook).

### 🟢 Opsi B — Lokal (Windows/macOS/Linux)

#### 1. Buat Virtual Environment
```bash
# Windows
python -m venv .venv
.venv\Scripts\activate

# macOS/Linux
python3 -m venv .venv
source .venv/bin/activate
```

#### 2. Install Library
```bash
pip install -r requirements.txt
```
*Isi file `requirements.txt` minimal:*
```text
selenium
pandas
requests
beautifulsoup4
google-search-results
```

#### 3. Driver Browser
Pastikan **Mozilla Firefox** dan **GeckoDriver** sudah terinstal dan terdaftar di PATH sistem komputer Anda.

---

## ▶️ Cara Menjalankan

1.  **Buka Jupyter Notebook:**
    ```bash
    jupyter notebook
    ```
2.  **Buka File:** Masuk ke folder `notebooks/` dan buka `Research_Publication_Scraper.ipynb`.
3.  **Eksekusi:** Jalankan sel secara berurutan:
    * 📦 **Import Library**
    * 🧭 **Scopus Section**
    * 🔎 **Google Scholar Section**
    * 🏛️ **SINTA Section**

---

## 🔐 Konfigurasi (Wajib)

Demi keamanan, **JANGAN** tulis email/password langsung di kode. Gunakan *Environment Variables*.

### 1. Kredensial Scopus
Atur variabel lingkungan di terminal/OS Anda:
```bash
# Linux/macOS
export SCOPUS_EMAIL="nur.aiiniinuraini@apps.ipb.ac.id"
export SCOPUS_PASSWORD="password_anda"
```
*(Di Windows gunakan `set` atau edit System Environment Variables)*

### 2. SerpAPI Key
Dapatkan API Key dari [SerpAPI](https://serpapi.com/).
```bash
export SERPAPI_KEY="api_key_anda"
```

### 3. ID Target (Di dalam Notebook)
Sesuaikan variabel berikut pada kode notebook:
* **Google Scholar:** `author_id = "apmXydQAAAAJ"`
* **SINTA:** `author_id = "6173018"`
* **Scopus:** Input nama depan & belakang pada fungsi input Selenium.

---

## 🧯 Troubleshooting

Berikut adalah solusi untuk masalah umum yang sering terjadi saat scraping:

| Modul | Masalah | Solusi Potensial |
| :--- | :--- | :--- |
| **🧭 Scopus** | **Login Gagal / CAPTCHA** | • Ganti koneksi internet (IP berbeda).<br>• Tambah durasi `time.sleep()` pada kode.<br>• Coba login manual sekali di browser.<br>• Pastikan akun memiliki akses langganan institusi. |
| **🧷 Selenium** | **GeckoDriver Not Found** | • Pastikan `geckodriver` terinstal.<br>• Cek apakah path driver sudah benar.<br>• Pastikan versi Firefox kompatibel dengan driver. |
| **🔎 SerpAPI** | **No Result / Kuota Habis** | • Cek sisa kuota di dashboard SerpAPI.<br>• Pastikan `author_id` valid dan benar. |
| **🏛️ SINTA** | **Request Timeout** | • Naikkan parameter `timeout` pada `requests.get`.<br>• Perbesar jeda waktu (*delay*) antar request. |

---

## ✅ Etika & Kepatuhan

1.  **Terms of Service:** Patuhi aturan penggunaan (*Terms of Service*) dan `robots.txt` dari Scopus, Google Scholar, dan SINTA.
2.  **Hak Cipta:** Data yang diambil mungkin memiliki hak cipta. Gunakan hanya untuk keperluan dokumentasi pribadi atau riset akademik.
3.  **Rate Limiting:** Script ini menerapkan *delay* (jeda) antar permintaan untuk menghormati beban server target. Jangan menghilangkan *delay* tersebut.
