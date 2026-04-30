## 1. Arsitektur Sistem Operasi Mobile (4 Lapisan)

**Point (Pernyataan Utama)**
Arsitektur Sistem Operasi Mobile dirancang dalam bentuk tumpukan (stack) yang terdiri dari empat lapisan hierarkis: *Kernel, Libraries, Framework*, dan *Application*, yang berfungsi sebagai jembatan penghubung antara perangkat keras fisik dengan pengguna akhir.

**Reason (Alasan)**
Pembagian lapisan ini diterapkan untuk menciptakan abstraksi sistem yang aman dan efisien. Lapisan paling bawah (*Kernel*) fokus mengatur perangkat keras tingkat rendah, sedangkan lapisan di atasnya menyediakan kumpulan instruksi terkompilasi (*Libraries*), kerangka kerja standar untuk *developer* (*Framework*), hingga lapisan teratas yang berinteraksi langsung dengan *user* (*Application*).

**Example (Contoh)**
Ketika pengguna membuka aplikasi kamera **(Application)**, aplikasi tersebut tidak langsung menyalakan lensa fisik. Ia meminta akses melalui *Camera API* **(Framework)**. API ini kemudian memanggil modul pemrosesan gambar berbasis C/C++ **(Libraries)**, yang pada akhirnya memberikan instruksi ke *Linux Kernel* **(Kernel)** untuk mengaktifkan perangkat keras kamera.

**Point (Penegasan Ulang)**
Dengan demikian, keempat lapisan ini saling bersinergi secara runtut dari atas ke bawah untuk memastikan aplikasi mobile dapat berjalan secara stabil dan dapat memanfaatkan *hardware* secara optimal.

***

## 2. Perbedaan Keamanan Mobile OS vs Desktop OS

**Point (Pernyataan Utama)**
Sistem Operasi Mobile memiliki tingkat keamanan bawaan yang jauh lebih ketat dibandingkan Desktop OS berkat penerapan mekanisme isolasi yang dikenal dengan istilah *Sandboxing*.

**Reason (Alasan)**
Pada sistem operasi *desktop* konvensional seperti Windows, banyak aplikasi berjalan dengan hak akses pengguna yang luas, sehingga rentan memodifikasi sistem *file* utama. Sebaliknya, OS mobile seperti Android dan iOS mengurung setiap aplikasi di dalam ruang virtualnya sendiri (*sandbox*). Aplikasi tidak dapat saling membaca data, mencuri memori, atau mengakses perangkat keras tanpa mendapatkan izin (*permission*) secara eksplisit dari pengguna.

**Example (Contoh)**
Jika Anda mengunduh sebuah aplikasi kalkulator sederhana di *smartphone*, aplikasi tersebut (yang berada di dalam *sandbox*) tidak akan bisa membaca daftar kontak, galeri foto, atau menyadap pesan. Ia harus memunculkan *pop-up* persetujuan terlebih dahulu. Berbeda dengan aplikasi *desktop* biasa yang terkadang bisa membaca *file* di *drive* lain tanpa peringatan.

**Point (Penegasan Ulang)**
Kesimpulannya, pendekatan *sandboxing* dan manajemen izin yang ketat inilah yang membuat arsitektur iOS dan Android jauh lebih tangguh dalam menahan penyebaran *malware* dibandingkan dengan lingkungan OS *desktop* pada umumnya.

***

## 3. Hierarki Proses Android

**Point (Pernyataan Utama)**
Untuk menjaga performa dan daya baterai, Android mengelola memori sistem (RAM) dengan membagi proses aplikasi ke dalam lima hierarki prioritas: *Foreground, Visible, Service, Background*, dan *Empty Process*.

**Reason (Alasan)**
Karena perangkat *mobile* memiliki memori yang terbatas, OS Android membutuhkan aturan baku untuk menentukan proses mana yang harus "dibunuh" (dimatikan) terlebih dahulu saat memori penuh. Sistem akan selalu mengorbankan proses dengan prioritas terendah untuk memberikan ruang bagi aplikasi yang sedang aktif digunakan pengguna.

**Example (Contoh)**
*   **Foreground Process:** Game berat yang sedang Anda mainkan di layar saat ini (Prioritas tertinggi, sangat jarang dimatikan).
*   **Visible Process:** Aplikasi yang masih terlihat di layar, misalnya *pop-up dialog* yang muncul di atas aplikasi lain.
*   **Service Process:** Aplikasi pemutar musik yang sedang memutar lagu di latar belakang, atau proses sinkronisasi RDBMS di *background*.
*   **Background Process:** Aplikasi kalkulator atau *browser* yang baru saja Anda tekan tombol *home*, sehingga masuk ke *task manager*.
*   **Empty Process:** Proses yang sudah tidak memiliki komponen aplikasi aktif, hanya disimpan di memori *cache* untuk mempercepat proses buka-ulang (Prioritas terendah, paling pertama dimatikan sistem).

**Point (Penegasan Ulang)**
Melalui kelima hierarki ini, Android secara cerdas dan otomatis menyeimbangkan ketersediaan sumber daya perangkat keras tanpa mengganggu pengalaman utama pengguna.

