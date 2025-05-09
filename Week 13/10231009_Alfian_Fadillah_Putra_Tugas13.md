# Laporan Progres Mingguan - BALLS (Borneo Anfield Loyalty System)


- **Kelompok**: 9
- **Mitra**: Borneo Anfield Stadium
- **Pekan ke-**: 12
- **Tanggal**: 01/05/2025

---
## Anggota Kelompok

- **Alfian Fadhillah Putra (10231009) (PM)**
- **Achmad Bayhaqi (10231009) (DevOps)**
- **Dahayu Azhka Daeshawnda (10231009) (Frontend)** 
- **Khanza Nabilla Tsabita (10231009) (Backend)**

---

## Progress Summary
Minggu ini tim telah berhasil mengimplementasikan beberapa sistem manajemen dashboard admin. Tim frontend telah fokus mengembangkan dan menyelesaikan menu utama pada role admin termasuk dashboard terkait sistem loyalty dan manajemen booking. Fitur-fitur baru meliputi tampilan dashboard admin, manajemen program loyalty untuk admin, serta menyelesaikan core featur#4 halaman loyalty pengguna. Pencapaian utama frontend meliputi:

- Pembuatan *Admin Dashboard* untuk mengelola booking, dengan tabel dan form input booking yang responsif
- Implementasi *Admin Loyalty* untuk pengelolaan reward dan poin pengguna dengan tampilan tab dan tabel data

1. **Admin Dashboard**:
- Menambahkan data pemesanan pelanggan secara manual
- *Action* untuk status pembayaran lapangan
- UI berubah secara dinamis berdasarkan langkah saat ini.

2. **Loyalty Management**:
- Managemen menu hadiah untuk ditukarkan oleh customer
- Menambah data pasca pelanggan mukarkan point (daftar reward)

3. **Admin Loyalty**:
- Implementasi *Admin Loyalty* untuk pengelolaan reward dan poin pengguna dengan tampilan tab dan tabel data

## Accomplished Tasks
1. **Backend Development (Next.js)**
- telah menyelesaikan seluruh struktur fitur backend

2. **Frontend Development (React)**
- Menambahkan tampilan tabel dinamis untuk Data Pemesanan Lapangan, termasuk kolom informasi seperti nomor telepon, lapangan, pelanggan, tanggal, jumlah pembayaran, metode pembayaran, status, dan aksi edit/hapus.
- Menambahkan form input dinamis untuk membuat pemesanan baru dengan validasi dasar (nomor telepon, nama pelanggan, tanggal, jumlah, metode pembayaran, status).
- Membuat tampilan manajemen loyalti dengan sistem kartu hadiah (rewards & gifts), termasuk fitur tambah, edit, dan hapus hadiah.
- Implementasi daftar transaksi loyalti, dengan kolom produk, pelanggan, tanggal, jumlah stempel ditukar, sisa stempel, dan status, serta tombol aksi edit/hapus.

3. **Database & API**
- 

4. **Project Manager + UI/UX**
- Mengkomunikasikan hasil diskusi terbaru dengan mitra dan menentukan alur dari website
- Menyelesaikan desain UI sesuai dengan kebutuhan mitra (User needs) dan untuk panduan tim Front End dalam mengimplementasikan websitenya

## Challenges and Solutions
- *Challenge 1*: Menyusun tampilan yang berbeda untuk admin dan pengguna dalam satu sistem  
  *Solution*: Mendesain layout modular dan reusable agar bisa digunakan kembali untuk berbagai peran pengguna

- *Challenge 2*: Menampilkan data loyalty dan reward dengan cara yang mudah dipahami pengguna  
  *Solution*: Menggunakan komponen visual seperti tabel, tab untuk meningkatkan keterbacaan dan interaksi

## Next Week Plan
### Next Week Plan
- Membuat menu manajemen transaksi
- Membuat data visualization: Chart/grafik sederhana untuk data pemain dan keuangan
- Bugfix report: Menganalisis bug (jika ada) dan menemukan solusinya
- Merencanakan deployment(hosting, domain, dan lain-lain)

