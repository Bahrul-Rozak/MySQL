Hai temen-temen! Kali ini kita bakal ngebahas tentang sesuatu yang super penting dalam dunia SQL, yaitu **Penggunaan Alias**. Mungkin buat temen-temen yang baru belajar, istilah ini kedengeran asing. Tapi tenang, gue bakal jelasin dengan cara yang gampang dipahami, pake analogi yang simpel, dan tentunya dilengkapi dengan contoh yang relevan.

#### Apa Itu Alias?

Oke, bayangin temen-temen lagi di kelas dan ada nama yang sama, misalnya ada dua orang yang namanya Bahrul Rozak. Nah, biar nggak bingung, guru kalian mungkin bakal kasih julukan alias panggilan buat salah satu dari mereka, kayak “Rozak A” dan “Rozak B”. Nah, fungsi alias di MySQL juga mirip banget. Alias ini adalah nama sementara yang temen-temen kasih buat kolom atau tabel di query SQL biar lebih gampang dipahami atau lebih singkat.

#### Kenapa Perlu Pakai Alias?

Alias bikin hidup kita sebagai developer jadi lebih gampang. Ada beberapa alasan kenapa kita butuh alias:

1. **Membuat Nama Kolom Lebih Deskriptif**: Kadang, nama kolom di database bisa agak membingungkan atau terlalu panjang. Dengan alias, kita bisa kasih nama yang lebih mudah dimengerti.
  
2. **Memperpendek Nama Kolom atau Tabel**: Kalau ada nama tabel atau kolom yang panjang, kita bisa kasih alias yang lebih pendek. Ini bakal sangat berguna kalo temen-temen sering nulis query yang panjang.
  
3. **Memudahkan Penggunaan Join**: Saat kita join beberapa tabel, alias sangat berguna buat membedakan antara kolom dari tabel yang satu dengan tabel yang lain, terutama kalau nama kolomnya sama.

#### Cara Menggunakan Alias di MySQL

Alias di MySQL bisa digunakan untuk kolom dan tabel. Caranya sangat sederhana, temen-temen cukup menggunakan kata kunci `AS` diikuti dengan nama alias yang diinginkan.

##### 1. Alias untuk Kolom

Misalnya, temen-temen punya tabel `students` yang menyimpan data mahasiswa dengan nama kolom `full_name` dan `age`. Kalau temen-temen pengen nama kolom `full_name` ditampilkan sebagai `Nama Mahasiswa`, kita bisa pakai alias seperti ini:

```sql
SELECT full_name AS 'Nama Mahasiswa', age AS 'Umur'
FROM students;
```

**Penjelasan Kode**:
- `full_name AS 'Nama Mahasiswa'`: Disini, kita kasih alias `Nama Mahasiswa` buat kolom `full_name`, jadi saat query ini dijalankan, outputnya bakal nampilin kolom dengan nama `Nama Mahasiswa` dan bukan `full_name`.
- `age AS 'Umur'`: Sama kayak sebelumnya, `age` dikasih alias `Umur`.

##### 2. Alias untuk Tabel

Bayangin temen-temen punya dua tabel, `students` dan `courses`. Temen-temen pengen tahu siapa aja mahasiswa yang mengambil mata kuliah tertentu. Nah, kita perlu melakukan `JOIN` antara dua tabel ini. Biasanya, nama tabel bisa panjang atau sulit diingat. Dengan alias, kita bisa bikin querynya jadi lebih rapi:

```sql
SELECT s.full_name, c.course_name
FROM students AS s
JOIN courses AS c ON s.course_id = c.id;
```

**Penjelasan Kode**:
- `students AS s`: Tabel `students` dikasih alias `s`. Jadi, setiap kali kita referensi tabel `students` di query ini, kita cukup pakai `s` aja.
- `courses AS c`: Tabel `courses` dikasih alias `c`. Ini bikin query lebih ringkas dan gampang dibaca.

#### Contoh Kasus: Bahrul Rozak dan Tabel Karyawan

Oke, bayangin temen-temen lagi bikin aplikasi HR (Human Resources) dan ada tabel `employees` yang nyimpen data karyawan dengan nama `Bahrul Rozak` sebagai salah satu karyawannya. Misalnya kita punya tabel seperti ini:

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    full_name VARCHAR(100),
    position VARCHAR(50),
    salary DECIMAL(10, 2)
);

INSERT INTO employees (id, full_name, position, salary)
VALUES (1, 'Bahrul Rozak', 'Software Engineer', 8000000),
       (2, 'Diana Putri', 'Data Analyst', 7500000);
```

Sekarang temen-temen pengen ambil data gaji karyawan tapi dengan kolom yang lebih deskriptif. Temen-temen bisa pakai query berikut:

```sql
SELECT full_name AS 'Nama Karyawan', salary AS 'Gaji'
FROM employees;
```

**Penjelasan Kode**:
- Query ini akan ngambil data dari tabel `employees`.
- Nama kolom `full_name` diganti dengan `Nama Karyawan`, dan `salary` diganti jadi `Gaji` di hasil output.

Hasilnya bakal kelihatan lebih rapi dan informatif:

```md
---------------------------
| Nama Karyawan | Gaji    |
---------------------------
| Bahrul Rozak  | 8000000 |
| Diana Putri   | 7500000 |
---------------------------
```

#### Kesimpulan

Menggunakan alias di MySQL adalah praktik yang sangat berguna dan sering dipakai dalam penulisan query SQL. Alias membantu temen-temen buat bikin query yang lebih mudah dimengerti, lebih rapi, dan efisien, terutama saat bekerja dengan query yang kompleks atau data yang berasal dari beberapa tabel.

Nah, semoga penjelasan ini membantu temen-temen buat memahami konsep alias di MySQL. Kalo masih ada yang pengen ditanyain, jangan ragu buat nanya, ya! Tetap semangat belajar SQL-nya!

#### Referensi
- [MySQL Documentation](https://dev.mysql.com/doc/refman/8.0/en/select.html)
- [W3Schools SQL Alias](https://www.w3schools.com/sql/sql_alias.asp)
