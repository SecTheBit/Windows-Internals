## Memory Management

### Virtual Address Space 
- There are 3 main types of data that are mapped to vistrual space:
  - Per-Process private code and data : Each process has a private address space that cannot be accessed by other processes. That is, a virtual address is always evaluated in the context of the current process and cannot refer to an address defined by any other process.
  - Session Wide Code and Data : A session consists of the processes and other system objects such as the window station, desktops, and windows that represent a single user’s logon session.Each session has a session-specific paged pool area used by the kernel-mode portion of the Windows subsystem (Win32k.sys) to allocate session-private GUI data structures.
  - System Wide Code and Data : System space contains global operating system code and data structures visible by kernel-mode code regardless of which process is currently executing
### x86 Address Space Layout
- By default, each user process on 32-bit versions of Windows has a 2 GB private address space. (The operating system takes the remaining 2 GB.)
- However, for x86, the system can be configured with the increaseuserva BCD boot option to permit user address spaces up to 3 GB
- For a process to grow beyond 2 GB of address space, the image file must have the IMAGE_FILE_LARGE_ADDRESS_AWARE flag set in the image header (in addition to the global increaseuserva setting).
- Several system images are marked as large address space aware so that they can take advantage of systems running with large process address spaces. These include the following:
  - lsass.exe
  - Inetinfo.exe
  - Chkdsk.exe
  - Smss.exe
  - Dllhst3g.exe
- For viewing if the process is using large process address space use the dumpbin tool with following command and search for string "Application can handle large (>2GB) addresses"
``` dumpbin /headers c:\windows\system32\smss.exe ```
- Memory allocations using VirtualAlloc, VirtualAllocEx, and VirtualAllocExNuma start with low virtual addresses and grow higher by default
- Therefore,for testing purposes, you can force memory allocations to start from high addresses by using the MEM_TOP_DOWN flag to the VirtualAlloc* functions or by adding a DWORD registry value named AllocationPreference to the HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management key and setting its value to 0x100000.

#### x86 System Address Space Layout
- The 32-bit versions of Windows implement a dynamic system address space layout by using a virtual address allocator
- Many kernel-mode structures use dynamic address space allocation. These structures are therefore not necessarily virtually contiguous with themselves
- Each can easily exist in several disjointed pieces in various areas of system address space.

#### x86 Session Space
- For systems with multiple sessions (which is almost always the case, as session 0 is used by system processes and services, while session 1 is used for the first logged on user), the code and data unique to each session are mapped into system address space but shared by the processes in that session

### 64-bit Address Space Layout
- The theoretical 64-bit virtual address space is 16 exabytes (EB), or 18,446,744,073,709,551,616 bytes
- The address space is divided in half, where the lower 128 TB are available as private user processes and the upper 128 TB are system space.
- System space is divided into several different-sized regions

#### x64 virtual addressing limitations
- As discussed, 64 bits of virtual address space allow for a possible maximum of 16 EB of virtual memory. Obviously, neither today’s computers nor tomorrow’s are even close to requiring support for that much memory.
- Accordingly, to simplify chip architecture and avoid unnecessary overhead—particularly in address translation (described later)—AMD’s and Intel’s current x64 processors implement only 256 TB of virtual address space.

### System virtual addres space quotas
- To address more specific quota requirementsthat system administrators might have, the memory manager collaborates with the process manager to enforce either system-wide or user-specific quotas for each process.
- You can configure the PagedPoolQuota, NonPagedPoolQuota, PagingFileQuota, and Working-SetPagesQuota values in the HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management key to specify how much memory of each type a given process can use.

### User address space layout
- Just as address space in the kernel is dynamic, the user address space is also built dynamically. The addresses of the thread stacks, process heaps, and loaded images (such as DLLs and an application’s executable) are dynamically computed (if the application and its images support it) through the ASLR mechanism.
- 
