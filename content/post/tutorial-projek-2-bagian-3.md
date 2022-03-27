---
title: "Tutorial SIDAS dengan Codeiniter #3 : Konsep Dasar CI4 yang Harus dipahami"
date: 2022-03-27T14:38:47+08:00
categories: ["Website"]
tags: ["Tutorial Project - 2", "Website", "PHP", "Codeigniter4"]
cover: "/img/codeigniter.svg"
draft: false
---

Kali ini kita akan berkenalan lebih dekat dengan CI4.

Harapannya, kamu bisa terbiasa denga lingkungan kerja atau codebase CI4.

Kita akan mulai dengan mengenal struktur direktorinya terlebih dahulu, lalu membahas konsep MVC yang ada di Codeigniter 4.

Baiklah..

Mari kita mulai!

# Struktur Direktori Codeigniter 4
Jika kamu baru pertama kali belajar Codeigniter, maka wajib hukumnya mengetahui apa saja isi direktori dan file yang ada di dalam project codeigniter.

Silahkan buka teks Editor VS Code, lalu pilih **File->Open Folder**. Cari folder <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `sidas`.

Maka kita akan mendapatan struktur direktori seperti ini:

![ci4_3.10](https://drive.google.com/uc?expand&id=1hXfw6tU9BP1lR03jPOuoeeCXMS2lpsug)

Terdapat beberapa direktori dan file di sana. Mari kita bahas satu persatu. Mulai dari direktori dulu ya.

<div class="figure">
    <img draggable="true" alt="folder-ci4" src="https://drive.google.com/uc?expand&id=1CWi3PjB_TVAOu6Ba7kt9Ppg5I-_hL08h">
    <p>Struktur direktori Codeigniter 4</p>
</div>

* <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `.github` folder ini kita butuhkan untuk konfigurasi repo github, seperti konfigurasi untuk build dengan _github action_
* <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `app` folder ini akan berisi kode dari aplikasi yang kita kembangkan
* <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `public` folder ini berisi file yang bisa diakses oleh publik, seperti `file index.php`, `robots.txt`, `favicon.ico`, `ads.txt`, dll;
* <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `tests` folder ini berisi kode untuk melakukan testing dengan PHPunit
* <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `vendor` folder ini berisi library yang dibutuhkan oleh aplikasi, isinya juga termasuk kode core dari system CI.
* <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `writable` folder ini berisi file yang ditulis oleh aplikasi. Nantinya, kita bisa pakai untuk menyimpan file yang di-upload, logs, session, dll.

Berikutnya, kita akan bahas tentang file-file yang ada di direktori CI 4.

* <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `.env` adalah file yang berisi variabel environment yang dibutuhkan oleh aplikasi.
* <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `.gitignore` adalah file yang berisi daftar nama file dan folder yang akan diabaikan oleh [Git](*cooming_soon!*).
* ⚙️ `build` adalah script untuk mengubah versi codeigniter yang digunakan. Ada versi `release` (stabil) dan `development` (labil).
* 📜 `composer.json` adalah file JSON yang berisi informasi tentang proyek dan daftar library yang dibutuhkannya. File ini digunakan oleh Composer sebagai acuan.
* 📜 `composer.lock` adalah file yang berisi informasi versi dari libraray yang digunakan aplikasi.
* ©️ `license.txt` adalah file yang berisi penjelasan tentang lisensi Codeigniter,
* 📜 `phpunit.xml.dist` adalah file XML yang berisi konfigurasi untuk PHPunit.
* 📖 `README.md` adalah file keterangan tentang codebase CI. Ini biasanya akan dibutuhkan pada repo github atau gitlab.
* ⚙️ `spark` adalah program atau script yang berfungsi untuk menjalankan server, generate kode, dll.

Kemudian, coba kita fokus ke folder <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg">  `app`, di sana ada beberapa fodler dan file yang perlu kita ketahui.

* <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg">  `Config` adalah folder yang berisi konfigurasi untuk aplikasi,
* <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg">  `Controllers` adalah folder yang berisi kode Controller dari aplikasi
* <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg">  `Database` adalah folder yang berisi kode untuk migrasi database
* <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg">  `Filters` adalah folder yang berisi kode untuk filter atau middleware
* <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg">  `Helpers` adalah folder yang berisi kode untuk fungsi-fungsi helper
* <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg">  `Language` adalah folder yang berisi kamus bahasa untuk aplikasi.
* <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg">  `Libraries` adalah folder yang berisi library tambahan untuk aplikasi
* <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg">  `Models` adalah folder yang berisi kode untuk model.
* <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg">  `ThridParty` adalah folder yang berisi library dari pihak ketiga.
* <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg">  `Views` adalah folder yang berisi kode untuk view.
* 📜 `.htaccess` adalah file yang berisi konfigurasi akses untuk web server
* 📜 `Common.php` adalah file yang berisi definisi fungsi untuk menindih fungsi core dari CI.
* 📜 `index.html` adalah file placeholder untuk mencegah direct access.

Nah, itulah beberapa file dan folder yang harus dipahami. Sebenarnya masih banyak lagi file di dalam folder app yang harus kamu ketahui.

Namun, karena terlalu banyak.. nanti kita bahas barengan dengan tutorial berikutnya.

# Mengenal Konsep MVC Codeigniter 4

Codeigniter sejak awal menganut konsep MVC. Karena itu, ia begitu terkenal. Soalnya, implementasi MVC di CI mudah dipahami.

Apa itu MVC?

MVC adalah singkatan dari _Model–View–Controller_. MVC merupakan sebuah pola desain arsitektur yang umum digunakan dalam pengembangan aplikasi.

Masih ingat latar belakang mengapa kita harus pakai framework?

Yap, biar kode program lebih konsisten dan tersetruktur. Sehingga kita akan mudah kolaborasi dengan tim.

Nah, si MVC ini adalah pola penulisan kode yang umum dipakai.. dimana kode untuk _Model_ di taruh dalam folder yang sama, begitu juga dengan kode untuk _View_ dan _Controller_.

Coba perhatikan gambar berikut:

![mvc1](https://drive.google.com/uc?expand&id=1y4m87B3DIOffTWBlpoefnQOvPnAbekuv)

Gambar ini menyatakan bagaimana hubungan kode pada MVC.

# Apa itu Model?
Model adalah kode yang bertugas untuk membuat pemodelan data. Kadang juga dipakai untuk pemodelan bisnis.

Model bisa mengakses data dari Database dan juga sumber lainnya.

Intinya:

Kalau berkaitan tentang data, itu tugasnya model.

# Apa itu View?
View adalah kode yang bertugas untuk membuat tampilan aplikasi.

Ingat:

Fokusnya untuk membuat tampilan aplikasi, bukan yang lain. Kita tidak boleh query data dari view, meskipun itu bisa dilakukan.

Kadang juga kita akan membuat sedikit logika di dalam view, seperti logika untuk menampilkan dan menghilangkan elemen tertentu.

Apa yang kita lihat di aplikasi, itu adalah kode dari View.

# Apa itu Controller?
Nah, si Controller inilah yang bertugas menyatukan Model dan View.

Jadi, setiap ada _request_..

Controller akan bertanggung jawab untuk membalas _reques_ tersebut.

Jika itu _request_ untuk menyimpan data ke database, maka Controller harus memanggil Model yang bertanggung jawab untuk data tersebut. Lalu meminta model untuk menyimpannya ke database.

Jika itu _request_ untuk view data, maka Controller akan mencari kode View yang bertanggung jawab untuk menampilkan data tersebut.

Kadang juga Controller akan membutuhkan beberapa library dan helper untuk memproses _request_.

Intinya:

Controller bertanggung jawab untuk membalas _reques_ dari client.

Tapi sebelum itu.. ada **router** di depan controller yang bertanggung jawab untuk menentukan Controller mana yang akan dieksekusi.

# Router di Codeigniter 4
Coba buka file `app/Config/Routes.php`. File ini adalah file router yang bertugas untuk menentukan, Controller mana yang akan bertanggung jawab pada _request_ tertentu.

![mvc1](https://drive.google.com/uc?expand&id=1bsrADdi1r9KuoAMuv3NglZXjeFJXheaK)

Sebagai contoh:

Perhatikan kode ini.
```
$routes->get('/', 'Home::index');
```
Saat ada _request_ ke halaman root (/) atau alamat domain dari aplikasi, maka Controller yang akan bertugas adalah Home dan method yang akan dipakai adalah index.

Intinya:

Router akan memberikan tugas pada Controller tertentu untuk membalas sebuah _request_.

# Apa Selanjutnya?
Jadi kesimpulannya:

Codeigniter 4, menggunakan konsep MVC. _request_ pada Codeigniter pertamakali akan diterima oleh file `public/index.php` kemudian diteruskan ke router dan diproses oleh Controller.

Berikutnya, silahkan pelajari:

* ➡️ [Tutorial CI 4: Memahami Router dan Controller](https://kos-it.github.io/post/tutorial-projek-2-bagian-4/)

<blockquote>Untuk tutorial CI lainnya, cek di 📚 <a href=https://kos-it.github.io/tags/codeigniter4>[List Tutorial Codeigntier]</a></blockquote>