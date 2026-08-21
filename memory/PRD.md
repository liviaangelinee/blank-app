# PRD — AquaRekap (Rekap Laporan Penjualan AMDK)

## Original Problem Statement
Aplikasi rekap laporan penjualan AMDK (Bahasa Indonesia): input transaksi (tanggal, customer, produk, jumlah, harga per varian Grosir/SO/Retail, harga dapat diubah per customer), tabel rekap, total per produk, filter tanggal/customer/status, export Excel & PDF, dashboard grafik, manajemen produk & customer, login sederhana (single admin), catat transaksi belum lunas per customer + sisa tagihan di dashboard, halaman rekap bulanan.
Produk seed: CHEERS ALKALINE (1200/550/330/230/GALON), CHEERS REGULAR (1500/600/330/220/GALON), VEMA (1500/600/220/GALON).

## User Choices
- Single admin login (JWT httpOnly cookie), email liviaangeline@gmail.com
- Export: Excel + PDF
- Mata uang: Rupiah (format Indonesia)
- Harga: kombinasi (default per varian, bisa diubah saat transaksi)
- Status pembayaran: Lunas / Belum Lunas

## Architecture
- Backend: FastAPI + MongoDB (motor). Auth JWT bcrypt + brute-force lockout. Export via openpyxl (Excel) & reportlab (PDF).
- Frontend: React + Tailwind + shadcn/ui + Recharts. Fonts Work Sans / IBM Plex Sans. Swiss high-contrast light theme.
- Collections: users, products, customers, transactions, login_attempts.

## Implemented (2026-08-21)
- Auth: login/logout/me/refresh, single-admin seed (idempotent), brute-force lockout (429 after 5).
- Manajemen Produk: CRUD, varian dengan 3 harga (Grosir/SO/Retail). Seed 3 produk.
- Manajemen Customer: CRUD, tipe harga default.
- Input Transaksi: multi-item, auto harga per varian & tipe, harga editable, subtotal/total otomatis, status Lunas/Belum Lunas.
- Tabel Rekap: filter tanggal/customer/status, total per produk, toggle status, hapus.
- Export Excel & PDF (mengikuti filter).
- Dashboard: total omset, transaksi, sisa tagihan, total customer, tren omset, produk terlaris, sisa tagihan per customer.
- Rekap Bulanan: pilih bulan/tahun, ringkasan omset/lunas/sisa, rekap per produk & customer, grafik omset harian.
- Tested: backend 100% after fixes, frontend 100%.

## Notes
- Harga varian yang di-seed adalah PLACEHOLDER — admin sebaiknya menyesuaikan di menu Produk.

## Backlog / Next
- P1: Ganti native date picker dengan shadcn Calendar + format tanggal Indonesia.
- P2: Pembayaran sebagian (cicilan) & histori pembayaran.
- P2: Multi-user (kasir/staff) + peran.
- P2: Import data dari file Excel lama.