4. **Unit Testing**

   - Test Case


## Contributions
**Alfian Fadhillah P (Project Manager)**: 
- Menyempurnakan dan melengkapi desain UI/UX untuk fitur-fitur;
- Component styling;
- Menemui stakeholder untuk mendiskusikan terkait progress dan permintaan baru stakeholder;
- Membuat laporan MD.

**Achmad Bayhaqi (DevOps)**:
- Merancang dan migrasi database PostgreSQL (balls);
- Membuat tabel: payment_methods, loyalty_programs, loyalty_points, redemptions, dll;
- Dokumentasi API;
- Integrasi dengan backend dan frontend.

**Dahayu Azhka Daeshawnda (Frontend)**:
- Frontend development (React components) & State management;
- Booking system, autentikasi, dashboard, dan fitur tambah pemain (FE).

**Khanza Nabilla Tsabita (Backend)**:
- Pengembangan fitur booking lapangan dengan validasi ketersediaan,
 - Integrasi database PostgreSQL (setup koneksi dan migrasi awal untuk payment dan program loyalty),
 - Implementasi endpoint payment dan loyalty (read & redeem points, admin program).

## Screenshots / Demo Core Feature

### 
<img src="">



### 
>



### 




### 



---

## 2. Core Feature
### Fitur Customer page


#### 


### Choose a schedule
    ```json
        export default function SchedulePage() {
    // Mock schedule data
    const schedule = {
        fieldA: [
        { time: "9:00 AM", available: false },
        { time: "11:00 AM", available: true },
        { time: "1:00 PM", available: true },
        { time: "3:00 PM", available: false },
        { time: "5:00 PM", available: true },
        ],
        fieldB: [
        { time: "9:00 AM", available: true },
        { time: "11:00 AM", available: false },
        { time: "1:00 PM", available: true },
        { time: "3:00 PM", available: true },
        { time: "5:00 PM", available: false },
        ],
    };

    return (
        <div className="schedule-container">
        <h1>Field Availability</h1>

        <div className="field-schedules">
            <div className="field-schedule">
            <h2>Field A</h2>
            <div className="time-slots">
                {schedule.fieldA.map((slot, index) => (
                <div
                    key={index}
                    className={`time-slot ${
                    slot.available ? "available" : "booked"
                    }`}
                >
                    {slot.time} - {slot.available ? "Available" : "Booked"}
                </div>
                ))}
            </div>
            </div>

            <div className="field-schedule">
            <h2>Field B</h2>
            <div className="time-slots">
                {schedule.fieldB.map((slot, index) => (
                <div
                    key={index}
                    className={`time-slot ${
                    slot.available ? "available" : "booked"
                    }`}
                >
                    {slot.time} - {slot.available ? "Available" : "Booked"}
                </div>
                ))}
            </div>
            </div>
        </div>
        </div>
    );
    }
    ```

#### Frontend Implementation


### API Implementation

**payment**
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/payment.jpeg">

**Redeem**
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/reedem%20point.jpeg">

**verivikasi**
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/verivikasi.jpeg">

**Delete Loyalty Program (Admin Only)**
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/Delete%20Loyalty%20Program%20(Admin%20Only).jpeg">

**Get User Points**
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/Get%20User%20Points.jpeg">

**Get Redemption History**
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/Get%20Redemption%20History.jpeg">

**Update loyalty prog**
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/PUT%20%20update%20loyalty%20prog.jpeg">

**get payment**
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/get%20payment.jpeg">

**create loyalty**
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/create%20loyalty.jpeg">

**Customer Get Available Loyalty Programs**
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/customer%20%20hal%2020.%20Get%20Available%20Loyalty%20Programs.jpeg">



#### Features Implemented
1. Integrasi Authentication - Frontend dengan Backend


2. Integrasi LoyaltyPoints - Frontend dengan Backend


3. Integrasi RedeemPoints - Frontend dengan Backend



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

### 3.4 Booking Flow Testing




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
