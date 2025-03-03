# TUGAS S10 CHAPTER 01  
## SISTEM OPERASI  

**Nama**      : Oktavia Ramadhani  
**NRP**       : 3124500038  
**Dosen Pengajar** : Dr. Ferry Astika Saputra ST, M.Sc  
**Program Studi** : D3 Teknik Informatika  
**Institusi** : Politeknik Elektronika Negeri Surabaya (PENS)  
**Tahun**     : 2024  

---

### 1.1 What are the three main purposes of an operating system?  
**Answer:**  
The three main purposes of an operating system are:  
1. **Resource Management**: The operating system manages the computer's hardware resources, such as the CPU, memory, and I/O devices, and allocates them to various programs and users.  
2. **Providing a User Interface**: The operating system provides an environment for users to interact with the computer, either through a command-line interface or a graphical user interface (GUI).  
3. **Execution of Application Programs**: The operating system provides a platform for application programs to run, acting as an intermediary between the hardware and the software.  

---

### 1.2 We have stressed the need for an operating system to make efficient use of the computing hardware. When is it appropriate for the operating system to forsake this principle and to "waste" resources? Why is such a system not really wasteful?  
**Answer:**  
It is appropriate for the operating system to "waste" resources when doing so improves user experience or system reliability. For example, an operating system might use extra memory to cache frequently accessed data, which speeds up access times. While this may seem wasteful in terms of memory usage, it actually improves overall system performance and user satisfaction. Similarly, redundancy in storage (e.g., RAID systems) may seem wasteful but is crucial for data reliability and fault tolerance. Therefore, such systems are not truly wasteful because they enhance performance, reliability, or user experience.  

---

### 1.3 What is the main difficulty that a programmer must overcome in writing an operating system for a real-time environment?  
**Answer:**  
The main difficulty in writing an operating system for a real-time environment is ensuring that the system meets strict timing constraints. Real-time systems must respond to events within a guaranteed time frame, and any delay could result in system failure. The programmer must design the system to prioritize time-critical tasks and ensure that the operating system can handle interrupts and process scheduling in a way that meets these strict deadlines.  

---

### 1.4 Keeping in mind the various definitions of operating system, consider whether the operating system should include applications such as web browsers and mail programs. Argue both that it should and that it should not, and support your answers.  
**Answer:**  
- **Argument for including applications:**  
  - **Convenience**: Including applications like web browsers and mail programs makes the operating system more user-friendly and ready to use out of the box.  
  - **Integration**: These applications can be tightly integrated with the operating system, providing a seamless user experience and better performance.  
- **Argument against including applications:**  
  - **Bloat**: Including too many applications can make the operating system bloated and slow, especially on systems with limited resources.  
  - **Flexibility**: Users may prefer to choose their own applications, and including default applications may limit user choice and flexibility.  

---

### 1.5 How does the distinction between kernel mode and user mode function as a rudimentary form of protection (security)?  
**Answer:**  
The distinction between kernel mode and user mode provides a basic level of protection by restricting certain operations to the kernel mode, which is reserved for the operating system. User programs run in user mode and cannot execute privileged instructions or directly access hardware resources. This separation prevents user programs from interfering with the operating system or other programs, thereby protecting the system from malicious or erroneous software.  

---

### 1.6 Which of the following instructions should be privileged?  
a. Set value of timer.  
b. Read the clock.  
c. Clear memory.  
d. Issue a trap instruction.  
e. Turn off interrupts.  
f. Modify entries in device-status table.  
g. Switch from user to kernel mode.  
h. Access I/O device.  

**Answer:**  
a. **Set value of timer** - Privileged  
b. **Read the clock** - Not privileged  
c. **Clear memory** - Privileged  
d. **Issue a trap instruction** - Not privileged  
e. **Turn off interrupts** - Privileged  
f. **Modify entries in device-status table** - Privileged  
g. **Switch from user to kernel mode** - Privileged  
h. **Access I/O device** - Privileged  

---

### 1.7 Some early computers protected the operating system by placing it in a memory partition that could not be modified by either the user job or the operating system itself. Describe two difficulties that you think could arise with such a scheme.  
**Answer:**  
1. **Limited Flexibility**: The operating system may need to modify its own memory for tasks such as dynamic memory allocation or loading device drivers. If it cannot modify its own memory partition, these tasks become difficult or impossible.  
2. **Difficulty in Debugging**: If the operating system cannot modify its own memory, debugging and patching the system becomes challenging, as errors in the operating system code cannot be easily corrected.  

---

### 1.8 Some CPUs provide for more than two modes of operation. What are two possible uses of these multiple modes?  
**Answer:**  
1. **Virtualization**: Additional modes can be used to support virtualization, where a virtual machine manager (VMM) runs in a mode with more privileges than user processes but fewer than the kernel.  
2. **Enhanced Security**: Multiple modes can provide finer-grained security controls, allowing certain system services to run in a mode with restricted privileges, reducing the risk of security breaches.  

---

### 1.9 Timers could be used to compute the current time. Provide a short description of how this could be accomplished.  
**Answer:**  
Timers can be used to compute the current time by counting the number of timer interrupts that have occurred since the system was booted. For example, if a timer is set to interrupt every 4 milliseconds (as in Linux with HZ=250), the system can keep track of the number of interrupts (jiffies) and multiply by the timer interval to calculate the elapsed time since boot. This elapsed time can then be added to the system's start time to determine the current time.  

---

### 1.10 Give two reasons why caches are useful. What problems do they solve? What problems do they cause? If a cache can be made as large as the device for which it is caching (for instance, a cache as large as a disk), why not make it that large and eliminate the device?  
**Answer:**  
- **Reasons caches are useful:**  
  - **Speed**: Caches provide faster access to frequently used data, reducing the time needed to retrieve information from slower storage devices.  
  - **Efficiency**: Caches reduce the load on the main memory and storage devices, improving overall system performance.  
- **Problems caches solve:**  
  - **Slow Access Times**: Caches mitigate the slow access times of main memory and secondary storage by keeping frequently accessed data in faster storage.  
- **Problems caches cause:**  
  - **Cache Coherency**: In multiprocessor systems, ensuring that all caches have consistent data can be complex.  
  - **Cache Size Limitations**: Caches have limited size, and managing which data to keep in the cache (replacement policies) can be challenging.  

**Why not make the cache as large as the device it is caching?**  
Even if a cache could be made as large as the device it is caching (e.g., a disk), it would still be more expensive and consume more power than the slower storage device. Additionally, the cache would still need to be managed, and the benefits of caching diminish as the cache size grows beyond a certain point.  

---

### 1.11 Distinguish between the client-server and peer-to-peer models of distributed systems.  
**Answer:**  
- **Client-Server Model**: In this model, clients request services from centralized servers. The server provides resources or services, such as file storage or database access, to the clients. This model is centralized, with the server acting as a bottleneck, but it is easier to manage and secure.  
- **Peer-to-Peer (P2P) Model**: In this model, all nodes in the system are peers and can act as both clients and servers. Each node can request and provide services, making the system decentralized. This model is more scalable and resilient but can be harder to manage and secure due to its decentralized nature.  

In summary, the client-server model is centralized and easier to manage, while the peer-to-peer model is decentralized and more scalable.  
