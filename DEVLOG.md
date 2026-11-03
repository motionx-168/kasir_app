# DEVLOG — kasir_app (Digital Why?)

## Setup environment (SELESAI)
- Termux + Flutter 3.47.9 + Android SDK 36
- adb dari Termux, symlink di SDK (adb.x86-backup disimpan)
- flutter doctor: Android toolchain OK, device OK

## Fix AAPT2 (build gagal pertama)
- Error: AAPT2 x86_64 di ARM64
- Fix: pkg install aapt2 + android.aapt2FromMavenOverride di ~/.gradle/gradle.properties
- Status: build ulang sedang dicoba

## Keputusan produk (BELUM FINAL, konfirmasi ke client dulu)
- Model bisnis: minimarket + canvasser
- Fokus awal: scanner barcode via kamera HP
- Barang tanpa barcode: PLU + quick keys
- Model stok: ledger (append-only), dua lokasi (toko/gudang)
- Stok berkurang saat scan, pakai reserve-commit
- Arsitektur: local-first, Flutter + ML Kit + SQLite
- Sync ke cloud: nanti (fase 3)

## Sedang dikerjakan
- Build APK debug (percobaan kedua setelah fix AAPT2)

## Langkah berikutnya
1. Verifikasi APK berhasil dibuat
2. Buat halaman scanner kosong (kamera → barcode → tampilkan kode)
3. Setelah scanner jalan, baru buat data produk minimal
- 2026-11-02: Build APK debug BERHASIL. Error llvm-strip = warning, aman diabaikan.
- 2026-11-02: APK debug arm64 = 60MB (sebelumnya 1.4GB). Fix berhasil.
- 2026-11-03: 🎉 SUKSES BESAR! Build APK Release (15.5MB) berhasil via proot Ubuntu + QEMU gen_snapshot + AAPT2 Termux override.
