---
title: Panduan Pindah Ke GNU/Linux (+Sedikit Cerita)
lang: id_ID
layout: post
tag: catatan
---
## Kata Pengantar
> Memberi gambaran dan panduan untuk migrasi ke GNU/Linux

Mereka yang hendak bermigrasi ke GNU/Linux membutuhkan gambaran dan panduan. Inilah alasan saya menulis catatan ini.

## Apa itu Linux?
Komputer bukan hanya tentang Windows. Ada beberapa operasi sistem yang bisa anda gunakan, antara lain GNU/Linux, BSD, Android, Haiku, dan masih banyak lagi. Apakah operasi sistem selain Windows bagus? Tergantung dari mana anda menilai.

Pernahkah anda mendengar [Linux](https://id.wikipedia.org/wiki/Linus_Torvalds)? Jika anda antusias di dunia teknologi mungkin tahu kernel ini. Linux adalah kernel yang dibuat oleh [Linus Torvalds](https://id.wikipedia.org/wiki/Linus_Torvalds) pada 17 September 1991. Dengan lisensi [GNU GPLv2](https://id.wikipedia.org/wiki/Lisensi_Publik_Umum_GNU), anda bisa mendapatkannya, mendistribusikan, dan memodifikasinya.

Tahukah kamu jika Linux 'mendominasi' teknologi? Salah satu buktinya adalah Android. Ponsel genggam kebanyakan ditenagai oleh [Android yang menggunakan kernel Linux](https://source.android.com/devices/architecture/kernel/android-common). Kalau tidak percaya, cobalah melihat detail ponsel genggam di handphone anda. Disitu akan muncul kernel yang digunakan, misalnya kernel 3.10, 4.4, 4.9, dan lain - lain.

## Lalu apa itu GNU/Linux?
Paragraf ini dikutip dari laman [Linux dan sistem GNU](https://www.gnu.org/gnu/linux-and-gnu.id.html)

Di awal tahun 1990-an, Tim GNU telah berhasil menyatukan keseluruhan komponen-komponen di luar kernel. Mereka baru saja mulai mengembangkan kernel, [GNU Hurd](https://www.gnu.org/software/hurd/hurd.html), yang digunakan oleh Mach. Pengembangan kernel ini kenyataannya lebih sulit dari yang mereka bayangkan.

Berkat kernel Linux, TIM GNU tidak perlu menunggu rampungnya pengembangan Hurd. Saat Linux dirilis, secara tidak langsung Torvalds telah membantu penyempurnaan sistem GNU. Kombinasi Linux dan sistem GNU merupakan sebuah sistem yang sempurna: yaitu versi sistem GNU berbasis Linux, atau singkatnya sistem GNU/Linux.

### Kenapa banyak sekali distribusi Linux?
> Dalam konteks ini, linux diartikan sebagai distro, bukan kernel.

Cobalah anda mencari dengan kata kunci `download linux` di mesin pencari. Maka akan muncul rekomendasi - rekomendasi, seperti download linux trisquel, download linux parabola, download linux devuan, dan lain - lain. Kenapa distribusi Linux beragam? Kembali lagi ke lisensi linux. Dengan lisensi GNU GPLv2, anda dapat mendapatkannya, memodifikasikan, dan mendistribusikan ulang Linux. Dengan itu, banyak komunitas atau perusahaan membuat distro Linux, misal [Manjaro](https://manjaro.org/), [Oracle Linux](https://www.oracle.com/linux/), [Arch Linux](https://archlinux.org/), dan masih banyak lagi.

Kebanyakan dari keberagaman distro hanyalah turunan dari distro Linux tertentu, apa maksudnya? Ratusan distribusi linux umumnya lahir dari distro tertentu, nama lainnya `distro turunan`, contohnya **Linux Mint turunan dari Ubuntu, lalu Ubuntu turunan dari Debian, dan Debian adalah basisnya**, **Manjaro adalah turunan dari Arch Linux dan Arch Linux adalah basisnya**, dan lain - lain.

Keberagaman distribusi Linux menjadi masalah bagi pemula, manakah yang harus dipilih? Setiap distribusi memiliki pasar dan tujuan tersendiri.
- Jika anda hanyalah pengguna biasa, distribusi [Devuan](https://devuan.org), [MX Linux](https://mxlinux.org/), [Linux Mint](https://linuxmint.com/), [OpenSuse](https://opensuse.org), dan [Fedora](https://getfedora.org/) cocok untuk digunakan.
- Jika anda menggunakan Linux sebagai server, distribusi [Red Hat](https://www.redhat.com/), [Debian](https://debian.org), [Ubuntu](https://ubuntu.com), dan [Alpine Linux](https://www.alpinelinux.org/) bisa dipilih.
- Jika anda ingin bermain game, distribusi [Garuda Linux](https://garudalinux.org/) dan [Drauger OS](https://draugeros.org/) dapat diandalkan.

### Kebanyakan Distro Linux Tidak 100% Bebas.
Sayang sekali anda kebanyakan distribusi Linux tidak benar 100% bebas. Rata - rata distribusi Linux membawa paket [*Proprietary Software*](https://malsasa.wordpress.com/2016/04/07/apa-itu-proprietary-software/). Paket - paket *proprietary* biasanya digunakan untuk *firmware*, *driver*, dan lain - lain.

Untungnya sudah ada distribusi linux yang 100% bebas, misalnya :
- [Dragora GNU/Linux-libre](https://dragora.org/en/index.html)
- [GUIX GNU/Linux](https://www.gnu.org/software/guix/)
- [Parabola GNU/Linux-libre](https://www.parabola.nu/)
- [Trisquel GNU/Linux](https://trisquel.info/)
- [PureOS](https://pureos.net/)

Bukan berarti untuk mencapai kebebasan penuh, anda harus menginstall distribusi di atas. Ada cara lain, yaitu membuang paket - paket *proprietary* yang terinstall dan hanya menggunakan repositori berisi *free software*.

## Kenapa  GNU/Linux?
GNU/Linux bisa untuk apa saja. Ratusan orang setiap hari mencari informasi dan memasang operasi sistem Linux. Mereka yang memasang GNU/Linux biasanya tertarik karena :
- **Gratis**. Linux bisa didapatkan secara gratis.
- **Lebih aman**. Meskipun setiap operasi sistem tidak ada yang aman. Jika dibandingkan dengan Windows, Linux lebih aman dari virus.
- **Mudah dikustomisasi**. Anda bisa memodifikasi GNU/Linux sesuai keinginan anda, mulai dari tampilan hingga ke kernelnya.
- **Ringan**. Tidak seperti Windows yang membutuhkan sumber daya besar. GNU/Linux dapat berjalan baik di spesifikasi mana saja, meskipun laptop anda berspesifikasi rendah dan [perangkat IoT](https://www.niagahoster.co.id/blog/iot-adalah/).

#### Alasan Saya Pindah Ke GNU/Linux
Saya antusias dengan berita teknologi. Suatu hari tidak sengaja menemukan CD [Debian Woody](https://www.debian.org/releases/woody/), akhirnya saya mencari infomrasi tentang GNU/Linux. Waktu itu saya hanya sebatas membaca saja, tidak mencoba.

Di tahun 2020, saya kembali membaca Linux setelah punya [laptop pribadi](https://support.lenovo.com/id/en/solutions/pd100280-detailed-specifications-thinkpad-t440p). Distro pertama saya adalah Linux Mint. Instalasi secara *single boot*, saya menghapus Windows.

Alasan saya pindah ke Linux awalnya ingin mencoba dunia baru. Saya membaca informasi tentang Linux kalau operasi sistem ini mudah dimodifikasi, tersedia [gratis secara kebebasan](https://en.wikipedia.org/wiki/Free_as_in_Freedom), dan lain - lain.

## Bagaimana Cara Migrasi Ke GNU/Linux Secara Penuh
Saya akan menulis pengalaman saya bermigrasi ke GNU/Linux secara penuh. Sampai catatan ini ditulis, saya hanya memasang operasi sistem GNU/Linux di laptop. Juga sedikit program proprietary yang terinstall, antara lain *Firmware-intel* dan *Fonts Microsoft Office*.
### Niat
Saya memiliki niat besar untuk mempelajari dan menggunakan GNU/Linux, akhirnya saya pasang secara *single boot*. Artinya tidak ada operasi sistem lain, selain GNU/Linux.

Jika anda ingin bermigrasi secara penuh, pastikan anda memiliki tekad kuat untuk menggunakan GNU/Linux. Kalau niatnya masih rendah, mungkin migrasinya hanya setengah - setengah.

### Berani Belajar dan Menanggung Resiko
Pindah dari zona nyaman itu tidak enak, menakutkan, dan menyusahkan. Ketika anda bermigrasi ke GNU/Linux, anda harus mau untuk belajar dan menanggung resiko. 

Contoh yang paling besar adalah resiko tidak ada Microsoft Office di Linux. Sebagian pemula tidak berani menggunakan [LibreOffice](https://www.libreoffice.org/) karena tidak sama seperti Microsoft Office, mereka takut hasilnya rusak, dokumennya bermasalah, dan lain - lain. Padahal tidak selalu hasil dari Libreoffice buruk. 

Saya sudah membuktikannya selama setahun menggunakan LibreOffice, dokumen - dokumen yang saya tulis menggunakan Libreoffice. Yang namanya dokumen bermasalah ketika diakses di Microsoft Office sangatlah jarang. Jika ada masalah, mudah sekali untuk memperbaikinya.

> Tapi, yang lebih menakutkan dari apapun yang pernah kita takutkan adalah kalau kita terus-terusan merasa takut.

### Sedikit Memaksa.
Saat bermigrasi ke GNU/Linux, saya memaksa diri saya untuk hanya menggunakan program *free software*. Jika tidak dipaksa, apakah saya bisa bermigrasi secara penuh? Saya mulai menggunakan [Mozzila Firefox](https://www.mozilla.org/en-US/firefox/new/) untuk berselancar di Internet, mengolah dokumen dengan [LibreOffice](https://www.libreoffice.org), memilih [GIMP](http://gimp.org/) sebagai editor foto, memakai [Kdenlive](https://kdenlive.org/) untuk mengedit video, dan lain - lain. 

Apakah ada masalah? Pasti ada. Tapi yang namanya masalah selalu ada penyelesaiannya. Alhamdulillah masalah - masalah saya dapat diselesaikan dengan baik. Akhirnya saya sering membaca agar terhindar dari masalah.
