# Tutorial CRUD PHP & MySQLi Dengan Bootstrap : Hapus Data Dari Database

## Pendahuluan

Kali ini kita semua akan bersama-sama belajar bagaimana cara membuat delete data dari database.

Ini adalah bagian terakhir dari seri tutorial CRUD (Create, Read, Update, Delete) PHP & MySQLi dengan Bootstrap yang telah kita pelajari bersama.

## Review: Tombol Hapus di index.php

Silahkan teman-teman perhatikan pada file **index.php** yang sudah kita buat sebelumnya. Pada bagian button hapus data, teman-teman akan melihat URL untuk menghapus data berdasarkan parameter ID, kurang lebih seperti ini:

```
http://localhost/sekolah/hapus-siswa.php?id=1
```

Dari link di atas, kita bisa mengetahui bahwa kita harus membuat file dengan nama **hapus-siswa.php** di dalam folder project sekolah kita.

## Cara Kerja Tombol Hapus

Ketika user mengklik tombol **HAPUS** di halaman `index.php`, maka:

1. **Browser membuka URL** `hapus-siswa.php?id=X` (dimana X adalah ID siswa)
2. **File hapus-siswa.php** akan memproses penghapusan
3. **User dialihkan** kembali ke `index.php` jika berhasil

## Langkah 1: Membuat File hapus-siswa.php

Sekarang silahkan buat file dengan nama **hapus-siswa.php** dan masukkan kode di bawah ini:

### Kode Lengkap hapus-siswa.php

```php
<?php
include('koneksi.php');

//get id dari parameter URL
$id = $_GET['id'];

//query untuk menghapus data berdasarkan ID
$query = "DELETE FROM tbl_siswa WHERE id_siswa = '$id'";

//kondisi pengecekan apakah data berhasil dihapus atau tidak
if($connection->query($query)) {
    //redirect ke halaman index.php jika berhasil
    header("location: index.php");
} else {
    //pesan error jika gagal menghapus data
    echo "DATA GAGAL DIHAPUS!";
}
?>
```

## Penjelasan Kode hapus-siswa.php

Mari kita bahas kode di atas step by step:

### 1. Mengambil Parameter ID

```php
include('koneksi.php');
$id = $_GET['id'];
```

**Penjelasan:**
- **`include('koneksi.php')`** - Menyertakan file koneksi database
- **`$id = $_GET['id']`** - Mengambil parameter ID dari URL menggunakan method GET

### 2. Query DELETE

```php
$query = "DELETE FROM tbl_siswa WHERE id_siswa = '$id'";
```

**Penjelasan:**
- **`DELETE FROM tbl_siswa`** - Perintah SQL untuk menghapus data dari tabel siswa
- **`WHERE id_siswa = '$id'`** - Kondisi untuk menghapus data berdasarkan ID tertentu

### 3. Struktur Query DELETE

```sql
DELETE FROM nama_tabel WHERE kondisi;
```

**Penting:** Selalu gunakan `WHERE` dalam query DELETE untuk menghindari penghapusan semua data!

### 4. Kondisi Pengecekan

```php
if($connection->query($query)) {
    header("location: index.php");
} else {
    echo "DATA GAGAL DIHAPUS!";
}
```

**Penjelasan:**
- Jika query berhasil dijalankan (`TRUE`), user akan diarahkan ke `index.php`
- Jika query gagal (`FALSE`), akan menampilkan pesan error "DATA GAGAL DIHAPUS!"

## Cara Kerja Proses Hapus

### Alur Lengkap Penghapusan Data:

1. **User klik tombol HAPUS** di halaman `index.php`
2. **Browser membuka** `hapus-siswa.php?id=X`
3. **System mengambil ID** dari parameter URL
4. **Query DELETE dijalankan** untuk menghapus data berdasarkan ID
5. **Jika berhasil**, user dialihkan kembali ke `index.php`
6. **Data sudah terhapus** dari database dan tidak muncul di tabel

### Contoh URL Penghapusan:

| ID Siswa | URL yang Dibuka |
|----------|----------------|
| 1 | `hapus-siswa.php?id=1` |
| 5 | `hapus-siswa.php?id=5` |
| 10 | `hapus-siswa.php?id=10` |

## Testing Fitur Hapus

Sekarang coba teman-teman menghapus sebuah data dengan cara:

1. **Buka halaman** `http://localhost/sekolah/index.php`
2. **Klik tombol HAPUS** pada salah satu data siswa
3. **Jika berhasil**, Anda akan diarahkan kembali ke `index.php` dengan data sudah terhapus
4. **Jika gagal**, Anda akan mendapatkan pesan error "DATA GAGAL DIHAPUS!"

