Halo temen-temen! Hari ini gue bakal ngajak lo semua untuk menggali lebih dalam tentang salah satu bagian dari SQL yang sering kita pakai dalam dunia database, yaitu fungsi matematika. Mungkin lo pernah dengar fungsi-fungsi seperti `ROUND()`, `CEIL()`, dan `FLOOR()`. Kalau lo belum pernah dengar atau masih bingung cara pakainya, santai aja! Gue akan jelasin semuanya dengan bahasa yang mudah dipahami, dan tentunya dengan contoh yang konkret biar lo makin paham.

### Fungsi ROUND(): Membulatkan Angka ke Nilai Terdekat

Bayangin lo lagi belanja di sebuah toko, dan lo dapet total belanjaan sebesar Rp 1.237,50. Nah, mungkin lo bakal pengen ngebulatinnya ke angka yang lebih rapi, misalnya Rp 1.238. Di sinilah fungsi `ROUND()` masuk!

#### Apa Itu Fungsi ROUND()?
Fungsi `ROUND()` di MySQL digunakan buat membulatkan angka desimal ke nilai terdekat. Lo bisa memilih berapa banyak angka desimal yang pengen ditampilkan. Kalau lo nggak spesifikin, secara default dia bakal ngebulatinnya ke bilangan bulat terdekat.

#### Sintaks ROUND()
```sql
SELECT ROUND(angka, jumlah_desimal);
```

- `angka`: Ini adalah angka yang pengen lo bulatin.
- `jumlah_desimal`: Ini adalah jumlah angka desimal yang pengen lo tampilkan. Kalau diisi 0, hasilnya adalah bilangan bulat terdekat.

#### Contoh Penggunaan ROUND()
Misalnya, temen-temen punya harga barang yang ingin dibulatkan:

```sql
SELECT ROUND(1237.567, 2) AS Hasil;
```

Ini akan mengembalikan nilai `1237.57`. Kenapa? Karena `567` kalau dibulatkan ke dua angka desimal terdekat jadi `57`.

Kalau temen-temen pengen ngebulatinnya ke bilangan bulat aja:

```sql
SELECT ROUND(1237.567, 0) AS Hasil;
```

Hasilnya adalah `1238`. Jadi, `ROUND()` akan selalu membulatkan ke atas atau ke bawah, tergantung pada angka terdekatnya.

#### Kapan Harus Pakai ROUND()?
Fungsi ini cocok banget buat situasi di mana lo pengen menampilkan data dalam format yang lebih rapi, misalnya harga, persentase, atau data keuangan lainnya. Jadi, misalnya Bahrul Rozak pengen bikin laporan keuangan yang datanya lebih rapi, dia bisa pake fungsi `ROUND()` buat ngebulatinnya.

### Fungsi CEIL(): Membulatkan Angka ke Atas

Sekarang, bayangin lo lagi main game, dan skor lo 99.7. Nah, lo pengen skornya dibulatkan ke 100 biar keliatan lebih keren, bukan? Di sini, fungsi `CEIL()` bisa membantu lo!

#### Apa Itu Fungsi CEIL()?
Fungsi `CEIL()` di MySQL digunakan buat membulatkan angka ke atas, terlepas dari berapa angka desimal di belakangnya. Bahkan kalau angkanya adalah 99.1, `CEIL()` bakal ngebulatinnya ke 100.

#### Sintaks CEIL()
```sql
SELECT CEIL(angka);
```

- `angka`: Ini adalah angka yang pengen lo bulatin ke atas.

#### Contoh Penggunaan CEIL()
Misalnya, temen-temen punya angka yang pengen dibulatkan ke atas:

```sql
SELECT CEIL(99.1) AS Hasil;
```

Ini akan mengembalikan nilai `100`. Begitu juga kalau lo punya:

```sql
SELECT CEIL(99.9) AS Hasil;
```

Hasilnya tetap `100`. Fungsi ini bener-bener simpel dan to the point!

#### Kapan Harus Pakai CEIL()?
Fungsi `CEIL()` sering dipake ketika lo pengen memastikan nilai yang lo dapet selalu dibulatkan ke atas. Contohnya, kalau Bahrul Rozak lagi bikin sistem penilaian dan pengen pastiin kalau nilai yang hampir sempurna selalu dapet skor penuh, dia bisa pake `CEIL()`.

