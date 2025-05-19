# SJF Scheduling Algorithm

**Nama Kelompok:**  
1. Dinda Diyah Arifa  
2. Oktavia Ramadhani  
3. Yosiyanti Cendekia Sari  

---

## 1. SJF Scheduling Algorithm Without Arrival Time

### Code Program:
```c
#include<stdio.h>

struct proc {
    int no, bt, ct, tat, wt;
};

struct proc read(int i) {
    struct proc p;
    printf("\nProcess No: %d\n", i);
    p.no = i;
    printf("Enter Burst Time: ");
    scanf("%d", &p.bt);
    return p;
}

int main() {
    struct proc p[10], tmp;
    float avgtat = 0, avgwt = 0;
    int n, ct = 0;
    printf("<--SJF Scheduling Algorithm Without Arrival Time (Non-Preemptive)-->\n");
    printf("Enter Number of Processes: ");
    scanf("%d", &n);
    
    for (int i = 0; i < n; i++)
        p[i] = read(i + 1);
    
    // Sorting processes by burst time (Bubble Sort)
    for (int i = 0; i < n - 1; i++)
        for (int j = 0; j < n - i - 1; j++)
            if (p[j].bt > p[j + 1].bt) {
                tmp = p[j];
                p[j] = p[j + 1];
                p[j + 1] = tmp;
            }
    
    printf("\nProcessNo\tBT\tCT\tTAT\tWT\tRT\n");
    for (int i = 0; i < n; i++) {
        ct += p[i].bt;
        p[i].ct = p[i].tat = ct;
        avgtat += p[i].tat;
        p[i].wt = p[i].tat - p[i].bt;
        avgwt += p[i].wt;
        printf("P%d\t\t%d\t%d\t%d\t%d\t%d\n", p[i].no, p[i].bt, p[i].ct, p[i].tat, p[i].wt, p[i].wt);
    }
    
    avgtat /= n, avgwt /= n;
    printf("\nAverage TurnAroundTime=%f\nAverage WaitingTime=%f", avgtat, avgwt);
    return 0;
}
```

### Output Program:  
![ss output](https://github.com/dindadiyaharifa/SisOp-2025/blob/main/Screenshot%202025-05-19%20144203.png?raw=true)

---

## Analisa

Kode tersebut mengimplementasikan algoritma penjadwalan **Shortest Job First (SJF) Non-Preemptive** tanpa arrival time (AT). Berikut penjelasannya:

### 1. Struktur Data
```c
struct proc {
    int no, bt, ct, tat, wt;
};
```
- `no`: Nomor proses.  
- `bt`: Burst Time (waktu eksekusi proses).  
- `ct`: Completion Time (waktu selesainya proses).  
- `tat`: Turnaround Time (waktu total dari kedatangan hingga selesai).  
- `wt`: Waiting Time (waktu menunggu proses di antrian).  

### 2. Fungsi `read()`
- Membaca input `Burst Time` untuk setiap proses.  
- Menyimpan nomor proses dan burst time ke dalam struct `proc`.  

### 3. Fungsi `main()`
1. **Input Jumlah Proses**  
   - Pengguna memasukkan jumlah proses (`n`).  
   - Data proses diisi menggunakan loop dan fungsi `read()`.  

2. **Sorting Proses (Bubble Sort)**  
   - Mengurutkan proses berdasarkan `Burst Time` dari terkecil ke terbesar.  
   - Contoh: Input `BT = [3, 5, 2]` → Hasil sorting `[2, 3, 5]`.  

3. **Menghitung CT, TAT, WT**  
   - **Completion Time (CT):** Diakumulasi dari `Burst Time` proses sebelumnya.  
     Contoh:  
     - P3 (BT=2) → CT = 2  
     - P1 (BT=3) → CT = 5  
     - P2 (BT=5) → CT = 10  
   - **Turnaround Time (TAT):** `TAT = CT` (karena AT = 0).  
   - **Waiting Time (WT):** `WT = TAT - BT`.  

4. **Output Hasil**  
   - Menampilkan tabel hasil perhitungan untuk setiap proses.  
   - **Response Time (RT)** diisi dengan nilai `WT` karena SJF non-preemptive.  

5. **Rata-rata TAT dan WT**  
   - Rata-rata TAT:  
     $$\frac{2 + 5 + 10}{3} = \frac{17}{3} = 5.666667$$  
   - Rata-rata WT:  
     $$\frac{0 + 2 + 5}{3} = \frac{7}{3} = 2.333333$$  

### 4. Contoh Perhitungan
| Proses | BT | CT  | TAT | WT  | RT  |
|--------|----|-----|-----|-----|-----|
| P3     | 2  | 2   | 2   | 0   | 0   |
| P1     | 3  | 5   | 5   | 2   | 2   |
| P2     | 5  | 10  | 10  | 5   | 5   |
```
