# Laporan Progres Mingguan - BALLS (Borneo Anfield Loyalty System)


- **Kelompok**: 9
- **Mitra**: Borneo Anfield Stadium
- **Pekan ke-**: 11 
- **Tanggal**: 23/04/2025


## Progress Summary


Pada minggu ke-11, tim fokus pada authentication dan authorization menggunakan Token Based Authentication (JWT), dan juga pengujian satu fitur pada aplikasi langsung.
Pada laporan ini juga melampirkan progress dari minggu 10 yang tidak tersampaikan seperti Desain ERD, pembuatan kerangka awal backend (REST API skeleton), dan penyiapan struktur frontend dasar.

Berikut beberapa pencapaian untuk di minggu ini:
1. **Authentication System**
    Dalam autentikasi disini kami mengimplementasikan 3 level user yaitu Super Admin, Admin. dan customer. Kemudian kami juga telah membuat sistem login yang terpisah untuk masing-masing level user tersebut.

2. **Booking Lapangan**
    Sesuai dengan salah satu kebutuhan mitra yaitu pemesananan lapangan berbasis website, di minggu ini kami mengimplementasikan fitur booking lapangan.


## Accomplished Tasks

1. **Frontend Development**
  - Menyiapkan struktur frontend dasar (routing, halaman login/register)
  - Halaman Login dan register
  - Integrasi API

2. **Backend Development**
  - Mengimplementasikan struktur database di PostgreSQL
  - Setup struktur project backend dengan arsitektur modular (controllers, models, routes)
  - Implementasi sistem autentikasi berbasis JWT untuk user dan admin
  - Perancangan dan integrasi database PostgreSQL (tabel: users, fields, bookings, payments, dll)
  - Pengembangan endpoint booking lapangan dengan validasi ketersediaan waktu
  - Pengelolaan error dan validasi input menggunakan middleware custom

3. **Database & API**
  - Merancang skema database sesuai kebutuhan aplikasi
  - Membuat REST API skeleton dengan endpoint dasar
  - Melakukan demo progres ke mitra dan mendapatkan masukan awal


## Challenges & Solutions

1. **Authentication System**
- **Challenge**: Penentuan relasi antar tabel pada skema database cukup kompleks
 - **Solution**: Diskusi tim secara intensif dan konsultasi dengan mitra untuk validasi kebutuhan data
- **Challenge**: Integrasi antara backend dan frontend masih belum sepenuhnya berjalan lancar
 - **Solution**: Membuat dokumentasi API yang jelas dan rencana integrasi bertahap untuk minggu berikutnya


## Next Week Plan

- Core Feature #2 & #3: Fitur utama kedua dan ketiga
- UI Enhancement: Perbaikan tampilan dan UX
- Menyempurnakan struktur database dan menambahkan data dummy
- Mengembangkan endpoint lanjutan untuk fitur utama


## Contributions


- **Alfian Fadhillah P (PM)**: Menyempurnakan desain UI/UX, Membuat laporan MD
- **Achmad Bayhaqi (DevOps)**: Dokumentasi API Lengkap, Desain Database (ERD dan Class Diagram) , Integrasi dengan backend dan frontend
- **Dahayu Azhka Daeshawnda (Frontend)**: Frontend development (React components) & State management 
- **Khanza Nabilla Tsabita (Backend)**: Backend architecture, Resource implementation, dan Authentication system


---

### 
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
## Screenshots
## 1. Sistem Autentikasi

### Login (3 Level user)
https://raw.githubusercontent.com/wounderfvl/ballsproweb-report/refs/heads/main/week%2011/WhatsApp%20Image%202025-04-25%20at%2015.04.26.jpeg

### Register
https://raw.githubusercontent.com/wounderfvl/ballsproweb-report/refs/heads/main/week%2011/WhatsApp%20Image%202025-04-25%20at%2015.02.51.jpeg

### Register (Super admin)
https://raw.githubusercontent.com/wounderfvl/ballsproweb-report/refs/heads/main/week%2011/WhatsApp%20Image%202025-04-25%20at%2015.29.29.jpeg


## 2. Core Feature #1

### Create Booking
https://raw.githubusercontent.com/wounderfvl/ballsproweb-report/refs/heads/main/week%2011/WhatsApp%20Image%202025-04-25%20at%2015.21.19.jpeg

#### Form booking

https://raw.githubusercontent.com/wounderfvl/ballsproweb-report/refs/heads/main/week%2011/skidipadapudu.jpeg

```tsx
"use client";

import { useState } from "react";

export default function BookingPage() {
  const [selectedField, setSelectedField] = useState("");
  const [date, setDate] = useState("");
  const [time, setTime] = useState("");
  const [duration, setDuration] = useState(1);

  const fields = [
    { id: 1, name: "Field A" },
    { id: 2, name: "Field B" },
  ];

  const handleSubmit = (e: React.FormEvent) => {
    e.preventDefault();
    alert(
      Booking submitted for Field ${selectedField} on ${date} at ${time} for ${duration} hour(s)
    );
  };

  return (
    <div className="booking-container">
      <h1>Book a Field</h1>
      <form onSubmit={handleSubmit} className="booking-form">
        <div className="form-group">
          <label>Select Field:</label>
          <select
            value={selectedField}
            onChange={(e) => setSelectedField(e.target.value)}
            required
          >
            <option value="">-- Select a field --</option>
            {fields.map((field) => (
              <option key={field.id} value={field.id}>
                {field.name}
              </option>
            ))}
          </select>
        </div>

        <div className="form-group">
          <label>Date:</label>
          <input
            type="date"
            value={date}
            onChange={(e) => setDate(e.target.value)}
            required
          />
        </div>

        <div className="form-group">
          <label>Time:</label>
          <input
            type="time"
            value={time}
            onChange={(e) => setTime(e.target.value)}
            required
          />
        </div>

        <div className="form-group">
          <label>Duration (hours):</label>
          <input
            type="number"
            min="1"
            max="3"
            value={duration}
            onChange={(e) => setDuration(Number(e.target.value))}
            required
          />
        </div>

        <button type="submit" className="submit-button">
          Confirm Booking
        </button>
      </form>
    </div>
  );
}
```

## Screenshots Tampilan Login & Register

https://raw.githubusercontent.com/wounderfvl/ballsproweb-report/refs/heads/main/week%2011/WhatsApp%20Image%202025-04-25%20at%2016.13.09.jpeg

https://raw.githubusercontent.com/wounderfvl/ballsproweb-report/refs/heads/main/week%2011/WhatsApp%20Image%202025-04-25%20at%2016.13.09%20(2).jpeg

https://raw.githubusercontent.com/wounderfvl/ballsproweb-report/refs/heads/main/week%2011/WhatsApp%20Image%202025-04-25%20at%2016.13.09%20(1).jpeg

## 3. Integration Test


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




