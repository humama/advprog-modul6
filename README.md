<details>
<summary> Commit 1 Reflection notes</summary>

di dalam handle_connection dibuat instance `BufReader` yang baru yang mengandung referensi yang bisa diubah ke `stream`. `BufReader` menambahkan buffering dengan mengelola panggilan ke metode sifat `std::io::Read` untuk kita.
Kita membuat variable bernama `http_request` untuk mengumpulkan baris permintaan yang dikirimkan browser keserver kita. Kita menunjukkan bahwa kita ingin mengumpulkan lines ini dalam vektor dengan menambahkan anotasi tipe `Vec<_>`.
`BufReader` mengimplementasikan sifat `std::io::BufRead`, yang menyediakan lines method. Lines method mengembalikan iterator `Result<String, std::io::Error>` dengan memisahkan stream data setiap kali ia melihat byte baris baru. Untuk mendapatkan setiap `String`, kami memetakan dan membuka setiap `Result`. `Result`nya mungkin error jika datanya tidak valid UTF-8 atau jika ada masalah saat membaca dari stream. Harusnya sebuah production program menghandle error dengan lebih baik, tetapi kita memilih untuk menghentikan program jika terjadi kesalahan agar lebih simple.
Browsers memberi sinyal akhir dari permintaan HTTP dengan mengirimkan dua karakter baris baru berturut-turut, jadi untuk mendapatkan satu permintaan dari stream, kita mengambil baris sampai kita mendapatkan baris yang merupakan string kosong. Setelah kita mengumpulkan garis-garisnya ke dalam vektor, kita mencetaknya menggunakan format debug yang bagus sehingga kita dapat melihat instruksi yang dikirimkan web browser ke server kita 