# Tutorial CRUD PHP MySQLi dengan Bootstrap

![PHP](https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-005C84?style=for-the-badge&logo=mysql&logoColor=white)
![Bootstrap](https://img.shields.io/badge/Bootstrap-563D7C?style=for-the-badge&logo=bootstrap&logoColor=white)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)

## 📝 Deskripsi

Repository ini berisi tutorial lengkap cara membuat aplikasi CRUD (Create, Read, Update, Delete) menggunakan PHP MySQLi dengan tampilan Bootstrap yang responsif. Tutorial ini dibuat untuk pemula yang ingin belajar pengembangan web dengan PHP dan database MySQL.

## ✨ Fitur

- ✅ **Create** - Menambah data siswa baru
- ✅ **Read** - Menampilkan daftar siswa dengan fitur pencarian dan paginasi
- ✅ **Update** - Mengedit dan mengupdate data siswa
- ✅ **Delete** - Menghapus data siswa
- 🎨 **Bootstrap 4** - Tampilan yang responsif dan modern
- 📊 **DataTables** - Tabel interaktif dengan pencarian dan sorting
- 🔒 **MySQLi** - Koneksi database yang aman

## 🛠️ Teknologi yang Digunakan

- **PHP** - Bahasa pemrograman server-side
- **MySQLi** - Extension PHP untuk MySQL
- **MySQL** - Sistem manajemen database
- **Bootstrap 4** - Framework CSS
- **DataTables** - Library JavaScript untuk tabel
- **HTML5** - Markup language
- **CSS3** - Styling
- **JavaScript** - Client-side scripting

## 📋 Persyaratan Sistem

- **PHP** >= 7.0
- **MySQL** >= 5.6
- **Web Server** (Apache/Nginx)
- **XAMPP/WAMP/LAMP** (untuk development)

## 🚀 Instalasi

### 1. Clone Repository

```bash
git clone https://github.com/muchamadhatta/Tutorial-CRUD-PHP-MySQLi-Dengan-Bootstrap.git
cd Tutorial-CRUD-PHP-MySQLi-Dengan-Bootstrap
```

### 2. Setup Database

1. Buka **phpMyAdmin** di `http://localhost/phpmyadmin`
2. Buat database baru dengan nama `db_sekolah`
3. Buat tabel `tbl_siswa` dengan struktur berikut:

```sql
CREATE TABLE `tbl_siswa` (
  `id_siswa` int(11) NOT NULL AUTO_INCREMENT,
  `nisn` varchar(50) NOT NULL,
  `nama_lengkap` varchar(200) NOT NULL,
  `alamat` text NOT NULL,
  PRIMARY KEY (`id_siswa`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

### 3. Konfigurasi Database

Edit file `koneksi.php` sesuai dengan konfigurasi database Anda:

```php
<?php
$db_host = "localhost";
$db_user = "root";           // Sesuaikan dengan username MySQL Anda
$db_pass = "";               // Sesuaikan dengan password MySQL Anda
$db_name = "db_sekolah";

$connection = mysqli_connect($db_host, $db_user, $db_pass, $db_name);
?>
```

### 4. Jalankan Aplikasi

1. Pindahkan folder project ke `htdocs` (XAMPP) atau `www` (WAMP)
2. Buka browser dan akses `http://localhost/nama-folder-project`

## 📁 Struktur File

```
Tutorial-CRUD-PHP-MySQLi-Dengan-Bootstrap/
├── koneksi.php              # Konfigurasi koneksi database
├── index.php                # Halaman utama (READ)
├── tambah-siswa.php         # Form tambah data siswa
├── simpan-siswa.php         # Proses simpan data (CREATE)
├── edit-siswa.php           # Form edit data siswa
├── update-siswa.php         # Proses update data (UPDATE)
├── hapus-siswa.php          # Proses hapus data (DELETE)
├── README.md                # Dokumentasi project
├── 1_tutorial_crud_php_mysql.md         # Tutorial Part 1: Koneksi Database
├── 2_tutorial_crud_php_input_data.md    # Tutorial Part 2: Input Data
├── 3_tutorial_crud_php_menampilkan_data.md  # Tutorial Part 3: Menampilkan Data
├── 4_tutorial_crud_php_edit_update.md   # Tutorial Part 4: Edit & Update
└── 5_tutorial_crud_php_hapus_data.md    # Tutorial Part 5: Hapus Data
```

## 📖 Tutorial Step by Step

### Part 1: [Koneksi Database](1_tutorial_crud_php_mysql.md)
- Membuat database dan tabel
- Konfigurasi koneksi PHP ke MySQL
- Testing koneksi database

### Part 2: [Input Data](2_tutorial_crud_php_input_data.md)
- Membuat form input data siswa
- Proses penyimpanan data ke database
- Validasi dan error handling

### Part 3: [Menampilkan Data](3_tutorial_crud_php_menampilkan_data.md)
- Menampilkan data dalam bentuk tabel
- Implementasi DataTables untuk pencarian dan paginasi
- Styling dengan Bootstrap

### Part 4: [Edit dan Update Data](4_tutorial_crud_php_edit_update.md)
- Form edit dengan data ter-populasi
- Proses update data ke database
- Parameter handling dengan GET dan POST

### Part 5: [Hapus Data](5_tutorial_crud_php_hapus_data.md)
- Implementasi fungsi delete
- Konfirmasi penghapusan
- Redirect setelah operasi berhasil

## 🎯 Cara Penggunaan

### 1. Menambah Data Siswa
- Klik tombol **"TAMBAH DATA"** di halaman utama
- Isi form dengan data siswa (NISN, Nama Lengkap, Alamat)
- Klik **"SIMPAN"** untuk menyimpan data

### 2. Melihat Data Siswa
- Data siswa akan ditampilkan di halaman utama
- Gunakan kotak pencarian untuk mencari data tertentu
- Gunakan pagination untuk navigasi data

### 3. Mengedit Data Siswa
- Klik tombol **"EDIT"** pada data yang ingin diubah
- Ubah data sesuai kebutuhan
- Klik **"UPDATE"** untuk menyimpan perubahan

### 4. Menghapus Data Siswa
- Klik tombol **"HAPUS"** pada data yang ingin dihapus
- Data akan langsung terhapus dari database

## 🔧 Kustomisasi

### Mengubah Tema Bootstrap
Ganti CDN Bootstrap di setiap file HTML:
```html
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css">
```

### Menambah Validasi Form
Tambahkan validasi JavaScript atau PHP untuk memastikan data yang diinput valid.

### Mengubah Struktur Database
Sesuaikan field di tabel `tbl_siswa` dan update file PHP yang terkait.

## 🛡️ Keamanan

⚠️ **Peringatan Keamanan**: Kode ini dibuat untuk tujuan pembelajaran. Untuk production, perlu ditambahkan:

- **Prepared Statements** untuk mencegah SQL Injection
- **Input Validation** yang lebih ketat
- **CSRF Protection** untuk form
- **Authentication & Authorization**
- **Password Hashing** jika ada sistem login

## 🤝 Kontribusi

Kontribusi selalu diterima! Jika Anda ingin berkontribusi:

1. Fork repository ini
2. Buat branch fitur baru (`git checkout -b fitur-baru`)
3. Commit perubahan (`git commit -am 'Menambah fitur baru'`)
4. Push ke branch (`git push origin fitur-baru`)
5. Buat Pull Request

## 📄 Lisensi

Project ini menggunakan lisensi MIT. Lihat file [LICENSE](LICENSE) untuk detail lengkap.

## 👨‍💻 Author

**Muchama Dhatta**
- GitHub: [@muchamadhatta](https://github.com/muchamadhatta)

## 🙏 Acknowledgments

- [Bootstrap](https://getbootstrap.com/) untuk framework CSS
- [DataTables](https://datatables.net/) untuk tabel interaktif
- [SantriKoding](https://santrikoding.com/) untuk inspirasi tutorial

## 📞 Support

Jika Anda mengalami masalah atau memiliki pertanyaan:

1. Buka [Issues](https://github.com/muchamadhatta/Tutorial-CRUD-PHP-MySQLi-Dengan-Bootstrap/issues)
2. Buat issue baru dengan deskripsi yang jelas
3. Atau hubungi melalui email

---

⭐ **Jika tutorial ini membantu, jangan lupa beri star!** ⭐
