# HapsyLash
Automated Booking & Studio Management System

Instruksi/project portfolio: Studi kasus sistem reservasi perawatan kecantikan (*eyelash extension & academy*) yang dikembangkan untuk digitalisasi pemesanan jadwal, otomatisasi pembayaran Down Payment (DP), serta manajemen operasional studio. Dilengkapi fitur manajemen slot jam kerja, program loyalitas pelanggan, dan dashboard analitik. Source code dibatasi untuk mematuhi NDA dan menjaga kerahasiaan data operasional studio serta privasi pelanggan. Halaman ini berfokus pada studi kasus, arsitektur sistem, dan penyelesaian masalah (*problem solving*).

> **Disclaimer Kerahasiaan (NDA):**  
> Repository ini adalah dokumentasi portofolio dari proyek sistem reservasi studio kecantikan. Demi mematuhi *Non-Disclosure Agreement* (NDA) dan menjaga kerahasiaan data finansial bisnis serta privasi data pribadi pelanggan (sesuai UU PDP), data riil, kredensial produksi, dan metrik keuangan sensitif tidak dipublikasikan. Halaman ini berfokus pada studi kasus rekayasa perangkat lunak, arsitektur sistem, dan dampak efisiensi bisnis.

---

# Latar Belakang Proyek

Studio kecantikan dan kursus *eyelash* membutuhkan sistem yang efisien untuk mengatur jadwal janji temu pelanggan, pembayaran uang muka (*down payment*), dan pelacakan program loyalitas. Sebelumnya, proses pemesanan dilakukan secara manual melalui pesan WhatsApp. Hal ini menimbulkan sejumlah kendala:
- **Resiko *Double-Booking*:** Sering terjadi tabrakan jadwal antarpelanggan karena pencatatan manual di buku agenda atau chat.
- **Tingginya Angka *No-Show* (Ghost Booking):** Pelanggan yang membatalkan janji temu secara sepihak di hari-H karena tidak adanya komitmen uang muka yang terverifikasi otomatis.
- **Beban Administrasi:** Waktu admin habis hingga 15–20 menit hanya untuk mengecek ketersediaan jam kerja dan memverifikasi bukti transfer bank satu per satu.
- **Pencatatan Poin Loyalitas yang Rentan Hilang:** Penggunaan kartu stempel manual sering tertinggal, rusak, atau hilang oleh pelanggan.

**HapsyLash** dibangun sebagai aplikasi web modern (*Modern Monolith Single Page Application*) untuk mendigitalisasi alur pemesanan secara mandiri (*self-service booking*), memverifikasi pembayaran DP via QRIS secara *real-time*, mengunci ketersediaan slot jam kerja studio, dan mengelola data retensi pelanggan secara otomatis.

---

# Peran & Tanggung Jawab

Dalam proyek ini, saya dipercaya penuh sebagai **Fullstack Web Developer** untuk merancang arsitektur sistem, merancang basis data, hingga mengimplementasikannya ke antarmuka pengguna yang interaktif. Tanggung jawab utama saya meliputi:

- **Pengembangan Backend & Logika Sistem:** Membangun arsitektur aplikasi berbasis **Laravel 12 (PHP)**, mengelola logika transaksi pemesanan, pembatalan otomatis pesanan yang kedaluwarsa, dan *event-listener* untuk pengiriman konfirmasi jadwal.
- **Integrasi Payment Gateway (Midtrans Snap):** Mengintegrasikan sistem pembayaran QRIS  dengan mekanisme notifikasi *asynchronous* (Webhook) yang aman guna memverifikasi DP secara otomatis tanpa campur tangan admin.
- **Desain & Implementasi Frontend (UI/UX):** Merancang antarmuka yang bersih, responsif, dan elegan menggunakan **React 18**, **Tailwind CSS**, dan **Inertia.js**, memberikan transisi antarhalaman yang instan tanpa *page reload*.
- **Visualisasi Data & Dashboard Operasional:** Mengembangkan dashboard interaktif untuk pemilik studio menggunakan **Recharts** guna memantau tren reservasi, pendapatan harian, dan layanan terpopuler.
- **Manajemen Basis Data & Relasi:** Merancang skema tabel relasional pada **PostgresSQL** untuk menangani entitas pelanggan, jadwal kerja, riwayat reservasi, add-on layanan, serta akumulasi poin loyalitas.
- **Privasi & Keamanan Data:** Merancang sistem verifikasi riwayat pesanan pelanggan berbasis nomor WhatsApp dengan otentikasi PIN Tanggal Lahir (DOB), sehingga pelanggan dapat mengecek jadwalnya secara privat tanpa perlu mendaftar akun berulang kali.

---

# Teknologi yang Digunakan (Tech Stack)

