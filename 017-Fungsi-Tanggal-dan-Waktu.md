Halo temen-temen! Di kesempatan kali ini, gue bakal ngajak kalian buat lebih dalam memahami salah satu konsep penting di MySQL, yaitu fungsi tanggal dan waktu. Buat temen-temen yang lagi ngulik database, pastinya bakal sering banget nemuin skenario di mana kita harus ngelola data yang berhubungan sama tanggal dan waktu. Nah, di MySQL, kita punya beberapa fungsi yang powerful banget buat nge-handle hal ini, di antaranya: `NOW()`, `CURDATE()`, `DATE_FORMAT()`, dan `TIMESTAMPDIFF()`. Yuk, kita bedah satu per satu dengan bahasa yang mudah dipahami dan disertai contoh nyata biar makin paham!

### 1. Fungsi `NOW()`

Bayangin temen-temen lagi bikin aplikasi manajemen proyek, dan kita perlu nyimpen informasi kapan suatu tugas dibuat. Nah, fungsi `NOW()` ini adalah solusi jitu buat dapetin informasi waktu sekarang (tanggal dan waktu). Fungsi ini bakal ngasih output berupa *datetime* yang menggabungkan informasi tanggal dan waktu dalam format `YYYY-MM-DD HH:MM:SS`.

**Contoh Implementasi:**
```sql
INSERT INTO tugas (nama_tugas, deskripsi, tanggal_dibuat)
VALUES ('Membuat API', 'Membuat API untuk fitur baru', NOW());
```
**Penjelasan:**
Di sini, `NOW()` digunakan buat ngisi kolom `tanggal_dibuat` dengan waktu saat tugas itu dimasukkan ke dalam database. Misalnya temen-temen memasukkan data ini pada 2024-08-18 pukul 10:30:00, maka nilai yang tersimpan di kolom `tanggal_dibuat` adalah `2024-08-18 10:30:00`.

### 2. Fungsi `CURDATE()`

Kalau fungsi `NOW()` ngasih temen-temen waktu sekarang dengan format lengkap (tanggal dan waktu), fungsi `CURDATE()` cuma fokus ngasih tanggal saat ini aja dalam format `YYYY-MM-DD`. Ini pas banget kalau temen-temen cuma butuh tanggalnya aja tanpa perlu detail jam dan menitnya.

**Contoh Implementasi:**
```sql
INSERT INTO absensi (nama_karyawan, tanggal_absen)
VALUES ('Bahrul Rozak', CURDATE());
```
**Penjelasan:**
Misalkan hari ini tanggal 18 Agustus 2024, kalau temen-temen jalankan query di atas, maka `CURDATE()` bakal ngehasilin `2024-08-18` dan itu yang disimpan di kolom `tanggal_absen`.

### 3. Fungsi `DATE_FORMAT()`

Nah, sering kali kita pengen tampilin tanggal atau waktu dalam format yang lebih *customized* sesuai kebutuhan. Misalnya, temen-temen pengen tanggal dalam format `18-08-2024` atau pengen nambahin nama bulan di formatnya. Di sinilah fungsi `DATE_FORMAT()` jadi penyelamat. Fungsi ini memungkinkan kita buat ngubah format tampilan dari tanggal dan waktu sesuai keinginan kita.

**Contoh Implementasi:**
```sql
SELECT nama_karyawan, DATE_FORMAT(tanggal_absen, '%d-%m-%Y') AS tanggal_absen_terformat
FROM absensi;
```
**Penjelasan:**
Misalnya di database `tanggal_absen` disimpan dalam format `2024-08-18`. Dengan `DATE_FORMAT()`, kita bisa ubah format tampilan jadi `18-08-2024` menggunakan string format `'%d-%m-%Y'`, di mana `%d` adalah hari, `%m` adalah bulan, dan `%Y` adalah tahun.

Beberapa format yang bisa temen-temen gunakan:
- `%d`: Hari dalam dua digit (01-31)
- `%m`: Bulan dalam dua digit (01-12)
- `%Y`: Tahun dalam empat digit (2024)
- `%M`: Nama bulan (August)
- `%H`: Jam dalam dua digit (00-23)
- `%i`: Menit dalam dua digit (00-59)

### 4. Fungsi `TIMESTAMPDIFF()`

Sekarang bayangin temen-temen pengen tahu berapa lama selisih waktu antara dua kejadian. Misalnya, buat ngitung berapa lama waktu yang dihabiskan antara pembuatan tugas dan penyelesaiannya. Di sinilah fungsi `TIMESTAMPDIFF()` berperan. Fungsi ini digunakan buat ngitung selisih waktu antara dua *timestamp* dalam unit yang kita pilih, misalnya hari, jam, menit, atau bahkan tahun.

