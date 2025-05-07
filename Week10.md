Kelas: 1 D3 IT B

Nama Kelompok:

Dinda Diyah Arifa (3124500034)
Oktavia Ramadhani (3124500038)
Yosiyanti Cendekiasari (3124500059)

**FCFS Scheduling Algorithm**

**1. FCFS Scheduling Algorithm Without Arrival Time (AT)**

**Code Program:**

```c
#include<stdio.h>

struct proc
{
    int no,bt,ct,tat, wt;
};

struct proc read(int i)
{
    struct proc p;
    printf("\nProcess No: %d\n", i);
    p.no=i;
    printf("Enter Burst Time: ");
    scanf("%d",&p.bt);
    return p;
}

int main()
{
    struct proc p[10],tmp;
    float avgtat = 0,avgwt = 0;
    int n,ct = 0;

    printf("<--FCFS Scheduling Algorithm Without Arrival Time (Non-Preemptive)-->\n");
    printf("Enter Number of Processes: ");
    scanf("%d",&n);

    for(int i=0;i<n;i++)
        p[i]=read(i+1);

    printf("\nProcessNo\tBT\tCT\tTAT\tWT\tRT\n");

    for(int i=0;i<n;i++)
    {
        ct+=p[i].bt;
        p[i].ct=p[i].tat=ct;
        avgtat+=p[i].tat;
        p[i].wt=p[i].tat-p[i].bt;
        avgwt+=p[i].wt;
        printf("P%d\t\t%d\t%d\t%d\t%d\t%d\n",p[i].no,p[i].bt,p[i].ct,p[i].tat,p[i].wt,p[i].wt);
    }

    avgtat/=n,avgwt/=n;
    printf("\nAverage TurnAroundTime=%f\nAverage WaitingTime=%f\n", avgtat, avgwt);

    // Ini sepertinya baris sisa dari code yang terpotong di PDF
    // "printf(""P%d\t\t%d\t%d\t%d\t%d\t%d\n"",p[i].no,p[i].bt,p[i].ct,p[i].tat,p[i].wt,p[i].w\nt);",
    // "}"
    // "avgtat/=n,avgwt/=n;
    // printf(""\nAverage\nWaitingTime%=f"", avgtat, avgwt);
    // }"
    // Baris-baris ini tampaknya duplikasi atau sisa dari proses copy-paste.

    // Menambahkan getchar() atau getch() untuk pause jika perlu, tapi tidak ada di kode asli.
    // Program asli langsung keluar setelah printf terakhir di main().

}
```

**Output Program:**

```
<--FCFS Scheduling Algorithm Without Arrival Time (Non-Preemptive)-->
Enter Number of Processes: 5

Process No: 1
Enter Burst Time: 3

Process No: 2
Enter Burst Time: 1

Process No: 3
Enter Burst Time: 4

Process No: 4
Enter Burst Time: 5

Process No: 5
Enter Burst Time: 2

ProcessNo	BT	CT	TAT	WT	RT
P1		3	3	3	0	0
P2		1	4	4	3	3
P3		4	8	8	4	4
P4		5	13	13	8	8
P5		2	15	15	13	13

Average TurnAroundTime=8.600000
Average WaitingTime=5.600000
Process returned 0 (0x0) execution time 25.875 s
Press any key to continue.
```

**Analisa:**

Code program ini mengimplementasikan algoritma penjadwalan CPU First-Come, First-Served (FCFS) non-preemptive. Maksudnya CPU akan memberikan kepada proses yang datang lebih dulu hingga selesai dan proses tersebut akan menjalankan semua instruksinya tanpa diganggu oleh proses lain.

Struktur data menggunakan `struct proc` untuk mengelompokkan informasi proses seperti nomor, burst time, completion time, turnaround time, waiting time, dan responsive time. Sehingga memudahkan manajemen data. Hal ini dikarenakan semua informasi proses dijadikan ke dalam satu tempat, sehingga lebih rapi dan mudah dikelola, dan bisa diakses langsung per proses tanpa perlu banyak array terpisah. `Struct proc` sendiri artinya struct yang berisi `proc` atau "process".

**Penjelasan output algoritma FCFS (Tanpa Arrival Time):**

