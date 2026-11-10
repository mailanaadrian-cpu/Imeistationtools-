# IMEI STATION TOOLS

Starter website React + Vite + Supabase untuk portal layanan. Fitur:
- Daftar/login email dan password.
- Saldo pengguna dan riwayat.
- Deposit manual dengan bukti wajib; saldo hanya bertambah setelah admin menyetujui.
- Katalog layanan sesuai harga awal.
- Form order dengan IMEI dan foto wajib.
- Pemotongan saldo atomik saat order dibuat.
- Dashboard admin untuk verifikasi deposit dan pembaruan status pesanan.
- File bukti/foto disimpan pada Supabase Storage privat.

## 1. Siapkan Supabase
1. Buat project di https://supabase.com.
2. Buka SQL Editor, jalankan seluruh isi `supabase/schema.sql`.
3. Buka Project Settings > API, salin Project URL dan anon/public key.
4. Salin `.env.example` menjadi `.env.local`, lalu isi:
   - `VITE_SUPABASE_URL`
   - `VITE_SUPABASE_ANON_KEY`
5. Jangan pernah memasukkan `service_role` key ke frontend atau GitHub.

## 2. Jalankan lokal
```bash
npm install
npm run dev
```
Buka alamat lokal yang ditampilkan Vite.

## 3. Jadikan akun sebagai admin
1. Daftarkan akun admin melalui website.
2. Di Supabase SQL Editor jalankan perintah berikut dengan email admin milik Anda:
```sql
update public.profiles set role='admin' where email='EMAIL_ADMIN_ANDA';
```
Jangan menyediakan fitur ubah role admin dari browser.

## 4. Pengaturan deposit manual
Tambahkan instruksi transfer resmi (nama bank/e-wallet dan nomor tujuan milik bisnis) pada bagian Deposit sebelum website dipakai pelanggan. Detail pembayaran sengaja tidak diisi otomatis karena harus berasal dari pemilik usaha dan diverifikasi.

## 5. Publikasikan
- Push repository ke GitHub.
- Import repository ke Vercel.
- Tambahkan Environment Variables yang sama di pengaturan Vercel.
- Deploy.

## Catatan penting sebelum produksi
- Website ini hanya menangani penerimaan pengajuan, administrasi, dan pemeriksaan melalui prosedur resmi. Website tidak menjalankan bypass, perubahan IMEI, atau penghindaran pemblokiran/registrasi perangkat.
- Tetapkan instruksi pembayaran resmi, kebijakan privasi, syarat layanan, kontak bantuan, dan prosedur pengembalian dana.
- Uji dengan akun user dan admin terpisah sebelum menerima pembayaran sungguhan.
- Untuk menjaga keamanan, aktifkan konfirmasi email dan proteksi tambahan pada akun admin.
- Harga awal berada di tabel `services` dan dapat diubah admin melalui SQL/dashboard database; frontend tidak memberi hak edit harga kepada user.
