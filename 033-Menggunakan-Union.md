Temen-temen, pernah gak sih kalian pengen menggabungkan hasil query dari beberapa tabel atau query yang berbeda? Misalnya, kalian punya dua tabel yang berbeda, tapi ingin melihat data dari kedua tabel tersebut dalam satu hasil query. Nah, di sinilah perintah `UNION` dan `UNION ALL` berperan. 

### **Apa Itu UNION?**

Perintah `UNION` digunakan untuk menggabungkan hasil dari dua atau lebih query `SELECT` menjadi satu hasil. Perintah ini menghilangkan duplikat secara otomatis, jadi setiap baris yang sama hanya akan muncul sekali dalam hasil akhir. 

### **Apa Itu UNION ALL?**

Berbeda dengan `UNION`, perintah `UNION ALL` menggabungkan hasil dari beberapa query `SELECT` tanpa menghilangkan baris duplikat. Ini berarti jika ada data yang sama dari query yang berbeda, semua data tersebut akan ditampilkan dalam hasil akhir.

### **Kapan Menggunakan UNION dan UNION ALL?**

- **UNION**: Gunakan `UNION` saat kalian ingin menggabungkan hasil dari beberapa query dan ingin menghindari duplikasi data.
- **UNION ALL**: Gunakan `UNION ALL` jika kalian ingin melihat semua hasil query, termasuk baris yang duplikat. Ini biasanya lebih cepat daripada `UNION` karena tidak perlu melakukan pengecekan duplikat.

### **Syarat Penggunaan**

Agar bisa menggunakan `UNION` atau `UNION ALL`, ada beberapa syarat yang harus dipenuhi:
1. **Jumlah Kolom**: Semua query yang digabungkan harus memiliki jumlah kolom yang sama.
2. **Tipe Data**: Tipe data dari kolom yang digabungkan harus kompatibel atau bisa dipromosikan satu sama lain.
3. **Urutan Kolom**: Urutan kolom dalam setiap query harus sama.

### **Contoh Kode**

Misalnya, kita punya dua tabel yang berbeda: `karyawan_2023` dan `karyawan_2024`. Kita ingin melihat semua karyawan dari kedua tahun tersebut.

**Tabel `karyawan_2023`:**

| id | nama       | jabatan   |
|----|------------|-----------|
| 1  | Ahmad      | Developer |
| 2  | Budi       | Designer  |

**Tabel `karyawan_2024`:**

| id | nama       | jabatan   |
|----|------------|-----------|
| 1  | Citra      | Developer |
| 2  | Dedi       | Manager   |

Kita bisa menggunakan `UNION` untuk menggabungkan data dari kedua tabel:

```sql
SELECT nama, jabatan FROM karyawan_2023
UNION
SELECT nama, jabatan FROM karyawan_2024;
```

Hasilnya:

| nama   | jabatan   |
|--------|-----------|
| Ahmad  | Developer |
| Budi   | Designer  |
| Citra  | Developer |
| Dedi   | Manager   |

Di sini, `UNION` secara otomatis menghilangkan baris duplikat, jadi jika ada data yang sama di kedua tabel, hanya satu baris yang ditampilkan. Tapi karena dalam contoh ini, semua data berbeda, hasilnya sama dengan jika kita menggunakan `UNION ALL`.

Sekarang, mari kita coba `UNION ALL`:

```sql
SELECT nama, jabatan FROM karyawan_2023
UNION ALL
SELECT nama, jabatan FROM karyawan_2024;
```

Hasilnya:

| nama   | jabatan   |
|--------|-----------|
| Ahmad  | Developer |
| Budi   | Designer  |
| Citra  | Developer |
| Dedi   | Manager   |

Dengan `UNION ALL`, semua baris dari kedua tabel ditampilkan, termasuk duplikat jika ada. Jadi, jika ada data yang sama di kedua tabel, akan muncul lebih dari sekali.

### **Analogi untuk Memudahkan Pemahaman**

Bayangkan kalian lagi di sebuah pesta dengan dua teman yang masing-masing bawa daftar tamu. Teman pertama bawa daftar tamu A, sedangkan teman kedua bawa daftar tamu B. 

- **UNION**: Ini seperti jika kalian menggabungkan kedua daftar tamu dan hanya menulis nama yang unik sekali saja. Jadi, kalau ada nama yang sama di kedua daftar, kalian hanya menuliskannya sekali.

- **UNION ALL**: Ini seperti menggabungkan kedua daftar tamu tanpa peduli apakah nama itu muncul lebih dari sekali. Jadi, jika ada nama yang sama di kedua daftar, kalian menuliskannya dua kali.

### **Referensi**

Untuk informasi lebih lanjut, kalian bisa cek referensi berikut:

- [MySQL Documentation: UNION](https://dev.mysql.com/doc/refman/8.0/en/union.html)
- [MySQL Documentation: UNION ALL](https://dev.mysql.com/doc/refman/8.0/en/union.html#union-all)

Dengan memahami penggunaan `UNION` dan `UNION ALL`, kalian bisa lebih fleksibel dalam mengelola data dari berbagai sumber dan mendapatkan hasil yang sesuai dengan kebutuhan kalian. Semoga penjelasan ini bermanfaat dan memudahkan temen-temen dalam bekerja dengan MySQL! 🚀

---
