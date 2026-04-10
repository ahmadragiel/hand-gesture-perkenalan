# 🖐️ Hand Gesture Recognition — Perkenalan Nama

Project computer vision berbasis **gesture tangan** untuk memperkenalkan diri secara interaktif menggunakan webcam. Setiap gesture tangan yang ditunjukkan akan memunculkan teks dan suara dalam Bahasa Indonesia secara real-time.

---

## 📸 Demo

> Tunjukkan gesture tangan ke kamera → teks muncul di layar → suara otomatis berbunyi

---

## ✨ Fitur

- 🖐️ Deteksi hingga **2 tangan** secara bersamaan
- 🤲 **Kombinasi 2 tangan** menghasilkan kalimat yang berbeda dari gesture tunggal
- 🔊 **Text-to-Speech** otomatis (Bahasa Indonesia) dengan sistem cache audio
- 🤏 Deteksi **16 gesture** berbeda — 8 gesture 1 tangan + 8 kombinasi 2 tangan
- 📋 **Panduan gesture on-screen** — tekan `g` untuk toggle tampilan panduan
- 🏷️ **Badge mode** — indikator `SINGLE HAND` / `DUAL HAND` di layar
- 📷 **Auto-detect kamera** — otomatis fallback ke index kamera lain jika gagal
- ⏱️ **Cooldown system** agar audio tidak spam
- 🧠 Palm detection cerdas menggunakan 3 metode: brightness, depth, dan normal vector
- 🐛 Debug overlay: tampilkan status jari per tangan secara real-time

---

## 🤟 Daftar Gesture

> Urutan jari: **[Jempol, Telunjuk, Tengah, Manis, Kelingking]** — `1` = terbuka, `0` = tertutup

### ✋ Gesture 1 Tangan

| Gesture | Kode Jari | Output |
|---|---|---|
| ✊ Kepalan | `(0,0,0,0,0)` | *"Halo!"* |
| ☝️ Telunjuk | `(0,1,0,0,0)` | *"Nama saya..."* |
| ✌️ Peace | `(0,1,1,0,0)` | *"Ahmad Ragiel Zaini"* |
| 🤟 Rock | `(0,1,0,0,1)` | *"Senang bertemu kalian!"* |
| 👍 Jempol | `(1,0,0,0,0)` | *"Sip!"* |
| 🖐️ Buka semua | `(1,1,1,1,1)` | *"Halo semuanya!"* |
| 🤙 Shaka | `(1,1,0,0,1)` | *"EZ!"* |
| 👋 4 jari | `(0,1,1,1,1)` | *"Salam kenal ya!"* |

### 🤲 Kombinasi 2 Tangan

| Tangan Kiri | Tangan Kanan | Output |
|---|---|---|
| ✊ Kepalan `(0,0,0,0,0)` | ☝️ Telunjuk `(0,1,0,0,0)` | *"Perkenalkan, nama saya..."* |
| ✌️ Peace `(0,1,1,0,0)` | ✌️ Peace `(0,1,1,0,0)` | *"Ahmad Ragiel Zaini!"* |
| 👍 Jempol `(1,0,0,0,0)` | 🖐️ Buka semua `(1,1,1,1,1)` | *"Terima kasih sudah mendengarkan!"* |
| 🖐️ Buka semua `(1,1,1,1,1)` | 🖐️ Buka semua `(1,1,1,1,1)` | *"Semoga kita bisa berteman!"* |
| ☝️ Telunjuk `(0,1,0,0,0)` | 👍 Jempol `(1,0,0,0,0)` | *"Saya siap belajar bersama kalian!"* |
| ✌️ Peace `(0,1,1,0,0)` | ☝️ Telunjuk `(0,1,0,0,0)` | *"Hai, apa kabar?"* |
| 🖐️ Buka semua `(1,1,1,1,1)` | ✊ Kepalan `(0,0,0,0,0)` | *"Yuk kita mulai!"* |
| 🤟 Rock `(0,1,0,0,1)` | ✌️ Peace `(0,1,1,0,0)` | *"Dengan senang hati berkenalan!"* |

---

## 🎯 Alur Perkenalan yang Disarankan

Urutan gesture untuk presentasi perkenalan yang natural:

1. 🖐️ **Buka semua** (kanan) → *"Halo semuanya!"*
2. ✊👉 **Kepalan kiri + Telunjuk kanan** → *"Perkenalkan, nama saya..."*
3. ✌️✌️ **Peace kedua tangan** → *"Ahmad Ragiel Zaini!"*
4. 🤟 **Rock** (kanan) → *"Senang bertemu kalian!"*
5. 👍🖐️ **Jempol kiri + Buka semua kanan** → *"Terima kasih sudah mendengarkan!"*

---

## 🛠️ Teknologi yang Digunakan

- [Python 3.8+](https://www.python.org/)
- [OpenCV](https://opencv.org/) — capture & display kamera
- [MediaPipe](https://mediapipe.dev/) — deteksi landmark tangan
- [gTTS](https://pypi.org/project/gTTS/) — Google Text-to-Speech
- [Pygame](https://www.pygame.org/) — playback audio
- [NumPy](https://numpy.org/) — kalkulasi vektor palm detection

---

## ⚙️ Instalasi

### 1. Clone repository
```bash
git clone https://github.com/ahmadragiel/hand-gesture-perkenalan.git
cd hand-gesture-perkenalan
```

### 2. Install dependencies
```bash
pip install opencv-python mediapipe==0.10.13 gtts pygame numpy
```

> ⚠️ Gunakan `mediapipe==0.10.13` — versi terbaru tidak kompatibel dengan `mp.solutions`.

### 3. Jalankan program
```bash
python gerakan.py
```

> Pastikan webcam terhubung sebelum menjalankan program.

---

## 📁 Struktur Project

```
hand-gesture-perkenalan/
│
├── gerakan.py          # Main program — deteksi gesture & TTS
├── test_kamera.py      # Utility untuk test koneksi kamera
├── audio_cache/        # Cache file audio TTS (auto-generated)
└── README.md
```

---

## 🚀 Cara Penggunaan

1. Jalankan `gerakan.py`
2. Arahkan tangan ke kamera
3. Tunggu **3 detik** setelah tangan terdeteksi (countdown muncul di layar)
4. Tunjukkan gesture sesuai tabel di atas
5. Teks dan suara akan muncul otomatis
6. Tekan **`g`** untuk toggle panduan gesture di layar
7. Tekan **`q`** untuk keluar

---

## 📝 Catatan

- Pastikan pencahayaan ruangan **cukup terang** agar deteksi lebih akurat
- Gunakan **latar belakang kontras** dengan warna kulit untuk hasil terbaik
- File audio di-cache di folder `audio_cache/` — bisa dihapus manual jika ingin generate ulang
- Program otomatis mencoba index kamera `0–3` jika kamera utama tidak terdeteksi
- Untuk gesture 2 tangan, program memprioritaskan **kombinasi dual hand** sebelum fallback ke gesture tunggal

---

## 👤 Author

**Ahmad Ragiel Zaini**

---