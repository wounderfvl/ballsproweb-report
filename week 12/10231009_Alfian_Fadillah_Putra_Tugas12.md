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
Minggu ini tim telah berhasil mengimplementasikan bebrapa sistem manajemen dan fitur utama yang dibutuhkan oleh stakeholder. Tim frontend telah menyelesaikan implementasi fitur inti berupa sistem booking multi-step, autentikasi pengguna, dan dashboard navigasi. Proses booking memungkinkan pengguna memilih lapangan, tanggal, dan waktu secara interaktif hingga tahap konfirmasi dan pembayaran (mock UI). Sistem autentikasi mendukung sign-in dan sign-up dengan validasi, serta opsi tambahan untuk kenyamanan pengguna. Dashboard menyediakan akses cepat ke fitur utama. Fitur tambahan berupa penambahan pemain saat booking juga telah tersedia, meskipun belum terhubung ke backend. Dan dari backend, backend sudah mengimplementasikan paymment dan program loyalty. Database, dan struktur folder backend dengan arsitektur modular (routes, controllers, models) sudah di setup. Pencapaian utama frontend meliputi:

1. **Step Management**:
- Menambahkan status langkah untuk mengelola langkah saat ini (1 untuk pemesanan, 2 untuk mengonfirmasi detail, 3 untuk pembayaran).
- UI berubah secara dinamis berdasarkan langkah saat ini.

2. **Payment Card (Mock UI)**:
- Menambahkan kartu baru untuk langkah pembayaran.
- Memungkinkan pengguna untuk memilih metode pembayaran dan mengonfirmasi pembayaran.
- Yang harus dilakukan: menerapkan gateway pembayaran yang sebenarnya

3. **Navigation Between Steps**:
- Mengklik "Konfirmasi Pemesanan" akan memindahkan pengguna ke langkah konfirmasi.
- Mengklik "Lanjutkan ke Pembayaran" akan memindahkan pengguna ke langkah pembayaran.
- Mengklik "Konfirmasi Pembayaran" akan menyelesaikan proses dan menyetel ulang formulir.

4. **Core feature #2**: 
- (FE) Tambah pemain saat pemesanan (untuk loyalitas per pemain).
- Menambahkan/menghapus pemain lain yang akan berpartisipasi dalam sesi.
- Pemain ditampilkan dalam kisi responsif.

## Accomplished Tasks
1. **Backend Development (Next.js)**
- Mengimplementasikan struktur database di PostgreSQL
- Setup struktur project backend dengan arsitektur modular (controllers, models, routes)
- Implementasi sistem autentikasi berbasis JWT untuk user, admin dan super admin
- Pengembangan beberapa endpoint terkait loyalty dan payment (GET /payment-methods, GET /loyalty/points, GET /loyalty/programs, GET /loyalty/redemptions, POST /loyalty/redeem)

2. **Frontend Development (React)**
- Menambahkan state untuk mengatur langkah pemesanan (booking → konfirmasi → pembayaran), dengan UI yang berubah dinamis sesuai langkah.
- Menambahkan tampilan kartu untuk langkah pembayaran, termasuk pilihan metode pembayaran dan tombol konfirmasi (belum terhubung dengan gateway pembayaran nyata).
- Tombol "Confirm Booking", "Proceed to Payment", dan "Confirm Payment" mengatur transisi antar langkah dan mengatur ulang form setelah pembayaran selesai.
- Menambahkan fitur untuk input pemain tambahan saat booking (untuk sistem loyalti), dengan tampilan grid responsif (belum terhubung ke backend).

3. **Database & API**
- Merancang dan migrasi database PostgreSQL (balls)
- Membuat tabel: payment_methods, loyalty_programs, loyalty_points, redemptions, dll

4. **Project Manager + UI/UX**
- Pengambilan keputusan terkait permintaan mitra yang mendadak.
- Menyelesaikan UI untuk pelanggan.

## Challenges and Solutions
- *Challenge 1*: Menangani transisi antar langkah dalam proses booking secara dinamis  
  *Solution*: Menggunakan state (useState) untuk mengelola current step dan user input agar UI bisa berubah sesuai alur

