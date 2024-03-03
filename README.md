# Coding Challenge – Backend

Coding challenge ini bertujuan untuk menguji kemampuan Anda dalam mengembangkan backend aplikasi web yang berfungsi sebagai platform berita online dengan menggunakan bahasa pemrograman **Go**. 

Anda perlu melakukan **commit** dan **push** ke repositori ini selama pengerjaan. Waktu pengerjaan adalah selama tiga hari, mulai dari Senin, 4 Maret 2023 hingga **Rabu**, 6 Maret 2023 pukul **23:59**. Setelah melewati batas waktu, peserta tidak dapat lagi melakukan **push** ke repo.

## Kriteria Umum
- Gunakan bahasa pemrograman Go dengan versi minimal 1.21.5
- Gunakan framework Gin untuk membuat web server
- Gunakan library GORM untuk menghubungkan dengan database (jenis database bebas)
- Gunakan https://github.com/samber/do untuk membuat IoC container
- Gunakan arsitektur Clean/Hexagonal/Onion untuk mengatur struktur kode

## Bentuk Response
- Untuk response dengan status sukses, kembalikan JSON dengan format berikut:
```json
{
  "message": "string",
  "data": "any"
}
```
- Untuk response dengan status error, kembalikan JSON dengan format berikut:
```json
{
  "error": "string"
}
```
- Untuk semua route yang memerlukan autentikasi, kembalikan pesan error jika user belum terautentikasi

## Fitur-Fitur
### Login
- Route ini menerima input berupa JSON yang berisi email dan kata sandi user
- Input harus divalidasi dengan ketentuan sebagai berikut:
  - Email: harus diisi, harus berformat email yang valid
  - Password: harus diisi
- Input password harus cocok dengan user yang memiliki email tersebut
- Jika email/password cocok, kembalikan data berupa string JWT token
- Jika email/password tidak cocok, kembalikan pesan error

### User Info
- Route ini memerlukan autentikasi
- Kembalikan data berupa object yang berisi id, email, nama, dan role dari user

### Daftar Berita
- Route ini tidak memerlukan autentikasi
- Berita yang ditampilkan hanya berita yang berstatus "published"
- Kembalikan data berupa object yang berisi judul, slug, dan tanggal berita dibuat

### Detail Berita
- Route ini tidak memerlukan autentikasi
- Berita yang dapat diakses hanya berita yang berstatus "published"
- Berita diakses berdasarkan slug
- Kembalikan data berupa object dengan isi berikut:
  - Judul berita
  - Slug berita
  - Konten berita
  - Pembuat berita
  - Moderator berita
  - Waktu pembuatan
- Kembalikan data berupa null jika berita tidak ada atau tidak berstatus "published"

### Dasbor Daftar Berita
- Route ini memerlukan autentikasi
- Berita yang ditampilkan memiliki kriteria sebagai berikut:
  - Jika akun memiliki role moderator, maka tampilkan berita yang memiliki status "dalam moderasi" atau "published"
  - Jika akun bukan moderator, maka tampilkan hanya berita yang dibuat oleh akun tersebut dengan status apapun
- Kembalikan data berupa object dengan isi berikut:
  - ID berita
  - Judul berita
  - Status berita
  - Waktu pembuatan

### Dasbor Lihat Berita
- Route ini memerlukan autentikasi
- Berita diakses berdasarkan ID
- Hak akses dari berita ditentukan dari role akun:
  - Jika memiliki role moderator, maka dapat mengubah berita dengan status "dalam moderasi" atau "published"
  - Jika bukan moderator, maka hanya dapat mengubah berita yang dibuat oleh akun tersebut dengan status "draft"
- Kembalikan data berupa null jika akun tidak memiliki hak akses atau berita tidak ada
- Kembalikan data berupa object dengan isi berikut:
  - ID berita
  - Judul berit
  - Slug berita
  - Konten berita
  - Pembuat berita
  - Moderator berita
  - Status berita
  - Waktu pembuatan

### Dasbor Buat Berita
- Route ini memerlukan autentikasi
- Route ini hanya dapat diakses oleh akun dengan role bukan moderator
- Route ini menerima input berupa JSON yang berisi judul, slug, dan isi berita
- Input harus divalidasi dengan ketentuan sebagai berikut:
  - Judul: harus diisi, panjang maksimal 255 karakter
  - Slug: harus diisi, panjang maksimal 255 karakter, hanya berisi huruf kecil dan tanda hubung ("-")
  - Isi berita: harus diisi, panjang maksimal 2048 karakter
- Slug harus unik, tidak boleh ada berita lain yang memiliki slug yang sama
- Kembalikan data berupa string yang berisi ID dari berita yang baru dibuat

### Dasbor Ubah Berita
- Route ini memerlukan autentikasi
- Berita diakses berdasarkan ID
- Route ini menerima input berupa JSON yang berisi judul, slug, dan isi berita
- Input harus divalidasi dengan ketentuan sebagai berikut:
  - Judul: harus diisi, panjang maksimal 255 karakter
  - Slug: harus diisi, panjang maksimal 255 karakter, hanya berisi huruf kecil dan tanda hubung ("-")
  - Isi berita: harus diisi, panjang maksimal 2048 karakter
- Slug harus unik, tidak boleh ada berita lain yang memiliki slug yang sama
- Ubah berita hanya dapat dilakukan pada kondisi berikut:
  - Jika role moderator, maka aksi dapat dilakukan pada saat berita berstatus dalam moderasi
  - Jika role bukan moderator, maka aksi dapat dilakukan pada saat berita berstatus draft
- Kembalikan data berupa null jika akun tidak memiliki hak akses atau berita tidak ada

### Dasbor Submit Berita
- Route ini memerlukan autentikasi
- Berita diakses berdasarkan ID
- Route ini hanya dapat diakses oleh akun dengan role bukan moderator
- Akun hanya dapat submit berita yang dibuat oleh akun tersebut dengan status "draft"
- Kembalikan data berupa string jika akun tidak memiliki hak akses atau berita tidak ada
- Kembalikan data berupa null jika berita berhasil diubah

### Dasbor Publikasi Berita
- Route ini memerlukan autentikasi
- Berita diakses berdasarkan ID
- Route ini hanya dapat diakses oleh akun dengan role moderator
- Akun hanya dapat publikasi berita yang dibuat oleh akun tersebut dengan status "dalam moderasi"
- Kembalikan data berupa string jika akun tidak memiliki hak akses atau berita tidak ada
- Kembalikan data berupa null jika berita berhasil diubah

Selamat mengerjakan coding challenge ini dan semoga berhasil. 🌟
