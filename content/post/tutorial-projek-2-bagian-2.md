---
title: "Tutorial SIDAS dengan Codeiniter #2 : Pengenalan Codeigniter untuk Pemula"
date: 2022-03-25T21:14:19+08:00
categories: ["Website"]
tags: ["Tutorial Project - 2", "Website", "PHP", "Codeigniter4"]
cover: "/img/codeigniter.svg"
draft: false
---

Sebelum mulai belajar Codeigniter 4 lebih, kita harus meyiapkan alat yang dibutuhkan untuk coding Codeigniter 4.

Apa Saja itu?

# Persiapan Sebelum Belajar CI 4
Prasyarat belajar Codeigniter 4..

* Memahami basic bahasa pemrograman PHP. Silahkan, [ikuti tutorial basic pemrograman PHP](*coming soon!*) jika kamu belum menguasainya.
* Untuk bisa belajar Codeigniter dengan lancar setidaknya kamu sudah paham konsep pemrograman berorientasikan objek (OOP) dengan PHP.
* Memahami sintaks dasar SQL

Nah, setelah prasyarat ini terpenuhi. Selanjutnya silahkan siapkan alat-alatnya untuk mulai belajar.

Berikut ini beberapa peralatan yang harus kamu siapkan di komputermu:

* Teks Editor
* Web Browser
* Web Server: PHP, MySQL, Phpmyadmin
*  Composer
* File Project Codeigniter

Mari kita siapkan satu-per-satu.

## 1. Teks Editor
Teks editor akan kita gunakan untuk menulis kode. Kamu bebas menggunakan teks editor apa saja untuk coding CI.

Saya merekomendasikan menggunakan [VS Code](*coming soon!*), karena mudah digunakan dan punya banyak fitur.


## 2. Web Browser
Web browser akan kita gunakan untuk melihat hasil dari aplikasi. Kamu juga bebas menggunakan web browser apapun, asalkan masih mendukung teknologi web modern zaman sekarang.

Rekomendasi, gunakan Google Chrome atau Firefox.

## 3. Web Server
Codeigniter merupakan framework PHP, karena itu ia pasti membutuhkan web server. Berikut ini requirement server untuk Codeigniter 4:

* PHP Versi 7.2+
* MySQL Versi 5.1+
* Phpmyadmin

Jika kamu sudah menginstal XAMPP, maka ketiga aplikasi server ini sudah terpenuhi. Tapi jika kamu pengguna Linux, maka ini bisa diinstal satu-per-satu.

Setelah menginstal webserver, kita harus mengaktifkan beberapa ekstension yang dibutuhkan untuk pengembangan CI 4.

Apa saja itu?

* `php-json` ekstension untuk bekerja dengan JSON
* `php-mysqlnd` native driver untuk MySQL
* `php-xml` ekstension untuk bekerja dengan XML
* `php-intl` ekstensi untuk membuat aplikasi multibahasa
* `libcurl` (opsional), jika ingin [pakai Curl](*coming soon!*).

Silahkan install semuanya dengan perintah (linux):
```bash
sudo apt install php-json php-mysqlnd php-xml php-intl libcurl
```
Untuk pengguna Windows dan XAMPP. Silahkan buka XAMPP Control Panel, lalu pada bagian apache klik **Config->PHP (php.ini)**.

Setelah itu, cari di bagian extension dan hapus ; yang ada di depan nama extension untuk mengaktifkannya.

