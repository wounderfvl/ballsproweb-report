# Laporan Progres Mingguan - BALLS (Borneo Anfield Loyalty System)


- **Kelompok**: 9
- **Mitra**: Borneo Anfield Stadium
- **Pekan ke-**: 11 
- **Tanggal**: 23/04/2025


## Progress Summary


Pada minggu ke-11, tim fokus pada authentication dan authorization menggunakan Token Based Authentication (JWT), dan juga pengujian satu fitur pada aplikasi langsung.
Pada laporan ini juga melampirkan progress dari minggu 10 yang tidak tersampaikan seperti Desain ERD, pembuatan kerangka awal backend (REST API skeleton), dan penyiapan struktur frontend dasar.


## Accomplished Tasks


- Merancang skema database sesuai kebutuhan aplikasi
- Mengimplementasikan struktur database di PostgreSQL
- Membuat REST API skeleton dengan endpoint dasar
- Menyiapkan struktur frontend dasar (routing, halaman login/register)
- Melakukan demo progres ke mitra dan mendapatkan masukan awal


## Challenges & Solutions


- **Challenge 1**: Penentuan relasi antar tabel pada skema database cukup kompleks
 - **Solution**: Diskusi tim secara intensif dan konsultasi dengan mitra untuk validasi kebutuhan data
- **Challenge 2**: Integrasi antara backend dan frontend masih belum sepenuhnya berjalan lancar
 - **Solution**: Membuat dokumentasi API yang jelas dan rencana integrasi bertahap untuk minggu berikutnya


## Next Week Plan


- Menyempurnakan struktur database dan menambahkan data dummy
- Mengembangkan endpoint lanjutan untuk fitur utama
- Mulai integrasi backend dengan frontend


## Contributions


- **Alfian Fadhillah P (PM)**:
- **Achmad Bayhaqi (DevOps)**: Dokumentasi API Lengkap, Desain Database (ERD dan Class Diagram) , Integrasi dengan backend dan frontend
- **Dahayu Azhka Daeshawnda (Frontend)**:
- **Khanza Nabilla Tsabita (Backend)**:


---


### Desain ERD
- https://raw.githubusercontent.com/AchmadLyraa/-prowebdevops/refs/heads/main/ArchitectureDesign-Database%20Design%20-%20ERD.jpg


-------


## Implementasi API - User Management


###### Dokumentasi API Lengkap:
https://github.com/AchmadLyraa/-prowebdevops/blob/main/API%20Documentation.md


### Register


**Endpoint**


```plaintext
/auth/register
```


**Method**


```plaintext
POST
```


**Request Body**


- `username` as string, must be unique
- `email` as string, must be unique
- `password` as string, must be at least 8 characters
- `full_name` as string
- `phone_number` as string




**Response**


```json
{
 "error": false,
 "message": "User registered successfully",
 "data": {
   "user_id": "user-123abc",
   "username": "johndoe"
 }
}
```


### Login


**Endpoint**


```plaintext
/auth/login
```


**Method**


```plaintext
POST
```


**Request Body**


- `email` as string
- `password` as string




**Response**


```json
{
 "error": false,
 "message": "Login successful",
 "data": {
   "user_id": "user-123abc",
   "username": "johndoe",
   "full_name": "John Doe",
   "user_type": "customer",
   "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
 }
}
```


### Get User Profile


**Endpoint**


```plaintext
/users/profile
```


**Method**


```plaintext
GET
```


**Headers**


- `Authorization: Bearer <token>`




**Response**


```json
{
 "error": false,
 "message": "Profile retrieved successfully",
 "data": {
   "user_id": "user-123abc",
   "username": "johndoe",
   "email": "john@example.com",
   "full_name": "John Doe",
   "phone_number": "1234567890",
   "user_type": "customer",
   "created_at": "2023-01-01T00:00:00.000Z",
   "is_active": true
 }
}
```


### Update User Profile


**Endpoint**


```plaintext
/users/profile
```


**Method**


```plaintext
PUT
```


**Headers**


- `Authorization: Bearer <token>`




**Request Body**


- `full_name` as string, optional
- `phone_number` as string, optional
- `password` as string, optional, must be at least 8 characters




**Response**


```json
{
 "error": false,
 "message": "Profile updated successfully"
}
```


----


### Wireframe / Mockup


- **Deskripsi**: Desain awal UI aplikasi.
- **Link**:
 - [ProWeb - Mock-up](https://www.figma.com/design/xEy22akByWa9LvHT4CHZ4G/ProWeb---Mock-up?node-id=0-1&t=NBg7COo7gK9H9btJ-1)
 - [Admin BAS - Mock-up](https://www.figma.com/proto/sHIRHBKkCxOVx5wCYpnv7n/Admin-BAS---Mock-Up?node-id=1-2)


----


### GitHub Repository


- **Link Backend**: [balls-backdoor](https://github.com/x3naline/balls-backdoor)
- **Link Frontend**: [balls-frontdoor](https://github.com/wounderfvl/balls-frontdoor)
- **Link DevOps**: [prowebdevops](https://github.com/AchmadLyraa/-prowebdevops)
- **Link Report**: [ballsproweb-report](https://github.com/wounderfvl/ballsproweb-report)








