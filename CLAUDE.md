# Puzzle SU — catatan untuk Claude (baca ini dulu, jangan baca seluruh index.html)

Repo khusus `kanademonday/puzzle_su` (terpisah dari landing_otomatis). Aplikasi 1 berkas: `index.html` di root repo (HTML+CSS+JS murni, tanpa library, tanpa API berbayar, jalan offline).
Tujuan: menyusun gambar SU (surat ukur) sebagai potongan puzzle per **peta analog**, untuk membayangkan
lokasi bidang yang sudah / belum landing di Bhumi ATR. Bahasa UI & jawaban: **Bahasa Indonesia**.

## Model data (IndexedDB `puzzleSU`, store: `peta`, `bidang`, `img`)
- peta: `{id, nama, dibuat}`
- bidang: `{id, petaId, no, status:'landing'|'belum', luas, nib, su, catatan, img, poly:[[x,y]..] (px gambar),
  c:[x,y] pusat poly (px), s: meter per px (= sqrt(luas/luas_px)), x,y: posisi pusat di dunia (meter), rot (radian),
  kunci, tetangga:[{no,x,y}] (px gambar), diubah}`
- img: `{id, data: dataURL JPEG}`
- Nomor dibandingkan dengan `norm()` (huruf besar, tanpa spasi).

## Peta kode di index.html (cari judul bagian `/* ===== ... ===== */`)
- UTIL, GEOMETRI (`keDunia`, `keLokal`, `pusat`, `luasPoly`)
- PENYIMPANAN (IndexedDB, `ambilGambar`)
- DATA: `infoTetangga()` → `{ada, kosong, garis}`; `letakkanOtomatis()` → posisi awal bidang baru
- PUZZLE: `draw()`, interaksi pointer (geser, putar via handle, snap titik sudut), `fit()`
- PANEL SAMPING: `renderSide()`
- EDITOR SU: mode batas / tetangga / geser, popup nomor tetangga, tombol Simpan (`#eSave`)
- EKSPOR/IMPOR: JSON cadangan (gabung berdasarkan nomor + `diubah` terbaru), DXF R12 (Y dibalik, meter lokal), CSV, PNG

## Aturan kerja
- Ubah dengan Edit kecil pada bagian yang relevan; jangan menulis ulang seluruh berkas.
- Setelah ubah: cek sintaks dengan `node --check` pada isi <script>.
- Commit & push langsung ke `main` tanpa bertanya.
