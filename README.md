Nama : Kintan Kinasih Mahaputri
NIM : H1D022019
Shift: A

Cara kerja proses login pada Ionic, mulai dari pengaturan database hingga implementasi pada aplikasi:

1. **Pembuatan Database dan Tabel User**: Dibuat database bernama `coba-ionic` beserta tabel `user` yang berisi kolom `username` dan `password`. Data pengguna diisi secara manual, dan kata sandi disimpan dalam bentuk hash menggunakan fungsi MD5 untuk keamanan tambahan.

2. **Membangun API Backend Menggunakan PHP**: Dibuat dua file PHP, yaitu `koneksi.php` untuk menghubungkan aplikasi dengan database, dan `login.php` untuk menangani proses autentikasi. Pada `login.php`, data `username` dan `password` yang dikirim dalam format JSON akan diverifikasi dengan data di database. Jika cocok, server akan mengembalikan status "berhasil" bersama token sederhana berupa timestamp. Jika tidak, status "gagal" akan diberikan.

3. **Membuat Frontend Login dengan Aplikasi Ionic**: Menggunakan framework Angular, aplikasi Ionic dibangun dengan modul dan halaman yang diperlukan. Modul `@capacitor/preferences` diinstal untuk menyimpan data token dan `username` secara lokal di perangkat pengguna.

4. **Membuat Service untuk Autentikasi (authentication.service.ts)**: Service ini menangani permintaan POST ke `login.php` pada server API. Selain itu, service ini menyimpan token dan `username` di perangkat menggunakan `Preferences`. Fungsi `postMethod()` digunakan untuk mengirim data login ke server, sementara `saveData()` dan `clearData()` menyimpan dan menghapus data autentikasi di perangkat.

5. **Menambahkan Guard untuk Mengamankan Halaman (auth.guard.ts dan auto-login.guard.ts)**: `authGuard` berfungsi melindungi halaman `home` sehingga hanya pengguna yang telah login yang dapat mengaksesnya. Sementara itu, `autoLoginGuard` mencegah pengguna yang sudah login mengakses kembali halaman login dengan mengarahkan mereka langsung ke halaman `home`.

6. **Mengonfigurasi Routing pada app-routing.module.ts**: Konfigurasi routing diatur agar halaman `home` hanya dapat diakses oleh pengguna yang telah login dengan perlindungan dari `authGuard`, sementara halaman login dilindungi oleh `autoLoginGuard` untuk pengguna yang sudah login.

7. **Implementasi Halaman Login (login.page.ts dan login.page.html)**: Halaman login dilengkapi dengan formulir input `username` dan `password`. Tombol login menjalankan fungsi `login()`, yang mengirimkan data ke service autentikasi untuk validasi. Jika berhasil, pengguna diarahkan ke halaman `home`. Jika gagal, notifikasi kesalahan akan muncul.

8. **Implementasi Halaman Home (home.page.ts dan home.page.html)**: Pada halaman `home`, aplikasi menampilkan pesan selamat datang kepada pengguna yang telah login. Terdapat tombol logout yang memanggil fungsi `logout()` pada service autentikasi, yang akan menghapus data token dan mengembalikan pengguna ke halaman login.

9. **Komponen Notifikasi**: Menggunakan `AlertController` dari Ionic untuk menampilkan pesan kesalahan atau konfirmasi login kepada pengguna. 

