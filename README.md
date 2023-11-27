# Lab8web

<br>

**Praktikum 8: PHP dan Database MySQL**

Instruksi Praktikum
1. Persiapkan text editor misalnya VSCode.
2. Buat folder baru dengan nama lab8_php_database pada docroot webserver 
(htdocs)

![image](https://github.com/Luxcario/Lab8web/assets/116184002/35937eef-03ca-447c-b02a-246bd2deb747)
<br>
3. Ikuti langkah-langkah praktikum yang akan dijelaskan berikutnya. 
<br>

**Persiapan**
Untuk memulai membuat aplikasi CRUD sederhana, yang perlu disiapkan adalah 
database server menggunakan MySQL. Pastikan MySQL Server sudah dapat dijalankan 
melalui XAMPP.

![image](https://github.com/Luxcario/Lab8web/assets/116184002/f8a7ea95-4677-4395-9aa4-a261fe508d75)
<hr>

**Mengakses MySQL Client menggunakan PHP MyAdmin**

Pastikan webserver Apache dan MySQL server sudah dijalankan. Kemudian buka 
melalui browser: http://localhost/phpmyadmin/

![image](https://github.com/Luxcario/Lab8web/assets/116184002/d498c02a-5679-4453-b989-fd4311428be3)
<hr>

**Membuat Database: Studi Kasus Data Barang**

![image](https://github.com/Luxcario/Lab8web/assets/116184002/cb97e6b5-88db-4769-9e4d-f749fb9e1391)
<br>

Membuat Database
```
CREATE DATABASE latihan1;
```
Membuat Table
```
Membuat Tabel
CREATE TABLE data_barang (
 id_barang int(10) auto_increment Primary Key,
 kategori varchar(30),
 nama varchar(30),
 gambar varchar(100),
 harga_beli decimal(10,0),
 harga_jual decimal(10,0),
 stok int(4)
);
```

![image](https://github.com/Luxcario/Lab8web/assets/116184002/b1f38b3c-a0fd-41e9-8f29-f2526bfa4a53)
<hr>

**Menambahkan Data**
```
INSERT INTO data_barang (kategori, nama, gambar, harga_beli, harga_jual, stok)
VALUES ('Elektronik', 'HP Samsung Android', 'hp_samsung.jpg', 2000000, 2400000, 5),
('Elektronik', 'HP Xiaomi Android', 'hp_xiaomi.jpg', 1000000, 1400000, 5),
('Elektronik', 'HP OPPO Android', 'hp_oppo.jpg', 1800000, 2300000, 5);
```

![image](https://github.com/Luxcario/Lab8web/assets/116184002/e4206d06-dfce-41df-bd33-855591fc4c5b)
<hr>

**Membuat Program CRUD**
Buat folder lab8_php_database pada root directory web server ```(d:\xampp\htdocs)```

![image](https://github.com/Luxcario/Lab8web/assets/116184002/6f322c1e-1d6b-4f30-a381-fb4c86782820)

Kemudian untuk mengakses direktory tersebut pada web server dengan mengakses URL: 
http://localhost/lab8_php_database/

![image](https://github.com/Luxcario/Lab8web/assets/116184002/f1301886-916a-4e75-932c-095eceef5572)
<hr>

**Membuat file koneksi database**
Buat file baru dengan nama koneksi.php
```
<?php
$host = "localhost";
$user = "root";
$pass = "";
$db = "latihan1";
$conn = mysqli_connect($host, $user, $pass, $db);
if ($conn == false)
{
 echo "Koneksi ke server gagal.";
 die();
} #else echo "Koneksi berhasil";
?>
```

kemudian untuk mengakses nya gunakan URL : http://localhost/lab8_php_database/koneksi.php/
![image](https://github.com/Luxcario/Lab8web/assets/116184002/b349c1d2-6049-4414-a560-6e31e0176da7)
