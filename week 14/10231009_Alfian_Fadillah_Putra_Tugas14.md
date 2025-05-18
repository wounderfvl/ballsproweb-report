# Laporan Progres Mingguan - BALLS (Borneo Anfield Loyalty System)


- **Kelompok**: 9
- **Mitra**: Borneo Anfield Stadium
- **Pekan ke-**: 14
- **Tanggal**: 15/05/2025

---
## Anggota Kelompok

- **Alfian Fadhillah Putra (10231009) (PM)**
- **Achmad Bayhaqi (10231009) (DevOps)**
- **Dahayu Azhka Daeshawnda (10231009) (Frontend)** 
- **Khanza Nabilla Tsabita (10231009) (Backend)**

---

## Progress Summary
Pada minggu ini, tim telah berhasil menyelesaikan beberapa tampilan antarmuka pengguna yang mencakup fitur-fitur utama sistem. Desain halaman mencakup autentikasi super admin, penambahan admin baru, serta manajemen transaksi, laporan, dan akun super admin. Setiap tampilan telah dirancang dengan fokus pada kemudahan navigasi dan fungsionalitas, mendukung peran masing-masing pengguna dalam sistem. Capaian ini menunjukkan kemajuan signifikan dalam pengembangan sisi frontend dan menjadi fondasi kuat untuk integrasi dengan sistem backend ke depannya. Sementara dari sisi backend, semua logika untuk kebutuhan sistem sudah selesai.

## Accomplished Tasks
1. **Backend Development (Next.js)**
- Telah menyelesaikan seluruh struktur fitur backend
- Melakukan pengecekan ulang terhadap endpoint yang telah dibuat (reports dan CRUD admin)
- Cross-check validasi input dan format response agar sesuai standar frontend

2. **Frontend Development (React)**
- Desain tampilan autentikasi super admin telah selesai untuk kebutuhan login dengan keamanan terpusat.
- Pembuatan UI untuk fitur penambahan admin baru, termasuk form input dan kontrol akses.
- Penyusunan tampilan halaman manajemen transaksi, mencakup daftar transaksi dan fitur pengelolaan.
- Perancangan halaman manajemen laporan untuk menampilkan data laporan yang mudah dibaca dan diakses.
- Pengembangan halaman manajemen super admin, berisi pengaturan dan pengelolaan akun super admin.
- Konsistensi visual dan struktur navigasi dijaga antar halaman untuk pengalaman pengguna yang lebih baik.

3. **QA & DevOps**
- QA telah melakukan pengujian fungsional awal dan usability test dengan minimal 3 pengguna untuk mengevaluasi alur dan kenyamanan tampilan, serta mencatat bug yang ditemukan untuk perbaikan lebih lanjut.
- DevOps menyiapkan lingkungan staging dan memastikan sinkronisasi versi frontend melalui Git, serta melakukan verifikasi awal terhadap kompatibilitas tampilan di berbagai perangkat.

4. **Project Manager + UI/UX**
- Menyelesaikan desain UI sesuai dengan kebutuhan mitra (User needs) dan untuk panduan tim Front End dalam mengimplementasikan websitenya.

## Challenges and Solutions
- *Challenge 1*: Ketidaksesuaian layout antar halaman yang menyebabkan tampilan tidak konsisten saat berpindah menu.
  *Solution*: Tim frontend menyusun ulang struktur layout utama dan menyatukan komponen UI yang bersifat global agar tampilan lebih seragam.

- *Challenge 2*: Beberapa elemen interaktif (seperti tombol dan input form) tidak merespons dengan baik saat dilakukan pengujian awal.
  *Solution*: QA mendokumentasikan bug tersebut dan frontend melakukan penyesuaian ulang pada properti elemen serta melakukan retesting untuk memastikan fungsionalitas berjalan sesuai.

### Next Week Plan
- Final Presentation: Slide dan demo lengkap (15-20 menit)
- Complete Documentation: README, API docs, user manual
- Source Code: Repo GitHub dengan tag/release final
- Deployed Application: Link aplikasi yang sudah di-deploy

