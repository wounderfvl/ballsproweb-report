# Laporan Progres Mingguan - BALLS (Borneo Anfield Loyalty System)


- **Kelompok**: 9
- **Mitra**: Borneo Anfield Stadium
- **Pekan ke-**: 13
- **Tanggal**: 09/05/2025

---
## Anggota Kelompok

- **Alfian Fadhillah Putra (10231009) (PM)**
- **Achmad Bayhaqi (10231009) (DevOps)**
- **Dahayu Azhka Daeshawnda (10231009) (Frontend)** 
- **Khanza Nabilla Tsabita (10231009) (Backend)**

---

## Progress Summary
Pada minggu ini, tim frontend telah fokus mengembangkan dan menyelesaikan menu utama pada role admin termasuk dashboard terkait sistem loyalty dan manajemen booking. Fitur-fitur baru meliputi tampilan dashboard admin, manajemen program loyalty untuk admin, serta menyelesaikan core featur#4 halaman loyalty pengguna. Dan dari backend, backend sudah mengimplementasikan  fitur baru seperti manajemen akun admin oleh super admin dan laporan statistik booking & loyalty. Database, dan struktur folder backend dengan arsitektur modular (routes, controllers, models) sudah di setup. Pencapaian utama minggu ini meliputi:

### Laporan Statistik & Analitik
Kami telah mengimplementasikan fitur laporan booking dan program loyalty yang dapat diakses oleh admin dan super admin. Laporan mencakup filter tanggal dan lapangan, jumlah pemesanan, pendapatan, serta kinerja program loyalti. Selain itu, super admin juga dapat melihat ringkasan statistik sistem seperti pertumbuhan pengguna, performa lapangan, dan program loyalti secara keseluruhan.

### Admin Panel
Fitur dashboard untuk admin dan super admin telah dibuat untuk memudahkan pengelolaan data seperti booking, program loyalti, serta manajemen lapangan. Admin dapat melakukan approval, penjadwalan ulang, atau membatalkan booking melalui panel ini. Super admin juga dapat mengelola akun admin lain melalui fitur CRUD manajemen user.

### Visualisasi Data
Untuk mendukung pemantauan data secara interaktif, kami menambahkan visualisasi data dalam bentuk grafik tren booking (harian, mingguan, bulanan), distribusi penukaran poin program loyalti. Hal ini memudahkan admin dan super admin dalam membaca performa sistem secara keseluruhan.

## Accomplished Tasks
1. **Backend Development (Next.js)**
- Mengimplementasikan struktur database terupdate di PostgreSQL
- Setup struktur project backend dengan arsitektur modular (controllers, models, routes)
- Implementasi sistem autentikasi berbasis JWT untuk user, admin dan super admin
- Pengembangan beberapa endpoint terbaru terkait reports(booking dan loyalty program) dan CRUD admin oleh super admin (GET /admin/reports/bookings, GET /super-admin/reports/bookings, GET /admin/reports/loyalty, GET /super-admin/reports/loyalty, GET /super-admin/statistics, POST & GET /super-admin/admins, PUT & DELETE /super-admin/admins/:user_id)

2. **Frontend Development (React)**
- Pengembangan *Pengguna Loyalty* yang menampilkan poin loyalty, daftar reward, dan QR code untuk penukaran poin
- Pembuatan *Admin Dashboard* untuk mengelola booking, dengan tabel dan form input booking yang responsif
- Implementasi *Admin Loyalty* untuk pengelolaan reward dan poin pengguna dengan tampilan tab dan tabel data

3. **Database & API**
- Merancang dan migrasi database PostgreSQL (balls)

4. **Project Manager + UI/UX**
- Mengkomunikasikan hasil diskusi terbaru dengan mitra dan menentukan alur dari website
- Menyelesaikan desain UI sesuai dengan kebutuhan mitra (User needs) dan untuk panduan tim Front End dalam mengimplementasikan websitenya

