---
title : Cara Install Gentoo Dengan Cepat (BIOS/MBR)
layout : post
tag : catatan
---

Saya menggunakan [Gentoo GNU/Linux](https://gentoo.org) yang menggantikan [Devuan GNU/Linux](https://devuan.org). Kenapa ganti distro? Karena kata orang, distro ini cocok untuk optimalisasi yang ingin saya lakukan agar mendapatkan performa lebih baik.

Sayang sekali, Gentoo GNU/Linux tidak menyediakan instalasi secara GUI. Hampir mirip dengan [Arch GNU/Linux](https://archlinux.org), namun lebih rumit Gentoo GNU/Linux. Anda diharuskan *compile* sebagian paket selama penginstallan.

Kali ini saya akan membuat catatan instalasi Gentoo GNU/Linux dengan ringkas dan mudah. Tentunya keringkasan ini mempunyai beberapa kekurangan yang mungkin anda rasakan karena **terlalu ringkas**.

## Apa itu Gentoo Linux
Gentoo adalah sistem operasi gratis berbasis Linux yang dapat dioptimalkan dan disesuaikan keinginan anda untuk semua kebutuhan.

Konfigurasi yang ekstrim, kinerja, dan komunitas pengguna dan pengembang terbaik adalah keunggulan dari pengalaman Gentoo.

Singkatnya, Gentoo Linux adalah distro berbasis kode sumber yang mengharuskan anda membangun paket dari sumbernya, kecuali anda lebih memilih paket yang sudah ada binary.

## Cara Install Gentoo 
Kali ini saya akan membuat catatan instalasi Gentoo GNU/Linux dengan ringkas dan mudah. Tentunya keringkasan ini mempunyai beberapa kekurangan yang mungkin anda rasakan karena **terlalu ringkas**.

### Membuat Bootable ISO
Unduh *Minimal Installation CD* di [website Gentoo](https://www.gentoo.org/downloads/). Lalu *burn* ISO ke flashdisk/memory card dengan aplikasi favorit, misalnya [Balena Etcher](https://www.balena.io/etcher/) dan [Rufus](https://rufus.ie/en/).

### Booting ISO
Lakukan booting dari Flashdisk. Setiap laptop punya cara berbeda, misalnya Laptop Thinkpad bisa booting dari Flashdisk menggunakan menu Boot Order dengan tombol **F12/F10**

### Menyambungkan WIFI dengan wpa_cli
Bootable ISO Gentoo menggunakan [wpa_supplicant](https://wiki.archlinux.org/title/wpa_supplicant) untuk menyambungkan WIFI.

Pertama kita buat file wpa_supplicant.conf dengan editor.
```
$ sudo vim /etc/wpa_supplicant/wpa_supplicant.conf
```
```
ctrl_interface=/run/wpa_supplicant
update_config=1
```

Selanjutnya kita jalankan perintah `wpa_cli`.
```
$ sudo wpa_cli
```

Kita pindai jaringan wifi yang tersedia dengan perintah `scan`.
```
> scan
OK
<3>CTRL-EVENT-SCAN-STARTED
<3>CTRL-EVENT-SCAN-RESULTS
<3>WPS-AP-AVAILABLE
```

Setelah melakukan pemindaian, hasil bisa dilihat dengan perintah `scan_results`.

```
> scan_results
bssid / frequency / signal level / flags / ssid
00:11:22:33:44:55       2450    -30     [WPA-PSK-CCMP][WPA2-PSK-CCMP][ESS]	linux
```

Saya ingin menyambungkan WiFI bernama linux, maka kita tambahkan ke daftar jaringan dengan perintah `add_network`.
```
> add_network
0
```
Kemudian kita isi kredensial jaringan linux dengan perintah berikut.
```
> set_network 0 ssid "linux"
OK
> set_network 0 psk "linuxuntuksemua"
OK
```
Jika tidak memiliki password, gunakan perintah 
```
> set_network 0 ssid "linux"
OK
> set_network 0 key_mgmt NONE
OK
```

Kalau sudah mengisi kredensial, saatnya menghubungkan dengan perintah `enable_network X`. X adalah angka yang didapatkan. Karena tadi saya mendapatkan 0, maka saya mengganti X dengan 0.

```
> enable_network 0
OK
```
Jika berhasil menyambungkan, akan muncul seperti ini.
```
<3>CTRL-EVENT-CONNECTED - Connection to 00:11:22:33:44:55 completed [id=0 id_str=]
<3>CTRL-EVENT-REGDOM-CHANGE init=CORE type=WORLD
```
### Memformat Drive
Kali ini kita akan mengatur partisi di drive. Saya akan membuat partisi / (atau yang biasa disebut ROOT) saja.

Jalankan perintah `cfdisk /dev/sdX` untuk mengatur. Sesuaikan X dengan milik anda, misal saya ingin menginstall di sda, maka yang saya jalankan adalah
```
root # cfdisk /dev/sda
```
Jika anda belum tahu caranya, bisa baca [artikel ini](http://sohibuna.blogspot.com/2013/02/membuat-partisi-menggunakan-cfdisk-di.html).

Saya ingin menggunakan filesistem [ext4](https://wiki.archlinux.org/title/ext4), maka yang saya lakukan adalah
```
root # mkfs.ext4 -L ROOT /dev/sda1
```
Sesuaikan dengan partisi kalian.

### Mount Partisi
Sekarang kita akan *mount* partisi dengan cara berikut.
```
root # mkdir -p /mnt/gentoo
root # mount /dev/sda1 /mnt/gentoo
root # mkdir /mnt/gentoo/boot
root # mount /dev/sda1 /mnt/gentoo/boot
```

### Mengunduh Stage3
Pertama kita ganti direktori ke /mnt/gentoo
```
root # cd /mnt/gentoo
```

Unduh [stage3 tarball](https://wiki.gentoo.org/wiki/Stage_tarball) sesuai keinginan masing - masing, misalnya ingin [OpenRC](https://en.wikipedia.org/wiki/OpenRC) atau [systemd](https://en.wikipedia.org/wiki/Systemd).
<hr>
> *Bagusnya pilih yang mana?*

Saya lebih memilih OpenRC, karena tidak terlalu *sreg* dengan systemd.
<hr>
Untuk mengunduh stage3, bisa menggunakan perintah 
```
root # links https://www.gentoo.org/downloads/
```
atau
```
root # wget https://bouncer.gentoo.org/fetch/root/all/releases/amd64/autobuilds/20211226T170559Z/stage3-amd64-openrc-20211226T170559Z.tar.xz
```
Sekali lagi, sesuaikan keinginan kalian.

Setelah selesai mengunduh, ekstrak file.
```
root # tar -xf stage3*
```

### Chroot
Kita akan chroot stage 3
```
root # mount -t proc none /mnt/gentoo/proc
root # mount --rbind /sys /mnt/gentoo/sys
root #mount --rbind /dev /mnt/gentoo/dev
root # cp /etc/resolv.conf etc && chroot . /bin/bash
root # source /etc/profile
```

Perbarui repositori Gentoo GNU/Linux
```
root # emerge-webrsync
root # emerge --sync
```

### Menentukan Profil
Kita akan menentukan profil yang sangat penting karena profil mendefinisikan fungsi-nya. 
```
root # eselect profile list
```
Sesuaikan keinginan anda. Kalau versi saya memilih list profil 1.
```
root # eselect profile set 1
```

### Mengatur Waktu
Tentukan waktu sesuai bagian anda.
```
root # ln -sf /us/share/zoneinfo/Asia/Jakarta /etc/localtime
```

### Pemasangan Kernel
Kita akan memasang kernel. 

#### Kernel dari kode sumber
Bagian ini sedikit melelahkan karena prosesnya lama, tergantung konfigurasi anda. 

Unduh kode sumber dari kernel.
```
root # emerge gentoo-sources
```

Ganti ke direktori kode sumber kernel dan melakukan konfigurasi. Sesuaikan konfigurasi sesuai keinginan anda.
```
root # cd /usr/src/linux
root # make menuconfig
```

Terakhir lakukan membangun kernel.
```
root # make && make modules_install && make install
```

#### Kernel Binary
Alhamdulillah ada solusi jika anda tidak ingin membangun kernel dari awal. Caranya dengan menggunakan [gentoo-kernel-bin](https://packages.gentoo.org/packages/sys-kernel/gentoo-kernel-bin).
```
root # emerge gentoo-kernel-bin
```

### Memasang Linux Firmware
[Linux firmware](https://wiki.gentoo.org/wiki/Linux_firmware) sangat penting karena berisi firmware dan modul, misalnya modul untuk WiFi, Bluetooth, dan lain - lain. Jadi kalau tidak diunduh, bisa saja WiFi anda tidak berjalan.
```
root # emerge linux-firmware
```

### Memasang GRUB2
[GRUB2](https://wiki.gentoo.org/wiki/GRUB2) adalah bootloader yang biasa digunakan di Linux.
```
root # emerge sys-boot/grub:2
```
Jika sudah jangan lupa pasang GRUB2 di partisi kalian, misalnya partisi Gentoo saya ada di /dev/sda.
```
root # grub-install /dev/sda
root # grub-mkconfig -o /boot/grub/grub.cfg
```

### Memasang Network Manager
[Network Manager](https://wiki.gentoo.org/wiki/NetworkManager) adalah salah satu program yang biasa saya gunakan untuk menyambungkan WiFi dan Ethernet.
```
root # emerge networkmanager
root # rc-update add networkmanager default
```

### Memasang DHCP
[Dynamic Host Configuration Protocol Client Daemon](https://wiki.gentoo.org/wiki/Dhcpcd) adalah klien DHCP populer yang untuk mengelola konfigurasi IPv4 dan IPv6.
```
root # emerge dhcpcd
root # rc-update add dhcpcd default
```

### Mengubah Password Akun Root
Kita akan mengubah password akun root, sesuaikan dengan keinginan anda.
```
root # passwd root
```
### Membuat Akun Baru
Kita buat akun baru, nama bisa anda ganti sesuai kebutuhan anda.
```
root # useradd -m -G wheel,audio,video,usb,cdrom -s /bin/bash linus
```
Jangan lupa buat passwordnya juga.
```
root # passwd linus
```

### Umount
Karena proses sudah selesai, jangan lupa umount dan reboot.
```
root # exit
root # umount /mnt/gentoo 
root # reboot
```

## Akhir Kata
Demikian catatan instalasi Gentoo GNU/Linux saya, semoga bisa membantu anda dalam menginstall Gentoo GNU/Linux di mesin anda. Jika ada kesalahan, bisa hubungi saya.
