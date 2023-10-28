## System Architecutre

### Architecute Overview

![image](https://github.com/SecTheBit/Windows-Internals/assets/46895441/91e51cce-858c-49e3-aa37-d4c09d6656ab)

W will first try to get a very high overview of the above architecture, starting with the four type of user mode process, given in the above diagram

- User Processs: These can be of following types, windows 32 bit and 64 bit , Windows 3.1 16-bit, MS-DOS 16-bit, or POSIX 32-bit or 64-bit. Note that 16-bitapplications can be run only on 32-bit Windows, and that POSIX applications are no longer supported as of Windows 8.
- Service Process : These are the processes that host windows services such as Task Scheduler, Print spooler, etc. services. Services generally have the requirement that they run independently of user logons.
- System Process: Process such as logon and session manager that are not started by service control manager
- Environment Subsytem server process : We will see about this in coming days

The kernel-mode components consist of following things:

- Executive: It helps in managing base OS service like memory management,process and thead management, networking, security,I/O  and inter process communication
- The Windows kernel: This consists of low-level OS functions, such as thread scheduling, interrupt and exception dispatching, and multiprocessor synchronization.
- Device Drivers: It includes both hardware and non-hardware drivers.
- Hardware Abstraction Layer: This is a layer of code that isolates the kernel, the device drivers, and the rest of the Windows executive from platform-specific hardware differences
- Hypervisor layer: Hypervisor itself.
