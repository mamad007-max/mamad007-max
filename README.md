<p align="center">
  <img src="https://img.shields.io/badge/📦-Store_Flux-blueviolet?style=for-the-badge&labelColor=1a1a2e" height="60" alt="Store Flux Logo"/>
</p>

<h1 align="center">Store Flux</h1>
<h3 align="center">🏭 Sistem Klasifikasi Kelayakan Pengiriman Material ke Produksi</h3>

<p align="center">
  <em>Aplikasi web untuk mengelola, memvalidasi, dan mengklasifikasi kelayakan material gudang sebelum dikirim ke lini produksi.</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Laravel-8.x-FF2D20?style=flat-square&logo=laravel&logoColor=white" alt="Laravel 8"/>
  <img src="https://img.shields.io/badge/PHP-≥7.3-777BB4?style=flat-square&logo=php&logoColor=white" alt="PHP"/>
  <img src="https://img.shields.io/badge/MySQL-Database-4479A1?style=flat-square&logo=mysql&logoColor=white" alt="MySQL"/>
  <img src="https://img.shields.io/badge/Tailwind_CSS-Styling-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white" alt="Tailwind CSS"/>
  <img src="https://img.shields.io/badge/DomPDF-Export-E34F26?style=flat-square&logo=adobeacrobatreader&logoColor=white" alt="DomPDF"/>
  <img src="https://img.shields.io/badge/Maatwebsite-Excel-217346?style=flat-square&logo=microsoftexcel&logoColor=white" alt="Excel Export"/>
  <img src="https://img.shields.io/badge/License-MIT-green?style=flat-square" alt="License"/>
</p>

---

## 📋 Daftar Isi

