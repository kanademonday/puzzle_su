# Puzzle SU — catatan untuk Claude (baca ini dulu, jangan baca seluruh index.html)

Repo khusus `kanademonday/puzzle_su` (terpisah dari landing_otomatis). Aplikasi 1 berkas: `index.html` di root repo (HTML+CSS+JS murni, tanpa library, tanpa API berbayar, jalan offline).
Tujuan: menyusun gambar SU (surat ukur) sebagai potongan puzzle per **peta analog**, untuk membayangkan
lokasi bidang yang sudah / belum landing di Bhumi ATR. Bahasa UI & jawaban: **Bahasa Indonesia**.

## Model data (IndexedDB `puzzleSU`, store: `peta`, `bidang`, `img`, `antrian`)
- peta: `{id, nama, dibuat}`
- bidang: `{id, petaId, no, status:'landing'|'belum', luas, nib, su, catatan, img, poly:[[x,y]..] (px gambar),
  c:[x,y] pusat poly (px), s: meter per px (= sqrt(luas/luas_px)), x,y: posisi pusat di dunia (meter), rot (radian),
  kunci, tetangga:[{no,x,y}] (px gambar), diubah}`
- img: `{id, data: dataURL JPEG}`
- antrian (SU yang menunggu digitasi): `{id, nama, petaNama, su, tahun, luas, no, sekitar:[], img, thumb, status, pesan, dibuat}`
- Nomor dibandingkan dengan `norm()` (huruf besar, tanpa spasi).

## Peta kode di index.html (cari judul bagian `/* ===== ... ===== */`)
- UTIL, GEOMETRI (`keDunia`, `keLokal`, `pusat`, `luasPoly`)
- PENYIMPANAN (IndexedDB, `ambilGambar`)
- DATA: `infoTetangga()` → `{ada, kosong, garis}`; `letakkanOtomatis()` → posisi awal bidang baru
- PUZZLE: `draw()`, interaksi pointer (geser, putar via handle, snap titik sudut), `fit()`
- PANEL SAMPING: `renderSide()`
- EDITOR SU: mode batas / tetangga / geser, popup nomor tetangga, tombol Simpan (`#eSave`)
- SUSUN GLOBAL: `susunTata(daftar,bebas)` (kendala dari semua nomor tetangga + dorong tumpang-tindih SAT `mtv`, putaran tetap, bidang terkunci = patokan), `susunSemua()`, `kembalikanPerkiraan(b)`, undo `S.undoTata`/`batalTata()`, opsi `S.opt.autoSusun`
- EDITOR juga: mode potong (`potong()`, undo via `E.stack`), popup nomor tetangga otomatis OK saat klik tempat lain, chip saran `E.saran`
- BANYAK SU: `masukkanBanyak()` → `prosesSatu()` (pdf.js, nama file `bacaNamaFile`, AI berantai Groq→Gemini→OpenRouter→Ollama `panggilAI`/`panggilProv`, penyedia penuh dicatat di `penuh{}` lalu pindah; kunci di localStorage `plotkw.ai` (sama dengan landing_otomatis), aktif/nonaktif di `puzzleSU.aiAktif`; `bacaUlang()` tombol ↻)
- DAFTAR SU: `bukaDaftar()`/`renderDaftar()` (semua bidang + antrian, pencarian), `cekNama()` hanya baca nama file → `#cekMasuk` memasukkan yang baru ke antrian; kunci duplikat dari `petaSUada()`
- BAYANGAN: nomor tetangga tanpa SU jadi kotak bayangan (`peta.bayangan`, `posKosong()`, `ukuranBayangan()`), ikut disusun di `susunTata` tapi tidak mendorong bidang asli
- DUPLIKAT SU: `kunciBidang()` (pemisah / \ - . spasi), `kunciSemuaBidang()` (No.SU + nama file + catatan), peringatan saat simpan `E.konfSU`
- MODE LANDING (tingkat 1 merah muda, 2 ungu, 3 hijau toska, berhenti di 3, `hubung()`): `kandidatLanding()` (jarak poligon ≤ `TOL_DEMPET` m atau saling tercatat sebagai tetangga di SU), tombol `#btnLanding`
- KE AUTOCAD: `lispBidang()` (entmake LWPOLYLINE+TEXT, Y dibalik), `salinGambar()`, `simpanGambar()` (JPG + world file .jgw untuk MAPIINSERT)
- EKSPOR/IMPOR: JSON cadangan (gabung berdasarkan nomor + `diubah` terbaru), DXF R12 (Y dibalik, meter lokal), CSV, PNG

## Aturan kerja
- Ubah dengan Edit kecil pada bagian yang relevan; jangan menulis ulang seluruh berkas.
- Setelah ubah: cek sintaks dengan `node --check` pada isi <script>.
- Commit & push langsung ke `main` tanpa bertanya.
