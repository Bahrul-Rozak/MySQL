Hai temen-temen! Kali ini kita bakal membahas tentang *Views* dan *Materialized Views* di MySQL. Kedua konsep ini sering digunakan dalam desain database untuk membantu kita dalam mengelola dan mengakses data dengan lebih efektif. Yuk, kita lihat lebih dalam!

#### 1. Apa Itu Views?

**Views** adalah *virtual table* dalam database yang dibentuk dari hasil query. Bayangkan views sebagai jendela yang menunjukkan pandangan spesifik dari data dalam tabel kita tanpa mengubah data aslinya. Dengan views, kita bisa menampilkan data dari beberapa tabel dalam satu tampilan yang sederhana.

##### Membuat Views

Untuk membuat view di MySQL, kita gunakan perintah `CREATE VIEW`. Misalnya, kita punya dua tabel: `employees` dan `departments`. Kita ingin membuat view yang menunjukkan nama karyawan bersama dengan nama departemennya.

**Contoh Tabel:**

```sql
CREATE TABLE employees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    department_id INT
);

CREATE TABLE departments (
    id INT AUTO_INCREMENT PRIMARY KEY,
    department_name VARCHAR(100)
);

INSERT INTO employees (name, department_id) VALUES ('Bahrul Rozak', 1);
INSERT INTO employees (name, department_id) VALUES ('John Doe', 2);

INSERT INTO departments (department_name) VALUES ('Engineering');
INSERT INTO departments (department_name) VALUES ('Marketing');
```

**Membuat View:**

```sql
CREATE VIEW employee_department AS
SELECT e.name AS employee_name, d.department_name
FROM employees e
JOIN departments d ON e.department_id = d.id;
```

**Penjelasan:**
- `CREATE VIEW employee_department AS` membuat view dengan nama `employee_department`.
- `SELECT e.name AS employee_name, d.department_name` memilih nama karyawan dan nama departemen.
- `FROM employees e JOIN departments d ON e.department_id = d.id` menggabungkan tabel `employees` dan `departments` berdasarkan `department_id`.

Sekarang, setiap kali temen-temen melakukan query ke view ini, MySQL akan menjalankan query di atas untuk menampilkan data:

```sql
SELECT * FROM employee_department;
```

#### 2. Apa Itu Materialized Views?

Berbeda dengan views biasa, **Materialized Views** adalah hasil query yang disimpan secara fisik di database. Ini berarti data dalam materialized view disimpan dalam bentuk tabel yang nyata dan tidak dihitung setiap kali kita mengaksesnya. Hal ini berguna untuk meningkatkan performa query yang sering dijalankan pada data yang tidak sering berubah.

Sayangnya, MySQL tidak secara langsung mendukung materialized views seperti beberapa database lain (misalnya, Oracle). Namun, kita bisa mensimulasikan materialized views dengan menggunakan tabel tambahan dan memanfaatkan *triggers* atau *scheduled events* untuk menyegarkan data.

##### Simulasi Materialized Views di MySQL

**Membuat Tabel untuk Materialized View:**

```sql
CREATE TABLE employee_department_mv (
    employee_name VARCHAR(100),
    department_name VARCHAR(100)
);
```

**Mengisi Data ke Tabel:**

```sql
INSERT INTO employee_department_mv
SELECT e.name AS employee_name, d.department_name
FROM employees e
JOIN departments d ON e.department_id = d.id;
```

**Menjaga Data Tetap Terupdate:**

Kita bisa menggunakan *triggers* untuk memperbarui tabel materialized view setiap kali ada perubahan pada tabel `employees` atau `departments`.

**Contoh Trigger untuk Pembaruan Data:**

```sql
CREATE TRIGGER update_employee_department_mv
AFTER INSERT ON employees
FOR EACH ROW
BEGIN
    INSERT INTO employee_department_mv (employee_name, department_name)
    SELECT NEW.name, d.department_name
    FROM departments d
    WHERE d.id = NEW.department_id;
END;
```

**Penjelasan:**
- `CREATE TRIGGER update_employee_department_mv` membuat trigger yang akan dijalankan setelah data baru ditambahkan ke tabel `employees`.
- `AFTER INSERT ON employees` menunjukkan bahwa trigger ini akan aktif setelah penyisipan data.
- `FOR EACH ROW` berarti trigger akan dijalankan untuk setiap baris yang ditambahkan.
- Bagian `BEGIN ... END` mendefinisikan aksi yang dilakukan oleh trigger, yaitu menyisipkan data ke `employee_department_mv` berdasarkan data yang baru ditambahkan.

#### Perbedaan antara Views dan Materialized Views

- **Views**:
  - Tidak menyimpan data secara fisik.
  - Selalu menampilkan data terbaru dari tabel yang diacu.
  - Biasanya lebih lambat jika query yang digunakan sangat kompleks, karena data dihitung setiap kali query dijalankan.

- **Materialized Views**:
  - Menyimpan data secara fisik.
  - Data mungkin tidak selalu terbaru jika tidak disegarkan secara berkala.
  - Lebih cepat dalam menampilkan data, terutama untuk query yang sering dijalankan.

Jadi, jika temen-temen perlu menampilkan data yang kompleks dengan performa tinggi dan tidak sering berubah, materialized view bisa menjadi pilihan yang lebih baik. Namun, jika temen-temen butuh data yang selalu up-to-date, menggunakan view adalah pilihan yang lebih tepat.

Referensi:
- [MySQL Documentation - Views](https://dev.mysql.com/doc/refman/8.0/en/create-view.html)
- [MySQL Documentation - Triggers](https://dev.mysql.com/doc/refman/8.0/en/create-trigger.html)
- [Simulating Materialized Views in MySQL](https://www.percona.com/blog/2015/07/01/simulating-materialized-views-in-mysql/)

Semoga penjelasan ini membantu temen-temen memahami lebih dalam tentang views dan materialized views di MySQL! Jangan ragu untuk mencoba dan eksplorasi lebih lanjut. Jika ada pertanyaan, feel free untuk bertanya! 😊
