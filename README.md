# Ahmad Sanusi Open API — REST API Data Islami Indonesia

[![FastAPI](https://img.shields.io/badge/FastAPI-0.135.2-059669?style=flat-square&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![Python](https://img.shields.io/badge/Python-3.12%2B-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![Database](https://img.shields.io/badge/MariaDB%20%2F%20MySQL-8.0%2B-003545?style=flat-square&logo=mariadb&logoColor=white)](https://mariadb.org/)
[![API Docs](https://img.shields.io/badge/Swagger-Docs-10b981?style=flat-square&logo=swagger&logoColor=white)](https://api.ahmadsanusi.com/docs)

**Ahmad Sanusi Open API** adalah layanan **REST API Islami gratis** untuk developer aplikasi Muslim di Indonesia. Menyediakan data terstruktur untuk **Al-Qur'an 30 Juz**, **Hadits (10 Kitab)**, **Jadwal Sholat Kemenag RI & Arah Kiblat**, **Doa & Dzikir**, **Kitab Kuning**, **Fatwa DSN-MUI**, **E-Code Halal**, **Direktori Pesantren**, serta **Kalkulator Zakat & Waris (Faraidh)**.

- **Portal & Demo**: [https://api.ahmadsanusi.com](https://api.ahmadsanusi.com)
- **Dokumentasi Swagger**: [https://api.ahmadsanusi.com/docs](https://api.ahmadsanusi.com/docs)
- **ReDoc**: [https://api.ahmadsanusi.com/redoc](https://api.ahmadsanusi.com/redoc)
- **Demo Kalkulator Zakat**: [https://api.ahmadsanusi.com/kalkulator-zakat](https://api.ahmadsanusi.com/kalkulator-zakat)
- **Demo Kalkulator Waris**: [https://api.ahmadsanusi.com/kalkulator-waris](https://api.ahmadsanusi.com/kalkulator-waris)

---

## Daftar Isi

- [Fitur & Modul API](#fitur--modul-api)
- [Autentikasi & Rate Limit](#autentikasi--rate-limit)
- [Quick Start](#quick-start)
- [Referensi Endpoint](#referensi-endpoint)
  - [Al-Qur'an (`/v1/quran`)](#1-al-quran-v1quran)
  - [Hadits (`/v1/hadits`)](#2-hadits-v1hadits)
  - [Jadwal Sholat & Kiblat (`/v1/sholat`)](#3-jadwal-sholat--kiblat-v1sholat)
  - [Doa & Dzikir (`/v1/doa`)](#4-doa--dzikir-v1doa)
  - [Kitab Kuning (`/v1/kitab`)](#5-kitab-kuning-v1kitab)
  - [Fatwa DSN-MUI (`/v1/fatwa`)](#6-fatwa-dsn-mui-v1fatwa)
  - [E-Code Halal (`/v1/ecode`)](#7-e-code-halal-v1ecode)
  - [Direktori Pesantren (`/v1/pesantren`)](#8-direktori-pesantren-v1pesantren)
  - [Kalkulator Zakat (`/v1/zakat`) — Publik](#9-kalkulator-zakat-v1zakat--publik)
  - [Kalkulator Waris / Faraidh (`/v1/waris`) — Publik](#10-kalkulator-waris--faraidh-v1waris--publik)
- [Menjalankan Secara Lokal (Development)](#menjalankan-secara-lokal-development)
- [Pengujian (Testing)](#pengujian-testing)
- [Dukungan & Kontak](#dukungan--kontak)

---

## Fitur & Modul API

| Modul | Prefix | Data | Auth |
| :--- | :--- | :--- | :--- |
| **Al-Qur'an & Tafsir** | `/v1/quran` | 114 Surah, 6.236 Ayat, Terjemahan, Tafsir, Asbabun Nuzul, Tema | `X-API-Key` |
| **Hadits** | `/v1/hadits` | 60.000+ Hadits dari 10 Kitab + Terjemahan Indonesia | `X-API-Key` |
| **Jadwal Sholat & Kiblat** | `/v1/sholat` | 551 Kota/Kabupaten (Kemenag RI) + GPS & Arah Kiblat | `X-API-Key` |
| **Doa & Dzikir** | `/v1/doa` | 298 Doa & Dzikir (5 Kategori) + Arab, Latin, Terjemah, Fawaid | `X-API-Key` |
| **Kitab Kuning** | `/v1/kitab` | 21 Kitab Klasik Pesantren + Bab & Pencarian | `X-API-Key` |
| **Fatwa DSN-MUI** | `/v1/fatwa` | 166 Fatwa Ekonomi Syariah No. 1–166 (2000–2026) | `X-API-Key` |
| **E-Code Halal** | `/v1/ecode` | 561 Kode Bahan Tambahan Pangan (Halal, Meragukan, Haram) | `X-API-Key` |
| **Direktori Pesantren** | `/v1/pesantren` | 27.722 Pondok Pesantren seluruh Indonesia | `X-API-Key` |
| **Kalkulator Zakat** | `/v1/zakat` | 13 Jenis Zakat (NU Care / Mazhab Syafi'i) | **Publik** |
| **Kalkulator Waris** | `/v1/waris` | Tirkah, Hijab, Furudh, Ashabah, Aul, Radd, Gharrawain | **Publik** |

---

## Autentikasi & Rate Limit

Endpoint data utama membutuhkan header `X-API-Key`. Daftar gratis di [https://api.ahmadsanusi.com/register](https://api.ahmadsanusi.com/register) atau via API `POST /v1/auth/register` untuk langsung mendapatkan API Key.

| Tier | Kuota Harian | Keterangan |
| :--- | :--- | :--- |
| **Free** | `300` requests / hari | Gratis untuk proyek personal & belajar |
| **Pro** | `10.000` requests / hari | Untuk aplikasi produksi dengan traffic lebih tinggi |
| **Admin** | Unlimited | Akses penuh |

> **Catatan:** Endpoint **Kalkulator Zakat** (`/v1/zakat/*`) dan **Kalkulator Waris** (`/v1/waris/*`) bersifat **publik** (tanpa `X-API-Key`) dengan pembatasan rate limit berbasis IP.

---

## Quick Start

### cURL

```bash
curl -X GET "https://api.ahmadsanusi.com/v1/quran/suras/1" \
  -H "X-API-Key: ask_xxxxxxxxxxxxxxxx"
```

### JavaScript (`fetch`)

```javascript
const res = await fetch("https://api.ahmadsanusi.com/v1/sholat/73.71", {
  headers: { "X-API-Key": "ask_xxxxxxxxxxxxxxxx" },
});
const { data } = await res.json();
console.log(data.waktu);
```

### Python (`requests`)

```python
import requests

res = requests.get(
    "https://api.ahmadsanusi.com/v1/hadits/shahih_bukhari/1",
    headers={"X-API-Key": "ask_xxxxxxxxxxxxxxxx"},
)
print(res.json()["data"])
```

Semua respons mengikuti format JSON standar:

```json
{
  "status": "success",
  "data": { ... }
}
```

---

## Referensi Endpoint

### 1. Al-Qur'an (`/v1/quran`)
- `GET /v1/quran/suras` — Daftar 114 surah
- `GET /v1/quran/suras/{sura_id}` — Detail surah & ayat
- `GET /v1/quran/daily` — Ayat harian (deterministik per hari)
- `GET /v1/quran/random` — Ayat acak
- `GET /v1/quran/search?q=` — Pencarian ayat & terjemahan

### 2. Hadits (`/v1/hadits`)
- `GET /v1/hadits` — Daftar 10 kitab hadits + jumlah hadits
- `GET /v1/hadits/daily` — Hadits harian
- `GET /v1/hadits/search?q=&kitab=&page=&limit=` — Full-text search terjemahan (min 3 karakter)
- `GET /v1/hadits/{kitab}?page=&limit=` — Daftar hadits per kitab
- `GET /v1/hadits/{kitab}/{nomor}` — Detail satu hadits

### 3. Jadwal Sholat & Kiblat (`/v1/sholat`)
- `GET /v1/sholat/wilayah/provinsi` — Daftar provinsi + koordinat + zona waktu
- `GET /v1/sholat/wilayah/search?q=&limit=` — Cari wilayah (min 2 karakter)
- `GET /v1/sholat/koordinat?lat=&lng=` — Jadwal sholat dari koordinat GPS (timezone otomatis)
- `GET /v1/sholat/{kode}?tanggal=YYYY-MM-DD` — Jadwal sholat berdasarkan kode wilayah
- `GET /v1/sholat/kiblat/koordinat?lat=&lng=&elv=` — Arah kiblat & jarak ke Ka'bah dari GPS
- `GET /v1/sholat/kiblat/{kode}` — Arah kiblat berdasarkan kode wilayah

### 4. Doa & Dzikir (`/v1/doa`)
- `GET /v1/doa/kategori` — 5 kategori (`doa-harian`, `dzikir-pagi`, `dzikir-petang`, `dzikir-setelah-shalat`, `doa-pilihan`)
- `GET /v1/doa/kategori/{slug}?page=&limit=` — Daftar doa per kategori
- `GET /v1/doa/search?q=` — Cari judul atau terjemahan doa
- `GET /v1/doa/{doa_id}` — Detail doa, Arab, latin, terjemahan, dan fawaid

### 5. Kitab Kuning (`/v1/kitab`)
- `GET /v1/kitab` — Daftar 21 kitab klasik (`?kategori=`, `?q=`)
- `GET /v1/kitab/kategori` — Daftar kategori kitab
- `GET /v1/kitab/{slug}` — Detail kitab dan daftar bab
- `GET /v1/kitab/{slug}/bab/{nomor}` — Konten satu bab
- `GET /v1/kitab/{slug}/search?q=` — Pencarian teks di dalam kitab

### 6. Fatwa DSN-MUI (`/v1/fatwa`)
- `GET /v1/fatwa?page=&limit=&tahun=&q=` — Daftar fatwa DSN-MUI No. 1–166
- `GET /v1/fatwa/kategori` — 15 kategori fatwa
- `GET /v1/fatwa/kategori/{slug}` — Fatwa per kategori
- `GET /v1/fatwa/tahun` — Daftar tahun penetapan
- `GET /v1/fatwa/search?q=` — Cari judul, isi, atau referensi
- `GET /v1/fatwa/{nomor}` — Detail fatwa berdasarkan nomor (1–166)

### 7. E-Code Halal (`/v1/ecode`)
- `GET /v1/ecode/summary` — Ringkasan statistik status halal
- `GET /v1/ecode/search?q=` — Cari kode E-Code atau nama bahan
- `GET /v1/ecode?status=&page=&limit=` — Daftar E-Code (`halal`, `doubtful`, `haram`)
- `GET /v1/ecode/{code}` — Detail E-Code (mis. `E471`)

### 8. Direktori Pesantren (`/v1/pesantren`)
- `GET /v1/pesantren/provinsi` — Daftar provinsi
- `GET /v1/pesantren/provinsi/{provinsi_id}/kabupaten` — Daftar kab/kota dalam provinsi
- `GET /v1/pesantren/provinsi/{provinsi_id}` — Pesantren per provinsi
- `GET /v1/pesantren/kabupaten/{kab_kota_id}` — Pesantren per kab/kota
- `GET /v1/pesantren/search?q=` — Cari nama pesantren atau pengasuh
- `GET /v1/pesantren/statistik/provinsi` — Statistik jumlah pesantren per provinsi

### 9. Kalkulator Zakat (`/v1/zakat`) — Publik
- `GET /v1/zakat/info` — Nisab emas/perak, harga default, dan daftar 13 jenis kalkulator
- `GET /v1/zakat/jenis` — Daftar 13 slug kalkulator zakat
- `POST /v1/zakat/hitung/{jenis}` — Hitung zakat (`mal`, `profesi`, `emas-perak-perhiasan`, `perdagangan`, `saham`, `peternakan`, `pertambangan`, `properti`, `pendapatan-jasa`, `pertanian`, `perusahaan`, `tambak`, `fitrah`)

### 10. Kalkulator Waris / Faraidh (`/v1/waris`) — Publik
- `GET /v1/waris/info` — Daftar kelompok ahli waris & batas wasiat `1/3`
- `POST /v1/waris/hitung` — Hitung *tirkah* bersih dan pembagian waris (*hijab*, *furudh*, *ashabah*, *aul*, *radd*, *gharrawain*)

---

## Menjalankan Secara Lokal (Development)

### 1. Clone & Siapkan Virtual Environment

```bash
git clone https://gitlab.com/asanusi007/portal-open-api-islam.git
cd portal-open-api-islam
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### 2. Konfigurasi `.env`

Salin `.env.example` menjadi `.env` lalu isi kredensial MariaDB/MySQL dan `SECRET_KEY`:

```bash
cp .env.example .env
```

> **Catatan:** Jangan mengatur `APP_VERSION` di `.env` karena otomatis diisi timestamp boot server untuk cache-busting aset statis.

### 3. Jalankan Server Development

```bash
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

Akses melalui browser:
- Portal Web: `http://localhost:8000`
- Swagger UI: `http://localhost:8000/docs`
- Health Check: `http://localhost:8000/v1/health`

---

## Pengujian (Testing)

Jalankan End-to-End unit test untuk seluruh 13 kategori Kalkulator Zakat:

```bash
venv/bin/python -m unittest tests/test_zakat_e2e.py -v
```

---

## Dukungan & Kontak

- **Website**: [https://ahmadsanusi.com](https://ahmadsanusi.com)
- **Email**: [asanusi007@gmail.com](mailto:asanusi007@gmail.com)
- **Donasi Server**: [https://api.ahmadsanusi.com/#donasi](https://api.ahmadsanusi.com/#donasi)
