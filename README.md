# Simple-WhistleBlowing

Aplikasi sederhana berbasis **Ionic Vue** untuk menampilkan dan memantau data pengaduan mahasiswa melalui **REST API**.

> **Status proyek:** Prototipe antarmuka pembacaan data pengaduan. Pada versi kode yang tersedia, aplikasi berfokus pada **menampilkan daftar pengaduan**, bukan menerima laporan baru atau menyediakan kanal pelaporan anonim yang telah terverifikasi aman.

## 📌 Tentang Proyek

**Simple-WhistleBlowing** merupakan proyek aplikasi pengaduan mahasiswa yang dibangun dengan Vue 3, Ionic Framework, dan TypeScript. Aplikasi mengambil data dari endpoint API, kemudian menampilkan informasi pengaduan dan statusnya dalam tampilan yang responsif.

Proyek ini dapat digunakan sebagai dasar pembelajaran integrasi aplikasi Ionic dengan REST API serta dikembangkan lebih lanjut menjadi sistem pengaduan yang lebih lengkap.

## ✨ Fitur yang Tersedia

- **Daftar pengaduan mahasiswa:** menampilkan judul, nama, NIM, kategori, isi pengaduan, dan status laporan.
- **Pengambilan data otomatis:** memuat data dari API ketika halaman utama dibuka.
- **Penyegaran data:** tombol sinkronisasi untuk mengambil ulang data pengaduan.
- **Indikator pemuatan:** menampilkan pesan ketika data sedang dimuat.
- **Penanganan kesalahan:** menampilkan pemberitahuan apabila pengambilan data dari API gagal.
- **Keadaan data kosong:** menampilkan pesan ketika belum ada pengaduan.
- **Konfigurasi endpoint:** URL API dapat ditentukan melalui variabel lingkungan `VITE_API_URL`.

## 🛠️ Teknologi yang Digunakan

| Teknologi | Kegunaan |
| --- | --- |
| **Ionic Vue** | Komponen antarmuka aplikasi |
| **Vue 3** | Framework antarmuka reaktif |
| **TypeScript** | Pengembangan aplikasi dengan tipe data |
| **Vite** | Development server dan proses build |
| **Vue Router** | Navigasi antarhalaman |
| **Capacitor** | Fondasi integrasi dengan platform perangkat |
| **Fetch API** | Pengambilan data dari REST API |
| **Vitest & Playwright** | Perangkat pengujian yang dikonfigurasi pada proyek |

## 📁 Struktur Proyek

```text
Simple-WhistleBlowing/
├── public/                   # Aset publik
├── src/
│   ├── App.vue               # Komponen utama aplikasi
│   ├── main.ts               # Inisialisasi Vue dan Ionic
│   ├── router/
│   │   └── index.ts          # Konfigurasi rute aplikasi
│   ├── views/
│   │   └── HomePage.vue      # Tampilan daftar pengaduan
│   └── theme/                # Pengaturan tema
├── tests/                    # Berkas pengujian
├── capacitor.config.ts       # Konfigurasi Capacitor
├── ionic.config.json         # Konfigurasi Ionic
├── package.json              # Dependensi dan skrip proyek
├── vite.config.ts            # Konfigurasi Vite
└── README.md                 # Dokumentasi proyek
```

## 🚀 Instalasi dan Menjalankan Aplikasi

### 1. Persyaratan

- **Node.js** dan **npm** terpasang (gunakan versi Node.js yang kompatibel dengan Vite pada proyek).
- Git untuk mengunduh repository.
- REST API pengaduan yang dapat diakses dari perangkat tempat aplikasi dijalankan.

### 2. Clone repository

```bash
git clone https://github.com/Nanang32/Simple-WhistleBlowing.git
cd Simple-WhistleBlowing
```

### 3. Instal dependensi

```bash
npm ci
```

### 4. Konfigurasi API

Buat file `.env` pada direktori utama proyek dan isi dengan:

```env
VITE_API_URL=http://localhost:3000/api/pengaduan
```

