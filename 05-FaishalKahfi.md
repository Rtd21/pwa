1. Manajemen Proses dan Memori (Pendalaman LMK & OOM Score)
Point: LMK sebenarnya tidak hanya mengategorikan aplikasi dalam 3 level, melainkan menggunakan sistem skoring matematis yang sangat granular bernama OOM Adjustment Score (oom_adj_score) di level kernel (inti sistem).

Reason: Setiap proses yang berjalan diberi nilai skor dinamis oleh OS. Semakin tinggi skornya, semakin besar kemungkinannya untuk "dibunuh" saat RAM penuh. Hierarki prioritas aslinya meliputi:

Foreground (Skor terendah/aman mutlak).

Visible Process (Aplikasi tidak tertutup penuh, misal terhalang keyboard atau pop-up dialog).

Service Process (Latar belakang yang sedang aktif, seperti download file).

Cached Process (Tersimpan di RAM tapi diam).

Empty Process (Aplikasi sudah ditutup penuh, tetapi "wadah/cangkang"-nya disisakan di RAM agar besok jika dibuka lagi, loading-nya lebih instan).

Example: Pemutar musik Spotify di latar belakang masuk ke kategori Service Process. Namun, karena ia menampilkan widget kontrol di bilah notifikasi (Foreground Service Notification), OS memberinya perlakuan khusus dengan menekan skor oom_adj-nya agar setara dengan Foreground. Saat RAM krisis karena Anda membuka game berat, OS akan memenggal proses Empty dan Cached secara berurutan. Spotify akan tetap hidup, kecuali RAM benar-benar sudah habis tanpa sisa.

Point: LMK adalah kalkulasi matematis real-time yang memastikan proses yang langsung dilihat dan didengar oleh pengguna akan selalu dilindungi, sementara proses "zombie" dikorbankan.

2. Komunikasi Antar Proses (Pendalaman Arsitektur Binder & Makelar Data)
Point: Interaksi antar sandbox aplikasi tidak pernah terjadi secara langsung. OS bertindak sebagai "Makelar" atau perantara mutlak menggunakan arsitektur level bawah (seperti penggerak Binder di Android) dan Intent Filters.

Reason: Membiarkan dua aplikasi berbagi memori (shared memory) adalah mimpi buruk keamanan. Ketika Aplikasi A ingin data dari Aplikasi B, ia tidak bisa "mengetuk pintu" Aplikasi B. Aplikasi A harus mengirim pesan berformat khusus (Intent) ke OS. OS akan memverifikasi hak akses (permissions), dan jika lolos, OS sendirilah yang akan mengekstrak data dari Aplikasi B untuk diserahkan ke Aplikasi A.

Example: Saat Anda menggunakan fitur "Login with Google" di aplikasi pihak ketiga (misal: Tokopedia). Tokopedia melempar Explicit Intent ke OS. OS membangunkan komponen otentikasi Google. Anda mengetik password di halaman Google (sehingga Tokopedia tidak bisa mengintip tombol yang Anda tekan). Setelah sukses, Google menitipkan "Token Enkripsi" ke OS, lalu OS yang menyerahkan token tersebut kembali ke Tokopedia.

Point: Sistem IPC dengan model makelar (Broker) ini memastikan komponen bisa saling melayani dengan mulus tanpa mengorbankan isolasi keamanan kriptografi dari masing-masing sandbox.

3. Eksekusi Latar Belakang (Pendalaman Constraints & Penghapusan AlarmManager)
Point: WorkManager berevolusi dari penjadwalan berbasis waktu statis (Time-based) menjadi penjadwalan sadar lingkungan (Context-Aware / Constraint-based).

Reason: Di masa lalu, pengembang menggunakan AlarmManager untuk memaksa HP bangun setiap 1 jam untuk mengecek pesan baru. Ini sangat menghancurkan baterai. Di OS modern, pengembang dilarang menggunakan cara itu. Sebagai gantinya, mereka menyerahkan tugas ke WorkManager dengan mendaftarkan "Syarat" (Constraints). OS yang akan memonitor sensor perangkat keras secara pasif dan mengeksekusi tugas hanya jika syarat terpenuhi bersamaan.

Example: Aplikasi Google Photos ingin mencadangkan ribuan foto resolusi tinggi ke server. Pengembang menyetel constraints: NetworkType.UNMETERED (hanya Wi-Fi), RequiresCharging (sedang dicas), dan DeviceIdle (HP tidak sedang dimainkan). OS akan menahan tugas ini berjam-jam. Begitu Anda tidur, menancapkan charger, dan Wi-Fi terhubung, barulah trigger internal OS meledak dan menginstruksikan WorkManager untuk mengunggah semuanya sekaligus.

Point: Integrasi ini mengubah cara aplikasi bekerja: dari yang awalnya agresif menuntut sumber daya, menjadi tunduk pada jadwal kolektif yang ditentukan oleh sistem operasi.