## Challenges and Solutions
- *Challenge 1*: Menyusun tampilan yang berbeda untuk admin dan pengguna dalam satu sistem  
  *Solution*: Mendesain layout modular dan reusable agar bisa digunakan kembali untuk berbagai peran pengguna

- *Challenge 2*: Menampilkan data loyalty dan reward dengan cara yang mudah dipahami pengguna  
  *Solution*: Menggunakan komponen visual seperti tabel, tab untuk meningkatkan keterbacaan dan interaksi

- *Challenge 3*: Menambahkan role Super Admin ke dalam sistem autentikasi yang sebelumnya hanya memiliki Admin dan Pelanggan  
  *Solution*: Sistem autentikasi diperluas dengan penambahan tipe role Super Admin. Middleware otorisasi dibuat agar hanya Super Admin yang dapat mengakses endpoint tertentu seperti manajemen akun admin.

- *Challenge 4*: Membuat laporan yang dapat diakses oleh dua user (Admin & Super Admin)  
  *Solution*: Menggunakan endpoint paralel untuk masing-masing peran (/admin/reports/ dan /super-admin/reports/) dengan kontrol otorisasi berdasarkan peran user melalui middleware

## Next Week Plan
- Membuat menu manajemen transaksi
- Membuat data visualization: Chart/grafik sederhana untuk data pemain dan keuangan
- Bugfix report: Menganalisis bug (jika ada) dan menemukan solusinya
- Merencanakan deployment(hosting, domain, dan lain-lain)

## Unit Testing
- ### *Manajemen Admin*

### Create Admin

**Endpoint**
```plaintext
/super-admin/admins
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
 "message": "Admin account created successfully",
 "data": {
    "user_id": "user-456def",
    "username": "admin1"
 }
}
```

### Get All Admin

**Endpoint**
```plaintext
/super-admin/admins
```

**Method**

```plaintext
GET
```

**Response**

```json
{
    "error": false,
    "message": "Admin accounts retrieved successfully",
    "data": [
        {
            "user_id": "user-456def",
            "username": "admin1",
            "email": "admin1@example.com",
            "full_name": "Admin One",
            "is_active": true,
            "created_at": "2023-01-01T00:00:00.000Z"
        }
    ]
}
```

### Update Admin

**Endpoint**
```plaintext
/super-admin/admins/:user_id
```

**Method**

```plaintext
PUT
```

**Request Body**

- `full_name` as string, optional
- `phone_number` as string, optional
- `is_active` as boolean, optional
- `password` as string, must be at least 8 characters


**Response**

```json
{
 "error": false,
 "message": "Admin account updated successfully"
}
```

### Delete Admin

**Endpoint**
```plaintext
/super-admin/admins/:user_id
```

**Method**

```plaintext
DELETE
```

**Response**

```json
{
 "error": false,
 "message": "Admin account deleted successfully"
}
```

- ### *Laporan statistk*

### Laporan Booking

**Endpoint**
```plaintext
/admin/reports/bookings
/super-admin/reports/bookings
```

**Method**

```plaintext
GET
```

**Parameters**

- `from_date` as string (YYYY-MM-DD format)
- `to_date` as string (YYYY-MM-DD format)
- `field_id` as string, optional
- `format`  as string, optional (json, csv, pdf, default: json)

**Response**

```json
{
    "error": false,
    "message": "Booking report generated successfully",
    "data": {
        "period": {
            "from_date": "2023-06-01",
            "to_date": "2023-06-30"
        },
        "total_bookings": 45,
        "completed_bookings": 40,
        "cancelled_bookings": 5,
        "total_revenue": 6750000,
        "fields_usage": [
            {
            "field_id": "field-123abc",
            "field_name": "Field A",
            "bookings_count": 25,
            "total_hours": 50,
            "revenue": 3750000
            }
        ],
        "daily_bookings": [
            {
            "date": "2023-06-01",
            "bookings_count": 3,
            "revenue": 450000
            }
        ]
    }
}
```

### Laporan Loyalty Program

