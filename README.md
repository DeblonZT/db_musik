
# Memahami perbedaan antara INNER, LEFT, dan RIGHT JOIN sangat penting dalam mengelola database, terutama saat bekerja dengan sistem yang kompleks seperti manajemen data sekolah atau sistem reservasi yang sedang di kembangkan.

Bayangkan kita memiliki dua tabel dari database db_musik dengan: <br>
Tabel Artis: Berisi ID_Artis dan Nama_Artis.

CREATE TABLE Artis ( <br>
ID_Artis INT(11) AUTO_INCREMENT PRIMARY KEY, <br>
Nama_Artis VARCHAR(100) NOT NULL <br>
);

Dan

Tabel Lagu: Berisi ID_Lagu, Judul_Lagu dan ID_Artis. (foreign key)

CREATE TABLE Lagu ( <br>
ID_Lagu INT(11) AUTO_INCREMENT PRIMARY KEY, <br>
Judul_Lagu VARCHAR(150) NOT NULL, <br>
ID_Artis INT(11), <br>
CONSTRAINT fk_artis_lagu <br>
FOREIGN KEY (ID_Artis) REFERENCES Artis(ID_Artis) ON DELETE CASCADE ON UPDATE CASCADE  <br>
);


ketika kedua table tersebut dimasukan data maka akan muncul tampilan seperti berikut: <br>
Table Artis: <br>
ID_Artis, Nama_Artis <br>
1, Tulus <br>
2, Sheila on 7 <br>
3, Autumn! <br>
4, Jnhygs <br>

Table Lagu: <br>
+---------+--------------------+----------+ <br>
| ID_Lagu | Judul_Lagu        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | ID_Artis | <br> 
+---------+--------------------+----------+ <br>
|       1 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| Hati-Hati di Jalan &nbsp;|        1 | <br>
|       2 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| Monokrom  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;     |        1 | <br>
|       3 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| Dan     &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;           |        2 | <br>
|       4 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| One Way!      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;     |        3 | <br>
|       5 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| Not 2 not 3     &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   |        3 | <br>
|       6 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| Shake That SH!T   &nbsp;&nbsp; |        4 | <br>
+---------+--------------------+----------+ <br>

#
### 1. INNER JOIN (Hasil yang Saling Memiliki Pasangan)
![alt text](https://media.geeksforgeeks.org/wp-content/uploads/20250607125822884856/SQL-Join.webp?raw=true) <br>
Query ini hanya akan menampilkan baris di mana ada kecocokan di kedua tabel. Karena semua lagu Anda memiliki ID_Artis yang valid (1, 2, 3, dan 4), maka semua data akan muncul.

select Artis.Nama_Artis, Lagu.Judul_Lagu from Artis inner join Lagu on Artis.ID_Artis = Lagu.ID_Artis; <br>
+-------------+--------------------+ <br>
| Nama_Artis  | Judul_Lagu         | <br>
+-------------+--------------------+ <br>
| Tulus  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;    | Hati-Hati di Jalan | <br>
| Tulus    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;  | Monokrom           | <br>
| Sheila on 7 &nbsp;| Dan                | <br>
| Autumn!    &nbsp;&nbsp;&nbsp;&nbsp; | One Way!           | <br>
| Autumn!     &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| Not 2 not 3        | <br>
| Jnhygs     &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Shake That SH!T    | <br>
+-------------+--------------------+ <br>

### 2. LEFT JOIN (Utamakan Tabel Kiri/ Tabel Artis)
![alt text](https://media.geeksforgeeks.org/wp-content/uploads/20250607130445309937/Left_Join.webp?raw=true) <br>
Query ini mengambil semua data dari tabel sebelah kiri (Artis). Jika ada artis yang belum punya lagu, barisnya tetap muncul tapi kolom lagunya akan kosong (NULL). <br>
ID_Artis, Nama_Artis  <br>
1, Tulus <br>
2, Sheila on 7 <br>
3, Autumn! <br>
4, Jnhygs <br>
