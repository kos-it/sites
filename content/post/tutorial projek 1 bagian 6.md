---
title: "Tutorial SIMKEP dengan Codeiniter #6: Membuat Fitur Login"
date: 2020-09-27T07:10:00+08:00
categories: ["Website"]
tags: ["Tutorial Project - 1", "Website", "PHP", "Codeigniter"]
cover: "https://drive.google.com//uc?export=view&id=1zKgyxiCm9R2RlIFO8O1cbknZGUN8NrRC"
---

Rencananya:

Pada aplikasi yang kita buat ini, akan ada dua jenis user yang bisa login, yakni admin dan staff.

Kita juga nanti akan membuat halaman khusus untuk staff.

Tapi…

Untuk saat ini, kita fokus dulu mengerjakan halaman admin.

Karena adminlah yang akan berperan pertama kali untuk menginput data staff dan data lainnya.

Baiklah, kita langsung saja masuk ke tutorial.

Jadi, berikut ini langkah-langkah yang harus kita kerjakan untuk membuat fitur login:

> 1. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Tabel `users` pada Database
2. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Model `User_model.php`
3. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Controller `User.php`
4. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Halaman View untuk Login
5. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Ujicoba Login

Mari kita Mulai
<hr>

# 1. Membuat Tabel untuk Users

Pertama kita membutuhkan sebuah tabel untuk menyimpan data user.

Silahkan buka Phpmyadmin, kemudian buatlah tabel bernama `users` dengan `11` kolom.