**Endpoint**
```plaintext
/admin/reports/loyalty
/super-admin/reports/loyalty
```

**Method**

```plaintext
GET
```

**Parameters**

- `from_date` as string (YYYY-MM-DD format)
- `to_date` as string (YYYY-MM-DD format)
- `format`  as string, optional (json, csv, pdf, default: json)

**Response**

```json
{
    "error": false,
    "message": "Loyalty program report generated successfully",
    "data": {
        "period": {
        "from_date": "2023-06-01",
        "to_date": "2023-06-30"
        },
    "total_points_issued": 4500,
    "total_points_redeemed": 1200,
    "active_users": 35,
    "programs_usage": [
        {
        "program_id": "program-123abc",
        "program_name": "Free 1-Hour Booking",
        "redemptions_count": 12,
        "points_used": 1200
        }
    ],
    "top_users": [
    {
    "user_id": "user-123abc",
    "full_name": "John Doe",
    "points_earned": 150,
    "points_redeemed": 100
    }
   ]
 }
}
```
 

## Contributions
**Alfian Fadhillah P (Project Manager)**: 
- Menyempurnakan dan melengkapi desain UI/UX untuk fitur-fitur;
- Component styling;
- Menemui stakeholder untuk mendiskusikan terkait progress
- Membuat laporan MD.

**Achmad Bayhaqi (DevOps)**:
- Dokumentasi API,
- Integrasi dengan backend dan frontend,
- Membuat laporan MD.

**Dahayu Azhka Daeshawnda (Frontend)**:
- Pembuatan UI Admin Dashboard, Admin Loyalty, dan Pengguna Loyalty

**Khanza Nabilla Tsabita (Backend)**:
- Pengembangan fitur reports(booking dan loyalty program) dan CRUD admin oleh super admin,
- Integrasi database PostgreSQL (setup koneksi dan migrasi awal untuk payment dan program loyalty),
- Implementasi endpoint laporan booking & loyalty untuk admin dan super admin,
- Membuat laporan MD.

## 1. Screenshots / Demo Core Feature

### Dashboard manajemen pemesanan Lapangan
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/Week%2013/Dashboard%20manajemen%20pemesanan%20Lapangan.jpeg">

### Tampilan create dalam manajemen pemesanan lapangan
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/Week%2013/Tampilan%20create%20dalam%20manajemen%20pemesanan%20lapangan.jpeg">

### Loyalty Management (Manajemen menu hadiah)
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/Week%2013/Loyalty%20Management%20(Manajemen%20menu%20hadiah).jpeg">

### Loyalty Management (Manajemen loyalty points)
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/Week%2013/Loyalty%20Management%20(Manajemen%20loyalty%20points).jpeg">

## 2. Core Feature
### Laporan statistik

- #### Booking

```js
///reportController.js
async generateBookingReport(req, res, next) {
    try {
    const { from_date, to_date, field_id, format = "json" } = req.query

    if (!from_date || !to_date) {
        return res.status(400).json(responseFormatter.error("From date and to date are required", "VALIDATION_ERROR"))
    }

    // Generate report
    const report = await bookingModel.generateReport({
        from_date,
        to_date,
        field_id,
    })

    // Handle different formats
    if (format === "json") {
        return res.status(200).json(responseFormatter.success("Booking report generated successfully", report))
    } else if (format === "csv") {
        // Implementation for CSV format would go here
        return res.status(501).json(responseFormatter.error("CSV format not implemented yet", "NOT_IMPLEMENTED"))
    } else if (format === "pdf") {
        // Implementation for PDF format would go here
        return res.status(501).json(responseFormatter.error("PDF format not implemented yet", "NOT_IMPLEMENTED"))
    } else {
        return res.status(400).json(responseFormatter.error("Invalid format parameter", "VALIDATION_ERROR"))
    }
    } catch (error) {
    next(error)
    }
}
```

- #### Loyalty

