# Puzzle SU – Peta Analog

Aplikasi web offline untuk menyusun gambar SU menjadi puzzle per peta analog, supaya terbayang letak
bidang yang **sudah** dan **belum** landing di Bhumi ATR.

## Cara pakai singkat
1. Buka `index.html` di Chrome/Edge (klik dua kali) atau lewat GitHub Pages.
2. **+ Bidang dari SU** → pilih/ketik nama peta analog → unggah gambar SU.
3. Mode **Batas bidang**: klik sudut-sudut bidang, klik titik pertama untuk menutup.
4. Isi **nomor pendaftaran** (isi sendiri bila tidak tertulis), status landing, luas (agar ukuran sebanding).
5. Mode **Nomor tetangga**: klik tiap nomor pendaftaran di sekitar bidang, ketik nomornya.
6. Simpan. Tetangga yang belum punya SU muncul sebagai lingkaran abu-abu; saat SU nomor itu dimasukkan,
   bidangnya otomatis diletakkan di tempat tanda tersebut.
7. Di puzzle: seret untuk geser, tarik bulatan biru untuk putar (Shift = per 15°), Q/E putar 1°, panah = geser halus,
   klik dua kali bidang = edit.

Data tersimpan di browser masing-masing. Untuk berbagi dengan tim: **Data ▸ Cadangkan (.json)** lalu
rekan memakai **Data ▸ Impor**. Ekspor **DXF** menghasilkan poligon dalam meter lokal (belum TM-3), siap dipindah/diputar di AutoCAD.
