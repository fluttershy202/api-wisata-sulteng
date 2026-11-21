
# API Wisata Sulawesi Tengah

Project ini merupakan API untuk data destinasi wisata di Sulawesi Tengah. Project ini digunakan untuk mengelola dan menampilkan informasi destinasi wisata, wilayah, serta informasi cuaca. API memiliki versi 1 dan versi 2, autentikasi API key, token berdasarkan role, dan GraphQL.

## Cara Menjalankan Project

### 1. Clone Repository

Clone repository menggunakan perintah:

```bash
git clone https://github.com/fluttershy202/api-wisata-sulteng.git
```

Masuk ke folder project:

```bash
cd api-wisata-sulteng
```

### 2. Instal Dependensi

Jalankan perintah berikut:

```bash
npm install
```

### 3. Membuat File Konfigurasi

Buat file `.env` di folder utama project, lalu isi dengan:

```env
TOKEN_SECRET=secret_acak_milik_sendiri
```

TOKEN_SECRET digunakan untuk pembuatan dan pemeriksaan token. Gunakan string acak yang kuat dan jangan membagikannya.

### 4. Menyiapkan File Data

File berikut perlu dibuat sendiri karena tidak disertakan dalam repository:

- `data/users.json` untuk data akun.
- `data/api-keys.json` untuk data API key.

File `destinations.json` dan `regions.json` sudah tersedia di repository.

Untuk membuat akun, gunakan file `buat-user.js`. Contoh pembuatan akun admin:

```bash
node buat-user.js admin password123 admin
```

Role yang tersedia adalah `admin`, `editor`, dan `viewer`. Username dan password pada contoh tersebut hanya contoh, bukan akun bawaan.

### 5. Menjalankan Server

Jalankan server menggunakan perintah:

```bash
node --env-file=.env server.js
```

API dapat diakses melalui:

```text
http://localhost:3000
```

Request API dapat diuji menggunakan Postman dengan menyertakan API key.

## Versi API yang Tersedia

### API v1

API v1 menggunakan awalan `/v1` dan format data versi lama.

Contoh endpoint:

- `GET /v1/destinations`
- `GET /v1/destinations/1`

### API v2

API v2 menggunakan awalan `/v2` dan format data terbaru. Versi ini menyediakan endpoint destinasi dan wilayah.

Contoh endpoint:

- `GET /v2/destinations`
- `GET /v2/destinations/1`
- `GET /v2/regions`

Destinasi dapat difilter berdasarkan wilayah menggunakan parameter `regionId`.

Contoh:

```text
GET /v2/destinations?regionId=3
```

Request tersebut menampilkan destinasi yang memiliki `regionId` bernilai 3.

### Header Versioning

Versi API juga dapat ditentukan menggunakan header `x-api-version`, tanpa awalan versi pada URL.

Contoh:

```http
GET /destinations/1
x-api-version: 1
```

Untuk menggunakan versi 2, ubah nilai header menjadi `2`. Jika versi tidak ditentukan melalui URL maupun header, server akan mengembalikan status `400 Bad Request`.

## GraphQL

GraphQL tersedia melalui endpoint:

```text
POST /graphql
```

GraphQL digunakan untuk mengambil data destinasi, wilayah, dan cuaca sesuai field yang diminta, seperti nama destinasi, nama wilayah, suhu, dan kecepatan angin.

Field `windSpeed` masih dapat digunakan, tetapi sudah deprecated. Field penggantinya adalah `windSpeedKmh`.

## Autentikasi

Request API menggunakan API key melalui header `x-api-key`. Autentikasi username dan password juga tersedia untuk mendapatkan token.

Token digunakan untuk mengakses endpoint tertentu sesuai role akun, yaitu `admin`, `editor`, dan `viewer`. Setiap role memiliki hak akses yang berbeda.

## Masa Berlaku API v1

API v1 berlaku hingga **30 Juni 2027**. Setelah tanggal tersebut, pengguna diharapkan menggunakan API v2.

## Teknologi yang Digunakan

- Node.js
- REST API
- GraphQL
- JSON
- Open-Meteo (data cuaca)
