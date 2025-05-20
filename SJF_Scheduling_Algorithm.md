SJF Scheduling Algorithm

Nama Kelompok:

1.     Dinda Diyah Arifa (3124500034)

2.     Oktavia Ramadhani (3124500038)

3.     Yosiyanti Cendekia Sari (3124500059)





2.      SJF Scheduling Algorithm

Analisa:

Kode tersebut mengimplementasikan algoritma Shortest Job First (SJF) Non-Preemptive untuk proses dengan waktu kedatangan (arrival time). Berikut merupakan penjelasannya: 

Struktur Data

struct proc {

    int no, at, bt, it, ct, tat, wt;

};

no: Nomor Proses

at: Arrival Time (Waktu Kedatangan Proses)

bt: Burst Time (Waktu Eksekusi Proses)

it: Idle Time (Waktu Mulai Eksekusi Proses)

ct: Completion Time (Waktu Selesainya Proses)

tat: Turnaround Time (Waktu Total dari Kedatangan Hingga Selesai)

wt: Waiting Time (Waktu Menunggu Proses di Antrian)




Fungsi read ()

struct proc read(int i) {

    struct proc p;

    p.no = i;

    printf("Enter Arrival Time: ");

    scanf("%d", &p.at);

    printf("Enter Burst Time: ");

    scanf("%d", &p.bt);

    return p;

}

Membaca Arrival Time dan Burst Time dari pengguna untuk setiap proses.

Menyimpan data ke dalam struct proc




Fungsi main ()




Input Jumlah Proses

printf("Enter Number of Processes: ");

scanf("%d", &n);

for(int i=0; i p[j+1].at) {

            temp = p[j];

            p[j] = p[j+1];

            p[j+1] = temp;

        }

Mengurutkan proses berdasarkan Arrival Time (proses yang datang lebih awal dijalankan lebih dulu)

Pemilihan Proses Pertama