- [Tentang Proyek](#-tentang-proyek)
- [Fitur Utama](#-fitur-utama)
- [Arsitektur Sistem](#-arsitektur-sistem)
- [Tech Stack](#-tech-stack)
- [Persyaratan Sistem](#-persyaratan-sistem)
- [Instalasi](#-instalasi)
- [Konfigurasi](#-konfigurasi)
- [Penggunaan](#-penggunaan)
- [Struktur Database](#-struktur-database)
- [Struktur Proyek](#-struktur-proyek)
- [Akun Default](#-akun-default)
- [Lisensi](#-lisensi)

---

## 🏗 Tentang Proyek

**Store Flux** adalah aplikasi web berbasis Laravel yang dirancang untuk mengelola proses klasifikasi kelayakan material di gudang sebelum dikirimkan ke lini produksi. Sistem ini memfasilitasi alur kerja dua peran utama:

| Peran | Tanggung Jawab |
|:---:|---|
| 🔧 **Admin** | Menginput data material masuk, mengunggah foto kemasan, dan melakukan re-edit material yang dinyatakan tidak layak |
| 🔍 **Supervisor** | Melakukan Quality Control (QC), mengklasifikasi kelayakan material (**Layak** / **Tidak Layak** / **Hold**), dan mengekspor laporan |

Dengan sistem notifikasi real-time, kedua peran dapat saling berkoordinasi secara efisien tanpa miskomunikasi.

---

## ✨ Fitur Utama

<table>
  <tr>
    <td width="50%">

### 🔧 Panel Admin
- ✅ Input data material (nama, batch, diameter, berat)
- ✅ Upload foto kondisi kemasan
- ✅ Pilih kondisi kemasan: **Baik** / **Rusak** / **Terkontaminasi**
- ✅ Re-edit & resubmit material yang ditolak
- ✅ CRUD material lengkap dengan soft delete
- ✅ Notifikasi hasil QC dari Supervisor

</td>
<td width="50%">

### 🔍 Panel Supervisor
- ✅ Dashboard review material masuk
- ✅ Klasifikasi QC: **Layak** / **Tidak Layak** / **Hold**
- ✅ Tambahkan keterangan hasil QC
- ✅ Laporan & filter data material
- ✅ Export laporan ke **Excel** & **PDF**
- ✅ Notifikasi material baru dari Admin

</td>
  </tr>
</table>

### 🔔 Sistem Umum
- 🔐 Autentikasi multi-role (Admin & Supervisor)
- 🔑 Fitur lupa & reset password
- 🔔 Sistem notifikasi in-app (baca / tandai semua dibaca)
- 📱 Responsive design dengan Tailwind CSS
- 🗑️ Soft delete untuk keamanan data

---

## 🏛 Arsitektur Sistem

```
┌─────────────────────────────────────────────────────────────────┐
│                        🌐 BROWSER                               │
│                    (Admin / Supervisor)                          │
└──────────────────────────┬──────────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────────┐
│                      🛡️ MIDDLEWARE                               │
│              Authentication  ·  Role Guard                      │
└──────────────────────────┬──────────────────────────────────────┘
                           │
              ┌────────────┼────────────┐
              ▼            ▼            ▼
     ┌──────────────┐ ┌──────────┐ ┌──────────────────┐
     │ AuthController│ │ Material │ │ SupervisorController│
     │              │ │Controller│ │                  │
     └──────┬───────┘ └────┬─────┘ └────────┬─────────┘
            │              │                │
            ▼              ▼                ▼
     ┌─────────────────────────────────────────────┐
     │              📦 MODELS (Eloquent)            │
     │    User  ·  Material  ·  Notification       │
     └──────────────────────┬──────────────────────┘
                            │
                            ▼
     ┌─────────────────────────────────────────────┐
     │           🗄️ MySQL Database                  │
     │   users · materials · notifications          │
     │   password_resets · failed_jobs              │
     └─────────────────────────────────────────────┘
```

---

## 🛠 Tech Stack

| Kategori | Teknologi |
|:---|:---|
| **Framework** | Laravel 8.x |
| **Bahasa** | PHP ≥ 7.3 |
| **Database** | MySQL / MariaDB |
| **Frontend** | Blade Templates + Tailwind CSS |
| **Export PDF** | barryvdh/laravel-dompdf |
| **Export Excel** | maatwebsite/excel 3.1 |
| **HTTP Client** | Guzzle 7.x |
| **Server Lokal** | Laragon / XAMPP / Valet |

---

## 📌 Persyaratan Sistem

Pastikan sistem Anda memiliki:

- **PHP** ≥ 7.3 beserta ekstensi: `mbstring`, `openssl`, `pdo`, `tokenizer`, `xml`, `ctype`, `json`, `bcmath`, `gd`/`imagick`
- **Composer** ≥ 2.x
- **MySQL** ≥ 5.7 atau **MariaDB** ≥ 10.3
- **Node.js** ≥ 12.x & **NPM** (untuk compile assets)
- **Git**

---

## 🚀 Instalasi

### 1️⃣ Clone Repository

```bash
git clone https://github.com/username/gudang.git
cd gudang
```

### 2️⃣ Install Dependencies

```bash
# PHP dependencies
composer install

# JavaScript dependencies
npm install
```

### 3️⃣ Konfigurasi Environment

```bash
# Salin file environment
cp .env.example .env

# Generate application key
php artisan key:generate
```

### 4️⃣ Setup Database

Buat database baru di MySQL, lalu sesuaikan `.env`:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=gudang
DB_USERNAME=root
DB_PASSWORD=
```

### 5️⃣ Migrasi & Seeder

```bash
# Jalankan migrasi tabel
php artisan migrate

# Seed data default (akun Admin & Supervisor)
php artisan db:seed --class=UsersTableSeeder
```

### 6️⃣ Storage Link

```bash
php artisan storage:link
```

### 7️⃣ Compile Assets & Jalankan Server

```bash
# Compile frontend assets
npm run dev

# Jalankan server development
php artisan serve
```

Aplikasi akan berjalan di: **http://localhost:8000**

---

## ⚙ Konfigurasi

### Variabel Environment Penting

| Variabel | Deskripsi | Default |
|:---|:---|:---|
| `APP_NAME` | Nama aplikasi | `Laravel` |
| `APP_ENV` | Environment | `local` |
| `APP_DEBUG` | Mode debug | `true` |
| `APP_URL` | URL aplikasi | `http://localhost` |
| `DB_DATABASE` | Nama database | `gudang` |
| `FILESYSTEM_DRIVER` | Storage driver | `public` |

---

## 📖 Penggunaan

### 🔧 Alur Kerja Admin

```
Login ➜ Input Material Baru ➜ Upload Foto ➜ Submit
                                                │
                        ┌───────────────────────┘
                        ▼
              Notifikasi ke Supervisor
                        │
                        ▼
        ┌───── Hasil QC dari Supervisor ─────┐
        │                                    │
   ✅ Layak                           ❌ Tidak Layak
   (Selesai)                          (Re-edit & Resubmit)
```

### 🔍 Alur Kerja Supervisor

```
Login ➜ Review Material Masuk ➜ Periksa Data & Foto
                                        │
                    ┌───────────────────┼───────────────────┐
                    ▼                   ▼                   ▼
              ✅ Layak            ⏸️ Hold            ❌ Tidak Layak
                    │                   │                   │
                    └───────────────────┼───────────────────┘
                                        ▼
                              Notifikasi ke Admin
                                        │
                                        ▼
                              Export Laporan (Excel/PDF)
```

---

## 🗄 Struktur Database

### Tabel `materials`

| Kolom | Tipe | Keterangan |
|:---|:---|:---|
| `id` | `bigint` | Primary key |
| `nama_material` | `varchar(150)` | Nama material |
| `no_batch` | `varchar(50)` | Nomor batch (unik) |
| `diameter` | `decimal(8,2)` | Diameter material (mm) |
| `berat` | `decimal(10,3)` | Berat material (kg) |
| `kondisi_kemasan` | `enum` | `Baik` / `Rusak` / `Terkontaminasi` |
| `foto_kemasan` | `varchar(255)` | Path foto kemasan |
| `hasil_qc` | `enum` | `Layak` / `Tidak Layak` / `Hold` |
| `keterangan` | `text` | Catatan QC dari Supervisor |
| `created_by` | `bigint` | FK → users (Admin pembuat) |
| `updated_by` | `bigint` | FK → users (User terakhir update) |
| `created_at` | `timestamp` | Waktu dibuat |
| `updated_at` | `timestamp` | Waktu diupdate |
| `deleted_at` | `timestamp` | Soft delete |

### Tabel `notifications`

| Kolom | Tipe | Keterangan |
|:---|:---|:---|
| `id` | `bigint` | Primary key |
| `user_id` | `bigint` | FK → users (penerima) |
| `type` | `varchar` | Tipe notifikasi |
| `title` | `varchar` | Judul notifikasi |
| `message` | `text` | Isi pesan |
| `material_id` | `bigint` | FK → materials |
| `is_read` | `boolean` | Status sudah dibaca |

---

## 📂 Struktur Proyek

```
gudang/
├── app/
│   ├── Exports/
│   │   └── MaterialsExport.php        # Export data ke Excel
│   ├── Http/
│   │   ├── Controllers/
│   │   │   ├── AuthController.php      # Login, logout, reset password
│   │   │   ├── MaterialController.php  # CRUD material (Admin)
│   │   │   ├── NotificationController.php  # Kelola notifikasi
│   │   │   └── SupervisorController.php    # Dashboard & QC Supervisor
│   │   └── Middleware/                 # Role-based middleware
│   └── Models/
│       ├── Material.php               # Model material + soft delete
│       ├── Notification.php           # Model notifikasi
│       └── User.php                   # Model user multi-role
├── database/
│   ├── migrations/                    # Skema tabel
│   └── seeders/
│       └── UsersTableSeeder.php       # Seed akun default
├── resources/views/
│   ├── admin/
│   │   └── dashboard.blade.php        # Dashboard Admin
│   ├── auth/
│   │   └── login.blade.php            # Halaman login
│   ├── supervisor/
│   │   ├── dashboard.blade.php        # Dashboard Supervisor
│   │   ├── report.blade.php           # Halaman laporan
│   │   └── report_export.blade.php    # Template export PDF
│   ├── layouts/                       # Layout utama
│   ├── notifications/                 # Komponen notifikasi
│   ├── home.blade.php                 # Halaman home
│   └── welcome.blade.php             # Landing page
└── routes/
    └── web.php                        # Definisi routing
```

---

## 🔑 Akun Default

Setelah menjalankan seeder, gunakan akun berikut untuk login:

| Role | Email | Password |
|:---:|:---|:---|
| 🔧 **Admin** | `admin@gudang.local` | `password` |
| 🔍 **Supervisor** | `supervisor@gudang.local` | `password` |

> ⚠️ **Penting:** Segera ganti password default setelah deployment ke environment production!

---

## 📄 Lisensi

Proyek ini dilisensikan di bawah [MIT License](https://opensource.org/licenses/MIT).

---

<p align="center">
  <sub>Dibuat dengan ❤️ menggunakan <a href="https://laravel.com">Laravel</a></sub>
</p>
