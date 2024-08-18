Hai temen-temen! Dalam studi kasus kali ini, kita akan membahas bagaimana membuat sistem inventaris sederhana menggunakan MySQL. Bayangkan kita punya toko yang menjual berbagai produk. Tugas kita adalah membuat sistem untuk mengelola stok barang dan transaksi penjualan. Yuk, kita mulai dari desain skema database hingga implementasi manajemen stok dan transaksi!

#### Desain Skema Database

Pertama-tama, kita perlu mendesain skema database kita. Skema ini adalah blueprint untuk database kita, yang mencakup tabel-tabel yang diperlukan serta hubungan antar tabel tersebut.

1. **Tabel Produk**: Menyimpan informasi tentang produk yang ada di toko.
2. **Tabel Stok**: Menyimpan informasi tentang jumlah stok yang tersedia untuk setiap produk.
3. **Tabel Transaksi**: Menyimpan informasi tentang transaksi penjualan yang terjadi.

##### Struktur Tabel

1. **Tabel Produk**
   ```sql
   CREATE TABLE Produk (
       id_produk INT AUTO_INCREMENT PRIMARY KEY,
       nama_produk VARCHAR(100) NOT NULL,
       harga DECIMAL(10, 2) NOT NULL
   );
   ```

   - `id_produk`: ID unik untuk setiap produk.
   - `nama_produk`: Nama produk.
   - `harga`: Harga produk.

2. **Tabel Stok**
   ```sql
   CREATE TABLE Stok (
       id_stok INT AUTO_INCREMENT PRIMARY KEY,
       id_produk INT,
       jumlah INT NOT NULL,
       FOREIGN KEY (id_produk) REFERENCES Produk(id_produk)
   );
   ```

   - `id_stok`: ID unik untuk setiap entri stok.
   - `id_produk`: ID produk yang terkait dengan stok.
   - `jumlah`: Jumlah stok yang tersedia.

3. **Tabel Transaksi**
   ```sql
   CREATE TABLE Transaksi (
       id_transaksi INT AUTO_INCREMENT PRIMARY KEY,
       id_produk INT,
       jumlah INT NOT NULL,
       total_harga DECIMAL(10, 2) NOT NULL,
       tanggal TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
       FOREIGN KEY (id_produk) REFERENCES Produk(id_produk)
   );
   ```

   - `id_transaksi`: ID unik untuk setiap transaksi.
   - `id_produk`: ID produk yang dijual.
   - `jumlah`: Jumlah produk yang terjual.
   - `total_harga`: Total harga transaksi.
   - `tanggal`: Tanggal transaksi.

#### Implementasi Manajemen Stok dan Transaksi

Setelah desain skema, saatnya implementasi. Berikut adalah langkah-langkah untuk mengelola stok dan transaksi.

1. **Menambahkan Produk Baru**
   ```sql
   INSERT INTO Produk (nama_produk, harga) VALUES ('Laptop', 15000000.00);
   ```

   - Menambahkan produk dengan nama "Laptop" dan harga 15.000.000.

2. **Menambahkan Stok untuk Produk**
   ```sql
   INSERT INTO Stok (id_produk, jumlah) VALUES (1, 50);
   ```

   - Menambahkan 50 unit stok untuk produk dengan `id_produk` 1 (misalnya Laptop).

3. **Mencatat Transaksi Penjualan**
   ```sql
   INSERT INTO Transaksi (id_produk, jumlah, total_harga) VALUES (1, 2, 30000000.00);
   ```

   - Mencatat penjualan 2 unit Laptop dengan total harga 30.000.000.

4. **Mengurangi Stok Setelah Transaksi**
   Untuk mengurangi stok setelah transaksi, kita bisa menggunakan query berikut:
   ```sql
   UPDATE Stok
   SET jumlah = jumlah - 2
   WHERE id_produk = 1;
   ```

   - Mengurangi 2 unit dari stok produk dengan `id_produk` 1.

#### Penjelasan Kode

- **Tabel Produk** menyimpan informasi tentang produk seperti nama dan harga. Setiap produk diidentifikasi dengan `id_produk`, yang merupakan primary key.
  
- **Tabel Stok** menyimpan jumlah stok untuk setiap produk. `id_produk` adalah foreign key yang menghubungkan tabel Stok dengan tabel Produk.
  
- **Tabel Transaksi** mencatat setiap penjualan produk. `id_produk` adalah foreign key yang menghubungkan tabel Transaksi dengan tabel Produk. 

Dengan tabel-tabel ini, kita bisa dengan mudah mengelola stok dan transaksi penjualan. Misalnya, jika kita menjual beberapa unit produk, kita akan mencatat transaksi di tabel Transaksi dan mengupdate stok di tabel Stok.

#### Studi Kasus Sederhana

Misalnya, kita baru saja menerima stok tambahan untuk Laptop, dan ada penjualan baru. Untuk mencatat stok tambahan, kita bisa melakukan hal berikut:

1. **Menambahkan Stok Baru**
   ```sql
   INSERT INTO Stok (id_produk, jumlah) VALUES (1, 20);
   ```

   - Menambahkan 20 unit stok untuk Laptop.

2. **Mencatat Penjualan**
   ```sql
   INSERT INTO Transaksi (id_produk, jumlah, total_harga) VALUES (1, 5, 75000000.00);
   ```

   - Mencatat penjualan 5 unit Laptop dengan total harga 75.000.000.

3. **Mengupdate Stok Setelah Penjualan**
   ```sql
   UPDATE Stok
   SET jumlah = jumlah - 5
   WHERE id_produk = 1;
   ```

   - Mengurangi 5 unit dari stok Laptop.

Dengan pendekatan ini, temen-temen bisa memanage stok dan transaksi secara efisien. Sistem inventaris ini akan membantu temen-temen dalam mengelola produk, memantau stok, dan mencatat penjualan dengan mudah.

Untuk referensi lebih lanjut, temen-temen bisa cek dokumentasi MySQL resmi di [MySQL Documentation](https://dev.mysql.com/doc/) dan [W3Schools MySQL Tutorial](https://www.w3schools.com/sql/).

Semoga penjelasan ini bermanfaat dan temen-temen bisa lebih memahami cara membuat dan mengelola sistem inventaris dengan MySQL. Selamat mencoba! 🚀
