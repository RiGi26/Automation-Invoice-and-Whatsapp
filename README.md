# 🚀 Automated Course Registration & Invoicing System

Sistem otomasi *end-to-end* berbasis cloud untuk menangani pendaftaran siswa baru, pembuatan invoice profesional, dan notifikasi WhatsApp secara *real-time*. Dibangun menggunakan **Google Apps Script (GAS)** untuk efisiensi biaya dan integrasi penuh dengan ekosistem Google Workspace.

![Project Status](https://img.shields.io/badge/Status-Production-success)
![Platform](https://img.shields.io/badge/Platform-Google_Apps_Script-blue)

## 📋 Overview

Proyek ini dibuat untuk memangkas waktu administrasi manual dari 10-15 menit per siswa menjadi **0 detik (Instan)**. Sistem secara otomatis memproses data dari Google Form, memvalidasi syarat diskon yang kompleks, menghasilkan Invoice PDF, dan mengirimkannya via WhatsApp.

**Studi Kasus:** Diterapkan pada pendaftaran Bimbel Bahasa Jepang dengan logika harga dinamis.

## ✨ Fitur Unggulan

* **🛡️ Concurrency Handling (Lock Service):** Dilengkapi dengan mekanisme antrian (`LockService`) untuk mencegah tabrakan data (*race condition*) dan duplikasi nomor invoice saat terjadi lonjakan pendaftar secara bersamaan.
* **📄 Dynamic PDF Generation:** Membuat file PDF Invoice dengan desain custom (HTML/CSS) yang rapi, lengkap dengan kop surat dan tanda tangan digital. Nama file dibuat dinamis sesuai nama peserta.
* **💸 Smart Pricing Logic:** Algoritma diskon bertingkat yang memvalidasi multiple-conditions (contoh: Wajib centang 3 syarat sosmed + Pembayaran Full) menggunakan logika `AND/OR` yang ketat.
* **📱 WhatsApp Gateway Integration:** Terintegrasi dengan API Fonnte untuk mengirim pesan personal dan melampirkan file Invoice PDF langsung ke nomor WhatsApp pendaftar.
* **📂 Auto-Archiving:** Invoice yang dibuat otomatis tersimpan di folder Google Drive yang terorganisir, dan link-nya tercatat di Google Sheet.

## 🛠️ Alur Kerja Sistem (Workflow)

1.  **Input:** Calon siswa mengisi Google Form.
2.  **Trigger:** Script mendeteksi submit baru -> Mengaktifkan `LockService` (Antrian).
3.  **Processing:**
    * Validasi input & normalisasi nomor WhatsApp.
    * Kalkulasi harga berdasarkan Kelas & Syarat Diskon.
    * Generate Nomor Invoice Unik (Format: `N3/S5/2026/001`).
4.  **Output:**
    * Render HTML ke PDF -> Upload ke Google Drive.
    * Kirim pesan WhatsApp + Attachment PDF.
    * Update status "TERKIRIM" di Google Sheet.
5.  **Release:** Melepas kunci antrian untuk pendaftar berikutnya.

## 💻 Tech Stack

* **Language:** JavaScript (Google Apps Script)
* **Database:** Google Sheets
* **Storage:** Google Drive
* **API:** Fonnte (WhatsApp Gateway), UrlFetchApp
* **Styling:** HTML5 & CSS3 (Inline for PDF rendering)

---
*Dikembangkan untuk solusi bisnis UMKM/Pendidikan.*
