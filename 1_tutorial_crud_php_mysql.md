# Tutorial CRUD PHP & MySQLi Dengan Bootstrap : Membuat Koneksi Database

## Pendahuluan

Halo teman-teman semuanya, pada kesempatan kali ini kita semua akan belajar tentang bagaimana cara mudah membuat CRUD PHP & MySQLi Dengan Bootstrap secara terstruktur step by step.

Untuk pembahasan pertama di tutorial kali ini kita akan membahas bagaimana cara membuat koneksi antara PHP kita ke Database.

PHP adalah bahasa pemrogramman web yang dinamis dan sangat populer yang biasanya digunakan untuk membangun website secara dinamis. Salah satu cara membuat website secara dinamis adalah dengan cara menyimpan data yang ada ke dalam database dan bisa dimanipulasi sesuai keinginan.

## Langkah 1: Membuat Database

Pertama, kita buat sebuah database baru dulu. Untuk teman-teman yang biasa menggunakan XAMPP, silahkan diaktifkan **apache** dan **mysql**.

Setelah itu silahkan ketikkan `http://localhost/phpmyadmin` dan kita akan melihat tampilan dari PHP MyAdmin. Di situ kita bisa membuat database dan tabel.

Sekarang kita buat database baru dengan nama **db_sekolah**. Setelah database berhasil terbuat, langkah selanjutnya kita akan memulai menyiapkan kode PHP untuk menyambungkannya.

## Langkah 2: Membuat Folder Project

Sekarang kita buat folder baru dengan nama **sekolah** di dalam `C:/XAMPP/htdocs` (jika kalian menggunakan XAMPP). 

Jika folder sudah terbuat, sekarang kita buat file baru di dalam folder tersebut dengan nama `koneksi.php`.

## Langkah 3: Membuat File Koneksi

Dan sekarang kita ketikkan kode berikut ini ke dalam file `koneksi.php`:

```php
<?php
//deklarasi variabel
$db_host = "localhost";
$db_user = "root";
$db_pass = "";
$db_name = "db_sekolah";

$connection = mysqli_connect($db_host, $db_user, $db_pass, $db_name);

if($connection) {
    echo "Koneksi Berhasil!";
} else {
    echo "Koneksi Gagal! : ". mysqli_connect_error();
}
?>
```

## Penjelasan Kode

Dari kode di atas, mari kita bahas bersama dan kita pahami fungsi-fungsinya:

### Variabel Konfigurasi Database

- **`$db_host`** - variabel ini digunakan untuk menyimpan nama host kita, yaitu localhost.
- **`$db_user`** - variabel ini digunakan untuk menyimpan username dari MySQL kita. Jika kita menggunakan XAMPP maka default isinya adalah root.
- **`$db_pass`** - variabel ini digunakan untuk menyimpan password dari MySQL kita. Secara default adalah kosong, maka kita tidak perlu mengisi variabel ini.
- **`$db_name`** - variabel ini digunakan untuk menyimpan nama database yang sudah kita buat sebelumnya.

### Kondisi Pengecekan Koneksi

Kemudian kita perhatikan kode ini juga:

```php
if($connection) {
    echo "Koneksi Berhasil!";
} else {
    echo "Koneksi Gagal! : ". mysqli_connect_error();
}
```

Dari kode di atas, kita membuat sebuah kondisi atau pengecekan apakah variabel `$connection` itu bernilai TRUE atau FALSE atau terpenuhi atau tidak.

## Menguji Koneksi

Maka jika kondisi dari variabel `$connection` itu terpenuhi, maka jika kita akses koneksi kita di web browser dengan cara mengetikkan `http://localhost/sekolah/koneksi.php`, maka akan keluar pesan:

**"Koneksi Berhasil!"**

Akan tetapi jika variabel `$connection` itu tidak terpenuhi atau bernilai FALSE, maka pesan yang akan ditampilkan adalah kurang lebih seperti berikut ini:

**"Koneksi Gagal! : [disertai penjelasan error]"**

## Kesimpulan

Sampai di sini dulu pembahasan tentang Cara Mudah Bagaimana Membuat CRUD PHP & MySQLi Dengan Bootstrap Part 1. Kita akan lanjutkan di artikel selanjutnya.

---

*Tutorial ini merupakan bagian pertama dari seri tutorial CRUD PHP & MySQLi dengan Bootstrap. Pastikan koneksi database sudah berhasil sebelum melanjutkan ke tutorial berikutnya.*