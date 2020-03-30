SOAL No.1
3 DBMS yang bisa digunakan untuk mengelola big data
 a. RDBMS = IBM DB2, MySQL, Microsoft SQL Server, dan Microsoft Access.
 b. ORDBMS= Oracle Database , PostgreSQL , dan Microsoft SQL Server .
 c. OODBMS= Database berorientasi objek Versant , Objectivity / DB , ObjectDB , dan ObjectStore .

SOAL NO.2
Carilah contoh masalah big data yang bisa dikelola menggunakan salah satu DBMS tersebut, jelaskan mulai dari instalasi sampai CRUD 
untuk data menggunakan DBMS tersebut. Asumsikan anda akan memecahkan masalah big data yang sudah anda cari contoh tadi, 
jelaskan kira-kira bagaimana arsitektur dari solusi big data menggunakan DBMS tersebut, gambarkan diagramnya.

Tutorial Python dan MySQL: Membuat Database Tiket Pesawat

1. Instalasi Modul MySQL Connector
   Ketik peritah berikut untuk menginstal modul mysql untuk Python.
   $ sudo apt install python3-mysql.connector ATAU pip3 install mysql-connector
   
2. Koneksi ke MySQL dan membuat connect.py
import mysql.connector
db = mysql.connector.connect(
  host="localhost",
  user="admin",
  passwd="admin"
)
if db.is_connected():
  print("Berhasil terhubung ke database")
  
3. Jalankan connect.py dengan Python 3.
   $python3 connect.py
   Ketika berhasil akan ada keterangan berhasil terhubung Ke Database
   
4. Kita membutuhkan modul mysql.connector untuk membuat koneksi ke MySQL.
   $import mysql.connector
    Lalu kita membuat koneksi dengan memanggil fungsi connect() dan parameter host, user, dan passwd.
db = mysql.connector.connect(
  host="localhost",
  user="admin",
  passwd="admin"
)

5. Jika menggunakan XAMPP, menggunakan parameter seperti dibawah:
db = mysql.connector.connect(
  host="localhost",
  user="root",
  passwd="")

6. Karena user default di XAMPP adalah root dan di sana biasanya tidak menggunakan password lalu cek koneksi.
if db.is_connected():
  print("Berhasil terhubung ke database")

7. Membuat Database
Membuat objek cursor kita tinggal buat seperti dibawah:
cursor = db.cursor()

8. Lalu untuk mengeksekusi query, tinggal panggil method execute() dengan parameter string query.
cursor.execute(sql)

9. Membuat file baru bernama create_db.py. Kemudian isi dengan kode berikut:
import mysql.connector
db = mysql.connector.connect(
  host="localhost",
  user="admin",
  passwd="admin"
)
cursor = db.cursor()
cursor.execute("CREATE DATABASE tiket_pesawat")
print("Database berhasil dibuat!")

10. Setelah itu menjalankan create_db.py dengan Python 3.
python3 create_db.py
Maka akan ada keterangan database dibuat

11. Membuat database toko mainan
db = mysql.connector.connect(
  host="localhost",
  user="admin",
  passwd="admin",
  database="tiket_pesawat"
)

12. Membuat file baru bernama create_table.py
import mysql.connector

db = mysql.connector.connect(
  host="localhost",
  user="admin",
  passwd="admin",
  database="tiket_pesawat"
)

cursor = db.cursor()
sql = """CREATE TABLE pembeli (  
  ID_pembeli INT AUTO_INCREMENT PRIMARY KEY,
  nama VARCHAR1(50),
  usia INT (11),
  e_mail VARCHAR (50)
)
"""
cursor.execute(sql)
print("Tabel pembeli berhasil dibuat!")

13. Akan ada keterangan tabel pembeli telah dibuat
python3 create_table.py

14. Membuat file baru bernama insert_one.py kemudian isi dengan kode berikut:
import mysql.connector

db = mysql.connector.connect(
  host="localhost",
  user="admin",
  passwd="admin",
  database="tiket_pesawat"
)

cursor = db.cursor()
sql = "INSERT INTO pembeli (ID pembeli, nama, usia, e_mail) VALUES (%s, %s, %s, %s)"
val = (110, "Muhammad Afrizal", 21 , muhammadafrizal@gmail.com )
cursor.execute(sql, val)

db.commit()

print("{} data ditambahkan".format(cursor.rowcount))

15. Menampilkan data dengan membuat file baru bernama select.py kemudia isi dengan kode berikut:
import mysql.connector

db = mysql.connector.connect(
  host="localhost",
  user="admin",
  passwd="admin",
  database="tiket_pesawat"
)

cursor = db.cursor()
sql = "SELECT * FROM pembeli"
cursor.execute(sql)

results = cursor.fetchall()

for data in results:
  print(data)

16. Update Data dengan membuat file baru bernama update.py. Kemudian isi dengan kode berikut:
import mysql.connector

db = mysql.connector.connect(
  host="localhost",
  user="admin",
  passwd="admin",
  database="tiket_pesawat"
)

cursor = db.cursor()
sql = "UPDATE pembeli SET nama=%s, usia=%s, e_mail=%s WHERE ID pembeli=%s"
val = ("Zhal", 21 , muhammadafrizal212@gmail.com, 120 )
cursor.execute(sql, val)

db.commit()

print("{} data diubah".format(cursor.rowcount))

17. Menghapus Data dengan membuat file baru bernama delete.py, kemudian isi dengan kode berikut:
import mysql.connector

db = mysql.connector.connect(
  host="localhost",
  user="admin",
  passwd="admin",
  database="tiket_pesawat"
)

cursor = db.cursor()
sql = "DELETE FROM pembeli WHERE ID_pembeli=%s"
val = (120, )
cursor.execute(sql, val)

db.commit()

print("{} data dihapus".format(cursor.rowcount))