![tutor6_1](https://drive.google.com/uc?export&id=1Pc9uSd5kkvNAWNkRic8QgSBMgItuixbR)

Kemudian, buat skema tabelnya seperti di bawah ini :

![tutor6_2](https://drive.google.com/uc?export&id=16YXjRqkotVB0BHNs3Ft1FEd27vkR2DjN)

kalau mau cepat.. kamu bisa juga membuat tabel `users` dnegan perintah SQL ini :

```sql
CREATE TABLE `users` (
  `user_id` int(11) NOT NULL AUTO_INCREMENT,
  `username` varchar(64) NOT NULL,
  `password` varchar(255) NOT NULL,
  `email` varchar(255) NOT NULL,
  `full_name` varchar(255) NOT NULL,
  `phone` varchar(20) NOT NULL,
  `role` enum('admin','staff') NOT NULL DEFAULT 'staff',
  `last_login` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP,
  `photo` varchar(64) NOT NULL DEFAULT 'default.jpg',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP,
  `is_active` tinyint(1) NOT NULL DEFAULT '0',
  PRIMARY KEY (`user_id`)
);
```

Jika kamu sudah membuat tabel, sekarang coba perhatikan kolom-kolomnya.

Sebenarnya, kita hanya butuh tiga kolom untuk membuat login `user_id`, `username`, dan `password`.

Tapi karena tabel `users` akan kita gunakan untuk menampung data lengkap dari user, kita membutuhkan beberapa kolom lagi, yakni:

* `email` untuk menyimpan email user, agar bisa kita hubungi apabila ia meminta untuk reset password 
* `full_name` untuk nama lengkap user
* `phone` untuk nomer telepon, yang bisa kita manfaatkan juga untuk SMS OTP atau 2FA
* `role` untuk membedakan user admin dan staff
* `last_login` untuk mencatat kapan terakhir user login
* `photo` untuk menyimpan foto dari user
* `created_at` untuk mencatat kapan user tersebut dibuat
* `is_active` untuk menyatakan user tersebut aktif atau tidak (sudah verifikasi email atau belum).

Kalau mau ditambahkan kolom lain juga boleh kok…

Tapi khusus untuk tutorial ini, kita pakai kolom ini aja ya.

Sebelum kita lanjut ke langkah berikutnya, kita butuh satu hal lagi nih di database.

Apa itu?

Sebuah user baru.

Kita anggap saja ini adalah user pertama yang akan kita pakai untuk uji coba aplikasi.

Cara buatnya gimana?

Cara buatnya, tinggal insert data ke tabel users.

Gampang kan?

Mari kita buat.

Masuk ke menu _Insert/Tambahkan_, kemudian isi data user seperti ini:

![tutor6_3](https://drive.google.com/uc?export&id=1HpEwCdlgeNuMGDArIuugJebblTRvNaJj)

Nah untuk `password`, silahkan isi dengan hash yang dibuat dengan fungsi `password_hash()`.

Kamu bisa buat dengan membuat file `index.php`, kemudian kamu jalankan di browser. dengan isi sebagai berikut :
```php
<?php
echo password_hash("admin", PASSWORD_DEFAULT);
?>
```
hasilnya..

![tutor6_4](https://drive.google.com/uc?export&id=1uEQABqW5GYg6WJQhjSzcpboRAc6n0P-P)

Perlu diketahui `password_hash()` akan membuat enkripsi satu arah, dengan kata lain password yang telah dienkripsi tidak dapat dikembalikan menjadi plain text.
Kalau kamu mau membalikkan hashing ke plain text coba aja cari di internet, dan jangan lupa algoritma apa yang dipakai MD5, SHA, DES, Bcrypt, Bluefish dll.

ok lanjut.. Kalau sudah, kita akan memiliki user pertama dengan `user_id` adalah `1`.

![tutor6_5](https://drive.google.com/uc?export&id=1oP2yjyrYGYUBo1_LHk30YF4vb_2ecWUB)

Mengapa sih password harus disimpan dalam bentuk hash?

Ini untuk keamanan, jika suatu saat ada orang yang berhasil membobol aplikasimu. Maka Si pembobol nggak akan tahu password-nya.

Oke dengan begini, tugas pertama kita selesai.

> 1. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Tabel `users` pada Database</s>
2. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Model `User_model.php`
3. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Controller `User.php`
4. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Halaman View untuk Login
5. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Ujicoba Login

Lanjur ke langkah berikutnya..

# 2. Membuat Model User

Silahkan buat model baru di dalam folder `application/models/` dengan nama `User_model.php`.

Kemudian isi dengan kode berikut:

<details>
  <summary> `User_model.php` (*klik untuk lihat)</summary>
  <!-- have to be followed by an empty line! -->
```php
<?php

class User_model extends CI_Model
{
    private $_table = "users";

    public function doLogin(){
		$post = $this->input->post();

        // cari user berdasarkan email dan username
        $this->db->where('email', $post["email"])
                ->or_where('username', $post["email"]);
        $user = $this->db->get($this->_table)->row();

        // jika user terdaftar
        if($user){
            // periksa password-nya
            $isPasswordTrue = password_verify($post["password"], $user->password);
            // periksa role-nya
            $isAdmin = $user->role == "admin";

            // jika password benar dan dia admin
            if($isPasswordTrue && $isAdmin){ 
                // login sukses yay!
                $this->session->set_userdata(['user_logged' => $user]);
                $this->_updateLastLogin($user->user_id);
                return true;
            }
        }
        
        // login gagal
		return false;
    }

    public function isNotLogin(){
        return $this->session->userdata('user_logged') === null;
    }

    private function _updateLastLogin($user_id){
        $sql = "UPDATE {$this->_table} SET last_login=now() WHERE user_id={$user_id}";
        $this->db->query($sql);
    }

}
```
</details>

Perhatikan kode di atas!

Ada tiga method yang kita buat:

1. Method `doLogin()` untuk melakukan login
![tutor6_6](https://drive.google.com/uc?export&id=12v_p6ldsOTQnTQSEHSP4H6OS_2-LhEFD)
2. Method `isNotLogin()` untuk mengecek status, apakah sudah login atau belum
3. Method `_updateLastLogin()` untuk mengupdate tanggal dan waktu login terakhir

Sebenarnya ada beberapa method lagi yang perlu kita tambahkan, yakni `add()`, `update()`, dan `delete()`.

Tapi nanti saja kita buat, saat membuat fitur manajemen user.

Baik, dengan begini tugas kedua kita sudah selesai…

> 1. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Tabel `users` pada Database</s>
2. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Model `User_model.php`</s>
3. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Controller `User.php`
4. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Halaman View untuk Login
5. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Ujicoba Login

…lnajut ke langkah berikutnya:

# 3. Membuat Controller Login

Silahkan membuat controller baru, di dalam folder `controllers/admin/` dengan nama `Login.php`…

…kemudian isi dengan kode berikut:

<details>
  <summary> `Login.php` (*klik untuk lihat)</summary>
  <!-- have to be followed by an empty line! -->
```php
<?php

class Login extends CI_Controller
{
    public function __construct()
    {
        parent::__construct();
        $this->load->model("user_model");
        $this->load->library('form_validation');
    }

    public function index()
    {
        // jika form login disubmit
        if($this->input->post()){
            if($this->user_model->doLogin()) redirect(site_url('admin'));
            $this->session->set_flashdata('failed', 'username atau password anda salah');
        }

        // tampilkan halaman login
        $this->load->view("admin/login_page.php");
    }

    public function logout()
    {
        // hancurkan semua sesi
        $this->session->sess_destroy();
        redirect(site_url('admin/login'));
    }
}
```
</details>

Setelah membaut controller Login…

Berikutnya kita harus edit controller yang lain untuk mengecek apakah user sudah login atau belum.

1. `controller/admin/Overview.php`
2. `controller/admin/Staff.php`
3. `controller/admin/Devisi.php`
4. `controller/admin/Kepanititaan.php`
5. dan tentunya disemua controller yang akan kita tambahkan nantinya dan hanya bisa diakses oleh user

Lalu, tambahkan kode ini di dalam konstruktor di setiap Controller:

```php
$this->load->model("user_model");
if($this->user_model->isNotLogin()) redirect(site_url('admin/login'));
```

Sebagai contoh controller Overview.php akan menjadi seperti ini:

![tutor6_9](https://drive.google.com/uc?export&id=1oT0vPXXv12H-YIEIQ_2NlGyxwVeZnjol)

Intinya, kita harus menambahkan kode tersebut pada halaman atau controller yang memerlukan login untuk mengaksesnya.

Nah, dengan begini.. urusan kita dengan controller sudah selesai.

> 1. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Tabel `users` pada Database</s>
2. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Model `User_model.php`</s>
3. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Controller `User.php`</s>
4. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Halaman View untuk Login
5. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Ujicoba Login

Tinggal satu hal lagi yang belum kita kerjakan, yaitu:

# 4. Membuat View untuk Halaman Login

Buatlah file baru di dalam folder `application/views/admin/` dengan nama `login_page.php`

Kemudian isi dengan kode berikut:

<details>
  <summary> `login_page.php` (*klik untuk lihat)</summary>
  <!-- have to be followed by an empty line! -->
```html
<!DOCTYPE html>
<html lang="en">

<head>
<?php $this->load->view("admin/_partials/head.php") ?>
</head>

<body class="bg-dark">

  <div class="container">
    <div class="card card-login mx-auto mt-5">
      <div class="card-header">Login</div>
      <?php 
      if ($this->session->flashdata('failed')): ?>
		<div class="alert alert-warning" role="alert">
		<?php echo $this->session->flashdata('failed'); ?>
		</div>
    	<?php endif; ?>
      <div class="card-body">
      <form action="<?= site_url('admin/login') ?>" method="POST">
          <div class="form-group">
            <div class="form-label-group">
              <input type="text" name="email" id="inputEmail" class="form-control" placeholder="Email address or Username" required="required" autofocus="autofocus">
              <label for="inputEmail">Email address or Username</label>
            </div>
          </div>
          <div class="form-group">
            <div class="form-label-group">
              <input type="password" name="password" id="inputPassword" class="form-control" placeholder="Password" required="required">
              <label for="inputPassword">Password</label>
            </div>
          </div>
          <div class="form-group">
            <div class="checkbox">
              <label>
                <input type="checkbox" value="remember-me">
                Remember Password
              </label>
            </div>
          </div>
          <input type="submit" class="btn btn-primary btn-block" value="Login" />
        </form>
        <div class="text-center">
          <a class="d-block small mt-3" href="register.html">Register an Account</a>
          <a class="d-block small" href="forgot-password.html">Forgot Password?</a>
        </div>
      </div>
    </div>
  </div>

  <!-- Bootstrap core JavaScript-->
  <script src="<?php echo base_url('assets/jquery/jquery.min.js') ?>"></script>
  <script src="<?php echo base_url('assets/bootstrap/js/bootstrap.bundle.min.js') ?>"></script>

  <!-- Core plugin JavaScript-->
  <script src="<?php echo base_url('assets/jquery-easing/jquery.easing.min.js') ?>"></script>

</body>

</html>
```
</details>

Berikutnya, kita harus membuat link untuk logout.

Silahkan buka file `views/admin/_partials/modal.php`, kemudian ubah alamat link Logout.

Dari kode ini:
```php
<a class="btn btn-primary" href="login.html">Logout</a>
```

Ubah menjadi :
```php
<a class="btn btn-primary" href="<?= site_url('admin/login/logout') ?>">Logout</a>
```

Sehingga akan menjadi seperti ini:

![tutor6_10](https://drive.google.com/uc?export&id=1PIPGXnhwv7FVsZ-epDib3e6KIgooReyT)

Akhirnya, selesai.. yay! 🎉

> 1. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Tabel `users` pada Database</s>
2. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Model `User_model.php`</s>
3. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Controller `User.php`</s>
4. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Halaman View untuk Login</s>
5. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Ujicoba Login

Tapi jangan senang dulu, karena ini belum kita coba.

Mungkin saja akan ada error.

Karena itu, mari kita lakukan:

# Uji Coba Fitur Login

Untuk percobaan pertama, silahkan buka halaman `http://localhost/simkep/index.php/admin/`.

Jika kamu diarahkan ke halaman login, maka artinya autentikasi untuk halaman tersebut sudah berhasil.

Sekarang coba login…

![tutor6_11](https://drive.google.com/uc?export&id=1oAMy2qAnOVhiXJRi2SeKiNXrCRmd0zUq)

Jika berhasil, maka akan diarahkan ke halaman admin.

![tutor6_12](https://drive.google.com/uc?export&id=1MYhp-041sv2XFVOntaIYjwLuBQOaslgq)

Sukses!

Fitur Login sudah kita buat… 🎉

> 1. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Tabel `users` pada Database</s>
2. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Model `User_model.php`</s>
3. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Controller `User.php`</s>
4. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Halaman View untuk Login</s>
5. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Ujicoba Login</s>

Oh iya, source code untuk tutorial ini dapat kamu download di Github.

[⬇️ Download Source Code](http://kos-it.github.io)

# Apa Selanjutnya?

Kita baru saja membuat fitur login untuk admin. Fitur ini akan digunakan untuk autentikasi halaman admin.

Namun ada beberapa bagian yang belum kita buat, seperti Remember Me agar admin bisa tetap login dan Lupa Password? untuk reset password.

Kita akan lanjutkan ini nanti ya…

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
 * [Tutorial SIMKEP dengan Codeiniter #4: (View) Membuat Template Admin](https://kos-it.github.io/post/tutorial-projek-1-bagian-4/)
 * [Tutorial SIMKEP dengan Codeiniter #5: (Model) Membuat CRUD yang Baik](https://kos-it.github.io/post/tutorial-projek-1-bagian-5/) 

