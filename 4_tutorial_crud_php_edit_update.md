# Tutorial CRUD PHP & MySQLi Dengan Bootstrap : Edit Dan Update Data Ke Database

## Pendahuluan

Halo teman-teman semuanya, pada kesempatan kali ini kita akan melanjutkan artikel dari seri CRUD PHP & MySQLi Dengan Bootstrap. Dan pada artikel kali ini kita semua akan belajar bagaimana cara mengedit dan mengupdate data ke dalam database.

Jika sebelumnya kita sudah banyak membahas tentang seri ini, mulai dari membuat koneksi database, memasukkan data atau input data hingga menampilkannya ke layar atau web browser.

Pada kesempatan kali ini kita mencoba membuat edit dan update data. Jika teman-teman belum membaca artikel sebelumnya maka teman-teman harus membacanya dari part 1 atau dari awal.

## Langkah 1: Membuat File edit-siswa.php

Buatlah sebuah file baru di dalam folder/project kita yang bernama **sekolah**, buat file dengan nama **edit-siswa.php**.

### Kode Lengkap edit-siswa.php

Kemudian masukkan kode berikut ini:

```php
<?php
include('koneksi.php');
$id = $_GET['id'];
$query = "SELECT * FROM tbl_siswa WHERE id_siswa = $id LIMIT 1";
$result = mysqli_query($connection, $query);
$row = mysqli_fetch_array($result);
?>
<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css">
    <title>Edit Siswa</title>
</head>
<body>
    <div class="container" style="margin-top: 80px">
        <div class="row">
            <div class="col-md-8 offset-md-2">
                <div class="card">
                    <div class="card-header">
                        EDIT SISWA
                    </div>
                    <div class="card-body">
                        <form action="update-siswa.php" method="POST">
                            <div class="form-group">
                                <label>NISN</label>
                                <input type="text" name="nisn" value="<?php echo $row['nisn'] ?>" placeholder="Masukkan NISN Siswa" class="form-control">
                                <input type="hidden" name="id_siswa" value="<?php echo $row['id_siswa'] ?>">
                            </div>
                            <div class="form-group">
                                <label>Nama Lengkap</label>
                                <input type="text" name="nama_lengkap" value="<?php echo $row['nama_lengkap'] ?>" placeholder="Masukkan Nama Siswa" class="form-control">
                            </div>
                            <div class="form-group">
                                <label>Alamat</label>
                                <textarea class="form-control" name="alamat" placeholder="Masukkan Alamat Siswa" rows="4"><?php echo $row['alamat'] ?></textarea>
                            </div>
                            <button type="submit" class="btn btn-success">UPDATE</button>
                            <button type="reset" class="btn btn-warning">RESET</button>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script src="https://code.jquery.com/jquery-3.4.1.slim.min.js"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/js/bootstrap.min.js"></script>
</body>
</html>
```

## Penjelasan Kode edit-siswa.php

Mari kita bahas kode di atas mulai dari bagian PHP di awal:

### 1. Mengambil Data Berdasarkan ID

```php
<?php
include('koneksi.php');
$id = $_GET['id'];
$query = "SELECT * FROM tbl_siswa WHERE id_siswa = $id LIMIT 1";
$result = mysqli_query($connection, $query);
$row = mysqli_fetch_array($result);
?>
```

**Penjelasan:**
- **`include('koneksi.php')`** - Menyertakan file koneksi database
- **`$id = $_GET['id']`** - Mengambil parameter ID dari URL (misalnya: `edit-siswa.php?id=1`)
- **`SELECT * FROM tbl_siswa WHERE id_siswa = $id LIMIT 1`** - Query untuk mencari data siswa berdasarkan ID
- **`LIMIT 1`** - Membatasi hasil query hanya 1 record
- **`mysqli_fetch_array($result)`** - Mengambil hasil query dalam bentuk array

### 2. Cara Kerja Parameter ID

Ketika kita klik tombol **EDIT** di halaman `index.php`, maka URL yang dihasilkan kurang lebih seperti ini:
```
http://localhost/sekolah/edit-siswa.php?id=1
```

Parameter `?id=1` inilah yang ditangkap oleh `$_GET['id']` untuk mencari data siswa dengan ID = 1.

### 3. Form dengan Data Ter-populasi

```html
<form action="update-siswa.php" method="POST">
    <div class="form-group">
        <label>NISN</label>
        <input type="text" name="nisn" value="<?php echo $row['nisn'] ?>" placeholder="Masukkan NISN Siswa" class="form-control">
        <input type="hidden" name="id_siswa" value="<?php echo $row['id_siswa'] ?>">
    </div>
    <!-- Form lainnya -->
</form>
```

**Penjelasan:**
- **`action="update-siswa.php"`** - Form akan dikirim ke file `update-siswa.php`
- **`value="<?php echo $row['nisn'] ?>"`** - Input field sudah terisi dengan data dari database
- **`<input type="hidden" name="id_siswa">`** - Field tersembunyi untuk menyimpan ID siswa

### 4. Perbedaan dengan Form Tambah

| Form Tambah | Form Edit |
|-------------|-----------|
| Field kosong | Field sudah terisi data |
| Tidak ada field hidden ID | Ada field hidden untuk ID |
| Action ke `simpan-siswa.php` | Action ke `update-siswa.php` |
| Button: SIMPAN | Button: UPDATE |

