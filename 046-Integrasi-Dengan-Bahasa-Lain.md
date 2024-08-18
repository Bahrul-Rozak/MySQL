
#### 1. **Integrasi MySQL dengan PHP**

**Pengenalan**
PHP adalah bahasa pemrograman server-side yang sering digunakan bersama MySQL untuk membangun aplikasi web dinamis. PHP mempermudah interaksi dengan database MySQL melalui ekstensi seperti `mysqli` dan `PDO`.

**Langkah-Langkah Integrasi**

1. **Koneksi ke Database MySQL:**
   Pertama-tama, kita perlu menghubungkan PHP ke database MySQL menggunakan `mysqli` atau `PDO`. Mari kita lihat contoh menggunakan `mysqli`.

   ```php
   <?php
   // Detail koneksi
   $servername = "localhost";
   $username = "root";
   $password = "";
   $dbname = "test_db";

   // Membuat koneksi
   $conn = new mysqli($servername, $username, $password, $dbname);

   // Mengecek koneksi
   if ($conn->connect_error) {
       die("Koneksi gagal: " . $conn->connect_error);
   }
   echo "Koneksi berhasil";
   ?>
   ```

   **Penjelasan:**
   - `mysqli` digunakan untuk membuat koneksi ke database.
   - `connect_error` memeriksa apakah koneksi gagal.
   - Jika koneksi berhasil, maka "Koneksi berhasil" akan ditampilkan.

2. **Mengambil Data dari Database:**

   ```php
   <?php
   $sql = "SELECT id, name FROM users";
   $result = $conn->query($sql);

   if ($result->num_rows > 0) {
       // Output data untuk setiap baris
       while($row = $result->fetch_assoc()) {
           echo "id: " . $row["id"]. " - Nama: " . $row["name"]. "<br>";
       }
   } else {
       echo "0 hasil";
   }
   $conn->close();
   ?>
   ```

   **Penjelasan:**
   - `query()` menjalankan perintah SQL untuk mengambil data.
   - `fetch_assoc()` mengembalikan baris data sebagai array asosiatif.

**Referensi:** [PHP MySQLi Documentation](https://www.php.net/manual/en/book.mysqli.php)

#### 2. **Integrasi MySQL dengan Python**

**Pengenalan**
Python menggunakan pustaka seperti `mysql-connector-python` atau `PyMySQL` untuk berinteraksi dengan MySQL. Kita akan menggunakan `mysql-connector-python` untuk contoh ini.

**Langkah-Langkah Integrasi**

1. **Koneksi ke Database MySQL:**

   ```python
   import mysql.connector

   # Koneksi ke database
   conn = mysql.connector.connect(
       host="localhost",
       user="root",
       password="",
       database="test_db"
   )

   cursor = conn.cursor()
   print("Koneksi berhasil")

   conn.close()
   ```

   **Penjelasan:**
   - `mysql.connector.connect()` digunakan untuk membuat koneksi.
   - `conn.cursor()` mengembalikan objek cursor untuk eksekusi perintah SQL.
   - Jangan lupa untuk menutup koneksi setelah selesai.

2. **Mengambil Data dari Database:**

   ```python
   import mysql.connector

   # Koneksi ke database
   conn = mysql.connector.connect(
       host="localhost",
       user="root",
       password="",
       database="test_db"
   )

   cursor = conn.cursor()
   cursor.execute("SELECT id, name FROM users")

   for (id, name) in cursor:
       print(f"id: {id}, Nama: {name}")

   conn.close()
   ```

   **Penjelasan:**
   - `cursor.execute()` menjalankan perintah SQL untuk mengambil data.
   - Iterasi melalui hasil cursor untuk menampilkan data.

**Referensi:** [MySQL Connector/Python Documentation](https://dev.mysql.com/doc/connector-python/en/)

#### 3. **Integrasi MySQL dengan Java**

**Pengenalan**
Java menggunakan JDBC (Java Database Connectivity) untuk berinteraksi dengan MySQL. JDBC adalah API yang memungkinkan Java untuk menghubungkan dan menjalankan perintah SQL pada database.

**Langkah-Langkah Integrasi**

1. **Koneksi ke Database MySQL:**

   ```java
   import java.sql.Connection;
   import java.sql.DriverManager;
   import java.sql.SQLException;

   public class MySQLConnection {
       public static void main(String[] args) {
           String url = "jdbc:mysql://localhost:3306/test_db";
           String user = "root";
           String password = "";

           try {
               Connection conn = DriverManager.getConnection(url, user, password);
               System.out.println("Koneksi berhasil");
               conn.close();
           } catch (SQLException e) {
               e.printStackTrace();
           }
       }
   }
   ```

   **Penjelasan:**
   - `DriverManager.getConnection()` digunakan untuk membuat koneksi.
   - Pastikan URL, username, dan password sesuai dengan konfigurasi database.

2. **Mengambil Data dari Database:**

   ```java
   import java.sql.Connection;
   import java.sql.DriverManager;
   import java.sql.ResultSet;
   import java.sql.Statement;
   import java.sql.SQLException;

   public class FetchData {
       public static void main(String[] args) {
           String url = "jdbc:mysql://localhost:3306/test_db";
           String user = "root";
           String password = "";

           try {
               Connection conn = DriverManager.getConnection(url, user, password);
               Statement stmt = conn.createStatement();
               String query = "SELECT id, name FROM users";
               ResultSet rs = stmt.executeQuery(query);

               while (rs.next()) {
                   int id = rs.getInt("id");
                   String name = rs.getString("name");
                   System.out.println("id: " + id + ", Nama: " + name);
               }
               conn.close();
           } catch (SQLException e) {
               e.printStackTrace();
           }
       }
   }
   ```

   **Penjelasan:**
   - `Statement` digunakan untuk menjalankan query SQL.
   - `ResultSet` menampung hasil query yang bisa diakses dengan metode `getInt()` dan `getString()`.

**Referensi:** [JDBC Documentation](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/)

### Kesimpulan

Integrasi MySQL dengan PHP, Python, dan Java memungkinkan kita untuk membangun aplikasi web dan desktop yang dinamis dan efisien. Masing-masing bahasa memiliki cara tersendiri untuk berinteraksi dengan MySQL, tetapi prinsip dasarnya adalah membuat koneksi ke database, menjalankan query, dan mengelola hasilnya. Dengan pemahaman ini, temen-temen bisa lebih fleksibel dalam memilih teknologi yang sesuai dengan kebutuhan proyek kalian.

**Referensi Tambahan:**
- [PHP MySQLi Documentation](https://www.php.net/manual/en/book.mysqli.php)
- [MySQL Connector/Python Documentation](https://dev.mysql.com/doc/connector-python/en/)
- [JDBC Documentation](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/)

Semoga penjelasan ini membantu temen-temen memahami bagaimana mengintegrasikan MySQL dengan PHP, Python, dan Java! Jangan ragu untuk mengeksplorasi lebih lanjut dan mencoba implementasi sederhana ini dalam proyek kalian.
