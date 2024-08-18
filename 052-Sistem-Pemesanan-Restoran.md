Halo teman-teman! Kali ini kita akan membahas bagaimana membuat sistem pemesanan restoran menggunakan MySQL. Untuk mempermudah pemahaman, kita akan menjelaskan desain skema database dan implementasi fitur pemesanan serta menu. Siap-siap ya, karena kita bakal masuk ke detail yang cukup seru!

#### **1. Desain Skema Database**

Pertama-tama, kita perlu merancang skema database untuk sistem pemesanan restoran. Skema ini akan membantu kita menyimpan informasi penting seperti menu, pelanggan, dan pesanan.

**a. Tabel Menu**

Tabel ini menyimpan data tentang makanan dan minuman yang tersedia di restoran.

```sql
CREATE TABLE Menu (
    MenuID INT AUTO_INCREMENT PRIMARY KEY,
    NamaMenu VARCHAR(100) NOT NULL,
    Deskripsi TEXT,
    Harga DECIMAL(10, 2) NOT NULL,
    Kategori VARCHAR(50)
);
```

- `MenuID`: Identifikasi unik untuk setiap item menu.
- `NamaMenu`: Nama dari makanan atau minuman.
- `Deskripsi`: Deskripsi singkat tentang menu.
- `Harga`: Harga dari menu.
- `Kategori`: Kategori menu, misalnya 'Makanan' atau 'Minuman'.

**b. Tabel Pelanggan**

Tabel ini menyimpan data pelanggan yang melakukan pemesanan.

```sql
CREATE TABLE Pelanggan (
    PelangganID INT AUTO_INCREMENT PRIMARY KEY,
    NamaPelanggan VARCHAR(100) NOT NULL,
    Telepon VARCHAR(15),
    Alamat TEXT
);
```

- `PelangganID`: Identifikasi unik untuk setiap pelanggan.
- `NamaPelanggan`: Nama pelanggan.
- `Telepon`: Nomor telepon pelanggan.
- `Alamat`: Alamat lengkap pelanggan.

**c. Tabel Pesanan**

Tabel ini menyimpan informasi tentang pesanan yang dibuat oleh pelanggan.

```sql
CREATE TABLE Pesanan (
    PesananID INT AUTO_INCREMENT PRIMARY KEY,
    PelangganID INT,
    TanggalPesanan DATETIME DEFAULT CURRENT_TIMESTAMP,
    Total DECIMAL(10, 2),
    FOREIGN KEY (PelangganID) REFERENCES Pelanggan(PelangganID)
);
```

- `PesananID`: Identifikasi unik untuk setiap pesanan.
- `PelangganID`: Referensi ke pelanggan yang membuat pesanan.
- `TanggalPesanan`: Tanggal dan waktu pesanan dibuat.
- `Total`: Total harga dari pesanan.

**d. Tabel DetailPesanan**

Tabel ini menyimpan rincian item yang termasuk dalam pesanan.

```sql
CREATE TABLE DetailPesanan (
    DetailID INT AUTO_INCREMENT PRIMARY KEY,
    PesananID INT,
    MenuID INT,
    Jumlah INT,
    Subtotal DECIMAL(10, 2),
    FOREIGN KEY (PesananID) REFERENCES Pesanan(PesananID),
    FOREIGN KEY (MenuID) REFERENCES Menu(MenuID)
);
```

- `DetailID`: Identifikasi unik untuk detail pesanan.
- `PesananID`: Referensi ke pesanan yang terkait.
- `MenuID`: Referensi ke item menu yang dipesan.
- `Jumlah`: Jumlah item menu yang dipesan.
- `Subtotal`: Harga subtotal untuk item tersebut.

#### **2. Implementasi Fitur Pemesanan dan Menu**

Sekarang kita akan menulis beberapa query SQL untuk mengelola pemesanan dan menu di restoran.

**a. Menambahkan Menu**

Untuk menambahkan item baru ke menu, kita gunakan query `INSERT INTO`.

```sql
INSERT INTO Menu (NamaMenu, Deskripsi, Harga, Kategori)
VALUES ('Pizza Margherita', 'Pizza dengan tomat dan mozzarella', 90.00, 'Makanan');
```

**b. Menambahkan Pelanggan**

Kita dapat menambahkan pelanggan baru dengan query berikut:

```sql
INSERT INTO Pelanggan (NamaPelanggan, Telepon, Alamat)
VALUES ('Bahrul Rozak', '08123456789', 'Jl. Raya No. 10, Jakarta');
```

**c. Membuat Pesanan**

Misalkan Bahrul membuat pesanan, kita perlu memasukkan data pesanan.

```sql
INSERT INTO Pesanan (PelangganID, Total)
VALUES (1, 90.00); -- Total dihitung setelah menambahkan detail pesanan
```

**d. Menambahkan Detail Pesanan**

Sekarang, kita tambahkan item ke pesanan yang sudah dibuat.

```sql
INSERT INTO DetailPesanan (PesananID, MenuID, Jumlah, Subtotal)
VALUES (1, 1, 1, 90.00);
```

**e. Mengupdate Menu**

Jika harga menu berubah, kita bisa memperbaruinya dengan query berikut:

```sql
UPDATE Menu
SET Harga = 100.00
WHERE MenuID = 1;
```

**f. Menghapus Pesanan**

Jika ada pesanan yang perlu dihapus, kita gunakan query `DELETE`.

```sql
DELETE FROM Pesanan
WHERE PesananID = 1;
```

**Penjelasan Kode:**

- **`CREATE TABLE`**: Digunakan untuk membuat tabel baru.
- **`INSERT INTO`**: Menambahkan data ke dalam tabel.
- **`UPDATE`**: Memperbarui data yang sudah ada.
- **`DELETE`**: Menghapus data dari tabel.
- **`FOREIGN KEY`**: Membuat hubungan antara tabel.

Dengan skema database ini dan query-query yang sudah kita bahas, kalian bisa mulai membangun sistem pemesanan restoran. Pastikan kalian menguji setiap fitur dengan baik agar semua berjalan lancar.

Untuk referensi lebih lanjut, kalian bisa mengunjungi [MySQL Documentation](https://dev.mysql.com/doc/) atau [W3Schools SQL Tutorial](https://www.w3schools.com/sql/). 

Semoga penjelasan ini bermanfaat dan membantu kalian dalam membangun sistem pemesanan restoran. Sampai jumpa di studi kasus berikutnya!
