Normalisasi database adalah proses penting dalam desain database untuk memastikan bahwa data disimpan secara efisien dan tanpa redundansi. Temen-temen, mari kita bahas prinsip-prinsip normalisasi serta bentuk normal pertama (1NF), kedua (2NF), dan ketiga (3NF) secara mendetail dengan analogi dan contoh kode sederhana.

#### Prinsip Normalisasi

Normalisasi bertujuan untuk:
1. **Mengurangi Redundansi**: Menghindari penyimpanan data yang sama di beberapa tempat.
2. **Meningkatkan Integritas Data**: Menjamin data akurat dan konsisten.
3. **Memudahkan Pemeliharaan**: Mempermudah proses pembaruan dan pengelolaan data.

#### Bentuk Normal Pertama (1NF)

**1NF** mengatur agar setiap kolom dalam tabel hanya berisi nilai atomik, yaitu nilai yang tidak dapat dibagi lagi. Dalam istilah sederhana, setiap kolom harus memiliki nilai tunggal, bukan set atau daftar.

**Contoh Kasus:**

Misalkan kita memiliki tabel `Pesanan` seperti ini:

| ID_Pesanan | Nama_Pelanggan | Produk |
|------------|----------------|--------|
| 1          | Andi           | Buku, Pensil |
| 2          | Budi           | Laptop |
| 3          | Cici           | Buku, Pulpen |

Dalam tabel ini, kolom `Produk` mengandung lebih dari satu nilai, yang melanggar prinsip 1NF. Untuk mengubah tabel ini menjadi 1NF, kita perlu memecah nilai-nilai dalam kolom `Produk` menjadi baris yang terpisah.

**Implementasi Kode:**

```sql
CREATE TABLE Pesanan_1NF (
    ID_Pesanan INT,
    Nama_Pelanggan VARCHAR(50),
    Produk VARCHAR(50)
);

INSERT INTO Pesanan_1NF (ID_Pesanan, Nama_Pelanggan, Produk) VALUES
(1, 'Andi', 'Buku'),
(1, 'Andi', 'Pensil'),
(2, 'Budi', 'Laptop'),
(3, 'Cici', 'Buku'),
(3, 'Cici', 'Pulpen');
```

**Penjelasan Kode:**

- Kita membuat tabel baru `Pesanan_1NF` dengan kolom `ID_Pesanan`, `Nama_Pelanggan`, dan `Produk`.
- Data dipecah menjadi baris terpisah untuk memastikan setiap kolom berisi nilai tunggal.

#### Bentuk Normal Kedua (2NF)

**2NF** mengharuskan tabel berada dalam 1NF dan semua kolom non-kunci bergantung sepenuhnya pada kunci utama. Ini berarti tidak boleh ada ketergantungan parsial, di mana kolom non-kunci bergantung hanya pada sebagian dari kunci utama.

**Contoh Kasus:**

Misalkan kita memiliki tabel `Detail_Pesanan` seperti ini:

| ID_Pesanan | Nama_Pelanggan | ID_Produk | Nama_Produk |
|------------|----------------|-----------|-------------|
| 1          | Andi           | 101       | Buku        |
| 1          | Andi           | 102       | Pensil      |
| 2          | Budi           | 103       | Laptop      |

Di sini, kolom `Nama_Pelanggan` bergantung pada `ID_Pesanan`, sedangkan `Nama_Produk` bergantung pada `ID_Produk`. Kita harus memecah tabel ini menjadi dua tabel: satu untuk `Pesanan` dan satu untuk `Produk`.

**Implementasi Kode:**

```sql
CREATE TABLE Pesanan (
    ID_Pesanan INT PRIMARY KEY,
    Nama_Pelanggan VARCHAR(50)
);

CREATE TABLE Produk (
    ID_Produk INT PRIMARY KEY,
    Nama_Produk VARCHAR(50)
);

CREATE TABLE Detail_Pesanan (
    ID_Pesanan INT,
    ID_Produk INT,
    FOREIGN KEY (ID_Pesanan) REFERENCES Pesanan(ID_Pesanan),
    FOREIGN KEY (ID_Produk) REFERENCES Produk(ID_Produk)
);

-- Insert data
INSERT INTO Pesanan (ID_Pesanan, Nama_Pelanggan) VALUES
(1, 'Andi'),
(2, 'Budi');

INSERT INTO Produk (ID_Produk, Nama_Produk) VALUES
(101, 'Buku'),
(102, 'Pensil'),
(103, 'Laptop');

INSERT INTO Detail_Pesanan (ID_Pesanan, ID_Produk) VALUES
(1, 101),
(1, 102),
(2, 103);
```

**Penjelasan Kode:**

- Kita membuat tiga tabel: `Pesanan`, `Produk`, dan `Detail_Pesanan`.
- Tabel `Pesanan` menyimpan informasi pelanggan, sementara `Produk` menyimpan informasi produk.
- Tabel `Detail_Pesanan` menghubungkan `Pesanan` dan `Produk` dengan kunci asing.

#### Bentuk Normal Ketiga (3NF)

**3NF** mengharuskan tabel berada dalam 2NF dan semua kolom non-kunci tidak bergantung pada kolom non-kunci lainnya. Ini memastikan bahwa tidak ada ketergantungan transitif.

**Contoh Kasus:**

Misalkan kita memiliki tabel `Karyawan` seperti ini:

| ID_Karyawan | Nama_Karyawan | ID_Departemen | Nama_Departemen |
|-------------|---------------|---------------|-----------------|
| 1           | Ali           | 10            | HR              |
| 2           | Siti          | 20            | IT              |
| 3           | Budi          | 10            | HR              |

Di sini, `Nama_Departemen` bergantung pada `ID_Departemen`, bukan pada `ID_Karyawan`. Kita perlu memecah tabel ini menjadi dua tabel: satu untuk `Karyawan` dan satu untuk `Departemen`.

**Implementasi Kode:**

```sql
CREATE TABLE Departemen (
    ID_Departemen INT PRIMARY KEY,
    Nama_Departemen VARCHAR(50)
);

CREATE TABLE Karyawan (
    ID_Karyawan INT PRIMARY KEY,
    Nama_Karyawan VARCHAR(50),
    ID_Departemen INT,
    FOREIGN KEY (ID_Departemen) REFERENCES Departemen(ID_Departemen)
);

-- Insert data
INSERT INTO Departemen (ID_Departemen, Nama_Departemen) VALUES
(10, 'HR'),
(20, 'IT');

INSERT INTO Karyawan (ID_Karyawan, Nama_Karyawan, ID_Departemen) VALUES
(1, 'Ali', 10),
(2, 'Siti', 20),
(3, 'Budi', 10);
```

**Penjelasan Kode:**

- Kita membuat dua tabel: `Departemen` dan `Karyawan`.
- Tabel `Departemen` menyimpan informasi departemen, sementara `Karyawan` menghubungkan dengan departemen menggunakan kunci asing.

#### Referensi

- [MySQL Official Documentation](https://dev.mysql.com/doc/)
- [Database Normalization: An Overview](https://www.databasestar.com/database-normalization/)

Dengan memahami dan menerapkan prinsip-prinsip normalisasi ini, temen-temen dapat merancang database yang lebih efisien, menghindari redundansi, dan menjaga integritas data. Selamat mencoba!
