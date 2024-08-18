Temen-temen! Kali ini kita bakal bahas studi kasus tentang aplikasi manajemen proyek. Tujuannya adalah memahami cara mendesain skema database dan implementasi untuk fitur-fitur seperti tugas, proyek, dan anggota tim. Yuk, kita mulai!

### **Desain Skema Database**

Dalam studi kasus ini, kita akan membuat aplikasi manajemen proyek yang sederhana. Kita akan memiliki tiga entitas utama:

1. **Proyek**
2. **Tugas**
3. **Anggota Tim**

Setiap entitas ini akan memiliki beberapa atribut yang relevan. Mari kita desain skemanya.

#### **1. Tabel Proyek**
Tabel ini akan menyimpan informasi tentang proyek-proyek yang dikelola.

- **ID_Proyek** (Primary Key)
- **Nama_Proyek**
- **Deskripsi**
- **Tanggal_Mulai**
- **Tanggal_Selesai**

#### **2. Tabel Tugas**
Tabel ini akan menyimpan informasi tentang tugas-tugas yang harus diselesaikan dalam proyek.

- **ID_Tugas** (Primary Key)
- **Nama_Tugas**
- **Deskripsi**
- **Status** (Misalnya: 'Belum Mulai', 'Dalam Proses', 'Selesai')
- **Tanggal_Ditugaskan**
- **Tanggal_Batas**
- **ID_Proyek** (Foreign Key dari Tabel Proyek)

#### **3. Tabel Anggota_Tim**
Tabel ini menyimpan informasi tentang anggota tim yang terlibat dalam proyek.

- **ID_Anggota** (Primary Key)
- **Nama_Anggota**
- **Email**
- **Telepon**

#### **4. Tabel Anggota_Proyek**
Tabel ini akan menghubungkan anggota tim dengan proyek-proyek yang mereka kerjakan.

- **ID_Anggota** (Foreign Key dari Tabel Anggota_Tim)
- **ID_Proyek** (Foreign Key dari Tabel Proyek)

### **Implementasi Database dengan SQL**

Sekarang, mari kita implementasikan skema database ini menggunakan SQL.

```sql
-- Membuat Tabel Proyek
CREATE TABLE Proyek (
    ID_Proyek INT AUTO_INCREMENT PRIMARY KEY,
    Nama_Proyek VARCHAR(255) NOT NULL,
    Deskripsi TEXT,
    Tanggal_Mulai DATE,
    Tanggal_Selesai DATE
);

-- Membuat Tabel Tugas
CREATE TABLE Tugas (
    ID_Tugas INT AUTO_INCREMENT PRIMARY KEY,
    Nama_Tugas VARCHAR(255) NOT NULL,
    Deskripsi TEXT,
    Status ENUM('Belum Mulai', 'Dalam Proses', 'Selesai') NOT NULL,
    Tanggal_Ditugaskan DATE,
    Tanggal_Batas DATE,
    ID_Proyek INT,
    FOREIGN KEY (ID_Proyek) REFERENCES Proyek(ID_Proyek)
);

-- Membuat Tabel Anggota_Tim
CREATE TABLE Anggota_Tim (
    ID_Anggota INT AUTO_INCREMENT PRIMARY KEY,
    Nama_Anggota VARCHAR(255) NOT NULL,
    Email VARCHAR(255) UNIQUE NOT NULL,
    Telepon VARCHAR(15)
);

-- Membuat Tabel Anggota_Proyek
CREATE TABLE Anggota_Proyek (
    ID_Anggota INT,
    ID_Proyek INT,
    PRIMARY KEY (ID_Anggota, ID_Proyek),
    FOREIGN KEY (ID_Anggota) REFERENCES Anggota_Tim(ID_Anggota),
    FOREIGN KEY (ID_Proyek) REFERENCES Proyek(ID_Proyek)
);
```

### **Penjelasan Kode**

1. **Tabel Proyek**: 
   - `ID_Proyek` adalah primary key yang otomatis bertambah setiap kali kita menambahkan proyek baru.
   - `Nama_Proyek`, `Deskripsi`, `Tanggal_Mulai`, dan `Tanggal_Selesai` menyimpan detail tentang proyek.

2. **Tabel Tugas**:
   - `ID_Tugas` adalah primary key yang otomatis bertambah.
   - `Nama_Tugas`, `Deskripsi`, `Status`, `Tanggal_Ditugaskan`, dan `Tanggal_Batas` menyimpan informasi terkait tugas.
   - `ID_Proyek` adalah foreign key yang menghubungkan tugas dengan proyek terkait.

3. **Tabel Anggota_Tim**:
   - `ID_Anggota` adalah primary key yang otomatis bertambah.
   - `Nama_Anggota`, `Email`, dan `Telepon` menyimpan data anggota tim.

4. **Tabel Anggota_Proyek**:
   - Tabel ini menghubungkan anggota tim dengan proyek menggunakan kombinasi `ID_Anggota` dan `ID_Proyek`.
   - `ID_Anggota` dan `ID_Proyek` adalah foreign key yang mengacu pada tabel `Anggota_Tim` dan `Proyek`.

### **Contoh Penggunaan**

Mari kita lihat bagaimana mengisi dan menggunakan tabel-tabel ini.

**Menambahkan Proyek:**
```sql
INSERT INTO Proyek (Nama_Proyek, Deskripsi, Tanggal_Mulai, Tanggal_Selesai)
VALUES ('Aplikasi Manajemen Proyek', 'Sistem untuk mengelola proyek dan tugas', '2024-01-01', '2024-12-31');
```

**Menambahkan Tugas:**
```sql
INSERT INTO Tugas (Nama_Tugas, Deskripsi, Status, Tanggal_Ditugaskan, Tanggal_Batas, ID_Proyek)
VALUES ('Desain Database', 'Mendesain skema database untuk aplikasi', 'Belum Mulai', '2024-01-02', '2024-01-10', 1);
```

**Menambahkan Anggota Tim:**
```sql
INSERT INTO Anggota_Tim (Nama_Anggota, Email, Telepon)
VALUES ('Bahrul Rozak', 'bahrul@example.com', '08123456789');
```

**Menghubungkan Anggota Tim dengan Proyek:**
```sql
INSERT INTO Anggota_Proyek (ID_Anggota, ID_Proyek)
VALUES (1, 1);
```

### **Referensi**

- [MySQL Official Documentation](https://dev.mysql.com/doc/)
- [W3Schools MySQL Tutorial](https://www.w3schools.com/sql/)

Dengan desain skema database dan contoh implementasi ini, temen-temen bisa membuat aplikasi manajemen proyek yang sederhana namun efektif. Semoga penjelasan ini membantu dan memudahkan temen-temen dalam memahami dan mengimplementasikan database MySQL. Jangan ragu untuk bertanya kalau ada yang kurang jelas!
