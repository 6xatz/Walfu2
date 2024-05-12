## Mata Kuliah

Sebagai tugas praktikum: [2] Basis Data | Universitas Pelita Bangsa.

## Laporan Praktikum

- Data Model Mapping:

```
Mahasiswa (nim, nama, jenis_kelamin, tgl_lahir, jalan, kota, kodepos, no_hp, kd_ds)

Dosen (kd_ds, nama)

Matakuliah (kd_mk, nama, sks)

JadwalMengajar (kd_ds, kd_mk, hari, jam, ruang)

KRSMahasiswa (nim, kd_mk, kd_ds, semester, nilai)
```

- Bagian 1:

  <p align="left">
    <img src="/ss/1.jpg" width="200">
  </p>

```
CREATE TABLE Mahasiswa (
    nim varchar(10) PRIMARY KEY,
    nama varchar(25) NOT NULL,
    jenis_kelamin ENUM('Laki-Laki', 'Perempuan'),
    tgl_lahir DATE,
    jalan varchar(15) NOT NULL,
    kota varchar(15) NOT NULL,
    kodepos varchar(5) NOT NULL,
    no_hp varchar(15) NOT NULL,
    kd_ds varchar(10) NOT NULL,
    FOREIGN KEY (kd_ds) REFERENCES Dosen(kd_ds)
    );

CREATE TABLE Dosen (
    kd_ds varchar(10) PRIMARY KEY,
    nama varchar(35) NOT NULL
    );

CREATE TABLE Matakuliah (
    kd_mk varchar(10) PRIMARY KEY,
    nama varchar(30) NOT NULL,
    sks INT NOT NULL
    );

CREATE TABLE JadwalMengajar (
    kd_ds varchar(10) NOT NULL,
    kd_mk varchar(10) NOT NULL,
    hari ENUM('Senin', 'Selasa', 'Rabu', 'Kamis', 'Jumat', 'Sabtu', 'Minggu') NOT NULL,
    jam TIME NOT NULL,
    ruang varchar(555) NOT NULL,
    PRIMARY KEY (kd_ds, kd_mk, hari, jam),
    FOREIGN KEY (kd_ds) REFERENCES Dosen(kd_ds),
    FOREIGN KEY (kd_mk) REFERENCES Matakuliah(kd_mk)
    );

CREATE TABLE KRSMahasiswa (
    nim varchar(10) NOT NULL,
    kd_mk varchar(10) NOT NULL,
    kd_ds varchar(10) NOT NULL,
    semester varchar(10) NOT NULL,
    nilai FLOAT NOT NULL,
    PRIMARY KEY (nim, kd_mk),
    FOREIGN KEY (nim) REFERENCES Mahasiswa(nim),
    FOREIGN KEY (kd_mk) REFERENCES Matakuliah(kd_mk),
    FOREIGN KEY (kd_ds) REFERENCES Dosen(kd_ds)
    );
```

**CREATE TABLE** digunakan untuk membuat Tabel, sedangkan **VARCHAR(15)** merupakan variable character atau karakter ber-tipe variabel berjumlah 15.

- Bagian 2:

  > Menambahkan 5 record data.

  <p align="left">
    <img src="/ss/2.jpg" width="400">
  </p>

```
insert into Mahasiswa (nim, nama, jenis_kelamin, tgl_lahir, jalan, kota, kodepos, no_hp, kd_ds) values 
-> (11223344,"6xatz","Laki-laki","1998-10-12","","Bekasi","","",""), 
-> (11223345,"Fluthfi","Laki-laki","1999-11-16","","Cikarang","","",""), 
-> (11223346,"Airalva","Perempuan","1997-12-01","","Karawang","","",""), 
-> (11223347,"Cixia","Perempuan","1996-01-02","","Bekasi","","",""), 
-> (11223348,"Salsa","Perempuan","1980-02-05","","Bekasi","","",""), 
-> (11223349,"Ryuutarde","Laki-Laki","1988-03-10","","Cikarang","","","");
```

Setiap **"** atau **()** diisi dengan values yang diinginkan.

- Bagian 3:

  > Memilih, Merubah, Menghapus record Mahasiswa.

  <p align="left">
    <img src="/ss/3.jpg" width="400">
  </p>

```
# Menampilkan dan Memilih record data (dengan kriteria tertentu).
select*from Mahasiswa;
select*from Mahasiswa -> order by nama asc;
select*from Mahasiswa where nim=11223344;
select*from Mahasiswa where tgl_lahir<='1996-1-2';
select*from Mahasiswa where kota='Bekasi' and jenis_kelamin='Perempuan';
select nama, jalan from Mahasiswa;

# Merubah record data salah satu Mahasiswa dengan kriteria tertentu.
update Mahasiswa set tgl_lahir='1979-08-31' where nim=11223344;

# Menghapus record data salah satu Mahasiswa dengan kriteria tertentu.
delete from Mahasiswa where nim=11223346;
```

Kriteria dapat digabungkan dan diisi dengan values yang diinginkan.

## Evaluasi dan Pertanyaan

- Bagian 1: Menambah data

`INSERT INTO <table> (field1, ..., fieldn) VALUE (value1, ..., valuen)`

*Contoh :*

  <p align="left">
    <img src="/ss/4.jpg" width="400">
  </p>

- Bagian 2: Menampilkan data

`SELECT * FROM <table> SELECT [field1, ..., fieldn] FROM <table>`

*Contoh :*

  <p align="left">
    <img src="/ss/5.jpg" width="400">
  </p>

- Bagian 3: Merubah data

`UPDATE <table> SET field1=val1, ..., fieldn=valn WHERE <kondisi>;`

*Contoh :*

  <p align="left">
    <img src="/ss/6.jpg" width="400">
  </p>

- Bagian 4: Menghapus data

`DELETE FROM <table> WHERE <kondisi>`

*Contoh :*

  <p align="left">
    <img src="/ss/7.jpg" width="400">
  </p>

- Bagian 5: Pertanyaan

***Apa bedanya penggunaan BETWEEN dan penggunaan operator >= dan <= ?***

- (misal: tgl_lahir BETWEEN '1990-10-10' AND '1992-10-11'),

- (misal: tgl_lahir >= '1990-10-10' AND tgl_lahir <= '1992-10-11').

***Jawaban nya :***

Operator BETWEEN ini untuk menangani operasi “jangkauan” sedangkan operator >= dan <= termasuk pada operator relasional. Operator yang digunakan untuk perbandingan antara dua buah nilai. Jenis dari operator ini adalah: = , >, <, >=, <=, <>.

***Berikan kesimpulan anda!***

Data Manipulation Language (DML) adalah bahasa pemrograman yang digunakan untuk mengakses, memanipulasi, dan mengelola data dalam sebuah database. DML memungkinkan pengguna untuk melakukan operasi seperti penyisipan data baru, pembaruan data yang sudah ada, penghapusan data, dan kueri data untuk pengambilan informasi yang diperlukan.

Dalam DML, pengguna dapat menggunakan perintah SQL (Structured Query Language) untuk mengakses data. SQL adalah bahasa standar untuk mengakses dan mengelola data dalam database relasional. Perintah SQL yang digunakan dalam DML termasuk menambah, mengubah, menghapus, dan menampilkan data seperti yang telah dipraktekkan diatas.

## Documentation

All associated resources. are licensed under the [MIT License](https://mit-license.org/).