### Fungsi FLOOR(): Membulatkan Angka ke Bawah

Nah, kebalikan dari `CEIL()`, kadang kita pengen ngebulatinnya ke bawah. Misalnya, lo punya skor 99.9, tapi lo pengen ngebulatinnya ke 99. Di sinilah `FLOOR()` bakal membantu lo.

#### Apa Itu Fungsi FLOOR()?
Fungsi `FLOOR()` di MySQL digunakan buat membulatkan angka ke bawah. Jadi, berapapun angka desimalnya, dia bakal selalu ngebulatinnya ke bilangan bulat yang lebih kecil.

#### Sintaks FLOOR()
```sql
SELECT FLOOR(angka);
```

- `angka`: Ini adalah angka yang pengen lo bulatin ke bawah.

#### Contoh Penggunaan FLOOR()
Misalnya, temen-temen punya angka yang pengen dibulatkan ke bawah:

```sql
SELECT FLOOR(99.9) AS Hasil;
```

Ini akan mengembalikan nilai `99`. Bahkan kalau lo punya:

```sql
SELECT FLOOR(99.1) AS Hasil;
```

Hasilnya tetap `99`. Jadi, fungsi `FLOOR()` ini bakal selalu ngebulatinnya ke angka yang lebih kecil.

#### Kapan Harus Pakai FLOOR()?
Fungsi `FLOOR()` sering dipake ketika lo pengen ngebulatinnya ke bawah, mungkin buat memastikan sesuatu nggak melampaui batas tertentu. Misalnya, kalau Bahrul Rozak lagi bikin sistem diskon dan pengen memastikan diskon maksimal tidak lebih dari batas yang ditentukan, dia bisa pake `FLOOR()`.

### Kombinasi Penggunaan ROUND(), CEIL(), dan FLOOR()

Lo juga bisa mengkombinasikan penggunaan ketiga fungsi ini tergantung dari kebutuhan lo. Misalnya, lo bisa pake `ROUND()` buat ngebulatin hasil penjualan ke angka tertentu, `CEIL()` buat ngebulatinnya ke atas kalau lo pengen selalu dapat keuntungan lebih, dan `FLOOR()` buat ngebulatinnya ke bawah kalau lo pengen tetap di bawah anggaran.

### Contoh Kasus dengan Bahrul Rozak

Bayangin Bahrul Rozak punya toko online dan dia pengen menghitung harga akhir barang setelah diskon dan pajak. Dia bisa pake kombinasi fungsi-fungsi ini buat ngebulatinnya.

Misalnya, harga barangnya Rp 99.99 dan dia kasih diskon 10%. Bahrul Rozak pengen memastikan harga akhir dibulatkan ke atas biar dia gak rugi:

```sql
SELECT CEIL(ROUND(99.99 * 0.9, 2)) AS Harga_Akhir;
```

Di sini, `ROUND()` ngebulatin hasilnya jadi dua angka desimal, dan `CEIL()` memastikan harganya dibulatkan ke atas. Kalau hasilnya Rp 89.991, `CEIL()` bakal ngebulatinnya ke Rp 90.

### Kesimpulan

Jadi, temen-temen, `ROUND()`, `CEIL()`, dan `FLOOR()` adalah fungsi-fungsi matematika dasar yang sangat berguna di MySQL buat ngebulatkan angka sesuai kebutuhan lo. `ROUND()` bisa ngebulatin ke nilai terdekat, `CEIL()` bakal selalu ngebulatinnya ke atas, dan `FLOOR()` ngebulatinnya ke bawah. Dengan memahami cara kerja fungsi-fungsi ini, lo bisa lebih fleksibel dalam menangani data numerik di database lo.

Gue harap penjelasan ini bisa membantu temen-temen dalam memahami fungsi-fungsi matematika di MySQL. Kalau temen-temen mau baca lebih lanjut, lo bisa cek referensi [di sini](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html) untuk dokumentasi resmi MySQL.

Terus belajar dan semoga sukses dalam coding, temen-temen!
