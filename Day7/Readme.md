# Memory Management

## Introduction to Memory Management
- The memory management in the operating system is to control or maintain the main memory and transfer processes from the primary memory to disk during execution.
- It also helps to keeps track of all memory locations, whether the process uses them or not.
- It tracks when memory is released or when it is shared and changes the status accordingly.
- These all things related to Memory management is being done by Memory Manager, like managing virtual address space, paging, etc.

## Virtual Address Space
- The virtual address space for a process is the set of virtual memory addresses that it can use. The address space for each process is private and cannot be accessed by other processes unless it is shared
- A virtual address does not represent the actual physical location of an object in memory; instead, the system maintains a page table for each process, which is an internal data structure used to translate virtual addresses into their corresponding physical addresses
- Each time a thread references an address, the system translates the virtual address to a physical address.
- Read more here https://learn.microsoft.com/en-us/windows/win32/memory/virtual-address-space

### Page
- Memory management is done in distinct chunks called pages. This is because the hardware memory management unit translates virtual to physical addresses at the granularity of a page.
- Hence, a page is the smallest unit of protection at the hardware level.
  
### Paging
- When the total memory requested by active processes exceeds the actual physical memory available, it leads to a situation known as overcommitment. Operating systems might allow this condition temporarily, anticipating that not all processes will simultaneously require their maximum allocated memory at the same time.
  Paging, in this context, helps manage overcommitted memory. When the system reaches a point of overcommitment and the physical memory becomes insufficient to hold all the data needed by active processes, the operating system adopts a technique where it selectively moves or "pages out" parts of the memory from RAM to the disk. This process is often referred to as "swapping" or "paging to disk."

## Memory Manager
- It resides in NtOSkrnl.exe
- No parts of the memmory manager exists in HAL
- The memory manager is fully reentrant and supports simultaneous execution on multiprocessor systems. That is, it allows two threads to acquire resources in such a way that they don’t corrupt each other’s data. To aquire this, memory manager implement various internal synchronizaion techniques.
- Windows API provided for Memory Mangement
  - Virtual API: It is used for memeory allocation and de-allocation. It includes VirtualAlloc, VirtualFree, VirtualProtect, VirtualLock and others.
  - Heap API: This provides functions for small allocations (typically less than a page). It uses the Virtual API internally, but adds management on top of it. It includes HeapAlloc, HeapFree, HeapCreate, HeapReAlloc and others.
  - Local/Global APIs: These are leftovers from 16-bit Windows and are now implemented using the Heap API.
  - Memory Mapped Files: A memory-mapped file contains the contents of a file in virtual memory. This mapping between a file and memory space enables an application, including multiple processes, to modify the file by reading and writing directly to the memory.Memory-mapped file functions include Create-FileMapping, OpenFileMapping, MapViewOfFile, and others.

![image](https://github.com/SecTheBit/Windows-Internals/assets/46895441/c77c0486-cfbe-4915-affe-584956560fac)

### Shared Memory and mapped Files

- Windows provides a mechanism to share memory among processes and the operating system. Shared memory can be defined as memory that is visible to more than one process or that is present in more than one process virtual address space
- For example, if two processes use the same DLL, it would make sense to load the referenced code pages for that DLL into physical memory only once and share those pages between all processes that map the DLL, as
- Each process would still maintain its private memory areas to store private data but the DLL code and unmodified data pages could be shared without harm.

## Data Execution Prevention
- Data Execution Prevention (DEP) is a technology built into Windows that helps protect you from executable code launching from places it's not supposed to. DEP does that by marking some areas of your PC's memory as being for data only, no executable code or apps will be allowed to run from those areas of memory
- This can prevent certain types of malware from exploiting bugs in the system through the execution of code placed in a data page such as the stack.
- DEP can also catch poorly written programs that don’t correctly set permissions on pages from which they intend to execute code.
- On 64-bit versions of Windows, execution protection is always applied to all 64-bit processes and device drivers and can be disabled only by setting the nx BCD option to AlwaysOff
- On 64-bit Windows, execution protection is applied to thread stacks (both user and kernel mode), user-mode pages not specifically marked as executable, the kernel paged pool, and the kernel session pool.
- On ARM systems, DEP is set to AlwaysOn.
- The application of execution protection for 32-bit processes depends on the value of the BCD nx option.
- Heap allocations made by calling the malloc and HeapAlloc functions are non-executable.
- DEP is configured at system boot according to the no-execute page protection policy setting in the boot configuration data.
- An application can get the current policy setting by calling the GetSystemDEPPolicy function. Depending on the policy setting, an application can change the DEP setting for the current process by calling the SetProcessDEPPolicy function
- Read more here https://learn.microsoft.com/en-us/windows/win32/memory/data-execution-prevention

### View DEP Status (Using Process Explorer)
- Go to any process
- Select it and click on view -> select columns -> DEP Status

![POC](https://github.com/SecTheBit/Windows-Internals/assets/46895441/71399911-c78a-4fdf-aeb0-1aaaf879bf7c)

### DEP Status Values
- DEP (permanent) This means the process has enabled DEP because it is a “necessary Windows program or service.”
- DEP This means the process opted in to DEP.
- Nothing If the column displays no information for this process, DEP is disabled.