- *Challenge 2*: Membuat form autentikasi yang fleksibel untuk dua mode (sign-in dan sign-up)  
  *Solution*: Membuat komponen AuthForm yang dapat merender field dinamis berdasarkan konfigurasi

## Next Week Plan
### Next Week Plan
- Menyelesaikan UI core feature ke-4 : Loyalty  
- Finalisasi tampilan serta validasi lanjutan pada form booking
- Admin Panel: Dashboard sederhana untuk pengelolaan data
- Membuat data visualization: Chart/grafik sederhana untuk data pemain dan keuangan

4. **Unit Testing**
   - Test Case 1 (Login): 
```tsx
// src/app/(auth)/sign-in/page.tsx
'use client';

import { useState } from 'react';
import { useRouter } from 'next/navigation';
import { useAuth } from '@/contexts';
import AuthForm from '../components/AuthForm';
import AuthInput from '../components/AuthInput';

export default function SignInPage() {
  const router = useRouter();
  const { login, isLoading, error } = useAuth();
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [formError, setFormError] = useState<string | null>(null);

  const handleSubmit = async (e: React.FormEvent) => {
    e.preventDefault();
    setFormError(null);

    // Simple validation
    if (!email || !password) {
      setFormError('Email and password are required');
      return;
    }

    try {
      // Call login from auth context
      await login(email, password);
      // Redirect after successful login
      router.push('/dashboard');
    } catch (error) {
      console.error('Login error:', error);
      // Error is set in the auth context
    }
  };

  return (
    <AuthForm title="Sign In" onSubmit={handleSubmit}>
      {formError && <div className="text-red-500 mb-4">{formError}</div>}
      {error && <div className="text-red-500 mb-4">{error}</div>}
      
      <AuthInput
        type="email"
        label="Email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
        required
      />
      
      <AuthInput
        type="password"
        label="Password"
        value={password}
        onChange={(e) => setPassword(e.target.value)}
        required
      />
      
      <button
        type="submit"
        className="w-full bg-blue-600 text-white py-2 rounded-lg hover:bg-blue-700 transition-colors"
        disabled={isLoading}
      >
        {isLoading ? 'Signing in...' : 'Sign In'}
      </button>
    </AuthForm>
  );
}
```
   
   - Test Case 2 (Loyalty Points): 