4. Keamanan Data (Pendalaman DE vs CE Storage & TEE)
Point: File-Based Encryption (FBE) yang sempurna membagi memori HP menjadi dua zona kriptografi: Device Encrypted (DE) dan Credential Encrypted (CE), yang dikunci oleh sirkuit perangkat keras terpisah (seperti Trusted Execution Environment / Secure Enclave).

Reason: Enkripsi DE (Terenkripsi Perangkat) kuncinya dirilis otomatis oleh OS saat HP menyala (boot). Ruang ini hanya berisi file esensial untuk fungsi dasar (kode aplikasi Telepon, Alarm). Sebaliknya, ruang CE (Terenkripsi Kredensial) berisi data pribadi (pesan, foto). Kunci ruang CE ini digembok mati di chip hardware khusus. OS bahkan tidak bisa melihat kuncinya sebelum Anda memasukkan PIN yang benar.

Example: Jika seorang peretas ahli mencuri HP Anda, membongkarnya, dan mencabut chip memorinya untuk dibaca di komputer (Chip-off attack), ia hanya akan melihat lautan kode acak. Tanpa otorisasi chip keamanan fisik yang mengonfirmasi ketukan PIN Anda di layar, data di ruang CE secara matematis mustahil untuk direkonstruksi menjadi foto atau teks.

Point: Keamanan FBE modern adalah pertahanan berlapis (perangkat lunak + perangkat keras) yang mengisolasi data paling rahasia bahkan dari mata sistem operasi itu sendiri ketika perangkat dalam status terkunci.

5. Manajemen Baterai (Pendalaman WakeLocks & Deep Doze)
Point: OS bertindak ekstrem untuk memperpanjang daya dengan memblokir permintaan WakeLocks secara otomatis dan memaksakan sinkronisasi lewat Deep Doze.

Reason: WakeLock adalah perintah dari aplikasi ke CPU yang berbunyi: "Jangan tidur, saya masih kerja". Dulu, satu aplikasi cacat yang lupa mematikan WakeLock bisa membuat baterai HP habis di dalam saku celana. OS modern kini dengan tegas mengabaikan WakeLock reguler saat masuk Deep Doze. OS menonaktifkan antena GPS, memblokir akses internet semua aplikasi, dan menunda semua tugas latar belakang. Jendela pemeliharaan (maintenance window) pun dibuat eksponensial (awalnya bangun setiap 1 jam sekali, turun menjadi 2 jam sekali, lalu 6 jam sekali jika HP tidak disentuh sama sekali).

Example: Bayangkan ada 5 aplikasi berbeda (Instagram, Twitter, Email, Cuaca, Game) yang ingin mengambil data dari server setiap 5, 8, 12, 15, dan 20 menit. Jika diizinkan, radio seluler HP akan terus menyala. Melalui Doze, OS mencekal mereka semua, membariskan permintaannya, dan memaksa kelimanya untuk mengakses internet secara serentak di menit ke-60 selama tepat 10 detik, lalu memaksa mereka semua tidur kembali.

Point: Pemusatan eksekusi (batching) dan pencekalan WakeLock ini secara radikal menghilangkan "kebisingan" CPU dan radio seluler, menyelamatkan daya tahan baterai secara masif.

6. Timeout & ANR (Pendalaman Main Thread vs Worker Thread)
Point: Peringatan Application Not Responding (ANR) sangat terikat pada tenggat waktu matematis per-bingkai (frame rendering time) yang wajib dipenuhi oleh aplikasi di Main Thread (Jalur Utama).

Reason: Layar HP modern di-refresh 60 hingga 120 kali per detik. Artinya, sistem operasi hanya mengizinkan Main Thread untuk berpikir dan menggambar piksel selama 8 hingga 16 milidetik per frame. Jika pengembang yang buruk menaruh proses berat (seperti mengambil gambar 5MB dari internet atau memuat database ribuan kontak) di Main Thread, proses tersebut memakan waktu 3000 ms (3 detik). Selama 3 detik itu, siklus 16 milidetik terlewat berkali-kali, menyebabkan antarmuka "membeku" (lag/freeze). Jika pembekuan menembus 5 detik, mekanisme pengawas OS (Watchdog timer) akan membunyikan alarm ANR.

Example: Aplikasi belanja yang dirancang dengan baik akan melempar tugas mengambil foto produk ke Background/Worker Thread (jalur belakang). Di Main Thread, aplikasi cukup menampilkan animasi bundar berputar (animasi ringan yang selesai dalam 5 milidetik). Saat Worker Thread selesai mengunduh foto di jalur belakang, ia mengetuk Main Thread: "Ini fotonya, tolong gambarkan di layar". Layar pun tidak pernah membeku sedetik pun.

Point: Mekanisme ANR bukan sekadar penghukum aplikasi rusak, melainkan standar arsitektur paksa yang mendikte pengembang untuk selalu memisahkan "proses komputasi/jaringan" dari "proses menggambar layar visual".
