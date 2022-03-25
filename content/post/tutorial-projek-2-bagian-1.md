---
title: "Tutorial SIDAS dengan Codeiniter #1 : Pengenalan Codeigniter untuk Pemula"
date: 2022-03-25T19:16:46+08:00
categories: ["Website"]
tags: ["Tutorial Project - 2", "Website", "PHP", "Codeigniter4"]
cover: "/img/codeigniter.svg"
draft: false
---

Kamu sudah belajar basic PHP dan OOP?

Bagus.

Kini saatnya belajar framework.

Framework telah terbukti banyak membantu web developer dalam mengembangkan web.

Proyek web yang diperkirakan bisa jadi dalam satu bulan, dengan framework..

..mungkin bisa jadi dalam seminggu.

Hebat kan.

Karena itu, kamu harus menggunakan framework agar bisa membuat web lebih cepat dan juga hemat biaya dan tenaga.

Baiklah…

Framework yang akan kita pelajari di tutorial ini adalah Codeigniter.

Codeigniter cukup populer di Indoensia dan juga banyak penggunanya.

Mari kita mulai..

# Apa itu Framework?
Sebelum masuk ke Codeigniter, kita bahas dulu pengertian **framework**.

Jadi:

**Framework** dalam bahasa indonesia artinya **kerangka kerja**.

Saya yakin, kamu yang sedang membaca artikel ini sudah pernah membuat web dengan PHP.

Setidaknya membuat web sederhana yang berisi beberapa halaman.

Apa yang akan kamu lakukan jika webnya semakin kompleks?

Ya ditambahin lagi donk kodenya.

Tapi..

Kadang ini tidak berjalan mulus.

Kode website kita akan semakin ribet dan berantakan. Bisa jadi disbeabkan karena kita asal-asalan menambahkan kode.

Belum lagi, kita dituntut menulis kode yang rapi agar bisa dipahami orang lain (misalnya teman satu tim).

Maka di sini kita tidak boleh seenaknya menulis kode yang asal-asalan.

Karena itu, diciptakanlah framework atau kerangka kerja.

Kerangka kerja dibuat agar kita bisa bekerja lebih mudah. Biasanya, framework menyediakan bahan-bahan yang siap pakai, sehingga kita tidak harus membuatnya dari nol.

Selain itu, framework juga memiliki aturan-aturan yang harus diikuti.

Contohnya seperti:

* Harus menaruh kode yang memiliki fungsi yang sama dalam satu folder;
* Harus mengikuti aturan penulisan kode (writing conventions) yang disepakati;
* Harus menggunakan pola desain ini, dan itu;
* dan lain sebagainya.

Jadi apa itu framework?

Framework adalah sebuah kerangka kerja yang digunakan untuk membantu developer dalam mengembangkan kode aplikasi secara konsisten.

Lalu..
# Apa itu Codeigniter?
Codeigniter adalah salah satu framework untuk membuat website dengan bahasa pemrograman PHP.

Codeigniter terkenal dengan konsep MVC-nya. MVC merupakan singkatan dari *Model–View–Controller*.

Nanti kita akan bahas lebih dalam tentang MVC pada: [Konsep dasar Framework Codeigniter.]()

