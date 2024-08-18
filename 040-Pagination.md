
**Pagination** 

adalah teknik yang digunakan untuk membagi data yang besar menjadi beberapa halaman kecil. Ini sangat penting ketika bekerja dengan dataset besar, terutama dalam aplikasi web, agar pengguna tidak dibanjiri dengan informasi sekaligus. Dengan pagination, kita bisa menampilkan data dalam potongan-potongan yang lebih mudah dicerna. Misalnya, kalau temen-temen punya 1000 data pengguna, lebih baik menampilkan 10 data per halaman daripada semua data sekaligus. 

Dalam MySQL, pagination umumnya diimplementasikan menggunakan dua klausa: `LIMIT` dan `OFFSET`. Yuk, kita bahas lebih dalam tentang bagaimana cara kerja pagination ini, serta implementasinya.

#### Apa Itu `LIMIT` dan `OFFSET`?

- **LIMIT**: Mengontrol jumlah baris yang ditampilkan pada satu halaman.
- **OFFSET**: Menentukan dari baris mana data dimulai untuk ditampilkan pada halaman tersebut.

#### Bagaimana Cara Kerja Pagination?

Bayangkan temen-temen lagi di sebuah toko buku yang memiliki banyak rak buku. Rak pertama mungkin berisi 10 buku. Ketika temen-temen selesai melihat rak pertama, temen-temen pindah ke rak kedua, dan seterusnya. Pagination bekerja dengan cara yang mirip: ia membagi data menjadi "rak-rak" kecil yang disebut halaman.

Misalnya, jika kita ingin menampilkan data dari baris ke-21 hingga ke-30, kita bisa menggunakan `LIMIT` dan `OFFSET` seperti ini:

- `LIMIT 10` berarti kita hanya ingin mengambil 10 baris.
- `OFFSET 20` berarti kita ingin mulai dari baris ke-21.

#### Implementasi Pagination dengan MySQL

Kita akan menggunakan sebuah contoh sederhana untuk menjelaskan pagination. Misalnya, kita punya tabel bernama `users` yang menyimpan data pengguna. Berikut adalah contoh implementasi pagination menggunakan MySQL.

##### Tabel `users`:

| id | name       | email              |
|----|------------|--------------------|
| 1  | John Doe   | john@example.com   |
| 2  | Jane Smith | jane@example.com   |
| ...| ...        | ...                |
| 100| Alex Brown | alex@example.com   |

Temen-temen ingin menampilkan 10 pengguna per halaman dan menampilkan halaman ke-3. Untuk melakukannya, kita bisa menggunakan query berikut:

```sql
SELECT * FROM users
LIMIT 10 OFFSET 20;
```

##### Penjelasan Kode:

- **`SELECT * FROM users`**: Mengambil semua kolom dari tabel `users`.
- **`LIMIT 10`**: Mengambil 10 baris data.
- **`OFFSET 20`**: Melewatkan 20 baris pertama (jadi mulai dari baris ke-21).

Jadi, query ini akan menampilkan data pengguna dari baris ke-21 sampai ke-30.

##### Implementasi dalam Aplikasi Web

Jika temen-temen menggunakan bahasa pemrograman seperti PHP atau Python, temen-temen bisa menggabungkan query SQL dengan logika pagination. Berikut contoh penggunaan pagination dalam PHP:

```php
<?php
// Koneksi ke database
$mysqli = new mysqli("localhost", "username", "password", "database");

// Menentukan halaman saat ini dan jumlah data per halaman
$page = isset($_GET['page']) ? (int)$_GET['page'] : 1;
$limit = 10;
$offset = ($page - 1) * $limit;

// Query SQL dengan LIMIT dan OFFSET
$query = "SELECT * FROM users LIMIT $limit OFFSET $offset";
$result = $mysqli->query($query);

// Menampilkan data
while ($row = $result->fetch_assoc()) {
    echo "ID: " . $row['id'] . " - Name: " . $row['name'] . " - Email: " . $row['email'] . "<br>";
}

// Menampilkan link navigasi
echo "<a href='?page=" . ($page - 1) . "'>Previous</a> | ";
echo "<a href='?page=" . ($page + 1) . "'>Next</a>";

// Menutup koneksi
$mysqli->close();
?>
```

##### Penjelasan Kode:

1. **Koneksi Database**: Menghubungkan ke database menggunakan MySQLi.
2. **Menentukan Halaman dan Batas**: Mengatur halaman saat ini dan menghitung offset.
3. **Query SQL**: Menjalankan query dengan `LIMIT` dan `OFFSET` untuk mendapatkan data halaman saat ini.
4. **Menampilkan Data**: Menampilkan data pengguna dalam format yang mudah dibaca.
5. **Navigasi Halaman**: Menyediakan link untuk berpindah ke halaman sebelumnya dan berikutnya.

Dengan pendekatan ini, temen-temen dapat dengan mudah menavigasi data yang besar dan membuat aplikasi lebih ramah pengguna.

### Referensi

Untuk informasi lebih lanjut dan dokumentasi MySQL, temen-temen bisa mengunjungi sumber-sumber berikut:

- [MySQL Documentation: LIMIT Clause](https://dev.mysql.com/doc/refman/8.0/en/select.html#idm140435493860416)
- [MySQL Documentation: OFFSET](https://dev.mysql.com/doc/refman/8.0/en/select.html#idm140435493860416)

Pagination adalah teknik penting dalam pengelolaan data yang besar, dan dengan menggunakan `LIMIT` dan `OFFSET`, temen-temen bisa mengimplementasikan sistem pagination yang efektif dalam aplikasi database temen-temen. Semoga penjelasan ini bermanfaat dan memudahkan temen-temen dalam memahami dan menerapkan pagination dalam proyek kalian!