### Unit Testing
1. **Autentikasi (Login)**:
```tsx
import { render, screen, fireEvent } from '@testing-library/react';
import SignInPage from './page';
import { useAuth } from '../../../contexts';
import { useRouter } from 'next/navigation';

// Mock context dan router
jest.mock('../../../contexts', () => ({
  useAuth: () => ({
    login: jest.fn(),
    isLoading: false,
    error: null,
  }),
}));
jest.mock('next/navigation', () => ({
  useRouter: () => ({ push: jest.fn() }),
}));

describe('SignInPage', () => {
  it('menampilkan pesan error kalau email atau password kosong', () => {
    render(<SignInPage />);
    fireEvent.click(screen.getByRole('button', { name: /sign in/i }));
    expect(screen.getByText('Email and password are required')).toBeInTheDocument();
  });

  it('memanggil login dan redirect kalau input valid', async () => {
    const { login } = useAuth();
    const { push } = useRouter();
    render(<SignInPage />);

    fireEvent.change(screen.getByPlaceholderText('Your Email'), {
      target: { value: 'a@b.com' }
    });
    fireEvent.change(screen.getByPlaceholderText('Your Password'), {
      target: { value: 'secret' }
    });
    fireEvent.click(screen.getByRole('button', { name: /sign in/i }));

    expect(login).toHaveBeenCalledWith('a@b.com', 'secret');
    // Anda bisa tunggu promise dan cek push dipanggil
    // await waitFor(() => expect(push).toHaveBeenCalledWith('/dashboard'));
  });
});
```

