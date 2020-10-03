---
title: "Tutorial SIMKEP dengan Codeiniter #1 : Pengenalan Codeigniter"
date: 2018-10-19T23:35:00+09:00
categories: ["Website"]
tags: ["Tutorial Project - 1", "Website", "PHP", "Codeigniter"]
cover: "https://drive.google.com//uc?export=view&id=1zKgyxiCm9R2RlIFO8O1cbknZGUN8NrRC"
---

Selamat datang di **KOS-IT** - Making and Developing..

Tutorial ini berisi sedikit pegenalan tentang salah satu frameowrk [PHP](https://kos-it.github.io/tags/php/) yakni [Codeigniter](https://kos-it.github.io/tags/codeigniter/), yang kita gunakan pada projek 1 kita yaitu [Sistem Management Kepanitaan](https://kos-it.github.io/projects/projek-sistem-menejement-kepanitiaan/). tutorial ini lebih ditujakan untuk yang bagi yang belum mengenal apa itu faramework [Codeigniter](https://kos-it.github.io/tags/codeigniter/), bagi kalian yang telah mengenal atau mungkin sudah tidak asing dengan [Codeigniter](https://kos-it.github.io/tags/codeigniter/) dapat langsung melangkahi tutrial ini ke [Tutorial #2](https://kos-it.guthub.io/tutorial-projek-1-bagian-2)

PHP memeliki banyak framework, yang paling populer yakni Laravel dan tentu saja Codeigniter yang kita gunakan pada projek 1 kami..

Oke lanjut..

# Apa itu Framework?
Ngomong-ngomong, apa itu framework?

Framework dalam bahasa indonesia artinya adalah kerangka kerja. Kerangka kerja untuk membuat sesuatu, sehingga [Codeigniter](https://kos-it.github.io/tags/codeigniter/) merupakan sebuah kerangka kerja yang memudahkan kita dalam membuat web dengan [PHP](https://kos-it.github.io/tags/php/). kita dapat merumpamakan [Codeigniter](https://kos-it.github.io/tags/codeigniter) sebuah traktor yang membantu petani membajak sawah akan lebih cepat dan efisien dibanding secara manual dengan cangkul. Dengan menggunakan framework, pembuatan web akan lebih cepat dibandingkan PHP Native. Karena kita tidak perlu membuat semuanya dari nol.

[Codeigniter](https://kos-it.github.io/tags/codeigniter/) sendiri merupakan framework [PHP](https://kos-it.github.io/tags/php/) yang menggunakan pola desain (*design pattern*) MVC(*Model View Controller*). Sampai saat ini Codegniter telah merilis versi 3.1.10 dan untuk versi 4.x masih dalam pengembangan (beta). kalian dapat langsung mengunjungi website resminya di <a href="https://codeigniter.com/" target="_blank"><i>codeingiter.com</i></a>

![Codeigniter](/img/projek1/codeigniter.png)

# Kelebihan Codeigniter

Ada beberapa kelebihan CodeIgniter (CI) dibandingkan dengan Framework PHP lain :

* **Performa cepat** : Codeigniter merupakan framework yang paling cepat dibanding framework yang lain. Karena tidak menggunakan template engine dan ORM yang dapat memperlambat proses.

* **Konfigurasi yang minim** (*nearly zero configuration*) : tentu saja untuk menyesuaikan dengan database dan keleluasaan routing tetap diizinkan melakukan konfigurasi dengan mengubah beberapa file konfigurasi seperti database.php atau autoload.php, namun untuk menggunakan codeigniter dengan setting standard, anda hanya perlu mengubah sedikit saja pada file di folder config.

* **Memiliki banyak komunitas** : Komunitas CI di indonesia cukup ramai, tutorialnya pun mudah dicari.

* **Dokumentasi yang lengkap** : Codeigniter disertai dengan user_guide yang berisi dokumentasi yang lengkap. 

* **Mudah dipelajari pemula** : Bagi pemula, CI sangat mudah dipelajari. Karena CI tidak terlalu bergantung pada tool tambahan seperti composer, ORM, Template Engine, dll.

# Mengenal Struktur Direktori Codeigniter

Inilah Struktur direktori [Codeiginter](https://kos-it.github.io/tags/codeigniter)

![Codeigniter](/img/projek1/downloadci.png)

Tedapat dua direktori penting di dalam CI:  <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg">`application` dan <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg">`system`. Selain itu terdapat juga direktori <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg">`user_guide` dan beberapa folder. Berikut ini penjelasannya:

 1. <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `applicaton` direktori ini merupakan tempat untuk menulis file semua kode aplikasi/web kita.
 2. <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `system` direktori ini berisi kode sistem dari framework [Codeigniter](http://kos-it.github.io/tags/codeigniter). jangan merubah apapun dalam direktori ini. jika kita ingin _meng-upgrade_ atau mnegganti versi [Codeigniter](htpp://kos-it.github.io/tags/codeigniter). kita cukup mengganti/ _me-replace_ direktori ini.
 3. <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `test` berisi file kode untuk unit testing.
 4. <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `user_guide` merupakan direktori berisi file kode dokumentasi [Codeigniter](http://kos-it.github.io/tags/codeigniter). kita dapat mengaksesnya pada halaman awal codeigniter, berisi panduan penggunaan/ dokumentasi. direktori ini dapat kita hapus bila sudah tidak diperlukan.
 5. <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `.editor_config` berisi kode konfigurasi untuk teks editor.
 6. <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `.gitignore` berisi daftar file yang akan diabaikan oleh Git.
 7. <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `.composer.json` file berisi keterangan projek dan keterangan library yang digunakan. File ini dibuthkan oleh komposer
 8. <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `comtributing.md` file yang berisi penjelasan cara berkontribusi di proyek CI. kita bisa menghapus file ini apabila telah jadi.
 9. <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `license.txt` adalah file yang berisi keterangan lisensi dari CI.
 10. <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `readme.rst` sama seperti file <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `contributing.md` file ini berisi penjelasan dan informasi tentang projek CI. kita juga dapat menghapus file ini saat apliasi/web sudah jadi.
 11. <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `index.php` adalh file utama dari CI. file yang dibuka pertama kali saat kita mengakses web.
 
 Selanjutnya kita akan membahas isi dari direktori <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `application` :

  * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `cache` berisi cache dari aplikasi
  * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `config` berisi konfogurasi aplikasi berupa :

    * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `autoload.php` tempat kita mendefinisikan autoload.
    * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `config.php` konfigurasi aplikasi/web.
    * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `constants.php` berisi konstanta.
    * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `database.php` konfigurasi database apikasi/web.
    * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `doctypes.php` berisi definisi untuk _doctype_ HTML.
    * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `foreign_chars.php` berisi karakter dan simbol.
    * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `hooks.php` berisi konfigurasi _hooks_.
    * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `index.html` untuk mencegah direct access.
    * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `memcached.php` berisi konfigurasi untuk memcached.
    * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `migration.php` konfigurasi untuk migrasi.
    * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `mimes.php` berisi defiisi tipe file.
    * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `profiler.php` berisi konfigurasi untuk profiler.
    * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `routers.php` tempat kita menulis route apikasi.
    * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `smileys.php` berisi kode untuk emoji.
    * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `user_agents.php` berisi konfigurasi untuk _user agents_.

  * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `controller` berisi kode untuk _controller_.
  * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `core` berisi code untuk custom core.
  * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `helper` berisi fungsi-fungsi helper.
  * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `hooks` berisi file untuk script _hooks_.
  * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `language` berisi string untuk bahasa, apabila aplikasi/web mendukung multibahasa
  * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `libraries` berisi librari
  * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `logs` berisi log dari aplikasi.
  * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `models` berisi kode untuk model.
  * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `thrid_party` berisi librari dari pihak ketiga.
  * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `views` berisi kode untuk view
  * <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `index.html` file html untuk mencegah direct access.
  
# Cara Instalasi Codeigniter & Konfigurasi Dasar

Langkah langkah yang harus dilakukan yakni :

 1. Download [Codeigniter](https://www.codeigniter.com/download).
 2. Ekstrak CI ke htdocs.

Silahkan kunjungi [Website Codeigniter](https://www.codeigniter.com/download) untuk mendownload

![Codeigniter](/img/projek1/downloadci.png)

Kita akan mendapatkan sebuah file zip <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `Codeigniter-3.x.x.zip`, ekstrak file tersebut ke dalam `C:\xampp\htdocs` (XAMPP) atau `/var/www/html` (Linux)

Setelah itu agar lebih memudahkan ubah nama folder Codeigniter tersebeut menjadi nama projek kita. karna projek kita adalah Sistem Menejement Kepanitiaan maka kita singkat saja menjadi SIMKEP.

Kemudian pada browser kalian silahkan masukkan url: [http://localhost/SIMKEP](http://localhost/SIMKEP)

![Codeigniter](/img/projek1/simkep1.jpg)

Gambar diatas adalah halaman awal dari Codeigniter "_Welocome to Codeigniter_. Jika kalian melihat halaman seperti diatas maka Codeigniter telah berhasil teristall

Selanjutnya, sebagai pengenalan awal. Silahkan buka teks editor kalian. Disini kami menggunakan teks editor VS Code. 

Kemudian cobalah untuk mengubah teks `Welcome to Codeigniter!` menjadi `Sistem Menejement Kepanitiaan`.

Caranya : 

Buka file <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `application/views/welcome_massage.php` lalu ubah teks pada line ke `71`.

![Codeigniter](/img/projek1/simkep2.jpg)

_Save_.. sekarang coba reload kembali halaman [http://localhost/SIMKEP](http://localhost/SIMKEP).

![Codeigniter](/img/projek1/simkep3.jpg)

Jejeng..

Sekarang header pada halaman awal [Codeigniter](https://kos-it.github.io/tagas/codeigniter) telah berubah menjadi `welcome to SIMKEP`.

Penjelasan:

File <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `welcome_message.php` yang berada di dalam direktori <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `views` merupakan file yang bertanggung jawab untuk menampilkan sesuatu. Di sini kita bisa menuliskan kode untuk template dan CSS.

File <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `welcome_message.php` di-load oleh sebuah controller <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `application/controllers/welcome.php` dengan kode:

![Codeigniter](/img/projek1/simkep4.jpg)

Controller welcome adalah controller default yang digunakan. Hal ini bisa kita lihat pada konfigurasi routers di <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `application/config/routers.php`.

![Codeigniter](/img/projek1/simkep5.jpg)

Bingung?

Tenang…

Kita akan pelajari di [tutorial berikutnya.](https://kos-it.github.io/post/tutorial-projek-1-bagian-2/)

# Selanjutnya :

 * [Tutorial SIMKEP dengan Codeiniter #2: (Controller) MVC dan Routing, Konsep dasar CI yang Harus Dipahami](https://kos-it.github.io/post/tutorial-projek-1-bagian-2/)
 * [Tutorial SIMKEP dengan Codeiniter #3: (View) Cara Menggunakan Bootstrap pada Codeiniger](https://kos-it.github.io/post/tutorial-projek-1-bagian-3/)
 * [Tutorial SIMKEP dengan Codeiniter #4: (View) Membuat Template Admin](https://kos-it.github.io/post/tutorial-projek-1-bagian-4/)
 * [Tutorial SIMKEP dengan Codeiniter #5: (Model) Membuat CRUD yang Baik](https://kos-it.github.io/post/tutorial-projek-1-bagian-5/)
 * [Tutorial SIMKEP dengan Codeiniter #6: Membuat Fitur Login](https://kos-it.github.io/post/tutorial-projek-1-bagian-6/)
 * [Tutorial SIMKEP dengan Codeiniter #7: Membuat Fitur Upload Gambar](https://kos-it.github.io/post/tutorial-projek-1-bagian-7/)
 * Tutorial SIMKEP dengan Codeiniter #8: Membuat Fitur Pencarian (Admin)
 * Tutorial SIMKEP dengan Codeiniter #9: Membuat Template untuk Landing Page dan Produk
 * Tutorial SIMKEP dengan Codeiniter #10: Membuat Pagination
 * Tutorial SIMKEP dengan Codeiniter #11: Cara Menggunakan Databales dan Optimasi
 * Tutorial SIMKEP dengan Codeiniter #12: Cara Membuat Laporan dengan DomPDF

