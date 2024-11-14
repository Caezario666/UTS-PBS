# Aplikasi Manajemen Inventaris

Aplikasi Manajemen Inventaris ini dirancang untuk membantu dalam pengelolaan barang dalam suatu sistem inventaris. Aplikasi ini menyediakan fitur seperti manajemen item (barang), kategori, pemasok, serta ringkasan stok barang. Dengan menggunakan teknologi Express.js, Prisma ORM, dan PostgreSQL, aplikasi ini dapat berjalan dengan mudah dalam lingkungan Docker.

## Fitur Aplikasi
- **Manajemen Barang (CRUD)**: Tambah, ubah, hapus, dan lihat data barang.
- **Manajemen Kategori**: Menambahkan kategori barang dan melihat daftar kategori.
- **Manajemen Pemasok**: Menambahkan pemasok dan melihat daftar pemasok.
- **Ringkasan Stok Barang**: Melihat total stok, total nilai stok, dan rata-rata harga barang.
- **Filter Stok**: Menampilkan barang dengan stok di bawah ambang batas yang ditentukan.
- **Laporan Kategori**: Melihat laporan barang berdasarkan kategori.
- **Laporan Pemasok**: Melihat laporan barang berdasarkan pemasok.
- **Autentikasi Admin**: Pendaftaran dan login menggunakan JWT untuk autentikasi.

## Teknologi yang Digunakan
- **Backend Framework**: Express.js
- **ORM**: Prisma
- **Database**: PostgreSQL
- **Containerization**: Docker Compose
- **Autentikasi**: JWT (JSON Web Token)

### Persiapan dan Instalasi
1. **Clone repository**:
   ```bash
   git clone <repository-url>
   cd <repository-folder>
   ```
2. **Setup Docker Compose**:
   Jalankan perintah berikut untuk menjalankan aplikasi dengan Docker Compose:
   ```bash
   docker-compose up --build
   ```
3. **Environment Variables**:
   Pastikan file `.env` sudah diisi dengan konfigurasi berikut:
   ```
   DATABASE_URL=postgresql://<username>:<password>@<host>:<port>/<database>
   JWT_SECRET=<your_jwt_secret>
   ```

### Urutan Flow Aplikasi dari Login
1. **User mengakses halaman login**.
2. **User mengisi form login** dengan `username` dan `password`.
3. **Request dikirim ke endpoint login**:
   - **Path**: `POST /auth/login`
   ```http
   POST http://localhost:3001/auth/login
   Content-Type: application/json

   {
     "username": "user",
     "password": "securePassword123",
     "email": "user@example.com"
   }
   ```
4. **Server memproses permintaan** dan memvalidasi kredensial.
5. **Jika valid**, server mengembalikan token JWT sebagai respons.
6. **User menyimpan token JWT** untuk digunakan dalam permintaan API selanjutnya.

### Endpoint dan Contoh Request
Berikut adalah daftar endpoint API beserta contoh request menggunakan format HTTP:

#### 1. Membuat Item Baru
**Path**: `POST /api/items`
```http
POST http://localhost:3001/api/items
Content-Type: application/json
Authorization: Bearer <token>

{
  "name": "Nike Air Jordan",
  "description": "Sepatu basket yang dipakai pleh Michael Jordan",
  "price": 15000000.00,
  "quantity": 10,
  "categoryId": 1,
  "supplierId": 1,
  "createdBy": 1
}
```

#### 2. Mendapatkan Semua Item
**Path**: `GET /api/items`
```http
GET http://localhost:3001/api/items
Authorization: Bearer <token>
```

#### 3. Menampilkan Ringkasan Stok Barang
**Path**: `GET /api/items/summary`
```http
GET http://localhost:3001/api/items/summary
Authorization: Bearer <token>
```

#### 4. Menampilkan Barang dengan Stok di Bawah Ambang Batas
**Path**: `GET /api/items/low-stock`
- **Parameter query**: `condition` (lessThan, equalTo, greaterThan), `threshold` (default: 5)
```http
GET http://localhost:3001/api/items/low-stock?condition=lessThan&threshold=5
Authorization: Bearer <token>
```

#### 5. Menampilkan Barang Berdasarkan Kategori
**Path**: `GET /api/items/category/:categoryId`
```http
GET http://localhost:3001/api/items/category/1
Authorization: Bearer <token>
```

#### 6. Menampilkan Ringkasan Per Kategori
**Path**: `GET /api/items/category-summary`
```http
GET http://localhost:3001/api/items/category-summary
Authorization: Bearer <token>
```

#### 7. Menampilkan Ringkasan Barang Berdasarkan Pemasok
**Path**: `GET /api/items/supplier-summary`
```http
GET http://localhost:3001/api/items/supplier-summary
Authorization: Bearer <token>
```

#### 8. Membuat Akun Admin Baru
**Path**: `POST /auth/register`
```http
POST http://localhost:3001/auth/register
Content-Type: application/json

{
  "username": "user",
  "password": "securePassword123",
  "email": "user@example.com"
}
```

#### 9. Login Admin
**Path**: `POST /auth/login`
```http
POST http://localhost:3001/auth/login
Content-Type: application/json

{
  "username": "user",
  "password": "securePassword123",
  "email": "user@example.com"
}
```

### Penjelasan Singkat Fitur Aplikasi
- **Manajemen Barang**: CRUD item dengan validasi data.
- **Ringkasan Stok**: Melihat total stok, nilai stok, dan rata-rata harga.
- **Filter Stok**: Melihat barang dengan stok kurang dari, sama dengan, atau lebih dari ambang batas tertentu.
- **Kategori dan Pemasok**: Menampilkan barang berdasarkan kategori dan pemasok, serta ringkasannya.
- **Autentikasi**: Sistem login dan pendaftaran menggunakan JWT.

Pastikan API berjalan di port `3001` seperti yang disetel dalam Docker Compose, atau sesuaikan dengan konfigurasi Anda.

