\# API Wisata Sulawesi Tengah



Project ini merupakan API untuk data destinasi wisata di Sulawesi Tengah. API ini dibuat untuk mengelola dan menampilkan informasi destinasi wisata dan wilayah, serta menyediakan informasi cuaca. API ini memiliki versi 1 dan versi 2, autentikasi menggunakan API key, sistem token berdasarkan role, dan GraphQL.



\## Cara Menjalankan Project



\### 1. Clone Repository



Salin repository ini ke komputer masing-masing menggunakan perintah:



```bash

git clone https://github.com/fluttershy202/api-wisata-sulteng.git

```



Setelah selesai, masuk ke folder project:



```bash

cd api-wisata-sulteng

```



\### 2. Instal Dependensi



Jalankan perintah berikut untuk menginstal dependensi yang dibutuhkan:



```bash

npm install

```



\### 3. Membuat File Konfigurasi



Buat file `.env` di folder utama project, lalu isi dengan:



```env

TOKEN\_SECRET=secret\_acak\_milik\_sendiri

```



`TOKEN\_SECRET` digunakan untuk proses pembuatan dan pemeriksaan token. Nilainya bebas dibuat sendiri, tetapi sebaiknya menggunakan string acak yang kuat dan tidak dibagikan.



\### 4. Menyiapkan File Data



Beberapa file tidak disertakan dalam repository, sehingga perlu dibuat sendiri, yaitu:



\- `data/users.json` untuk menyimpan data akun.

\- `data/api-keys.json` untuk menyimpan API key.



File `destinations.json` dan `regions.json` sudah tersedia sehingga tidak perlu dibuat ulang.



Untuk membuat akun, project sudah menyediakan file `buat-user.js`. Contoh perintah untuk membuat akun admin:



```bash

node buat-user.js admin password123 admin

```



Role yang tersedia adalah `admin`, `editor`, dan `viewer`. Username dan password pada contoh tersebut hanya untuk contoh pembuatan akun, bukan akun yang sudah tersedia.



\### 5. Menjalankan Server



Setelah konfigurasi selesai, jalankan server menggunakan perintah:



```bash

node --env-file=.env server.js

```



Jika berhasil, API dapat diakses melalui alamat:



```text

http://localhost:3000

```



Pengujian request API dapat dilakukan menggunakan Postman dengan menyertakan API key yang sudah disiapkan.



\## Versi API yang Tersedia



\### API v1



API v1 dapat diakses menggunakan awalan `/v1`. Versi ini menggunakan format data lama dan masih dapat digunakan, tetapi sudah memiliki pemberitahuan masa berakhir layanan.



Contoh endpoint:



\- `GET /v1/destinations`

\- `GET /v1/destinations/1`



\### API v2



API v2 dapat diakses menggunakan awalan `/v2`. Versi ini menggunakan format data terbaru dan menyediakan endpoint destinasi serta wilayah.



Contoh endpoint:



\- `GET /v2/destinations`

\- `GET /v2/destinations/1`

\- `GET /v2/regions`



Destinasi juga dapat difilter berdasarkan wilayah menggunakan parameter `regionId`. Contohnya:



```text

GET /v2/destinations?regionId=3

```



Request tersebut akan menampilkan destinasi yang memiliki `regionId` bernilai 3.



\### Header Versioning



Selain menggunakan awalan versi pada URL, API juga dapat diakses menggunakan header `x-api-version`.



Contoh request:



```http

GET /destinations/1

x-api-version: 1

```



Untuk menggunakan versi 2, nilai header diubah menjadi `2`. Jika versi tidak dicantumkan melalui URL maupun header, server akan mengembalikan status `400 Bad Request`.



\## GraphQL



Selain REST API, project ini juga menyediakan GraphQL yang dapat diakses melalui endpoint:



```text

POST /graphql

```



GraphQL digunakan untuk mengambil data destinasi, wilayah, dan informasi cuaca sesuai field yang diminta. Salah satu contohnya adalah mengambil nama destinasi, nama wilayah, suhu, dan kecepatan angin.



Field `windSpeed` masih dapat digunakan, tetapi sudah ditandai deprecated. Field yang disarankan untuk digunakan selanjutnya adalah `windSpeedKmh`.



\## Autentikasi



Request API menggunakan API key yang dikirim melalui header `x-api-key`. Selain itu, tersedia autentikasi menggunakan username dan password untuk mendapatkan token.



Token digunakan untuk mengakses endpoint tertentu sesuai role akun, yaitu `admin`, `editor`, atau `viewer`. Setiap role memiliki hak akses yang berbeda.



\## Masa Berlaku API v1



API v1 memiliki batas masa penggunaan hingga \*\*30 Juni 2027\*\*. Setelah tanggal tersebut, pengguna diharapkan sudah menggunakan API v2 agar tetap mengikuti versi API yang tersedia.



\## Teknologi yang Digunakan



\- Node.js

\- REST API

\- GraphQL

\- JSON

\- Open-Meteo (data cuaca)