![sidas1](https://drive.google.com/uc?expand&id=12RuwjqLsmSaYiXXzXFBTq-c2RmrTro0t)

## 4. Composer
Composer adalah program berbasis command line (CLI) untuk menajemen proyek PHP. Tugas dari composer adalah melakukan instalasi paket, membuat proyek baru, menjalankan script, dan lain-lain.

Silahkan install Composer dengan perintah berikut:
```bash
apt install composer
```
Jika kamu ingin belajar tentang composer lebih lanjut, silahkan baca:

* [Cara Menggunakan Composer untuk Manajemen Proyek PHP](*coming soon!*)


## 5. File Project Codeigniter
File project Codeigniter dapat di-download di website resmi Codeigniter. Nanti kita akan mendapatkan file berupa ZIP. File inilah yang akan kita gunakan untuk mulai membuat proyek Codeigniter.

File project ini juga dapat kita download dengan composer.

Silahkan ikuti:

### Install CI 4 dengan Composer
```bash
composer create-project codeigniter4/appstarter sidas -vvv
```
Tungulah sampai prosesnya selesai.

Ada beberapa argumen yang kita berikan pada perintah ini:

* `create-project` adalah perintah untuk membuat proyek baru dengan composer
* `codeigniter4/appstarter` adalah file CI yang akan di-download
* `sidas` adalah nama proyek yang akan kita buat
* `-vvv` berfungsi untuk melihat proses install lebih detail.

Setelah prosesnya selesai, kita akan mendapatkan folder baru dengan nama `sidas`.

buka folder sidas dengan teks editor VS Code (terminal windows juga bisa asal didalam folder project tapi akan lebih mudah jg mmenggunakan terminal vs code).

Setelah itu buka terminal dengan menekan <kbd>Ctrl</kbd> + <kbd>`</kbd> dan jalankan perintah:
```bash
composer install -vvv
```
Perintah ini akan menginstal semua library yang dibutuhkan CI 4.

Setelah selesai, coba ketik perintah:
```bash
php spark serve
```
Perintah ini akan menjalankan server CI 4 pada port `8080`.

Coba buka web browser dan arahkan ke alamat `http://localhost:8080`, maka hasilnya:

![ci4_1](https://drive.google.com/uc?expand&id=1nikaBHEYcWhDZ-4FnT0T1s_WkJ5TsKVB)

Selamat. 👏👏👏

CI 4 sudah berhasil diinstal.

Selanjutnya kita tinggal mulai coding.

### Install CI 4 dengan Cara Manual
Nah, buat kamu yang ingin menginstal CI4 dengan cara manual, tanpa harus melalui Composer, bisa ikuti cara ini.

Langkah-langkah yang harus dilakukan:

1. Download Codeigniter;
2. Ekstrak File ZIP Codeigniter ke htdocs.

Silahkan buka [website Codeigniter](https://codeigniter.com/download) untuk mendownload.

<blockquote><b>Note</b>: versi CI4 yang digunakan pada tutorial ini, yakni 4.1.9.</blockquote>

Kita akan mendapatkan sebuah file zip 📦 `framework-4.x.x.zip`, ekstrak file tersebut ke dalam `c:\xampp\htdocs` (XAMPP) atau `/var/www/html` (di Linux).

Setelah itu, ubah nama `framework-4.x.xx` menjadi `sidas` (nama project kita).

Sekarang coba buka web browser dan buka alamat: `http://localhost/sidas/public/`.

Jiak hasilnya kosong atau blank, maka kita harus melakukan install library yang dibutuhkan.

Silahkan buka folder ci-news dengan Visual Studio Code, lalu buka terminal dan ketik perintah berikut.
```bash
composer install -vvv
```
Perintah ini akan menginstal semua library yang dibutuhkan CI 4.

Setelah itu, ubah kepemilikan dari folder writable dengan perintah berikut ini:
```bash
sudo chown -Rv www-data writable/
```
<blockquote>Note: ini khusus di Linux</blockquote>

Setelah selesai, coba buka kembali http://localhost/ci-news/public/, maka hasilnya:

![ci4_1](https://drive.google.com/uc?expand&id=1nikaBHEYcWhDZ-4FnT0T1s_WkJ5TsKVB)

Selamat. 👏👏👏

CI 4 sudah berhasil diinstal.

Selanjutnya kita tinggal mulai coding.

# Biar Enak, Hidupkan Mode Debugging
CI4 menyediakan fitur debugging yang cukup bagus. Ini sama seperti profiler pada CI3.

Secara default, fitur ini belum aktif. Jika ada error pada aplikasi, maka ia akan menampilkan pesan Whoops! seperti ini:

![ci4_1](https://drive.google.com/uc?expand&id=1xfCiw0Xvc3C7TpNimlTiwgtXme-ElsJi)

Kita tidak akan bisa tahu tempat masalahnya jika aplikasi cuma menampilkan ini. Cocoknya ini dipakai pada aplikasi _production_.

Nah, untuk mengaktifkan mode debugging, kita harus mengubah environment variabel `CI_ENVIRONMENT` menjadi `development`.

Silahkan buka file `env`, kemudian cari variabel `CI_ENVIRONMENT` dan ubahlah nilainya menjadi `development`.

![ci4_development](https://drive.google.com/uc?expand&id=1mjuxLDTpxuKqIHHv1bcNNLmPwsTjWIfq)

Setelah itu, ubah nama file `env` menjadi `.env` (tinggal tambah titik di depan).

![ci4_env](https://drive.google.com/uc?expand&id=1iPDm6lU7Nv2ymXHvQMRecB86zs50BsfI)

Sekarang, coba buat sebuah kesalahan. Misalnya, saya menghapus titik koma pada controller `Home`.

![ci4_env](https://drive.google.com/uc?expand&id=11Q4uoII_B6aGFQ1Z0tKI0ll2YokuXqwO)

Lalu buka kembali aplikasinya.

Maka hasilnya:

![parse error ci4](https://drive.google.com/uc?export&id=13_sczHesLI0Yk3cRs1tWsNt71foBbOJi)

Nah, dengan begini.. kita bisa debug aplikasi dengan lebih mudah. CI akan ngasih tahu, di mana letak error-nya.

Nanti, setelah kita selesai mengembangkan aplikasi. Ubah kembali `CI_ENVIRONTMENT` menjadi `production`.
 
# Troubleshooting..

Saya yakin ada beberapa diantara kamu yang akan mendapatkan masalah saat install Codeigniter 4. Berikut ini beberapa masalah yang sering ditemukan.

## Tidak bisa menjalankan server
Saat menjalankan server dengan perintah php spark serve muncul pesan error seperti ini:
```
PHP Warning:  require(/app/Config/../../vendor/codeigniter4/framework/system/bootstrap.php): failed to open stream: No such file or directory in /home/dian/Playground/ci-playground/ci-news/spark on line 44
```

✅ Solusi:

Lakukan install dengan perintah
```bash
composer install -vvv
```
Argumen `-vvv` berfungsi untuk melihat proses instalasi lebih detail.

Tunggulah sampai prosesnya selesai..

hasilnya akan ada folder `vendor` di proyek kita.

## Tidak bisa melakukan install
Saat melakukan install dengan perintah composer install, muncul pesan seperti ini:
```
codeigniter4/framework v4.0.4 requires ext-intl * -> the requested PHP extension intl is missing from your system
Installation request for codeigniter4/framework ^4 -> satisfiable by codeigniter4/framework[4.0.0, v4.0.1, v4.0.2, v4.0.3, v4.0.4].
```
Ini artinya ekstensi `ext-intl` belum terinstal

✅ Solusi:

Instal ekstensi tersebut dengan perintah (linux):
```
sudo apt install php-intl
```
dan untuk pengguna xampp atau laragon (windows) aktifkan pada configurasi php di control panel.

Setelah itu, coba jalankan lagi composer install

# Apa Selanjutnya?
Pada tahapan ini, kita sudah berhasil membuat proyek baru Codeigniter. Baik itu dengan composer, maupun install secara manual ke htdocs.

Kamu lebih suka cara yang mana?

Kalau saya, lebih suka yang pakai Composer, karena lebih praktis.

Berikutnya, silahkan pelajari tentang:

* ➡️ Tutorial CI 4 #03: Memahami Konsep MVC di CI 4 ())

<blockquote>Untuk tutorial CI lainnya, cek di 📚 <a href=https://kos-it.github.io/tags/codeigniter4>[List Tutorial Codeigntier]</a></blockquote>