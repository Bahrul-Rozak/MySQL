Halo temen-temen! Kali ini kita bakal bahas tentang *Cursors* di MySQL. Kalau lo penasaran apa itu cursor, bagaimana cara membuatnya, dan kenapa itu penting dalam pemrograman database, lo berada di tempat yang tepat! Yuk, kita mulai.

#### Apa itu Cursor?

Bayangkan lo punya sebuah buku besar yang isinya banyak banget halaman. Nah, kadang-kadang lo butuh buat membaca halaman per halaman, bukan? Nah, cursor di MySQL itu ibarat penanda yang nempel di halaman yang lagi lo baca. Cursor memungkinkan lo untuk melakukan operasi baris-per-baris pada hasil query. Jadi, daripada memproses semua hasil query sekaligus, lo bisa mengakses dan mengolah satu baris data pada satu waktu.

Cursor sangat berguna saat lo perlu melakukan operasi yang rumit pada setiap baris hasil query. Misalnya, kalau lo mau mengupdate atau menghitung data baris per baris, cursor bisa jadi alat yang sangat membantu.

#### Membuat dan Menggunakan Cursor

Sekarang kita bakal lihat bagaimana cara membuat dan menggunakan cursor di MySQL dengan kode sederhana.

##### Langkah 1: Membuat Database dan Tabel

Pertama-tama, kita butuh database dan tabel. Mari kita buat database dan tabel untuk contoh ini.

```sql
CREATE DATABASE IF NOT EXISTS contoh_db;
USE contoh_db;

CREATE TABLE IF NOT EXISTS pegawai (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nama VARCHAR(50),
    gaji DECIMAL(10, 2)
);

INSERT INTO pegawai (nama, gaji) VALUES 
('Bahrul Rozak', 3000.00),
('Ali Bastian', 2500.00),
('Diana Putri', 2700.00);
```

Di sini, kita buat database `contoh_db` dan tabel `pegawai` dengan kolom `id`, `nama`, dan `gaji`. Kita juga menambahkan beberapa data untuk contoh.

##### Langkah 2: Membuat Cursor

Langkah berikutnya adalah membuat cursor. Cursor ini akan kita gunakan untuk mengakses setiap baris dari tabel `pegawai`.

```sql
DELIMITER //

CREATE PROCEDURE tampilkan_pegawai()
BEGIN
    DECLARE selesai INT DEFAULT FALSE;
    DECLARE nama_pegawai VARCHAR(50);
    DECLARE gaji_pegawai DECIMAL(10, 2);

    DECLARE cursor_pegawai CURSOR FOR SELECT nama, gaji FROM pegawai;
    DECLARE CONTINUE HANDLER FOR NOT FOUND SET selesai = TRUE;

    OPEN cursor_pegawai;

    baca_loop: LOOP
        FETCH cursor_pegawai INTO nama_pegawai, gaji_pegawai;
        IF selesai THEN
            LEAVE baca_loop;
        END IF;
        -- Lakukan sesuatu dengan data yang diambil
        SELECT CONCAT('Nama: ', nama_pegawai, ', Gaji: ', gaji_pegawai) AS hasil;
    END LOOP;

    CLOSE cursor_pegawai;
END //

DELIMITER ;
```

#### Penjelasan Kode:

1. **Deklarasi Cursor**: `DECLARE cursor_pegawai CURSOR FOR SELECT nama, gaji FROM pegawai;` mendefinisikan cursor yang akan digunakan untuk memilih kolom `nama` dan `gaji` dari tabel `pegawai`.

2. **Deklarasi Handler**: `DECLARE CONTINUE HANDLER FOR NOT FOUND SET selesai = TRUE;` membuat handler yang akan mengatur variabel `selesai` menjadi `TRUE` ketika tidak ada lagi baris yang ditemukan.

3. **Membuka Cursor**: `OPEN cursor_pegawai;` membuka cursor dan memulai proses pengambilan data.

4. **Looping Melalui Data**: `FETCH cursor_pegawai INTO nama_pegawai, gaji_pegawai;` mengambil data dari cursor dan menyimpannya ke dalam variabel `nama_pegawai` dan `gaji_pegawai`. Jika `selesai` adalah `TRUE`, maka loop akan berhenti.

5. **Menutup Cursor**: `CLOSE cursor_pegawai;` menutup cursor setelah semua baris telah diproses.

#### Mengapa Menggunakan Cursor?

Cursor sangat berguna ketika:
- Lo perlu melakukan operasi pada setiap baris data secara individual.
- Lo bekerja dengan proses yang kompleks yang tidak bisa diselesaikan hanya dengan satu query.

Namun, perlu diingat bahwa cursor bisa lebih lambat dibandingkan dengan operasi set-based. Jadi, jika memungkinkan, coba gunakan operasi set-based sebelum memutuskan untuk menggunakan cursor.

#### Referensi

Untuk lebih mendalami tentang cursor di MySQL, temen-temen bisa cek beberapa referensi berikut:
- [MySQL Documentation on Cursors](https://dev.mysql.com/doc/refman/8.0/en/cursors.html)
- [TutorialsPoint MySQL Cursor](https://www.tutorialspoint.com/mysql/mysql-cursors.htm)

Semoga penjelasan ini bermanfaat dan membantu lo dalam memahami cursor di MySQL! Kalau ada pertanyaan atau butuh bantuan lebih lanjut, jangan ragu untuk bertanya. Happy coding, temen-temen!
