---
title: "Cara Membuat Blog Dengan Hugo"
date: 2022-03-24T14:54:13+08:00
categories: ["Website"]
tags: ["Website", "HTML", "Hugo"]
cover: "/img/hugo.svg"
draft: false
---

Pada panduan ini, kita akan belajar cara ngeblog dengan Hugo dari awal hingga tahap deploy atau hosting.

Mari kita mulai…

Langkah-langkah membuat blog dengan Hugo:

# 1 Instalasi Git, Go, dan Hugo
“Mari kita persiapkan semua alat-alat yang diperlukan”

Diantaranya:

1. `Git` — untuk upload dan deploy Hugo ke repositori git.
2. `Go` — bahasa pemrograman Go.
3. `Hugo` — Mesin SSG untuk membuat blog.

Berikut cara menginstalnya:

## Install Git di Linux:

Untuk menginstal Git di Linux, silahkan ketik perintah berikut.
```
apt install git
```
Setelah itu, periksa versi yang terinstal dengan perintah:
```
git --version
```

## Install Go di Linux:

Ada dua cara yang bisa dilakukan untuk menginstal Go di Linux.

1. Menginstal melalui apt atau manajemen paket yang lainnya;

2. Menginstal manual dengan men-download dari website resminya.

Untuk menginstal melalui apt, silahkan ketik perintah berukut:
```
apt install go
```
Setelah itu periksa versi yang terinstal dengan perintah:
```
go version
```

## Install Hugo di Linux:

Hugo juga bisa diinstal melalui apt dan manual…

…tapi saya lebih menyarankan menginstal manual.

Karena versi yang di repositori apt, masih versi lama.

Donwload Hugo:

Silahkan buka repositori hugo, ambil versi Hugo yang akan diinstal.

Sebagai contoh:

Saya akan menginstal versi Hugo 0.24.1 di Linux 64-bit:
```
wget https://github.com/gohugoio/hugo/releases/download/v0.24.1/hugo_0.24.1_Linux-64bit.deb
```
Setelah itu instal dengan dpkg atau apt deb:
```
apt deb hugo_0.24.1_Linux-64bit.deb
```
Setelah itu…

buka terimal baru dan ketik perintah:
```
hugo version
```
Semua sudah beres…

Selanjutnya mari kita mulai membuat blog.

# 2. Membuat Blog Baru dengan Hugo

Hugo menyediakan perintah berikut untuk membuat blog baru:
```
hugo new site [nama-blog]
```

