Temen-temen, dalam dunia database, sering banget kita berurusan dengan transaksi. Kalau kita analogikan, transaksi itu kayak serangkaian langkah yang harus dilaksanakan secara bersamaan atau semuanya dibatalkan. Bayangkan aja lo mau beli barang di toko. Lo harus bayar di kasir, dan kasir harus memasukkan data pembelian ke sistem. Kalau salah satu langkah ini gagal, seperti lo gak jadi bayar atau kasir kelupaan memasukkan data, transaksi tersebut harus dibatalkan supaya data di sistem tetap konsisten.

#### Apa Itu Transaksi?

Dalam konteks database, transaksi adalah serangkaian operasi database yang dianggap satu unit kerja. Transaksi ini harus memenuhi empat prinsip dasar yang dikenal dengan ACID, yaitu:

1. **Atomicity**: Transaksi harus dieksekusi sepenuhnya atau tidak sama sekali. Kalau ada satu bagian transaksi yang gagal, semua perubahan yang sudah dilakukan selama transaksi harus dibatalkan.
2. **Consistency**: Transaksi harus membawa database dari satu keadaan yang konsisten ke keadaan yang konsisten lainnya.
3. **Isolation**: Transaksi yang sedang berlangsung tidak boleh mempengaruhi transaksi lain yang berjalan bersamaan.
4. **Durability**: Setelah transaksi berhasil, perubahan yang dilakukan harus permanen dan tidak bisa hilang, bahkan jika terjadi crash atau kerusakan sistem.

#### START TRANSACTION, COMMIT, dan ROLLBACK

Mari kita bahas bagaimana kita bisa menggunakan tiga perintah utama dalam transaksi: `START TRANSACTION`, `COMMIT`, dan `ROLLBACK`.

1. **START TRANSACTION**

   Perintah `START TRANSACTION` digunakan untuk memulai sebuah transaksi baru. Semua perintah SQL yang dijalankan setelah `START TRANSACTION` akan menjadi bagian dari transaksi tersebut.

   ```sql
   START TRANSACTION;
   ```

2. **COMMIT**

   Perintah `COMMIT` digunakan untuk menyimpan semua perubahan yang dilakukan selama transaksi. Setelah `COMMIT`, perubahan menjadi permanen dan tidak bisa dibatalkan.

   ```sql
   COMMIT;
   ```

3. **ROLLBACK**

   Perintah `ROLLBACK` digunakan untuk membatalkan semua perubahan yang dilakukan selama transaksi. Jika ada kesalahan atau kondisi yang menyebabkan transaksi gagal, `ROLLBACK` akan mengembalikan database ke keadaan sebelum transaksi dimulai.

   ```sql
   ROLLBACK;
   ```

#### Implementasi Kode Sederhana

Sekarang, kita akan lihat implementasi transaksi dengan kode sederhana. Misalnya, kita punya tabel `akun` dan `transaksi`, dan kita mau mentransfer uang dari satu akun ke akun lain.

##### Struktur Tabel

```sql
CREATE TABLE akun (
    id INT PRIMARY KEY,
    nama VARCHAR(100),
    saldo DECIMAL(10, 2)
);

CREATE TABLE transaksi (
    id INT AUTO_INCREMENT PRIMARY KEY,
    id_akun_pengirim INT,
    id_akun_penerima INT,
    jumlah DECIMAL(10, 2),
    tanggal TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

##### Menambahkan Data Contoh

```sql
INSERT INTO akun (id, nama, saldo) VALUES (1, 'Bahrul Rozak', 1000.00);
INSERT INTO akun (id, nama, saldo) VALUES (2, 'Temen Temen', 500.00);
```

##### Proses Transaksi

Misalnya, kita mau mentransfer 200 dari akun Bahrul Rozak ke akun Temen Temen.

```sql
START TRANSACTION;

-- Kurangi saldo dari akun pengirim
UPDATE akun SET saldo = saldo - 200 WHERE id = 1;

-- Tambah saldo ke akun penerima
UPDATE akun SET saldo = saldo + 200 WHERE id = 2;

-- Catat transaksi
INSERT INTO transaksi (id_akun_pengirim, id_akun_penerima, jumlah) VALUES (1, 2, 200);

-- Jika semua perintah berhasil, simpan perubahan
COMMIT;
```

##### Mengatasi Error

Kalau ada masalah di salah satu perintah, kita bisa menggunakan `ROLLBACK` untuk membatalkan semua perubahan.

```sql
START TRANSACTION;

-- Kurangi saldo dari akun pengirim
UPDATE akun SET saldo = saldo - 200 WHERE id = 1;

-- Misalkan terjadi masalah di sini
-- Tambah saldo ke akun penerima
-- UPDATE akun SET saldo = saldo + 200 WHERE id = 2;

-- Catat transaksi
-- INSERT INTO transaksi (id_akun_pengirim, id_akun_penerima, jumlah) VALUES (1, 2, 200);

-- Jika ada error, batalkan transaksi
ROLLBACK;
```

##### Penjelasan Kode

1. **START TRANSACTION**: Memulai transaksi baru.
2. **UPDATE akun**: Mengurangi saldo dari akun pengirim.
3. **UPDATE akun**: Menambah saldo ke akun penerima.
4. **INSERT INTO transaksi**: Mencatat transaksi.
5. **COMMIT**: Menyimpan perubahan jika semua perintah berhasil.
6. **ROLLBACK**: Membatalkan perubahan jika ada kesalahan.

Transaksi sangat penting untuk menjaga konsistensi dan integritas data dalam database. Dengan memahami dan menerapkan transaksi, lo bisa memastikan bahwa data lo tetap aman dan akurat, meskipun terjadi kesalahan atau gangguan.

Untuk referensi lebih lanjut, temen-temen bisa cek [dokumentasi resmi MySQL tentang Transactions](https://dev.mysql.com/doc/refman/8.0/en/commit.html) yang memberikan penjelasan lengkap tentang penggunaan transaksi di MySQL.

Semoga penjelasan ini membantu temen-temen dalam memahami konsep transaksi dan penerapannya dalam MySQL! Kalau ada pertanyaan lebih lanjut, jangan ragu untuk bertanya.
