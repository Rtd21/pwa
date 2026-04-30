
---

### **P1: Fondasi - Wireless vs Mobile Computing**

**PREP:**

**Point:** Perbedaan mendasar Wireless dan Mobile Computing terletak pada fokusnya: Wireless = media transmisi, Mobile = perpindahan device.

**Reason:** Wireless Computing hanya membahas cara data dikirim tanpa kabel, tetapi device bisa tetap diam. Sedangkan Mobile Computing menekankan mobilitas device/user yang berpindah lokasi tanpa kehilangan koneksi.

**Example:** Wireless saja = CCTV WiFi di rumah (tidak berpindah). Mobile saja = laptop pindah ruangan tapi pakai LAN. Keduanya = HP 4G yang bisa internet sambil bergerak.

**Point:** Jadi, semua Mobile Computing pasti Wireless, tapi Wireless belum tentu Mobile.

---

### **P2: Mobilitas - Hard vs Soft Handoff**

**PREP:**

**Point:** Soft Handoff lebih unggul dibanding Hard Handoff untuk komunikasi real-time seperti voice call.

**Reason:** Hard Handoff bekerja dengan metode “break before make” (putus dulu baru sambung), sehingga ada jeda yang bisa menyebabkan gangguan suara. Sedangkan Soft Handoff menggunakan “make before break” (sambung dulu baru putus), sehingga koneksi tetap stabil.

**Example:** Saat telepon di perjalanan, suara tetap lancar karena jaringan modern menggunakan Soft Handoff. Pada sistem lama (GSM), sering terjadi suara terputus saat pindah tower.

**Point:** Jadi, Soft Handoff lebih ideal untuk layanan yang membutuhkan koneksi kontinu.

---

### **P3: Jaringan - WPAN/WLAN/WMAN/WWAN + IEEE**

**PREP:**

**Point:** Standar IEEE membedakan jaringan berdasarkan jangkauan dan arsitektur koneksi.

**Reason:** IEEE 802.15 (WPAN) untuk jarak dekat, 802.11 (WLAN) untuk jaringan lokal, 802.16 (WMAN) untuk skala kota, dan 802.20 (WWAN) untuk jaringan luas. Selain itu, Ad-Hoc tidak membutuhkan pusat, sedangkan Infrastructure membutuhkan Access Point.

**Example:** Ad-Hoc = transfer file langsung antar HP. Infrastructure = koneksi WiFi melalui router.

**Point:** Jadi, pemilihan standar dan mode jaringan tergantung kebutuhan jarak dan stabilitas koneksi.

---

### **P4: OS Mobile - Arsitektur 4 Lapisan + Sandbox**

**PREP:**

**Point:** Sistem operasi mobile memiliki arsitektur berlapis dengan keamanan sandbox yang ketat.

**Reason:** Lapisan terdiri dari Linux Kernel (hardware), Native Libraries & Runtime, Application Framework, dan Application. Sandbox membatasi akses aplikasi demi melindungi data sensitif pengguna.

**Example:** Aplikasi galeri tidak bisa mengakses SMS tanpa izin pengguna.

**Point:** Jadi, arsitektur berlapis dan sandbox penting untuk menjaga keamanan data di perangkat mobile.

---

### **P5: OS Lanjutan - LMK + IPC + Intent**

**PREP:**

**Point:** Android mengelola performa dan komunikasi aplikasi menggunakan LMK dan Intent.

**Reason:** LMK menghapus proses berdasarkan prioritas untuk menghemat RAM. Intent digunakan untuk komunikasi antar aplikasi, baik secara eksplisit maupun implisit.

**Example:** Share foto ke WhatsApp = Intent implisit. Membuka halaman tertentu dalam aplikasi = Intent eksplisit.

**Point:** Jadi, LMK menjaga performa sistem, dan Intent memungkinkan interaksi antar aplikasi secara fleksibel.

---

### **P6: Mobile Web - Native vs Hybrid vs PWA**

**PREP:**

**Point:** PWA adalah solusi paling optimal untuk aplikasi inventaris dengan keterbatasan budget dan kebutuhan sederhana.

**Reason:** PWA unggul dalam biaya rendah, waktu pengembangan cepat, dan distribusi mudah tanpa instalasi. Walaupun akses hardware dan performa lebih rendah, hal ini tidak menjadi masalah untuk aplikasi inventaris.

**Example:** Aplikasi inventaris berbasis web yang bisa langsung diakses via browser untuk scan barcode dan input data tanpa instalasi.

**Point:** Jadi, PWA menjadi pilihan terbaik karena efisien dalam biaya, waktu, dan kemudahan distribusi.

*Tabel A-P-B-D-P untuk P6:*

| Kriteria | Native | Hybrid | PWA | Rekomendasi Inventaris |
|----------|--------|--------|-----|------------------------|
| **A - Access Hardware** | Full: Fingerprint, NFC, Laser scanner | Full via plugin: Kamera + barcode | Terbatas: Kamera saja | Hybrid/PWA cukup (scan barcode pakai kamera) |
| **P - Performance** | Tertinggi | Menengah | Rendah | PWA cukup (hanya input data, tidak butuh grafis berat) |
| **B - Budget/Biaya** | 400–800 juta (2 OS) | 200–400 juta (2 OS) | 50–150 juta | PWA paling hemat (sesuai budget terbatas) |
| **D - Development Time** | 8–12 bulan | 4–6 bulan | 1–2 bulan | PWA tercepat (kebutuhan cepat) |
| **P - Platform/Distribusi** | Install via App Store/Play Store | Install via Store | Akses via link, tanpa install | PWA paling praktis untuk internal |

*Penjelasan A-P-B-D-P:*
1. *A - Access Hardware* = Seberapa banyak sensor/fitur HP yang bisa dipake. App inventaris cuma butuh kamera buat scan barcode, jadi PWA udah cukup. Gak perlu Native yang bisa NFC.
2. *P - Performance* = Seberapa kenceng aplikasinya. App inventaris cuma isi form, gak butuh 60fps. Jadi Performance rendah PWA bukan masalah.
3. *B - Budget/Biaya* = Duit yang keluar. Soalnya bilang "budget terbatas", jadi ini faktor utama. PWA paling murah 50-150jt vs Native 800jt.
4. *D - Development Time* = Kecepatan bikin & update. PWA jadi 1-2 bulan + update instan. Kantor butuh cepat, jadi PWA paling cocok.
5. *P - Platform/Distribusi* = Cara bagi aplikasinya. PWA tinggal share link WA, gak perlu IT install satu-satu di HP karyawan. Paling praktis buat internal.

*Kesimpulan P6:* Karena *B-Budget* dan *D-Development* paling kritikal di soal, maka *PWA* direkomendasikan meskipun *A-Access* dan *P-Performance* dikorbankan.
