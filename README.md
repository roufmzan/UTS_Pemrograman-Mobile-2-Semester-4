# Tugasku

Aplikasi Android untuk membantu kamu mengelola **tugas** dan **catatan materi** dengan pengalaman yang modern. Tugasku juga mendukung fitur **rekam audio** lalu menghasilkan **transkrip & ringkasan otomatis** menggunakan AI (Gemini), sehingga materi bisa tersimpan lebih rapi dan mudah dicari.

## Fitur

- **Manajemen Tugas**
  - Tambah, lihat, dan kelola daftar tugas.

- **Catatan Materi**
  - Buat dan edit catatan manual.
  - **Auto-save** saat menulis catatan (lebih aman dari kehilangan draft).
  - **Pencarian real-time** di halaman Catatan Materi (filter judul & isi).

- **Audio to Notes (AI)**
  - Rekam audio dari aplikasi.
  - Menghasilkan **transkrip** dan **ringkasan**.
  - Simpan hasil ringkasan ke catatan.

## Tech Stack

- **Android** (Java)
- **AndroidX**
- **RecyclerView**
- **Material Components**
- **OkHttp** (request ke Gemini API)
- **WorkManager** (proses ringkasan background)
- **SharedPreferences** (penyimpanan lokal catatan)

## Persiapan Project

### Prasyarat

- Android Studio (disarankan versi terbaru)
- Android SDK sesuai target project

### Konfigurasi API Key (Gemini)

Project ini menggunakan API key untuk akses Gemini.

- **Jangan commit API key ke GitHub**.
- Simpan API key di `local.properties` (disarankan) atau gunakan cara aman lain.

#### Opsi yang disarankan: `local.properties`

Tambahkan:

```properties
GEMINI_API_KEY=ISI_API_KEY
```

Lalu pastikan `build.gradle.kts` membaca nilai tersebut dan memasukkannya ke `BuildConfig`.

Catatan: Jika project kamu saat ini sudah memakai `buildConfigField("String", "GEMINI_API_KEY", ...)`, pastikan value-nya tidak hardcoded di repo publik.

## Cara Menjalankan

1. Clone repo:

```bash
git clone https://github.com/<username>/<repo>.git
```

2. Buka project di Android Studio.

3. Pastikan API key sudah dikonfigurasi (lihat bagian **Konfigurasi API Key**).

4. Sync Gradle.

5. Run aplikasi ke emulator / device.

## Catatan Penting

- **Pencarian Catatan** bekerja dengan memfilter daftar catatan berdasarkan **judul** atau **isi**.
- Penyimpanan catatan menggunakan **SharedPreferences**, cocok untuk kebutuhan sederhana. Jika skala data membesar, pertimbangkan migrasi ke Room database.

## Struktur Singkat

- `app/src/main/java/com/example/tugasku/`
  - `NotesActivity.java` — halaman Catatan Materi + pencarian
  - `NoteAdapter.java` — adapter RecyclerView + filter
  - `AddNoteActivity.java` — tambah/edit catatan + auto-save
  - `AudioRecordActivity.java` — rekam audio + waveform
  - `AudioResultActivity.java` — tampilan hasil transkrip & ringkasan
  - `GeminiSummarizeWorker.java` — ringkasan background via WorkManager
  - `NoteManager.java`, `AudioNoteManager.java` — persistensi lokal
