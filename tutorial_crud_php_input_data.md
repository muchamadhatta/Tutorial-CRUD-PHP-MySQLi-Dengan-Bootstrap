# Tutorial CRUD PHP & MySQLi Dengan Bootstrap : Input Data Ke Database

## Pendahuluan

Halo teman-teman semuanya, di artikel sebelumnya kita sudah membahas bagaimana cara membuat sebuah koneksi dari PHP ke Database kita.

Pada tutorial kali ini, kita semua akan belajar bagaimana caranya memasukkan data atau input data dari PHP ke database yang sudah kita buat sebelumnya.

Untuk teman-teman yang baru belajar, silahkan dibaca artikel sebelumnya tentang cara membuat koneksi dari PHP ke Database di Part 1.

## Langkah 1: Membuat Tabel Database

Sebelum kita membuat form yang digunakan untuk menyimpan data ke database, langkah pertama kita harus buat sebuah tabel baru terlebih dahulu di dalam database **db_sekolah** yang sudah kita buat di artikel pertama.

Silahkan buka dan klik **db_sekolah**. Dan buatlah tabel baru dengan nama **tbl_siswa**.

### Struktur Tabel tbl_siswa

Berikut adalah struktur kolom yang perlu dibuat:

| Nama Kolom | Tipe Data | Length/Value | Keterangan |
|------------|-----------|--------------|------------|
| `id_siswa` | INT | 11 | PRIMARY KEY, AUTO_INCREMENT |
| `nisn` | VARCHAR | 50 | Nomor Induk Siswa Nasional |
| `nama_lengkap` | VARCHAR | 200 | Nama lengkap siswa |
| `alamat` | TEXT | - | Alamat siswa |

### Penjelasan Kolom:

- **`id_siswa`** - digunakan sebagai PRIMARY KEY dan dijadikan AUTO INCREMENT dengan tipe data INT dan dengan Length/Value 11, dimana kolom ini sebagai perwakilan satu record/satu baris.
- **`nisn`** - kolom ini digunakan untuk menyimpan data NISN dengan tipe data VARCHAR dengan Length/Value 50.
- **`nama_lengkap`** - kolom ini digunakan untuk menyimpan nama lengkap dari siswa dengan tipe data VARCHAR dengan Length/Value 200.
- **`alamat`** - kolom terakhir ini adalah untuk menyimpan alamat dari data siswa, di kolom ini kita menggunakan tipe data TEXT dan kita tidak perlu memberikan isian dari Length/Value.

## Langkah 2: Membuat Form Input Data

Jika sudah berhasil semuanya, kita sekarang lanjut membuat tampilan form yang digunakan untuk menyimpan data siswa ke dalam database.

Silahkan buat file baru dengan nama **tambah-siswa.php** di dalam folder sekolah.

### Struktur Folder:
```
sekolah/
├── koneksi.php
└── tambah-siswa.php
```

Pada kesempatan kali ini, untuk tampilan kita akan menggunakan **Bootstrap 4**, jadi kita tidak perlu membuat CSS lagi dari awal dan proses pembuatan tampilan akan sangat cepat dan terbantu.

Untuk file Bootstrap yang akan kita gunakan adalah online atau mengambil dari CDN. Jika teman-teman ingin mencobanya secara offline, teman-teman bisa mengunduh file bootstrap dan ditaruh di folder project kita.

### Kode tambah-siswa.php

Silahkan copy dan paste kode di bawah ini ke dalam file **tambah-siswa.php** yang sudah kalian buat sebelumnya:

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css">
    <title>Tambah Siswa</title>
</head>
<body>
    <div class="container" style="margin-top: 80px">
        <div class="row">
            <div class="col-md-8 offset-md-2">
                <div class="card">
                    <div class="card-header">
                        TAMBAH SISWA
                    </div>
                    <div class="card-body">
                        <form action="simpan-siswa.php" method="POST">
                            <div class="form-group">
                                <label>NISN</label>
                                <input type="text" name="nisn" placeholder="Masukkan NISN Siswa" class="form-control">
                            </div>
                            <div class="form-group">
                                <label>Nama Lengkap</label>
                                <input type="text" name="nama_lengkap" placeholder="Masukkan Nama Siswa" class="form-control">
                            </div>
                            <div class="form-group">
                                <label>Alamat</label>
                                <textarea class="form-control" name="alamat" placeholder="Masukkan Alamat Siswa" rows="4"></textarea>
                            </div>
                            <button type="submit" class="btn btn-success">SIMPAN</button>
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

