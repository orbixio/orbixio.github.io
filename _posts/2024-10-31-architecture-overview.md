> Computer architecture describes the functionality, organization, and implementation of computer systems

The most commonly used architecture, most computers today are built on is the [Von Neumann Architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).

![](https://orbixio.netlify.app/assets/img/Pasted image 20241030221046.png)
_Von Neuman Architecture (Overview)_

#### **Memory**

> - Temporary data and instructions stored here
> - Also known as "Primary Memory"

There are two types of memory:
1. `Cache` 
2. `Random Access Memory (RAM)`

**Cache Memory**

> "*Located within the CPU itself and runs at the same clock speed as the CPU.*"

There are "three" levels of cache memory, depending on their *closeness to the CPU* core:

| **Level**       | **Description**                                                                                            |
| --------------- | ---------------------------------------------------------------------------------------------------------- |
| `Level 1 Cache` | Usually in kilobytes, the fastest memory available, located in each CPU core. (Only registers are faster.) |
| `Level 2 Cache` | Usually in megabytes, extremely fast (but slower than L1), shared between all CPU cores.                   |
| `Level 3 Cache` | Usually in megabytes (larger than L2), faster than RAM but slower than L1/L2. (Not all CPUs use L3.)       |

**Random Access Memory (RAM)**

> "*Slower than cache and registers but, comes in sizes ranging from GBs to TBs.*"
> "*For x64 systems, the memory address range is from `0x0000000000000000` to `0xffffffffffffffff`*"

Random Access Memory (Physical Memory) consists of frames which are mapped via "paging" to Virtual Memory. A record of pages and their corresponding frame is kept which is also called as "page table". 
Whenever an application is run it is allocated it very own Virtual Memory that consists of `stack`, `heap`, `data` and `text` segments.

![](https://academy.hackthebox.com/storage/modules/85/memory_structure.jpg)

| Segment | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Stack` | > *Last-in First-out (LIFO) design, fixed in size and data in it can only be accessed in a specific order by push-ing and pop-ing data.*<br>> *Grows from higher address to lower addresses.*<br>> *Contains local variables, arguments passed on to the program, and the return address of the parent process that called the program.*<br>[Visual Reference](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/aed105638dc28ee3524baeaba8925e12.png) |
| `Heap`  | > *Data can be stored and retrieved in any order.* <br>> *Heap is slower than the Stack.*<br>> *Memory is dynamically allocated using functions like `malloc` etc.*                                                                                                                                                                                                                                                                                                                               |
| `Data`  | > *Used to store global and static data that is not variable remains constant.*<br>> Consists of "two parts": <br>    `Data` is used to hold variables<br>    `.bss` is used to hold unassigned variables                                                                                                                                                                                                                                                                                         |
| `Text`  | > *Used to store `.text` section of PE (Portable Executable) which contains the "instructions" that are executed by the CPU.*                                                                                                                                                                                                                                                                                                                                                                     |
#### **IO/Storage Devices**

> I/O (Input/Output) and storage devices are the peripheral devices that interact with the processor through bus interfaces, which function as 'highways' to transfer data and addresses, utilizing electrical charges to represent binary data.

Each Bus has a capacity of bits (or electrical charges) it can carry simultaneously. This usually is a multiple of 4-bits, ranging up to 128-bits. 

![](https://orbixio.netlify.app/assets/img/Pasted image 20241030223707.png)
_Bus Interfaces_
---

#### **Speed**

| Component   | Speed                             | Size                |
| ----------- | --------------------------------- | ------------------- |
| `Registers` | Fastest                           | Bytes               |
| `L1 Cache`  | Fastest, other than Registers     | Kilobytes           |
| `L2 Cache`  | Very fast                         | Megabytes           |
| `L3 Cache`  | Fast, but slower than the above   | Megabytes           |
| `RAM`       | Much slower than all of the above | Gigabytes-Terabytes |
| `Storage`   | Slowest                           | Terabytes and more  |
