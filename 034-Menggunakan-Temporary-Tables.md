#### Apa itu Temporary Table?

Temen-temen, pernah nggak sih ngerasa perlu menyimpan data sementara yang hanya digunakan selama sesi tertentu? Misalnya, saat kita lagi ngolah data dari beberapa tabel dan butuh tempat sementara untuk nyimpen hasil intermediate-nya. Nah, di sinilah **temporary tables** berfungsi. Temporary tables itu tabel yang hanya ada selama sesi database aktif dan akan otomatis dihapus begitu sesi berakhir atau kita menutup koneksi ke database. 

Temporary tables sangat berguna ketika kita perlu memproses data secara sementara tanpa mempengaruhi tabel-tabel permanen di database. Mereka membantu mengurangi kompleksitas query dan meningkatkan performa.

#### Cara Membuat Temporary Table

Membuat temporary table sangat mudah, temen-temen. Kita cuma perlu menambahkan kata kunci `TEMPORARY` di depan perintah `CREATE TABLE`. Berikut ini adalah langkah-langkahnya:

1. **Membuat Temporary Table**

   Misalkan kita lagi kerja dengan database yang berisi data penjualan, dan kita ingin membuat temporary table untuk menyimpan data penjualan bulanan sementara. Ini contoh kode SQL-nya:

   ```sql
   CREATE TEMPORARY TABLE TempSales AS
   SELECT product_id, SUM(sales_amount) AS total_sales
   FROM sales
   WHERE sales_date BETWEEN '2024-01-01' AND '2024-01-31'
   GROUP BY product_id;
   ```

   **Penjelasan Kode:**
   - `CREATE TEMPORARY TABLE TempSales AS`: Perintah ini membuat temporary table dengan nama `TempSales`.
   - `SELECT product_id, SUM(sales_amount) AS total_sales`: Kita memilih kolom `product_id` dan total penjualan (`total_sales`) untuk setiap produk.
   - `FROM sales`: Data diambil dari tabel `sales`.
   - `WHERE sales_date BETWEEN '2024-01-01' AND '2024-01-31'`: Hanya data penjualan di bulan Januari 2024 yang dipilih.
   - `GROUP BY product_id`: Data dikelompokkan berdasarkan `product_id`.

2. **Menggunakan Temporary Table**

   Setelah temporary table dibuat, kita bisa langsung menggunakannya dalam query lainnya. Misalnya, kita mau ambil data dari temporary table tersebut dan tampilkan:

   ```sql
   SELECT * FROM TempSales;
   ```

   **Penjelasan Kode:**
   - `SELECT * FROM TempSales`: Mengambil semua data dari temporary table `TempSales`.

3. **Menghapus Temporary Table**

   Walaupun temporary table otomatis dihapus saat sesi berakhir, kita bisa menghapusnya secara manual dengan perintah berikut:

   ```sql
   DROP TEMPORARY TABLE IF EXISTS TempSales;
   ```

   **Penjelasan Kode:**
   - `DROP TEMPORARY TABLE IF EXISTS TempSales`: Menghapus temporary table `TempSales` jika ada.

#### Keuntungan Menggunakan Temporary Table

1. **Performa yang Lebih Baik:**
   Temporary tables membantu dalam mengurangi kompleksitas query yang sangat besar. Dengan menggunakan temporary tables, kita bisa membagi query kompleks menjadi beberapa langkah yang lebih sederhana dan efisien.

2. **Pengolahan Data yang Fleksibel:**
   Kita bisa melakukan berbagai operasi pada temporary table tanpa mempengaruhi data di tabel asli. Misalnya, jika kita perlu melakukan kalkulasi tambahan atau filter pada data yang telah digabungkan, temporary table adalah tempat yang tepat.

3. **Penggunaan Sumber Daya yang Efisien:**
   Temporary tables hanya ada selama sesi aktif, sehingga tidak memakan ruang penyimpanan yang tidak perlu setelah sesi berakhir. 

#### Studi Kasus Sederhana

Mari kita lihat studi kasus sederhana dengan menggunakan temporary tables. Misalkan kita punya sebuah database dengan tabel `sales` dan `products`. Kita ingin mengetahui produk mana yang terjual paling banyak selama bulan lalu dan hanya tertarik pada produk yang terjual lebih dari 100 unit.

1. **Langkah 1: Membuat Temporary Table**

   ```sql
   CREATE TEMPORARY TABLE MonthlySales AS
   SELECT p.product_name, SUM(s.sales_amount) AS total_sales
   FROM sales s
   JOIN products p ON s.product_id = p.product_id
   WHERE s.sales_date BETWEEN DATE_SUB(NOW(), INTERVAL 1 MONTH) AND NOW()
   GROUP BY p.product_name;
   ```

2. **Langkah 2: Mengambil Data dari Temporary Table**

   ```sql
   SELECT * FROM MonthlySales
   WHERE total_sales > 100;
   ```

3. **Langkah 3: Menghapus Temporary Table**

   ```sql
   DROP TEMPORARY TABLE IF EXISTS MonthlySales;
   ```

#### Referensi

Untuk informasi lebih lanjut tentang temporary tables dan praktik terbaik dalam penggunaannya, temen-temen bisa kunjungi beberapa referensi berikut:
- [MySQL Official Documentation on Temporary Tables](https://dev.mysql.com/doc/refman/8.0/en/create-temporary-table.html)
- [W3Schools MySQL Temporary Tables](https://www.w3schools.com/sql/sql_temp_tables.asp)

Dengan temporary tables, temen-temen bisa mengelola data sementara dengan lebih efisien dan mengoptimalkan performa query yang kompleks. Semoga penjelasan ini membantu temen-temen dalam memahami dan memanfaatkan temporary tables di MySQL! 🚀
