
# SJF Scheduling Algorithm With Arrival Time

**Nama Kelompok:**
1. Dinda Diyah Arifa (3124500034)
2. Oktavia Ramadhani (3124500038)
3. Yosiyanti Cendekia Sari (3124500059)

---


## 1. SJF Scheduling Algorithm Non - Preemtive

### Code Program:
```c
#include<stdio.h>
struct proc
{
    int no,at,bt,it,ct,tat,wt;
};
struct proc read(int i)
{
    struct proc p;
    printf("\nProcess No: %d\n",i);
    p.no=i;
    printf("Enter Arrival Time: ");
    scanf("%d",&p.at);
    printf("Enter Burst Time: ");
    scanf("%d",&p.bt);
    return p;
}
int main()
{
    int n,j,min=0;
    float avgtat=0,avgwt=0;
    struct proc p[10],temp;
    printf("<--SJF Scheduling Algorithm (Non-Preemptive)-->\n");
    printf("Enter Number of Processes: ");
    scanf("%d",&n);
    for(int i=0;i<n;i++)
        p[i]=read(i+1);
    for(int i=0;i<n-1;i++)
        for(j=0;j<n-i-1;j++)    
            if(p[j].at>p[j+1].at)
            {
                temp=p[j];
                p[j]=p[j+1];
                p[j+1]=temp;
            }
    for(j=1;j<n&&p[j].at==p[0].at;j++)
        if(p[j].bt<p[min].bt)
            min=j;
    temp=p[0];
    p[0]=p[min];
    p[min]=temp;
    p[0].it=p[0].at;
    p[0].ct=p[0].it+p[0].bt;
    for(int i=1;i<n;i++)
    {
        for(j=i+1,min=i;j<n&&p[j].at<=p[i-1].ct;j++)
            if(p[j].bt<p[min].bt)
                min=j;
        temp=p[i];
        p[i]=p[min];
        p[min]=temp;
        if(p[i].at<=p[i-1].ct)
            p[i].it=p[i-1].ct;
        else
            p[i].it=p[i].at;
        p[i].ct=p[i].it+p[i].bt;
    }
    printf("\nProcess\t\tAT\tBT\tCT\tTAT\tWT\tRT\n");
    for(int i=0;i<n;i++)
    {
        p[i].tat=p[i].ct-p[i].at;
        avgtat+=p[i].tat;
        p[i].wt=p[i].tat-p[i].bt;
        avgwt+=p[i].wt;
        printf("P%d\t\t%d\t%d\t%d\t%d\t%d\t%d\n",p[i].no,p[i].at,p[i].bt,p[i].ct,p[i].tat,p[i].wt,p[i].wt);
    }
    avgtat/=n,avgwt/=n;
    printf("\nAverage TurnAroundTime=%f\nAverage WaitingTime=%f",avgtat,avgwt);
}
```

### Output Program:
```
Process   AT   BT   CT   TAT   WT   RT
P1        0     7     7     7     0     0
P3        4     1     8     4     3     3
P2        2     4    12    10     6     6
P4        5     4    16    11     7     7

Average TurnAroundTime=8.0
Average WaitingTime=4.0
```

### Analisa:
Kode tersebut mengimplementasikan algoritma Shortest Job First (SJF) Non-Preemptive untuk proses dengan waktu kedatangan (arrival time). Berikut merupakan penjelasannya:

**Struktur Data**
```c
struct proc {
    int no, at, bt, it, ct, tat, wt;
};
```
- `no`: Nomor Proses
- `at`: Arrival Time (Waktu Kedatangan Proses)
- `bt`: Burst Time (Waktu Eksekusi Proses)
- `it`: Idle Time (Waktu Mulai Eksekusi Proses)
- `ct`: Completion Time (Waktu Selesainya Proses)
- `tat`: Turnaround Time (Waktu Total dari Kedatangan Hingga Selesai)
- `wt`: Waiting Time (Waktu Menunggu Proses di Antrian)

**Fungsi read()**
```c
struct proc read(int i) {
    struct proc p;
    p.no = i;
    printf("Enter Arrival Time: ");
    scanf("%d", &p.at);
    printf("Enter Burst Time: ");
    scanf("%d", &p.bt);
    return p;
}
```
- Membaca Arrival Time dan Burst Time dari pengguna untuk setiap proses
- Menyimpan data ke dalam struct proc

**Fungsi main()**

**Input Jumlah Proses**
```c
printf("Enter Number of Processes: ");
scanf("%d", &n);
for(int i=0; i<n; i++)
    p[i] = read(i+1);
```
- Meminta jumlah proses (n) dan mengisi data proses ke array p

