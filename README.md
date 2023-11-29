![image](https://github.com/Luxcario/Lab8web/assets/116184002/d80ef533-5219-497f-a301-0e0c87d4ac6a)# Lab8web

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

![image](https://github.com/Luxcario/Lab8web/assets/116184002/d67971e1-0fc4-41b6-9c77-2ffabfe66a6b)

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
![image](https://github.com/Luxcario/Lab8web/assets/116184002/1cf57581-568d-4bc4-9b0f-d92e3f86111d)
<hr>

**Membuat file index untuk menampilkan data (Read)**

Buat file baru dengan nama index.php
```
<?php
include ("koneksi.php");

// query untuk menampilkan data
$sql = 'SELECT*FROM data_barang';
$result = mysql_query($conn, $sql);
?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="style.css" rel="stylesheet" type="text/css"> 
    <title>Data Barang</title>
</head>
<body>
    <div class="container">
        <h1>Data Barang</h1>
        <div class="main">
            <table>
                <tr>
                    <th>Gambar</th>
                    <th>Nama Barang</th>
                    <th>Kategori</th>
                    <th>Harga Jual</th>
                    <th>Harga Beli</th>
                    <th>Stok</th>
                    <th>Aksi</th>
                </tr>
                <?php if ($result): ?>
                <?php while ($row = mysql_fetch_array($result)) : ?>
                <tr>
                    <td><img src="gambar/<?=$row['gambar'];?>" alt="<?=$row['nama'];?>"></td>
                    <td><?= $row['nama'];?></td>
                    <td><?= $row['kategori'];?></td>
                    <td><?= $row['harga_beli'];?></td>
                    <td><?= $row['harga_jual'];?></td>
                    <td><?= $row['stok'];?></td>
                    <td><?= $row['id_barang'];?></td>
                </tr>
                <?php endwhile; else:?>
                <tr>
                    <td colspan="7">Belum ada data</td>
                </tr>
                <?php endif;?>
            </table>
        </div>
    </div>
</body>
</html>
```
Untuk melihat hasil gunakan URL : http://localhost/lab8_php_database/index.php/

![image](https://github.com/Luxcario/Lab8web/assets/116184002/61a8ba84-4baa-451c-b313-4fc18e00967c)
<hr>

**Menambah Data (Create)**
Buat file baru dengan nama tambah.php
```
<?php
error_reporting(E_ALL);
include_once 'koneksi.php';

if(isset($_POST['submit'])){
    $nama = $_POST['nama'];
    $kategori = $_POST['kategori'];
    $harga_jual = $_POST['harga_jual'];
    $harga_beli = $_POST['harga_beli'];
    $stok = $_POST['stok'];
    $file_gambar = $_FILES['file_gambar'];
    $gambar = null;
    if($file_gambar['error'] == 0){
        $filename = str_replace('','', $file_gambar['name']);
        $destination = dirname(__FILE__).'/gambar/'.$filename;
        if(move_uploaded_file($file_gambar['tmp_name'],$destination)){
            $gambar = 'gambar/' . $filename;;
        }
    }
    $sql = 'INSERT INTO data_barang(nama, kategori, harga_jual, harga_beli, stok, gambar)';
    $sql .= "VALUE ('{$nama}','{$kategori}','{$harga_jual}','{$harga_beli}','{$stok}','{$gambar}')";
    $result = mysqli_query($conn, $sql);
    header('location : index.php');
}
?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="style.css" rel="stylesheet" type="text/css" />
    <title>Tambah Barang</title>
</head>
<body>
    <div class="container">
        <h1>Tambah Barang</h1>
        <div class="main">
            <form method="post" action="tambah.php" enctype="multipart/form-data">
                <div class="input">
                    <label>Nama Barang</label>
                    <input type="text" name="nama">
                </div>
                <div class="input">
                    <label>Kategori</label>
                    <select name="kategori">
                        <option value="komputer">Komputer</option>
                        <option value="elektronik">Elektronik</option>
                        <option value="hand phone">Hand Phone</option>
                    </select>
                </div>
                <div class="input">
                    <label>Harga Jual</label>
                    <input type="text" name="harga_jual">
                </div>
                <div class="input">
                    <label>Harga Beli</label>
                    <input type="text" name="harga_beli">
                </div>
                <div class="input">
                    <label>Stok</label>
                    <input type="text" name="stok">
                </div>
                <div class="input">
                    <label>Gambar</label>
                    <input type="file" name="file_gambar">
                </div>
                <div class="input">
                    <input type="submit" name="sumbit" value="simpan">
                </div>
            </form>
        </div>
    </div>
</body>
</html>
```
untuk melihat hasil gunakan URL : http://localhost/lab8_php_database/tambah.php/ 

![image](https://github.com/Luxcario/Lab8web/assets/116184002/875cb591-baa5-4aec-8c52-ffb50cf56c5b)
<hr>

**Mengubah Data (Update)**
Buat file baru dengan nama ubah.php
```
<?php
error_reporting(E_ALL);
include_once 'koneksi.php';
if (isset($_POST['submit']))
{
    $id = $_POST['id'];
    $nama = $_POST['nama'];
    $kategori = $_POST['kategori'];
    $harga_jual = $_POST['harga_jual'];
    $harga_beli = $_POST['harga_beli'];
    $stok = $_POST['stok'];
    $file_gambar = $_FILES['file_gambar'];
    $gambar = null;    
    if ($file_gambar['error'] == 0)
    {
        $filename = str_replace(' ', '_', $file_gambar['name']);
        $destination = dirname(__FILE__) . '/gambar/' . $filename;
        if (move_uploaded_file($file_gambar['tmp_name'], $destination))
        {
            $gambar = 'gambar/' . $filename;;
        }
    }
    $sql = 'UPDATE data_barang SET ';
    $sql .= "nama = '{$nama}', kategori = '{$kategori}', ";
    $sql .= "harga_jual = '{$harga_jual}', harga_beli = '{$harga_beli}', stok = '{$stok}' ";
    if (!empty($gambar))
    $sql .= ", gambar = '{$gambar}' ";
    $sql .= "WHERE id_barang = '{$id}'";
    $result = mysqli_query($conn, $sql);
    header('location: index.php');
}

$id = $_GET['id'];
$sql = "SELECT * FROM data_barang WHERE id_barang = '{$id}'";
$result = mysqli_query($conn, $sql);
if (!$result) die('Error: Data tidak tersedia');
$data = mysqli_fetch_array($result);
function is_select($var, $val) {
    if ($var == $val) return 'selected="selected"';
    return false;
}
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="style.css" rel="stylesheet" type="text/css" />
    <title>Ubah Barang</title>
</head>
<body>
    <div class="container">
        <h1>Ubah Barang</h1>
        <div class="main">
            <form method="post" action="ubah.php" enctype="multipart/form-data">
                <div class="input">
                    <label></label>
                    <input type="text" name="nama" value="<?php echo $data['nama'];?>">
                </div>
                <div class="input">
                    <label></label>
                    <select name="kategori">
                        <option <?php echo is_select('Komputer', $data['kategori']);?> value="Komputer">Komputer</option>
                        <option <?php echo is_select('Komputer', $data['kategori']);?> value="Elektronik">Elektronik</option>
                        <option <?php echo is_select('Komputer', $data['kategori']);?> value="Hand Phone">Hand Phone</option>
                    </select>
                </div>
                <div class="input">
                    <label>Harga Jual</label>
                    <input type="text" name="harga_jual" value="<?php echo $data['harga_jual'];?>">
                </div>
                <div class="input">
                    <label>Harga Beli</label>
                    <input type="text" name="harga_beli" value="<?php echo $data['harga_beli'];?>">
                </div>
                <div class="input">
                    <label>Stok</label>
                        <input type="text" name="stok" value="<?php echo $data['stok'];?>">
                </div>
                <div class="input">
                    <label>File Gambar</label>
                    <input type="file" name="file_gambar">
                </div>
                <div class="submit">
                    <input type="hidden" name="id" value="<?php echo $data['id_barang'];?>">
                    <input type="submit" name="submit" value="Simpan" >
            </form>
        </div>
    </div>
</body>
</html>
```

kemudian tambahkan code pada index.php 
![image](https://github.com/Luxcario/Lab8web/assets/116184002/9e1eff6d-42dc-4cab-bc24-4c093253ccf9)

```
<a href="ubah.php?id=<?= $row['id_barang'];?>">Ubah</a>
<a href="?action=hapus&id_barang=<?= $row['id_barang']; ?>" onclick="return confirm('Anda yakin ingin menghapus data ini?')">Hapus</a>  
<a href="tambah.php">Tambah</a>
```

untuk melihat hasil gunakan URL : http://localhost/lab8_php_database/

![image](https://github.com/Luxcario/Lab8web/assets/116184002/2cd7d6a5-f7e9-4dea-9477-199dd4db5239)