2. **CRUD Admin (oleh Super Admin)**:
```tsx
import React from 'react'
import { render, screen, fireEvent, waitFor } from '@testing-library/react'
import SuperAdminDashboard from '../page'
import * as nextNavigation from 'next/navigation'

// --- 1) Mock useRouter dari next/navigation ---
const pushMock = jest.fn()
jest.spyOn(nextNavigation, 'useRouter').mockImplementation(() => ({
  push: pushMock,
} as any))

// --- 2) Mock komponen anak: AdminList & AddAdminForm ---
jest.mock('@/components/admin/superadmin/AdminList', () => (props: any) => (
  <div data-testid="admin-card">
    <span>{props.admin.name}</span>
    <button data-testid="edit-btn" onClick={() => props.onEdit()}></button>
    <button data-testid="delete-btn" onClick={() => props.onDelete()}></button>
    <button data-testid="verify-btn" onClick={() => props.onVerify()}></button>
  </div>
))
jest.mock('@/components/admin/superadmin/AddAdmminForm', () => (props: any) => (
  <div data-testid="add-form">
    {/* Simulasikan form dengan dua input */}
    <input
      data-testid="name-input"
      defaultValue={props.initialData?.name || ''}
      placeholder="Name"
      onChange={e => (props.initialData = { ...props.initialData, name: e.target.value })}
    />
    <input
      data-testid="email-input"
      defaultValue={props.initialData?.email || ''}
      placeholder="Email"
      onChange={e => (props.initialData = { ...props.initialData, email: e.target.value })}
    />
    <button
      data-testid="submit-btn"
      onClick={() =>
        props.onSubmit(
          props.initialData || { name: 'New Admin', email: 'new@example.com' }
        )
      }
    ></button>
    <button data-testid="cancel-btn" onClick={props.onCancel}></button>
  </div>
))

describe('SuperAdminDashboard CRUD UI', () => {
  beforeEach(() => {
    jest.clearAllMocks()
    // reset storages
    sessionStorage.clear()
    localStorage.clear()
  })

  it('redirects to /admin/super-admin jika belum login', () => {
    render(<SuperAdminDashboard />)
    expect(pushMock).toHaveBeenCalledWith('/admin/super-admin')
  })

  it('menampilkan daftar admin dari state & localStorage saat authenticated', async () => {
    // siapkan sessionStorage & localStorage
    sessionStorage.setItem('superAdminAuthenticated', 'true')
    localStorage.setItem(
      'adminUsers',
      JSON.stringify([
        { id: 'x', name: 'Foo Admin', email: 'foo@a.com', verified: false },
      ])
    )

    render(<SuperAdminDashboard />)
    // tunggu efek useEffect
    await waitFor(() => expect(screen.queryByText('Loading...')).toBeNull())

    // kartu admin dari localStorage
    expect(screen.getByText('Foo Admin')).toBeInTheDocument()
  })

  it('bisa menambah admin baru lewat form', async () => {
    sessionStorage.setItem('superAdminAuthenticated', 'true')
    render(<SuperAdminDashboard />)
    await waitFor(() => expect(screen.queryByText('Loading...')).toBeNull())

    // klik tombol "Tambah Admin"
    const addBtn = screen.getByRole('button', { name: /Tambah Admin/i })
    fireEvent.click(addBtn)

    // form muncul
    expect(screen.getByTestId('add-form')).toBeInTheDocument()

    // isi & submit
    fireEvent.change(screen.getByTestId('name-input'), { target: { value: 'Zed Admin' }})
    fireEvent.change(screen.getByTestId('email-input'), { target: { value: 'zed@a.com' }})
    fireEvent.click(screen.getByTestId('submit-btn'))

    // kartu baru muncul
    await waitFor(() => {
      expect(screen.getByText('Zed Admin')).toBeInTheDocument()
      // juga tersimpan di localStorage
      const saved = JSON.parse(localStorage.getItem('adminUsers')!)
      expect(saved.find((a: any) => a.name === 'Zed Admin')).toBeTruthy()
    })
  })

  it('bisa mengedit admin yang ada', async () => {
    sessionStorage.setItem('superAdminAuthenticated', 'true')
    localStorage.setItem(
      'adminUsers',
      JSON.stringify([{ id: '1', name: 'Old Name', email: 'old@a.com', verified: true }])
    )
    render(<SuperAdminDashboard />)
    await waitFor(() => expect(screen.queryByText('Loading...')).toBeNull())

    // klik edit di kartu pertama
    fireEvent.click(screen.getByTestId('edit-btn'))
    // form muncul dengan initialData
    expect(screen.getByTestId('add-form')).toBeInTheDocument()

    // ubah nama & submit
    fireEvent.change(screen.getByTestId('name-input'), { target: { value: 'Updated Name' }})
    fireEvent.click(screen.getByTestId('submit-btn'))

    // kartu ter‐update
    await waitFor(() => {
      expect(screen.getByText('Updated Name')).toBeInTheDocument()
      const saved = JSON.parse(localStorage.getItem('adminUsers')!)
      expect(saved[0].name).toBe('Updated Name')
    })
  })

  it('bisa menghapus admin', async () => {
    sessionStorage.setItem('superAdminAuthenticated', 'true')
    localStorage.setItem(
      'adminUsers',
      JSON.stringify([
        { id: '1', name: 'To Be Deleted', email: 'del@a.com', verified: false },
      ])
    )
    render(<SuperAdminDashboard />)
    await waitFor(() => expect(screen.queryByText('Loading...')).toBeNull())

    // klik delete
    fireEvent.click(screen.getByTestId('delete-btn'))

    await waitFor(() => {
      expect(screen.queryByText('To Be Deleted')).toBeNull()
      const saved = JSON.parse(localStorage.getItem('adminUsers')!)
      expect(saved.length).toBe(0)
    })
  })

  it('bisa toggle verifikasi admin', async () => {
    sessionStorage.setItem('superAdminAuthenticated', 'true')
    localStorage.setItem(
      'adminUsers',
      JSON.stringify([
        { id: '1', name: 'Veri Admin', email: 'veri@a.com', verified: false },
      ])
    )
    render(<SuperAdminDashboard />)
    await waitFor(() => expect(screen.queryByText('Loading...')).toBeNull())

    // klik verify
    fireEvent.click(screen.getByTestId('verify-btn'))

    await waitFor(() => {
      const saved = JSON.parse(localStorage.getItem('adminUsers')!)
      expect(saved[0].verified).toBe(true)
    })
  })
})
```

