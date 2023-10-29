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

#### Hypervisor
- All modern solutions employ the use of a hypervisor, which is a specialized and highly privileged component that allows for the virtualization and isolation of all resources on the machine, from virtual to physical memory, to device interrupts, and even to PCI and USB devices
- Hypervisor has more access to OS than kernel itself
- It can protect and monitor a single host instance to offer assurances and guarantees beyond what the kernel provides
- In Windows 10, Microsoft now leverages the Hyper-V hypervisor to
- provide a new set of services known as virtualization-based security (VBS):
  - Device Guard
  - Hyper Guard
  - Credential Guard
  - Application Guard
- The key advantage of all these technologies is that unlike previous kernel-based security improvements, they are not vulnerable to malicious or badly written drivers, regardless of whether 
   they are signed or not
- This makes them highly resilient against today’s advanced adversaries. This is possible due to the hypervisor’s implementation of Virtual Trust Levels (VTLs).
- Because the normal operating system and its components are in a less privileged mode (VTL 0), but these VBS technologies run at VTL 1 (a higher privilege), they cannot be affected even by 
  kernel mode code, even if there is some malicious code running in the kernel.
  ![image](https://github.com/SecTheBit/Windows-Internals/assets/46895441/4cf7b4a5-cf23-4d58-8f5a-a08295cc32fa)

- the regular user versus kernel rules apply, but are now augmented by VTL considerations.In other words, kernel-mode code running at VTL 0 cannot touch user mode running at VTL 1 becauseVTL 
  1 is more privileged. Yet, user-mode code running at VTL 1 cannot touch kernel mode running at VTL 0 either because user (ring 3) cannot touch kernel (ring 0)

#### Environment subsytems and subsystems DLLs
- The role of an environment subsystem is to expose some subset of the base Windows executive system services to application programs. Each subsystem can provide access to different subsets of the native services in Windows.
- Each executable image (.exe) is bound to one and only one subsystem
  