- **Backend:** PHP 8.2+, Laravel 12 Framework (Eloquent ORM, Events & Queue)
- **Frontend & SPA Bridge:** React 18, Inertia.js v2
- **Styling & Komponen UI:** Tailwind CSS, Headless UI, Sonner (Toast Notification)
- **Payment Gateway:** Midtrans Snap API (QRIS)
- **Data Visualization & Media:** Recharts (Interactive Analytics), React-Image-Crop, React-Quill
- **Generasi Dokumen:** Barryvdh Laravel DomPDF (Kwitansi / Invoice PDF)
- **Database & Local Tooling:** PostgreSQL, TablePlus, Laravel Pail, Concurrently

---

# Fitur Utama

- **Reservasi Mandiri & Kalkulasi Add-on Otomatis:** Pelanggan dapat memilih treatment, opsi tambahan (seperti *lash remover* atau serum vitamin), dan sistem langsung mengkalkulasi total durasi pengerjaan serta biaya DP.
- **Pembayaran DP Instan (QRIS & E-Wallet):** Notifikasi pembayaran terverifikasi dalam hitungan detik dengan batas waktu kedaluwarsa 15 menit untuk mencegah penimbunan slot jadwal.
- **Manajemen Jam Kerja & Slot Blackout:** Admin studio dapat mengatur jam operasional harian serta menutup (*blackout*) tanggal atau jam tertentu sewaktu-waktu jika studio libur.
- **Portal Cek Pesanan & Program Loyalitas:** Pelanggan dapat memeriksa riwayat booking dan status voucher/reward gratis treatment berdasarkan akumulasi jumlah kunjungan.
- **Dashboard Analitik & Rekap Reservasi:** Visualisasi grafik performa studio, konversi booking, dan ekspor kwitansi digital resmi berformat PDF.

---

# Dampak & Hasil (Impact)

Berikut adalah penyelesaian masalah utama (*problem solving*) yang berhasil dicapai melalui sistem ini:

- **Efisiensi Waktu Pemesanan:**
  - *Sebelumnya:* Proses tanya jawab jadwal dan verifikasi bukti transfer memakan waktu rata-rata 15 hingga 20 menit per pelanggan di chat WhatsApp.
  - *Sesudah:* Pelanggan dapat memilih jadwal dan menyelesaikan pembayaran DP mandiri dalam waktu **kurang dari 2 menit**.
- **Pencegahan Risiko Double-Booking (Zero Schedule Collision):**
  - *Sebelumnya:* Rentan terjadi dua pelanggan memesan jam yang sama akibat kelalaian pencatatan manual di jam sibuk.
  - *Sesudah:* Sistem secara otomatis mengunci slot waktu begitu transaksi DP terverifikasi, **menghilangkan 100% risiko tabrakan jadwal**.
- **Penurunan Angka Pembatalan Sepihak (*Ghost Bookings*):**
  - *Sebelumnya:* Banyak pelanggan tidak hadir (*no-show*) karena tidak ada uang muka yang mengikat.
  - *Sesudah:* Pemberlakuan DP wajib via QRIS yang otomatis membatalkan pesanan yang tidak dibayar dalam 15 menit, memastikan hanya pelanggan serius yang memesan slot.
- **Digitalisasi Poin Loyalitas & Retensi Pelanggan:**
  - *Sebelumnya:* Kartu stempel fisik sering hilang atau lupa dibawa pelanggan, sehingga menyulitkan evaluasi program promo.
  - *Sesudah:* Jumlah kunjungan terakumulasi otomatis ke database nomor pelanggan, meningkatkan *repeat-order* dan kepuasan pelanggan secara transparan.

---

# Tampilan Antarmuka Sistem

- **Halaman Pemesanan, Pemilihan Treatment Pelanggan, DOB Pin**
  <img width="1470" height="956" alt="image" src="https://github.com/user-attachments/assets/b1f31969-1bb0-41bb-9712-7e3a32865e59" />
  <img width="1470" height="956" alt="image" src="https://github.com/user-attachments/assets/b369fdb2-62a0-45b0-affe-132308adcc8f" />
  <img width="1470" height="956" alt="image" src="https://github.com/user-attachments/assets/5e285407-e180-4b5e-a4c7-cb292982c93a" />
  <img width="1470" height="956" alt="image" src="https://github.com/user-attachments/assets/44fcbff8-fd62-49e9-9015-2425112c5f86" />

- **Modal Pembayaran DP (Midtrans QRIS)**
  <img width="2940" height="1912" alt="Untitled design" src="https://github.com/user-attachments/assets/ff4cbc51-b192-4893-956c-152f79b9d3e4" />

- **Dashboard Analitik & Monitoring Jadwal Admin Studio**
  <img width="1470" height="956" alt="image" src="https://github.com/user-attachments/assets/6f1bb581-fb9b-433c-99fd-369043c158df" />

- **Kwitansi Digital / Invoice PDF**
  <img width="1470" height="956" alt="image" src="https://github.com/user-attachments/assets/0e818ffd-787b-4b13-912d-4b2428ac603d" />

