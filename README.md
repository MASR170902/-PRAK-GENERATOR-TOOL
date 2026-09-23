# 📚 Laporan Praktikum AI Generator (Multi-Provider Edition)

Generator otomatis berbasis AI untuk menyusun Laporan Praktikum teknis dari dokumen Modul dan Foto hasil praktikum. Output langsung berupa file **Microsoft Word (.docx)** yang sudah terstruktur dengan rapi. Dikembangkan oleh MASR.

Versi terbaru ini berjalan **100% Client-Side di browser**. Tidak ada backend atau proxy perantara. Keamanan privasi terjamin karena dokumen dan API Key Anda dikirim langsung ke penyedia layanan AI.

## ✨ Fitur Utama
* **Multi-Provider & Universal API:** Mendukung ekosistem AI terlengkap mulai dari Anthropic (Claude), OpenAI (ChatGPT), Google Gemini, Groq, OpenRouter, hingga Local LLM.
* **100% Privacy & Client-Side:** API Key dan file dokumen hanya diproses di memori lokal browser Anda (tersimpan aman di `localStorage`).
* **Direct to DOCX:** Generator lokal tanpa *library* eksternal untuk mengubah output AI langsung menjadi file Word siap pakai.
* **Auto Humanizer & Auto Anti-Slop:** Mesin prompt khusus yang memaksa model AI untuk menulis dengan gaya bahasa manusia natural, menghindari kata-kata klise (seperti *menyelami*, *permadani*, *lanskap*), dan langsung fokus pada inti teknis.
* **Native PDF Support:** Kemampuan membaca file PDF secara langsung (khusus untuk provider Anthropic/Claude).

---

## 🟢 Panduan Pengguna (User Awam)

Jika Anda hanya ingin langsung menggunakan tool ini dengan API Key yang Anda miliki (misalnya dari OpenAI atau Anthropic), ikuti langkah berikut:

1. Buka file `index.html` di browser Anda, atau akses link GitHub Pages tempat tool ini di-*hosting*.
2. Pilih **Provider AI** yang ingin Anda gunakan pada menu *dropdown* (misal: `OpenAI (ChatGPT)` atau `Anthropic (Claude)`).
3. Kolom **Endpoint URL** dan **ID Model AI** akan terisi otomatis. Anda bisa mengganti ID Model jika ingin menggunakan versi lain (misal dari `gpt-4o` ke `gpt-4o-mini`).
4. Masukkan **API Key** Anda. Data ini akan tersimpan di browser agar Anda tidak perlu mengetiknya ulang setiap saat.
5. Upload file **Modul Praktikum**. *(Catatan: Gunakan format Gambar JPG/PNG jika Anda memilih OpenAI. Gunakan PDF/Gambar jika Anda memilih Anthropic).*
6. Upload **Foto Hasil Praktikum** (Bukti *screenshot* atau foto perangkat).
7. Klik **🚀 Generate Laporan** dan tunggu hingga file `.docx` terunduh secara otomatis.

---

## 🔴 Panduan Pengguna Tingkat Lanjut (Pro & Local Server)

Bagi pengembang atau pengguna *Home Lab* yang ingin menjalankan model AI secara lokal sepenuhnya (tanpa biaya API) menggunakan mesin seperti **Ollama**, **LM Studio**, atau **vLLM**.

### Menggunakan Local AI (Ollama / LM Studio)
1. Jalankan server lokal Anda (misalnya Ollama).
2. Pilih **Local AI (Ollama / LM Studio)** pada menu *dropdown* Provider.
3. Pastikan **Endpoint URL** mengarah ke server lokal Anda (standarnya `http://localhost:11434/v1/chat/completions`).
4. Ketikkan nama model yang sudah Anda unduh di kolom **ID Model AI** (contoh: `llava`, `llama3.2-vision`, atau `qwen2.5`).
5. Kosongkan kolom **API Key**.

**⚠️ Penting untuk Pengguna Ollama (CORS Issue):**
Karena tool ini berjalan di browser klien dan melakukan *fetch* ke `localhost`, Anda wajib mengizinkan CORS pada sistem operasi yang menjalankan Ollama.
* **Linux/Proxmox LXC:** Edit service systemd (`systemctl edit ollama.service`) dan tambahkan `Environment="OLLAMA_ORIGINS=*"` di bawah `[Service]`, lalu restart service.
* **Windows/macOS:** Set *environment variable* `OLLAMA_ORIGINS="*"` sebelum meluncurkan aplikasi Ollama.

### Menggunakan Custom Provider / API Gateway Sendiri
Jika Anda memiliki *endpoint* API Gateway kustom (seperti Cloudflare AI Gateway atau AWS Bedrock *proxy*):
1. Pilih **Custom Provider**.
2. Ganti URL bawaan dengan URL *endpoint* kustom Anda.
3. Masukkan ID Model yang dikonfigurasi di *gateway* tersebut.
4. Sistem pengiriman *payload* akan beradaptasi secara otomatis tergantung format dasar (*Anthropic* atau *OpenAI*) dari opsi Custom yang Anda pilih.

---

--------------------------------------CREATOR BY MASR---------------------------------------------------------------------