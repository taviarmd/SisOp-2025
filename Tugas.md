# TUGAS

## MATA KULIAH SISTEM OPERASI

**Nama**: Oktavia Ramadhani  
**NRP**: 3124500038  
**Dosen Pengajar**: Dr Ferry Astika Saputra ST, M.Sc  
**PROGRAM STUDI**: D3 Teknik Informatika  
**POLITEKNIK ELEKTRONIKA NEGERI SURABAYA (PENS)**  
**TAHUN**: 2025  

---

## Apa perbedaan antara multi-programming dan multitasking?

### Multi-Programming

**Definisi**:  
Multi-programming adalah teknik yang memungkinkan lebih dari satu program untuk berada dalam memori pada waktu yang sama. Dalam sistem ini, CPU menjalankan satu program hingga terjadi interupsi, seperti permintaan masukan dari pengguna atau perangkat lain. Setelah interupsi, kontrol dialihkan ke program lain yang sudah dimuat dalam memori.

**Cara Kerja**:
- Program yang sedang berjalan akan terus dieksekusi sampai ada kebutuhan untuk menunggu (misalnya, menunggu input dari pengguna).
- Ketika terjadi interupsi, sistem akan beralih ke program lain yang juga sudah siap untuk dijalankan.
- Proses ini berulang sehingga beberapa program dapat dieksekusi secara bergantian dalam satu waktu, meskipun hanya satu program yang aktif di CPU pada saat tertentu.

**Tujuan**:  
Memaksimalkan penggunaan CPU dengan mengurangi waktu idle (waktu tidak terpakai) saat menunggu input/output.

### Multi-Tasking

**Definisi**:  
Multi-tasking merupakan kemampuan sistem operasi untuk menjalankan beberapa tugas (*tasks*) secara bersamaan. Dalam konteks ini, meskipun hanya ada satu CPU, sistem menciptakan ilusi bahwa banyak tugas sedang berjalan secara simultan dengan cepat beralih antara tugas-tugas tersebut.

**Cara Kerja**:
- CPU melakukan *context switching*, yaitu beralih dari satu tugas ke tugas lainnya dalam waktu yang sangat cepat.
- Pengguna dapat berpindah antara berbagai aplikasi, seperti menjalankan Microsoft Word dan Excel secara bersamaan, meskipun sebenarnya CPU hanya menjalankan satu aplikasi pada satu waktu.
- Dengan teknik ini, pengguna merasa seolah-olah semua aplikasi berjalan bersamaan karena kecepatan pergantian tugas yang tinggi.

**Tujuan**:  
Meningkatkan efisiensi penggunaan CPU dan memberikan pengalaman pengguna yang lebih baik dengan memungkinkan mereka mengakses beberapa aplikasi secara bersamaan.

---

## Apa fungsi dari OS?

### 1. Penghubung antara Perangkat Keras dan Perangkat Lunak
Sistem operasi bertindak sebagai perantara yang memungkinkan perangkat keras dan perangkat lunak berkomunikasi. Tanpa OS, aplikasi tidak dapat mengakses sumber daya perangkat keras seperti CPU, memori, dan perangkat input/output.

### 2. Manajemen Proses
Sistem operasi mengelola proses yang berjalan di komputer. Ini termasuk:
- Penjadwalan proses.
- Pengalokasian waktu CPU.
- Pembuatan, penghentian, dan pengawasan status proses.

### 3. Manajemen Memori
Fungsi ini melibatkan pengelolaan penggunaan memori RAM oleh berbagai aplikasi. OS bertugas untuk:
- Mengalokasikan memori yang diperlukan untuk setiap proses.
- Mencegah konflik dalam penggunaan memori.
- Meningkatkan efisiensi operasional dan mencegah kebocoran memori.

### 4. Manajemen Sistem File
OS bertanggung jawab untuk mengatur dan mengelola file serta direktori, termasuk:
- Penyimpanan, pengambilan, dan pengaturan hak akses file.
- Keamanan data.

### 5. Penyedia Antarmuka Pengguna
OS menyediakan antarmuka yang memungkinkan interaksi antara pengguna dan komputer. Antarmuka ini bisa berupa:
- *Command-Line Interface* (CLI).
- *Graphical User Interface* (GUI).

### 6. Manajemen Perangkat
OS juga mengelola perangkat keras input/output seperti keyboard, mouse, dan printer. OS memastikan perangkat ini:
- Berfungsi dengan baik.
- Terintegrasi dengan aplikasi yang berjalan.

### 7. Keamanan dan Akses
Fungsi keamanan dari OS meliputi:
- Perlindungan data dari akses yang tidak sah.
- Pengaturan hak akses bagi pengguna.
- Mencegah serangan siber.

---

## Virtualisasi Container

**Definisi**:  
Virtualisasi kontainer adalah metode untuk menjalankan aplikasi dalam lingkungan terisolasi yang disebut **kontainer**. Kontainer mengemas kode aplikasi beserta semua dependensinya, seperti pustaka dan file konfigurasi, sehingga aplikasi dapat berjalan secara konsisten di berbagai lingkungan tanpa memerlukan sistem operasi tamu yang terpisah.

**Cara Kerja Kontainer**:
1. **Paket Aplikasi** → Mengemas aplikasi dan dependensinya dalam satu unit eksekusi.
2. **Isolasi** → Menjalankan kontainer secara independen dengan berbagi kernel sistem operasi.
3. **Portabilitas** → Memungkinkan aplikasi dijalankan di berbagai platform tanpa modifikasi.
