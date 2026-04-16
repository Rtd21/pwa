1. Manajemen Proses dan Memori (Low Memory Killer)
Sistem operasi mobile memiliki sumber daya memori (RAM) yang sangat terbatas. Untuk mencegah sistem crash, OS menggunakan mekanisme yang disebut Low Memory Killer (LMK) atau Out-Of-Memory (OOM) Killer. Saat RAM mulai penuh, sistem operasi akan mengurutkan aplikasi dan proses yang sedang berjalan berdasarkan prioritas kepentingannya, lalu "membunuh" (menghentikan) proses dari prioritas paling rendah untuk membebaskan RAM.

Urutan prioritas dari yang paling aman hingga yang paling pertama dihentikan adalah:

Foreground (Prioritas Tertinggi): Proses aplikasi yang sedang tampil di layar dan sedang berinteraksi langsung dengan pengguna. OS akan mengalokasikan sumber daya maksimal agar aplikasi ini tidak tertutup tiba-tiba.

Background (Prioritas Menengah): Proses yang berjalan di latar belakang, namun sedang menjalankan tugas krusial yang disadari oleh pengguna. Contohnya: navigasi peta yang sedang menuntun jalan atau pemutar musik yang sedang aktif. Proses ini dilindungi agar layanannya tidak terputus.

Cache / Cached Process (Prioritas Terendah): Aplikasi yang sebelumnya dibuka lalu ditutup atau diminimalkan (masuk Home). Aplikasi ini sengaja dibiarkan "membeku" di RAM agar jika pengguna membukanya kembali, proses loading menjadi lebih cepat. Namun, jika OS membutuhkan memori darurat untuk aplikasi Foreground, proses Cache inilah yang akan "dibunuh" paling pertama.

2. Komunikasi Antar Proses (Inter-Process Communication / IPC)
Setiap aplikasi di mobile OS berjalan di dalam "ruang isolasi" masing-masing (disebut Sandboxing) untuk alasan keamanan, sehingga aplikasi A tidak bisa sembarangan membaca data aplikasi B. Agar aplikasi bisa saling berinteraksi, OS menyediakan jalur IPC khusus, salah satunya menggunakan mekanisme Intent. Intent adalah objek pesan yang digunakan untuk meminta tindakan dari komponen lain.

Terdapat dua jenis eksekusi Intent:

Intent Eksplisit (Explicit Intent): Digunakan saat pengembang sudah tahu secara spesifik aplikasi atau komponen mana yang ingin dijalankan. (Misal: Kode di dalam aplikasi menekan tombol untuk membuka halaman ActivityLogin internal milik aplikasi itu sendiri).

Intent Implisit (Implicit Intent): Digunakan saat pengembang hanya mendeklarasikan tindakan (aksi) yang ingin dilakukan, tanpa peduli aplikasi apa yang akan mengerjakannya. OS akan mencari dan menawarkan aplikasi yang mendukung aksi tersebut. (Misal: Aplikasi melempar perintah "Baca tag NFC", maka OS akan membangunkan aplikasi apapun di HP tersebut yang memiliki izin dan kemampuan membaca NFC).

3. Eksekusi Latar Belakang dan Paradigma Event-Driven
WorkManager: Ini adalah komponen sistem yang bertugas menangani pekerjaan latar belakang (background tasks) yang sifatnya wajib selesai (guaranteed execution), meskipun pengguna sudah menutup aplikasi atau bahkan jika perangkat baru saja di-restart. Biasanya digunakan untuk sinkronisasi data penting atau mengunggah file ke server.

Event-Driven: Sistem operasi mobile menggunakan paradigma pemrograman berbasis kejadian (event). Aplikasi tidak mengeksekusi kode secara terus-menerus (yang akan menguras CPU), melainkan dalam mode "tidur" hingga terjadi sebuah event. Event ini bisa berupa ketukan jari di layar, notifikasi masuk, atau perubahan orientasi HP. Saat event terjadi, barulah aplikasi "bangun" untuk meresponsnya.

4. Keamanan Data (File-Based Encryption / FBE)
FBE adalah standar enkripsi modern di mobile OS. Alih-alih mengenkripsi seluruh penyimpanan fisik ponsel sebagai satu kesatuan (Full-Disk Encryption), FBE mengenkripsi setiap file secara individu menggunakan kunci (key) yang berbeda-beda.
Keuntungan utamanya adalah mendukung fitur Direct Boot. Jika HP Anda mati lalu menyala kembali (restart), Anda biasanya belum memasukkan PIN. Berkat FBE, file sistem operasi dasar tetap bisa diakses sehingga HP tetap bisa berdering saat ada panggilan masuk atau alarm berbunyi, sementara file foto, pesan, dan data pribadi Anda tetap terkunci rapat secara kriptografi hingga Anda memasukkan PIN.

5. Manajemen Baterai dan Optimasi Layanan
OS mobile sangat ketat dan agresif dalam mengelola daya baterai agar HP bisa bertahan seharian.

Aplikasi Aktif vs. Pasif: Aplikasi yang berjalan terus-menerus secara "Aktif" (menggunakan Services untuk mengecek lokasi atau data secara konstan) akan menguras baterai dengan cepat.

Oleh karena itu, OS modern menerapkan optimasi otomatis seperti fitur Doze Mode atau App Standby. Jika HP diletakkan di meja dengan layar mati selama beberapa waktu, OS akan memaksa aplikasi masuk ke mode "Pasif". Dalam mode ini, akses aplikasi ke CPU dan internet diputus, dan OS hanya akan memberi "jendela waktu" sesekali agar aplikasi bisa melakukan sinkronisasi sejenak sebelum ditidurkan kembali.

6. Antrean Eksekusi dan Batas Waktu Waktu (Timeout / ANR)
Sistem operasi mengelola berbagai tugas dari berbagai aplikasi menggunakan antrean proses (Task Stack atau Thread Queue). Agar perangkat seluler tetap responsif, sistem memberikan batasan waktu toleransi (timeout) untuk setiap operasi yang berjalan di proses utama (main thread / UI thread).
Jika sebuah aplikasi melakukan kalkulasi berat atau download file di main thread dan memakan waktu terlalu lama (misalnya membeku lebih dari 10 detik), sistem akan mencegatnya dan menampilkan peringatan Application Not Responding (ANR). Peringatan ini melindungi pengguna dari aplikasi yang hang, memberikan mereka keleluasaan untuk mematikan paksa (force close) aplikasi tersebut.
