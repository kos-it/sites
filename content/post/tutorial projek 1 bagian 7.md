---
title: "Tutorial SIMKEP dengan Codeiniter #7: Membuat Fitur Upload File"
date: 2020-10-02T21:10:00+08:00
categories: ["Website"]
tags: ["Tutorial Project - 1", "Website", "PHP", "Codeigniter"]
cover: "https://drive.google.com//uc?export=view&id=1zKgyxiCm9R2RlIFO8O1cbknZGUN8NrRC"
---

Pada tutorial sebelumnya, kita sudah menyelesaikan fitur CRUD. Ini merupakan fitur utama yang harus ada di dalam aplikasi.

Tetapi, masih ada yang kurang…

Apa itu?

Gambar atau photo untuk staff, ini sebenarnya opsional. Kalian bisa memilih ingin menambahkannya atau tidak.

Jika kalian ingin menambahkannya langsung saja kita ketutorialnya

Pada tutorial kali ini kita akan mengubah dan menambahkan sedikit pada CRUD(_Create, Read, Update and Delete_) yang telah kiata buat pada [tutorial 5 sebelumnya](https://kos-it.github.io/post/tutorial-projek-1-bagian-5/)

Oke, langsung saja tahap pertama yang perlu kita lakukan

# 1. Membuat folder Image
Silahkan buat sebuah folder baru pada folder projek kita dengan nama `upload`, lalu di dalamnya berisi folder lagi bernama `staff` (`simkep/upload/staff`).

![tutor7_0](https://drive.google.com/uc?expand&id=1eFkx4vuJXA7iRpKlB9fXkewZOBJGFvtk)

Folder ini akan menyimpan file foto yang akan kita upload nantinya

# 2. Menambah Kolom Foto pada Tabel Staff
kita akan menambah kolom/field dari Tabel `staff` pada Database `simkep` yang telah kita buat, kolom baru ini bertujuan untuk menampung nama file foto dari staff. 

Ok langsung saja kita buat 

Silahkan buka PHPMyadmin, expand database `simkep` kemudia pilih tabel `staff` lalu pada menu tab pilih `stuktur`, tambahkan satu kolom setelah/after `no_absen`.

![tutor7_1](https://drive.google.com/uc?expand&id=1_vWCx_xlhkaDtgfzqKKSkN_0-QIPHIVP)

Sebenarnya kolom baru ini dapat kita simpan dimana saja, tapi untuk estetika ea.. haha kita akan buat setelah `no_absen` dan atau sebelum `name`.

Ok lanjut selanjutnya isikan nama kolom dengan `foto` dengan type srting `varchar` dan panjang `255` kemudian untuk default/bawaan isikan denga as definied/seperti yang didefinisiakn lalu isi kolom yang muncul dengan `default.jpg` fungsi ini adalah untuk mengisi kolom secara otomatis dengan `default.jpg` jika form yang disi tidak menyertakan foto yang akan diupload.. dan seluruh data yang telah ada, sehingga kita tidak perlu repot update data yang telah ada sebelumnya.. untuk jelasnya perthatikan gambar dibawah...

![tutor7_2](https://drive.google.com/uc?expand&id=1AKM91-m3Knz_PXL4xbfIL7LtVzPy01qd)

Terakhik klik save/simpan untuk menyimpan

sehingga kita sekarang punya tabel `staff` dengan strutktur sebagai berikut :

![tutor7_3](https://drive.google.com/uc?expand&id=1h9yFZPPlnx52X5IFYLEhZh8usPnMlKNn)

kode SQL nya :

```sql
ALTER TABLE staff ADD foto varchar(255) NOT NULL DEFAULT 'default.jpg' AFTER no_absen;
```

Berikutnya, kita akan menambah kode untuk `Staff_model.php`.

# 3. Mengedit Staff_model.php
Selanjutnya kita akan mulai mengedit kode untuk `Staff_model.php` dan menambahkan fitur upload file, yang berada di `application/model/Staff_model.php`

Namun sebelum kita membuat fitur upload, kita perlu pahami dulu bagaimana konsep kerjanya.

Upload file memiliki alur proeses seperti ini:

1. User mengirim file melalui form
2. File di-upload ke server dan disimpan dalam folder tmp dulu
3. Kita pindahkan file yang ada di direktori tmp ke dalam direktori `upload/staff/` yang sudah kita buat
4. Selesai.

Terdengar sederhana…

Tapi mari kita lihat dalam prekteknya.

Silahkan buka model `Staff_model.php`, kemudian tambahakan method `_uploadImage()` tepat di bawah method `delete()`.

Berikut ini isi kode method `_uploadImage()`:

```php
private function _uploadImage()
{
    $config['upload_path']          = './upload/staff/';
    $config['allowed_types']        = 'gif|jpg|png';
    $config['file_name']            = $this->staff_id;
    $config['overwrite']			= true;
    $config['max_size']             = 1024; // 1MB
    // $config['max_width']            = 1024;
    // $config['max_height']           = 768;

    $this->load->library('upload', $config);

    if ($this->upload->do_upload('foto')) {
        return $this->upload->data("file_name");
    }
    
    return "default.jpg";
}
```

sehingga `Staff_model.php` akan menjadi seperti ini

![tutor7_4](https://drive.google.com/uc?expand&id=1eXGzB0Uz8q5f2E4dIJga_7V5-8_dh8y_)

Apa yang dilakuakn oleh method ini?

Sederhana…

1. Kita membuat konfigurasi untuk upload file seperti:
    * `upload_path` untuk menentukan alamat lokasi file akan terupload
    * `file_name` untuk menentukan nama filenya, nama file akan kita ambil dari ID staff. Karena itu, kita mengisinya dengan $this->staff_id.
    * `overwrite` untuk menindih file yang sudah ter-upload saat di-upload file baru (edit data).
    * `allowed_types` untuk membatasi tipe file yang boleh di-upload.
    * `max_size` untuk menentukan batasan ukuran file.
    * `max_wdith` dan `max_height` sengaja saya komentari agar tidak diaktifkan. Ini fungsinya untuk membatasi ukuran lebar dan tinggi image. Apabila image yang di-upload melebihi dari ukuran yang ditetapkan, maka upload akan gagal.
2. Kita me-load library `upload` dengan konfigurasi yang sudah ditentukan
3. Kita akan mengembalikan nama file yang sudah di-upload. Apabila upload gagal, maka kembalikan saja `default.jpg`

Mengapa method ini diberikan modifier `private`?

Bukankah nanti kita akan memanggilnya dari _Controller_?

Oh tidak-tidak…

Kita tidak akan memanggil method ini dari _Controller_. Karena itu, kita memberikan modifier `priavate`.

Method ini nanti akan dipanggil dari class `Staff_model` (class itu sendiri), pada method `save()` dan `update()`.

Nah, sekarang tugas kita adalah mengubah method `save()` dan `update()`.

Penggunaan `_uploadImage()` pada method `save()` dan `update()` digunakan untuk mengisi properti `$this->foto`.

Silahkan ubah method `save()` dan `update()` menjadi seperti ini:

![tutor7_5](https://drive.google.com/uc?expand&id=1KeAcEaKBQEHpxRltLeLCDHP3OvEfcU82)

Khusus untuk method `update()`, kita membuat pengecekan seperti ini:

```php
if (!empty($_FILES["foto"]["name"])) {
    $this->foto = $this->_uploadImage();
} else {
    $this->foto = $post["old_foto"];
}
```

Artinya, jika ada file yang di-upload saat mengedit data, maka upload file-nya.

Tapi kalau tidak ada, cukup gunakan nama file yang sudah ada (old_foto).

Nilai `old_foto` kita dapatkan dari form, karena pada `edit_form.php` kita akan membuat field ini dengan tipe hidden.

Selanjutnya kiata akan melakukan penambahan code pada bagian `view` namun sebelum itu tugas kita pada bagian `Staff_model` belum selesai..

Apa lagi.. ?

Kita belum mendefinisikan variabel `foto` yang kita gunakan pada method `save()` dan `edit()`

Silahkan perhtaikan bagian ini:

![tutor7_6](https://drive.google.com/uc?expand&id=1KC8AVZ-d_gakguxSwjLbJF-ieCkQ3N0J)

Kita menambahkan deklarasi variabel `$foto` dengan value/nilai `default.jpg`

Kita langsung mengisi nilainya dengan `default.jpg`. Ini nanti akan menjadi nilai default-nya, sebenarnya kita bisa saja tidak isi demikian. Karena di tabel sudah kita berikan nilai default-nya.

sehingga keseluruhan file `Staff_model.php` akan menjadi seperti ini :

<details>
  <summary> `Staff_model.php` (*klik untuk lihat)</summary>
  <!-- have to be followed by an empty line! -->
```php
<?php defined('BASEPATH') OR exit('No direct script access allowed');

class Staff_model extends CI_Model
{
    private $_table = "staff";

    // nama kolom di tabel, harus sama huruf besar dan huruf kecilnya!
    public $staff_id;
    public $no_absen;
    public $foto = "default.jpg";
    public $name;
    public $status;
    public $jabatan;
    public $keterangan;

    public function rules()
    {
        return [

            ['field' => 'absen',
            'label' => 'Absen',
            'rules' => 'numeric'],

            ['field' => 'name',
            'label' => 'Name',
            'rules' => 'required'],

            ['field' => 'status',
            'label' => 'Status',
            'rules' => 'required'],
            
            ['field' => 'jabatan',
            'label' => 'Jabatan',
            'rules' => 'required'],

        ];
    }

    public function getAll()
    {
        return $this->db->get($this->_table)->result();
    }
    
    public function getById($id)
    {
        return $this->db->get_where($this->_table, ["staff_id" => $id])->row();
    }

    public function save()
    {
        $post = $this->input->post();
        $this->staff_id = uniqid();
        $this->no_absen = $post["absen"];
        $this->foto = $this->_uploadImage();
        $this->name = $post["name"];
        $this->status = $post["status"];
        $this->jabatan = $post["jabatan"];
        $this->keterangan = $post["keterangan"];
        $this->prioritas = '100';
        $this->db->insert($this->_table, $this);
    }

    public function update()
    {
        $post = $this->input->post();
        $this->staff_id = $post["id"];
        $this->no_absen = $post["absen"];
        if (!empty($_FILES["foto"]["name"])) {
            $this->foto = $this->_uploadImage();
        } else {
            $this->foto = $post["old_foto"];
        }
        $this->name = $post["name"];
        $this->status = $post["status"];
        $this->jabatan = $post["jabatan"];
        $this->keterangan = $post["keterangan"];
        $this->db->update($this->_table, $this, array('staff_id' => $post['id']));
    }

    public function delete($id)
    {
        return $this->db->delete($this->_table, array("staff_id" => $id));
    }

    private function _uploadImage()
    {
    $config['upload_path']          = './upload/staff/';
    $config['allowed_types']        = 'gif|jpg|png';
    $config['file_name']            = $this->staff_id;
    $config['overwrite']			= true;
    $config['max_size']             = 1024; // 1MB
    // $config['max_width']            = 1024;
    // $config['max_height']           = 768;

    $this->load->library('upload', $config);

    if ($this->upload->do_upload('foto')) {
        return $this->upload->data("file_name");
    }
    
    return "default.jpg";
    }
}
```
</details>

OK.. lanjut

# 4. Mengedit Bagian View
Bagian view yang harus kita edit adalah pada `application/views/admin/staffv` meliputi file `list.php`, `new_form.php` dan `edit_form.php`

Mari kita mulai dengan `list.php`

## Edit list.php
Silahkan buka terlebih dahulu file `list.php`-nya.. `application/views/admin/staffv/list.php`

Hal yang akan kita edit/tambahkan pada file ini adalah pada bagain data tabel.. pada penyajian tabel sebelumnya akan kita tambahkan kolom foto, Ok langsung saja..

file `list.php` akan menjadi seperti berikut 

<details>
  <summary> `list.php` (*klik untuk lihat)</summary>
  <!-- have to be followed by an empty line! -->
```html
<!DOCTYPE html>
<html lang="en">

<head>
	<?php $this->load->view("admin/_partials/head.php") ?>
</head>

<body id="page-top">

	<?php $this->load->view("admin/_partials/navbar.php") ?>
	<div id="wrapper">

		<?php $this->load->view("admin/_partials/sidebar.php") ?>

		<div id="content-wrapper">

			<div class="container-fluid">

				<?php $this->load->view("admin/_partials/breadcrumb.php") ?>

				<!-- DataTables -->
				<div class="card mb-3">
					<div class="card-header">
						<a href="<?php echo site_url('admin/staff/add') ?>"><i class="fas fa-plus"></i> Add New</a>
					</div>
					<div class="card-body">

						<div class="table-responsive">
							<table class="table table-hover" id="dataTable" width="100%" cellspacing="0">
								<thead>
									<tr>
										<th>No. Absen</th>
										<th>Foto</th>
										<th>Nama</th>
										<th>Status</th>
										<th>Jabatan</th>
										<th>Keterangan</th>
										<th>Action</th>
									</tr>
								</thead>
								<tbody>
									<?php foreach ($staff as $staffv): ?>
									<tr>
										<td>
											<?php echo $staffv->no_absen ?>
										</td>
										<td>
											<img src="<?php echo base_url('upload/staff'.$staffv->foto) ?>" width="64" />
										</td>
										<td>
											<?php echo $staffv->name ?>
										</td>
										<td>
											<?php echo $staffv->status ?>
										</td>
										<td>
											<?php echo $staffv->jabatan ?>
										</td>
										<td class="small">
											<?php echo substr($staffv->keterangan, 0, 120) ?>...</td>
										<td width="250">
											<a href="<?php echo site_url('admin/staff/edit/'.$staffv->staff_id) ?>"
											 class="btn btn-small"><i class="fas fa-edit"></i> Edit</a>
											<a onclick="deleteConfirm('<?php echo site_url('admin/staff/delete/'.$staffv->staff_id) ?>')"
											 href="#!" class="btn btn-small text-danger"><i class="fas fa-trash"></i> Hapus</a>
										</td>
									</tr>
									<?php endforeach; ?>

								</tbody>
							</table>
						</div>
					</div>
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
	<script>
	function deleteConfirm(url)
	{
		$('#btn-delete').attr('href', url);
		$('#deleteModal').modal();
	}
	</script>
</body>

</html>
```
</details>

Perhatikan bagian yang kita tambahkan :

![tutor7_7](https://drive.google.com/uc?expand&id=1-BWYZGFGISFO_8uaQUYuXteiuIbVX5c_)

Pertama pada bagian tabel head (`thead`) kita tambahkan kolom baru yakni `Foto`
kemudian pada bagian tabel body (`tbody`) kita akan meminta menampilkan gambar `img` dengan _path_ `base_url` kemudian `/upload/staff/` lalu `nama_file` (yang tersimpan di database).

sekarang mari kita coba buka http://localhost/simkep/index.php/admin/staff

maka hasilnya akan seperti gambar dibawah :

![tutor7_8](https://drive.google.com/uc?expand&id=1kLMzaUjmVhfZgTwQDNWrVXHLU4oIPV70)

Gambar staff pada path yang dituju belum ada. Sehingga akan ditampilkan _broken image_.

Gambar untuk staff, kita akan diisi dengan nilai `default.jpg`. Jika tidak ada gambar yang di-upload.

Kalau kita lihat alamat path yang dipakai, gambar ini akan berlokasi di `/upload/staff/default.jpg`.

Bagaimana cara mengatasinya?

Sederhana…

kita tinggal menaruh file gambar dengan nama `default.jpg` pada _path_ yang dimaksud

Gambar `default.jpg` akan menjadi gambar placeholder apabila tidak ada gambar yang di-upload.

Sebagai contoh, saya akan mengisinya dengan gambar logo kami seperti berikut

![tutor7_9](https://drive.google.com/uc?expand&id=1ZESrlJazKzu2wPujO8B2IuTzrxFV7uer)

Setelah itu, silahkan taruh gambar tersebut pada folder `upload/staff/`

Maka hasilnya:

![tutor7_10](https://drive.google.com/uc?expand&id=16UM5R6Ycqql1si3iSRtbgMK5ZNGrsJKo)

Bagus!

Tapi masalahanya:

Tidak semua produk akan menggunakan gambar default.jpg.

Karena itu, kita harus membuatkan fitur upload, agar admin bisa menentukan gambar yang ia sukai.

Bagaimana caranya?

Mari kita bahas…

## Edit new_form.php

Silahkan buka terlebih dahulu file `new_form.php`-nya.. `application/views/admin/staffv/new_form.php`

Hal yang akan kita edit/tambahkan pada file ini adalah pada bagain data form.. pada form akan kita tambahkan input baru yang akan berfungsi sebai tempat kita untuk mengupload file dengan menampilkan window explorer file..

```html
<div class="form-group">
	<label for="foto">Foto</label>
	<input class="form-control-file <?php echo form_error('foto') ? 'is-invalid':'' ?>"
	type="file" name="foto" />
   	<div class="invalid-feedback">
		<?php echo form_error('foto') ?>
    </div>
</div>
```

![tutor7_11](https://drive.google.com/uc?expand&id=1fdeJO_GHCyEs88ePAcPxZEmoq5XtBuow)

sehingga keseluruhan file `new_form.php` akan menjadi seperti berikut :

<details>
  <summary> `new_form.php` (*klik untuk lihat)</summary>
  <!-- have to be followed by an empty line! -->
```html
<!DOCTYPE html>
<html lang="en">

<head>
	<?php $this->load->view("admin/_partials/head.php") ?>
</head>

<body id="page-top">

	<?php $this->load->view("admin/_partials/navbar.php") ?>
	<div id="wrapper">

		<?php $this->load->view("admin/_partials/sidebar.php") ?>

		<div id="content-wrapper">

			<div class="container-fluid">

				<?php $this->load->view("admin/_partials/breadcrumb.php") ?>

				<?php if ($this->session->flashdata('success')): ?>
				<div class="alert alert-success" role="alert">
					<?php echo $this->session->flashdata('success'); ?>
				</div>
				<?php endif; ?>

				<div class="card mb-3">
					<div class="card-header">
						<a href="<?php echo site_url('admin/staff/') ?>"><i class="fas fa-arrow-left"></i> Back</a>
					</div>
					<div class="card-body">

						<form action="<?php base_url('admin/staff/add') ?>" method="post" enctype="multipart/form-data" >
							<div class="form-group">
								<label for="name">Nama*</label>
								<input class="form-control <?php echo form_error('name') ? 'is-invalid':'' ?>"
								 type="text" name="name" placeholder="Nama Staff" />
								<div class="invalid-feedback">
									<?php echo form_error('name') ?>
								</div>
							</div>

							<div class="form-group">
								<label for="absen">No. Absen*</label>
								<input class="form-control <?php echo form_error('absen') ? 'is-invalid':'' ?>"
								 type="number" name="absen" placeholder="Nomor Absen Staff" />
								<div class="invalid-feedback">
									<?php echo form_error('absen') ?>
								</div>
							</div>

							<div class="form-group">
								<label for="status">Status*</label><br/>
								<input class="form-control-1 <?php echo form_error('status') ? 'is-invalid':'' ?>"
								 type="radio" name="status" value="aktiv" checked/>Aktiv<br/>
                                 <input class="form-control-1 <?php echo form_error('status') ? 'is-invalid':'' ?>"
								 type="radio" name="status" value="nonaktiv" />Non-Aktiv<br/>
								<div class="invalid-feedback">
									<?php echo form_error('status') ?>
								</div>
							</div>


							<div class="form-group">
								<label for="jabatan">Jabatan*</label>
								<input class="form-control <?php echo form_error('jabatan') ? 'is-invalid':'' ?>"
								 type="text" name="jabatan" placeholder="Unit Kerja Staff" />
								<div class="invalid-feedback">
									<?php echo form_error('jabatan') ?>
								</div>
							</div>

							<div class="form-group">
								<label for="keterangan">Keterangan</label>
								<textarea class="form-control <?php echo form_error('keterangan') ? 'is-invalid':'' ?>"
								 name="keterangan" placeholder="Keterangan..."></textarea>
								<div class="invalid-feedback">
									<?php echo form_error('keterangan') ?>
								</div>
							</div>

							<div class="form-group">
									<label for="foto">Foto</label>
									<input class="form-control-file <?php echo form_error('foto') ? 'is-invalid':'' ?>"
										type="file" name="foto" />
									<div class="invalid-feedback">
										<?php echo form_error('foto') ?>
									</div>
							</div>

							<input class="btn btn-success" type="submit" name="btn" value="Save" />
						</form>

					</div>

					<div class="card-footer small text-muted">
						* required fields
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

		<?php $this->load->view("admin/_partials/js.php") ?>

</body>

</html>
```
</details>

### Percobaan Upload File

Coba tambahkan staff baru dan jangan lupa sertakan gambarnya...

![tutor7_12](https://drive.google.com/uc?expand&id=1H22jn3IaVkvSsmNduvyr-h0mdaCdBrzX)

Setelah itu, klik Save dan buka halaman list Staff dan cari data yang baru saja kita input.

Maka hasilnya:

![tutor7_13](https://drive.google.com/uc?expand&id=1-wlxfhDsw3uLdHkGvU2SJPeVi_9RGPz2)

Jika kita mengecek pada direktori `upload/staff`, maka akan ada file baru di sana.

Hasil upload data di dalam direktori `upload/staff`

## Edit edit_form.php

Silahkan buka terlebih dahulu file `edit_form.php`-nya.. `application/views/admin/staffv/edit_form.php`

Hal yang akan kita edit/tambahkan pada file ini adalah pada bagain data form.. pada form akan kita tambahkan input baru yang akan berfungsi sebai tempat kita untuk mengupload file dengan menampilkan window explorer file.. sama saja dengan `new_form.php` tapi dengan sebuah hidden input seperti kita bahas diatas apabila saat update data `staff` dan tidak mengupload file baru maka nilai dari field akan dikembalikan/ atau diisi kembali dengan nilai yang sudah ada..

```html
<div class="form-group">
	<label for="foto">Photo</label>
	<input class="form-control-file <?php echo form_error('foto') ? 'is-invalid':'' ?>"
	type="file" name="foto" />
	<input type="hidden" name="old_foto" value="<?php echo $staff->foto ?>" />
	<div class="invalid-feedback">
		<?php echo form_error('foto') ?>
	</div>
</div>
```

![tutor7_14](https://drive.google.com/uc?expand&id=1JZGFNwdsw05pp8kM0zl3OuJbrD2geIlM)

sehingga keseluruhan file `edit_form.php` akan menjadi seperti berikut :

<details>
  <summary> `new_form.php` (*klik untuk lihat)</summary>
  <!-- have to be followed by an empty line! -->
```html
<!DOCTYPE html>
<html lang="en">

<head>
	<?php $this->load->view("admin/_partials/head.php") ?>
</head>

<body id="page-top">

	<?php $this->load->view("admin/_partials/navbar.php") ?>
	<div id="wrapper">

		<?php $this->load->view("admin/_partials/sidebar.php") ?>

		<div id="content-wrapper">

			<div class="container-fluid">

				<?php $this->load->view("admin/_partials/breadcrumb.php") ?>

				<?php if ($this->session->flashdata('success')): ?>
				<div class="alert alert-success" role="alert">
					<?php echo $this->session->flashdata('success'); ?>
				</div>
				<?php endif; ?>

				<!-- Card  -->
				<div class="card mb-3">
					<div class="card-header">

						<a href="<?php echo site_url('admin/staff/') ?>"><i class="fas fa-arrow-left"></i>
							Back</a>
					</div>
					<div class="card-body">

						<form action="<?php base_url('admin/staff/edit') ?>" method="post" enctype="multipart/form-data">

							<input type="hidden" name="id" value="<?php echo $staff->staff_id?>" />

							<div class="form-group">
								<label for="name">Nama*</label>
								<input class="form-control <?php echo form_error('name') ? 'is-invalid':'' ?>"
								 type="text" name="name" placeholder="staff name" value="<?php echo $staff->name ?>" />
								<div class="invalid-feedback">
									<?php echo form_error('name') ?>
								</div>
							</div>

							<div class="form-group">
								<label for="absen">No. Absen*</label>
								<input class="form-control <?php echo form_error('absen') ? 'is-invalid':'' ?>"
								 type="number" name="absen" placeholder="Nomor Absen Staff" value="<?php echo $staff->no_absen ?>" />
								<div class="invalid-feedback">
									<?php echo form_error('absen') ?>
								</div>
							</div>

							<div class="form-group">
								<label for="status">Status*</label><br/>
								<input class="form-control-1 <?php echo form_error('status') ? 'is-invalid':'' ?>"
								 type="radio" name="status" value="aktiv" checked/>Aktiv<br/>
                                 <input class="form-control-1 <?php echo form_error('status') ? 'is-invalid':'' ?>"
								 type="radio" name="status" value="nonaktiv" />Non-Aktiv<br/>
								<div class="invalid-feedback">
									<?php echo form_error('status') ?>
								</div>
							</div>


							<div class="form-group">
								<label for="jabatan">Jabatan*</label>
								<input class="form-control <?php echo form_error('jabatan') ? 'is-invalid':'' ?>"
								 type="text" name="jabatan" placeholder="staff name" value="<?php echo $staff->jabatan ?>" />
								<div class="invalid-feedback">
									<?php echo form_error('jabatan') ?>
								</div>
							</div>

							<div class="form-group">
								<label for="keterangan">Keterangan</label>
								<textarea class="form-control <?php echo form_error('keterangan') ? 'is-invalid':'' ?>"
								 name="keterangan" placeholder="staff keterangan..."><?php echo $staff->keterangan ?></textarea>
								<div class="invalid-feedback">
									<?php echo form_error('keterangan') ?>
								</div>
							</div>

							<div class="form-group">
								<label for="foto">Photo</label>
								<input class="form-control-file <?php echo form_error('foto') ? 'is-invalid':'' ?>"
								type="file" name="foto" />
								<input type="hidden" name="old_foto" value="<?php echo $staff->foto ?>" />
								<div class="invalid-feedback">
									<?php echo form_error('foto') ?>
								</div>
							</div>

							<input class="btn btn-success" type="submit" name="btn" value="Save" />
						</form>

					</div>

					<div class="card-footer small text-muted">
						* required fields
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

		<?php $this->load->view("admin/_partials/js.php") ?>

</body>

</html>
```
</details>

### Percobaan Edit Upload File

Coba Edit data staff yang baru kita buat tadi dan jangan lupa sertakan gambar yang baru...

![tutor7_15](https://drive.google.com/uc?expand&id=1v9artMFLdKnf1WpLrX7WQYksEoRu677-)

Setelah itu, klik Save dan buka halaman list Staff dan cari data yang baru saja kita edit.

Maka hasilnya:

![tutor7_16](https://drive.google.com/uc?expand&id=1EtpvuDRg4fjTVe0kyWm7UXx_g_hYr53m)

Jika kita mengecek pada direktori `upload/staff`, maka file lama di sana telah terganti dengan file yang baru.

Selamat, kita sudah berhasil membuat fitur upload 👏👏👏…

…Tapi masih ada yang kurang.

Apa itu?

Ketika kita menghapus data, filenya akan tetap ada di dalam direktori. Karena belum ada fungsi untuk menghapus file.

Mari kita perbaiki…

# 5. Menghapus File yang di-upload

Kita membutuhkan sebuah method khusus untuk menghapus file yang telah di-upload.

Silahkan tambahkan method berikut pada class `Staff_model`, tepat di bawah method `_uploadImage()`.

```php
private function _deleteImage($id)
{
    $staff = $this->getById($id);
    if ($staff->foto != "default.jpg") {
	    $filename = explode(".", $staff->foto)[0];
		return array_map('unlink', glob(FCPATH."upload/staff/$filename.*"));
    }
}
```

Sehingga akan menjadi seperti ini:

![tutor7_17](https://drive.google.com/uc?expand&id=101aoBpDe4QQRGEMj6bZ4ccXGiZ7fQGYp)

Terakhir, panggil method `_deleteImage()` pada method `delete()`.

![tutor7_18](https://drive.google.com/uc?expand&id=1VKGvqb-wiBqkdUFRVySpT5dHgWMlNh1W)

Oke, sekarang kita sudah bisa menghapus data dan juga file yang terupload.

Mari kita coba…

![tutor7_19](https://drive.google.com/uc?expand&id=1qNn4v3wPc-30ibmSVCRZZZbUPI2d9f3U)

Yep! berhasil 🎉

Mungkin kamu akan bertanya,

Mengapa ada dua file yang terhapus?

Jadi gini…

Coba perhatikan method-nya, khususnya kode yang ada di dalam if.

```php
if ($product->image != "default.jpg") {
    $filename = explode(".", $product->image)[0];
	return array_map('unlink', glob(FCPATH."upload/product/$filename.*"));
}
```

Di sana kita mengambil nama file dengan fungsi `exlode()`. Lalu kita cari file berdasarkan nama tersbut dengan fungsi `glob()`.

Setelah file-file ditemukan, lalu kita gunakan fungsi `array_map()` untuk mengeksekusi fungsi `unlink()` pada tiap file yang ditemukan.

Tanda bitang (*) setelah `$filename `artinya semua ektensi dipilih.

Ini nanti akan menghapus semua file dengan nama yang sama dan apapun ekstensinya.

Mengapa demikian?

Karena pada fungsi upload yang kita buat, di sana kita membolehkan untuk upload file dengan ekstensi `jpg`, `gif`, dan `png`.

Ketika data diedit dan gambar yang di-upload berekstensi berbeda dengan yang sudah ada di server…

…maka ia akan membuat file baru.

Misalnya di server sudah ada `123.jpg`, lalu di-upload lagi—misal file `.png`— maka nanti akan dibuat lagi `123.png`.

Mengapa bisa begitu? Bukankah kita sudah memberikan konfigurasi overwrite = true?

overwrite pada konfigurasi upload, hanya akan menindih file dengan nama dan ekstensi yang sama.

Misal:

Di server sudah ada `123.jpg`. Ketika kita upload file lagi dengan ekstensi yang sama, maka `123.jpg` akan ditindih dengan file yang baru.

# Apa Selanjutnya?

 * Tutorial SIMKEP dengan Codeiniter #8: Membuat Fitur Pencarian (Admin)
 * Tutorial SIMKEP dengan Codeiniter #9: Membuat Template untuk Landing Page
 * Tutorial SIMKEP dengan Codeiniter #10: Membuat Pagination
 * Tutorial SIMKEP dengan Codeiniter #11: Cara Menggunakan Databales dan Optimasi
 * Tutorial SIMKEP dengan Codeiniter #12: Cara Membuat Laporan dengan DomPDF

# Tutorial Sebelumnya

 * [Tutorial SIMKEP dengan Codeiniter #1 : Pengenalan Codeigniter](https://kos-it.github.io/post/tutorial-projek-1-bagian-1/)
 * [Tutorial SIMKEP dengan Codeiniter #2: (Controller) MVC dan Routing, Konsep dasar CI yang Harus Dipahami](https://kos-it.github.io/post/tutorial-projek-1-bagian-2/)
 * [Tutorial SIMKEP dengan Codeiniter #3: (View) Cara Menggunakan Bootstrap pada Codeiniger](https://kos-it.github.io/post/tutorial-projek-1-bagian-3/)
 * [Tutorial SIMKEP dengan Codeiniter #4: (View) Membuat Template Admin](https://kos-it.github.io/post/tutorial-projek-1-bagian-4/)
 * [Tutorial SIMKEP dengan Codeiniter #5: (Model) Membuat CRUD yang Baik](https://kos-it.github.io/post/tutorial-projek-1-bagian-5/) 
 * [Tutorial SIMKEP dengan Codeiniter #6: Membuat Fitur Login](https://kos-it.github.io/post/tutorial-projek-1-bagian-6/)