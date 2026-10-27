# SIKOM E-Learning
Media Pembelajaran Berbasis Website — Mata Pelajaran Sistem Komputer
Studi Kasus: SMA Negeri 1 Pematangsiantar

Dibangun dengan **PHP native + MySQL**, siap dijalankan di **XAMPP**.

---

## 1. Fitur

**Guru — CRUD penuh di setiap menu (Create, Read, Update, Delete)**
- Login & kelola profil **(termasuk unggah foto profil — bebas dimensi, hanya dibatasi format JPG/PNG/WEBP & maksimal 2MB)**
- **Data Siswa**: tambah akun, **edit data (nama/NIS/kelas/kontak)**, **reset kata sandi**, hapus, dan **export ke CSV/Excel**
- **Materi**: unggah, **edit judul/deskripsi/ganti file**, hapus — tampil dengan **thumbnail asli** (bukan sekadar ikon)
- **Jadwal Absensi**: **guru yang menjadwalkan sesi kehadiran** (tanggal + keterangan), membuka/menutup sesi kapan saja, memverifikasi (menyetujui/menolak) kehadiran per siswa, **export rekap ke CSV/Excel**
- **Tugas**: buat tugas (tersimpan sebagai **draft**), **edit tugas**, **Bagikan/Tarik ke Draft**, hapus, menilai tugas siswa dengan pratinjau **thumbnail file**, **export nilai ke CSV/Excel**
- **Kuis**: buat kuis (tersimpan sebagai **draft**), **edit judul/durasi**, kelola soal (tambah/**edit**/hapus), **Bagikan/Tarik ke Draft** (tidak bisa dibagikan tanpa soal), lihat rekap hasil, **export nilai ke CSV/Excel**
- **Rekomendasi Buku**: unggah, **edit judul/penulis/deskripsi/ganti file**, sampul otomatis dari thumbnail file (atau unggah sampul manual), hapus

**Siswa**
- Login & kelola profil **(unggah foto profil bebas dimensi, hanya dibatasi format JPG/PNG/WEBP & maksimal 2MB)**
- Melihat & mengunduh Materi (PDF/DOC/PPT/Video) — dengan **thumbnail asli** dari file (bukan ikon statis)
- **Mengisi Absensi sesuai jadwal yang sudah dibuka guru** (tidak bisa asal pilih tanggal sendiri) — dapat diubah selama belum diverifikasi guru
- Mengunggah, mengubah, dan menghapus Tugas Harian **— hanya tugas yang sudah "Dibagikan" guru yang tampil**
- Mengerjakan Kuis interaktif dengan timer otomatis & melihat hasil/pembahasan **— hanya kuis yang sudah "Dibagikan" guru yang tampil**
- Melihat & mengunduh Rekomendasi Buku

**Thumbnail File Otomatis**
- Setiap file yang diunggah (materi, tugas, buku) menampilkan **thumbnail asli**, bukan sekadar ikon:
  gambar tampil langsung, **PDF menampilkan halaman pertamanya** (dirender di browser),
  video menampilkan **cuplikan frame** otomatis. Tipe file lain (DOC/PPT/dll) memakai ikon bertema warna yang rapi.
- Nama pengguna di seluruh tabel/daftar (Data Siswa, verifikasi absensi, penilaian tugas, hasil kuis)
  kini disertai **foto profil** (atau inisial nama jika belum punya foto).

**Jadwal Absensi oleh Guru**
- Guru membuat sesi absensi baru (tanggal + keterangan opsional) — begitu dibuat, sesi langsung **terbuka**.
- Siswa hanya bisa mengisi kehadiran untuk sesi yang **sedang dibuka**; tidak bisa mengisi tanggal sembarangan sendiri.
- Guru dapat **menutup** sesi kapan saja agar siswa tidak bisa mengisi/mengubah lagi, atau **membuka kembali** bila perlu.
- Guru memverifikasi (setuju/tolak) kehadiran tiap siswa per sesi dari halaman **Lihat & Verifikasi**.

**Sistem Draft & Bagikan (Tugas dan Kuis)**
- Tugas dan Kuis yang baru dibuat guru **otomatis berstatus Draft** dan tidak
  langsung terlihat siswa, sehingga guru bisa menyusun soal/instruksi dengan
  tenang tanpa khawatir siswa membuka tugas yang belum selesai disiapkan.
- Setelah siap, guru menekan tombol **"Bagikan"** agar tugas/kuis langsung
  tampil di halaman siswa.
- Guru juga bisa menekan **"Tarik ke Draft"** kapan saja untuk menyembunyikan
  kembali tugas/kuis dari siswa (misalnya untuk revisi).
