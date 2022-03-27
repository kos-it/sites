---
title: "Tutorial SIDAS dengan Codeiniter #4 : Memahami Routing dan Controller"
date: 2022-03-27T15:31:39+08:00
categories: ["Website"]
tags: ["Tutorial Project - 2", "Website", "PHP", "Codeigniter4"]
cover: "/img/codeigniter.svg"
draft: false
---

Routing dan Controller..

Kedua hal ini wajib kamu pahami.

Mengapa?

Karena kedua hal inilah yang menjadi ‘penggerak’ dalam aplikasi.

Pada tutorial ini, kita akan belajar seputar Routing dan Controller pada Codeigniter 4.

Pastikan kamu menyimaknya sampai selesai agar benar-benar paham.

Baiklah…

Mari kita mulai!

# Apa itu Routing dan Controller?
**Routing** adalah proses menentukan arah atau rute yang harus dilalui.

Pada framework CI4, _routing_ bertujuan untuk menentukan Controller mana yang harus merespon sebuah request.

Controller adalah class atau script yang bertanggung jawab merespon sebuah _request_.

Ia bisa saja merespon dengan mengirimkan view, data JSON, data XML, atau bahkan tidak mengirimkan respon apapun.

Karena ada juga bagian dari Controller yang harnya bertugas menerima data dan menyimpannya ke database.

Coba perhatikan lagi gambar ini:

