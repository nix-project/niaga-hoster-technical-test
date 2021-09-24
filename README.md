# Niaga Hoster Fullstack Test
berikut ini akan dijelaskan **step by step** build image docker yang berisi:

 - BoxBilling (Debian Base image) **(Step 2 Test)**
 - Nginx + MySQL + PHP-FPM **(Untuk running Step 1 Test)**
 
saya asumsikan package **docker** dan **docker-compose** telah terinstall dan siap digunakan. untuk detail installasi docker dan docker-compose dapat dilihat pada dokumentasi resmi docker https://docs.docker.com/get-docker/

### Step 1 (Clone Repository)
silahkan clone repository git berikut lalu masuk ke directory project yang telah di clone

    git clone https://github.com/angganix/niaga-hoster-technical-test.git && cd niaga-hoster-technical-test
### Step 2 (Running docker-compose up)
pastikan laptop terhubung dengan koneksi internet yang stabil, karena langkah **compose** ini akan melakukan pull image yang dibutuhkan, terutama pada saat sesi build **BoxBilling** dimana mana saya menggunakan **Base Image Debian**  yang pasti akan memakan banyak waktu untuk mendownload package. pada current directory yang telah dibuat, ketikan command berikut:

    docker-compose up --build
 silahkan ambil secangkir kopi dan tunggu hingga proses build selesai. untuk deskripsi service yang akan berjalan adalah sebagai berikut:
 
|  Service| Running Port
|--|--|
|Box Billing|8004|
|Web Server|8080|
|MySQL Server|3307|
|PHPMyAdmin|8081|

detail informasi variable environment dapat dilihat pada file **.env**
Credentials MySQL:
|Username|Password
|--|--|
|root|123456
|niagaweb|123456

Credentials BoxBilling MySQL:
|Username|Password
|--|--|
|root|123456
---
### Jika Proses build telah selesai
silahkan buka web browser dan masukan alamat address http://localhost:8080 makan final test untuk step satu akan muncul yaitu **front-end web test**.

--
untuk mengakses **BoxBiling** dapat membuka alamat address http://localhost:8004/install, jika membuka tanpa url **/install** makan akan terjadi error dikarenakan perlu adanya step awal installasi BoxBilling dengan mengisi beberapa dialog installasi. silahkan mengisi dialog BoxBilling yang ada dengan ketentuan sebagai berikut:

-- Untuk Informasi Database
 - Database Hostname : **localhost**
 - Database Name : **boxbilling**
 - Database Username : **root**
 - Database Password : **123456**

-- Untuk informasi BoxBilling ***(boleh disesuaikan)***

 - Administrator Name : **Administrator**
 - Email : **email.anda@yangvalid.com**
 - Password : **P@sswordUntukL0ginBoxB1lling**

---
Untuk live preview **Test Step 1** dapat dibuka pada link https://enigmatic-ravine-73607.herokuapp.com/

Terima Kasih Banyak