```tsx
// src/app/loyalty/points/page.tsx
'use client';

import { useEffect } from 'react';
import { useLoyalty } from '@/contexts';

export default function LoyaltyPointsPage() {
  const { points, isLoading, error, fetchUserPoints } = useLoyalty();

  // Fetch points data when component mounts
  useEffect(() => {
    fetchUserPoints();
  }, [fetchUserPoints]);

  if (isLoading) {
    return (
      <div className="p-6">
        <h1 className="text-2xl font-bold mb-4">Loading Points...</h1>
      </div>
    );
  }

  if (error) {
    return (
      <div className="p-6">
        <h1 className="text-2xl font-bold mb-4">Loyalty Points</h1>
        <div className="bg-red-100 text-red-700 p-4 rounded-md">
          {error}
        </div>
      </div>
    );
  }

  if (!points) {
    return (
      <div className="p-6">
        <h1 className="text-2xl font-bold mb-4">Loyalty Points</h1>
        <p>No points data available. Please check back later.</p>
      </div>
    );
  }

  return (
    <div className="p-6">
      <h1 className="text-2xl font-bold mb-6">Loyalty Points</h1>
      
      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4 mb-8">
        <div className="bg-white p-4 rounded-lg shadow">
          <h2 className="text-lg font-semibold mb-2">Total Points</h2>
          <p className="text-3xl font-bold">{points.total_points}</p>
        </div>
        
        <div className="bg-white p-4 rounded-lg shadow">
          <h2 className="text-lg font-semibold mb-2">Active Points</h2>
          <p className="text-3xl font-bold text-green-600">{points.active_points}</p>
        </div>
        
        <div className="bg-white p-4 rounded-lg shadow">
          <h2 className="text-lg font-semibold mb-2">Used Points</h2>
          <p className="text-3xl font-bold text-blue-600">{points.used_points}</p>
        </div>
        
        <div className="bg-white p-4 rounded-lg shadow">
          <h2 className="text-lg font-semibold mb-2">Expired Points</h2>
          <p className="text-3xl font-bold text-gray-500">{points.expired_points}</p>
        </div>
      </div>
      
      <h2 className="text-xl font-semibold mb-4">Points History</h2>
      {points.points_history.length === 0 ? (
        <p>No points history available.</p>
      ) : (
        <div className="overflow-x-auto">
          <table className="min-w-full bg-white rounded-lg overflow-hidden">
            <thead className="bg-gray-100">
              <tr>
                <th className="py-3 px-4 text-left">Points</th>
                <th className="py-3 px-4 text-left">Source</th>
                <th className="py-3 px-4 text-left">Date Earned</th>
                <th className="py-3 px-4 text-left">Expiry Date</th>
                <th className="py-3 px-4 text-left">Status</th>
              </tr>
            </thead>
            <tbody>
              {points.points_history.map((history) => (
                <tr key={history.point_id} className="border-t">
                  <td className="py-3 px-4">{history.points_earned}</td>
                  <td className="py-3 px-4 capitalize">{history.source}</td>
                  <td className="py-3 px-4">
                    {new Date(history.earned_date).toLocaleDateString()}
                  </td>
                  <td className="py-3 px-4">
                    {new Date(history.expiry_date).toLocaleDateString()}
                  </td>
                  <td className="py-3 px-4">
                    {history.is_used ? (
                      <span className="text-gray-500">Used</span>
                    ) : (
                      <span className="text-green-600">Active</span>
                    )}
                  </td>
                </tr>
              ))}
            </tbody>
          </table>
        </div>
      )}
    </div>
  );
}
```
   
   - Test Case 3 (Redeem Points): 