for(j=1; j P3 -> P2 -> P4

Algoritma SJF NoN-Preemptive Berjalan Benar:

Proses dengan BT terkecil selalu dipilih setelah proses sebelumnya selesai

Jika BT sama (P2 DAN P4), proses dengan AT lebih awal (P2) diprioritaskan

Response Time (RT) = Waiting Time (WT):

Pada SJF Non-Preemptive, RT selalu sama dengan WT karena proses langsung dieksekusi saat dipilih.

Tidak Ada Kesalahan Perhitungan:

Semua nilai CT, TAT, WT, dan RT sesuai dengan simulasi manual.



3.      SRTF Scheduling Algorithm



Analisa:

Struktur Data 

struct proc {

    int no, at, bt, rt, ct, tat, wt;

};

Fungsi : Menyimpan informasi proses

no = Nomor proses (P1, P2, dst)

at = Arrival Time (waktu datang)

bt = Burst Time (lama proses)

rt = Remaining Time (waktu sisa, digunakan untuk SRTF)

ct = Completion Time (waktu selesai)

tat = Turnaround Time (ct - at)

wt = Waiting Time (tat - bt)




Fungsi read(int i)

struct proc read(int i) {

    struct proc p;

    printf("\nProcess No: %d\n",i);

    p.no = i;

    printf("Enter Arrival Time: ");

    scanf("%d", &p.at);

    printf("Enter Burst Time: ");

    scanf("%d", &p.bt);

    p.rt = p.bt;  // Initialize remaining time with burst time

    return p;

}

Fungsi ini bertugas untuk:

Mengisi data proses ke-i dari input pengguna (AT dan BT).

Menginisialisasi rt sebagai bt, karena saat proses belum berjalan, waktu sisanya = waktu penuh.

Mengembalikan struktur proc yang sudah diisi.




Fungsi main()

int main() {

Deklarasi dan Input Awal

struct proc p[10], temp;

float avgtat = 0, avgwt = 0;

int n, s, remain = 0, time;

printf("<--SRTF Scheduling Algorithm (Preemptive)-->\n");

printf("Enter Number of Processes: ");

scanf("%d", &n);

p[10] = array dari maksimal 10 proses.

remain = jumlah proses yang sudah selesai (untuk kontrol loop utama).

time = waktu simulasi berjalan.




Input Proses

    for(int i=0; i p[j+1].at) {

                temp = p[j];

                p[j] = p[j+1];

                p[j+1] = temp;

            }

Bubble sort sederhana untuk mengurutkan proses berdasarkan waktu kedatangan (at).

Membantu algoritma bekerja lebih stabil (meskipun tidak wajib dalam SRTF, tapi mempermudah urutan).




Header Tabel Output

    printf("\nProcess\t\tAT\tBT\tCT\tTAT\tWT\n");

Menampilkan header untuk tabel hasil penjadwalan.




Inisialisasi Sentinel Proses

    p[9].rt = MAX;

Menjadikan elemen p[9] (elemen terakhir array) sebagai sentinel dengan waktu sangat besar (MAX = 9999).

Tujuannya agar dalam pencarian proses dengan rt terkecil, jika tidak ada proses lain, maka proses dummy ini akan menjadi default.




Loop Utama SRTF

    for(time = 0; remain != n; time++) {

        s = 9;

        for(int i = 0; i < n; i++)

            if(p[i].at <= time && p[i].rt < p[s].rt && p[i].rt > 0)

                s = i;

Loop berjalan setiap waktu (time) hingga semua proses selesai (remain == n).

Mencari proses s dengan rt terkecil yang sudah datang (at <= time) dan masih memiliki rt > 0.




Menjalankan Proses Terpilih

        p[s].rt--;  

Menjalankan 1 unit waktu




Jika Proses Selesai

        if(p[s].rt == 0) {

            remain++;

            p[s].ct = time + 1;             // Waktu selesai

            p[s].tat = p[s].ct - p[s].at;   // TAT

            avgtat += p[s].tat;

            p[s].wt = p[s].tat - p[s].bt;   // WT

            avgwt += p[s].wt;

            printf("P%d\t\t%d\t%d\t%d\t%d\t%d\n", p[s].no, p[s].at, p[s].bt, p[s].ct, p[s].tat, p[s].wt);

        }

    }

Jika proses selesai (rt == 0), hitung:

Completion Time (ct)

Turnaround Time (tat)

Waiting Time (wt)

Tambahkan ke total rata-rata.

Cetak hasil proses.




Menghitung dan Menampilkan Rata-rata

    avgtat /= n;

    avgwt /= n;

    printf("\nAverage TurnAroundTime = %f\nAverage WaitingTime = %f", avgtat, avgwt);

}

Hitung dan cetak rata-rata TAT dan WT.




Eksekusi

Input:

P1: at=0, bt=7  

P2: at=2, bt=4  

P3: at=4, bt=1  

P4: at=5, bt=4 

Langkah - langkah

Waktu 0-1 : P1 dieksekusi (rt=7→6).

Waktu 2 : P2 tiba (rt=4), lebih pendek dari P1 (rt=6). Alihkan ke P2.

Waktu 4 : P3 tiba (rt=1), lebih pendek dari P2 (rt=3). Alihkan ke P3.

Waktu 5 : P3 selesai (ct=5, tat=1, wt=0).

Waktu 5-7 : P2 dieksekusi hingga selesai (ct=7, tat=5, wt=1).

Waktu 7-11 : P4 dieksekusi (ct=11, tat=6, wt=2).

Waktu 11-16 : P1 dieksekusi hingga selesai (ct=16, tat=16, wt=9).

Output:

Process    AT    BT    CT    TAT    WT  

P3               4       1       5        1     0  

P2               2       4       7         5      1  

P4               5       4      11        6       2  

P1               0       7      16       16      9

Rata-Rata:

Turnaround Time (TAT):

(1+5+6+16) / 4 = 7.0

Waiting Time (WT):

(0+1+2+9) / 4 = 3.0