### Menjalankan Form

Jika dijalankan dengan mengetikkan `http://localhost/sekolah/tambah-siswa.php`, maka jika berhasil tampilannya akan menampilkan form input data siswa dengan tampilan Bootstrap yang rapi.

### Penting untuk Diperhatikan

Perlu diperhatikan pada baris kode berikut ini:

```html
<form action="simpan-siswa.php" method="POST">
```

Dari kode di atas, form yang sudah kita buat akan mengarah ke file baru yang bernama **simpan-siswa.php**, jadi proses input dari form akan langsung diproses oleh file yang bernama **simpan-siswa.php** dengan menggunakan method POST.

## Langkah 3: Membuat File Pemroses Data

Sekarang kita buat file baru dengan nama **simpan-siswa.php** di dalam folder sekolah, yang mana file ini sejajar dengan file **tambah-siswa.php**.

### Kode simpan-siswa.php

Silahkan masukkan kode berikut ini ke dalam file **simpan-siswa.php**:

```php
<?php
//include koneksi database
include('koneksi.php');

//get data dari form
$nisn = $_POST['nisn'];
$nama_lengkap = $_POST['nama_lengkap'];
$alamat = $_POST['alamat'];

//query insert data ke dalam database
$query = "INSERT INTO tbl_siswa (nisn, nama_lengkap, alamat) VALUES ('$nisn', '$nama_lengkap', '$alamat')";

//kondisi pengecekan apakah data berhasil dimasukkan atau tidak
if($connection->query($query)) {
    //redirect ke halaman index.php
    header("location: index.php");
} else {
    //pesan error gagal insert data
    echo "Data Gagal Disimpan!";
}
?>
```

## Penjelasan Kode simpan-siswa.php

### 1. Mengambil Data dari Form

```php
//get data dari form
$nisn = $_POST['nisn'];
$nama_lengkap = $_POST['nama_lengkap'];
$alamat = $_POST['alamat'];
```

Kode di atas adalah sebuah deklarasi variabel yang mana isinya mengambil dari hasil input Form menggunakan method POST.

### 2. Query Insert Data

```php
//query insert data ke dalam database
$query = "INSERT INTO tbl_siswa (nisn, nama_lengkap, alamat) VALUES ('$nisn', '$nama_lengkap', '$alamat')";
```

Pada kode di atas itu adalah sebuah Query SQL yang digunakan untuk menyimpan data ke dalam database dengan perintah INSERT INTO.

### 3. Kondisi Pengecekan

```php
//kondisi pengecekan apakah data berhasil dimasukkan atau tidak
if($connection->query($query)) {
    //redirect ke halaman index.php
    header("location: index.php");
} else {
    //pesan error gagal insert data
    echo "Data Gagal Disimpan!";
}
```

Kode di atas adalah sebuah kondisi dimana:
- Jika variabel bernilai **TRUE** atau Query berjalan dengan sukses, maka otomatis kita akan diarahkan ke dalam file yang bernama **index.php**.
- Tapi jika kondisi tidak terpenuhi atau bernilai **FALSE**, maka akan mengeluarkan pesan error **"Data Gagal Disimpan!"**.

## Langkah Selanjutnya

Terakhir, karena jika berhasil menyimpan data ke database akan langsung diarahkan ke file yang bernama **index.php**, maka otomatis kita harus membuat file baru dengan nama **index.php** di dalam folder sekolah.

Dan untuk pembahasan **index.php** akan kita bahas pada artikel selanjutnya. Untuk **index.php** ini adalah tahap bagaimana data ditampilkan dari Database ke browser atau aplikasi kita.

## Struktur File Akhir

```
sekolah/
├── koneksi.php
├── tambah-siswa.php
├── simpan-siswa.php
└── index.php (akan dibuat di tutorial selanjutnya)
```

---

*Tutorial ini merupakan bagian kedua dari seri tutorial CRUD PHP & MySQLi dengan Bootstrap. Pastikan semua file sudah dibuat dengan benar sebelum melanjutkan ke tutorial berikutnya tentang menampilkan data.*