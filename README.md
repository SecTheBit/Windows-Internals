# Windows-Internals
Learnings about windows Internals from malware development/reversing purpose. 
I will cover only those topics which are necessary in maldev . Hope it helps to Red Teamers.!!

## Day 1
- Introduction to following things
  - Windows API
  - OLE
  - COM
  - Process
  - Process Status
  - Threads
  - Threads Scheduling
 
## Day 2
- Introduction to Virtual Memory
- Kernel mode vs User mode
  - Introduction
  - What are terms ring0 , ring3, etc. signify
  - Memory regions accessible through User mode and kernel mode
  - context switching
  - Driver Signing
- Brief Introduction to Windows Registry

## Day 3
- Viewing Exported functions of a DLL file using Dependency Walker
- Kernel Debugging (Locally) using WinDbg

## Day 4
- System architecture
- How Hypervisor helps in protecting system from malicious kernel drivers

## Day 5
- CreateProcess Function Explained

## Day 6
- Process Environment Block
- Basic Info about Jobs

## Day 7
- Memory Management
  - Introuction to Memory Managment
    - Virtual Address Space
    - Page
    - Paging
  - Memory Manager
    - Memory Related Windows API
    - Shared Memory and Mapped Files
  - Data Execution Policy
    - Introduction
    - Viewing DEP Status using Process Explorer
    - DEP Status Values Description
## Day 8
- System Memory Pools
  - Paged Pool
  - Non Paged Pool
  - APIs used for allocating memory with kernel memory pool
- Heaps
  - Introduction
  - Types
  - Viewing Structure of Heap using WinDBG
## Day 9
- Virtual Address Space
  - Types of data mapped to Virtual Address Space
  - x86 Address Space Layout
    - x86 System Address Space Layout
    - x86 Session Space
  - System Virtual Address Space Quotas
  - User Address Space layout
    - Analyzing user virtual address space using VMMap