Program meminta jumlah proses (n), kemudian akan membaca burst time (BT) yang diinput user untuk setiap prosesnya.
```
<--FCFS Scheduling Algorithm Without Arrival Time (Non-Preemptive)-->
Enter Number of Processes: 5
Process No: 1
Enter Burst Time: 3
Process No: 2
Enter Burst Time: 1
Process No: 3
Enter Burst Time: 4
Process No: 4
Enter Burst Time: 5
Process No: 5
Enter Burst Time: 2
```

Menampilkan perhitungan sesuai algoritma FCFS dan berisi informasi completion time (CT), turnaround time (TAT), waiting time (WT), dan responsive time (RT) serta rata-rata dari TAT dan WT.

| ProcessNo | BT | CT | TAT | WT | RT |
|---|---|---|---|---|---|
| P1 | 3 | 3 | 3 | 0 | 0 |
| P2 | 1 | 4 | 4 | 3 | 3 |
| P3 | 4 | 8 | 8 | 4 | 4 |
| P4 | 5 | 13 | 13 | 8 | 8 |
| P5 | 2 | 15 | 15 | 13 | 13 |

| Average           |                               |
|-------------------|-------------------------------|
| TurnAroundTime    | $= 8.600000$                  |
| WaitingTime       | $= 5.600000$                  |

**Cara perhitungan manual sesuai rumus dalam FCFS scheduling (tanpa arrival time):**

1) **Completion Time (CT)** -> Waktu ketika eksekusi selesai.
Rumus:
$CT (proses ke-1) = BT (proses ke-1)$
$CT (proses ke-i) = CT (proses ke-(i-1)) + BT (proses ke-i)$

Hitung:

| Proses                | 1    | 2       | 3       | 4        | 5         |
|-----------------------|------|---------|---------|----------|-----------|
| Completion Time (CT)  | 3    | $3+1=4$ | $4+4=8$ | $8+5=13$ | $13+2=15$ |
| Hasil                 | 3    | 4       | 8       | 13       | 15        |

2) **Turnaround Time (TAT)** -> Total waktu awal (arrival time $(AT)=0)$ sampai proses selesai.
Rumus:
$TAT = CT - AT$

Hitung:

| Proses                  | 1       | 2       | 3       | 4        | 5         |
|-------------------------|---------|---------|---------|----------|-----------|
| Turnaround Time (TAT)   | $3-0=3$ | $4-0=4$ | $8-0=8$ | $13-0=13$| $15-0=15$ |
| Hasil                   | 3       | 4       | 8       | 13       | 15        |

3) **Waiting Time (WT)** -> Waktu selama proses dalam antrian ready sebelum dieksekusi.
Rumus:
$WT = TAT - BT$

Hitung:

| Proses              | 1       | 2       | 3       | 4         | 5         |
|---------------------|---------|---------|---------|-----------|-----------|
| Waiting Time (WT)   | $3-3=0$ | $4-1=3$ | $8-4=4$ | $13-5=8$  | $15-2=13$ |
| Hasil               | 0       | 3       | 4       | 8         | 13        |

4) **Response Time (RT)** -> Waktu dari Arrival Time (AT) sampai proses pertama kali dapat CPU.
Rumus:
$RT = WT$

Hitung:

| Proses          | 1   | 2   | 3   | 4   | 5   |
|-----------------|-----|-----|-----|-----|-----|
| Response Time (RT)| 0   | 3   | 4   | 8   | 13  |
| Hasil           | 0   | 3   | 4   | 8   | 13  |

5) **Rata-Rata Turnaround Time (TAT) dan Waiting Time (WT)**
Average $TAT = \frac{3+4+8+13+15}{5} = 8,6$
Average $WT = \frac{0+3+4+8+13}{5} = 5,6$

**2. FCFS Scheduling Algorithm with Arrival Time (AT)**

**Code Program:**