**Sorting Berdasarkan Arrival Time**
```c
for(int i=0; i<n-1; i++)
    for(int j=0; j<n-i-1; j++)    
        if(p[j].at > p[j+1].at) {
            temp = p[j];
            p[j] = p[j+1];
            p[j+1] = temp;
        }
```
- Mengurutkan proses berdasarkan Arrival Time (proses yang datang lebih awal dijalankan lebih dulu)

**Pemilihan Proses Pertama**
```c
for(j=1; j<n && p[j].at == p[0].at; j++)
    if(p[j].bt < p[min].bt)
        min=j;
temp = p[0];
p[0] = p[min];
p[min] = temp;
```
- Memilih proses dengan Burst Time terpendek di antara proses yang memiliki Arrival Time sama dengan proses pertama
- Proses ini dijadikan proses pertama yang dieksekusi

**Penjadwalan SJF Non-Preemptive**
```c
p[0].it = p[0].at;  // Waktu mulai = arrival time
p[0].ct = p[0].it + p[0].bt;

for(int i=1; i<n; i++) {
    // Cari proses dengan burst time terpendek yang sudah tiba
    for(j=i+1, min=i; j<n && p[j].at <= p[i-1].ct; j++)
        if(p[j].bt < p[min].bt)
            min = j;

    // Tukar posisi proses
    temp = p[i];
    p[i] = p[min];
    p[min] = temp;

    // Hitung waktu mulai (idle time)
    if(p[i].at <= p[i-1].ct)
        p[i].it = p[i-1].ct;  // Lanjut setelah proses sebelumnya selesai
    else
        p[i].it = p[i].at;    // Proses mulai saat tiba jika CPU idle

    p[i].ct = p[i].it + p[i].bt;  // Waktu selesai
}
```
**Langkah Utama:**
1. Untuk setiap proses, cari proses dengan Burst Time terpendek yang sudah tiba (at <= CT proses sebelumnya)
2. Proses tersebut dipindahkan ke posisi berikutnya dalam antrian eksekusi
3. Hitung Idle Time (it):
   - Jika proses tiba sebelum/saat CPU selesai: mulai setelah proses sebelumnya (it = CT sebelumnya)
   - Jika proses tiba setelah CPU idle: mulai saat tiba (it = at)
4. Hitung Completion Time (ct = it + bt)

**Perhitungan TAT, WT, dan Output**
```c
for(int i=0; i<n; i++) {
    p[i].tat = p[i].ct - p[i].at;  // TAT = CT - AT
    avgtat += p[i].tat;
    p[i].wt = p[i].tat - p[i].bt;  // WT = TAT - BT
    avgwt += p[i].wt;
    printf("P%d\t\t%d\t%d\t%d\t%d\t%d\t%d\n", p[i].no, p[i].at, p[i].bt, p[i].ct, p[i].tat, p[i].wt, p[i].wt);
}
```
- Turnaround Time (TAT): Waktu total dari kedatangan hingga selesai
- Waiting Time (WT): Waktu menunggu di antrian (TAT - BT)
- Response Time (RT): Sama dengan WT karena SJF non-preemptive

**Rata-rata TAT dan WT**
```c
avgtat /= n, avgwt /= n;
printf("\nAverage TurnAroundTime=%f\nAverage WaitingTime=%f", avgtat, avgwt);
```

**Analisa Output Program SJF Non-Preemptive**

**Data Input:**
- Proses 1 (P1): Arrival Time (AT) = 0, Burst Time (BT) = 7
- Proses 2 (P2): AT = 2, BT =4
- Proses 3 (P3): AT = 4, BT = 1
- Proses 4 (P4): AT = 5, BT = 4

**Langkah-Langkah Penjadwalan:**
1. Time 0-7: P1 dieksekusi (BT=7)
2. Time 7-8: P3 dieksekusi (BT=1)
3. Time 8-12: P2 dieksekusi (BT=4)
4. Time 12-16: P4 dieksekusi (BT=4)

**Output Program:**
```
Process   AT   BT   CT   TAT   WT   RT
P1        0     7     7     7     0     0
P3        4     1     8     4     3     3
P2        2     4    12    10     6     6
P4        5     4    16    11     7     7
```

**Rata-rata Turnaround Time (TAT):**
(7 + 4 + 10 + 11)/4 = 32/4 = 8

**Rata-rata Waiting Time (WT):**
(0 + 3 + 6 + 7)/4 = 16/4 = 4