## Struktur File Lengkap

Setelah tutorial ini selesai, struktur file project kita menjadi:

```
sekolah/
├── koneksi.php           # Koneksi ke database
├── index.php             # Menampilkan data (READ)
├── tambah-siswa.php      # Form tambah data
├── simpan-siswa.php      # Proses tambah data (CREATE)
├── edit-siswa.php        # Form edit data
├── update-siswa.php      # Proses update data (UPDATE)
└── hapus-siswa.php       # Proses hapus data (DELETE)
```

## Rangkuman Operasi CRUD

Berikut adalah rangkuman lengkap operasi CRUD yang telah kita pelajari:

| Operasi | File | Query SQL | Fungsi |
|---------|------|-----------|---------|
| **CREATE** | `simpan-siswa.php` | `INSERT INTO tbl_siswa (...) VALUES (...)` | Menambah data baru |
| **READ** | `index.php` | `SELECT * FROM tbl_siswa` | Menampilkan data |
| **UPDATE** | `update-siswa.php` | `UPDATE tbl_siswa SET ... WHERE id_siswa = ...` | Mengubah data |
| **DELETE** | `hapus-siswa.php` | `DELETE FROM tbl_siswa WHERE id_siswa = ...` | Menghapus data |

## Perbedaan Method GET vs POST

| Method | Penggunaan | Karakteristik |
|--------|------------|---------------|
| **GET** | `edit-siswa.php?id=1`<br>`hapus-siswa.php?id=1` | Parameter terlihat di URL<br>Untuk mengambil/menampilkan data |
| **POST** | Form submit di `tambah-siswa.php`<br>Form submit di `edit-siswa.php` | Data tersembunyi<br>Untuk mengirim data form |

## Tips Keamanan untuk Operasi DELETE

1. **Konfirmasi Penghapusan** - Tambahkan JavaScript confirmation sebelum hapus
2. **Validasi ID** - Pastikan ID valid dan ada di database
3. **Prepared Statement** - Gunakan prepared statement untuk mencegah SQL Injection
4. **Soft Delete** - Pertimbangkan soft delete (menandai data sebagai dihapus) daripada hard delete

### Contoh Konfirmasi JavaScript:

```html
<a href="hapus-siswa.php?id=<?php echo $row['id_siswa'] ?>" 
   class="btn btn-sm btn-danger" 
   onclick="return confirm('Apakah Anda yakin ingin menghapus data ini?')">
   HAPUS
</a>
```

## Troubleshooting Umum

### 1. Data Tidak Terhapus
- **Periksa koneksi database** di file `koneksi.php`
- **Pastikan ID valid** dan ada di database
- **Cek query SQL** apakah sudah benar

### 2. Error "DATA GAGAL DIHAPUS!"
- **Periksa syntax query** DELETE
- **Pastikan nama tabel dan kolom** sudah benar
- **Cek apakah ada constraint** yang mencegah penghapusan

### 3. Halaman Tidak Redirect
- **Pastikan tidak ada output** sebelum `header("location: index.php")`
- **Cek apakah ada error** dalam query

## Kesimpulan

Sampai di sini pembahasan tentang **Cara Mudah Membuat CRUD PHP & MySQLi Dengan Bootstrap 4** telah selesai.

Dalam seri tutorial ini, kita telah mempelajari:

1. **Part 1:** Membuat koneksi database
2. **Part 2:** Input data ke database (CREATE)
3. **Part 3:** Menampilkan data dari database (READ)
4. **Part 4:** Edit dan update data (UPDATE)
5. **Part 5:** Hapus data dari database (DELETE)

### Fitur yang Telah Berhasil Dibuat:

- ✅ **Koneksi Database** dengan MySQLi
- ✅ **Form Tambah Data** dengan Bootstrap
- ✅ **Tampilan Data** dengan DataTables
- ✅ **Form Edit Data** dengan data ter-populasi
- ✅ **Proses Update Data** ke database
- ✅ **Proses Hapus Data** dari database

### Teknologi yang Digunakan:

- **PHP** - Bahasa pemrograman server-side
- **MySQLi** - Extension untuk database MySQL
- **Bootstrap 4** - Framework CSS untuk tampilan
- **DataTables** - Library JavaScript untuk tabel interaktif
- **HTML5** - Markup bahasa untuk struktur halaman

Selamat! Anda telah berhasil membuat aplikasi CRUD lengkap dengan PHP, MySQLi, dan Bootstrap.

---

*Terima kasih telah mengikuti tutorial CRUD PHP & MySQLi dengan Bootstrap. Semoga tutorial ini bermanfaat untuk pengembangan project Anda selanjutnya.*