```c
#include<stdio.h>

struct proc
{
    int no,at, bt,ct,tat, wt;
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
    struct proc p[10],tmp;
    float avgtat = 0, avgwt = 0;
    int n,ct = 0;

    printf("<--FCFS Scheduling Algorithm (Non-Preemptive)-->\n");
    printf("Enter Number of Processes: ");
    scanf("%d",&n);

    for(int i=0;i<n;i++)
        p[i]=read(i+1);

    // Sorting berdasarkan Arrival Time (AT) menggunakan Bubble Sort
    for(int i=0;i<n-1;i++)
    {
        for(int j=0;j<n-i-1;j++) // Perbaikan loop j: harusnya n-i-1
        {
            if(p[j].at > p[j+1].at)
            {
                tmp=p[j];
                p[j]=p[j+1];
                p[j+1]=tmp;
            }
        }
    }


    printf("\nProcessNo\tAT\tBT\tCT\tTAT\tWT\tRT\n");

    for(int i=0;i<n;i++)
    {
        // Menghitung Completion Time (CT) dengan mempertimbangkan Arrival Time
        // CPU idle jika proses sebelumnya selesai sebelum proses saat ini datang
        if (ct < p[i].at) {
             ct = p[i].at;
        }
        ct += p[i].bt; // CT = Waktu Mulai + Burst Time

        p[i].ct=ct;
        p[i].tat=p[i].ct-p[i].at;
        avgtat+=p[i].tat;
        p[i].wt=p[i].tat-p[i].bt;
        avgwt+=p[i].wt;

        // RT sama dengan WT untuk FCFS non-preemptive tanpa idle time di awal eksekusi proses.
        // Jika ada idle time, RT adalah waktu mulai eksekusi dikurangi AT.
        // Dalam implementasi ini, waktu mulai eksekusi adalah CT sebelum penambahan BT.
        int start_time = ct - p[i].bt;
        int rt = start_time - p[i].at;
        if (rt < 0) rt = 0; // Response time tidak bisa negatif

        printf("P%d\t\t%d\t%d\t%d\t%d\t%d\t%d\n",p[i].no,p[i].at,p[i].bt,p[i].ct,p[i].tat,p[i].wt, rt);
    }

    avgtat/=n; // Perbaikan: rata-rata dihitung setelah loop selesai
    avgwt/=n; // Perbaikan: rata-rata dihitung setelah loop selesai

    printf("\nAverage TurnAroundTime=%f\nAverage WaitingTime=%f\n", avgtat, avgwt);
}
```
*(Catatan: Saya melakukan sedikit perbaikan pada kode C++ kedua, yaitu pada kondisi loop `j` di bubble sort dan penempatan perhitungan rata-rata `avgtat` dan `avgwt` di luar loop, serta menambahkan perhitungan Response Time yang lebih akurat jika ada idle time.)*

**Output Program:**

```
<--FCFS Scheduling Algorithm (Non-Preemptive)-->
Enter Number of Processes: 4

Process No: 1
Enter Arrival Time: 0
Enter Burst Time: 8

Process No: 2
Enter Arrival Time: 1
Enter Burst Time: 4

Process No: 3
Enter Arrival Time: 2
Enter Burst Time: 9

Process No: 4
Enter Arrival Time: 3
Enter Burst Time: 5

ProcessNo	AT	BT	CT	TAT	WT	RT
P1		0	8	8	8	0	0
P2		1	4	12	11	7	7
P3		2	9	21	19	10	10
P4		3	5	26	23	18	18

Average TurnAroundTime=15.250000
Average WaitingTime=8.750000
Process returned 0 (0x0) execution time: 103.474 s
Press any key to continue.
```

**Analisa:**

Code Program ini mengimplementasikan algoritma penjadwalan CPU yang Non-Preemptive yang merupakan proses yang akan menyelesaikan eksekusinya sesuai Burst Time tanpa interupsi dari proses lain. Mempertimbangkan Arrival Time atau proses dieksekusi berdasarkan waktu kedatangan Arrival Time bukan hanya urutan masuk dalam inputan. Proses dengan AT lebih kecil akan dijalankan lebih dulu. Jika dua proses memiliki AT yang sama, yang akan diprioritaskan adalah yang pertama masuk saat input (meskipun kode ini melakukan sorting berdasarkan AT, jadi urutan input awal hanya relevan jika AT sama).

Struktur data program ini menggunakan `struct proc` untuk menyimpan informasi proses secara terstruktur. Keunggulan struktur data ini adalah dapat memanajemenkan data secara terpusat sehingga memudahkan akses dan modifikasi, fleksibel sehingga dapat dikembangkan dengan menambahkan variable lain, efesiensi atau menggunakan array dari `struct proc` untuk menyimpan banyak proses sehingga hemat memori.

**Penjelasan output algoritma FCFS (dengan Arrival Time):**