**Kesimpulan**
- Urutan Eksekusi: P1 -> P3 -> P2 -> P4
- Algoritma SJF Non-Preemptive Berjalan Benar:
  - Proses dengan BT terkecil selalu dipilih setelah proses sebelumnya selesai
  - Jika BT sama (P2 dan P4), proses dengan AT lebih awal (P2) diprioritaskan
- Response Time (RT) = Waiting Time (WT):
  - Pada SJF Non-Preemptive, RT selalu sama dengan WT karena proses langsung dieksekusi saat dipilih
- Tidak Ada Kesalahan Perhitungan:
  - Semua nilai CT, TAT, WT, dan RT sesuai dengan simulasi manual

---

## 2. SRTF Scheduling Algorithm (Preemptive)

### Code Program:
```c
#include<stdio.h>
#define MAX 9999
struct proc
{
    int no,at,bt,rt,ct,tat,wt;
};
struct proc read(int i)
{
    struct proc p;
    printf("\nProcess No: %d\n",i);
    p.no=i;
    printf("Enter Arrival Time: ");
    scanf("%d",&p.at);
    printf("Enter Burst Time: ");
    scanf("%d",&p.bt);
    p.rt=p.bt;
    return p;
}
int main()
{
    struct proc p[10],temp;
    float avgtat=0,avgwt=0;
    int n,s,remain=0,time;
    printf("<--SRTF Scheduling Algorithm (Preemptive)-->\n");
    printf("Enter Number of Processes: ");
    scanf("%d",&n);
    for(int i=0;i<n;i++)
        p[i]=read(i+1);
    for(int i=0;i<n-1;i++)
        for(int j=0;j<n-i-1;j++)    
            if(p[j].at>p[j+1].at)
            {
                temp=p[j];
                p[j]=p[j+1];
                p[j+1]=temp;
            }
    printf("\nProcess\t\tAT\tBT\tCT\tTAT\tWT\n");
    p[9].rt=MAX;
    for(time=0;remain!=n;time++)
    {
        s=9;
        for(int i=0;i<n;i++)
            if(p[i].at<=time&&p[i].rt<p[s].rt&&p[i].rt>0)
                s=i;
        p[s].rt--;
        if(p[s].rt==0)
        {
            remain++;
            p[s].ct=time+1;
            p[s].tat=p[s].ct-p[s].at;
            avgtat+=p[s].tat;
            p[s].wt=p[s].tat-p[s].bt;
            avgwt+=p[s].wt;
            printf("P%d\t\t%d\t%d\t%d\t%d\t%d\n",p[s].no,p[s].at,p[s].bt,p[s].ct,p[s].tat,p[s].wt);
        }
    }
    avgtat/=n,avgwt/=n;
    printf("\nAverage TurnAroundTime=%f\nAverage WaitingTime=%f",avgtat,avgwt);
}
```

### Output Program:
```
Process   AT   BT   CT   TAT   WT
P3        4     1     5     1     0
P2        2     4     7     5     1
P4        5     4    11     6     2
P1        0     7    16    16     9

Average TurnAroundTime=7.0
Average WaitingTime=3.0
```

### Analisa:

**Struktur Data**
```c
struct proc {
    int no, at, bt, rt, ct, tat, wt;
};
```
**Fungsi**: Menyimpan informasi proses
- `no` = Nomor proses (P1, P2, dst)
- `at` = Arrival Time (waktu datang)
- `bt` = Burst Time (lama proses)
- `rt` = Remaining Time (waktu sisa, digunakan untuk SRTF)
- `ct` = Completion Time (waktu selesai)
- `tat` = Turnaround Time (ct - at)
- `wt` = Waiting Time (tat - bt)

**Fungsi read(int i)**
```c
struct proc read(int i) {
    struct proc p;
    printf("\nProcess No: %d\n",i);
    p.no = i;
    printf("Enter Arrival Time: ");
    scanf("%d", &p.at);
    printf("Enter Burst Time: ");
    scanf("%d", &p.bt);
    p.rt = p.bt;  // Initialize remaining time with burst time
    return p;
}
```
**Fungsi ini bertugas untuk:**
1. Mengisi data proses ke-i dari input pengguna (AT dan BT)
2. Menginisialisasi rt sebagai bt, karena saat proses belum berjalan, waktu sisanya = waktu penuh
3. Mengembalikan struktur proc yang sudah diisi

**Fungsi main()**
```c
int main() {
```