![mvc1](https://drive.google.com/uc?expand&id=1bsrADdi1r9KuoAMuv3NglZXjeFJXheaK)

File `index.php` adalah file _entri point_ yang akan dieksekusi pertamakali saat aplikasi dibuka.

_Request_ yang diterima oleh `index.php` akan diserahkan ke _Router_. Lalu si _Router_ akan menentukan Controller yang akan meresponnya.

Oh iya, jangan bingung dengan istilah routes, router, dan routing..

Berikut ini penjelasannya:

* _Routes_ adalah kumpulan definisi routing
* _Router_ adalah script yang menentukan routing
* _Routing_ adalah proses menentukan rute.

Lalu, bagaimana cara kita membuat Routes di Codeigniter?

Mari kita bahas:

# Membuat Routes di Codeigniter

Oke, sekarang coba lihat kembali kode aplikasi sidas.

Buka file `app/config/Routes.php`.

![ci4-routes](https://drive.google.com/uc?expand&id=1UwWO3UQS3UuyI1X0e23rxHyjoMENrvIk)

Pada file `Routes.php`, kita bisa mendefinisikan rute untuk aplikasi.

Coba perhatikan bagian ini:
```
$routes->get('/', 'Home::index');
```
Ini adalah rute untuk home page.

Bingung?

Coba perhatikan gambar berikut:

![ci4_4.10_](https://drive.google.com/uc?expand&id=1piklUNkfKPceDowNiSZ8gkkoBVqvTSOJ)

Sudah paham?

Bagus..

Sekarang mari kita coba membuat sebuah rute baru.

Tambahkan kode berikut di dalam `Routes.php`:
```
$routes->get('/about', 'Page::about');
$routes->get('/contact', 'Page::contact');
$routes->get('/faqs', 'Page::faqs');
```
Nah, di sini kita membuat tiga buat rute baru. Pada rute ini kita memberikan tugas kepada controller Page untuk merespon request pada rute tersebut.

Untuk memastikan rute sudah dibuat dengan benar, coba ketik perintah:
```
php spark routes
```
Jika muncul seperti ini:

![ci4_4.11_](https://drive.google.com/uc?expand&id=1bv1XBxy-3N-izv5Adtkidu2RDj9icxlV)

Maka pembuatan rute berhasil.

Selanjutnya kita harus membuat Controller `Page.php`.

# Membuat Controller
Silahkan buat file baru di dalam folder `app/Controllers` dengan nama `Page.php`.

Pastikan kamu menggunakan huruf kapital di awal nama file. Karena ini sudah menjadi aturan pada Codeigniter.

Kemudian isi file `Page.php` dengan kode berikut:

```php
<?php namespace App\Controllers;

class Page extends BaseController
{
	public function about()
	{
		echo "about page";
	}
    
    public function contact()
	{
		echo "contact page";
	}
    
    public function faqs()
	{
		echo "Faqs page";
	}

}
```
Controller Page memiliki tiga method, yakni `about()`, `contact()`, dan `faqs()`.

Nama method ini mengikuti nama yang sudah kita tentukan di dalam rute. Jika kita menggunakan nama yang berbeda, maka ia tidak akan bisa dibuka.

Pada setiap method di Controller `Page`, kita membuat respon dengan perintah `echo`. Kita juga nanti bisa merespon dengan view.

Oke, sekarang mari kita tes hasilnya.

jalankan pertintah cli pada project dengan
```
php spark serve
```
Silahkan buka halaman berikut:

* `localhost:8080/about`
* `localhost:8080/contact`
* `localhost:8080/faqs`

Hasilnya :

![ci4_4.12](https://drive.google.com/uc?expand&id=1mPDtjNCRUc8IQHoFK5123zSQ7cr3tM8T)

Bagus..

Rute yang kita buat berhasil dibuka.

# Autoroute di Codeigniter 4
Pada Codeigniter 3, routing dilakukan secara otomatis dengan mengikuti nama Controller dan method-nya.

Pada Codeigniter 4, kita juga bisa mengaktifkan fitur ini pada app/config/Routes.php dengan kode:
```php
$routes->setAutoRoute(true);
```
Jika ingin menonaktifkan autoroute, tinggal ganti true menjadi false.
```php
$routes->setAutoRoute(false);
```

Secara default, fitur autoroute sudah aktif.

Mari kita coba..

Tambahkan method tos() pada Controller Page dengan isi seperti ini:
```php
public function tos()
{
    echo "Halaman Term of Service";
}
```
Sehingga sekarang kode Controller Page menjadi seperti ini:
```php
<?php namespace App\Controllers;

class Page extends BaseController
{
	public function about()
	{
		echo "about page";
	}
    
    public function contact()
	{
		echo "contact page";
	}
    
    public function faqs()
	{
		echo "Faqs page";
    }
    
    public function tos()
    {
        echo "Halaman Term of Service";
    }

}
```

Ingat:

Method tos() belum kita daftarkan di dalam `Routes.php`. Namun, karena autoroute aktif, maka method ini bisa kita akses melalui:

`localhost:8080/index.php/page/tos`

Hasilnya:

![ci4_4.13](https://drive.google.com/uc?expand&id=1zUGepeJry91iT9e97FKSBY78pNpSEtIs)

Sekarang coba matika fitur _autoroute_.

Pada kode `app/Config/Routes.php`, berikan nilai false pada `setAutoRoute()`.
```php
$routes->setAutoRoute(false);
```
Maka sekarang method `tos()` tidak akan bisa dibuka.

![ci4_4.14](https://drive.google.com/uc?expand&id=13FDBfqYPlBjTn_4fQ6N5xdvbWB5pxhhp)

Ini karena kita mematikan fitur _autoroute_.

Sebaiknya pakai _autoroute_ atau manual route?

Sebenarnya ini tergantung kita sebagai developer, jika tidak ingin repot-repot membuat rute maka baiknya pakai autoroute. Namun atuoroute akan membuat semua method public di Controller akan bisa diakses.

# Apa Selanjutnya?
Sebenarnya masih banyak lagi hal tentang routing yang harus diketahui. Namun, untuk tutorial basic.. saya cukupkan sampai di sini.

Nanti kita akan pelajari routing lebih lenjut, bersamaan dengan dengan pembahasan fitur Codeigniter lainnya.

Barikutnya kita akan belajar tentang View di Codeigniter.

Silahkan lanjutkan ke:

* ➡️ [Tutorial Codeigniter: Memahami View di Codeigniter](https://kos-it.github.io/post/tutorial-projek-2-bagian-5/)

<blockquote>Untuk tutorial CI lainnya, cek di 📚 <a href=https://kos-it.github.io/tags/codeigniter4>[List Tutorial Codeigntier]</a></blockquote>