**Contoh Implementasi:**
```sql
SELECT nama_tugas, TIMESTAMPDIFF(DAY, tanggal_dibuat, tanggal_selesai) AS durasi_hari
FROM tugas;
```
**Penjelasan:**
Misalnya temen-temen punya dua kolom `tanggal_dibuat` dan `tanggal_selesai`, dan kita pengen tahu berapa hari yang dihabiskan buat nyelesain tugas tersebut. `TIMESTAMPDIFF(DAY, tanggal_dibuat, tanggal_selesai)` bakal ngasih kita selisihnya dalam satuan hari.

Kalo unit yang dipake `DAY`, maka fungsi ini bakal ngitung jumlah hari antara dua tanggal. Kalau pake `HOUR`, maka hasilnya dalam jam. Pilihan lain termasuk `MINUTE`, `SECOND`, `YEAR`, dll.

### Contoh Kasus Nyata

Bayangin Bahrul Rozak adalah seorang manajer proyek yang butuh laporan tentang tugas-tugas di proyek yang lagi dikerjakannya. Bahrul pengen tahu berapa lama tiap tugas diselesaikan dan kapan tugas tersebut dibuat.

```sql
CREATE TABLE tugas (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nama_tugas VARCHAR(255),
    deskripsi TEXT,
    tanggal_dibuat DATETIME,
    tanggal_selesai DATETIME
);

INSERT INTO tugas (nama_tugas, deskripsi, tanggal_dibuat, tanggal_selesai)
VALUES
('Membuat API', 'Membuat API untuk fitur baru', NOW(), '2024-08-19 14:00:00'),
('Desain UI', 'Desain user interface untuk aplikasi', '2024-08-17 09:00:00', '2024-08-18 18:30:00');

SELECT nama_tugas, 
       DATE_FORMAT(tanggal_dibuat, '%d-%m-%Y %H:%i:%s') AS dibuat_pada, 
       DATE_FORMAT(tanggal_selesai, '%d-%m-%Y %H:%i:%s') AS selesai_pada,
       TIMESTAMPDIFF(HOUR, tanggal_dibuat, tanggal_selesai) AS durasi_jam
FROM tugas;
```

**Penjelasan:**
1. **Tabel tugas:** Tabel ini menyimpan informasi tentang tugas termasuk nama tugas, deskripsi, tanggal dibuat, dan tanggal selesai.
2. **Data Insert:** Di sini, kita menambahkan dua tugas dengan menggunakan `NOW()` untuk mencatat waktu pembuatan tugas dan waktu selesai manual.
3. **Query:** Kita menampilkan hasilnya dengan format tanggal dan waktu yang lebih manusiawi menggunakan `DATE_FORMAT()` dan menghitung durasi pengerjaan tugas dalam jam menggunakan `TIMESTAMPDIFF()`.

Hasilnya bisa jadi kayak gini:

| nama_tugas | dibuat_pada          | selesai_pada        | durasi_jam |
|------------|----------------------|---------------------|------------|
| Membuat API | 18-08-2024 10:30:00  | 19-08-2024 14:00:00 | 27         |
| Desain UI  | 17-08-2024 09:00:00   | 18-08-2024 18:30:00 | 33.5       |

Di contoh ini, Bahrul bisa lihat bahwa tugas "Membuat API" diselesaikan dalam 27 jam dan "Desain UI" diselesaikan dalam 33,5 jam.

### Kesimpulan

Jadi, temen-temen, fungsi tanggal dan waktu di MySQL bukan cuma buat nyimpen kapan sesuatu terjadi, tapi juga buat ngolah dan menyajikan data tanggal dan waktu sesuai kebutuhan kita. Mulai dari `NOW()` yang ngasih kita waktu saat ini, `CURDATE()` buat tanggal aja, `DATE_FORMAT()` buat nge-format tanggal sesuai keinginan, sampe `TIMESTAMPDIFF()` buat ngitung selisih waktu, semuanya penting banget buat berbagai macam aplikasi.

Semoga penjelasan ini bisa bantu temen-temen lebih paham dan bisa langsung dipraktekkin di proyek-proyek temen-temen!

**Referensi:**
- [MySQL Documentation: Date and Time Functions](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html)
- [MySQL Tutorial: DATE_FORMAT() Function](https://www.mysqltutorial.org/mysql-date_format/)
