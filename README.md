# 101 Recorder — Perekam

Satu halaman statis (`index.html`) yang di-host di **luar** Google Apps Script
(GitHub Pages). Google tidak memberi izin mikrofon di bingkai tempat semua web
app Apps Script jalan, jadi app `recorder-101/` membuka halaman ini di tab baru,
di sini mikrofon dipakai, lalu audionya dikirim BALIK ke app lewat
`postMessage` — app itulah yang mengunggahnya ke Drive orang yang merekam.

- Tidak ada server, tidak ada yang disimpan di GitHub. Audio cuma ada di HP
  (IndexedDB, cadangan) dan di Drive.
- Audio hanya dikirim ke asal `…-script.googleusercontent.com` (dari `?asal=`).
  App hanya menerima dari asal halaman ini (`PEREKAM_URL` di `recorder-101/Code.gs`).
- Cadangan di HP dibuang HANYA sesudah app menjawab `aman: true` — yaitu
  sesudah app sendiri menyimpannya ke IndexedDB.

## Terbitkan / perbarui

Salin `index.html` ke repo GitHub Pages (publik), lalu isi `PEREKAM_URL` di
`recorder-101/Code.gs` dengan alamatnya dan deploy app itu.

## Uji lokal

Dua asal berbeda, supaya jalur antar-asal teruji sungguhan:
`recorder-101/make-local.py` (app, localhost:8781, `perekam` = 127.0.0.1:8782)
dan halaman ini disajikan di `127.0.0.1:8782`. Browser pratinjau membuka
`window.open` di tab yang SAMA, jadi untuk uji, perekam dimuat sebagai iframe
di atas app dengan `window.opener` = induknya. Langkah `window.open` itu sendiri
hanya bisa dibuktikan di HP.
