#### Apa Itu Full Text Search?

Full Text Search adalah fitur di MySQL yang memungkinkan kamu melakukan pencarian teks dengan lebih efektif, terutama untuk teks panjang. Biasanya, fitur ini digunakan saat kamu perlu mencari kata-kata atau frasa dalam kolom teks yang besar, seperti artikel, deskripsi produk, atau konten blog. Ini berbeda dengan pencarian dasar yang hanya mencocokkan string secara langsung.

Misalnya, bayangkan kamu memiliki sebuah blog dengan banyak artikel, dan kamu ingin mencari artikel yang mengandung kata "programming" di dalamnya. Full Text Search memungkinkan kamu menemukan artikel tersebut dengan cara yang lebih efisien dibandingkan metode pencarian biasa.

#### Implementasi Full Text Search

Untuk menggunakan Full Text Search di MySQL, kamu perlu memastikan beberapa hal:

1. **Jenis Kolom**: Kolom yang akan digunakan untuk pencarian full text harus menggunakan tipe data `TEXT` atau `VARCHAR`.

2. **Index**: Kamu harus membuat index full text pada kolom yang ingin dipindai.

3. **Fungsi**: Kamu akan menggunakan fungsi `MATCH()` dan `AGAINST()` untuk melakukan pencarian.

Mari kita lihat implementasi langkah demi langkah.

#### Langkah 1: Menyiapkan Database dan Tabel

Pertama-tama, kita akan membuat database dan tabel yang diperlukan. Misalnya, kita membuat tabel `articles` untuk menyimpan artikel dengan kolom `title` dan `content`.

```sql
CREATE DATABASE blog;
USE blog;

CREATE TABLE articles (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255),
    content TEXT,
    FULLTEXT(title, content) -- Membuat index full text pada kolom title dan content
);
```

Penjelasan:
- `FULLTEXT(title, content)` membuat index full text pada kolom `title` dan `content`. Index ini memungkinkan pencarian teks di kolom-kolom tersebut.

#### Langkah 2: Menambahkan Data

Sekarang, kita tambahkan beberapa data ke tabel `articles`.

```sql
INSERT INTO articles (title, content) VALUES
('Introduction to Programming', 'Programming is the process of creating a set of instructions that tell a computer how to perform a task.'),
('Advanced Programming Techniques', 'In advanced programming, you use complex algorithms and data structures to solve problems more efficiently.'),
('Database Management Systems', 'A database management system (DBMS) is software that uses a standard method of storing and retrieving data.');
```

#### Langkah 3: Menggunakan MATCH() dan AGAINST()

Sekarang kita akan melakukan pencarian full text menggunakan `MATCH()` dan `AGAINST()`. Fungsi `MATCH()` digunakan untuk menentukan kolom yang akan dicari, dan `AGAINST()` menentukan kata atau frasa yang dicari.

```sql
SELECT id, title, content,
    MATCH(title, content) AGAINST('programming' IN BOOLEAN MODE) AS relevance
FROM articles
WHERE MATCH(title, content) AGAINST('programming' IN BOOLEAN MODE);
```

Penjelasan:
- `MATCH(title, content)`: Menentukan kolom `title` dan `content` yang akan dicari.
- `AGAINST('programming' IN BOOLEAN MODE)`: Mencari kata "programming" dalam mode boolean. Ini memberikan hasil yang lebih relevan.
- `AS relevance`: Memberikan nama alias untuk hasil relevansi pencarian.

#### Mode Pencarian

Ada beberapa mode pencarian yang bisa kamu gunakan dengan `AGAINST()`:

1. **Natural Language Mode**: Ini adalah mode default yang memungkinkan pencarian berbasis bahasa alami. Misalnya, pencarian akan memperhitungkan kata-kata umum dan relevansi berdasarkan frekuensi.

2. **Boolean Mode**: Memungkinkan penggunaan operator logika seperti `+` (harus ada), `-` (harus tidak ada), dan `*` (wildcard) untuk meningkatkan fleksibilitas pencarian. Misalnya, `+programming -advanced` mencari artikel yang mengandung kata "programming" tapi tidak "advanced".

3. **Query Expansion Mode**: Memperluas query dengan sinonim dan kata terkait untuk meningkatkan cakupan pencarian.

#### Contoh Penggunaan Boolean Mode

Misalkan kita ingin mencari artikel yang mengandung kata "programming" tetapi tidak "advanced". Kita bisa menggunakan:

```sql
SELECT id, title, content,
    MATCH(title, content) AGAINST('+programming -advanced' IN BOOLEAN MODE) AS relevance
FROM articles
WHERE MATCH(title, content) AGAINST('+programming -advanced' IN BOOLEAN MODE);
```

#### Studi Kasus Sederhana

**Studi Kasus: Blog Bahrul Rozak**

Bayangkan Bahrul Rozak memiliki blog dengan berbagai artikel teknis dan dia ingin pengguna mencari artikel tentang "database" tetapi tidak terlalu teknis. Dengan menggunakan Full Text Search, Bahrul dapat dengan mudah menemukan artikel yang relevan untuk ditampilkan kepada pembaca.

```sql
SELECT id, title, content,
    MATCH(title, content) AGAINST('database -technical' IN BOOLEAN MODE) AS relevance
FROM articles
WHERE MATCH(title, content) AGAINST('database -technical' IN BOOLEAN MODE);
```

#### Referensi

Untuk informasi lebih lanjut dan dokumentasi resmi MySQL mengenai Full Text Search, kamu bisa mengunjungi:

- [MySQL Full-Text Search Documentation](https://dev.mysql.com/doc/refman/8.0/en/fulltext-boolean.html)
- [MySQL MATCH() Function](https://dev.mysql.com/doc/refman/8.0/en/fulltext-boolean.html#fulltext-function-match)
- [MySQL AGAINST() Function](https://dev.mysql.com/doc/refman/8.0/en/fulltext-boolean.html#fulltext-function-against)

Dengan memahami dan menggunakan Full Text Search, kamu bisa meningkatkan kemampuan pencarian dalam aplikasi atau situs web kamu secara signifikan. Semoga panduan ini membantu!
