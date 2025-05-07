```markdown
# Analisa Algoritma FCFS  
**Kelas**: 1 D3 IT B  
**Nama Kelompok**:  
- Dinda Diyah Arifa (3124500034)  
- Oktavia Ramadhani (3124500038)  
- Yosiyanti Cendekiasari (3124500059)  

---

## 1. FCFS Scheduling Algorithm Without Arrival Time (AT)  
### Code Program  
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
    printf("<-FCFS Scheduling Algorithm Without Arrival Time (Non-Preemptive)->\n");
    printf("Enter Number of Processes: ");
    scanf("%d", &n);
    for (int i = 0; i < n; i++)
        p[i] = read(i + 1);
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
    printf("\nAverage TurnAroundTime = %f\nAverage WaitingTime = %f", avgtat, avgwt);
    return 0;
}
```

### Output Program  
```
<-FCFS Scheduling Algorithm Without Arrival Time (Non-Preemptive)->
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

ProcessNo    BT    CT    TAT    WT    RT  
P1          3     3     3      0     0  
P2          1     4     4      3     3  
P3          4     8     8      4     4  
P4          5     13    13     8     8  
P5          2     15    15     13    13  

Average TurnAroundTime = 8.600000  
Average WaitingTime = 5.600000  
```

### Analisa  
- **Struktur Data**: Menggunakan `struct proc` untuk mengelompokkan informasi proses (nomor, burst time, completion time, turnaround time, waiting time).  
- **Cara Kerja**:  
  - Proses dijalankan sesuai urutan kedatangan tanpa interupsi.  
  - **Completion Time (CT)**: Akumulasi burst time.  
  - **Turnaround Time (TAT)**: \( \text{CT} - \text{AT} \) (AT = 0).  
  - **Waiting Time (WT)**: \( \text{TAT} - \text{BT} \).  
  - **Response Time (RT)**: Sama dengan WT karena non-preemptive.  

**Perhitungan Manual**:  
| Proses | BT | CT  | TAT  | WT   |  
|--------|----|-----|------|------|  
| P1     | 3  | 3   | 3    | 0    |  
| P2     | 1  | 4   | 4    | 3    |  
| P3     | 4  | 8   | 8    | 4    |  
| P4     | 5  | 13  | 13   | 8    |  
| P5     | 2  | 15  | 15   | 13   |  

**Rata-Rata**:  
- \( \text{TAT} = \frac{3+4+8+13+15}{5} = 8.6 \)  
- \( \text{WT} = \frac{0+3+4+8+13}{5} = 5.6 \)  

---

## 2. FCFS Scheduling Algorithm With Arrival Time (AT)  
### Code Program  
```c
#include<stdio.h>
struct proc {
    int no, at, bt, ct, tat, wt;
};

struct proc read(int i) {
    struct proc p;
    printf("\nProcess No: %d\n", i);
    p.no = i;
    printf("Enter Arrival Time: ");
    scanf("%d", &p.at);
    printf("Enter Burst Time: ");
    scanf("%d", &p.bt);
    return p;
}

int main() {
    struct proc p[10], tmp;
    float avgtat = 0, avgwt = 0;
    int n, ct = 0;
    printf("<--FCFS Scheduling Algorithm (Non-Preemptive)-->\n");
    printf("Enter Number of Processes: ");
    scanf("%d", &n);
    for (int i = 0; i < n; i++)
        p[i] = read(i + 1);
    for (int i = 0; i < n - 1; i++)
        for (int j = 0; j < n - 1; j++)
            if (p[j].at > p[j + 1].at) {
                tmp = p[j];
                p[j] = p[j + 1];
                p[j + 1] = tmp;
            }
    printf("\nProcessNo\tAT\tBT\tCT\tTAT\tWT\tRT\n");
    for (int i = 0; i < n; i++) {
        ct = (ct < p[i].at) ? p[i].at : ct;
        ct += p[i].bt;
        p[i].ct = ct;
        p[i].tat = p[i].ct - p[i].at;
        avgtat += p[i].tat;
        p[i].wt = p[i].tat - p[i].bt;
        avgwt += p[i].wt;
        printf("P%d\t\t%d\t%d\t%d\t%d\t%d\t%d\n", p[i].no, p[i].at, p[i].bt, p[i].ct, p[i].tat, p[i].wt, p[i].wt);
    }
    avgtat /= n, avgwt /= n;
    printf("\nAverage TurnAroundTime = %f\nAverage WaitingTime = %f", avgtat, avgwt);
    return 0;
}
```

### Output Program  
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

ProcessNo    AT    BT    CT    TAT    WT    RT  
P1          0     8     8      8      0     0  
P2          1     4     12     11     7     7  
P3          2     9     21     19     10    10  
P4          3     5     26     23     18    18  

Average TurnAroundTime = 15.250000  
Average WaitingTime = 8.750000  
```

### Analisa  
- **Struktur Data**: `struct proc` dengan penambahan field arrival time (`at`).  
- **Cara Kerja**:  
  - Proses diurutkan berdasarkan arrival time.  
  - **Completion Time (CT)**: \( \max(\text{CT sebelumnya}, \text{AT saat ini}) + \text{BT} \).  
  - **Turnaround Time (TAT)**: \( \text{CT} - \text{AT} \).  
  - **Waiting Time (WT)**: \( \text{TAT} - \text{BT} \).  

**Perhitungan Manual**:  
| Proses | AT | BT | CT  | TAT  | WT   |  
|--------|----|----|-----|------|------|  
| P1     | 0  | 8  | 8   | 8    | 0    |  
| P2     | 1  | 4  | 12  | 11   | 7    |  
| P3     | 2  | 9  | 21  | 19   | 10   |  
| P4     | 3  | 5  | 26  | 23   | 18   |  

**Rata-Rata**:  
- \( \text{TAT} = \frac{8 + 11 + 19 + 23}{4} = 15.25 \)  
- \( \text{WT} = \frac{0 + 7 + 10 + 18}{4} = 8.75 \)  
```