Codeigniter pernah menapat pujian dari creator PHP: [Rasmus Lerdorf](https://en.wikipedia.org/wiki/Rasmus_Lerdorf)

Ia menyukai Codeigniter karena lebih cepat dan lebih ringan. 1

## Keunggulan Codeigniter
Ada beberapa kelebihan CodeIgniter (CI) dibandingkan dengan Framework PHP lain,

* **Performa cepat**: Codeigniter merupakan framework yang paling cepat dibanding framework yang lain. Karena tidak menggunakan template engine dan ORM yang dapat memperlambat proses.
* **Konfigurasi yang minim** (*nearly zero configuration*): tentu saja untuk menyesuaikan dengan database dan keleluasaan routing tetap diizinkan melakukan konfigurasi dengan mengubah beberapa file konfigurasi seperti `database.php` atau `autoload.php`, namun untuk menggunakan codeigniter dengan setting standard, anda hanya perlu mengubah sedikit saja pada file di folder `config`.
* **Memiliki banyak komunitas**: Komunitas CI di indonesia cukup ramai, tutorialnya pun mudah dicari.
* **Dokumentasi yang lengkap**: Codeigniter disertai dengan `user_guide` yang berisi dokumentasi yang lengkap.
* **Mudah dipelajari pemula**: Bagi pemula, CI sangat mudah dipelajari. Karena CI tidak terlalu bergantung pada tool tambahan seperti composer, ORM, Template Engine, dll.

# Sejarah Singkat Codeigniter
Codeigniter pertamakali dibuat oleh EllisLab, sebuah perushaan software yang berbasis di Santa Barbara California.

EllisLab merilis Codeigniter pertamakali pada tanggal **28 Februari 2006**.

Beberapa tahun kemudian…

Sudah sekian lama tidak dikembangkan. EllisLab akhirnya ingin memberikan proyek Codeigniter kepada orang lain.

Pada tanggal **9 Juli 2013**, EllisLab mencari pemilik baru Codeigniter. Akhirnya pada tanggal **6 Oktober 2014** pengembangan Codeigniter dialnjutkan dibawa kepengurusan dari **British Columbia Institute of Technology** (BCIT).

Lalu..

Pada tanggal **23 Oktober 2019**, Codeigniter Foundation mengambil alih proyek ini dan tidak lagi dibawa kepengurusan BCIT.

Codeigniter Foundation adalah yayasan non-profit yang dibentuk untuk pengembangan Codeigniter lebih lanjut.

Proyek Codeigniter 4 pun dimulai dengan [Jim Parry](https://github.com/jim-parry) sebagai project lead.

…dan akhirnya pada tanggal **24 Februari 2020** Codeigniter 4 resmi dirilis.

Tanggal ini diambil, sebagai penghormatan terakhir kepada Jim Parry yang telah meninggal dunia pada tanggal **15 Januari 2020**.

<div class="figure">
    <img draggable="true" alt="image" src="https://drive.google.com/uc?expand&id=1P5u8D9jaDPrb4bjpthmEDUzgHfUBqNFs">
    <p>Jim Parry</p>
</div>

R.I.P Jim Parry, terimakasih atas kontribusinya di Codeigniter 4.

# Versi dan Perkembangan Codeigntier
* Codeigniter 1 oleh EllisLab (sudah tidak dikembangkan)
* Codeigniter 2 oleh BCIT (sudah tidak dikembangkan)
* Codeigniter 3 oleh BCIT (masih dikembangkan)
* Codeigniter 4 oleh Codeingter Foundation (versi saat ini)

# Codeigniter Versi Berapa yang Harus saya Pelajari?
Saya merekomendasikan mempelajari Codeigniter 3 atau Codeigniter 4. Karena kedua versi ini masih dikembangkan hingga saat ini.

Codeigniter 3, adalah codeigniter yang dirilis oleh BCIT dan ditargetkan untuk digunakan pada PHP 5.

Codeigniter 3 juga bisa digunakan di PHP 7.

Meskipun sudah ada Codeigniter 4, versi 3 masih tetap dikembangkan.

Jadi, masih akan ada update terbaru di versi 3 hingga waktu yang belum ditentukan.

Kita tunggu saja, pengumuman resmi kapan Codeigniter 3 akan dihentikan.

Sementara itu Codeigniter 4, ditargetkan untuk digunakan pada PHP 7 ke atas. Versi ini dirilis oleh Codeigniter Foundation dan akan menjadi generasi penerus Codeigniter 4.

Bingung mau belajar yang mana?

Mari kita coba bandingkan secara detail

## Perbedaan Codeigniter 3 dengan Codeigniter 4
<table>
<thead>
<tr>
<th>Dari segi</th>
<th>Codeigniter 3</th>
<th>Codeigniter 4</th>
</tr>
</thead>
<tbody>
<tr>
<td>Versi PHP</td>
<td>PHP 5.6+</td>
<td>PHP 7.2+</td>
</tr>
<tr>
<td>Release oleh</td>
<td>BCIT</td>
<td>Codeigniter Foundation</td>
</tr>
<tr>
<td>Konsep</td>
<td>MVC</td>
<td>MVC</td>
</tr>
<tr>
<td>Site Root</td>
<td>project root folder</td>
<td><code>public</code> folder</td>
</tr>
<tr>
<td>Application folder</td>
<td><code>application</code></td>
<td><code>app</code></td>
</tr>
<tr>
<td>Controller Class</td>
<td><code>CI_Controller</code></td>
<td><code>\CodeIgniter\Controller</code></td>
</tr>
<tr>
<td>Object HTTP req/res</td>
<td>tidak ada</td>
<td><code>Request</code> dan <code>Response</code></td>
</tr>
<tr>
<td>Model Class</td>
<td><code>CI_Model</code></td>
<td><code>\CodeIgniter\Model</code></td>
</tr>
<tr>
<td>CRUD di Model</td>
<td>Bikin sendiri</td>
<td>Sudah disediakan</td>
</tr>
<tr>
<td>Entity Class</td>
<td>Tidak ada</td>
<td>Ada</td>
</tr>
<tr>
<td>View</td>
<td><code>$this-&gt;load-&gt;view(x);</code></td>
<td><code>echo view(x);</code></td>
</tr>
<tr>
<td>View Cell</td>
<td>tidak ada</td>
<td>ada</td>
</tr>
<tr>
<td>Load Library</td>
<td><code>$this-&gt;load-&gt;library(x);</code></td>
<td><code>$this-&gt;x = new X();</code></td>
</tr>
<tr>
<td>Middleware</td>
<td>Tidak ada</td>
<td>Ada Filters</td>
</tr>
<tr>
<td>FIle <code>.env</code></td>
<td>Tidak ada</td>
<td>Ada</td>
</tr>
<tr>
<td>Command Line Tools</td>
<td>Tidak ada</td>
<td>Ada <code>spark</code></td>
</tr>
</tbody>
</table>

Nah, itulah beberapa perbandingan dari segi teknis. Semoga kamu bisa menentukan versi Codeigniter yang akan dipelajari.

Kalau bedasarkan pilihan pribadi, saya lebih menyarankan belajar yang versi 4, karena punya lebih banyak fitur dan lebih canggih dan juga terupdate.

# Apa Selanjutnya?
Sejauh ini, kita sudah mengenal Codeigniter. Mulai dari mempelajari sejarah dan asal usulnya. Hingga versi terbaru saat ini.

Jika kamu sudah menentukan versi Codeigniter yang akan dipelajari, silahkan lanjutkan ke:

* [Persiapan Belajar Codeigniter 3](https://kos-it.github.io/tags/tutorial-project-1)
* [Persiapan Belajar Codeigniter 4](https://kos-it.github.io/tags/tutorial-project-2)

Selamat belajar.