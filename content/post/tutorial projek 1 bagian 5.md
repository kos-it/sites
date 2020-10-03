---
title: "Tutorial SIMKEP dengan Codeiniter #5: (Model) Membuat CRUD yang Baik dan Benar"
date: 2020-06-29T11:35:00+09:00
categories: ["Website"]
tags: ["Tutorial Project - 1", "Website", "PHP", "Codeigniter"]
cover: "https://drive.google.com//uc?export=view&id=1zKgyxiCm9R2RlIFO8O1cbknZGUN8NrRC"
---

Pada tutorial sebelumnya, kita sudah belajar bagaimana [cara membuat template admin yang benar dan efisien](https://kos-it.github.io/post/tutorial-projek-1-bagian-4/).

Kita juga sudah membahas tentang [Controller dan routing pada Codeigniter](https://kos-it.github.io/post/tutorial-projek-1-bagian-2/).

Tahap selanjutnya adalah… Pembahasan tentang **database** dan **model**.

Oke, judulnya ini cukup clickbait: **“Cara Membuat Fitur CRUD di Codeigniter yang Baik dan Benar!"**.

Mengapa saya bilang demikian?

Karena, beberapa tutorial Codeigniter yang pernah saya ikuti tidak mengajari praktek terbaik (*best practice*) dalam ngoding CI.

Bukan berarti mereka salah…

…dan mengklaim cara pada tutorial ini yang paling benar.

Semua cara dan solusi, benar.

Hanya saja, jika kita menulis kode sembarangan, akibatnya bisa rugi.

Saya pernah mengerjakan project menggunakan Codeigniter, lalu kode-kode yang saya tulis sangat berantakan dan kotor.

Hasilnya:

Project gagal, karena saya tidak mau mengembangkannya lagi.

Ribet!

Saya lebih memilih ngoding ulang dari awal daripada mengembangkan kode tersebut.

Seperti itulah rasanya menulis kode yang buruk dan kotor.

Namun, dari hasil pengulangan tersebut. Saya belajar banyak hal.

Seperti, bagaimana sebaiknya cara menerima data dari form. Apakah langsung di simpan ke database, atauhkah divalidasi dulu.

Ternyata yang benar adalah:

Data harus divalidasi dulu.

Jika tidak divalidasi, bisa jadi nanti akan banyak bugs dan rentan dengan serangan XSS.

Tambah kerjaan lagi… 😫

Belajar dari pengalaman, saya tidak ingin kamu bernasib sama seperti saya yang gagal menyelesaikan project.

Maka saya membuat tutorial ini…

*Jika ada solusi yang lebih baik lagi, silahkan diusulkan di komentar!*

Oke, kita masuk ke tutorial.

Pada tutorial ini, kita akan mengerjakan banyak hal. Mulai dari membuat database, menyiapkan library, membuat model, sampai membuat CRUD.

CRUD (Create, Read, Update Delete) adalah fitur dasar yang harus kita buat saat bekerja dengan database.

Berikut ini daftar pekerjaannya…

> 1. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Database
2. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Konfigurasi Codeigntier
3. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Model untuk Tabel
3. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Controller
4. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat View
5. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Form Add
6. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Form Edit
7. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Fitur Hapus Data

Mari kita mulai kerjakan…

# Membuat Database untuk Codeigniter
Silahkan buka [PHPMyadmin](localhost/phpmyadmin), kemudian buatlah database baru dengan nama `simkep`.

![database0](https://drive.google.com/uc?export=view&id=1QYa74vJRTx8gTnfPMi_ZMQqX18d426XG)
![database1](https://drive.google.com/uc?export=view&id=1TWNKguvMLAGITmTstQjHSHlke0IQVl6L)


## Tabel `devisi`
Setelah itu, buat tabel `devisi` dengan 4 kolom. Tabel ini nanti akan menyimpan data devisi kepanitiaan.

![database2](https://drive.google.com/uc?export=view&id=1Kz-_F2kFIqs1sYpsbjLoQle_Tew9XtG3)

Kolom yang dibutuhkan:

1. `devisi_id` (*Primary Key*) bertipe *int* dengan panjang 10
2. `devisi` bertipe *varchar* dengan panjang 64
3. `nama` bertipe *varchar* dengan panjang 64
4. `keterangan` bertipe *text*.

![database3](https://drive.google.com/uc?export=view&id=1P3dZIYoiWKgW4gATvggA2xd-TMMEscd4)

…dan jangan lupa jadikan kolom `devisi_id` sebagai **primary key**, dan lakukan **auto increment** pada extra, *auto increment* disini bertujuan untuk memberikan nilai dalam kolom `devisi_id` secara otomatis dan berurutan...

![database4](https://drive.google.com/uc?export=view&id=1lzFeyG_l1loE9IiiUnv_42iYMN4R8f7y)

Terakhir, klik **Save** untuk menyimpan.

![database5](https://drive.google.com/uc?export=view&id=1IgoT1HskA1gEeJ1Zce7AIgPoxsX_5Eoq)

Sehingga kita sekarang punya tabel `devisi` dengan struktur seperti ini:

![databaase6](https://drive.google.com/uc?export=view&id=1Bn4PEid8v5kxpqz1yTctVh_LZz8zh_cf)

Kode **SQL**-nya:

```sql
CREATE TABLE `devisi` (
  `devisi_id` int(10) NOT NULL,
  `devisi` varchar(64) NOT NULL,
  `nama` varchar(64) NOT NULL,
  `keterangan` text NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

ALTER TABLE `devisi`
  ADD PRIMARY KEY (`devisi_id`);

ALTER TABLE `devisi`
  MODIFY `devisi_id` int(10) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=0;
```

selain tabel `devisi` kita jega perlu membuat tabel `kepanitiaan` dan `staff` lakukan langkah yang sama atau menggunakan kode **SQL** yang telah kami sediakan

## Tabel `kepanititaan`
Kolom yang dibutuhkan:

1. `kepanitiaan_id` (*Primary Key*) bertipe int dengan panjang 64
2. `no_surat` bertipe *varchar* dengan panjang 64
3. `nama` bertipe *varchar* dengan panjang 255
4. `tanggal` bertipe *date*
5. `keterangan` bertipe *text*
6. `relasi` bertipe *varchar* dengan panjang 64

Kode **SQL**-nya:

```sql
CREATE TABLE `kepanitiaan` (
  `kepanitiaan_id` int(64) NOT NULL,
  `no_surat` varchar(64) NOT NULL,
  `nama` varchar(255) NOT NULL,
  `tanggal` date NOT NULL,
  `keterangan` text NOT NULL,
  `relasi` varchar(64) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

ALTER TABLE `kepanitiaan`
  ADD PRIMARY KEY (`kepanitiaan_id`);

ALTER TABLE `kepanitiaan`
  MODIFY `kepanitiaan_id` int(64) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=0;
```

## Tabel `staff`
Kolom yang dibutuhkan :

1. `staff_id` (*Primary Key*) bertipe *int* dengan panjang 10
2. `no_absen` bertipe *int* dengan panjang 11
3. `name` bertipe *varchar* dengan panjang 64
4. `status` bertipe *varchar* dengan panjang 64
5. `jabatan` bertipe *varchar* dengan panjang 64
6. `keterangan` bertipe *text*
7. `prioritas` bertipe *int* dengan panjang 11
8. `panitia_id` bertipe *varchar* dengan panjang 64
9. `kep_dev` bertipe *int* dengan panjang 11
10. `foto` bertipe *varchar* dengan panjang 255

Kode **SQL**-nya:

```sql
CREATE TABLE `staff` (
  `staff_id` varchar(64) NOT NULL,
  `no_absen` int(11) NOT NULL,
  `name` varchar(64) NOT NULL,
  `status` varchar(64) NOT NULL,
  `jabatan` varchar(64) NOT NULL,
  `keterangan` text NOT NULL,
  `prioritas` int(11) NOT NULL,
  `panitia_id` varchar(64) NOT NULL,
  `kep_dev` int(11) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

ALTER TABLE `staff`
  ADD PRIMARY KEY (`staff_id`);
```

Satu pekerjaan sudah selesai…

> 1. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Database</s>
2. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Konfigurasi Codeigntier
3. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Model untuk Tabel
3. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Controller
4. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat View
5. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Form Add
6. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Form Edit
7. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Fitur Hapus Data

Berikutnya kita akan melakukan konfigurasi pada Codeigniter agar dapat terhubung dengan database.

# Konfigurasi Codeigniter
Silahkan buka <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `config/database.php`, kemudian isi seperti ini:

```php
$db['default'] = array(
	'dsn'	=> '',
	'hostname' => 'localhost',
	'username' => 'root',
	'password' => '',
	'database' => 'simkep',
	'dbdriver' => 'mysqli',
	'dbprefix' => '',
	'pconnect' => FALSE,
	'db_debug' => (ENVIRONMENT !== 'production'),
	'cache_on' => FALSE,
	'cachedir' => '',
	'char_set' => 'utf8',
	'dbcollat' => 'utf8_general_ci',
	'swap_pre' => '',
	'encrypt' => FALSE,
	'compress' => FALSE,
	'stricton' => FALSE,
	'failover' => array(),
	'save_queries' => TRUE
);
```

Perhatikan pada item berikut:

```php
'hostname' => 'localhost',
'username' => 'root',
'password' => '',
'database' => 'simkep',
```
Silahkan ubah sesuai dengan konfigurasi server mysql pada komputermu.

Pada komputer saya, username MySQL-nya adalah `root` dan password-nya kosong. ini sudah bawaan konfigurasi XAMPP pada windows, silahkan disesuikan saja.

Berikutnya, silahkan buka <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `config/autoload.php`.

Kemudian cari `$autoload['libraries']` dan tambahkan database dan session di sana.

```php
$autoload['libraries'] = array('database', 'session');
```

Ini artinya, kita akan me-load library `database` dan `session` secara otomatis.

Apa fungsinya?

* Library `database` akan menyediakan fungsi-fungsi untuk operasi database. Kita butuh ini, karena kita akan menggunakan database dalam aplikasi,
* Library `session` menyediakan fungsi-fungsi untuk mengakses variabel `$_SESSION`. Kita butuh ini untuk menampilkan *flash message* dan membuat *login*.

Dengan demikian konfigurasi selesai…

> 1. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Database</s>
2. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Konfigurasi Codeigntier</s>
3. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Model untuk Tabel
3. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Controller
4. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat View
5. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Form Add
6. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Form Edit
7. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Fitur Hapus Data

Jika ada yang ingin kita konfigurasi lagi atau mau tambah library lagi, nanti kita bisa ubah konfigurasinya.

Untuk saat ini, kita cukup butuh konfigurasi *database8* dan *autoload* library saja.

Berikutnya, kita akan mulai menulis kode untuk model.

# Membuat Model untuk Tabel

Model merupakan *class* atau kode yang berhubungan dengan data.

Di dalam model, kita akan membuat pemodelan data dari *database*. Sehingga kita akan lebih mudah mengaksesnya.

Biasanya satu tabel, dibuatkan satu modelnya.

Silahkan buat folder baru di dalam direktori <img class="emoji" draggable="true" alt="folder" src="/icon/icons8-folder.svg"> `application/model/` dengan nama `admin`, kemudian buat file model baru dengan nama `Devisi_model.php`, `Kepanitiaan_model.php` dan `Staff_model.php`

Perhatikan, namanya harus diawali dengan huruf kapital.

Pada contoh di atas, `Devisi` "D" adalah huruf kapital.

Lalu untuk akhiran _model ini bersifat opsional.

Saya sengaja membuat akhiran ini untuk memudahkan dalam membedakan *class* *Controller* dengan *class* *Model*.

Nanti kita juga akan membuat *class Controller* yang bernama `Devisi.php`, karena itu kita sebaiknya menggunakan akhiran _model pada *class Model*.

Setelah membuat file, lalu apa lagi?

Selanjutnya kita akan mulai menulis kode setiap file yang telah kita buat

Silahkan ketik kode berikut…

(*ketik ya! jangan copas, agar dapat pengalaman coding, bukan pengalaman copas* 😄)

<details>
  <summary> `Devisi_model.php` (*klik untuk lihat)</summary>
  <!-- have to be followed by an empty line! -->
## Devisi_model.php
```php
<?php defined('BASEPATH') OR exit('No direct script access allowed');

class Devisi_model extends CI_Model
{
    private $_table = "devisi";
    private $_table1 = "staff";

    public $devisi_id;
    public $devisi;
    public $nama;
    public $keterangan;

    public function rules()
    {
        return [

            ['field' => 'devisi',
            'label' => 'Devisi',
            'rules' => 'required'],

            ['field' => 'nama',
            'label' => 'Nama',
            'rules' => 'required'],
            

        ];
    }

    public function getAll()
    {
        $query="SELECT de.devisi_id, de.devisi, de.nama, st.jabatan, de.keterangan
        FROM devisi as de, staff as st 
        WHERE de.nama=st.name order by de.devisi asc";
        return $this->db->query($query)->result();
        
    }

    public function getStaff()
    {
        return $this->db->get($this->_table1)->result();
    }

    public function getStaffId($id)
    {
        return $this->db->get_where($this->_table1, ["staff_id" => $id])->row();
    }
    
    public function getById($id)
    {
        return $this->db->get_where($this->_table, ["devisi_id" => $id])->row();
    }
    public function getCount()
    {
        return $this->db->select('*')->from('devisi')->get()->num_rows();
    }

    public function save()
    {
        $post = $this->input->post();
        $this->devisi = $post["devisi"];
        $this->nama= $post["nama"];
        $this->keterangan = $post["keterangan"];
        $this->db->insert($this->_table, $this);

        $query="UPDATE staff, devisi
        SET staff.kep_dev=2
        WHERE staff.name=devisi.nama";
        return $this->db->query($query);
    }

    public function update()
    {
        $query="UPDATE staff, devisi
        SET staff.kep_dev=1
        WHERE staff.name=devisi.nama";
        $this->db->query($query);

        $post = $this->input->post();
        $this->devisi_id = $post["id"];
        $this->devisi = $post["devisi"];
        $this->nama= $post["nama"];
        $this->keterangan = $post["keterangan"];
        $this->db->update($this->_table, $this, array('devisi_id' => $post['id']));

        $query="UPDATE staff, devisi 
        SET staff.kep_dev=2
        WHERE staff.name=devisi.nama";
        return $this->db->query($query);
    }

    public function delete($id)
    {
        $query="UPDATE staff, devisi
        SET staff.kep_dev=1
        WHERE staff.name=devisi.nama AND devisi.devisi_id=$id";
        $this->db->query($query);
        return $this->db->delete($this->_table, array("devisi_id" => $id));
    }
}
```
</details>

Sudah selesai ngetiknya?

Baik, sekarang giliran kami menjelaskan:

Kode di atas memang belum bisa kita coba, karena ini hanya pemodelan data saja.

Nanti kita akan gunakan fungsi-fungsi atau method yang ada di dalam kode ini pada *class Controller*.

Pertama silahkan perhtaikan bagian ini:

```php
private $_table = "devisi";
private $_table1 = "staff";

// nama kolom di tabel, harus sama huruf besar dan huruf kecilnya!
public $devisi_id;
public $devisi;
public $nama;
public $keterangan;
```

Ini adalah properti atau *variabel* yang kita butuhkan dalam model Devisi.

Pada properti `$_tabel` kita memberikan modifier private, karena properti ini hanya akan digunakan pada class ini saja.

Jika kamu pernah belajar OOP, pasti paham.

Selanjutnya silahkan perhatikan method `rules()`:

```php
public function rules()
{
    return [

        ['field' => 'devisi',
        'label' => 'Devisi',
        'rules' => 'required'],

        ['field' => 'nama',
        'label' => 'Nama',
        'rules' => 'required'],

    ];
}
```

Method ini akan mengembalikan sebuah *array* yang berisi *rules*.

*Rules* ini nanti kita butuhkan untuk *validasi input*.

Pada *Rules* di atas, kita memberikan aturan untuk wajib mengisi (*required*) field `devisi` dan `nama`. adapun untuk field `keterangan` tidak kita berikan *rules* dan `devisi_id` akan terisi secara otomatis, karna kita telah mmberikan attribut *auto_increment* pada saat pembuatannya.

Berikutnya, silahkan perhatikan method `get()` dan `getAll()`. Kedua method ini akan kita gunakan untuk mengambil data dari *database*.

![model1](https://drive.google.com/uc?export=view&id=18_SeoPJ_NHsPuHE6FkYemfQNsjS6GeOJ)

Berikutnya perhatikan method `save()`:

![model2](https://drive.google.com/uc?export=view&id=1zuyaHSJNFxfyi-dzw0hFGH58I-TxUwaS)

Method ini akan kita gunakan untuk menyimpan data ke tabel devisi dan imbasnya (_update_) pada tabel staff.

Kita mengambil input yang dikirim dari form menggunakan `$this->input->post()`.

Mengapa ini ditulis di _Model_?

Biasanya orang menuliskannya pada _Controller_. Namun, biar _Controller_ lebih fokus mengatur hubungan _Model_ dengan _View_, maka sebaiknya ini kita tulis di _Model_.

Karena nanti pada _Controller_, kita tinggal validasi saja inputannya.

Untuk method berikutnya hampir sama.

Method `update()` untuk update data dan `delete()` untuk menghapus data.

Pada method `update()`, kita mengisi `$this->devisi_id` dengan id yang didapatkan dari form (`$post['id']`). Karena ini untuk update.

kemudian untuk _Model_ `Kepanitiaan_model.php` dan `Staff_model.php` kodenya dapat kalihan lihat berikut ini :

<details>
  <summary> `Kepanitiaan_model.php` (*klik untuk lihat)</summary>
  <!-- have to be followed by an empty line! -->
## Kepanitiaan_model.php
```php
<?php defined('BASEPATH') OR exit('No direct script access allowed');

class Kepanitiaan_model extends CI_Model
{
    private $_table1 = "devisi";
    private $_table2 = "staff";
    private $_table3 = "kepanitiaan";

    public $kepanitiaan_id;
    public $no_surat;
    public $nama;
    public $tanggal;
    public $keterangan;
    public $relasi;

    public function rules()
    {
        return [

            ['field' => 'nama',
            'label' => 'Nama',
            'rules' => 'required'],

            ['field' => 'tanggal',
            'label' => 'Tanggal',
            'rules' => 'required'],
            
            // ['field' => 'jumlah',
            // 'label' => 'Jumlah',
            // 'rules' => 'required'],

            ['field' => 'relasi',
            'label' => 'Relasi',
            'rules' => 'required']

        ];
    }

    public function getAll()
    {
        $query="SELECT ke.kepanitiaan_id, ke.no_surat, ke.nama, ke.tanggal, ke.keterangan
        FROM kepanitiaan as ke";
        return $this->db->query($query)->result();
    }

    //<<------fungsi get---------->>
    public function getCount()
    {
        return $this->db->select('*')->from('staff')->get()->num_rows();
    }
    public function getCountKepanitiaan()
    {
        return $this->db->select('*')->from('kepanitiaan')->get()->num_rows();
    }

    public function getCountDevisi()
    {
        return $this->db->select('*')->from('devisi')->get()->num_rows();
    }
  
    public function getById($id)
    {
        return $this->db->get_where($this->_table3, ["kepanitiaan_id" => $id])->row();
    }

    public function getStaff()
    {
        return $this->db->get($this->_table2)->result();
    }
    public function getStaffId($id)
    {
        return $this->db->get_where($this->_table2, ["staff_id" => $id])->row();
    }

    function get_data_stok(){
        $query = $this->db->query("SELECT name, prioritas FROM staff ");
        foreach($query->result() as $data)
        {
            $hasil[] = $data;
        }
            return $hasil;
    }

    public function getDevisi()
    {
        // return $this->db->get($this->_table1)->result();
        $query="SELECT de.devisi, de.nama, st.name, st.no_absen 
        FROM devisi as de, staff as st
        WHERE de.nama=st.name";
        return $this->db->query($query)->result();
        // return $this->db->get($this->_table1)->result();
    }

    public function getRelasi()
    {
            $query="SELECT st.staff_id, ke.kepanitiaan_id, st.no_absen, st.name, st.panitia_id, ke.relasi
            FROM staff as st, kepanitiaan as ke
            WHERE st.panitia_id=ke.relasi order by st.no_absen asc";
            return $this->db->query($query)->result();
    }

    public function save()
    {
        // $query="SELECT staff_id FROM staff WHERE name = 'nama'";
        // $data["staff_id"]=$this->db->query($query)->result();
        $post = $this->input->post();
        $this->no_surat = $post["surat"];
        $this->nama = $post["nama"];
        $this->tanggal = $post["tanggal"];
        $this->keterangan = $post["keterangan"];
        $this->relasi = $post["relasi"];
        $this->db->insert($this->_table3, $this);
    }
    
    public function update()
    {
        $post = $this->input->post();
        $this->kepanitiaan_id = $post["id"];
        $this->no_surat = $post["surat"];
        $this->nama = $post["nama"];
        $this->tanggal = $post["tanggal"];
        $this->keterangan = $post["keterangan"];
        $this->relasi = $post["relasi"];
        $this->db->update($this->_table3, $this, array('kepanitiaan_id' => $post['id']));
    }
    
    public function buat()
    {
            // menyimpan data kedalam variabel
            $var0 = $_POST['jumlah'];
            $var10 = $_POST['relasi'];

            $query="UPDATE staff 
            SET panitia_id='$var10', prioritas=0
            WHERE kep_dev=1 AND status='aktiv' ORDER BY prioritas desc 
            LIMIT $var0";
            $this->db->query($query);
            $query="UPDATE staff 
            SET prioritas=prioritas+15
            WHERE kep_dev=1";
            return $this->db->query($query); 
 
    }

    public function delete($id)
    {
        $query="UPDATE staff, kepanitiaan
        SET staff.panitia_id=0
        WHERE staff.panitia_id=kepanitiaan.relasi AND kepanitiaan.kepanitiaan_id=$id";
        $this->db->query($query);
        return $this->db->delete($this->_table3, array("kepanitiaan_id" => $id));
    }

    public function conf()
    {
        $var0 = $_POST['ganti1'];
        $var1 = $_POST['ganti2'];
        $query="UPDATE staff, panitia 
        SET staff.panitia_id=$var1
        WHERE staff.name=$var0";
        $this->db->query($query);
    }
}
```
</details>

<details>
  <summary> `Staff_model.php` (*klik untuk lihat)</summary>
  <!-- have to be followed by an empty line! -->
## Staff_model.php
```php
<?php defined('BASEPATH') OR exit('No direct script access allowed');

class Staff_model extends CI_Model
{
    private $_table = "staff";

    public $staff_id;
    public $no_absen;
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
}
```
</details>

Baik, dengan demikian…

…kita sudah selesai membuat model.

> 1. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Database</s>
2. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Konfigurasi Codeigntier</s>
3. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Model untuk Tabel</s>
3. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Controller
4. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat View
5. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Form Add
6. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Form Edit
7. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Fitur Hapus Data

Berikutnya kita akan membuat Controller.

# Membuat Contoller

Seperti yang sudah kita pelajari pada [tutorial sebelumnya](https://kos-it.github.io/post/tutorial-projek-1-bagian-2/), _Controller_ adalah bagian dari CI yang bertugas untuk menangani HTTP request dan menghubungan _Model_ dengan _View_.

Pada _Controller_, kita akan memanggil method-method yang ada di dalam _Model_ untuk mendapatkan data.

Setelah itu data tersebut di-render ke dalam _View_ dengan me-load-nya.

Untuk lebih jelasnya…

Mari kita mulai coding.

Silahkan buat file baru di dalam folder <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `application/controllers/admin/` dengan nama `Devisi.php`, `Kepanitiaan.php`, `Staff.php`. Kemudian isi file `Devisi.php`, `Kepanitiaan.php`, `Staff.php` dengan kode berikut:

<details>
  <summary> `Devisi.php` (*klik untuk lihat)</summary>
  <!-- have to be followed by an empty line! -->
## Devisi.php
```php
<?php

defined('BASEPATH') OR exit('No direct script access allowed');

class Devisi extends CI_Controller
{
    public function __construct()
    {
        parent::__construct();
        $this->load->model("devisi_model");
        $this->load->library('form_validation');
    }

    public function index()
    {
        $data["devisi"] = $this->devisi_model->getAll();
        $this->load->view("admin/devisiv/list", $data);
    }

    public function add()
    {
        $data["devisi"] = $this->devisi_model->getStaff();
        $data["count"] = $this->devisi_model->getCount();
        $devisi = $this->devisi_model;
        $validation = $this->form_validation;
        $validation->set_rules($devisi->rules());

        if ($validation->run()) {
            $devisi->save();
            $this->session->set_flashdata('success', 'Berhasil disimpan');
        }

        $this->load->view("admin/devisiv/new_form", $data);
    }

    public function edit($id = null)
    {
        if (!isset($id)) redirect('admin/devisi');
        
        $data["devisii"] = $this->devisi_model->getStaff();
        $devisi = $this->devisi_model;
        $validation = $this->form_validation;
        $validation->set_rules($devisi->rules());

        if ($validation->run()) {
            $devisi->update();
            $this->session->set_flashdata('success', 'Berhasil disimpan');
        }

        $data["devisi"] = $devisi->getById($id);
        if (!$data["devisi"]) show_404();
        
        $this->load->view("admin/devisiv/edit_form", $data);
    }

    public function delete($id=null)
    {
        if (!isset($id)) show_404();
        
        if ($this->devisi_model->delete($id)) {
            redirect(site_url('admin/devisi'));
        }
    }
}
```
</details>

<details>
  <summary> `Kepanitiaan.php` (*klik untuk lihat)</summary>
  <!-- have to be followed by an empty line! -->
## Kepanitiaan.php
```php
<?php

defined('BASEPATH') OR exit('No direct script access allowed');

class Kepanitiaan extends CI_Controller
{
    public function __construct()
    {
        parent::__construct();
        $this->load->model("kepanitiaan_model");
        $this->load->library('form_validation');
    }

    public function index()
    {
        $data["panitia"] = $this->kepanitiaan_model->getAll();
        $this->load->view("admin/kepanitiaanv/list", $data);   
    }

    public function detail($id = null)
    {
        if (!isset($id)) redirect('admin/kepanitiaan');

        $data["panitia"] = $this->kepanitiaan_model->getById($id);

        if (!$data["panitia"]) show_404();

        $data['devisi'] =$this->kepanitiaan_model->getDevisi();

        $data['relasi'] =$this->kepanitiaan_model->getRelasi();
        
        $this->load->view("admin/kepanitiaanv/detail", $data);
    }

    public function add()
    {
        $data["devisi"] = $this->kepanitiaan_model->getDevisi();
        $data["devisicount"] = $this->kepanitiaan_model->getCountDevisi();
        $data["panitiacount"] = $this->kepanitiaan_model->getCountKepanitiaan();        
        $kepanitiaan = $this->kepanitiaan_model;
        $validation = $this->form_validation;
        $validation->set_rules($kepanitiaan->rules());

        if ($validation->run()) {
            $kepanitiaan->save();        
            $kepanitiaan->buat();
            $this->session->set_flashdata('success', 'Berhasil disimpan');
        }
        $this->load->view("admin/kepanitiaanv/new_form", $data);
    }

    public function edit($id = null)
    {
        if (!isset($id)) redirect('admin/kepanitiaan');
        
        $panitia = $this->kepanitiaan_model;
        $validation = $this->form_validation;
        $validation->set_rules($panitia->rules());

        if ($validation->run()) {
            $panitia->update();
            $this->session->set_flashdata('success', 'Berhasil disimpan');
        }

        $data["panitia"] = $panitia->getById($id);
        if (!$data["panitia"]) show_404();
        
        $this->load->view("admin/kepanitiaanv/edit_form", $data);
    }

    public function delete($id=null)
    {
        if (!isset($id)) show_404();
        
        if ($this->kepanitiaan_model->delete($id)) {
            redirect(site_url('admin/kepanitiaan'));
        }
    }

    public function config($id = null)
    {
        if (!isset($id)) redirect('admin/kepanitiaan');
        
        $panitia = $this->kepanitiaan_model;
        $validation = $this->form_validation;
        $validation->set_rules($panitia->rules());

        if ($validation->run()) {
            $panitia->conf();
            $this->session->set_flashdata('success', 'Berhasil disimpan');
        }

        $data["panitia"] = $panitia->getById($id);
        if (!$data["panitia"]) show_404();

        $data["staff"] = $this->kepanitiaan_model->getStaff();
        
        $this->load->view("admin/kepanitiaanv/edit_panitia", $data);
    }
}
```
</details>

<details>
  <summary> `Staff.php` (*klik untuk lihat)</summary>
  <!-- have to be followed by an empty line! -->
## Staff.php
```php
<?php

defined('BASEPATH') OR exit('No direct script access allowed');

class Staff extends CI_Controller
{
    public function __construct()
    {
        parent::__construct();
        $this->load->model("staff_model");
        $this->load->library('form_validation');
    }

    public function index()
    {
        $data["staff"] = $this->staff_model->getAll();
        $this->load->view("admin/staffv/list", $data);
    }

    public function add()
    {
        $staff = $this->staff_model;
        $validation = $this->form_validation;
        $validation->set_rules($staff->rules());

        if ($validation->run()) {
            $staff->save();
            $this->session->set_flashdata('success', 'Berhasil disimpan');
        }

        $this->load->view("admin/staffv/new_form");
    }

    public function edit($id = null)
    {
        if (!isset($id)) redirect('admin/staff');
       
        $staff = $this->staff_model;
        $validation = $this->form_validation;
        $validation->set_rules($staff->rules());

        if ($validation->run()) {
            $staff->update();
            $this->session->set_flashdata('success', 'Berhasil disimpan');
        }

        $data["staff"] = $staff->getById($id);
        if (!$data["staff"]) show_404();
        
        $this->load->view("admin/staffv/edit_form", $data);
    }

    public function delete($id=null)
    {
        if (!isset($id)) show_404();
        
        if ($this->staff_model->delete($id)) {
            redirect(site_url('admin/staff'));
        }
    }
}
```
</details>

Sudah selesai?

Sekarang mari kita perhatikan penjelasannya… kita akan fokus pada _Controller_ `Staff.php`

Ada lima method dalam class tersebut:

### 1. Method `__construct()`

Method `__construct()` merupakan sebuah konstruktor. Method ini yang akan dieksekusi pertama kali saat Controller diakses.

Pada method ini, kita melakukan load model (`porduct_model`) dan library (`form_validation`).

```
    public function __construct()
    {
        parent::__construct();
        $this->load->model("staff_model");
        $this->load->library('form_validation');
    }
```

Library `form_validation` akan kita gunakan untuk memvalidasi input pada method `add()` dan `edit()`.

Mengapa harus divalidasi?

Karena bisa saja pengguna menginputkan data sembarang. Misalnya, sengaja mengisi dengan data kosong, script jahat seperti: serangan XSS, dll.

Intinya:

Sebelum menyimpan data ke database, pastikan data tersebut sudah benar.

### 2. Method `index()`

Pada method ini, kita akan mengambil data dari model dengan memanggil method `Staff_model->getAll()`.

Lalu kita me-rendernya ke dalam view `admin/staffv/list`.

```
    public function index()
    {
        $data["staff"] = $this->staff_model->getAll();
        $this->load->view("admin/staffv/list", $data);
    }
```

View `admin/staff/list` belum ada. Nati kita akan membuatnya.

### 3. Method `add()`

Method ini bertugas untuk menampilkan form add dan menyimpan data ke database. Tentunya dengan memanggil method `save()` yang ada pada model.

Namun, sebelum memanggil method `save()`, kita lakukan validasi terlebih dahulu dengan mengeksekusi method `run()` pada objek `$validation`.

```
    public function add()
    {
        $staff = $this->staff_model; //object model
        $validation = $this->form_validation; //object form validation
        $validation->set_rules($staff->rules()); //terapkan rules

        if ($validation->run()) { //melakukan validasi
            $staff->save(); //simpan data kedatabase
            $this->session->set_flashdata('success', 'Berhasil disimpan'); //tampilkan pesan berhasil
        }

        $this->load->view("admin/staffv/new_form"); //tampilkan form add
    }
```

Jika berhasil, maka pesan `"Berhasil disimpan"` akan ditampilkan.

Terakhir, kita akan menampilkan view `staffv/new_form`. View ini berisi sebuah form untuk menambah data.

View ini juga belum ada.

Nanti kita akan membuatnya.

### 4. Method `edit()`

Hampir sama dengan method `add()`, method `edit()` juga bertugas untuk menampilkan form dan menyimpan data.

![contoller1](https://drive.google.com/uc?export&id=1Xr9ZV0KhSXbGgFPxhsiD9p-BZNO4fSuA)

Mungkin kamu akan bertanya…

Nilai `$id` akan didapatkan dari mana?

Nilai `$id` akan kita dapatkan dari parameter atau argumen pada URL.

Ini sudah pernah kita bahas pada [tutorial routing pada CI](https://kos-it.github.io/post/tutorial-projek-1-bagian-2/).

### 5. Method `delete()`

Method `delete()` befungsi untuk menangni penghapusan data.

Prinsipnya hampir sama seperti method `edit()`, method `delete()` juga membutuhkan `$id` untuk menentukan data mana yang akan dihapus.

```    
  public function delete($id=null)
    {
        if (!isset($id)) show_404();
        
        if ($this->staff_model->delete($id)) {
            redirect(site_url('admin/staff'));
        }
    }
```

Apabila data berhasil dihapus, maka kita langsung alihkan (`redirect()`) menuju ke halaman `admin/staffv/`.

Dengan demikian…

Kita sudah selesai membuat Controller. 👏👏👏

> 1. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Database</s>
2. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Konfigurasi Codeigntier</s>
3. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Model untuk Tabel</s>
3. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Controller</s>
4. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat View
5. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Form Add
6. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Form Edit
7. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Fitur Hapus Data

Tugas kita masih belum selesai dan aplikasi masih belum dapat dicoba, karena kita belum membuat view-nya.

# Membuat View

View merupakan bagian yang bertugas mengurus tampilan.

Ada tiga macam view yang harus kita buat dalam aplikasi ini untuk _Controller_ `Devisi.php` dan `Staff.php` yang kita buat, yaitu:

1. `list.php` untuk menampilkan data;
2. `new_form.php` untuk menampilkan form tambah data;
3. dan `edit_form.php` untuk menampilkan form edit data.

sedangkan untuk _Controller_ `Kepanitiaan.php` sama seperti _Controller_ lainnya namun ada penambahan yaitu

1. `detail.php` untuk menampikan detail (anggota panitia) yang telah terpilih
2. `edit_panitia.php` untuk menampilkan form mengganti panitia yang bertugas (jika panitia terpilih berhalangan)

Mari kita buat semuanya.

Tapi sebelum itu, silahkan buat folder baru pada direktori `views/admin` dengan nama `devisiv`, `Staffv`, `Kepanitiaanv`.

Setelah itu, kita akan membuat view di dalam folder <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `views/admin/devisiv/`, <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `views/admin/staffv/`, dan <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `views/admin/kepanitiaanv/`sesuai dengan yang kita sebutkan diatas.

Kami akan jelaskan untuk pembuatan view `kepanitiaanv` untuk dua yang lainnya kalian bisa menyesuaikan

## 1. View List Data

Buatlah file baru dengan nama `list.php` di dalam folder <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `views/admin/kepanitiaanv/`.

Setelah itu, isi dengan kode berikut:

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
						<a href="<?php echo site_url('admin/kepanitiaan/add') ?>"><i class="fas fa-plus"></i> Add
							New</a>
					</div>
					<div class="card-body">

						<div class="table-responsive">
							<table class="table table-hover" id="dataTable" width="100%" cellspacing="0">
								<thead>
									<tr>
										<th>No. Surat</th>
										<th>Nama Kegiatan</th>
										<th>Tanggal</th>
										<th>Keterangan</th>
										<th>Action</th>
									</tr>
								</thead>
								<tbody>
									<?php foreach ($panitia as $panitiav): ?>
									<tr>
										<td>
											<?php echo $panitiav->no_surat ?>
										</td>
										<td width="150">
											<?php echo $panitiav->nama ?>
										</td>
										<td>
											<?php echo $panitiav->tanggal ?>
										</td>
										<td class="small">
											<?php echo substr($panitiav->keterangan, 0, 120) ?>...</td>
										<td width="200">
											<a href="<?php echo site_url('admin/kepanitiaan/detail/'.$panitiav->kepanitiaan_id) ?>"
												class="btn btn-small"><i class="fas fa-eye"></i> Detail</a>
											<a href="<?php echo site_url('admin/kepanitiaan/edit/'.$panitiav->kepanitiaan_id) ?>"
												class="btn btn-small"><i class="fas fa-edit"></i> Edit</a>
											<a href="<?php echo site_url('admin/cetak/') ?>"
												class="btn btn-small"><i class="fas fa-print"></i> Print</a>
											<a onclick="deleteConfirm('<?php echo site_url('admin/kepanitiaan/delete/'.$panitiav->kepanitiaan_id) ?>')"
												href="#!" class="btn btn-small text-danger"><i class="fas fa-trash"></i>
												Hapus</a>
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
		function deleteConfirm(url) {
			$('#btn-delete').attr('href', url);
			$('#deleteModal').modal();
		}

	</script>
</body>

</html>
```

View `kepanitiaanv/list.php` bertugas untuk menampilkan data pada halaman admin.

Datanya didapat dari mana?

Datanya kita dapat dari Controller, coba saja perhatikan method `index()` pada controller `Kepanitiaan.php`.

```
    public function index()
    {
        $data["panitia"] = $this->kepanitiaan_model->getAll();
        $this->load->view("admin/kepanitiaanv/list", $data);   
    }
```
## 2. Membuat Form Add

View berikutnya yang harus kita buat adalah `new_form.php`.

Silahkan buat file baru di dalam folder <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `view/admin/kepanitiaanv/` dengan nama `new_form.php`.

Setelah itu, isi dengan kode berikut:

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
						<a href="<?php echo site_url('admin/kepanitiaan/') ?>"><i class="fas fa-arrow-left"></i> Back</a>
					</div>
					<div class="card-body">

						<form action="<?php base_url('admin/kepanitiaan/add') ?>" method="post" enctype="multipart/form-data" >
							
							<div class="form-group">
								<label for="surat">No. Surat</label>
								<input class="form-control <?php echo form_error('surat') ? 'is-invalid':'' ?>"
								 type="text" name="surat" placeholder="No. Surat Kegiatan" />
								<div class="invalid-feedback">
									<?php echo form_error('surat') ?>
								</div>
							</div>

							<input type="hidden" name="relasi" value="<?php echo uniqid();?>" />

							<div class="form-group">
								<label for="nama">Jenis Kegiatan*</label>
								<input class="form-control <?php echo form_error('nama') ? 'is-invalid':'' ?>"
								 type="text" name="nama" placeholder="Jenis Kegiatan" />
								<div class="invalid-feedback">
									<?php echo form_error('nama') ?>
								</div>
							</div>
							
							<div class="form-group">
								<label for="tanggal">Waktu Pelaksana*</label>
								<input class="form-control <?php echo form_error('tanggal') ? 'is-invalid':'' ?>"
								 type="date" name="tanggal" />
								<div class="invalid-feedback">
									<?php echo form_error('tanggal') ?>
								</div>
							</div>
							
							<div class="form-group">
								<label for="jumlah">Jumlah Staff yang akan Berpartisipasi*</label><br/>
								<select name="jumlah"class="form-control <?php echo form_error('jumlah') ? 'is-invalid':'' ?>">
									<option value="0">-PILIH-</option>
									<?php for($i=1; $i<100; $i++) {
	                    			echo "<option value=$i>$i</option>";
									} ?>
	                    		</select>
								<div class="invalid-feedback">
									<?php echo form_error('jumlah') ?>
								</div>
							</div>
							<input type="hidden" name="count" value="<?php echo $devisicount?>" />

							<div class="form-group">
								<label for="keterangan">Keterangan</label>
								<textarea class="form-control <?php echo form_error('keterangan') ? 'is-invalid':'' ?>"
								 name="keterangan" placeholder="Keterangan..."></textarea>
								<div class="invalid-feedback">
									<?php echo form_error('keterangan') ?>
								</div>
							</div>

							<input type="hidden" name="count" value="<?php echo $devisicount?>" />

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

View `new_form.php` betugas untuk menampilkan form input untuk pembuatan data baru.

Form ini akan mengirim data ke: `/admin/kepanitiaan/add` (_Controller_ `Kepanitiaan`, method `add`).

Perhatikan pada form-nya.

```
<form action="<?php echo site_url('admin/kepanitiaan/add') ?>" method="post" enctype="multipart/form-data" >
...
</form>
```

Pada form tersebut, kita menggunakan enctype="multipart/form-data". Ini nanti akan kita gunakan untuk upload file.

Untuk saat ini fitur upload belum kita buat.

## 3. Membuat Form Edit

View selanjutnya yang harus kita buat adalah `edit_form.php`. Isi kodenya hampir sama seperti `new_form.php`.

Bedanya, di `edit_form.php` kita menampilkan nilai untuk setiap field-nya.

Silahkan buat file baru di dalam folder <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `views/admin/kepanitiaan/` dengan nama `edit_form.php`.

Setelah itu, isi dengan kode berikut:

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

						<a href="<?php echo site_url('admin/kepanitiaan/') ?>"><i class="fas fa-arrow-left"></i>
							Back</a>
					</div>
					<div class="card-body">

						<form action="<?php base_url('admin/kepanitiaan/edit') ?>" method="post"
							enctype="multipart/form-data">

							<input type="hidden" name="id" value="<?php echo $panitia->kepanitiaan_id?>" />

							<div class="form-group">
								<label for="surat">No. Surat</label>
								<input class="form-control <?php echo form_error('surat') ? 'is-invalid':'' ?>"
									type="text" name="surat" placeholder="No. Surat"
									value="<?php echo $panitia->no_surat ?>" />
								<div class="invalid-feedback">
									<?php echo form_error('surat') ?>
								</div>
							</div>

							<div class="form-group">
								<label for="nama">Jenis Kegiatan*</label>
								<input class="form-control <?php echo form_error('nama') ? 'is-invalid':'' ?>"
									type="text" name="nama" placeholder="Jenis Kegiatan"
									value="<?php echo $panitia->nama ?>" />
								<div class="invalid-feedback">
									<?php echo form_error('panitia') ?>
								</div>
							</div>

							<div class="form-group">
								<label for="tanggal">Waktu Kegiatan*</label><br />
								<input class="form-control <?php echo form_error('tanggal') ? 'is-invalid':'' ?>"
									type="date" name="tanggal" value="<?php echo $panitia->tanggal ?>" />
								<div class="invalid-feedback">
									<?php echo form_error('nama') ?>
								</div>
							</div>

							<div class="form-group">
								<label for="keterangan">Keterangan</label>
								<textarea class="form-control <?php echo form_error('keterangan') ? 'is-invalid':'' ?>"
									name="keterangan"
									placeholder="keterangan kegiatan..."><?php echo $panitia->keterangan ?></textarea>
								<div class="invalid-feedback">
									<?php echo form_error('keterangan') ?>
								</div>
							</div>

							<input type="hidden" name="relasi" value="<?php echo $panitia->relasi?>" />

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

## 4. Membuat Form Edit Panitia Terpilih

View selanjutnya yang harus kita buat adalah `edit_panitia.php`. form ini bertujuan mengganti anggota panitia yang telah terpilih oleh sistem berrasarkan prioritas mereka jika orang yang bersangkutan berhalangan/ tidak sanggup

Silahkan buat file baru di dalam folder <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `views/admin/kepanitiaan/` dengan nama `edit_panitia.php`.

Setelah itu, isi dengan kode berikut:

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

						<a href="<?php echo site_url('admin/kepanitiaan/') ?>"><i class="fas fa-arrow-left"></i>
							Back</a>
					</div>
					<div class="card-body">

						<form action="<?php base_url('admin/kepanitiaan/config') ?>" method="post" enctype="multipart/form-data">

                        <input type="hidden" name="ganti1" value="<?php echo $panitia->relasi?>" />
							<div class="form-group">
								<label for="ganti2">Staff Pengganti*</label><br/>
								<select name="ganti2"class="form-control <?php echo form_error('ganti2') ? 'is-invalid':'' ?>">
									<?php foreach($staff as $relasiv):?>
	                    			<option value="<?php echo $relasiv->name;?>"><?php echo $relasiv->name;?></option>
	                    			<?php endforeach;?>
	                    		</select>
								<div class="invalid-feedback">
									<?php echo form_error('ganti') ?>
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

## 5. Membuat Tampilan Detail Kepanitiaan

View terakhir yang harus kita buat pada folder <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `views/admin/kepanitiaan/` adalah `detail.php`. Isi kodenya hampir sama seperti `list.php`.

Bedanya, di `detail.php` kita menampilkan list anggota kepanitiaan yang terpilih berdasarkan prioritas dan kepala devisi yang bertugas pada kepanitaan yang kita buat.

Silahkan buat file baru di dalam folder <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `views/admin/kepanitiaan/` dengan nama `detail.php`.

Setelah itu, isi dengan kode berikut:

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

				<!-- 
        karena ini halaman overview (home), kita matikan partial breadcrumb.
        Jika anda ingin mengampilkan breadcrumb di halaman overview,
        silahkan hilangkan komentar (//) di tag PHP di bawah.
        -->
				<?php //$this->load->view("admin/_partials/breadcrumb.php") ?>

				<!-- Icon Cards-->
				<div class="row" align="center">
					<div class="col-xl-31 mb-3">
						<div class="card text-white bg-danger o-hidden h-100">
							<div class="card-body">
								<div class="card-body-icon">
									<i class="fas fa-fw fa-list"></i>
								</div>
								<div class="mr-5">Paitia Pelaksana : <?php echo $panitia->nama ?><br />Tanggal
									<?php echo $panitia->tanggal ?></div>
							</div>
							<a class="card-footer text-white clearfix small z-1"
								href="<?php echo site_url('admin/kepanitiaan/') ?>">
								<span class="float-left">
									<i class="fas fa-angle-left">-</i>
								</span>
								<span class="float-left">Kembali</span>
							</a>
						</div>
					</div>
				</div>
				<a href="<?php echo site_url('admin/cetak/') ?>"
				class="btn btn-small"><i class="fas fa-print"></i> Print</a>
				<br>
				<!-- DataTables -->
				<label>
					<h2>Staff Panitia Pelaksana</h2>
				</label>
				<div class="card mb-3">
					<div class="card-body">
						<div class="table-responsive">
							<table class="table table-hover" id="dataTable" width="100%" cellspacing="0">
								<thead>
									<tr>
										<th>No. Absen</th>
										<th>Nama</th>
										<th>Action</th>
									</tr>
								</thead>
								<tbody>
									<?php foreach ($relasi as $staffv): ?>
									<tr>
										<td>
											<?php echo $staffv->no_absen ?>
										</td>
										<td width="500">
											<?php echo $staffv->name ?>
										</td>
										<td width="250">
											<a href="<?php echo site_url('admin/kepanitiaan/config/'.$staffv->kepanitiaan_id) ?>"
												class="btn btn-small"><i class="fas fa-edit"></i> Edit</a>
											<!-- <a onclick="deleteConfirm('<?php echo site_url('admin/staff/delete/'.$staffv->panitia_id) ?>')"
												href="#!" class="btn btn-small text-danger"><i class="fas fa-trash"></i>
												Hapus</a> -->
										</td>
									</tr>
									<?php endforeach; ?>

								</tbody>
							</table>
						</div>
					</div>
				</div>
				

				<br /><br /><br />

				<label>
					<h2>Panitia Penaggung Jawab</h2>
				</label>
				<div class="card mb-3">
					<div class="card-body">
						<div class="table-responsive">
							<table class="table table-hover" id="dataTable" width="100%" cellspacing="0">
								<thead>
									<tr>
										<th>No. Absen</th>
										<th>Kepla Penaggung Jawab</th>
										<th>Tanggung Jawab</th>
									</tr>
								</thead>
								<tbody>
									<?php foreach ($devisi as $devisiv): ?>
									<tr>
										<td>
											<?php echo $devisiv->no_absen ?>
										</td>
										<td>
											<?php echo $devisiv->nama ?>
										</td>
										<td>
											<?php echo $devisiv->devisi ?>
										</td>
									</tr>
									<?php endforeach; ?>
								</tbody>
							</table>
						</div>
					</div>
				</div>

			</div>
		</div>

		<!-- Area Chart Example-->

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

untuk kode script dua view yang lainnya dapat kalian lihat berikut :

<details>
  <summary> `devisiv` (*klik untuk lihat)</summary>
  <!-- have to be followed by an empty line! -->
  Silahkan buat file baru di dalam folder <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `views/admin/devisiv/` dengan nama `list.php`. Setelah itu, isi dengan kode berikut:
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
						<a href="<?php echo site_url('admin/devisi/add') ?>"><i class="fas fa-plus"></i> Add New</a>
					</div>
					<div class="card-body">

						<div class="table-responsive">
							<table class="table table-hover" id="dataTable" width="100%" cellspacing="0">
								<thead>
									<tr>
										<th>P. J.</th>
										<th>Kepla PJ</th>
										<th>Jabatan</th>
										<th>Keterangan</th>
										<th>Action</th>
									</tr>
								</thead>
								<tbody>
									<?php foreach ($devisi as $devisiv): ?>
									<tr>
										<td width="150">
											<?php echo $devisiv->devisi ?>
										</td>
										<td>
											<?php echo $devisiv->nama ?>
										</td>
										<td>
											<?php echo $devisiv->jabatan ?>
										</td>
										<td class="small">
											<?php echo substr($devisiv->keterangan, 0, 120) ?>...</td>
										<td width="250">
											<a href="<?php echo site_url('admin/devisi/edit/'.$devisiv->devisi_id) ?>"
											 class="btn btn-small"><i class="fas fa-edit"></i> Edit</a>
											<a onclick="deleteConfirm('<?php echo site_url('admin/devisi/delete/'.$devisiv->devisi_id) ?>')"
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

  Silahkan buat file baru di dalam folder <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `views/admin/devisiv/` dengan nama `new_form.php`. Setelah itu, isi dengan kode berikut:
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
						<a href="<?php echo site_url('admin/devisi/') ?>"><i class="fas fa-arrow-left"></i> Back</a>
					</div>
					<div class="card-body">

						<form action="<?php base_url('admin/devisi/add') ?>" method="post" enctype="multipart/form-data" >
							<div class="form-group">
								<label for="devisi">Tanggung Jawab*</label>
								<input class="form-control <?php echo form_error('devisi') ? 'is-invalid':'' ?>"
								 type="text" name="devisi" placeholder="Jenis Tanggung Jawab" />
								<div class="invalid-feedback">
									<?php echo form_error('devisi') ?>
								</div>
							</div>

							<div class="form-group">
								<label for="nama">Kepala Penanggung Jawab*</label><br/>
								<select name="nama"class="form-control <?php echo form_error('nama') ? 'is-invalid':'' ?>">
									<option value="">-PILIH-</option>
									<?php foreach($devisi as $devisiv):?>
	                    			<option value="<?php echo $devisiv->name;?>"><?php echo $devisiv->name;?></option>
	                    			<?php endforeach;?>
	                    		</select>
								<div class="invalid-feedback">
									<?php echo form_error('nama') ?>
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

  Silahkan buat file baru di dalam folder <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `views/admin/devisiv/` dengan nama `edit_form.php`. Setelah itu, isi dengan kode berikut:
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

						<a href="<?php echo site_url('admin/devisi/') ?>"><i class="fas fa-arrow-left"></i>
							Back</a>
					</div>
					<div class="card-body">

						<form action="<?php base_url('admin/devisi/edit') ?>" method="post" enctype="multipart/form-data">

							<input type="hidden" name="id" value="<?php echo $devisi->devisi_id?>" />

							<div class="form-group">
								<label for="devisi">Tanggung Jawab*</label>
								<input class="form-control <?php echo form_error('devisi') ? 'is-invalid':'' ?>"
								 type="text" name="devisi" placeholder="Jenis Tanggung Jawab" value="<?php echo $devisi->devisi ?>" />
								<div class="invalid-feedback">
									<?php echo form_error('devisi') ?>
								</div>
							</div>

							<div class="form-group">
								<label for="nama">Kepala Penaggung Jawab*</label><br/>
								<select name="nama"class="form-control <?php echo form_error('nama') ? 'is-invalid':'' ?>">
									<option value="<?php echo $devisi->nama;?>"><?php echo $devisi->nama;?></option>
									<?php foreach($devisii as $devisiv):?>
	                    			<option value="<?php echo $devisiv->name;?>"><?php echo $devisiv->name;?></option>
	                    			<?php endforeach;?>
	                    		</select>
								<div class="invalid-feedback">
									<?php echo form_error('nama') ?>
								</div>
							</div>

							<div class="form-group">
								<label for="keterangan">Keterangan</label>
								<textarea class="form-control <?php echo form_error('keterangan') ? 'is-invalid':'' ?>"
								 name="keterangan" placeholder="devisi keterangan..."><?php echo $devisi->keterangan ?></textarea>
								<div class="invalid-feedback">
									<?php echo form_error('keterangan') ?>
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

<details>
  <summary> `staffv` (*klik untuk lihat)</summary>
  <!-- have to be followed by an empty line! -->
  Silahkan buat file baru di dalam folder <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `views/admin/staffv/` dengan nama `list.php`. Setelah itu, isi dengan kode berikut:
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
										<td width="150">
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

  Silahkan buat file baru di dalam folder <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `views/admin/staffv/` dengan nama `new_form.php`. Setelah itu, isi dengan kode berikut:
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

  Silahkan buat file baru di dalam folder <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `views/admin/staffv/` dengan nama `edit_form.php`. Setelah itu, isi dengan kode berikut:
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
								 type="number" name="absen" placeholder="Nomor Absen Staff" value="<?php echo $staff->name ?>" />
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

Akhirnya selesai juga… 👏👏👏

> 1. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Database</s>
2. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Konfigurasi Codeigntier</s>
3. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Model untuk Tabel</s>
3. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Controller</s>
4. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat View</s>
5. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Form Add</s>
6. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Form Edit</s>
7. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox1.svg"> Membuat Fitur Hapus Data

Tinggal sentuhan terakhir nih.

Tapi sebelum itu, kita coba dulu aplikasinya.

# Uji Coba Aplikasi

Coba buka: http://localhost/simkep/index.php/admin/staff

Jika kamu tidak melihat error, maka itu artinya berhasil.

![ujicoba1](https://drive.google.com/uc?export&id=1OLaQxBU3kdYnFotPAfOsO9MSlwUoSi9W)

Pada tampilan kalian mungkin belum ada data yang ditampilkan di dalam halaman list staff, karena kita belum menambahkan data apapun.

Mari kita coba buat data baru.

Silahkan buka: http://localhost/tokobuah/index.php/admin/staff/add atau klik link + **Add New**.

Kemudian isi dengan data baru.

![ujicoba2](https://drive.google.com/uc?export&id=11UU27__rcmBDGVOotyWoThFa0tl-TzWE)

Klik **Save**, jika muncul seperti ini…

![ujicoba3](https://drive.google.com/uc?export&id=1sAo3Wh9w4coCqGaW5JQwiXyvuKudD7JH)

…artinya data berhasil ditambahkan.

Coba periksa lagi halaman **Staff**.

![ujicoba4](https://drive.google.com/uc?export&id=17rZ4KzgyZw2ptBrDYG9Z-jtHc_tBoalG)

Berikutnya coba lakukan update data. Klik tombol **Edit** yang ada di dekat tombol **Hapus**.

![ujicoba5](https://drive.google.com/uc?export&id=1BbMEZrItbPoH9E1DtlkwHctsjm-Y5Vzz)

Hasilnya...

![ujicoba6](https://drive.google.com/uc?export&id=14BFtt_VCxbVQDIAEn2rj0x-oc1-0lakE)

# Fitur Untuk Menghapus Data

Terakhir…

Kita belum membuat fungsi konfirmasi pada tombol **Hapus**.

Mengapa kita perlu konfirmasi?

Karena tindakan ini berbahaya.

Bisa saja nanti terjadi salah klik, kalau tidak dikonfirmasi data bisa hilang.

Dan ini tentu akan menjadi pengalaman buruk bagi pengguna.

Sebenarnya pada tahapan ini, kita hanya akan membuat satu fungsi Javascript saja.

Karena kita memanggilnya pada tombol **Hapus**.

Perhatikan view `list.php`.

```html
<a onclick="deleteConfirm('<?php echo site_url('admin/staff/delete/'.$staffv->staff_id) ?>')"
    href="#!" class="btn btn-small text-danger"><i class="fas fa-trash"></i> Hapus</a>
```

Di sana ada *event onclick* yang akan memanggil fungsi `deleteConfirm()`. Ini adalah fungsi javascript, bukan PHP.

Fungsi ini nanti akan menampilkan sebuah modal konfirmasi.

Oke, tapi di mana kita akan menulis kode Javascript?

Ada dua tempat yang bisa kita gunakan:

1. Embed langsung di dalam view.
2. Membuat file Javascript terpisah.

Kita akan menggunakan cara yang pertama, karena fungsi yang kita butuhkan hanya akan digunakan pada view `staffv/list.php` saja.

Jika nanati ada fungsi Javascript yang digunakan di beberapa view, maka sebaiknya membuat file terpisah.

Baiklah, silahkan buka file <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `views/admin/staffv/list.php`, kemduian tambahkan kode berikut di bagian bawah, sebelum tutup `<body>`.

```html
<script>
function deleteConfirm(url){
	$('#btn-delete').attr('href', url);
	$('#deleteModal').modal();
}
</script>
```

Sehingga akan menjadi seperti ini:

![ujicoba7](https://drive.google.com/uc?export&id=1lavpNrgSkCwt0qglXi3g4Hn6MkUAAejT)

Setelah itu, tambahkan sebuah modal untuk delete di dalam file <img class="emoji" draggable="true" alt="folder" src="/icon/file-icon.svg"> `views/admin/_partials/modal.php`.

```html
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

Sehingga akan menjadi seperti ini :

![ujicoba8](https://drive.google.com/uc?export&id=17SogRp3hCeFYk7UofCTXQqYTHyQqJeL5)

Oke, setelah itu coba hapus sebuah data.

![ujicoba9](https://drive.google.com/uc?export&id=1xjDqDiAR3mMESad12Z_nZZpIdIMe6l9t)

Akhirnya selesai juga… 😫

> 1. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Database</s>
2. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Konfigurasi Codeigntier</s>
3. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Model untuk Tabel</s>
3. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Controller</s>
4. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat View</s>
5. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Form Add</s>
6. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Form Edit</s>
7. <img class="emoji" draggable="true" alt="check" src="/icon/checkbox2.svg"> <s>Membuat Fitur Hapus Data</s>

# Apa Selanjutnya?

Kita memang sudah selesai membuat CRUD (Create, Read, Update, Delete) untuk products dan sudah dapat ditampilkan dengan baik menggunakan datatables.

Tapi masih ada fitur yang belu kita buat, seperti:

 * [Tutorial SIMKEP dengan Codeiniter #6: Membuat Fitur Login](https://kos-it.github.io/post/tutorial-projek-1-bagian-6/)
 * [Tutorial SIMKEP dengan Codeiniter #7: Membuat Fitur Upload Gambar](https://kos-it.github.io/post/tutorial-projek-1-bagian-7/)
 * Tutorial SIMKEP dengan Codeiniter #8: Membuat Fitur Pencarian (Admin)
 * Tutorial SIMKEP dengan Codeiniter #9: Membuat Template untuk Landing Page
 * Tutorial SIMKEP dengan Codeiniter #10: Membuat Pagination
 * Tutorial SIMKEP dengan Codeiniter #11: Cara Menggunakan Databales dan Optimasi
 * Tutorial SIMKEP dengan Codeiniter #12: Cara Membuat Laporan dengan DomPDF

Karena itu, jangan berhenti sampai di sini…

Nanti (insya’allah) kita akan lanjutkan lagi.

Oya, buat kamu yang butuh source code dari tutorial ini. Kamu bisa mendownloadnya di Github.

[🎁 [Download Source Code](https://github.com/taqwa26/SIMKEP-Sistem-Menejement-Kepanitiaan)]

…dan apabila ada error dan kamu kesulitan mengikuti tutorial ini, silahkan bertanya di komentar.

# Tutorial Sebelumnya :

 * [Tutorial SIMKEP dengan Codeiniter #1 : Pengenalan Codeigniter](https://kos-it.github.io/post/tutorial-projek-1-bagian-1/)
 * [Tutorial SIMKEP dengan Codeiniter #2: (Controller) MVC dan Routing, Konsep dasar CI yang Harus Dipahami](https://kos-it.github.io/post/tutorial-projek-1-bagian-2/)
 * [Tutorial SIMKEP dengan Codeiniter #3: (View) Cara Menggunakan Bootstrap pada Codeiniger](https://kos-it.github.io/post/tutorial-projek-1-bagian-3/)
 * [Tutorial SIMKEP dengan Codeiniter #4: (View) Membuat Template Admin](https://kos-it.github.io/post/tutorial-projek-1-bagian-4/)