## Langkah 2: Membuat File update-siswa.php

Sekarang kita harus membuat file yang bernama **update-siswa.php** di dalam project sekolah kita.

### Kode Lengkap update-siswa.php

Masukkan kode berikut ini ke dalam file **update-siswa.php**:

```php
<?php
//include koneksi database
include('koneksi.php');

//get data dari form
$id_siswa = $_POST['id_siswa'];
$nisn = $_POST['nisn'];
$nama_lengkap = $_POST['nama_lengkap'];
$alamat = $_POST['alamat'];

//query update data ke dalam database berdasarkan ID
$query = "UPDATE tbl_siswa SET nisn = '$nisn', nama_lengkap = '$nama_lengkap', alamat = '$alamat' WHERE id_siswa = '$id_siswa'";

//kondisi pengecekan apakah data berhasil diupdate atau tidak
if($connection->query($query)) {
    //redirect ke halaman index.php
    header("location: index.php");
} else {
    //pesan error gagal update data
    echo "Data Gagal Diupdate!";
}
?>
```

## Penjelasan Kode update-siswa.php

### 1. Mengambil Data dari Form

```php
//get data dari form
$id_siswa = $_POST['id_siswa'];
$nisn = $_POST['nisn'];
$nama_lengkap = $_POST['nama_lengkap'];
$alamat = $_POST['alamat'];
```

**Penjelasan:**
- Kode di atas adalah deklarasi variabel yang mengambil data dari form menggunakan method POST
- **`$id_siswa`** - Mengambil ID siswa dari field hidden
- **`$nisn`**, **`$nama_lengkap`**, **`$alamat`** - Mengambil data yang sudah diedit dari form

### 2. Query UPDATE

```php
//query update data ke dalam database berdasarkan ID
$query = "UPDATE tbl_siswa SET nisn = '$nisn', nama_lengkap = '$nama_lengkap', alamat = '$alamat' WHERE id_siswa = '$id_siswa'";
```

**Penjelasan:**
- **`UPDATE tbl_siswa SET`** - Perintah SQL untuk mengupdate tabel siswa
- **`nisn = '$nisn', nama_lengkap = '$nama_lengkap', alamat = '$alamat'`** - Field yang akan diupdate dengan nilai baru
- **`WHERE id_siswa = '$id_siswa'`** - Kondisi untuk mengupdate data berdasarkan ID tertentu

### 3. Struktur Query UPDATE

```sql
UPDATE nama_tabel 
SET kolom1 = 'nilai1', kolom2 = 'nilai2', kolom3 = 'nilai3' 
WHERE kondisi;
```

**Penting:** Selalu gunakan `WHERE` dalam query UPDATE untuk menghindari update semua data!

### 4. Kondisi Pengecekan

```php
//kondisi pengecekan apakah data berhasil diupdate atau tidak
if($connection->query($query)) {
    //redirect ke halaman index.php
    header("location: index.php");
} else {
    //pesan error gagal update data
    echo "Data Gagal Diupdate!";
}
```

**Penjelasan:**
- Jika query berhasil dijalankan (`TRUE`), user akan diarahkan ke `index.php`
- Jika query gagal (`FALSE`), akan menampilkan pesan error "Data Gagal Diupdate!"

## Alur Kerja Edit dan Update

1. **User klik tombol EDIT** di `index.php`
2. **Browser membuka** `edit-siswa.php?id=X`
3. **System mengambil data** siswa berdasarkan ID
4. **Form ditampilkan** dengan data yang sudah ter-populasi
5. **User mengubah data** dan klik UPDATE
6. **Data dikirim** ke `update-siswa.php`
7. **System mengupdate** data di database
8. **User dialihkan** kembali ke `index.php`

## Struktur File Saat Ini

```
sekolah/
├── koneksi.php
├── tambah-siswa.php
├── simpan-siswa.php
├── index.php
├── edit-siswa.php        ← Baru dibuat
├── update-siswa.php      ← Baru dibuat
└── hapus-siswa.php       (akan dibuat di tutorial selanjutnya)
```

## Perbedaan INSERT vs UPDATE

| Operasi | Query | Fungsi |
|---------|-------|---------|
| **INSERT** | `INSERT INTO tbl_siswa (nisn, nama_lengkap, alamat) VALUES ('nilai1', 'nilai2', 'nilai3')` | Menambah data baru |
| **UPDATE** | `UPDATE tbl_siswa SET nisn='nilai1', nama_lengkap='nilai2', alamat='nilai3' WHERE id_siswa='X'` | Mengubah data yang sudah ada |

## Tips Keamanan

1. **Validasi Input** - Selalu validasi data yang diterima dari form
2. **Escape String** - Gunakan `mysqli_real_escape_string()` untuk mencegah SQL Injection
3. **Prepared Statement** - Untuk keamanan yang lebih baik, gunakan prepared statement

## Langkah Selanjutnya

Sampai di sini dulu pembahasan tentang edit dan update data ke dalam database. Di artikel selanjutnya kita akan membahas tentang **menghapus data dari database**.

---

*Tutorial ini merupakan bagian keempat dari seri tutorial CRUD PHP & MySQLi dengan Bootstrap. Pastikan fitur edit dan update sudah berfungsi dengan baik sebelum melanjutkan ke tutorial berikutnya tentang menghapus data.*