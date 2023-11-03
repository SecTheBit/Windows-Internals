# Memory Management

## Kernel-mode heaps (system memory pools)
- At system initialization, the memory manager creates two dynamically sized memory pools, or heaps, that most kernel-mode components use to allocate system memory:
  - Paged Pool: This is a region of virtual memory in system space that can be paged into and out of the system  
  - Non Paged Pool: Unlike the paged pool, the non-paged pool is memory that must stay in physical RAM at all times. It's reserved for critical system objects that the operating system or device drivers need for various essential functions
- Both memory pools are in the system part of the address space and are mapped in the virtual address space of every process
- The executive provides routines to allocate and deallocate from these pools. For information on these routines, see the functions that start with *ExAllocatePool*, *ExAllocatePoolWithTag*, and *ExFreePool* in the Windows Development Kit (WDK) documentation

## Heap
- Heaps are memory areas allocated to each program. Memory allocated to heaps can be dynamically allocated, unlike memory allocated to stacks. 
### Heap Manager
- User program calls heap manager to allocate a block of any desired size to store some dynamic data.
- Heap manager returns a pointer to a block. The program uses that block for its purpose. The block’s memory is reserved exclusively for that use.
- The heap manager exists in two places: Ntdll.dll and Ntoskrnl.exe
- The most common Windows heap functions are:
  - HeapCreate or HeapDestroy: These create or delete, respectively, a heap. The initial reserved and committed size can be specified at creation
  - HeapAlloc: This allocates a heap block. It is forwarded to RtlAllocateHeap in Ntdll.dll.
  - HeapFree: This frees a block previously allocated with HeapAlloc
  - HeapReAlloc: This changes the size of an existing allocation, growing or shrinking an existing block. It is forwarded to RtlReAllocateHeap in Ntdll.dll.
  - HeapLock and HeapUnlock: These control mutual exclusion to heap operations
  - HeapWalk: This enumerates the entries and regions in a heap.
 
### Types of Heap
- NT Heap
- Segemnt Heap

### View Heap Structure using WinDbg
Attach calculator process to WinDbg, use the command ```!heap```
![POC](https://github.com/SecTheBit/Windows-Internals/assets/46895441/0a0dba2b-f718-4029-8956-b54afc97c8b9)

View Structure of NT Heap
![POC](https://github.com/SecTheBit/Windows-Internals/assets/46895441/f6cdb7c2-5ded-4df8-b7f9-e13914bf3132)


