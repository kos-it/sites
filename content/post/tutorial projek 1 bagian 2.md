---
title: "Tutorial SIMKEP dengan Codeiniter #2 : MVC dan Routing, Konsep dasar CI"
date: 2020-01-01T23:35:00+09:00
categories: ["Website"]
tags: ["Tutorial Project - 1", "Website", "PHP", "Codeigniter"]
cover: "https://drive.google.com//uc?export=view&id=1zKgyxiCm9R2RlIFO8O1cbknZGUN8NrRC"
---

Selamat datang di **KOS-IT** - Making and Developing...

Pada [tutorial sebelumnya](https://kos-it.github.io/post/tutorial-projek-1-bagian-1), kita sudah mengetahui cara menginstall [Codeigniter](https://kos-it.github.io/tags/codeigniter/) dan mengenal struktur direktori dari [Codeigniter](https://kos-it.github.io/tags/codeigniter/).

Pada tutorial kali ini kita akan belajar tentang *routing* dan MVC pada projek 1 kita yaitu [Sistem Management Kepanitaan](https://kos-it.github.io/projects/projek-sistem-menejement-kepanitiaan/).

Namun sebelum kita melakukannya ada baiknya kita berkenalan dulu dengan konsep dasar [Codeigniter](https://kos-it.github.io/tags/codeigniter/)

[Codeigniter](https://kos-it.github.io/tags/codeigniter/) adalah framework [PHP](https://kos-it.github.io/tags/php/) yang menggunakan konsep MVC.

Apa itu MVC ?

Mari kita bahas

# Mengenal Konsep MVC pada Codeigniter 
Model-View-Controller atau MVC adalah sebuah metode untuk membuat sebuah aplikasi dengan memisahkan data (Model) dari tampilan (View) dan cara bagaimana memprosesnya (Controller).

MVC membagi aplikasi ke dalam tiga bagian fungsional: model, view, dan controller.
    
* **Model**, Model mewakili struktur data. Model merupakan bagian yang bertugas untuk mengatur, menyiapkan, memanipulasi, dan mengorganisir data (biasanya dari basis data). Tugas yang ia lakukan meliputi memasukkan data ke basis data, pembaruan data, menghapus data, dan lain-lain. Model menjalankan tugasnya berdasarkan instruksi dari controller.
* **View**, View merupakan bagian yang mengatur tampilan ke pengguna. Bisa dikatakan berupa halaman web.
* **Controller**, Controller merupakan bagian yang menjembatani model dan view. Controller berisi perintah-perintah yang berfungsi untuk memproses suatu data dan mengirimkannya ke halaman web.

Dengan menggunakan metode MVC maka aplikasi akan lebih mudah untuk dirawat dan dikembangkan. Untuk memahami metode pengembangan aplikasi menggunakan MVC diperlukan pengetahuan tentang pemrograman berorientasi objek (Object-oriented programming).

Alur kerja seperti ini

![MVC](https://drive.google.com/uc?export=view&id=1IfzaXngiTMfZ1Ij89zf3BKNNaR-AR_eY)

1. Mulai;
2. User mengirim request ke web;
3. File yang pertama kali dieksekusi adalah <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `index.php`
4. Lalu dari <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `index.php`, request akan diteruskan oleh <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `routers.php`
5. <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `routers.php` akan mencari cache di server, apabila tedapat cache maka cache itu yang akan dikirim sebagai balasan (response). Apabila tidak ada cache barulah request diteruskan ke Controller
6. Controller akan bertanggunag jawab untuk mengambil data dari Model dan me-rendernya ke dalam View dengan menggunakan library, plugin, dan helper yang ada.
7. Hasil render (view) dikirim ke pengguna dan disimpan dalam cache, apabila fitur cache aktif
8. Selesai.

![MVC2](https://drive.google.com/uc?export=view&id=1WxiyhMAaIg11ZIqMoE2A-plZVj33XCG6)

# Memahami Router pada Codeigniter

Router pada Codeigniter bertugas untuk menentukan controller dan method/fungsi yang akan dieksekusi.

Ketika kita membuka, http://localhost/simkep/ maka fungsi yang akan dieksekusi adalah fungsi index() yang berada di dalam controller welcome.

<!--{{< highlight php "linenos=table,hl_lines=4,linenostart=7" >}}
class Welcome extends CI_Controller {
	public function index()
	{
		$this->load->view('welcome_message');
	}
}
{{< / highlight >}}-->

```php {linenos=table,hl_lines=[8,"15-17"],linenostart=199}
class Welcome extends CI_Controller {
	public function index()
	{
		$this->load->view('welcome_message');
	}
}
```

Kenapa bisa begitu?

Ini karena konfigurasi router defaultnya adalah controller `welcome`.

Coba saja buka pada file <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `config/routers.php`

![Router](https://drive.google.com/uc?export=view&id=1mlQtiQTb4Iy_jcY9_OL-UO7oZQvjx4i6)

Fungsi `index()` adalah fungsi yang akan dieksekusi saat kita mengakses *controller* `welcome`.

Sekarang coba buka: 
<a href="http://localhost/simkep/index.php/welcome/index/" target="_blank">http://localhost/simkep/index.php/welcome/index/</a> , maka kita akan mendapatkan hal yang sama seperti membuka
<a href="http://localhost/simkep/" target="_blank">http://localhost/simkep/..</a>

![Router2](https://drive.google.com/uc?export=view&id=1TK9aVsdHbYbsG4ePAOlbM2pNw6Swhvxz)

# Membuat Beberapa Router

Sebagai latihan, coba tambahkan route `/about/` dan `/contact/` di dalam Controller <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `Welcome` dengan method ini:

```php
public function about()
{
	// fungsi untuk me-load view about.php
	$this->load->view('about');
}

public function contact()
{
	// fungsi untuk me-load view contact.php
	$this->load->view('contact');
}
```

Tambahkan di bawah method `index()`.

![route](https://drive.google.com/uc?export=view&id=1mExQOG9ZTZxIDBbL_T2PuNoisnaffMMc)

Setelah itu tambahkan dua buah file view di dalam direktori <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `views` dengan isi sebagai berikut.

<img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `views/about.php`

```html
<h1>About Us</h1>
<p>Ini adalah halaman about</p>
```

<img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `views/contact.php`

```html
<h1>Contact Us</h1>
<p>Ini adalah halaman Contact</p>
```
Route sudah kita tambahkan.

Sekarang coba buka:

* http://localhost/simkep/index.php/welcome/about/

* dan http://localhost/simkep/index.php/welcome/contact/

Hasilnya adalah akan terjadi error 404 not found.

![route2](https://drive.google.com/uc?export=view&id=1rDv_QldFrb2Sy8rk0n81Smhitm3_rN5k)

Kenapa seperti itu?

Ini karena route yang baru saja kita buat, belum didaftarkan ke dalam `routers.php`.

Sekarang buka file <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `config/routers.php`, lalu tambahkan kode berikut.

```php
$route['about'] = 'welcome/about';
$route['contact'] = 'welcome/contact';
```
Tambahkan di bawah kode route yang sudah ada.

![route3](https://drive.google.com/uc?export=view&id=1nJXhRIl8f-P0oQUn0Xif9hhxVq2NmQDV)

Hasilnya:

![route4](https://drive.google.com/uc?export=view&id=1Wy4IwxHaF_3jfAkx1YtMNAGalHn10SY3)

**Apakah kita harus menambahkan route pada routers.php di setiap pembuatan route baru?**

Jawabannya:

**Tidak harus**, karena CI juga mampu mendeteksi otomatis route berdasarkan nama controller dan method yang dibuat.

![Router2](https://drive.google.com/uc?export=view&id=1TK9aVsdHbYbsG4ePAOlbM2pNw6Swhvxz)

Ini formatnya:

```
http://example.com/[controller-class]/[controller-method]/[arguments]
```

Penambahan route pada <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `routers.php` dibutuhkan saat kita ingin membuat kustom route untuk controller tertentu.

# Apa Selanjutnya?

Kita sudah belajar tentang MVC dan Route. Ini memang masih dasar. Selanjutnya nanti kita akan banyak menggunakannya.

Jadi, harap diphami betul dua hal ini.

Jika masih bingung, silahkan ditanyakan melalui komentar.

Berikutnya pelajari tentang:

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

 Selamat belajar.

 # Sebelumnya 

 * [Tutorial SIMKEP dengan Codeiniter #1 : Pengenalan Codeigniter](https://kos-it.github.io/post/tutorial-projek-1-bagian-1/) 