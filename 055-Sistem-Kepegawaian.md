Dalam studi kasus ini, kita akan membahas bagaimana merancang dan mengimplementasikan sebuah sistem kepegawaian menggunakan MySQL. Sistem ini akan mencakup pengelolaan data karyawan dan gaji mereka. Mari kita lihat lebih dekat bagaimana kita bisa membangun sistem ini dari awal hingga akhir.

#### 1. Desain Skema Database

**a. Konsep Dasar**

Skema database adalah peta yang menggambarkan bagaimana data disimpan dan dihubungkan dalam database. Untuk sistem kepegawaian, kita memerlukan beberapa tabel utama untuk menyimpan informasi karyawan dan gaji mereka. Berikut adalah tabel yang kita butuhkan:

1. **Tabel `employees`**: Menyimpan data dasar tentang karyawan.
2. **Tabel `salaries`**: Menyimpan informasi tentang gaji karyawan.

**b. Struktur Tabel**

1. **Tabel `employees`**
   - `employee_id` (INT, PRIMARY KEY, AUTO_INCREMENT): ID unik untuk setiap karyawan.
   - `first_name` (VARCHAR(50)): Nama depan karyawan.
   - `last_name` (VARCHAR(50)): Nama belakang karyawan.
   - `date_of_birth` (DATE): Tanggal lahir karyawan.
   - `position` (VARCHAR(50)): Jabatan atau posisi karyawan.
   - `hire_date` (DATE): Tanggal karyawan dipekerjakan.

2. **Tabel `salaries`**
   - `salary_id` (INT, PRIMARY KEY, AUTO_INCREMENT): ID unik untuk setiap record gaji.
   - `employee_id` (INT, FOREIGN KEY): ID karyawan yang menerima gaji.
   - `amount` (DECIMAL(10, 2)): Jumlah gaji.
   - `salary_date` (DATE): Tanggal pembayaran gaji.

**c. Diagram Skema**

Berikut adalah representasi sederhana dari skema database:

```
+----------------+         +----------------+
|  employees     |         |   salaries     |
+----------------+         +----------------+
| employee_id    |<--------| employee_id    |
| first_name     |         | salary_id      |
| last_name      |         | amount         |
| date_of_birth  |         | salary_date    |
| position       |         +----------------+
| hire_date      |
+----------------+
```

#### 2. Implementasi Pengelolaan Karyawan dan Gaji

Mari kita lihat bagaimana cara membuat dan mengelola tabel-tabel ini dengan SQL. Di sini, kita akan membuat tabel, menambahkan data, dan menjalankan beberapa query dasar.

**a. Membuat Tabel**

```sql
-- Membuat tabel employees
CREATE TABLE employees (
    employee_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    date_of_birth DATE,
    position VARCHAR(50),
    hire_date DATE
);

-- Membuat tabel salaries
CREATE TABLE salaries (
    salary_id INT AUTO_INCREMENT PRIMARY KEY,
    employee_id INT,
    amount DECIMAL(10, 2),
    salary_date DATE,
    FOREIGN KEY (employee_id) REFERENCES employees(employee_id)
);
```

**Penjelasan:**
- Tabel `employees` menyimpan informasi dasar tentang setiap karyawan, seperti nama, tanggal lahir, posisi, dan tanggal perekrutan.
- Tabel `salaries` menyimpan informasi tentang gaji yang dibayarkan kepada karyawan, termasuk jumlah gaji dan tanggal pembayarannya. Relasi antara `salaries` dan `employees` dihubungkan dengan `employee_id`.

**b. Menambahkan Data**

```sql
-- Menambahkan data ke tabel employees
INSERT INTO employees (first_name, last_name, date_of_birth, position, hire_date)
VALUES ('Bahrul', 'Rozak', '1990-08-25', 'Software Engineer', '2023-01-15');

-- Menambahkan data ke tabel salaries
INSERT INTO salaries (employee_id, amount, salary_date)
VALUES (1, 5000.00, '2024-08-15');
```

**Penjelasan:**
- Perintah `INSERT INTO` digunakan untuk menambahkan data ke tabel. Di sini, kita menambahkan satu karyawan bernama Bahrul Rozak dan memberikan gaji pada tanggal tertentu.

**c. Mengambil Data**

```sql
-- Mengambil data karyawan
SELECT * FROM employees;

-- Mengambil data gaji dengan informasi karyawan
SELECT e.first_name, e.last_name, s.amount, s.salary_date
FROM salaries s
JOIN employees e ON s.employee_id = e.employee_id;
```

**Penjelasan:**
- Query pertama menampilkan semua data dari tabel `employees`.
- Query kedua menggabungkan tabel `salaries` dengan `employees` untuk menampilkan informasi gaji bersama dengan nama karyawan.

**d. Mengupdate dan Menghapus Data**

```sql
-- Mengupdate data gaji
UPDATE salaries
SET amount = 5500.00
WHERE salary_id = 1;

-- Menghapus data karyawan
DELETE FROM employees
WHERE employee_id = 1;
```

**Penjelasan:**
- `UPDATE` digunakan untuk memperbarui informasi gaji, sedangkan `DELETE` digunakan untuk menghapus data karyawan.

### Referensi

Untuk referensi lebih lanjut dan dokumentasi tentang MySQL, kalian bisa mengunjungi:
- [MySQL Official Documentation](https://dev.mysql.com/doc/)
- [W3Schools SQL Tutorial](https://www.w3schools.com/sql/)

Dengan panduan ini, temen-temen sekarang sudah punya pemahaman dasar tentang bagaimana merancang dan mengelola sistem kepegawaian menggunakan MySQL. Kalian bisa mulai mengembangkan sistem ini lebih lanjut sesuai dengan kebutuhan spesifik dari aplikasi atau proyek kalian. Selamat mencoba! 🚀
