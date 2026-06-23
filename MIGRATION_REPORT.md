# MIGRATION REPORT — v2.0.0

## Auto-Migration yang Dijalankan Saat Pertama Buka

Saat membuka database lama (v1.x) di versi 2.0.0:

1. **masterBarang dibuat otomatis** dari:
   - `DB.jenisGabah` → items dengan kategori 'Gabah'
   - `DB.jenisBeras` → items dengan kategori 'Beras'
   - `DB.jenisSamping` → items dengan kategori 'Produk Samping'
   - `DB.jenisBahanBaku` → items dengan kategori 'PK'
   - PK ditambahkan jika belum ada

2. **jenis arrays lama tetap berfungsi** — selalu sync dari masterBarang

3. **Tidak ada data transaksi yang diubah** — hanya penambahan masterBarang

## Backward Compatibility

| Fitur | v1.x | v2.0 |
|---|---|---|
| Data pembelian lama | ✅ | ✅ |
| Data produksi lama | ✅ | ✅ |
| Data penjualan lama | ✅ | ✅ |
| Jurnal lama | ✅ | ✅ |
| LOT tracking lama | ✅ | ✅ |
| jenisGabah/jenisBeras/dll. | ✅ | ✅ (sync dari masterBarang) |
| Kategori di getMutasiHistory | ❌ (bug) | ✅ (fixed) |
