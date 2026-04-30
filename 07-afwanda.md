Soal Latihan Wireless & Mobile Computing
1. Konsep Dasar Mobility (Modul 1 & 2) Jelaskan mengapa sebuah perangkat yang terhubung ke Wi-Fi di dalam ruangan statis disebut sebagai wireless tetapi tidak selalu dianggap mobile. Dalam konteks tersebut, apa risiko teknis yang terjadi jika sebuah koneksi suara (voice call) mengalami Hard Handoff saat pengguna mulai berpindah tempat?
2. Standar Jaringan (Modul 3) Sebutkan perbedaan standar IEEE yang digunakan untuk teknologi Bluetooth (WPAN) dan Wi-Fi (WLAN). Mengapa pada area publik yang sangat luas, penggunaan Infrastructure Mode jauh lebih disarankan dibandingkan dengan Ad-Hoc Mode?
3. Arsitektur dan Keamanan OS (Modul 4) Sistem operasi mobile menerapkan konsep Sandboxing yang lebih ketat dibandingkan sistem operasi desktop. Analisis mengapa kebijakan ini sangat krusial bagi keamanan data pribadi pengguna dan jelaskan pada lapisan (layer) mana dalam arsitektur 4 lapis pengaturan hak akses ini biasanya dikelola.
4. Mekanisme Kerja Android (Modul 5) Seorang pengembang aplikasi ingin membuat fitur "Bagikan Foto" di mana aplikasinya dapat memanggil aplikasi pihak ketiga (seperti WhatsApp atau Instagram) tanpa menentukan aplikasi mana yang akan terbuka secara spesifik. Jenis Intent apa yang harus digunakan? Jelaskan pula apa yang akan terjadi pada hirarki proses Android jika aplikasi tersebut dipindahkan oleh sistem ke kategori Cached Process.
5. Studi Kasus Strategi Pengembangan (Modul 6) Sebuah perusahaan rintisan (startup) memiliki dana terbatas dan ingin segera meluncurkan aplikasi inventaris yang bisa diakses baik oleh pengguna Android maupun iOS.
•	Strategi pengembangan mana (Native, Hybrid, atau PWA) yang paling efektif untuk kasus ini?
•	Berikan alasan teknis dan ekonomis di balik pemilihan strategi tersebut berdasarkan perbandingan efisiensi kode dan biaya.




Kunci Jawaban & Pembahasan
1. Konsep Dasar Mobility (Modul 1 & 2)
•	Wireless vs Mobile: Perangkat disebut wireless karena menggunakan medium transmisi tanpa kabel (seperti sinyal radio), namun tidak selalu mobile jika penggunaannya tetap berada di satu titik (statis). Mobile menekankan pada kemampuan pengguna atau layanan untuk tetap terhubung saat berpindah tempat.
•	Risiko Hard Handoff: Karena bersifat "break-before-make", koneksi lama diputus sebelum koneksi baru tersambung. Risikonya adalah terjadi jeda suara atau pemutusan koneksi sesaat yang mengganggu kualitas panggilan suara (tidak seamless).
2. Standar Jaringan (Modul 3)
•	Standar IEEE: WPAN (Bluetooth) menggunakan standar IEEE 802.15, sedangkan WLAN (Wi-Fi) menggunakan standar IEEE 802.11.
•	Infrastructure vs Ad-Hoc: Pada area luas, Infrastructure Mode lebih disarankan karena menggunakan Access Point terpusat untuk mengatur lalu lintas data dan jangkauan, sementara Ad-Hoc bersifat peer-to-peer yang sulit dikelola dan jangkauannya sangat terbatas jika perangkat saling menjauh.
3. Arsitektur dan Keamanan OS (Modul 4)
•	Pentingnya Sandboxing: Sandboxing di mobile lebih ketat karena perangkat mobile menyimpan data yang sangat sensitif (GPS, kontak, privasi). Dengan sandbox, satu aplikasi tidak bisa mengakses data aplikasi lain atau sistem secara ilegal, sehingga meminimalkan dampak serangan.
•	Lapisan Pengaturan: Pengaturan ini umumnya dikelola pada Arsitektur 4 Lapisan (terutama pada Kernel dan Middleware/Runtime) yang memisahkan ruang eksekusi tiap aplikasi.
4. Mekanisme Kerja Android (Modul 5)
•	Jenis Intent: Harus menggunakan Implicit Intent. Dengan ini, sistem akan mencarikan aplikasi yang mampu menangani aksi "Bagikan" dan memberikan pilihan kepada pengguna.
•	Cached Process: Jika aplikasi masuk ke kategori Cached Process, aplikasi tersebut tidak lagi aktif digunakan dan berada di urutan terbawah hirarki kepentingan. Jika sistem membutuhkan memori (RAM), proses ini akan menjadi yang pertama untuk dihentikan (terhapus dari memori).
5. Studi Kasus Strategi Pengembangan (Modul 6)
•	Strategi Terpilih: Hybrid atau PWA adalah yang paling efektif untuk budget terbatas.
•	Alasan Ekonomis: Biaya lebih murah karena hanya memerlukan satu basis kode (single codebase) untuk dijalankan di Android dan iOS sekaligus, sehingga tidak perlu menyewa dua tim pengembang yang berbeda.
•	Alasan Teknis: Efisiensi kode lebih tinggi dalam hal pemeliharaan (maintenance), karena perubahan fitur hanya perlu dilakukan pada satu tempat namun langsung berdampak pada kedua platform.