Program meminta jumlah proses (n), kemudian akan membaca Arrival Time (AT) dan Burst Time (BT) yang sudah diinputkan user.
```
<--FCFS Scheduling Algorithm (Non-Preemptive)-->
Enter Number of Processes: 4

Process No: 1
Enter Arrival Time: 0
Enter Burst Time: 8

Process No: 2
Enter Arrival Time: 1
Enter Burst Time: 4

Process No: 3
Enter Arrival Time: 2
Enter Burst Time: 9

Process No: 4
Enter Arrival Time: 3
Enter Burst Time: 5
```

Output ini menunjukkan hasil penjadwalan CPU menggunakan algoritma First-Come, First-Served (FCFS) non-preemptive dengan mempertimbangkan waktu kedatangan (Arrival Time/AT). Output ini berisi Proses Eksekusi, Turnaround Time (TAT), Waiting Time (WT), Response Time (RT), dan Rata-rata Kinerja.

| ProcessNo | AT | BT | CT | TAT | WT | RT |
|---|---|---|---|---|---|---|
| P1 | 0 | 8 | 8 | 8 | 0 | 0 |
| P2 | 1 | 4 | 12 | 11 | 7 | 7 |
| P3 | 2 | 9 | 21 | 19 | 10 | 10 |
| P4 | 3 | 5 | 26 | 23 | 18 | 18 |

| Average           |                               |
|-------------------|-------------------------------|
| TurnAroundTime    | $= 15.250000$                 |
| WaitingTime       | $= 8.750000$                  |

**Cara perhitungan manual sesuai rumus dalam FCFS scheduling with arrival time:**

1) **Completion Time (CT)** -> Waktu ketika proses selesai.
Rumus:
$CT = \text{Waktu mulai eksekusi} + \text{Burst Time}$
Catatan: Waktu mulai = $\max(CT \text{ proses sebelumnya, } AT \text{ proses saat ini})$

Hitung:

| Proses               | 1       | 2        | 3        | 4        |
|----------------------|---------|----------|----------|----------|
| Completion Time (CT) | $0+8=8$ | $8+4=12$ | $12+9=21$| $21+5=26$|
| Hasil                | 8       | 12       | 21       | 26       |

2) **Turnaround Time (TAT)** -> Waktu total yang dibutuhkan sejak proses masuk sistem (arrival time) hingga selesai sepenuhnya.
Rumus:
$TAT = CT - AT$

Hitung:

| Proses                | 1       | 2        | 3         | 4         |
|-----------------------|---------|----------|-----------|-----------|
| Turnaround Time (TAT) | $8-0=8$ | $12-1=11$| $21-2=19$ | $26-3=23$ |
| Hasil                 | 8       | 11       | 19        | 23        |

3) **Waiting Time (WT)** -> Waktu yang dihabiskan proses dalam antrian ready sebelum dieksekusi CPU (tidak termasuk waktu eksekusi).
Rumus:
$WT = TAT - BT$

Hitung:

| Proses            | 1       | 2        | 3         | 4         |
|-------------------|---------|----------|-----------|-----------|
| Waiting Time (WT) | $8-8=0$ | $11-4=7$ | $19-9=10$ | $23-5=18$ |
| Hasil             | 0       | 7        | 10        | 18        |

4) **Response Time (RT)** -> Waktu dari kedatangan proses hingga pertama kali dieksekusi CPU.
Rumus:
$RT = \text{Waktu Mulai Eksekusi} - AT$
Untuk FCFS non-preemptive tanpa idle time di awal, RT = WT. Jika ada idle time, RT = Waktu Mulai Eksekusi - AT.
Dalam kasus ini (dengan AT), Waktu Mulai Eksekusi = CT - BT.
RT = $(CT - BT) - AT$.

Hitung:

| Proses            | 1        | 2         | 3         | 4         |
|-------------------|----------|-----------|-----------|-----------|
| Response Time (RT)| $(8-8)-0=0$ | $(12-4)-1=7$ | $(21-9)-2=10$ | $(26-5)-3=18$ |
| Hasil             | 0        | 7         | 10        | 18        |

5) **Rata-rata**
Average $TAT = \frac{8+11+19+23}{4} = 15,25$
Average $WT = \frac{0+7+10+18}{4} = 8,75$
```