Sebagai contoh Saya akan membuat blog bernama TempeTahu:
```
hugo new site TempeTahu
```
Maka Hugo akan membuatkan direktori baru beserta strukturnya.
![hugo_site](https://drive.google.com/uc?expand&id=146ouHKXvm2ZfrVFIrJ9toFwB8lsAO0Vr)
Silahkan dibuka direktori tersebut dengan teks editor dan coba jelajahi isinya.

Masih kosong?

Ya benar sekali, kita harus membut isinya dari nol 😄.

Tenang saja…

Tidak sulit kok.

Tapi sebelumnya mari kita kenalan dulu dengan direktori-direktori tersebut.

# 3. Mengenal Struktur Direktori Hugo
Ada enam buah direktori dan satu file yang dibuatkan oleh Hugo.
## direktori _archetype_
Direktori ini berisi _archetype_ atau template _Front Matter_ dari konten.
![hugo_site](https://drive.google.com/uc?expand&id=18Ily8DxyxNQR5yV1W1fvKIqMD17aPsgI)
Misalkan kita punya lebih dari satu jenis konten:

Ada artikel, portofolio, produk, proyek, podcast, dll.

Maka kita harus membuatkan _archetype_ untuk masing-masing jenis konten tersebut.

Mari kita coba membuat archetype default.

Silahkan tambahak file `default.md` di dalamnya, kemudian isi dengan kode berikut.

```md
+++
title = "{{ replace .TranslationBaseName "-" " " | title }}"
date = "{{ .Date }}"
draft = true
+++
```
archetype ini akan menjadi archetype default setiap kali kita membuat konten.
## direktoori _content_
Sudah bisa ditebak, isi dari direktori ini adalah konten dari blog kita.

Format kontennya adalah markdown.

Contoh konten milik Kos-IT:
![hugo_site](https://drive.google.com/uc?expand&id=1hpBGheBhKM5gv58qy2J93I43BRejQQfV)
Kos-IT menggunakan _archetype_ post dan project untuk artikel biasa, sedangkan untuk halaman seperti about, contact, portofolio, dll…

…Kos-IT menggunakan _archetype_ page.
## direktori _data_
Direktori ini berisi data-data dalam format JSON, YAML, TOML dan lain-lain.

Data ini bisa kita manfaatkan pada tema.

Misal:

Agar tidak repot mengetik link sosial media pada tema, kita bisa membuatkan datanya.
```md
facebook = "https://facebook.com/kos-it"
twitter = "https://twitter.com/kos-it"
instagram = "https://instagram.com/kos-it"
googleplus = "https://google.com/+kos-it"
```
Nanti pada pembuatan tema, kita bisa panggil seperti ini:
```html
<a href="{{ .Data.facebook }}">Facebook</a>
```
## direktori _layout_
Direktori ini berisi file HTML untuk tema atau layout blognya.

Jika kita ingin membuat tema _default_-nya, kita bisa letakkan di sini.

## direktori _static_
Direktori ini berisi file-file statis seperti CSS, javascript, Gambar, dan sebagainya.

Nanti kita akan pakai direktori ini untuk menyimpan gambar dan file aset lainnya.

## direktori _themes_
Seperti namanya, direktori ini tempat menyimpan tema-tema Hugo.

Kita bisa menaruh beberapa tema di dalamnya, kemudian untuk menggunakannya…

…kita harus menentukannya di file konfigurasi `config.toml`.

## File `config.toml`
File ini berisi konfigurasi blognya.

Contoh konfigurasi milik Kos-IT:
```
baseurl = "https://kos-it.github.io"
title = "KOS-IT — Making and Developing"
languageCode = "id-id"

theme = "programmer"
themesdir = "themes"

paginate = 4

disqusShortname = "kos-it-github-io"
googleAnalytics = "UA-XXXXXXXX-X"

[author]
    name = "Karcaqs"
    homepage = "https://web.facebook.com/taqwa.prakoso"
    bio = "Sejenis Terong"
    image = "/img/karcaqs.svg"
    email = "taqwaalmutawakkil97@gmail.com"

pygmentsstyle = "monokai"
pygmentsuseclasses = true
```
Sekarang coba ganti konfigurasi blog yang sudah dibuat…
```
baseURL = "https://www.tempetahu.com/"
languageCode = "id-id"
tite = "TempeTahu"
```
Variabel baseURL dan title wajib diisi.

Silahkan isi dengan alamat blog-nya.
# 4. Menambahkan Tema Hugo
Hugo memiliki banyak kontributor yang membuat tema dan disebarkan secara gratis.

Silahkan cari tema yang kalian sukai di: https://themes.gohugo.io/

Pilih tema yang mana saja.

Tapi perlu diingat:

“Baca dulu dokumentasi tema-nya, karena di sana ada konfigurasi yang harus diikuti agar temanya bisa digunakan sesuai harapan”

Contoh:

Saya akan memilih tema [Hello Programmer](https://themes.gohugo.io/themes/hugo-hello-programmer-theme/)…

…maka kita harus membuat konfigurasi seperti ini:
```md
baseURL = "https://www.tempetahu.com/"
languageCode = "id-id"
tite = "TempeTahu"
theme = "programmer"
disqusShortname = "XXXX"
googleAnalytics = "UA-XXXXXXXX-X"
paginate = 7

[author]
    name = "your-name"
    email = "your-email"

[params]
    description = "desribe-your-site"
```
Setelah itu kita tambahkan temanya…

Silahkan masuk ke direktori `tempetahu/themes` melalui terminal (sesuaikan dengan nama blog-mu).
```bash
cd tempetahu/themes/
```
Setelah itu, gunakan Git untuk klon repositori temanya.
```bash
git clone https://github.com/parsiya/Hugo-Octopress.git
```
Tunggu sampai selesai…

Setelah itu, pindah ke direktori root blognya dan jalankan server hugo.
```bash
cd ..
hugo server
```
Maka hugo akan membuat server baru pada alamat http://localhost:1313.
![hugo_server](https://drive.google.com/uc?expand&id=18QXNymzk44DNdbIaaMQ-dkBIT3ia9NQI)
Silahkan buka alamat tersebut…
![hugo_view](https://drive.google.com/uc?expand&id=1VllY24eErE1pqAx2SZnz3EWO-9ju0H50)

🎉 berhasil…

Kita sudah berhasil menambahkan temanya, selanjutnya kita akan coba menambahkan konten.

# 5. Menulis Artikel di Blog Hugo
Jika pada CMS seperti Wordpress, kita mengisi konten melalui halaman admin…

…maka pada Hugo kita gunakan teks editor.

Pertama:

Silahkan buat kotennya melalui terminal.

Hugo sudah menyediakan perintah hugo new untuk membuat konten.
```
hugo new post/[nama-file-konten].md
```
Contoh:
```
hugo new post/tempe-vs-tahu.md
```
Maka file baru akan dibuat pada direktori `content/post/` dengan nama `tempe-vs-tahu.md`.
![hugo_post](https://drive.google.com/uc?expand&id=1iE_wAB3WBbsu4QaIwvBRV0kIJB00NzVh)
Silahkan buka file tersebut, modifikasi dan tambahkan isinya:
![hugo_post](https://drive.google.com/uc?expand&id=12mjK4H156XYpm4-COIIhnJbaTI5GdFEB)
Jangan lupa mengubah nilai `draft` pada _Front Matter_ menjadi `false`.

Setelah itu, simpan, jalankan server…

…dan coba lihat perubahannya sekarang.

![hugo_artikel](https://drive.google.com/uc?expand&id=1YRC9fJlP0GhpjceRi2I_6y5juO_35Spz)

# 4. Deploy Hugo ke Server
Hugo bisa di-_deploy_ di mana saja:

Github, Gitlab, BitBucket, Heroku, Google Cloud, Shared Hosting, dan sebagainya.

Berbagai cara deploy hugo bisa dibaca di [dokumentasinya](https://gohugo.io/hosting-and-deployment/hosting-on-github/).

Tapi, bila belum paham…

Coba baca catatan saya: [Cara Deploy Hugo di Github Pages.](#)

# Apa Selanjutnya?
Sepertinya terlihat susah ya…

Tapi tenang saja, karena ini masih awal.

Saya juga seperti itu, waktu pertama kali mencoba…

…banyak sekali error dan masalah yang didapatkan.

Namun, masalah itu akan membuat kita lebih paham.

Selanjutnya, mungkin kamu tertarik:

* [Membuat Tema Hugo Sendiri dari Nol]()

Atau masih bingung?

Silahkan tanyakan di komentar!