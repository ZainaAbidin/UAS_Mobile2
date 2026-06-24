`Leafio` adalah aplikasi berbasis Android yang dikembangkan menggunakan bahasa Java untuk membantu pengguna 
mengelola dan mengingat jadwal perawatan tanaman hias. Aplikasi ini dirancang dengan
prinsip *simple on the outside, powerful on the inside*, yaitu menghadirkan 
antarmuka yang minimalis dan mudah digunakan, namun ditopang oleh logika latar belakang yang 
andal dan kaya fitur. Tujuan utamanya adalah memastikan pengguna tidak melewatkan waktu penting 
untuk menyiram maupun memupuk tanaman, sekaligus menyediakan sarana konsultasi mengenai kesehatan 
tanaman melalui asisten berbasis kecerdasan buatan.

## Latar Belakang

Merawat tanaman hias kerap kali terkendala oleh kesibukan sehari-hari, sehingga pengguna mudah lupa kapan terakhir kali menyiram atau memberi pupuk. Leafio hadir untuk menjawab persoalan tersebut dengan menggabungkan sistem penjadwalan yang fleksibel dan pengingat otomatis yang akurat, tanpa mengorbankan kesederhanaan tampilan yang menjadi ciri khas aplikasi ini.

## Fitur Utama

Leafio memungkinkan pengguna menentukan jadwal penyiraman secara fleksibel. Pengguna dapat memilih satu tanggal 
sekaligus menetapkan beberapa waktu penyiraman dalam satu hari, misalnya pagi dan sore, melalui dialog yang 
berulang secara otomatis. Selain penyiraman, aplikasi juga menyediakan penjadwalan pemupukan yang
dikelola secara terpisah agar kebutuhan masing-masing tetap jelas.

Inti dari aplikasi ini adalah sistem pengingat yang presisi. Dengan 
memanfaatkan `AlarmManager` dan `BroadcastReceiver` bawaan Android, Leafio 
mampu memunculkan notifikasi tepat pada waktu yang ditentukan, bahkan ketika 
aplikasi sedang ditutup. Sebagai contoh, pengguna akan menerima notifikasi bertuliskan "MAWAR harus disiram sekarang!" sesuai jadwal yang telah dimasukkan.

Di sisi pengalaman pengguna, seluruh logika tingkat lanjut diterapkan sepenuhnya 
pada lapisan latar belakang sehingga estetika antarmuka tetap konsisten dan tidak 
berubah. Aplikasi turut dilengkapi mode gelap (*dark mode*) yang menyesuaikan tema 
secara dinamis mengikuti preferensi sistem perangkat. Sebagai pelengkap, tersedia pula
fitur konsultasi berbasis AI yang membantu pengguna mendiagnosis penyakit tanaman serta memperoleh tips perawatan secara instan.

## Struktur Proyek

Proyek ini mengikuti arsitektur standar Android Studio dengan pemisahan yang jelas antara berkas kode Java 
dan sumber daya (*resource*) XML. Gambaran umum struktur direktorinya adalah sebagai berikut.
```
Leafio/
|-- app/
|   |-- src/main/
|   |   |-- java/com/example/leafio/
|   |   |   |-- BaseActivity.java          # Kelas induk manajemen tema (dark mode)
|   |   |   |-- MainActivity.java          # Halaman utama dan akses fitur AI
|   |   |   |-- SplashScreenActivity.java  # Splash screen beranimasi
|   |   |   |-- InputJadwalActivity.java   # Input data, penanggalan, dan pemasangan alarm
|   |   |   |-- DetailJadwalActivity.java  # Ringkasan jadwal dan aktivasi notifikasi
|   |   |   |-- NotifReceiver.java         # BroadcastReceiver pengolah alarm menjadi notifikasi
|   |   |   |-- PlantAdapter.java          # Adapter daftar tanaman
|   |   |   `-- Tanaman.java               # Model data (POJO)
|   |   |-- res/
|   |   |   |-- anim/                       # Berkas animasi (splash_animation.xml)
|   |   |   |-- drawable/                   # Aset gambar dan background custom
|   |   |   |-- layout/                     # Desain antarmuka XML
|   |   |   |-- values/                     # colors.xml, strings.xml, themes.xml
|   |   |   `-- values-night/colors.xml     # Palet warna khusus dark mode
|   |   `-- AndroidManifest.xml             # Pendaftaran activity, receiver, dan permission
|   `-- build.gradle                        # Dependensi gradle tingkat modul (GSON, dll)
`-- build.gradle                            # Konfigurasi gradle tingkat proyek
```

## Teknologi dan Pustaka

Aplikasi ini dibangun menggunakan bahasa Java dengan memanfaatkan sejumlah komponen inti Android, 
antara lain `AlarmManager`, `BroadcastReceiver`, `PendingIntent`, dan `SharedPreferences`. Mekanisme 
notifikasi ditangani melalui `NotificationCompat` dan `NotificationChannel`, sementara penyimpanan data 
daftar tanaman dilakukan secara lokal dengan bantuan pustaka GSON untuk proses serialisasi objek. Pada 
sisi antarmuka, Leafio mengadopsi prinsip Material Design serta memanfaatkan `DatePickerDialog` dan `TimePickerDialog` untuk interaksi pemilihan tanggal dan waktu.

## Konfigurasi Permission

Agar fitur pengingat dan notifikasi dapat berjalan sebagaimana mestinya, beberapa izin perlu didaftarkan pada berkas `AndroidManifest.xml` sebagai berikut.
```
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.POST_NOTIFICATIONS" />
<uses-permission android:name="android.permission.SCHEDULE_EXACT_ALARM" android:maxSdkVersion="32" />
<uses-permission android:name="android.permission.USE_EXACT_ALARM" />
```