3. **Booking**:
```tsx
import React from 'react'
import { render, screen, fireEvent, waitFor } from '@testing-library/react'
import BookingPage from '../page'
import * as nextNavigation from 'next/navigation'

// --- Mock useRouter ---
const pushMock = jest.fn()
jest.spyOn(nextNavigation, 'useRouter').mockImplementation(() => ({ push: pushMock } as any))

// Mock alert supaya tidak muncul native dialog
window.alert = jest.fn()

describe('BookingPage flow', () => {
  beforeEach(() => {
    jest.clearAllMocks()
    sessionStorage.clear()
    localStorage.clear()
  })

  it('redirects to /auth/login when not logged in', () => {
    render(<BookingPage />)
    expect(pushMock).toHaveBeenCalledWith('/auth/login')
  })

  it('loads user from localStorage and shows user info', async () => {
    sessionStorage.setItem('irrelevant', '1')
    localStorage.setItem(
      'user',
      JSON.stringify({ id: 'u1', name: 'Alice', email: 'alice@x.com', phone: '123' })
    )
    render(<BookingPage />)
    // menunggu useEffect
    await waitFor(() => expect(screen.getByText(/Alice/)).toBeInTheDocument())
    expect(screen.getByText('alice@x.com')).toBeInTheDocument()
    expect(screen.getByText('123')).toBeInTheDocument()
  })

  it('allows selecting field, time, date and enables Confirm Booking', async () => {
    localStorage.setItem(
      'user',
      JSON.stringify({ id: 'u1', name: 'Alice', email: 'alice@x.com', phone: '123' })
    )
    render(<BookingPage />)
    await waitFor(() => expect(screen.queryByText('Loading...')).toBeNull())

    // pilih field pertama
    const fieldCards = screen.getAllByText('Field A')
    fireEvent.click(fieldCards[0])

    // pilih time slot 9:00 AM
    const slot = screen.getByText('9:00 AM')
    fireEvent.click(slot)

    // pilih tanggal hari ini dalam calendar
    const today = new Date().getDate().toString()
    const dateCell = screen.getAllByText(today).find(el => el.className.includes('cursor-pointer'))
    fireEvent.click(dateCell!)

    // tombol Confirm sekarang enabled
    const confirmBtn = screen.getByRole('button', { name: /Confirm Booking/i })
    expect(confirmBtn).not.toBeDisabled()
  })

  it('prevents booking a slot twice with alert', async () => {
    // setup existing booking at 9:00 AM today
    const todayStr = new Date().toISOString().split('T')[0]
    localStorage.setItem(
      'user',
      JSON.stringify({ id: 'u1', name: 'Alice', email: 'alice@x.com', phone: '123' })
    )
    localStorage.setItem(
      'bookings',
      JSON.stringify([{
        id: 'b1',
        field: { id: '1', name: 'Field A', location: 'North Wing' },
        date: todayStr,
        time: '9:00 AM',
        user: {},
        status: 'pending',
        createdAt: new Date()
      }])
    )
    render(<BookingPage />)
    await waitFor(() => expect(screen.queryByText('Loading...')).toBeNull())

    // pilih field/time/date yang sama
    fireEvent.click(screen.getAllByText('Field A')[0])
    fireEvent.click(screen.getByText('9:00 AM'))
    const todayCell = screen.getAllByText(new Date().getDate().toString())
      .find(el => el.className.includes('cursor-pointer'))
    fireEvent.click(todayCell!)

    // klik Confirm Booking -> harus munculkan alert
    fireEvent.click(screen.getByRole('button', { name: /Confirm Booking/i }))
    expect(window.alert).toHaveBeenCalledWith(
      'This time slot is already booked. Please select another time.'
    )
  })

  it('advances to step 2 then step 3 and on confirm payment saves booking and redirects', async () => {
    localStorage.setItem(
      'user',
      JSON.stringify({ id: 'u1', name: 'Alice', email: 'alice@x.com', phone: '123' })
    )
    render(<BookingPage />)
    await waitFor(() => expect(screen.queryByText('Loading...')).toBeNull())

    // Step 1 selections
    fireEvent.click(screen.getAllByText('Field B')[0])
    fireEvent.click(screen.getByText('11:00 AM'))
    fireEvent.click(screen.getAllByText(new Date().getDate().toString())[0])

    fireEvent.click(screen.getByRole('button', { name: /Confirm Booking/i }))
    // sekarang tampil Step 2
    expect(screen.getByText(/Confirm Your Booking/i)).toBeInTheDocument()

    // lanjut ke pembayaran
    fireEvent.click(screen.getByRole('button', { name: /Proceed to Payment/i }))
    expect(screen.getByText(/Proceed Payment/i)).toBeInTheDocument()

    // confirm payment
    fireEvent.click(screen.getByRole('button', { name: /Confirm Payment/i }))
    await waitFor(() => {
      // redirect
      expect(pushMock).toHaveBeenCalledWith('/pengguna/booking/upload-payment')
      // booking tersimpan
      const all = JSON.parse(localStorage.getItem('bookings')!)
      expect(all.some((b: any) => b.time === '11:00 AM')).toBe(true)
    })
  })

  it('toggles booking history panel', async () => {
    localStorage.setItem(
      'user',
      JSON.stringify({ id: 'u1', name: 'Alice', email: 'alice@x.com', phone: '123' })
    )
    render(<BookingPage />)
    await waitFor(() => expect(screen.queryByText('Loading...')).toBeNull())

    const toggleBtn = screen.getByRole('button', { name: /Show Booking History/i })
    fireEvent.click(toggleBtn)
    expect(screen.getByText(/Booking History/i)).toBeInTheDocument()
    fireEvent.click(toggleBtn)
    expect(screen.queryByText(/Booking History/i)).toBeNull()
  })
})
```

