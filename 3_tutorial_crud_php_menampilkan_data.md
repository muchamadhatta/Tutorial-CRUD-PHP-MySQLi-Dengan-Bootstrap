# Tutorial CRUD PHP & MySQLi Dengan Bootstrap : Menampilkan Data Dari Database

## Pendahuluan

Selamat datang teman-teman semuanya di artikel lanjutan dari seri membuat CRUD PHP & MySQLi Dengan Bootstrap di **Part 3** yaitu menampilkan data dari database.

Jika di artikel sebelumnya kita sudah membahas tentang bagaimana cara memasukkan data atau input data dari Form ke Database, maka di artikel kali ini kita semua akan belajar bagaimana cara menampilkan data yang sudah berhasil diinputkan ke database.

## Menggunakan DataTables

Pada artikel kali ini kita akan menampilkan data dari database menggunakan Library yang bernama **[DataTables](https://datatables.net/)**. 

### Mengapa menggunakan DataTables?

Dengan DataTables kita tidak harus membuat pencarian dan paginasi data secara manual, semuanya sudah disediakan secara otomatis, termasuk:

- **Pencarian data** otomatis
- **Paginasi** (pembagian halaman)
- **Sorting** (pengurutan data)
- **Responsive design**
- **Customizable** tampilan

## Implementasi File index.php

Di artikel sebelumnya kita sudah membuat file yang bernama **index.php** dan file tersebut masih kosong. Maka di tutorial kali ini kita akan menuliskan beberapa kode di file **index.php** tersebut.

Karena file **index.php** inilah yang bertugas untuk menampilkan data dari database ke layar browser kita.

### Kode Lengkap index.php

Silahkan copy dan paste kode di bawah ini ke dalam file **index.php**:

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css">
    <link rel="stylesheet" href="//cdn.datatables.net/1.10.20/css/jquery.dataTables.min.css">
    <title>Data Siswa</title>
</head>
<body>
    <div class="container" style="margin-top: 80px">
        <div class="row">
            <div class="col-md-12">
                <div class="card">
                    <div class="card-header">
                        DATA SISWA
                    </div>
                    <div class="card-body">
                        <a href="tambah-siswa.php" class="btn btn-md btn-success" style="margin-bottom: 10px">TAMBAH DATA</a>
                        <table class="table table-bordered" id="myTable">
                            <thead>
                                <tr>
                                    <th scope="col">NO.</th>
                                    <th scope="col">NISN</th>
                                    <th scope="col">NAMA LENGKAP</th>
                                    <th scope="col">ALAMAT</th>
                                    <th scope="col">AKSI</th>
                                </tr>
                            </thead>
                            <tbody>
                                <?php
                                include('koneksi.php');
                                $no = 1;
                                $query = mysqli_query($connection,"SELECT * FROM tbl_siswa");
                                while($row = mysqli_fetch_array($query)){
                                ?>
                                <tr>
                                    <td><?php echo $no++ ?></td>
                                    <td><?php echo $row['nisn'] ?></td>
                                    <td><?php echo $row['nama_lengkap'] ?></td>
                                    <td><?php echo $row['alamat'] ?></td>
                                    <td class="text-center">
                                        <a href="edit-siswa.php?id=<?php echo $row['id_siswa'] ?>" class="btn btn-sm btn-primary">EDIT</a>
                                        <a href="hapus-siswa.php?id=<?php echo $row['id_siswa'] ?>" class="btn btn-sm btn-danger">HAPUS</a>
                                    </td>
                                </tr>
                                <?php } ?>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script src="https://code.jquery.com/jquery-3.4.1.slim.min.js"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/js/bootstrap.min.js"></script>
    <script src="//cdn.datatables.net/1.10.20/js/jquery.dataTables.min.js"></script>
    <script>
        $(document).ready( function () {
            $('#myTable').DataTable();
        } );
    </script>
</body>
</html>
```

## Penjelasan Kode

Mari kita bahas kodenya step by step untuk memahami cara kerjanya:

### 1. Library yang Digunakan

```html
<!-- Bootstrap CSS -->
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css">

<!-- DataTables CSS -->
<link rel="stylesheet" href="//cdn.datatables.net/1.10.20/css/jquery.dataTables.min.css">
```

Kita menggunakan dua library utama:
- **Bootstrap 4** untuk styling dan layout
- **DataTables** untuk fungsionalitas tabel yang interaktif

### 2. Struktur Tabel

```html
<table class="table table-bordered" id="myTable">
    <thead>
        <tr>
            <th scope="col">NO.</th>
            <th scope="col">NISN</th>
            <th scope="col">NAMA LENGKAP</th>
            <th scope="col">ALAMAT</th>
            <th scope="col">AKSI</th>
        </tr>
    </thead>
    <tbody>
        <!-- Data akan ditampilkan di sini -->
    </tbody>
</table>
```

Tabel memiliki 5 kolom:
- **NO.** - Nomor urut
- **NISN** - Nomor Induk Siswa Nasional
- **NAMA LENGKAP** - Nama lengkap siswa
- **ALAMAT** - Alamat siswa
- **AKSI** - Tombol Edit dan Hapus

### 3. Menampilkan Data dari Database

```php
<?php
include('koneksi.php');
$no = 1;
$query = mysqli_query($connection,"SELECT * FROM tbl_siswa");
while($row = mysqli_fetch_array($query)){
?>
<tr>
    <td><?php echo $no++ ?></td>
    <td><?php echo $row['nisn'] ?></td>
    <td><?php echo $row['nama_lengkap'] ?></td>
    <td><?php echo $row['alamat'] ?></td>
    <td class="text-center">
        <a href="edit-siswa.php?id=<?php echo $row['id_siswa'] ?>" class="btn btn-sm btn-primary">EDIT</a>
        <a href="hapus-siswa.php?id=<?php echo $row['id_siswa'] ?>" class="btn btn-sm btn-danger">HAPUS</a>
    </td>
</tr>
<?php } ?>
```

**Penjelasan:**
- **`include('koneksi.php')`** - Menyertakan file koneksi database
- **`$no = 1`** - Inisialisasi variabel untuk nomor urut
- **`SELECT * FROM tbl_siswa`** - Query untuk mengambil semua data dari tabel siswa
- **`while($row = mysqli_fetch_array($query))`** - Loop untuk menampilkan setiap baris data
- **`$no++`** - Increment nomor urut otomatis
- **`$row['nama_kolom']`** - Mengambil nilai dari setiap kolom

### 4. Tombol Aksi

```html
<td class="text-center">
    <a href="edit-siswa.php?id=<?php echo $row['id_siswa'] ?>" class="btn btn-sm btn-primary">EDIT</a>
    <a href="hapus-siswa.php?id=<?php echo $row['id_siswa'] ?>" class="btn btn-sm btn-danger">HAPUS</a>
</td>
```

- **Tombol EDIT** - Mengarah ke file `edit-siswa.php` dengan parameter ID siswa
- **Tombol HAPUS** - Mengarah ke file `hapus-siswa.php` dengan parameter ID siswa

### 5. Inisialisasi DataTables

```javascript
<script>
$(document).ready( function () {
    $('#myTable').DataTable();
} );
</script>
```

**Penjelasan:**
- Kode di atas adalah cara DataTables diaplikasikan ke sebuah tabel dengan ID `myTable`
- `$(document).ready()` memastikan DataTables dijalankan setelah halaman selesai dimuat
- `$('#myTable').DataTable()` mengaktifkan fitur DataTables pada tabel dengan ID `myTable`

### 6. Library JavaScript

```html
<script src="https://code.jquery.com/jquery-3.4.1.slim.min.js"></script>
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/js/bootstrap.min.js"></script>
<script src="//cdn.datatables.net/1.10.20/js/jquery.dataTables.min.js"></script>
```

Urutan library JavaScript:
1. **jQuery** - Dependency untuk Bootstrap dan DataTables
2. **Bootstrap JS** - Untuk komponen interaktif Bootstrap
3. **DataTables JS** - Library utama DataTables

## Menjalankan Aplikasi

Jika kalian jalankan dengan mengetikkan di browser `http://localhost/sekolah`, maka tampilannya akan menampilkan:

- **Tabel data siswa** dengan fitur pencarian otomatis
- **Paginasi** untuk navigasi data yang banyak
- **Sorting** pada setiap kolom
- **Tombol "TAMBAH DATA"** untuk menambah siswa baru
- **Tombol "EDIT"** dan **"HAPUS"** di setiap baris data

## Fitur DataTables yang Tersedia

Setelah DataTables diimplementasikan, tabel akan memiliki fitur:

1. **Search Box** - Kotak pencarian otomatis di kanan atas tabel
2. **Show Entries** - Dropdown untuk memilih jumlah data per halaman
3. **Sorting** - Klik header kolom untuk mengurutkan data
4. **Pagination** - Navigasi halaman di bawah tabel
5. **Info** - Informasi jumlah data dan halaman saat ini

## Struktur File Saat Ini

```
sekolah/
├── koneksi.php
├── tambah-siswa.php
├── simpan-siswa.php
├── index.php
├── edit-siswa.php (akan dibuat di tutorial selanjutnya)
└── hapus-siswa.php (akan dibuat di tutorial selanjutnya)
```

## Langkah Selanjutnya

Untuk edit dan sekaligus update data siswa akan kita bahas pada artikel selanjutnya, dimana kita akan membuat:

- **edit-siswa.php** - Form untuk mengubah data siswa
- **hapus-siswa.php** - Proses untuk menghapus data siswa

---

*Tutorial ini merupakan bagian ketiga dari seri tutorial CRUD PHP & MySQLi dengan Bootstrap. Pastikan data sudah berhasil ditampilkan dengan benar sebelum melanjutkan ke tutorial berikutnya tentang edit dan hapus data.*