- Kuis khusus tidak bisa dibagikan jika belum memiliki soal sama sekali.

**Tampilan & interaksi**
- Modal popup untuk form Edit (tidak berpindah halaman, terasa seperti aplikasi modern)
- Animasi halus: fade-in konten saat halaman dimuat, efek hover terangkat pada kartu,
  efek tombol, transisi sidebar, dan highlight jawaban kuis
- **Desain sepenuhnya responsif** untuk ponsel/Android: sidebar menjadi menu geser (hamburger)
  dengan overlay gelap, tabel dapat digeser mendatar, kartu & formulir otomatis menyusun ulang
  kolom mengikuti lebar layar
- Halaman login menampilkan **foto sekolah** dengan efek zoom halus (Ken Burns) di latar
- Menghormati preferensi pengguna yang menonaktifkan animasi (`prefers-reduced-motion`)

---

## 2. Instalasi di XAMPP

1. **Salin folder** `sikom-elearning` ke dalam folder `htdocs` XAMPP Anda, contoh:
   - Windows: `C:\xampp\htdocs\sikom-elearning`
   - macOS/Linux: `/Applications/XAMPP/htdocs/sikom-elearning`

2. **Jalankan XAMPP Control Panel**, aktifkan modul **Apache** dan **MySQL**.

3. **Buat database**:
   - Buka `http://localhost/phpmyadmin`
   - Klik tab **Import**, pilih file `database.sql` dari folder proyek, lalu klik **Go**.
   - (Alternatif: buat database baru bernama `sikom_elearning`, lalu tempel isi `database.sql` ke tab SQL.)

4. **Cek konfigurasi koneksi** di `config/db.php` — secara default sudah sesuai
   pengaturan standar XAMPP (`host: localhost`, `user: root`, `password: kosong`).
   Sesuaikan jika instalasi MySQL Anda berbeda.

   > **Sudah pernah install sebelum fitur Bagikan/Draft ada?** Jalankan
   > `migrasi_bagikan.sql` sekali lewat tab SQL di phpMyAdmin untuk menambahkan
   > kolom status ke tabel `tugas` dan `kuis`.
   >
   > **Sudah pernah install sebelum fitur Jadwal Absensi ada?** Jalankan juga
   > `migrasi_jadwal_absensi.sql` sekali lewat tab SQL di phpMyAdmin — data
   > absensi lama akan otomatis dipindahkan menjadi sesi terjadwal.
   >
   > Instalasi baru tidak perlu kedua migrasi ini karena strukturnya sudah
   > otomatis ada di `database.sql`.

5. **Buat akun Guru pertama — akun ASLI, bukan demo**:
   - Buka `http://localhost/sikom-elearning/daftar_akun_guru.php`
   - Isi nama, username, dan kata sandi **sesuai keinginan Anda sendiri**.
   - Halaman ini otomatis terkunci setelah akun guru pertama berhasil dibuat
     (mencegah orang lain membuat akun guru tambahan lewat browser).

6. **Buat akun Siswa** (juga akun asli, tanpa data demo):
   - Login sebagai Guru menggunakan akun yang baru dibuat di langkah 5.
   - Buka menu **Data Siswa**, isi form **Tambah Akun Siswa** (username, nama,
     NIS, kelas, kata sandi) sesuai data siswa sekolah Anda.

7. **Buka aplikasi**: `http://localhost/sikom-elearning/`
   Anda akan diarahkan otomatis ke halaman login.

8. **(Opsional) Tambahkan foto sekolah di halaman login**:
   - Simpan foto gedung/lingkungan sekolah Anda dengan nama **`sekolah.jpg`**
   - Letakkan di folder: `assets/img/sekolah.jpg`
   - Foto akan otomatis tampil sebagai latar halaman login dengan efek zoom
     halus. Jika file belum ada, halaman login tetap tampil normal dengan
     latar gradien gelap (tidak error).

> **Sekadar ingin coba-coba dulu dengan data contoh?** Tersedia juga
> `setup_akun_demo.php` yang membuat 1 akun Guru + 2 akun Siswa contoh
> (lihat bagian 8). Ini sepenuhnya opsional, bukan langkah wajib instalasi —
> Anda bisa langsung pakai langkah 5–6 di atas tanpa menyentuh file ini sama sekali.

---

## 3. Struktur Folder

