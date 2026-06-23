# CHANGELOG — ERP Penggilingan Padi PRO+ v2.0.0

## v2.0.0 STABLE (2026-06-23) — Sprint v2.0: Single Source of Truth

### New: Master Barang
- Tabel `masterBarang` di database dengan field: kodeBarang, namaBarang, kategori, satuan, aktif
- 15 item default: 5 Gabah, 5 PK, 2 Beras, 3 Produk Samping
- CRUD penuh: Tambah, Ubah, Hapus, Toggle Aktif
- Auto-migration: masterBarang dibangun dari jenisGabah/jenisBeras/jenisSamping/jenisBahanBaku
- `_syncJenisFromMasterBarang()`: sync balik ke jenis arrays untuk backward compat
- Halaman baru: Data Master → Master Barang (nav 12)

### New: Helper Functions (Single Source of Truth)
- `getBarang(namaBarang)` — resolusi item ke {kodeBarang, kategori, satuan}
- `getKategoriBarang(namaBarang)` — shorthand kategori
- `getKategoriPembelian(r)` — kategori dari record pembelian aktual
- `getStokByItem(namaBarang)` — stok satu item dari semua sumber

### Bug Fixes: Kategori Sinkronisasi
- `getMutasiHistory() pembelian`: `kategori:'Gabah'` hardcoded → `getKategoriPembelian(r)`
  - Pembelian beras sekarang tampil sebagai 'Beras', bukan 'Gabah'
- `getMutasiHistory() penjualan`: binary Gabah/Beras → `getKategoriBarang(r.produk)`
  - Penjualan Bekatul/Menir tampil sebagai 'Produk Samping', bukan 'Beras'
- `getMutasiHistory() produksi GABAH_BERAS`:
  - Menir: `'Beras'` → `'Produk Samping'` ✅
  - Bekatul: `'Beras'` → `'Produk Samping'` ✅
- `getMutasiHistory() produksi PK_BERAS`:
  - Menir: `'Beras'` → `'Produk Samping'` ✅
  - Bekatul: `'Beras'` → `'Produk Samping'` ✅
- `getMutasiHistory() produksi GABAH_PK`:
  - PK: `'Produk Samping'` → `'PK'` ✅
- `getMutasiHistory() produksi PK_BERAS keluar`:
  - PK: `'Produk Samping'` → `'PK'` ✅
- Keterangan pembelian: "Pembelian gabah X" → "Pembelian [kategori] X"

### Backward Compatibility
- Semua jenis arrays lama (jenisGabah, jenisBeras, dll.) tetap berfungsi
- Data lama tanpa masterBarang → auto-migrated on first load
- Semua form lama tetap membaca dari jenis arrays (melalui _syncJenisFromMasterBarang)

---

## v1.1.0 STABLE (2026-06-23) — Full Audit & Hardening
- 13 bug fix null safety, division zero, dead references
- Global error handler, renderPage try-catch
- Simulasi 948 TX: stok valid

## v1.0.1 HOTFIX-1 (2026-06-23)
- saveKasManual: kas_tanggal → km_tanggal (bug utama pembayaran hutang)

## v1.0.0 RC-FINAL (2026-06-23)
- Production Ready: 80/80 test pass
- Sprint 15: LOT Traceability, Kartu LOT, Dashboard LOT
- Sprint 14: Produksi 3-Mode (Gabah→Beras, Gabah→PK, PK→Beras)
- Sprint 13: Staged batch, double-click protection
- Sprint 12: Terminologi Husker/Polisher
- Sprint 11: Laporan, BI, Chart.js
- Sprint 8: Jurnal Double-Entry, Neraca, L/R
- Sprint 5: Produksi, HPP FIFO, Stok real-time
