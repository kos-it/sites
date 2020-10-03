---
title: "Tutorial SIMKEP dengan Codeiniter #4: (View) Membuat Template Admin"
date: 2020-06-28T23:35:00+09:00
categories: ["Website"]
tags: ["Tutorial Project - 1", "Website", "PHP", "Codeigniter"]
cover: "https://drive.google.com//uc?export=view&id=1zKgyxiCm9R2RlIFO8O1cbknZGUN8NrRC"
---

Pada tutorial sebelumnya, kita sudah berhasil menambahkan Bootstrap [Template SB Admin](https://startbootstrap.com/template-overviews/sb-admin/) pada proyek CI.

Tapi, masih belum selesai…

Template yang kita buat masih dibuat dalam satu file saja. Ini akan bermasalah ketika kita membuat halaman baru.

Permsalahannya:

Kita akan menulis kode template yang sama berulang-ulang dalam file `view` yang berbeda.

Bagaimana nanti kalau ada perubahan?

Misal, perubahan link pada navbar.

Maka kita harus mengubah semua file template yang kita buat satu per satu.

Tentu ini kurang efektif, karena kita akan menghabiskan banyak waktu dan tentaga untuk mengubahnya.

Salah satu solusi dari permasalahan ini yaitu dengan menggunakan partials. Dengan partials kita akan membagi template menjadi bagian-bagian kecil yang akan kita panggil kedalam file `view` menggunakan fungsi `$this->load->view()`. yang fungsinya yaitu untuk me-load sebuah view.

Fungsi `$this->load->view()` ini, nanti akan kita gunakan untuk me-load partials ke dalam template.

# Membuat Partials Template

Partial merupakan teknik untuk membagi template menjadi bagian-bagian kecil agar mudah digunakan.
<div class="figure">
    <img draggable="true" alt="image" src="https://drive.google.com/uc?export=view&id=1KL1aqt_uPMtNgCgXp_IIxaytqeh9H196">
    <p>Partials Template</p>
</div>

Sekarang coba buka file <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `index.html` pada SB Admin dan perhatikan, apa saja partial yang bisa kita buat dari sana?

![partials](https://drive.google.com/uc?export=view&id=1-40t06Sk8ZOeCTnYYfEKn7ypqzyldqUU)

Berdasarkan gambar di atas ditambah beberapa kode asser, berikut ini partial yang akan kita buat:

* <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `head.php` untuk meinyimpan isi dari tag `<head>`
* <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `navbar.php` untuk menyimpan kode navbar
* <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `sidebar.php` untuk menyimpan kode menu bagian samping (sidebar)
* <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `breadcrumb.php` untuk menyimpan kode link breadcrumb
* <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `scrolltop.php` untuk menyimpan kode tombol scrolltop
* <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `footer.php` untuk menyimpan kode footer
* <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `modal.php` untuk menyimpan kode modal
* <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `js.php` untuk meload javascript

Mari kita buat satu per satu…

Tapi sebelum itu, silahkan buat dulu direktori baru bernama <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `_partials` di dalam <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `views/admin/`.

![createpartials](https://drive.google.com/uc?export=view&id=13MhRIMXFrcTDyrCvDhKmSie6uQJfmKRi)

Apakah nama direktorinya harus `_partials`?

Tidak harus, karena ada juga membarikan nama includes atau _includes.

Nama _partials menurut kami lebih jelas dan menggambarkan isinya.

Kenapa ada garis bawah (underscore) di depannya?

Ini untuk memudahkan dalam membedakan view dan partial. View akan kita load dari Controller, sedangkan partial akan kita load dari view.

Biasanya dalam penulisan kode (OOP), sesuatu yang bersifat private dan lokal kadang ditulis dengan garis bawah di depannya.

Oke, lanjut…

Berikutnya kita akan membuat semua partial yang telah kita tentukan di atas.

# Partial `head.php`

Partial ini berisi kode-kode untuk tag <head>. Kita bisa copy dari file views/admin/overview.php mulai dari tag <head> sampai penutupnya </head>.

Sehinggak kode untuk partial head.php akan menjadi seperti ini:

```html
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, shrink-to-fit=no">

    <title><?php echo SITE_NAME .": ". ucfirst($this->uri->segment(1)) ." - ". ucfirst($this->uri->segment(2)) ?></title>
    <link rel="shortcut icon" href="<?php echo base_url('assets/img/ppptk.png')?>">

    <!-- Bootstrap core CSS-->
    <link href="<?php echo base_url('assets/bootstrap/css/bootstrap.min.css') ?>" rel="stylesheet">

    <!-- Custom fonts for this template-->
    <link href="<?php echo base_url('assets/fontawesome-free/css/all.min.css') ?>" rel="stylesheet" type="text/css">

    <!-- Page level plugin CSS-->
    <link href="<?php echo base_url('assets/datatables/dataTables.bootstrap4.css') ?>" rel="stylesheet">

    <!-- Custom styles for this template-->
    <link href="<?php echo base_url('css/sb-admin.css') ?>" rel="stylesheet">
</head>
```

Perhatikan kode pada tag `<title>`, di sana kita menggunakan sebuah konstanta `SITE_NAME` untuk mengambil nama web.

Konstanta ini sudah kita buat pada [tutorial sebelumnya](https://kos-it.github.io/post/tutorial-projek-1-bagian-3/).

Berikutnya perhatikan di bagian:

```
ucfirst($this->uri->segment(1)) ." - ". ucfirst($this->uri->segment(2))
```

Ini akan menjadi judul yang akan tampil di browser. Fungsi ucfirst() untuk membuat huruf besar di awal kata. Lalu judulnya kita ambil dari segment URL.

Sehingga nanti pada browser akan tampil seperti ini:

![createpartials](https://drive.google.com/uc?export=view&id=14QgWAGLTf7EUF352YMjHsZKF4KOKFDfk)

# Partial `navbar.php`

Partial ini hanya berisi kode untuk menu navbar. Berikut ini isi kode dari partial `navbar.php`:

```html
<nav class="navbar navbar-expand navbar-dark bg-secondary static-top">

<img width="60" height="50" src="<?php echo base_url()?>assets/img/ppptk.png"/>
    <a class="navbar-brand mr-1" href="<?php echo site_url('admin') ?>">&nbsp;&nbsp;&nbsp;<?php echo SITE_NAME ?></a>

    <button class="btn btn-link btn-sm text-white order-1 order-sm-0" id="sidebarToggle" href="#">
        <i class="fas fa-bars"></i>
    </button>

    <!-- Navbar Search -->
    <form class="d-none d-md-inline-block form-inline ml-auto mr-0 mr-md-3 my-2 my-md-0">
        <div class="input-group">
            <input type="text" class="form-control" placeholder="Search for..." aria-label="Search" aria-describedby="basic-addon2">
            <div class="input-group-append">
                <button class="btn btn-light" type="button">
                    <i class="fas fa-search"></i>
                </button>
            </div>
        </div>
    </form>

    <!-- Navbar -->
    <ul class="navbar-nav ml-auto ml-md-0">
        <li class="nav-item dropdown no-arrow mx-1">
            <a class="nav-link dropdown-toggle" href="#" id="alertsDropdown" role="button" data-toggle="dropdown" aria-haspopup="true"
                aria-expanded="false">
                <i class="fas fa-bell fa-fw"></i>
                <span class="badge badge-danger">9+</span>
            </a>
            <div class="dropdown-menu dropdown-menu-right" aria-labelledby="alertsDropdown">
                <a class="dropdown-item" href="#">Action</a>
                <a class="dropdown-item" href="#">Another action</a>
                <div class="dropdown-divider"></div>
                <a class="dropdown-item" href="#">Something else here</a>
            </div>
        </li>

        <li class="nav-item dropdown no-arrow mx-1">
            <a class="nav-link dropdown-toggle" href="#" id="messagesDropdown" role="button" data-toggle="dropdown" aria-haspopup="true"
                aria-expanded="false">
                <i class="fas fa-envelope fa-fw"></i>
                <span class="badge badge-danger">7</span>
            </a>
            <div class="dropdown-menu dropdown-menu-right" aria-labelledby="messagesDropdown">
                <a class="dropdown-item" href="#">Action</a>
                <a class="dropdown-item" href="#">Another action</a>
                <div class="dropdown-divider"></div>
                <a class="dropdown-item" href="#">Something else here</a>
            </div>
        </li>

        <li class="nav-item dropdown no-arrow">
            <a class="nav-link dropdown-toggle" href="#" id="userDropdown" role="button" data-toggle="dropdown" aria-haspopup="true"
                aria-expanded="false">
                <i class="fas fa-user-circle fa-fw"></i> Admin
            </a>
            <div class="dropdown-menu dropdown-menu-right" aria-labelledby="userDropdown">
                <a class="dropdown-item" href="#">Settings</a>
                <a class="dropdown-item" href="#">Activity Log</a>
                <div class="dropdown-divider"></div>
                <a class="dropdown-item" href="#" data-toggle="modal" data-target="#logoutModal">Logout</a>
            </div>
        </li>
    </ul>

</nav>
```

Pada kode navbar, kita menggunakan konstanta `SITE_NAME` untuk menampilkan nama web di navbar.

Lalu kita menggunakan class `bg-secondary` untuk mengubah warnanya menjadi lebih ke-abu-abu. Supaya selaras dengan brand aplikasinya.

Ini tampilannya:
![navbar](https://drive.google.com/uc?export=view&id=1XoeCXO0mgbSpvw7cxOvYEIB-5OrCQShq)

# Partial `sidebar.php`

Partial ini berisi kode untuk menampilkan menu bagian samping (sidebar). Berikut ini isi kode sidebar.php:

```html
<ul class="sidebar navbar-nav">
    <li class="nav-item <?php echo $this->uri->segment(2) == '' ? 'active': '' ?>">
        <a class="nav-link" href="<?php echo site_url('admin') ?>">
            <i class="fas fa-fw fa-tachometer-alt"></i>
            <span>Overview</span>
        </a>
    </li>
    <li class="nav-item dropdown <?php echo $this->uri->segment(2) == 'staff' ? 'active': '' ?>">
        <a class="nav-link dropdown-toggle" href="#" id="pagesDropdown" role="button" data-toggle="dropdown" aria-haspopup="true"
            aria-expanded="false">
            <i class="fas fa-fw fa-users"></i>
            <span>Staff</span>
        </a>
        <div class="dropdown-menu" aria-labelledby="pagesDropdown">
            <a class="dropdown-item" href="<?php echo site_url('admin/staff/add') ?>">New Staff</a>
            <a class="dropdown-item" href="<?php echo site_url('admin/staff') ?>">List Staff</a>
        </div>
    </li>
    <li class="nav-item dropdown <?php echo $this->uri->segment(2) == 'devisi' ? 'active': '' ?>">
        <a class="nav-link dropdown-toggle" href="#" id="pagesDropdown" role="button" data-toggle="dropdown" aria-haspopup="true"
            aria-expanded="false">
            <i class="fas fa-fw fa-address-book"></i>
            <span>Penanggung Jawab</span>
        </a>
        <div class="dropdown-menu" aria-labelledby="pagesDropdown">
            <a class="dropdown-item" href="<?php echo site_url('admin/devisi/add') ?>">New P. J.</a>
            <a class="dropdown-item" href="<?php echo site_url('admin/devisi') ?>">List P. J.</a>
        </div>
    </li>
    <li class="nav-item <?php echo $this->uri->segment(2) == 'kepanitiaan' ? 'active': '' ?>">
        <a class="nav-link" href="<?php echo site_url('admin/kepanitiaan') ?>">
            <i class="fas fa-fw fa-boxes"></i>
            <span>Kepanitiaan</span>
        </a>
    </li>
    <li class="nav-item <?php echo $this->uri->segment(2) == 'guide' ? 'active': '' ?>">
        <a class="nav-link" href="<?php echo site_url('admin/guide') ?>">
            <i class="fas fa-fw fa-cog"></i>
            <span>Guide</span>
        </a>
    </li>
</ul>
```

Pada kode di atas, kita menggunakan segment URI untuk mengecek apakah menu itu sedang dibuka atau tidak.

Jika menu sedang dibuka, maka tambahkan class `active`.

Misalnya ini:

```php
<?php echo $this->uri->segment(2) == 'staff' ? 'active': '' ?>">
```

Kode ini akan mengecek, apakah halaman `/admin/staff` sedang dibuka atau tidak.

Oya, halaman untuk menu **_staff_**, **_kepanitiaan_**, dan **_devisi_** belum kita buat. Insya’allah di tutorial berikutnya akan kita buat.

# Partial `broadcrump.php`

Partial ini berisi kode untuk menampilkan _breadcrumb_. Breadcrumbs adalah sebuah link navigasi yang menampilkan link halaman sebelumnya dari halaman tempat kita berada.

Berikut ini kode untuk parital breadcrumb.php:

```html
<ol class="breadcrumb">
<?php foreach ($this->uri->segments as $segment): ?>
	<?php 
		$url = substr($this->uri->uri_string, 0, strpos($this->uri->uri_string, $segment)) . $segment;
		$is_active =  $url == $this->uri->uri_string;
	?>
	<li class="breadcrumb-item <?php echo $is_active ? 'active': '' ?>">
		<?php if($is_active): ?>
			<?php echo ucfirst($segment) ?>
		<?php else: ?>
			<a href="<?php echo site_url($url) ?>"><?php echo ucfirst($segment) ?></a>
		<?php endif; ?>
	</li>
<?php endforeach; ?>
</ol>
```

# Partial `scrolltop.php`

Partial ini berisi kode untuk tombol _scrolltop_. Berikut ini isinya:

```html
<a class="scroll-to-top rounded" href="#page-top">
	<i class="fas fa-angle-up"></i>
</a>
```

# Partial `footer.php`

Partial ini berisi kode untuk bagian footer, berikut ini isi kode untuk partial footer.php:

```html
<footer class="sticky-footer">
  <div class="container my-auto">
    <div class="copyright text-center my-auto">
      <span>Copyright © <?php echo SITE_NAME ." ". Date('Y') ?></span>
    </div>
  </div>
</footer>
```

Pada kode partial `footer.php`, kita menggunakan konstanta `SITE_NAME` untuk menampilkan nama website. Lalu menggunakan fungsi `Date('Y')` untuk menampilkan tahun saat ini.

# Partial `modal.php`

Partial ini berisi kode-kode untuk _modal_. Berikut ini isinya:

```html
<div class="modal fade" id="logoutModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Ready to Leave?</h5>
        <button class="close" type="button" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">×</span>
        </button>
      </div>
      <div class="modal-body">Select "Logout" below if you are ready to end your current session.</div>
      <div class="modal-footer">
        <button class="btn btn-secondary" type="button" data-dismiss="modal">Cancel</button>
        <a class="btn btn-primary" href="login.html">Logout</a>
      </div>
    </div>
  </div>
</div>

<!-- Logout Delete Confirmation-->
<div class="modal fade" id="deleteModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Are you sure?</h5>
        <button class="close" type="button" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">×</span>
        </button>
      </div>
      <div class="modal-body">Data yang dihapus tidak akan bisa dikembalikan.</div>
      <div class="modal-footer">
        <button class="btn btn-secondary" type="button" data-dismiss="modal">Cancel</button>
        <a id="btn-delete" class="btn btn-danger" href="#">Delete</a>
      </div>
    </div>
  </div>
</div>
```

Kita juga nanti bisa tambahkan beberapa modal di sini.

# Partial `js.php`

Partial ini berisi kode-kode untuk me-load _Javascript_. Berikut ini kode untuk js.php:

```html
<script src="<?php echo base_url('assets/jquery/jquery.min.js') ?>"></script>
<script src="<?php echo base_url('assets/bootstrap/js/bootstrap.bundle.min.js') ?>"></script>

<!-- Core plugin JavaScript-->
<script src="<?php echo base_url('assets/jquery-easing/jquery.easing.min.js') ?>"></script>

<!-- Page level plugin JavaScript-->
<script src="<?php echo base_url('assets/chart.js/Chart.min.js') ?>"></script>
<script src="<?php echo base_url('assets/datatables/jquery.dataTables.js') ?>"></script>
<script src="<?php echo base_url('assets/datatables/dataTables.bootstrap4.js') ?>"></script>
<!-- Custom scripts for all pages-->
<script src="<?php echo base_url('js/sb-admin.min.js') ?>"></script>
<!-- Demo scripts for this page-->
<script src="<?php echo base_url('js/demo/datatables-demo.js') ?>"></script>
<script src="<?php echo base_url('js/demo/chart-area-demo.js') ?>"></script>
```

Kita juga nanti bisa tambahkan beberapa kode javascript di sini.

# Menggunakan Partials pada Template

Kita sudah membuat semua partial yang dibutuhkan:

![_partials](https://drive.google.com/uc?export=view&id=1v3xXkAC8c5pYsSacZkDuyM9t74u-S_oi)

Langkah berikutnya, kita harus menggunakannya dalam template.

Silahkan ubah isi `views/admin/overview.php`

<details>
  <summary>Sehingga file `overview.php` akan terisi seperti ini: (*klik untuk lihat)</summary>
  <!-- have to be followed by an empty line! -->
## overview.php
```html
<!DOCTYPE html>
<html lang="en">

<?php $this->load->view("admin/_partials/head.php") ?>

<body id="page-top">

<?php $this->load->view("admin/_partials/navbar.php") ?>

<div id="wrapper">

	<?php $this->load->view("admin/_partials/sidebar.php") ?>

	<div id="content-wrapper">

		<div class="container-fluid">

        <!-- 
        karena ini halaman overview (home), kita matikan partial breadcrumb.
        Jika anda ingin mengampilkan breadcrumb di halaman overview,
        silahkan hilangkan komentar (//) di tag PHP di bawah.
        -->
		<?php //$this->load->view("admin/_partials/breadcrumb.php") ?>

        <!-- Icon Cards-->
        <div class="row">
          <div class="col-xl-3 col-sm-6 mb-3">
            <div class="card text-white bg-primary o-hidden h-100">
              <div class="card-body">
                <div class="card-body-icon">
                  <i class="fas fa-fw fa-comments"></i>
                </div>
                <div class="mr-5">26 New Messages!</div>
              </div>
              <a class="card-footer text-white clearfix small z-1" href="#">
                <span class="float-left">View Details</span>
                <span class="float-right">
                  <i class="fas fa-angle-right"></i>
                </span>
              </a>
            </div>
          </div>
          <div class="col-xl-3 col-sm-6 mb-3">
            <div class="card text-white bg-warning o-hidden h-100">
              <div class="card-body">
                <div class="card-body-icon">
                  <i class="fas fa-fw fa-list"></i>
                </div>
                <div class="mr-5">11 New Tasks!</div>
              </div>
              <a class="card-footer text-white clearfix small z-1" href="#">
                <span class="float-left">View Details</span>
                <span class="float-right">
                  <i class="fas fa-angle-right"></i>
                </span>
              </a>
            </div>
          </div>
          <div class="col-xl-3 col-sm-6 mb-3">
            <div class="card text-white bg-success o-hidden h-100">
              <div class="card-body">
                <div class="card-body-icon">
                  <i class="fas fa-fw fa-shopping-cart"></i>
                </div>
                <div class="mr-5">123 New Orders!</div>
              </div>
              <a class="card-footer text-white clearfix small z-1" href="#">
                <span class="float-left">View Details</span>
                <span class="float-right">
                  <i class="fas fa-angle-right"></i>
                </span>
              </a>
            </div>
          </div>
          <div class="col-xl-3 col-sm-6 mb-3">
            <div class="card text-white bg-danger o-hidden h-100">
              <div class="card-body">
                <div class="card-body-icon">
                  <i class="fas fa-fw fa-life-ring"></i>
                </div>
                <div class="mr-5">13 New Tickets!</div>
              </div>
              <a class="card-footer text-white clearfix small z-1" href="#">
                <span class="float-left">View Details</span>
                <span class="float-right">
                  <i class="fas fa-angle-right"></i>
                </span>
              </a>
            </div>
          </div>
        </div>

        <!-- Area Chart Example-->
        <div class="card mb-3">
          <div class="card-header">
            <i class="fas fa-chart-area"></i>
            Area Chart Example</div>
          <div class="card-body">
            <canvas id="myAreaChart" width="100%" height="30"></canvas>
          </div>
          <div class="card-footer small text-muted">Updated yesterday at 11:59 PM</div>
        </div>

		</div>
		<!-- /.container-fluid -->

		<!-- Sticky Footer -->
		<?php $this->load->view("admin/_partials/footer.php") ?>

	</div>
	<!-- /.content-wrapper -->

</div>
<!-- /#wrapper -->


<?php $this->load->view("admin/_partials/scrolltop.php") ?>
<?php $this->load->view("admin/_partials/modal.php") ?>
<?php $this->load->view("admin/_partials/js.php") ?>
    
</body>
</html>
```
</details>

Pada kode template tersebut, kita me-load partial dengan fungsi `$this->load->view()`.

Maka hasilnya akan seperti ini:
![overviewnew](https://drive.google.com/uc?export=view&id=168OUlj8dO2xPH5b-Ww6RKMgKLVUOyUBN)

Mantul..

oh iya pada gambar diatas sudah terdapat chart yang terhubung dengan database.. kita akan membahas cara membuat chart setelah kiata belajar membuat CRUD pada codeigniter
bagi kalian yang ingin full source code dari Sistem Manegement Keapanitiaan ini:
🎁 [Download Source Code SIMKEP](https://kos-it.github.io/projects/projek-sistem-menejement-kepanitiaan/)

# Apa Selanjutnya?

Sepertinya masalah template sudah selesai. Kalian juga bisa mengembangkannya sesuai kreasi sendiri.

Silahkan pelajari Bootstrap untuk mengetahui class-class CSS yang dapat digunakan.

Berikutnya kita bisa mulai membuat CRUD 

 * [Tutorial SIMKEP dengan Codeiniter #5: (Model) Membuat CRUD yang Baik](https://kos-it.github.io/post/tutorial-projek-1-bagian-5/)
 * [Tutorial SIMKEP dengan Codeiniter #6: Membuat Fitur Login](https://kos-it.github.io/post/tutorial-projek-1-bagian-6/)
 * [Tutorial SIMKEP dengan Codeiniter #7: Membuat Fitur Upload Gambar](https://kos-it.github.io/post/tutorial-projek-1-bagian-7/)
 * Tutorial SIMKEP dengan Codeiniter #8: Membuat Fitur Pencarian (Admin)
 * Tutorial SIMKEP dengan Codeiniter #9: Membuat Template untuk Landing Page
 * Tutorial SIMKEP dengan Codeiniter #10: Membuat Pagination
 * Tutorial SIMKEP dengan Codeiniter #11: Cara Menggunakan Databales dan Optimasi
 * Tutorial SIMKEP dengan Codeiniter #12: Cara Membuat Laporan dengan DomPDF

# Tutorial Sebelumnya :

 * [Tutorial SIMKEP dengan Codeiniter #1 : Pengenalan Codeigniter](https://kos-it.github.io/post/tutorial-projek-1-bagian-1/)
 * [Tutorial SIMKEP dengan Codeiniter #2: (Controller) MVC dan Routing, Konsep dasar CI yang Harus Dipahami](https://kos-it.github.io/post/tutorial-projek-1-bagian-2/)
 * [Tutorial SIMKEP dengan Codeiniter #3: (View) Cara Menggunakan Bootstrap pada Codeiniger](https://kos-it.github.io/post/tutorial-projek-1-bagian-3/)