Ganti alamat tersebut dengan endpoint API yang digunakan. Jika variabel `VITE_API_URL` tidak diatur, aplikasi menggunakan alamat bawaan:

```text
http://localhost:3000/api/pengaduan
```

**Catatan:** `localhost` mengarah ke perangkat tempat aplikasi berjalan. Jika API berada di komputer lain atau aplikasi dibuka dari perangkat seluler, gunakan alamat server yang dapat dijangkau perangkat tersebut.

### 5. Jalankan aplikasi

```bash
npm run dev
```

Buka alamat lokal yang ditampilkan oleh Vite pada terminal.

### 6. Build produksi

```bash
npm run build
```

Untuk melihat hasil build secara lokal:

```bash
npm run preview
```

## 🔌 Integrasi REST API

Pada implementasi saat ini, halaman utama mengirim permintaan **GET** ke endpoint yang ditentukan oleh `VITE_API_URL`.

Aplikasi mengharapkan respons JSON dengan atribut `success` bernilai `true` serta `data` berupa array. Contoh respons:

```json
{
  "success": true,
  "data": [
    {
      "id": 1,
      "nama": "Mahasiswa Contoh",
      "nim": "123456789",
      "kategori": "Layanan Akademik",
      "judul": "Pengaduan layanan akademik",
      "isi": "Contoh isi pengaduan untuk keperluan pengujian.",
      "status": "Diproses"
    }
  ]
}
```

Contoh di atas merupakan **data ilustratif**, bukan data pengaduan sebenarnya. Field yang digunakan oleh tampilan saat ini adalah `id`, `nama`, `nim`, `kategori`, `judul`, `isi`, dan `status`.

> Repository ini memperlihatkan implementasi **frontend** yang mengambil data dari API eksternal. Backend, database, dan endpoint API perlu disiapkan secara terpisah jika belum tersedia.

## 🧪 Perintah Pengembangan

| Perintah | Fungsi |
| --- | --- |
| `npm run dev` | Menjalankan development server |
| `npm run build` | Membuat build aplikasi |
| `npm run preview` | Menjalankan pratinjau hasil build |
| `npm run lint` | Menjalankan pemeriksaan lint, tipe E2E, dan format |
| `npm run lint:fix` | Menerapkan perbaikan lint dan format otomatis |
| `npm run test:unit` | Menjalankan pengujian unit dengan Vitest |
| `npm run test:e2e` | Menjalankan pengujian E2E dengan Playwright |
| `npm test` | Menjalankan pengujian unit dan E2E |

## 🔐 Catatan Keamanan dan Privasi

Whistleblowing dapat melibatkan informasi sensitif. **Versi aplikasi yang ditinjau saat ini menampilkan nama dan NIM pelapor**, sehingga tidak tepat disebut sebagai sistem pelaporan anonim. Sebelum digunakan untuk pengaduan nyata, perlu dilakukan evaluasi dan pengembangan terkait autentikasi, otorisasi akses, perlindungan identitas, keamanan API, penyimpanan data, serta penggunaan HTTPS.

Jangan menggunakan data pengaduan atau identitas mahasiswa yang sebenarnya pada server pengembangan publik tanpa dasar izin dan kontrol keamanan yang memadai.

## 🗺️ Pengembangan Selanjutnya

Berikut fitur yang **dapat direncanakan** untuk versi berikutnya dan **belum dinyatakan tersedia** pada implementasi yang ditinjau:

- Formulir pengiriman laporan/pengaduan.
- Pengunggahan bukti atau lampiran.
- Panel petugas untuk verifikasi dan tindak lanjut.
- Pelacakan perkembangan laporan oleh pelapor.
- Pengaturan hak akses dan perlindungan data pribadi.
- Mekanisme pelaporan anonim yang dirancang dan diuji secara khusus.

## 👤 Repository

Dikelola melalui akun GitHub [Nanang32](https://github.com/Nanang32).

**Tautan repository:** https://github.com/Nanang32/Simple-WhistleBlowing

---

Dokumentasi ini disusun berdasarkan kode yang tersedia di repository; silakan sesuaikan apabila fitur, API, atau arsitektur aplikasi berubah.
