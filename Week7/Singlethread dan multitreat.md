# Konsep Single Thread dan Multithread

## Single Thread
Single thread adalah model eksekusi di mana sebuah proses hanya menjalankan satu thread atau satu alur instruksi pada satu waktu. Dalam single thread, setiap perintah dieksekusi secara berurutan, satu per satu, tanpa tumpang tindih. Jika suatu perintah memerlukan waktu lama untuk selesai, maka perintah berikutnya harus menunggu hingga perintah tersebut selesai. Model ini sederhana dan mudah diimplementasikan karena tidak ada kebutuhan untuk sinkronisasi antar thread, sehingga risiko terjadinya konflik data juga kecil. Namun, model single thread kurang efisien untuk aplikasi yang memerlukan multitugas atau respons cepat karena tidak dapat menjalankan beberapa tugas secara bersamaan.

## Multithread
Berbeda dengan single thread, multithread memungkinkan sebuah proses menjalankan beberapa thread secara bersamaan dalam satu waktu. Setiap thread dapat menjalankan tugas yang berbeda secara paralel, sehingga meningkatkan efisiensi dan responsivitas aplikasi. Misalnya, dalam aplikasi pengolah kata, satu thread dapat menangani pengetikan teks sementara thread lain melakukan pemeriksaan ejaan secara bersamaan. Pada prosesor single-core, thread-thread ini dijalankan secara bergantian sangat cepat sehingga tampak seolah-olah berjalan paralel (concurrency). Pada prosesor multi-core, thread-thread dapat benar-benar berjalan secara paralel pada core yang berbeda, meningkatkan performa aplikasi secara signifikan. Multithread juga memungkinkan pemanfaatan resource yang lebih efisien karena thread dalam satu proses berbagi memori dan resource lainnya.

![image](https://github.com/user-attachments/assets/1a57227d-80f5-41a3-ba04-fa5d41e3c196)

## Perbandingan
| Karakteristik | Single Thread | Multithread |
|--------------|--------------|-------------|
| Model Eksekusi | Sequential | Paralel |
| Kompleksitas | Rendah | Tinggi |
| Efisiensi CPU | Rendah | Tinggi |
| Penggunaan Resource | Dedicated | Shared |
| Kemampuan Multitasking | Terbatas | Optimal |
| Contoh Aplikasi | Program sederhana | Browser, Game, Aplikasi Produktivitas |