```tsx
// src/app/loyalty/redeem/page.tsx
'use client';

import { useEffect, useState } from 'react';
import { useLoyalty } from '@/contexts';

export default function RedeemPointsPage() {
  const { 
    points, 
    programs, 
    isLoading, 
    error, 
    fetchUserPoints, 
    fetchLoyaltyPrograms, 
    redeemPoints 
  } = useLoyalty();
  
  const [selectedProgram, setSelectedProgram] = useState<string>('');
  const [redemptionSuccess, setRedemptionSuccess] = useState<string | null>(null);
  const [redemptionError, setRedemptionError] = useState<string | null>(null);

  // Fetch data when component mounts
  useEffect(() => {
    fetchUserPoints();
    fetchLoyaltyPrograms();
  }, [fetchUserPoints, fetchLoyaltyPrograms]);

  const handleRedeem = async () => {
    if (!selectedProgram) {
      setRedemptionError('Please select a program to redeem');
      return;
    }

    setRedemptionSuccess(null);
    setRedemptionError(null);

    try {
      // Find the selected program
      const program = programs?.find(p => p.program_id === selectedProgram);
      
      if (!program) {
        setRedemptionError('Selected program not found');
        return;
      }

      // Check if user has enough points
      if (!points || points.active_points < program.points_required) {
        setRedemptionError('Not enough points to redeem this reward');
        return;
      }

      // Execute redemption
      const result = await redeemPoints(selectedProgram, program.points_required);
      setRedemptionSuccess(`Redemption successful! Your code is: ${result.redemption_code}`);
      setSelectedProgram('');
    } catch (error) {
      console.error('Redemption error:', error);
      if (error instanceof Error) {
        setRedemptionError(error.message);
      } else {
        setRedemptionError('Failed to redeem points');
      }
    }
  };

  if (isLoading) {
    return (
      <div className="p-6">
        <h1 className="text-2xl font-bold mb-4">Loading...</h1>
      </div>
    );
  }

  if (error) {
    return (
      <div className="p-6">
        <h1 className="text-2xl font-bold mb-4">Redeem Points</h1>
        <div className="bg-red-100 text-red-700 p-4 rounded-md">
          {error}
        </div>
      </div>
    );
  }

  return (
    <div className="p-6">
      <h1 className="text-2xl font-bold mb-6">Redeem Points</h1>
      
      {/* Points Summary */}
      <div className="bg-white p-4 rounded-lg shadow mb-6">
        <h2 className="text-lg font-semibold mb-2">Your Active Points</h2>
        <p className="text-3xl font-bold text-green-600">{points?.active_points || 0}</p>
      </div>
      
      {/* Redemption Form */}
      <div className="bg-white p-6 rounded-lg shadow mb-6">
        <h2 className="text-xl font-semibold mb-4">Select a Reward</h2>
        
        {redemptionSuccess && (
          <div className="bg-green-100 text-green-700 p-4 rounded-md mb-4">
            {redemptionSuccess}
          </div>
        )}
        
        {redemptionError && (
          <div className="bg-red-100 text-red-700 p-4 rounded-md mb-4">
            {redemptionError}
          </div>
        )}
        
        {(!programs || programs.length === 0) ? (
          <p>No loyalty programs available at the moment.</p>
        ) : (
          <>
            <div className="mb-4">
              <label htmlFor="program" className="block text-sm font-medium text-gray-700 mb-1">
                Loyalty Program
              </label>
              <select
                id="program"
                value={selectedProgram}
                onChange={(e) => setSelectedProgram(e.target.value)}
                className="w-full p-2 border border-gray-300 rounded-md focus:ring-blue-500 focus:border-blue-500"
              >
                <option value="">Select a program</option>
                {programs.map((program) => (
                  <option 
                    key={program.program_id} 
                    value={program.program_id}
                    disabled={points?.active_points < program.points_required}
                  >
                    {program.program_name} ({program.points_required} points)
                  </option>
                ))}
              </select>
            </div>
            
            {selectedProgram && (
              <div className="mb-4">
                <h3 className="font-medium mb-2">Reward Details</h3>
                <div className="bg-gray-50 p-3 rounded-md">
                  {(() => {
                    const program = programs.find(p => p.program_id === selectedProgram);
                    if (!program) return null;
                    
                    return (
                      <>
                        <p className="mb-1"><span className="font-medium">Name:</span> {program.program_name}</p>
                        <p className="mb-1"><span className="font-medium">Description:</span> {program.description}</p>
                        <p className="mb-1"><span className="font-medium">Points Required:</span> {program.points_required}</p>
                        <p className="mb-1"><span className="font-medium">Reward Type:</span> {program.reward_type}</p>
                        <p><span className="font-medium">Reward Value:</span> {program.reward_value}</p>
                      </>
                    );
                  })()}
                </div>
              </div>
            )}
            
            <button
              onClick={handleRedeem}
              disabled={!selectedProgram || isLoading}
              className="w-full bg-blue-600 text-white py-2 rounded-lg hover:bg-blue-700 transition-colors disabled:bg-blue-300"
            >
              {isLoading ? 'Processing...' : 'Redeem Points'}
            </button>
          </>
        )}
      </div>
    </div>
  );
}
```

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

### Customer page
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/Customer%20page.png">



### Choose a schedule
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/choose%20a%20schedule.png">



### Confirm Booking
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/Confirm%20Booking.png">



### Payment
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/Payment.png">



---

## 2. Core Feature
### Fitur Customer page


#### Booking
    ```json
    "use client";
    import BookingCard from "../../components/BookingCard";

    export default function BookingPage() {
    return (
        <div className="bg-image">
        <div className="booking-page-container">
            {/* Page Title */}
            <h1 className="booking-title">Borneo Anfield Stadium</h1>

            {/* Booking Content */}
            <div className="booking-content">
            <BookingCard />
            </div>
        </div>

        <style jsx>{`
            body {
            color: green;
            }
        `}</style>
        </div>
    );
    }
    ```

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