***

## 4. Intent pada Android

**Point (Pernyataan Utama)**
*Intent* pada Android adalah objek perpesanan (mekanisme komunikasi) yang digunakan untuk meminta sebuah aksi dari komponen aplikasi lain, yang secara umum terbagi menjadi dua jenis: *Intent Eksplisit* dan *Intent Implisit*.

**Reason (Alasan)**
*Intent Eksplisit* digunakan ketika *developer* sudah mengetahui secara pasti nama kelas atau komponen tujuan yang akan dipanggil (umumnya berada di dalam satu aplikasi yang sama). Di sisi lain, *Intent Implisit* tidak menyebutkan komponen tujuan secara spesifik, melainkan hanya mendeklarasikan "aksi" apa yang ingin dilakukan, sehingga sistem operasi akan mencarikan aplikasi yang cocok untuk menangani aksi tersebut.

**Example (Contoh)**
*   **Contoh Intent Eksplisit:** Di dalam aplikasi buatan Anda, ketika pengguna mengklik tombol "Profil", Anda menggunakan intent ini untuk berpindah dari kelas `BerandaActivity` menuju `ProfilActivity`.
*   **Contoh Intent Implisit:** Aplikasi Anda ingin membuka sebuah tautan (URL). Anda menggunakan intent dengan `ACTION_VIEW`. Sistem Android kemudian akan memunculkan *pop-up* pilihan *browser* yang ada di perangkat Anda (misalnya Chrome, Brave, atau *browser* bawaan) untuk membuka tautan tersebut.

**Point (Penegasan Ulang)**
Singkatnya, *Intent Eksplisit* ideal untuk navigasi internal aplikasi yang terstruktur, sedangkan *Intent Implisit* adalah kunci kolaborasi dinamis antar berbagai aplikasi di dalam ekosistem Android.

***

## 5. Perbandingan Native App, Hybrid App, dan PWA

| Aspek Perbandingan | Native App (Aplikasi Asli) | Hybrid / Cross-Platform App | Progressive Web App (PWA) |
| :--- | :--- | :--- | :--- |
| **Akses Hardware** | Akses penuh & optimal (Kamera, GPS, Sensor, dll). | Cukup baik, bergantung pada ketersediaan *plugin/bridge*. | Terbatas, hanya fitur yang didukung oleh API *Browser* web. |
| **Performa** | Sangat Tinggi & responsif. | Menengah hingga Tinggi (sedikit *overhead* komputasi). | Menengah (bergantung pada mesin *browser* dan koneksi awal). |
| **Biaya & Waktu** | Sangat Mahal & Lama (butuh 2 kode terpisah: Swift untuk iOS, Kotlin untuk Android). | Efisien (Satu *codebase* untuk iOS dan Android). | Sangat Murah (Pada dasarnya adalah *website* yang dioptimalkan). |
| **Distribusi** | Play Store & App Store. | Play Store & App Store. | Melalui *link URL/Browser* (tanpa instalasi *store*). |
| **Pilihan Tepat Untuk** | Game berat (grafis tinggi), aplikasi dengan animasi kompleks. | Aplikasi sistem informasi, E-commerce, manajemen basis data. | Portal berita, katalog ringan, aplikasi web transisi. |

***

## Kesimpulan: Solusi Aplikasi Inventaris dengan Budget Terbatas

Jika ingin mengembangkan aplikasi inventaris untuk Android dan iOS dengan status **budget terbatas**, pilihan terbaik adalah menggunakan pendekatan **Hybrid App** (seperti menggunakan *framework* Flutter atau React Native).

**Alasannya:**
Aplikasi inventaris umumnya berfokus pada manajemen basis data (seperti operasi *Create, Read, Update, Delete* dari MariaDB/PostgreSQL) dan tidak memerlukan pemrosesan grafis tingkat tinggi seperti sebuah *mobile game*. Dengan pendekatan Hybrid:
1.  **Efisiensi Biaya dan Waktu:** Anda hanya perlu menulis satu basis kode (*single codebase*), yang dapat langsung di-*build* menjadi aplikasi Android (`.apk`/`.aab`) maupun iOS (`.ipa`). Hal ini menghemat biaya pengembang hingga 50%.
2.  **Fungsionalitas Terpenuhi:** Kebutuhan *hardware* dasar untuk aplikasi inventaris (seperti akses kamera untuk *scan barcode* atau QR Code) sudah sangat didukung oleh ekosistem *plugin* pada aplikasi Hybrid.
3.  **Pengalaman Pengguna (UX):** Meskipun lebih murah, aplikasi Hybrid masih bisa didistribusikan secara resmi melalui Play Store dan App Store, memberikan kesan profesional kepada pengguna layaknya aplikasi *Native*.

*(Sebagai opsi sekunder, jika tidak wajib masuk App Store/Play Store, membangun ekosistem berbasis **PWA** juga merupakan langkah logis bagi mahasiswa atau developer web yang ingin aplikasinya diakses multi-platform tanpa biaya registrasi developer Apple/Google).*
