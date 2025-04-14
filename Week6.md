
# TUGAS SISTEM OPERASI - WEEK 6

**Nama:** Oktavia Ramadhani  
**NRP:** 3124500038  
**Dosen Pengajar:** Dr. Ferry Astika Saputra ST, M.Sc  
**Program Studi:** D3 Teknik Informatika  
**Politeknik Elektronika Negeri Surabaya (PENS)**  
**Tahun:** 2025

---

## Code Thread 3

```c
#include <stdio.h>
#include <pthread.h>

pthread_cond_t cond1 = PTHREAD_COND_INITIALIZER;
pthread_cond_t cond2 = PTHREAD_COND_INITIALIZER;
pthread_cond_t cond3 = PTHREAD_COND_INITIALIZER;
pthread_mutex_t lock = PTHREAD_MUTEX_INITIALIZER;
int done = 1;

void *foo(void *arg) {
    int thread_num = *(int *)arg;
    while (1) {
        pthread_mutex_lock(&lock);
        while (done != thread_num) {
            if (thread_num == 1) {
                pthread_cond_wait(&cond1, &lock);
            } else if (thread_num == 2) {
                pthread_cond_wait(&cond2, &lock);
            } else {
                pthread_cond_wait(&cond3, &lock);
            }
        }

        printf("%d ", thread_num);
        fflush(stdout);

        if (done == 3) {
            done = 1;
            pthread_cond_signal(&cond1);
        } else if (done == 1) {
            done = 2;
            pthread_cond_signal(&cond2);
        } else if (done == 2) {
            done = 3;
            pthread_cond_signal(&cond3);
        }

        pthread_mutex_unlock(&lock);
    }

    return NULL;
}

int main() {
    pthread_t tid1, tid2, tid3;
    int n1 = 1, n2 = 2, n3 = 3;

    pthread_create(&tid1, NULL, foo, &n1);
    pthread_create(&tid2, NULL, foo, &n2);
    pthread_create(&tid3, NULL, foo, &n3);

    pthread_join(tid1, NULL);
    pthread_join(tid2, NULL);
    pthread_join(tid3, NULL);

    return 0;
}
```

---

## Langkah Menjalankan Kode di Linux

1. **Simpan kodenya ke file**
   ```bash
   nano thread_sequence.c
   ```
   Tempelkan kode, lalu tekan `CTRL + O`, `Enter`, dan `CTRL + X`.

2. **Kompilasi dengan gcc dan pthread**
   ```bash
   gcc thread_sequence.c -o thread_sequence -lpthread
   ```

3. **Jalankan program**
   ```bash
   ./thread_sequence
   ```

   Output:
   ```
   1 2 3 1 2 3 1 2 3 ...
   ```

   Program akan mencetak angka 1, 2, 3 secara berulang hingga dihentikan dengan `CTRL + C`.

---

## Penjelasan Output

- Thread 1 mencetak `1`, lalu memberi sinyal ke Thread 2.
- Thread 2 mencetak `2`, lalu memberi sinyal ke Thread 3.
- Thread 3 mencetak `3`, lalu memberi sinyal kembali ke Thread 1.
- Proses ini berulang terus menerus selama program berjalan.

---

## Apa itu Forking?

**Forking** adalah proses untuk membuat proses baru dari proses yang sedang berjalan. Di C (Linux/Unix), dilakukan menggunakan fungsi `fork()` dari `<unistd.h>`.

Saat `fork()` dipanggil:
- Proses induk membuat **salinan dirinya sendiri** yang disebut **proses anak**.
- Keduanya berjalan paralel dan menjalankan kode setelah `fork()`.

---

### Fungsi `fork()` – Cara Kerja

```c
pid_t pid = fork();
```

- `pid == 0` → proses anak
- `pid > 0` → proses induk
- `pid < 0` → fork gagal

---

### Contoh Program Forking

```c
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>

int main() {
    pid_t pid;

    pid = fork();

    if (pid < 0) {
        perror("Fork gagal");
        return 1;
    } else if (pid == 0) {
        printf("Ini proses anak! PID: %d\n", getpid());
    } else {
        printf("Ini proses induk! PID: %d, anak: %d\n", getpid(), pid);
    }

    return 0;
}
```

---

### Analisis Output

Kemungkinan output:
```
Ini proses induk! PID: 1234, anak: 1235
Ini proses anak! PID: 1235
```

Penjelasan:
- Proses induk mencetak PID-nya dan PID anak.
- Proses anak mencetak PID-nya sendiri.
- Keduanya berjalan paralel, jadi urutan bisa bervariasi.

---

## Soal 3 & 4

### Soal 3: Keuntungan Time Quantum Berbeda di Multilevel Queue

- **Efisiensi**: Proses cepat ditangani lebih dahulu.
- **Respons Time Lebih Baik**: Proses interaktif lebih responsif.
- **Throughput Meningkat**: Proses selesai cepat, ruang lebih cepat tersedia.
- **Keadilan**: Proses berat tetap mendapat giliran.

---

### Soal 4: Gantt Chart Berbagai Algoritma

#### **Data Proses**
| Proses | Burst Time | Prioritas |
|--------|------------|-----------|
| P1     | 10         | 3         |
| P2     | 1          | 1         |
| P3     | 2          | 2         |
| P4     | 1          | 4         |
| P5     | 5          | 2         |

Semua datang di `t = 0`.

---

#### a. **FCFS**
```
| P1 | P2 | P3 | P4 | P5 |
0   10   11  13  14  19
```

---

#### b. **SJF**
```
| P2 | P4 | P3 | P5 | P1 |
0    1    2    4    9   19
```

---

#### c. **Prioritas (Non-preemptive)**
```
| P2 | P5 | P3 | P1 | P4 |
0    1    6    8   18  19
```

---

#### d. **Round Robin (Quantum = 2)**
```
| P1 | P2 | P3 | P4 | P5 | P1 | P5 | P1 | P5 | P1 | P1 |
0    2    3    5    6    8   10   12  14   15  17  19
```
