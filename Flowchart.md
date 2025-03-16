# Flowchart Booting dan Shutdown Sistem Operasi

## Start

1. **Menekan Power On**
2. **Power On Self Test (POST)**  
   - Melakukan pemeriksaan hardware  
   - Apakah POST berhasil?
     - **Yes:** Lanjut ke BIOS/UEFI  
     - **No:** Menampilkan pesan error dan sistem menyimpan data serta mengakhiri proses  

## Proses Booting

3. **BIOS/UEFI** menjalankan Bootloader  
4. **Bootloader** menemukan Kernel OS  
5. **Kernel** diinisialisasi  
6. **Kernel** memuat driver hardware dasar  
7. **Kernel** menginisialisasi subsistem  
8. **Memulai Essential Services**  
9. **Login Manager** dijalankan  
10. **Menampilkan Login Screen**  
11. **Memulai Desktop Environment/Shell**  
12. **User Session Aktif**  

## Proses Shutdown

13. **User Meminta Shutdown**  
14. **Sistem menyimpan data dan mengakhiri proses**  
15. **Kernel melakukan Unmount Filesystem**  
16. **Kernel mematikan hardware**  
17. **Shutdown/Restart**  
18. **End**  