```
sikom-elearning/
├── database.sql                    # Skema database (import ke phpMyAdmin)
├── migrasi_bagikan.sql              # Migrasi kolom status Draft/Bagikan (instalasi lama)
├── migrasi_jadwal_absensi.sql       # Migrasi absensi ke sistem terjadwal (instalasi lama)
├── config/db.php                    # Konfigurasi koneksi database
├── includes/                        # Komponen bersama (header, sidebar, fungsi, auth)
├── assets/css/style.css             # Desain visual aplikasi (termasuk responsif mobile)
├── assets/js/script.js              # Interaksi (timer kuis, modal edit, thumbnail file, dll)
├── assets/img/sekolah.jpg           # (Tambahkan sendiri) foto sekolah untuk halaman login
├── uploads/                         # Tempat penyimpanan file materi/tugas/buku/foto profil
├── login.php / logout.php / index.php
├── daftar_akun_guru.php             # Pendaftaran akun Guru pertama (akun ASLI)
├── setup_akun_demo.php              # (Opsional) Pembuat akun uji coba/demo
├── siswa/                           # Seluruh halaman untuk peran Siswa
└── guru/                            # Seluruh halaman untuk peran Guru
```

---

## 4. Menambah Akun Guru Kedua (jika lebih dari 1 guru pengampu)

`daftar_akun_guru.php` sengaja hanya bisa dipakai **satu kali** demi keamanan
(mencegah sembarang orang membuat akun guru lewat browser kapan saja). Untuk
menambah guru kedua dan seterusnya:

1. Buat file sementara di folder utama proyek, misalnya `buat_guru_baru.php`:

   ```php
   <?php
   require 'config/db.php';
   $hash = password_hash('kata_sandi_baru_anda', PASSWORD_BCRYPT);
   $pdo->prepare('INSERT INTO users (username, password, role, nama) VALUES (?,?,"guru",?)')
       ->execute(['username_guru_baru', $hash, 'Nama Guru Baru']);
   echo 'Akun guru baru berhasil dibuat.';
   ```

2. Buka file tersebut sekali lewat browser:
   `http://localhost/sikom-elearning/buat_guru_baru.php`

3. **Hapus file itu** setelah selesai dipakai, agar tidak disalahgunakan orang lain.

Akun Siswa **tidak perlu** cara manual seperti ini — cukup lewat menu
**Data Siswa** di panel Guru yang sudah tersedia langsung di antarmuka.

---

## 5. Catatan Keamanan

- Password disimpan ter-enkripsi menggunakan `password_hash()` (bcrypt), bukan teks polos.
- Folder `uploads/` diproteksi dengan `.htaccess` agar file yang diunggah tidak bisa dieksekusi sebagai skrip.
- Semua query database menggunakan *prepared statements* (PDO) untuk mencegah SQL Injection.
- `daftar_akun_guru.php` otomatis menonaktifkan diri setelah dipakai sekali.
- Untuk penggunaan produksi (bukan hanya demo skripsi), disarankan menambahkan
  HTTPS, pembatasan ukuran upload di `php.ini`, dan backup database berkala.
- Sebaiknya hapus `setup_akun_demo.php` dari server jika tidak lagi dipakai.

---

## 6. Kesesuaian dengan Rancangan Proposal

Struktur menu (Login → Dashboard → Materi/Absensi/Tugas/Kuis/Buku/Profil → Logout),
Use Case Diagram, dan Activity Diagram pada proposal skripsi *"Pengembangan Media
Pembelajaran Berbasis Website pada Mata Pelajaran Sistem Komputer Studi Kasus
SMA Negeri 1 Pematangsiantar"* menjadi acuan langsung pembuatan aplikasi ini.

---

## 7. Ringkasan Cepat: Masuk Tanpa Data Demo

| Langkah | Aksi |
|---|---|
| 1 | Import `database.sql` (tabel masih kosong, tidak ada akun apa pun) |
| 2 | Buka `daftar_akun_guru.php` → buat akun Guru dengan username/password Anda sendiri |
| 3 | Login sebagai Guru → menu **Data Siswa** → tambahkan akun tiap siswa |
| 4 | Selesai — seluruh akun adalah data asli, tidak ada satu pun akun demo dipakai |

---

## 8. (Opsional) Akun Demo untuk Uji Coba Cepat

Jika hanya ingin mencoba tampilan aplikasi tanpa mengisi data asli:

- Buka `http://localhost/sikom-elearning/setup_akun_demo.php`
- Klik tombol **Buat Akun Demo**

| Peran | Username | Kata Sandi |
|-------|----------|------------|
| Guru  | `guru01` | `guru123`  |
| Siswa | `X1-01`  | `siswa123` |
| Siswa | `X1-02`  | `siswa123` |

Setelah selesai uji coba, hapus file `setup_akun_demo.php` dan akun-akun demo
tersebut (lewat menu Data Siswa untuk siswa, atau phpMyAdmin untuk guru) sebelum
dipakai secara nyata di sekolah.
#   S i s k o m S i a n t a r  
 #   S i s k o m S i a n t a r  
 