```js
///reportController.js
async generateLoyaltyReport(req, res, next) {
    try {
    const { from_date, to_date, format = "json" } = req.query

    if (!from_date || !to_date) {
        return res.status(400).json(responseFormatter.error("From date and to date are required", "VALIDATION_ERROR"))
    }

    // Generate report
    const report = await loyaltyModel.generateReport({
        from_date,
        to_date,
    })

    // Handle different formats
    if (format === "json") {
        return res.status(200).json(responseFormatter.success("Loyalty program report generated successfully", report))
    } else if (format === "csv") {
        // Implementation for CSV format would go here
        return res.status(501).json(responseFormatter.error("CSV format not implemented yet", "NOT_IMPLEMENTED"))
    } else if (format === "pdf") {
        // Implementation for PDF format would go here
        return res.status(501).json(responseFormatter.error("PDF format not implemented yet", "NOT_IMPLEMENTED"))
    } else {
        return res.status(400).json(responseFormatter.error("Invalid format parameter", "VALIDATION_ERROR"))
    }
    } catch (error) {
    next(error)
    }
}
```

#### Frontend Implementation


### API Implementation

### Create Admin
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/Week%2013/Create%20Admin.jpeg">

### Read Admin
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/Week%2013/Get%20All%20Admins.jpeg">

### Update Admin
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/Week%2013/Update%20Admin.jpeg">

### Delete Admin
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/Week%2013/Delete%20Admin.jpeg">

### Booking Reports
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/Week%2013/bookings%20report.jpeg">

### Loyalty Reports
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/Week%2013/loyalty%20programs%20reports.jpeg">

### revenue Reports
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/Week%2013/revenue%20reports.jpeg">


#### Features Implemented
1. Integrasi ?? - Frontend dengan Backend


2. Integrasi ?? - Frontend dengan Backend


3. Integrasi ?? - Frontend dengan Backend



### 3. Frontend-Backend Integration
#### Menu Display Integration


### 3.3 Database Integration Testing
```ts
// src/services/api/config.ts
export const API_BASE_URL = 'https://localhost:3000';

// Default headers for API requests
export const getDefaultHeaders = (token?: string) => {
  const headers: Record<string, string> = {
    'Content-Type': 'application/json',
  };

  if (token) {
    headers['Authorization'] = `Bearer ${token}`;
  }

  return headers;
};

// API request wrapper with error handling
export async function apiRequest<T>(
  endpoint: string,
  options: RequestInit = {}
): Promise<T> {
  try {
    const response = await fetch(`${API_BASE_URL}${endpoint}`, options);
    
    if (!response.ok) {
      // Try to get error details from response if available
      let errorData;
      try {
        errorData = await response.json();
      } catch (e) {
        // If response is not JSON, use status text
        throw new Error(`API Error: ${response.status} ${response.statusText}`);
      }
      
      throw new Error(
        errorData.message || `API Error: ${response.status} ${response.statusText}`
      );
    }

    return await response.json() as T;
  } catch (error) {
    console.error('API request failed:', error);
    throw error;
  }
}
```

### 3.4 




----
### Mockup

- **Deskripsi**: Desain UI Website.
- **Link**:
 - [ProWeb - Mock-up](https://www.figma.com/design/xEy22akByWa9LvHT4CHZ4G/ProWeb---Mock-up?node-id=0-1&t=NBg7COo7gK9H9btJ-1)
 - [Admin BAS - Mock-up](https://www.figma.com/proto/sHIRHBKkCxOVx5wCYpnv7n/Admin-BAS---Mock-Up?node-id=1-2)

----

### GitHub Repository

- **Link Backend**: [balls-backdoor](https://github.com/x3naline/balls-backdoor)
- **Link Frontend**: [balls-frontdoor](https://github.com/wounderfvl/balls-frontdoor)
- **Link DevOps**: [prowebdevops](https://github.com/AchmadLyraa/-prowebdevops)
- **Link Report**: [ballsproweb-report](https://github.com/wounderfvl/ballsproweb-report)
