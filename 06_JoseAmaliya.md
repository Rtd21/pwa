1. Konsep Wireless Computing & Teknologi Mobile
Dalam dunia pengembangan aplikasi, Wireless Computing bukan sekadar tentang "tanpa kabel", tapi tentang bagaimana aplikasi Anda bisa tetap cerdas meskipun berpindah-pindah tempat. Papan tulis tersebut menyoroti tiga jalan utama (Teknologi Mobile) yang bisa diambil oleh pengembang:
--Teknologi Native: Ini adalah cara "asli". Jika Anda membuat aplikasi Android dengan bahasa Kotlin atau iOS dengan Swift, Anda sedang berada di jalur ini. Hasilnya sangat cepat dan punya akses penuh ke "jeroan" HP (seperti sensor gerak, kamera, hingga NFC) tanpa hambatan.
--Teknologi Hybrid: Ini adalah jalan tengah. Pengembang hanya perlu menulis satu kode (biasanya menggunakan web teknologi) lalu dibungkus agar bisa diinstal seperti aplikasi biasa. Lebih hemat biaya, tapi ada sedikit penurunan performa karena aplikasi harus berkomunikasi lewat "penerjemah".
--Progressive Web Apps (PWA): Ini sebenarnya adalah website yang sangat canggih sehingga terlihat dan terasa seperti aplikasi. Tidak perlu download di Playstore, cukup buka lewat browser, tapi fitur akses ke hardware-nya sangat terbatas.

2. Memahami Framework PREP
Di papan tulis Anda, FW PREP (Framework PREP) digunakan sebagai struktur berpikir untuk menentukan pilihan teknologi mana yang akan dipakai. Framework ini membantu pengembang agar tidak asal pilih teknologi hanya karena sedang tren. Begini cara kerjanya:
--Point (P): Langsung pada intinya. Tentukan posisi atau keputusan teknis yang akan diambil. Misalnya: "Kita akan menggunakan jalur Native."
--Reason (R): Berikan alasan teknis yang kuat. Kenapa Native? Mungkin karena aplikasi yang dibuat butuh pengolahan grafis tinggi atau fitur AR/VR (seperti yang tertulis di bagian bawah papan).
--Example (E): Berikan bukti nyata atau perbandingan performa. Di papan tulis ada poin mengenai "Akses Hardware" dan "Performa". Di sini Anda menjelaskan bahwa jika pakai Hybrid, akses ke fitur tertentu (seperti NFC) mungkin akan lambat atau tidak stabil.
--Point (P): Kesimpulan akhir. Mengunci keputusan bahwa dengan pertimbangan biaya, waktu, dan fitur, teknologi tertentu adalah yang paling pas.

3. Penjelasan Detail Poin di Papan Tulis
Jika kita bedah tulisan tangan yang ada di foto, dosen Anda ingin menekankan beberapa poin krusial dalam pengambilan keputusan:
--Akses Hardware: Ini adalah pembeda utama. Di kolom Native tertulis "Full NFC, Cam". Artinya, kalau aplikasi Anda sangat bergantung pada sensor, jangan pakai Web/PWA karena keterbatasannya sangat tinggi.
--Distribusi: Jalur Native dan Hybrid punya keunggulan di sisi "gengsi" dan kepercayaan karena bisa muncul di Playstore atau App Store, sedangkan PWA hanya lewat link.
--Kasus Khusus (Game & AR/VR): Perhatikan tulisan di bagian bawah. Untuk teknologi masa depan seperti Game AR/VR, dosen Anda memberi catatan bahwa Native adalah pilihan utama. Ini karena teknologi tersebut butuh "tenaga" maksimal dari prosesor dan baterai yang hanya bisa didapat lewat jalur Native.

Secara garis besar, materi ini mengajarkan bahwa tidak ada teknologi yang "terbaik" secara mutlak. Yang ada hanyalah teknologi yang paling cocok dengan kebutuhan fitur, ketersediaan biaya, dan target waktu rilis aplikasi tersebut.
