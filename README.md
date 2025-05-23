## Refleksi Modul 10 - Timer

### Nama : Micheline Wijaya Limbergh
### NPM : 2306207013

![image](https://github.com/user-attachments/assets/c71be560-4119-414b-9f75-f83621aa63f9)

Hasil cargo run dan analisisnya : 
C:\Users\lenovo\Desktop\Coolyeah_4\adpro\adpro-modul10\timer>cargo run
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.06s
     Running `target\debug\timer_future.exe`
Micheline's Computer: hey hey
Mciheline's Computer: howdy!
Micheline's Computer: done!

Baris println!("Micheline's Computer: hey hey"); dieksekusi segera oleh thread utama karena tidak bergantung pada proses async.
Ketika sebuah blok async dijalankan menggunakan spawn, task tersebut tidak langsung diproses, melainkan dibuat sebagai future yang siap dijalankan ketika waktunya tiba.
Future ini akan menunggu giliran untuk dieksekusi, dan tugas ini diatur oleh executor, yaitu komponen yang mengatur kapan dan bagaimana task async dijalankan.
Ketika executor mulai menjalankan future, barulah muncul output seperti Micheline's Computer: howdy!.
Jika terdapat delay seperti TimerFuture, task tersebut akan menyerahkan kontrol sementara dan dilanjutkan lagi setelah waktu tunggu selesai.
Setelah delay selesai, eksekusi kembali dilanjutkan dan hasil seperti Micheline's Computer: done! dicetak.
Ini menunjukkan bahwa Rust async bekerja berdasarkan prinsip tunda dan lanjut (pause-resume), bukan eksekusi serentak, dan sangat bergantung pada manajemen dari executor.
 
Multiple spawn memungkinkan user menjadwalkan banyak task async sekaligus.
Remove spawner (dengan drop(spawner)) memberi sinyal bahwa semua task sudah dijadwalkan, jadi executor boleh mulai menyelesaikan semua task yang ada lalu berhenti.
Hasil : 
![image](https://github.com/user-attachments/assets/3263384f-8f01-4614-a282-1a2fa8c3a73f)
