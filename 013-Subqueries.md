Hai temen-temen! Kali ini gue mau ngajak lo semua buat lebih mendalami salah satu fitur keren di MySQL, yaitu **Subqueries**. Kalau lo suka coding dan main-main sama database, subqueries ini adalah salah satu tool yang wajib lo kuasai. Gak usah bingung, kita bakal bahas dengan bahasa yang santai dan mudah dipahami. Yuk, kita mulai!

#### Apa Itu Subquery?

Sebelum kita masuk lebih dalam, kita perlu tahu dulu apa itu subquery. **Subquery** adalah sebuah query yang ditulis di dalam query lain. Ibaratnya, subquery itu kayak anak query yang membantu induknya buat mendapatkan data yang lebih spesifik. Lo bisa taruh subquery di dalam perintah `SELECT`, `WHERE`, atau bahkan `FROM`. Nah, kita bakal bahas satu per satu nih penggunaannya.

### 1. Subquery di dalam SELECT

**Subquery di dalam `SELECT`** digunakan untuk mengambil nilai yang dihasilkan oleh query lain dan menjadikannya bagian dari hasil query utama. Misalnya, lo pengen menampilkan nama karyawan beserta gaji tertinggi di departemen mereka masing-masing. Nah, lo bisa pake subquery buat ngambil gaji tertinggi itu.

#### Contoh Kasus

Misalkan kita punya dua tabel: `karyawan` dan `departemen`. 

**Tabel karyawan:**

| id_karyawan | nama_karyawan | id_departemen | gaji |
|-------------|---------------|---------------|------|
| 1           | Bahrul Rozak  | 1             | 5000 |
| 2           | Ahmad         | 1             | 7000 |
| 3           | Budi          | 2             | 4500 |
| 4           | Chandra       | 2             | 5500 |

**Tabel departemen:**

| id_departemen | nama_departemen |
|---------------|-----------------|
| 1             | IT              |
| 2             | HR              |

Nah, lo pengen tau nih siapa yang punya gaji tertinggi di tiap departemen. Query-nya bakal kayak gini:

```sql
SELECT nama_karyawan,
       gaji,
       (SELECT MAX(gaji) 
        FROM karyawan k2 
        WHERE k2.id_departemen = k1.id_departemen) AS gaji_tertinggi
FROM karyawan k1;
```

#### Penjelasan Kode

1. **SELECT nama_karyawan, gaji**: Bagian ini bakal nampilin nama karyawan dan gajinya.
2. **Subquery di dalam `SELECT`**: `(SELECT MAX(gaji) FROM karyawan k2 WHERE k2.id_departemen = k1.id_departemen) AS gaji_tertinggi` – Subquery ini ngecek ke tabel `karyawan` lagi buat nyari gaji tertinggi di tiap departemen. Kita pake alias `k2` buat tabel karyawan di subquery biar bisa dibedain sama tabel utama yang kita kasih alias `k1`.
3. **Output**: Hasil dari query ini adalah daftar karyawan beserta gaji mereka dan gaji tertinggi di departemen mereka.

### 2. Subquery di dalam WHERE

Kalau subquery di dalam `WHERE`, itu gunanya buat ngefilter data. Contohnya, lo pengen tau siapa aja karyawan yang punya gaji lebih tinggi dari rata-rata gaji di departemennya. Di sini, kita pake subquery buat ngitung rata-rata gaji dulu, baru kita filter siapa aja yang gajinya di atas itu.

#### Contoh Kasus

Lo pengen cari karyawan yang gajinya lebih tinggi dari rata-rata di departemen mereka. Query-nya gini:

```sql
SELECT nama_karyawan, gaji
FROM karyawan k1
WHERE gaji > (SELECT AVG(gaji) 
              FROM karyawan k2 
              WHERE k2.id_departemen = k1.id_departemen);
```

#### Penjelasan Kode

1. **Subquery di dalam `WHERE`**: `(SELECT AVG(gaji) FROM karyawan k2 WHERE k2.id_departemen = k1.id_departemen)` – Subquery ini ngehitung rata-rata gaji per departemen. Terus hasilnya dipake buat bandingin sama gaji tiap karyawan di query utama.
2. **Output**: Hasilnya adalah daftar karyawan yang punya gaji di atas rata-rata di departemennya.

### 3. Subquery di dalam FROM

**Subquery di dalam `FROM`** biasanya digunakan kalau lo pengen bikin tabel sementara dari hasil query lain. Ini kayak bikin temporary table yang lo bisa pake lagi buat nge-query data lebih lanjut. Misalnya, lo pengen tahu berapa jumlah karyawan di tiap departemen, terus lo gabungin dengan informasi gaji rata-rata di tiap departemen.

#### Contoh Kasus

Misalkan lo pengen tau jumlah karyawan dan rata-rata gaji di tiap departemen. Query-nya kayak gini:

```sql
SELECT d.nama_departemen,
       jumlah_karyawan,
       rata_gaji
FROM departemen d
JOIN (SELECT id_departemen,
             COUNT(*) AS jumlah_karyawan,
             AVG(gaji) AS rata_gaji
      FROM karyawan
      GROUP BY id_departemen) AS stat_karyawan
ON d.id_departemen = stat_karyawan.id_departemen;
```

#### Penjelasan Kode

1. **Subquery di dalam `FROM`**: `(SELECT id_departemen, COUNT(*) AS jumlah_karyawan, AVG(gaji) AS rata_gaji FROM karyawan GROUP BY id_departemen) AS stat_karyawan` – Subquery ini bikin tabel sementara yang isinya jumlah karyawan dan rata-rata gaji per departemen.
2. **JOIN**: Query utama gabungin tabel `departemen` sama tabel sementara dari subquery tadi buat nampilin nama departemen beserta jumlah karyawan dan rata-rata gajinya.

### Kesimpulan

Subqueries di MySQL itu powerful banget buat ngebantu lo ngambil data yang lebih kompleks. Lo bisa pake subqueries di `SELECT`, `WHERE`, dan `FROM` buat nge-solve masalah-masalah yang mungkin lebih rumit kalau pake query biasa. Anggap aja subqueries ini kayak "senjata rahasia" lo saat main-main dengan database.

Kalau lo udah ngerti konsep ini, lo bisa lebih kreatif dan efisien dalam ngolah data di MySQL. So, jangan ragu buat explore lebih lanjut dan cobain sendiri ya, temen-temen!

#### Referensi
Untuk penjelasan lebih lanjut, lo bisa cek [MySQL Subquery Documentation](https://dev.mysql.com/doc/refman/8.0/en/subqueries.html) biar makin paham.

Happy coding, temen-temen! 🚀
