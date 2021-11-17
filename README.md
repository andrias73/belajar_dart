# Write and build with Flutter app, part 1
Beberapa panduan untuk membuat aplikasi Flutter pertama. jika terbiasa dengan kode berorientasi objek dan konsep pemrograman dasar seperti variabel, loop, dan kondisional, dapat menyelesaikan tutorial ini. tidak memerlukan pengalaman sebelumnya dengan Dart, seluler, atau pemrograman web.
# Apa yang akan dibangun pada bagian pertama ?
menerapkan aplikasi sederhana yang menghasilkan nama yang diusulkan untuk perusahaan startup. Pengguna dapat memilih dan membatalkan pilihan nama, menyimpan yang terbaik. Kode dengan malas menghasilkan 10 nama sekaligus. Saat pengguna menggulir, lebih banyak nama dihasilkan. Tidak ada batasan seberapa jauh pengguna dapat menggulir.
# Apa yang akan dipelajari dibagian pertama ini ?
- Cara menulis aplikasi Flutter yang terlihat natural di iOS, Android, dan web
- Struktur dasar aplikasi Flutter
- Menemukan dan menggunakan paket untuk memperluas fungsionalitas
- Menggunakan hot reload untuk siklus pengembangan yang lebih cepat
- Bagaimana menerapkan widget stateful
- Cara membuat daftar yang tak terbatas dan dimuat dengan malas
# Apa yang akan digunakan ?
memerlukan dua perangkat lunak untuk menyelesaikan lab : Flutter SDK dan editor. Codelab ini mengasumsikan Android Studio, tetapi juuga dapat menggunakan editor pilihan. dapat juga menjalankan codelab ini dengan menggunakan salah satu perangkat berikut:
- Perangkat fisik (Android atau iOS) yang terhubung ke komputer Anda dan disetel ke mode pengembang
- Simulator iOS (memerlukan penginstalan alat Xcode)
- Emulator Android (memerlukan penyiapan di Android Studio)
- Sebuah browser (Chrome diperlukan untuk debugging)
# Langkah ke-1 membuat aplikasi flutter pemula
Buat aplikasi Flutter dengan template sederhana, menggunakan petunjuk di Memulai dengan aplikasi Flutter pertama. Beri nama proyek startup_namer (bukan flutter_app) Tip: Jika tidak melihat “New Flutter Project” sebagai opsi di IDE, pastikan telah menginstal plugin untuk Flutter dan Dart.
1. Ganti konten lib/main.dart. Hapus semua kode dari lib/main.dart. Ganti dengan kode berikut, yang menampilkan "Hello World" di tengah layar. Tip: Saat menempelkan kode ke aplikasi, lekukan bisa menjadi miring. hal ini dapat memperbaikinya dengan alat Flutter berikut: Android Studio dan IntelliJ IDEA: Klik kanan kode dan pilih Reformat Code with dartfmt. Kode VS: Klik kanan dan pilih Format Dokumen. Terminal: Jalankan format flutter .
2. Jalankan aplikasi seperti yang dijelaskan oleh IDE. dari sana akan terlihat output Android, iOS, atau web, tergantung pada perangkat. Tip: Pertama kali menjalankan di perangkat fisik, mungkin perlu beberapa saat untuk memuat. Setelah itu, dapat menggunakan hot reload untuk pembaruan cepat. Save juga melakukan hot reload jika aplikasi sedang berjalan. Saat menjalankan aplikasi langsung dari konsol menggunakan flutter run, masukkan r untuk melakukan hot reload.
Observasi
Contoh ini membuat aplikasi Material. Materi adalah bahasa desain visual yang standar di seluler dan web. Flutter menawarkan serangkaian widget Material yang kaya. Sebaiknya gunakan desain bahan-penggunaan: entri yang benar di bagian flutter file pubspec.yaml. Ini akan memungkinkan untuk menggunakan lebih banyak fitur Material, seperti kumpulan Ikon yang telah ditentukan sebelumnya.
- Metode main() menggunakan notasi panah (=>). Gunakan notasi panah untuk fungsi atau metode satu baris.
- Aplikasi ini memperluas StatelessWidget, yang menjadikan aplikasi itu sendiri sebagai widget. Di Flutter, hampir semuanya adalah widget, termasuk perataan, padding, dan tata letak.
- Widget Scaffold, dari pustaka Material, menyediakan bilah aplikasi default, dan properti badan yang menampung pohon widget untuk layar beranda. Subpohon widget bisa sangat kompleks.
- Tugas utama widget adalah menyediakan metode build() yang menjelaskan cara menampilkan widget dalam kaitannya dengan widget tingkat rendah lainnya.
- Badan untuk contoh ini terdiri dari widget Pusat yang berisi widget turunan Teks. Widget Tengah menyelaraskan subpohon widgetnya ke tengah layar.
# Langkah ke-2 Menggunakan paket eksternal
Pada langkah ini, akan mulai menggunakan paket sumber terbuka bernama english_words, yang berisi beberapa ribu kata bahasa Inggris yang paling sering digunakan ditambah beberapa fungsi utilitas.
1. File pubspec.yaml mengelola aset dan dependensi untuk aplikasi Flutter. Di pubspec.yaml, tambahkan english_words (3.1.5 atau lebih tinggi) ke daftar dependensi.
2. Saat melihat file pubspec.yaml di tampilan editor Android Studio, klik Pub get. Ini menarik paket ke dalam proyek. Performing Pub get juga menghasilkan file pubspec.lock secara otomatis dengan daftar semua paket yang ditarik ke dalam proyek dan nomor versinya.
3. Di lib/main.dart, impor paket baru: Saat mengetik, Android Studio memberi saran untuk perpustakaan yang akan diimpor. itu kemudian membuat string impor menjadi abu-abu, memberi tahu bahwa perpustakaan yang diimpor tidak digunakan (sejauh ini).
4. Gunakan paket kata bahasa Inggris untuk menghasilkan teks alih-alih menggunakan string "Hello World":
5. Jika aplikasi sedang berjalan, muat ulang untuk memperbarui aplikasi yang sedang berjalan. Setiap kali mengklik hot reload, atau menyimpan proyek, akan melihat pasangan kata yang berbeda, dipilih secara acak, di aplikasi yang sedang berjalan. Ini karena pasangan kata dihasilkan di dalam metode build, yang dijalankan setiap kali MaterialApp memerlukan rendering, atau saat mengaktifkan Platform di Flutter Inspector.
Problem / masalah ? Jika aplikasi tidak berjalan dengan benar, cari kesalahan ketik. Jika Anda ingin mencoba beberapa alat debugging Flutter, lihat rangkaian alat debugging dan profil DevTools. Jika perlu, gunakan kode di tautan berikut untuk kembali ke jalur semula.
- pubspec.yaml
- lib/main.dart
# Langkah ke-3 Tambahkan widget Stateful
Widget stateless tidak dapat diubah, artinya propertinya tidak dapat diubah—semua nilai bersifat final. Widget stateful mempertahankan status yang mungkin berubah selama masa pakai widget. Menerapkan widget stateful membutuhkan setidaknya dua kelas:
1. kelas StatefulWidget yang membuat instance
2. kelas State. Kelas StatefulWidget, dengan sendirinya, tidak dapat diubah dan dapat dibuang dan dibuat ulang, tetapi kelas State tetap ada selama masa pakai widget.
Pada langkah ini, Anda akan menambahkan widget stateful, RandomWords, yang membuat kelas State-nya, _RandomWordsState. kemudian akan menggunakan RandomWords sebagai anak di dalam widget stateless MyApp yang ada.
1. Buat kode boilerplate untuk widget stateful. Di lib/main.dart, posisikan kursor setelah semua kode, masukkan Return beberapa kali untuk memulai pada baris baru. Di IDE, mulailah mengetik stful. Editor menanyakan apakah ingin membuat widget Stateful. Tekan Kembali untuk menerima. Kode boilerplate untuk dua kelas muncul, dan kursor diposisikan bagi Anda untuk memasukkan nama widget stateful.
2. Masukkan RandomWords sebagai nama widgetnya. Widget RandomWords tidak melakukan banyak hal selain membuat kelas State-nya. Setelah memasukkan RandomWords sebagai nama widget stateful, IDE secara otomatis memperbarui kelas State yang menyertainya, menamakannya _RandomWordsState. Secara default, nama kelas State diawali dengan underbar. Awalan pengenal dengan garis bawah memberlakukan privasi dalam bahasa Dart dan merupakan praktik terbaik yang direkomendasikan untuk objek Negara. IDE juga secara otomatis memperbarui kelas status untuk memperluas Status, yang menunjukkan bahwa kita menggunakan kelas Status generik khusus untuk digunakan dengan RandomWords. Sebagian besar logika aplikasi berada di sini—ini mempertahankan status untuk widget RandomWords. Kelas ini menyimpan daftar pasangan kata yang dihasilkan, yang tumbuh tanpa batas saat pengguna menggulir dan, di bagian 2 lab ini, pasangan kata favorit saat pengguna menambahkan atau menghapusnya dari daftar dengan mengalihkan ikon hati.
3. Perbarui metode build() di _RandomWordsState:
4. Hapus kode pembuatan kata dari MyApp dengan membuat perubahan yang ditunjukkan pada diff.
5. Mulai ulang aplikasi. Aplikasi harus berperilaku seperti sebelumnya, menampilkan pasangan kata setiap kali Anda memuat ulang atau menyimpan aplikasi.
tips : Jika melihat peringatan pada hot reload bahwa mungkin perlu memulai ulang aplikasi, pertimbangkan untuk memulai ulang. Peringatannya mungkin positif palsu, tetapi memulai ulang aplikasi memastikan bahwa perubahan Anda tercermin di UI aplikasi.
Problem / masalah : Jika aplikasinya tidak berjalan dengan benar, cari kesalahan ketik. Jika ingin mencoba beberapa alat debugging Flutter, lihat rangkaian alat debugging dan profil DevTools. Jika perlu, gunakan kode di tautan berikut untuk kembali ke jalur semula.
lib/main.dart
# Langkah ke-4 Buat ListView bergulir tak terbatas
Pada langkah ini akan memperluas _RandomWordsState untuk menghasilkan dan menampilkan daftar pasangan kata. Saat pengguna menggulir daftar (ditampilkan dalam widget ListView) tumbuh tanpa batas. Konstruktor pabrik pembuat ListView memungkinkan untuk membuat tampilan daftar dengan malas, sesuai permintaan.
1. Tambahkan daftar _suggestions ke kelas _RandomWordsState untuk menyimpan pasangan kata yang disarankan. Juga, tambahkan variabel _biggerFont untuk membuat ukuran font lebih besar. selanjutnya, menambahkan fungsi _buildSuggestions() ke kelas _RandomWordsState. Metode ini membangun ListView yang menampilkan pasangan kata yang disarankan. Kelas ListView menyediakan properti pembangun, itemBuilder, yang merupakan pembangun pabrik dan fungsi panggilan balik yang ditentukan sebagai fungsi anonim. Dua parameter diteruskan ke fungsi—BuildContext, dan iterator baris, i. Iterator dimulai dari 0 dan bertambah setiap kali fungsi dipanggil. Ini bertambah dua kali untuk setiap pasangan kata yang disarankan: sekali untuk ListTile, dan sekali untuk Pembagi. Model ini memungkinkan daftar yang disarankan untuk terus bertambah saat pengguna menggulir.
2. Tambahkan fungsi _buildSuggestions() ke kelas _RandomWordsState /1/ Callback itemBuilder dipanggil sekali per pasangan kata yang disarankan, dan menempatkan setiap saran ke dalam baris ListTile. Untuk baris genap, fungsi menambahkan baris ListTile untuk pasangan kata. Untuk baris ganjil, fungsi menambahkan widget Pembagi untuk memisahkan entri secara visual. Perhatikan bahwa pembagi mungkin sulit dilihat pada perangkat yang lebih kecil. /2/ Tambahkan widget pembagi setinggi satu piksel sebelum setiap baris di ListView. /3/ Ekspresi i ~/ 2 membagi i dengan 2 dan mengembalikan hasil integer. Misalnya: 1, 2, 3, 4, 5 menjadi 0, 1, 1, 2, 2. Ini menghitung jumlah sebenarnya dari pasangan kata dalam ListView, dikurangi widget pembagi. /4/ Jika Anda telah mencapai akhir dari pasangan kata yang tersedia, buat 10 lagi dan tambahkan ke daftar saran.
3. Tambahkan fungsi _buildRow() ke _RandomWordsState
4. Di kelas _RandomWordsState, perbarui metode build() untuk menggunakan _buildSuggestions(), daripada langsung memanggil pustaka pembuatan kata. (Perancah mengimplementasikan tata letak visual Desain Material dasar.) Ganti badan metode dengan kode yang disorot:
5. Di kelas MyApp, perbarui metode build() dengan mengubah judul, dan mengubah home menjadi widget RandomWords
6. Mulai ulang aplikasi. Anda akan melihat daftar pasangan kata tidak peduli seberapa jauh Anda menggulir.
Problem / masalah ? Jika aplikasi Anda tidak berjalan dengan benar, cari kesalahan ketik. Jika Anda ingin mencoba beberapa alat debugging Flutter, lihat rangkaian alat debugging dan profil DevTools. Jika perlu, gunakan kode di tautan berikut untuk kembali ke jalur semula. lib/main.dart
# Profil atau Rilis berjalan
Sejauh ini kita telah menjalankan aplikasi dalam mode debug. Mode debug memperdagangkan kinerja untuk fitur pengembang yang berguna seperti hot reload dan step debugging. Bukan hal yang tidak terduga untuk melihat kinerja yang lambat dan animasi yang tersendat-sendat dalam mode debug. Setelah siap untuk menganalisis kinerja atau merilis aplikasi, kita dapat menggunakan mode build "profil" atau "rilis" Flutter. Untuk detail selengkapnya, lihat mode build Flutter.
