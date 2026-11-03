# ASCII Camera Color

Webcam jadi ASCII art berwarna, langsung di browser. Satu file HTML, tanpa library.

## Jalankan

Kamera hanya bisa diakses lewat `localhost` atau https, jadi jangan buka file langsung.

```bash
python -m http.server 5200
```

Buka `http://localhost:5200`, lalu izinkan kamera.

## Mode warna

| Mode | Hasil |
|------|-------|
| Warna asli | Karakter diwarnai sesuai pixel kamera |
| Warna vivid | Sama, saturasi dinaikkan |
| Blok warna | Latar tiap sel ikut diwarnai, paling mirip foto |
| Matrix hijau | Hijau gelap ke neon mengikuti terang-gelap |
| Hitam putih | ASCII klasik |
| Hijau-Biru-Merah | Tiga panel warna solid, karakter putih |

## Kontrol

- **Karakter**: Detail 70, Standar 10, Padat, Blok `░▒▓█`, Biner `01`
- **Kolom**: 60–400. Makin banyak, makin detail
- **Kontras**: naikkan supaya area gelap kosong dan bentuk lebih tegas
- **Invert, Mirror, Bg putih**
- **Snapshot PNG, Pause, Fullscreen**

## Cara kerja

1. Frame kamera diperkecil ke grid `kolom × baris`, 1 pixel = 1 karakter.
2. Kecerahan tiap pixel memilih karakter dari ramp (tipis ke tebal).
3. Satu baris karakter digambar sekaligus ke canvas sebagai layer putih.
4. Layer itu diwarnai sekali jalan dengan `source-in` memakai gambar warna yang di-scale tanpa smoothing.

Render sekitar 5 ms per frame di 220 kolom.