**Deklarasi dan Input Awal**
```c
struct proc p[10], temp;
float avgtat = 0, avgwt = 0;
int n, s, remain = 0, time;
printf("<--SRTF Scheduling Algorithm (Preemptive)-->\n");
printf("Enter Number of Processes: ");
scanf("%d", &n);
```
- `p[10]` = array dari maksimal 10 proses
- `remain` = jumlah proses yang sudah selesai (untuk kontrol loop utama)
- `time` = waktu simulasi berjalan

**Input Proses**
```c
for(int i=0; i<n; i++)
    p[i] = read(i+1);
```
Melakukan input data untuk tiap proses dengan memanggil read()

**Sorting Proses Berdasarkan Arrival Time**
```c
for(int i=0; i<n-1; i++)
    for(int j=0; j<n-i-1; j++)
        if(p[j].at > p[j+1].at) {
            temp = p[j];
            p[j] = p[j+1];
            p[j+1] = temp;
        }
```
Bubble sort sederhana untuk mengurutkan proses berdasarkan waktu kedatangan (at)
Membantu algoritma bekerja lebih stabil (meskipun tidak wajib dalam SRTF, tapi mempermudah urutan)

**Header Tabel Output**
```c
printf("\nProcess\t\tAT\tBT\tCT\tTAT\tWT\n");
```
Menampilkan header untuk tabel hasil penjadwalan

**Inisialisasi Sentinel Proses**
```c
p[9].rt = MAX;
```
Menjadikan elemen p[9] (elemen terakhir array) sebagai sentinel dengan waktu sangat besar (MAX = 9999)
Tujuannya agar dalam pencarian proses dengan rt terkecil, jika tidak ada proses lain, maka proses dummy ini akan menjadi default

**Loop Utama SRTF**
```c
for(time = 0; remain != n; time++) {
    s = 9;
    for(int i = 0; i < n; i++)
        if(p[i].at <= time && p[i].rt < p[s].rt && p[i].rt > 0)
            s = i;
```
Loop berjalan setiap waktu (time) hingga semua proses selesai (remain == n)
Mencari proses s dengan rt terkecil yang sudah datang (at <= time) dan masih memiliki rt > 0

**Menjalankan Proses Terpilih**
```c
p[s].rt--;  
```
Menjalankan 1 unit waktu

**Jika Proses Selesai**
```c
if(p[s].rt == 0) {
    remain++;
    p[s].ct = time + 1;             // Waktu selesai
    p[s].tat = p[s].ct - p[s].at;   // TAT
    avgtat += p[s].tat;
    p[s].wt = p[s].tat - p[s].bt;   // WT
    avgwt += p[s].wt;
    printf("P%d\t\t%d\t%d\t%d\t%d\t%d\n", p[s].no, p[s].at, p[s].bt, p[s].ct, p[s].tat, p[s].wt);
}
```
Jika proses selesai (rt == 0), hitung:
1. Completion Time (ct)
2. Turnaround Time (tat)
3. Waiting Time (wt)
Tambahkan ke total rata-rata
Cetak hasil proses

**Menghitung dan Menampilkan Rata-rata**
```c
avgtat /= n;
avgwt /= n;
printf("\nAverage TurnAroundTime = %f\nAverage WaitingTime = %f", avgtat, avgwt);
}
```
Hitung dan cetak rata-rata TAT dan WT

**Eksekusi**

**Input:**
- P1: at=0, bt=7  
- P2: at=2, bt=4  
- P3: at=4, bt=1  
- P4: at=5, bt=4 

**Langkah-langkah:**
1. Waktu 0-1: P1 dieksekusi (rt=7→6)
2. Waktu 2: P2 tiba (rt=4), lebih pendek dari P1 (rt=6). Alihkan ke P2
3. Waktu 4: P3 tiba (rt=1), lebih pendek dari P2 (rt=3). Alihkan ke P3
4. Waktu 5: P3 selesai (ct=5, tat=1, wt=0)
5. Waktu 5-7: P2 dieksekusi hingga selesai (ct=7, tat=5, wt=1)
6. Waktu 7-11: P4 dieksekusi (ct=11, tat=6, wt=2)
7. Waktu 11-16: P1 dieksekusi hingga selesai (ct=16, tat=16, wt=9)

**Output:**
```
Process    AT    BT    CT    TAT    WT  
P3         4     1     5     1     0  
P2         2     4     7     5     1  
P4         5     4    11     6     2  
P1         0     7    16    16     9
```

**Rata-Rata:**
- Turnaround Time (TAT): (1+5+6+16)/4 = 7.0
- Waiting Time (WT): (0+1+2+9)/4 = 3.0
```