### Bugfix Report
-

### 

## Contributions
**Alfian Fadhillah Putra (Project Manager)**: 
- Menyempurnakan dan melengkapi desain UI/UX untuk fitur-fitur;
- Component styling;
- Menemui stakeholder untuk mendiskusikan terkait progress dan permintaan baru stakeholder;
- Membuat laporan MD.

**Achmad Bayhaqi (DevOps)**:
- Dokumentasi API,
- Integrasi dengan backend dan frontend,
- Membuat laporan MD.

**Dahayu Azhka Daeshawnda (Frontend)**:
- Frontend development (React components) & State management;
- Booking system, autentikasi, dashboard, dan fitur tambah pemain (FE).

**Khanza Nabilla Tsabita (Backend)**:
- Merapikan dan menyelaraskan struktur kode backend,
- Melakukan pengecekan endpoint untuk memastikan tidak ada error,
- Membuat laporan MD.

## Screenshots / Demo Core Feature

---

## 2. Core Feature
#### Frontend Implementation

**Transaction management**
<img src="Transaction management.jpeg">

**Super admin management**
<img src="Super admin management.jpeg">

**Report management**
<img src="Report management.jpeg">

**Add new admin**
<img src="Add new admin.jpeg">

**Super Admin Authentication**
<img src="Super Admin Authentication.jpeg">

### 3. Deployment Plan
Kami merencanakan mendeploy di vercel.com dengan backend service supabase

### 3.1 Hosting? domain? dll
- Deployment: vercel.com
- Backend Service: supabase.com
- Domain: https://balls.vercel.app

Alternatif: VPS Hosting di domanesia


### 3.2 Lorem ipsum Flow Testing
```
User Input
     ↓
Middleware (Auth & Validation)
     ↓
Backend Logic (Controllers / Services)
     ↓
Database / Storage
     ↓
Response dikirim ke User
```


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
