Kali ini kita bakal bahas tentang dasar-dasar mengambil data di MySQL menggunakan perintah `SELECT`. Ini adalah langkah pertama yang penting banget untuk memulai bekerja dengan database. Yuk, kita kupas tuntas!

### **1. Perintah `SELECT`**

Perintah `SELECT` adalah perintah yang digunakan untuk mengambil data dari tabel di database. Ini seperti meminta data yang kita butuhkan dari penyimpanan di database. Bayangkan database itu seperti lemari arsip, dan perintah `SELECT` ini adalah cara kita untuk meminta dokumen tertentu dari lemari itu.

#### **Menampilkan Semua Data**

Kalau temen-temen mau melihat semua data yang ada di tabel, kita bisa menggunakan perintah `SELECT` dengan format sederhana berikut:

```sql
SELECT * FROM nama_tabel;
```

**Penjelasan Kode:**
- `SELECT *` : Asterik (*) di sini artinya ambil semua kolom yang ada.
- `FROM nama_tabel` : `nama_tabel` adalah nama tabel yang datanya ingin kita ambil.

**Contoh Implementasi:**

Misalnya, kita punya tabel `mahasiswa` dengan data seperti berikut:

| id | nama      | jurusan    | umur |
|----|-----------|------------|------|
| 1  | Bahrul Rozak | Teknik Informatika | 22   |
| 2  | Ani        | Sistem Informasi | 21   |
| 3  | Budi       | Teknik Elektro | 23   |

Untuk menampilkan semua data dari tabel `mahasiswa`, kita gunakan perintah:

```sql
SELECT * FROM mahasiswa;
```

Hasilnya bakal menampilkan semua baris dan kolom dari tabel `mahasiswa`.

#### **Menampilkan Kolom Tertentu**

Kadang kita hanya butuh kolom tertentu saja. Misalnya, kita cuma ingin melihat nama dan jurusan mahasiswa. Kita bisa menyebutkan kolom yang ingin kita ambil dengan perintah `SELECT`:

```sql
SELECT nama, jurusan FROM nama_tabel;
```

**Penjelasan Kode:**
- `SELECT nama, jurusan` : Menyebutkan kolom-kolom yang ingin ditampilkan.
- `FROM nama_tabel` : Nama tabel dari mana data diambil.

**Contoh Implementasi:**

Jika kita hanya ingin menampilkan nama dan jurusan dari tabel `mahasiswa`, kita pakai perintah:

```sql
SELECT nama, jurusan FROM mahasiswa;
```

Hasilnya akan seperti ini:

| nama         | jurusan          |
|--------------|-------------------|
| Bahrul Rozak | Teknik Informatika|
| Ani          | Sistem Informasi  |
| Budi         | Teknik Elektro    |

### **Referensi**

Untuk penjelasan lebih lanjut mengenai perintah `SELECT`, temen-temen bisa cek dokumentasi resmi MySQL atau tutorial berikut ini:

- [MySQL SELECT Statement](https://dev.mysql.com/doc/refman/8.0/en/select.html) (MySQL Official Documentation)
- [Tutorial: SQL SELECT Statement](https://www.w3schools.com/sql/sql_select.asp) (W3Schools)

Semoga penjelasan ini membantu temen-temen memahami cara mengambil data dari database dengan `SELECT`! Kalau ada yang mau ditanya atau butuh penjelasan lebih lanjut, jangan ragu untuk tanya ya!
